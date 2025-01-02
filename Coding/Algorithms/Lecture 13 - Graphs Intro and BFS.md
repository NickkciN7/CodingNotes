- Graphs have vertices and edges
- vertex is a node with edges (lines/arrows between) to other nodes
- if 2 vertices are connected by edge they are neighbors and adjacent to each other
- G =(V,E)
	- Graph G has a set of Vertices V and a set of Edges E
	- for example if you V = {0,1,2}, E could be {(0,1), (0,2)} which is like an L shape where 0 touches both but 1 and 2 don't touch. (in this case treat them like they are bi-directional, but there are such things as directional graphs we will talk about later, and in that case treat 0,1 like there an arrow from 0 to 1 but not 1 to 0)
	- graphs don't need to have edges
- The two most common representations of Graphs are as follows:
	- Adjacency Matrix -- 2D array (table) where the indices (rows and columns) represent nodes, and each in `graph[i][j] = 1`  represents an edge (0 means there is no edge)
		- space is O(|V|^2)
		- in java adding new element is O(N^2) because need to make new 2d array and copy old values. I think in ts you can just push new values to the arrays so I think that would be O(N)
		- determining if x,y neighbors? O(1):
	- Adjacency List -- A list of lists of integers, where each list at index i represents all the neighbors for a vertex i.
		- space is O(|V| + |E|)
		- adding new is O(1) assuming we have pointer to tail of list handy and it is just empty with no edges
		- determining if x,y neighbors? O(N): N to get to first number of the 2 shown, and N if for example y is at the end of it's neighbor list
## Breadth first traversal
- consider we must handle loops and disconnected nodes
- basically (doesn't deal with disconnected nodes yet, they just won't be traversed)
```
  algorithm bfs
    Input: undirected graph G = (V,E), int s and int t
    Output: true if there's a path from s to t; false otherwise

    fringe = Queue of integers
    visited = new boolean array of size |V|
    fringe.add(s)
    visited[s] = true
    while fringe.size() > 0
      currNode = fringe.remove()
      if currNode == t
        return true
      for each neighbor of currNode, starting at the smallest labeled neighbor
        if !visited[neighbor]
          visited[neighbor] = true
          fringe.add(neighbor)
    return false
```
