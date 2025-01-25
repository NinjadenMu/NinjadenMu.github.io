---
layout: post
title:  "Drone Swarm Flocking and Particle Swarm Optimization"
date:   2025-01-17 01:10:34 -0400
categories: AI
author: Jaden Mu
---
Schools of fish are really quite incredible: each fish independently moves cohesively with the group, matching every other fish's direction and velocity with no collisions.  More interesting, the groups are resilient: schools of fish can split and reform around obstacles, or scatter and gather back together in the presence of predators.  The behavior of fish and flocks of birds inspired Craig Reynolds to develop "Boids", which simulates the behavior of a flock that coordinates and avoids collisions.

With some small modifications, his original paradigm from 1986 can be applied to drone swarms and a problem known as drone flocking.  
Drone flocking seeks to accomplish a few qualitative goals: 
1. Gather all drones into one cohesive, compact "flock"
2. Avoid collisions within the flock
3. Moving in a group, head towards some destination

On the level of an individual drone, the above goals translate into the following:
1. Move towards other drones (to keep the flock compact)
2. Move away from drones that are too close (to avoid collisions)
3. Move towards the target
4. Match the average velocity of the flock

We want to consider motion on the level of an individual drone so we know the correct control signals for each drone.  Specifically, a drone's velocity vector is defined by the sum of 3 vectors that account for each of the above objectives.  We can think of these velocity vectors as a result of some "force" that acts on each drone.  Because the same rules apply for every drone, each drone considers itself to be the "active drone" when calculating its control vector.  
#### Vector 1: Centering
The center of mass of every drone in the swarm is calculated (or approximated by all the drones the active drone is within sensing range of).  Every drone will move in the direction of the center of mass to make the flock more "compact".  Given that drone i's location *<x, y, z>* is represented by X<sub>i</sub>, the center of mass of the swarm is Σ(X<sub>i</sub>)/n, and the centering vector is Σ(X<sub>i</sub>)/n - X<sub>active drone</sub>.  By having every drone move towards the center, the whole swarm becomes more compact/"cohesive".
#### Vector 2: Avoidance
To avoid collisions, drones that are too close should move apart from each other.  The active drones moves away from all drones within some safety threshold *s*.  This vector can be represented as:

-Σ<sub>i: |X<sub>i</sub>-X<sub>active</sub> < s|</sub> (X<sub>i</sub> - X<sub>active drone</sub>)

The advantage of using a safety threshold is that as soon as drones are far enough apart from each other, the repulsive force stops, allowing the flock to be very compact.  It's also computationally faster than some nonlinearity.
#### Vector 3: Targetting
This vector is pretty simple: each drone also also tries to head towards some waypoint/target X<sub>target</sub>.  The nice thing is that objective 3 (moving towards the target) and objective 4 (matching the average velocity) can be rolled into one, since the average velocity will be pointing towards the waypoint.  The attraction and avoidance vectors cancel out due to how the forces are symmetric for both drones. 

#### The Final Control Vector
To get our overall control vector, we simply compute the weighted sum of each of the three vectors (the weights depend on the qualitative priorities you're looking for.)  When we run this program, it turns out that we get all our desired flocking properties: every drone joins up into a cohesive flock, and the flock heads towards the waypoint with no inter-drone collisions.  The three vectors we defined are very similar to Reynold's original Boids algorithm, so this method of drone flocking is called "Reynolds-rule based flocking".  We can see the algorithm in action below, where the red dot represents the target/waypoint and the blue dots represent drones:

![Flocking GIF](/assets/swarms/89174F31-764F-4B20-A45D-E456645988D6.gif)

We can see that the drones group up into a flock, and then move towards the target (this is because when the drones are dispersed, the attractive force is at its strongest.  You'll notice that the attractive force magnitude decreases linearly as the drones get closer.)  More interestingly, because each drone's movement vector is computed by averaging the positions of every other drone, the group as a whole is robust to a few drones malfunctioning (these errors get averaged out.)  To illustrate this, in the next example, 20% of the drones will report a completely random position to every other drone.  This is a fairly significant portion of the flock, so every drone will receive some erroneous information when it's calculating its control vector.

![Perturbed Flocking GIF](/assets/swarms/7FFB0075-425F-424B-9FD6-EB8DEE8CAF0C.gif)

You'll notice there's a little bit noise as the flock is heading towards the waypoint, but every drone still makes it to the target: the random reported positions are causing some jitters but are averaged out.

### Particle Swarm Optimization (PSO)
Overall, the above drone flocking algorithm is pretty simple and qualitative, although I do think it's kinda cool.  However, it's very close to an algorithm called particle swarm optimization, which I found interesting both conceptually and mathematically (this is the first time I've looked at optimization from a more rigorous angle.)

Imagine some higher dimensional space, where each point is associated with some "cost" (in a space of n dimensions, each point is defined by (a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>), where each a ∈ ℝ, or rather, each point belongs to ℝ^n.  In 3d space, (a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>) correspond to (x, y, z).)  Our goal is to find the point in this space with the lowest cost.  If we can't differentiate this cost function, we have to resort to methods like PSO, which explore the space to try and find a good solution (the solution may not be optimal - it's generally infeasible to explore the whole space).  






