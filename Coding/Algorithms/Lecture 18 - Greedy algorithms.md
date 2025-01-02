- A greedy algorithm, as the name suggests, always makes the choice that seems to be the best at that moment. This means that it makes a locally-optimal choice in the hope that this choice will lead to a globally-optimal solution.
- In other words, in a greedy algorithm, we don't really plan and we don't really look back. We just assume picking the next "obvious" thing will lead to an optimal result.
- This approach only works for some problems, so the skill to build is recognizing when the greedy approach will work, and knowing how to pick the next "obvious" thing.

```
Example 1: Serving Customers

Say you had n customers. Customer i will take xi time to serve.

- You can only serve one customer at a time.
    
- You want to minimize the combined wait time of all customers.
    

Who do you serve first? Who do you serve after that?

Example: customers = [4, 2, 2, 6, 1]



Answer: Sort by smallest wait time first 
[(4, 1), (2, 2), (2, 3), (6, 4), (1, 5)] 
[(1, 5), (2, 2), (2, 3), (4, 1), (6, 4)] Then add the wait times
  0        1       1       1       1
           0       2       2       2
                   0       2       2
                           0       4
                                   0
                                   
  0   +    1    +   3   +  5   +   9   =   18
```

```
Example 2: Scheduling Lecture Hall

Say you want to schedule lectures for a lecture hall. Each lecture i has a start time si and a finish time fi. We want to maximize the number of lectures we can schedule in the hall (lecture can't overlap). How do you pick which lectures to schedule? Assume lectures are sorted by finish time.

Example:  
  Lecture  1  2  3  4  5  6  
  Start    1  3  0  5  8  5  
  Finish   2  4  6  7  9  9

What's the "obvious" way to pick here?


Answer: Already sorted by end times. Pick first, then select next lecture that doesn't conflict with previous, repeat

If we pick NOT the first lecture, one of two things will happen.

Either the lecture we picked will conflict with the first lecture, or it won't.

CONFLICT, one of two things will happen
- Either we'll still be able to get the same number of lectures booked OR
- The lecture we picked will force us to pick less lectures overall

DOESN'T CONFLICT -- why wouldn't we pick the first lecture here?
```

- which algorithms we have seen are greedy?
	- Dijkstra's
	- Prim's
	- Kruskal's
	- Selection sort
## When not to use greedy approach
- proving a greedy is approach is best is hard, but not as hard to say when not to use it
- 2 properties of problem need be satisfied before can use greedy
	1. Optimal substructure
		 - optimal solution to problem can be solved based on optimal solutions to subproblems
	2. Greedy property ("No regrets" or "YOLO" principle)
	     - if make choice that seems best at that moment and solve remaining sub problems later, you still reach an optimal solution. never have to reconsider earlier choices
	- if problem doesn't satisfy 1, can't use greedy at all. If doesn't satisfy 2, can use it but will end up with sub optimal solution
- if want prove shouldn't use greedy, come up with counter example

## When to use greedy
- when those 2 properties are met
- when you only need solution that is "good enough" but not optimal
	- comes up a lot in the industry
## Takeaways
- typically with greedy, we'll be sorting something first