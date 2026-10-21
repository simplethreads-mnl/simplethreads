# Build this site for Vercel: Simple Threads

You are an expert creative front-end developer. Produce a **single self-contained `index.html`**
that reproduces the project below **exactly** — same layout, sections, copy, palette, type, and
motion. Pure HTML/CSS/JS in one file: **no build step, no framework, no bundler.** Use ES modules
with CDN imports for the two libraries used (Lenis for smooth scroll; optionally GSAP for the
scroll-scrub parallax). Load fonts from CDN. Hardcode every value given here as a fixed constant —
all copy is verbatim, all colors are exact hex, all sizes are the literal rem/px below. Rebuild each
section described below as a labeled block of the one file.

> **Deployment target: Vercel.** Ship a static site: `index.html` at the project root plus the six
> photos in `/images/` (uploaded with this prompt — see Assets). No framework or build step is needed;
> if your tool insists on one, use Next.js with this page as a single static route and the photos in
> `/public/images/`. Business details below are final — no placeholders. There are **no social media
> links** anywhere on the site.

## What it is

A hushed, monochrome **editorial portfolio one-pager** for **Simple Threads**, an apparel
manufacturing and design studio based in **Manila, Philippines**. The studio helps clothing brands go from idea to finished
garment: **design assistance**, sampling, and production of **shirts, hoodies, long sleeves, polos,
jackets, caps, beanies, and lanyards**, printed by **DTF, DTG, silk screen, sublimation**, or finished with **embroidery**. It serves
brands, teams, schools, events, and anyone with an idea. There is **no minimum order**;
pricing is tiered by quantity, so the more pieces ordered, the lower the price per piece.
The page doubles as a lookbook of brands the studio has designed and manufactured for — dark
streetwear tees with white back prints, shot in moody black-and-white.

Large serif (Playfair Display) display headings against a clean Satoshi sans body; a fine
dashed-hairline grid; lots of negative space; black-and-white photography. The whole page is
long-scroll with **spring-based reveals** — headings reveal line-by-line (clipped slide-up), body
copy fades in word-by-word, image plates rise with a faint scale-settle and drift with parallax.
**Lenis smooth scroll** glides the whole page. Two full-viewport dark "pinned" CTA blocks punctuate
the flow, and a full-screen modal menu grows down from the top edge. Strictly black/white/grey — no
color accent anywhere. All portfolio photos should be displayed **grayscale**
(`filter:grayscale(1)` on every `<img>`) so color casts in the source shots don't break the palette.

## Page shell & libraries

- **Fonts (CDN):**
  - Body / UI sans — **Satoshi** via Fontshare:
    `https://api.fontshare.com/v2/css?f[]=satoshi@400,500,700,900&display=swap`
    (weights used: 400 regular, 500 medium, 700 bold, 900 black).
  - Display serif — **Playfair Display** via Google Fonts, normal + italic, weight 400:
    `https://fonts.googleapis.com/css2?family=Playfair+Display:ital@0;1&display=swap`
- **Smooth scroll — Lenis** via CDN ESM, e.g.
  `import Lenis from "https://cdn.jsdelivr.net/npm/lenis@1.3.19/+esm"`. Init with
  `{ smoothWheel: true }`, drive it from a `requestAnimationFrame` loop (`lenis.raf(time)`). When the
  modal menu is open, call `lenis.stop()` and lock native scroll (`html { overflow:hidden; height:100%; position:relative }`); on close call `lenis.start()` and remove those styles.
- **(Optional) GSAP + ScrollTrigger** via CDN only for the portfolio scroll-scrub parallax. If
  you prefer no extra lib, drive parallax from the Lenis scroll callback by mapping each plate's
  viewport progress to a `translateY` (math below).
- **CSS reset:** box-sizing border-box; remove default margins; `img { display:block; max-width:100% }`;
  `body { -webkit-font-smoothing:antialiased; text-rendering:optimizeLegibility; overflow-x:hidden }`.
- **Background / base:** `body { background:#ffffff; color:#191917; font-family:"Satoshi",sans-serif; }`.
- **Headings:** `h1,h2,h3 { font-family:"Playfair Display",serif; font-weight:400; text-transform:none;
  letter-spacing:-0.01em; line-height:1.12; }`.
- **Selection:** `::selection { background:#191917; color:#ffffff; }`.
- **Rem-based adaptive grid (IMPORTANT).** Replicate these exact media queries:
  ```css
  html { font-size: 16px; }
  @media (max-width: 1920px) { html { font-size: 0.833333vw; } }
  @media (max-width: 1440px) { html { font-size: 1.111111vw; } }
  @media (max-width: 1024px) { html { font-size: 1.5625vw;  } }
  @media (max-width: 640px)  { html { font-size: 4.444444vw; } }
  ```
  Use Tailwind-style rem sizing: `text-xs`=0.75rem, `text-sm`=0.875rem, `text-base`=1rem,
  `text-lg`=1.125rem, `text-xl`=1.25rem, `text-2xl`=1.5rem, `text-3xl`=1.875rem, `text-4xl`=2.25rem,
  `text-5xl`=3rem, `text-6xl`=3.75rem, `text-7xl`=4.5rem, `text-8xl`=6rem. Spacing: `gap-2`=0.5rem,
  `gap-3`=0.75rem, `gap-4`=1rem, `gap-5`=1.25rem, `gap-6`=1.5rem, `gap-8`=2rem, `gap-10`=2.5rem,
  `gap-12`=3rem, `gap-16`=4rem, `py-24`=6rem, `py-28`=7rem, `py-32`=8rem, `py-40`=10rem,
  `px-6`=1.5rem, `px-12`=3rem.
