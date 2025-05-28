# Adjacency List

The big problem with matrices is theres a lot of empty space

- Use itn 0..n-1 to represent nodes
  - an array to represent info about nodes
  - `private Node[] nodes`

- Use an array of arrays to represent the graph
  - `private int[][] neighbours`
  - `private List<Integer>[] neighbors`

- What about extra information?
  - Lists could store edge objects containing:
    - Nodes at each end
    - Length/capacity/labels on edges

dynamic size

## Time Complexity

Assume simple graph: at most one edge between each pair of nodes, with N nodes and E edges, typically N < E < N^2

- Row i : a list of node neighbours of node i
- Maximum degree of a graph: Delta (max number of neighbours)

- Find all nodes                              -> O(N)
- Find all edges                              -> O(E)
- Find all edges of a node                    -> O(Delta)
- Check if there is an edge between 2 nodes   -> O(Delta)

# Adjacency List Directed Graph

- Use itn 0..n-1 to represent nodes
  - an array to represent info about nodes
  - `private Node[] nodes`

- Use an array of arrays to represent the graph
  - `private int[][] outNeighbours`
  - `private List<Integer>[] outNeighbors`
  - `private List<Edge>[] outEdges`

- in-degree counts the incoming edges for each node in the graph.
- out-degree tells you how many outgoing edges there are from each node in a directed graph.
- If graph has a maximum in-degree and/or out-degree
  - Delta in Delta out, Delta = (Delta in + Delta out) = maximum degree

> 0 -> [1,7,8]
> 1 -> [2,6]
> 2 -> [3,9]
> 3 -> [4,9]
> 4 -> [5]
> 5 -> [6,9]
> 6 -> [7,8]
> 7 -> []
> 8 -> [1,2,4,9]
> 9 -> [6,7]

- Find all nodes                              -> O(N)
- Find all edges                              -> O(E)
- Find all outgoing edges of a node           -> O(Delta out)
- Find all incoming edges of a node           -> O(E)
- Find all outgoing node neighbors            -> O(Delta out)
- Find all outgoing node neighbors            -> O(E)
- Check if there is an edge between 2 nodes   -> O(Delta out)

Store 2 lists, outEdges and inEdges

- Worse case complexity of finding edge/node neighbours in O(N), if the graph is fully connected
- In practice, this complexity is much smaller
- Node degree: the number of outgoing/incomingt edges of a node
- Max degree of a graph: the maximal number of neighbours of the nodes in the graph
  - An intersection connects at most 4 streets, delta/degree = 4
- Complexity of finding all outgoing/incoming neighbors
  - O(Delta) < O(N)
  - almost O(1)

# Edge List

- Array of edges

```
edge list
      0123
      ----
to    0203
from  3201
len   3572
```

- Slow for almost everything
  - Except finding the next shortest edge
  - Sort then pop


edge list cost is usually O(E)

# Object oriented approach

Forget arrays

Dont use integers to represent nodes

Big linked structure of objects

Collections can be Lists or Sets

- Nodes
  - Graph has a collection of nodes
    - `private Collection<Node> allNodes;`
  - And maybe a collection of edges
    - `private Collection<Edge> allEdges;`
- Edges
  - Nodes contain a collection of Edges
    - `private Collection<Edge> edges;`
  - Or two if directed graph
    - `private Collection<Edge> outgoing;`
    - `private Collection<Edge> incoming;`

Graph could contain a HashMap from  pairs of Nodes to Edges
