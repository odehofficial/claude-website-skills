# Security Check — Run Before Every Handover

**The client's customers are trusting this site with their name, phone number, and sometimes why they need a doctor. Protecting that is part of the job, not an extra.**

Run this on **every** site before handover — brochure sites included. A contact form alone is enough to leak personal data.

**Most of this you run yourself.** Do not hand a beginner a checklist and ask them to interpret it. Run the automated checks, report what you found in plain language, fix what you can, and only involve the user for the things that need their login.

---

# Part 1 — Checks you run yourself

Work through all of these before telling the user anything. Then report findings together.

## 1.1 Secrets that escaped into the code

The single most damaging failure. A leaked key lets anyone read the client's entire customer list.

```bash
git grep -nE "(sk-|re_[A-Za-z0-9]{10,}|eyJhbGciOi|SERVICE_ROLE|PRIVATE_KEY|_SECRET *=)" -- . ":(exclude).env*"
```

> **Expected: no output.** Any hit is a real key sitting in tracked source.

**Was `.env.local` ever committed?**

```bash
git log --all --oneline -- .env.local .env
```

> **Expected: no output.** If there is any output, the key is in git history **and deleting the file does not remove it**. The key must be treated as compromised and rotated — see 3.1.

**Is `.gitignore` actually protecting it?**

```bash
git check-ignore -v .env.local
```

> **Expected:** a line naming the `.gitignore` rule. No output means the file is *not* ignored.

## 1.2 Server-only keys reaching the browser

Anything in a file with `"use client"`, or any variable **not** prefixed `NEXT_PUBLIC_`, must never appear in browser code.

```bash
git grep -l "use client" | xargs grep -lE "SERVICE_ROLE|RESEND_API_KEY" 2>/dev/null
```

> **Expected: no output.** A hit means a master key is being shipped to every visitor.

**Then check the built output, which is what actually ships:**

```bash
npm run build
grep -rlE "re_[A-Za-z0-9]{10,}|service_role" .next/static 2>/dev/null
```

> **Expected: no output.** This catches leaks the source scan misses.

**Understand the distinction and explain it to the user:** `NEXT_PUBLIC_SUPABASE_ANON_KEY` is *designed* to be public and is safe in the browser — it is restricted by Row Level Security. `SUPABASE_SERVICE_ROLE_KEY` ignores every security rule and is catastrophic if exposed.

## 1.3 Personal data written to logs

Vercel keeps runtime logs. A form handler that logs the request body puts customer names and phone numbers into them.

```bash
git grep -nE "console\.(log|error|warn)\(.*(body|data|email|phone|name|input)" -- app/ src/
```

Review each hit. Logging that an error *occurred* is fine; logging **what the customer typed** is not.

```ts
// Bad — customer's details land in the log
console.error('Contact form failed:', err, data)

// Fine — no personal data
console.error('Contact form failed:', err instanceof Error ? err.message : 'unknown')
```

## 1.4 Server-side validation on every route that writes data

Client-side validation is a convenience, not a control — anyone can post directly to the endpoint. Read every file under `app/api/` and confirm each one:

- Validates required fields **on the server**
- Caps the length of every string it accepts (an unbounded text field is a denial-of-service and a storage-cost problem)
- Never interpolates user input into a database query as raw SQL
- Returns a generic error message to the browser and keeps details server-side

```ts
if (typeof name !== 'string' || name.length > 100) {
  return NextResponse.json({ error: 'Invalid name.' }, { status: 400 })
}
```

## 1.5 Security headers

```bash
curl -sI https://THEIR-DOMAIN.com | grep -iE "strict-transport|x-content-type|x-frame|referrer-policy|content-security"
```

> **Expected:** at minimum `strict-transport-security`, `x-content-type-options`, `x-frame-options`, and `referrer-policy`. Missing ones are fixed in 3.2.

## 1.6 Known vulnerabilities in dependencies

```bash
npm audit --omit=dev
```

Report **high** and **critical** only — a beginner shown 40 low-severity dev-dependency warnings will either panic or learn to ignore all of it. `npm audit fix` handles most; anything requiring a major version bump needs testing before it ships.

## 1.7 Third-party scripts

```bash
git grep -nE "<script[^>]+src=|googletagmanager|hotjar|facebook\.net|<iframe"
```

Every third-party script can read the page, including anything typed into a form. Flag any the client did not explicitly ask for. Analytics that sets no cookies (Vercel Analytics) is the safer default.

## 1.8 Database rules — Tier 2 only

If the site uses Supabase, **re-run the leak test** from `client-dashboard/references/supabase-setup.md`. It must return `Rows a stranger can read: 0`.

If the Supabase connector is enabled, also run the security advisors and report what they flag. They catch misconfigurations the manual test does not.

## 1.9 Repository visibility

Confirm the repo is **private**. A public repo for a client site exposes the whole codebase and its full history to anyone.

---

# Part 2 — Things only the user can check

Now bring the user in. One at a time, in the house format.

## 2.1 Two-factor authentication — the highest-value item here