- **Color tokens:**
  ```css
  :root{
    --canvas:#ffffff; --surface-grey:#f3f3f3; --surface-dark:#191917;
    --ink:#191917; --ink-muted:rgba(25,25,23,0.6); --ink-faint:rgba(25,25,23,0.3);
    --on-dark:#ffffff; --on-dark-muted:rgba(255,255,255,0.6); --on-dark-faint:rgba(255,255,255,0.3);
    --line:rgba(25,25,23,0.2); --line-strong:rgba(25,25,23,0.4); --line-on-dark:rgba(255,255,255,0.2);
  }
  ```
- **Dashed hairlines:** most sections begin with a 1px **dashed** top border in `--line`
  (`.rule-dashed`). On dark sections use `--line-on-dark` (`.rule-dashed-dark`). Use them on section
  tops, figcaption tops, ledgers, and accordion rows as specified.
- **Container:** centered, `max-width:120rem`. Section horizontal padding `1.5rem` mobile / `3rem`
  (lg ≥1024px). Vertical padding `6rem` mobile / `8rem` lg (the statement uses `7rem`/`10rem`).
- **Breakpoints:** `sm`=640px, `md`=768px, `lg`=1024px. Single column below `lg`; 12-column grids at `lg`.
- **Images:** every image is ratio-locked — a `position:relative; overflow:hidden` box with the given
  `aspect-ratio` containing an absolutely-filled `object-fit:cover` `<img>` (grayscale). Because
  every portfolio photo is a **back view of a printed tee**, set `object-position:center 60%` so the
  print, not the head, sits at the visual center.

## Layout & sections (in order)

**Header (fixed)** · main = **Hero → Statement → Portfolio → Pinned CTA #1 → Principles → About →
Process → Services → Pinned CTA #2 (centered) → Testimonials → Clients → FAQ** · **Footer**. Plus the
**Modal Menu** overlay.

---

### Header (fixed, mix-blend-difference)

Fixed bar, `position:fixed; inset-inline:0; top:0; z-index:50; color:#fff; mix-blend-mode:difference`.
Inner grid: `padding:1.25rem 1.5rem` (lg `1.25rem 3rem`), `grid-template-columns:1fr 1fr` mobile,
**3 columns** at lg, `align-items:center`.

- **Left column** (hidden below lg): `<p>` "Apparel Design & Manufacturing" (0.875rem, letter-spacing
  -0.02em) and `<p>` "Design · Print · Produce" (0.75rem, uppercase, letter-spacing 0.16em,
  color rgba(255,255,255,0.7)).
- **Center — Logo** (`justify-self:start` mobile / `center` lg): the **Diamond Stitch mark** (1.5rem inline SVG: an outlined diamond with a smaller dashed diamond inside, both `stroke:currentColor`), then the wordmark "simple threads" in
  **Playfair Display, italic, lowercase**, 1.125rem, letter-spacing 0.04em. Gap 0.75rem. Links to `#top`.
- **Right column** (`justify-self:end`, flex, gap 2rem): `<nav aria-label="Primary">` (hidden below
  lg) with the first three links — "Work" (`#work`), "Services" (`#services`), "Process" (`#process`) —
  0.875rem uppercase letter-spacing 0.14em, each with a `1px×1px` white dot before it that fades
  0→1 on hover (gap 0.5rem). Then a **Menu button**: "Menu" (hidden below sm, 0.875rem uppercase
  letter-spacing 0.16em) plus a two-bar hamburger (`height:1px; width:1.5rem; background:#fff`, gap
  0.375rem). Opens the Modal Menu.

Full nav list (Menu overlay + footer): **Work** `#work`, **Services** `#services`,
**Process** `#process`, **About** `#about`, **Contact** `#contact`.

---

### Hero (`<section>`, full viewport)

`position:relative; min-height:100svh; padding:8rem 1.5rem 4rem` (lg `10rem 3rem 4rem`). Inner grid
1-col → **12-col at lg**, `align-items:center`, gap 3rem (lg 2rem).

- **Left (lg col-span 6):**
  - **Eyebrow** "Apparel design & manufacturing" (fade).
  - **`<h1>`**, max-width 14ch, line-revealed, 3.75rem → sm 4.5rem → lg 6rem, line-height 1.04.
    Text: **`Your idea, simply made.`** with **"simply"** as an `<Accent>`.
  - **Lead `<p>`** (word reveal, +500ms): max-width 46ch, 1.125rem, line-height 1.625, `--ink-muted`,
    margin-top 2.5rem. Verbatim: "From one shirt to a full collection — design help, sampling, and
    production of shirts, hoodies, caps, lanyards, and more for brands, teams, schools, events, and
    anyone with an idea. Printed or embroidered."
  - **CTA row** (fade-up, +800ms), margin-top 2.5rem, flex wrap gap 1rem: **solid** "See our work" →
    `#work`; **ghost** "Get a quote" → `#contact`.
  - **Facts row** (fade, +1000ms, hidden below lg), margin-top 3rem, `border-top:1px solid var(--line)`,
    padding-top 2rem. `<dl>` 3 columns gap 1.5rem: **Based** / "Manila, Philippines", **Minimum order** /
    "None", **Decoration** / "Print & embroidery".
