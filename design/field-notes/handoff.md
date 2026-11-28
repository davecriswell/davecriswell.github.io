# davecriswell.com Field Notes: Claude Code Handoff

November 2026 · Dave Criswell

## How to use this doc

This doc lives in the repo at `design/field-notes/handoff.md`, with the six approved mockups in `design/field-notes/mockups/`, on the `field-notes-handoff` branch. That folder is outside `docs/`, so GitHub Pages never publishes it. Start a Claude Code session on that branch and paste the prompt below. The mockups are reference files from the Field Notes Site design canvas; they don't run on their own.

```markdown
You're redesigning my personal site into the "Field Notes" design.

First run git pull, and follow CLAUDE.md throughout. Work on the field-notes-handoff branch, not main, so nothing goes live until I merge it.

Read design/field-notes/handoff.md in full before changing anything. The files in design/field-notes/mockups/ are the approved mockups: match their layout, type, and spacing, but build clean HTML and CSS in docs/ and docs/style.css, not their inline-style markup. Where a mockup and the handoff differ, the handoff wins. Where the handoff conflicts with CLAUDE.md's public-content rules, CLAUDE.md wins.

Work in this order:
1. Inventory the current site: list every page, section, and piece of copy, and map each one to the new page specs. Show me that map and wait for my OK.
2. Build the shared styles (tokens in docs/style.css, header, contact band, footer) and the Home page. Stop so I can review it.
3. Build Work, Playbook & AI, Writing, the essay template (apply it to all three essays), and About.
4. Update CLAUDE.md's Design, Page structure, and Case study format sections to describe the new design.
5. Run the acceptance checklist at the end of the handoff and report back in plain language.

Rules: reuse my existing copy word for word unless the handoff gives new copy. Never invent stats, quotes, or results. No em dashes anywhere. Keep it plain HTML and CSS with no build step.
```

## Goal and audience

The site should leave a visitor understanding what Dave brings as a person, colleague, and friend, not a menu of services. Readers are people who might work with Dave: organizations, partners, and club leaders.

- **First impression:** a sharp, knowledgeable, empathetic person who sees the big picture and turns that insight into meaningful work, from personal interactions to complex business solutions.
- **Personality comes from voice first**, then one signature visual accent: the hand-drawn underline in burnt orange.
- **Don't Make Me Think (Steve Krug):** scannable, obvious navigation, short paragraphs, no walls of text.
- **Not salesy:** no service menus, no hard-sell calls to action, no testimonials on Home.
- **Interaction only when it's useful:** links and anchors yes; decorative animation, parallax, and scroll effects no.
- **Discreet:** nothing on the site suggests a job search.
- **Honest about status:** every case study states how far along it is, as plain text.

## Design system

White page, near-black ink, one burnt-orange accent, Space Grotesk headings over Inter body. Set these as CSS custom properties in `:root` in `docs/style.css` and use nothing else.

**Color**

| Token | Value | Use |
| --- | --- | --- |
| `--ink` | #111418 | Headings, primary text, dark sections |
| `--text` | #3a4048 | Body copy |
| `--body-long` | #1f242a | Article body text |
| `--muted` | #5b636d | Labels, dates, captions |
| `--line` | #e6e8eb | Dividers, card borders |
| `--surface` | #f6f7f8 | Panels (Now, callouts, testimonials) |
| `--placeholder` | #eef0f2 | Image placeholders |
| `--accent` | #c2410c | Underline, numbers, active nav, text links |
| `--accent-link` | #b8430a | Default link color |
| `--accent-on-dark` | #ff8a4c | Accent on the dark contact band |
| `--dark-muted` | #c4c9cf | Body text on dark |
| `--footer` | #8b939c | Footer text on dark |

**Type**

