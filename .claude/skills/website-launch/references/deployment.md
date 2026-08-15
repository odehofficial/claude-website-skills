# Go-Live Walkthrough

*Last reviewed: August 2026.*

**How to use this file.** Give the user **one numbered action at a time**, then wait. Do not paste a whole step at once — a wall of instructions is exactly what makes a beginner freeze. Every step ends with a visible check; do not advance until they confirm it.

**On button names.** These sites redesign their dashboards. If the user says a button is not where this file claims, do not argue and do not send them back to the start. Ask what they *do* see, and work from that. The fallback lines exist for this — use them.

**Never assume a step is done.** They confirm it, or you verify it with a tool. If they move on without saying, go back and check before continuing.

**Show the current step in full, and everything after it as headlines only.** Keep each step to one or two minutes of work.

**The step numbers below are for you, not for the user.** They have seen one picture with six columns — *Install + skills · Free accounts · Build the site · Put it online · Bookings · Finish & hand over* — and nothing else. Never say "Step 8", "Module 7", or "lesson 3" to them. Say the column name and the plain task: *"You're on **Put it online** — this bit takes about two minutes."*

---

# Step 1 — Install your tools

**What this does:** puts the three programs on their computer that everything else needs.

### 1a. Node.js — the engine that builds websites

1. Open **https://nodejs.org**
2. You will see two big green download buttons. Click the **left one**, labelled **LTS** (it also says "Recommended For Most Users").
3. A file downloads. Open it from your Downloads folder.
4. An installer window opens. Click **Next** through every screen, accept the licence when asked, and click **Install** at the end.
5. If Windows asks "Do you want to allow this app to make changes?", click **Yes**.
6. Click **Finish**.

> **Check it worked:** In Claude, ask "check my node version". It should print something like `v22.x.x`.
> **If it says "not recognized":** close Claude completely and reopen it. New programs are only visible to programs started afterwards. This fixes it almost every time.

### 1b. Python — needed for the design engine

1. Open **https://www.python.org/downloads/**
2. Click the big yellow button at the top: **Download Python 3.x.x**
3. Open the downloaded file.
4. **Important — before clicking anything else, tick the box at the bottom that says "Add python.exe to PATH".** It is easy to miss and skipping it causes an error later.
5. Click **Install Now**.
6. Click **Close** when it finishes.

> **Check it worked:** ask Claude "check my python version". It should print `Python 3.x.x`.
> **If Windows says "Python was not found" and opens the Microsoft Store:** that is a Windows placeholder, not real Python. Close the Store. Either reinstall with the PATH box ticked, or turn the placeholder off: open **Settings → Apps → Advanced app settings → App execution aliases**, and switch **off** both entries named `python.exe` and `python3.exe`.

### 1c. GitHub Desktop — saves and publishes your work

1. Open **https://desktop.github.com**
2. Click **Download for Windows** (or macOS).
3. Open the downloaded file. It installs on its own and opens when finished.
4. Leave it open — the account comes next.

> **Check it worked:** GitHub Desktop is open and showing a welcome screen.

---

# Step 2 — Create your accounts

**Assume they have none of these.** Not a GitHub account, not a Vercel account, nothing. Walk them through creating each one from zero — do not say "sign in to GitHub" to someone who has never had a GitHub account.

Four free accounts, then the connectors. Do them in this order — the later ones connect to the earlier ones.

### 2a. GitHub — where your website files are stored safely

1. Open **https://github.com/signup**
2. Enter your email, click **Continue**.
3. Create a password, click **Continue**. Save it in your password manager now.
4. Choose a username. This appears in your web address, so keep it professional — your name or business name.
5. Answer the email preference question, click **Continue**.
6. Solve the puzzle it shows you to prove you are human.
7. Click **Create account**.
8. Check your email for a code, type it in.
9. It may ask a few questions about how you plan to use GitHub. Answer anything, or look for **Skip** — it changes nothing.

> **Check it worked:** you can see **https://github.com** while signed in, with your profile picture at the top right.

### 2b. Connect GitHub Desktop to that account

