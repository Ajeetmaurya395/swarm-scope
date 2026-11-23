# Demo video script (≈ 4 minutes)

Record the screen at 1080p, with the browser at about 90% zoom so all three columns fit. Use OBS, Loom or the Windows Game Bar (Win + G).

| Time | On screen | Say |
|---|---|---|
| 0:00–0:20 | Landing page, Sphere | "This is SwarmScope, an interactive tool for learning Particle Swarm Optimization. Every iteration is broken into five phases, and each one is animated, explained and shown with its real numbers." |
| 0:20–1:10 | Press **Step** slowly through one iteration. Point at the phase bar, the highlighted pseudocode and the explanation card | "Evaluate: each particle measures f. Personal best: the green rings are particles that beat their own record. Global best: the gold star is the swarm's best. Velocity: each particle mixes three urges. Move: x becomes x plus v." |
| 1:10–1:50 | Click a particle. Point at the force diagram and the Inspector | "This is what's new: the grey, blue and orange arrows are inertia, memory and social pull, tip to tail. Their sum is the pink arrow. On the right is the same equation with this particle's real numbers substituted." |
| 1:50–2:20 | Press **◀ Back** twice, then **Step** again | "Back is a true undo. Every phase is snapshotted, including the random seed." |
| 2:20–3:00 | Switch to **Rastrigin**, click **Exploiter**, press Play. Then Reset, click **Explorer**, press Play. Point at the convergence and spread charts | "Parameters change the behaviour: the Exploiter converges fast but gets stuck in a local dip. The Explorer keeps searching. Explosion, with w = 1.1, flies apart. Ring topology on Himmelblau forms sub-swarms." |
| 3:00–3:30 | Turn on **Predict-the-move challenge** and click a guess | "In challenge mode the tool rolls r₁ and r₂, then asks you to predict where the particle lands. It scores your guess, so you test your understanding rather than just watch." |
| 3:30–4:10 | **Worked example** tab. Step two iterations, scroll to the sheet, press **Run self-test** | "Here is the textbook check: three particles with fixed random numbers. The hand calculation is printed here, and the self-test runs the same engine and compares 30 values: all 30 match. P3 leads but has zero velocity, so it never moves. That's a classic PSO weakness you can see." |
| 4:10–4:20 | Custom function box | "You can also type your own function. It's one HTML file, hosted free on GitHub Pages. Thanks!" |
