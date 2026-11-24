# Clothing rail hero (removed Nov 2026, owner: "remove the clothing rack for now")

index-with-rail.html is the full home page as it was with the 3D clothing rail,
its close-up view and the cream quick-quote window. To bring it back, copy from it:
1. CSS: the block starting "/* hero clothing rail" down to the reduced-motion `.rl-…` line.
2. HTML: `<div class="rl" id="rail">` + `<p class="rl-hint" id="railHint">` in the hero,
   and the "QUICK QUOTE WINDOW" `#quoteModal` block before the contact section.
3. JS: the `<script>` that starts "/* ===== HERO CLOTHING RAIL =====".
Images are still in images/rail/ and images/rail/soft/.
