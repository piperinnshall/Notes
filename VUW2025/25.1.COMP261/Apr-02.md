# Graphs and Data structures

## Graph Algorithms

Many graph problems require searching through the graph, following edges.

- Simplest:
    - search a graph from a node, doing something to each node you reach.
- Key issue:
    - Must keep track of the nodes you have visited, so you don't visit them again.
- Key question: what order to search in?
    - Depth first search (DFS)
        - Select the first neighbor
    - Breadth first search (BFS)
        - Select the first neighbor, and the the next of the same starting node
    - Priority first search
        - Search the most promising options
        - Heavily consider the weights
        - Optimizing path from start to target node

### Recursice DFS

```DFSPseudo.java
traverseGraph(node) {
    if (!node.visited) {
        node.visit();
        node.process();
        for (neighbour : node.neighbors()) {
            if (!neighbour.visited()) {
                traverseGraph(neighbour)
            }
        }
    }
}
```

- Recording visited:
    - keep a Set of visited nodes

### Iterative

```IterativePseudo.java
traverseGraph(startNode) {
    fringe; // Collection of nodes      Stack, Queue        Dfs or Bfs
    fringe.put(startNode);

    while (!fringe.isEmpty()) {
        node = fringe.poll();
        if (!node.visited()) {
            node.visit();
            node.process();
            for(neighbor : node.neighbors()) {
                if (!neighbour.visited()) {
                    fringe.add(neighbor);
                }
            }
        }
    }
}
```

```Iterative.java
public void traverseGraph(Node start){
    Set<Node> visited = new HashSet<Node>();
    Queue<Node> fringe = new ArrayDeque<Node>(); // (or Stack, or PriorityQueue)
    fringe.offer(start);
    while (!fringe.isEmpty()){
        Node node = fringe.poll();
        if (!visited.contains(node)) {
            visited.add(node);
            process(node);
            for (Node neighbour : node.getNeighbours()){
                if (!visited.contains(neighbour)){
                    fringe.offer(neighbour);
                }
            }
        }
    }
}
```

Multiple components.

If the graph is not connected, add an array of nodes (a list of all the nodess) to see if they have been visited.

![Queue](./2-Apr-Queue.png)
