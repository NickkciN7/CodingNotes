- A Spanning Tree is a Tree within a connected Graph that such that every node can path to every other node. Here, a Tree is a subgraph with no cycles.
- A Minimum Spanning Tree (MST) is a Spanning Tree within a connected, weighted Graph that has the least total cost when you sum all the edge weights.
- for spanning trees on graph with |V| nodes, we have exactly  |V|-1 edges
	- if less edges, then not fully connected tree, meaning it doesn't span
	- if more edges, then we have a cycle, and therefore it is not a tree
- only considering undirected graphs
```
MST problem
Input: Weighted, undirected, connected Graph G = (V,E)
Output: Tree T = (V, E'), where E' is subset of E, that minimizes the edge weight sum  
```

## How to solve? Prim's algorithm
- what if we just started picking nodes to visit?
- each node has neighbors with cost. we know we have to visit at least one of those edges to a neighbor in order to have all nodes connected: a requirement of a spanning tree
- so each time visit a new node, just pick the least one with least cost edge
- considered a greedy algorithm
	- picking most locally optimal choice (inconsiderate of future information that would lead you to change this to be more efficient or whatever)
	- we pick the least cost edge, which is best locally optimal solution, but that doesn't mean it is the end choice as a different edge may be better overall

```
algorithm Prims  
  Input: Weighted, Undirected, connected Graph G = (V, E) with edge weights we  
  Output: A Tree T = (V, E'), with E' ⊆ E that minimizes the edge weight sum
* something to note is this pseudocode doesn't even return a tree. I think rather it should say it returns prev and cost, from which a mst could be formed

  
  for all u ∈ V :  
    cost(u) = ∞  
    prev(u) = nil  
  Pick any initial node u0  
  cost(u0) = 0

  H = makequeue(V) (priority queue, using cost-values as keys)  
  while H is not empty:  
    u = deletemin(H)  
    // edge from node u to node v
    for each {u, v} ∈ E: 
      if cost(v) > w(u, v) and H.contains(v):  
        cost(v) = w(u, v)  
        prev(v) = u  
        decreasekey(H, v)
```

- Regarding H.contains(v) (inQueue in my prim.ts code), the pseudocode provided by class did not originally have that and it was a bug. Someone called out a mistake this bug produces on Piazza:
	- "In lecture 25 (https://www.youtube.com/watch?v=4jJbh5q4j-8&ab_channel=AndrewHuang) at 27:57 it says that we don't update C because its cost is already 1.  But on the left you can see that C's cost is actually 3.  Is this a mistake?  If so, then what step should the algorithm actually take at that point?"
	- So Prim's alg should first update C, F, U costs. Then select C as it has lowest cost. Then update U and E. Select U next as it has lowest cost now (1). Look at U's neighbors and update. Of course we can update D, but what about C. Without the H.contains, we could still update it, and then we have no connection from S to U OR to C making it disconnected. We should have that H.contains so we don't overwrite an edge to C. Basically once a node has been set as being in the MST and the edge was chosen (already removed from queue), then we NEVER modify it again. This is in line with the fact Prim's is a greedy algorithm, meaning we stick with our decision that we made before.
![[Pasted image 20241126205832.png]]
- same runtime as in [[Lecture 15 - Weighted Graphs and Dijkstra's]]
- quoting the end of runtime analysis in particular
	- putting together
		- `|V|*LogV + |E|*LogV = (|V| + |E|) * LogV` 
		- should really be `|V|*LogV + |E|*|V| = |V|*(LogV + |E|)`
- can simplify for prims since we know is connected graph
	-  |E| >= |V| - 1
		- because if less, then not connected
	- |E| <= |V|^2
	- so could substitute and simplify as allowed by runtime analysis. looks prettier in wrong analysis: becomes `|E|*LogV`

## Kruskal's
- what if just started picking edges for mst?
- start with cheapest, then another, etc
- issues
	- may be disconnected
	- what if create cycle
	
```
In general:
Pick next cheapest edge that doesn't create cycle

Do until have |V| - 1 edges



Pseudocode:
sort edges increasing weight
T = {}
for e of edges
	if adding e to T doesn't form cycle
		add e to T
	else ignore e

MST = T




More descriptive (from homework 7):

algorithm kruskal(G, w)
  Input: A connected undirected graph G = (V, E) with edge weights w(u, v) for all (u,v) in E
  Output: A minimum spanning tree defined by the edges X

  for all u ∈ V:
    makeset(u)
  X = {}
  Sort the edges E by weight
  for all edges {u, v} ∈ E, in increasing order of weight:
    if find(u) != find(v):
      add edge {u, v} to X
      union(u, v)
  return X
  
algorithm makeset(x)
  Input: a graph node x
  Output: modify x such that it has a "rank" and a "parent"

  x.rank = 0
  x.parent = x

algorithm find(x)
  Input: a graph node x
  Output: the ancestor

  if x != x.parent
    x.parent = find(x.parent)
  return x.parent

algorithm union(x, y)
  Input: graph nodes x and y
  Output: modify x and y so that they are now connected in the same "set"

  x = find(x)
  y = find(y)

  if x.rank > y.rank
    y.p = x
  else
    x.p = y
    if x.rank == y.rank
      y.rank = y.rank + 1
```





- runtime
	- sort edges first ELogE
	- for loop E
		- assuming adding edge to edge list is cheap and checking cycles is cheap, overall is E
	- ELogE more expensive so it is the runtime'
	- simplify
		- E = V^2 worst case, for a fully connected graph
		- `ELogE = ELog(V^2) = E*2LogV` and in Big O it is just `O(ELogV)`

## Comparison
- Prim's
	- looks like dijkstra
	- explores nodes based on edges we can reach
	- has source node we start at
	- mst so far is always connected
- Kruskal's
	- No past algorithms we saw look like it
	- explore edges instead of nodes
	- no start node
	- mst can be disconnected and slowly become connected as the algorithm runs