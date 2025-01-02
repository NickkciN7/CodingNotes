- after sorting, elements in "non-decreasing" order. for example 1,1,2,3
	- 1,1 technically not increasing, so better to say non-decreasing
- *In place*: sorting algorithm uses constant space, meaning we only create constant space data structures to aid in our sorting.
- *Stable*: sorting algorithm ensures that elements of same value will be in same order after sorting
	- for example imagine you have object person with 2 values: age and name and we want to sort by age
		- [{age:20, name: "John"}, {age:20, name: "Tom"}, {age:15, name: "Sarah"}]
		- after sorting, of course age 15 object goes first, but we need to ensure that John and Tom will be in that same order to be stable
## Merge sort
- see `lecture/sorting/merge.ts`

![[Screenshot 2024-11-25 153531.png]]
![Description](https://github.com/NickkciN7/CodingNotes/blob/main/Screenshot%202024-11-25%20153531.png)
## Heap Sort
### Heap
- binary tree
	- has a value, a left, and right
- *complete* binary tree has all levels filled except the last row, which might miss some nodes on the right. 
	- binary trees can be represented as arrays. if last level doesn't start from left and has gaps, then the array will have gaps, probably why a complete tree is considered important
- height of tree is LogN.
	- binary means each node has 2 children. So each level will have 2 times the previous level. If there are N total nodes, we will run out on the Log base 2 N level
- max heap: each element is <= parent
- min heap: each element is >= parent
- doesn't matter if left or right child are bigger/smaller than each other
### Max Heap operations

```
//Time O(logn), Space O(1)
private void bubbleUp(int pos) {
	int parentPos = (pos-1)/2;
	T value = heap[pos];
	while (pos > 0 && (value.compareTo(heap[parentPos]) > 0)) {
		heap[pos] = heap[parentPos];
		pos = parentPos;
		parentPos= (parentPos-1)/2;
	}
	// note above it doesn't set a position to value until the end, as it is unecessary to set it intermediately
	heap[pos] = value;
}
```

- Add a new element
	- put at first opening in tree. compare to parent, if greater, swap (bubbling up)
	- continue same process until it meets a parent greater than itself or hits the top
	- Worst case: O(LogN)
		- if new number is largest, then do tree height swaps which is Log base 2 which is in O(LogN)
	 - Best case: O(1)
		 - new number is smaller than 1st parent
- Look at the current largest element
	- "peeking"
	- in array implementation, first number of array is largest so just return arrary[0], this is 1 step
- Remove the largest element
	- can only remove the top
	- "extract max"
	- take out top element and return it; swap last element to top; bubble down until reaches correct place
	- Worst case: O(LogN)
		- last number might need to bubble down tree height (LogN) times
	 - Best case: O(1)
		 - last number could for example come from right subtree and be 5. Left subtree is bigger so swaps down to left. If left subtree grandchild (2 levels down) are 3,4 then 5 is bigger and only made 1 swap

```
//Time O(logn), space O(1)
private void bubbleDown(int pos) {
	T item = heap[pos];
	int index;
	while (pos < length/2) {
		int left = 2*pos + 1;
		int right = 2*pos + 2;
		// left compare right < 0 means left smaller than right, see compareFn of https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort ONLY for the compare function, below is not a whole sort, but compare function is same
		if (right < length && heap[left].compareTo(heap[right])
		< 0){
			index = right;
		} else {
			index = left;
		}
		
		if (item.compareTo(heap[index]) >= 0){
			break;
		}
		
		heap[pos] = heap[index];
		pos = index;
	}
	heap[pos] = item;
}
```

- my explanation for [Why does the formula 2n + 1 find the child node in a binary heap?](https://cs.stackexchange.com/a/170115/175906)"
Not mentioned in lecture
- heapify (see code below)
	- LogN worst case, 1 best
	- if index is root, will take log n, if index is parent of leaves, will take 1
```
swap index with the larger of its 2 children and recurse where next index is original index of swapped child (now contains the previous parent)
```
- build heap
	- O(N)
		- most nodes on bottom of heap (since node count doubles per level) and these are more like O(1) time to heapify. So the majority of nodes are quick. Only the few nodes at the top will take like LogN. Since the loop is N/2 and the minHeapify is more like constant, we can say N/2 * ~constant is in O(N)
	
```
// Build heap. Math.floor(arr.length / 2) - 1 should be last index of second to last row. we don't care about last row because last row are leaves and have no children, and thus we cannot heapify them. Heapify 2nd to last row will potentially swap a element with its children in last row though.

for (let i = Math.floor(arr.length / 2) - 1; i >= 0; i--)
        heapify(arr, n, i);

// To heapify a subtree rooted with node i
// which is an index in arr[].
function heapify(arr, n, i) {
    // Initialize largest as root
    let largest = i;
    
    // left index = 2*i + 1
    let l = 2 * i + 1; 
    
    // right index = 2*i + 2
    let r = 2 * i + 2; 

    // If left child is larger than root
    if (l < n && arr[l] > arr[largest]) {
        largest = l;
    }

    // If right child is larger than largest so far
    if (r < n && arr[r] > arr[largest]) {
        largest = r;
    }

    // If largest is not root
    if (largest !== i) {
        let temp = arr[i]; // Swap
        arr[i] = arr[largest];
        arr[largest] = temp;
        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
}
```
### Heap Sort
- Selection sort definition with heap definition modifications in ( )
	- **If we repeatedly pick the next smallest (largest) element (from the heap), we can build up an answer with the elements we picked**
```
**

algorithm heapSort  
  Input: list of integers lst of size N  
  Output: lst such that its elements are in sorted order  
  
  heap = new max heap of size N  
  result = new list of size N  
  // N
  for index i = 0, 1, 2, ..., N-1  
    // LogN
    heapAdd(heap, lst[i]) 
  // N
  while heap.size() > 0  
    // addFirst O(1) heapExtractMax O(LogN)
    result.addFirst(heapExtractMax(heap))  
  return result

**
```
- So above is N*LogN + N*LogN which is in O(NLogN)
- Turns out to be runtime in best, worst, and average cases
- space is 2N which is in O(N)

## Counting sort
- Domain Utilization
	- when know something extra about a problem, use it to make algorithm faster
- If have array of nums, arr, and a number k where each element of arr is between 0 and k (inclusive), then can use k+1 size array to store counts of how often each element occurs, then make a sorted list from that
```
N = n + k
n = arr.length
k = largest number
```
- best, worst, average runtime O(N)
- space: O(N)
- bad if k is huge relative to n. like [3,1,99999]. We would need to make array of 99999 + 1 size for count, just to sort a 3 length array
## Radix sort
- apply "counting" sort to 1s place, and get sorted array
	- instead of incrementing count, count will be an array, and we append the value whose 1s place corresponds to that count array (which is always 0-9)
- Then apply counting sort the the 10s place, and get sorted array
- etc.
- At end will have a sorted array
- here k will always be 9 since numbers are 0-9 in each 10s place
```
N = d(n + k)
n = size of array
k is always 0-9 so constant, we can ignore and say n
d = largest number of places of any number, but most numbers at most have 100 places. so we can basically treat d as a constant
and we can say radix is 100(n + 9) which is in O(n)

space: O(n)
at most at one time, each 0-9 bucket will have a subset of the original numbers. In total all those arrays of all buckets will always have n items in them. And there is a k size array to hold them, but that is 9 and can be ignored. So even though there are multiple arrays, it is just in O(n)
```
