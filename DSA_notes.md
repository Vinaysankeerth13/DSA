# Data Structures and Algorithms

## Note :
The optimisation code for each problem is given by AI, so there might be a possibility that they're not an exact fit for the problem you're solving. Please bear that in mind and modify the code implementing the concepts that are provided for optimisation.

## 25-04-2024
### Selection Sort

- Selection Sort is a simple sorting algorithm that works by repeatedly finding the minimum element from the unsorted part of the array and swapping it with the first element of the unsorted part.

Pseudocode for the Selection Sort algorithm:

```
SELECTION-SORT(A)
    n = length(A)
    for i = 0 to n-2
        min = i
        for j = i+1 to n-1
            if A[j] < A[min]
                min = j
        swap A[i] and A[min]
```

Explanation:

1. `SELECTION-SORT` is the function that takes an array `A` as input.
2. `n` is the length of the array `A`.
3. The outer loop iterates from `i=0` to `n-2` (since the last element will be in its correct position after `n-1` iterations).
4. In each iteration of the outer loop, we assume that the minimum element is at index `i` (hence `min = i`).
5. The inner loop iterates from `i+1` to `n-1` (the unsorted part of the array).
6. In each iteration of the inner loop, we check if the current element `A[j]` is smaller than the assumed minimum `A[min]`. If so, we update `min` to `j`.
7. After the inner loop completes, `min` will hold the index of the smallest element in the unsorted part of the array.
8. We then swap `A[i]` with `A[min]`, effectively placing the smallest element at the beginning of the unsorted part of the array.
9. The process repeats until the entire array is sorted.

The time complexity of Selection Sort is O(n^2) in both the average and worst cases, because the inner loop runs for each element in the unsorted part of the array. However, it has the advantage of swapping elements only when necessary, making it more efficient than other quadratic sorting algorithms like Bubble Sort when dealing with partially sorted arrays.

Here's a breakdown of the code:

```java
public static void selectionSort(int[] arr) {
    int len = arr.length;
    for (int i = 0; i < len - 1; i++) {
        int lowest = arr[i]; // Assume the first unsorted element is the minimum
        int lowIn = i; // Index of the minimum element
        for (int j = i + 1; j < len; j++) {
            if (arr[j] < lowest) { // If a smaller element is found
                lowest = arr[j]; // Update the minimum
                lowIn = j; // Update the index of the minimum
            }
        }
        swap(arr, i, lowIn); // Swap the minimum element with the first unsorted element
    }
}
```

The `selectionSort` method takes an integer array `arr` as input. It iterates over the array from index `0` to `len - 2` (where `len` is the length of the array). For each iteration `i`, it finds the minimum element in the unsorted part of the array (from `i + 1` to `len - 1`). It keeps track of the minimum value (`lowest`) and its index (`lowIn`). After finding the minimum, it calls the `swap` method to swap the minimum element with the element at index `i`.

```java
public static void swap(int[] arr, int a, int b) {
    int temp = arr[a];
    arr[a] = arr[b];
    arr[b] = temp;
}
```

The `swap` method is a helper method that swaps the elements at indices `a` and `b` in the array `arr`.

As for a better version of this code, there are a few potential improvements:

1. **Optimized Swapping**: Instead of using a temporary variable to swap elements, you can use XOR swapping or Java's built-in `Math.min` method to find the minimum element directly, which can improve performance slightly.

2. **Generic Implementation**: You can make the code more generic by using a generic type instead of `int` arrays, allowing it to work with other types of arrays as well.

3. **Functional Programming Style**: If you prefer a functional programming style, you can rewrite the code using Java 8 lambda expressions and streams, which can make the code more concise and readable (although it might not improve performance).

Here's an example of a generic and functional implementation using Java 8 streams:

```java
public static <T extends Comparable<T>> void selectionSort(T[] arr) {
    for (int i = 0; i < arr.length - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < arr.length; j++) {
            if (arr[j].compareTo(arr[minIndex]) < 0) {
                minIndex = j;
            }
        }
        swap(arr, i, minIndex);
    }
}

private static <T> void swap(T[] arr, int i, int j) {
    T temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

This implementation uses generics to work with any type that implements the `Comparable` interface. It also uses the `compareTo` method for comparison instead of hard-coding it for integers. The `swap` method is also made generic. While this version is more flexible and arguably more readable, it might not offer significant performance improvements over the original version.

[Selection Sort (Java)](https://youtu.be/dsqsnngsoD8?feature=shared "Selection Sort")


### Bubble Sort

Bubble Sort is a simple sorting algorithm that repeatedly swaps adjacent elements if they are in the wrong order, making the largest element "bubble up" towards the end of the array.

Here's the pseudocode for the Bubble Sort algorithm:

Sure, here's the pseudocode for Bubble Sort with explanations:

```
BUBBLE-SORT(A)
    n = length(A)             
    swapped = true            
    while swapped             
        swapped = false       
        for i = 0 to n-2      
            if A[i] > A[i+1]  
                swap A[i] and A[i+1]  
                swapped = true                     
```

Explanations:

1. `BUBBLE-SORT` is the function that takes an array `A` as input.
2. `n` is the length of the array `A`.
3. The `swapped` flag is initialized to `true` to ensure that the outer loop runs at least once.
4. The outer loop continues until no swaps are performed during an iteration (i.e., `swapped` is `false`).
5. Inside the outer loop, the `swapped` flag is set to `false` initially.
6. The inner loop iterates from `0` to `n-2` (since the last element will be in its correct position after `n-1` iterations).
7. If the current element `A[i]` is greater than the next element `A[i+1]`, it means they are in the wrong order, so they are swapped.
8. After swapping, the `swapped` flag is set to `true` to indicate that a swap occurred during this iteration.
9. If no swaps occurred during an iteration of the outer loop, the `swapped` flag remains `false`, and the loop terminates, indicating that the array is sorted.
10. After each iteration of the outer loop, the largest remaining element will be in its correct position at the end of the array.

The time complexity of Bubble Sort is O(n^2) in both the average and worst cases, because the inner loop runs for each element in the array, and the outer loop may run up to `n` times in the worst case (when the array is in reverse order).

Here's a breakdown of the code:

```java
public static void bubbleSort(int[] arr, int n) {
    boolean toSwap = true;
    while (toSwap) {
        toSwap = false;
        for (int i = 0; i < arr.length - 1; i++) {
            if (arr[i] > arr[i + 1]) {
                toSwap = true;
                int temp = arr[i];
                arr[i] = arr[i + 1];
                arr[i + 1] = temp;
            }
        }
    }
}
```

1. The method takes an integer array `arr` and its length `n` as input.
2. The `toSwap` flag is initialized to `true` to ensure that the outer loop runs at least once.
3. The outer loop continues until no swaps are performed during an iteration (i.e., the array is sorted).
4. Inside the outer loop, the `toSwap` flag is set to `false` initially.
5. The inner loop iterates from `0` to `arr.length - 2` (since the last element will be in its correct position after `n-1` iterations).
6. If the current element `arr[i]` is greater than the next element `arr[i + 1]`, it means they are in the wrong order, so they are swapped using a temporary variable `temp`.
7. After swapping, the `toSwap` flag is set to `true` to indicate that a swap occurred during this iteration.
8. If no swaps occurred during an iteration of the outer loop, the `toSwap` flag remains `false`, and the loop terminates, indicating that the array is sorted.

The time complexity of Bubble Sort is O(n^2) in both the average and worst cases, because the inner loop runs for each element in the array, and the outer loop may run up to `n` times in the worst case (when the array is in reverse order).

As for an optimized version of the code, there's a small optimization that can be made. Instead of always iterating from `0` to `n-2` in the inner loop, we can keep track of the last swap position and only iterate up to that position. This is because after the first iteration, the largest element will be at the end of the array, so we don't need to compare it with the rest of the elements in subsequent iterations.

Here's the optimized version of the Bubble Sort code:

```java
public static void bubbleSort(int[] arr) {
    int n = arr.length;
    boolean swapped;
    for (int i = 0; i < n - 1; i++) {
        swapped = false;
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr, j, j + 1);
                swapped = true;
            }
        }
        if (!swapped) {
            break;
        }
    }
}

private static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

In this optimized version, the outer loop iterates from `0` to `n-2`, and the inner loop iterates from `0` to `n-i-2`. If no swaps occurred during an iteration of the inner loop, we can break out of the outer loop because the array is already sorted.

This optimization reduces the number of comparisons and swaps performed, but the time complexity remains O(n^2) in both the average and worst cases.

