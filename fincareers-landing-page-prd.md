# PRD: FinCareers Landing Page (fincareers.ca)
**Version:** 1.2
**Purpose:** Validation landing page — waitlist collection
**Status:** Pre-build brief
**Last updated:** Reflects cohort framing, UGC strategy split, and pricing signal decisions

---

## Changelog

| Version | Change |
|---|---|
| 1.0 | Initial PRD |
| 1.1 | Removed UGC from landing page — moved to ads only. Added cohort framing. |
| 1.2 | Added pricing signal strategy. Updated social proof to Phase 2. Updated ad strategy notes. |

---

## 1. Project Overview

Build a single-page, conversion-focused validation landing page for **FinCareers** — a Canadian compliance career bootcamp. The page's sole job is to collect waitlist emails and qualify leads for the next cohort.

**Important context:** FinCareers has informally trained people in compliance before. This is NOT framed as a new company launching for the first time. It is framed as an **established program opening applications for its next cohort.** That distinction affects every headline, CTA, and trust signal on the page.

**Domain:** fincareers.ca
**Market:** Canada-first. US expansion later.
**Primary Track:** AML (Anti-Money Laundering)
**Future Tracks:** KYC, Fraud, FINTRAC, OSFI, broader financial compliance
**Deployment:** Vercel (static HTML — no build step required)

---

## 2. Business Goal

Validate sufficient demand to justify running a paid cohort.

**Success threshold:** 50+ quality waitlist signups at under $5 cost-per-lead within the first 2 weeks, converting to at least 10 paid enrollments when the cohort is announced to the list.

If threshold is met → open enrollment, run first paid cohort.
If not → pivot offer, messaging, or audience before spending more on ads.

---

## 3. Target Audience

Three primary segments, all in Canada, all with zero or minimal compliance experience:

| Segment | Pain | Motivation |
|---|---|---|
| **New immigrants** | Foreign credentials not recognised. Can't get "Canadian experience." | Stable, well-paying career pathway into Canadian financial services |
| **Fresh graduates** | Finance/business degree but every role requires 2+ years experience | Stand out, get hired fast, use a credential employers want |
| **Unemployed / career changers** | No direction, wrong industry, no upward mobility | Clear structured path into a growing, stable industry |

**Psychographic:** Ambitious, resourceful, slightly frustrated. Not looking for theory — looking for a job. Price-sensitive but will invest in a clear, proven outcome.

---

## 4. Brand Identity

