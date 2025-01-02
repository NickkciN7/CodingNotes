- All nodes to the left of the current node have values smaller than or equal to it
	- *even descendants beyond immediate children*
- All nodes to the right of the current node have values larger than it
- We call this the BST property.
- useful because algorithms quick to find if node exists
- 3 operations we care about
	- searching: is integer x in the binary search tree
		- if x less than current go left, else go right
	- adding
		- same as above but look for empty spot
	- removing
		- search for x in tree and call found node v
		- if v is null, x not in tree, return
		- v is leaf, just delete it from its parent
		- if v has 1 child bypass it
		- if 2 children need successor which is next largest node
			- meaning if have below tree and remove the root 8, it chooses 9 as a successor since it is the next largest
			- something to note is that you can't ever have a successor with 2 children, because then the left child would be smaller than the would be successor (and larger than the removed node), and therefore a more suitable successor as it is closer to being the "next largest node"
	
```
       8
    /       \
    3          12
             /   \ 
           11    15
         /
        9
```



- have to be careful to maintain bst property when doing operations
- flaw: adding does not guarantee it will stay as a bst. could become a list like structure then there i no LogN operations advantage like with trees
## AVL tree
- type of self balancing bst
- guarantees O(logN) operations
- height
	- null: -1
	- leaf: 0
	- otherwise 1 + max( height(left), height(right) )
- height balanced property
	- for every node, height(left) - height(right) must not be greater than 1