# SwarmScope: Particle Swarm Optimization, one step at a time

SwarmScope is a browser-based teaching tool for **Particle Swarm Optimization (PSO)**. You pick a landscape, set the coefficients and step through the algorithm one phase at a time. Each step has an animation, the exact numbers behind it and a plain-language explanation.

**Live demo:** `https://ajeetmaurya395.github.io/swarm-scope/`
**Demo video:** `<link to your 3–5 min video>`

It is a single `index.html` file with no build step and no dependencies. It works offline, apart from the web fonts.

---

## Features

| Requirement | How SwarmScope does it |
|---|---|
| Pick a problem | 6 standard test functions (Sphere, Booth, Himmelblau, Rosenbrock, Rastrigin, Ackley), plus **your own f(x, y)** typed as a formula |
| Change parameters | w, c₁, c₂ (these apply live, mid-run), swarm size N, random seed, max iterations, global vs **ring** neighbourhood, constant vs linearly decreasing inertia, v<sub>max</sub> limit, clamp vs bounce at the walls |
| Play / pause / step / reset | ▶ Play, Step (one phase), +1 iteration, **◀ Back (true undo)**, Reset, speed slider, keyboard shortcuts |
| Show the state at every step | Each iteration is split into 5 phases (Evaluate → Personal best → Global best → Velocity → Move). A phase bar, highlighted pseudocode, a live table of every particle and convergence/spread charts update at every phase |
| Visualise + explain | A heat map with contour lines, trails, personal bests, a gold star for the global best and a velocity arrow on every particle. Every phase gets a plain-language explanation that uses that step's actual numbers, plus a running log |
| Checked against a hand calculation | **Worked-example mode** with a fully hand-solved 3-particle example and a **built-in self-test** that compares 30 engine values with the hand values (all pass, tolerance 10⁻⁹) |

### What's new compared with VisuAlgo-style tools

1. **Velocity force diagram.** For the particle you click, the new velocity is drawn as three arrows placed tip to tail: <span>inertia</span> (grey), cognitive pull (blue) and social pull (orange). Their sum is drawn as a dashed pink arrow. You can *see* why a particle turns.
2. **Live substituted equation (Inspector).** The velocity formula is shown with that particle's real numbers plugged in (w, v, r₁, r₂, pbest, gbest, x), for both x and y. This is what a student writes in an exam.
3. **Predict-the-move challenge.** Before each Velocity phase the tool pauses, shows the dice rolls r₁ and r₂, and asks you to click where the particle will land. Then it shows the real landing spot and scores your guess. This tests whether you understand the update rule, not just whether you've watched it run.
4. **Behaviour presets as experiments.** *Balanced (Clerc)*, *Explorer*, *Exploiter*, *Loners (c₂ = 0)*, *Herd (c₁ = 0)* and *Explosion (w = 1.1)* each show one idea, with a one-line explanation of what to watch for.
5. **True step-back.** Every phase is snapshotted, including the random-number generator state, so ◀ Back is an exact undo, not a replay.
6. **Reproducible runs.** A seeded RNG (mulberry32) means the same seed gives the same run every time, which is handy for a demo or a viva.

---

## The algorithm (as implemented)

For each particle *i* and dimension *d*:

```
v_id ← w·v_id + c1·r1·(pbest_id − x_id) + c2·r2·(gbest_d − x_id)
x_id ← x_id + v_id
```

* r₁, r₂ ~ U[0, 1) are drawn fresh for each particle and each dimension. In worked-example mode they come from a fixed table instead.
* `gbest` is the best personal best in the whole swarm (*global* topology) or among the particle and its 2 neighbours (*ring* topology).
* Optional v<sub>max</sub> caps each velocity component at a fraction of the search width.
* At the walls, a particle either stops (its position is clamped and that velocity component is set to 0) or bounces (it is reflected and that component is negated).
* Personal bests update only on a *strict* improvement (`f < f(pbest)`).
* Linear inertia schedule: w(t) = w − (w − 0.4)·(t − 1)/(T − 1).

Inertia-weight PSO follows Shi & Eberhart (1998). The "Balanced" preset uses the Clerc & Kennedy (2002) constriction-equivalent values w = 0.729, c₁ = c₂ = 1.494.

---

## Verification: hand calculation

**Setup:** minimise f(x, y) = x² + y² on [−4, 4]². N = 3, w = 0.5, c₁ = c₂ = 1, all particles start with v = 0. Each particle uses one r₁ and one r₂ per iteration, for both dimensions.