1. Go back to **GitHub Desktop**.
2. Click **Sign in to GitHub.com**.
3. Your browser opens. Click **Authorize desktop**.
4. The browser asks to reopen GitHub Desktop. Allow it.
5. It asks for a name and email for your saved work. Use your real name and the email you signed up with. Click **Finish**.

> **Check it worked:** GitHub Desktop no longer shows a sign-in button, and your username appears when you open the **File → Options → Accounts** menu.

### 2c. Vercel — puts your website on the internet

1. Open **https://vercel.com/signup**
2. Choose **Hobby** if it asks which plan — this is the free one.
3. Enter your name when prompted.
4. **Click "Continue with GitHub".** This matters — signing up any other way means extra work connecting them later.
5. A GitHub window opens asking for permission. Click **Authorize Vercel**.

> **Check it worked:** you land on the Vercel dashboard, which will say something like "Let's build something new" because you have no projects yet.

### 2d. Resend — sends the contact form emails

1. Open **https://resend.com/signup**
2. Sign up with email, or click **Continue with GitHub** to reuse the account you just made.
3. Confirm your email address if it sends you a link.

> **Check it worked:** you can see the Resend dashboard with a menu down the left side.

### 2e. Cal.com — handles appointment booking

*Skip this if the business will take bookings by phone or WhatsApp only.*

1. Open **https://cal.com/signup**
2. Sign up with email or GitHub.
3. It asks you to pick a username — this becomes the booking link, e.g. `cal.com/smile-dental`. Use the business name.
4. It asks for availability and connected calendars. You can click through these for now; the real settings come in Step 11.

> **Check it worked:** you reach the Cal.com dashboard.

### 2f. Turn on the connectors — optional, but saves a lot of clicking

**What this does:** lets Claude work with Vercel, GitHub and Supabase directly, instead of telling you where to click. A fifteen-click job in a dashboard becomes about two minutes.

**Explain the trade-off honestly:** everything in this guide works without connectors. They make it faster, not possible. If someone would rather not connect their accounts, do not push — give them the manual route.

1. In Claude, open **Settings**.
2. Look for **Connectors** in the menu.
3. Find the connector you want. Start with **Vercel**.
4. Click **Connect**.
5. A browser window opens asking for permission. Sign in and click **Authorize**.
6. Back in Claude, it now shows as **Connected**.
7. Repeat for **Supabase**, but only if a client dashboard is planned.

> **Check it worked:** ask Claude *"list my Vercel projects"*. It answers with your actual projects instead of telling you to open a website.
>
> **If your Settings screen does not look like this:** take a screenshot of it and paste it into the chat. Claude's menus move between versions and app types, and Claude will find the right place with you rather than guessing.

**Once a connector is on, use it.** Do not walk someone through fifteen dashboard clicks when you can do the job yourself — but always tell them what you did and where to find it, because they will need to support the client later without you.

---

# Steps 3 to 6 — Build the website

These are handled in conversation, not on any website. Follow the workflow in `SKILL.md`:

- **Step 3** — answer questions about the business
- **Step 4** — approve the colours, fonts, and style
- **Step 5** — the site gets built
- **Step 6** — preview it on their own computer

> **Check it worked:** they open the local address in their browser and see the website.
> **If the page will not load:** confirm the preview is actually running, and that they typed the full address including the port number.

---

# Step 7 — Save it to GitHub

**What this does:** stores a safe copy online. Nothing is public yet, and nobody can see it.

### First, a safety check

Before anything is saved, confirm the project has a `.gitignore` file listing `.env.local` and `node_modules`. If `.env.local` is missing from it, add it now.

Explain why in one sentence: **once a password is saved to GitHub, deleting it later does not remove it — it stays in the history.**

### Then publish

1. Open **GitHub Desktop**.
2. Click **File** in the top menu, then **Add local repository**.
3. Click **Choose...** and select the website's project folder. Click **Select Folder**.
4. If it says *"this directory does not appear to be a Git repository"*, click the blue **create a repository** link in that message, then click **Create repository** on the next screen.
5. Look at the **bottom left**. There is a box that says **Summary (required)**. Type: `First version of my website`.
6. Click the blue **Commit to main** button underneath it.
7. Look at the **top of the window**. Click the blue **Publish repository** button.
8. A box appears. Leave the name as it is.
9. **Leave "Keep this code private" TICKED.** This is a client's website — it should not be public.
10. Click **Publish repository**.