- **Right (`grid-column: 8 / span 5`) — "Three steps" card** (fade-up, +200ms; NO photo here): `<aside
  aria-label="How ordering works">`, `background:#191917; color:#fff; padding:2.5rem 2rem` (lg
  `3.5rem 3rem`), flex column gap 2.5rem. Top: the Diamond Stitch mark (3.5rem) then Playfair title
  "Three steps. That’s it." (2.25rem → lg 3rem). Then an `<ol>`; each `<li>` has a dashed top border in
  `--line-on-dark`, padding-block 1.25rem, a Playfair index (0.875rem `--on-dark-muted`), a title
  (1.125rem weight 500) and a line (0.9375rem `--on-dark-muted`):
  01 **Send your idea** — "A sketch, a photo, or just a description." ·
  02 **Approve your sample** — "Check the fit, print, and color before we run the order." ·
  03 **Wear it** — "Your order is ready 2–3 weeks after sample approval."
  Footer line (dashed top border, 0.75rem uppercase letter-spacing 0.18em `--on-dark-muted`):
  "No minimum order · Design help included".
  **Grid note:** always set start and span together (`grid-column: 8 / span 5`), never
  `grid-column-start` after a `span` rule, or the item collapses to one column. Hero top padding at lg
  is **12rem** so the eyebrow clears the fixed header.
- **Mobile scroll cue** (hidden at lg, fade +1400ms): "Scroll to enter" (0.6rem uppercase
  letter-spacing 0.3em `--ink-faint`) + a `1px × 2.5rem` line in `--line-strong`, gap 0.75rem,
  margin-top 3rem.

---

### Statement (light)

`border-top:1px dashed var(--line); background:#fff; padding:7rem 1.5rem` (lg `10rem 3rem`).
Inner `max-width:80rem`.

- **Eyebrow** "How we work" (fade), margin-bottom 3rem.
- **Passage** (`<p>`, Playfair, word reveal, stagger 30ms): 1.875rem → sm 2.25rem → lg 3rem,
  line-height 1.3 (lg 1.25), `--ink`. Verbatim: "A shirt is the first thing people hold of your
  brand. We treat it that way — refining the artwork with you, matching the print method to the
  design, and checking every piece before it ships under your name."
- **Signature** (fade-up, +400ms), margin-top 3rem: Playfair italic 1.25rem `--ink-muted`:
  **"— The Simple Threads team"**

---

### Portfolio (`id="work"`, light)

`border-top:1px dashed var(--line); background:#fff; padding:6rem 1.5rem` (lg `8rem 3rem`);
`scroll-margin-top:6rem`.

- **SectionHeading:** eyebrow "Brands we’ve built"; title (line reveal) =
  `Designed with them, made by us.` with **"made"** as an `<Accent>`.
- **Intro `<p>`** (fade), margin-top 1.5rem, max-width 52ch, 1rem line-height 1.625 `--ink-muted`:
  "A selection of client pieces we helped design and manufacture. Artwork and brand names belong to
  each client."
- **Gallery grid**, margin-top 4rem (lg 6rem): 1-col → **12-col at lg**, `gap-x:2rem`, `gap-y:0` at
  lg (4rem mobile). **Asymmetric zig-zag:** each `<article>` spans **6 of 12** columns (portrait
  photos need less width than landscapes); items 1, 3, 5 are `col-start:1`; items 2, 4, 6 are
  `col-start:7` and pushed down `margin-top:8rem`.
- Each item: `<figure>` (plate reveal) whose image plate **scroll-scrubs** parallax — translateY
  `+2.5rem → −2.5rem` across viewport progress. `<figcaption>`: `border-top:1px dashed var(--line)`,
  margin-top 1.5rem, padding-top 1.25rem, flex `justify-between` baseline gap 1.5rem. Left: `<h3>`
  piece name (1.25rem, weight 500, `--ink`) + `<p>` garment (0.875rem `--ink-muted`,
  margin-top 0.25rem) + `<p>` service tags (0.75rem uppercase letter-spacing 0.16em `--ink-faint`,
  margin-top 0.25rem). Right: the **client brand** in Playfair italic (1rem, `--ink`).

The six pieces (piece · client · garment · services · image · ratio):
1. **The Dragon · Reverend · The Warrior Collection, oversized tee in 100% French terry cotton ·
   Design assistance, production · `dragon.jpg` · 3 / 4**
2. **Pegasus · Stoicism · Black tee, back print with split-quote hem line ·
   Design assistance, production · `pegasus-1.jpg` · 3 / 4**
3. **The Pen & the Sword · Stoicism · Oversized tee, full-back print ·
   Design assistance, production · `knight-1.jpg` · 3 / 4**
4. **The Excalibur · Reverend · The Warrior Collection, oversized tee in 100% French terry cotton ·
   Design assistance, production · `excalibur.jpg` · 3 / 4**
5. **The Pen & the Sword, at night · Stoicism · Fit and print shown in low light ·
   Production · `knight-2.jpg` · 3 / 4**
6. **Pegasus, in the city · Stoicism · Regular-fit tee, on location ·
   Production · `pegasus-2.jpg` · 3 / 4**

(Image alt = "{client} — {piece}, back print".)

---

### Pinned CTA #1 (dark, with photo)

`border-top:1px dashed var(--line); background:#191917; min-height:100svh; display:flex;
align-items:center; padding:6rem 1.5rem` (lg px 3rem). Grid 1-col → 12-col at lg, `align-items:center`,
gap 3rem (lg 2rem).

