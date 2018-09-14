# Search 

## Search Terminology

- Search Tree --> Generated as the search space is traversed.(not always a tree in storage)
- Search Space --> The items we can search and the relations between them

---

## Evaluating Searche

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

## Inromed Search