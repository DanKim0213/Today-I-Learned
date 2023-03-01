# Overview

## Canonical Examples

- Sets of Clothing  
![topsort algorithm](https://inginious.org/course/competitive-programming/graphs-toposort/topo.png)
Given the constraints above, how many different sets of clothing can I make by choosing an article from each category?
- Social Network
  - How many friends does person X have?
  - How many degrees of separation are there between person X and person Y?

## Types of Graph

- Undirected Graph
  - An undirected graph is a graph in which edges have no orientation. The edge (u, v) is identical to the edge (v, u). For example, roads.
- Directed Graph
  - A directed graph or digraph is a graph in which edges have orientations. For example, buying friends a gift.
- Weighted Graphs
  - Many graphs can have edges that contain a certain weight to represent an arbitrary value such as cost, distance, quantity, or etc.
- Tree
  - A tree is an undirected graph with no cycles. Equivalently it is a connected graph with N nodes and N-1 edges.
- Rooted Trees
  - A rooted tree is a tree with a designated root node where every edge either points away from or towards the root node.
  - An arborescence tree (out-tree) VS. An anti-aborescence tree (in-tree).
- Directed Acyclic Graphs (DAGs)
  - DAGs are directed graphs with no cycles. These graphs play an important role in representing structures with dependencies.
  - All out-trees are DAGs but not all DAGs are out-trees.
- Bipartite Graph
  - A bipartite graph is one whose vertices can be split into two independent group U, V such that every edge connects between U and V.
  - For example, how many people can be matched to jobs?
- Complete Graphs
  - A complete graph is one where there is a unique edge between every pair of nodes.
  - Complete graphs are often seen as a worst case you can possibly encounter. Thus, you can use it for performance test.

## Representing Graphs

- Adjacency Matrix
  - ![Adjacency Matrix](https://www.researchgate.net/profile/Janet_Prichard/publication/239491573/figure/fig2/AS:669390177591317@1536606463620/a-A-directed-graph-and-b-its-adjacency-matrix.ppm)
  - Space efficient for representing dense graphs, but it requires O(V^2) space (i.e. iterating over all edges takes O(V^2) time).
- Adjacency List
  - ![Adjacency List](https://www.researchgate.net/profile/Janet_Prichard/publication/239491573/figure/fig3/AS:669390177566727@1536606463912/a-A-directed-graph-and-b-its-adjacency-list.ppm)
  - A graph as a map from nodes to lists of edges.
  - Space efficient for representing sparse graphs (i.e. iterating over all edges is efficient), but edge weight lookup is O(E).
- Edge List
  - [ (C, A, 4), (A, C, 1), (B, C, 6) ]
  - A graph simply as an unordered list of edges.
  - This representation is seldomly used because of its lack of structure.

## Common Graph Theory Problems

- For the upcoming problems, ask yourself:
  - Is the graph directed or undirected?
  - Are the edges of the graph weighted?
  - Is the graph I will encounter likely to be sparse or dense with edges?
  - Should I use an adjacency matrix, adjacency list, an edge list or other structure to represent the graph efficiently?
- Shortest Path Problem
  - Find the shortest path of edges from node A to node B.
  - Algorithms: BFS (unweighted graph), Dijkstra's, Bellman-Ford, Floyd, etc
- Connectivity
  - Does these exist a path between node A and node B?
  - Algorithms: Union-find data structure, DFS.
- Negative cycles
  - Does my weighted digraph have any negative cycles? If so, where? (e.g. trading currencies across exchange)
  - Algorithms: Bellman-Ford and Floyd-Warshall.
- Strongly Connected Components
  - Strongly Connected Components (SCCs) can be thought of as **self-contained cycles** within **a directed graph** where every vertext in a given cycle can reach every other vertex in the same cycle.
  - Algorithms: Tarjan's and Kosarajn's
- Traveling Salesman Problem
  - "Given a list of cities and the distances between each pair of cities, what is the shortest possible route that visits each city exactly once and returns to the origin?"
  - Algorithms: Held-Karp (Dynamic Programming), branch and bound and many approximation algorithms.
  - The TSP problem is NP-Hard meaning it's a very computationally challenging problem. This is unfortunate because the TSP has several very important applications.
- Minimum Spanning Tree (MST)
  - A MST is a subset of the edges of a connected, edge-weighted graph that connects all the vertices together, without any cycles and with the minimum possible total edge weight.
  - Algorithms: Kruskal's and Prim's.
  - Applications: Designing a least cost network, circuit design, trasportation networks, and etc.
- Network Flow: max flow
  - Q: With an infinite input source how much "flow" can we push through the network?
  - Algorithms: Ford-Fulkerson, Edmonds-Karp & Dinic's.
  