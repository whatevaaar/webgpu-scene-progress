Build a real-time gothic haunted-mansion scene (Edgar Allan Poe decadence with a creeping
Lovecraftian/Bloodborne dread at the margins) that runs in the browser. It only needs to look
beautiful and let me fly a free camera through it.

PRIORITIES (in this order when they conflict)
1. Visual quality
2. Stable frame pacing at the target spec
3. Small bundle size

FIDELITY TARGET: painterly-stylized direction (baroque chiaroscuro), fully committed. The
rendering language is oil-painting tonal, Rembrandt/Caravaggio: a single dominant light source
carving form out of near-total darkness, soft painterly edges, warm/cool tonal separation, rich
shadow gradients — NOT photoreal literalism, but committed as a coherent graphic language. Both
stylized and realistic are valid end states; this scene picks painterly-stylized. Two rules at
ANY fidelity: (1) commit every effect completely — no half-done realism (albedo noise faking
grime, half-SSS, milky diffuse god-rays, flat lambert with plastic specular) = the uncanny
failure; execute each effect convincingly or cut it. (2) Model hero elements and creatures TO THE
SUBJECT, never a stand-in primitive — the chandelier has arms + crystal drops + a cracked frame,
the grandfather clock has a case + face + pendulum + visible gears, bats have wings + bodies, the
staircase has balustrades + steps + a landing — painterly but unmistakable, never "box = clock"
or "triangle = bat". CYCLE CEILING: HIGH — push ambition and subject-specific craft up as review
cycles allow; a score plateau means "pursue more specific geometry/technique", never "lower the
bar". A render taking many cycles to reach high fidelity is expected and fine. Do NOT cap ambition
to avoid uncanny — avoid uncanny by committing fully to the painterly language, not by going
simpler. The critic judges commitment + subject-specificity, not proximity to realism.

The two real failure modes to design against (both independent of realism-vs-stylized):
1. HALF-COMMITMENT → uncanny valley. Uncanny comes from realism done partway, NOT from realism
   itself. Every effect is either executed convincingly or cut — never half.
2. GENERIC FIXED TOOLKIT → homogenization (every theme collapses to box=building, cone=tree,
   sphere/oval=any-creature, triangle=bird). Model hero elements and creatures TO THE SUBJECT.

VISUAL SIGNATURE:
1. Volumetric dust-laden moonlight shafts cast through broken gothic tracery — crisp mullion/
   rosette dappling patterns projected across the floor and furniture, with suspended golden dust
   motes swirling inside each beam (the defining atmospheric effect of this scene).
2. Painterly chiaroscuro tonal grading (baroque oil-paint falloff) + a colossal cracked crystal
   chandelier that refracts the moonlight into drifting caustic glints and faintly tinkles.

ART REFERENCE: Bloodborne (Yharnam interiors) — oppressive Victorian gothic, tarnished gold, damp
stone and rotting wood, sick moonlight. Secondary note: Crimson Peak / baroque chiaroscuro
painting for the tonal language.

HERO ELEMENTS (max effort spent here; everything else is atmospheric filler):
1. The grand double staircase under a colossal, half-fallen crystal chandelier at the heart of the
   atrium — where the moonlight falls. Maximum geometry + crystal refraction/caustic effort.
2. The haunted ancestor portrait gallery — a wall of warped portraits whose eyes subtly track the
   camera, with one oversized central canvas half-shrouded. Psychological unease is the payoff.
(Supporting high-quality landmarks, not hero: the broken rose-window with the sick oversized moon
behind it; the colossal stopped grandfather clock.)

CONSTRAINTS
- No Three.js/Babylon.js or other engines.
- WebGPU rendered.
- Everything procedural: no texture/model files. Deliverable is a single self-contained
  index.html. Report minified size.
- Zero per-frame JS allocations (no GC stutter). Preallocate all buffers.

TARGET
- Windows 11 25H2, Chrome 157, RTX 5070 Ti, Ryzen 7800X3D, 180 Hz monitor
- 2560×1440 at full resolution. GPU frame time ≤ 11 ms average, no frame > 16.7 ms during a
  scripted 60 s fly-through.

SCENE
- Labyrinthine mansion interior: a colossal multi-story atrium anchored by a grand double
  staircase; branching galleries of pointed gothic arches, columns and long corridors the camera
  threads under and between; traversable archways and a broken doorway opening onto fog.
- Strong depth fog/absorption: warm candle-amber and suspended golden dust near the camera →
  putrid green-black that swallows the far corridors. Medium dust-laden haze.
- Key light: raking moonlight entering through tall broken gothic windows and a shattered rose
  window, throwing volumetric dust shafts with crisp mullion/tracery dappling across floor and
  furniture. A sick, oversized pale moon visible behind the broken rose window. Scattered dying
  candle points give secondary warm flicker; everything outside their reach falls to near-black.
- Static detail (library / cabinet of curiosities): colossal leaning bookshelves, toppled and
  stacked books, dusty globes, specimens in murky jars, stopped mantel clocks, cracked mirrors,
  cobweb sheets in the corners; pale fungus and spectral-green phosphorescent mold creeping as
  ground cover and up the shelves (the cool accent against the warm amber).
- Animated life: distant Lovecraftian silhouettes — slow tendrils/limbs — stirring in the far fog
  (the implied hero presence, never fully resolved); a flock of bats with flocking behavior
  wheeling through the atrium; creeping ground mist, plus golden dust motes drifting inside the
  light shafts and spectral-green spores adrift in the dark.
- Set pieces: [HERO] grand double staircase beneath a colossal cracked crystal chandelier that
  refracts moonlight into drifting caustics and faintly tinkles; [HERO] haunted ancestor portrait
  gallery with eyes that track the camera and one shrouded central canvas; [support] the shattered
  rose window with the sick moon behind it (the god-ray source); [support] a colossal stopped
  grandfather clock with visible gears and a frozen pendulum.
- Motion cadence: a slow, uneasy "breathing" — curtains and cobweb sheets stirring faintly, candle
  flames trembling, dust in perpetual drift, the occasional crystal tinkle and a barely-perceptible
  pulse through the far mist. Quiet, held, wrong.
- World: bounded ~400 m, interior-dominant with glimpses of a dead grove and grounds through broken
  windows; boundaries hidden by night fog and the dead trees, never visible from the starting
  vantage. Camera starts in a side gallery with a clear sightline to the staircase and chandelier.

CONTROLS
WASD move, mouse look (pointer lock), Q/E up/down, Shift to accelerate

VERIFICATION
- Visual critic: a separate subagent that sees ONLY the renders, never the code or reasoning.
  Give it 6 fixed camera poses, rendered at 2560×1440 in GPU-accelerated Chrome, plus a short
  recording of the fly-through to catch shimmer, aliasing, popping and banding. It returns
  prioritized, concrete defects. Iterate until it reports nothing above "minor".
- Performance: GPU timestamp queries plus a frame-time log from the scripted fly-through.
  Report average, 99th percentile and max.

DONE WHEN: both verification gates pass. Deliver index.html, the bundle size, the perf report
and the critic's final review.