| Element | Direction |
|---|---|
| **Brand name** | FinCareers |
| **Tagline** | *Your path into Canada's financial compliance industry — no experience required* |
| **Tone** | Confident, warm, direct. Not corporate. Not academic. Speaks like a mentor, not a brochure. |
| **Colour palette** | Deep navy (#0A1628) as primary. Gold/amber (#D4A853) as accent. White backgrounds. No bright colours. |
| **Typography** | Inter or similar clean sans-serif. Heavy weight headlines. Generous whitespace. |
| **Feel** | Premium but accessible. Apple-esque minimalism. Feels like a proper institution, not a side hustle. |

---

## 5. Cohort Framing — Critical Positioning Decision

**Do not launch this page like a new company.** The copy, hero, and CTA must all signal that this is an ongoing, established program accepting applications for its next intake.

**Use this framing throughout:**
- ✅ "Applications now open for the next cohort"
- ✅ "Previous cohorts have placed graduates at Canadian banks and fintechs"
- ✅ "Secure your spot before the cohort fills"
- ✅ "Join the waitlist for the next intake"
- ❌ "We're launching soon"
- ❌ "Be the first to know"
- ❌ "Coming soon"

This framing creates three conversion advantages: authority (established program), scarcity (cohort has limited seats), and social proof (others have done this before you) — without requiring testimonials on the page.

---

## 6. UGC & Social Proof Strategy

### What is available for V1 (landing page launch)
UGC from previously trained students is **not yet ready** for the landing page. The page must convert without testimonials or video proof.

**How the page compensates without UGC:**
1. Cohort framing signals track record (see Section 5)
2. Industry outcome stats replace personal proof (salary data, job market growth, FINTRAC demand)
3. Curriculum credibility shows depth of programme
4. Low-commitment offer (free waitlist, founding member pricing) reduces purchase risk
5. Founding member pricing language creates urgency without pressure

### Where UGC will be used (V1)
UGC from previously trained students will be deployed **in paid ads only.** The ads do the trust-building and emotional connection work. By the time the visitor lands on the page, social proof has already been established by the ad creative. The landing page then confirms the ad message and captures the conversion.

**UGC ad creative direction:**
- Raw and authentic — phone camera, natural lighting, real words. Not produced.
- Specific outcomes over generic praise: *"I was unemployed for 6 months and landed at TD within 8 weeks"* beats *"This course is amazing."*
- One testimonial per ad. Don't stack. One strong story is more powerful than three average ones.
- Match the audience segment in the ad to the testimonial speaker — immigrant ad uses immigrant story, graduate ad uses graduate story.

### Phase 2 (post first cohort)
Once the first paid cohort completes, add a dedicated social proof section to the landing page between Section 5.6 (Why FinCareers) and Section 5.7 (FAQ). This section should contain:
- 3–5 video or written testimonials with photo, name, previous role → new role
- One specific outcome stat pulled from cohort results (e.g., "8 out of 10 graduates from our first cohort secured interviews within 60 days")

---

## 7. Pricing Signal Strategy

**Do not show a specific price on the V1 landing page.** The price is not yet finalised and committing to a number too early creates anchoring problems.

**Do signal clearly that this is a paid programme.** Without any pricing signal, freebie-seekers pollute the waitlist and the list quality drops.

**How to signal paid without committing to a number:**

Add the following elements to the page:

1. **Below the hero form**, in small text alongside the "no spam" note:
   *"Paid bootcamp · Founding member pricing available to waitlist members only"*

2. **In the FAQ** (Question 4 — "How much will it cost?"):
   *"FinCareers is a paid professional bootcamp. Exact pricing will be announced to waitlist members first — and founding members will receive a significant discount not available after launch. Join the waitlist to be first in line."*

3. **In the final CTA section**, sub-copy beneath the headline:
   *"Waitlist members get founding member pricing — the lowest this programme will ever be."*

**Planned pricing ladder (internal reference — not shown on page):**
- Cohort 1 (founding): ~$497 — never available again
- Cohort 2: ~$650 — as social proof builds
- Cohort 3+: ~$800 — full price with testimonials and track record
- Payment plan option: ~$97–150/month across 6 months (to be confirmed)

---

## 8. Page Sections (in order)

### 8.1 Navigation Bar
- Logo: "FinCareers" wordmark with small icon (shield or path motif)
- Single CTA button top right: **"Apply for Next Cohort"** (scrolls to form)
- Sticky on scroll, background becomes opaque navy after 40px scroll

### 8.2 Hero Section
**Goal:** Immediate clarity + emotional resonance + first conversion point

- **Badge above headline:** *"Applications open · Next cohort — Canada"* with a pulsing dot
- **Headline:** Outcome-first, career-entry focused. Direction: *"Break into Canada's Compliance Industry — No Experience Required"*
- **Sub-headline:** 2 sentences max. Calls out the three audience segments. Mentions AML as the first track. Mentions Canada specifically. Example: *"Built for newcomers, fresh graduates, and career changers. Previous cohorts have placed graduates at Canadian banks and fintechs."*
- **Inline email form:** Email input + "Join the Waitlist" button side by side (stacks on mobile)
- **Trust note below form:** *"Paid bootcamp · Founding member pricing for waitlist members · No spam"*
- **3 trust stats below form** (in a row):
  - $65K+ average entry-level compliance salary in Canada
  - 2,800+ compliance job postings in Canada annually
  - 90 days to job-ready
- Background: Dark navy with subtle grid pattern overlay and radial gold glow at top

### 8.3 "Does This Sound Like You?" Section
**Goal:** Audience identification — make each segment feel seen

- 3-card grid, one per audience segment
- Each card: emoji icon, segment title, 2-sentence pain description, 3 bullet points of specific frustrations
- Segments: New to Canada / Fresh Graduate / Career Changer
- Light off-white background section

### 8.4 "What Is AML?" Section
**Goal:** Educate the uninitiated — most of the audience doesn't know what AML is

- Split layout: text left, stats cards right
- Left side: 2–3 short paragraphs explaining AML simply, why Canadian banks need it, why entry-level roles don't require finance degrees
- Right side: 2x2 grid of stat cards in navy/gold
  - 34% AML job growth in Canada (3yr)
  - $85K senior AML analyst average salary
  - Big 6 banks all actively hiring compliance staff
  - FINTRAC = mandatory compliance framework in Canada

### 8.5 "What You'll Learn" — Curriculum Preview
**Goal:** Build credibility, show the transformation arc

- 6-card grid showing the 12-week curriculum at a high level
- Each card: week range, module title, 1-sentence description
- Modules: AML Foundations → KYC & Due Diligence → Transaction Monitoring → Canadian Banking Context → Job Placement Prep → Certification Support (CAMS)
- Top gold accent bar on each card
- Note: *"Curriculum shown is indicative. Final curriculum confirmed with each cohort intake."*

### 8.6 "Why FinCareers" Section
**Goal:** Differentiation — why this over a YouTube playlist or a generic course

- 6-item grid (icon, title, 2-sentence description per item)
- Key differentiators to cover:
  1. Canada-specific curriculum (FINTRAC, PCMLTFA, Big 6 banking context)
  2. Zero experience required — built for absolute beginners
  3. Outcome-focused, not theory-heavy — maps to what hiring managers actually test for
  4. Immigrant-friendly — helps newcomers translate existing strengths into compliance language Canadian employers understand
  5. Live cohort + community — not a passive video course
  6. Expandable career path — AML is just the start; KYC, fraud, and more tracks are coming

### 8.7 ~~Social Proof Section~~ — PHASE 2 ONLY
**Status:** Not included in V1. To be added after first paid cohort completes.
**Placeholder:** Section slot is reserved between 8.6 and 8.7 for future insertion of testimonials and cohort outcome stats.

### 8.7 FAQ Section
**Goal:** Eliminate objections before the final CTA

Minimum 6 questions, accordion style:
1. Do I need any prior finance or compliance experience?
2. I'm a newcomer to Canada. Will this help me specifically?
3. How long is the bootcamp and what's the format?
4. How much will it cost? *(see Section 7 for answer copy)*
5. Will this help me get a job at a Canadian bank?
6. What if I join the waitlist but the cohort doesn't run?

### 8.8 Final Waitlist CTA Section
**Goal:** Primary conversion point — capture email + qualify the lead

- Dark navy background
- Bold headline: *"Ready to Make the Move?"*
- Sub-copy: *"Waitlist members get founding member pricing — the lowest this programme will ever be."*
- Form fields:
  1. Email address (required)
  2. Dropdown: "What best describes you?" — New to Canada / Fresh Graduate / Currently Job Searching / Career Changer / Other
- CTA button: **"Secure My Spot →"**
- Note below: *"Paid bootcamp · Founding pricing for waitlist only · Unsubscribe anytime"*
- Success state: Form hides, thank-you message appears inline (no redirect)
- Thank-you message: *"You're on the list. We'll be in touch with cohort details and your founding member pricing shortly."*

### 8.9 Footer
- FinCareers wordmark
- Copyright line
- Email: hello@fincareers.ca (placeholder)
- Links: Privacy Policy · Terms of Service (placeholder pages)

---

## 9. Technical Requirements

| Requirement | Detail |
|---|---|
| **Format** | Single HTML file — deployable directly to Vercel with no build step |
| **Performance** | No JS frameworks. Vanilla JS only. Google Fonts via CDN. Target LCP < 2s. |
| **Forms** | Formspree.io free tier (replace `YOUR_FORM_ID` placeholder). No backend needed. |
| **Responsiveness** | Mobile-first. Fully responsive at 375px, 768px, 1280px breakpoints. |
| **Animations** | Scroll-triggered fade-up reveals (IntersectionObserver). Hero entrance animation. No jarring motion. |
| **Accessibility** | Semantic HTML. 4.5:1 contrast minimum. Keyboard navigable. |
| **Analytics** | Add placeholder for Google Analytics / Meta Pixel script tags in `<head>` |

---

## 10. Form Behaviour

- **Hero form** (email only): On submit → smooth scroll to final waitlist section → pre-fill email into final form. Does NOT submit separately.
- **Final form** (email + dropdown): Submits to Formspree via fetch. On success → hide form, show inline thank-you message. On error → re-enable button with error message.
- **Both forms** must have loading state on submit button ("Submitting…" + disabled state).

---

## 11. SEO & Meta

```html
<title>FinCareers — Launch Your Compliance Career in Canada</title>
<meta name="description" content="Break into Canada's AML and compliance industry — no prior experience required. Join the waitlist for FinCareers, the bootcamp built for newcomers, fresh graduates, and career changers.">
<meta property="og:title" content="FinCareers — Launch Your Compliance Career in Canada">
<meta property="og:description" content="No experience? No problem. Get job-ready for AML and compliance roles in Canada in 90 days.">
<meta property="og:image" content="/og-image.png"> <!-- 1200x630 -->
<link rel="canonical" href="https://fincareers.ca">
```

---

## 12. Ad Strategy & Landing Page Alignment

This page will receive paid traffic primarily from Meta (Facebook/Instagram) with LinkedIn as secondary.

**The trust-building split:**
- **Ads** carry the social proof and emotional connection via UGC — raw testimonials from previously trained students, one story per ad, matched to audience segment
- **Landing page** confirms the ad message and converts — it does not need to re-establish trust from scratch

**Design with this flow in mind:**
- Above the fold must mirror the ad message — if the ad says "break into AML with no experience," the headline must say the same thing
- No outbound links anywhere on the page — keep visitors on page
- No navigation links to other pages — nav CTA scrolls to form only
- One CTA throughout — "Join Waitlist" / "Secure My Spot" everywhere. No competing actions
- Mobile-first priority — majority of Meta ad traffic lands on mobile

**Ad audience targeting (for reference):**
- Meta: Target by interest (job searching, career change, finance), life events (recently moved to country), language communities (newcomer-heavy)
- LinkedIn: Target by job title (KYC Analyst, Bank Teller, Fraud Analyst, Finance Graduate) and geography (Canada)
- Budget: Start at $5–10/day per ad set. Kill underperformers at 500 impressions. Scale winners.

---

## 13. Phase 2 — Post-Validation Additions

Once first paid cohort is complete and results are available, add the following in V2:

- Social proof section with video/written testimonials and cohort outcome stats
- Specific pricing section with cohort pricing ladder
- Instructor / founder bio section
- Multiple track pages (KYC, Fraud, FINTRAC)
- US market variant (fincareers.com or /us subdirectory)

---

## 14. Prompt Instructions for Build Session

When using this PRD to build the page, use the following prompt:

> *"Build the FinCareers landing page as a single HTML file following the attached PRD (v1.2). Use the frontend-architect skill. Navy (#0A1628) and gold (#D4A853) colour palette. Mobile-first. Vanilla JS only. Formspree for form handling with placeholder form ID. No social proof section — that is Phase 2. Use cohort framing throughout — not new company framing. Include pricing signal copy exactly as specified in Section 7. All sections as per Section 8. Deploy-ready for Vercel."*

---

*PRD version 1.2 — FinCareers Validation Phase*
