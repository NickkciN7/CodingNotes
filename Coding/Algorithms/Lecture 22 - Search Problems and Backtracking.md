- min vertex cover, set of nodes with minimum size that touch all edges
	- min spanning tree relates to edges touching all nodes
- make power set https://www.geeksforgeeks.org/power-set/
	- basically makes use of fact a binary number could represent on/off for indexes of an array. Like 101, means choose a and c from `[a, b, c]`. 000 up to 111 will represent every possible combination of "on" and "off". And based on this can construct all subsets in the power set.

![[Pasted image 20241123172459.png]]
![Description]([Pasted image 20241123172459.png)
- constraint satisfaction problem
	- problems that have requirements
	- example
		- sudoku
		- map coloring
			- all countries touching have different colors
		- n queens
### n queens
- place n queens on board that could not attach another based on rules of chess
- when notice the solution you are building cannot work,  "backtrack"/undo

![[Pasted image 20241123173544.png]]
