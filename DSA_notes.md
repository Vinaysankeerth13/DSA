# Data Structures and Algorithms

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

**Largest Element in the Array**

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

**Second Smallest Number without sorting**

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

