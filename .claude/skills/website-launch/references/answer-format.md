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

## When to batch, and when to stop

**Batch** a numbered list of tasks when the sequence is fixed and each task has its own `You should see:`. The sample above is six tasks in one message and it works, because every task is independently checkable.

**Stop and wait** when:

- their answer changes what comes next ("is it Public or Private?")
- the step is irreversible — deleting, publishing, paying, going live
- something failed and you are diagnosing
- they have told you they are stuck or confused

**Ask them to report back at the checkpoints.** Batching the instructions does not mean skipping verification — end a batch with which "You should see" results you need confirmed.

---

## Never

- **Never** send a raw error log and ask them to interpret it. Translate it, then give the one fix.
- **Never** write "just", "simply", or "obviously".
- **Never** say "navigate to" — say "Click:" and give the link.
- **Never** describe a button by what it does instead of what it says.
- **Never** claim a step is done. They confirm it.
