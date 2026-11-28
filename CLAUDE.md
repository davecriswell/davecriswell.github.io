# davecriswell.com

Dave Criswell's personal website. Plain HTML and CSS, no build step, hosted on GitHub Pages.
Dave is new to development and uses this project to learn Claude Code and GitHub, so explain changes in plain language.

## Before changing anything
Dave sometimes edits files directly on GitHub, so GitHub may be ahead of this copy. At the start of every task, before editing any file, pull the latest version: `git pull origin main`. If the pull brings in new commits, look at what changed and mention it to Dave, so his edits aren't overwritten or undone.

## Files
GitHub Pages publishes only the `docs/` folder. Files outside it (like this one) stay off the website but are still public on github.com.

| Page | File | URL |
| --- | --- | --- |
| Home | `docs/index.html` | `/` |
| Work | `docs/work/index.html` | `/work/` |
| Playbook & AI | `docs/playbook/index.html` | `/playbook/` |
| About | `docs/about/index.html` | `/about/` |
| Writing | `docs/writing/index.html` | `/writing/` |
| Essay: The Club Platform I Keep Sketching | `docs/writing/the-club-platform-i-keep-sketching.html` | |
| Essay: A Dashboard That Can Show Its Math | `docs/writing/a-dashboard-that-can-show-its-math.html` | |
| Essay: Reading Club Software's Future From Outside the Club | `docs/writing/reading-club-softwares-future-from-outside-the-club.html` | |

- `docs/style.css` holds every style. Colors and fonts are tokens at the top in `:root`; use only those tokens, never a new hex value.
- Every page links styles and pages with root paths (`/style.css`, `/work/`), which work on github.io and on a custom domain.
- **The header and the contact band plus footer are repeated on every page.** If you change one, change it on every page (eight pages, counting each essay).
- The header is sticky: it stays pinned to the top while scrolling. `[id] { scroll-margin-top }` in `style.css` keeps anchor links from landing under it; if the header gets taller, raise that value.
- The About photo is `docs/images/dave.jpg` (556 x 695, cropped so only Dave is in frame; shown at 280px wide on desktop, 220px on phones). To change it, replace that file and update the `width`/`height` on its `<img>` tag in `docs/about/index.html`.
- **Every link to an outside site opens in a new tab:** add `target="_blank" rel="noopener"` to any `<a href="https://...">`. This covers LinkedIn (footer and About), sources cited in essays, and any new outside link. Links between pages of this site (`/work/`, `/writing/...`, `#contact`) and the `mailto:` email link open normally.
- Menu: wordmark "Dave Criswell." (period in accent) links Home, then Work · Playbook & AI · Writing · About · Say hello. Say hello jumps to the contact band (`#contact`) on the current page. The current page's link gets `aria-current="page"`. On phones the menu sits on its own line under the wordmark; the phone `scroll-margin-top` allows for that.
- Each case study has an anchor so one example can be linked directly: `#data-foundation`, `#lead-funnel`, `#shift-imports`, `#game-reports`, `#pacing-dashboard`, `#trainingpeaks`, `#rafflecopter`.

## Page structure
Every page ends with the dark contact band ("Say hello.", Email me and LinkedIn buttons) and the footer ("© 2026 Dave Criswell · Built with Claude Code").
- **Home:** hero ("Hi, I'm Dave." with the hand-drawn underline), photo (placeholder until Dave supplies a running or riding photo), How I think (three numbered cards), A little about me, Selected work (four rows, no status), Writing (the two newest essays) beside the Now panel. No testimonial on Home. When a new essay is added, it replaces the older of the two on Home.
- **Work:** H1 and intro, At Select Soccer Club (five case studies), Earlier, in software (two columns), Greg Goodson pull quote.
- **Playbook & AI:** header, stat row (63 · 6 · 10 · 30+), four cards, Anatomy of a play beside the sample play, Plays that run as skills, How it stays current (five numbered cards), then The workspace behind it and Guardrails I build in as two grey panels.
- **Writing:** H1 and intro, then the essay list (date and topic left, title, summary, Read →).
- **Essay:** ← All writing, topic · month · read time, title, summary line (the same one as in the Writing list), short accent rule, body, author note, Keep reading (the next older essay; the oldest links back to the newest).
- **About:** H1, lead, intro, photo; How I work (six principles, `#how-i-work`, linked from Home); Experience; Kind words; Outside work with the milestone stat row and closing quote.

## Positioning
"I build the systems underneath revenue and operations: the CRM, the data, the automation, and the reporting that tells you what's actually working."
The site is a record of how Dave works and what he's learning: the systems he's built, the principles behind them, and his thinking on practical AI. A reader should come away understanding what he does and who he is as a person.

## Voice
First person, plain-spoken, calm, and warm, with real empathy for the people who use the systems. No hype. **No em dashes.**

## Case study formats
- **Select:** a summary row (title, one line, and "Status: **...**" as plain text on the right), then four cards (The problem / What I built / What it changes / Built to hold up, the last one dark), then Tools.
  - "Built to hold up" describes lasting design choices (safeguards, rules, structure), not progress, so it shouldn't need updating as projects change. Don't add progress or "where it stands" lines back.