A stolen password on any one of these accounts hands over the whole site and its data. Two-factor authentication stops that outright, and it is the single most effective thing on this page.

Walk them through turning it on for **GitHub, Vercel, Supabase, and Resend**, one at a time. Each lives under the account's own security settings, and each will show a QR code to scan with an authenticator app on their phone.

> **Check it worked:** sign out and back in. It asks for a code from your phone.

## 2.2 Who else can get in

Ask directly: has anyone else been given the password, and is anyone else added as a collaborator on the repo or the Vercel project? Old contractors and former staff are a common way data walks out. Remove anyone who no longer needs access.

## 2.3 Where the customer data actually lives

Have them name it out loud, because they will be asked one day and should know:

- **Enquiries** → the client's email inbox (and the database, on Tier 2)
- **Bookings** → Cal.com, or the client's own database
- **Nothing else is stored** unless something else was built

## 2.4 Who can read the inbox

Form submissions land in an email account. If that inbox is shared by five staff on one password, the data is only as protected as that password. Recommend a dedicated address with its own strong password and 2FA.

---

# Part 3 — Fixes

## 3.1 A key was exposed — rotate it, don't just delete it

**Deleting a key from a file does not un-leak it.** If a key was ever committed, pushed, or pasted somewhere shared, it must be replaced.

1. Create a new key in the service's dashboard.
2. Update `.env.local` locally.
3. Update the variable in the Vercel project settings.
4. **Redeploy** — the change does nothing until the site rebuilds.
5. Delete the old key in the service's dashboard so it stops working.
6. Confirm the site still functions.

Do all five. Creating the new key without deleting the old one leaves the leak wide open.

## 3.2 Add the security headers

`next.config.js`:

```js
const securityHeaders = [
  { key: 'Strict-Transport-Security', value: 'max-age=63072000; includeSubDomains' },
  { key: 'X-Content-Type-Options', value: 'nosniff' },
  { key: 'X-Frame-Options', value: 'SAMEORIGIN' },
  { key: 'Referrer-Policy', value: 'strict-origin-when-cross-origin' },
  { key: 'Permissions-Policy', value: 'camera=(), microphone=(), geolocation=()' },
]

module.exports = {
  async headers() {
    return [{ source: '/:path*', headers: securityHeaders }]
  },
}
```

Deploy, then re-run the check in 1.5.

**On Content-Security-Policy:** it is the strongest header here and also the one most likely to break a working site — a wrong policy blanks the page. Add it only if you can test every page afterwards, and never as a last-minute change on handover day.

## 3.3 Collect less data — the cheapest security there is

**Data you never collected cannot leak.** This is more effective than any header, and it costs nothing.

Go through every form field and ask what breaks if it is removed:

- A booking needs a name, a phone number, and a service. It does not need a date of birth.
- A clinic enquiry needs to know *which service*. It does not need a free-text box where someone will type their medical history.
- Nothing needs a national ID, an insurance number, or a payment detail. **If a form is collecting any of those, remove the field** and have the client take it in person.

Replacing a free-text "describe your problem" box with a dropdown of services removes an entire category of sensitive data from the system.

## 3.4 Do not keep data forever

Enquiries and past bookings pile up indefinitely by default. Agree a retention period with the client — a year is reasonable for most businesses — and delete what is older. Less stored history means less to lose.

## 3.5 Stop bots hammering the form

Every public form gets found by bots. The honeypot field in the standard build stops the crude ones. If real spam appears, add Cloudflare Turnstile, and cap the length of every field so a single request cannot be enormous.

## 3.6 The privacy notice

Any form collecting personal details needs a visible, plain-language notice saying what is collected, why, and who sees it. This is a legal requirement in most jurisdictions and takes two sentences.

---

# Part 4 — The handover conversation

Do not just hand over a passing checklist. Tell the client, in plain language:

1. **What is collected, and where it lives.**
2. **Who can access it**, and that this list should be reviewed when staff leave.
3. **That 2FA is on**, and must stay on.
4. **How long data is kept**, and who deletes it.
5. **What to do if something looks wrong** — who to contact, and how fast.

**Rotate every key the builder ever saw.** The student has had the client's API keys on their screen. At handover, rotate them so the live site runs on credentials only the client has held. This is normal professional practice, not an accusation — say so, and do it in front of them.

---

# Report format

Report findings grouped by severity, in plain language, with the fix beside each. Never paste raw tool output at the user.

```
**Security check — smiledental.com**

CRITICAL — fix before handover
  • None found.

IMPORTANT — should fix now
  • No security headers. Fix: 2 minutes, no risk. (3.2)
  • 2FA is off on Vercel. Fix: 5 minutes. (2.1)

WORTH DOING
  • The enquiry form has a free-text box where people describe
    symptoms. Replacing it with a service dropdown removes the
    most sensitive data on the site. (3.3)

CHECKED AND CLEAN
  • No keys in the code or in git history
  • No customer data written to logs
  • Repository is private
  • Every form validates on the server
```

**If anything is CRITICAL, say plainly that the site should not be handed over until it is fixed**, and fix it with them. Do not soften it — this is the one place where being agreeable is the wrong call.
