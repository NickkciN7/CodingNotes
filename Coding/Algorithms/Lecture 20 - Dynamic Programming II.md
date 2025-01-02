- Can find code for this in `homework/homework1/homework1.ts` or `lecture/Dynamic Programming/pickTree.ts` (includes recursive and Dynamic programming solutions)
- Slow recursive solution that tries all combinations
- The idea for pickTrees is to chop trees in a combination that gives most wood, but we cannot cut neighbors
```
Pick Trees (SLOW)

public static int pickTrees(int[] arr) {  
  return pickTrees(arr, 0);  
}

private static int pickTrees(int[] arr, int index) {  
  if (index >= arr.length) {  
    return 0;  
  } else {  
    int cut = arr[index] + pickTrees(arr, index + 2);  
    int dontCut = pickTrees(arr, index+1);  
    return Math.max(cut, dontCut);  
  }  
}
```

- Fast dynamic programming solution
- Remember from [[Lecture 19 - Dynamic Programming I]], 
	1. Come up with the recursive subproblem (i.e. the optimal substructure)
	2. Initialize your "table" of solutions to the subproblem
	3. Update your table from the bottom up using the subproblem
	4. Return the correct value from your table

![[Screenshot 2024-11-09 200008.png]]
![Description](https://github.com/NickkciN7/CodingNotes/blob/main/Screenshot%202024-11-09%20200008.png)
## Greedy vs. Dynamic Programming
- Both Greedy and Dynamic Programming solve optimization problems
- I.e. "find the shortest path", "find the best outfit", "find the biggest profit", etc.
- Both Greedy and Dynamic Programming require the problem to have an optimal substructure--i.e. you should be able to come up with a recursive subproblem.
- However, where Greedy can fail to produce an optimal solution, Dynamic Programming can succeed, BUT often at a cost to runtime.
- DP usually worse runtime complexity
- For optimization problems
	- First try Greedy
	- Then try Dynamic Programming
	- Naive Recursive / Exhaustive Search
		- (try every single possible combination)
## Bellman-Ford

![[Pasted image 20241109201505.png]]
![Description](https://github.com/NickkciN7/CodingNotes/blob/main/Pasted%20image%2020241109201505.png)
- dijskta fails with negative edges, because it is greedy we never update `dist[C]` after visiting `D`
- Bellman Ford accounts for negative edges and is a DP algorithm
- Bellman actually created phrase "Dynamic Programming"

![[Pasted image 20241109202013.png]]
![Description](https://github.com/NickkciN7/CodingNotes/blob/main/Pasted%20image%2020241109202013.png)
- I don't agree with what he says runtime of dijsktra is, see my notes in [[Lecture 15 - Weighted Graphs and Dijkstra's]]

- Videos assigned by teacher relating to Bellman:
	- Theory in 4-minutes: [https://www.youtube.com/watch?v=9PHkk0UavIM](https://www.youtube.com/watch?v=9PHkk0UavIM)
	- Step by step example: [https://www.youtube.com/watch?v=obWXjtg0L64](https://www.youtube.com/watch?v=obWXjtg0L64)
- According to video only need repeat v-1 times not v
	- If there are more than |V|-1  edges there is a cycle. And if you run the update one more time than |V|-1 and the dist value decreases, the cycle MUST be a negative cycle and thus we throw the error. Something to note is that even if we did the loop V times, it would work and throw the error correctly because negative cycles make this alg decrease dist in a never ended cycle, regardless of if you do it 1 or 2 more times. But if there is a positive cycle it won't affect the result since the comparison will see the cycle as increasing dist and wont update.

## Homework 8
- table from the class Piazza channel I used to make a solution (in `homework/homework8/homework8.ts`) that I assume is similar to whatever the class solution is (no longer have access to homework solutions)
- Below, `[4, 10, 2, 1]` is counts and `[3, 1, 5, 10]` is values.
- A row represents the best value combination of bars (only bars index i or less), that can fit in bag of weight column number. For example, index 1 (0 row and column are empty placeholders to make algorithm work easier, 1 is actual first bar), represents choosing bar 1 and only considering bar 1. It has weight 4 and value 3. So we set column 4 (weight 4) to 12, which is `4*3`. Next row, bar 2 of count 10, can't fit, so just copy previous row, which once again is done to make algorithm work easier (so we can add values from previous row to current bar value if the counts added together can fit in the bag). Next bar 3 with count 2 and value 5. It is the best choice for weight 2 and 3 at total value of `2*5=10`. we can say 3 also even though the weight is 2 because our algorithm allows values to represent any weight value, regardless of if it is exactly that weight. Because at the end of the day, if we want the most valuable bar we can fit, we don't care if our bag isn't reaching its max weight, if anything this would make travelling easier lol. And since we can fit bar 1 of total value 12 into weight 4, this is better than 10, and therefore 12 remains best value at weight 4. Finally the last bar: count 1, value 10, total value `1*10=10`. It is best value at weight 1, same value for weight 2, but we can combine bar 3 and 4 for total weight of 3, adding 10 and 10, to get 20 there. And this also replaces at weight 4.

 ![[Pasted image 20241126223925.png]]
 ![Description](https://github.com/NickkciN7/CodingNotes/blob/main/Pasted%20image%2020241126223925.png)
