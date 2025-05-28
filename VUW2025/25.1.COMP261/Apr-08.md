# A* Path finding

A* search is the standard good algorithm for finding shortest paths to a goal.

Nodes on the fringe are ordered by estimated total path length through this node:

Length of path from start to this node > Same as Dijkstras

Estimate of remaining distance > new: Straight line distance

- Fringe items must have
  - node,
  - previous node or edge (for the backpointers)
  - distance to node from start (needed to compute the distance to the neighbours)
  - total estimated path length

```psuedo
FindShortestPath(start, goal):
  fringe <- PriorityQueue of <node, edge, length-to-node, estimate-total-path> ordered by estimate
  backpointers <- Map of nodes to edges
  put <start, null, 0, est(start,goal)> on the fringe
  while fringe is not empty:
      <node, edge, length-to-node,, estimate-total-path> <- remove from fringe
      if node is not visited:
        visit node
        put <node, edge> into backpointers
        if node = goal:
          return ReconstructPath(start, goal, backpointers)
        for each neigh-edge out of node to a neighbor:
          if neighbor not visited:
            length-to-neighbour <- length-to-node + neigh-edge.length
            estimate-total-path <- length-to-neighbour + est(neighbour, goal)
            add <neighbour, neigh-edge, length-to-neighbour, estimate-total-path> to fringe

```

- The path found for by A* Search is the shortest path from the start node to the goal node if the following conditions are satisfied.
  - The estimated cost to goal is an underestimate - never greater than the true cost
    - (the heuristic estimate must be "admissible")
  - When we take a node off the fringe, this must be the shortest path to that node from the start.
    - (the heuristic estimate must be "consistent" or "monotonic")
- If the estimate doesn't satisfy these conditions, the A* algorithm may break.

## Admissible heuristics for A*

