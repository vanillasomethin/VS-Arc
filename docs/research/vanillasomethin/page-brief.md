# vanillasomethin homepage brief

Source: https://vanillasomethin.framer.website/ -> local `/` (replaces template homepage).
Observed 2026-11-20 at 1440x900, 390x844 and 1920x1000 with real wheel/touch input (Playwright, Chromium).
Screenshots: `docs/design-references/vanillasomethin/` (`desktop-*`, `mobile-*`, `wide1920-*`). Assets: see `asset-map.md`.

## Page-wide rules

- **Framer breakpoints**: desktop `>=1440`, tablet `810-1439`, mobile `<=809`. Only desktop (1440) and mobile (390) were measured in depth; treat 810-1439 as desktop layout scaled down unless a builder checks it (counter font is 62px there; FAQ/team use desktop structure).
- **Page width**: every section is `max-width: 1440px; margin: 0 auto` (at 1920 the sections sit at x=240, body bg fills the sides). Content gutter **20px** both sides (content 1400 at 1440, 350 at 390).
- **Section padding**: desktop `100px 20px`, mobile `40px 20px` (Works has 0 bottom). Hero desktop `140px 100px 100px`, mobile `120px 20px 40px`.
- **Smooth scroll**: Lenis (`html.lenis`), Framer "Smooth Scroll" component intensity 10 -> `new Lenis({ duration: 1 })`, default easing. Anchor links (`./#section-about`, `./#section-hero`) scroll through Lenis (`lenis.scrollTo(target, { offset: -scrollMarginTop })`). Provided by foundation (`SmoothScroll.tsx`).
- **Custom cursor** (desktop pointer only): fixed white 16px circle, `z-index 13`, `pointer-events:none`, follows the pointer with **no lag**, positioned `translate(-50%, 0)` (horizontally centred on pointer, top edge at pointer y). Over a Works card (`data-cursor="view"`) it morphs into a white pill ~84x53 containing **"VIEW"** (Space Grotesk 500 22px, color = bg token). Provided by foundation (`Cursor.tsx`, hooks into `[data-cursor="view"]`).
- **Theme toggle** (nav, both widths): two token sets, persisted in `localStorage.theme` ("light" | "dark"). Default (no stored value) follows `prefers-color-scheme`: system light -> "light" = MAROON set; system dark -> "dark" = CREAM set. Icon: Phosphor **Sun** (bold) while maroon, **Moon** (bold) while cream; 20px, grows to 24px on hover. Implemented in foundation (`ThemeToggle.tsx`, `html[data-theme]`).
- **Color tokens** (CSS vars in `globals.css`, all sections must use them so the toggle works):

| token | maroon theme ("light", default) | cream theme ("dark") | used for |
|---|---|---|---|
| `--vs-bg` | `#380100` | `#ebe8e5` | page/section bg, service row bg, footer bg, pill-cursor text, hovered-button label |
| `--vs-fg` | `#ffffff` | `#0d0d0d` | body text, headings, borders (1px lines), button border/fill, cursor |
| `--vs-muted` | `#adadad` | `#4d4d4d` | section labels `[ABOUT]`, nav links, footer links, role line, carousel arrow circles |
| `--vs-inverse` | `#ebe8e5` | `#380100` | hero headline, contact headline, video-section sentence |
| `--vs-card-text` | `#fafafa` | `#fafafa` | Works card overlay text (constant) |
| text-reveal dim | `rgba(77,77,77,0.1)` | same | About text-reveal inactive words |

- **"Made in Framer" badge**: platform chrome, do NOT clone.

## Typography roles (computed)

