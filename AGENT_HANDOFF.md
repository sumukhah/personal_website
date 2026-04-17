# Sumukha QR Founder Site - Agent Handoff

This document is for the next agent who will continue work on the personal website in this repo.

Use this together with the original Obsidian planning/context note:
- `YC Event Personal Website design`

That note already contains the original business context, event context, startup story background, and linked notes. This handoff focuses on:
- what has already been implemented
- what decisions were made during planning/building
- what changed during implementation
- what still needs to happen next

## 1. Goal of the site

This is **not** a generic portfolio site.

It is a **mobile-first landing page for QR scans from a T-shirt** worn during a co-founder search / YC event context. The page is meant to help a potential co-founder quickly answer:
- who is Sumukha
- what has he actually built
- is he credible
- what kind of person is he looking for
- should I reach out

Tone direction is intentionally:
- casual
- playful
- funny / internet-native
- founder-personal
- not corporate / not polished portfolio energy

## 2. Current implementation status

The repo now contains a working Astro site with:
- homepage implemented
- thank-you page implemented
- custom visual system implemented
- custom LinkedIn helper UX implemented
- Tally-based contact flow integrated at the page level

The site currently builds successfully with:
- `npm run check`
- `npm run build`

## 3. Major decisions that were taken

### Hosting / stack

Locked decisions:
- Host on GitHub Pages
- Root domain target: `https://sumukhah.github.io`
- Use Astro
- Use Tailwind CSS v4
- Output is static

Reason:
- simple deployment
- static site is enough
- fast mobile performance
- good fit for a QR landing page

### Site structure

We intentionally chose a **single-page landing page**, not a multi-page personal website.

Reason:
- QR traffic should be fast and focused
- event visitors are likely on mobile
- the primary job is scan -> understand -> contact

Current section order on the homepage:
1. Hero
2. Why this page exists
3. Proof snapshot
4. Founder journey
5. Why Sumukha is good to work with
6. Things built
7. What he is looking for
8. Contact / apply section
9. Footer

### Visual direction

We locked a **Matrix-inspired founder showcase**, but explicitly avoided “terminal cosplay”.

Chosen design traits:
- dark cinematic background
- neon green signal color
- off-white / cream text
- red/green pill CTA motif
- glassy cards
- grid / scanline atmosphere
- subtle motion only

Explicitly avoided:
- fake CLI as the entire UI
- over-animated gimmicks
- generic AI landing page styling
- corporate portfolio structure

### Humor / memes / GIFs

We decided the site should be more fun and more human, not just metrics-heavy.

So the page includes **placeholder slots** for:
- hero reaction visual
- solo-founder-chaos visual
- builder-energy visual
- fit-check / co-founder reaction visual

These are placeholders right now, not final assets.

Important rule for the next agent:
- memes/GIFs should feel intentional
- every visual joke should reinforce credibility or personality
- do not turn the page into random meme clutter

### Contact flow

This changed multiple times during planning.

Final decision:
- only 2 fields
- `LinkedIn profile URL` is required
- `Anything else?` is optional free text

Explicitly removed:
- name
- email
- phone
- social extras as separate fields

Reason:
- name is redundant if LinkedIn is present
- LinkedIn is the main screening signal
- the form should stay extremely low-friction

### Why LinkedIn is mandatory

This was a deliberate product decision.

Reason:
- Sumukha wants to screen inbound leads before replying
- LinkedIn is the clearest structured signal about work history / career background
- it reduces low-signal inbound compared to pure text-only contact

### LinkedIn helper UX

A major design concern was that people may not know their LinkedIn profile URL off-hand.

So instead of just a plain required URL field, the page includes:
- `How do I find this?`
- `Paste from clipboard`

The helper modal gives:
- desktop instructions
- mobile instructions
- `Open LinkedIn` CTA

The clipboard flow:
- tries to read from clipboard only on explicit user action
- validates whether the clipboard contains a LinkedIn profile URL
- auto-fills if valid
- opens helper guidance if invalid / blocked

Important constraint we explicitly respected:
- the site does **not** claim it can fetch data from a LinkedIn account
- it only helps the visitor copy/paste the profile URL faster

### Form backend choice

This changed during implementation.

History:
- Early plan used Formspree
- then free-tier concerns pushed evaluation toward alternatives
- Web3Forms was implemented briefly
- user reported Web3Forms was not working / did not want it
- final direction switched to **Tally**

Current implementation uses:
- `PUBLIC_TALLY_FORM_URL`

Meaning:
- the page is custom
- Tally handles the actual submission UI/backend
- the page still keeps the LinkedIn helper UI

Important nuance:
- the page does **not** submit a custom HTML form anymore
- instead, the page now opens / embeds a Tally form URL
- current code also tries to sync current field values into the Tally URL as query params