[Bubble Sort Video (Java)](https://www.youtube.com/watch?v=g8qeaEd2jTc "Bubble Sort")

## Recursive Bubble sort

The recursive approach works by dividing the array into two parts: the sorted part and the unsorted part. The recursion is used to sort the unsorted part, and then the last element of the unsorted part is "bubbled up" to its correct position in the sorted part.

Here's the pseudocode for the recursive Bubble Sort:

```
RECURSIVE-BUBBLE-SORT(A, n)
    if n == 1
        return
    else
        for i = 0 to n-2
            if A[i] > A[i+1]
                swap A[i] and A[i+1]
        RECURSIVE-BUBBLE-SORT(A, n-1)
```

Explanation:

1. `RECURSIVE-BUBBLE-SORT` is the function that takes an array `A` and its length `n` as input.
2. The base case is when `n` is equal to 1, which means the array contains only one element, so it is already sorted.
3. If `n` is greater than 1, the function performs the following steps:
   a. Iterate from `0` to `n-2` (since the last element will be in its correct position after `n-1` iterations).
   b. If the current element `A[i]` is greater than the next element `A[i+1]`, swap them.
   c. After the loop completes, the largest element will be at the end of the array.
4. The function then recursively calls itself with the same array `A` and `n-1` as the new length, effectively sorting the first `n-1` elements.

Here's the Java implementation of the recursive Bubble Sort:

```java
public static void recursiveBubbleSort(int[] arr, int n) {
    if (n == 1) {
        return; // Base case: single element is already sorted
    }

    // Bubble up the largest element to the end
    for (int i = 0; i < n - 1; i++) {
        if (arr[i] > arr[i + 1]) {
            swap(arr, i, i + 1);
        }
    }

    // Recursively sort the remaining unsorted part
    recursiveBubbleSort(arr, n - 1);
}

private static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

Time Complexity:
- The time complexity of the recursive Bubble Sort is still O(n^2) in both the average and worst cases, just like the iterative version.
- This is because the outer loop runs `n` times, and the inner loop runs up to `n-1` times for each iteration of the outer loop.

Space Complexity:
- The space complexity of the recursive Bubble Sort is O(n) due to the recursive calls on the call stack.
- In the worst case, when the array is in reverse order, the recursion stack will have a depth of `n`, leading to O(n) space complexity.

While the recursive version of Bubble Sort has the same time complexity as the iterative version, it may be less efficient due to the overhead of recursive function calls and the additional space required for the call stack. The recursive approach is generally less preferred for sorting algorithms, as it can lead to stack overflow errors for large input sizes.

It's worth noting that Bubble Sort itself is not an efficient algorithm for large datasets, as its time complexity is quadratic. For large datasets, more efficient sorting algorithms like Merge Sort or Quicksort, which have an average time complexity of O(n log n), are generally preferred.

[Bubble Sort Video (Java)](https://www.youtube.com/watch?v=g8qeaEd2jTc "Bubble Sort")

## Insertion Sort

Insertion Sort is a simple sorting algorithm that builds the final sorted array one item at a time by taking an element from the input array and inserting it into its correct position in the sorted part of the array.

Pseudocode for Insertion Sort:

```
INSERTION-SORT(A)
    n = length(A)
    for i = 1 to n-1                      
        key = A[i]                        
        j = i - 1                         
        while j >= 0 and A[j] > key       
            A[j+1] = A[j]                 
            j = j - 1                     
        A[j+1] = key                      
```

Explanations:

1. `INSERTION-SORT` is the function that takes an array `A` as input.
2. `n` is the length of the array `A`.
3. The outer loop iterates from the second element (`i = 1`) to the last element (`n-1`).
4. For each iteration `i`, the current element `A[i]` is stored in the `key` variable.
5. The inner loop starts from the previous element (`j = i - 1`) and moves towards the beginning of the array.
6. The inner loop continues as long as `j` is greater than or equal to 0, and the element `A[j]` is greater than the `key`.
7. Inside the inner loop, the elements greater than the `key` are shifted one position to the right by assigning `A[j+1] = A[j]`.
8. After the inner loop completes, the correct position for the `key` is found, and it is inserted at `A[j+1]`.

Now, let's analyze the given Java code:

```java
public static void insertionSort(int[] arr, int size) {
    for (int i = 1; i < size; i++) {
        int currVal = arr[i];    // Store the current element to be inserted
        int j = i - 1;           // Start from the previous element
        while (j >= 0 && arr[j] > currVal) {  // Move elements greater than currVal to the right
            arr[j + 1] = arr[j];              // Shift the elements to the right
            j--;                              // Decrement j to the next element
        }
        arr[j + 1] = currVal;    // Insert currVal at the correct position
    }
}
```

The Java code follows the same logic as the pseudocode, with a few minor differences in variable naming and array indexing.

Time Complexity:
- Best Case: O(n) when the array is already sorted.
- Average and Worst Case: O(n^2) because the inner loop may run for each element in the array.

Space Complexity:
- O(1) - Insertion Sort is an in-place algorithm, meaning it doesn't require additional memory proportional to the input size.

Optimizations:
Insertion Sort is already efficient for small datasets and partially sorted arrays. However, for large datasets that are completely unsorted, other sorting algorithms like Merge Sort or Quicksort perform better in the average case, with time complexities of O(n log n).

One potential optimization for Insertion Sort is to use a binary search instead of a linear search to find the correct position for the `key` element. This optimization reduces the time complexity to O(n log n) in the worst case, but it comes with the trade-off of increased code complexity and additional memory overhead for the binary search.

Another optimization is to combine Insertion Sort with other sorting algorithms, using Insertion Sort for small subarrays and another efficient algorithm for larger subarrays. This hybrid approach can leverage the strengths of both algorithms and provide better overall performance.

[Insertion Sort (Java)](https://youtu.be/0lOnnd50cGI?feature=shared "Insertion Sort")

### Recursive Insertion Sort

The recursive approach works by dividing the array into two parts: the sorted part and the unsorted part. The recursion is used to sort the unsorted part, and then the first element of the unsorted part is inserted into its correct position in the sorted part.

Pseudocode for the recursive Insertion Sort:

```
RECURSIVE-INSERTION-SORT(A, n)
    if n <= 1
        return  // Base case: array with 0 or 1 element is already sorted
    
    RECURSIVE-INSERTION-SORT(A, n-1)  // Sort the first n-1 elements
    
    // Insert the last element into the sorted subarray
    key = A[n-1]  // The last element to be inserted
    j = n-2       // Start from the last sorted element
    while j >= 0 and A[j] > key
        A[j+1] = A[j]  // Shift elements greater than key to the right
        j = j - 1
    A[j+1] = key  // Insert the key at the correct position
```

Explanation:

1. `RECURSIVE-INSERTION-SORT` is the function that takes an array `A` and its length `n` as input.
2. The base case is when `n` is less than or equal to 1, which means the array contains zero or one element, so it is already sorted.
3. If `n` is greater than 1, the function performs the following steps:
   a. Recursively call `RECURSIVE-INSERTION-SORT` with the first `n-1` elements of the array.
   b. After the recursive call returns, the first `n-1` elements are sorted.
   c. The last element `A[n-1]` is stored in the `key` variable.
   d. Start from the last sorted element `A[n-2]` and move towards the beginning of the array.
   e. Shift all elements greater than the `key` one position to the right.
   f. Insert the `key` at the correct position.

Here's the Java implementation of the recursive Insertion Sort:

```java
public static void recursiveInsertionSort(int[] arr, int n) {
    if (n <= 1) {
        return; // Base case: array with 0 or 1 element is already sorted
    }

    // Sort the first n-1 elements
    recursiveInsertionSort(arr, n - 1);

    // Insert the last element into the sorted subarray
    int key = arr[n - 1];
    int j = n - 2;
    while (j >= 0 && arr[j] > key) {
        arr[j + 1] = arr[j]; // Shift elements greater than key to the right
        j--;
    }
    arr[j + 1] = key; // Insert the key at the correct position
}
```

Time Complexity:
- The time complexity of the recursive Insertion Sort is O(n^2) in both the average and worst cases, just like the iterative version.
- This is because, in the worst case, the inner loop runs `n-1` times for each recursive call, and there are `n` recursive calls.

Space Complexity:
- The space complexity of the recursive Insertion Sort is O(n) due to the recursive calls on the call stack.
- In the worst case, when the array is in reverse order, the recursion stack will have a depth of `n`, leading to O(n) space complexity.

Similar to the recursive Bubble Sort, the recursive version of Insertion Sort has the same time complexity as the iterative version, but it may be less efficient due to the overhead of recursive function calls and the additional space required for the call stack. The recursive approach is generally less preferred for sorting algorithms, as it can lead to stack overflow errors for large input sizes.

It's worth noting that Insertion Sort is efficient for small datasets and partially sorted arrays, with a time complexity of O(n) in the best case. However, for large datasets that are completely unsorted, other sorting algorithms like Merge Sort or Quicksort, which have an average time complexity of O(n log n), are generally preferred.

[Insertion Sort (Java)](https://youtu.be/0lOnnd50cGI?feature=shared "Insertion Sort")


## 26-04-2024
### Merge Sort

Merge Sort is a divide-and-conquer algorithm that repeatedly divides the input array into two halves until each subarray contains only one element. It then merges the subarrays in a sorted manner to produce the final sorted array.

Pseudocode for Merge Sort with explanations:

```
MERGE-SORT(A, left, right)
    if left < right
        middle = (left + right) / 2
        MERGE-SORT(A, left, middle)       
        MERGE-SORT(A, middle + 1, right)  
        MERGE(A, left, middle, right)     

MERGE(A, left, middle, right)
    n1 = middle - left + 1    
    n2 = right - middle       
    Create temporary arrays L[n1] and R[n2]

   
    for i = 0 to n1 - 1
        L[i] = A[left + i]
    for j = 0 to n2 - 1
        R[j] = A[middle + 1 + j]

    i = 0   
    j = 0   
    k = left

    
    while i < n1 and j < n2
        if L[i] <= R[j]
            A[k] = L[i]
            i = i + 1
        else
            A[k] = R[j]
            j = j + 1
        k = k + 1

    
    while i < n1
        A[k] = L[i]
        i = i + 1
        k = k + 1

    
    while j < n2
        A[k] = R[j]
        j = j + 1
        k = k + 1
```

Explanation:

1. `MERGE-SORT` is the main function that takes an array `A`, along with the left and right indices of the subarray to be sorted.
2. The base case is when `left` is greater than or equal to `right`, which means the subarray has zero or one element, and is already sorted.
3. If the base case is not met, the function calculates the middle index `middle = (left + right) / 2`.
4. The function recursively calls `MERGE-SORT` on the left subarray `A[left..middle]` and the right subarray `A[middle+1..right]`.
5. After the recursive calls return, the left and right subarrays are sorted.
6. The `MERGE` function is called to merge the sorted left and right subarrays into the original array `A`.

7. The `MERGE` function creates temporary arrays `L` and `R` to store the elements of the left and right subarrays, respectively.
8. The function then iterates through the temporary arrays and copies the elements back into the original array `A` in sorted order.
9. If there are any remaining elements in either the left or right subarray, they are copied back into `A` as they are already sorted.

Now, let's analyze the given Java code:

```java
public static void mergeSort(int[] arr, int l, int r) {
    if (l >= r) {
        return;
    }
    int mid = (l + r) / 2;
    mergeSort(arr, l, mid);
    mergeSort(arr, mid + 1, r);
    merge(arr, l, mid, r);
}

public static void merge(int[] arr, int low, int mid, int high) {
    ArrayList<Integer> temp = new ArrayList<>();
    int left = low;
    int right = mid + 1;

    while (left <= mid && right <= high) {
        if (arr[left] <= arr[right]) {
            temp.add(arr[left]);
            left++;
        } else {
            temp.add(arr[right]);
            right++;
        }
    }

    while (left <= mid) {
        temp.add(arr[left]);
        left++;
    }

    while (right <= high) {
        temp.add(arr[right]);
        right++;
    }

    for (int i = low; i <= high; i++) {
        arr[i] = temp.get(i - low);
    }
}
```

The Java code follows the same logic as the pseudocode, with a few minor differences:

1. Instead of creating temporary arrays `L` and `R`, the code uses an `ArrayList` called `temp` to store the merged elements.
2. The code uses two pointers, `left` and `right`, to traverse the left and right subarrays, respectively.
3. After merging the sorted elements from the left and right subarrays, any remaining elements from either subarray are copied into the `temp` ArrayList.
4. Finally, the elements from the `temp` ArrayList are copied back into the original array `arr`.

Time Complexity:
- The time complexity of Merge Sort is O(n log n) in both the average and worst cases.
- This is because the divide step takes O(log n) time, and the merge step takes O(n) time for each level of the recursion tree.

Space Complexity:
- The space complexity of Merge Sort is O(n) due to the use of temporary arrays or data structures (like the `ArrayList` in the given code) for merging the subarrays.

Optimizations:
The given implementation of Merge Sort is already quite efficient, but there are a few potential optimizations:

1. **In-place Merge Sort**: Instead of using an additional data structure like an `ArrayList`, an in-place merge sort algorithm can be implemented by allocating a temporary array of the same size as the input array and merging the subarrays directly into the temporary array. This approach can slightly improve space efficiency by eliminating the overhead of dynamic memory allocation and deallocation.

2. **Parallel Merge Sort**: Since Merge Sort is a divide-and-conquer algorithm, it can be parallelized to take advantage of multiple cores or processors. This can significantly improve performance, especially for large datasets.

3. **Linked List Implementation**: If the input data is already in the form of a linked list, a specialized Merge Sort implementation can be used that avoids the need for copying elements during the merge step, potentially improving performance.

4. **Hybrid Approach**: For small subarrays, Merge Sort can be combined with a more efficient sorting algorithm like Insertion Sort, which has a time complexity of O(n^2) but performs better for small inputs. This hybrid approach can leverage the strengths of both algorithms and provide better overall performance.

Overall, Merge Sort is a efficient and stable sorting algorithm, making it a popular choice for various applications, especially when dealing with large datasets.

[Merge Sort video (Java)](https://www.youtube.com/watch?v=bOk35XmHPKs "Merge Sort")

### Quick Sort

Quicksort is a divide-and-conquer algorithm that is widely used for sorting arrays and lists. It works by partitioning the array around a pivot element and recursively sorting the subarrays before and after the pivot.

Pseudocode for Quicksort with explanations:

```
QUICKSORT(A, start, end)
    if start < end
        pivot = PARTITION(A, start, end)
        QUICKSORT(A, start, pivot - 1)
        QUICKSORT(A, pivot + 1, end)

PARTITION(A, start, end)
    pivotIndex = end
    pivot = A[pivotIndex]
    leftPointer = start
    rightPointer = end - 1

    while leftPointer <= rightPointer
        while A[leftPointer] < pivot
            leftPointer = leftPointer + 1

        while A[rightPointer] > pivot
            rightPointer = rightPointer - 1

        if leftPointer <= rightPointer
            swap A[leftPointer] and A[rightPointer]
            leftPointer = leftPointer + 1
            rightPointer = rightPointer - 1

    swap A[leftPointer] and A[pivotIndex]
    return leftPointer
```

Explanation:

1. `QUICKSORT` is the main function that takes an array `A`, along with the start and end indices of the subarray to be sorted.
2. The base case is when `start` is greater than or equal to `end`, which means the subarray has zero or one element, and is already sorted.
3. If the base case is not met, the function calls `PARTITION` to partition the array around a pivot element.
4. The `PARTITION` function selects the last element of the subarray as the pivot.
5. It then creates two pointers, `leftPointer` and `rightPointer`, which initially point to the start and end-1 indices of the subarray, respectively.
6. The function moves the `leftPointer` to the right until it finds an element greater than or equal to the pivot, and the `rightPointer` to the left until it finds an element less than or equal to the pivot.
7. If `leftPointer` is still less than or equal to `rightPointer`, the elements at these indices are swapped.
8. This process continues until `leftPointer` is greater than `rightPointer`.
9. Finally, the pivot element is swapped with the element at `leftPointer`, and `leftPointer` is returned as the partitioning index.
10. The `QUICKSORT` function recursively calls itself on the left and right subarrays, divided by the partitioning index.

Now, let's analyze the given Java code:

```java
public static void quickSort(int[] input, int startIndex, int endIndex) {
    if (startIndex >= endIndex) {
        return;
    }

    int pivot = input[endIndex];
    int leftPointer = startIndex;
    int rightPointer = endIndex;

    while (leftPointer < rightPointer) {
        while (input[leftPointer] <= pivot && leftPointer < rightPointer) {
            leftPointer++;
        }
        while (input[rightPointer] >= pivot && leftPointer < rightPointer) {
            rightPointer--;
        }
        swap(input, leftPointer, rightPointer);
    }

    swap(input, leftPointer, endIndex);
    quickSort(input, startIndex, leftPointer - 1);
    quickSort(input, leftPointer + 1, endIndex);
}

private static void swap(int[] array, int index1, int index2) {
    int temp = array[index1];
    array[index1] = array[index2];
    array[index2] = temp;
}
```

The Java code follows the same logic as the pseudocode, with a few minor differences:

1. The `quickSort` function takes an input array `input`, along with the start and end indices of the subarray to be sorted.
2. The pivot element is chosen as the last element of the subarray, `input[endIndex]`.
3. The `leftPointer` and `rightPointer` initially point to the start and end indices of the subarray, respectively.
4. The `while` loop moves the `leftPointer` to the right and the `rightPointer` to the left, swapping elements as needed, until `leftPointer` is greater than `rightPointer`.
5. After the `while` loop, the pivot element is swapped with the element at `leftPointer`.
6. The `quickSort` function is recursively called on the left and right subarrays, divided by the `leftPointer` index.
7. The `swap` function is a helper function that swaps the elements at the given indices in the input array.

Time Complexity:
- The average time complexity of Quicksort is O(n log n), where n is the size of the input array.
- In the best case, when the partitioning is always balanced, the time complexity is O(n log n).
- In the worst case, when the array is already sorted (or reverse sorted), the time complexity degrades to O(n^2) due to unbalanced partitioning.

Space Complexity:
- The space complexity of Quicksort is O(log n) on average, due to the recursive calls on the call stack.
- In the worst case, when the partitioning is highly unbalanced, the space complexity can degrade to O(n) due to the deeper recursion stack.

Optimizations:
The given implementation of Quicksort is a standard and efficient implementation, but there are a few potential optimizations:

1. **Pivot Selection**: Instead of always choosing the last element as the pivot, more advanced pivot selection strategies can be used to improve the average case performance. For example, the "median-of-three" strategy selects the median of the first, middle, and last elements as the pivot, which can help reduce the likelihood of unbalanced partitioning.

2. **Hybrid Approach**: For small subarrays, Quicksort can be combined with a simpler sorting algorithm like Insertion Sort, which has a time complexity of O(n^2) but performs better for small inputs. This hybrid approach can leverage the strengths of both algorithms and provide better overall performance.

3. **In-place Partitioning**: The given implementation uses two pointers and swaps elements as needed, which can be inefficient for large datasets due to the overhead of swapping. An in-place partitioning algorithm can be used to avoid unnecessary swaps and improve performance.

4. **Parallel Quicksort**: Since Quicksort is a divide-and-conquer algorithm, it can be parallelized to take advantage of multiple cores or processors. This can significantly improve performance, especially for large datasets.

Overall, Quicksort is a highly efficient and widely used sorting algorithm, particularly for large datasets. Its average time complexity of O(n log n) and in-place sorting make it a popular choice in various applications.

[Quick Sort (Java)](https://www.youtube.com/watch?v=h8eyY7dIiN4 "Quick Sort")

## Array Problems

### Easy:

**1. Largest Element in the Array**

[Largest Element in the array](https://www.naukri.com/code360/problems/largest-element-in-the-array-largest-element-in-the-array_5026279?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

Given an array ‘arr’ of size ‘n’ find the largest element in the array.

Example:

Input: 'n' = 5, 'arr' = [1, 2, 3, 4, 5]

Output: 5

Explanation: From the array {1, 2, 3, 4, 5}, the largest element is 5.

Pseudocode with explanations:

```
FIND-LARGEST-ELEMENT(A, n)
    largest = A[0]  // Initialize largest with the first element
    for i = 1 to n-1
        if A[i] > largest
            largest = A[i]  // Update largest if a larger element is found
    return largest
```

Explanation:

1. `FIND-LARGEST-ELEMENT` is a function that takes an array `A` and its length `n` as input.
2. The variable `largest` is initialized with the first element of the array `A[0]`.
3. The loop iterates from the second element (`i = 1`) to the last element (`n-1`).
4. For each element `A[i]`, it is compared with the current value of `largest`.
5. If `A[i]` is greater than `largest`, the value of `largest` is updated to `A[i]`.
6. After the loop completes, the function returns the value stored in `largest`, which represents the largest element in the array.

Now, let's analyze the given Java code:

```java
public class Solution {
    static int largestElement(int[] arr, int n) {
        int largest = 0;
        for (int i = 0; i < n; i++) {
            if (arr[i] > largest) {
                largest = arr[i];
            }
        }
        return largest;
    }
}
```

The Java code follows the same logic as the pseudocode, with a few minor differences:

1. The `largestElement` function takes an integer array `arr` and its length `n` as input.
2. The variable `largest` is initialized with `0`, assuming that the array contains non-negative integers.
3. The loop iterates from `i = 0` to `i < n` (instead of `1` to `n-1`).
4. For each element `arr[i]`, it is compared with the current value of `largest`.
5. If `arr[i]` is greater than `largest`, the value of `largest` is updated to `arr[i]`.
6. After the loop completes, the function returns the value stored in `largest`, which represents the largest element in the array.

Time Complexity:
- The time complexity of this algorithm is O(n), where n is the length of the input array.
- This is because the algorithm needs to iterate through the entire array once to find the largest element.

Space Complexity:
- The space complexity is O(1), which means it uses a constant amount of extra space, regardless of the input size.
- The algorithm only uses a few variables to store temporary values and does not require any additional data structures proportional to the input size.

Optimizations:
The given implementation is already efficient for finding the largest element in an array, with a time complexity of O(n) and a constant space complexity of O(1). However, there are a few potential optimizations that can be considered:

1. **Parallelization**: If you have access to multiple processors or cores, you can parallelize the algorithm by dividing the array into smaller chunks and finding the largest element in each chunk concurrently. Then, you can compare the largest elements from each chunk to find the overall largest element. This optimization can provide significant performance improvements, especially for large arrays.

2. **Early Termination**: If you know that the array is sorted (in ascending or descending order), you can terminate the loop early once you encounter an element that is smaller (or larger) than the current `largest` value, since all remaining elements will also be smaller (or larger) than `largest`.

3. **Divide and Conquer**: You can also apply a divide-and-conquer approach to finding the largest element. Split the array into two halves, find the largest element in each half recursively, and then compare the two largest elements to find the overall largest element. This approach has a time complexity of O(n log n), which is less efficient than the linear approach for finding the largest element, but it can be useful if you need to perform additional operations on the subarrays.

In general, the given implementation is simple and efficient for finding the largest element in an array, and no significant optimizations are required unless you have specific constraints or requirements, such as parallelization or the need to perform additional operations on the array.

**2. Second Smallest Number without sorting**

[Second smallest number without sorting](https://www.naukri.com/code360/problems/ninja-and-the-second-order-elements_6581960?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

You have been given an array ‘a’ of ‘n’ unique non-negative integers.

Find the second largest and second smallest element from the array.

Return the two elements (second largest and second smallest) as another array of size 2.

Example :
Input: ‘n’ = 5, ‘a’ = [1, 2, 3, 4, 5]
Output: [4, 2]

The second largest element after 5 is 4, and the second smallest element after 1 is 2.

Here's the pseudocode with explanations:

```
FIND-SECOND-ORDER-ELEMENTS(A, n)
    max = -1        // Initialize max to a small value
    secMax = -1     // Initialize secMax to a small value
    min = MAX_VALUE // Initialize min to a large value
    secMin = MAX_VALUE // Initialize secMin to a large value

    for each num in A
        if num > max
            secMax = max  // Update secMax with the previous max
            max = num     // Update max with the new larger value
        else if num > secMax
            secMax = num  // Update secMax with the new larger value

        if num < min
            secMin = min  // Update secMin with the previous min
            min = num     // Update min with the new smaller value
        else if num < secMin
            secMin = num  // Update secMin with the new smaller value

    return [secMax, secMin]
```

Explanation:

1. `FIND-SECOND-ORDER-ELEMENTS` is a function that takes an array `A` and its length `n` as input.
2. The variables `max` and `secMax` are initialized with a small value (-1 in this case), assuming that the array contains positive integers.
3. The variables `min` and `secMin` are initialized with the maximum possible value for integers (`Integer.MAX_VALUE` in Java), assuming that the array contains non-negative integers.
4. The loop iterates through each element `num` in the array `A`.
5. For each element `num`:
   a. If `num` is greater than `max`, `secMax` is updated with the previous value of `max`, and `max` is updated with `num`.
   b. If `num` is greater than `secMax` but not greater than `max`, `secMax` is updated with `num`.
   c. If `num` is smaller than `min`, `secMin` is updated with the previous value of `min`, and `min` is updated with `num`.
   d. If `num` is smaller than `secMin` but not smaller than `min`, `secMin` is updated with `num`.
6. After the loop completes, the function returns an array containing `secMax` and `secMin`, which represent the second maximum and second minimum elements in the array, respectively.

Now, let's analyze the given Java code:

```java
public class Solution {
    public static int[] getSecondOrderElements(int n, int[] a) {
        int max = -1, secMax = -1, min = Integer.MAX_VALUE, secMin = Integer.MAX_VALUE;
        for (int num : a) {
            if (num > max) {
                secMax = max;
                max = num;
            } else if (num > secMax) {
                secMax = num;
            }
            if (num < min) {
                secMin = min;
                min = num;
            } else if (num < secMin) {
                secMin = num;
            }
        }
        return new int[]{secMax, secMin};
    }
}
```

The Java code follows the same logic as the pseudocode, with a few minor differences:

1. The `getSecondOrderElements` function takes an integer `n` (which is not used in the implementation) and an integer array `a` as input.
2. The variables `max`, `secMax`, `min`, and `secMin` are initialized as in the pseudocode.
3. The `for` loop uses the enhanced `for` loop syntax to iterate through each element `num` in the array `a`.
4. The conditional statements update the values of `max`, `secMax`, `min`, and `secMin` as described in the pseudocode.
5. After the loop completes, the function returns a new integer array containing `secMax` and `secMin`.

Time Complexity:
- The time complexity of this algorithm is O(n), where n is the length of the input array.
- This is because the algorithm needs to iterate through the entire array once to find the second maximum and second minimum elements.

Space Complexity:
- The space complexity is O(1), which means it uses a constant amount of extra space, regardless of the input size.
- The algorithm only uses a few variables to store temporary values and does not require any additional data structures proportional to the input size.

Optimizations:
The given implementation is already efficient for finding the second maximum and second minimum elements in an array, with a time complexity of O(n) and a constant space complexity of O(1). However, there are a few potential optimizations that can be considered:

1. **Early Termination**: If you know that the array is sorted (in ascending or descending order), you can terminate the loop early once you have found the second maximum and second minimum elements, since all remaining elements will either be smaller than the second minimum or larger than the second maximum.

2. **Divide and Conquer**: You can apply a divide-and-conquer approach to finding the second maximum and second minimum elements. Split the array into two halves, find the second maximum and second minimum in each half recursively, and then combine the results to find the overall second maximum and second minimum elements. This approach has a time complexity of O(n log n), which is less efficient than the linear approach for this specific problem, but it can be useful if you need to perform additional operations on the subarrays.

3. **Parallelization**: If you have access to multiple processors or cores, you can parallelize the algorithm by dividing the array into smaller chunks and finding the second maximum and second minimum in each chunk concurrently. Then, you can combine the results from each chunk to find the overall second maximum and second minimum elements. This optimization can provide significant performance improvements, especially for large arrays.

In general, the given implementation is simple and efficient for finding the second maximum and second minimum elements in an array, and no significant optimizations are required unless you have specific constraints or requirements, such as parallelization or the need to perform additional operations on the array.

## 27-04-2024

**3. Check Sorted Array**

[Check Sorted Array (CodeStudio)](https://www.naukri.com/code360/problems/ninja-and-the-sorted-check_6581957?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM "Check Sorted Array")

Pseudocode with explanations:

```
IS-SORTED(A, n)
    for i = 0 to n-2
        if A[i] > A[i+1]
            return 0  // Array is not sorted
    return 1  // Array is sorted
```

Explanation:

1. `IS-SORTED` is a function that takes an array `A` and its length `n` as input.
2. The loop iterates from index `0` to `n-2` (since we only need to check up to the second-to-last element).
3. For each index `i`, the function compares the element `A[i]` with the next element `A[i+1]`.
4. If `A[i]` is greater than `A[i+1]`, it means the array is not sorted in non-decreasing order, so the function immediately returns `0` (indicating that the array is not sorted).
5. If the loop completes without finding any pair of adjacent elements in the wrong order, the function returns `1` (indicating that the array is sorted).

Now, let's analyze the given Java code:

```java
public static int isSorted(int n, int[] a) {
    for (int i = 0; i < n - 1; i++) {
        if (a[i] > a[i + 1]) {
            return 0;
        }
    }
    return 1;
}
```

The Java code follows the same logic as the pseudocode, with a few minor differences:

1. The `isSorted` function takes an integer `n` (representing the length of the array) and an integer array `a` as input.
2. The loop iterates from index `0` to `n-2` (since we only need to check up to the second-to-last element).
3. For each index `i`, the function compares the element `a[i]` with the next element `a[i+1]`.
4. If `a[i]` is greater than `a[i+1]`, the function immediately returns `0` (indicating that the array is not sorted).
5. If the loop completes without finding any pair of adjacent elements in the wrong order, the function returns `1` (indicating that the array is sorted).

Time Complexity:
- The time complexity of this algorithm is O(n), where n is the length of the input array.
- This is because the algorithm needs to iterate through the entire array once to check if it is sorted.

Space Complexity:
- The space complexity is O(1), which means it uses a constant amount of extra space, regardless of the input size.
- The algorithm only uses a few variables to store temporary values and does not require any additional data structures proportional to the input size.

Optimizations:
The given implementation is already efficient for checking if an array is sorted in non-decreasing order, with a time complexity of O(n) and a constant space complexity of O(1). However, there are a few potential optimizations that can be considered:

1. **Early Termination**: Instead of checking the entire array, you can terminate the loop early as soon as you find a pair of adjacent elements in the wrong order. This optimization is already implemented in the given code.

2. **Checking for Sorted in Decreasing Order**: If you need to check if the array is sorted in decreasing order as well, you can modify the condition in the loop to `if (a[i] < a[i+1])` instead of `if (a[i] > a[i+1])`.

3. **Checking for Strict Sorting**: If you need to check if the array is strictly sorted (i.e., no adjacent elements are equal), you can modify the condition in the loop to `if (a[i] >= a[i+1])` for non-decreasing order or `if (a[i] <= a[i+1])` for non-increasing order.

4. **Parallelization**: If you have access to multiple processors or cores, you can parallelize the algorithm by dividing the array into smaller chunks and checking if each chunk is sorted concurrently. Then, you can combine the results from each chunk to determine if the entire array is sorted. This optimization can provide significant performance improvements, especially for large arrays.

In general, the given implementation is simple and efficient for checking if an array is sorted in non-decreasing order, and no significant optimizations are required unless you have specific constraints or requirements, such as checking for sorted in decreasing order, strict sorting, or parallelization.

[Check if the array is sorted and rotated (Leetcode)](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/description/)

Java implementation of a function that checks if an array of integers is a non-decreasing rotated sorted array. A non-decreasing rotated sorted array is an array that has been rotated such that the elements are still in non-decreasing order, but the starting point has changed.

Pseudocode with explanations:

```
CHECK-ROTATED-SORTED-ARRAY(A, n)
    count = 0
    for i = 0 to n-1
        if A[i] > A[(i+1) % n]
            count = count + 1
        if count > 1
            return false  // More than one transition point found
    return true  // Array is a non-decreasing rotated sorted array
```

Explanation:

1. `CHECK-ROTATED-SORTED-ARRAY` is a function that takes an array `A` and its length `n` as input.
2. The variable `count` is initialized to `0`. It will keep track of the number of transition points in the array.
3. The loop iterates from index `0` to `n-1`.
4. For each index `i`, the function compares the element `A[i]` with the next element `A[(i+1) % n]`. The modulus operator `%` is used to wrap around the array when `i` reaches the end.
5. If `A[i]` is greater than `A[(i+1) % n]`, it means there is a transition point, and `count` is incremented.
6. If `count` becomes greater than `1`, it means there are more than one transition points, which violates the condition for a non-decreasing rotated sorted array. In this case, the function immediately returns `false`.
7. If the loop completes without finding more than one transition point, the function returns `true`, indicating that the array is a non-decreasing rotated sorted array.

Now, let's analyze the given Java code:

```java
public boolean check(int[] nums) {
    int count = 0;
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] > nums[(i + 1) % nums.length]) {
            count++;
        }
        if (count > 1) {
            return false;
        }
    }
    return true;
}
```

The Java code follows the same logic as the pseudocode, with a few minor differences:

1. The `check` function takes an integer array `nums` as input.
2. The variable `count` is initialized to `0`.
3. The loop iterates from index `0` to `nums.length-1`.
4. For each index `i`, the function compares the element `nums[i]` with the next element `nums[(i+1) % nums.length]`. The modulus operator `%` is used to wrap around the array when `i` reaches the end.
5. If `nums[i]` is greater than `nums[(i+1) % nums.length]`, it means there is a transition point, and `count` is incremented.
6. If `count` becomes greater than `1`, the function immediately returns `false`.
7. If the loop completes without finding more than one transition point, the function returns `true`, indicating that the array is a non-decreasing rotated sorted array.

Time Complexity:
- The time complexity of this algorithm is O(n), where n is the length of the input array.
- This is because the algorithm needs to iterate through the entire array once to check for transition points.

Space Complexity:
- The space complexity is O(1), which means it uses a constant amount of extra space, regardless of the input size.
- The algorithm only uses a few variables to store temporary values and does not require any additional data structures proportional to the input size.

Optimizations:
The given implementation is already efficient for checking if an array is a non-decreasing rotated sorted array, with a time complexity of O(n) and a constant space complexity of O(1). However, there is one potential optimization that can be considered:

1. **Early Termination**: Instead of checking the entire array, you can terminate the loop early as soon as you find more than one transition point. This optimization is already implemented in the given code.

In general, the given implementation is simple and efficient for checking if an array is a non-decreasing rotated sorted array, and no significant optimizations are required unless you have specific constraints or requirements.

**4. Remove Duplicates from sorted array**

[Remove Duplicates from Sorted Array (CodeStudio)](https://www.naukri.com/code360/problems/remove-duplicates-from-sorted-array_1102307?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

[Remove Duplicates from Sorted Array (Leetcode)](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

The given code is a Java implementation of a function that removes duplicate elements from an array and returns the length of the modified array containing only the unique elements.

Here's the pseudocode with explanations:

```
REMOVE-DUPLICATES(A, n)
    k = 0  // Index to track the position of the last unique element

    for i = 1 to n-1
        if A[i] != A[k]
            k = k + 1
            A[k] = A[i]  // Move the unique element to the next position

    return k + 1  // Length of the modified array
