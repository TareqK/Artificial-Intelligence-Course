<!-- Required extensions:  mathjax -->

# Search 

## Search Terminology

- Search Tree --> Generated as the search space is traversed.(not always a tree in storage).
- Search Space --> The items we can search and the relations between them.

---

## Evaluating Searches

- Completeness --> Can we always reach the goal?
- Time complexity --> If I can reach a goal , how long did it take?
- Space complexity --> How much storage did i use?
- Optimality --> Will i always find the best solution?

---

## Acheiving Intelligence by Searching a Solution

We can solve a lot of problems by searching for the solution. For example, we can some the problem of getting the shortest path between 2 places by searching for the path. 

Searching is one of the most important stratageies to slove many issues. However, we must first **formulate the problem** then **optimize the search**.

---

### Formulating the Problem

One approach to do this is to divide the problem to 6 parts

1. State --> Each item is a state.
2. Initial State --> Where we start.
3. Actions --> How to move from state to state.
4. Goal Test --> Did i get what i want?
5. Path Cost --> how much time/space/iterations/etc did it take?
6. Solution --> The end result.


For example, the route finding problem can be devided to :

1. Locations.
2. Start location and unvisited locations.
3. Next location choice.
4. Arriving at the desired location.
5. Depends on domain, could be time, hops, etc.
6. The final route chosen.

---

## Uninformed Search

### Breadth First Search

We start from the top of the tree(the root) wanting to find some value. first, we check all the direct children of the root , and see what is connected to them, then i go one level down(from the left most to the rightmost), checking all the children of the nodes on that level, then go down another level and check the children on that one, so on, and so forth, until i find the the goal. 


- Completeness --> Yes, we can always find the goal using BFS(assuming the space is finite), so as long as it really does exist.
- Time Complexity --> b<sup>d+1</sup>, where d is the **depth(levels) of the goal**, and b is the average amount of leaves/node, called the **brahcing factor**.
- Space Complexity -->  b<sup>d+1</sup>, because we keep every generated node in memory.
- Optimality --> Yes, if the cost/step is always the same between nodes.

While it can always extract the solution, and that solution is always optimal, it is not suitable for searching large graphs.

---

### Uniform Cost First

Start from the top of the tree(the root), noting the cost of every node connected to it, then taking the least costing node in that list and searching from that, so on, and so forth, replacing costs with cheaper one, until the goal is found.

Think of it as dijkstra, but we stop as soon as we find the node we want, rather than the shortest path between all nodes and the starting node

- Completness --> Yes, if b is fininte
- Time Complexity --> much larger than b<sup>d</sup>, and just  b<sup>d</sup> if all the steps have the same cost.
- Space Complexity -->  b<sup>d</sup>.
- Optimality --> Yes.


#### BFS vs UCF

BFS is a special case of UCF search where all edges are identical and positive.  However, BFS always expands in the shallowest node, and they are both not suitable for large graphs.

---

### Depth First Search

We start from the top node, exploring each node's children down to the leaves, recursively, until the desired result is found. 

- Completness --> Failes in infinite space, or looped space, so we need to modify spaces to avoid repeated states, but complete in finite spaces.
- Time Complexity --> $O(b^m)$ , where $m$ is the maximum depth of the state space.
- Space Complexity -->  $O(bm)$, ie, linear
- Optimal --> No

### BFS vs DFS

TODO

---

### Depth Limited Search

Similar to DFS, but limited by depth. The depth limit can be inferred from the problem statement.

- Complete --> no, if goal is beyond i.
- Time --> $b^i$, where i is the depth limit
- Space --> b*i
- Optimal --> no

---

### Iterative Deeping Depth First Search

Same as DLS, but increments the search depth limit on every failed iteration. It combines the best of DFS and BFS. It is one of the best uninformed search methods, for large spaces with unknown depth.

- Complete --> yes
- Time --> $O(b^d)$
- Space --> $O(bd)$
- Optimal --> Yes, if cost is always the same.


---

### Bi-Direction Search 

Searching from two directions, from the start to the goal and from the goal to the start.

