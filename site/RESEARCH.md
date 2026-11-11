# How astronomy apps do it — research notes (2026-10-05)

Researched: SkyView (Terminal Eleven), Star Walk 2 (Vito Technology),
Stellarium Mobile (Noctua), Stellarium desktop source (github.com/stellarium/stellarium,
src/core — source-verified: StelSkyDrawer.cpp, StelMovementMgr.cpp,
StarMgr / LabelMgr / MilkyWay / Constellation modules).

## 1. ART — how they render the sky

- **Stars are drawn sprites, never photos** (all three). That's why they stay
  sharp on zoom. Stellarium: every star = a screen-space quad with a small
  radial-gradient halo texture, additive blending (`GL_ONE, GL_ONE`), batched
  1000/draw-call via streaming VBO. Size/brightness from magnitude through an
  eye tone-reproduction model with luminance adaptation — **as you zoom in,
  fainter stars fade in and bright stars grow** (`powFactor = pow(60/fov, 0.8)`).
  Radius clamped: min 1.2 px (kills sub-pixel shimmer), soft sqrt compression
  above ~8 px. Color from a 128-entry B-V → RGB table (hot `#9AB6FF`, cool
  `#FFC69B`). Twinkle: per-frame random multiplier, subtle (0.3), stronger
  near the horizon. Bright stars get a second 150 px soft halo (bloom);
  optional diffraction-spike sprite variant.
- **Backgrounds are painted/analytic, not photos.** Stellarium night sky =
  analytic sky-brightness model + faint horizon glow + zodiacal light band.
  Star Walk 2 = painted deep-space gradient with subtle nebula noise.
  SkyView = navy gradient + glowing sprites.
- **The one exception: Stellarium's Milky Way IS a photo** (equirectangular
  panorama) — handled with the trick that matters: the fragment shader
  unprojects screen → sky direction → UV, and **the whole band fades out
  between FOV 2.5° and 0.25°**, so zooming never reveals blurry pixels.
- **What we adopted:** drawn star sprites (already ours, now bigger);
  painted procedural background crossfading in past fov 40 → 18, exactly the
  photo-fade-out pattern; analytic teal gradient + true-band wisps instead of
  a second photo.

## 2. MOVEMENT — how it feels

- **Stellarium (source): pan = direct 1:1 drag tracking, NO inertia on
  release.** 4 px threshold separates tap from drag. Wheel/pinch changes FOV
  directly. FOV range effectively unlimited (0.001°–360°).
- **Fly-to feel (the cinematic secret):** programmatic moves default 1.5 s
  through a smoother: **duration ≥ 1 s → easeInOutQuart; < 1 s → easeOutQuad**,
  tweening view direction (slerp) and FOV together. We copied this rule.
- **The shared trait across all three:** 1:1 directness (gyro-follow in AR
  modes is the same idea). None document strong inertia; SkyView/Star Walk
  add only light momentum.
- **What we adopted:** true 1:1 tracking (radians-per-pixel derived from live
  FOV and viewport each frame — a fixed constant was ~2× too fast),
  gentle strongly-damped momentum on release (exp decay, always settles),
  fly-tos keep cubic in-out (matches InOutQuart feel).

## 3. LABELING

- **Stellarium (source):** constellation names at member-star centroid,
  centered, pale blue, through a `LinearFader` — **labels fade, never pop**.
  Known weakness: NO overlap decluttering (crowded labels do collide).
  Star names: only named stars, gated by a **zoom-dependent label budget**
  (`maxMag = (limitMag − 6.5) × 0.7 + density × 1.2 − 2`) — the budget
  automatically expands as you zoom. Brightness-first priority. Placement NE
  of star with leader-line style option. Re-projected every frame (glued to
  the sky; stability from data-driven positions, never cached screen coords).
- **SkyView:** constellation names fade in/out with proximity; caps labels;
  magnitude slider = label-density control.
- **Star Walk 2:** minimal labels; tap-to-identify for the rest.
- **What we adopted (and where we beat Stellarium):** HTML overlay labels
  re-projected per frame (crisp text, CSS fades); zoom-gated budget
  (LOD tiers); brightness-first priority; **greedy screen-space overlap
  reject — hide what doesn't fit, never stack** (fixes Stellarium's known
  weakness); fade in/out + 3-frame hysteresis so nothing flickers;
  placement re-runs only on significant view change with CSS transform
  transitions for smooth tracking.