```

Explanation:

1. `REMOVE-DUPLICATES` is a function that takes an array `A` and its length `n` as input.
2. The variable `k` is initialized to `0`. It will keep track of the position of the last unique element in the array.
3. The loop iterates through the array from the second element (index `1`) to the last element (`n-1`).
4. For each element `A[i]`, it checks if it is different from the element at `A[k]`.
5. If `A[i]` is not a duplicate, `k` is incremented, and `A[i]` is assigned to `A[k]`. This effectively moves the unique element to the next available position after the last unique element.
6. After the loop completes, `k` holds the index of the last unique element in the modified array.
7. The function returns `k + 1`, which represents the length of the modified array containing only the unique elements.

Now, let's analyze the given Java code:

```java
public static int removeDuplicates(int[] arr, int n) {
    int k = 0;
    for (int i = 1; i < n; i++) {
        if (arr[i] != arr[k]) {
            arr[++k] = arr[i];
        }
    }
    return k + 1;
}
```

The Java code follows the same logic as the pseudocode, with a few minor differences:

1. The function takes an integer array `arr` and its length `n` as input.
2. The variable `k` is initialized to `0`.
3. The loop iterates through the array from the second element (index `1`) to the last element (`n-1`).
4. For each element `arr[i]`, it checks if it is different from the element at `arr[k]`.
5. If `arr[i]` is not a duplicate, `arr[++k] = arr[i]` is executed, which first increments `k` and then assigns `arr[i]` to `arr[k]`. This moves the unique element to the next available position after the last unique element.
6. After the loop completes, `k` holds the index of the last unique element in the modified array.
7. The function returns `k + 1`, which represents the length of the modified array containing only the unique elements.

Example:

Let's consider the input array `arr = [1, 2, 2, 3, 3, 4, 5, 5]` and `n = 8`.

Initially, `k = 0`.

- Iteration 1: `i = 1`, `arr[i] = 2`, `arr[k] = 1`, they are not equal, so `arr[++k] = arr[i]`, i.e., `arr[1] = 2`, `k = 1`.
- Iteration 2: `i = 2`, `arr[i] = 2`, `arr[k] = 2`, they are equal, so no assignment is done.
- Iteration 3: `i = 3`, `arr[i] = 3`, `arr[k] = 2`, they are not equal, so `arr[++k] = arr[i]`, i.e., `arr[2] = 3`, `k = 2`.
- Iteration 4: `i = 4`, `arr[i] = 3`, `arr[k] = 3`, they are equal, so no assignment is done.
- Iteration 5: `i = 5`, `arr[i] = 4`, `arr[k] = 3`, they are not equal, so `arr[++k] = arr[i]`, i.e., `arr[3] = 4`, `k = 3`.
- Iteration 6: `i = 6`, `arr[i] = 5`, `arr[k] = 4`, they are not equal, so `arr[++k] = arr[i]`, i.e., `arr[4] = 5`, `k = 4`.
- Iteration 7: `i = 7`, `arr[i] = 5`, `arr[k] = 5`, they are equal, so no assignment is done.

After the loop completes, the modified array is `arr = [1, 2, 3, 4, 5]`, and the function returns `k + 1 = 5`, which is the length of the modified array containing only the unique elements.

Time Complexity: O(n), where n is the length of the input array. We iterate through the array once.

Space Complexity: O(1), as we are modifying the input array in-place without using any additional data structures that scale with the input size.

Optimizations:

The given implementation is already quite efficient and concise, as it modifies the input array in-place and avoids unnecessarily setting the remaining elements to a default value. However, one potential optimization could be:

1. **Early Termination**: If you know that the input array is already sorted, you can terminate the loop early as soon as you encounter a duplicate element. This is because all subsequent elements will also be duplicates. However, this optimization assumes that the input array is sorted, which may not always be the case.

In general, the provided implementation is an efficient solution for removing duplicates from an array, with a linear time complexity and constant space complexity.

**5. Left Rotate an Array by One**

Given an array 'arr' containing 'n' elements, rotate this array left once and return it.

Rotating the array left by one means shifting all elements by one place to the left and moving the first element to the last position in the array.

Example:
Input: 'a' = 5, 'arr' = [1, 2, 3, 4, 5]

Output: [2, 3, 4, 5, 1]

Explanation: We moved the 2nd element to the 1st position, and 3rd element to the 2nd position, and 4th element to the 3rd position, and the 5th element to the 4th position, and move the 1st element to the 5th position.

Sure, let's start by providing the pseudocode for the `rotateArray` method:

```
rotateArray(arr, n):
    Create a new array rotatedArr of size n
    Set k to 0
    
    For each index i from 0 to n-1:
        Calculate the new index k using the formula ((i - 1 + n) % n)
        Assign the value of arr[i] to rotatedArr[k]
    
    Return rotatedArr
