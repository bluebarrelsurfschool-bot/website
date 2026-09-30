# Blue Barrel Surf School: site redesign

Code for the redesigned pages of https://www.bluebarrelsurf.co.uk (Squarespace 7.1).
Work happens on branch `claude/blue-barrel-redesign-twaojg`.

## How the pages are built

- **`custom-css.css`** is one shared stylesheet, pasted at the bottom of
  Website > Website Tools > Custom CSS, between the `BLUE BARREL REDESIGN: START` and `END` markers.
  Every page's styles live here, scoped under `.bb`. When a page needs new styles, add them here
  and the user replaces the whole section.
- **One `.html` file per page**, pasted into a single Code Block (HTML mode, Display Source unticked),
  alone in its own Squarespace section. It holds only the Google Fonts link, the markup, JSON-LD and scripts.
- **Don't put a `<style>` block in the page files.** It was lost every time the user pasted, which is why
  all styling moved to Custom CSS.
- Squarespace Custom CSS is compiled as LESS. Wrap `calc()` and `min()` in `~"..."`, use longhand
  `font-*` properties (no `font:` shorthand with `/`), avoid `/` in values such as `grid-column:1 / -1` (old LESS divides it; use `span 2`), and check it compiles with both `less@1.7.5` and `less@4`.

## Design rules

- Colours (CSS variables on `.bb`): ink #0A2A3B, mute #4A6472, line #B9CFD0, sea #0F5C7A, deep #082638,
  sun #FFC24A (buttons), panel #DCEBEA, bg #EAF2F1, h1 #FFFFFF (white; was orange #F15A29).
- Headings h1–h3 use the site's own font `'Blue'` (Hello-Handmade Sans, loaded by an `@font-face` already in
  the user's Custom CSS). It's weight 400 only, and the font renders in capitals. Sentence case in the HTML.
- Body: Figtree 17px. Extra display text (price figure, FAQ questions): Bricolage Grotesque 800.
- Hero is a `<div class="hero">` (never `<header>`), with a photo, dark gradient, h1, paragraph, yellow `.btn`,
  outlined `.btn.ghost` and three `.facts`.
- Sections alternate bg / `.alt` or `.price` (panel), ruled lists with a 2px ink top border, 14px photos,
  `.tags` or `.tag` blue outlined pills, `.bp` sea band, `.dark` navy band. One memorable element per page.
- Mobile hero is tightened under 760px (see the media query in `custom-css.css`).

## Shared script (copy into every page)

`headBottom()` + `flush()` sit `.bb` exactly under the visible header bar (Squarespace's `#header` can report
0 height, so it measures `.header-announcement-bar-wrapper` / `.header-inner` too). Handles both a gap and an
overlap, and re-runs on load, on resize and at 600ms and 1500ms. Manual override: `--bb-pull` in Custom CSS.

## SEO rules

- One h1, then h2 and h3 with no skipped levels. Keyword-rich headings, descriptive link text.
- JSON-LD on every page: the same `SportsActivityLocation` business object (see `surf-lessons.html`),
  plus `FAQPage` generated from the page's own `<details>` text. No review-rating schema unless reviews are verified.
- Prices and FAQs are written in HTML, not built by JavaScript. No `<form>`, no localStorage.

## Business facts

- Email bluebarrelsurfschool@gmail.com, phone 07572 526698 (+447572526698).
- Booking: https://app.vikingbookings.com/widget/booking/b401000001000000e56b5529
- 2-hour private lessons, all equipment included, from age 5 with a parent or guardian in the water.
- Price: £100 for 1, +£30 per extra person up to 8 (totals 100/130/160/190/220/250/280/310;
  per person rounded 100/65/53/48/44/42/40/39). You pay the total.
- Times: Nov–Mar 10am and 1pm; Apr–Oct 10am, 1pm, 4pm, plus optional 6pm sunset.
- Main bases: South Fistral (sheltered from S/SW winds by cliffs) and St Ives Bay (Gwithian; Porthkidney,
  sheltered by the St Ives headland). Also Perran Sands, Marazion, Perranuthnoe, Praa Sands.
- ISA-qualified instructors, 75+ five-star reviews. Socials: Instagram and TikTok @bluebarrelsurf, Facebook,
  TripAdvisor (listed in Hayle), LinkedIn (links are in the schema in `surf-lessons.html`).
- Photos: images.squarespace-cdn.com/content/v1/64ea4b114e8ebf6aced48b0e/... (see the page files).

## Status

