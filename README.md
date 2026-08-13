# Claude Website Skills

Ten skills that take Claude Code from *"build me a website for a dental clinic"* all the way to a live site on a real domain — with working contact email and online booking.

Each skill knows the industry: what converts, what the page structure should be, and which legal and compliance rules apply. You answer questions; Claude builds and then walks you through going live, one step at a time.

---

## What's included

| Skill | For |
|---|---|
| `website-launch` | **The engine.** Build workflow, stack, and the full go-live roadmap. Required. |
| `dentist-website` | Dental and orthodontic clinics, medical and aesthetic clinics |
| `restaurant-website` | Restaurants, cafes, bakeries, bars, food trucks, catering |
| `gym-website` | Gyms, studios, personal trainers, yoga, martial arts |
| `law-firm-website` | Law firms, solicitors, attorneys, legal consultancies |
| `salon-website` | Hair, barbers, beauty, nails, spa, massage, aesthetics |
| `real-estate-website` | Agencies, brokers, individual agents, developers |
| `home-services-website` | Plumbers, electricians, HVAC, cleaning, handyman, landscaping |
| `consultant-website` | Consultants, coaches, freelancers, agencies |
| `ecommerce-website` | Small online stores (read the scope warning inside first) |
| `client-dashboard` | **Optional upgrade.** Adds a booking system your client owns plus a private login where they manage appointments and enquiries themselves |

**Stack:** Next.js + Tailwind, hosted on Vercel, email via Resend, booking via Cal.com. Fixed on purpose, so one deployment roadmap always applies.

---

## Install

### Step 1 — Install the design engine first (required)

These skills depend on [`ui-ux-pro-max`](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) for colour, typography, and layout decisions:

```
/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
/plugin install ui-ux-pro-max@ui-ux-pro-max-skill
```

It needs **Python 3** to run its search tool. Check with `python --version`, and install from [python.org](https://python.org) if missing.

### Step 2 — Install these skills

```
/plugin marketplace add odehofficial/claude-website-skills
/plugin install website-skills@claude-website-skills
```

<details>
<summary>Manual install (if <code>/plugin</code> isn't available in your setup)</summary>

Clone the repo and copy the skill folders into your Claude skills directory:

**macOS / Linux**
```bash
git clone https://github.com/odehofficial/claude-website-skills.git
cp -r claude-website-skills/.claude/skills/* ~/.claude/skills/
```

**Windows (PowerShell)**
```powershell
git clone https://github.com/odehofficial/claude-website-skills.git
Copy-Item claude-website-skills\.claude\skills\* "$env:USERPROFILE\.claude\skills\" -Recurse -Force
```

Restart Claude Code afterwards so the skills are picked up.
</details>

### Step 3 — Check your tools

You need these installed before building:

```bash
node --version    # must be 18 or newer
git --version
```

Missing Node? Get it from [nodejs.org](https://nodejs.org).

**New to Git?** Install [GitHub Desktop](https://desktop.github.com) as well. It publishes your site to GitHub visually — no terminal commands to memorise — and it installs Git and signs you in at the same time. The deployment roadmap covers both the visual and the command-line route, so you can use whichever you prefer.

---

## How to use

Just describe the business:

> Build me a website for a dental clinic in Dubai

Claude picks the matching skill, interviews you about the business, generates a design system for your approval, builds the site, and then walks you through going live.

**The interview matters.** The more real detail you give — actual services, real hours, real contact details — the less you rewrite later. Claude will use clearly marked placeholders for anything you don't supply, and list them at the end so nothing ships half-finished.

---

## What you'll need accounts for

| Service | Purpose | Cost |
|---|---|---|
| GitHub | Stores your code | Free |
| Vercel | Hosts the site | Free tier |
| Resend | Contact form email | Free tier |
| Cal.com | Online booking | Free tier |
| Supabase | Database + login (only for the dashboard upgrade) | Free tier |
| Domain registrar | Your domain name | ~$10–15/year |

Only the domain costs money. Check each provider's current pricing — free tier limits change.

---

## Honest limitations

**Claude can't create your accounts.** It wires up every integration and leaves the API key slot ready, but signing up for Vercel or Resend is your step. The roadmap tells you exactly when and what to do.

**A contact form needs a backend to actually send mail.** Until you complete the Resend setup, the form is UI only. This surprises people — plan for it.

**Third-party dashboards change.** The walkthrough names exact buttons and where to find them, but these services redesign their screens. If something isn't where the instructions say, tell Claude what you *do* see on screen and it will adapt — you never need to start over.

**Compliance rules vary by country.** Each skill includes the industry rules it knows about, but medical, legal, and consumer-protection requirements differ by jurisdiction. Confirm against your local authority before publishing a regulated site.

**Claude won't invent business facts.** No fake testimonials, no invented credentials, no made-up statistics. This is deliberate — fabricated reviews for a real business are a legal problem, not a shortcut.

---

## License

MIT — use them, change them, teach with them.