- **Copy (lg col-span 6)**, `max-width:34rem`:
  - **Eyebrow tone=dark** "Start a run", margin-bottom 1.5rem.
  - **`<h2>`** (line reveal): 2.25rem → sm 3rem → lg 3.75rem, `--on-dark`. Verbatim:
    "Every idea starts with one shirt."
  - **Body `<p>`** (word reveal, stagger 16ms): margin-top 2rem, 1.125rem line-height 1.625,
    `--on-dark-muted`. Verbatim: "Bring a finished design, a rough sketch, or just a name. We’ll help
    shape the artwork, pick the right blank and print, and sample it before the full run."
  - **CtaButton tone=dark** (fade-up, +300ms), margin-top 2.5rem: "Get a quote" → `#contact`.
- **Image (`grid-column: 8 / span 5`):** plate ratio **3 / 4**, image `excalibur.jpg`, empty alt.

---

### Principles (grey)

`border-top:1px dashed var(--line); background:#f3f3f3; padding:6rem 1.5rem` (lg `8rem 3rem`).

- **SectionHeading:** eyebrow "What we stand by"; title "Three things we never cut corners on."
- **Card grid** (1-col → 3-col at sm), margin-top 4rem, gap-x 3rem gap-y 2.5rem. Each `<article>`
  (fade-up, stagger index × 90ms): `border-top:1px dashed var(--line)`, padding-top 2rem —
  index in Playfair 1.5rem `--ink`; `<h3>` margin-top 1.5rem, 1.25rem weight 500; `<p>` margin-top
  0.75rem, 1rem line-height 1.625 `--ink-muted`.
1. **01 — Your design stays yours.** — "We refine the artwork with you, never around you. Files and
   rights stay with your brand."
2. **02 — The print fits the art.** — "Fine linework, photo prints, and all-over graphics each suit a
   different method. We recommend the one that will last."
3. **03 — Every piece is checked.** — "Print placement, color, and stitching are inspected before
   anything leaves the shop."

---

### About (`id="about"`, light)

`border-top:1px dashed var(--line); background:#fff; padding:6rem 1.5rem` (lg `8rem 3rem`);
`scroll-margin-top:6rem`.

- **Top grid** (1-col → 12-col at lg):
  - **Left (lg col-span 7):** Eyebrow "About the studio" (margin-bottom 2rem); `<h2>` (line reveal),
    max-width 20ch, 2.25rem → sm 3rem → lg 3.75rem, line-height 1.1: "We make the clothes behind
    the brands."
  - **Right (lg col-span 5):** three word-reveal paragraphs (stagger 10ms; max-width 52ch, 1rem,
    line-height 1.625, `--ink-muted`; 1.5rem apart):
    1. "Simple Threads is a Manila-based apparel studio. We work with independent labels, teams, and
       companies that want merch they’re proud to put their name on."
    2. "Our designers help turn rough ideas into print-ready artwork. Our production floor handles the
       rest — cutting, printing, finishing, and packing — so one team is responsible from start to
       finish."
    3. "Whether it’s fifty tees for an event or a full collection for a streetwear launch, we treat the
       order like it’s our own brand on the tag."
- **Photo grid**, margin-top 4rem (lg 5rem): 1-col → 3-col at sm, gap 1.5rem. Each cell
  `overflow:hidden`, plate reveal (stagger index × 100ms), hover scale 1 → 1.06 (~700ms ease-out).
  Ratio **3 / 4**:
  - `knight-2.jpg` alt "Knight back print, close detail"
  - `pegasus-1.jpg` alt "Pegasus print and hem quote"
  - `dragon.jpg` alt "Linework print on French terry"
- **Facts ledger** (fade-up), margin-top 4rem, `border-top:1px dashed var(--line)`, padding-top 2.5rem,
  grid 2-col → 4-col at sm, gap-x 2rem gap-y 1.5rem. `<dt>` 0.75rem uppercase letter-spacing 0.18em
  `--ink-faint`; `<dd>` margin-top 0.5rem 1rem `--ink`:
  **Based** / "Manila, Philippines" · **Minimum order** / "None" · **Pricing** / "Lower per piece in
  bulk" · **Design help** / "On every order".

---

### Process (`id="process"`, light, sticky heading)

`border-top:1px dashed var(--line); background:#fff; padding:6rem 1.5rem` (lg `8rem 3rem`);
`scroll-margin-top:6rem`. Grid 1-col → 12-col at lg.

- **Left (lg col-span 5):** `position:sticky; top:8rem` at lg — SectionHeading: eyebrow "From idea to
  delivery"; title "How an order comes together."
- **Right (lg col-span 7):** `<ol>` of 5 steps. Each `<li>` (fade-up): `border-top:1px dashed var(--line)`,
  padding-block 2.5rem (sm 3rem), flex column → row at sm, gap 1rem (sm 3rem). Index in Playfair
  4.5rem → sm 6rem, line-height 1, `--ink-faint`. Right (sm padding-top 0.75rem): `<h3>` 1.5rem
  (lg 1.875rem) weight 500; `<p>` margin-top 1rem, max-width 48ch, 1.125rem line-height 1.625 `--ink-muted`.
1. **01 Consult** — "Tell us about the brand, the garments, the quantities, and the date you need
   them. We’ll recommend blanks and print methods that fit the budget."
2. **02 Design** — "Our designers help refine your artwork or build it with you, then prepare
   print-ready files and a mockup for approval."
3. **03 Sample** — "We produce a sample so you can check fit, fabric, color, and print placement
   before committing to the full run."
4. **04 Produce** — "Once the sample is approved, the order is printed, finished, and inspected piece
   by piece."
5. **05 Deliver** — "Orders are folded, tagged if requested, packed, and shipped or ready for pickup."

---

### Services (`id="services"`, light) — replaces the original "Acquire" section