```

Now, let's explain the provided code with an example array `[1, 2, 3, 4, 5]`:

1. Initialize `k` to 0.
2. Create a new array `rotatedArr` of size `n`, where `n` is the number of elements in the input array.
3. Iterate over each index `i` from 0 to `n-1`.
4. Calculate the new index `k` using the formula `((i - 1 + n) % n)`. This formula shifts each index to the left by one position, with the last element wrapping around to the beginning of the array.
5. Assign the value of `arr[i]` to `rotatedArr[k]`.
6. Return the rotated array `rotatedArr`.

Let's go through each iteration of the provided code using the input array `[1, 2, 3, 4, 5]`.

Given the input array `[1, 2, 3, 4, 5]` and assuming `n = 5`:

1. **Iteration 1 (i = 0)**:
   - Calculate the new index `k` using the formula `((0 - 1 + 5) % 5)`, which results in `k = 4`.
   - Assign the value of `arr[0]` (which is 1) to `rotatedArr[4]`.
   - Result: `rotatedArr = [0, 0, 0, 0, 1]`

2. **Iteration 2 (i = 1)**:
   - Calculate the new index `k` using the formula `((1 - 1 + 5) % 5)`, which results in `k = 0`.
   - Assign the value of `arr[1]` (which is 2) to `rotatedArr[0]`.
   - Result: `rotatedArr = [2, 0, 0, 0, 1]`

3. **Iteration 3 (i = 2)**:
   - Calculate the new index `k` using the formula `((2 - 1 + 5) % 5)`, which results in `k = 1`.
   - Assign the value of `arr[2]` (which is 3) to `rotatedArr[1]`.
   - Result: `rotatedArr = [2, 3, 0, 0, 1]`

4. **Iteration 4 (i = 3)**:
   - Calculate the new index `k` using the formula `((3 - 1 + 5) % 5)`, which results in `k = 2`.
   - Assign the value of `arr[3]` (which is 4) to `rotatedArr[2]`.
   - Result: `rotatedArr = [2, 3, 4, 0, 1]`

5. **Iteration 5 (i = 4)**:
   - Calculate the new index `k` using the formula `((4 - 1 + 5) % 5)`, which results in `k = 3`.
   - Assign the value of `arr[4]` (which is 5) to `rotatedArr[3]`.
   - Result: `rotatedArr = [2, 3, 4, 5, 1]`

After all iterations, the `rotatedArr` becomes `[2, 3, 4, 5, 1]`, which represents the input array rotated to the left by one position. Each element of the original array is shifted one position to the left, and the last element wraps around to the beginning of the array.

Time Complexity:
- The time complexity of this implementation is O(n) because it iterates over each element of the input array once.

Space Complexity:
- The space complexity is also O(n) because it creates a new array of size `n` to store the rotated elements.

Optimization:
- The code can be optimized by removing the need for the `k` variable and calculating the new index directly within the assignment statement. Here's the optimized version:

```java
static int[] rotateArray(int[] arr, int n) {
    int[] rotatedArr = new int[n];
    for (int i = 0; i < n; i++) {
        rotatedArr[(i - 1 + n) % n] = arr[i];
    }
    return rotatedArr;
}
```

This optimization eliminates the need for the `k` variable, making the code cleaner and more concise.

[Rotate Array (Leetcode)](https://leetcode.com/problems/rotate-array/submissions/1243067790/)

Given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

Here's the pseudocode for the provided `rotate` method:

```sql
rotate(nums, k):
    Calculate the effective rotation count k = k % length of nums
    Calculate the index d where the array will be divided into two parts: d = length of nums - k
    
    Reverse the first part of the array from index 0 to d-1
    Reverse the second part of the array from index d to the end of the array
    Reverse the entire array
    
    The array nums is now rotated to the right by k positions
