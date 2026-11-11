# Prachi Patel — personal site, Stem Cell run (round 3: "Plate VII")

**Client:** Prachi herself. **Direction:** antique celestial atlas (her brief, 2026-10-04).

## Why this exists
Round 1 (hand-built outside Stem Cell, 2026-10-04) was deleted at her request
("very buggy and ai generated... i asked for that personality web of my interests").
Round 2 (personality web, draggable nodes) she liked the *mind map* but rejected the
colors ("still full of primary colors"), the design, and the fonts.

Round 3 is her explicit brief: **a scientifically-accurate constellation atlas**.
Her interests are real constellations plotted from real J2000 catalog data
(positions, magnitudes, Bayer designations, spectral classes); clusters group by
real similarity, explained in-universe as the observer's log (the LARP).

## Build
- Single `site/index.html` + `site/art/` (9 paintings, WebP, from her Drive "my art" folder)
- **Sky view** — 3 interest constellations + 3 background neighbors + the Observer:
  - CASSIOPEIA = the hand cluster: Caph→jewelry, Schedar→painting (opens Pleiades),
    γ Cas→embroidery, Ruchbah→paper-mache fish, Segin dim
  - ORION = the systems cluster: Rigel→software (opens Big Dipper),
    Betelgeuse→geology, Bellatrix→space, belt + Meissa + Saiph dim
  - GEMINI = the signal cluster: Pollux→music, Castor→writing, Alhena→plants,
    Wasat/Mebsuta/Tejat dim
  - PERSEUS / TAURUS / SCORPIO dim background, name-only ("not mine; just the neighbors")
  - prachi patel = "the Observer", ringed star marker → about/facts/contacts panel
- **Big Dipper sub-view** (from Rigel): 8 repo stars from real UMa positions —
  Dubhe→stem-cell, Merak→keiko, Phecda→gneissvision, Megrez→fish-and-chips-sleep-tracker,
  Alioth→spotclean, Mizar→lens, Alkaid→petrova-log, Alcor→heliotrope;
  dashed 12′ Mizar–Alcor link ("the pair that watches"); click a star → repo card panel
- **Pleiades sub-view** (from Schedar): 9 painting stars from real arcmin offsets —
  Alcyone→nightshade detail view, Atlas→space, Electra→snklily, Maia→celeste,
  Merope→consumption 3, Taygeta→beach mountian, Pleione→duck 2, Celaeno→pug,
  Asterope→pug2; no connecting lines (true charts never connect a cluster);
  click a star → painting lightbox
- **Observer's log** (top-right): in-universe field notes — honesty framing
  (J2000 per figure, not to common scale), cluster binding similarities,
  Mizar/Alcor, Merope the lost Pleiad, Algol's 2.87-day blink