`border-top:1px dashed var(--line); background:#fff; padding:6rem 1.5rem` (lg `8rem 3rem`);
`scroll-margin-top:6rem`.

- **Header row** (flex column → row at lg, items-end, justify-between, gap 2.5rem):
  SectionHeading — eyebrow "What we make"; title "Garments, accessories, print, and embroidery." ·
  Lead `<p>` (fade), max-width 42ch, 1rem line-height 1.625 `--ink-muted`: "Pick the products, choose
  a print method, and we’ll handle the rest. No minimum order — the more you order, the less you pay
  per piece."
- **Products grid**, margin-top 4rem: 2-col → **4-col at lg**, gap-x 2rem gap-y 0. Each `<article>`
  (fade-up, stagger (index % 4) × 80ms): `border-top:1px dashed var(--line)`, padding-block 2rem,
  flex column. Index in Playfair 0.875rem `--ink-muted`; `<h3>` margin-top 1rem, 1.5rem Playfair
  `--ink`; `<p>` margin-top 0.5rem, 0.875rem line-height 1.6 `--ink-muted`.
  1. **T-shirts** — "Regular, oversized, and boxy fits in cotton, French terry, and blends."
  2. **Hoodies** — "Pullover and zip-up, mid to heavy weight, with front, back, and sleeve prints."
  3. **Long sleeves** — "Crewneck tees and jerseys with room for sleeve graphics."
  4. **Polos** — "Pique and dri-fit polos for teams, uniforms, and corporate wear."
  5. **Jackets** — "Windbreakers, varsity, and coach jackets, printed or embroidered."
  6. **Caps** — "Dad caps, snapbacks, and trucker hats, embroidered or printed."
  7. **Beanies** — "Cuffed and fisherman beanies with woven or printed labels."
  8. **Lanyards** — "Full-color sublimated lanyards for events, schools, and offices."
- **Methods explained** (text only, no images), margin-top 6rem. Header row (column → row at lg,
  items-end, justify-between, gap 1.5rem): `<h3>` (line reveal, Playfair 1.875rem → lg 2.25rem,
  max-width 16ch) "Print and embroidery, explained." + `<p>` (fade, max-width 46ch, 1rem `--ink-muted`):
  "Not sure which to pick? Here’s how each method works and what it’s best at. We’ll recommend one with
  your quote." Then five `<article>` rows (fade-up), each `border-top:1px dashed var(--line)`,
  padding-block 3rem. At lg each row is a 12-col grid: cols 1–4 hold a small label (0.75rem uppercase
  letter-spacing 0.18em `--ink-muted`) above the method name (Playfair 2.25rem → lg 3rem); cols 5–12
  hold the "how it works" paragraph (1.125rem `--ink-muted`, max-width 48ch) and below it a 2-col `<dl>`
  (dashed top border) with **Best for** and **Good to know**. Stack on mobile.
  1. *Direct-to-film* · **DTF** — "Your design is printed onto a special film, coated with an adhesive
     powder, then heat-pressed onto the garment, where it bonds as a thin, flexible layer." Best for:
     "Detailed, full-color designs and small runs on almost any fabric — cotton, polyester, or blends."
     Good to know: "Works on light and dark garments alike, and the print stays bright."
  2. *Direct-to-garment* · **DTG** — "A specialized printer sprays water-based ink straight onto the
     shirt, like an inkjet printer for fabric. The ink soaks into the fibers instead of sitting on
     top." Best for: "Photos, gradients, and many-color artwork on cotton, even for a single piece."
     Good to know: "Gives the softest feel of any print. Looks best on 100% cotton."
  3. *Screen printing* · **Silk screen** — "A stencil is made on a fine mesh screen, one for each
     color. Ink is pushed through the open parts of the mesh with a squeegee, then cured with heat."
     Best for: "Bold designs with a few solid colors, especially in larger quantities." Good to know:
     "Each color needs its own screen, so it gets more affordable per piece the more you order. Very
     durable."
  4. *Dye sublimation* · **Sublimation** — "The design is printed on transfer paper, then
     heat-pressed. The heat turns the ink into a gas that bonds into the polyester fibers, so the print
     becomes part of the fabric." Best for: "All-over prints, jerseys, activewear, and lanyards." Good
     to know: "Only works on polyester in white or light colors. It never cracks or peels, and you
     can’t feel it at all."
  5. *Machine embroidery* · **Embroidery** — "Your logo is converted into a stitch file, then an
     embroidery machine sews it into the fabric with thread, giving a raised, textured finish." Best
     for: "Logos on polos, caps, jackets, and beanies — anything that should look premium." Good to
     know: "Best for simpler designs without tiny text or gradients. Extremely durable and outlasts the
     garment."
- **Bottom CTA** (fade-up), margin-top 4rem, centered: solid CtaButton "Get a quote" → `#contact`.

---

### Contact & quote form (`id="contact"`, dark, centered)

Dark shell like Pinned CTA #1 but stacked and centered; `scroll-margin-top:6rem`. Every "Get a quote"
button on the page scrolls here.

- **Eyebrow tone=dark** "Get in touch"; **`<h2>`** (line reveal) "Tell us what you want to make.";
  **body** (word reveal): "Fill in what you can — rough numbers are fine. No minimum order; we’ll reply
  with options and a price for your quantity."