```

Java Code: 

```java
class Solution {
    public static void rev(int[] arr,int start,int end){
        while(start<end){
            int temp=arr[start];
            arr[start]=arr[end];
            arr[end]=temp;
            start++;
            end--;
        }
    }
    public void rotate(int[] nums, int k) {
        k=k%nums.length;
        int d=nums.length-k;
        rev(nums,0,d-1);
        rev(nums,d,nums.length-1);
        rev(nums,0,nums.length-1);
        
    }
}
```

Let's now go through the provided code with an example array `[1, 2, 3, 4, 5]`:

Given the input array `[1, 2, 3, 4, 5]` and assuming `k = 2`:

1. Calculate `k = 2 % 5 = 2` and `d = 5 - 2 = 3`.

2. Reverse the first part of the array from index 0 to d-1 (0 to 2):
   - Original: `[1, 2, 3, 4, 5]`
   - Reversed: `[3, 2, 1, 4, 5]`

3. Reverse the second part of the array from index d to the end of the array (3 to 4):
   - Original: `[3, 2, 1, 4, 5]`
   - Reversed: `[3, 2, 1, 5, 4]`

4. Reverse the entire array:
   - Original: `[3, 2, 1, 5, 4]`
   - Reversed: `[4, 5, 1, 2, 3]`

The array `[1, 2, 3, 4, 5]` is now rotated to the right by 2 positions, resulting in `[4, 5, 1, 2, 3]`.

Time Complexity:
- The time complexity of the `rotate` method is O(n), where n is the length of the input array `nums`. This is because the method performs three passes over the array, each of which takes linear time.

Space Complexity:
- The space complexity is O(1) because the method only uses a constant amount of extra space regardless of the size of the input array.

Optimization:
- The provided code is already optimized and performs the rotation efficiently in O(n) time with O(1) space complexity. Further optimization is not necessary for this problem.

**6. Left rotate the array by D places** 

Let's break down the provided code, first with pseudocode and then with an example.

Pseudocode:

```
rotateArray(arr, k):
    Iterate k times:
        Remove the first element from the ArrayList and store it in a variable first
        Add the removed element to the end of the ArrayList
    Return the modified ArrayList
```

Java Code:

```java
public class Solution {
	public static ArrayList<Integer> rotateArray(ArrayList<Integer> arr, int k) 
    {
        for(int i=0;i<k;i++)
        {
            int first = arr.remove(0);
            arr.add(first);
        }
       return arr; 
    }
}
```

Explanation with Example:

Consider the input ArrayList `arr = [1, 2, 3, 4, 5]` and `k = 2`.

1. **Iteration 1**:
   - Remove the first element (`1`) from the ArrayList.
   - Add the removed element (`1`) to the end of the ArrayList.
   - ArrayList after Iteration 1: `[2, 3, 4, 5, 1]`

2. **Iteration 2**:
   - Remove the first element (`2`) from the ArrayList.
   - Add the removed element (`2`) to the end of the ArrayList.
   - ArrayList after Iteration 2: `[3, 4, 5, 1, 2]`

The final ArrayList is `[3, 4, 5, 1, 2]`, which represents the input ArrayList `[1, 2, 3, 4, 5]` rotated to the left by 2 places.

**Time Complexity**: The time complexity of this code is O(k * n), where n is the size of the ArrayList. This is because the loop runs k times, and each iteration involves removing an element from the beginning of the ArrayList, which takes O(n) time due to shifting elements.

**Space Complexity**: The space complexity is O(1) because the code modifies the input ArrayList in place without using any additional space proportional to the size of the input.

**Optimization**:
- The current implementation has a time complexity of O(k * n), which can be inefficient for large values of k or large ArrayLists. To optimize, we can use the `%` operator to reduce the number of iterations in case k is larger than the size of the ArrayList. Additionally, we can use the `Collections.rotate()` method to achieve the same rotation in a single step, which may be more efficient.

Here's the optimized code using the `%` operator:

```java
public static ArrayList<Integer> rotateArray(ArrayList<Integer> arr, int k) {
    int n = arr.size();
    k = k % n; // Reduce k to the range [0, n)
    for (int i = 0; i < k; i++) {
        int first = arr.remove(0);
        arr.add(first);
    }
    return arr;
}
```

## 28-04-2024

**7. Move Zeros to end**

[Move Zeros to the end (CodeStudio)](https://www.naukri.com/code360/problems/ninja-and-the-zero-s_6581958?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

[Move Zeros to the end (LeetCode)](https://leetcode.com/problems/move-zeroes/description/)

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.

Example 1:
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]

This code is a solution to the problem of moving all zeros to the end of an array while preserving the relative order of non-zero elements.

Pseudocode:

```
function moveZeroes(nums):
    nonZero = 0  // Index for storing non-zero elements

    // Move all non-zero elements to the front
    for i from 0 to length of nums:
        if nums[i] is not zero:
            nums[nonZero] = nums[i]
            nonZero += 1

    // Fill the remaining elements with zeros
    while nonZero is less than length of nums:
        nums[nonZero] = 0
        nonZero += 1
```

Time Complexity: O(n), where n is the length of the input array. The algorithm iterates through the array once to move the non-zero elements and then again to fill the remaining positions with zeros.

Space Complexity: O(1), as the algorithm operates in-place on the input array without using any additional data structures that scale with the input size.

Example:

Let's consider the example `nums = [0, 1, 0, 3, 12]`.

Iteration 1 (i = 0):
- `nums[i]` is 0, so no action is taken.

Iteration 2 (i = 1):
- `nums[i]` is 1, a non-zero element.
- `nums[nonZero] = nums[i]`, so `nums[0] = 1`.
- `nonZero` is incremented to 1.

Iteration 3 (i = 2):
- `nums[i]` is 0, so no action is taken.

Iteration 4 (i = 3):
- `nums[i]` is 3, a non-zero element.
- `nums[nonZero] = nums[i]`, so `nums[1] = 3`.
- `nonZero` is incremented to 2.

Iteration 5 (i = 4):
- `nums[i]` is 12, a non-zero element.
- `nums[nonZero] = nums[i]`, so `nums[2] = 12`.
- `nonZero` is incremented to 3.

After the first loop, the array is `[1, 3, 12, 0, 0]`.

The `while` loop then fills the remaining positions with zeros:
- `nums[3] = 0` and `nums[4] = 0`.

The final array is `[1, 3, 12, 0, 0]`.

Java Code:

```java
public class Solution {
        public static int[] moveZeros(int n, int []a) 
        {
            int nonZero =0;
            for(int i=0;i<n;i++)
            {
                if(a[i] != 0)
                {
                   a[nonZero++] = a[i];
                }
            }
            while(nonZero < n)
            {
                a[nonZero++] = 0;
            }
            return a;
        }
}
```

Optimizations:

This solution is already optimal in terms of time and space complexity. However, there is a minor optimization that can be made to reduce the number of write operations:

```java
int lastNonZero = 0;
for (int i = 0; i < nums.length; i++) {
    if (nums[i] != 0) {
        int temp = nums[lastNonZero];
        nums[lastNonZero] = nums[i];
        nums[i] = temp;
        lastNonZero++;
    }
}
```

Instead of overwriting the elements one by one, this approach swaps the non-zero elements with the elements at the `lastNonZero` index. This way, each non-zero element is written to the array only once, reducing the number of write operations.

However, this optimization does not improve the overall time or space complexity of the algorithm, as it still requires iterating through the entire array once.

## 29-04-2024

**8. Linear search**

[Linear Search (CodeStudio)](https://www.naukri.com/code360/problems/linear-search_6922070?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

You are given an array ‘arr’ containing ‘n’ integers. You are also given an integer ‘num’, and your task is to find whether ‘num’ is present in the array or not.

If ‘num’ is present in the array, return the 0-based index of the first occurrence of ‘num’. Else, return -1.

Example:
Input: ‘n’ = 5, ‘num’ = 4 
'arr' =  [6,7,8,4,1] 

Output: 3

Explanation:
4 is present at the 3rd index.

Pseudocode:

```
function linearSearch(n, num, arr):
    sol = -1  // Initialize solution index to -1 (not found)

    // Iterate through the array
    for i from 0 to n-1:
        if arr[i] is equal to num:
            sol = i  // Found the element, update the solution index
            break    // Exit the loop since the element is found

    return sol  // Return the solution index
```

Time Complexity: O(n), where n is the size of the input array. In the worst case scenario, the algorithm will have to traverse the entire array to find the target element or determine that it is not present.

Space Complexity: O(1), as the algorithm uses a constant amount of extra space, regardless of the input size.

Example:

Let's consider the example where `n = 5`, `num = 3`, and `arr = [1, 5, 3, 7, 9]`.

Iteration 1 (i = 0):
- `arr[i]` is 1, which is not equal to `num` (3), so no action is taken.

Iteration 2 (i = 1):
- `arr[i]` is 5, which is not equal to `num` (3), so no action is taken.

Iteration 3 (i = 2):
- `arr[i]` is 3, which is equal to `num` (3).
- `sol` is updated to 2 (the index of the found element).
- The `break` statement is executed, and the loop terminates.

The function returns `sol = 2`, which is the index of the element 3 in the array.

Java Code:

```java
import java.util.*;
public class Solution {
    public static int linearSearch(int n, int num, int []arr)
    {
        int sol = -1;
        for(int i=0;i<n;i++)
        {
            if(arr[i]==num)
            {
                sol = i;
                break;
            }
        }
        return sol;
    }
}
```

Optimizations:

The Linear Search algorithm is already optimal for an unsorted array. However, if the array is sorted, you can use the Binary Search algorithm, which has a better time complexity of O(log n) on average. Binary Search works by repeatedly dividing the search interval in half until the target element is found or the remaining interval is empty.

Another optimization that can be applied in some cases is to stop the search if the target element is known to be absent. For example, if you're searching for an element in a sorted array, and the current element is greater than the target, you can stop the search immediately since the remaining elements will also be greater than the target.

Here's an optimized version of the Linear Search for a sorted array:

```java
public static int linearSearchSorted(int n, int num, int[] arr) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == num) {
            return i;  // Element found
        } else if (arr[i] > num) {
            return -1; // Element not found (array is sorted)
        }
    }
    return -1; // Element not found
}
```

In this optimized version, the loop breaks as soon as an element greater than the target is encountered, since the array is sorted, and the remaining elements will also be greater than the target.

**9. Find the union**

[Merge Two Sorted Arrays (CodeStudio)](https://www.naukri.com/code360/problems/sorted-array_6613259?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

Given two sorted arrays, ‘a’ and ‘b’, of size ‘n’ and ‘m’, respectively, return the union of the arrays.

The union of two sorted arrays can be defined as an array consisting of the common and the distinct elements of the two arrays. The final array should be sorted in ascending order.

Note: 'a' and 'b' may contain duplicate elements, but the union array must contain unique elements.

Example:
Input: ‘n’ = 5 ‘m’ = 3
‘a’ = [1, 2, 3, 4, 6]
‘b’ = [2, 3, 5]

Output: [1, 2, 3, 4, 5, 6]

Explanation: 
Common elements in ‘a’ and ‘b’ are: [2, 3]
Distinct elements in ‘a’ are: [1, 4, 6]
Distinct elements in ‘b’ are: [5]
Union of ‘a’ and ‘b’ is: [1, 2, 3, 4, 5, 6]

Pseudocode:

```
function sortedArray(a, b):
    sol = empty list
    m = length of a
    n = length of b
    i = 0  // Index for array a
    j = 0  // Index for array b

    // Merge elements from both arrays into sol
    while i is less than m and j is less than n:
        if a[i] is less than b[j]:
            if sol is empty or the last element in sol is not equal to a[i]:
                add a[i] to sol
            increment i
        else if a[i] is greater than b[j]:
            if sol is empty or the last element in sol is not equal to b[j]:
                add b[j] to sol
            increment j
        else:  // a[i] is equal to b[j]
            if sol is empty or the last element in sol is not equal to a[i]:
                add a[i] to sol
            increment i and j

    // Add remaining elements from array a to sol
    while i is less than m:
        if sol is empty or the last element in sol is not equal to a[i]:
            add a[i] to sol
        increment i

    // Add remaining elements from array b to sol
    while j is less than n:
        if sol is empty or the last element in sol is not equal to b[j]:
            add b[j] to sol
        increment j

    return sol