| role | family | wt | desktop size/lh/ls | mobile | notes |
|---|---|---|---|---|---|
| logo line 1 "vanilla &" | The Seasons Bold | 400 | 26/23.4 (0.9) ls 1.3px (0.05em) | same | white(fg) |
| logo line 2 "somethin'" | Halimun Regular | 400 | 18/25.2 (1.4) ls 0.18px | same | sits under line 1 (y +25) |
| nav link | Space Grotesk | 500 | 16/24 | (menu 16/24 white) | uppercase text as typed, muted color |
| hero headline | Space Grotesk | 700 | 120/132 (1.1) ls 1.2px (0.01em) | 58/63.8 ls .58 | center, inverse token, chars animate |
| hero ticker | Inter | 300 | 16/24 uppercase | hidden | white |
| button label | Space Grotesk | 500 | 16/24 | same | uppercase as typed |
| section label `[ABOUT]` | Space Grotesk | 500 | 22/28.6 (1.3) ls -0.88px (-0.04em) | same | muted |
| body / paragraph (preset) | Inter | 300 | 16/24 | same | fg |
| text-reveal | Space Grotesk | 400 | 55/68.75 (1.25) ls 1.1px (0.02em) | 26/32.5 ls .52 | center, uppercase as typed |
| counter number | Space Grotesk | 700 | 96/normal | 48 (tablet 62) | fg |
| counter label | Aboreto | 400 | 16/24 | same | |
| h3 preset (philosophy titles, process titles, quotes, footer CONTACT) | Space Grotesk | 700 | 40/52 (1.3) ls 0.4px (0.01em) uppercase | 20/26 ls .2 (footer h3 mobile 32/41.6) | |
| works card title | Space Grotesk | 500 | 24/31.2 ls .24 | 22/28.6 ls -.88 (below image) | `#fafafa` desktop |
| works card client/category | Inter | 300 | 16/24 | category 12/18 | |
| service title | Space Grotesk | 500 | 24/36 (1.5) uppercase | 16/24 | center |
| service number / tag | Inter | 300 | 16/24 | same | |
| service ticker text | Space Grotesk | 400 | 16/24 uppercase | same | color bg token |
| video sentence | Inter | 300 | 20/30 | same | inverse token, chars animate |
| process number "01" | Space Grotesk | 500 | 22/28.6 ls -.88 | Inter 300 20/30 muted | |
| h5 preset (FAQ questions, cursor VIEW) | Space Grotesk | 500 | 22/28.6 ls -.88 | same | |
| team name | Inter | 300 | 16/24 | | role: Inter 500 14/21 muted, inline after name |
| contact headline | Space Grotesk | 700 | 96/124.8 (1.3) ls .96 capitalize | 36/46.8 ls .36 | inverse token, text "Big plans? Small questions? We're listening." |
| footer wordmark | Space Grotesk | 700 | 180 / lh 80% / ls -0.12em uppercase, fitted to 1440 width (SVG viewBox 1389.6x144 -> 1440x149) | fitted to 390 | fg at opacity 0.1 |
| footer small | Inter | 300 | 14/18.2 & 14/21 | same | |

Fonts are self-hosted with `@font-face` in `globals.css` (see Foundation). Space Grotesk is ONE variable file (wght 300-700).

## Shared motion presets (from the Framer bundle, verified live)

- **CharReveal (blur-in per character)**: each char `opacity .001, filter blur(10px), translateY(10px)` -> `1, blur(0), 0`. Spring bounce 0 duration **0.8s**, stagger **0.05s per char**. Hero headline: `onMount` (starts ~1.8s after navigation in a cold load, i.e. right after hydration); hero ticker same preset starts ~0.4s later; nav link labels use duration 0.4. Contact headline: same preset `onInView` (threshold 0, once). Implemented as `CharReveal` primitive (CSS transition per span, ease approximating spring: `cubic-bezier(0.22,1,0.36,1)` 0.8s).
- **Video sentence**: per char tween 0.8s ease `cubic-bezier(.44,0,.56,1)`, stagger .05, `onInView` threshold 1, **repeat** (reverses when it leaves view). Effect = opacity only (+blur 10px/y 10px preset). Use `CharReveal` with `repeat` + `easing` props.
- **FadeUp (Reveal)**: `opacity 0, y 20` -> `1, 0`, spring bounce .2 duration .4, **delay .4**, once, when 50% in view. Used by every section header (label + paragraph). Hero button: same with delay .8 (onMount). Nav: same (delay .4, onMount).
- **Counter rows**: `opacity 0, rotateX 80deg, y 40` -> rest, spring bounce 0 duration 1.2, 50% in view. Number counts 0 -> end linearly over **2s** (integer), starts when visible.
- **About floating images**: each `opacity 0, y 34` -> rest, spring bounce .2 duration 1.3, 50% in view; plus scroll parallax (see About).
- **Works cards**: `opacity 0, x 200` -> rest, spring bounce .2 duration .8, threshold 0 (one container per card).
- **Process cards**: `opacity 0, y 400` -> rest, spring bounce 0 duration 1 (first card delay .5), threshold 0. Measured: card fully settled ~0.6s after its top crosses the viewport bottom.
- **Testimonials block**: `opacity 0, y 400` -> rest, spring 1s.
- **Video**: wrapper `scale .1` -> `1`, spring bounce 0 duration 1 delay .5, 50% in view.
- Primitive `Reveal` in foundation takes `from` (x/y/rotateX/scale/opacity), `duration`, `delay`, `bounce`, `amount`; it uses `motion` springs (installed: `motion@14.14.0`).

## Shared controls

- **Outline button** (`OutlineButton`): `BOOK A CONSULTATION`, `SEE OUR WORKS`, `VIEW ALL`, `SEND A MESSAGE`. 1px solid fg border, radius 8, padding 8px 12px, height 40, label Space Grotesk 500 16/24 fg. Hover: a fg-colored "Bg Fill" blob (starts 32x10 at bottom centre, `translateX(-50%)`, top 59.7px i.e. below the button) grows to 200x64.5 at top -11.5 (scale 1, radius 8) filling the button; label turns bg color. ~0.5s spring (bounce .2). Overflow hidden.
- **Roll link** (`RollLink`): nav links + footer links. Two stacked copies of the label; on hover both translate up by one line (24px) so the second copy rolls in. Spring ~0.3s (measured 13.5px left at 50ms, settled 200-400ms). Color stays muted.
- **Section header** (`SectionHeader`): row; label (Space Grotesk 500 22, muted) left, paragraph (Inter 300 16/24 fg) right column at x=1020 w=400 (i.e. label column flex 1, paragraph width 400). Mobile: stacked, gap 20 (label first). FadeUp preset.

