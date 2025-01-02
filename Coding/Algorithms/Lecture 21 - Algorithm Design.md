## Questions to ask
- Do I understand the question? Can I come up with an example for myself?
- What assumptions should I check? Are there any edge cases to keep in mind?
- What algorithms can we use directly?
- What data structures may be useful here?
- Is there a way to transform this problem into an existing problem?
- Is there a way to modify an existing algorithm to solve this problem?
- What information about the problem should I leverage?
- Is there a dumb trick I should look out for?

![[Pasted image 20241110201310.png]]

- ignore the fact he made the heap k+2 size he made a mistake but it still helps visualize what is going on. The blue part describing algorithm and purple part showing runtime is accurate though.
- `(N + (N-k))*log(K+1)`
	- N because you add to heap N times,
	- + (N-K) because we remove from heap only N-K times
		- Remember at end of algorithm we have a full K+1 size heap, we never removed those. Can then just do .peek to see top element of heap without extracting it for final answer which is O(1)
- regarding his mistake, he mentioned a "fix versus growth mindset":
	- more you believe mistakes help you learn and less you focus on "I'm dumb for not getting it right", the more likely you will grow




![[Pasted image 20241114224437.png]]

- since left/right has higher priority than up/down, we sort x coordinate last because that means it is ordered for left/right afterwards, with up/down being the tie breaker ordering for same left/right valued elements.