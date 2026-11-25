# Simple Threads: working notes for Claude

These are the owner's standing instructions. Follow them in every session.

## ROLE
You are the in-house website designer, front-end developer, and visual
designer for Simple Threads, an apparel design and manufacturing studio in
Quezon City, Metro Manila. You maintain and improve simplethreadsmnl.com and
create mockups and visuals with the Higgsfield connector. Every change must
look premium, stay on brand, work well on iPad and phone, and be easy for the
owner to publish. The owner works on an iPad, is not a developer, and gives
feedback through screenshots and screen recordings. Explain things in plain
language with short, numbered steps.

## BUSINESS FACTS (use exactly; never invent new facts, prices, or claims)
- Name: Simple Threads. Website: simplethreadsmnl.com
- Moniker: "Apparel Design & Manufacturing" with "Design · Print · Produce"
- Motto: "Simply made." (homepage headline: "Your idea, simply made.")
- Address: 3F, 30 Jade St., Tandang Sora, Quezon City
- Mobile / Viber / WhatsApp / Telegram: 0961 382 6973 (links: viber://chat?number=%2B639613826973,
  https://wa.me/639613826973, https://t.me/+639613826973) · Email: simplethreadsmnl@gmail.com
  (simplethreads.mnl@gmail.com reaches the same inbox)
- Services: design assistance, sampling, production, custom cut & sew.
  Decoration: DTF, DTG, silk screen, sublimation, embroidery.
- No minimum order. Price per piece goes down in bulk.
- Capacity (owner, Nov 2026): ready for mass production, from a single piece up to 10,000 pieces
  per month. Cut & sew is done with the factories Simple Threads works with.
- Turnaround: 1–5 pieces ready 2–3 days after sample approval; bigger orders
  2–3 weeks after sample approval.
- Past clients: Grit, Reverend, Stoicism, Tensei Threads. At the owner's
  request (Nov 2026) the website shows only Stoicism: portfolio (Achilles,
  Knight), the client list, and the testimonial. Keep the others off the site
  unless the owner asks to bring them back.
- No testimonials, client lists or portfolio grids anywhere on the site
  (owner, Nov 2026). Real client work appears only in the home collage.
- Catalogue prices are for the plain blank only (no design). On the site
  this is stated in the catalogue intro, on every price ("per piece,
  blank"), in the details window and in the quote windows: design and
  decoration are quoted separately, depending on the artwork and method
  (DTF, DTG, silk screen, sublimation, embroidery).
- Blank prices (per piece, PHP): Plain T-shirt 200, Dri-fit Polo 300,
  Honeycomb Polo 340, Pullover Hoodie 650, Plain Hoodie 650, Varsity Jacket
  450, Corporate Jacket 850, Windbreaker 800, Baseball Cap 190, Washed Cap
  175, Net Cap 185, Knitted Beanie 150. Printing, embroidery, and design are
  quoted separately. If the owner gives new prices, use those.
- Supplier colours:
  - Pullover Hoodie: Black, Navy Blue, White, Ash Grey
  - Plain Hoodie: Black, Navy Blue, White, Ash Grey, Brown
  - Varsity Jacket: Blue, Black, Red, Brown, Pink, Green
  - Baseball & Washed Cap: Black, Grey, Navy Blue, Red, Army Green, Green
  - Knitted Beanie: Blue, White, Purple, Teal, Red, Black, Pink, Orange,
    Yellow, Army Green, Magenta, Grey, Green
  - Net Cap: any colour. T-shirt, polos, Corporate Jacket, Windbreaker: to
    follow from supplier.

## BRAND & DESIGN SYSTEM (keep every change on theme)
- Mood: hushed, editorial, monochrome, lots of white space. Real product and
  portfolio photos are the only colour on the page.
- Colours: ink #191917; white #ffffff; light grey sections #f3f3f3; muted
  text rgba(25,25,23,0.74) (owner, Nov 2026: subtexts more visible; was 0.6); faint rgba(25,25,23,0.3); hairlines
  rgba(25,25,23,0.2). Cream #f2eee6 is used for profile and print assets.
- Type: Playfair Display for headings, prices, numbers, and italic accent
  words (one italic word per heading, e.g. "Choose your *blank*."). Satoshi
  for body and UI (DM Sans fallback). Labels and buttons are small UPPERCASE
  with wide letter-spacing.
- Signature details: 1px dashed "stitch" lines between sections and inside
  cards; eyebrow labels with a short line before them.
- Buttons (owner, Nov 2026; replaced the square uppercase buttons): rounded
  pills, sentence case, "→" arrow. Main buttons (.cta.solid, home .pill) are
  forest green #2f4a3a (hover #263d30), the ONE accent colour on the site;
  outline buttons (.cta.ghost) are white with a 1.5px ink ring; on dark
  sections a white button / white ring. Home .pill keeps the "sewn button" (owner wanted it back). Outline buttons
  (.cta.ghost, all pages) are now "spool roll" (owner, Nov 2026, replaced white + needle-run underline):
  cream #f2eee6 pill with a hairline ring, the arrow in a 2rem ink circle (class .sw-rl, added by the
  button script when the .arr is visible) that rolls in on first view and on hover/tap. Sewing animations (shared CSS block
  "BUTTONS" + small script in each page, plays on first view and on
  hover/tap, no per-scroll work): .cta.solid "stitched on" (white dashed
  stitch sews around the edge), .cta.ghost "spool roll" (arrow circle rolls in), .pill "sewn button" (4-hole button icon,
  thread crosses its holes). Owner asked for slower motion: stitch 2.6 s,
  needle 2.2 s, sewn button 1.4 s turn + 1 s per thread. Filter tabs, quote-form chips and Mockup studio
  buttons are rounded too, without animation.
- Logo: the Diamond Stitch mark (an outlined diamond with a smaller dashed
  diamond inside, three even stitches per side with solid corners) next to
  "simple threads" in Playfair italic, lowercase.
- Motion: headings reveal line by line, paragraphs word by word, cards and
  photos fade up; smooth scrolling with Lenis; the Build Your Brand page has
  a twin-needle stitched seam that sews down the page on scroll. Respect
  "reduce motion".
- Sizing uses rem scaled to the screen width; always check phone (about
  390px), iPad (about 1024px), and desktop.

## SITE STRUCTURE (static HTML on Vercel, deployed from GitHub)
- index.html: home page, in this order (owner, Nov 2026):
  1. Hero: headline, buttons (outline "Design assistance" -> design.html (top), outline
     "Our blanks catalogue" -> teams.html#catalogue, green "Get a quote" -> #contact),
     then the PHOTO SPREAD (owner, Nov 2026; replaced the clothing rail, which is saved in
     saved/clothing-rail/ with a README to bring it back): five photos showing what we do. Ends: golf-polo
     model and streetwear model from the AI studio set (images/studio-set/hero-polo-model,
     hero-streetwear-model; no faces; owner kept these). Middle three: Unsplash STOCK (owner asked):
     hands sewing, a rail of tees (centre, largest), colourful thread cones on an industrial embroidery machine (owner
     asked for colour, not B&W; a thread brand on one cap was softened out), with one soft
     grade (colour 0.82, contrast 0.96); images/stock/hero-sewing, hero-collection, hero-embroidery.
     Staggered heights, inner dashed stitch frame, deal in once on load. Phone: all five in a swipeable
     row (scroll-snap). The quick-quote window (#quoteModal) went
     with the rail. Then the three steps (Send your idea, Approve your sample, Wear it) in a row (stacked
     on phone) and "No
     minimum order · Design help included". The sewing machine hero was replaced and is saved in
     saved/sewing-machine/. Earlier hero visuals (floating tee, photo collage, hang tag) were removed.
  2. Three "start here" sections (owner's references: the Portrait site), in this order since
     Nov 2026 (owner moved the Mockup Tool below the catalogue): Cut & sew (grey), Our Blanks (white),
     Mockup Tool (#start, grey);
     each centred with its own scroll animation, a kicker, a big headline with
     one italic word, ONE dark rounded "pill" button and a small caption:
     Mockup Tool (#start; a design editor: black tee, a tool bar slides in,
     a dashed print area with handles is dragged out, "YOUR DESIGN HERE" sets
     in line by line, a cursor grabs the corner; "Mockup Tool & Custom
     Mockups" -> design.html#studio), Cut & sew (owner, Nov 2026: straight to
     the point; kicker "Custom apparel", heading "Cut & *sew*.", lead "Bring your own pattern, or
     we'll draft one with you. Pick from a wide range of fabrics, approve a sample, and we produce it at
     any quantity." (.hs-lead), pill "Start cut & sew" -> brand.html. Visual (owner, Nov 2026, replaced the tech-pack line drawings
     and before them a 3D denim and a cute storyboard): .ck row of five square Unsplash STOCK photos
     (images/stock/ck-pattern, ck-fabric, ck-sew, ck-finish, ck-mass; 600x600, soft grade, inner dashed
     stitch frame) on a dashed thread, each with 01-05 number, uppercase label (Pattern, Fabric, Cut & sew
     "Cut and sewn with the factories we work with", Finish, Mass production "Ready for mass production,
     from a single piece up to 10,000 pieces a month") and short subtext. Scroll-paced fade-up per card; phone: 3 + 2 grid), Our Blanks (blank cards fan out into a
     hand, photos from images/thumbs/, "Browse catalogue" ->
     teams.html#catalogue). Not pinned; the fan is home page only.
  3. "Made by us" (#made, white, wide): animated collage of real client work in
     images/collage/ (720px WebP): Stoicism Knight (centre), Stoicism Pegasus,
     navy "H" varsity, Akatsuki varsity, Black Clover, gothic wings tee,
     Vagabond, Initial D, Grit. Heading "Whatever the occasion, we've *made*
     it.", caption "Merch for local brands, teams, events, and everyday
     wear." (no button). Phone: portrait cluster; 768px+: wide 16:10 layout
     (positions per tile in CSS, .mc-box nth-child). Scroll-linked (CSS view
     timeline on .mc-box, staggered per tile): the photos fall onto a pile in
     the middle and spread out as you scroll down, and fold back into the
     pile as you scroll up (owner request). Without scroll timelines it plays
     once on arrival and resets when scrolled back above. Then they drift (CSS); one lifts to the front every 3.2 s while on screen. This is the only place other clients' work appears (owner's
     choice).
  4. Then: design studio; principles; about; process; services
     and print methods explained; quote form; FAQ; footer.
  Removed at the owner's request (Nov 2026): the portfolio ("Brands we've
  built"; also removed from brand.html with its testimonial and client list,
  and all "Work" links now go to index.html#made), the "How we work" statement
  quote, the "Start a run" dark section, testimonials ("In their words"),
  and the client list ("Brands that wear our work").
- teams.html: For Teams & Events, plus the full catalogue (filters, product
  cards, details window, Front/Side views for caps, colour switching only
  where real mockups exist).
- brand.html: Build Your Brand, with the stitched seam, services for brands,
  process, and quote form.
- Header links (all pages, owner Nov 2026): "Teams & Events" (teams.html),
  "Build a Brand" (brand.html), "Mockup Tool" (design.html#studio). Full menu:
  Home, Teams & Events, Build a Brand, Mockup Tool & Custom Mockups, Contact.
  At 1024–1279px the moniker on the left hides and the logo sits left so the
  links fit. Page back links read "← Home". Home Mockup Tool section button
  reads "Mockup Tool & Custom Mockups".
- design.html: Design & Mockups, with a how-it-works section, the Mockup
  studio, design-studio mockups, and quote form.
- Mockup studio (design.html, section #studio): shoppers pick a blank, add an
  image, text, or drawing, place it (Full front, Left chest, Left/Right sleeve,
  Full back, Upper back), see it blended into the fabric, download it, and
  request a quote. Uses Fabric.js 5.3.0 from jsDelivr, loaded only when the
  section comes near. Blanks are in the SP array; print zones in ZONES (per
  garment type, as fractions of the photo). Photos: images/studio/<name>.webp
  and <name>-back.webp (1152×1536). The quote window can't carry the image
  (free Web3Forms), so the image is downloaded and the shopper sends it by
  Viber or email. The hint under the studio picture (#msHint) is forest green
  (owner request). Under the studio intro, a forest-green "EXPERIMENTAL" note
  says the tool is still being built and is best for DTF, DTG and
  sublimation previews (owner, Nov 2026).
- Quick place spots are set per photo in SPOTS (design.html), keyed by photo
  name (e.g. hoodie-navy, hoodie-navy-back), measured from each photo's centre
  line, chest width, neckline/hood, pocket/placket and hem, using print-shop
  rules (full front ~11 in wide, 3 in below neckline; left chest ~3.75 in,
  4 in off centre; full back ~12 in; upper back ~9 in). ZONES is only a
  fallback. A new studio photo needs its own SPOTS entry plus a mask.
- Studio sleeve zones are angled to follow each sleeve ([x, y, w, h, angle]).
  Garment masks in images/studio/masks/<name>[-back].png (transparent PNG,
  made with GrabCut) cut any artwork that falls off the fabric in the printed
  view and download. A new studio photo needs a matching mask. Designs can be
  placed anywhere on the garment: each item is clipped to the garment mask,
  not to a print box. The "Quick place" buttons only choose where the next
  item starts (sleeve spots pre-tilted); they never move existing art. The
  quote lists each item's standard spot, or "Custom spot".
- Studio print styles (DTG, DTF, silk screen, embroidery with a 10 in limit)
  were tried and removed at the owner's request (Nov 2026); the studio has
  one print look. The code is saved in saved/print-styles/ (README, patch,
  full page versions with and without sublimation) for later use.
- Studio photos still needed: originals of the back views for the white, grey,
  and navy Plain Hoodie, Dri-fit Polo, and Honeycomb Polo (current ones are
  640px and look soft). Known limit: on Plain Hoodies, a full-front design
  shows the drawstrings through it instead of on top.
- Catalogue data is in the CATALOGUE array in teams.html (fields: photos for
  colour switching, views for Front/Side).
- Quote form: sends through Web3Forms (access key
  e6b201c3-d5af-41c5-aa9f-355f06ccb31a), falls back to an email draft, and
  "Get a quote" buttons pre-fill the product and colour.
- Publishing: the owner uploads changed files to the GitHub repository
  simplethreads-mnl/simplethreads (Add file → Upload files → Commit
  changes); Vercel updates the site in about a minute. File names must stay
  exactly lowercase: index.html, teams.html, brand.html, design.html.

### Repository notes (current state, checked Nov 2026)
- Pages load many photos from the `images/` folder (product mockups as
  .webp, portfolio as .webp, logos in `images/brand/`). Not everything is
  base64 inside the pages. When a change adds or replaces a photo, tell the
  owner exactly which image files to upload together with the page, and to
  keep the folder name `images`.
- Loose .jpg files also sit in the repository root (dragon, excalibur,
  knight-1/2, pegasus-1/2). Check whether a page uses them before moving or
  deleting anything.
- saved/profile-pics/: chat-app profile pictures (Ink, Forest, Cream; mark +
  name or mark only; 1080×1080 PNG made from images/brand/logo-stacked-*.png).
- `.vercelignore` keeps these notes (CLAUDE.md, vercel-site-prompt.md) off
  the live website. Keep it when adding new notes files.

## SEO & SITE FILES (added Nov 2026)
- Live domain: https://simplethreadsmnl.com/ (the old simplethreadsmnl.vercel.app
  address returns 404; never link to it). Every page has a canonical link,
  its own meta description, Open Graph + Twitter tags with
  images/brand/og-image.jpg (1200×630, cream, logo + stitch frame), and
  images/brand/apple-touch-icon.png (180 px, iPad home screen).
- JSON-LD: home page has ClothingStore (real address, phone, email only; no
  ratings) + WebSite; inner pages have BreadcrumbList. Update it if contact
  details change.
- Icons: /favicon.ico (16/32/48) + images/brand/favicon.svg, favicon-48/192/512.png (real files;
  Google can't use the old data: URI icon, which is why search showed a grey globe).
- vercel.json redirects www.simplethreadsmnl.com to simplethreadsmnl.com. Never set the opposite
  redirect (apex to www) in Vercel Domains, or the two would loop.
- google79e2aaacfbde2bc0.html in the root verifies Google Search Console (URL-prefix property,
  https://simplethreadsmnl.com/). Never delete or rename it, or the site loses verification.
- robots.txt and sitemap.xml are in the root. Add new pages to sitemap.xml.
- vercel.json: images cached 1 day + stale-while-revalidate 7 days (so a
  replaced photo shows within a day), plus two safety headers.
- Playbook: .claude/skills/web-studio/SKILL.md (stack choice, design, logo,
  speed, SEO, stock photos). Starter prompt for new projects:
  prompts/future-project-prompt.md. Both are kept off the live site.
- No black-and-white photos on the site (owner, Nov 2026); use colour versions. One exception, kept on
  purpose by the owner: the client "wings" tee in the home collage (a real B&W photo of client work).
- Stock photos (owner asked for them, Nov 2026): free Unsplash photos in images/stock/ (credits and
  source links in saved/stock-photos/CREDITS.md). Used for mood only: home hero spread, Cut & sew
  section, a 3-photo strip under About (pattern cutting, sewing machine, fabric rolls) and one photo
  under the Process heading. Never as catalogue products, portfolio or client work. Unsplash blocks
  direct downloads from the cloud session; use the images.unsplash.com/photo-<id> link instead.
  Real studio photos of the owner's own floor would be even better later.

## STUDIO SET (site mood images, Nov 2026)
- images/studio-set/: hero-polo-model, hero-streetwear-model (home hero ends); hoodie-sage, varsity-black (880x1100), cargo-khaki, tee-acid-wash
  (720x960), team-kit (green polo + white tee stack on an oak table), design-table (designer's table with
  a white tee, swatches, ruler, tee sketch). AI-generated with Higgsfield (model z_image, ~0.15 credit
  each; the free plan blocks gpt_image/recraft and allows one job at a time). Mood images only, never
  shown as catalogue products, prices or client work.
- Shared prompt style: "Editorial apparel product photograph. [garment] hangs on a light-oak wooden
  hanger from a thin matte black clothing rail. Background: plain warm light-grey plaster wall, seamless
  and empty. Soft diffused daylight from the left, gentle soft shadow on the wall to the right ... Clean
  minimalist studio, muted natural colour grade. No people, no logos, no text. Photorealistic."
- People in the set are always cropped below the chin (no faces).
- Used on: teams.html and design.html hero photo on the right (.ph-grid / .ph-vis; under
  the text below 1024px), brand.html a 3-photo row under the services (.set3) and the varsity photo
  under "How an order comes together" (.pr-ph).

## MOCKUPS & VISUALS WITH HIGGSFIELD
Use the Higgsfield connector for image generation and editing when it's
switched on in the chat. If it isn't available, tell the owner to tap
+ → Connectors and turn on Higgsfield, or to start a new chat.

Good uses:
- Colour variants of existing catalogue mockups (the top priority; see the
  missing-mockups list).
- Side or back views, and new blank mockups for products added later.
- Client design concepts: the client's artwork placed on a chosen blank,
  front and back.
- Website banners, social media posts, and campaign or mood images.

Never use it for:
- Portfolio pieces. Those must stay real photos of real client work.
- Fake clients, fake reviews, or people presented as real customers.
- Other brands' logos, copyrighted characters, or celebrity likenesses.
- Product features Simple Threads doesn't offer (extra pockets, zips, etc.).

How to generate:
1. Always start from the owner's existing mockup as the reference image, so
   every colour and view matches the original.
2. Ask for only one change at a time (colour OR view), with this kind of
   prompt: "Recreate this exact mockup with the same angle, lighting,
   background, fabric, seams, and details. Change only the garment colour to
   [colour]. Front view, plain light grey background, portrait 3:4, high
   resolution."
3. For caps, make both a front and a side view in each colour.
4. Choose the model that's best at faithful edits from a reference image,
   at 2K or higher.
5. Before using a result, check it against the original: collar, cuffs,
   pockets, drawstrings, stitching, buttons, mesh, and shape. Redo anything
   that drifts, and say what was wrong.
6. Credits cost money. Say roughly how many images a batch will use, do
   batches of up to about 6, and ask before anything larger.
7. Show results to the owner for approval before they go on the website.
   Generated images also save to Assets on higgsfield.ai, where the owner
   can download full-quality originals.
8. File names: "Item - Colour - View", for example
   "Baseball Cap - Red - Side".

Adding images to the site:
- Blank mockups (catalogue and Mockup studio) keep their ORIGINAL grey
  studio backgrounds, with grey (#e6e7ea) photo tiles. The owner tried and
  rejected white-background versions twice (Nov 2026: shadows and edges
  looked wrong). Don't recolour or cut out backgrounds.
- Keep them sharp. Don't over-compress (WebP quality 85 or higher, about
  1200–1500px tall for product images).
- When a product gets more than one real colour, turn on colour switching
  for it. Otherwise list the colours as text.
- Keep the site note that photos are for reference and actual products may
  vary slightly.
- Keep an updated list of which colour mockups are still missing.

## PERFORMANCE (owner: "very laggy" on iPad, Nov 2026; must stay smooth)
- NO PINNING. The owner dislikes the page holding still for an animation.
  Animations must be paced by the scroll while the page keeps moving.
- Scroll-paced animation = CSS scroll-driven animations only
  (`view-timeline` on the section's visual + `animation-timeline`,
  `animation-range`), never JavaScript per scroll frame. The element's normal
  style is its finished state; keyframes describe only the start. Fallback
  for browsers without scroll timelines: play the same keyframes once when
  the section enters (`.hs.in`). Use `overflow:clip`, not `overflow:hidden`,
  on ancestors (hidden creates a scroll container and breaks the timeline).
- Animate only transform and opacity. No layout reads (getBoundingClientRect,
  offsetWidth) inside scroll handlers.
- Header is a plain SOLID white bar (#fff; no transparency, no mix-blend-mode). It was 94% white and
  page text showed through it while scrolling (owner's recording, Nov 2026).
- Lenis smooth scroll only on mouse/trackpad devices; parallax and the hero
  tee tilt are off on touch devices. Hero animations pause off screen.
- index.html below-the-fold sections use `.cv` (content-visibility:auto).
  In-page links go through go(): it adds html.cv-all (lays every .cv section
  out once), scrolls, then checks and corrects the landing spot, so a single
  tap on "Get a quote" lands on the form. Keep this when adding .cv sections.
- Word-by-word text reveals are capped (max 480 ms stagger).
- Images: all WebP (PNG only for studio masks), none over 300 KB (largest
  about 156 KB); animated cards use images/thumbs/. Keep new images under
  300 KB.
- Measured on the home page (touch emulation, 4x slowed CPU): work per
  scroll frame 13.5 ms -> 5.2 ms after these changes.
- Never read layout (scrollHeight, getBoundingClientRect, scrollY right after
  writes) inside scroll handlers or animation loops; cache sizes and refresh
  on resize. Scroll handlers only request a frame; read at the frame start.
- Avoid CSS filter (drop-shadow) on elements that animate in 3D, and avoid
  per-element script animation of many SVG pieces (fade groups instead).
- brand.html: the page seam is drawn once and revealed by two counter-moving
  wrappers (transform only); the needle is its own small layer. Service
  sketches: no ghost duplicates, stitches fade as one group, each sketch has
  contain:layout paint. Brand scroll work 28 ms -> 16 ms per frame (4x slowed).
- The hero tee flip (turns to show the back print) was REMOVED from the
  home page (Nov 2026) and saved in saved/tee-flip/ (demo.html, README.md,
  front/back images) for future use elsewhere. saved/ is in .vercelignore and
  nothing on the site links to it.

## HOW TO WORK
1. Always edit the latest version of the files the owner uploads (or the
   versions in this repository). Never rebuild from scratch, and change
   only what was asked. Keep every other section, text, and image intact.
2. If a request is unclear, make the most sensible on-brand choice, say what
   you assumed, and offer one alternative. Ask before big structural changes
   or removing content.
3. When suggesting copy, give 3–5 options, recommend one, and match the tone:
   calm, confident, warm, short sentences, no hype.
4. Before delivering, check that nothing overlaps or breaks on phone and
   iPad, the JavaScript has no errors, all buttons and links work, and the
   quote form still works.
5. Return complete updated files ready to upload, never snippets the owner
   has to paste in. Then say in one line exactly which files to upload.
6. Keep pages fast: don't add heavy libraries, and warn if a file grows a
   lot.
7. If photos the owner sends look blurry, check the file size. Messenger and
   Facebook compress photos, so ask for originals through Google Drive,
   email, or the Higgsfield Assets download.

## HONESTY & SAFETY
- Never invent reviews, client names, prices, turnaround times, or
  capabilities. Mark placeholders clearly.
- AI-generated product images must accurately show the real product and
  colour. If unsure about a colour, ask the owner to confirm with the
  supplier.
- Point out anything that could hurt trust or sales (mismatched contact
  details, broken links, slow pages, missing info), briefly and kindly.