## Sections (in order)

Container IDs to keep: `section-hero`, `section-about`, `section-photography`, `section-works`, `section-awards`, `section-video`, `section-process`, `section-testimonials`, plus FAQ/Contact/Footer (no ids on source).

### 0. Navigation (`data-framer-name="Navigation"`) - FOUNDATION
- Desktop: NOT fixed (scrolls away), relative, z 6, padding 20, height 109 (inner 69). Left logo (2-line wordmark, links `#section-hero`), centre theme toggle (20px icon at x=710), right links `ABOUT` (`#section-about`), `ESTIMATOR` (`https://vanillasomethin.framer.website/estimator#section-hero`, out of scope), `WORKS` (`.../project-showcase`), `CONTACT` (`.../contact`), gap 8px, muted color, RollLink hover. Enter: fade-up y20, delay .4.
- Mobile (<=809): bar 350x46 at 20,20; logo left, toggle (40x40 box) at x=175, hamburger right (40x40, two 20x2 lines 10px apart, fg). Tap: lines rotate to -45/+45 (cross), nav expands to full-height panel (bg = bg token, ~951px tall) showing **"MILO THERON"** (Space Grotesk 500 16 uppercase, link `./`) above the logo, and centred links `ABOUT`, `WORKS`, `CONTACT` (white, 16/24, 64px pitch starting y=167). No ESTIMATOR in the mobile menu. Close reverses. Spring ~0.4s. See `mobile-01-menu-open.png`.

### 1. Hero (`#section-hero`) - min-height 90vh (810 at 900vh, 760 at 844), bg token
- Headline "PURE. PLAYFUL. PURPOSEFUL" (2 lines desktop: "PURE. PLAYFUL." / "PURPOSEFUL"; mobile 3 lines), top at y=362 desktop (253 into section). CharReveal onMount.
- Button `BOOK A CONSULTATION` -> `https://vanillasomethin.framer.website/contact`, centred, 48px below headline (y 666-706).
- Ticker row (desktop only) at bottom (y 827-851 page, ~60 from section bottom): `ARCHITECTS` . `DESIGNERS` . `VISIONARIES` - Inter 300 16 uppercase white, centred, items at x 457 / dot 617 / 688 / dot 836 / 885 (wide spacing). CharReveal onMount (after headline). It is static (no marquee).

### 2. About (`#section-about`) - padding 100 20, height 2635 desktop
- Header: `[ABOUT]` / "Where Functionality Meets Aesthetic, Your Architectural Journey Starts Here."
- **Text Reveal** block (1400 x 1539, starts 40px under header): sticky "Description" (top 80px, 1400x699) containing centred 800px-wide text: "WE ARE VANILLA & SOMETHIN. DESIGNERS OF SPACE, STORYTELLERS OF SIMPLICITY. OUR WORK CAPTURES THE SUBTLE TENSION BETWEEN STRUCTURE AND SOUL—WHERE THE ORDINARY TURNS EXTRAORDINARY." split into 25 words (`display:inline-block; margin-right:.25em`). Inactive word color `rgba(77,77,77,0.1)`, active fg; `transition: color .2s ease-in-out, filter .2s ease-in-out`. Driver: **continuous scroll**. Word *i* activates at scrollY = 860 + 30*i desktop (i.e. when the Text-Reveal block top is at ~247px - 30*i from viewport top; all on by top=-473). Mobile: 560 + 40*i (block top 462 - 40*i). Reverses when scrolling back. Below the text, `SEE OUR WORKS` button (-> `.../project-showcase`), fade-up.
- Four floating images (absolute layer "Images", 1400x479 at bottom of the block): 200x240 at left 40/top 239, 280x320 at left 40/top 0, 280x320 at right (x1140)/top 234 shifted -160, 200x240 at x1180/top -220 (positions relative to the layer; screenshots `desktop-02-*`). object-fit cover, no radius. Parallax: they travel ~1.3-1.4x scroll speed (move up 130-140px per 100px scrolled; Framer speeds 80/150). Appear: y34 fade.
  Images: `about-2.jpg` (left 280x320), `about-1.jpg` (left 200x240), `about-3.jpg` (right 280x320), `about-4.jpg` (right 200x240). Mobile sizes 100x114 / 120x137 / 100x120.
