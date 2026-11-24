---
name: web-studio
description: Professional web developer, web designer and logo designer playbook. Use for any website build, redesign, speed fix, SEO work, logo or brand mark, or when choosing stock photos, tools or a tech stack. Covers picking the right tool for the problem, performance (Core Web Vitals), on-page SEO, accessibility, logo design, and where to get licensed stock photos and when to use them.
---

# Web Studio playbook

Work like a senior studio: decide with evidence, change only what is needed,
measure before and after, and explain results in plain language.
Project rules (CLAUDE.md) always win over this playbook.

## 1. Pick the right tool for the problem

| Problem | Best fit | Avoid |
|---|---|---|
| Small brochure / portfolio site, owner edits by upload | Plain HTML + CSS + a little JS, hosted on Vercel or Netlify | Frameworks and build steps the owner can't run |
| Content site, blog, many pages | Astro (static output) or Eleventy | Client-side SPA (bad for SEO) |
| Web app with logins, dashboards, data | Next.js (App Router) or SvelteKit + Supabase / Postgres | Hand-rolled auth |
| Online shop | Shopify (or Shopify Buy Button on a static site); WooCommerce only if they already run WordPress | Building a cart from scratch |
| Owner wants to edit text themselves | Static site + headless CMS (Decap, Sanity) or Framer / Webflow | Raw HTML edits by a non-developer |
| Forms on a static site | Web3Forms, Formspree, Netlify Forms | Exposing an email address only |
| Scroll animation | CSS scroll-driven animations (`animation-timeline: view()`), IntersectionObserver for triggers | JS on every scroll frame, pinning |
| Complex timeline animation | GSAP (free incl. plugins) | Several animation libraries at once |
| Smooth scroll | Lenis, desktop pointer devices only | Smooth scroll on touch |
| 3D | CSS 3D for cards/rails; Three.js only when real 3D models are needed | WebGL for effects CSS can do |
| Image editing in the browser | Fabric.js or Konva | Canvas code from scratch |
| Icons | Inline SVG, Lucide, Phosphor | Icon fonts |
| Fonts | Google Fonts / Fontshare with `display=swap`, or self-host WOFF2 | More than 2 families or 4 weights |
| Images | WebP (AVIF if supported pipeline), Squoosh / sharp / Pillow | PNG/JPEG photos, images over 300 KB |
| Analytics | Vercel Analytics, Plausible, GA4 + Search Console | Many tracking scripts |

Rule: the simplest tool that meets the need and the owner can maintain wins.

## 2. Design fundamentals

- Start from a design system: colour tokens, a type scale (2 families max),
  spacing scale (4/8 px base), radius, shadow, motion durations.
- Hierarchy: one clear H1 and one main action per screen. Contrast, size and
  white space do the work, not extra colour.
- Layout: mobile first; check about 390 px (phone), 768/1024 px (iPad),
  1440 px (desktop). No horizontal scroll. Tap targets at least 44 px.
- Type: body 16–18 px, line height 1.5–1.7, line length 45–75 characters.
- Colour: text contrast at least 4.5:1 (WCAG AA); one accent colour for actions.
- Motion: purposeful, 200–600 ms for UI, transform and opacity only, respect
  `prefers-reduced-motion`.
- Copy: short sentences, real facts only, a clear call to action on every page.

## 3. Logo design

1. Brief: name, audience, 3 personality words, competitors, where it will
   appear (sign, label, embroidery, app icon, favicon).
2. Sketch 20+ ideas in black and white first: wordmark, lettermark, symbol,
   combination mark, emblem.
3. Build in vector (Figma, Illustrator, Inkscape). Use a grid and optical
   balance; outline the text when final.
4. Test: 16 px favicon, 1-colour (embroidery and screen print), reversed on
   dark, on photos, at sign size. Avoid fine hairlines that won't embroider.
5. Deliver a kit: SVG + PNG (transparent) + PDF; horizontal, stacked and mark
   only; black, white, brand colour; favicon (SVG + 180 px apple-touch-icon +
   512 px), social profile picture (1080 px) and an Open Graph image (1200×630).
6. Write short usage rules: clear space, minimum size, do and don't.
7. Never copy other brands' marks or use licensed characters.

## 4. Speed and smoothness (Core Web Vitals)

Targets: LCP under 2.5 s, INP under 200 ms, CLS under 0.1, on a mid phone.