- **Quote form** (`max-width:48rem`, centered, left-aligned text, `border:1px dashed var(--line-on-dark)`,
  padding 2rem 1.5rem → sm 2.5rem, `color-scheme:dark`). Title (Playfair 1.875rem) "Request a quote".
  Labels 0.75rem uppercase letter-spacing 0.16em `--on-dark-muted`; inputs: white text,
  `background:rgba(255,255,255,0.05)`, `border:1px solid rgba(255,255,255,0.28)`, no radius, padding
  0.8rem 1rem, font-size at least 16px, `box-sizing:border-box`. Two columns at sm:
  **Name *** (text, required) · **Email *** (email, required) · **Mobile number** (tel, placeholder
  "09XX-XXX-XXXX") · **Brand, team, or event** (text).
  **What do you need?** — a `<fieldset>` of checkbox chips (min-height 2.75rem, 1px border; checked =
  white fill, ink text): T-shirts, Hoodies, Long sleeves, Polos, Jackets, Caps, Beanies, Lanyards, Other.
  Then two columns: **Quantity (rough is fine)** (number, placeholder "e.g. 50") · **Print or
  embroidery** (select: "Not sure — recommend one", DTF, DTG, Silk screen, Sublimation, Embroidery) ·
  **Needed by** (date) · **Design link (optional)** (url, placeholder "Google Drive or any link").
  Full width: **Tell us about your idea** (textarea, 4 rows, placeholder "Colors, sizes, where the
  print goes, anything you have in mind."). A hidden honeypot checkbox `name="botcheck"`.
  Submit: dark solid CtaButton "Send quote request →"; beside it a `role="status" aria-live="polite"`
  message line.
  **iOS fix (required):** give each field wrapper `min-width:0`, and the date input
  `-webkit-appearance:none; display:block; min-width:0; max-width:100%; height:2.9rem`, or Safari
  makes it overflow into the next column.
- **Submission (Web3Forms):** on submit, validate name and email (mark invalid fields
  `aria-invalid="true"`, focus the first), then `fetch("https://api.web3forms.com/submit")` with `POST`,
  JSON headers, and body `{access_key:"b8ca9f24-9168-41e9-8a6f-62bea840c844", subject:"Quote request —
  {name}", from_name:"Simple Threads website", replyto:{email}, name, email, mobile, organization,
  products (comma-joined), quantity, method, deadline, design_link, message}`. If the honeypot is
  ticked, show the thank-you without sending. Success (`json.success`): reset the form; status
  "Thanks, {name}! Your request is in. We’ll reply by email soon." Failure: status "Sorry, that didn’t
  send." with a link opening a `mailto:` to simplethreads.mnl@gmail.com pre-filled with the same
  details, "or message us on Viber."
- **Direct contact block** (below the form, same max-width): Playfair 1.5rem "Prefer to message us
  directly?" then two columns at sm, each with a dashed top border:
  **Viber** — "0961-382-6973" (1.25rem) + dark ghost button "Message on Viber →", both linking
  `viber://chat?number=%2B639613826973`.
  **Email** — "simplethreads.mnl@gmail.com" + dark ghost button "Send an email →"
  (`mailto:simplethreads.mnl@gmail.com?subject=Quote%20request`).

---

### Testimonials (light)

`border-top:1px dashed var(--line); background:#fff; padding:6rem 1.5rem` (lg `8rem 3rem`).

- **SectionHeading:** eyebrow "From our clients"; title "What the brands say."
- **Grid** (1-col → 2-col at md), margin-top 4rem, gap 2.5rem. Each `<figure>` (fade-up, stagger
  index × 110ms): `border-top:1px dashed var(--line)`, padding-top 2rem, flex column justify-between.
  `<blockquote>` Playfair 1.25rem (lg 1.5rem) line-height 1.625 `--ink`, max-width 32ch, wrapped in
  “ ”; `<figcaption>` margin-top 2.5rem: brand name (1rem `--ink`) + label (0.875rem `--ink-muted`,
  margin-top 0.25rem).
1. "They took our rough idea and turned it into a print we’re proud of. The quality speaks for
   itself." — **Stoicism**, *Clothing brand*
2. "The detail in our linework came out sharp on every piece. Easy to work with from design to
   delivery." — **Reverend**, *Clothing brand, The Warrior Collection*

---

### Clients (grey) — replaces "Exhibitions"

`border-top:1px dashed var(--line); background:#f3f3f3; padding:6rem 1.5rem` (lg `8rem 3rem`).

- **SectionHeading** (margin-bottom 4rem): eyebrow "Who we’ve worked with"; title "Brands that wear our work."
- **`<ul>`** 1-col → 2-col (sm) → 3-col (lg). Each `<li>` (fade-up, stagger (index % 3) × 80ms):
  `border-top:1px dashed var(--line)`, padding-block 1.5rem, flex baseline gap 1.25rem — zero-padded
  index in Playfair (0.875rem `--ink-muted`) + client name in Playfair (1.25rem, lg 1.5rem, `--ink`).

Clients, in order: **Reverend · Stoicism.** (Add more names as other clients agree to be listed.)

---

### FAQ (light, accordion)

`border-top:1px dashed var(--line); background:#fff; padding:6rem 1.5rem` (lg `8rem 3rem`). Grid
1-col → 12-col at lg.

- **Left (lg col-span 4):** SectionHeading — eyebrow "Questions"; title "Before you order."
- **Right (lg col-span 8):** accordion rows (fade, stagger index × 80ms). Each row:
  `border-top:1px dashed var(--line)`; `<h3>` with a full-width `<button>` (flex justify-between
  items-center gap 2rem, padding-block 2rem, left-aligned). Question 1.25rem (lg 1.5rem) weight 500
  `--ink`; a **"+"** glyph (1.5rem) that rotates to 45° when open (~450ms). Panel (`role="region"`)
  animates height 0 → measured and opacity 0 → 1 (~550ms, `overflow:hidden`); content padding-bottom
  2.5rem, `<p>` max-width 60ch, 1.125rem line-height 1.625 `--ink-muted`. Wire `aria-expanded`,
  `aria-controls`, `aria-labelledby`. Rows toggle independently.
1. **Is there a minimum order?** — "No. You can order as few or as many pieces as you need. Pricing
   is tiered by quantity, so the larger the order, the lower the price per piece."
2. **I don’t have a finished design. Can you help?** — "Yes. Design assistance is part of what we do.
   Send a sketch, a reference, or a description, and our designers will prepare print-ready artwork
   and a mockup for your approval."
3. **Which print method should I choose?** — "It depends on the artwork, the fabric, and the quantity.
   Fine detail and small runs suit DTF or DTG, bold designs in volume suit silk screen, all-over
   polyester prints suit sublimation, and logos on polos, caps, and jackets look best embroidered. We’ll recommend one with your quote."
4. **How long does production take?** — "Typically 2–3 weeks after sample approval, depending on
   quantity, garment, and print method. Rush orders may be possible — ask early."
5. **Can I see a sample first?** — "Yes. We produce a sample for approval before the full run so you
   can check fit, fabric, and print."

---

### Footer (dark)

`background:#191917; color:#fff; padding:6rem 1.5rem 3rem` (lg px 3rem).

- **Top grid** (1-col → 12-col at lg, gap 4rem / lg 3rem):
  - **Brand (lg col-span 5)** (fade-up): the Logo; a Playfair italic tagline `<p>` (margin-top 1.5rem,
    max-width 28ch, 1.5rem, `--on-dark-muted`): "Your idea, simply made."; a mailto link
    (margin-top 2rem, 0.875rem uppercase letter-spacing 0.16em, hover `--on-dark-muted`):
    **simplethreads.mnl@gmail.com**.
  - **"Explore" (lg col-span 2):** title `<p>` 0.75rem uppercase letter-spacing 0.18em
    `--on-dark-faint`; links (margin-top 1.5rem, 0.75rem apart, 1rem `--on-dark-muted`, hover
    `--on-dark`): Work `#work`, Services `#services`, Process `#process`, About `#about`.
  - **"Products" (lg col-span 2):** Shirts & hoodies `#services`, Outerwear `#services`,
    Headwear `#services`, Lanyards `#services`.
  - **"Contact" (lg col-span 3):** Get a quote `#contact`, Email us
    `mailto:simplethreads.mnl@gmail.com`, Call us `tel:+639613826973`, Viber
    `viber://chat?number=%2B639613826973`.
- **Giant wordmark** (fade-up, `overflow:hidden`, aria-hidden), margin-top 6rem: "Simple Threads" at
  `font-size:10.5vw; white-space:nowrap` (so the two words fit on one line),
  weight 900 Satoshi, uppercase, line-height 0.8, letter-spacing -0.04em, `rgba(255,255,255,0.1)`.
- **Legal bar:** margin-top 3rem, `border-top:1px dashed var(--line-on-dark)`, padding-top 2rem, flex
  column → row at sm, justify-between. Left: "© 2026 Simple Threads. All rights reserved. Client
  artwork shown with permission and remains the property of each brand." (0.875rem
  `--on-dark-faint`). Right: **Privacy** `#`, **Terms** `#` (0.875rem `--on-dark-faint`, hover
  `--on-dark-muted`, gap 1.5rem).

