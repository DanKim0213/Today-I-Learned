# Prim's Minimum Spanning Tree Algorithm

## What is a Minimum Spanning Tree?
- Given an undirected graph with weighted edges,
- a **Minimum Spanning Tree** (MST) is a subset of the edges in the graph which connects all vertices together 
- (without creating any cycles) 
- while minimizing the total edge cost.

!(MST)[https://miro.medium.com/max/920/1*WXDyVZ-nJTjfY4BeF6hmTg.png]

## Prim's MST Algorithm Overview
- A greedy Algorithm.
- It works well on dense graphs.
- However, when it comes to finding the **minimum spanning forest** on a disconnected graph, Prim's cannot do this as easily.
- O(E*log(E))

## Lazy Prim's MST Implementation
- 
```java
n = ... # number of nodes in the graph
pq = ... # Priority Queue which stores edge objects consisting of {start, end, edge cost}
g = ... # graph representing an adjacency list of weighted edges; for dense graph, an adjacency matrix is more preferable.  
visited = [false, ..., false] # size n

function lazyPrims(s = 0):
  m = n - 1 # num of edges in MST
  edgeCount, mstCost = 0, 0
  mstEdges = [null, ..., null] # size m
  addEdges(s)

  while (!pq.isEmpty() and edgeCount != m):
    edge = pq.dequeue()
    nodeIndex = edge.to

    if visited[nodeIndex]: continue

    mstEdges[edgeCount++] = edge
    mstCost += edge.cost

    addEdges(nodeIndex)

  if edgeCount != m:
    return (null, null) # No MST exists!
  
  return (mstCost, mstEdges)

function addEdges(nodeIndex):
  # Mark the current node as visited
  visited[nodeIndex] = true

  # Iterate over all edges going outwards from the current node.
  # Add edges to the PQ which point to unvisited nodes.
  edges = g[nodeIndex]
  for (edge : edges):
    if !visited[edge.to]:
      pq.enqueue(edge)
```


1. Maintain a min Priority Queue (PQ) that sorts edges based on min edge code. - This will be used to determine the next node to visit and the edge used to get there.
2. Start the algorithm on any node s. Mark node s as visited and iterate over all edges of s, adding them to the PQ.
3. While the PQ is not empty and a MST has not been formed, dequeue the next cheapest edge from the PQ. - If the dequeued edge is outdated (meaning the node it points to has already been visited) then skip it and poll again. Otherwise, mark the current node as visited and add the selected edge to the MST.
4. Iterate over the new current node's edges and add all its edges to the PQ. - Do not add edges to the PQ which point to already visited nodes. 