| Role | Font | Size | Weight / tracking |
| --- | --- | --- | --- |
| Home H1 | Space Grotesk | clamp(46px, 7vw, 92px), line-height 0.98 | 700, -0.04em |
| Page H1 | Space Grotesk | clamp(44px, 6vw, 80px), line-height 1 | 700, -0.04em |
| Home subline | Space Grotesk | clamp(22px, 2.6vw, 30px) | 500, -0.015em |
| H2 section | Space Grotesk | 32 to 48px | 700, -0.03em |
| H3 / row title | Space Grotesk | 22 to 26px | 700, -0.02em |
| Body | Inter | 17 to 18px, line-height 1.6 | 400 |
| Article body | Inter | 19px, line-height 1.75, about 66ch column | 400 |
| Eyebrow label | Inter | 13px, uppercase | 700, 0.1em |

Load both from Google Fonts (Space Grotesk 500/600/700, Inter 400/500/600/700).

**Layout and components**

- Content container: max-width 1120px, 24px side padding. Article column: max-width 720px.
- Section rhythm: 64 to 88px vertical padding. Lists of items use a 2px ink top rule, then 1px `--line` dividers between rows.
- Cards: 1px `--line` border, 16px radius, 22 to 26px padding. The emphasized card in a sequence is filled `--ink` with `--accent-on-dark` numbering.
- Numbered steps: "01, 02, 03" in Space Grotesk 700, accent color, with a "→" between cards on wide screens.
- Buttons: 52px min height, 12px radius. Primary is `--accent-on-dark` fill on dark sections; secondary is a 1px outline.
- **Signature accent:** a hand-drawn SVG underline under one key word (Home: "Dave"). Use it once per page at most, `aria-hidden`.
- Responsive: every multi-column row is flex-wrap or auto-fit grid and stacks to one column on phones. Test at 390px.
- Accessibility: semantic landmarks, real links, `aria-current="page"` on the active nav item, 4.5:1 contrast, 44px touch targets.

## Site map and shared elements

Six templates, same URLs as today so existing links keep working.

| Page | URL | File | Template |
| --- | --- | --- | --- |
| Home | `/` | `docs/index.html` | Home |
| Work | `/work/` | `docs/work/index.html` | Index of case studies |
| Playbook & AI | `/playbook/` | `docs/playbook/index.html` | Long-form case study |
| Writing | `/writing/` | `docs/writing/index.html` | Post index |
| Each essay | `/writing/<slug>.html` | `docs/writing/<slug>.html` | Article |
| About | `/about/` | `docs/about/index.html` | About |

**Nav (every page):** wordmark "Dave Criswell." (period in accent) links Home; then Work · Playbook & AI · Writing · About · **Say hello** (accent, links to `#contact`). Active page in accent, weight 700. Bottom border 1px `--line`. Wraps on phones; no hamburger needed. Keep the existing sticky behavior and `scroll-margin-top` described in CLAUDE.md.

**Contact band (every page, `id="contact"`, the anchor the site uses today):** dark `--ink` section. H2 "Say hello." with "hello." in `--accent-on-dark`. Line: "I'm always up for a conversation about systems, AI, youth sports, or a good trail." Buttons: **Email me** (`mailto:davecriswell@gmail.com`) and **LinkedIn** (`https://www.linkedin.com/in/davecriswell/`, opens in a new tab).

**Footer:** on the same dark ground: "© 2026 Dave Criswell · Built with Claude Code". Keep the skip-to-content link the site has now.

## Page specs

Sections run top to bottom in the order listed. Copy in quotes is approved new copy; use it as written.

### Home (`/`)

1. **Hero**, two columns that stack on phones.
   - Left: H1 "Hi, I'm Dave." with the hand-drawn underline under "Dave" (accent). Subline: "Systems builder. Former coach. Endurance athlete. Curious about how things work for the people who use them."
   - Right: "Most of my career has been in software marketing and operations. For the past three years I've built operations for a youth soccer club and figured out where AI actually helps." Then: "Away from the desk, I'm usually running or riding the roads and trails near home."