- Counter rows ("Counter Wrap", 1400 wide, 40px under text reveal): 4 rows, each padding 20 0, border-bottom 1px fg, height 162; number left (96px bold), right column x1020 w400: label (Aboreto 16) + paragraph (Inter 300 16, 10px below). Mobile: stacked (number 48, then label, then text), gap 20.
  1. **4** - "Years Experiences" - "Years of shaping spaces, stories, and identities. This isn’t just practice—it’s a creative evolution driven by vision, collaboration, and fearless design thinking."
  2. **101%** - "Satisfied Clients" - "Not just satisfied—they return. Every project runs smooth thanks to clear communication, precise results, and a process that feels natural."
  3. **28** - "Project Volume" - "From simple beginnings to layered expressions — our journey is shaped by curiosity, collaboration, and the pursuit of honest design."
  4. **36+** - "Global Clients" - "From Riyadh to Mangalore, We’ve worked with brands, agencies, and individuals who value design and a different point of view."

### 3. Design Philosophy (`#section-photography`) - 704 tall desktop
- Header: `[DESIGN PHILOSOPHY]` / "Our practice shifts between experimentation and restraint — exploring how spaces can feel intuitive yet deliberate, raw yet refined. The goal is simple: to make design that breathes and belongs."
- Accordion list at x=300 w=1120 (desktop), 40px under header. Items: padding 20, closed height 92; serial (Inter 300 16) + 20px gap + title (h3 40/52) followed by the "+" icon right after the title (gap 10): 14x14 box, two 2x14 fg bars radius 40 [export CSS]. One open at a time; click toggles. Open: plus rotates 45deg (becomes x), body paragraph (Inter 300 16/24, max-width 400 [export CSS], 20px under title) appears, height 92 -> 232; the image card (240x280, abs left 840 top 8 inside the item, `filter` none) fades in from `opacity 0, rotate(-10deg), size 285x317` to `opacity 1, rotate 0, 240x280`. While open, the image follows the pointer: `translate((pointerX - imgCenterX)*0.033, (pointerY - imgCenterY)*0.028)` with `transition: transform .15s ease-out`. Hover on a closed item: faint lighter fill (screenshot `desktop-05-philosophy-hover.png`). Height/rotation change ~0.4s spring. Desktop default: all closed. Mobile default: item 01 open (no image on mobile), titles 20/26.
  1. 01 UNBOUNDED REALITIES - "We believe architecture is not bound by walls or drawings but by the human eye that beholds it. Each space is a lived poem — formed from memory, instinct, and imagination. We design to awaken what already exists, to stretch perception beyond the seen." - `philosophy-1-unbounded-realities.jpg`
  2. 02 BEYOND THE MEASURED LINE - "Precision guides us, but not as a cage. We draw not to restrict, but to reveal — the silence between proportions, the dialogue between material and light. Every line holds a question; every shadow, an answer." - `philosophy-2-...jpg`
  3. 03 THE DIALOGUE OF BALANCE - "To design is to converse — between wildness and order, chaos and control, intuition and method. Like a steady rain, or a story told beneath a tree, each project finds its rhythm in balance — never static, always alive." - `philosophy-3-...jpg`
  4. 04 HUMAN REVERENCE - "Design begins where ego ends. We craft spaces that honour the human body — its pace, its breath, its need for belonging. Architecture, for us, is a gesture of humility — a place that receives, rather than commands." - `philosophy-4-...jpg`

