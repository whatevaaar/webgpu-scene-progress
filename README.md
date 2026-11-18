# WebGPU Scene Progress

Historial público del avance de un pipeline de **escenas 3D procedurales en tiempo real para
el navegador** (WebGPU, sin motores, un solo `index.html`, todo procedural, cero asignaciones
de JS por frame) y de la calidad de sus resultados a lo largo de las sesiones.

Este repo es el **registro/galería**. El cerebro —las *skills* que generan las escenas— vive en
el repo padre:

> **Repo padre (skills):** [`whatevaaar/webgpu-scene-skills`](https://github.com/whatevaaar/webgpu-scene-skills)
> Pipeline de 3 skills para Claude Code: `scene-spec` → `scene-build` → `scene-verify`.
> Generaliza el prompt de **Abyssal Garden** de Noniv
> ([demo](https://noniv.github.io/abyssal-garden/), MIT).

---

## Cómo se produce cada escena

1. **`/scene-spec`** — Drill-down en español a partir de una idea mínima → un `scene-spec.md`
   técnico en inglés (firma visual, hero elements, referencia de arte, atmósfera, vida, hitos).
2. **`/scene-build`** — Un único `index.html` autocontenido: WebGPU, geometría/ruido/materiales
   procedurales, cero asignaciones por frame, hooks de verificación (`?pose=0..5`,
   `?flythrough=1`, `?calib=1`, `window.__perf()`).
3. **`/scene-verify`** — Tres gates: **Gate 0** correctitud mecánica (orientación + frame-no-vacío,
   sin LLM), **Gate 1** critic visual aislado (un subagente que sólo ve los renders), **Gate 2**
   performance (GPU timestamps, avg/p99/max).
4. **Video deliverable** — `record-video.js` graba el fly-through a `.webm` en
   **horizontal (1920×1080)** o **vertical (1080×1920)**, duración parametrizable (~5 s).

Cada escena vive en su propia carpeta y se archiva acá con su spec, `index.html`, renders y video.

---

## Cómo ver una escena

Abrí su `index.html` en **Chrome/Edge recientes** (WebGPU activo por defecto). Controles:
click para pointer-lock, **WASD** moverse, **mouse** mirar, **Q/E** bajar/subir, **Shift**
acelerar. Vistas fijas: `?pose=0..5`. Recorrido automático: `?flythrough=1`.

---

## Línea de tiempo del progreso

### Sesión 1 — Jardín cyberpunk en azotea (bajo lluvia neón)
Primera corrida de punta a punta: validó el pipeline (spec rico → render correcto y rápido →
critic + perf). **Postmortem clave:** un bug de orientación de cámara (giro de 180°) sobrevivió
~16 rondas porque el critic estético no verifica corrección → se institucionalizó el **Gate 0
mecánico** (correctitud barata y determinista ANTES de la belleza).

### Sesión 1.5 — Biblioteca infinita borgesiana
Segunda escena. Reforzó los "postmortem levers" (Gate 0 + grounded-ensemble critic).

### Sesión 2 — Ciudad inundada *(Sunken City)* · archivada acá
Metrópolis submarina muerta reconquistada por coral neón. Resultados de verificación:
**Gate 0 PASS**, critic convergió de *blocker + 6 majors* a pulido en 6 rondas,
**Gate 2 PASS** (avg **4.9 ms** / p99 **7.7 ms** / max **8.5 ms** @ 2560×1440, presupuesto 11 ms).

**Hallazgos y mejoras de esta sesión** (ver `POSTMORTEM.md` del repo padre):
- **Las escenas salían demasiado parecidas** entre sí: un *toolkit fijo de primitivas*
  (cubos + conos + sprites) hacía que cualquier tema colapsara a "cajas brillantes + conos +
  niebla", cambiando sólo la paleta. → Se agregaron **firma visual** y **hero elements** al spec,
  **rúbrica de calidad positiva** + **check de unicidad** al verify, y guía de materiales/geometría
  específicos del tema al build.
- El **"techo de fidelidad"** se usaba como excusa para esfuerzo bajo → reformulado.
- **Bug del mouse** (en varias escenas): overlays a pantalla completa sin `pointer-events:none`
  tapaban el canvas e impedían el pointer-lock → corregido y codificado como check P0.
- Nueva convención: **una carpeta por escena**. Nuevo **deliverable de video** (vertical/horizontal).

### Sesión 3 — Mansión embrujada gótica *(Haunted Mansion)* · archivada acá
Test de punta a punta de las skills **recién actualizadas** (levers de *fidelidad = compromiso +
especificidad temática*, con techo que escala con los ciclos). Tema: decadencia Poe + pavor
lovecraftiano. Resultados: **Gate 0 PASS** (atrapó bugs reales: frames negros por readback de
GPU-timestamps a un buffer con `mapAsync` pendiente, y una luna inexistente como geometría),
**Gate 2 no verificable** en la máquina (iGPU Intel, no la RTX del TARGET).

**Hallazgo clave — el *plateau de primitivas*:** es la **primera escena que NO cruza el Gate 1**.
Convergió en todo lo atmosférico (se cerraron niebla lechosa, sobreexposición, aliasing de sombras;
sin god-rays difusos ni specular plástico), pero 5 critics aislados coinciden en que los **hero
elements** (rosetón, retratos, murciélagos, llamas) hechos con quads/discos/cuñas se leen como
"primitivas temáticas". Los scores **rebotan** (especificidad 4→3→5→3→4), señal de que cruzar el
gate exige **cambio estructural** (mallas de tracería/bustos/criaturas reales), no parche cosmético.
Expone el techo del enfoque "todo procedural a mano" para sujetos sensibles (rostros, tracería).
Ver el postmortem completo en la carpeta de la escena.

---

## Galería

| Escena | Carpeta | Estado |
|---|---|---|
| Sunken City | [`scenes/2026-11-16-sunken-city/`](scenes/2026-11-16-sunken-city/) | Gate 0 ✅ · Critic convergido · Gate 2 ✅ (4.9 ms avg) |
| Haunted Mansion | [`scenes/2026-11-17-haunted-mansion/`](scenes/2026-11-17-haunted-mansion/) | Gate 0 ✅ · Critic **no convergió** (plateau de primitivas) · Gate 2 no verificable (iGPU) |

---

## Licencia

Las escenas se generan con el pipeline del repo padre (`webgpu-scene-skills`, **GPLv3**), a su vez
derivado del prompt de **Abyssal Garden** (Noniv, MIT). Este repo de progreso hereda esa cadena de
atribución; ver el repo padre para los términos completos.