| Particle | x⁰ | r₁, r₂ (iter 1) | r₁, r₂ (iter 2) |
|---|---|---|---|
| P1 | (2, 2) | 0.3, 0.5 | 0.4, 0.7 |
| P2 | (−1, 3) | 0.5, 0.2 | 0.6, 0.3 |
| P3 | (1, −1) | 0.8, 0.9 | 0.2, 0.5 |

**Iteration 1**
* f = 8, 10, 2. Personal bests are the start points, so gbest = P3 (1, −1), f = 2.
* P1: v = 0.5·0 + 1·0.3·0 + 1·0.5·((1,−1) − (2,2)) = **(−0.5, −1.5)**, so x = **(1.5, 0.5)**
* P2: v = 1·0.2·((1,−1) − (−1,3)) = **(0.4, −0.8)**, so x = **(−0.6, 2.2)**
* P3: v = **(0, 0)**. The leader is at rest and does not move.

**Iteration 2**
* f = 2.5, 5.2, 2. P1 and P2 improve their pbest. gbest stays P3, f = 2.
* P1: v = 0.5·(−0.5,−1.5) + 0.4·0 + 0.7·((1,−1) − (1.5,0.5)) = (−0.25,−0.75) + (−0.35,−1.05) = **(−0.6, −1.8)**, so x = **(0.9, −1.3)**
* P2: v = 0.5·(0.4,−0.8) + 0 + 0.3·((1,−1) − (−0.6,2.2)) = (0.2,−0.4) + (0.48,−0.96) = **(0.68, −1.36)**, so x = **(0.08, 0.84)**
* P3: v = **(0, 0)**

**Iteration 3 (evaluate)**
* f = 2.5, **0.712**, 2, so **gbest becomes P2 at (0.08, 0.84), f = 0.712**.

To run the check, open **Worked example · hand check** and press **Run self-test**. The result is **30 / 30 checks pass**. You can also step through it and compare the Inspector with the lines above.

The engine was also tested headless in Node and Chrome. On all six test functions, with both topologies and both wall rules, 100 iterations give no NaN and every particle stays inside the bounds. The runs reach the known optimum (for example Booth → (1.000, 3.000), Rastrigin → (0, 0)).

---

## How to use

| Key | Action |
|---|---|
| `Space` | Play / pause |
| `→` | Step one phase |
| `Shift` + `→` | Step one full iteration |
| `←` | Step back |
| `R` | Reset |

Click a particle (or a table row) to inspect it.

Things to try:
* **Rastrigin + Exploiter**: fast convergence, often into the wrong dimple. Then try **Explorer**.
* **Himmelblau + Ring**: sub-swarms settle in different minima.
* **Explosion (w = 1.1)**: the spread chart grows without limit.
* **Loners (c₂ = 0)**: the swarm never agrees on one answer.

---

## Run locally / deploy

```bash
git clone https://github.com/Ajeetmaurya395/swarm-scope.git
cd swarm-scope
open index.html        # or: python3 -m http.server 8000
```

**GitHub Pages (free):** go to repo → Settings → Pages → *Deploy from a branch* → `main` / `root` → Save. The site goes live at `https://ajeetmaurya395.github.io/swarm-scope/` within a minute. A workflow is also included in `.github/workflows/pages.yml` if you prefer *GitHub Actions* as the source.

Netlify / Vercel also work: drag the folder onto Netlify Drop, or import the repo with no build command.

## Project structure

```
index.html                    whole app: engine (pure functions) + UI
README.md                     this file
DEMO_SCRIPT.md                3–5 minute demo-video script
.github/workflows/pages.yml   optional auto-deploy to GitHub Pages
LICENSE                       MIT
```

The engine (`createState`, `stepPhase`, `selfTest`) has no DOM code. It sits between `ENGINE START` / `ENGINE END` markers so it can be tested in Node.

## Team

* `<Member 1 name>`
* `<Member 2 name>`

## References

* Kennedy, J. & Eberhart, R. (1995). *Particle swarm optimization.* Proc. IEEE ICNN.
* Shi, Y. & Eberhart, R. (1998). *A modified particle swarm optimizer.* Proc. IEEE CEC.
* Clerc, M. & Kennedy, J. (2002). *The particle swarm: explosion, stability, and convergence in a multidimensional complex space.* IEEE TEC 6(1).
* Inspiration for step-through UI: VisuAlgo (visualgo.net). No code reused.