---

### Modal Menu (full-screen overlay)

`position:fixed; inset:0; z-index:60; color:#fff`, hidden until opened; lock scroll while open.

- **Black panel** `position:absolute; inset:0; background:#191917; transform-origin:top;
  transform:scaleY(0) → scaleY(1)` (~600ms).
- **Content** (`height:100%`, flex column, `padding:1.5rem 1.5rem 2.5rem`, lg px 3rem):
  - **Top bar:** "Menu" (0.75rem uppercase letter-spacing 0.28em `--on-dark-faint`) · "Close ✕"
    button (0.75rem uppercase letter-spacing 0.18em, hover `--on-dark-muted`).
  - **Nav** (`flex:1`, centered column, gap 0.5rem): 5 links staggering in from `opacity:0 /
    translateY(1.5rem)` (delay 180 + index × 70ms). Each: 2-digit index (width 2rem, 0.875rem
    `--on-dark-muted`) + label in Playfair 3rem → sm 3.75rem → lg 4.5rem, **italic on hover**.
    Clicking closes the menu and scrolls to the target. 01 Work · 02 Services · 03 Process ·
    04 About · 05 Contact.
  - **Bottom block** (fade, +600ms): `border-top:1px dashed var(--line-on-dark)`, padding-top 2rem,
    flex column → row at sm, items-end, justify-between. Left: mailto **simplethreads.mnl@gmail.com** (1.125rem) +
    "Manila, Philippines · 0961-382-6973" (0.875rem `--on-dark-muted`). No social links.

---

## Shared UI primitives

- **Eyebrow:** inline-flex, gap 0.75rem — a `1px × 2rem` line (`--ink-muted` / `--on-dark-muted`) +
  label 0.75rem uppercase letter-spacing 0.2em, same color.