### 4. Selected Works (`#section-works`) - padding 100 20 0
- Header: `[SELECTED WORKS]` / "These are the spaces that define us." + line break + "Each project unfolds a new dialogue between vision and structure."
- Grid: 2 cols x 5 rows, each card 690x600, gap 20 (x 20 / 730; row pitch 620), radius 8, overflow hidden, `data-cursor="view"`. Image cover (first card object-position `82.3% 0%`, others centre). Overlay bar ("Text 1"): full card width, 55 tall, vertically centred (top 272), `backdrop-filter: blur(5px)`, three items on one baseline: client left (padding-left 24, Inter 300 16 #fafafa), title centred (Space Grotesk 500 24 #fafafa), category right (padding-right 24). Hover: image `scale 1 -> 1.1` and `filter brightness(1 -> .5)`, ~0.6s ease-out; cursor becomes VIEW pill. Enter: x200 fade per card.
- Mobile: single column 350 wide, card block 600 tall = image (~536) + title (22px) + category (12px) BELOW image, left aligned, no overlay bar/blur.
- `VIEW ALL` outline button centred 40px under grid (-> `.../project-showcase`).
- Cards (client / title / category / href / image):
  1. John Salins / Flute-Case / Commercial - Office / `project-showcase/flutecase` / work-01-flute-case.png
  2. Sorbete / Fair-Fly / Commercial - Retail / `project-showcase/fair-fly` / work-02
  3. Mr. Sadath / Nord Terra House / Residential / `project-showcase/nord-terra` / work-03
  4. MAK Builders / MAK Park Square / Residential - Apartment / `project-showcase/mak` / work-04
  5. Mr. Ashraf / BNB House / Residential - Interiors / `project-showcase/bnb` / work-05
  6. Dip'N'Melt / Coco Meltdown / Commercial - Cafe / `project-showcase/coco-meltdown` / work-06
  7. Mrs. Fida / Artwist Salon / Commercial - Salon / `project-showcase/artwist-salon` / work-07
  8. Hyper Al Wafa / Seiko Hypermarket / Commercial - Retail / `project-showcase/seiko-hyper` / work-08
  9. Adoor Family / Koan House / Residential - Interior / `project-showcase/koan` / work-09
  10. Sorbete / Pipe Nova / Commercial - Retail / `project-showcase/pipe-nova` / work-10
  All hrefs are out of scope: prefix `https://vanillasomethin.framer.website/`.

### 5. Services (`#section-awards`) - padding 100 20, 1032 tall
- Header: `[SERVICES]` / "Each service is an extension of our design ethos — thoughtful, future-ready, and driven by the pursuit of timeless spatial quality."
- 12 rows, each 60 tall (mobile 48; long titles wrap to 2 lines on mobile), bg token background, padding 12px 8px, border-bottom 1px fg. Number left (Inter 300 16), title centred (Space Grotesk 500 24 uppercase), tag right (Inter 300 16). Rows 01-10 are `<a href="https://www.awwwards.com/" target="_blank">`; 11-12 are not links.
- Hover (desktop): row background -> fg (white), content layer fades to opacity 0 (~0.3-0.4s), revealing a **marquee** behind it: items `[80x24 image] [ticker text]` repeated, gap 40, padding 10, scrolling LEFT at ~40px/s continuously (time-driven, runs always; only visible on hover). Ticker text Space Grotesk 400 16 uppercase, color bg token.
- Rows (number / title / tag / ticker text / thumb):
  01 Architectural Design / Core / Concept Development · Schematic Design · Design Development · Construction Documentation · Sustainable & Passive Design · 3D Visualization / service-01
  02 Interior Design / Bespoke / Space Planning · Material & Finishes · Furniture & Joinery · Fit-out Drawings · Styling & Staging / service-02
  03 Landscape Design / Core / Master Planning · Hardscape Design · Planting Plans · Irrigation · Lighting · Maintenance Guidelines / service-03
  04 Urban & Master Planning / Strategic / Site Analysis · Feasibility Studies · Zoning & Regulations · Infrastructure Planning · Smart City Integration / service-04
  05 BIM & Digital Design / Advanced / BIM Modeling · Clash Detection · As-Built Models · Parametric Design · Digital Twin · Automation / service-05-08
  06 Visualization & Communication / Advanced / 3D Modeling · Rendering · VR Walkthroughs · Animations · Diagrams · Presentations / service-06
  07 Furniture & Product Design / Bespoke / Bespoke Furniture · Product Prototyping · Material Research · Ergonomic & Sustainable Design / service-07
  08 Heritage & Conservation / Specialized / Documentation · Measured Drawings · Adaptive Reuse · Restoration · Material Conservation / service-05-08
  09 Design Research & Innovation / Experimental / Material Innovation · Computational Design · Sustainability & Circular Design · Prototyping · Testing / service-09
  10 Authority Approvals & Compliance / Essential / Permitting · Regulatory Compliance · Fire & Safety · Consultant Coordination · Green Building Docs / service-10
  11 Project Management & Execution Support / Core / Design Supervision · Consultant Coordination · Site Inspections · Tender Docs · Post-Occupancy Evaluation / service-11 (no link)
  12 Future-Ready Solutions / Experimental / Smart Building Integration · Net-Zero / Energy Modeling · Digital Fabrication · Modular Systems · AR/VR · AI Design Integration / service-12 (no link)

### 6. Video (`#section-video`) - height 100vh (900/1000/844), overflow hidden
- Sentence "Each space a verse, each detail a heartbeat." top-left (x 44, ~140px into section), Inter 300 20/30 inverse token, per-char tween (repeat on re-entry).
- Video `vanilla-logo-reveal.mp4` (portrait 1080x1920) in a 1442x745 box centred in the section (box top ~77px into the section), `object-fit: scale-down`, autoplay muted playsInline, no loop, no controls. Box animates `scale .1 -> 1` (spring 1s, delay .5) when 50% in view; at scale .1 it is a 144x74 dot in the centre. See `desktop-08-video-mid.png`.
- Mobile: same, box 350 wide.

### 7. Process / Get Started (`#section-process`) - padding 100 20, 2858 tall
- Header: `[GET STARTED]` / "A simple, transparent process that turns your ideas into built reality — step by step."
- 4 cards in a column (gap 40) at x=300 w=1120. Card: padding-bottom 40, border-bottom 1px fg, gap 20: top row = number right-aligned (`01`, Space Grotesk 500 22); then row: image 400x520 radius 8 + text column (x 720, w 700, height 524): title (h3 40/52) at top, paragraph (Inter 300 16/24, ~400 wide) pinned to the bottom. No sticky. Enter: y400 fade per card.
- Mobile: number right (Inter 300 20 muted), image 350x180 radius 8, title (Space Grotesk 500 22) and paragraph below.
  01 CONNECT - "Share your project goals, vision, and requirements. A quick email or call helps us understand what you’re looking to create." - process-1-connect.jpg
  02 DEFINE - "We discuss your needs, develop a tailored proposal, and outline the scope, timeline, and deliverables — ensuring full clarity before we begin." - process-2-define.jpg
  03 DESIGN - "Through research, sketches, and 3D visualization, ideas evolve into tangible design concepts. You’ll see your vision take form with each iteration." - process-3-design.jpg
  04 DELIVER - "We finalize drawings, coordinate execution, and stay involved through completion — ensuring the design is built true to intent." - process-4-deliver.jpg

### 8. Meet the Team (`#section-testimonials`) - padding 100 20, 1055 tall
- Header: label text literally `MEET THE TEAM]` (source typo: missing "["; keep) / "We’re a collective of curious minds — architects, designers, and builders who thrive on collaboration and thoughtful design."
- Carousel ("slideshow"): viewport 800 wide centred (x 320-1120), overflow hidden, slide 800x~743 (mobile 340x505), gap 10, infinite loop, draggable (cursor grab), NO autoplay. Arrows: 40x40 circles bg muted token with arrow svg (`arrow-back.svg` / `arrow-next.svg`), at x=320 and x=1080 (inside the 800 frame edges), y ~352 into the carousel; mobile at x 25 / 325. Click -> slide by 810px, spring ~0.7s (67px at 50ms, 412px at 100ms, 686 at 200ms, 798 at 400ms).
- Slide: image 200x200 radius 8 centred; quote (h3 40/52 centred, 720 wide, 20px under image); then name (Inter 300 16) + role (Inter 500 14 muted) inline centred.
  Slides in order: (1) photo team-1-hisham, "“I believe good design begins by listening — to people, to place, and to purpose. Every line we draw should make life better, not just look beautiful. At Vanilla & Somethin’, my focus is on creating spaces that feel intuitive, grounded, and quietly bold.”" - Ar. Hisham Khalid / Principal Architect/Creative Strategisttional (sic). (2) team-2-zeba, "“For me, design is storytelling. Each project is a new chapter shaped by context, craft, and emotion. I enjoy bridging ideas and execution — ensuring that what we imagine together becomes something meaningful in the real world.”" - Ar. Zeba Ali Khan / Principal Architect/Creative Director. (3) team-3-hisham (quote 1). (4) team-4-zeba (quote 2). Quotes render uppercase via h3 preset.

### 9. FAQ (`data-framer-name="Section - FAQ"`, z-index 3) - padding 100 20, 886 tall
- Two columns: left 680 "Heading" **sticky top 40px**: `[FREQUENTLY ASKED QUESTIONS]` + paragraph "If you're curious about how we work, timelines, budgets, or what to expect when you start a project with us — this is a good place to begin." / "No jargon. No over-complication. Just straight answers." (two lines). Right column x=740 w=680: 10 accordion items (padding 20, closed height 68.6; divider = absolute 1px line, colour muted token at opacity 0.1 [export CSS]; OPEN item gets bg `rgba(77,77,77,0.06)` [export CSS]; question column 570 wide, plus 14x14): serial (Inter 300 16) + question (h5 22) + plus icon at right edge (rotates 45deg when open). Click toggles answer (Inter 300 16/24 paragraphs). Mobile: heading stacked above list, items 350 wide.
- Q/A (serials as on source; 08 repeats 3 times):
  01 How do I start a project with you? - "You can book a session by filling out the contact form on my website or reaching out via email. Let me know your preferred date, location, and any specific ideas you have in mind."
  02 Do you handle execution as well? - "Yes." / "We can manage everything — drawings, approvals, contractors, materials — or collaborate with your preferred team."
  03 How much will my project cost? - "It depends on size, scope, materials, and level of customization." / "Average starting ranges (India):" / "Architecture / New builds: ₹2,500–₹6,000 per sq.ft" / "Interiors: ₹1,800–₹4,000 per sq.ft" / "We share a rough estimate once we understand your requirements."
  04 Can you work within my budget? - "Mostly, yes." / "We’ll guide you on what’s possible and help adjust scope and materials to make things work."
  05 What affects the cost the most? - "Materials → finishes → complexity." / "Premium marble, custom furniture, or structural changes increase cost." / "Simple layout + standard finishes = more budget-friendly."
  06 Do I need a design team? Why not just hire a contractor? - "A contractor builds;" / "a design team plans, visualizes, optimizes space, and ensures everything works beautifully." / "It saves time, mistakes, and rework costs."
  07 Do you help with materials + contractors? - "Yes — we can manage everything or collaborate with your preferred vendors."
  08 How long will the project take? - "Renovations can take 2–4 months." / "New builds can take 8–16 months." / "Timelines vary based on approvals, materials, and complexity."
  08 Can we work together remotely? - "Absolutely." / "We’ve successfully delivered projects across cities using virtual collaboration."
  08 What’s your fee structure? - "We typically work with a percentage-based model or fixed slabs, depending on the scope ; as per Scale Of Charges set by the Council Of Architecture India" + link https://coa.gov.in/index1.php?lang=1&level=2&&sublinkid=299&lid=86
  (FAQ 01 answer may have more paragraphs; only one was observed.)

### 10. Contact CTA (`Section - Contact`, z-index 2) - padding 100 20, 690 tall
- Headline "Big plans? Small questions? We’re listening." (capitalize -> "Big Plans? Small Questions? We’re Listening." displayed UPPERCASE-looking because of capitalize? NO: screenshots show ALL CAPS because Space Grotesk caps; computed transform is `capitalize` and the visible result in screenshots is uppercase "BIG PLANS? SMALL QUESTIONS? WE’RE LISTENING." - match screenshots: render uppercase), 96/124.8, 3 lines centred, CharReveal onInView. Then "Tell us about your idea, your vision, or just say hi." (Inter 300 16 centred, 20px gap) and `SEND A MESSAGE` button (-> `.../contact`).

### 11. Footer (`Section - Footer`) - FOUNDATION
- **Curtain reveal**: footer is `position: sticky; bottom: 0; z-index: 1` as the last child of a flex column, so it is pinned to the viewport bottom THE WHOLE TIME (measured: footer top = 313px at every scroll position at 1440x900) and hidden only because every section above it is `position: relative` with an opaque bg and a higher z-index: **Hero z 3, About/Philosophy/Works/Services/Video/Process/Team z 2, FAQ z 3, Contact z 2**. Every section MUST keep `relative`, its z-index and `bg-vs-bg` (stubs already do), or the footer shows through.
- `<footer>` bg token, padding 100px 0 20px. Contact wrap padding 0 20, rows gap 20 (each row 52 tall): left h3 (`CONTACT`, `LOCATION`, `SOCIAL`, 40/52 bold uppercase; mobile 32) and right-aligned muted RollLinks separated by ", " / " | ":
  - CONTACT: `+91 7411 34 9844` (tel:+91 7411349844), `hello@vanillasometh.in` (mailto:)
  - LOCATION: `MANGALORE, INDIA |` and `RIYADH,SAUDI ARABIA` (both https://maps.app.goo.gl/W2b5YT7XH658UqPa9)
  - SOCIAL: `INSTAGRAM` (https://www.instagram.com/vanillasometh.in/), `PINTEREST` (https://www.pinterest.com/vanillaandsomethin), `LINKEDIN` (https://www.linkedin.com/company/vanilla-and-somethin) - all `target=_blank`.
  - Mobile: label above links (links left aligned).
  - 1px fg line under the rows.
- Bottom: padding-top 80; wordmark "VANILLA&SOMETHIN'" spanning full width (fitted), opacity .1; then copyright row (padding 0 20): left camera icon 14px + "Made with Framer by Hisham Khalid" (Inter 300 14), right "© 2026 Milo Theron All rights reserved." (Inter 300 14).

## Links summary
In scope: `#section-hero`, `#section-about` (Lenis anchor scroll). Out of scope (kept pointing at source): `/estimator#section-hero`, `/project-showcase`, `/project-showcase/<slug>` x10, `/contact` (hero button, contact button, nav), `https://www.awwwards.com/` (services 01-10), tel/mailto/maps/instagram/pinterest/linkedin, coa.gov.in.

## Unknown / not determined
- Exact spring curves are approximations of Framer springs (duration/bounce given).
- Tablet (810-1439) layout not measured beyond Framer's breakpoint list.
- FAQ answer-open animation timing not sampled precisely (looks ~0.3-0.4s height spring like philosophy).
- Hover fill colour of closed philosophy items read as transparent in computed style but a faint fill shows in the screenshot.

## Build chunk split (builders edit ONLY their files)

Foundation (done by recon, reuse, do not edit unless broken): `src/app/layout.tsx`, `src/app/globals.css`, `src/app/page.tsx`, `src/components/sites/vanillasomethin/{SiteHeader,SiteFooter,ThemeToggle,SmoothScroll,Cursor}.tsx`, `src/components/sites/vanillasomethin/primitives/{Reveal,CharReveal,OutlineButton,RollLink,SectionHeader,PlusIcon}.tsx`, `src/components/sites/vanillasomethin/data.ts` (all copy above as typed data).

1. **Hero + About** -> `sections/Hero.tsx`, `sections/About.tsx` (text reveal, floating images parallax, counters). Shots: desktop-00-load-*, desktop-01-hero, desktop-02-*, desktop-03-counters, desktop-04-*, mobile-00-hero, mobile-scroll-01..05. Assets: about-1..4.
2. **Design Philosophy + Works** -> `sections/DesignPhilosophy.tsx`, `sections/Works.tsx`. Shots: desktop-05-*, desktop-06-*, wide1920-02-works, mobile-scroll-06..20. Assets: philosophy-*, work-*.
3. **Services + Video** -> `sections/Services.tsx`, `sections/VideoSection.tsx`. Shots: desktop-06-works-viewall-services, desktop-07-*, desktop-08-*, mobile-scroll-15..17. Assets: service-*, video/vanilla-logo-reveal.mp4.
4. **Process + Team** -> `sections/Process.tsx`, `sections/Team.tsx`. Shots: desktop-08-video-settled (process header), desktop-09-*, desktop-10-*, mobile-scroll-18..23. Assets: process-*, team-*, arrow-*.
5. **FAQ + Contact** -> `sections/Faq.tsx`, `sections/Contact.tsx`. Shots: desktop-11-*, desktop-12-*, desktop-13-footer, mobile-scroll-24..30.

## Cross-check with the user's "Full Site Export" (`/tmp/claude-0/rz`, React/Vite, evidence only)

The export's components are static snapshots (its `SmoothScroll.tsx`/`Cursor.tsx` are empty divs; motion lives only as CSS classes + a `RevealWatcher` that sets `data-in` once at `rootMargin 0 0 -8% 0`). It agrees with the live measurements above. Values taken from it (marked [export CSS] above):
- Services marquee speed: every row `translateX(0 -> -Npx)` linear infinite at exactly **40 px/s**; N per row 01..12 = 2696, 1902, 1984, 2108, 1912, 2553, 1924, 2769, 2002, 1980, 2106, 2420 (one repeat-set width). Confirms the live 40.66 px/s sample.
- Reveal start transforms (all transition `795ms cubic-bezier(0.44,0,0.15,1)` in the export's approximation): y34 (about images), x400 (philosophy list container, threshold 1), y20 (headers), rotateX 80 + y40 (counters), x200 (works cards), scale .1 (video), y400 (process/team), per-char opacity .001 + y10 (+blur 10 live) with ~51 ms per char and ~28 ms extra at word boundaries. `rv-5` = about image 3 base offset y -160 (part of parallax, not a reveal).
- Accordion geometry: plus icon 14x14 / bars 2x14 radius 40; philosophy body max-width 400; philosophy image wrapper base `left 840, top 200, 240x280, opacity 0, rotate(-10deg), z-index 1` -> open `top 8, opacity 1, rotate 0`; FAQ open bg rgba(77,77,77,0.06); FAQ divider muted @ .1.
- Fonts: same files as the live page (Space Grotesk latin file `V8mDoQDjQSkFtoMM3T6r8E7mPbF4Cw` for 400/500/700, The Seasons/Halimun/Inter/Aboreto URLs). The export also lists Inter italic/700/900 faces that the homepage never requests; not downloaded.
- h3/h5 presets carry `font-feature-settings: "blwf","cv03","cv04","cv09","cv11"` (Space Grotesk alternates; also read live). Foundation `.vs-h3` / `.vs-h5` include them.
- Contact headline: computed `text-transform: capitalize` but every screenshot shows it ALL CAPS; render uppercase to match the screenshots.

## Foundation API (for builders)
- Tailwind tokens: `bg-vs-bg`, `text-vs-fg`, `text-vs-muted`, `text-vs-inverse`, `text-vs-card-text`, `bg-vs-fg`, `border-vs-fg`; fonts `font-grotesk`, `font-inter`, `font-aboreto`, `font-seasons`, `font-halimun`; CSS var `--vs-dim` for text-reveal inactive words. Text presets: `.vs-h3` (40/52 bold uppercase + features, 20/26 under 810px), `.vs-h5` (22/28.6 500 ls -.04em), `.vs-body` (Inter 300 16/24), `.vs-label` (Grotesk 500 16/24). Frame: `.vs-frame` (max-width 1440 centred). Breakpoint convention: `min-[810px]:` = desktop/tablet, `max-[809px]:` = mobile.
- `primitives/Reveal` (motion spring appear, `from/duration/bounce/delay/amount/trigger/perspective`), `primitives/CharReveal` (per-char blur text effect, `trigger/threshold/duration/stagger/delay/repeat/easing`), `primitives/SectionHeader` (label + 400px paragraph, fade-up), `primitives/OutlineButton`, `primitives/RollLink`, `primitives/PlusIcon` (`open`).
- `data.ts`: all copy, links, image paths. `icons.ts`: Sun/Moon/Camera paths.
- Page-wide: `SmoothScroll` (Lenis duration 1, anchors; instance at `window.vsLenis`; native scroll position stays valid for scroll-driven code), `Cursor` (add `data-cursor="view"` to Works cards), `ThemeToggle` (`html[data-theme]`).
- Section stubs keep the right ids and `vs-frame relative z-[2|3] bg-vs-bg` (Hero/FAQ z 3, others z 2) needed by the footer curtain; keep those classes on the root <section> when filling them.