Images
- WebP/AVIF, quality 80–90, sized to the largest display size (2x for retina).
- `loading="lazy"` + `decoding="async"` below the fold; hero image
  `fetchpriority="high"` and never lazy.
- Always set `width` and `height` (or `aspect-ratio` in CSS) so nothing jumps.
- `srcset`/`sizes` when one image serves phone and desktop.

Fonts
- `preconnect` to font hosts, `display=swap`, only the weights used, or
  self-host WOFF2 and `preload` the one used above the fold.

CSS and JS
- Inline critical CSS for small sites; `defer` scripts; load heavy libraries
  only when their section comes near (IntersectionObserver).
- No layout reads in scroll handlers; batch reads then writes; requestAnimationFrame.
- Animate only `transform` and `opacity`; `will-change` sparingly.
- `content-visibility: auto` on long below-the-fold sections.
- Avoid CSS filter/backdrop-filter on animated elements, big box-shadows on
  moving things, and `mix-blend-mode` on fixed headers.

Delivery
- Cache headers (vercel.json / netlify.toml): images a day or more with
  `stale-while-revalidate`; hashed assets `immutable` for a year.
- HTTP/2+ and compression are automatic on Vercel/Netlify.

Measure
- PageSpeed Insights (real-user data + Lighthouse), Chrome DevTools
  Performance with 4x CPU slowdown, WebPageTest. Record before/after numbers.

## 5. On-page SEO checklist

Every page
- Unique `<title>` (50–60 chars, main keyword + brand) and meta description
  (140–160 chars, a benefit + call to action).
- `<link rel="canonical">` to the live domain (one version: with or without
  www, always https).
- One `<h1>`, logical h2/h3 order, descriptive link text (not "click here").
- `lang` on `<html>`, viewport meta, descriptive `alt` on content images
  (`alt=""` on decorative ones).
- Open Graph + Twitter tags with a 1200×630 image, so links look good on
  Facebook, Messenger, Viber and X.
- Structured data (JSON-LD): `LocalBusiness` (or a subtype such as
  `ClothingStore`) with name, address, phone, email, url, logo on the home
  page; `BreadcrumbList` on inner pages; `Product`/`Offer` only with real
  prices; `FAQPage` only matching visible FAQs. Never fake ratings or reviews.
  Test in Google's Rich Results Test.

Site level
- `robots.txt` (allow all, block private folders, link the sitemap) and
  `sitemap.xml` with every public page.
- Google Search Console: verify the domain, submit the sitemap, check
  "Pages" for errors. Bing Webmaster Tools too.
- Google Business Profile with the same name, address and phone (NAP) as the
  site. Same NAP everywhere (Facebook, directories).
- Internal links between related pages; clean, lowercase, stable URLs; 301
  redirects when a URL changes.
- Fast, mobile-friendly, HTTPS: these are ranking factors too.
- Content: answer what customers search ("custom shirts Quezon City",
  "hoodie printing Manila") in real headings and paragraphs, not hidden text.

## 6. Stock photos: where and when

Free, commercial use allowed (check each photo's licence page):
- Unsplash, Pexels, Pixabay: lifestyle, texture, mood, workspace.
- Burst (Shopify): small-business and product-style shots.
- Rawpixel public domain, Openverse (filter "commercial use").
Paid, for exact needs and model releases: Adobe Stock, Shutterstock, Getty /
iStock, Stocksy (premium, editorial look).
Mockup templates: Freepik, Mockup World, Placeit, Smartmockups.
Illustrations/icons: unDraw, Humaaans, Lucide, Phosphor.

When stock fits
- Mood, texture and background (fabric close-ups, thread, studio light),
  blog headers, social posts, "about the process" scenes with no claim.
When it does NOT fit
- Portfolio, client work, team photos, the shop or products: these must be
  real. A stock photo presented as your work hurts trust.
- Anything with visible brands, logos or recognisable people used as customers.
How to use
- Match the site's palette and mood (grade or choose monochrome if the
  brand is monochrome), crop to the layout, compress to WebP under 300 KB,
  write a real alt text, keep a note of the source and licence.

## 7. Before you deliver

1. Check phone, iPad and desktop; nothing overlaps; no console errors.
2. Every link, button and form works (send a test form).
3. Lighthouse: Performance, Accessibility, Best Practices, SEO all 90+.
4. Titles, descriptions, canonical, OG image, structured data valid.
5. List exactly which files changed and must be uploaded.