- **Accent:** Playfair Display italic, weight 400, normal case `<span>`.
- **CtaButton:** inline-flex gap 0.75rem, padding `1rem 2rem`, 0.875rem uppercase letter-spacing 0.14em.
  Light solid `#191917`/`#fff` (hover ~90%); light ghost `1px dashed var(--line)` (hover fills ink);
  dark solid `#fff`/`#191917`; dark ghost `1px dashed var(--line-on-dark)` (hover fills white).
  Trailing **"→"** slides `translateX(0) → 0.4rem` on hover (~400ms).
- **SectionHeading:** optional Eyebrow (fade, margin-bottom 1.5rem) + line-revealed `<h2>`, max-width
  18ch, 2.25rem → sm 3rem → lg 4.5rem, `--ink` (or `--on-dark`).

## Motion system

IntersectionObserver-gated, play once (`threshold:0`, `rootMargin:"0px 0px -10% 0px"`). Respect
`prefers-reduced-motion` (show everything, no transforms).

- **fadeUp** — `{opacity:0, translateY:2.5rem}` → visible, **720ms** `cubic-bezier(0.16,1,0.3,1)`.
- **fade** — opacity 0 → 1, **640ms**.
- **plate** — `{opacity:0, translateY:3.5rem, scale:1.04}` → visible, **700ms**.
- **Line reveal** — each word/line clipped in `overflow:hidden`, from `translateY(110%); opacity:0`,
  **1000ms** easeOutExpo, **line stagger 90ms** (hero h1 140ms). Accent words animate inline.
- **Word reveal** — words from `translateY(0.8rem); opacity:0`, **720ms**
  `cubic-bezier(0.165,0.84,0.44,1)`; stagger: hero lead 18ms (+500ms start), statement 30ms, about
  10ms, pinned-CTA bodies 16ms.
- **Delays/staggers:** hero eyebrow 0, heading 0, lead +500, CTA +800, facts +1000, plate +200, cue
  +1400; principles index×90; about photos index×100; products (index%4)×80; print methods index×90;
  testimonials index×110; clients (index%3)×80; FAQ index×80.
- **Hover (pointer devices, >768px only):** CTA arrow 400ms; about photo scale 1.06 at 700ms; print
  method card lift −0.75rem at 600ms; header nav dot fade; menu link italic.
- **Portfolio parallax:** progress 0 (plate top at viewport bottom) → 1 (plate bottom at viewport top)
  maps linearly to `translateY` **+2.5rem → −2.5rem**; update on Lenis scroll; disable below lg.
- **Modal:** panel scaleY ~600ms; links stagger (180 + index×70ms); bottom block fade +600ms; close
  reverses quickly.
- **FAQ:** "+" → 45° (~450ms); panel height/opacity (~550ms); re-measure with ResizeObserver.

## Fixed parameters (bake these in)

- **Palette:** canvas `#ffffff`; grey `#f3f3f3`; dark / ink `#191917`; ink-muted `rgba(25,25,23,0.6)`;
  ink-faint `rgba(25,25,23,0.3)`; on-dark `#ffffff`; on-dark-muted `rgba(255,255,255,0.6)`;
  on-dark-faint `rgba(255,255,255,0.3)`; line `rgba(25,25,23,0.2)`; line-strong `rgba(25,25,23,0.4)`;
  line-on-dark `rgba(255,255,255,0.2)`. **Strictly monochrome; photos grayscale.**
- **Fonts:** Playfair Display for headings, accents, quotes, product and method names, numerals,
  wordmark; Satoshi for body, UI, and labels.
- **Breakpoints:** sm 640 / md 768 / lg 1024; root font-size queries at 1920 / 1440 / 1024 / 640.
- **Section rhythm:** 6rem / 8rem vertical (statement 7rem / 10rem); 1.5rem / 3rem horizontal;
  container 120rem; dashed top hairlines; `scroll-margin-top:6rem` on `#work #services #process
  #about #contact`.
- **Image ratios:** all portfolio and about plates **3 / 4**, `object-position:center 60%`.
- **Portfolio zig-zag:** items span 6/12; even items col-start 7 + margin-top 8rem; gap-x 2rem.

## Assets

Upload the six photos with this prompt and save them in `/images/` with exactly these names (all
displayed grayscale):

- `dragon.jpg` — Reverend, The Warrior Collection, "The Dragon". Used: portfolio 1, about photo 3.
- `excalibur.jpg` — Reverend, "The Excalibur". Used: portfolio 4, Pinned CTA #1.
- `pegasus-1.jpg` — Stoicism, Pegasus print, indoor shot. Used: portfolio 2, about photo 2.
- `pegasus-2.jpg` — Stoicism, Pegasus, by a window at night. Used: portfolio 6.
- `knight-1.jpg` — Stoicism, The Pen & the Sword, outdoor night. Used: portfolio 3.
- `knight-2.jpg` — Stoicism, The Pen & the Sword, concrete wall. Used: portfolio 5, about photo 1.

**Logo and favicon:** the Diamond Stitch mark — an inline SVG (viewBox 0 0 72 72) of a 40×40 square
rotated 45° about (36,36), stroked `currentColor` width 2–3, with a 23×23 rotated square inside,
dashed (`stroke-dasharray:3.5 3`). Use it in the header, footer, and menu logo (1.5rem, before the
italic wordmark "simple threads") and as the favicon (white mark on a #191917 rounded square).

**SEO:** `<title>` "Simple Threads — Apparel Design & Manufacturing, Manila"; meta description
"Simple Threads is a Manila-based apparel studio offering design assistance and custom shirts,
hoodies, jackets, caps, beanies, and lanyards in DTF, DTG, silk screen, sublimation, and embroidery.
No minimum order."; og:image `/images/dragon.jpg`; theme-color `#191917`.
