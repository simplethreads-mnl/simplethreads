# Saved feature: Mockup studio print styles (not used on the site)

A "Print style" choice for the Mockup studio on design.html: DTG, DTF, Silk screen and
Embroidery (plus Sublimation in one version). It was on the site in Nov 2026 and removed at the
owner's request; the studio went back to its original single print look. Kept here for later use.
Nothing on the website links to this folder, and `.vercelignore` keeps it off the live site.

## Files
- `design-with-print-styles.html`: full design.html with DTG, DTF, Silk screen, Embroidery.
- `design-with-sublimation.html`: the same, plus Sublimation (enabled only on the white
  Dri-fit Polo, greyed out on other blanks).
- `print-styles.patch`: the exact changes (4-style version) against the plain design.html.

Both .html files are snapshots of the whole page from Nov 2026. If design.html has changed since,
don't copy a snapshot over it; add the parts below into the current page instead.

## Owner rules (Nov 2026)
- Embroidery: max 10 in wide or tall on every blank and spot (`EMB_MAX_IN`, `clampEmb`).
  Inches come from `ppi()`: the photo's SPOTS full-front spot = 11 in, full-back = 12 in.
  Switching to Embroidery or dragging past the limit sizes the design down with a message.
- Silk screen: only black, red, blue, green, white inks (`INKS`); the note shows the ink count.
- Embroidery: up to 6 thread colours (k-means) with a diagonal stitch texture and a soft shadow.
- Sublimation (sublimation version only): only on blanks listed in `SUBLIM`.

## Parts
- Markup: the "Print style" group (`#msMethods` buttons with `data-m`, `#msMethodNote`) before
  the Colour group.
- State: `st.method` (default "DTG").
- Logic: `METHOD_NOTE`, `ppi`, `clampEmb`, `paintMethods`, `setMethod`, `quantize`, the click
  listener on `#msMethods`, and clampEmb calls in `object:modified` / `object:scaling`.
- `composite()`: per-style drawing (fabric shading strength, DTF on top, embroidery shadow).
- The quote window pre-fills "Print or embroidery" with `st.method`, and the download file name
  includes the style.

## To reuse
Apply `print-styles.patch` to design.html (`git apply saved/print-styles/print-styles.patch`),
or copy the parts above by hand if the page has changed. Then retest the studio on phone and iPad.
