```
algorithm dfs
  Input: undirected graph G = (V, E), int s and int t
  Output: true if there's a path from s to t; false otherwise

  visited = new boolean array of size |V|
  return dfsHelper(G, s, t, visited)

algorithm dfsHelper
  Input: undirected graph G = (V, E), int s and int t, and boolean array visited
  Output: true if there's a path from s to t; false otherwise

  visited[s] = true
  if s == t
    return true;
  for each neighbor of s, starting at the smallest labeled neighbor
    if !visited[neighbor] and dfsHelper(G, neighbor, t, visited)
      return true
  return false
```

- runtime
	- assuming getting a list of neighbors takes O(1)
	- best: O(1)
		1.  s === t, then we return right away
		2. any graph with no edges
	- worst: O(|V| + |E|)
		- given fully connected undirected graph, will look at every node once and every edge twice
	- average: O(|V| + |E|)
		- something like worst case. Most of the time a graph will have a decent amount of edges connecting the nodes
- space
	- worst: O(|V|)
		- as many recursive calls as there are nodes if the graph is a linked list like structure
	- best: O(|V|)
		- need to make that visited array that is of size |V|
- to see all nodes even disconnected ones, do
```
visited = boolean array
for each unvisited node in G
	dfsHelper(G,some node, |V|, visited)
```
- Passing |V| above meaning find node that doesn't exist because highest is |V|-1. And so it will search as far as there are edges since it only stops once it finds the node of interest.
## Properties of Graphs
- 2 pairs we care about
	- direction
		- undirected
			- Friends on fb: both
		- directed
			- followers: one way
	-  cycles
		- cyclic
		- acyclic
			- all trees are acyclic
## Directed Acyclic Graphs
- DAG
- has arrows and doesn't have cycles
- source: node with no inbound edges
- sink: node with no outbound edges
## Topological sort
- topological sort of a Directed Acyclic Graph (DAG) G = (V, E) is a linear ordering of all vertices such that if G has edge u,v then u appears before v in the ordering.
	- Think of classes you can take at college, some like calc 2 depend on you taking calc 1 first. So think of classes as nodes and the edges as connecting dependent classes.
- if contains a cycle, then no linear ordering is possible
- isn't rearranging items like other sorts, it's just shows a valid ordering of nodes
- algorithm
```
for each unvisted node u
	dfs(u)
		for each neighbor v of u
			if v unvisited, dfs(v)
		else skip v
		when done with loop (no more neighbors), add u to back of list

reverse the list
``` 



~59:40 https://www.youtube.com/watch?v=KDbAxZZfHWo&ab_channel=AndrewHuang