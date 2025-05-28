# Graphs and Data Structures

## Graph

- A collection of nodes and edges
  - Entities and relationships between them
- Many real world applications
  - Places with connetions
    - Airports
      - Airports are nodes and flights are edges
    - Intersections
    - Roads
    - Railways
- Entities and relationships between them
  - Social network
    - Person node, relationship edge

## Different kinds of graphs

- Undirected vs directed:
  - Are the edges symmetric or one-way (digraph)

digraph's have arrows ->

- Single or multi-graph:
  - Can there be 2+ edges between a pair of nodes?
  - Multidigraphs have the same source+target node

- Sparse graphs
  - most pairs of nodes not connected
    - |edges| << |nodes|^2
- Dense graphs
  - nodes connected to most other nodes
    - |edges| ~= |nodes|^2

- Do the edges have information attached?
  - Weights
  - Lengths
  - Labels

- Bipartite graphs
   - Two kinds of nodes
   - Edges between types
   - e.g. supervisors and projects

Is the graph known or is it constructed as you traverse it? (implicit graph)

Focusing on undirected, directed, single, multi, edge information

## Graph as a data structure

What data structure should be used to represent a graph?

- A good data structure should support the important operations efficiently
  - Find all nodes of the graph
  - Find all edges of the graph
  - Find all outgoing edges of a node
  - Find all incoming edges of a node
  - Find all outgoing neighbors of a node
  - Find all incoming neighbors of a node
  - Find out whether two nods are directly connected or not

- Two traditional data structures
  - Adjacency matrix
  - Adjecency list

- Object based
  - Collection of node objects with lists of neighbors
  - Collections of edge objects with pairs of nodes

Big O notation - how fast is the graph

## Data representations

- Adjacency Matrix
  - Use integers 0..n-1 to represent nodes
  - Use an array to represent info about nodes
    - private Node[] nodes;
  - Use a 2d matrix to represent the graph
    - private int[][] edges
    - Number of rows and columns = number of nodes
    - M(ij) = 1 if there is an edge from node i to node j
    - M(ij) = 0 blank otherwise


`nodes[]`
0 1 2 3
A B C D

`edges[row(y)][col(x)]`
  y
x - 0 1 2 3
  0       1
  1 1     1
  2
  3 1   1

A -> D
B -> A, D
C -> _
D -> A, C

A <- B, D
B <- _
C <- D
D <- A, B

row(y) = outgoing
col(x) = incoming

There's no spatial information to draw the class unless the node has a data field.

- What about edges with lablels?
  - Instead of 0 and 1 for the edges use 0,1,2,3,4,5 to store extra information
- Cannot deal with multi-graphs

### Time complexity

Assume simple graph: at most one edge between each pair of nodes, with N nodes and E edges, typically N < E < N^2

2D adjacency matrix, requires O(N^2) memory

- Time code
  - Find all nodes of the graph                   -> O(N)
  - Find all edges of the graph                   -> O(N^2)
  - Find all outgoing edges of a node             -> O(N)     ROW
  - Find all incoming edges of a node             -> O(N)     COL
  - Find all outgoing neighbors of a node         -> O(N)     ROW
  - Find all incoming neighbors of a node         -> O(N)     COL
  - Check if there is an edge between 2 nodes     -> O(1)
