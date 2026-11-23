# SwarmScope demo video script (about 4 minutes)

**Before you record**
- Open https://ajeetmaurya395.github.io/swarm-scope/ and set the browser zoom to about 90% so all three columns fit.
- Leave everything on the defaults: Sphere, seed 7, 20 particles.
- Set the Speed slider to about 2/s, so viewers can follow along when you press Play.
- Don't read this word for word. Read each part once, then say it in your own words, as if you're explaining it to a friend. Small pauses and "so…" are fine.
- If you're recording with a teammate, split it at the 2:30 mark. One person does the first half, the other does parameters onwards.

---

### 0:00 · Intro *(landing page)*

> Hi, I'm Ajeet. For this assignment we picked **Particle Swarm Optimization** and built a tool called **SwarmScope**.
>
> PSO is usually taught as one scary-looking equation on a slide. We wanted you to actually *watch* that equation work, one small step at a time.

### 0:20 · What's on screen *(point at the map)*

> So, this coloured map is the function we're trying to minimise. Think of it as a landscape where we want the lowest point. White is low, dark blue is high, and this little cross is the true answer.
>
> Each black dot is a particle. A particle is just a guess, and all of them together make the swarm.

### 0:40 · One iteration, slowly *(press **Step** five times, pausing after each)*

> Instead of jumping straight to the next frame, we split every iteration into five phases. You can see them up here.
>
> **Step.** *Evaluate*: every particle checks how good its spot is.
>
> **Step.** *Personal best*: the green rings are particles that just beat their own record. Each one remembers its best spot, which is these small blue squares.
>
> **Step.** *Global best*: the gold star is the best spot anyone has found so far. That's the leader.
>
> **Step.** *Velocity*: this is where every particle decides where to go next.
>
> **Step.** *Move*: and everyone takes their step.
>
> And on the right, the pseudocode highlights the line we're on, and this box explains what just happened in plain English, using the real numbers.

### 1:35 · Why a particle moves the way it does *(click any particle, then press **Step** four times so the phase bar shows Velocity)*

> This is my favourite part. I'll click on one particle, and it turns pink.
>
> At the velocity step you get three arrows joined tip to tail. **Grey** is inertia: "keep going the way I was going". **Blue** is memory: "go back to my own best spot". **Orange** is the social pull: "go where the leader is". Add them up and you get this **pink dashed arrow**, which is where it really goes.
>
> And the Inspector on the right writes out the formula with this particle's actual numbers plugged in. If you had to show your working in an exam, this is exactly it.

### 2:15 · Back button *(press **Back** twice, then **Step**)*

> If you miss something, just hit Back. It's a proper undo. It even rewinds the random numbers, so stepping forward again gives exactly the same result.

### 2:30 · Changing the parameters *(Problem → Rastrigin, click **Exploiter**, press **Play**)*

> Now let's play with the settings. I'll switch to Rastrigin. It looks like an egg tray, full of fake dips that trap you.
>
> With the **Exploiter** preset, the particles follow the leader very strongly… and look, the whole swarm rushes together really fast. The spread chart drops straight down. But the best value gets stuck at about **1**, not 0. It settled in the wrong dip. That's called *premature convergence*.
>
> *(press **Reset**, click **Balanced**, press **Play**)*
>
> Same problem, same starting positions, just the balanced values of w, c1 and c2… and this time it finds the real minimum, right at zero. Same algorithm, completely different result, just from three numbers.
>
> *(click **Explosion**, press **Play** for a few seconds)*
>
> And just for fun: with inertia above 1, the speeds keep growing and the swarm flies apart. That's why textbooks tell you to keep w below 1.

### 3:15 · Challenge mode *(Reset, tick **Predict-the-move challenge**, press **+1 iteration**)*

> We also added a little game. Before each move, it shows you the random numbers and asks where you think this particle will land. I'll guess… here.
>
> *(click your guess)*
>
> …and it shows how far off I was. It's a quick way to find out whether you really understand the update rule, or whether you've just been watching.

### 3:40 · Is it actually correct? *(untick the challenge, open the **Worked example** tab, press **Step** about 9 times, scroll down, click **Run self-test**)*

> Finally, how do we know the maths is right? In the Worked example tab there's a small problem: three particles with fixed random numbers, so you can do the whole thing with pen and paper. The full hand calculation is written out down here.
>
> When I step through, the Inspector gives exactly the same numbers as the paper working. And **Run self-test** compares thirty values from our code with the hand values. Thirty out of thirty match.
>
> This example also shows something interesting: particle 3 is the leader, but its velocity is zero, so it doesn't move at all while it's in front. That's a real weakness of basic PSO.

### 4:10 · Wrap-up

> That's SwarmScope. It's a single HTML file with no libraries, hosted for free on GitHub Pages. The link and the code are in the description. Thanks for watching!