2. **Photo**, full container width, 380px tall, 20px radius: Dave running or riding on a road or trail. Placeholder until Dave supplies it.
3. **How I think**, eyebrow label, then three numbered cards joined by arrows (third card dark):
   - 01 "See the whole field." "Systems first, then the tool. Every handoff and every person, before touching anything."
   - 02 "Find where it breaks." "Meet people where they already work, and show the math. Where they get stuck is the map."
   - 03 "Build what gets used." "Start small, then scale. Write it down so it holds up without me."
   - Link: "All six principles →" to About.
4. **A little about me**, H2, then two columns:
   - "How I show up": "I'm a calm presence, and I think first about the people on the other end of a system: the coach, the parent registering a kid, the director who needs one number they can trust." / "About ten years of coaching soccer shaped the rest. Set people up to succeed, watch closely, adjust with patience. I still work that way."
   - "What I like to work on": "Work that starts as a messy manual process and ends as a system people actually use. And I'll always tell you exactly where it stands." Link "Selected work ↓".
5. **Selected work**, eyebrow plus "All work →". Four rows, each: org label (150px column), title, one line. **No status chips or badges here.**
   - Select · The Select Playbook · "Club operations documented as 63 repeatable plays. Ten run as AI skills." → `/playbook/`
   - Select · A data foundation for a platform with no API · "One trusted source of registration data for reports and internal tools." → `/work/#data-foundation`
   - Select · A lead-to-enrollment funnel · "Every interested family gets a quick response and a clear path to registering." → `/work/#lead-funnel`
   - TrainingPeaks · A 500,000-contact migration · "Email revenue tripled in six months, against a twelve-month goal." → `/work/#trainingpeaks`
6. **Writing + Now**, side by side.
   - Writing (wide): the two most recent essays, each with topic · month, title, one-line summary; "All writing →".
   - Now panel (`--surface`, "Updated November 2026"): "Exploring where practical AI helps youth sports clubs, and where it's hype" · "Writing about club software and where it's headed" · "Running and riding the roads and trails near home". Divider, then **1.95 Ironman triathlons.** "I learned the most from the 0.05 I didn't finish."
7. Contact band and footer. **No testimonial on Home.**

### Work (`/work/`)

1. Header: H1 "Work" beside "Each case study covers the problem, what I built, and what it changes. I'd rather tell you exactly where something stands, so every project says how far along it is."
2. **At Select Soccer Club** ("2023 to now"), five case studies, each keeping its anchor. Summary row: title, one-line summary, then a side column with "Status: **Live / Partly automated / In development**" as plain text. Data foundation and Lead funnel: Partly automated. Schedule PDFs to shifts and Game-report system: Live. Dashboard that can show its math: In development, linking to its essay. Keep each case study's full content (The problem / What I built / What it changes / Built to hold up / Tools) below its summary, restyled with the card components.
3. **Earlier, in software** ("2011 to 2023"), two-column grid: TrainingPeaks 500,000-contact migration; Rafflecopter personas, lifecycle stages, and KPIs. Keep their full content.
4. **Pull quote**: Greg Goodson, Co-Founder, Rafflecopter, with "a firm grasp of the emotional side of our customers" highlighted in accent. Use his full quote from the current site.

### Playbook & AI (`/playbook/`)

1. Header: eyebrow "Playbook & AI", H1 "The Select Playbook", the current intro.
2. **Stat row** with a 2px rule: 63 plays (accent) · 6 areas · 10 run as AI skills · 30+ years.
3. **Four cards**: The problem · What I built · What it changes · Built to hold up (last one dark).
4. **Anatomy of a play** (8 numbered parts, two-column grid) beside a **sample play card**: "Game results dashboard", "Live · runs as a skill".
5. **Plays that run as skills**: the listed skills as a two-column divided list.
6. **How it stays current**: the 5-step cycle as numbered cards, last one dark.
7. **The workspace behind it** and **Guardrails I build in**, as two `--surface` panels.

### Writing (`/writing/`)

