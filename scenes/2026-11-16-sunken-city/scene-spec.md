Build a real-time drowned-metropolis dreamscape that runs in the browser — a dead post-human
city reclaimed by neon coral and iridescent toxic beauty, flooded and sunk. It only needs to
look beautiful and let me fly a free camera through it.

PRIORITIES (in this order when they conflict)
1. Visual quality
2. Stable frame pacing at the target spec
3. Small bundle size

FIDELITY CEILING: stylized-minimalist procedural (not photoreal). The critic must NOT flag
flat-shaded matte surfaces, hard-edged emissive, banded fog, or blocky/low-poly geometry as
defects — those are the intended look. The mood is "toxic-beautiful ruin": oil-slick
iridescence over decay is a feature, not grime to be cleaned.

CONSTRAINTS
- No Three.js/Babylon.js or other engines. WebGPU rendered. Everything procedural: no
  texture/model files. Single self-contained index.html. Report minified size.
- Zero per-frame JS allocations. Preallocate all buffers.

TARGET
- Windows 11 25H2, Chrome 157, RTX 5070 Ti, Ryzen 7800X3D, 180 Hz monitor
- 2560×1440 full resolution. GPU frame time ≤ 11 ms average, no frame > 16.7 ms during a
  scripted 60 s fly-through.

SCENE
- A sunken post-apocalyptic city in deep water. Leaning skyscraper columns of glass and
  concrete form submerged canyons and avenues the camera flies down; broken elevated highways
  and suspension bridges arch between towers with severed cables drifting; collapsed domes and
  a half-caved stadium open into interior lagoons/amphitheaters. Traversable arches
  (bridge spans, blown-out tower floors, highway underpasses) everywhere.
- Street level is a reef of coralized urban junk: cars, buses, traffic signs, lampposts and
  street furniture encrusted with coral and barnacles, forming the ground-cover detail.
- Strong depth fog/absorption with an explicit near→far gradient: acid toxic-green up close →
  green-black murk in the distance. Dense turbid medium with suspended sediment that hides the
  world bounds completely from the start.
- Light is multi-source and sickly: pale god-ray shafts filter down from a distant wavy
  surface high above, with faint caustics dappling horizontal surfaces; the dominant light is
  BIOLUMINESCENCE from the neon coral and organisms (pulsing emissive magenta/cyan/electric-
  green); dying artificial lights still flicker and short-circuit underwater — neon signs,
  streetlamps and scattered lit windows stutter and buzz; iridescent chemical/oil films coat
  submerged ceilings and still surfaces, refracting rainbow sheens (oil-slick iridescence).
- "Flora": branching neon coral colonies (iridescent magenta/cyan) climbing façades and
  windows; forests of giant green-gold kelp swaying between the buildings with a low algae
  ground cover; pulsing toxic anemones and bioluminescent barrel sponges on ledges and debris;
  coralized junk as scattered prop clusters.
- Animated life: a colossal hero creature (a great whale or manta) gliding slowly through the
  tower canyons for scale; a dense fish school that schools and snakes through the avenues with
  flocking (turning as a mass); drifting bioluminescent jellyfish pulsing slowly as they float;
  particle systems — falling marine snow / sediment, rising bubbles from leaks and vents, and
  drifting glowing spores/motes.
- Set pieces: (1) a colossal iconic skyscraper SNAPPED in half, coralized, leaning across the
  avenue — the central hero landmark; (2) a giant submerged civic monument/statue half-buried
  and overgrown with life; (3) a crashed airliner (or shipwreck) broken across the buildings,
  torn open and coralized; (4) a collapsed stadium/dome that forms an open bioluminescent
  amphitheater lagoon.
- Motion cadence: kelp and anemones sway slowly in a current; coral bioluminescence pulses and
  breathes; dying neon flickers/shorts erratically; bubbles rise, marine snow falls, spores and
  motes drift constantly; the hero creature and jellyfish glide slowly and majestically.
- World: bounded; the boundaries dissolve into dense green murk and can't be seen from the
  start. Camera begins in a wide submerged canyon-avenue, facing down the street toward the
  snapped hero skyscraper, with towers receding into fog on both sides.

CONTROLS
WASD move, mouse look (pointer lock), Q/E up/down, Shift to accelerate.
Building collision + ground clamp on (free-fly can't pass through buildings or fall through the
seabed; flying up over the rooftops is allowed).

VERIFICATION
- Gate 0 (mechanical, first): orientation via ?calib markers + void/empty-frame metrics.
- Gate 1 (critic): isolated critic anchored to the fidelity ceiling; claims verified; ensemble.
- Gate 2 (perf): GPU timestamp queries, avg/p99/max.

DONE WHEN: all three gates pass. Deliver index.html, bundle size, perf report, critic review.