Complete-->  Yes
Time --> $b^{d/2}$ + coordination time (assuming that one algorithm costs $b^d$)
Space --> $b^{d/2}$
Optimal --> Depends on algorithm

It might not always give better performance or applicable, and coordination could be costly.
 
---

## Informed Search

While uninformed search did not contain any sort of AI, informed search contains AI that changes the behavior while running.

### Heuristics and Evaluation Function

Hueristics is any approach to problem solving, learning, or discovery that employs a practical method, not guaranteed to be optimal, perfect, logical, or rational, but instead sufficient for reaching an immediate goal.

The evaluation function $f(n)$ is a function that evaluates how close we are to our goal. It is a problem-specific function. 

The function ranks the alternatives in every possbiel branching step.


An  **admissible heuristic** never over or understates the distance to the goal, that is, it is **optimistic**.

A heuristic is called admissable if $h(n) \le h^*(n)$, where $h^*(n)$ is the true cost. 

Furthermore, if we have two admissible heuristics $h_1 , h_2$, and $h_2(n) \ge h_1(n) \forall n$, then $h_2$ is said to **dominate** $h_1$, and is better for searching, since $h_2$ will expand less nodes.

If we have $h_1, h_2 ... h_m$, and none of them dominate eachother, 
then we create a new function $h(n)=MAX(h_1(n), h_2(n) ... h_m(n))$.

The best way to find a heuristic function is by easing the restrictions on the problem. The resultant problem is called a **relaxed problem**.

---
### Greedy Best-First Search

Go to the next node that brings you closest to the goal by $f(n)$, that is to say,  $f(n) = h(n)$

- Completeness --> no, can get stuck sometimes.
- Time Complexity --> $O(b^m)$, where $m$ is the maximum depth of the search.
- Space Complexity --> $O(b^m)$
- Optimal --> No

---

### A* Search

Go to the next node that brings you closer to the goal by $f(n)$ 
that is cheapest, that is $f(n) = h(n) + g(n)$ where $g(n)$ where $g(n)$ is the cost so far and $h(n)$ is the estimated cost from $n$ to the goal

- Completeness --> Yes
- Time Complexity --> exponential
- Space Complexity --> Stores all nodes in memory
- Optimal --> Yes, if $h(n)$ is admissable.

---

### Memory Bound Heuristic Search

The idea is something similar to iterative deeping search but the cut off is based on memory rather than depth.

#### Recursive Bound Best-First Search

---

#### Simple Memory-Bounded A*

---

## Local Search 

In many problems, the path to the goal doesnt matter. The solution is the goal itself.

The idea is to keep the current state, and improve it according to an **objective function**

The benefits is that local search uses little memory and finds a reasonable solution.

### Hill Climbing Search

- Keep moving in the direction of increasing value.
- Terminates when it reaches a peak.
- Does not look beyond the immediate estimate.
- Sometimes called Local Greedy Search

However, HCS can get stuck in a local maximum rather than finding the true solution.

It is only good for certain search problems, depending on the space, and its result varies depending on the size of the step.

---

### Simulated Annealing Algorithm

- Moves randomly using a probability function, and if the situation is better, it stays. otherwise, it goes back and tries another random point.
- Terminates when it finds a reasonable solution, based on a time frame or a number of hops.

However, we are not guaranteed to contain any better solutions.

It cannot get stuck on a local maximum, and given unlimited time, it will find the best solution.

---

### Genetic Algorithm

- Inspired by natural selection in biology
- Evolves towards better solutions.
- Solutions are generated by combining two states into a single state.
- Start with $k$ randomly generated states and begin combining.
- Use a **Fitness Function** to evaluate the state. A higher value means that the solution is better. 
- Choose Parents selected by random with respect to some probabilites.
- Terminate after a certain number of generations or when a satisfactory fitness level has been reached.

An Optimal solution may not be found, But generally, the solution will get better with time.

---

## Adveserial Search Problems(Games)
Playing a game can be seen as a search problem. Multiplayer games are seen as multi-agent environments. Most games are determenistic and fully observable.


### Game Tree

#### Utility Function
A function to evaluate the board/game state and how strong the position is 

- MAX --> I want to maximize my position(The utility).
- MIN --> I want to minimize your position(The utility).

---






