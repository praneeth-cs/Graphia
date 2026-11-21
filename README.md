# Graphia

**See what a matrix does.** Type a 3×3 matrix and watch it move 3D space: stretching, shearing, rotating, flipping or flattening it.

**Live demo:** https://praneeth-cs.github.io/Graphia/

Graphia is a free, browser-based visualiser for linear algebra. It treats a matrix as an *action on space*, not a grid of numbers. Every feature answers one question: **what does this matrix do to space?**

---

## Why Graphia

Most matrix calculators give you numbers: a determinant, some eigenvalues, an inverse. Graphia shows you what those numbers mean:

| Number | What you see |
|---|---|
| Columns of M | Where the basis vectors î, ĵ, k̂ land |
| Determinant | How the volume of the unit cube changes (and whether it flips inside out) |
| Rank | Whether space gets squashed onto a plane, a line or a point |
| Eigenvectors | The directions that only stretch and never turn |
| Inverse | The animation played backwards |
| SVD | Any matrix split into rotate → stretch → rotate |
| Ax = b | Three planes meeting at a point, along a line, or not at all |

## Features

**Core**
- 3×3 matrix input with live updates
- Smooth animation from the identity to M
- Transformed grid, unit cube and basis vectors, colour-coded to the matrix columns
- Orbit, zoom and reset camera (mouse, trackpad and touch)
- Determinant, rank, trace and eigenvalues (real and complex) shown live
- Presets: rotation, shear, stretch, reflection, projection, symmetric, random

**Understanding**
- Plain-language reading of the matrix ("Rotates 30° about z…", "Squashes space onto a plane…")
- Step-by-step basis view: move î, then ĵ, then k̂ to their columns
- Eigenvector lines labelled with their eigenvalues

**Deeper views**
- **Composition:** A then B next to B then A, showing why AB ≠ BA
- **Inverse:** undo the transformation, or see why it can't be undone
- **Decomposition (SVD):** a sphere becoming an ellipsoid in three animated stages
- **Linear systems:** Ax = b as intersecting planes, with the solution type explained

**Sharing**
- Every view stores its matrix in the URL, so you can send someone a link to a specific example

## Mockups

The repo currently contains six interactive design directions for the same idea. One will become the main app.

| Page | Direction | Focus |
|---|---|---|
| [`lab.html`](lab.html) | Dark, technical workbench | Transform, volume, eigenvectors, inverse, share links |
| [`notebook.html`](notebook.html) | Light, paper-style explainer | Basis vectors one at a time, plain-language description |
| [`compose.html`](compose.html) | Clean studio, split view | AB vs BA with synced cameras |
| [`decompose.html`](decompose.html) | Warm dark | SVD as rotate → stretch → rotate |
| [`systems.html`](systems.html) | Blueprint | Ax = b as planes: point, line, or no solution |
| [`studio.html`](studio.html) | Red, black and white | Transform, decompose and inverse in one page |

## Scope

Graphia stays focused on one idea. This list keeps it that way.

**In scope**
- 2×2 and 3×3 matrices as transformations of space
- Visual explanations of determinant, rank, eigenvectors, inverse, composition, SVD and linear systems
- Teaching aids: presets, step-by-step animations, plain-language descriptions
- Sharing through URLs
- Running entirely in the browser with no account and no server

**Out of scope**
- Matrices larger than 3×3 as transformations (they can't be drawn as a change of 3D space)
- Symbolic algebra (variables, exact fractions, step-by-step row reduction proofs)
- User accounts, saved libraries or any backend
- General-purpose graphing (functions, surfaces, data plots)

If a feature doesn't help someone *see* what a small matrix does, it belongs in a different project.

## Roadmap

**v1.0: one app**
- [ ] Choose the main design direction from the mockups
- [ ] Merge the best features into a single app with modes (Transform · Compose · Decompose · Systems)
- [ ] Keyboard-friendly matrix input (Tab / arrow keys between cells)
- [ ] Mobile layout pass

**v1.1: interaction**
- [ ] Drag basis-vector tips in 3D to edit the matrix directly
- [ ] Slider per cell, plus a rotation-angle slider for rotation presets
- [ ] 2×2 mode (the same engine, flattened to a plane)
- [ ] Undo / redo for matrix edits

**v1.2: learning**
- [ ] Quadratic forms: a symmetric matrix drawn as the ellipsoid xᵀAx = 1
- [ ] Null space and column space highlighted for singular matrices
- [ ] Guided challenges ("find a matrix that sends this cube to that shape")
- [ ] Export the current view as a PNG

## Tech

- **Plain HTML, CSS and JavaScript.** No framework, no build step, no dependencies.
- **`js/graphia.js`** (about 500 lines) contains:
  - Matrix maths: multiply, determinant, inverse, rank, eigenvalues (closed-form cubic), eigenvectors, symmetric eigen (Jacobi), SVD, axis–angle rotations, solving Ax = b
  - A small canvas 3D renderer: perspective camera, orbit and zoom, depth-sorted lines, polygons, arrows and labels
  - Shared widgets: matrix editor, presets, URL sharing
- The maths is tested against hundreds of random matrices and edge cases: singular, repeated eigenvalues, complex eigenvalues and reflections.

## Run locally

Open `index.html` in a browser. To use a local server instead:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy (free)

**GitHub Pages**
1. Push the files to the root of the repo (or a `docs/` folder).
2. Go to **Settings → Pages → Build and deployment**.
3. Choose **Deploy from a branch**, then `main` and `/ (root)` (or `/docs`).
4. The site is live at `https://<username>.github.io/Graphia/` within a minute or two.

The included `.nojekyll` file tells GitHub Pages to serve the files exactly as they are.

Netlify, Cloudflare Pages and Vercel also work: point them at the folder, with no build command.

## Project structure

```
Graphia/
├── index.html          Gallery / landing page
├── lab.html            Mockup 1: workbench
├── notebook.html       Mockup 2: explainer
├── compose.html        Mockup 3: AB vs BA
├── decompose.html      Mockup 4: SVD
├── systems.html        Mockup 5: Ax = b
├── studio.html         Mockup 6: red / black / white
├── js/
│   └── graphia.js      Matrix maths + 3D renderer
├── assets/             Gallery thumbnails
├── .nojekyll
└── README.md
```

## Contributing

Issues and pull requests are welcome. Before proposing a feature, check it against the **Scope** section above. Graphia aims to do one thing well.

1. Fork the repo and create a branch.
2. Make your change. Keep it dependency-free.
3. Open the affected pages in a browser and check the browser console for errors.
4. Open a pull request describing what you changed and why.

## Inspiration

- 3Blue1Brown, *Essence of Linear Algebra*, for the idea of reading a matrix as a transformation of space.

## License

MIT