> **Check it worked:** open **https://github.com** in your browser. Click your picture at the top right, then **Your repositories**. Your project is in the list.
> **Ask them:** "Can you see your project name in that list? (yes / no)"

---

# Step 8 — Put it on the internet

**What this does:** takes the files from GitHub and makes them a real website anyone can visit.

1. Open **https://vercel.com/new**
2. You will see a list headed **Import Git Repository**.
3. Find your project name in the list and click **Import** next to it.
4. **If your project is not listed:** click **Adjust GitHub App Permissions** (or **Configure GitHub App**) underneath the list, then choose **All repositories**, then **Save**. Go back and it will appear.
5. A settings screen appears. **Change nothing.** Vercel has already worked out how to build the site.
6. Click **Deploy**.
7. Wait. It takes one to three minutes, and you will see text scrolling as it builds.
8. When it finishes you get a congratulations screen with a picture of your website.
9. Click that picture, or the **Visit** button.

> **Check it worked:** your website opens at an address ending in `.vercel.app`. **Send that link to your own phone and open it.**
> **Ask them:** "Did the site open on your phone? (yes / no)"

**Tell them the thing that surprises everyone:** from now on, whenever they change the site and click **Push origin** in GitHub Desktop, the live site updates by itself within a minute or two. There is no uploading, ever.

### If the build failed

Do not paste the error log at them. It is almost always one of two things:

- **A missing setting** — they have not added the email keys yet. Normal at this point; it comes in Step 10.
- **A capital letter in a filename.** Their computer treats `Header.tsx` and `header.tsx` as the same file. Vercel does not. Find the mismatch and fix it.

---

# Step 9 — Connect your domain

**What this does:** replaces the long `.vercel.app` address with the real one people will type.

### 9a. Buy the domain

1. Open **https://www.namecheap.com** (or Cloudflare, or Porkbun — any is fine).
2. Type the domain you want into the search box and press Enter.
3. If it is available, click **Add to cart**, then **Checkout**.
4. **Decline every add-on it offers** except free WHOIS privacy, which is worth keeping.
5. Pay. It costs roughly $10–15 for the year.

> **Check it worked:** the domain appears in your account under **Domain List**.

### 9b. Tell Vercel about it

1. Open **https://vercel.com/dashboard** and click your project.
2. Click **Settings** in the row of tabs near the top.
3. Click **Domains** in the menu on the left.
4. Type your domain into the box, without `www` and without `https://`. Just `yourbusiness.com`.
5. Click **Add**.
6. Vercel now shows you a table of settings to copy. **Leave this tab open.** You need these exact values, and they are different for every project — never copy them from a tutorial, including this one.

### 9c. Enter those settings at the registrar

1. Open your registrar in a **new tab** and sign in.
2. Find your domain and open its **Manage** page.
3. Find the section called **Advanced DNS** (Namecheap) or **DNS Records**.
4. Add each record Vercel showed you, one at a time, copying the Type, Host, and Value **exactly**.
5. Save.
6. Go back to the Vercel tab and wait. It usually updates within a few minutes.

> **Check it worked:** the domain shows a green tick or **Valid Configuration** in Vercel, and typing `yourbusiness.com` opens the site with a padlock in the address bar.
> **If it still says invalid after 30 minutes:** that is normal, not broken. It can take up to 48 hours. Check back later.

---

# Step 10 — Make the contact form work

**Say this before starting:** right now the form looks finished but does not send anything. That is expected. This step connects it.

### 10a. Prove you own the domain

1. Open **https://resend.com/domains**
2. Click **Add Domain** at the top right.
3. Type your domain, click **Add**.
4. Resend shows a table of settings — a different set from Step 9.
5. Go to your registrar, into **Advanced DNS** again, and add each of these records exactly as shown.
6. Back in Resend, click **Verify**. It may take a few minutes.

