# Chapter 5: Adversarial Search
### Games
- Games are a form of multi-agent environment
   - What do other agents do and how do they affect our success?
   - Cooperative vs. Competitive multi-agent
   - Competitive multi-agent environments give rise to Adversarial problems A.k.a. Games
- Why study games?
   - interesting subject of study because they are hard
   - easy to represent and agents restricted to small number of actions

### Games vs Search problems
- __Search__ - no adversary
   - solution is (heuristic) method for finding goal
   - heuristics can find optimal solution
   - Evaluation function: estimate of cost from start to goal through given node
   - Examples: path planning, scheduling activities
- __Games__ - adversary
   - Unpredictable opponent solution => solution is a __strategy__
   - Time limits -> unlikely to find goal, must approximate plan of attack
   - Evaluation function: evaluate "goodness" of game position
- Iterative methods apply here since search space is too large, thus search will be don before each move in order to select best move to be made.
- __Adversarial search algorithms:__ designed to return optimal paths, or winning strategies, through game trees, assuming that the players are adversaries(rational and self-interested)->Play to win.
- Evaluation function(static evaluation function): unlike in heuristic search where the evaluation function was a non-negative estimate of the cost from the start node to a goal and passing through the given node, here the evaluation function, can be positive for a winning or negative for a losing

### Games search
- aka __"Adversarial search":__ 2+ opponents working against each other
- __Game tree:__ a tree in which nodes denote board configurations, and branches are board transitions
   - a state based tree: configuration = state
- Most 2-player game require players taking turns
   - then levels of tree denote moves by one player followed by another, and so on
   - each transition is therefore a moves
- __Ply:__ total number of levels in tree, including root
- Note: most non-trivial game situations do no permit:
   - exhaustive search -> trees to large
   - pure goal reduction -> situations defy simple decomposition
      - i.e. difficult to convert board into simple sequence of steps
- thus __search + heuristics__ needed

### Minimax Procedure
- Game playing involves competition:
   - two players are working towards opposing goals
   - thus the search tree differs from previous examples in that transitions representing game turns are done towards opposite goals
      - __There isn't one search for a single goal__
- Static evaluation: a numeric value that represents the board quality
   - done by a static evaluator
   - basically a heuristic score
- Utility function: maps an end-game state to a score
   - essentially same as the static evaluator
- __Maximizer:__ player hoping for high/positive static evaluation scores
- __Minimizer:__ the other player wants low/negative values
- Thus the game tree consists of alternate maximizing and minimizing layers
  - each layer presumes that player desires the evaluation score most advantageous to them
- Presume that we - the computer entity- are always the MAX
- When examining a game tree, the MAX wants to obtain the highest static eval. score at each levels
   - but the MAX presumes that the opponent is intelligent, and has access to the same evaluation scores
   - hence must presume that opponent will try to prevent you from obtaining best score... and vice versa
- __Minimax procedure:__ a search strategy for game trees in which:
   1. a finite search ply level p is used: tree expanded p deep
   2. static evaluation done on all expanded leaf configurations
   3. presumption that opponent will force you to make least desirable move for yourself, and best for themself
- Idea: choose move to position with highest minimax value - best achievable payoff against best player
---
  ```
  function Minimax-Decision(state)returns actions
     v <- Max-Value(state)
     return the action in Successors(state) with value v
  ```
  ```
  function Max-Value(state) returns a utility value
     if Terminal-Test(state)
        return Utility(state)
    v <- -INFINITY
    for a,s in Successors(state) do
       v <- Max(v, Min-Value(s))
    return v
  ```
  ```
  function Min-Value(state) returns a utility values
     if Terminal-Test(state)
        return Utility(state)
     v <- INFINITY
     for a,s in Successors(state) do
        v <- Min(v,Max-Value(s))
     return v
  ```
  ---
##### Properties of minimax
- Complete: Yes
- Optimal: Yes
- Time Complexity: O(b<sup>m</sup>)
- Space Complexity: O(bm)(depth first exploration)

##### Strengths
- Presumption that opponent is at least as intelligent as you are
- Ply parameter can be played with
- Practical: search can continue while opponent is thinking

##### Short-comings
- single static evaluation score is descriptively poor
   - convenient for analytical and search purposes
   - but it's a lossy compression scheme
- Requires entire subtree of ply depth p to be generated
   - may be expensive, especially in computing moves and static evaluation scores

#### Minimax problem
- Number of games states is exponential to the number of moves.
   - __Solution:__ Do not examine every node
      - Alpha-beta pruning
        - __Alpha:__ value of best choice found so far at any choice point along the MAX path
        - __Beta:__ value of best choice found so far at any choice point along the MIN path

### Alpha-Beta pruning
- __Pruning:__ the deletion of unproductive searching in a search tree
    - normally involves ignoring the whole branches
    - Wrt search strategies, a qualitative decision about suitability in searching a particular branch is made        
- __Procedure:__
   - In concert with the minimax procedure, alpha beta prevents the unnecessary evaluation of whole branches of the search tree
   - decision to ignore a branch is based on knowing what your opponent will do if a clearly good move is available to him
- __best case:__ alpha-beta cuts exponential growth rate by 1/2

### Why is it called alpha beta?
- Alpha is the value of the best choice found so far at any choice point along the path for maxima
- if v is worse than alpha, max will avoid it and prune the branch
- Same for Beta ish

##### Properties of alpha-beta
- Advantages
   - an efficient means to determine when particular branches are not worth further consideration
   - again, presumes opponent has same heuristic information as your
- Disadvantages
   - doesn't reduce exponentiality of trees
- It does seem paradoxical that alpha beta can force the ignoring of a whole branch!
  - Why can we ignore it?
  - __Reason:__ we must presume the opponent is as intelligent as we are, and will make moves that strengthen his position and make moves that weaken us
  - --> a smart opponent will foil our brilliant moves(alpha-beta knows this)

### Heuristics and game trees
- Horizon effect: when using a finite, fixed search depth, you cannot see any deeper
   - decisions are necessarily based on limited information
   - an effect of this is that decisions can be unduly influenced by what look like outstanding moves... but if the search progressed a little further, these moves might be bad after all
   - another effect: delaying the inevitable(move bad situations beyond the "horizon")
- singular-extension heuristic: if one move appears considerably better than others, search its subtree a little deeper
   - this tries to discount superficially good moves that are really bad
- Search-until-quiescent heuristic: don't let captures)or key game configuration changes_ unduly influence choices
- tapered search: vary depth factor among nodes
   - can vary the depth factor with heuristic ranking of children
- can also use rule based decisions in controlling search
   - high level database of domain knowledge can influence search decisions
