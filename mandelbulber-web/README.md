# Fractalarium — a browser Mandelbulb explorer

A real-time, interactive **3D Mandelbulb** fractal explorer that runs entirely in
the browser. Inspired by the gorgeous [Mandelbulber2](https://github.com/buddhi1980/mandelbulber2)
desktop renderer, this is a lightweight, zero-dependency, "more interactive vibe"
take: a single HTML file that ray-marches the fractal on the GPU with WebGL.

![preview](./preview.png)

## Try it

Just open `index.html` in any WebGL-capable browser — no build step, no server, no
dependencies. Or host the folder (e.g. GitHub Pages) and share the link.

## What it does

The fractal is rendered by **ray marching a distance estimator** of the Mandelbulb
in a GLSL fragment shader, with orbit-trap coloring, soft shadows, ambient
occlusion, fresnel rim light, and a volumetric glow pass.

### Controls
- **Drag** to orbit · **scroll / pinch** to zoom
- **Power (morph)** — reshape the fractal from blobby (2) to spiky (16)
- **Auto-morph power** — breathe the power value up and down over time
- **Auto-rotate** — slow turntable spin
- **Detail (iterations)** — fractal recursion depth
- **Palettes + Hue shift** — seven cosine-gradient color moods
- **Glow / Light angle** — mood and key-light direction
- **Quality** — Draft → Ultra (trades resolution/steps for framerate)
- **Soft shadows** — toggle the shadow march
- **Surprise me** — randomize the look · **Save PNG** — grab the current frame

### Keyboard
`H` hide/show UI · `Space` pause · `R` reset view · `F` fullscreen

## How it works (quick tour)

- A single full-screen triangle runs the fragment shader for every pixel.
- `map()` evaluates the classic Mandelbulb iteration
  `z → z^power + c` in spherical coordinates and returns an analytic distance
  estimate plus an orbit trap (used for coloring).
- The camera is a simple yaw/pitch/distance orbit around the origin; the shader
  gets the camera position and an orthonormal basis as uniforms.
- Everything is driven by uniforms, so all sliders update live with no shader
  recompilation.

## Notes

- Runs on WebGL 1 for broad compatibility. Rendering resolution scales with the
  Quality setting and device pixel ratio.
- Software renderers (e.g. headless/SwiftShader) work but are slow; a real GPU
  gives smooth interaction.

Not affiliated with Mandelbulber2 — just a fan's browser tribute to it.
