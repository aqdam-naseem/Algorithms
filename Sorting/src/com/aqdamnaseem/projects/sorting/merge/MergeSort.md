# Merge Sort

Merge Sort is a kind of Divide and Conquer algorithm in computer programrming. It is one of the most popular sorting algorithms and a great way to develop confidence in building recursive algorithms.

<p align="center">
<img src="https://github.com/AqdamNaseem/Algorithms/blob/master/Sorting/src/com/aqdamnaseem/projects/sorting/merge/images/MergeSort_3.png"></p>

### Divide and Conquer Strategy
Using the Divide and Conquer technique, we divide a problem into subproblems. When the solution to each subproblem is ready, we 'combine' the results from the subproblems to solve the main problem.

Suppose we had to sort an array A. A subproblem would be to sort a sub-section of this array starting at index p and ending at index r, denoted as A[p..r].

### Divide
 
If q is the half-way point between p and r, then we can split the subarray A[p..r] into two arrays A[p..q] and A[q+1, r].
 
### Conquer
 
In the conquer step, we try to sort both the subarrays A[p..q] and A[q+1, r]. If we haven't yet reached the base case, we again divide both these subarrays and try to sort them.
 
### Combine
 
When the conquer step reaches the base step and we get two sorted subarrays A[p..q] and A[q+1, r] for array A[p..r], we combine the results by creating a sorted array A[p..r] from two sorted subarrays A[p..q] and A[q+1, r]

The __MergeSort__ function repeatedly divides the array into two halves until we reach a stage where we try to perform MergeSort on a subarray of size 1 i.e. p == r.
 
After that, the merge function comes into play and combines the sorted arrays into larger arrays until the whole array is merged.

  mergeSort(A, p, r)
      If p > r 
          return;
      q = (p+r)/2;
      mergeSort(A, p, q)
      mergeSort(A, q+1, r)
      merge(A, p, q, r)
      
      
To sort an entire array, we need to call MergeSort(A, 0, length(A)-1).

As shown in the image below, the merge sort algorithm recursively divides the array into halves until we reach the base case of array with 1 element. After that, the merge function picks up the sorted sub-arrays and merges them to gradually sort the entire array.

<p align="center">
<img src="https://github.com/AqdamNaseem/Algorithms/blob/master/Sorting/src/com/aqdamnaseem/projects/sorting/merge/images/MergeSort_2.png">
 </p>


### The merge step of merge sort

Every recursive algorithm is dependent on a base case and the ability to combine the results from base cases. Merge sort is no different. The most important part of the merge sort algorithm is, you guessed it, the "merge" step.

The merge step is the solution to the simple problem of merging two sorted lists(arrays) to build one large sorted list(array).

The algorithm maintains three pointers, one for each of the two arrays and one for maintaining the current index of final sorted array.

Have we reached the end of any of the arrays?
    No:
        Compare current elements of both arrays 
        Copy smaller element into sorted array
        Move pointer of element containing smaller element
    Yes:
        Copy all remaining elements of non-empty array

<p align="center">
<img src="https://github.com/AqdamNaseem/Algorithms/blob/master/Sorting/src/com/aqdamnaseem/projects/sorting/merge/images/MergeSort_1.png">
 </p>
 
 ### Implementation
 

	void merge_sort(int A[], int start, int end) {
		if (start < end) {
			int mid = (start + end) / 2; // defines the current array in 2 parts
											// .
			merge_sort(A, start, mid); // sort the 1st part of array .
			merge_sort(A, mid + 1, end); // sort the 2nd part of array.

			// merge the both parts by comparing elements of both the parts.
			merge(A, start, mid, end);
		}
	}

	void merge(int A[], int start, int mid, int end) {
		// stores the starting position of both parts in temporary variables.
		int p = start, q = mid + 1;

		int[] Arr = new int[end - start + 1];
		int k = 0;

		for (int i = start; i <= end; i++) {
			if (p > mid) // checks if first part comes to an end or not .
				Arr[k++] = A[q++];

			else if (q > end) // checks if second part comes to an end or not
				Arr[k++] = A[p++];

			else if (A[p] < A[q]) // checks which part has smaller element.
				Arr[k++] = A[p++];

			else
				Arr[k++] = A[q++];
		}
		for (int j = 0; j < k; j++) {
			/*
			 * Now the real array has elements in sorted manner including both
			 * parts.
			 */
			A[start++] = Arr[j];
		}
	}

### Time Complexity

The list of size N is divided into a max of Log N parts, and the merging of all sublists into a single list takes O(N)time, the worst case run time of this algorithm is O(N Log N)

