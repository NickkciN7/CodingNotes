## single source shortest path
- input
	- weighted graph G = (V, E) where len(ith e) > 0 for all e in E.
		- length of each edge is greater than 0
		- G can be directed or undirected
	 - source node s in V
- output 
	- array `dist` where `dist[u]` is shortest distance between s and u for some reachable node u in V
		- dist to s is 0
		- inf is unreachable
	- array `prev` where `prev[u]` is previous node along shortest path between s and u
		- prev of s is null
		- null if unreachable
## silly approach
- george = next unvisited node closest to s based on distance
	- says first george is the source node...
- look at george's neighbors and update the dist for them if needed
- after, pick next george
- start with dist = array size |V| filled with infinity
	- then set `dist[s]` to 0
- start with dist = array size |V| filled with infinity
```
(X) is weight of edge

3 -(1)- 4  -(3)-   5
|       |
(1)    (2)
|       |
1 -(1)- 2 
\      /
(4)  (2)
  \  /
    0

1: George = no one
 dist: [inf, inf, inf, inf, inf, inf]
 prev: [null, null, null, null, null, null]
 
2: George = 1
 dist: [4*, 0*, 1*, 1*, inf, inf]
 prev: [1*, null, 1*, 1*, null, null]
 
3: George = 2 (2 and 3 both 1 away, tie breaker is the lower number so choose 2)
 dist: [3*, 0, 1, 1, 3*, inf]
 prev: [2*, null, 1, 1, 2*, null]
 
4: George = 3 (2 and 3 both 1 away, but 2 already visited so choose 3)
 dist: [3, 0, 1, 1, 2*, inf]
 prev: [2, null, 1, 1, 3*, null]

5: George = 4 
 dist: [3, 0, 1, 1, 2, 5*]
 prev: [2, null, 1, 1, 3, 4*]

6: George = 0 
 dist: [3, 0, 1, 1, 2, 5]
 prev: [2, null, 1, 1, 3, 4]
```

## How to solve with code
- intuition: breadth first search kind of works in the case where all the weights are one
- what if we accounted for the weights when we're adding to queue 
### priority queue
- It's a queue, but each thing you add to the queue has a priority key. Queue stays sorted smallest first, so that the thing with the smallest key is removed first.
- operations
	- add: add a thing to the queue, inserting in the right place based on its key    
	- deletemin: delete the next smallest priority key and returns the associated thing
	- decreaseKey: updated an existing key in the queue and re-sorts the queue
- You can build one by using the Heap we saw in Lecture 6. What you need to remember:
	- add: O(log(n))
	- deletemin: O(log(n))
	- decreaseKey
		- what it says in the lecture: O(log(n)) 
		- correct runtime: O(N)
			- Though there is the property that a parent in a minheap is smaller than children there is no guarantee about the children other than that. We therefore can not search for a value in LogN time like in a binary search tree, and will be more like N to find the element. And then bubbling up is LogN but N dominates


### Dijkstra
```
Input:
Graph G=(V,E), directed or undirected;
positive edge lengths {l of e : e in E}; vertex s in V

Output:
For all vertices u reachable from s, dist(u) is set
to the distance from s to u.

for all u in V:
	dist(u)= infinity
	prev(u) = null
dist(s)=0

H = makequeue(V) (using dist-values as keys)
while H is not empty:
	u= deletemin(H)
	// edge from node u to node v
	for all edges (u,v) in E: 
		if dist(v)>dist(u)+l(u,v):
			dist(v)=dist(u)+l(u,v)
			prev(v) = u
			decreasekey(H,v)
```

- runtime
	- `u= deletemin(H)`
		- while loop V, deleteMin logV so this is `V*LogV`
	 - makeQueue is also `V*LogV` and since we already have 1 above adding together will be `2*VLogV` and we can ignore constant factors
    - `decreasekey(H,v)`
	    - although in while loop remember that edges of a node are a subset of E, so we are not doing V (while loop) times E or times subset of E. Instead the number of steps that for loop takes over all iterations of the while loop, is just E subset 1 + E subset 2 + ....  = just E
	    - and decreasekey is LogV (according to teacher, but actually V see above)
	    - so we do `E*LogV`
	- putting together
		- `|V|*LogV + |E|*LogV = (|V| + |E|) * LogV` 
		- should really be `|V|*LogV + |E|*|V| = |V|*(LogV + |E|)`