# House Answer Format

**This is how every instruction is written. Not a suggestion — the format.**

The user is a beginner who has never used these dashboards. They should never have to search a screen, guess which button, or wonder whether it worked.

---

## The shape

```
**1. Short task title**

Click: https://exact.deep/link/to/the/screen

1. First single action
2. Second single action
3. Green button "Exact Button Text"

You should see: the literal thing that appears when it worked.
```

Then the next numbered task. Nothing between them.

---

## The nine rules

### 1. Deep links, never homepages

Land them on the exact screen. Build the URL from IDs you already know.

- **Bad:** "Go to Supabase and open the SQL editor"
- **Good:** `Click: https://supabase.com/dashboard/project/abcd1234/sql/new`

**Record every ID in `PROGRESS.md` as soon as you learn it** — GitHub username and repo name, Vercel project, Supabase project ref, the domain. Every later link is built from them. Common patterns:

| Screen | URL |
|---|---|
| Supabase SQL editor | `https://supabase.com/dashboard/project/<ref>/sql/new` |
| Supabase tables | `https://supabase.com/dashboard/project/<ref>/editor` |
| Supabase logins | `https://supabase.com/dashboard/project/<ref>/auth/users` |
| Supabase extensions | `https://supabase.com/dashboard/project/<ref>/database/extensions` |
| GitHub repo | `https://github.com/<user>/<repo>` |
| GitHub build status | `https://github.com/<user>/<repo>/actions` |
| Vercel project list | `https://vercel.com/dashboard` |
| Vercel new project | `https://vercel.com/new` |
| Resend domains | `https://resend.com/domains` |
| Resend keys | `https://resend.com/api-keys` |
| Cal.com hours | `https://app.cal.com/availability` |

If you do not know the ID, ask for it once, write it to `PROGRESS.md`, and use deep links from then on. If you are unsure a deep path is still correct, give the dashboard link **plus** the click path — never a bare homepage.

### 2. Name the button exactly, with its colour

Write it as the user sees it, in quotes.

- **Bad:** "confirm the merge"
- **Good:** `Green button "Confirm merge"`

Colour first, then the exact label. If it is not a button, say what it is: `the "Actions" tab at the top of the repo`.

### 3. Describe icons physically

An icon has no name to search for. Give its shape, its position, and its tooltip.

> Click the copy icon (two overlapping squares — tooltip says "Copy raw file"), top-right corner of the grey file box.

### 4. Both keyboard shortcuts, every time

> Press **Ctrl+A** (Windows) or **Cmd+A** (Mac)

Never assume the operating system.

### 5. Exact text to type, in code format

Never paraphrase something they must type.

> Type: `select public.purge_expired(180);`

### 6. "You should see:" ends every task

State the literal result — the actual number, the actual words, the actual colour.

- **Bad:** "check that it worked"
- **Good:** `You should see: 0`
- **Good:** `You should see: a row saying purge-expired-applications | 20 3 1 * * | true`
- **Good:** `You should see: green text — "On — this account asks for a code at sign-in."`

If there is nothing visible to check, the task is written wrong. Find something.

### 7. Error branches inline, with their own links

Put the likely error where it will happen, not in a troubleshooting section at the end.

```
If you see a red error mentioning `pg_cron`:

- Go to https://supabase.com/dashboard/project/<ref>/database/extensions
- Type `pg_cron` in the search box
- Click the toggle next to it → "Enable extension"
- Go back to the SQL editor and click "Run" again

If no error: you'll see a result row. Move on.
```

Always give the "no error" path too, so a user who sailed through knows to continue.

### 8. Say how long waiting takes

> Wait for the top row to show a green tick. Usually 1–2 minutes.

Without this, a beginner assumes a slow step is a broken step and starts clicking things.

### 9. One action per numbered line

"Sign in and open settings" is two lines. Never bundle.

---

## One step at a time — full detail for the current step only

Give the complete detail for **the step they are on right now**. Everything after it is a **headline with no detail**, so they can see what is coming without drowning in it.

```
**Step 7 — Save your work to GitHub**

Click: https://github.com/odehofficial/smile-dental

1. Open GitHub Desktop
2. Blue button "Publish repository", top of the window
3. Leave "Keep this code private" ticked

You should see: your project name in the list at github.com

---
Coming next: 8. Put it on the internet · 9. Connect your domain · 10. Make the contact form work
```

Then **stop**. Do not begin the next step until this one is confirmed.

### Keep every step to one or two minutes of work

If a step takes longer than that, split it. A ten-minute step has too many places to go wrong, and when it fails neither of you can tell which part broke. Creating an account is one step. Copying the keys out of it is another.

---

## Check they actually did it — do not take silence as success

People skip steps. They also move on without saying whether the last one worked.

**If they jump ahead without confirming, go back and check the previous step yourself before continuing.** Do not carry on and hope.

**Verify with tools first, questions second.** You can often check without asking:

| To confirm | Check |
|---|---|
| Files created, keys added | Read the file |
| Work saved or uploaded | `git status`, `git log`, or the repo page |
| Site is live | Fetch the URL |
| Database, tables, security rules | The Supabase connector, if enabled |
| Deployment succeeded | The Vercel connector, or the deployments page |

Only ask when no tool can tell you — anything that lives behind their login, or that only they can see on screen.

**Then update the chart honestly.** Mark a step `Done` only when it is verified. If you could not confirm it, mark it `Not confirmed` and say so — a chart claiming things are finished when they are not is worse than no chart.

---

## Offer a connector when it removes real work

If a task means a lot of clicking through a dashboard, and a connector could do it directly, **offer it before starting the manual route**:

> This next part is about fifteen clicks in the Supabase dashboard. If you turn on the Supabase connector, I can create the tables for you and check the security settings myself — about two minutes instead of fifteen. Want to do that first?

Good candidates: **Supabase** (create projects, run SQL, check security advisors), **Vercel** (deployments, environment variables, build logs), **GitHub** (repositories, settings).

Then show them how to switch it on, in the house format. Connectors live in Claude's settings under **Connectors** — confirm the exact menu location in the version they are running rather than guessing, and if you are unsure, say "look for Connectors in Settings" instead of inventing a click path.

**Always offer the manual route as well.** Some people cannot or will not enable a connector, and the course must still work for them.

---

## Ask for a screenshot or a recording

You cannot see their screen. Ask when it would settle something faster than a paragraph of questions:

**Ask for a screenshot when:**
- something is not working and their description is unclear
- an error appeared and you need the exact wording
- a screen does not match what this guide describes
- they say a design "looks wrong" — you need to see what they see

> Take a screenshot of that whole screen and paste it here. That will be quicker than describing it.

**Ask for a screen recording when:**
- they want to copy the look or feel of another website — a recording captures the animations, hover effects, and scrolling that a still image misses
- a problem only appears while doing something (a form that fails halfway, a menu that flickers)

> If you have seen a site whose look you want, record your screen for ten or twenty seconds scrolling through it. I will see the animations and spacing, not just the colours.

---

## Never

- **Never** send a raw error log and ask them to interpret it. Translate it, then give the one fix.
- **Never** write "just", "simply", or "obviously".
- **Never** say "navigate to" — say "Click:" and give the link.
- **Never** describe a button by what it does instead of what it says.
- **Never** claim a step is done. They confirm it, or you verify it with a tool.
- **Never** show the detail of a step they are not on yet.
