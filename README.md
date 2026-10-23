# Interactive Leaf Vein Growth Simulation

Leaf veins form branching networks as they grow toward sources of growth signals. This browser-based JavaScript simulation lets you explore a simple version of that process: each press of **Space** adds attraction points and advances a network of vein points toward them. The result makes the relationship between local attraction and the emerging pattern visible one step at a time.

## Team members

- **NeefMan** — [@NeefMan](https://github.com/NeefMan) (repository contributor)

## Setup and installation

**Requirements:** A browser with JavaScript and HTML Canvas support. There are no packages to install, build steps, datasets, API keys, or environment variables.

1. Clone the repository:

   ```sh
   git clone https://github.com/NeefMan/leaf-veination-simulation.git
   cd leaf-veination-simulation
   ```

2. Open `index.html` in your browser.
3. Press **Space** to add attraction points and advance the simulation. Press it again to continue growing the network.

The 600 × 600 canvas starts with one green vein point near its bottom edge. New attraction points are red; the background is gray. Refresh the page to start over.

## Project highlights

- **Step-by-step interaction:** Each Space press attempts to add three attraction points, assigns every point to its nearest vein point, and performs one growth step.
- **Consistent growth distance:** A vein point with a nonzero growth direction creates a new point 2 pixels away in that direction.
- **Local point removal:** Attraction points within 5 pixels of a vein point are removed, so growth can move on toward remaining points.
- **No installation:** The entire simulation runs from `index.html` and `index.js` in a browser.

These are implementation details, not performance measurements; the repository does not include benchmarks or automated tests.

## How it works

1. **Seed the network.** `index.js` creates one vein point at the bottom center of the canvas and starts a `requestAnimationFrame` loop that redraws the current state.
2. **Add attraction points.** On each Space press, the simulation tries three random positions across the canvas. A candidate is discarded if it falls within 5 pixels of an existing attraction point or vein point.
3. **Choose the nearest vein.** For each attraction point, the simulation finds the closest vein point and adds the vector toward the attraction point to that vein's growth direction. Several attraction points can therefore steer the same vein point.
4. **Grow.** Each vein point with nonzero horizontal and vertical direction components creates one new vein point. The summed direction is normalized to a 2-pixel step before the new point is added; growth directions are then reset.
5. **Remove reached points and redraw.** Attraction points within 5 pixels of a vein point are removed. The animation loop draws vein points in green and remaining attraction points in red.

Nearest-vein assignment makes each attraction point influence one part of the network. Summing the vectors lets nearby points combine their pull, while normalization keeps each new step the same length regardless of that sum's magnitude. The display draws points rather than connecting vein segments, and attraction points can appear anywhere on the square canvas; there is no leaf-shaped boundary.