This means the next agent should verify whether the chosen Tally setup actually supports the expected prefill behavior for:
- `linkedin_url`
- `details`
- `src`

That part should be treated as something to validate, not as already guaranteed.

## 4. What is already built in the repo

### Main app files

- `src/pages/index.astro`
  - full landing page
  - section copy
  - contact card
  - LinkedIn helper modal
  - client-side helper logic

- `src/pages/thanks.astro`
  - thank-you page

- `src/layouts/BaseLayout.astro`
  - shared metadata / fonts / canonical setup

- `src/styles/global.css`
  - entire visual system
  - colors
  - glass styles
  - motion
  - background effects

### Project setup files

- `astro.config.mjs`
- `package.json`
- `tsconfig.json`
- `.env.example`
- `README.md`

### Static assets

- `public/favicon.svg`
- `public/og-preview.svg`

## 5. Important implementation details

### Env variable

Current expected env var:

```env
PUBLIC_TALLY_FORM_URL=https://tally.so/r/your-form-id
```

This is documented in:
- `.env.example`
- `README.md`

### Current contact section behavior

Current UX in the page:
- visitor can type/paste LinkedIn URL
- helper modal can guide them
- optional details textarea exists in the page UI
- CTA opens Tally form
- inline iframe embed is shown if `PUBLIC_TALLY_FORM_URL` exists
- direct link button is also shown

Important caveat for the next agent:
- the page-level input fields are custom UI
- Tally is a separate hosted form
- if the page values are not being correctly transferred into Tally in production, the next agent should decide between:
  - fully rely on Tally embed and remove the duplicated custom fields
  - or return to a fully custom submit flow with a different backend

Because the user explicitly said:
- Web3Forms is not working
- use Tally only

So if Tally prefill turns out to be weak, the safer move is likely:
- make Tally the actual visible form source of truth
- keep the helper UI on the page only as guidance

### Copy / content decisions already reflected in the current page

The implemented copy assumes:
- Sumukha built SpeakUp solo
- traction matters, but the site should not be metrics-only
- the failed co-founder attempt should be acknowledged without sounding bitter
- “good to work with” matters as much as raw traction

The site currently emphasizes:
- speed
- ownership
- product + growth ability
- honesty / directness
- low-ego execution

### Placeholder content still present

Still placeholders:
- meme/GIF assets
- hero visual asset
- some visual inserts

Not final:
- exact media assets
- final Tally form URL
- final confirmation that Tally-prefill flow behaves correctly

## 6. What the next agent should verify first

The next agent should start with these checks:

1. Run the site locally.
   - `npm install`
   - `cp .env.example .env`
   - put the real Tally URL in `.env`
   - `npm run dev`

2. Verify the contact flow end-to-end.
   - Does the Tally form open correctly?
   - Does the iframe embed render correctly?
   - Does Tally accept / preserve the intended 2-field structure?
   - Do the current query params actually prefill the Tally form fields?
   - Is the `src=yc-shirt` info captured somewhere useful?

3. Decide whether the current hybrid UX is the final one.
   - Current hybrid = custom LinkedIn helper + external Tally form
   - This may be okay, or it may feel duplicated/confusing

4. Replace placeholder visuals.
   - Add real meme / GIF / image assets carefully
   - Keep the tone intentional

5. Improve mobile polish.
   - Especially the contact section
   - embedded form height
   - hero balance
   - typography scaling

## 7. Strong recommendations for the next agent

### Recommendation 1

Do not redesign from scratch unless the user asks.

The current direction already reflects a lot of deliberate decisions:
- single page
- Matrix-adjacent
- funny but credible
- LinkedIn-first screening
- casual founder showcase

### Recommendation 2

Treat the form flow as the highest-risk area.

The content/design foundation is already strong enough to iterate on.
The biggest product risk now is whether the final Tally-based submission experience feels:
- clean
- consistent
- low-friction
- technically reliable

### Recommendation 3

If Tally prefill is awkward, simplify rather than over-engineer.

Possible fallback:
- keep the helper UI above
- replace the duplicated custom fields with a short explanation + embedded Tally form only

This would preserve:
- custom site feel
- LinkedIn helper value
- Tally-only backend

while reducing mismatch between page UI and actual submission UI.

### Recommendation 4

Preserve the 2-field form constraint unless the user explicitly changes it.

This was a clear late-stage decision and should be treated as locked.

## 8. Current commands

Validated commands:

```sh
npm run check
npm run build
```

These passed during the latest implementation pass.

## 9. Summary of current state in one paragraph

The repo now contains a working Astro/Tailwind single-page founder landing page for QR traffic, with a dark Matrix-inspired visual system, proof-first storytelling, playful placeholder meme slots, a custom LinkedIn helper UX, and a Tally-based contact flow that needs final real-form verification and media polish rather than a full rebuild.
