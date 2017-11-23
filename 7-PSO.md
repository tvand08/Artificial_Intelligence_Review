# Chapter 7: Particle Swarm optimization

### Introduction
- Particle Swarm Optimization is a population based, stochastic optimization technique.
   - Inspired by swarming behaviors of birds, PSO is based upon a collection of agents
   - Movement governed by iterative calculation and application of a velocity vector, causing flight like movements
- Particle movement premised on two simple behaviors
   - Move towards own best position
   - Move toward the best position in a neighborhood

### Fundamentals
- Particles represent solutions
   - Simple approach - the position of the particle is the solutions
   - more complicated - the position is interpreted/decoded as a solution
- Each particle holds three pieces of information
   1. _x(t)_ - current position
   2. _v(t)_ - velocity
   3. _y(t)_ - personal best solution
- Goal is to have the particle move towards the optimal point in the search space
- particle moves through space by calculating and applying a velocity
- Swarms are networks of particles - usually fully connected
   - keeps track of __*y*__ - the best solution found in the neighborhood

### Velocity Update
- Vanilla velocity Update
   - v<sub>i</sub>(_t_ + 1) = _w_ v<sub>i</sub>(_t_) + c<sub>1</sub>r<sub>1</sub>(_y_(t) - x<sub>i</sub>(_t_)) + c<sub>2</sub>r<sub>2</sub>(__*y*__(_t_) - x<sub>i</sub>(_t_))

### Vanilla PSO algorithm
```
function(Synchronous) PSO
   initialize particles randomly
   initialize velocities to zero
   while (iteration < max_iterations || stopping criteria not met) do
      for all (particles in swarm) do
         evaluate fitness
         update personal best position
      end for
      update neighborhood best particle(s)
      for all (particles in swarm) do
         calculate new velocity
         update particle position
      end for
  end while
  return global best particle
end function
```

### Why use PSO?
- Some Advantages
   - simple operations lead to complex emergent behaviors
   - easily parallelized, especially in synchronous version
   - relatively small number of parameters
   - vey efficient for certain continuous optimization problems
   - many extensions/variations exist for various types of problems
- Some disadvantages
   - Naive representation may be too simple for some problems
   - vanilla PSO can easily get stuck in local optima
   - difficult to represent discrete problems
      - leads to poor performance
  - convergence rate slows dramatically later in the run
     - local refinement is a problem
