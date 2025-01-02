- Divide and Conquer is a pattern in recursive algorithms that has two defining characteristics:
- At each step, there are 2 or more recursive calls
- The problem is being reduced by some multiplicative factor at each call
- If there is only one recursive call, then it's called decrease and conquer.
- in worst case, quick sort is not divide and conquer, but it is divide and conquer in best case
- binary search not divide and c, but it is decrease and c because there is 1 recursive call. one per if else if else branch
	- if target is less than current, search left half, else search right
	- best case is O(1) so not d and c. but usually we don't care as much about the best case as the worst
### quandary2
```
public static int quandary2(int N) {
  if (N == 1) {
    return 1;
  }
  return quandary2(N/2) + quandary2(N/2);
}
```
- 2n-1 recursive calls. In O(N). we can see number of calls by counting, but also consider we do 2^k calls at level k and there are log2 of N levels (not including root so add 1 in formula below): 1 + 2 + 4 + 8 + ... + 2^(log2 of N). this is geometric series https://www.cuemath.com/geometric-sum-formula/:

```
(1*(1-2^(log2 of (N+1)))/(1-2)

(1-2*2^(log2 of N))/(-1)

-1*(1-2N) = 2N-1
```

```
q(8)
 q(4)
  q(2)
   q(1)
   q(1)
  q(2)
   q(1)
   q(1)
 q(4)
  q(2)
   q(1)
   q(1)
  q(2)
   q(1)
  q(1)
```

- there is 1 step of work each recursive call so add up how many there are (2n-1). 
- best case quicksort is NlogN because LogN levels times each level does (1/2)N +1/2 then 1/4 + 1/4 + 1/4 + 1/4 work so each level is ~1N work.
- space of quandary2 is LogN because at one time there is the recursive calls for 8,4,2, 1 remembered. 1 returns and is discarded no longer taking memory, then the next 1 happens but technically just those 4 are active at once. That is logn + 1 in O(logn)
- https://stackoverflow.com/questions/10342890/merge-sort-time-and-space-complexity
### Recurrence Relations

```
Given a recursive algorithm, if we can create a recurrence relation

T(n) = aT(n/b) + f(n)

by identifying the following:

- a > 0: how many recursive calls we made at each step?
 
- b > 1: by what multiplicative factor do we reduce the problem?
  
- f(n): how much work do we do at each recursive call?
```
### Master Theorem

```
Given a recurrence relation T(n) = aT(n/b) + O(n^k), then one of the following is true

1. If a < b^k, then T(N) ∈ Ө(n^k)
   
2. If a = b^k, then T(N) ∈ Ө((n^k)logn)
 
3. If a > b^k, then T(N) ∈ Ө(n^(log_b(a)))
```