- Rendering: 4-point sparkle stars sized by magnitude, color by spectral class in
  desaturated antique tones (O/B #b9cbe8, A #dfe6f2, F #ece5d3, G #e3c896,
  K #d69a6d, M #c07f72) — no saturated/primary colors anywhere; aged-gold
  constellation lines with the staggered draw-in intro she liked; Cormorant Garamond
  names + Plex Mono designations; drag-to-pan sky; zoom transitions between views
- Stem Cell rules applied: dark-ground desaturation (the round-2 lesson, now in
  UI_TASTE.md), scientific accuracy with honest labeling, observer's-log LARP,
  sparse plain copy, headers > subtext, labels never wrap, touch targets ≥44px,
  reduced-motion respected, no AI credit

## QA (2026-10-04)
- Desktop 1440×900: all three views render north-up (verified Betelgeuse above
  Rigel, Segin above Schedar); every click flow passes — interest panels, all
  8 repo stars → correct repo card, all 9 painting stars → correct lightbox,
  observer panel (5 facts, 4 contacts), log panel (5 entries), dim-star hover
  tooltips, drag-pan, Escape ordering; zero JS errors
- Mobile 390×844: dedicated figure layout (interest band / observer / bg band),
  programmatic label-collision detection → zero overlaps; bottom-sheet panels;
  touch taps verified (Rigel→dipper, Alcor→heliotrope, Schedar→pleiades);
  zero JS errors
- Bugs caught and fixed: figures initially rendered south-up (sign error in
  projection); Mizar/Alcor 12′ pair needed nearest-wins hit testing; per-view
  intro clock (transition used to restart the draw-in); view changes now close
  open panels

## Deploy
- Preview worker: `prachi-web` (old `prachi-personal-site` worker deleted)
- Live: https://prachi-true-sky.prachidpatel1.workers.dev
  (content-verified: live page contains "Alcyone", not just HTTP 200)
- $0 spent. Preview-only: no GitHub push.
- Awaiting her iPhone verdict (round 4 if needed — 3 retries remaining)

## Round 4 — "one true sky" (2026-10-04, her three corrections)
- **Correction 1 — astronomically correct:** deleted the art-directed cluster
  composition and the separate fantasy sub-views. ONE pannable/zoomable
  equirectangular sky (x = RA 0–24h with wraparound drag, y = Dec, clamped
  −40°/+70°); every constellation at its real relative J2000 position from the
  catalog data — Cas ~1h/+60, Per ~3.5h/+45, Tau ~4.3h/+15, Pleiades 3h47m/
  +24°07′, Ori ~5.5h/0°, Gem ~7.5h/+22°, UMa dipper ~11h/+55°, Sco ~16.5h/−30°.
  Schedar (painting) flies to the true Pleiades; Rigel (software) flies to the
  true Big Dipper; "return to the sky" zooms back out. Initial framing RA
  ~23h–9h (wrapping). Edge-hint pills ("SCORPIUS →", "URSA MAJOR →",
  "POLARIS · THE OBSERVER") for offscreen figures, suppressed when zoomed in.
  The Observer star moved to Polaris (α UMi, 2h31m/+89°15′), ringed, opens the
  about/contact panel; header keeps a Polaris link. Sizes exaggerated for
  tappability, honestly footnoted ("positions J2000 · star sizes exaggerated ·
  one sky, one scale"). Zoom via +/− buttons (now bottom-left), double-tap,
  pinch, wheel; staggered draw-in; reduced-motion; Escape ordering kept.
- **Correction 2 — fonts she likes:** Playfair Display 700/800/900 + italics
  for ALL display type (title, star names, panel headings, poetic subtitles);
  Cormorant Garamond removed entirely. IBM Plex Mono kept for designations
  (17 Tau, α Ori) and data labels.
- **Correction 3 — stars drawn her way:** canvas reimplementation of her recipe
  (studied from site/art/space.webp + the sleep tracker's dstars SVG layer):
  (a) soft radial-gradient halo behind bright stars, (b) concave-sided 4-point
  sparkle (quadratic sides, control point at center) in desaturated antique
  spectral tints (O/B #b9cbe8, A #dfe6f2, F #ece5d3, G #e3c896, K #d69a6d,
  M #c07f72), (c) hot white core dot at 90%, (d) long thin cross flares
  (vertical 6×R, horizontal 3.4×R) on the brightest stars only (mag<1.6),
  (e) gentle staggered twinkle (±15%). Dim field stars: tiny sparkles/dots,
  no halo. Flat straight-edged sparkles gone. All content preserved verbatim:
  8 repos, 9 paintings, 4 contacts, 5 fact rows, all interest copy, Log
  (rewritten for the true sky, in-universe voice kept).
- Label engine: on-screen-only labels, viewport clamping, radial
  leader-line labels with angular-gap enforcement + wrap-aware sectoring +
  edge-mirroring for tight clusters (Pleiades when zoomed, Cas on mobile);
  figure captions; programmatic overlap detection in QA.
- **QA (2026-10-04):** JS syntax clean; desktop 1440×900 — home 13 labels,
  pleiades 9, dipper 8, polaris 1, ZERO overlaps; mobile 390×844 — home 6,
  pleiades 9, dipper 3, polaris 1, ZERO overlaps; fly-to both ways, zoom
  buttons (±1.6×), repo card, lightbox, observer/log panels, pan, Escape all
  pass; zero JS errors (one sandbox-only Google-Fonts fetch failure inside
  the VM's Chromium — curl from the VM returns HTTP 200, fonts will load on
  her iPhone). Screenshots read and approved by the worker.
- **Deploy:** same preview worker `prachi-sky` (account
  41da1e5c3d737ecaf1e600f05ee10a29); live
  https://prachi-true-sky.prachidpatel1.workers.dev verified: contains "Alcyone",
  title "prachi patel — plate vii · one true sky". $0 spent. Preview-only.
  Awaiting her iPhone verdict (round 5 if needed — 3 retries remaining).

## Round 5 — Insight Melody font swap (2026-10-04, her order: "no use the font from heliotrope")
- She rejected Playfair Display. **Insight Melody** (her Heliotrope wordmark/title
  font) now serves ALL display type: site title, star names, panel headings,
  poetic subtitles, ledes, repo descriptions, log entries, lightbox captions,
  edge-hint pills (title-cased, arrow falls back to Plex Mono).
- Self-hosted: `site/fonts/InsightMelody.otf` (53 KB) declared via @font-face
  (weight range 100–900, no faux bold); Google Fonts link now loads only
  IBM Plex Mono. IBM Plex Mono kept for catalog designations (17 Tau, α Ori),
  data labels, tooltips, and chrome — scientific labeling, not display type.
- Script-legibility sizes: star names 18/21px (was 14/16), subtitles 19/23px,
  wordmark 1.9rem, panel titles 2.5rem, ledes 1.4rem, log entries 1.28rem —
  all bumped because script x-heights read small.
- The wider script broke label layout, so the label engine grew teeth (all
  verified by programmatic box checks, not eyeballing):
  - canvas labels avoid the HTML chrome (wordmark top-left, nav top-right);
  - labels clamp inside the viewport vertically (true extents, not centers);
  - radial labels: line-height 19/22 (was 12/13), wider sectors, pairwise
    de-collision, chrome avoidance;
  - figure captions render in a second pass and candidate-nudge clear of
    labels, earlier captions, and chrome; captions also avoid the bottom
    chrome (hint pill + microline); x-clamped to viewport;
  - edge-hint pills nudge clear of labels and captions;
  - data fixes: Bellatrix below-star + lo x:-25, Rigel below-star + lo x:-60,
    Castor lo x:-48, Merak lo y:+55, Ruchbah lo x:-100 (unjammed the
    Perseus/Cassiopeia/Pleiades caption pile-up), UMa caption to bottom.
- **Legibility note for her verdict:** Insight Melody at 18–21px is readable
  for star names and headings, but long-form script (log paragraphs, repo
  descriptions) is inherently harder to scan than a serif — in Heliotrope
  itself she uses it only for wordmark/titles with system-ui body. If she
  finds body text tiring, recommend restricting the script to display type.
- **QA (2026-10-04):** desktop 1440×900 — 13 labels + 7 captions, ZERO overlaps,
  zero chrome collisions, zero offscreen; mobile 390×844 — 6 labels +
  5 captions, ZERO issues; fly-to (Schedar→Pleiades, Rigel→dipper), panels,
  lightbox, zoom, pan, Escape all pass; zero JS errors. Screenshots read.
- **Deploy:** same worker `prachi-true-sky`; live
  https://prachi-true-sky.prachidpatel1.workers.dev verified: title
  "prachi patel — plate vii · one true sky", contains "Alcyone",
  /fonts/InsightMelody.otf serves 200 (53,468 bytes, font/otf). $0 spent.
  Preview-only. Awaiting her iPhone verdict (round 6 if needed — 3 retries
  remaining).

## Round 7 — the 3D celestial sphere (2026-10-04, her pick over the cinematic chart)
- **What changed structurally:** the flat 2D chart is voided. The site is now a
  true 3D celestial sphere (Three.js r160, self-hosted at
  `site/vendor/three.module.min.js`, no CDN): the camera sits INSIDE a sphere
  of radius 100 and all 58 content stars are plotted at true 3D RA/Dec
  positions (J2000, north-up). Custom orbit controls (drag w/ inertia,
  wheel/pinch/double-tap/buttons zoom via fov 20–115, idle auto-spin after
  6s, off under prefers-reduced-motion). Star sprites bake her recipe
  (concave 4-point sparkle + halo + hot core + flares on mag<1.6) to canvas
  textures, tinted per spectral class, sized by magnitude (exaggerated,
  footnoted). Milky Way = ribbon mesh on the true galactic equator with
  procedural amber brightness + dark lanes; faint RA/Dec graticule; M42 glow
  in Orion's sword; M31 elongated smudge; 12 subtle teal/copper nebula wisps;
  occasional shooting star.
- **Cluster mapping (her final):** CASSIOPEIA=HAND (Caph jewelry,
  Schedar painting→Pleiades, γ Cas embroidery, Ruchbah fish), ORION=FIELD
  (Betelgeuse geology, Bellatrix space, Rigel plants), GEMINI=MIND (Pollux
  music→Big Dipper, Castor writing, Alhena software). Perseus/Taurus/Scorpius
  dim neighbors. Polaris (α UMi) double gold-ringed = the observer, opens
  about/contact. Schedar→true Pleiades (9 painting stars, tap→lightbox);
  Pollux→true Big Dipper (8 repo stars, tap→repo card); "return to the sky"
  flies home. Observer's Log rewritten for hand/field/mind.
- **Art-direction pivot (Carina "Cosmic Cliffs" ref):** deep teal space
  #07222e, copper constellation lines #d29a5e, warm ivory labels, glowing
  amber MW band, teal nebula wisps. Pleiades cursor (desktop fine-pointer
  only): 7 brightest in true relative pattern, lerped follow, native cursor
  hidden over canvas. Chromatic-aberration fringing baked into the 9 Pleiades
  star textures (tasteful RGB split). Dismissible hint bar visible by
  default + visible zoom buttons.
- **Text system (her Heliotrope rule):** Insight Melody = display only
  (wordmark, panel titles, constellation/star names). ALL body copy
  (panel ledes, log paragraphs, repo blurbs, lightbox captions, hints) =
  system-ui sans, 1–1.08rem, 1.75–1.85 line-height. Strict hierarchy:
  title > section head > body > meta. Plex Mono = catalog designations only.
- **Zoom behavior:** starts zoomed out (fov 92, opening sweep 112→92);
  LOD tiers — 0 (fov≥64): figure captions only; 1 (44–64): + interest star
  names; 2 (fov<44): full detail (designations, repo/painting lines), figure
  captions hidden. Clicks zoom: caption click flies into the figure; star
  click flies to fov 30 then opens its panel/lightbox on arrival.
- **Readability QA (top gate):** programmatic label-overlap audit
  (?audit=1 writes boxes to title) — home/dipper/pleiades/mobile all ZERO
  overlaps. Fixed in QA: de-collision rewritten (symmetric 40-pass
  relaxation, clamp-per-pass — the old down-only push was undone by the
  bottom clamp on the Pleiades); figure captions hidden below fov 44;
  +26px swash pad on label widths (Insight Melody capitals paint past their
  advance widths — "Dubhe" rendered 110px in a 66px box); top clearance
  accounts for the back button; mobile header wraps to two rows (all links
  visible); mobile microline clears the zoom buttons.
- **Interaction QA:** tap Alkaid→petrova-log panel→Escape closes; caption
  click zooms 92→44; Polaris header link flies + opens about panel;
  return-to-sky restores fov 92; zoom buttons; lightbox opens w/ her painting
  + Escape closes; reduced-motion = no spin, instant draw-in. Screenshots
  read at 1440×900 and 390×844. Zero JS errors.
- **Compromises:** Google Fonts (Plex Mono) still CDN — graceful fallback to
  monospace offline; everything else self-hosted. The M42/Rosette copy
  ("the rosette nebula (M42)") is her verbatim text — factually M42 is the
  Orion Nebula, not the Rosette; flagged, not silently edited.
- **Deploy:** same worker `prachi-true-sky`; live
  https://prachi-true-sky.prachidpatel1.workers.dev verified: HTTP 200,
  title "prachi patel — plate vii · the celestial sphere", "Alcyone"
  present, /vendor/three.module.min.js serves 200. $0 spent. Preview-only.
  Awaiting her iPhone verdict.
- **Round 4 (2026-10-04): real Milky Way texture, deeper zoom, winter sky, palette, Scorpius removed.**
  - **Milky Way texture (winner: NASA SVS Deep Star Maps 2020).** Leads checked in her
    priority order: (1) Stellarium's milkyway.png = Axel Mellinger's panorama, per-project
    license, not cleanly reusable — rejected; (2) OpenSpace — no single clean equirectangular
    texture found; (3) 2MASS — public domain but IR false-color; (4) ESO eso0932a (CC BY 4.0,
    credit S. Brunier, verified at eso.org/public/copyright) kept as fallback. Winner:
    NASA/Goddard Scientific Visualization Studio Deep Star Maps 2020
    (https://svs.gsfc.nasa.gov/4851) — 1.7 billion real stars (Hipparcos-2 + Tycho-2 +
    Gaia DR2), plate carrée ALREADY in ICRF/J2000 RA/Dec (RA 0h at center, RA increasing
    left; verified against openagents PROVENANCE.md) so NO galactic→equatorial reprojection
    was needed. Public domain (NASA). Credit on the on-page honesty note:
    "NASA/Goddard Space Flight Center Scientific Visualization Studio, from Gaia DR2
    (ESA/Gaia/DPAC) — public domain." Bright catalog stars are omitted from the product,
    so her sprite stars sit on top with no doubles. File:
    `site/art/milkyway-equatorial.jpg` (4096×2048, 797KB, q80). Mapped on a custom-UV
    sphere (uv recomputed per-vertex from each vertex's own RA/Dec — alignment by
    construction; texture.flipY=false). Procedural amber ribbon + 12 nebula wisps removed;
    M42 glow and M31 smudge kept. **Structure stays the survey's** (band path, dark rifts,
    galactic-center bulge position) — verified: bulge brightest at RA~270°/Dec~-28°,
    band passes through Cas/Per/Tau/Gem/Aur/CMa stars, Orion sits off-band.
  - **Decisive Carina recolor** (her override of "grade gently"): pixels recolored firmly
    into sampled `palette-carina.png` tones — deep teals #06374f/#084a68/#09688c background,
    golden #d9a45c star clouds, copper #ce7151 + red #d95f43 warm regions — while luminance
    structure (the astronomy) is untouched. Star sprites re-tinted golden/red by spectral
    class; constellation lines, rings, UI gold → copper #cf7a44; renderer clear → deep teal.
  - **Deeper zoom:** star clicks fly to fov 12 (was 30); zoom range floor 20→10 (wheel,
    pinch, buttons); caption clicks 30→18 (Pleiades/Ursa Major) / 44→30 (others); empty-sky
    tap zooms to min 14; flyTo targets deepened (dipper 18, pleiades 16, polaris 26).
    Panel still opens on arrival. Verified: desktop 1440×900 + mobile 390×844 — Betelgeuse
    at fov 12 + geology panel frames well (bottom sheet on mobile).
  - **Winter sky:** added Canis Major (Sirius), Canis Minor (Procyon), Auriga (Capella),
    Lepus, Aries, Andromeda as dim non-interactive bg figures at true J2000 RA/Dec
    (all line endpoints validated). **Scorpius removed entirely** — stars, lines, labels,
    copy; the Log notes honestly that it's a summer constellation sitting this one out.
  - **QA:** node --check clean; zero JS errors across all headless runs; desktop +
    mobile screenshots read and confirmed (band through her constellations, credit renders
    in the Log). Live: https://prachi-true-sky.prachidpatel1.workers.dev — root 200,
    /art/milkyway-equatorial.jpg 200 (797,444 bytes, image/jpeg). $0 spent. Preview-only.
    Structural retries used: 3 of 4 — one left. Awaiting her iPhone verdict.

## 2026-10-04 — label de-collision + iPhone feedback batch 2 (deployed)
- **Labels:** de-collision rewritten to separate along the axis of least penetration
  (was vertical-only), minimum gaps raised (16px x / 14px y), 60 passes, x clamped
  per-pass. Betelgeuse/Bellatrix now sit ~15px apart at fov 30 on 390×844.
- **Auto-spin removed** — the sphere sits still at rest; opening sweep kept, never resumes.
- **Drag 1:1** — inertia drift removed (velocity zeroed on release).
- **Constellation chips** — 13 thumb-friendly tap-to-fly chips (Cassiopeia→Andromeda)
  in a scrollable bottom row; zoom buttons raised to clear the taller chrome.
- **Color back** — star tints saturated (vivid gold/red), halo + Pleiades fringe boosted;
  Milky Way rebaked: Gaussian-denoised (silky, grain gone) + saturation/contrast lift,
  band structure / dark rift / bulge preserved.
- **QA:** ?audit=1 home mobile 0 overlaps; fov 30/16/12 mobile + desktop home all
  0 overlaps, screenshots read; no-spin verified (0 drift over 9s); chip tap flies to
  fov 30; drag moves view with 0 post-release drift; zero JS errors throughout.
  Live: https://prachi-true-sky.prachidpatel1.workers.dev — root 200,
  /art/milkyway-equatorial.jpg 200 (608,679 bytes). $0 spent. Preview-only.

## 2026-10-05 — repair round: texture artifacts root-caused + fixed (deployed)
Her iPhone verdict was "unusable bad." Diagnosed from her actual screenshots, reproduced
both rendering artifacts in headless Chromium (390x844 DPR2), fixed the causes:
- **Pole starburst (root cause):** equirectangular pole-pinch — the texture's noisy top
  rows (per-pixel std ~20 at Dec=+90deg) get stretched radially where all meridians
  converge. Fixed in the texture bake: rows above |dec| 75deg fade (smoothstep) toward
  the dec~70deg mean — kills the high-frequency pinch with no visible brightness lid.
  Verified: ?view=polaris shows a smooth pole, no radial streaks.
- **Vertical banding (root cause):** texture-seam smear, not grain. The code overwrote
  SphereGeometry's built-in seam-duplicate UVs with per-vertex u = ((0.5 - ra/360) % 1
  + 1) % 1, so triangles crossing the RA 180deg meridian interpolate u from ~0.0003
  through 0.5 to ~0.9997 — smearing the entire sky width into one full-height stripe
  (visible at RA~180deg, right in the Big Dipper view). Fixed: toNonIndexed() + raw
  u = 0.5 - ra/360 (no modulo) + per-triangle unwrap at the ra=0 branch cut +
  RepeatWrapping. Verified: ?view=dipper shows no stripe.
- **Texture rebaked from scratch:** NASA SVS Deep Star Maps 2020 8k EXR (130 MB)
  processed MINIMALLY — exposure + luminance-preserving Reinhard tonemap + sRGB,
  gentle denoise only (NO saturation hammer; the last 1.5x bake is what emphasized the
  grain), gentle teal-shadows/golden-highlights grade via smooth curves. 4096x2048,
  JPEG q85 4:4:4, 2.05 MB. Before/after crops verified: silky, no banding, band path /
  dark rift / bulge structure true to the survey. Credit unchanged: NASA/Goddard SVS,
  Gaia DR2 (ESA/Gaia/DPAC), public domain.
- **Stars bigger:** magScale 0.85-3.4 -> 1.6-5.6 world units (exponent -0.25 -> -0.22);
  field-star point sizes now multiplied by renderer.getPixelRatio() (were fixed 1.1).
  Sprite recipe untouched (concave 4-point sparkle + halo + hot core + flares).
- **Label overlaps (root causes):** (a) captions were measured while display:none ->
  cached 0-width boxes; now shown BEFORE measuring. (b) captions were missing the
  +44px swash pad (star labels had +26) — why ?audit=1 passed while POLARIS/URSA MAJOR
  painted over each other on her phone. (c) caption nudge upgraded to 10 tries each
  direction (down then up) against all placed boxes. (d) the fixed "RETURN TO THE SKY"
  button is now a real getBoundingClientRect() avoidance rect inside the 60-pass
  relaxation loop (was a topPad heuristic). Caption name+subtitle stay one glued
  block; document.fonts.ready re-trigger already existed.
- **Copy:** "draw the living world in Latin" deleted everywhere (lede + draws fact
  row) — she disowned it. Lede ends "...I turn annoyances into tools."; draws row is
  "paintings." Plain, no invented voice.
- **QA:** zero JS errors on every run; screenshots READ at 390x844 DPR2 — polaris
  (no starburst, Polaris label clear of return button), dipper (no seam stripe, 7
  labels separated, Dubhe clear of button), Orion at fov 30 (Bellatrix/Betelgeuse
  cleanly separated, stars bigger and vivid), home (Pleiades/Orion captions clean);
  ?audit=1 0 overlaps; desktop 1440x900 spot-check clean.
  Live: https://prachi-true-sky.prachidpatel1.workers.dev — root 200 (74,302 bytes),
  /art/milkyway-equatorial.jpg 200 (2,051,851 bytes), byte-verified. $0 spent.
  Preview-only. Structural retries used: 3 of 4 — one left. Awaiting her iPhone verdict.

## Round 7 — subtitle fixes + full Carina recolor in HDR (2026-10-05)
- **Subtitles (her: "don't make sense"):** exact replacements — 'the big dipper ·
  the software ledger' -> 'the big dipper · eight repositories' (caption + repo
  panel title + 'fly to the big dipper' button), 'the observer · the one fixed
  star' -> 'the observer', 'neighbors, not mine' -> 'neighbors' (Perseus, Taurus),
  'winter neighbors · not mine' -> 'winter neighbors' (6 winter figures), Log
  sentence "winter neighbors, not mine" -> "winter neighbors". All replacements
  are shorter than the originals, so collision risk is strictly reduced.
  Untouched per brief: 'the hand cluster', 'the field cluster', 'the mind
  cluster', 'the sketchbook · nine paintings', and the Log prose lines 265
  ("the one fixed star") and 280 ("where the software ledger lives") — FLAGGED:
  same disowned phrases survive in Log voice copy; parent to decide.
- **Full Carina recolor, zero quality loss:** re-downloaded NASA SVS Deep Star Maps
  2020 8k EXR (130 MB); ALL color work in 32-bit linear HDR before quantization
  (never graded the JPEG): exposure + Reinhard, smooth-curve grade — teal shadows
  (R-30%/G+20%/B+42% in darks), orange midtones (R+34%/G+12%/B-32% gaussian bump),
  golden highlights (R+32%/G+10%/B-30%), red-giant boost, 1.28x chroma lift;
  polar de-pinch via per-row FFT horizontal gaussian blur (sigma ramps 0->6px from
  |dec| 65-88 deg) — kills equirect pinch streaks, preserves large-scale color,
  no flat "lid". BUG FOUND+FIXED mid-bake: pole fade used .mean(axis=0) giving a
  per-column (4096,3) reference -> vertical streaks; corrected to scalar mean, then
  replaced the fade entirely with the blur ramp. Lanczos 8k->4k, sRGB, JPEG q90.
  Output: site/art/milkyway-equatorial.jpg (4096x2048, 3,751,445 bytes).
  Bake script of record: ~/workspace/.bake/bake_mw.py (EXR at ~/workspace/.bake/starmap_8k.exr).
- **QA:** ?audit=1 home mobile 0 overlapping pairs; screenshots READ at 390x844
  DPR2 — home (band sweeps through, PLEIADES/ORION captions clean), polaris
  ("the observer" subtitle, clear of return button, natural pole, no lid/streaks),
  dipper deep zoom (8 repo labels separated), desktop 1440x900 (4 captions clean,
  band through Cassiopeia/Gemini/Pleiades/Orion). Zero JS errors (only
  sandbox-blocked Google Fonts request; loads on her phone). Before/after crops:
  galactic center (rich gold, dark rift true), Orion (teal + gold, silky).
  Credit unchanged: NASA/Goddard SVS, Gaia DR2 (ESA/Gaia/DPAC), public domain.
  Live: https://prachi-true-sky.prachidpatel1.workers.dev — root 200 (74,160
  bytes), texture 200 byte-identical. $0 spent. Preview-only. Structural retries
  used: 3 of 4 — one left. Awaiting her iPhone verdict.

