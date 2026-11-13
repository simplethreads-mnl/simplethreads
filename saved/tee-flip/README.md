# Saved effect: floating tee turns to show its back (not used on the site)

Removed from the home page hero at the owner's request (Nov 2026) and kept here for later use elsewhere.
Nothing on the website links to this folder, and `.vercelignore` keeps it off the live site.

## Files
- `demo.html`: the effect on its own; open it in a browser to see it.
- `hero-tee-front.webp`: front of the tee (copy of `images/hero-tee.webp`, still used by the hero).
- `hero-tee-back.webp`: back of the tee with the large Simple Threads print (1294×1400, transparent).

## How it works
- Two images stacked in `.h3-flip`; the back one is rotated 180° and both hide their back face.
- `@keyframes h3turn` (10 s loop): hold front, turn through edge-on (slight scale dip) to the back, hold, turn back.
- The parents need `transform-style: preserve-3d` and the tilt layer `perspective: 1100px`, or the turn looks flat.
- Pause it when off screen (`.h3.off .h3-flip { animation-play-state: paused }`) and disable it under reduce motion.
- Do not put a CSS `filter` (such as drop-shadow) on the turning images: it makes the iPad redraw every frame.

## To reuse
Copy the CSS block and the `.h3-flip` markup from `demo.html`, move the two images into `images/`, and fix the image paths.
