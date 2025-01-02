- Technique for writing algorithms on optimization problems. Optimization problems ask you to find the "best" solution (i.e. the shortest path in a graph, the longest increasing subsequence, the total (i.e. max) number of paths, etc.)
- You can solve a problem with Dynamic Programming when you identify its optimal substructure--a recursive expression of the optimal solution given the optimal solution to the smaller subproblems.
- Dynamic Programming produces an efficient solution when there's overlapping subproblems in the tree recursive solution.
## How to use Dynamic Programming

- Essentially, you'll want to first think about the "top-down" recursive solution, and then figure out how to translate that to a "bottom-up" iterative solution. The general steps are as follows:
	1. Come up with the recursive subproblem (i.e. the optimal substructure)
	2. Initialize your "table" of solutions to the subproblem
	3. Update your table from the bottom up using the subproblem
	4. Return the correct value from your table
```
Recursive:
**
algorithm countPaths  
  input: positive integer n -- number of steps on  
    a staircase  
  output: the number of paths you could take down  
    the staircase by either going down one step or  
    two steps at a time

  if n < 0  
    return 0:  
  if n == 0:  
    return 1

  return countPaths(n-1) + countPaths(n-2)
**

Iterative:
**
algorithm countPaths  
  input: positive integer n -- number of steps on  
    a staircase  
  output: the number of paths you could take down  
    the staircase by either going down one step or  
    two steps at a time

  prev = 0  
  curr = 1  
  for i = 1, 2, 3, .., n  
    temp = prev  
    prev = curr  
    curr = temp + curr  
  return curr
**
```
- Relating the 4 steps mentioned above to the recursive and iterative algorithms for `countPaths`
1. `countPaths(n) = countPaths(n-2) + countPaths(n-1)` from recursive
   `curr = temp (remember temp=prev above) + curr`  from iterative
    - like making use of a table (an array), but we don't use an array in the algorithm above. the 2 variables `prev` and `curr` replace an actual array for example like `curr[i] = curr[i-2] + curr[i-1]`, but the solution could had been implemented using an array. single dimensional arrays don't provoke much imagery of tables, but some problems require 2d arrays like `number[][]` which are more like a table, as there are rows and columns. So basically your "table" just needs to keep track of steps we can build upon
- countPaths = curr = the # of paths possible with # steps in my staircase
2. table
```
prev = 0  
curr = 1  
```
3. update table
```
for i = 1, 2, 3, .., n  
    temp = prev  
    prev = curr  
    curr = temp + curr 
```
4. return correct value from table
```
return curr
```

## Longest Increasing Subsequence

```
Input: array of integers arr of size N > 0

Output: length of the longest increasing subsequence within the array

Subsequence: pick numbers within the array in order--you're allowed to skip some

Example: [5, 2, 8, 6, 3, 6, 9, 7] → 4  
  (longest subsequence is [2, 3, 6, 9])

```


```
Question: how do we solve this?

1: Base cases: What are the simplest inputs that we'll
immediately know the answer for?

longIncSub([]) = 0
longIncSub([1]) = 1

2: Recursive Step:

longIncSub([5, 2, 8, 6, 3, 6, 9, 7])
find the longest possible subsequence starting at 5
longIncSubHelper([5, 2, 8, 6, 3, 6, 9, 7], 5) => 3
compare it to
longIncSub([2, 8, 6, 3, 6, 9, 7]) => 4

3: Combination: max(^ stuff above)

This is probably going to be expensive, probably O(2^n)
if we're bad at optimizing.
```


- above is complicated, let's turn this into a graph (directed acyclic graph) problem
	- nodes: numbers
	- edges: if node A comes before B and A < B
	- all dynamic programming problems can be formulated as a directed acyclic graph
- Find the longest path from all sources to sinks. The longest of these will be the longest increasing subsequence. Return it's length.

- Non graph, dynamic programming Solution:

![[Pasted image 20241109144259.png]]
