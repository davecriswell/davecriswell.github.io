# davecriswell.com

Dave Criswell's personal website. Plain HTML and CSS, no build step, hosted on GitHub Pages.
Dave is new to development and uses this project to learn Claude Code and GitHub, so explain changes in plain language.

## Files
GitHub Pages publishes only the `docs/` folder. Files outside it (like this one) stay off the website but are still public on github.com.

| Page | File | URL |
| --- | --- | --- |
| Home | `docs/index.html` | `/` |
| Work | `docs/work/index.html` | `/work/` |
| Playbook & AI | `docs/playbook/index.html` | `/playbook/` |
| About | `docs/about/index.html` | `/about/` |
| Writing (not linked yet) | `docs/writing/index.html` | `/writing/` |
| Essay (not linked yet) | `docs/writing/a-dashboard-that-can-show-its-math.html` | |

- `docs/style.css` holds every style. Colors, fonts, and status-badge colors are tokens at the top in `:root`.
- Every page links styles and pages with root paths (`/style.css`, `/work/`), which work on github.io and on a custom domain.
- **The header and footer are repeated on every page.** If you change one, change it on all six pages.
- The header is sticky: it stays pinned to the top while scrolling. `[id] { scroll-margin-top }` in `style.css` keeps anchor links from landing under it; if the header gets taller, raise that value.
- The About photo is `docs/images/dave.jpg` (556 x 695, cropped so only Dave is in frame; shown at 280px wide on desktop, 220px on phones). To change it, replace that file and update the `width`/`height` on its `<img>` tag in `docs/about/index.html`.
- Menu: Work · Playbook & AI · About · Contact. Contact jumps to the footer (`#contact`) on the current page.
- Each case study has an anchor so one example can be linked directly: `#data-foundation`, `#lead-funnel`, `#shift-imports`, `#game-reports`, `#pacing-dashboard`, `#trainingpeaks`, `#rafflecopter`.

## Page structure
- **Home:** intro, Selected work, How I work.
- **Work:** case studies, Select first, then earlier software work.
- **Playbook & AI:** the Select Playbook and the Claude workspace behind it.
- **About:** bio, Experience, Kind words, Outside work, closing quote.

## Positioning
"I build the systems underneath revenue and operations: the CRM, the data, the automation, and the reporting that tells you what's actually working."
The site is a record of how Dave works and what he's learning: the systems he's built, the principles behind them, and his thinking on practical AI. A reader should come away understanding what he does and who he is as a person.

## Voice
First person, plain-spoken, calm, and warm, with real empathy for the people who use the systems. No hype. **No em dashes.**

## Case study formats
- **Select:** The problem / What I built / What it changes / Built to hold up / Tools, with a status badge beside the title.
  - "Built to hold up" describes lasting design choices (safeguards, rules, structure), not progress, so it shouldn't need updating as projects change. Don't add progress or "where it stands" lines back.
- **Software (TrainingPeaks, Rafflecopter):** The project (or approach) / What it took (or built) / The result. These results are verified.
- **Status badges** (`<span class="badge" data-status="...">`). Only three, so they change only when a project moves to a new stage:

| Badge | data-status | Meaning |
| --- | --- | --- |
| Live | `live` | In regular use |
| Partly automated | `partial` | In use; some steps run on their own, the rest are still manual |
| In development | `dev` | Still being built or tested |

## Design
Inspired by m3ka.com (warm off-white, serif headings, typewriter-style labels, thin rules) and chester.how (a large serif intro with key words highlighted). No playful toggles for now.

## Open items
- **Writing:** the Writing page and essay are built but not linked, and marked `noindex`. Once Dave rewrites the essay in his own words: remove the draft note and `noindex`, link it from the pacing case study on the Work page ("Read the story behind the rebuild →"), and add Writing to the menu on every page.
- **Custom domain:** move the site to davecriswell.com (see "Custom domain" below).
- **Optional:** a short Avid4 Adventure or Bonusly case study to cover 2017 to 2023.

## Custom domain (planned, not done yet)
The site still lives at davecriswell.github.io. davecriswell.com is registered with Squarespace Domains and still points to the old WordPress site. The plan for the move:
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