```

Time Complexity: O(m + n), where m and n are the lengths of the input arrays `a` and `b`, respectively. The algorithm iterates through both arrays once, performing a constant amount of work for each element.

Space Complexity: O(m + n), as the resulting list `sol` can contain up to `m + n` elements in the worst case when all elements are distinct.

Example:

Let's consider the example where `a = [1, 2, 3, 4, 5]` and `b = [3, 4, 5, 6, 7]`.

Iteration 1 (i = 0, j = 0):
- `a[i]` (1) is less than `b[j]` (3).
- `sol` is empty, so 1 is added to `sol`.
- `i` is incremented to 1.

Iteration 2 (i = 1, j = 0):
- `a[i]` (2) is less than `b[j]` (3).
- The last element in `sol` (1) is not equal to `a[i]` (2), so 2 is added to `sol`.
- `i` is incremented to 2.

Iteration 3 (i = 2, j = 0):
- `a[i]` (3) is equal to `b[j]` (3).
- The last element in `sol` (2) is not equal to `a[i]` (3), so 3 is added to `sol`.
- `i` and `j` are incremented to 3 and 1, respectively.

Iteration 4 (i = 3, j = 1):
- `a[i]` (4) is less than `b[j]` (4).
- The last element in `sol` (3) is not equal to `a[i]` (4), so 4 is added to `sol`.
- `i` is incremented to 4.

Iteration 5 (i = 4, j = 1):
- `a[i]` (5) is greater than `b[j]` (4).
- The last element in `sol` (4) is not equal to `b[j]` (4), so 4 is added to `sol`.
- `j` is incremented to 2.

Iteration 6 (i = 4, j = 2):
- `a[i]` (5) is equal to `b[j]` (5).
- The last element in `sol` (4) is not equal to `a[i]` (5), so 5 is added to `sol`.
- `i` and `j` are incremented to 5 and 3, respectively.

After the `while` loops, no more elements are left in `a` or `b`, so the final list `sol` is [1, 2, 3, 4, 5, 6, 7].

```java
import java.util.*;
public class Solution {
    public static List<Integer> sortedArray(int[] a, int[] b) {
        List<Integer> sol = new ArrayList<>();
        int m = a.length;
        int n = b.length;
        int i = 0, j = 0;

        while (i < m && j < n) {
            if (a[i] < b[j]) {
                if (sol.isEmpty() || sol.get(sol.size() - 1) != a[i]) {
                    sol.add(a[i]);
                }
                i++;
            } else if (a[i] > b[j]) {
                if (sol.isEmpty() || sol.get(sol.size() - 1) != b[j]) {
                    sol.add(b[j]);
                }
                j++;
            } else {
                if (sol.isEmpty() || sol.get(sol.size() - 1) != a[i]) {
                    sol.add(a[i]);
                }
                i++;
                j++;
            }
        }

        // Add remaining elements from array a
        while (i < m) {
            if (sol.isEmpty() || sol.get(sol.size() - 1) != a[i]) {
                sol.add(a[i]);
            }
            i++;
        }

        // Add remaining elements from array b
        while (j < n) {
            if (sol.isEmpty() || sol.get(sol.size() - 1) != b[j]) {
                sol.add(b[j]);
            }
            j++;
        }

        return sol;
    }
}
```

Optimizations:

This implementation is already optimized for time complexity, as it iterates through both input arrays only once. However, there is a potential optimization for space complexity.

Instead of creating a new list and adding elements to it, you can modify the input arrays in-place and then copy the distinct elements to a new array or list. This approach would reduce the space complexity to O(1) in the average case, where the number of distinct elements is much smaller than the total number of elements in the input arrays.

Here's an optimized version of the code that modifies the input arrays in-place:

```java
public static int[] sortedArray(int[] a, int[] b) {
    int m = a.length;
    int n = b.length;
    int i = 0, j = 0, k = 0;

    // Merge elements from both arrays into a
    while (i < m && j < n) {
        if (a[i] < b[j]) {
            a[k++] = a[i++];
        } else if (a[i] > b[j]) {
            a[k++] = b[j++];
        } else {
            a[k++] = a[i++];
            j++;
        }
    }

    // Add remaining elements from array a
    while (i < m) {
        a[k++] = a[i++];
    }

    // Add remaining elements from array b
    while (j < n) {
        a[k++] = b[j++];
    }

    // Create a new array with distinct elements
    int[] sol = new int[k];
    int prev = -1;
    int index = 0;
    for (int x : a) {
        if (x != prev) {
            sol[index++] = x;
            prev = x;
        }
    }

    return sol;
}
```

In this optimized version, the elements from both input arrays are merged into the `a` array in-place. Then, a new array `sol` is created with the distinct elements from `a`. The space complexity of this approach is O(1) in the average case when the number of distinct elements is much smaller than the total number of elements in the input arrays.

**10. Missing Number**

[Missing Number (Leetcode)](https://leetcode.com/problems/missing-number/description/)

Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.

Example 1:

Input: nums = [3,0,1]
Output: 2
Explanation: n = 3 since there are 3 numbers, so all numbers are in the range [0,3]. 2 is the missing number in the range since it does not appear in nums.
Example 2:

Input: nums = [0,1]
Output: 2
Explanation: n = 2 since there are 2 numbers, so all numbers are in the range [0,2]. 2 is the missing number in the range since it does not appear in nums.
Example 3:

Input: nums = [9,6,4,2,3,5,7,0,1]
Output: 8
Explanation: n = 9 since there are 9 numbers, so all numbers are in the range [0,9]. 8 is the missing number in the range since it does not appear in nums.

Pseudocode:

```
function missingNumber(nums):
    n = length of nums
    expectedSum = (n * (n + 1)) / 2  // Calculate the expected sum using the formula for the sum of the first n natural numbers
    actualSum = 0

    // Calculate the sum of all elements in the array
    for i from 0 to n - 1:
        actualSum += nums[i]

    solution = expectedSum - actualSum  // The missing number is the difference between the expected sum and the actual sum

    return solution
```

Time Complexity: O(n), where n is the length of the input array `nums`. The algorithm iterates through the array once to calculate the actual sum.

Space Complexity: O(1), as the algorithm uses a constant amount of extra space, regardless of the input size.

Example:

Let's consider the example where `nums = [3, 0, 1]`.

First, we calculate the length of the array:
```
n = 3
```

Then, we calculate the expected sum using the formula for the sum of the first n natural numbers:
```
expectedSum = (n * (n + 1)) / 2
            = (3 * (3 + 1)) / 2
            = 12 / 2
            = 6
```

Next, we initialize `actualSum` to 0 and iterate through the array to calculate the sum of its elements:

Iteration 1 (i = 0):
- `actualSum += nums[i]` => `actualSum = 0 + 3 = 3`

Iteration 2 (i = 1):
- `actualSum += nums[i]` => `actualSum = 3 + 0 = 3`

Iteration 3 (i = 2):
- `actualSum += nums[i]` => `actualSum = 3 + 1 = 4`

After the loop, `actualSum` is 4.

Finally, we calculate the missing number as the difference between the expected sum and the actual sum:
```
solution = expectedSum - actualSum
         = 6 - 4
         = 2
```

The missing number in the array `[3, 0, 1]` is 2.

Java code:

```java
class Solution {
    public int missingNumber(int[] nums) 
    {
        int n = nums.length;
        int expectedeSum = (n*(n+1)/2);
        int actualSum = 0;
        for(int i=0;i<n;i++)
        {
            actualSum += nums[i];
        }
        int solution = expectedeSum-actualSum;
        return solution;
    }
}
```

Optimizations:

This solution is already optimal in terms of time complexity, as it iterates through the array only once. However, there is an alternative approach using the XOR operation that can achieve the same time complexity without using the formula for the sum of the first n natural numbers.

Here's the optimized version using XOR:

```java
public int missingNumber(int[] nums) {
    int n = nums.length;
    int xor = 0;

    // Calculate the XOR of all numbers from 0 to n
    for (int i = 0; i <= n; i++) {
        xor ^= i;
    }

    // Calculate the XOR of all numbers in the array
    for (int num : nums) {
        xor ^= num;
    }

    return xor;
}
```

In this approach, we use the XOR operation to cancel out the numbers that are present in both the range `[0, n]` and the input array `nums`. The remaining number after performing the XOR operation will be the missing number.

The time complexity of this approach is still O(n), as it iterates through the array once and performs a constant amount of work for each element. However, it avoids the use of the formula for the sum of the first n natural numbers, which may be more efficient in some cases.

**11. Maximum Consecutive Ones**

[Maximum Consecutive Ones (CodeStudio)](https://www.naukri.com/code360/problems/traffic_6682625?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)


Pseudocode:

```
function traffic(n, m, vehicle):
    maxConsecutive = 0  // Initialize the maximum consecutive vehicles count
    zerosCount = 0  // Initialize the count of consecutive zeros
    left = 0  // Initialize the left pointer of the sliding window

    // Iterate through the vehicle array using a sliding window
    for right from 0 to n - 1:
        if vehicle[right] is 0:
            zerosCount += 1  // Increment the consecutive zeros count

        // Shrink the window if the number of zeros exceeds m
        while zerosCount > m:
            if vehicle[left] is 0:
                zerosCount -= 1  // Decrement the consecutive zeros count
            left += 1  // Move the left pointer to shrink the window

        // Update the maximum consecutive vehicles count
        maxConsecutive = max(maxConsecutive, right - left + 1)

    return maxConsecutive
```

Time Complexity: O(n), where n is the length of the input array `vehicle`. The algorithm iterates through the array once using a sliding window approach.

Space Complexity: O(1), as the algorithm uses a constant amount of extra space, regardless of the input size.

Example:

Let's consider the example where `n = 6`, `m = 2`, and `vehicle = [1, 1, 0, 0, 1, 0]`.

Iteration 1 (right = 0):
- `vehicle[right]` is 1, so no action is taken.
- `maxConsecutive` is updated to 1 (right - left + 1 = 0 - 0 + 1 = 1).

Iteration 2 (right = 1):
- `vehicle[right]` is 1, so no action is taken.
- `maxConsecutive` is updated to 2 (right - left + 1 = 1 - 0 + 1 = 2).

Iteration 3 (right = 2):
- `vehicle[right]` is 0, so `zerosCount` is incremented to 1.
- `maxConsecutive` is updated to 3 (right - left + 1 = 2 - 0 + 1 = 3).

Iteration 4 (right = 3):
- `vehicle[right]` is 0, so `zerosCount` is incremented to 2.
- Since `zerosCount` is now equal to `m` (2), no shrinking of the window is needed.
- `maxConsecutive` is updated to 4 (right - left + 1 = 3 - 0 + 1 = 4).

Iteration 5 (right = 4):
- `vehicle[right]` is 1, so no action is taken.
- `maxConsecutive` is updated to 5 (right - left + 1 = 4 - 0 + 1 = 5).

Iteration 6 (right = 5):
- `vehicle[right]` is 0, so `zerosCount` is incremented to 3.
- Since `zerosCount` is now greater than `m` (2), the window needs to be shrunk.
- `vehicle[left]` is 1, so no decrement of `zerosCount` is needed.
- `left` is incremented to 1.
- `maxConsecutive` is updated to 4 (right - left + 1 = 5 - 1 + 1 = 5).

After the loop, the function returns `maxConsecutive = 5`, which is the maximum number of consecutive vehicles that can pass through the toll bridge.

Java code:

```java
public class Solution {
    public static int traffic(int n, int m, int []vehicle) 
    {
        int maxConsecutive = 0;
        int zerosCount = 0;
        int left = 0;
        
        for (int right = 0; right < n; right++) {
            
            if (vehicle[right] == 0) {
                zerosCount++;
            }
            
            // Shrink the window if the number of zeros exceeds M
            while (zerosCount > m) {
                if (vehicle[left] == 0) {
                    zerosCount--;
                }
                left++;
            }
            
            // Update the maximum consecutive vehicles count
            maxConsecutive = Math.max(maxConsecutive, right - left + 1);
        }
        
        return maxConsecutive;
    }
}
```

Optimizations:

This implementation is already optimized for both time and space complexity. However, there is a minor optimization that can be made to avoid unnecessary updates to `maxConsecutive` when the window size decreases.

Here's the optimized version:

```java
public static int traffic(int n, int m, int[] vehicle) {
    int maxConsecutive = 0;
    int zerosCount = 0;
    int left = 0;
    int windowSize = 0;  // Keep track of the current window size

    for (int right = 0; right < n; right++) {
        if (vehicle[right] == 0) {
            zerosCount++;
        }

        // Shrink the window if the number of zeros exceeds m
        while (zerosCount > m) {
            if (vehicle[left] == 0) {
                zerosCount--;
            }
            left++;
            windowSize--;  // Decrement the window size
        }

        windowSize++;  // Increment the window size
        maxConsecutive = Math.max(maxConsecutive, windowSize);
    }

    return maxConsecutive;
}
```

In this optimized version, we keep track of the current window size using the `windowSize` variable. We increment `windowSize` when the right pointer moves forward, and decrement it when the left pointer moves forward. We update `maxConsecutive` only when `windowSize` is greater than the current value of `maxConsecutive`.

This optimization avoids unnecessary updates to `maxConsecutive` when the window size decreases, potentially improving the performance for certain input cases.

[Max Consecutive Ones (Leetcode)](https://leetcode.com/problems/max-consecutive-ones/description/)

Given a binary array nums, return the maximum number of consecutive 1's in the array.

Example 1:
Input: nums = [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.

Example 2:
Input: nums = [1,0,1,1,0,1]
Output: 2

Pseudocode:

```
function findMaxConsecutiveOnes(nums):
    maxCount = 0  // Initialize the maximum count of consecutive 1's
    curCount = 0  // Initialize the current count of consecutive 1's

    // Iterate through each element in the array
    for each element in nums:
        if element is 0:
            // Update the maxCount if the current count is greater
            maxCount = max(maxCount, curCount)
            // Reset the current count to 0
            curCount = 0
        else:
            // Increment the current count
            curCount += 1

    // After the loop, compare the final current count with the maximum count
    // and return the larger value
    return max(maxCount, curCount)