## Round 8 — greedy priority decluttering (2026-10-05, finishing interrupted work)
- **Problem:** Pleiades fly-to showed 9 stacked labels (names + designations +
  painting titles all piled). Previous agent died mid-implementation (daemon
  restart); touch Pleiades cursor + starPriority() survived, placement did not.
- **Greedy placement (Stellarium-style):** star labels sort by (pri asc, mag asc)
  — observer 10, interest 20, repo/painting 30, other 40 — and place
  highest-priority first. Each star tries 8 anchors in order (above, below,
  right, left, 4 diagonals); the first anchor whose box clears already-placed
  boxes, the return-button rect, and viewport clamps wins. Anything that can't
  fit is `display:none` — never stacked, never pushed into another label.
  Captions keep their glued name+subtitle blocks with directional nudging.
- **Progressive detail tiers:** `deep` threshold moved fov < 24 -> fov < 14.
  Cluster fly-tos (fov 18) show star NAMES only; star taps fly to fov 12 where
  the full triple (name | designation | repo/painting title) appears.
- **QA (screenshots READ at 390x844 DPR2):** Pleiades fov 18 — 7 clean separated
  names (Alcyone, Atlas, Electra, Maia, Merope, Taygeta, Pleione), 0 designation
  lines, zero stacking; fov 12 — full triples visible (e.g. "Alcyone | η Tau |
  nightshade detail view"); home mobile audit 0 overlapping pairs; desktop
  1440x900 clean. Touch cursor follows fingertip (opacity/transform verified),
  taps unaffected. Zero JS errors (only sandbox-blocked Google Fonts).
- **Ship:** deployed to prachi-true-sky, curl-verified root 200 and byte-identical
  to local (75,083 bytes). $0 spent. Preview-only. Structural retries used:
  3 of 4 — one left.

## Round 9 (2026-10-05) — 4th & FINAL structural retry: SkyView-brief rebuild
Her brief from SkyView-style reference screenshots: hybrid drawn stars, research
2-3 astronomy apps, far-view constellation name + simple interest subtitle,
stable labels, easier movement + real menu, zoom subtitles = element names,
hybrid photo->painted background on deep zoom.

- **RESEARCH.md** (new, in site dir): full report on SkyView / Star Walk 2 /
  Stellarium Mobile + Stellarium desktop source. Findings applied: (1) ART — all
  apps draw stars as procedural sprites, never photos; Stellarium's Milky Way
  photo fades out between FOV 2.5°→0.25° so zoom never shows blur. (2) MOVEMENT
  — direct 1:1 touch tracking, no inertia in Stellarium; fly-to uses
  easeInOutQuart (≥1s) / easeOutQuad (<1s). (3) LABELING — priority-ordered,
  zoom-gated label budgets, fade in/out (never pop), greedy overlap rejection.
- **Drawn stars:** concave 4-point sparkle + halo + hot core + flares on
  brightest, golden/red tints, at 2.6–9 world units (bigger, same relative
  magnitude curve). Sizes already footnoted as exaggerated.
- **Hybrid background:** procedural 2048×1024 Carina-palette painting (teal
  gradient, soft blotches, golden wisps along the TRUE galactic band computed
  from the north galactic pole, dark rift, galactic-center glow — zero grain).
  Crossfade photo→painted as fov goes 40→18 (smoothstep); deep zoom fully
  drawn, sharp at any level. Palettes matched for seamless blend (verified in
  screenshots at fov 40/30/24/18/12).
- **Movement:** true 1:1 tracking (radians-per-pixel derived live from fov +
  viewport each frame — old 0.0038 constant was ~2× too fast). Release velocity
  = windowed ~120ms average (robust to event spacing); gentle momentum capped
  24 px/frame, exp(-5.5·dt) damping — glides then always settles (verified:
  fast flick → ~20° coast over ~2s, then 0 drift). No auto-spin at rest.
- **Menu:** slide-in bottom sheet (type system: Insight Melody titles,
  system-ui body, Plex Mono designations) — the sky (13 constellations fly-to),
  interests (digital art + 9 hand/field/mind elements), archives (Pleiades
  paintings, Big Dipper repos), observer (Polaris about/contact, log). Chip row
  removed. Thumb-friendly, closes on fly-to/Escape.
- **Labels:** far view = constellation name + simple interest word only (hand,
  field, mind, digital art, eight repositories, the observer); "digital art"
  replaced "the sketchbook · nine paintings" everywhere. Stability: CSS
  transitions on transform/opacity, placement re-runs only on significant view
  change, TIME-based hysteresis (pumpFlips applies pending show/hide every
  frame — fixed a bug where the old run-counted hysteresis never fired under
  the stability gate, leaving stale captions visible). Zoom subtitles (fov<14)
  = element name: Pleiades→"digital art", Big Dipper→"eight repositories"
  (fixed: was showing painting titles like "snklily"). Fixed zombie-label bug:
  measurement forced display:block on labels the greedy then declined, leaving
  them visible with _shown undefined — now corrected in wantShow.
- **QA (all screenshots READ at 390×844 DPR2 + 1440×900):** zero JS errors;
  ?audit=1 home = 0 overlaps; drag test tracking ratio 1.00; momentum settles;
  crossfade seamless at 6 fov steps; Pleiades fov 16/12/24, Orion, menu open,
  desktop — all clean, no overlaps, no zombie labels. flyTarget extended with
  all constellations (was missing 'orion' etc.).
- **Ship:** deployed to prachi-true-sky (canonical URL), curl-verified HTTP 200
  and live build contains the fixes. $0 spent. Preview-only. Structural
  retries used: 4 of 4 — this was the final one.

## Round 10 — her redirect (2026-10-05, ~15:00 ET): new constellation map + ice-blue palette
- **New map:** Polaris=intro ("start here", menu lists it first), Ursa Major=tech
  projects (untouched), Pleiades=about me (9 factual facet cards, plain copy),
  Perseus=digital art (9 paintings moved here; 4 real stars added — ξ Per
  Menkib, ο Per Atik, ρ Per Gorgonea Tertia, π Per Gorgonea Secunda, true J2000
  RA/Dec/mags, verified via Wikipedia/SIMBAD), Cassiopeia=fabric arts (γ Cas
  embroidery stays; Schedar placeholder panel, Caph plain, Ruchbah plain),
  Orion=jewelry (Betelgeuse real panel; Bellatrix/Rigel honest "to come"
  placeholders), Auriga=hire me (plain copy + contact links), Canis Major=
  writing (Sirius; "book reviews — coming soon" gap noted in-panel), Gemini=
  background neighbors. Parked (data kept): music, software, geology, space,
  plants, fish. Big Dipper/photography: on hold awaiting her answer.
- **Palette:** ALL copper/orange removed per her call — star tints, UI accents,
  painted canvas, photo regrade. New accent cold light ice blue (#a9d6f2);
  starfield cool white-blue; backgrounds stay deep teal. Photo re-graded cool
  in the 32-bit pipeline (bake_mw.py): 0.07% warm pixels remain, mean B>G>R.
  GitHub language dots on repo cards kept (functional, not accent).
- **Hero stars:** root-caused the faint-sprite issue (magScale cap pinned bright
  heroes at 14; Pleiades about-stars weren't flagged heroes at all). Now:
  hero scale raw×3.0 cap 20 floor 7.5; bigger/harder texture core + hot white
  center; tighter halo falloff; about-stars included in hero flag; photo
  quieted 30% at far view. Zoom compensation reworked to (tan(fov/2)/tan25°)²
  so deep zoom holds near-constant screen size — the Pleiades cluster stays
  9 distinct stars instead of one blob.
- **Menu:** sections start here / the sky / interests (7 destinations) /
  the observer. Observer's log entries rewritten for the new map.
- **QA (screenshots READ at 390×844 DPR2 + 1440×900):** zero JS errors;
  ?audit=1 zero overlaps (9 boxes); far view shows bold cool heroes with name
  + subtitle; tap Alcyone→about panel, Mirfak→painting lightbox,
  Capella→hire-me, Sirius→writing, Schedar→fabric placeholder, Merope
  (unlabeled)→about panel — all direct, designation detail lines present;
  Pleiades/Perseus/Auriga/Canis Major/Cassiopeia fly-tos clean; deep zoom
  fov 10 distinct; desktop clean.
- **Ship:** deployed to prachi-true-sky (canonical URL), curl-verified HTTP 200,
  index.html + regraded milkyway-equatorial.jpg both byte-identical live.
  $0 spent. Preview-only.
- **Content gaps needing her:** jewelry inventory (Betelgeuse panel is the real
  one; Bellatrix/Rigel are "to come" placeholders), fabric-arts pieces beyond
  embroidery (Schedar placeholder), book reviews (noted in writing panel).

## Round 11 — her update (2026-10-05, ~15:45 ET): final ten constellations
- **GEMINI → photography** (my pick for her "move photography to another
  constellation" — bright, prominent, content-free; she can veto). Pollux
  anchors the panel; photos unknown — honest "to come" placeholder panel.
  Music/software stay parked.
- **TAURUS → geology.** Aldebaran anchors the geology panel (real content:
  gneissvision repo link); other Taurus stars stay as figure background. The
  Pleiades sit inside the Taurus sky region — both figures kept, labels
  declutter via the greedy placer (verified coexisting: Aldebaran/geology +
  Alcyone/ai/ml engineer + Atlas/geology minor side by side).
- **Background constellations DELETED** per her "the rest don't need to be
  here": Canis Minor, Lepus, Aries, Andromeda — figures, stars, lines,
  captions, menu entries all gone (grep-verified zero references). Final 10:
  Polaris, Ursa Major, Pleiades, Perseus, Cassiopeia, Orion, Auriga,
  Canis Major, Taurus, Gemini. The NASA photo still supplies the full
  starfield behind them. Observer's-log m31 line reworded (no Andromeda
  figure to reference).
- **Menu:** sky section lists exactly the 10; interests now 9 destinations
  (+ photography, + geology). sr-only nav updated too.
- **QA:** zero JS errors; ?audit=1 zero overlaps; Pollux→photography panel
  (desig "Pollux · β Gem"), Aldebaran→geology panel (desig + repo link);
  far-view screenshots read — bold cool heroes, no deleted-figure traces.
- **Ship:** deployed to prachi-true-sky, curl-verified HTTP 200 and
  byte-identical live (first curl caught pre-deploy edge state ~8s after
  upload; re-curl confirmed). $0 spent. Preview-only.
- **Content gaps needing her:** jewelry pieces (Bellatrix/Rigel placeholders),
  photography photos (Pollux placeholder), book reviews (writing panel note),
  fabric arts beyond embroidery (Schedar placeholder). Parked: music,
  software, space, plants, fish (+ painting interest entry).

## Round 12 — 2026-10-13 (defect repairs from her iPhone review + Roboto subtitles)
- **Captions pinned:** figure captions now sit exactly at the projected centroid of
  their constellation — no declutter nudging, no star-avoidance shove. If the home
  block doesn't fit (edge/chrome/caption collision) the caption fades out instead
  of moving (astronomy-app behavior). Verified per-figure: caption center within
  0–1px of the figure's star centroid at fov 52 for all 10 figures.
- **Hero stars for every figure's majors:** was flag-only (interest/repo/painting/
  about), which left Orion's belt, Elnath, Castor, Sirius's companions etc. as dim
  smudges while all-repo Ursa Major blazed. Now hero = flagged OR mag ≤ 2.6 OR
  top-3 brightest of the figure. Added heroes: Caph; Elnath, ε Tau; Alnitak,
  Alnilam, Mintaka, Saiph; Castor, Alhena; Mirzam, Wezen, Adhara, Aludra;
  Menkalinan, θ Aur.
- **Scaling audit:** magScale table is monotonic (hero 20.0/20.0/17.4/10.5/7.5/7.5
  and non-hero 11.0/11.0/7.8/4.7/2.8/2.6 world units at mag −1.5/0/1/2/3/4);
  angular extents from the data match the real sky (Orion 19.9°, Gemini 20.2°,
  Big Dipper 25.7°, Pleiades 1.1°). Positions are true J2000 — the bunching is
  real (winter constellations, RA 3h–7.5h). Nothing moved.
- **Roboto subtitles shipped:** Roboto 400;500 loaded; --sub var drives
  .lbl .th, .cap .cs, .menu-item .ms. Bayer designations stay IBM Plex Mono.
- QA: zero JS errors; ?audit=1 zero overlaps (mobile + desktop); deploy
  curl-verified HTTP 200, byte-identical to local. $0. Preview-only.

## Round 13 — 2026-10-13 (the spread, approved by Prachi 2026-10-13)
- Her content constellations were all winter figures bunched in RA 3h–7.5h.
  Five interests moved to figures spread across the whole sky; positions stay
  true J2000, only the topic assignments changed:
  geology Taurus→**Leo** (Regulus), hire me Auriga→**Boötes** (Arcturus),
  digital art Perseus→**Lyra** (Vega; all 9 paintings, brightness order,
  indices/titles/metadata kept), photography Gemini→**Aquila** (Altair),
  writing Canis Major→**Pegasus** (Markab + Scheat).
  Kept: Polaris, Cassiopeia, Pleiades, Orion, Ursa Major.
- Retired figures removed completely (figures, lines, captions, menu, fly-tos,
  sr buttons). Star data: standard catalog J2000 RA/Dec + visual mags; Lyra's
  nine verified against Wikipedia's List of stars in Lyra (κ Lyr really is at
  RA 274.97°, west of Vega; δ2 Lyr mag 4.22). Spans from the data: Leo 30.4°,
  Boötes 26.3°, Lyra 11.4°, Aquila 22.0°, Pegasus 38.8°.
- Lyra fly-to tuned to fov 28 so all nine stars fit the portrait frame
  (κ and η included); Leo/Pegasus fly at the generic 30 — at fov 40 the
  photo sky swallows their lines and sprites.
- Observer's Log updated (lyra entry; sheliak note replaces algol; winter-sky
  line rewritten for the four-season spread). Painting lede now "hang in
  Lyra". Menu sky list runs Polaris first, then by RA.
