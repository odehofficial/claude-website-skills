---
name: law-firm-website
description: Build a website for a law firm, solicitor, attorney, advocate, legal consultancy, or individual lawyer — collects the brief, applies legal advertising compliance rules, then hands off to the website-launch skill to build and go live. Use when the user wants a website for any legal practice, or mentions practice areas, case results, legal consultations, or bar admission.
---

# Law Firm Website

Collects the brief for a legal practice, then hands off to `website-launch` for the build and deployment.

**Read the compliance section before building.** Legal advertising is one of the most heavily regulated categories on this list, and the rules differ sharply by jurisdiction. Getting it wrong can expose the client to disciplinary action, not just a bad website.

## How to run this

1. Interview the user with the questions below — use `AskUserQuestion` for the discrete choices.
2. Confirm the brief back in a short summary.
3. Invoke `website-launch` and follow its workflow from Step 2 (design system) onward.

## Intake questions

**Required before building:**

1. Firm name, city, country, full address
2. **Jurisdiction and regulating body** — which bar, law society, or council governs their advertising
3. Language(s) — if Arabic, full RTL layout
4. Practice areas
5. Lawyers — names, qualifications, bar admissions, years qualified
6. Phone, email, office hours
7. Consultation — free or paid, and how it is booked
8. Client type — individuals, businesses, or both
9. Domain — owned or needs buying?

**Ask if relevant:**

10. Notable cases or results they want featured — subject to the disclaimer rules below
11. Professional memberships, accreditations, rankings
12. Languages the team speaks — often a genuine differentiator
13. Fee model — hourly, fixed fee, no-win-no-fee (heavily regulated in some jurisdictions)

## What actually converts for a law firm

Someone contacting a lawyer is usually stressed and often embarrassed. They are choosing on trust and approachability, not on a feature comparison.

1. **Practice area pages are the whole SEO strategy.** "Divorce lawyer [city]" is the search that brings clients, and each practice area needs its own page with real depth to rank. A single combined services page will not compete.
2. **Named, photographed humans.** Anonymous firms do not convert. Real headshots and real names, with credentials, beat any amount of polished copy.
3. **Lower the barrier to first contact.** A free initial consultation, where permitted, dramatically increases enquiries. If the firm charges, say what it costs — uncertainty stops people from calling.
4. **Explain in plain language.** The firm that explains the process in words a non-lawyer understands wins against the firm that demonstrates expertise through jargon. This is genuinely the biggest differentiator available in this category.
5. **Responsiveness is the top complaint** about lawyers. A promise like "we respond within one business day" converts well — but only include it if the client will actually honour it.

## Page structure

**Home** — hero stating clearly what they do and for whom · practice areas · why this firm · the team · credentials and accreditations · testimonials or case results (with disclaimers) · process explained simply · consultation CTA · location and contact

**Other pages** — One page per practice area · About the firm · Individual lawyer profiles · Fees and funding · Contact and consultation booking · FAQ · Insights/blog (strong for SEO in this category)

## Compliance — read this carefully

Rules vary by jurisdiction. **Tell the user to confirm every point below against their own bar or law society's advertising rules before publishing.** Do not assume US, UK, or Gulf rules apply universally.

- **Never guarantee outcomes.** No "we will win your case", no "guaranteed compensation". This is prohibited essentially everywhere.
- **Case results require a disclaimer** stating that past results do not guarantee or predict future outcomes. In some jurisdictions publishing results is restricted outright.
- **The contact form must state that submitting it does not create a lawyer-client relationship**, and must warn against sending confidential information before a formal engagement exists. This protects both parties and is standard practice.
- **State bar admissions and the jurisdictions where each lawyer is qualified to practise.** Implying a right to practise somewhere they are not admitted is a serious violation.
- **"Specialist" and "expert" are restricted terms** in several jurisdictions, usable only with formal accreditation. Prefer "focuses on" or "practice includes" unless the user confirms accreditation.
- **No testimonials at all** in some jurisdictions; permitted with a disclaimer in others. Ask before building the component.
- **Include the firm's registration or licence number** and regulatory body in the footer where required.
- **Contact forms need real privacy handling.** People will describe sensitive legal problems in a free-text field. Keep the form minimal, state clearly how the data is handled, and never route it somewhere insecure.

## Design direction

Credible and calm. This category tolerates conservative design far better than it tolerates anything that looks cheap or gimmicky — a client is deciding whether to trust this firm with something serious.

That does not mean dated. The common failure is a site that looks like it was built in 2009, signalling a firm that is not paying attention. Aim for clean, modern, restrained: generous whitespace, strong typographic hierarchy, a restricted palette, real photography of real people.

Avoid the visual clichés — gavels, scales of justice, columns, stock photos of anonymous handshakes. Every competitor uses them, so they communicate nothing.
