# Saved effect: line-drawn sewing machine (not used on the site)

Was the home hero visual (Nov 2026), replaced by the clothing rail at the owner's request and kept here.
Nothing on the website links to this folder, and `.vercelignore` keeps it off the live site.

- `demo.html`: the machine on its own; open it in a browser to see it.
- SVG + CSS only: the needle bobs (1.1 s per stitch), the fabric feeds left, stitches appear behind the needle,
  the handwheel turns, the spool wiggles. The thread piece above the needle clamp stretches with the needle
  (`.sew-tk`, scaleY) so it never looks detached.
- To reuse: copy the `<svg class="sew">` markup and the CSS block from `demo.html`; pause it off screen
  (e.g. `.off .sew *{animation-play-state:paused}`) and keep the reduced-motion rule.