- QA: zero JS errors; ?audit=1 zero overlaps (mobile + desktop); fly-to
  screenshots read for all 10 figures; DOM sweep shows no retired names.
  Deploy curl-verified HTTP 200, byte-identical. $0. Preview-only.

## Round 14 — 2026-10-15 (her three calls: no name tag, Polaris home, no flipping)
- **"prachi patel / the observer" label removed.** Polaris itself carried her
  name as a star label; the label is gone everywhere. The star stays (hero,
  double ring, tappable → intro panel). Wordmark and panel copy untouched.
- **Home = Polaris centered.** HOME is now ra 37.95 / dec +89.26 at fov 88/92;
  measured projection lands at exact screen center (195,422 on 390×844).
  Opening sweep now spirals in from ra +55 / dec 58. Fly-to Polaris targets
  the real pole (was a dec-80 proxy). Side effect: Cassiopeia's caption
  hides at home rather than sit under the zoom buttons (chrome avoidance
  now includes #zoomctl); it returns on any pan.
- **Labels fixed in the sphere.** The greedy 8-anchor placer, the placement
  stability gate, and the CSS transform transitions are all gone. Every
  label is projected from its sky anchor every frame: captions at figure
  centroids (as round 12), star labels hanging directly under their stars.
  Declutter may only hide a lower-priority label whose fixed rect collides
  — positions never move, so nothing drifts, glides, or flips sides.
- **Navigation is yaw/pitch, never roll.** State is (ra, dec, fov); drags,
  fly-tos, and zoom anchoring all compute in ra/dec. Dec clamps at ±89.5°
  (the old clamp was -55/+88 with a renormalize that skewed the view), ra
  wraps fully, ra steps widen by 1/cos(dec) capped ×6. Screen up is always
  celestial north: the whole sphere is reachable (deep south and both polar
  caps verified) and the sky can never end up upside down.
- QA: local Playwright (SwiftShader) — home, mid-sky, deep south (dec -62),
  south cap (-89.5), synthetic drag at the pole, Pleiades and Polaris
  fly-tos. Zero JS errors; labels verified under their stars.
- KNOWN CAVEAT: the NASA photo texture smears near the exact poles at deep
  zoom (equirectangular pinch, pre-existing in the asset) — visible in the
  fov-26 Polaris close-up as a soft wedge. Fixable via pole-cap rebake if
  she wants it; not touched this round.
- Status: built + QA'd locally, preview attachment sent 2026-10-15 — but the
  single-file attachment can't run the multi-file site standalone ("its not
  loading", her report 2026-10-16). Deployed to the canonical preview URL
  2026-10-16 so she can review it live; curl-verified byte-identical to the
  QA'd local build. Her iPhone verdict on round 14 still pending.

## Round 14b — 2026-10-16 (scroll calibration, her ask: "make scrolling easier")
- **Drag model corrected.** Round 14's ra/dec drag steps distorted at the
  pole (home!): horizontal drags raced the center around the tiny polar
  circle. Drags again rotate the view direction about the screen's own axes
  (grab-the-sky), in ≤3px substeps, with a pole clamp (clampOffPole) that
  stops the center at dec ±89.5° and refuses pole crossings — full range,
  never a flip. ra/dec remain the canonical state for fly-tos/zoom and are
  re-derived after each drag. QA: view rotation matches the drag angle to
  0.01° against an independent simulation, mid-sky and at the pole.
- **First-pixel tracking:** the 6px tap/drag threshold no longer eats the
  travel before it — rotation is measured from the last applied position
  (rotX/rotY), so tracking is 1:1 from the finger's first pixel.
- **Caption dead zones removed.** Captions were pointer-events:auto blocks:
  a drag starting on one silently never started (home's Polaris caption sat
  at screen center!). Captions are click-through now; their taps route
  through the canvas tap path via labelBoxes (star under the tap still
  wins; otherwise the tap flies to the figure — verified live in QA).
- **Pleiades fingertip cluster glued:** the follow-lerp (0.16/frame, ~100ms
  trail) no longer applies while a touch is active — the cluster sits
  exactly on the fingertip (QA: transform matched the touch point to the
  pixel). Desktop hover keeps the soft lag.
- Deployed to the canonical preview URL 2026-10-16, curl byte-identical.
  Awaiting her feel-test (the real calibration): star under finger, cluster
  placement, circling Polaris.

## Round 15 — 2026-10-17 (flip root cause + geometric stars)

Her feel-test came back with two reports: (1) "The sky is continuously
flipping on mobile — but the cursor is staying under my finger" (the 14b
cursor fix confirmed working); (2) with a screenshot: "The stars are too
circular, make them pretty and geometric."

- FLIP ROOT CAUSE (the miss in rounds 14/14b): the drag math was exact —
  but applyView derived the camera's up vector FRESH from the pole every
  frame (celestialUp(dir)). Near a pole that up is hypersensitive: home IS
  the pole (dec 89.26), so as her finger wandered, the view center circled
  the pole and "north up" wheeled with its azimuth — the whole sky
  continuously reoriented even though the center tracked perfectly. QA had
  only ever measured the center, never the roll.
- FIX: the view now keeps a PERSISTENT up vector, parallel-transported
  (each frame it is only re-orthogonalized against the current direction —
  the least rotation the motion forces). Drag axes come from the
  transported up. Fly-tos ease up to the destination's canonical north-up
  (targetUpFor; within 4° of a pole, the meridian tangent — home's up is
  the tangent of increasing dec at ra 37.95). RM path sets it instantly.
- MEASURED (same circling drag at home, both models scored on the screen
  bearing of a fixed reference point): pole-derived up swung +81° in the
  first quarter of the gesture with direction reversals (the wheel);
  transported up drifted a smooth +28° total with no jumps — and that
  drift is the genuine bearing change of dragging the center ~20° across
  the sky, present in any correct model.
- STARS: sprite recipe rebuilt. The old one was a big soft halo ball
  (Ø 0.96 of sprite, alpha .42) plus a ROUND white core (Ø ~0.26) with a
  small sparkle inside — on her phone it read as pale moons, exactly as
  her screenshot showed. New (256px canvas): a crisp 4-point star
  POLYGON (long vertical point = 0.40 of sprite for heroes / 0.26
  standard, horizontal 0.62×, faceted waist at 0.17), cut-gem facets
  (lighter top triangle, deeper bottom), a tiny white DIAMOND core instead
  of a disc, glow cut to a tight whisper (radius 0.30, alpha .20/.13),
  diffraction spikes thinner and fainter. Chroma (cursor) variant uses the
  same polygon with the RGB fringe offsets. Sizes/magnitudes untouched —
  the footprint is the same, the shape carries it now.
- CHROME (visible in her screenshot, fixed while in there): on phones
  .topright never wrapped internally, so MENU/LOG + GITHUB/ART/LINKEDIN/
  POLARIS ran off the right edge and clipped. .topright now wraps (links
  get their own right-aligned row), the hint pill wraps inside 94vw
  instead of clipping "drag" off-screen, the mobile back button drops to
  9.6rem (measured clear of the links row, bottom 144px), and the label
  topPad on mobile is 152px to match the taller two-row header.
- Label behavior double-checked after the orientation change (a scare:
  an Orion fly-to screenshot at +2.6s showed no labels): placement is
  intact (labelBoxes: Betelgeuse, Bellatrix; Alcyone at the Pleiades) —
  the fade-in hysteresis just takes seconds at the sandbox's ~1fps; on a
  real phone it resolves in ~200ms. Not a regression.
- Deployed 2026-10-17 to the canonical preview URL, curl byte-identical
  (99,712 bytes). Awaiting her iPhone verdict: circle Polaris slowly (no
  wheeling), and the new star shapes.

## Round 16 — 2026-10-30 (neat framing + easier star taps)

Her words: "When I click a constellation it should neatly zoom in a place
where all the stars are visible. Right now clicking a star isn't easy."

- FRAMING: fly-tos used a fixed fov table (30° for most figures, 16–28 for
  a few). On a portrait phone the horizontal fov is a fraction of the
  vertical, so wide figures were silently cropped (Pegasus spans ~39°).
  Now the landing fov is SOLVED per figure (fitFovFor): a scratch camera
  at the figure's centroid with the destination's canonical up binary-
  searches the smallest fov that puts every one of the figure's stars
  inside the label safe rect (3% margin), clamped [6, home fov]. All three
  fly-to call sites (flyTarget, caption taps, menu items) share
  figureFit(). Measured landings (390×844, all stars verified inside the
  safe rect through the real camera): cas 23.4, ple 10, ori 29.4,
  leo 67.8, uma 50.2, boo 40.8, lyr 26.7, aql 39.5, peg 70.7.
  Two traps caught in QA: a scratch camera needs updateMatrixWorld(true)
  before project() (nobody renders it, so its matrixWorldInverse is
  identity and every fit reads garbage — the first pass landed everything
  at the clamp); and the cap must be the home fov, not 64 — Pegasus
  honestly needs ~71 on a portrait phone, which IS the neat framing.
- TAPS: hitStar's catch radius was max(24, screenR+8)px and a tap died if
  the finger drifted >8px. Now max(38, screenR+14) on mobile (nearest star
  within it wins, so the dense Pleiades stay sane) and taps tolerate 16px
  of fingertip drift on mobile (10 desktop). Verified: a tap 29px off
  Betelgeuse's center opens it; a 12px-drift wobble tap on Alcyone opens
  it (the old rule turned that into a drag).
- Sandbox note: the local Chromium now refuses to start without the Hatch
  WebGL domain-policy switches (--hatch-webgl-allowed-domains-file +
  --hatch-webgl-allowed-domains-sha256; an all-origins policy file works
  for local QA). Recipe recorded in TOOLS.md.
- Deployed 2026-10-30 to the canonical preview URL, curl byte-identical
  (101,805 bytes). Awaiting her iPhone verdict.

## Round 17 — 2026-11-03 (the Pleiades landing, fixed for real; star patches gone)

Her verdict on round 16: "if I click Pleiades it should zoom in with all
the stars visible with the correct captions. This view is too small and
doesn't even look accurate to the constellation. Also on the main page
can you see how those stars with the transparent backgrounds still
aren't an aesthetic."

Root causes found (three separate clamps conspired, plus bad data):
1. fitFovFor's binary search never probed below fov 9 (early return),
   and flyToDir/zoomBy/pinch all clamped fov to >= 10. The Pleiades'
   true fit is ~3.4°, so it landed 3x too wide. Search now starts at
   2.5°, zoom floor is 3 everywhere.