> **Check it worked:** the domain shows **Verified** in Resend.

### 10b. Get the key

1. Open **https://resend.com/api-keys**
2. Click **Create API Key**.
3. Name it after the website. Leave the other settings alone. Click **Add**.
4. A long code starting `re_` appears. **Copy it now — it is shown only once.**
5. Paste it straight into the next step. Do not put it in a message, an email, or a document.

### 10c. Give the key to Vercel

1. Open **https://vercel.com/dashboard**, click your project.
2. Click **Settings**, then **Environment Variables** on the left.
3. Add each variable, clicking **Save** after each one:
   - Name `RESEND_API_KEY`, value: the `re_...` code
   - Name `CONTACT_TO_EMAIL`, value: the address that should receive enquiries
   - Name `CONTACT_FROM_EMAIL`, value: `website@yourdomain.com`
4. Click **Deployments** in the top tabs.
5. Find the newest one at the top. Click the **⋯** menu at its right. Click **Redeploy**, then **Redeploy** again to confirm.

> **The step everyone forgets is 4 and 5.** Settings only take effect when the site is rebuilt. Without the redeploy, nothing changes and it looks broken.

> **Check it worked:** open the **live site** — not the preview on your computer — fill in the contact form, and send it. The email arrives.
> **If it does not arrive:** check the spam folder first. Brand-new domains often land there for a few weeks, and the verification in 10a is what fixes it over time.

---

# Step 11 — Add online booking

*Skip if they chose phone or WhatsApp only.*

## First, ask which kind

This is the fork in the road. Ask it as an outcome, never by naming products:

> Two ways to handle appointments:
>
> **A — Simple.** Customers pick a time on the site, and the appointment lands in the business's calendar with automatic reminder emails. Quick to set up, and it uses a free outside service.
>
> **B — Their own system.** Same for the customer, but the owner also gets a private login on their own website where they can see the day's appointments, cancel, reschedule, and read every enquiry in one place. More work to build, and worth more.
>
> Which fits this business?

**If A** — continue below with Cal.com.

**If B** — stop here and switch to the **`client-dashboard`** skill. It picks up at this exact point, adds the database and the owner's login, and rejoins this walkthrough at the **"Get found on Google"** step. Do not do both; B replaces the booking part of A entirely. Both paths still finish with the security check and handover.

Guidance for the recommendation: B suits a business that already juggles a diary and loses track — a clinic, a salon with several staff. A is right for most others. Ask what the owner does today before recommending anything, and do not sell a database to someone happy with a paper diary.

---

## Option A — Cal.com

1. Open **https://app.cal.com/availability**
2. Click your schedule to open it.
3. Set the real working days and hours. Untick days they are closed.
4. Click **Save**.
5. Click **Event Types** in the left menu.
6. Click **+ New**.
7. Give it the name of a service, e.g. `Check-up`, and set how long it takes.
8. Click **Continue**, then **Save**.
9. Repeat for each service with a different length.
10. Open the event, find **Reminders** or **Workflows**, and turn on the reminder email. **This is the single biggest thing that reduces no-shows.**
11. Copy the booking link shown at the top of the event — it looks like `cal.com/your-name/check-up`.
12. Give that link to Claude to put it on the site.

> **Check it worked:** open the website, click the booking button, and **make a real test appointment**. The confirmation email arrives. Then cancel it.

**Always keep the phone number next to the booking button.** Booking widgets get blocked by ad blockers and privacy settings. An older customer who cannot make it work must never be left stranded.

---

# Step 12 — Get found on Google

### 12a. Google Business Profile — do this one first

For a local business this brings **more customers than the website itself**. Most people find a clinic or restaurant through Google Maps.

1. Open **https://business.google.com**
2. Click **Manage now**.
3. Enter the business name and category.
4. Add the address, phone number, and website — **exactly as they appear on the site**, down to the punctuation. Mismatches hurt ranking.
5. Verify. Google usually sends a postcard, a call, or a video verification.

### 12b. Search Console