- **Software (TrainingPeaks, Rafflecopter):** The project (or approach) / What it took (or built) / The result. These results are verified.
- **Status** is plain text (`<p class="status">Status: <strong>Live</strong></p>`), not a colored badge. Only three, so they change only when a project moves to a new stage. Status shows on the Work page only, never on Home.

| Status | Meaning |
| --- | --- |
| Live | In regular use |
| Partly automated | In use; some steps run on their own, the rest are still manual |
| In development | Still being built or tested |

## Writing
- Essays live in `docs/writing/`, one HTML file each, named from the title (`the-club-platform-i-keep-sketching.html`).
- To add one: copy an existing essay page, replace the content inside `<article class="article essay">` (keeping its `<header>` and author note), update the topic, date, read time (about 230 words a minute), title, summary line, `<title>`, and meta description. Then add a `<li>` to the top of the list in `docs/writing/index.html` (newest first), update the Writing section on Home, and fix the Keep reading links so they still run from newest to oldest.
- Optional essay blocks are styled and ready: a definition callout (`<aside class="callout"><p class="callout-label">Definition</p><p>...</p></aside>`) and a pull line (`<blockquote class="pull-line">`). Quotes from other writers stay ordinary blockquotes.
- Dates show month and year only ("November 2026"), on the essay page and in the Writing list. No exact days.
- Essay titles capitalize every major word (title case). Case study titles on the Work page stay in sentence case.
- Essays keep Dave's wording. Only fix what he asks for, plus em dashes (none allowed). A diagram from a private artifact gets redrawn on the page, since visitors can't open his artifacts.
- The architecture diagram in "The Club Platform I Keep Sketching" is plain HTML and CSS (`.arch` styles in `style.css`), redrawn from Dave's "Club data core architecture" whiteboard.
- The foundation diagram in "Reading Club Software's Future From Outside the Club" is an inline SVG (`.leap` styles in `style.css`), redrawn from the diagram in Dave's draft. Its table uses `.essay-table`.

## Design
"Field Notes" (November 2026; the handoff and approved mockups are in `design/field-notes/`, which isn't published). White page, near-black ink, one burnt-orange accent (`--accent` #c2410c), Space Grotesk headings over Inter body text, loaded from Google Fonts.
- Personality comes from the voice first, then one signature accent: a hand-drawn SVG underline under one key word (Home: "Dave"). At most once per page, `aria-hidden`.
- Content is 1120px wide with 24px side padding (16px on phones); essays are a 720px column at 19px.
- Lists of items use a 2px ink top rule, then thin `--line` dividers. Cards have a 1px border and 16px corners; the emphasized card in a sequence is filled dark with orange numbering. Numbered steps read 01, 02, 03 with a → between cards on wide screens.
- Small uppercase "eyebrow" labels (13px, bold) name sections. Grey `--surface` panels hold the Now panel, testimonials, and Playbook panels.
- Interaction only when it's useful: links and anchors, no decorative animation or scroll effects. Not salesy: no service menus or hard-sell calls to action.
- Every multi-column row wraps or stacks on phones; check at 390px, 768px, and 1280px.

## Open items
- **Home photo:** Dave to supply a photo of himself running or riding on a road or trail. Replace the `.photo-placeholder` div in `docs/index.html` with an `<img>` (full width, 380px tall, 20px corners).
- **Custom domain:** finish GitHub's Pages settings (step 3 below).
- **Optional:** a short Avid4 Adventure or Bonusly case study to cover 2017 to 2023.

## Custom domain (in progress)
davecriswell.com is registered with Squarespace Domains. Steps 1 and 2 are done (DNS moved off the old WordPress site in November 2026, and the GitHub Pages domain-verification TXT record added). The steps:
1. In Squarespace Domains, point the domain's DNS at GitHub Pages (the A records for the root domain, plus a `www` CNAME record pointing to `davecriswell.github.io`).
2. Add `docs/CNAME` with one line: `davecriswell.com`. Do this only once the DNS records are in place; adding it earlier sends visitors to a domain that doesn't reach the site yet.
3. Set the domain in the repository's Settings → Pages, turn on "Enforce HTTPS" once GitHub has issued the certificate, and verify the domain under the account's Pages settings.
4. After the move, old github.io links redirect to davecriswell.com automatically.

## Public-content rules (this repository is public)
- Select Soccer Club can be named. Write about Select with respect: describe challenges as the natural ones of a growing club, and credit the club for the work it supported. Never criticize people or the club.
- Playbook counts are approved for public use: 63 plays, 6 areas, 10 run as skills.
- Call the registration platform "the club's registration platform." Don't name it.
- No colleague, staff, coach, family, or player names.
- No revenue, staff counts, internal metrics, pacing or retention figures, or vendor-selection details (for example, how many CRMs were evaluated).
- No phone number, home address, or location. Running and riding copy says "the roads and trails near home."
- Badges and "Built to hold up" lines describe the work, never the people who did or didn't use it.
- Keep the closing line as it is: an open invitation to talk systems, operations, practical AI, or youth sports.
- Nothing that suggests a job search.
- Only publish projects and past work Dave has approved for public use. Ask Dave before adding anything else.
- The private source brief lives in Dave's Google Drive ("dave-criswell-website-brief.md"). Never copy it into this repository.