| Page | File | State |
|---|---|---|
| Surf Lessons | `surf-lessons.html` | Live and checked on desktop and mobile |
| Our Locations | `our-surf-lesson-locations.html` | Live; beach wind directions still need owner's check |
| Group Surf Lessons | `group-surf-lessons-cornwall.html` | Built; groups of 9–16 priced on request (owner to confirm) |
| About | `about.html` | Built; confirm whether Jack is the only instructor |
| Home | `home.html` | Built; old page had no h1 and mixed /our-locations links |
| Contact Us | `contact-us.html` | Built; old Form Block dropped (optional: add one in its own section below) |
| Terms and Conditions | `terms-conditions.html` | Built; clause wording kept exactly as the old page (owner to confirm clause 1.1) |
| The Blueprint, Gift Vouchers, Blog | – | To do |

Open items: new pages are built on disabled test pages (General > Enable page off). On swap day the user renames the old
page's slug (e.g. `surf-lessons-old`), gives the new page the real slug, SEO title and description, enables it, and adds a 301 from
the test URL in URL Mappings. The homepage is swapped with "Set as homepage". An Instagram Block can sit in its own section below the
home Code Block if the user wants the live feed. Hayle as the base town in the schema isn't confirmed.
Beach-specific photos are wanted for Perran Sands, Marazion, Perranuthnoe and Praa Sands.

## SEO settings per page (Squarespace: page gear icon > General and SEO)

| Page | URL slug | Nav title | SEO title | SEO description |
|---|---|---|---|---|
| Home | (homepage) | Home | Blue Barrel Surf School \| Private Surf Lessons in Cornwall | Cornwall's mobile private surf school. Tailored surf lessons for beginners to intermediates at Fistral, Gwithian and more. ISA-qualified, all kit included. |
| Surf Lessons | `surf-lessons` | Surf Lessons | Private Surf Lessons in Cornwall \| Blue Barrel Surf School | Private 2-hour surf lessons in Cornwall for beginners, improvers and families. £100 for one, plus £30 per extra surfer. All kit included. Book online. |
| Our Locations | `our-surf-lesson-locations` | Our Locations | Surf Lesson Locations in Cornwall \| Blue Barrel Surf School | Private surf lessons at Newquay's South Fistral, Gwithian and Porthkidney in St Ives Bay, Perran Sands, Marazion, Perranuthnoe and Praa Sands. |
| Group Surf Lessons | `group-surf-lessons-cornwall` | Group Lessons | Group Surf Lessons in Cornwall \| Stag, Hen & Team Days | Private group surf lessons in Cornwall for stag and hen parties, corporate team days and birthdays. Up to 16 people, all kit included, no experience needed. |
| About | `about` | About | About Blue Barrel \| Private Surf Coach in Cornwall | Meet Jack, founder of Blue Barrel Surf School: ISA-qualified, RLSS lifeguard trained and insured, offering private mobile surf lessons across Cornwall. |
| Contact Us | `contact-us` | Contact | Contact Blue Barrel Surf School \| Surf Lessons Cornwall | Call 07572 526698 or email Blue Barrel Surf School about private surf lessons, group bookings and gift vouchers in Cornwall, or book your lesson online. |
| Terms and Conditions | `terms-conditions` | Terms | Terms and Conditions \| Blue Barrel Surf School | Booking terms for Blue Barrel surf lessons in Cornwall: 48-hour cancellation and refund policy, weather cancellations, swimming ability and under-18 rules. |

## Working notes for the next session

- This environment can't fetch bluebarrelsurf.co.uk or static1.squarespace.com, and it can't load images from
  images.squarespace-cdn.com either. The user uploads each current page saved as "Webpage, HTML only". Extract the text,
  links and image URLs from `<main>` with a small Python script.
- Build each page as `<slug>.html`, reusing the shared header script and business schema from `surf-lessons.html`, and generate
  the FAQPage JSON-LD from the page's own `<details>`. Add any new CSS to `custom-css.css`, compile it with both LESS versions,
  render it in Playwright (Chromium at /opt/pw-browsers/chromium) at 390px and 1280px, then send the user the page file and,
  if it changed, custom-css.css. The user replaces the whole Blue Barrel section in Custom CSS each time.
- Hero headings are white (`--h1`). `.hero.fit` (plus an `img.fill` copy) shows the whole photo on desktop; it's used on About.
- Reviews on Home are real customer quotes (Harley, Richard, Tom, Edward). Keep their wording and fix only spelling.
- Keep Squarespace in mind: every Code Block sits alone in its own section, and scripts don't run inside the editor.
- Give the SEO title (60 characters or fewer) and description (about 150–160 characters) for every page, and add them to the table above.