1. Open **https://search.google.com/search-console**
2. Click **Add property**, choose **URL prefix**, and enter the full site address.
3. Verify — the DNS method uses the same registrar screen as before.
4. Once verified, click **Sitemaps** on the left, type `sitemap.xml`, and click **Submit**.

> **Check it worked:** after a few days, search `site:yourdomain.com` on Google and see pages listed.
> **Set expectations:** new sites take weeks to appear properly. This is normal.

### 12c. Being found by AI assistants

**What this does:** gives the site the best chance of being recommended when someone asks ChatGPT or Claude for "the best dentist in [city]".

Most of this was built in — the structured data, the FAQ, one page per service. Two things remain:

1. **Check the structured data passes.** Open **https://search.google.com/test/rich-results**, paste the live address, click **Test URL**.

> **You should see:** the business listed as a valid item, and the FAQ detected.

2. **Decide about the AI crawlers — ask the client, do not decide for them.**

> "To be recommended by AI assistants, they have to be allowed to read the site. The trade-off is that the content may also be used to train those systems. For a local business wanting customers, allowing it is usually the right call — but it's your decision."

Then set `app/robots.ts` to match their answer. See `references/performance-and-discovery.md` § 4.1.

**Be honest about what this buys.** Nobody can guarantee an AI recommendation. Tell the client what actually weighs most for local questions — **a complete Google Business Profile and real reviews outrank anything on the website itself.** Saying so is the honest advice and it is what actually works.

---

# Step 13 — Final checks

Run every one of these **on the real domain**, on a real phone.

- [ ] Every menu link opens a real page
- [ ] The contact form sends and the thank-you message appears
- [ ] Tapping the phone number starts a call
- [ ] The WhatsApp button opens the right number
- [ ] The map points at the right building
- [ ] Opening hours match reality, and match Google
- [ ] A test booking completes
- [ ] Nothing looks broken on a phone
- [ ] No leftover `[[PLACEHOLDER]]` text anywhere
- [ ] No made-up reviews, statistics, or credentials
- [ ] The site has an icon in the browser tab
- [ ] A wrong address shows a proper "page not found" page

**Then test the speed — on the live address, and show the user the score.**

1. Open **https://pagespeed.web.dev**
2. Paste the live address, click **Analyse**
3. Wait about a minute, then click the **Mobile** tab

> **You should see:** Performance **95 or above**.
>
> **If it is lower:** read the top item under "Opportunities" and fix that first. It is almost always an oversized image. `references/performance-and-discovery.md` § 1.7 has the fixes.

This number is worth showing the client — most websites in their market will not come close to it.

**If the site has more than one language, run every check above in each language**, and PageSpeed on both. The other language is not a second-class version.

---

# Step 14 — Security check

**Never hand over a site without this.** Customers are giving this business their name, their phone number, and sometimes why they need a doctor. Protecting that is part of the job.

**Follow `references/security-check.md` in full.** Run every automated check yourself before involving the user — scan the code and git history for leaked keys, confirm no server-only key reaches the browser, check that no personal data is written to the logs, verify server-side validation, check the security headers, and re-run the database leak test if the site has one.

Then bring the user in for the two things only they can do: **turning on two-factor authentication** on every account, and confirming who else has access.

Report findings grouped by severity in plain language, with the fix beside each — never paste raw tool output at them.

> **Check it worked:** the report shows nothing under CRITICAL.
>
> **If anything is CRITICAL, say plainly that the site must not be handed over until it is fixed**, and fix it together. This is the one place where being agreeable is the wrong call.

---

# Step 15 — Hand it to the client

Only for client work.

**Ownership.** The client should own the domain and the Vercel account, with the builder invited as a collaborator. When the domain sits in the builder's personal account, separating later is painful for both sides.

**Credentials** go through a password manager, never email or WhatsApp.

**Write down for them:**
- Their live address, and where the site is hosted
- How to ask for content changes
- The domain renewal date and cost — sites die every year because nobody knew who was paying
- Who to contact when something breaks

**Offer a maintenance plan** at handover, not months later. Content updates, monitoring, and renewals are a legitimate monthly service and the reason a one-off build becomes an ongoing income.
