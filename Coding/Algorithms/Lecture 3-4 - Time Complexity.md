- Big O
	- O(g)
	- upper bound
	- if something is in O(g) it takes no longer than g
	- **f ∈ O(g)**?
		- **We have to make f(n) ≤ k · g(n) as n → ∞ true by picking a k**
	- technically correct to say that if something is in O(N), it is also in O(N^2), since if N is greater than f for any k, N^2 must also be greater. But we tend to choose the most limiting one, as it gives more valuable insight into the algorithm's efficiency.
	- **The following runtimes are from most efficient to least efficient. Indicate any complexities that are equivalent (i.e. O(x) = O(y)).**
		- https://docs.google.com/document/d/1reR6E1ml0-UnFjpv5p7lzAmgrIC5xcRNBJ_0xcXGHXE/edit
		- O(c), where c is a constant. = O(1)                    
		- O(log n)                                                  
		- O(n) = O(n log c), where c is a constant.
		- O(n log n)                                                  
		- O(n^c), where c is a constant.                     
		- O(c^n), where c is a constant.                
		- O(n!)                                                          
		- O(n^n)
 - Omega
	 - omega(g)
	 - g is lower bound of f
	 - takes at least as long as f
	 - if f in omega(g) we can say g ≤ k · f as n → ∞
		 - basically reversing function order and doing big O
- Theta
	- theta(g)
	- tight bound
	- takes at least as long and no longer than f
	- if you used theta, keep in mind this means that under any circumstance (even favorable ones where it returns in like O(1)), it will always be doing whatever time complexity g is. Meaning if it can be O(1) in best case but O(N) in worst case, then it is not in theta(N)
	- "However, there is a broader reason that people informally use O (instead of theta). At a human level, it's a pain to always make two-sided statements when the converse side is "obvious" from context."
		- https://stackoverflow.com/a/3230535/10398996
- example
```
function printPairs(arr: number[])
	for(i = 0...){
		for(j = i+1...){
			console.log(arr[i] + " " + arr[j])
		}
	}
```
- n = arr.length
- outer for loop goes n times
- inner goes n-1 first time n-2
- steps for first outer iteration is n times the inner which is n-1 etc.
- n-1 + n-2 + n-3 ... + 1 ~= (n-1)n + (-1 + -2 + -3...) = n^2 +... can ignore lower degree
- also just summing 1 to n and there is well known formula S = (n(n+1))/2 which is in O(n^2)
	- https://omerseyfeddinkoc.medium.com/the-proof-behind-the-sum-of-the-first-n-natural-numbers-8559ebfb8346
```
// assume arr is a array of positive integer
public static void rollingCounts(int[] arr) {
  for (int i = 0; i < arr.length; i++) {
    for (int j = 0; j < arr[i]; j++) {
      System.out.println(j);
    }
  }
}
```
- inner loop determined by size of `arr[i]`
- N = sum of all values in arr
- or N times average size of val. N*(arr[0] + arr[1] + ...)/N = sum also since N cancels out
- each inner does the j++ and comparison of j<arr[i] and print is 1 so 3 steps time those N times gives ~3N and that is in O(N)
- N not always the input size. Here it would be inaccurate to say the size is the only factor when the size of individual elements affect it so this time we included the size of individual elements in our definition of N
```
public static void silly(int z) {
   if (z <= 0) {
     System.out.println("Done!");
     return;
   }
   System.out.println("Not Done!");
   silly(z/2);
 }
```
- divide by 2 until x/2 less than 1 and since int are whole number a decimal becomes 0 then it ends
- this essentially is asking how many times does 2 go into z which is log base 2 of z. change of base formula allows conversion between bases and shows that really any base will be a constant multiple of another. It is standard to say something is in O(logz) where log is the standard 10 base since we can get rid of constant multiples in time complexity analysis
- in typescript a number type can be a decimal though so wouldn't quite work the same. would need to alter the base case to be z < 1
### twoSumSlow
```
public static int[] twoSumSlow(int[] arr, int target) {
  for (int i = 0; i < arr.length; i++) {
    for (int j = i+1; j < arr.length; j++) {
      if (arr[i] + arr[j] == target) {
        return new int[] {i, j};
      }
    }
  }
  return new int[] {-1, -1}
}
```
- below is best case analysis
	- big-O, omega, theta are not limited to only 1 of best,average,worst case analyses
- in O(N^2)
	- n-1 inner for loop first iteration of outer. then n-2...
	- basically 1 + 2 + ... + n-1 and sum formula from 1 to n is (n(n+1))/2 which is in O(n^2)
- But is it in omega(N^2)?
	- no because best case of twoSumSlow is in O(1), when the first 2 numbers added equal target.
	- remember "is twoSum in omega(n^2)" means that n^2 (g in this case) takes no longer than twoSum, but that is not true because n^2 takes longer that 1.