2. Four Pleiades positions were wrong vs J2000 (Alcyone ra +0.27, Maia
   +0.31/+0.15, Merope dec -0.15, Asterope ra +0.50 — Asterope sat on
   Alcyone's RA). Corrected; the little-dipper shape is the real one.
3. Labels: at the deep tier, name+subtitle blocks (~116x43) under each
   star could only fit 2 of 9 in the cluster. Now tier-2 labels are
   name-only mini (18px, h 22, tighter collision pads), sprites are
   screen-capped at deep zoom (hero 84px / standard 60px diameter —
   the zk compensation saturates below fov ~13 and sprites ballooned
   to ~150px and merged), and tier-2 labels anchor on the side of
   their star AWAY from the figure centroid (deepDir; bearing is a
   pure function of the sky geometry per frame, so labels stay fixed
   in the sphere), rotated by anchorFit only as far as needed to stay
   on screen. The fit stays label-aware ONLY for tight figures
   (starFit < 20): an all-fovs label fit is non-monotonic across the
   tier-44 boundary and dragged Orion/Lyra landings out to 44.
   Result: Pleiades lands at fov 3.37 with 8 of 9 labels placed
   (Celaeno — 14px from Maia on the sky — still shares; a small pan
   separates them). Other landings unchanged (cas 23.4, ori 29.4,
   lyr 26.7 with 7 labels now, peg 70.7).
4. The "transparent backgrounds": every star sprite carried a
   full-canvas radial glow wash (alpha .22-.30). Over the photo it
   reads as a translucent patch/sticker behind each star. Removed
   from both star textures; the sparkle body, spikes and the tight
   core halo carry the star now.
- Deployed 2026-11-03 to the canonical preview URL, curl byte-identical
  (109,113 bytes). Awaiting her iPhone verdict.

## Round 18 — 2026-11-05 (zoom, THEN the option for detail)

Her screenshot showed the failure plainly: she tapped URSA MAJOR and
got Alioth's spotclean panel over a wide view — "when I click on Ursa
Major it should zoom in and show all tech projects not simply show
this one or another one. Zoom then option for detail." Cause: the tap
pipeline ran hitStar BEFORE the caption check ("a star under the tap
wins"), and the caption sits on the figure centroid amid the stars,
so a caption tap almost always landed inside some star's generous hit
radius. This supersedes the 2026-10-05 "opens the project directly,
no intermediate step" rule for constellation-level taps.

New flow in endPointer:
- Star hit + multi-star figure + current fov > the figure's fitted
  fov x 1.3 -> fly to the figure's fitted view (all its stars, all
  labels), NO panel. Once in the view, star taps open panels — even
  when the caption overlaps the star (caption-first was tried and
  killed exactly that case; the zoom-state test is the arbiter).
- No star hit + caption hit (capHit) -> same fly.
- Single-star figures (Polaris/intro) unchanged: direct panel.
QA (real taps, sandbox 390x844): far Dubhe tap -> fov 50.2, no panel;
in-view Alioth tap -> spotclean panel; Polaris at home -> intro
panel; zero JS errors. (Caption-only branch shares figureFit/
flyToDir with the proven paths; sandbox caption placement at wide
fovs is too flaky to tap-test directly.)
- Deployed 2026-11-05, curl byte-identical (109,704 bytes). Awaiting
  her iPhone verdict.
- Side finding, verified by projection: the rendered sky is MIRRORED
  east-west vs the real sky (our radecVec swaps two axes — a
  reflection, not a rotation; Betelgeuse renders on Orion's right,
  Atlas/Pleione on the Pleiades' right, dipper handle reversed).
  Raised with her 2026-11-03; she has not yet ruled on the flip
  (stars + NASA photo must flip together to keep alignment).
- She also asked (2026-11-05) for a disclosure of every binary/
  multiple system among the site's 69 stars "so I can use them
  cleverly" — DELIVERED in chat 2026-11-05 (all 70 incl. Polaris
  checked against web sources). Headlines: Polaris triple; Mizar/
  Alcor sextuple (lens + heliotrope sit on it); Dubhe quadruple
  (stem-cell); Regulus quadruple; Rigel quadruple; Mintaka
  quintuple; Sheliak multiple; epsilon Lyrae quintuple (Double
  Double); Atlas + Taygeta triples; Pleione binary; Betelgeuse
  PROBABLE companion "Siwarha" (2025, unconfirmed until ~2027);
  Algenib binary discovered 2025. Optical-only (NOT bound): Schedar,
  Adhafera, Asterope/Sterope, rho Boo, theta Lyr, Enif, Altair's
  companions. Unconfirmed either way: Electra, Maia, Merope,
  Celaeno, Zosma, eta Leo, Megrez, Nekkar, Tarazed.

## Round 19 — 2026-11-05 (illustrated stars; hobby subtitles at landings)

Her screenshot of the round-18 UMA landing: names floating over the
photo with no visible stars and no subtitles — "Stars need to be
illustrated and there should be subtitles for the hobby." Three
stacked causes, all structural:
1. THE SPRITES WERE BURIED. Transparent-object sorting goes by object
   position; the sky spheres sit at the origin (near the camera), so
   the photo sphere sorted AFTER the star sprites and painted over
   them at up to 94% opacity at constellation zooms (farK leaves the
   photo ~0.94 opaque at fov 44-64). Only the brightest cores poked
   through — photo dots. Fix: content sprites + rings renderOrder 3
   (drawn after both sky layers; additive blending does the rest).
2. THE SPRITE ITSELF WAS A WHISPER: spikes at lineWidth 0.008S are
   sub-pixel at phone size. Now 0.02S, fuller spark body (Rv 0.235 ->
   0.30 standard / 0.36 -> 0.40 hero), fuller waist (0.17 -> 0.22),
   halo disc 0.13 -> 0.15S. No glow wash — the r17 ban stands.
3. SUBTITLES COULD NEVER SHOW: minors (repos/paintings/facets) were
   gated to tier 2 (fov < 44) AND tier 2 strips the subtitle (.mini).
   At every zoom, one rule or the other erased them. Tiers re-cut:
   0 = fov >= 64 (far: captions + interest only), 1 = 20-64
   (constellation view: ALL content stars, name + subtitle, minors
   in a compact `mid` size), 2 = fov < 20 (deep cluster: name-only
   mini + spokes, as round 17). The Pleiades fit path (starFit < 20)
   keeps its original tight rect — the new 42px label margin in the
   wide-fit path widened its landing to 4.1 and cost 3 labels before
   the split (verified back at 3.37 / 8 labels).
   Placement rescue at tier 1: a label whose below-anchor fails no
   longer hides — it walks bearings in 15° steps (below first, then
   the away-from-centroid spoke), each candidate judged by the FULL
   fits test (bounds + buttons + collisions). anchorFit alone stops
   at the first in-bounds candidate, which is how Arcturus stayed
   hidden behind a 5px zoom-button overlap.
Verified landings (390x844, placement truth via labelBoxes):
UMA fov 59.5 — caption + ALL 8 stars labeled with repo subtitles
(Alcor included; its label sits mid-figure — its star shares
Mizar's sprite, 3px away at this scale). Boo: Arcturus placed.
Lyr: 8. Ple: 8 at 3.37 (unchanged). Cas/ori/aql remain sparse
(pre-existing density; not regressed). Zero JS errors.
- Deployed 2026-11-05, curl byte-identical (114,122 bytes). Awaiting
  her iPhone verdict.

## Round 20 — 2026-11-05 (icon stars; labels directly under; title on zoom)

Three calls from her, same night:
1. "All the button stars look so weird they should be shaped like
   the app icon, feel glowy/pulse ethereal. Maybe extremely fine
   starlight lightly radiated." The cut-gem body (rounds 15-19) is
   RETIRED. Every star now wears the app icon: the two-layer ice ✦
   from favicon.svg in its own proportions (tips on the axes, waist
   vertices on the diagonals at 0.124 of the tip radius, straight
   edges), the icon's soft glow disc (filled as a circle — the 2023
   "transparent background" patch came from a rect wash, a disc has
   no square edge), hair-fine radiated rays (lineWidth 0.005S, peaks
   0.50/0.36/0.18), and a slow scale pulse in the frame loop (±5%,
   per-star phase, after the size cap so capped stars still
   breathe). Lyra keeps its prism fringe on the outer sparkle.
2. "Labels are not situated directly under their star." The round-19
   bearing-walk rescue is REMOVED — a label hangs directly under its
   star or it hides. Two supports: the anchor gap was a full sprite
   DIAMETER (the _screenR misnomer) — now radius + 10, so labels
   nestle under the sparkle and stop stacking into the next star;
   and fitFovFor's constellation pass now SCORES candidate fovs by
   how many below-labels they carry (bounds + the CSS-derived chrome
   rects + pairwise, greedy in placer priority) and lands on the
   best. Labels anchor to the unpulsed diameter so borderline
   placements don't flicker on the pulse cycle; tier-1 collision
   pads relaxed (12/10 -> 6/4). The deep tier keeps its spokes.
   Honest ceilings on a 390px screen, verified: UMA 5 of 8 under
   their stars (Megrez's 179px label vs Phecda 46px away, Mizar vs
   Alioth, Alcor hides); Orion 2 of 3 (Rigel's below-spot is the
   zoom buttons' corner); Lyra 3 of 9 (the core stars sit closer
   than the labels are wide). Hidden labels appear as she pans —
   placement is live every frame.
3. "On zoom, the constellation's label should appear at the top of
   the screen with the subheading, like a title." When the view is
   inside a figure (fov < 64, centroid within max(14°, 0.4·fov)),
   #figtitle shows the figure's name + sub in the WORDMARK's slot
   (top-left; centered ran into "prachi patel" in QA) and the
   wordmark crossfades out; that figure's in-sky caption stands
   down. Far view unchanged: captions in the sky, wordmark home.
Tap flow re-verified (far Dubhe flies, in-view Alioth opens,
Polaris opens). Zero JS errors.
- Deployed 2026-11-05, curl byte-identical (119,123 bytes). Awaiting
  her iPhone verdict.

## Round 21 — 2026-11-06 (button under title; glowier stars; magnitudes at 1/3)

Her screenshot of the round-20 UMA landing + three calls:
1. "Return to the sky button should be under the title — current
   placement is odd." It floated at top 9.6rem, under the links row.
   Now top 3.7rem mobile / 4.2rem desktop — directly under the
   figure title (verified geometry: title 11-51px, button 59-103px,
   an 8px stack). The fit's backbtn rect and the label topPad
   (152 -> 140 mobile) moved with it; the placer's live-rect guard
   is unchanged.
2. "These stars still aren't pretty enough — add more glow and
   dynamic." Glow disc deepened (peak .38 -> .55 alpha, radius to
   the full sprite), fine rays carry more light (peaks
   .50/.36/.18 -> .78/.55/.30 at the same hair width), sparkle body
   a touch larger (.36/.27 -> .38/.29 of canvas), twinkle deepened
   (.86-.14 -> .78-.22), and the pulse strengthened (±5% -> ±8%)
   with a per-star rate so the sky doesn't breathe in unison.
3. "Somewhat mimic the relative sizes and magnitudes... only a
   little bit. Scale by like .33." magScale's exponent is now the
   Pogson-style 0.22 × 0.33: a 5-magnitude span reads as a ~2.3x
   size range instead of ~12x. Verified base scales: anchors
   (Arcturus, Vega, Dubhe) 20, Merak 18.6, Alcor 14.2, Celaeno 11.1
   — a gentle gradient; faint stars stay visible, per her reason
   ("in real life this can make it hard to see").
Landings unchanged (UMA 5 labels, PLE 8, BOO Arcturus, ORI 2,
LYR 4 — kappa Lyrae gained from the topPad room). Zero JS errors.
- Deployed 2026-11-06, curl byte-identical (119,639 bytes).
  Her verdict on it: "too big now... should still somewhat blend
  into the background" (the 0.33 compression at the old base pushed
  every hero into the on-screen cap — the whole sky rendered at one
  maximum size). Superseded same night by round 23.

## Round 23 — 2026-11-06 (focus dimming; size math at 0.8; glitter layer; bigger title)

Her burst of five asks over the round-21 screenshots:
1. FOCUS: "when one constellation is the focus, the rest should not
   be 'on'. Clashing is happening at the top." When a figure title
   is up, every other figure falls to 22% — stars, glow, gold lines,
   captions, and zoomed-view labels all dim together (verified:
   UMA stars avg opacity .80 vs .18 for the rest at the landing).
   The far map (no focus) is unchanged.
2. SIZE MATH: she asked what math demonstrates relative sizes while
   staying aesthetic, visible, clickable — and dialed "more
   variation, maybe .8". Answer shipped: compressed Pogson —
   d ~ 10^(-0.2 * k * mag), k = 0.8 (the physical sqrt-flux law is
   k = 1 = ~12x across her span; .33 read as one size), with a
   floor (2.2 world) so the faintest stay visible and caps
   (10 world / 76px) so anchors can't eat the sky; the gradient
   lives in the middle magnitudes. Base scales: Vega 8.1, Dubhe
   4.2, Merak 3.4, Alcor at the 2.2 floor. Tap targets keep their
   own 38px floor regardless of drawn size, so small != hard to
   tap. Home now reads as a real starfield: Cassiopeia is a chain
   of small sparkles, nothing overlaps into blobs.
3. "Stars should never overlap this much — realistic space vibe":
   the shrink (round 22's 2.9 re-base + caps 84/60 -> 76/46, kept)
   plus the .8 spread ends the merged-blob look.
4. "Twinkle softly. Where is the glitter/starlight glow?" Body
   twinkle softened (.78-1.0 fast blink -> .88-1.0 slow swell) and
   a NEW live glitter layer: a soft ice glow sprite under every
   star, 2.4x its size, breathing on its own slower phase offset
   from the body's — shimmer instead of pulsing. The baked texture
   glow stepped down (.42 -> .30) since the live layer carries it.
5. "Make the title bigger": figure title 1.3rem -> 1.7rem mobile /
   1.75 -> 2.3rem desktop; the back button re-spaced under it
   (4.1rem mobile, title bottom 58px / button top 66px verified).
Fit predicates now use each star's EXPECTED diameter at the
candidate fov instead of the flat 76px cap (they were spacing
labels for stars that no longer exist). Known wobble: Pleiades
places 6 of 9 mini labels at the exact landing (Pleione/Asterope,
the faintest pair 35px apart, collide out; a small pan reveals
them) — the count has fluctuated 6-8 across rounds 20-23 with the
size changes; flagged to her.
- Deployed 2026-11-06, curl byte-identical (123,116 bytes).
  Her verdict: "Stars look better" — then four more calls, round 24.

## Round 24 — 2026-11-06 (button deleted; six-pointed stars; more pulse and glow)

1. "Get rid of return to sky button." Gone entirely — element, CSS,
   click handler, the show/hide updater (now a no-op), and both
   label-avoidance rects (the placer's and the fit's) that reserved
   its space. Verified absent from the live HTML. Zooming back out
   is pinch/scroll and the menu, as before.
2. "Also bigger stars six pointed." The star body is now a
   SIX-POINTED star (supersedes the round-20 app-icon ✦, which
   itself superseded the gem): tips on three axes, vertical longest,
   diagonals at +/-30 degrees a step shorter, waists pinched at
   0.26 — a snowflake star; the hair-fine rays follow the same
   three axes; Lyra keeps its prism fringe. Bigger: base 2.6 ->
   3.4, hero world cap 10 -> 12, on-screen caps 76/46 -> 88/54px.
   Verified base scales: Vega 10.6, Dubhe 5.5, Merak 4.5, Alcor 2.5.
3. "Make them pulse and glow more." Pulse amplitude +/-8% ->
   +/-14%; the glitter layer's breath deepened (opacity .15-.30 ->
   .24-.48) and widened (2.4x -> 2.8x the star); the baked glow
   disc stepped back up (.30 -> .38 peak).
