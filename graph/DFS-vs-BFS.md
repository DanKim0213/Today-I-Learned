# When is it practical to use Depth-First Search (DFS) VS. Breadth-First Search (BFS)? 

## Overview
That heavily depends on the structure of the search tree and the number and location of solutions (aka searched-for items).

- If you know a solution is not far from the root of the tree, a breadth first search (BFS) might be better.
- If the tree is very deep and solutions are rare, depth first search (DFS) might take an extremely long time, but BFS could be faster.
- If the tree is very wide, a BFS might need too much memory, so it might be completely impractical.
- If solutions are **frequent but located deep** in the tree, BFS could be impractical.
- If the search tree is very deep you will need to **restrict the search depth for depth first search (DFS)**, anyway (for example with iterative deepening).

## DFS 
assuming the depth is manageable
- Simulations of games (You can decide what to do by seeing which move leads to the best outcome)
- Finding **any** family member who is still alive, given a family tree (solutions are frequent. However, it would take the same amount of time if you need to find all family members who are still alive)
- Searching for people who have completely different interests of a specified person

## BFS 
assuming the branching factor is manageable
- peer to peer networks like BitTorrent
- GPS systems to find nearby locations
- SNS to find people in the specified distance
- Finding a family member who died a very long time ago
- SNS to find people who have similar interests of a specific person

## Reference
  - [here](https://stackoverflow.com/questions/3332947/when-is-it-practical-to-use-depth-first-search-dfs-vs-breadth-first-search-bf) 