1. Header: H1 "Writing" beside "Notes on systems, operations, and practical AI. Short pieces that show how I think through a problem."
2. Essay list, newest first, 2px top rule: left column month and year plus topic; right column large title (clamp 26 to 36px), one-line summary, "Read →".

### Article template (`/writing/<slug>.html`)

1. "← All writing", then topic · month and year · read time, H1, a 21px dek, a short 64px accent rule.
2. Body at 19px in the 720px column, H2s at 28px. Supported blocks: a `--surface` definition callout with an accent eyebrow, and a pull line in Space Grotesk 30px.
3. Author note: small avatar plus "Dave Criswell builds the systems behind operations and revenue, and spends his free time on the roads and trails near home."
4. "Keep reading" link to the next most recent essay, then contact band.
5. Apply it to all three existing essays: "Reading Club Software's Future From Outside the Club", "A Dashboard That Can Show Its Math", and "The Club Platform I Keep Sketching". Keep each essay's diagram and table styles (`.arch`, `.leap`, `.essay-table`).

### About (`/about/`)

1. Header: H1 "About", then the 24 to 28px lead "A New Englander with a calm temperament, who thinks first about the people on the other end of a system." and the current intro paragraphs, beside the existing photo (`docs/images/dave.jpg`).
2. **How I work**: all six principles as numbered cards in a three-column grid, with their current descriptions.
3. **Experience**: a divided timeline (years column, then org and role), linking to LinkedIn. Use the current Experience content.
4. **Kind words**: the three current testimonials as `--surface` cards.
5. **Outside work**: one line, then the milestone stat row (1.95 Ironman triathlons · 6 Half Ironmans · 5 marathons · 1 ultramarathon) and the closing quote.

## Content rules and placeholders

The mockups use [brackets] where the exact wording lives on the current site. Fill every one from the existing pages, word for word. Never write new copy to fill a gap; flag it instead.

| Placeholder in mockup | Fill from |
| --- | --- |
| Playbook: 8 parts of a play | Current Playbook "Anatomy of a play" |
| Playbook: sample play summary and parts | Current "Game results dashboard" sample play |
| Playbook: 5-step update cycle | Current "How it stays current" |
| Playbook: 5 workspace decisions, 6 guardrails | Current "The workspace behind it" and "Guardrails I build in" |
| About: six principle descriptions | Current "How I work" section |
| About and Work: testimonial quotes | Current "Kind words", full quotes, unedited |
| Article: body, read time | Each existing essay |
| Home photo | Dave supplies; keep a labeled placeholder until then |

**Rules**

- The repo's CLAUDE.md public-content rules always apply: no location, no colleague names, the registration platform stays unnamed, nothing that suggests a job search.
- No em dashes anywhere, in copy or in code comments that render.
- No invented numbers, quotes, results, or dates.
- Case-study status stays honest and matches the current Work page.
- Outside links open in a new tab (`target="_blank" rel="noopener"`), as CLAUDE.md describes.
- Dates show month and year only, newest first.
- Copy approved in this doc replaces the old version; everything else keeps its current wording.
- Keep "Built with Claude Code" in the footer.

## Done means

The build is done when every box below is checked and Claude Code has reported back.

- [ ] All six templates built and every existing page and essay moved onto them, at its current URL
- [ ] Home matches the approved copy exactly; no chips in Selected Work, no testimonial on Home
- [ ] Every [bracket] filled from the current site, or listed as missing
- [ ] Colors, fonts, and sizes come only from the tokens in this doc
- [ ] Pages checked at 390px, 768px, and 1280px; nothing overflows and every row stacks
- [ ] Lighthouse accessibility score of 95 or higher on Home and one essay
- [ ] No broken internal links; nav marks the active page; case-study anchors still work
- [ ] A search of the site finds no em dashes
- [ ] CLAUDE.md updated to describe the new design

**Report back with:** a page-by-page list of what changed, any copy that couldn't be placed, the placeholders still waiting on Dave (photo), and screenshots of Home at phone and desktop widths.
