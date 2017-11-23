# Chapter 3: Blind search

### Problem-solving agent
- Four general steps in problem solving:
   - Goal formulation
      - what are the successful world state    
   - Problem formulation
     - what actions and states to consider give the Goal
   - Search
     - Determine the possible sequence of actions that lead to the states of known values and then choosing the best sequence
   - Execute
      - Give the solution perform the actions

### Search problems
- A search problem consists of:
   - A state space
   - A successor function
   - A start state and a goal test
- A solution is a sequence of actions which transforms the start state to a goal state

- Example: vacuum world
   - states: two locations (with or without dirt)
   - initial state: any
   - Actions: {Left, Right, Suck}
   - Goal test: No dirt at all locations
   - Path cost: number of actions to reach goal

Problem Space example: chess
- Problem space:
   - states: all possible board positions
   - operators: the legal moves of chess
- Initial state: starting board positions
- Goal: set of all positions in which opponent is checkmated

### Basic search algorithms
- How do we find the solutions of previous problems?
   - Search the state space
   - Here: search through explicit tree generation
     - Initial State: root
     - Nodes and leafs generated through successor function
     - In general search generates a graph

#### Tree search algorithms
- Basic idea:
   - offline, simulated exploration of state space by generating successors of already explored states
   - Pseudocode
   ```
   function Tree-Search(problem, strategy)returns solution or nil
      //initialize the search tree using the initial state of problem
      loop do
         if (no candidates for expansion)
            then return nil
         //choose a leaf node for expansion according to strategy
         if (node contains a goal state) then
            return the corresponding solution
         else
            expand the node and add the resulting nodes to the search tree
   ```

#### Infrastructure for search algorithms
- Each node of the tree has four components:
- A state: the state in the state space to which the node corresponds
- A parent: the node in the search tree that generated this node
- Action: the action that was applied to the parent node to the generate the node
- Path Cost: cost of the path from initial state to goal state

### Search strategies
- A strategy is defined by picking the order of node expansion
- Problem-solving Performance is measured in four ways:
   - Completeness: does it always find a solution if one exists?
   - Optimality: does it always find the least cost solution?
   - Time Complexity: Number of nodes generated/expanded?
   - Space complexity: Number of nodes stored in memory during search?
- Time and space complexity are measured in terms of problem difficulty defined by:
   - b: maximum branching factor of the search tree
   - d: depth of the least cost solution
   - m: maximum depth of the state space

### Uninformed search Strategies(blind search)
- Use only information available in problem definitions

#### Summary of algorithms
|Criterion|Breadth-First|Uniform-Cost|Depth-First|Depth-Limited|Iterative Deepening|
| --- |:---:|:---:|:---:|:---:|:---:|
|Complete|Yes|Yes|No|No|Yes|
|Time|O(b<sup>d+1</sup>)|O(b<sup>⌈C<sup>*</sup>/e⌉</sup>|O(b<sup>m</sup>)|O(b<sup>l</sup>)|O(b<sup>d</sup>)|
|Time|O(b<sup>d+1</sup>)|O(b<sup>⌈C<sup>*</sup>/e⌉</sup>|O(bm)|O(bl)|O(bd)|
|Optimal |Yes|Yes|No|No|Yes|

## Summary
- Problem formulation usually requires abstracting away real-world details to define a state space that can feasibly be explored
- variety of uninformed search strategies
- Iterative deepening search uses only linear space and not much more time than other uninformed algorithms