Focus dimming re-verified after all changes (UMA .81 vs the rest
.18). Honest cost: Pleiades mini labels at the exact landing are
down to 5 of 9 — the bigger stars leave less room in the tightest
cluster in the sky; all 9 stars show, and the missing names
(Merope, Pleione, Asterope, Celaeno) appear on a small pan or a
touch more zoom. Flagged to her with the round.
- Deployed 2026-11-06, curl byte-identical (122,317 bytes).
  Her verdict: "No the four pointed was better."

## Round 25 — 2026-11-06 (four points restored)

The six-pointed body and its three-axis rays are reverted verbatim
to the round-20/23 four-pointed ✦ (icon proportions, four-axis
hair-fine rays). Everything else from round 24 stays: the deleted
button, the bigger sizes, the ±14% pulse, the deeper glitter.
Landings unchanged (UMA 5, PLE 5). Zero JS errors.
- Deployed 2026-11-06, curl byte-identical (122,137 bytes).

## Round 26 — 2026-11-06 (name at title size; menu/log gone; liquid glass; deep-zoom shapes)

Four calls from her home + Pleiades screenshots:
1. "Make my name bigger like the titles." Wordmark is now the
   figure-title size: 2.3rem desktop / 1.7rem mobile (verified
   27.2px computed on mobile).
2. "Remove menu and log buttons." Both pills deleted (elements,
   CSS, listeners). The bottom-sheet menu and the Observer's Log
   still exist in the code, dormant — nothing opens them now. She
   hasn't said whether they get a new door or go entirely.
3. "Make buttons below into liquid glass display." The zoom +/-
   and the hint pill (and its close circle) are liquid glass now:
   bright translucent gradient, backdrop blur 14px + saturate
   170%, white specular top edge, inner glow, soft drop shadow.
4. "Hard to see — make more dynamic shapes" (Pleiades deep zoom:
   the 2.8x glitter halo had turned stars into cotton balls). The
   sparkle body is bolder (Rv .38/.29 -> .44/.35 of the texture,
   waist 0.124 -> 0.16), and the glow's reach now tightens with
   zoom — 1.7x at deep fovs ramping to 2.8x far out — so up close
   the shape carries and the haze hugs it.
Landings unchanged (UMA 5 labels, PLE 5). Zero JS errors.
- Deployed 2026-11-06, curl byte-identical (122,999 bytes).

## Round 27 — 2026-11-06 (spindly stars; more pulse and twinkle; smaller, spread kept)

Her words: "Make stars pulse more and make them more spindly/
deeper webbing sharper more pervasive edges. But do make them
smaller on average and maintain difference relative sizes" +
"Make more twinkly."
- Spindly: the ✦ waist carves to 0.085 (past the icon's 0.124) —
  long thin points, deep webs between them. Rays sharper and more
  pervasive: alphas .62/.44/.24 -> .80/.58/.38 on the four axes.
  Baked glow stepped down (.38 -> .30 peak) so edges read crisp.
- Smaller on average: base 3.4 -> 2.7, hero cap 12 -> 9.5 world,
  on-screen caps 88/54 -> 76/46px. The 0.8 magnitude law is
  untouched, so relative differences hold: Vega 8.4, Dubhe 4.4,
  Merak 3.5, Alcor 2.0.
- Pulse +/-14% -> +/-20%. Twinkle: wider swing (.88-1.0 ->
  .82-1.0) with a per-star rate, layered against the pulse and the
  glitter's own phase.
Landings unchanged (UMA 5 labels, PLE 5). Zero JS errors.
- Deployed 2026-11-06, curl byte-identical (123,077 bytes).

## Round 28 — 2026-11-06 (constellation lines more apparent)

Her call: "make the constellation lines more apparent but not
obnoxious i do like that." Gold line opacity .30 -> .45 (content
figures), .14 -> .20 (background figures), dashed faint lines
.45 -> .55. Focus dimming scales from the new base values, so a
focused figure's lines stand out against dimmed neighbors by the
same ratio as before. (Built with round 27's deploy cycle but
interrupted before QA; verified and shipped with round 29.)

## Round 29 — 2026-11-06 ("why are Leo and Regulus still doing that")

Diagnosis (her earlier question was the same symptom): Leo is so
wide it FITS at fov 78.8 — inside 1.3x of the home fov (88). Two
systems keyed off fov alone, so Leo fell through both:
1. The zoom-then-detail gate (round 18) asked only "is the current
   fov within 1.3x of the fit?" From most wide views the answer
   was already yes, so tapping Regulus opened the geology panel
   directly — no zoom, Leo and Regulus behaving as one thing.
   Pegasus (fit 70.7) had the same defect. FIX: "in the view" now
   requires DIRECTION too — the view must actually be centered on
   the figure (within 0.35 x its fit fov). Verified: home sits
   71.8deg off Leo's centroid vs a 27.6deg threshold; a real tap
   on Regulus from 34deg off-center now flies to Leo first
   (panel stays shut), and a tap once landed opens the panel.
2. The title/focus system required fov < 64, so Leo's landing
   never showed the LEO title and never dimmed the rest. FIX: at
   fov >= 64 the title engages only at a figure's own fitted view
   (fov <= fit x 1.15), truly centered (within 0.18 x fov) —
   home (Polaris, single-star fit 26) can't false-trigger.
   Verified: landed state reports title 'leo' at fov 78.8.
- Deployed 2026-11-06 (with round 28), curl byte-identical
  (124,061 bytes).

## Round 30 — 2026-11-06 (the duplicated word: LEO · geology / Regulus · geology)

Her screenshot (taken just before round 29 landed) showed the
other half of the sameness: at the wide view, Leo's caption read
"LEO · geology" and Regulus's label read "Regulus · geology" —
the same word twice, nothing showing one lives inside the other.
Regulus's panel IS Leo's topic, so his subtitle was a photocopy
of the caption. FIX (in starSubtitle): when a star's subtitle
equals its figure's subtitle, the star's label is name-only — the
word belongs to the constellation alone. Hits exactly the four
anchor stars: Regulus (geology), Cassiopeia's fabric star (fabric
arts), Orion's jewelry star (jewelry), Arcturus (hire me). Repo
and painting subtitles never equal their figures' words, so
Dubhe/Vega et al. are untouched. Verified at the Leo landing:
label "Regulus" bare, title "LEO · geology" above.
- Deployed 2026-11-06, curl byte-identical (124,631 bytes).

## Round 31 — 2026-11-06 (ghostly blue lines; and why they'd been vanishing)

Her call: "make the lines a very thin ghostly glowing blue."
The color change (gold 0xcf7a44 -> ice blue 0x8fc9f2) took ten
seconds; the QA screenshot showed NO lines at all, at any opacity
— which exposed the real bug: the lines have been silently BURIED
for rounds. Transparent sorting ties at the origin, so the photo
sphere (drawn after them, ~94% opacity, no depth write) blended
over every line and left ~nothing. The round-19 fix gave the
STARS renderOrder 3 for exactly this burial; nobody gave it to
the lines. Her round-28 "more apparent" ask was this bug, not a
styling preference. FIX: lines renderOrder 2 (above both spheres,
under glow and stars); ghost blue at .55 content / .22 bg / .50
dashed, normal blending (additive at .34 vanished against the
starfield). Verified in a full-res crop: hair-thin pale threads
run the whole dipper, bowl and handle.
- Deployed 2026-11-06, curl byte-identical (125,332 bytes).

## Round 32 — 2026-11-06 (Leo's name moves onto the Sickle; "isn't Regulus in Canis Minor?")

She confirmed the lines ("Looks nice!") but Leo/Regulus still read
as two things — and she doubted the data itself: Regulus is NOT
in Canis Minor (that's Procyon); Regulus is alpha Leonis, Leo's
heart, and the site's coordinates for it are true J2000. Her doubt
was well-aimed anyway: Leo is two shapes (Sickle + triangle) and
its caption sat at the centroid — the empty gap between them — so
the name floated in the void and the Sickle's base read as its own
little figure. FIX: per-figure caption anchors (CAP_ANCHORS) —
Leo's caption now projects from the midpoint of Algieba and
Regulus, on the Sickle's spine, instead of the centroid. View
centering, fits and titles still use the centroid. Verified in her
framing (Leo low, wide fov): cap:leo places on the figure, no
title, Regulus labeled beneath his star. The one remaining
Leo-looks-wrong contributor is the east-west mirror (diagnosed
2026-11-03/05, still undecided): the Sickle hooks backwards vs
the real sky. Raised with her again alongside this round, as a
choice.
- Deployed 2026-11-06, curl byte-identical (126,160 bytes).

## Round 33 — 2026-11-06 (THE FLIP: sky un-mirrored; and the Pleiades lace)

She approved the flip ("Flip the sky to match the real sky"), and
mid-build added: the Pleiades at constellation distance read as
one giant glowing orb — special-case it: lace, small delicate
distinctive stars close together.

THE FLIP: radecVec's z is negated (the old +z form was a
reflection, not a rotation), and the same sign is carried through
every (ra, dec) consumer so stars, photo and painting stay glued:
both sphere UV builders (atan2(-z, x)), dirToRaDec, HOME_UP,
targetUpFor's polar branch, clampOffPole's pole fallbacks. The
graticule and field clouds ride radecVec and follow on their own.
Verified by projection at Orion's fitted view: Betelgeuse LEFT of
Bellatrix, Rigel RIGHT of Saiph, shoulders above feet — the true
sky (previously exactly reversed). The whole map's handedness is
now correct: Leo's Sickle hooks the way the real one does.

THE LACE (figure 'ple' only): a lace factor L = clamp((fov-25)/30)
in the frame loop. Past fov 25 the sisters progressively shed
size (x(1-.55L)), pulse (amplitude x(1-.7L)) and glitter (opacity
x(1-.78L), reach x(1-.72L)) — the glitter was the main orb-maker:
nine 2.8x additive blooms inside a ~15px span. Fully laced by
fov 55; flying in, the lace blooms back into the full treatment;
at the landing (fov ~3.4) L = 0 and nothing changes (5 labels,
verified). Wide-view crop confirms: a knot of distinct tiny pins
under the caption, no merged orb.
- Deployed 2026-11-06, curl byte-identical (128,063 bytes).

## Round 34 — 2026-11-06 (one vocabulary at a time)

Her screenshot: at a wide view, a lone star label "Schedar" in the
display type floated beside the PEGASUS caption, Cassiopeia's own
caption nowhere — a star impersonating a constellation. Her rule:
"Stars should not be visible when constellations are. It creates
confusion." FIX (one gate in updateLabels): while the caption
layer is up (fov >= 44), star labels hide — UNLESS the star
belongs to the focused figure (title up, one constellation owns
the screen). Below fov 44 the captions have gone home and star
labels carry the view, as before. Verified: home shows captions
only (zero star labels); UMA landing keeps its 5 repo labels; Leo
landing keeps Regulus.
- Deployed 2026-11-06, curl byte-identical (128,700 bytes).

## Round 35 — 2026-11-06 (full constellation audit; two real data bugs; glow touched down)

Her ask: check ALL the constellations — "starting to look
inaccurate" — and touch the glow down. Audit method: every
star's site coordinates cross-checked against catalog J2000
values, then all ten figures flown to and screenshot-checked.

FOUND AND FIXED (real data bugs, both old):
- CASSIOPEIA — Caph's RA was 9.10: the catalog's "00h 09m 10.7s"
  misread as degrees (true value 2.29°). Caph sat 6.8° east of
  true; the W's first segment was squashed to ~1/8 of its width
  for the site's whole life. Now 2.29; the W spans properly.