```

Time Complexity: O(n), where n is the length of the input array `nums`. The algorithm iterates through the array once.

Space Complexity: O(1), as the algorithm uses a constant amount of extra space, regardless of the input size.

Example:

Let's consider the example where `nums = [1, 1, 0, 1, 1, 1]`.

Iteration 1 (element = 1):
- `element` (1) is not 0, so `curCount` is incremented to 1.
- `maxCount` remains 0.

Iteration 2 (element = 1):
- `element` (1) is not 0, so `curCount` is incremented to 2.
- `maxCount` remains 0.

Iteration 3 (element = 0):
- `element` is 0, so `maxCount` is updated to 2 (the maximum of 0 and 2).
- `curCount` is reset to 0.

Iteration 4 (element = 1):
- `element` (1) is not 0, so `curCount` is incremented to 1.
- `maxCount` remains 2.

Iteration 5 (element = 1):
- `element` (1) is not 0, so `curCount` is incremented to 2.
- `maxCount` remains 2.

Iteration 6 (element = 1):
- `element` (1) is not 0, so `curCount` is incremented to 3.
- `maxCount` remains 2.

After the loop, `maxCount` is compared with the final `curCount` (3), and the maximum value (3) is returned.

The function returns `3`, which is the maximum count of consecutive 1's in the array `[1, 1, 0, 1, 1, 1]`.

Java Code:

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums)
    {
        // Initialize variables to track the maximum count and current count of consecutive 1s
        int maxCount=0;
        int curCount=0;

        // Iterate through each element in the array
        for(int element: nums){
            if(element==0){
        //reset curCount and maxCount whenever 0 is encountered.
                if(maxCount<curCount){
                    maxCount=curCount;
                }
                curCount=0;                
            }
            else{
                curCount++;
            }
        }
        // After the loop, compare the final current count with the maximum count and return the larger value
        return maxCount>curCount? maxCount:curCount;
        
    }
}
```

Optimizations:

This implementation is already optimized for both time and space complexity. However, there is a potential optimization that can be made to simplify the code and make it more readable:

```java
public int findMaxConsecutiveOnes(int[] nums) {
    int maxCount = 0;
    int currentCount = 0;

    for (int num : nums) {
        if (num == 1) {
            currentCount++;
            maxCount = Math.max(maxCount, currentCount);
        } else {
            currentCount = 0;
        }
    }

    return maxCount;
}
```

In this optimized version, we don't need to update `maxCount` inside the loop when we encounter a 0. Instead, we reset `currentCount` to 0 whenever we encounter a 0 in the array, and update `maxCount` only when we encounter a 1. This simplifies the code and makes it more readable without changing the time or space complexity.

