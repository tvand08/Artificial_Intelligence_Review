# Chapter 4: Informed Search algorithms

### Heuristics
- Heuristic: Any rule or method that provides some guidance in decision making
   - we use problem-domain specific information in making a decision
   - heuristics vary in the amount of useful information they can lend us
     - e.g. a stronger Heuristic: don't make any chess move that results in you losing a piece
     - e.g. a weaker heuristic: knights are  best moved into central board positions
-  heuristics are often denoted by a functional value: high values denote positive paths, while lower or negative are less promising ones

### A heuristic functional
- definition: A rule of thumb, simplification, or educated guess that reduces or limits the search for solutions in domains that are difficult and poorly understood
   - *h(n)* = estimated cost of the cheaptes path from node n to goal node
   - if *n* is goal then *h(n)=0*

### Heuristics algorithms
- Optimal (path) Search
   - best-first
   - A<sup>_*_</sup>
- Non-optimal Search
   - Hill-climbing
   - Beam Search
   - Simulated Annealing, Tabu Search
   - Genetic algorithms

##### best-first Search
- General approach of informed search:
   - node is selected for expansion based on an _evaluation function f(n)_
- Idea: evaluation function measures distance to the goal
   - choose node which appears best
- Implementation
  - _fringe_ is queue sorted in decreasing order of desirability.
  - Special cases: greedy search, A<sup>_*_</sup> Search

##### Greedy best-first Search
- Greedy expands the node with the lowest Straight line distance
- Properties
   - Complete:No
   - Time: O(b<sup>m</sup>)
   - Space: O(b<sup>m</sup>) - keeps all nodes in memory
   - Optimal: No

##### A<sup>_*_</sup> Search
- Idea: avoid expanding paths that are already expensive
- Evaluation function _f(n)=g(n) + h(n)_
   - g(n) = cost (so far) to reach n
   - h(n) = estimated cost to reach the goal from n
   - f(n) = estimated total cost of path through n to goal
- A* uses an admissible heuristic
   - a heuristic is admissible if it never overestimates the cost to reach the goal
   - Optimistic
   - Formally:
      1. h(n)<= h<sup>_*_</sup>(n) where h<sup>_*_</sup>(n) is the true cost form n
      2. h(n) >= 0 so h(G)=0 for any goal G
   - e.g. h<sub>SLD</sub>(n) never overestimates the actual road distance
- Properties of A<sup>_*_</sup>
   - Complete: Yes
   - Time: Exponential
   - Space: Keeps all nodes in memory
   - Optimal: Yes
- We can improve the memory cost of A<sup>_*_</sup> by using an Iterative deepening strategy
###### Iterative Deepening A<sup>_*_</sup> (IDA)
- Always finds an optimal solution
- Uses space linear in solution depth
- Same time complexity as A<sup>_*_</sup>
- Assuming a tree structure space, we don't have to check for cycles
- IDA<sup>_*_</sup> is as good as we can do, given an (admissible) heuristic function

### Definitions:
- __Admissible heuristic:__ the measurement never overestimates the score (distance)
   - otherwise, overestimates may cause good nodes to be skipped, because they are being ignored when they shouldn't be
   - however, if heuristics are too cautious, no useful information is provided.
- __Consistency__: for distance measurements, a consistent heuristic will give smaller values as you get closer to goal

### Admissible heuristic
- A heuristic _h(n)_ is admissible if for every node n, _h(n)_ <= _h_<sup>_*_</sup>_(n)_ where _h_<sup>_*_</sup>_(n)_ is the **true** cost to reach the goal state from n.
- __Theorem:__ If _h(n)_ is admissible, A<sup>_*_</sup> using tree-search is optimal
- Examples:
  - 8-puzzle
    1. _h<sub>1</sub>(n)_ = number of misplaced tiles
    2. _h<sub>2</sub>(n)_ = total manhatten distance

### Local search and optimization
- __Local Search:__ use single current state and move to neighboring states.
- __Advantages:__
   - Use very little memory
   - find often reasonable solutions in large or infinite state spaces.
- Are also useful for pure optimization problems
   - find best state according to some objective function

### Hill-climbing search
- Terminates when a peak is reached
- Hill climbing does not look ahead of the current state.
- Hill-climbing chooses randomly amond the best successors, if there is more than one.
- (greedy local search)
- __Problem:__ Depending on initial state, can get stuck in local maxima.
   - Ridge: sequence of local maxima difficult for greedy algorithms to navigate
   - Plateaux: an area of the state space where the evaluation function is flat
   - Gets stuck 86% of the Time

### Local beam search
- Keep track of k states instead of one

```
func beamSearch()
  initially: k random states
  next: determine all successors of k states
  if any of successors is goal
     finished
  else
     select k best from successors and repeat
```
- Major difference with random-restart search
   - information is shared among k search threads
- Can suffer form lack of diversity

## Summary
- The best search method is problem specific