- PLEIADES — five sisters sat off their Hipparcos positions by
  0.10–0.29° (Alcyone 0.29° west of true — its 56.58 was a
  transposition of 56.87; Maia −0.16°, Pleione +0.16°, Asterope
  −0.11°, Celaeno +0.10° RA; Maia's dec also −0.05°). Inside a
  1.6° cluster those are shape-breaking. All nine now match the
  Hipparcos table (Norris & Norris). Bonus: the landing now
  places SEVEN labels (was 5) — untangled positions freed Merope
  and Asterope.
- The other eight figures (Orion, Leo, Ursa Major, Boötes, Lyra,
  Aquila, Pegasus, Polaris) checked out star-by-star as correct.

GLOW TOUCHED DOWN (her hypothesis, confirmed as a contributor:
fat halos blur where a star actually sits and bend patterns):
baked disc .30/.20/.09 -> .21/.13/.055; glitter opacity
.24–.48 -> .15–.32; glitter reach 1.7–2.8x -> 1.45–2.25x. Stars
now read as crisp sparkles; every pattern legible in the audit
sheets.
- Deployed 2026-11-06, curl byte-identical (129,600 bytes).
- HER VERDICT (2026-11-06, ~03:15): "Okay i like the look now!" —
  the round 28–35 arc (lines, Leo/Regulus, the flip, the lace,
  one-vocabulary labels, the audit fixes, the glow touch-down) is
  approved as a whole. The sky's look is SETTLED unless she reopens
  it. Still open elsewhere: the dormant menu/log door question,
  swung-vs-hidden labels, book review text, pole-smear rebake,
  content gaps (jewelry/photos/fabric), the Rosette M42 copy fix.

## Round 37 — 2026-11-06: centered titles, how-to card, shooting stars, tonight line

Four asks from one 03:16–03:19 burst, one round.

DEAD-CENTER TITLES (her words: "Keep my name here. When you center
the constellation can you place the name dead center. This requires
that centering the constellation has to happen in an orientation
where the title can be placed neatly — orientation and zoom"):
- The wordmark KEEPS the top-left slot permanently — the round-20
  crossfade (body.figzoom hid it) is retired. #figtitle moved to
  screen center (translate(-50%,-50%)), name 2.8rem desktop /
  2.2rem mobile, subtitle under it.
- New landingFit(f): from the centroid figureFit, search 25 view
  offsets (8 compass dirs x reaches .25/.5/.8 of the figure radius,
  in the destination's own screen frame) x zoom-outs (1/1.1/1.22/
  1.36); each candidate must keep every star inside the frame rect,
  then scores: star clearance from the centered title rect (star
  center distance minus drawn radius, capped at 40) - zoom tax -
  offset tax - bbox-off-center tax (0.14/px; added after QA showed
  clearance-only scoring exiling the dipper to the top edge) -
  label tax (12 per label the title would eat; labels hang below
  stars, estimated generously — the bowl framing ate Dubhe/Merak's
  labels in QA before this term existed). Winner cached per
  figure+viewport; stored as f._land.
- All flights route through landingFit now (flyTarget, caption
  taps, star-gate flights); the tap gate compares against the
  landing, and activeFig ALSO engages at the landing framing
  (angle <= 0.06 rad, fov within 22%) since the landing sits off
  the centroid. The label placer routes around the centered title
  rect (hitsBtn) and around the how-to card while it's open.
- Verified landings (sandbox): LEO wraps its waist around the
  title (offset 13.9 deg); CASSIOPEIA's W drapes under it at the
  plain centroid fit; PEGASUS needs no offset (the Great Square's
  middle is already empty); URSA MAJOR settles just off-centroid
  with the dipper arcing under its name; LYRA floats above the
  lyre. KNOWN COST, disclosed to her: at the exact landing the
  title zone prices out some labels on the densest figures — UMA
  shows Alioth + Phecda of 8 at rest (was 5 in the top-left-title
  world), Lyra 2 of 9, Pleiades 4 of 9; the rest surface on any
  small pan/zoom and every star keeps its 38px tap floor. Hers to
  judge; dials are title size or label priority.

HOW-TO CARD (her words: "when you open the page you should get a
cute thematically appropriate 'how to' and then x out so it's not
always there. Also, there can be a help icon they can click to get
it back. If someone swipes in ways that suggest struggle, make it
glow"):
- The old hint pill is GONE (markup, CSS, listener). #howto: a
  liquid-glass card, "how this sky works ✦", four ✦-bulleted rows
  (drag / pinch or scroll / tap a name / tap a star), ✕ top-right,
  tonight line as its footer. Shows ~0.9s after every load; no
  storage (nothing to lose, nothing to go stale). While it's up,
  the bottom tonight line hides (one home per fact) and labels
  route around it. Any flight auto-closes it (flyToDir).
- "?" joins the zoom stack as a third glass button; reopens the
  card, clears the glow. Struggle detector: >=7 drag direction
  reversals in 6s, or >=6 drag-starts in 25s, with no success yet
  (success = a flight starts or a panel opens, via noteSuccess in
  flyToDir/tapStar) and the card closed -> #helpbtn.glow pulses an
  ice halo (static glow under prefers-reduced-motion). Verified
  with synthetic PointerEvents (Playwright's mouse plumbing on the
  mobile-emulated page never reached the detector; real touch
  produces the genuine events).

SHOOTING STARS (her ask; an old soft-dot system existed that she
never noticed): rebuilt as a real tapered streak — canvas texture
(transparent tail feathering to a bright ice head), sprite scaled
to its arc's world length, head riding the arc while the center
trails half a length behind, rotation recomputed PER FRAME from
the projected path (the old code aimed once, in world xy). 0.85s
crossings, peak opacity .92, cadence ~15-30s (first at 5-11s).
Sandbox renders ~1fps so the streak can't be frame-verified
there; state hooks confirm it spawns/scales/aims without errors.

TONIGHT LINE (her ask: "pull in current space events and display
them nicely on the screen very concisely"): computed on-device
from the date — no fetch, never stale. New #tonight microline
above the positions line, and the same line as the card footer.
Moon from REAL sun/moon positions (compact suncalc model): a
mean-cycle count off a 2000 epoch read 14% lit against the
catalogs' 8% on 2026-11-06; the positional model reads 8.2% and
nails all four Nov 2026 principal phases (new Nov 9 07:02 UTC
0.0%, first quarter Nov 17 51%, full Nov 24 100%). Meteor showers
from the fixed annual calendar (9 showers, year-wrap windows
handled): tonight's line reads "TONIGHT · WANING CRESCENT · 8%
LIT · LEONIDS · PEAKS NOV 17".

- Deployed 2026-11-06, curl byte-identical (147,615 bytes).
- Awaiting her iPhone verdict.

## Round 38 — 2026-11-06 (centered figures, title discipline, the open-night glow)

Her two messages after round 37: "Hey it should be centered" and a
screenshot from her phone showing the violation that proved it: the
PLEIADES title dead center in empty sky while the cluster sat small at
the bottom and an Alcyone star label showed beside it. Root causes:
round 37's landingFit deliberately framed figures OFF their centroids
so the title sat in clear sky — the constellation itself was not
centered; and the title-engagement rule still carried the old fov<64
nearest-figure slack (up to ~24 degrees), so a title could claim a
figure the view was merely passing. Fixes:
- landingFit DELETED (5.2 KB with its cache). Every flight is the
  centroid figureFit again: the constellation centers, the name sits
  dead center over its heart.
- Title engagement rewritten: activeFig requires centeredness within
  the figure's own span (max(fit*0.18 rad, figureRadius*1.15)) AND
  zoom at the fitted fov*1.35 or deeper (fov < 64 counts as deeper
  only while still centered) — no title for a figure off-center at a
  wide fov. Her exact screenshot state was recreated in QA (zoomed
  out, cluster dragged low): no title, captions only, zero star
  labels — the round-34 constellation-and-star rule holds.
- The glow: the sleep tracker's open night breathes cardPulse (4s
  ease-in-out, rgba(169,196,244) shadow swelling 16px -> 36px).
  Ported as a periwinkle text-shadow halo ON the title's name,
  swelling 18px/.42 -> 30px/.72 over the same 4s. A first attempt as
  a radial-gradient disc behind the text rendered as a DARK edged
  plate over the sky (caught in QA screenshots; an emanating glow
  can have no edge — the glow lives on the glyphs now).
- QA caught a self-inflicted bug mid-round: the title text was set
  via figTitleEl.children[0]/[1]; adding a glow div as a child
  shifted the indexes and put the topic in the name slot. Population
  is by class query now (.ft-nm / .ft-th).
- Verified landings: UMA (title over the bowl, dipper centered),
  Pleiades (6 labels at rest, cluster centered under its name),
  Leo (title at its fov-78.8 landing). Deployed together with
  round 39: 144,571 bytes, md5 3173e1b3817f2644870c29153d6fa88b,
  curl byte-identical.

## Round 39 — 2026-11-06 (Polaris holds the menu; the pole's neighbours are her priorities)

Her words: "If Polaris is where it starts, Polaris should have the
menu of constellations," with her intro draft, and "the constellations
near Polaris need to be closer to what i care about — so tech
projects, hire me, whichever art i have the best of."
- The Polaris panel (tap the pole star, or the POLARIS topbar link)
  now leads with her intro, near-verbatim: "Hey! This is how I
  envision my mind palace would look — with all my interests sorted
  as stars into constellations. Click on a constellation to get
  started! Thanks :-)" (only tidy: "get start" -> "get started").
  Facts and contact links stay below.
- Below the intro, the menu of constellations: one row per figure
  (name + topic), sorted by angular distance from Polaris, nearest
  first. Tapping a row closes the panel and flies there (delegated
  data-fly handler on the panel body).
- The remap that makes the pole's neighbourhood match her
  priorities: HIRE ME moved from Boötes to CASSIOPEIA (29 degrees
  from the pole, the nearest figure) — panel anchor Schedar; FABRIC
  ARTS moved from Cassiopeia to BOÖTES — anchor Arcturus. Tech
  projects (Ursa Major, 34 degrees) and digital art (Lyra, the next
  nearest) were already in place. Menu order now opens: Cassiopeia
  (hire me), Ursa Major (tech projects), Lyra (digital art),
  Boötes (fabric arts), Pleiades, Pegasus, Leo, Aquila, Orion.
  Figure subs, both anchor stars' interest keys, the dormant menu
  rows, and the map comment all swapped consistently; the subtitle
  dedupe follows automatically (Schedar and Arcturus show name-only
  labels again).
- Verified end to end: panel opens with the copy and menu; menu tap
  flies to Cassiopeia and closes; Schedar opens the hire-me panel;
  Arcturus opens fabric arts; Boötes' title reads fabric arts.

## Round 40 — 2026-11-06 (the card centered + glowing; title halo; star sizes follow the zoom)

Her burst, reading the deployed 38+39 on her phone: (1) the how-to
card — "Center this vertically and you never added the starlight
glow from sleep tracker." She was right on both: the card sat
bottom-anchored, and the sleep-tracker glow was the one owed to the
CARD (the round-38 reading put a halo on the constellation title —
it stays, it's gentle — but the card is what she meant). (2) A
Cassiopeia screenshot: the centered title lay "smack dab on the
constellation," its stars ~11px and faint beside the 2.2rem name —
"add a glow behind it when zoomed to star, so we know it's the
constellation name and the stars look different"; "make the stars
bigger in this view"; "star sizes dynamically need to change with
zoom — appropriate at every level."
- HOW-TO CARD: now dead-center on the screen (top 50%, verified
  rect center = viewport center exactly) and wearing the open
  night's cardPulse VERBATIM — border rgba(169,196,244,.65), outer
  shadow swelling 0 0 16px -2px rgba(169,196,244,.5) ->
  0 0 36px 2px rgba(169,196,244,.8), 4s ease-in-out, the card's own
  resting shadows carried inside the keyframes; static halo under
  reduced-motion.
- TITLE GLOW: a backing cloud was tried first (box-shadow on an
  empty ellipse) and rendered — like the round-38 gradient disc —
  as an edged oval plate. LAW, twice-proven in this engine: any
  element-shaped glow behind the title plates; the only edge-free
  glow is glyph-shaped. So the halo is the name's own text-shadow,
  strengthened (22px/.55 -> 34px/.85 plus a 92px outer bloom at
  peak) breathing on the same 4s rhythm, with a matching gentler
  pulse on the topic line. The name now reads as a lit nameplate
  floating over the constellation — a different layer from the
  stars, which was the point of the ask.
- STAR SIZES FOLLOW THE ZOOM: the draw loop's zoom compensation
  (zk) squared the tangent ratio (exponent 2.0), which starved the
  constellation landings — at Cassiopeia's fov 33 the factor fell
  to 0.40. Exponent now 1.2: home still clamps, deep zoom still
  hands off to the px caps, and the mid-zooms hold their presence
  (Schedar ~11px -> ~38px measured). The FOCUSED constellation
  additionally gets a 1.25x size lift, +16px on its px caps, and a
  ~19px presence floor for every one of its stars (the mag law's
  clamped standard stars — Caph was ~12px beside 38px heroes; the
  figure now reads evenly). The Pleiades lace still multiplies
  after the floor, so at distance the sisters stay lace.
- Verified: Cassiopeia landing (W even and present, halo on the
  name, no plate), UMA landing (Dubhe ~52px), card centered with
  the pulse running. Deployed 147,662 bytes, md5
  d10a0b716d2b0a78076a4d75cf6555fb, curl byte-identical.

## Round 41 — 2026-11-06 (the escaping stars)

Her follow-up to round 40: "It's glowing now but where's the stars
escaping like in sleep tracker?" Correct again — the open night's
effect is TWO parts and I had only ported the halo. The other half,
from the sleep tracker source (.glimmer, beside the in-bed card):
14 ✦ spans now ring the how-to card's rim (the tracker uses 16,
including 2 interior; the perimeter set only here, the card is
text-dense), each with its own outward drift vector, peak opacity
(.45–1), size (5–11 px) and staggered delay (0–3.3 s), all on the
verbatim glimmerDrift keyframes — flare to 1.15 scale at 20% while
moving out, a twinkle dip at 55%, a second flare at 80%, gone at
the full vector — 3.8 s ease-out, infinite. Same colour #d7e5fc,
same text-shadow (0 0 8px rgba(169,196,244,.95), 0 0 2px white).
They animate only while the card is shown; still under
reduced-motion. QA sampled computed opacities over time: 13 of 14
lit at staggered phases (the first single-instant sample caught
them all at spawn during the card's fade-in — sampled properly
before concluding anything). Deploy note: attempts at
04:29–04:34 EST returned HTTP 503 "no healthy upstream" (the live
worker kept serving round 40; a transient upstream outage, NOT a
deploy limit — no 429 anywhere); her "try again" at 04:42 EST
went through. Deployed: 150,864 bytes, md5
3429ff567fdbd5e4404d6233819a1e2a, curl byte-identical. The
scheduled retry was stood down once this landed.

## Round 42 — 2026-11-06 (the eclipse boot)

Her ask, in three messages: the background must fully load before
the sky is used, with a cute loading screen like the sleep
tracker's; make it a solar eclipse; "It goes from totality to not
totality until loaded, stars around the eclipse as sky darkens";
plus Baily's beads, a loading subtitle, and "rainbow flare with
totality?" — yes, dialed low.

THE LOADER (#boot, a classic script before the module so it owns
the theatre even if the module crawls): full-screen deep-teal sky,
her name in Bigskate, the eclipse center-stage, and a subtitle
that names the phase as it changes — TOTALITY → THE MOON DRIFTS
ON → BAILY'S BEADS → THE DIAMOND RING → FIRST LIGHT — with the
percent in IBM Plex Mono beside it.

- Totality: black moon on the sun, ice corona (limb-hugging radial
  ring + two counter-rotating irregular streamer layers — the
  first cut's regular repeating-conic read as sun-icon spokes;
  irregular stops + blur fixed it), stars standing around the
  eclipse in the darkened sky (twinkling dots + three ✦), and the
  rainbow flare as a thin prismatic halo ring standing OFF the
  corona like a 22° halo (first cut was a saturated donut; thinner
  mask band, blur 9, opacity .42 — it fades by mid-load like
  everything totality-only).
- Egress pacing is deliberate geometry: mx = pow(easeIO(dp), 1.5)
  × 112 px, so the moon rides the sun until ~85% and ends just
  clear (the first cut's linear 158 px had it fully separated by
  55% and off-stage by 97%, beads stranded in empty sky).
- Baily's beads: five warm beads strung along the moon's western
  limb (128°–238°), staggered in from 24% as the limb crosses the
  sun, twinkling, fading as the discs separate (0.86–0.97) while
  the diamond — a ✦ at the last-contact point (228°) — blazes up
  (smooth 0.88–1.0). At 100%: a first-light flash, then the
  loader lifts (1 s fade) and only THEN does the how-to's 900 ms
  timer start (BOOT.then gates the old setTimeout).
- PROGRESS IS REAL: the 3.6 MB background now STREAMS via fetch +
  ReadableStream with byte progress (was a bare TextureLoader —
  binary progress only), weighted tex .78 / fonts .10 / first
  frame .12. Fail-overs everywhere: fetch hiccup → plain load;
  texture error still counts as done; a 15 s failsafe forces the
  reveal — her standing rule (assets resolve or fail over, never
  hostage). Displayed progress eases toward real (0.45/s crawl,
  1.6/s finish sweep, 1.1 s minimum show). Reduced motion: no
  spin/twinkle, faster reveal.
- QA: window.__qa.bootState()/bootPin(f, snap) added. Sandbox
  rAF crawls (~2 fps with dt clamped), so states were snap-pinned
  and verified by screenshot: totality (corona + halo + stars),
  55% (crescent + beads ON the limb — the money shot), 95%
  (diamond at last contact); release → boot removed, how-to
  shows, zero page errors. Playwright's own screenshot stalled
  on font-wait in this sandbox; CDP captureScreenshot worked.
Deployed: 164,301 bytes, md5 69c2f0969656728ba736bc6a88b1fe0c,
curl byte-identical.

## Round 43 — 2026-11-06 (loader restyle: stylized, minimal)

Her verdict on round 42: "That looks bad it needs to be way more
stylized" + three specs: "The flare is linear not radial and it's
brighter" / "Don't put my name here just 'loading'" / "It needs to
be cute and minimalist."

- SCALE: the whole eclipse shrinks to a jewel — stage 300→170 px,
  sun 92→54, moon 100→58, corona 330→190 with its falloff
  re-stopped for the smaller box; one streamer layer (the second
  deleted). Air everywhere; the composition is mostly empty sky.
- FLARE: the radial rainbow halo ring is OUT. In its place a
  LINEAR anamorphic flare through the eclipse: a bright hairline
  streak (plus a soft blurred under-streak) on the horizontal
  axis, with five ghost discs strung along it — two prismatic-
  rimmed (violet/cyan/gold spectral rims), two ice, one warm —
  exactly the sleep tracker's lens-ghost vocabulary at jewel
  scale. It sits above the sun, below the moon (the moon occludes
  it as it passes — correct optics), brightest at totality (.85),
  dipping mid-egress, flaring again at the diamond ring. Our
  radius-49 bead math became 28.5; egress travel 112→68 px on the
  same pow(ease, 1.5) pacing, so the moon still rides the sun
  until ~85%.
- TEXT: her name is GONE from the loader. The subtitle is just
  "loading" (lowercase now, no uppercase transform) + the percent
  in mono. The phase narration no longer displays (phaseFor still
  feeds BOOT.state() for QA only).
- Stars thinned: 19→12 dots + 2 tiny ✦ glyphs.
Everything else from round 42 stands: real streamed progress,
weights, fail-overs, 15 s failsafe, how-to gated on the reveal.
QA: snap-pinned states screenshot-verified (totality — jewel
eclipse, ghost rings on the streak; 55% — beads on the contact
limb, streak behind the pair; 95% — diamond at last contact),
zero page errors. Deployed: see below.

## Round 44 — 2026-11-06 (label boundaries, strict)

Her report, with phone screenshots: "the label boundaries need
stricter enforcement while zooming around — i saw the same
constellation name bigger and small and star named [together]."
Diagnosis from her three shots + the code: three thresholds
(captions from fov 44, tiers at 64, the star gate at 44) plus
180 ms flip hysteresis and a .28 s fade smeared every crossing —
mid-zoom she got the small caption (22 px) and the big title
(2.2 rem) for the same name in adjacent moments, a star label
(Scheat) floating in caption territory, and Leo's caption still
up at a zoom where its stars were big and nameless (the 44–64
dead band: captions on, star labels gated off, Leo's strict
centered-test just missed).

- ONE line now: LOD = 56. Tier 0 (captions) is fov >= 56; the
  caption band and the round-34 star gate both sit on it. Below
  it captions are gone and star labels own the sky. (The archive
  figures' fov<64 caption clause is untouched — a content rule,
  not a boundary.)
- HARD CUTS: when the band changes (tier crossed, focus
  gained/lost/moved), pending flips apply instantly, show/hide
  skip the fade, and every label snaps to its settled state —
  no frame after a crossing shows a half-faded wrong layer.
  Verified: a 70->50 jump had zero captions visible 260 ms on.
- The focused figure's star-label exception tightens to its true
  landing (fov <= fit x 1.1, was any centered pass at fit x 1.35).
- Landing band metrics: a figure landing above the line (Ursa
  Major fits at 63.1) labels its stars with tier-1 metrics (mid
  size, tight pads) while its title is up — tier-0 metrics had
  emptied its landing. A related exemption lets the focused
  figure's own minor (repo/painting) stars label at tier 0.
- Placement stickiness: a placed label tests with a shrunken
  rect (pulse/drift can't flick it out); an entering label needs
  4 px extra clearance. Boundaries strict AND still.
Verified in the sandbox: home = captions only; Leo at fov 52 =
labels, no caption; at 60 = caption, no labels; Leo/Pegasus
landings keep title + their stars, captions off; zero errors.
Standing cost, unchanged from round 37 and already flagged to
her: the centered title's avoidance box eats the dipper's middle
labels (Mizar, Alioth) at Ursa Major's landing — the offset-title
offer from round 40 remains the fix if she wants it.
Deployed with round 43's loader: 168,027 bytes,
md5 5ac114f3705e2e9818b43d3af89b7a10, curl byte-identical.
(Round 43 deployed alone first: 164,489 bytes,
md5 5d3d2efb9fe9b119e0b8270d6c07d98f.)

## Round 45 — 2026-11-06 (eclipse scrapped; the little cluster)

Her word: "Scrap it. Just do something cute and space themed."
The eclipse (rounds 42 AND 43) is gone entirely — sun, moon,
corona, flare, beads, diamond, flash, all deleted (zero remnants
in the file). In their place: a little cluster of nine ✦
sparkles in a Pleiades-ish knot-and-chain (her cursor cluster,
shrunk to a charm) over a soft periwinkle glow. Each star pops
in at its load threshold with a small overshoot, then twinkles
gently; the glow deepens as the cluster completes. Text is just
"loading" + the percent. Everything underneath is the round-42
machine, untouched: streamed texture progress, fonts, first
frame, weights, 15 s failsafe, lift-and-reveal, how-to gated on
the lift. Verified: pinned states render correctly, a fresh
load completes the full cycle (boot lifts and removes itself,
how-to appears), zero page errors. (Sandbox note: the frame
loop crawls at ~1 fps under SwiftShader, so DOM readbacks lag
one pin behind; the rendered frames are correct.)
Deployed: 163,657 bytes, md5 below, curl byte-identical.
94ffc57361e63591a31370f990377f66  site/index.html

## Round 46 — 2026-11-06 (steal Set & Rise; load honesty)

Her three counts against round 45: (1) "loading is still not
cute. Can you just steal from sleep tracker?" (2) "when it
loaded the correct sky was not fully loaded" (3) "why did it
get stuck for so long"

THEATRE: Nightshade's Set & Rise boot, stolen wholesale — the
160 px stage, wavy lake horizon (its wave SVGs), warm sun glint
and cool moon glint on the water, the rayed sun SVG that sets,
the moon that rises, its four twinkles. Hers runs one 3.2 s
pass; here every animation loops while the load runs. Two
adaptations: it sits on our teal ground, and the moon's face is
a CSS shade in the tracker's tones — its real maria are a
176 KB vector asset, which would more than double this page for
a 44 px disc. Our sprinkle-star field stays around it (renamed
.bgstar — the scene owns .boot-star now). Reduced motion gets a
static night state (moon up, no sun). QA catch: the stolen CSS
extraction clipped @keyframes bootTwinkle's closing brace,
which silently ate the moon rule in parsing — caught by a
computed-style probe (background: none), not by eye.

HONESTY (counts 2 and 3 — one family): the loader was declaring
victory early AND could hang. (a) The streamed path called
finish() on a TextureLoader texture the moment its BYTES
arrived — before the JPEG decoded — so "tex" (78% of progress)
completed early and the loader could lift onto the painted
stand-in sky. Now tex completes only in the loader's onLoad,
and the module sets __texApplied. (b) The frame credit fired
after ANY first frame; it now requires a frame rendered with
the photo applied (or the fail-over flag set) — the reveal is
structurally incapable of preceding the real sky. (c) A stalled
stream hung reader.read() forever, leaving only the flat 15 s
failsafe: each read now races a 6 s timer and aborts to the
plain load, and the boot script force-completes any part that
has not moved in 6 s (worst case the painted sky shows and the
photo swaps in when it lands — graceful, never hostage).
Verified: texApplied/framed transitions precede the lift;
full cycle completes; zero errors.
Deployed: see md5 below, curl byte-identical.
cbb710a11c372b26dc606d0b5a891b1e  site/index.html

## Round 47 — 2026-11-06 (stars lean; subtitles stand up)

Her screenshot (Pegasus landing: PEGASUS, a washed-out "writing",
and Markab in the same upright cream as the constellation):
"Stars and constellations need some difference and the subtitles
under need to stand out more" + "Maybe italics but still cream."

- Star names (.lbl .nm) are now ITALIC — the browser's oblique
  of Bigskate; same cream, different posture. Constellation
  names (captions and the centered title) stay upright. In the
  QA shot the difference reads at a glance: PEGASUS stands,
  Markab leans under its star.
- Subtitles everywhere they sit under a name got bigger, bolder,
  brighter: title topic .ft-th 10px -> 13px weight 600 full-
  bright ice; caption sub .cap .cs 12px -> 14px (inline 13/14 ->
  15/16) weight 600; star subs .lbl .th 10px -> 11px weight 600
  brighter ice. (Archive figures' dim captions keep their dim
  colors — they are meant to recede.)
Verified at the Pegasus landing and at home (POLARIS "start
here", CASSIOPEIA "hire me" both clearly legible now); zero
errors. Note Markab shows no subtitle — correct: its word IS
the figure's ("writing"), deduped since round 30.
Deployed: see md5 below, curl byte-identical.
b1ce8bf5f4ee122ab260659c6e0f493b  site/index.html

## Round 48 — 2026-11-06 (name in the upper third, constellation under it)

Her words: "Can you have constellation name on upper vertical
third, and the constellation under it." This supersedes round
37's dead-center title — and settles the standing round-40/44
question (title physically off the stars) HER way: the name
moves up, the framing moves down.

- #figtitle: top 50% -> 27% (its block measures y 197-259 on
  390x844 — inside the upper third, clear of the header links).
  titleRect follows (center H*0.27, h +6 for the bigger sub).
- figureFit now returns a cached LANDING {dir, fov} per figure
  per viewport: the fov is solved for the band UNDER the title
  (fitFovFor takes cyT; its top bound is the title's bottom + 14,
  and scoreFit refuses labels under the title rect), then
  landingDirFor tilts the view (3-pass projection iteration)
  so the centroid projects at LAND_TY = 60% of the height.
  Two fit/tilt rounds. Polaris (single star) stays centered.
  The dipper shortcut gets the same composition.
- Everything that keyed off the centroid now keys off the
  landing dir: the activeFig nearest/centered test (frame loop),
  and transitively the tap gate (it already used flyTarget's
  dir). fitFovFor's other y-gates (belowRects, anchorFit's
  labelFits) use the same inBand test.
Measured: Pegasus — title cy 228, centroid y 495, highest star
y 415 (156px of clear sky under the name); Leo — fov 80.1 fits
the tighter band under the 88 cap, centroid 519, top star 487.
Zero errors. The title now eats NO labels by position; the
dipper's sparse landing should recover its title-blocked stars
(Mizar/Alioth/Megrez) the same way.
Deployed: see md5 below, curl byte-identical.
99740943cd2cdc60fb64ae2ca22d9ef6  site/index.html

## Round 48 — REJECTED and REVERTED, 2026-11-06

The upper-third composition (name at 27%, figure framed under
it at 60% height, landing-dir fits) shipped, measured clean in
QA — and she rejected it on sight: "No that looks bad. Revert."
Reverted byte-exact to the round-47 build (md5
b1ce8bf5f4ee122ab260659c6e0f493b, restored from the verified
live copy) and redeployed; live verified byte-identical to
round 47. The dead-center title stands. Do not re-propose
moving the title up or reframing landings downward — tried,
hers to reopen if she ever wants it.