Another potential optimization is to use bit manipulation instead of iterating through the array. However, this optimization is only suitable when the input array is large and dense (contains many consecutive 1's), and it may not be more efficient for small or sparse arrays.

## 30-04-2024

**12. Find the number that appears once, and other numbers twice**

[Find the number that appears once, and other numbers twice (CodeStudio)](https://www.naukri.com/code360/problems/find-the-single-element_6680465?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

[Find the number that appears once, and other numbers twice(Leetcode)](https://leetcode.com/problems/single-number/)

You are given a sorted array 'arr' of positive integers of size 'n'.

It contains each number exactly twice except for one number, which occurs exactly once.

Find the number that occurs exactly once.

Example :
Input: ‘arr’ = {1, 1, 2, 3, 3, 4, 4}.
Output: 2

Explanation: 1, 3, and 4 occur exactly twice. 2 occurs exactly once. Hence the answer is 2.

Pseudocode:

```
function getSingleElement(arr):
    sol = 0  // Initialize the solution variable

    // Iterate through the array
    for each element in arr:
        sol = sol XOR element  // Apply the XOR operation

    return sol
```

Time Complexity: O(n), where n is the length of the input array `arr`. The algorithm iterates through the array once.

Space Complexity: O(1), as the algorithm uses a constant amount of extra space, regardless of the input size.

Explanation with an example:

Let's consider the example where `arr = [1, 2, 2, 3, 1]`.

Iteration 1 (i = 0):
- `sol = 0 ^ 1 = 1`

Iteration 2 (i = 1):
- `sol = 1 ^ 2 = 3`

Iteration 3 (i = 2):
- `sol = 3 ^ 2 = 1`

Iteration 4 (i = 3):
- `sol = 1 ^ 3 = 2`

Iteration 5 (i = 4):
- `sol = 2 ^ 1 = 3`

After the loop, `sol` contains the value 3, which is the single element in the array `[1, 2, 2, 3, 1]`.

The XOR operation has the following properties:

1. `x ^ 0 = x` (Identity property)
2. `x ^ x = 0` (Idempotent property)
3. `x ^ y = y ^ x` (Commutative property)

In this solution, we use the XOR operation to cancel out the duplicates in the array. When we XOR a number with itself, the result is 0 (due to the idempotent property). Since all elements except one appear twice, their XOR operations will cancel out, leaving us with the single element.

Optimizations:

This implementation is already optimized for both time and space complexity. However, there is a potential optimization that can be made if the input array is sorted.

If the array is sorted, we can skip the XOR operation for consecutive duplicate elements, as their XOR will always be 0. This optimization can potentially improve the performance for certain input cases.

Here's the optimized version for a sorted array:

```java
public static int getSingleElement(int[] arr) {
    int sol = 0;
    int i = 0;

    while (i < arr.length) {
        sol ^= arr[i];
        i += 1;  // Skip the next element if it's a duplicate
    }

    return sol;
}
```

In this optimized version, we iterate through the array using a `while` loop instead of a `for` loop. We XOR the current element with `sol` and then increment the index `i` by 2 if the next element is a duplicate (which is guaranteed by the sorted nature of the array).

This optimization can potentially improve the performance for input arrays with large consecutive duplicates, as it reduces the number of XOR operations performed.

However, it's important to note that this optimization assumes that the input array is sorted. If the array is not sorted, this optimization may not provide any performance benefits and could even degrade the performance due to the additional checks required.

**13. Longest subarray with given sum K (positives)**

You are given an array 'a' of size 'n' and an integer 'k'.

Find the length of the longest subarray of 'a' whose sum is equal to 'k'.

Example :
Input: ‘n’ = 7 ‘k’ = 3
‘a’ = [1, 2, 3, 1, 1, 1, 1]

Output: 3

Explanation: Subarrays whose sum = ‘3’ are:

[1, 2], [3], [1, 1, 1] and [1, 1, 1]

Here, the length of the longest subarray is 3, which is our final answer.

Pseudocode:

```
function longestSubarrayWithSumK(a, k):
    left = 0  // Initialize the left pointer
    right = 0  // Initialize the right pointer
    max = 0  // Initialize the maximum length of the subarray
    sum = 0  // Initialize the running sum

    // Iterate through the array using the two-pointer technique
    while right is less than the length of a:
        sum += a[right]  // Add the current element to the running sum
        right += 1  // Move the right pointer forward

        // Shrink the subarray from the left side until the sum is less than or equal to k
        while sum > k:
            sum -= a[left]  // Subtract the leftmost element from the running sum
            left += 1  // Move the left pointer forward

        // If the sum is equal to k, update the maximum length
        if sum is equal to k:
            max = max(max, right - left)

    return max
```

Time Complexity: O(n), where n is the length of the input array `a`. The algorithm iterates through the array once using the two-pointer technique.

Space Complexity: O(1), as the algorithm uses a constant amount of extra space, regardless of the input size.

Example:

Let's consider the example where `a = [1, 2, 3, 4, 5]` and `k = 9`.

Iteration 1 (left = 0, right = 0):
- `sum = 0 + a[0] = 1`
- Since `sum` (1) is not greater than `k` (9), no shrinking of the subarray is needed.
- `max` remains 0.

Iteration 2 (left = 0, right = 1):
- `sum = 1 + a[1] = 3`
- Since `sum` (3) is not greater than `k` (9), no shrinking of the subarray is needed.
- `max` remains 0.

Iteration 3 (left = 0, right = 2):
- `sum = 3 + a[2] = 6`
- Since `sum` (6) is not greater than `k` (9), no shrinking of the subarray is needed.
- `max` remains 0.

Iteration 4 (left = 0, right = 3):
- `sum = 6 + a[3] = 10`
- Since `sum` (10) is greater than `k` (9), the subarray needs to be shrunk from the left side.
- `sum = 10 - a[0] = 9`
- Since `sum` (9) is equal to `k` (9), `max` is updated to 3 (right - left = 3 - 0 = 3).

Iteration 5 (left = 1, right = 4):
- `sum = 9 + a[4] = 14`
- Since `sum` (14) is greater than `k` (9), the subarray needs to be shrunk from the left side.
- `sum = 14 - a[1] = 12`
- Since `sum` (12) is greater than `k` (9), the subarray needs to be shrunk again from the left side.
- `sum = 12 - a[2] = 9`
- Since `sum` (9) is equal to `k` (9), `max` is updated to 3 (right - left = 4 - 2 = 2), but the previous value of 3 is larger, so `max` remains 3.

After the loop, the function returns `max = 3`, which is the length of the longest subarray whose sum is equal to `k` (9).

```java
public class Solution {
    public static int longestSubarrayWithSumK(int []a, long k) {
        int left = 0, right = 0, max = 0;
        long sum = 0;
        while(right < a.length){
            sum += a[right++];
            while(sum > k){
                sum -= a[left++];
            }
            if(sum == k) max = Math.max(max, right - left);
        }
        return max;
    }
}
```

Optimizations:

This implementation is already optimized for both time and space complexity. However, there is a potential optimization that can be made using a hash table (or a dictionary in Python) to store the cumulative sums seen so far. This optimization can improve the time complexity for certain input cases.

Here's the optimized version using a hash table:

```java
public static int longestSubarrayWithSumK(int[] a, long k) {
    int max = 0;
    long sum = 0;
    Map<Long, Integer> sumToIndex = new HashMap<>();
    sumToIndex.put(0, -1); // Initialize the hash table with 0 sum at index -1

    for (int i = 0; i < a.length; i++) {
        sum += a[i];

        // If the current sum is equal to k, update the maximum length
        if (sum == k) {
            max = Math.max(max, i + 1);
        } else {
            // Check if (sum - k) exists in the hash table
            long remaining = sum - k;
            if (sumToIndex.containsKey(remaining)) {
                max = Math.max(max, i - sumToIndex.get(remaining));
            }
        }

        // Store the current sum and its index in the hash table
        if (!sumToIndex.containsKey(sum)) {
            sumToIndex.put(sum, i);
        }
    }

    return max;
}
```

In this optimized version, we use a hash table `sumToIndex` to store the cumulative sums seen so far and their indices. We initialize the hash table with a sum of 0 at index -1, which allows us to handle the case where the target sum `k` itself is present as a subarray.

For each element in the array, we update the running sum `sum` and check if it is equal to `k`. If it is, we update the maximum length. Otherwise, we check if `(sum - k)` exists in the hash table, which means that the subarray starting from the index corresponding to `(sum - k)` and ending at the current index has a sum equal to `k`. If `(sum - k)` exists in the hash table, we update the maximum length accordingly.

Finally, we store the current sum and its index in the hash table for future use.

The time complexity of this optimized solution is O(n), where n is the length of the input array `a`, as we iterate through the array once. However, the additional operations involving the hash table may add some overhead, making this optimization more effective for larger input arrays or arrays with many subarrays that satisfy the target sum condition.

The space complexity of this optimized solution is O(n) in the worst case, where all the elements in the array are distinct, and we need to store all the cumulative sums in the hash table.

But there seems to be a problem with the optimsed code. 

**14. Longest subarray with sum K (Positives + Negatives)**

[Longest subarray with sum K (Positives + Negatives)](https://www.naukri.com/code360/problems/longest-subarray-with-sum-k_5713505?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=SUBMISSION)

Ninja and his friend are playing a game of subarrays. They have an array ‘NUMS’ of length ‘N’. Ninja’s friend gives him an arbitrary integer ‘K’ and asks him to find the length of the longest subarray in which the sum of elements is equal to ‘K’.

Ninjas asks for your help to win this game. Find the length of the longest subarray in which the sum of elements is equal to ‘K’.

If there is no subarray whose sum is ‘K’ then you should return 0.

Example:
Input: ‘N’ = 5,  ‘K’ = 4, ‘NUMS’ = [ 1, 2, 1, 0, 1 ]

Output: 4

There are two subarrays with sum = 4, [1, 2, 1] and [2, 1, 0, 1]. Hence the length of the longest subarray with sum = 4 is 4.

Pseudocode:

```
function getLongestSubarray(nums, k):
    map = new HashMap  // Create an empty hash map
    map.put(0, -1)  // Initialize the hash map with sum 0 at index -1

    sum = 0  // Initialize the running sum
    max = 0  // Initialize the maximum length of the subarray

    // Iterate through the array
    for i from 0 to length of nums:
        sum += nums[i]  // Update the running sum

        // If (sum - k) exists in the hash map, update the maximum length
        if map contains (sum - k):
            max = max(max, i - map.get(sum - k))

        // Store the current sum and its index in the hash map
        if map does not contain sum:
            map.put(sum, i)

    return max
```

Time Complexity: O(n), where n is the length of the input array `nums`. The algorithm iterates through the array once, and the operations on the hash map take constant time on average.

Space Complexity: O(n), in the worst case where all the elements in the array are distinct, and we need to store all the cumulative sums in the hash map.

Example:

Let's consider the example where `nums = [1, 2, 3, 4, 5]` and `k = 9`.

Iteration 1 (i = 0):
- `sum = 0 + nums[0] = 1`
- `map` does not contain `(sum - k) = 1 - 9 = -8`, so no update to `max`.
- `map` does not contain `sum = 1`, so `map.put(1, 0)` is executed.

Iteration 2 (i = 1):
- `sum = 1 + nums[1] = 3`
- `map` does not contain `(sum - k) = 3 - 9 = -6`, so no update to `max`.
- `map` does not contain `sum = 3`, so `map.put(3, 1)` is executed.

Iteration 3 (i = 2):
- `sum = 3 + nums[2] = 6`
- `map` does not contain `(sum - k) = 6 - 9 = -3`, so no update to `max`.
- `map` does not contain `sum = 6`, so `map.put(6, 2)` is executed.

Iteration 4 (i = 3):
- `sum = 6 + nums[3] = 10`
- `map` contains `(sum - k) = 10 - 9 = 1`, so `max` is updated to 3 (i - map.get(1) = 3 - 0 = 3).
- `map` does not contain `sum = 10`, so `map.put(10, 3)` is executed.

Iteration 5 (i = 4):
- `sum = 10 + nums[4] = 15`
- `map` does not contain `(sum - k) = 15 - 9 = 6`, so no update to `max`.
- `map` does not contain `sum = 15`, so `map.put(15, 4)` is executed.

After the loop, the function returns `max = 3`, which is the length of the longest subarray whose sum is equal to `k` (9).

Optimizations:

This implementation is already optimized for time and space complexity by using a hash map to store the cumulative sums and their indices. However, there is a potential optimization that can be made to handle negative values in the input array more efficiently.

If the input array contains negative values, the cumulative sum can become negative, which means we need to store negative keys in the hash map. However, hash maps in Java (and most programming languages) do not handle negative keys efficiently, as they are typically implemented using arrays or other data structures that require non-negative indices.

To handle negative values more efficiently, we can use a technique called "remapping" or "offset mapping." The idea is to add a constant offset to all the cumulative sums, making them non-negative, and then store these remapped sums in the hash map.

Here's the optimized version with remapping:

```java
public static int getLongestSubarray(int[] nums, int k) {
    int max = 0;
    int sum = 0;
    int minSum = 0; // Keep track of the minimum cumulative sum
    HashMap<Integer, Integer> map = new HashMap<>();
    map.put(0, -1); // Initialize the hash map with sum 0 at index -1

    for (int i = 0; i < nums.length; i++) {
        sum += nums[i];
        int remappedSum = sum - minSum; // Remap the cumulative sum by subtracting the minimum sum

        if (map.containsKey(remappedSum - k)) {
            max = Math.max(max, i - map.get(remappedSum - k));
        }

        if (!map.containsKey(remappedSum)) {
            map.put(remappedSum, i);
        }

        minSum = Math.min(minSum, sum); // Update the minimum cumulative sum
    }

    return max;
}
```

In this optimized version, we keep track of the minimum cumulative sum `minSum` seen so far. Before storing the cumulative sum in the hash map or checking for `(sum - k)`, we remap the cumulative sum by subtracting `minSum` from it. This remapping ensures that all the keys in the hash map are non-negative, even if the input array contains negative values.

The time complexity of this optimized solution remains O(n), where n is the length of the input array `nums`. The space complexity is also O(n) in the worst case, where all the elements in the array are distinct, and we need to store all the remapped cumulative sums in the hash map.

This optimization can improve the performance of the algorithm, especially when the input array contains negative values and the cumulative sums have a wide range.

**15. Two Sum**

[Two Sum (CodeStudio)](https://www.naukri.com/code360/problems/reading_6845742?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

Sam want to read exactly ‘TARGET’ number of pages.

He has an array ‘BOOK’ containing the number of pages for ‘N’ books.

Return YES/NO, if it is possible for him to read any 2 books and he can meet his ‘TARGET’ number of pages.

Example:
Input: ‘N’ = 5, ‘TARGET’ = 5
‘BOOK’ = [4, 1, 2, 3, 1] 

Output: YES
Explanation:
Sam can buy 4 pages book and 1 page book.

This code is a Java implementation to check if there exists a pair of numbers in the given array `book` whose sum is equal to the target value `target`.

Pseudocode:

```
function read(n, book, target):
    a = "NO"  // Initialize the result string to "NO"

    // Iterate through all possible pairs in the array
    for i from 0 to n-2:
        for j from i+1 to n-1:
            // Check if the sum of the current pair is equal to the target
            if book[i] + book[j] is equal to target:
                a = "YES"  // If a pair is found, update the result string to "YES"

    return a
```

Time Complexity: O(n^2), where n is the length of the input array `book`. The algorithm uses nested loops to iterate through all possible pairs of elements, resulting in a quadratic time complexity.

Space Complexity: O(1), as the algorithm uses a constant amount of extra space, regardless of the input size.

Example:

Let's consider the example where `n = 4`, `book = [1, 2, 3, 4]`, and `target = 5`.

Iteration 1 (i = 0, j = 1):
- `book[i] + book[j]` is `1 + 2 = 3`, which is not equal to `target` (5).

Iteration 2 (i = 0, j = 2):
- `book[i] + book[j]` is `1 + 3 = 4`, which is not equal to `target` (5).

Iteration 3 (i = 0, j = 3):
- `book[i] + book[j]` is `1 + 4 = 5`, which is equal to `target` (5).
- `a` is updated to "YES".

Since a pair (1, 4) is found whose sum is equal to the target, the function will return "YES" without completing the remaining iterations.

```java
public class Solution {
    public static String read(int n, int []book, int target)
    {
        String a = "NO";
        for (int i=0;i<n-1;i++)
        {
            for(int j=1;j<n;j++)
            {
                if(book[i]+book[j]== target)
                {
                    a = "YES";
                }
            }
        } 
       return a;
    }
}
```

Optimizations:

This implementation has a quadratic time complexity, which can be inefficient for large input arrays. We can optimize the solution by using a more efficient algorithm, such as the two-pointer technique or a hash table-based approach.

Here's an optimized version using the two-pointer technique:

```java
public static String read(int n, int[] book, int target) {
    Arrays.sort(book); // Sort the array in ascending order
    int left = 0;
    int right = n - 1;

    while (left < right) {
        int sum = book[left] + book[right];
        if (sum == target) {
            return "YES";
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }

    return "NO";
}
```

In this optimized version, we first sort the input array `book` in ascending order. Then, we use two pointers, `left` and `right`, to iteratively check if the sum of the elements at the two pointers is equal to the target.

If the sum is equal to the target, we return "YES" immediately.
If the sum is less than the target, we increment the `left` pointer to increase the sum.
If the sum is greater than the target, we decrement the `right` pointer to decrease the sum.
We repeat these steps until the `left` pointer crosses the `right` pointer, at which point all possible pairs have been checked.

The time complexity of this optimized solution is O(n log n) due to the sorting step, where n is the length of the input array `book`. The sorting step takes O(n log n) time, and the two-pointer iteration takes O(n) time in the average case.

The space complexity of this optimized solution is O(1), as it uses a constant amount of extra space, regardless of the input size.

This optimization significantly improves the time complexity compared to the original solution, especially for large input arrays.

[Two Sum (Leetcode)](https://leetcode.com/problems/two-sum/description/)

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

Example 1:

Input: 

nums = [2,7,11,15], target = 9

Output: [0,1]

Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:

Input: nums = [3,2,4], target = 6

Output: [1,2]

Example 3:

Input: nums = [3,3], target = 6

Output: [0,1]

This code is a Java implementation of the "Two Sum" problem, which aims to find two numbers in an array that add up to a given target value, and return their indices.

Pseudocode:

```
function twoSum(nums, target):
    for i from 0 to length of nums - 1:
        for j from i + 1 to length of nums - 1:
            if nums[i] + nums[j] is equal to target:
                return [i, j]  // Return the indices of the two numbers

    return []  // If no two numbers sum up to the target, return an empty array
```

Time Complexity: O(n^2), where n is the length of the input array `nums`. The algorithm uses nested loops, resulting in a quadratic time complexity.

Space Complexity: O(1), as the algorithm uses a constant amount of extra space, regardless of the input size.

Example:

Let's consider the example where `nums = [2, 7, 11, 15]` and `target = 9`.

Iteration 1 (i = 0, j = 1):
- `nums[i] + nums[j]` is `2 + 7 = 9`, which is equal to `target` (9).
- The function returns `[0, 1]`, which are the indices of the two numbers (2 and 7).

Since a pair of numbers (2 and 7) is found whose sum is equal to the target, the function will return `[0, 1]` without completing the remaining iterations.

```java
class Solution {
    public int[] twoSum(int[] nums, int target) 
    {
        for (int i=0 ; i < nums.length ; i++)
        {
            for (int j=i+1 ; j < nums.length ; j++)
            {
                if (nums[i] + nums[j] == target)
                {
                    return new int[]{i,j};
                }
                
            }
        }
        return new int[]{};
    }
}
```

Optimizations:

This implementation has a quadratic time complexity, which can be inefficient for large input arrays. We can optimize the solution by using a hash table (or dictionary in Python) to achieve a time complexity of O(n).

Here's the optimized code:

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> numMap = new HashMap<>();

        // Iterate through the array
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];

            // Check if the complement exists in the map
            if (numMap.containsKey(complement)) {
                // Return the indices of the two numbers
                return new int[] { numMap.get(complement), i };
            }

            // Store the current number and its index in the map
            numMap.put(nums[i], i);
        }

        // No two sum solution found
        return new int[] {};
    }
}
```

In this optimized version, we use a hash map `numMap` to store the numbers and their indices. We iterate through the array `nums` and for each element `nums[i]`, we calculate the complement `complement = target - nums[i]`. If the complement exists in the `numMap`, it means we have found a pair of numbers whose sum is equal to the target, and we return their indices. Otherwise, we store the current number `nums[i]` and its index `i` in the `numMap`.

The time complexity of this optimized solution is O(n), where n is the length of the input array `nums`. This is because we iterate through the array once, and the operations on the hash map (insertion and lookup) take constant time on average.

The space complexity is O(n) in the worst case, where all the elements in the array are distinct, and we need to store all of them in the hash map.

The optimized solution is more efficient than the brute force approach, especially for large input arrays, as it avoids the nested loop and performs better time-wise.