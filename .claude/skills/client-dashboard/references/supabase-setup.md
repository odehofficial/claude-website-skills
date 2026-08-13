# Supabase Setup

*Last reviewed: August 2026.*

**One numbered action at a time.** Wait for confirmation before the next.

**If the Supabase connector is available**, you can create the project and run the SQL directly instead of walking the user through the dashboard. Still show them what you did and where to find it — a student who has never seen the dashboard cannot support the client later.

---

# Step 11 — Set up your database

**Explain first, in one sentence:** a database is where the appointments get stored, so the business owner can log in and see them. Until now the site had nothing to remember.

## 11a. Create the account

1. Open **https://supabase.com**
2. Click **Start your project** (green button, top right).
3. Click **Continue with GitHub** — reuses the account from Step 2.
4. Click **Authorize supabase**.

> **Check it worked:** you can see the Supabase dashboard.

## 11b. Create the project

1. Click **New project**.
2. If it asks for an organisation, pick the one with your name.
3. **Name:** the business name, e.g. `smile-dental`.
4. **Database Password:** click **Generate a password**, then **copy it into your password manager immediately**. It is shown once. You rarely need it, but recovering without it is painful.
5. **Region:** pick the one closest to where the customers are. A clinic in Dubai should not have its database in Virginia — every page load pays that distance.
6. Leave the plan as **Free**.
7. Click **Create new project**.
8. Wait one to two minutes while it sets up.

> **Check it worked:** the project page opens and stops saying "setting up".

## 11c. Copy the three keys

1. In the left sidebar, click the **gear icon** (Project Settings), at the bottom.
2. Click **API Keys**.
3. You need three values. Copy each into `.env.local` in the project folder as you go:

```
NEXT_PUBLIC_SUPABASE_URL=https://xxxxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJ...
SUPABASE_SERVICE_ROLE_KEY=eyJ...
```

4. **The service role key is a master key.** It ignores every security rule. It must never appear in browser code, never be pasted into a chat or email, and never be committed. Confirm `.env.local` is in `.gitignore` before continuing.

> **Check it worked:** all three values are in `.env.local`, and `.gitignore` contains `.env.local`.

## 11d. Create the tables

1. In the left sidebar, click **SQL Editor**.
2. Click **New query**.
3. Paste the SQL below and click **Run**.

```sql
-- What the business offers
create table public.services (
  id               uuid primary key default gen_random_uuid(),
  name             text not null,
  duration_minutes int  not null default 30,
  price_cents      int,
  is_active        boolean not null default true,
  sort_order       int  not null default 0
);

-- Appointments
create table public.bookings (
  id             uuid primary key default gen_random_uuid(),
  service_id     uuid references public.services(id),
  customer_name  text not null,
  customer_phone text not null,
  customer_email text,
  starts_at      timestamptz not null,
  status         text not null default 'confirmed'
                 check (status in ('confirmed','cancelled','completed','no_show')),
  notes          text,
  created_at     timestamptz not null default now()
);

-- Contact form messages, kept in one place
create table public.enquiries (
  id         uuid primary key default gen_random_uuid(),
  name       text not null,
  phone      text,
  email      text,
  message    text,
  created_at timestamptz not null default now(),
  read_at    timestamptz
);

-- Two people cannot take the same slot.
-- Cancelled bookings free the slot again.
create unique index bookings_unique_slot
  on public.bookings (starts_at)
  where status <> 'cancelled';

create index bookings_starts_at_idx on public.bookings (starts_at);
```

> **Check it worked:** click **Table Editor** in the sidebar. You see `services`, `bookings`, and `enquiries`.

## 11e. Turn on the security rules

**Explain why before running it.** Right now those tables are wide open. Supabase talks to the browser directly, so without rules, anyone who opens the site could read every customer's name and phone number. This step closes that.

1. Back in **SQL Editor**, **New query**.
2. Paste and **Run**:

```sql
-- Lock every table by default
alter table public.services  enable row level security;
alter table public.bookings  enable row level security;
alter table public.enquiries enable row level security;

-- Visitors may see the service list. That is all they may see.
create policy "anyone can read active services"
  on public.services for select
  to anon, authenticated
  using (is_active = true);

-- Signed-in staff may read and manage everything
create policy "staff read bookings"
  on public.bookings for select to authenticated using (true);

create policy "staff update bookings"
  on public.bookings for update to authenticated using (true);

create policy "staff read enquiries"
  on public.enquiries for select to authenticated using (true);

create policy "staff update enquiries"
  on public.enquiries for update to authenticated using (true);

create policy "staff manage services"
  on public.services for all to authenticated using (true) with check (true);
```

**Notice what is deliberately absent:** there is no policy letting visitors read `bookings` or `enquiries`, and none letting them insert. With row level security on and no matching policy, the answer is always no. Bookings are created by the site's own server code, which uses the service role key and bypasses these rules — which is exactly why that key must never reach the browser.

> **Check it worked:** in **Table Editor**, each table shows an **RLS enabled** label.

## 11f. Create the owner's login

1. In the sidebar, click **Authentication**.
2. Click **Users**, then **Add user** → **Create new user**.
3. Enter the business owner's email and a strong password.
4. Tick **Auto Confirm User** so they can sign in immediately.
5. Click **Create user**.
6. Give the password to the owner through a password manager, never by email or WhatsApp, and tell them to change it on first login.

> **Check it worked:** the owner's email appears in the Users list.

---

# Step 14 — Prove the data is private

**Do not skip this, and do not accept "it looks fine".** This is the difference between a professional build and a data leak. A student who cannot demonstrate this should not launch.

**Explain the test in one sentence:** we are going to pretend to be a stranger and try to read the customer list. It should come back empty.

1. Add a temporary page to the site at `/leak-test` containing:

```tsx
'use client'
import { createClient } from '@supabase/supabase-js'

// The public key — exactly what any visitor's browser can see.
const supabase = createClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!,
)

export default function LeakTest() {
  const check = async () => {
    const { data, error } = await supabase.from('bookings').select('*')
    alert(
      `Rows a stranger can read: ${data?.length ?? 0}\n` +
      `Error: ${error?.message ?? 'none'}`,
    )
  }
  return <button onClick={check}>Run leak test</button>
}
```

2. Make sure at least one real-looking booking exists in the table.
3. Open `/leak-test` in the browser and click the button.

> **This must say `Rows a stranger can read: 0`.**
>
> **If it shows any other number, stop.** Customer data is exposed. Row level security is off, or a policy is granting `select` to `anon`. Fix it and run the test again before doing anything else.

4. Once it passes, **delete the `/leak-test` page** and confirm it is gone.

**If the Supabase connector is available**, also run the security advisors and show the user the result — they catch misconfigurations this manual test does not.

> **Ask them:** "Did it say zero rows? (yes / no)"

---

# Adding the keys to Vercel

The site will not work live until Vercel has the keys too.

1. Open **https://vercel.com/dashboard**, click the project.
2. Click **Settings**, then **Environment Variables**.
3. Add all four, clicking **Save** after each:
   - `NEXT_PUBLIC_SUPABASE_URL`
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - `SUPABASE_SERVICE_ROLE_KEY`
   - (the Resend variables should already be there from Step 10)
4. Click **Deployments**, find the newest, click the **⋯** menu, then **Redeploy**.

**Same trap as Step 10:** settings do nothing until the site is rebuilt. If bookings work locally but not live, this is why.

> **Check it worked:** make a test booking on the live site and see it appear in the Supabase Table Editor.
