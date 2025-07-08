# Dijkstra's Algorithm

Find a path from the start to a goal

- Assume a graph is made from physical spaces
  - each node has a location
  - each edge has the actual path length

DFS?
BFS?
Other?

## Iterative traversal

fringe is all the nodes we look at but havent traversed

- priority queue
  - remove and are are log n

Use backpointers to record path

Use a map from node to previous node

`fringe <- PriorityQueue of <node, prev, edge…> `

use backpointers to create a path

## Shortest path

Build up the path

Total length not immediate edge length

```sudo
Initialize Data Structures:
    Create a distances map: set all nodes to inf, except the start node (set to 0).
    Create a backpointers map: set all nodes to None.
    Initialize a priority queue (fringe) with (0, start_node).
While the fringe is not empty:
    Pop the node with the smallest distance from the fringe. Let’s call it current.
    If current_distance > distances[current], skip it (stale entry).
    For each neighbor of current:
        Compute new_distance = distances[current] + edge_weight.
        If new_distance < distances[neighbor]:
            Update distances[neighbor] = new_distance.
            Update backpointers[neighbor] = current.
            Push (new_distance, neighbor) onto the fringe.
End:
    When the fringe is empty, distances holds the shortest distances.
    Use backpointers to reconstruct shortest paths by walking backward from any target node to the start.
```


If you want all the shortest paths dijkstra is fastest

If not its a waste
