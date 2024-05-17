# Data Structures and Algorithms

## Note :

The optimisation code for each problem is given by AI, so there might be a possibility that they're not an exact fit for the problem you're solving. Please bear that in mind and modify the code implementing the concepts that are provided for optimisation.

## 25-04-20242

**Selection Sort**

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

**Bubble Sort**

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

**Recursive Bubble sort**

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

**Insertion Sort**

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

**Recursive Insertion Sort**

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

**Merge Sort**

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

**Quick Sort**

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

**Time Complexity**: The time complexity of this code is O(k \* n), where n is the size of the ArrayList. This is because the loop runs k times, and each iteration involves removing an element from the beginning of the ArrayList, which takes O(n) time due to shifting elements.

**Space Complexity**: The space complexity is O(1) because the code modifies the input ArrayList in place without using any additional space proportional to the size of the input.

**Optimization**:

- The current implementation has a time complexity of O(k \* n), which can be inefficient for large values of k or large ArrayLists. To optimize, we can use the `%` operator to reduce the number of iterations in case k is larger than the size of the ArrayList. Additionally, we can use the `Collections.rotate()` method to achieve the same rotation in a single step, which may be more efficient.

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
'arr' = [6,7,8,4,1]

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
Input: ‘N’ = 5, ‘K’ = 4, ‘NUMS’ = [ 1, 2, 1, 0, 1 ]

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

## Medium

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

## 1-05-2024

**16. Sort An Array of 0s, 1s and 2s**

[Sort An Array of 0s, 1s and 2s (CodeStudio)](https://www.naukri.com/code360/problems/sort-an-array-of-0s-1s-and-2s_892977?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

[Sort Colors (Leetcode)](https://leetcode.com/problems/sort-colors/description/)

You have been given an array/list 'arr' consisting of 'n' elements.

Each element in the array is either 0, 1 or 2.

Sort this array/list in increasing order.

Do not make a new array/list. Make changes in the given array/list.

Example :
Input: 'arr' = [2, 2, 2, 2, 0, 0, 1, 0]

Output: Final 'arr' = [0, 0, 0, 1, 2, 2, 2, 2]

Explanation: The array is sorted in increasing order.

Pseudocode:

```
function sortArray(arr, n):
    mid = 0  // Initialize the mid pointer
    low = 0  // Initialize the low pointer
    high = n - 1  // Initialize the high pointer

    for i from 0 to n - 1:
        if arr[mid] is 0:
            swap arr[mid] with arr[low]
            increment mid and low

        else if arr[mid] is 1:
            increment mid

        else:  // arr[mid] is 2
            swap arr[mid] with arr[high]
            decrement high
```

Time Complexity: O(n), where n is the length of the input array `arr`. The algorithm iterates through the array once.

Space Complexity: O(1), as the algorithm uses a constant amount of extra space, regardless of the input size.

Example:

Let's consider the example where `arr = [0, 1, 2, 0, 1, 2]` and `n = 6`.

Iteration 1 (i = 0, mid = 0, low = 0, high = 5):

- `arr[mid]` is 0.
- Swap `arr[mid]` (0) with `arr[low]` (0), so no actual swap is performed.
- Increment `mid` to 1 and `low` to 1.

Iteration 2 (i = 1, mid = 1, low = 1, high = 5):

- `arr[mid]` is 1.
- Increment `mid` to 2.

Iteration 3 (i = 2, mid = 2, low = 1, high = 5):

- `arr[mid]` is 2.
- Swap `arr[mid]` (2) with `arr[high]` (2), so no actual swap is performed.
- Decrement `high` to 4.

Iteration 4 (i = 3, mid = 3, low = 1, high = 4):

- `arr[mid]` is 0.
- Swap `arr[mid]` (0) with `arr[low]` (1), so the array becomes `[0, 1, 2, 1, 2, 0]`.
- Increment `mid` to 4 and `low` to 2.

Iteration 5 (i = 4, mid = 4, low = 2, high = 4):

- `arr[mid]` is 1.
- Increment `mid` to 5.

Iteration 6 (i = 5, mid = 5, low = 2, high = 4):

- `arr[mid]` is 2.
- Swap `arr[mid]` (2) with `arr[high]` (2), so no actual swap is performed.
- Decrement `high` to 3.

After the loop, the array `arr` is sorted as `[0, 0, 1, 1, 2, 2]`.

Java Code:

```java
import java.util.* ;
import java.io.*;
public class Solution {
public static void sortArray(ArrayList<Integer> arr, int n) {
int mid=0;
int low=0;
int high=n-1;
int temp=0;
for(int i=0;i<n;i++)
{
    if (arr.get(mid)==0)
    {
        temp=arr.get(mid);
        arr.set(mid,arr.get(low));
        arr.set(low,temp);
        mid++;
        low++;
    }
    else if(arr.get(mid)==1)
    {
        mid++;
    }
    else
    {
        temp=arr.get(mid);
        arr.set(mid,arr.get(high));
        arr.set(high,temp);
        high--;
    }
}
}
}
```

Optimizations:

This implementation is already optimized for both time and space complexity. However, there is a potential optimization that can be made to avoid unnecessary swaps when the elements at the `low` and `mid` pointers, or the `mid` and `high` pointers, are equal.

Here's the optimized version:

```java
public static void sortArray(ArrayList<Integer> arr, int n) {
    int mid = 0;
    int low = 0;
    int high = n - 1;

    while (mid <= high) {
        if (arr.get(mid) == 0) {
            swap(arr, mid, low);
            mid++;
            low++;
        } else if (arr.get(mid) == 1) {
            mid++;
        } else {
            swap(arr, mid, high);
            high--;
        }
    }
}

private static void swap(ArrayList<Integer> arr, int i, int j) {
    if (arr.get(i) != arr.get(j)) {
        int temp = arr.get(i);
        arr.set(i, arr.get(j));
        arr.set(j, temp);
    }
}
```

In this optimized version, we have introduced a separate `swap` function that checks if the elements at the given indices are different before performing the swap. This avoids unnecessary swaps when the elements are already in the correct position, potentially improving the performance for certain input cases.

The time complexity of this optimized solution remains O(n), where n is the length of the input array `arr`. The space complexity is still O(1), as the algorithm uses a constant amount of extra space.

**17. Majority Element**

[Majority Element](https://www.naukri.com/code360/problems/majority-element_6783241?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

You are given an array 'a' of 'n' integers.

A majority element in the array ‘a’ is an element that appears more than 'n' / 2 times.

Find the majority element of the array.

It is guaranteed that the array 'a' always has a majority element.

Example:
Input: ‘n’ = 9, ‘a’ = [2, 2, 1, 3, 1, 1, 3, 1, 1]

Output: 1

Explanation: The frequency of ‘1’ is 5, which is greater than 9 / 2.
Hence ‘1’ is the majority element.

This code is a Java implementation of the Boyer-Moore Majority Vote Algorithm, which is used to find the majority element in an array (if it exists). A majority element is an element that appears more than ⌊n/2⌋ times in an array of size n.

Pseudocode:

```
function majorityElement(v):
    n = length of v
    ele = v[0]  // Initialize the candidate for majority element
    count = 0  // Initialize the count of the candidate

    // Find the candidate for majority element
    for i from 0 to n - 1:
        if count is 0:
            ele = v[i]  // Reset the candidate

        if v[i] is equal to ele:
            increment count
        else:
            decrement count

    // Check if the candidate is indeed the majority element
    count = 0
    for i from 0 to n - 1:
        if v[i] is equal to ele:
            increment count

    if count > n / 2:
        return ele
    else:
        return -1  // No majority element found
```

Time Complexity: O(n), where n is the length of the input array `v`. The algorithm iterates through the array twice: once to find the candidate for the majority element, and once to validate if the candidate is indeed the majority element.

Space Complexity: O(1), as the algorithm uses a constant amount of extra space, regardless of the input size.

Example:

Let's consider the example where `v = [2, 2, 1, 1, 1, 2, 2]`.

Iteration 1 (i = 0):

- `ele` is initialized to `v[0]` (2).
- `count` is initialized to 0.
- `v[i]` (2) is equal to `ele` (2), so `count` is incremented to 1.

Iteration 2 (i = 1):

- `v[i]` (2) is equal to `ele` (2), so `count` is incremented to 2.

Iteration 3 (i = 2):

- `v[i]` (1) is not equal to `ele` (2), so `count` is decremented to 1.

Iteration 4 (i = 3):

- `v[i]` (1) is not equal to `ele` (2), so `count` is decremented to 0.

Iteration 5 (i = 4):

- `count` is 0, so `ele` is reset to `v[i]` (1).
- `v[i]` (1) is equal to `ele` (1), so `count` is incremented to 1.

Iteration 6 (i = 5):

- `v[i]` (2) is not equal to `ele` (1), so `count` is decremented to 0.

Iteration 7 (i = 6):

- `count` is 0, so `ele` is reset to `v[i]` (2).
- `v[i]` (2) is equal to `ele` (2), so `count` is incremented to 1.

After the first loop, `ele` is 2, which is the candidate for the majority element.

In the second loop (not shown in the code), the count of the candidate element 2 is computed, and since it appears 4 times (which is greater than ⌊n/2⌋ = ⌊7/2⌋ = 3), the function returns 2 as the majority element.

Java Code:

```java
public class Solution {
    public static int majorityElement(int []v) {
        int n=v.length;
        int ele=v[0];
        int count=0;
        for(int i=0;i<n;i++){
            if(count==0)
            ele=v[i];
            if(v[i]==ele)
            {
                count++;
            }
            else
            {
                count--;
            }
        }
        return ele;
    }
}
```

Optimizations:

This implementation is already optimized for both time and space complexity. However, there is a potential optimization that can be made if the input array is sorted.

If the array is sorted, we can use a linear-time algorithm to find the majority element (if it exists) by keeping track of the current element and its count. We iterate through the array, and whenever the current element changes, we decrement the count. If the count becomes zero, we reset the current element and its count.

Here's the optimized version for a sorted array:

```java
public static int majorityElement(int[] v) {
    int n = v.length;
    int currentElement = v[0];
    int count = 1;

    for (int i = 1; i < n; i++) {
        if (v[i] == currentElement) {
            count++;
        } else {
            count--;
        }

        if (count == 0) {
            currentElement = v[i];
            count = 1;
        }
    }

    // Check if the candidate is indeed the majority element
    count = 0;
    for (int num : v) {
        if (num == currentElement) {
            count++;
        }
    }

    if (count > n / 2) {
        return currentElement;
    } else {
        return -1;  // No majority element found
    }
}
```

In this optimized version, we iterate through the sorted array once, keeping track of the current element and its count. Whenever the count becomes zero, we reset the current element and its count to the current element in the array.

After the loop, we validate if the candidate element is indeed the majority element by counting its occurrences and checking if the count is greater than ⌊n/2⌋.

The time complexity of this optimized solution is O(n), where n is the length of the input array `v`. The space complexity is still O(1), as the algorithm uses a constant amount of extra space.

This optimization can improve the performance of the algorithm when the input array is already sorted, as it avoids the need for the first loop to find the candidate element.

**18. Maximum subarray**

[Maximum Subarray (CodeStudio)](https://www.naukri.com/code360/problems/maximum-subarray-sum_630526?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=SUBMISSION)

[Maximum Subarray (Leetcode)](https://leetcode.com/problems/maximum-subarray/)

Given an integer array nums, find the subarray
with the largest sum, and return its sum.

Example 1:

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The subarray [4,-1,2,1] has the largest sum 6.
Example 2:

Input: nums = [1]
Output: 1
Explanation: The subarray [1] has the largest sum 1.
Example 3:

Input: nums = [5,4,-1,7,8]
Output: 23
Explanation: The subarray [5,4,-1,7,8] has the largest sum 23.

This code is a Java implementation of Kadane's Algorithm, which is used to find the maximum subarray sum in an array of integers. It efficiently solves the problem by iterating through the array only once and keeping track of two variables: `maxEndingHere` and `maxSoFar`.

Pseudocode:

```
function maxSubArray(nums):
    maxEndingHere = nums[0]  // Initialize maxEndingHere with the first element
    maxSoFar = nums[0]  // Initialize maxSoFar with the first element

    // Iterate through the array
    for i from 1 to length of nums - 1:
        maxEndingHere = max(nums[i], maxEndingHere + nums[i])  // Update maxEndingHere
        maxSoFar = max(maxSoFar, maxEndingHere)  // Update maxSoFar

    return maxSoFar
```

Time Complexity: O(n), where n is the length of the input array `nums`. The algorithm iterates through the array once.

Space Complexity: O(1), as the algorithm uses a constant amount of extra space, regardless of the input size.

Example:

Let's consider the example where `nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]`.

Iteration 1 (i = 1):

- `maxEndingHere = max(-2, -2 + 1) = max(-2, -1) = -1`
- `maxSoFar = max(-2, -1) = -1`

Iteration 2 (i = 2):

- `maxEndingHere = max(-3, -1 + (-3)) = max(-3, -4) = -3`
- `maxSoFar = max(-1, -3) = -1`

Iteration 3 (i = 3):

- `maxEndingHere = max(4, -3 + 4) = max(4, 1) = 4`
- `maxSoFar = max(-1, 4) = 4`

Iteration 4 (i = 4):

- `maxEndingHere = max(-1, 4 + (-1)) = max(-1, 3) = 3`
- `maxSoFar = max(4, 3) = 4`

Iteration 5 (i = 5):

- `maxEndingHere = max(2, 3 + 2) = max(2, 5) = 5`
- `maxSoFar = max(4, 5) = 5`

Iteration 6 (i = 6):

- `maxEndingHere = max(1, 5 + 1) = max(1, 6) = 6`
- `maxSoFar = max(5, 6) = 6`

Iteration 7 (i = 7):

- `maxEndingHere = max(-5, 6 + (-5)) = max(-5, 1) = 1`
- `maxSoFar = max(6, 1) = 6`

Iteration 8 (i = 8):

- `maxEndingHere = max(4, 1 + 4) = max(4, 5) = 5`
- `maxSoFar = max(6, 5) = 6`

After the loop, the function returns `maxSoFar = 6`, which is the maximum subarray sum.

```java
public int maxSubArray(int[] nums)
    {
        int maxEndingHere = nums[0];
        int maxSoFar = nums[0];
        for (int i = 1; i < nums.length; i++) {
            maxEndingHere = Math.max(nums[i], maxEndingHere + nums[i]);
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }
        return maxSoFar;

    }
```

Optimizations:

This implementation is already optimized for both time and space complexity. However, there is a potential optimization that can be made if the input array contains only non-negative integers.

If the input array contains only non-negative integers, we can simplify the code by removing the `Math.max(nums[i], maxEndingHere + nums[i])` part, as we know that adding any non-negative number to `maxEndingHere` will always result in a value greater than or equal to `maxEndingHere`.

Here's the optimized version for non-negative input arrays:

```java
public int maxSubArray(int[] nums) {
    int maxSoFar = 0;
    int maxEndingHere = 0;

    for (int num : nums) {
        maxEndingHere = maxEndingHere + num;
        maxSoFar = Math.max(maxSoFar, maxEndingHere);
        if (maxEndingHere < 0) {
            maxEndingHere = 0;
        }
    }

    return maxSoFar;
}
```

In this optimized version, we initialize `maxSoFar` and `maxEndingHere` to 0 since we know that the maximum subarray sum cannot be negative for non-negative input arrays. We then iterate through the array and update `maxEndingHere` by adding the current element to it. If `maxEndingHere` becomes negative, we reset it to 0, as we know that any subarray starting from that point will have a non-negative sum.

The time complexity of this optimized solution remains O(n), where n is the length of the input array `nums`. The space complexity is still O(1), as the algorithm uses a constant amount of extra space.

This optimization can improve the performance of the algorithm for non-negative input arrays by avoiding unnecessary comparisons and operations.

Note : Problem 13 can also be solved with the above algorithm eventhough the given solution is viable and a better option.

## 2-05-2024

**19. Best time to buy and sell stock**

[Best time to buy and sell stock (CodeStudio)](https://www.naukri.com/code360/problems/best-time-to-buy-and-sell-stock_6194560?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

[Best time to buy and sell stock (Leetcode)](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)

You are given an array of integers 'prices' of size 'n', where ‘prices[i]’ is the price of a given stock on an ‘i’-th day. You want to maximize the profit by choosing a single day to buy one stock and a different day to sell that stock.

Please note that you can’t sell a stock before you buy one.

Sample Input 1:
6
7 1 5 4 3 6

Sample Output 1 :
5

Explanation Of Sample Input 1:
Purchase stock on day two, where the price is one, and sell it on day six, where the price is 6. Profit = 6 - 1 = 5.

Sample Input 2:
5
5 4 3 2 1

Sample Output 2 :
0

Pseudocode:

```
function bestTimeToBuyAndSellStock(prices):
    minimum = prices[0]  // Initialize minimum price with the first element
    maxProfit = 0  // Initialize maximum profit to 0

    // Iterate through the array
    for each price in prices:
        cost = price - minimum  // Calculate the potential profit
        maxProfit = max(maxProfit, cost)  // Update the maximum profit
        minimum = min(minimum, price)  // Update the minimum price

    return maxProfit
```

Time Complexity: O(n), where n is the length of the input array `prices`. The algorithm iterates through the array once.

Space Complexity: O(1), as the algorithm uses a constant amount of extra space, regardless of the input size.

Explanation with an example:

Let's consider the example where `prices = [7, 1, 5, 3, 6, 4]`.

Iteration 1 (i = 0):

- `minimum` is initialized to `prices[0]` (7).
- `maxProfit` is initialized to 0.

Iteration 2 (i = 1):

- `cost = prices[i] - minimum = 1 - 7 = -6`
- `maxProfit` remains 0, since -6 is less than 0.
- `minimum` is updated to 1, since 1 is less than the previous minimum (7).

Iteration 3 (i = 2):

- `cost = prices[i] - minimum = 5 - 1 = 4`
- `maxProfit` is updated to 4, since 4 is greater than the previous maximum profit (0).
- `minimum` remains 1, since 5 is not less than the previous minimum (1).

Iteration 4 (i = 3):

- `cost = prices[i] - minimum = 3 - 1 = 2`
- `maxProfit` remains 4, since 2 is less than the current maximum profit (4).
- `minimum` remains 1, since 3 is not less than the previous minimum (1).

Iteration 5 (i = 4):

- `cost = prices[i] - minimum = 6 - 1 = 5`
- `maxProfit` is updated to 5, since 5 is greater than the previous maximum profit (4).
- `minimum` remains 1, since 6 is not less than the previous minimum (1).

Iteration 6 (i = 5):

- `cost = prices[i] - minimum = 4 - 1 = 3`
- `maxProfit` remains 5, since 3 is less than the current maximum profit (5).
- `minimum` remains 1, since 4 is not less than the previous minimum (1).

After the loop, the function returns `maxProfit = 5`, which is the maximum profit that can be obtained by buying and selling the stock once.

```java
public static int bestTimeToBuyAndSellStock(int []prices)
{
        int minimum=prices[0];
        int maxProfit=0;
        for(int i=0;i<prices.length;i++)
        {
            int cost=prices[i]-minimum;
            maxProfit=Math.max(maxProfit, cost);
            minimum=Math.min(minimum, prices[i]);
        }
        return maxProfit;
    }
```

Optimizations:

This implementation is already optimized for both time and space complexity. However, there is a potential optimization that can be made if the input array is sorted in ascending or descending order.

If the input array is sorted in ascending order, we can simply return the difference between the last and first elements, as this would represent the maximum profit that can be obtained by buying at the lowest price and selling at the highest price.

If the input array is sorted in descending order, we can immediately return 0, as it is impossible to make a profit when the prices are monotonically decreasing.

Here's the optimized version that checks if the input array is sorted:

```java
public static int bestTimeToBuyAndSellStock(int[] prices) {
    int n = prices.length;

    // Check if the array is sorted in ascending order
    boolean isAscending = true;
    for (int i = 1; i < n; i++) {
        if (prices[i] < prices[i - 1]) {
            isAscending = false;
            break;
        }
    }

    if (isAscending) {
        return prices[n - 1] - prices[0]; // Maximum profit for ascending order
    }

    // Check if the array is sorted in descending order
    boolean isDescending = true;
    for (int i = 1; i < n; i++) {
        if (prices[i] > prices[i - 1]) {
            isDescending = false;
            break;
        }
    }

    if (isDescending) {
        return 0; // No profit for descending order
    }

    // If the array is not sorted, apply the original algorithm
    int minimum = prices[0];
    int maxProfit = 0;
    for (int i = 0; i < n; i++) {
        int cost = prices[i] - minimum;
        maxProfit = Math.max(maxProfit, cost);
        minimum = Math.min(minimum, prices[i]);
    }

    return maxProfit;
}
```

In this optimized version, we first check if the input array is sorted in ascending order. If it is, we return the difference between the last and first elements, as this represents the maximum profit.

If the input array is not sorted in ascending order, we check if it is sorted in descending order. If it is, we return 0, as no profit can be made when the prices are monotonically decreasing.

If the input array is not sorted in either ascending or descending order, we apply the original algorithm to find the maximum profit.

The time complexity of this optimized solution is O(n) in the worst case, where n is the length of the input array `prices`. In the best case, when the input array is sorted, the time complexity becomes O(1) as we can directly return the maximum profit without iterating through the entire array.

The space complexity remains O(1), as the algorithm uses a constant amount of extra space, regardless of the input size.

This optimization can improve the performance of the algorithm for sorted input arrays, as it avoids unnecessary iterations and computations.

**20. Rearrange the array in alternating positive and negative items**

[Rearrange the array in alternating positive and negative items (CodeStudio)](https://www.naukri.com/code360/problems/alternate-numbers_6783445?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

[Rearrange Array Elements by Sign (Leetcode)](https://leetcode.com/problems/rearrange-array-elements-by-sign/)

**Pseudocode:**

```
function rearrangeArray(nums):
    create an empty list positive
    create an empty list negative
    for each num in nums:
        if num is positive:
            add num to positive list
        else:
            add num to negative list
    create an empty result array of length nums.length
    i = 0, j = 0, k = 0
    while i is less than length of positive list and j is less than length of negative list:
        result[k] = positive[i]
        k = k + 1
        i = i + 1
        result[k] = negative[j]
        k = k + 1
        j = j + 1
    return result
```

**Explanation:**

1. The algorithm starts by creating two empty lists: `positive` and `negative`.
2. It then iterates over the input array `nums` and adds each positive number to the `positive` list and each negative number to the `negative` list.
3. Next, it creates a new array `result` of the same length as the input array `nums`.
4. The algorithm then uses three pointers: `i` for the `positive` list, `j` for the `negative` list, and `k` for the `result` array.
5. It iterates simultaneously over the `positive` and `negative` lists until one of them is exhausted.
6. In each iteration, it assigns the current value from the `positive` list to `result[k]`, increments `k` and `i`, then assigns the current value from the `negative` list to `result[k]`, and increments `k` and `j`.
7. Finally, the rearranged `result` array is returned.

**Time Complexity:** The algorithm has two main parts:

1. Splitting the input array into positive and negative lists: This part takes O(n) time, where n is the length of the input array.
2. Rearranging the elements into the result array: This part takes O(n) time, as it iterates through the positive and negative lists once.

Therefore, the overall time complexity is O(n).

**Space Complexity:** The algorithm creates two additional lists (positive and negative) to store the positive and negative numbers from the input array. In the worst case, where all elements are positive or negative, one of the lists will store n elements, and the other will be empty. Therefore, the space complexity is O(n).

**Example:**
Let's consider the example `nums = [3, 1, -2, -5, 2, -4]`.

1. Initially, `positive = []` and `negative = []`.
2. After the first loop, `positive = [3, 1, 2]` and `negative = [-2, -5, -4]`.
3. The result array is initialized with length 6: `result = [0, 0, 0, 0, 0, 0]`.
4. Iteration 1: `i = 0`, `j = 0`, `k = 0`
   - `result[0] = positive[0] = 3`
   - `result = [3, 0, 0, 0, 0, 0]`
   - `k = 1`, `i = 1`
5. Iteration 2: `i = 1`, `j = 0`, `k = 1`
   - `result[1] = negative[0] = -2`
   - `result = [3, -2, 0, 0, 0, 0]`
   - `k = 2`, `j = 1`
6. Iteration 3: `i = 1`, `j = 1`, `k = 2`
   - `result[2] = positive[1] = 1`
   - `result = [3, -2, 1, 0, 0, 0]`
   - `k = 3`, `i = 2`
7. Iteration 4: `i = 2`, `j = 1`, `k = 3`
   - `result[3] = negative[1] = -5`
   - `result = [3, -2, 1, -5, 0, 0]`
   - `k = 4`, `j = 2`
8. Iteration 5: `i = 2`, `j = 2`, `k = 4`
   - `result[4] = positive[2] = 2`
   - `result = [3, -2, 1, -5, 2, 0]`
   - `k = 5`, `i = 3` (out of bounds for positive list)
9. Iteration 6: `i = 3`, `j = 2`, `k = 5`
   - `result[5] = negative[2] = -4`
   - `result = [3, -2, 1, -5, 2, -4]`
   - `k = 6`, `j = 3` (out of bounds for negative list)

The final result is `[3, -2, 1, -5, 2, -4]`.

Java Code:

```java
public int[] rearrangeArray(int[] nums)
    {
        List<Integer> positive = new ArrayList<>();
        List<Integer> negative = new ArrayList<>();
        for(int num: nums)
        {
            if (num > 0)
            {
                positive.add(num);
            }
            else
            {
                negative.add(num);
            }
        }
        int[] result = new int[nums.length];
        int i=0,j=0,k=0;
        while(i<positive.size() && j<negative.size())
        {
            result[k++] = positive.get(i++);
            result[k++] = negative.get(j++);
        }
        return result;
    }
```

**Potential Optimizations:**

1. **In-place operation:** Instead of creating separate lists for positive and negative numbers, we can rearrange the elements within the original input array itself. This would reduce the space complexity from O(n) to O(1).

2. **Two-pointer approach:** We can use two pointers, one starting from the beginning and the other from the end of the array. At each iteration, we can swap elements if they have different signs. This approach would also have a time complexity of O(n) and a space complexity of O(1).

3. **Avoid unnecessary swaps:** In the current implementation, we are swapping elements even when they are already in the correct position. We can optimize this by checking if the current element is already in the correct position and skipping the swap if it is.

4. **Early termination:** If the input array is already rearranged correctly, we can terminate the algorithm early, saving unnecessary iterations.

These optimizations can potentially improve the performance of the algorithm, especially for large input arrays or scenarios where space complexity is a critical factor.

Here's the optimized code using the in-place operation and two-pointer approach:

```java
class Solution {
    public int[] rearrangeArray(int[] nums) {
        int n = nums.length;
        int left = 0, right = 1;

        while (right < n) {
            while (left < n && nums[left] >= 0) {
                left += 2;
            }
            while (right < n && nums[right] < 0) {
                right += 2;
            }
            if (left < n && right < n) {
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
            }
        }

        return nums;
    }
}
```

**Explanation:**

1. We initialize two pointers, `left` and `right`, at indices 0 and 1, respectively.
2. We use `left` to traverse the array and find the next positive number, skipping over negative numbers.
3. We use `right` to traverse the array and find the next negative number, skipping over positive numbers.
4. If we find a positive number at `left` and a negative number at `right`, we swap them.
5. We repeat steps 2-4 until either `left` or `right` reaches the end of the array.

This approach rearranges the elements in-place within the original input array, without using any additional data structures. It has a time complexity of O(n) and a space complexity of O(1), as it operates directly on the input array.

**Example:**
Let's consider the same example `nums = [3, 1, -2, -5, 2, -4]`.

1. Initially, `left = 0` and `right = 1`.
2. Iteration 1:
   - `left = 0` (nums[0] = 3, positive)
   - `right = 1` (nums[1] = 1, positive)
   - `right` is incremented to 3 (nums[3] = -5, negative)
   - `nums[0]` and `nums[3]` are swapped, `nums = [-5, 1, -2, 3, 2, -4]`
3. Iteration 2:
   - `left = 2` (nums[2] = -2, negative)
   - `left` is incremented to 4 (nums[4] = 2, positive)
   - `right = 3` (nums[3] = 3, positive)
   - `right` is incremented to 5 (nums[5] = -4, negative)
   - `nums[4]` and `nums[5]` are swapped, `nums = [-5, 1, -2, 3, -4, 2]`
4. Iteration 3:
   - `left = 6` (out of bounds)
   - `right = 6` (out of bounds)
   - The loop terminates, and the final result is `[-5, 1, -2, 3, -4, 2]`.

This optimized code has a time complexity of O(n) and a space complexity of O(1), and it performs the rearrangement in-place without using any additional data structures.

**21. Superior Elements**

[Superior Elements (CodeStudio)](https://www.naukri.com/code360/problems/superior-elements_6783446?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

**Pseudocode:**

```
function superiorElements(a):
    create an empty list result
    add the last element of a to result
    for each element num in a from second-to-last to first:
        if num is greater than the next element in a and greater than the last element in result:
            add num to result
    return result
```

**Explanation:**

1. The function starts by creating an empty list `list` to store the superior elements.
2. It adds the last element of the input array `a` to the `list` because there are no elements after it.
3. Then, it iterates over the array `a` from the second-to-last element to the first element in reverse order using a `for` loop.
4. Inside the loop, for each element `a[i]`, it checks two conditions:
   - `a[i]` is greater than the next element `a[i+1]` in the array.
   - `a[i]` is greater than the last element in the `list`, which is `list.get(list.size()-1)`.
5. If both conditions are met, `a[i]` is considered a superior element, and it is added to the `list`.
6. After iterating through the entire array, the `list` contains all the superior elements, and it is returned.

**Time Complexity:** The time complexity of this algorithm is O(n), where n is the length of the input array `a`. This is because it iterates through the array once in reverse order, performing constant-time operations (comparisons and list additions) for each element.

**Space Complexity:** The space complexity is O(m), where m is the number of superior elements in the input array `a`. In the worst case, where all elements are superior (sorted in descending order), the space complexity becomes O(n), as the list will store all the elements.

**Example:**
Let's consider the example `a = [5, 7, 3, 9, 4, 9, 8, 6, 5]`.

1. Initially, `list = []`.
2. The last element `5` is added to the list: `list = [5]`.
3. Iteration 1 (reverse order): `i = a.length-2 = 7`
   - `a[7] = 6` is not greater than `a[8] = 5` or `list.get(0) = 5`, so it is not added to the list.
4. Iteration 2: `i = 6`
   - `a[6] = 8` is greater than `a[7] = 6` and `list.get(0) = 5`, so it is added to the list: `list = [8, 5]`.
5. Iteration 3: `i = 5`
   - `a[5] = 9` is greater than `a[6] = 8` and `list.get(0) = 8`, so it is added to the list: `list = [9, 8, 5]`.
6. Iteration 4: `i = 4`
   - `a[4] = 4` is not greater than `a[5] = 9` or `list.get(0) = 9`, so it is not added to the list.
7. Iteration 5: `i = 3`
   - `a[3] = 9` is not greater than `a[4] = 4`, but it is greater than `list.get(0) = 9`, so it is added to the list: `list = [9, 9, 8, 5]`.
8. Iteration 6: `i = 2`
   - `a[2] = 3` is not greater than `a[3] = 9` or `list.get(0) = 9`, so it is not added to the list.
9. Iteration 7: `i = 1`
   - `a[1] = 7` is not greater than `a[2] = 3`, but it is greater than `list.get(0) = 9`, so it is added to the list: `list = [9, 9, 8, 7, 5]`.
10. Iteration 8: `i = 0`
    - `a[0] = 5` is not greater than `a[1] = 7` or `list.get(0) = 9`, so it is not added to the list.

The final result is `[9, 9, 8, 7, 5]`.

Java Code:

```java
public static List< Integer > superiorElements(int []a) {
        List<Integer> list = new ArrayList<>();
        list.add(a[a.length-1]);
        for(int i=a.length-2; i>=0; i--)
        {
            if(a[i]>a[i+1] && a[i]>list.get(list.size()-1))
            {
                list.add(a[i]);
            }

        }
        return list;
```

**Potential Optimizations:**

1. **Early Termination:** If the current element `a[i]` is not greater than the last element in the `list`, we can terminate the loop early because all the remaining elements will also be smaller than the last element in the `list`.

Here's the optimized code:

```java
public static List<Integer> superiorElements(int[] a) {
    List<Integer> list = new ArrayList<>();
    list.add(a[a.length - 1]);
    int lastSuperior = a[a.length - 1];

    for (int i = a.length - 2; i >= 0; i--) {
        if (a[i] > lastSuperior) {
            list.add(a[i]);
            lastSuperior = a[i];
        } else if (a[i] == lastSuperior) {
            list.add(a[i]);
        } else {
            break; // Early termination
        }
    }

    return list;
}
```

In this optimized code:

- We initialize `lastSuperior` with the last element of the array `a[a.length - 1]`.
- Inside the loop, if `a[i]` is greater than `lastSuperior`, we update `lastSuperior` to `a[i]` and add `a[i]` to the `list`.
- If `a[i]` is equal to `lastSuperior`, we add `a[i]` to the `list` without updating `lastSuperior`.
- If `a[i]` is less than `lastSuperior`, we break out of the loop using the `break` statement (early termination).

This optimization can improve the performance of the algorithm, especially when the input array contains a large number of consecutive descending elements towards the beginning of the array, as it avoids unnecessary iterations and comparisons.

## 3-05-2024

**22. Longest Consecutive Sequence in an Array**

[Longest Consecutive Sequence in an Array](https://www.naukri.com/code360/problems/longest-successive-elements_6811740?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=DISCUSS)

[Longest Consecutive Sequence in an Array](https://leetcode.com/problems/longest-consecutive-sequence/)

There is an integer array ‘A’ of size ‘N’.

A sequence is successive when the adjacent elements of the sequence have a difference of 1.

You must return the length of the longest successive sequence.

Note:

You can reorder the array to form a sequence.
For example,

Input:
A = [5, 8, 3, 2, 1, 4], N = 6
Output:
5
Explanation:
The resultant sequence can be 1, 2, 3, 4, 5.  
The length of the sequence is 5.

**Pseudocode:**

```
function longestConsecutive(nums):
    if nums is empty:
        return 0
    sort nums in ascending order
    count = 0
    longest = 1
    lastSmaller = MIN_VALUE

    for each num in nums:
        if num - 1 == lastSmaller:
            count += 1
            lastSmaller = num
        else if num != lastSmaller:
            count = 1
            lastSmaller = num
        update longest with the maximum of longest and count

    return longest
```

**Explanation:**

1. The function first checks if the input array `nums` is empty. If it is, it returns 0 since there can be no consecutive sequence.
2. If the array is not empty, it sorts the array in ascending order using `Arrays.sort(nums)`.
3. The function initializes three variables:
   - `count`: Keeps track of the length of the current consecutive sequence.
   - `longest`: Stores the length of the longest consecutive sequence found so far.
   - `lastSmaller`: Stores the value of the last element in the current consecutive sequence.
4. The function then iterates over the sorted array `nums`.
5. For each element `num` in `nums`:
   - If `num - 1` is equal to `lastSmaller`, it means that `num` is part of the current consecutive sequence. In this case, `count` is incremented by 1, and `lastSmaller` is updated to `num`.
   - If `num` is not equal to `lastSmaller`, it means that a new consecutive sequence starts from `num`. In this case, `count` is reset to 1, and `lastSmaller` is updated to `num`.
   - The `longest` variable is updated with the maximum value between its current value and the current value of `count`.
6. After iterating through the entire array, the function returns the value of `longest`, which represents the length of the longest consecutive sequence found in the input array.

**Time Complexity:** The time complexity of this algorithm is O(n log n), where n is the length of the input array `nums`. This is because the sorting operation using `Arrays.sort(nums)` takes O(n log n) time in the average case.

**Space Complexity:** The space complexity is O(1), as the algorithm uses a constant amount of extra space to store the variables `count`, `longest`, and `lastSmaller`, regardless of the size of the input array.

**Example:**
Let's consider the example `nums = [100, 4, 200, 1, 3, 2]`.

1. After sorting, `nums` becomes `[1, 2, 3, 4, 100, 200]`.
2. Initially, `count = 0`, `longest = 1`, and `lastSmaller = MIN_VALUE`.
3. Iteration 1: `num = 1`
   - `num - 1 != lastSmaller`, so `count = 1` and `lastSmaller = 1`.
   - `longest = max(longest, count) = max(1, 1) = 1`.
4. Iteration 2: `num = 2`
   - `num - 1 == lastSmaller`, so `count = 2` and `lastSmaller = 2`.
   - `longest = max(longest, count) = max(1, 2) = 2`.
5. Iteration 3: `num = 3`
   - `num - 1 == lastSmaller`, so `count = 3` and `lastSmaller = 3`.
   - `longest = max(longest, count) = max(2, 3) = 3`.
6. Iteration 4: `num = 4`
   - `num - 1 == lastSmaller`, so `count = 4` and `lastSmaller = 4`.
   - `longest = max(longest, count) = max(3, 4) = 4`.
7. Iteration 5: `num = 100`
   - `num - 1 != lastSmaller`, so `count = 1` and `lastSmaller = 100`.
   - `longest = max(longest, count) = max(4, 1) = 4`.
8. Iteration 6: `num = 200`
   - `num - 1 != lastSmaller`, so `count = 1` and `lastSmaller = 200`.
   - `longest = max(longest, count) = max(4, 1) = 4`.

The function returns `4`, which is the length of the longest consecutive sequence `[1, 2, 3, 4]` in the input array.

**Potential Optimizations:**

The given implementation is already optimized for time complexity, as it uses sorting to ensure that consecutive elements are processed together. However, there is a potential optimization to improve the space complexity:

Instead of using an auxiliary data structure like an array or a list, we can use a set data structure to store the unique elements of the input array. This way, we can skip the sorting step and directly iterate over the set. The time complexity will remain O(n log n) due to the set construction, but the space complexity will improve from O(n) (for sorting) to O(m), where m is the number of unique elements in the input array.

Here's the optimized code using a set:

```java
public int longestConsecutive(int[] nums) {
    int n = nums.length;
    if (n == 0) {
        return 0;
    }

    Set<Integer> numSet = new HashSet<>();
    for (int num : nums) {
        numSet.add(num);
    }

    int longest = 0;
    for (int num : numSet) {
        if (!numSet.contains(num - 1)) {
            int currentNum = num;
            int currentCount = 1;

            while (numSet.contains(currentNum + 1)) {
                currentNum++;
                currentCount++;
            }

            longest = Math.max(longest, currentCount);
        }
    }

    return longest;
}
```

In this optimized code:

1. We create a `HashSet` `numSet` and add all the elements from the input array `nums` to it.
2. We iterate over the elements in `numSet`.
3. For each element `num`, we check if `num - 1` is not present in the set. If it's not present, it means `num` is the start of a new consecutive sequence.
4. We then count the length of the consecutive sequence starting from `num` by incrementing `currentNum` and `currentCount` until we encounter a number that is not present in the set.
5. We update the `longest` variable with the maximum length of the consecutive sequence found so far.
6. Finally, we return the value of `longest`.

This optimization improves the space complexity to O(m), where m is the number of unique elements in the input array `nums`. However, the time complexity remains O(n log n) due to the set construction, which involves sorting the elements internally.

**23. Set Matrix Zeros**

[Zero Matrix (CodeStudio)](https://www.naukri.com/code360/problems/zero-matrix_1171153?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

You are given a matrix 'MATRIX' of dimension 'N' x 'M'. Your task is to make all the elements of row 'i' and column 'j' equal to 0 if any element in the ith row or jth column of the matrix is 0.

Note:

1. The number of rows should be at least 1.

2. The number of columns should be at least 1.

3. For example, refer to the below matrix illustration:

![Example 1](https://files.codingninjas.in/zero-8066.png)

**Pseudocode:**

```
function zeroMatrix(matrix, n, m):
    create an empty set rows to store row indices
    create an empty set cols to store column indices

    for each row i in matrix:
        for each column j in row i:
            if matrix[i][j] is 0:
                add i to rows
                add j to cols

    for each row i in matrix:
        create a list ls to store the current row
        for each column j in row i:
            if i is in rows or j is in cols:
                set ls[j] to 0
        update matrix[i] with ls

    return matrix
```

**Explanation:**

1. The function starts by creating two sets: `rows` and `cols`. These sets will store the indices of rows and columns, respectively, that contain at least one 0.
2. It then iterates over the matrix using nested loops. If any element `matrix[i][j]` is 0, it adds the row index `i` to the `rows` set and the column index `j` to the `cols` set.
3. After iterating over the entire matrix, the `rows` and `cols` sets contain the indices of rows and columns that need to be set to 0.
4. The function then iterates over the matrix again using a nested loop.
5. For each row `i`, it creates a new list `ls` to store the modified row.
6. For each column `j` in the current row `i`, it checks if the row index `i` is present in the `rows` set or the column index `j` is present in the `cols` set.
7. If either condition is true, it sets the corresponding element `ls[j]` to 0.
8. After processing all columns in the current row, it updates the original matrix by setting `matrix[i]` to the modified row `ls`.
9. Finally, the modified matrix is returned.

**Time Complexity:** The time complexity of this algorithm is O(n \* m), where n is the number of rows and m is the number of columns in the matrix. This is because the algorithm iterates over the entire matrix twice using nested loops.

**Space Complexity:** The space complexity is O(n + m), where n is the number of rows and m is the number of columns in the matrix. This is because the algorithm uses two sets (`rows` and `cols`) to store the indices of rows and columns that need to be set to 0. In the worst case, all rows and columns may need to be set to 0, resulting in a space complexity of O(n + m).

**Example:**
Let's consider the example `matrix = [[1, 1, 1], [1, 0, 1], [1, 1, 1]]`, `n = 3`, and `m = 3`.

1. Initially, `rows = {}`, `cols = {}`, and `finalList = []`.
2. Iteration 1: `i = 0`, `j = 0`, `matrix[0][0] = 1`, so no updates.
3. Iteration 2: `i = 0`, `j = 1`, `matrix[0][1] = 1`, so no updates.
4. Iteration 3: `i = 0`, `j = 2`, `matrix[0][2] = 1`, so no updates.
5. Iteration 4: `i = 1`, `j = 0`, `matrix[1][0] = 1`, so no updates.
6. Iteration 5: `i = 1`, `j = 1`, `matrix[1][1] = 0`, so `rows = {1}`, `cols = {1}`.
7. Iteration 6: `i = 1`, `j = 2`, `matrix[1][2] = 1`, so no updates.
8. Iteration 7: `i = 2`, `j = 0`, `matrix[2][0] = 1`, so no updates.
9. Iteration 8: `i = 2`, `j = 1`, `j = 1` is in `cols`, so `finalList = [[1, 0, 1]]`.
10. Iteration 9: `i = 2`, `j = 2`, `j = 2` is not in `cols`, so `finalList = [[1, 0, 1], [1, 0, 1]]`.
11. Iteration 10: `i = 1`, `i = 1` is in `rows`, so `finalList = [[1, 0, 1], [0, 0, 0], [1, 0, 1]]`.
12. Iteration 11: `i = 0`, `i = 0` is not in `rows`, so `finalList = [[1, 0, 1], [0, 0, 0], [1, 0, 1]]`.

The final matrix is `[[1, 0, 1], [0, 0, 0], [1, 0, 1]]`.

**Potential Optimizations:**

The given implementation is already optimized for both time and space complexity. However, there is a potential optimization to improve the readability and maintainability of the code:

Instead of using nested loops to iterate over the matrix, we can use a single loop and access the elements using indices. This can make the code more concise and easier to understand.

Here's the optimized code:

```java
public static ArrayList<ArrayList<Integer>> zeroMatrix(ArrayList<ArrayList<Integer>> matrix, Integer n, Integer m) {
    // Create a set to store row indices and column indices
    Set<Integer> rows = new HashSet<>();
    Set<Integer> cols = new HashSet<>();

    // Iterate over the matrix and store the row and column indices with 0
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (matrix.get(i).get(j) == 0) {
                rows.add(i);
                cols.add(j);
            }
        }
    }

    // Iterate over the matrix again and set elements to 0 if the row or column index is in the respective set
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (rows.contains(i) || cols.contains(j)) {
                matrix.get(i).set(j, 0);
            }
        }
    }

    return matrix;
}
```

In this optimized code:

1. We create two sets `rows` and `cols` to store the row and column indices with 0, respectively.
2. We iterate over the matrix using a single loop and store the row and column indices with 0 in the respective sets.
3. We iterate over the matrix again using a single loop and set the elements to 0 if the corresponding row or column index is present in the `rows` or `cols` set, respectively.
4. Finally, we return the modified matrix.

This optimization improves the readability and maintainability of the code without affecting the time and space complexity.

[Set Matrix Zeroes (Leetcode)](https://leetcode.com/problems/set-matrix-zeroes/description/)

Given an m x n integer matrix matrix, if an element is 0, set its entire row and column to 0's.

You must do it in place.

![Example 1](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

![Example 2](https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg)

**Pseudocode:**

```
function setZeroes(matrix):
    m = number of rows in matrix
    n = number of columns in matrix
    create a new matrix matrix2 of size m x n

    # Copy the original matrix to matrix2
    for each row i in matrix:
        for each column j in row i:
            matrix2[i][j] = matrix[i][j]

    # Traverse the original matrix
    for each row i in matrix:
        for each column j in row i:
            if matrix[i][j] is 0:
                # Set the entire row and column to 0 in matrix2
                for each column k in row i:
                    matrix2[i][k] = 0
                for each row k:
                    matrix2[k][j] = 0

    # Copy the modified matrix2 back to the original matrix
    for each row i in matrix:
        for each column j in row i:
            matrix[i][j] = matrix2[i][j]
```

**Explanation:**

1. The function takes a 2D integer matrix as input.
2. It creates a new matrix `matrix2` of the same size as the input matrix to store the modified values.
3. It copies the original matrix to `matrix2` using nested loops.
4. It then iterates over the original matrix using nested loops.
5. If an element `matrix[i][j]` is 0, it sets the entire row `i` and column `j` to 0 in `matrix2` using two additional nested loops.
6. After processing all elements, `matrix2` contains the modified matrix with the desired changes.
7. Finally, it copies the modified `matrix2` back to the original matrix using nested loops.

**Time Complexity:** The time complexity of this algorithm is O(m _ n _ (m + n)), where m is the number of rows and n is the number of columns in the matrix. This is because the algorithm iterates over the matrix three times using nested loops, and for each non-zero element, it performs two additional nested loops to set the corresponding row and column to 0 in `matrix2`.

**Space Complexity:** The space complexity is O(m \* n), where m is the number of rows and n is the number of columns in the matrix. This is because the algorithm creates a new matrix `matrix2` of the same size as the input matrix to store the modified values.

**Example:**
Let's consider the example `matrix = [[1, 1, 1], [1, 0, 1], [1, 1, 1]]`.

1. Initially, `m = 3`, `n = 3`, and `matrix2` is a new 3x3 matrix with all elements set to the same values as the input matrix.
2. Iteration 1: `i = 0`, `j = 0`, `matrix[0][0] = 1`, so no changes are made.
3. Iteration 2: `i = 0`, `j = 1`, `matrix[0][1] = 1`, so no changes are made.
4. Iteration 3: `i = 0`, `j = 2`, `matrix[0][2] = 1`, so no changes are made.
5. Iteration 4: `i = 1`, `j = 0`, `matrix[1][0] = 1`, so no changes are made.
6. Iteration 5: `i = 1`, `j = 1`, `matrix[1][1] = 0`, so `matrix2[1][0] = matrix2[1][1] = matrix2[1][2] = 0` (set the entire row to 0), and `matrix2[0][1] = matrix2[1][1] = matrix2[2][1] = 0` (set the entire column to 0).
7. Iteration 6: `i = 1`, `j = 2`, `matrix[1][2] = 1`, but since the row and column have already been set to 0, no further changes are made.
8. Iteration 7: `i = 2`, `j = 0`, `matrix[2][0] = 1`, but since the column has already been set to 0, no further changes are made.
9. Iteration 8: `i = 2`, `j = 1`, `matrix[2][1] = 1`, but since the column has already been set to 0, no further changes are made.
10. Iteration 9: `i = 2`, `j = 2`, `matrix[2][2] = 1`, but since the column has already been set to 0, no further changes are made.
11. Finally, the modified `matrix2` is copied back to the original matrix, resulting in `matrix = [[0, 0, 0], [0, 0, 0], [0, 0, 0]]`.

**Potential Optimizations:**

The given implementation is not optimized for space complexity, as it creates a new matrix `matrix2` of the same size as the input matrix. We can optimize the space complexity by using two additional boolean arrays to keep track of the rows and columns that need to be set to 0, instead of creating a separate matrix.

Here's the optimized code:

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        boolean[] rows = new boolean[m];
        boolean[] cols = new boolean[n];

        // Mark the rows and columns that need to be set to 0
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == 0) {
                    rows[i] = true;
                    cols[j] = true;
                }
            }
        }

        // Set the rows and columns to 0 based on the boolean arrays
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (rows[i] || cols[j]) {
                    matrix[i][j] = 0;
                }
            }
        }
    }
}
```

In this optimized code:

1. We create two boolean arrays `rows` and `cols` of sizes `m` and `n`, respectively, to store the information about rows and columns that need to be set to 0.
2. We iterate over the matrix and mark the corresponding rows and columns in the `rows` and `cols` arrays if an element is 0.
3. We iterate over the matrix again and set the elements to 0 if the corresponding row or column is marked in the `rows` or `cols` arrays, respectively.

This optimization reduces the space complexity from O(m \* n) to O(m + n), as we only need to store two boolean arrays instead of creating a separate matrix.

The time complexity remains O(m _ n _ (m + n)), as we still need to iterate over the matrix twice, and for each non-zero element, we need to mark the corresponding row and column.

**24. Rotate Matrix by 90 degrees**

Yet to learn

**25. Print the matrix in spiral manner**

Yet to learn

**26. Count All Subarrays With Given Sum**

[Count All Subarrays With Given Sum (CodeStudio)](https://www.naukri.com/code360/problems/subarray-sums-i_1467103?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

[Subarray Sum Equals K (Leetcode)](https://leetcode.com/problems/subarray-sum-equals-k/submissions/1248079219/)

**Pseudocode:**

```
function subarraySum(nums, k):
    create a map sumFrequency to store the cumulative sum and its frequency
    initialize sumFrequency with key 0 and value 1 (to handle the case when sum equals k)
    count = 0 (to store the number of subarrays with sum k)
    sum = 0 (to store the cumulative sum)

    for each num in nums:
        sum += num
        diff = sum - k
        if diff is present in sumFrequency:
            count += the frequency of diff in sumFrequency
        increment the frequency of sum in sumFrequency

    return count
```

**Explanation:**

1. The function initializes an empty `HashMap` called `sumFrequency` to store the cumulative sum and its frequency.
2. It initializes `sumFrequency` with `key=0` and `value=1`. This step is crucial because it accounts for the case when the cumulative sum equals `k`, which means there is a subarray whose sum is `k`.
3. The function initializes two variables: `count` to store the number of subarrays with sum `k`, and `sum` to store the cumulative sum.
4. It then iterates over the input array `nums`.
5. For each element `num` in `nums`, it updates the `sum` by adding `num` to it.
6. It calculates the `diff` as `sum - k`. If there exists a subarray with a cumulative sum equal to `diff`, then by adding `num` to that subarray, we can create a new subarray with a sum equal to `k`.
7. If `diff` is present as a key in the `sumFrequency` map, it means there are subarrays with a cumulative sum equal to `diff`. The function adds the frequency of `diff` to the `count`.
8. After processing the current element, the function updates the frequency of the current `sum` in the `sumFrequency` map.
9. Finally, the function returns the `count`, which represents the number of subarrays with a sum equal to `k`.

**Time Complexity:** The time complexity of this algorithm is O(n), where n is the length of the input array `nums`. This is because the algorithm iterates over the array once, and the operations performed in the loop (sum calculation, map lookup, and map update) take constant time on average.

**Space Complexity:** The space complexity is O(n) in the worst case, where all elements in the input array are distinct. In this case, the `sumFrequency` map will store a cumulative sum for each element, resulting in a space complexity of O(n). However, if the input array contains many duplicate elements, the space complexity can be reduced due to the fact that the `sumFrequency` map will store fewer distinct cumulative sums.

**Example:**
Let's consider the example `nums = [1, 1, 1]` and `k = 2`.

1. Initially, `sumFrequency = {0: 1}`, `count = 0`, and `sum = 0`.
2. Iteration 1: `num = 1`, `sum = 1`, `diff = 1 - 2 = -1`. `-1` is not present in `sumFrequency`, so `count` remains 0. `sumFrequency = {0: 1, 1: 1}`.
3. Iteration 2: `num = 1`, `sum = 2`, `diff = 2 - 2 = 0`. `0` is present in `sumFrequency` with a frequency of 1, so `count = 1`. `sumFrequency = {0: 1, 1: 1, 2: 1}`.
4. Iteration 3: `num = 1`, `sum = 3`, `diff = 3 - 2 = 1`. `1` is present in `sumFrequency` with a frequency of 1, so `count = 2`. `sumFrequency = {0: 1, 1: 1, 2: 1, 3: 1}`.

The function returns `2`, which is the number of subarrays with a sum equal to `k = 2` (the subarrays are `[1, 1]` and `[1, 1, 1]`).

**Potential Optimizations:**

The given implementation is already optimized for both time and space complexity. However, there is a potential optimization to improve the readability and maintainability of the code:

Instead of using the `getOrDefault` method to handle the case when the `sum` is not present in the `sumFrequency` map, we can use a single conditional statement to check if the `sum` is present in the map or not, and update the frequency accordingly.

Here's the optimized code:

```java
public int subarraySum(int[] nums, int k) {
    Map<Integer, Integer> sumFrequency = new HashMap<>();
    sumFrequency.put(0, 1); // Initialize with 0 sum frequency
    int count = 0;
    int sum = 0;
    for (int num : nums) {
        sum += num;
        int diff = sum - k;
        count += sumFrequency.getOrDefault(diff, 0);
        sumFrequency.put(sum, sumFrequency.getOrDefault(sum, 0) + 1);
    }
    return count;
}
```

In this optimized code, we use the `getOrDefault` method to handle the case when the `diff` or `sum` is not present in the `sumFrequency` map. If the key is not present, the `getOrDefault` method returns the default value of 0.

This optimization improves the readability and maintainability of the code without affecting the time and space complexity.

## 4-05-2024

**27. Pascals Triangle**

[Pascals Triangle (CodeStudio)](https://www.naukri.com/code360/problems/print-pascal-s-triangle_6917910?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=DISCUSS)

The given Java code is an implementation of a function `pascalTriangle` that generates Pascal's Triangle up to a specified number of rows `N`. The function returns a 2D integer array representing the triangle.

**Pseudocode:**

```
function pascalTriangle(N):
    create a 2D array arr with N rows
    for each row i from 0 to N-1:
        create a row of size i+1
        for each column j from 0 to i:
            if j is 0 or j is i:
                set arr[i][j] to 1
            else:
                set arr[i][j] to the sum of arr[i-1][j] and arr[i-1][j-1]
    return arr
```

**Explanation:**

1. The function takes an integer `N` as input, which represents the number of rows to generate in Pascal's Triangle.
2. It creates a 2D integer array `arr` with `N` rows, where each row is initially an empty array.
3. The function then iterates over the rows from `0` to `N-1` using a `for` loop.
4. For each row `i`:
   - A new row of size `i+1` is created to store the elements of that row in the triangle.
   - The function then iterates over the columns from `0` to `i` using another `for` loop.
   - For each column `j`:
     - If `j` is 0 or `j` is equal to `i`, the element `arr[i][j]` is set to 1 (as the first and last elements of each row in Pascal's Triangle are always 1).
     - Otherwise, the element `arr[i][j]` is set to the sum of the elements directly above it and above-left to it in the previous row (`arr[i-1][j]` and `arr[i-1][j-1]`, respectively).
5. After filling all the elements in the 2D array `arr`, the function returns `arr`, which represents Pascal's Triangle.

**Time Complexity:** The time complexity of this algorithm is O(N^2), where N is the number of rows in Pascal's Triangle. This is because for each row, the function iterates over the elements in the previous row to calculate the current row's elements, and the number of elements in each row increases linearly with the row number.

**Space Complexity:** The space complexity is O(N^2), where N is the number of rows in Pascal's Triangle. This is because the algorithm creates a 2D array to store all the elements of the triangle, and the total number of elements across all rows is proportional to N^2.

**Example:**
Let's consider the example `N = 5`.

1. The 2D array `arr` is created with 5 rows: `arr = [[],[],[],[],[]]`.
2. Iteration 1: `i = 0`
   - A new row of size 1 is created: `arr[0] = [1]`.
3. Iteration 2: `i = 1`
   - A new row of size 2 is created: `arr[1] = [0, 0]`.
   - `arr[1][0] = 1` (first element is 1).
   - `arr[1][1] = 1` (last element is 1).
   - `arr = [[1], [1, 1]]`.
4. Iteration 3: `i = 2`
   - A new row of size 3 is created: `arr[2] = [0, 0, 0]`.
   - `arr[2][0] = 1` (first element is 1).
   - `arr[2][1] = arr[1][0] + arr[1][1] = 1 + 1 = 2`.
   - `arr[2][2] = 1` (last element is 1).
   - `arr = [[1], [1, 1], [1, 2, 1]]`.
5. Iteration 4: `i = 3`
   - A new row of size 4 is created: `arr[3] = [0, 0, 0, 0]`.
   - `arr[3][0] = 1` (first element is 1).
   - `arr[3][1] = arr[2][0] + arr[2][1] = 1 + 2 = 3`.
   - `arr[3][2] = arr[2][1] + arr[2][2] = 2 + 1 = 3`.
   - `arr[3][3] = 1` (last element is 1).
   - `arr = [[1], [1, 1], [1, 2, 1], [1, 3, 3, 1]]`.
6. Iteration 5: `i = 4`
   - A new row of size 5 is created: `arr[4] = [0, 0, 0, 0, 0]`.
   - `arr[4][0] = 1` (first element is 1).
   - `arr[4][1] = arr[3][0] + arr[3][1] = 1 + 3 = 4`.
   - `arr[4][2] = arr[3][1] + arr[3][2] = 3 + 3 = 6`.
   - `arr[4][3] = arr[3][2] + arr[3][3] = 3 + 1 = 4`.
   - `arr[4][4] = 1` (last element is 1).
   - `arr = [[1], [1, 1], [1, 2, 1], [1, 3, 3, 1], [1, 4, 6, 4, 1]]`.

The function returns `arr`, which represents Pascal's Triangle up to 5 rows.

Java Code :

```java
import java.util.*;
public class Solution {
public static int[][] pascalTriangle(int N)
{
 int[][] arr = new int[N][];
 for(int i=0;i<N;i++)
{
 arr[i]=new int[i+1];
        for(int j=0;j<=i;j++) {
           if(j==0||j==i)
           arr[i][j]=1;
           else
           {
            arr[i][j]=arr[i-1][j]+arr[i-1][j-1];
            }
     }
}
       return arr;
}
}
```

**Potential Optimizations:**

The given implementation is already optimized for both time and space complexity. However, there is a potential optimization to improve the readability and maintainability of the code:

Instead of using nested loops, we can use a single loop and calculate the row elements using the previous row's elements. This can make the code more concise and easier to understand.

Here's the optimized code:

```java
import java.util.*;

public class Solution {
    public static int[][] pascalTriangle(int N) {
        int[][] arr = new int[N][];
        arr[0] = new int[1];
        arr[0][0] = 1;

        for (int i = 1; i < N; i++) {
            arr[i] = new int[i + 1];
            arr[i][0] = 1;
            for (int j = 1; j < i; j++) {
                arr[i][j] = arr[i - 1][j - 1] + arr[i - 1][j];
            }
            arr[i][i] = 1;
        }

        return arr;
    }
}
```

In this optimized code:

1. The first row (`arr[0]`) is initialized with `[1]`.
2. The function then iterates from `1` to `N-1` to generate the remaining rows.
3. For each row `i`:
   - A new row of size `i+1` is created (`arr[i]`).
   - The first element (`arr[i][0]`) is set to 1.
   - The function then iterates from `1` to `i-1` to calculate the remaining elements.
   - For each column `j`, the element `arr[i][j]` is set to the sum of the elements directly above it and above-left to it in the previous row (`arr[i-1][j-1]` and `arr[i-1][j]`, respectively).
   - The last element of the row (`arr[i][i]`) is set to 1.
4. Finally, the 2D array `arr` representing Pascal's Triangle is returned.

This optimization improves the readability and maintainability of the code without affecting the time and space complexity.

[Pascals Triangle (Leetcode)](https://leetcode.com/problems/pascals-triangle/description/)

The given Java code is an implementation of the `generate` function, which takes an integer `numRows` as input and returns a list of lists representing Pascal's Triangle up to the specified number of rows.

**Pseudocode:**

```
function generate(numRows):
    create an empty list triangle to store the rows
    if numRows is 0:
        return triangle (empty list)

    create a new list firstRow with element 1
    add firstRow to triangle

    for i from 1 to numRows-1:
        get the previous row prevRow from triangle
        create a new empty list currRow

        add 1 as the first element of currRow

        for j from 1 to i-1:
            prevLeft = prevRow[j-1]
            prevRight = prevRow[j]
            currVal = prevLeft + prevRight
            add currVal to currRow

        add 1 as the last element of currRow
        add currRow to triangle

    return triangle
```

**Explanation:**

1. The function initializes an empty list `triangle` to store the rows of Pascal's Triangle.
2. It checks if `numRows` is 0. If so, it returns the empty `triangle` list (base case).
3. The first row of Pascal's Triangle is always `[1]`, so it creates a new list `firstRow` with the element 1 and adds it to the `triangle` list.
4. The function then iterates from `1` to `numRows-1` to generate the remaining rows.
5. For each iteration `i`:
   - It retrieves the previous row `prevRow` from the `triangle` list.
   - It creates a new empty list `currRow` to store the current row.
   - It adds 1 as the first element of `currRow` (since the first element of each row in Pascal's Triangle is always 1).
   - It then iterates from `1` to `i-1` to calculate the remaining elements of `currRow`.
   - For each iteration `j`:
     - It retrieves the elements `prevLeft` and `prevRight` from the previous row `prevRow` at indices `j-1` and `j`, respectively.
     - It calculates the current element `currVal` as the sum of `prevLeft` and `prevRight`.
     - It adds `currVal` to the `currRow` list.
   - After calculating all the elements of `currRow`, it adds 1 as the last element (since the last element of each row in Pascal's Triangle is always 1).
   - It adds the `currRow` list to the `triangle` list.
6. Finally, it returns the `triangle` list containing all the rows of Pascal's Triangle.

**Time Complexity:** The time complexity of this algorithm is O(n^2), where n is the value of `numRows`. This is because for each row, the algorithm iterates over the previous row to calculate the current row, and the number of elements in each row increases linearly with the row number.

**Space Complexity:** The space complexity is O(n^2), where n is the value of `numRows`. This is because the algorithm stores all the rows of Pascal's Triangle in the `triangle` list, and the total number of elements across all rows is proportional to n^2.

**Example:**
Let's consider the example `numRows = 5`.

1. Initially, `triangle` is an empty list.
2. Since `numRows` is not 0, a new list `firstRow = [1]` is created and added to `triangle`.
3. Iteration 1: `i = 1`, `prevRow = [1]`, `currRow = [1, 1]`. `currRow` is added to `triangle`.
4. Iteration 2: `i = 2`, `prevRow = [1, 1]`, `currRow = [1, 2, 1]`. `currRow` is added to `triangle`.
5. Iteration 3: `i = 3`, `prevRow = [1, 2, 1]`, `currRow = [1, 3, 3, 1]`. `currRow` is added to `triangle`.
6. Iteration 4: `i = 4`, `prevRow = [1, 3, 3, 1]`, `currRow = [1, 4, 6, 4, 1]`. `currRow` is added to `triangle`.

The final `triangle` list is `[[1], [1, 1], [1, 2, 1], [1, 3, 3, 1], [1, 4, 6, 4, 1]]`.

```java
class Solution {
    public List<List<Integer>> generate(int numRows)
    {
        List<List<Integer>> triangle = new ArrayList<>();
        // Base case: If numRows is 0, return an empty triangle
        if (numRows == 0) {
            return triangle;
        }
        // First row of the triangle
        List<Integer> firstRow = new ArrayList<>();
        firstRow.add(1);
        triangle.add(firstRow);
        // Generate remaining rows
        for (int i = 1; i < numRows; i++) {
            List<Integer> prevRow = triangle.get(i - 1);
            List<Integer> currRow = new ArrayList<>();
            // The first element of each row is 1
            currRow.add(1);
            // Calculate the remaining elements using the previous row
            for (int j = 1; j < i; j++) {
                int prevLeft = prevRow.get(j - 1);
                int prevRight = prevRow.get(j);
                int currVal = prevLeft + prevRight;
                currRow.add(currVal);
            }
            // The last element of each row is 1
            currRow.add(1);
            triangle.add(currRow);
        }
        return triangle;
    }
}
```

**Potential Optimizations:**

The given implementation is already optimized for both time and space complexity. However, there is a potential optimization to improve the readability and maintainability of the code:

Instead of using nested loops, we can use a single loop and calculate the row elements using the previous row's elements. This can make the code more concise and easier to understand.

Here's the optimized code:

```java
public List<List<Integer>> generate(int numRows) {
    List<List<Integer>> triangle = new ArrayList<>();

    // Base case: If numRows is 0, return an empty triangle
    if (numRows == 0) {
        return triangle;
    }

    // First row of the triangle
    List<Integer> firstRow = new ArrayList<>();
    firstRow.add(1);
    triangle.add(firstRow);

    // Generate remaining rows
    for (int i = 1; i < numRows; i++) {
        List<Integer> prevRow = triangle.get(i - 1);
        List<Integer> currRow = new ArrayList<>(i + 1);
        currRow.add(1); // First element is always 1

        for (int j = 1; j < i; j++) {
            int prevLeft = prevRow.get(j - 1);
            int prevRight = prevRow.get(j);
            currRow.add(prevLeft + prevRight);
        }

        currRow.add(1); // Last element is always 1
        triangle.add(currRow);
    }

    return triangle;
}
```

In this optimized code:

1. The first row (`firstRow = [1]`) is initialized and added to the `triangle` list.
2. The function then iterates from `1` to `numRows-1` to generate the remaining rows.
3. For each row `i`:
   - A new list `currRow` of size `i+1` is created.
   - The first element (`currRow.add(1)`) is set to 1.
   - The function then iterates from `1` to `i-1` to calculate the remaining elements.
   - For each column `j`, the element `currRow.add(prevLeft + prevRight)` is calculated using the elements directly above it and above-left to it in the previous row (`prevRow.get(j-1)` and `prevRow.get(j)`, respectively).
   - The last element of the row (`currRow.add(1)`) is set to 1.
   - The `currRow` list is added to the `triangle` list.
4. Finally, the `triangle` list representing Pascal's Triangle is returned.

This optimization improves the readability and maintainability of the code without affecting the time and space complexity.

**28. Majority Element (n/3)**

[Majority Element (n/3) (CodeStudio)](https://www.naukri.com/code360/problems/majority-element_6915220?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=SUBMISSION)

[Majority Element II (Leetcode)](https://leetcode.com/problems/majority-element-ii/description/)

Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.

Example 1:

Input: nums = [3,2,3]
Output: [3]
Example 2:

Input: nums = [1]
Output: [1]
Example 3:

Input: nums = [1,2]
Output: [1,2]

**Pseudocode:**

```
function majorityElement(v):
    n = length of v
    create an empty list ls to store the majority elements
    create an empty hashmap mpp to store the frequency of elements
    mini = (n / 3) + 1 (minimum frequency required for a majority element)

    for each element num in v:
        value = frequency of num in mpp (default to 0 if not present)
        increment the frequency of num in mpp by 1
        if the frequency of num is equal to mini:
            add num to ls
        if the size of ls is 2:
            break the loop (since there can be at most 2 majority elements)

    sort ls in ascending order
    return ls
```

**Explanation:**

1. The function initializes the following variables:
   - `n`: The length of the input array `v`.
   - `ls`: An empty list to store the majority elements.
   - `mpp`: An empty hashmap to store the frequency of elements in `v`.
   - `mini`: The minimum frequency required for an element to be considered a majority element. It is calculated as `(n / 3) + 1`.
2. The function then iterates over the input array `v`.
3. For each element `v[i]`:
   - It retrieves the current frequency of `v[i]` from the `mpp` hashmap, defaulting to 0 if `v[i]` is not present in `mpp`.
   - It increments the frequency of `v[i]` in `mpp` by 1.
   - If the frequency of `v[i]` is equal to `mini`, it adds `v[i]` to the `ls` list.
   - If the size of `ls` becomes 2, it breaks out of the loop because there can be at most 2 majority elements in the array (since the sum of frequencies of all elements is `n`, and each majority element has a frequency greater than `n/3`).
4. After the loop, the `ls` list contains the potential majority elements.
5. The function sorts the `ls` list in ascending order using the `Collections.sort(ls)` method.
6. Finally, the sorted `ls` list containing the majority elements is returned.

**Time Complexity:** The time complexity of this algorithm is O(n log n), where n is the length of the input array `v`. This is because the algorithm iterates over the array once to count the frequencies, which takes O(n) time, and then sorts the list `ls`, which takes O(k log k) time, where k is the number of potential majority elements (at most 2). Since k is a constant (2), the overall time complexity becomes O(n log n).

**Space Complexity:** The space complexity is O(n), where n is the length of the input array `v`. This is because the algorithm uses a hashmap `mpp` to store the frequencies of elements, which can take up to O(n) space in the worst case when all elements are distinct.

**Example:**
Let's consider the example `v = [1, 2, 2, 3, 2, 1, 1, 3]`.

1. Initially, `n = 8`, `ls = []`, `mpp = {}`, and `mini = (8 / 3) + 1 = 4`.
2. Iteration 1: `v[0] = 1`, `mpp = {1: 1}`, `ls = []`.
3. Iteration 2: `v[1] = 2`, `mpp = {1: 1, 2: 1}`, `ls = []`.
4. Iteration 3: `v[2] = 2`, `mpp = {1: 1, 2: 2}`, `ls = []`.
5. Iteration 4: `v[3] = 3`, `mpp = {1: 1, 2: 2, 3: 1}`, `ls = []`.
6. Iteration 5: `v[4] = 2`, `mpp = {1: 1, 2: 3, 3: 1}`, `ls = [2]`.
7. Iteration 6: `v[5] = 1`, `mpp = {1: 2, 2: 3, 3: 1}`, `ls = [2, 1]`, and the loop breaks because `ls.size() == 2`.
8. The `ls` list is sorted: `ls = [1, 2]`.
9. The function returns `[1, 2]`, which are the majority elements in the input array `v`.

```java
class Solution {
    public List<Integer> majorityElement(int[] nums)
    {
        int n = nums.length;
        List<Integer> ls = new ArrayList<>();
        HashMap<Integer, Integer> mpp = new HashMap<>();
        int mini = (int)(n / 3) + 1;
        for (int i = 0; i < n; i++)
        {
            int value = mpp.getOrDefault(nums[i], 0);
            mpp.put(nums[i], value + 1);
            if (mpp.get(nums[i]) == mini)
            {
                ls.add(nums[i]);
            }
            if (ls.size() == 2) break;
        }
        Collections.sort(ls);
        return ls;
    }
}
```

**Potential Optimizations:**

The given implementation is already optimized for both time and space complexity. However, there is a potential optimization to improve the readability and maintainability of the code:

Instead of using the `getOrDefault` method to handle the case when an element is not present in the `mpp` hashmap, we can use a single conditional statement to check if the element is present and update the frequency accordingly.

Here's the optimized code:

```java
import java.util.*;

public class Solution {
    public static List<Integer> majorityElement(int[] v) {
        int n = v.length;
        List<Integer> ls = new ArrayList<>();
        HashMap<Integer, Integer> mpp = new HashMap<>();
        int mini = (int) (n / 3) + 1;

        for (int num : v) {
            int value = mpp.getOrDefault(num, 0);
            mpp.put(num, value + 1);
            if (mpp.get(num) == mini) {
                ls.add(num);
                if (ls.size() == 2) break;
            }
        }

        Collections.sort(ls);
        return ls;
    }
}
```

In this optimized code, we use the `getOrDefault` method to handle the case when an element is not present in the `mpp` hashmap. This can make the code more concise and easier to understand.

This optimization does not affect the time and space complexity of the algorithm.

## 6-05-2024

**29. 3 Sum**

[3 Sum (Leetcode)](https://leetcode.com/problems/3sum/description/)

[3 Sum (CodeStudio)](https://www.naukri.com/code360/problems/three-sum_6922132?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

Example 1:

Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation:
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.
Example 2:

Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.
Example 3:

Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.

The given code is a solution to the "3Sum" problem, which is a famous problem in computer science. The problem statement is as follows:

Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

The solution should not contain duplicate triplets.

Pseudocode

```
1. Sort the input array nums in ascending order
2. Initialize an empty list to store the triplets (ans)
3. Iterate through the array with a variable i from 0 to length - 2
    a. If i > 0 and nums[i] is the same as nums[i-1], skip this iteration (to avoid duplicates)
    b. Initialize two pointers, j = i + 1 and k = length - 1
    c. While j < k:
        i. Calculate the sum of nums[i], nums[j], and nums[k]
        ii. If the sum is 0:
            1. Add the triplet [nums[i], nums[j], nums[k]] to ans
            2. Move j and k inwards until they point to different values (to avoid duplicates)
        iii. If the sum is less than 0, increment j (to increase the sum)
        iv. If the sum is greater than 0, decrement k (to decrease the sum)
4. Return ans
```

**Time Complexity:** O(n^2), where n is the length of the input array `nums`. The sorting step takes O(n log n), but the nested loops have a time complexity of O(n^2).

**Space Complexity:** O(n), where n is the length of the input array `nums`. In the worst case, the output list `ans` could contain O(n^2) triplets, but the space required for the sorted array and the pointers is O(n).

**Explanation with Example:**

Let's consider the example `nums = [-1, 0, 1, 2, -1, -4]`.

1. The array is sorted: `nums = [-4, -1, -1, 0, 1, 2]`.
2. An empty list `ans` is initialized to store the triplets.
3. The outer loop starts with `i = 0` and `nums[i] = -4`.
   - `j = 1` and `k = 5` (initially pointing to the second and last elements).
   - While `j < k`:
     - `sum = nums[i] + nums[j] + nums[k] = -4 + (-1) + 2 = -3 < 0`, so `j` is incremented to 2.
     - `sum = nums[i] + nums[j] + nums[k] = -4 + (-1) + 1 = -4 < 0`, so `j` is incremented to 3.
     - `sum = nums[i] + nums[j] + nums[k] = -4 + 0 + 1 = -3 < 0`, so `j` is incremented to 4.
     - `sum = nums[i] + nums[j] + nums[k] = -4 + 1 + 1 = -2 < 0`, so `j` is incremented to 5, which is not less than `k`, so the inner loop terminates.
4. The outer loop continues with `i = 1` and `nums[i] = -1`.
   - `j = 2` and `k = 5` (initially pointing to the third and last elements).
   - While `j < k`:
     - `sum = nums[i] + nums[j] + nums[k] = -1 + (-1) + 2 = 0`, so the triplet `[-1, -1, 2]` is added to `ans`. `j` is incremented to 3, and `k` is decremented to 4.
     - `sum = nums[i] + nums[j] + nums[k] = -1 + 0 + 1 = 0`, so the triplet `[-1, 0, 1]` is added to `ans`. `j` is incremented to 4, and `k` is decremented to 3, which is not less than `j`, so the inner loop terminates.
5. The outer loop continues with `i = 2` and `nums[i] = -1`, but since `nums[i]` is the same as `nums[i-1]`, this iteration is skipped to avoid duplicates.
6. The outer loop continues with `i = 3` and `nums[i] = 0`.
   - `j = 4` and `k = 5` (initially pointing to the fifth and last elements).
   - While `j < k`:
     - `sum = nums[i] + nums[j] + nums[k] = 0 + 1 + 2 = 3 > 0`, so `k` is decremented to 4, which is not greater than `j`, so the inner loop terminates.
7. The outer loop continues with `i = 4` and `nums[i] = 1`.
   - `j = 5` and `k = 5` (initially pointing to the last element).
   - While `j < k`: This condition is false, so the inner loop is not executed.
8. The outer loop terminates, and the list `ans` containing the triplets `[-1, -1, 2]` and `[-1, 0, 1]` is returned.

Java Code:

```java
List<List<Integer>> ans = new ArrayList<>();

        Arrays.sort(nums);

        for(int i=0; i<nums.length-2;i++)
        {
            if(i>0 && nums[i] == nums[i-1])
            {
                continue;
            }
            int j = i+1;
            int k = nums.length - 1;

            while(j<k)
            {
                int sum = nums[i]+nums[j]+nums[k];

                if(sum == 0)
                {
                    ans.add(Arrays.asList(nums[i],nums[j],nums[k]));

                    while (j<k && nums[j] == nums[j+1])
                    {
                        j++;
                    }

                    j++;
                    k--;
                }
                else if(sum<0)
                {
                    j++;
                }
                else
                {
                    k--;
                }
            }
        }
        return ans;
```

**Possible Optimizations:**

The given code is already optimized for the "3Sum" problem, as it avoids duplicates and has an optimal time complexity of O(n^2). However, one potential optimization could be to use a `HashSet` instead of a `List` to store the triplets. This would prevent duplicate triplets from being added to the set, eliminating the need for the `while` loops to skip over duplicates. However, this optimization might not significantly improve the time complexity, as the nested loops still have a time complexity of O(n^2).

Here's the optimized code using a `HashSet`:

```java
List<List<Integer>> ans = new ArrayList<>();
HashSet<List<Integer>> triplets = new HashSet<>();
Arrays.sort(nums);

for (int i = 0; i < nums.length - 2; i++) {
    if (i > 0 && nums[i] == nums[i - 1]) {
        continue;
    }
    int j = i + 1;
    int k = nums.length - 1;
    while (j < k) {
        int sum = nums[i] + nums[j] + nums[k];
        if (sum == 0) {
            triplets.add(Arrays.asList(nums[i], nums[j], nums[k]));
            j++;
            k--;
        } else if (sum < 0) {
            j++;
        } else {
            k--;
        }
    }
}

ans.addAll(triplets);
return ans;
```

In this optimized code, the triplets are added to a `HashSet` instead of a `List`. After the nested loops, the `HashSet` is converted back to a `List` and returned as the final result.

**30. Largest Subarray with Zero sum**

[Largest Subarray with Zero sum (CodeStudio)](https://www.naukri.com/code360/problems/longest-subarray-with-zero-sum_6783450?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

Ninja is given an array ‘Arr’ of size ‘N’. You have to help him find the longest subarray of ‘Arr’, whose sum is 0. You must return the length of the longest subarray whose sum is 0.

For Example:
For N = 5, and Arr = {1, -1, 0, 0, 1},
We have the following subarrays with zero sums:
{{1, -1}, {1, -1, 0}, {1, -1, 0, 0}, {-1, 0, 0, 1}, {0}, {0, 0}, {0}}
Among these subarrays, {1, -1, 0, 0} and {-1, 0, 0, 1} are the longest subarrays with their sum equal to zero. Hence the answer is 4.

The given code is an optimized solution to find the length of the longest subarray with a sum of 0 in a given array of integers.

**Pseudocode with Explanation (Time Complexity and Space Complexity):**

```
1. Initialize maxLength to 0 (to store the length of the longest subarray with sum 0)
2. Initialize sum to 0 (to keep track of the cumulative sum)
3. Create a HashMap sumIndex to store the cumulative sum and its index
4. Initialize the HashMap with 0 as the key and -1 as the value (to handle the case where a subarray starts from the beginning of the array and has a sum of 0)
5. Iterate through the array:
    a. Update the sum by adding the current element
    b. If the current sum exists in the HashMap:
        i. Calculate the length of the subarray with sum 0 ending at the current index (i - sumIndex.get(sum) + 1)
        ii. Update maxLength with the maximum value between the current maxLength and the calculated length
    c. If the current sum doesn't exist in the HashMap:
        i. Add the current sum and its index to the HashMap
6. Return maxLength
```

**Time Complexity:** O(n), where n is the length of the input array. We iterate through the array once, and the HashMap operations (get and put) have an average time complexity of O(1).

**Space Complexity:** O(n), where n is the length of the input array. In the worst case, when all elements are distinct, the HashMap will store all elements and their indices, resulting in a space complexity of O(n).

**Explanation with Example:**

Let's consider the example `arr = [1, -1, 3, -3, 2, -2, 4, 5, -5]`.

1. `maxLength` is initialized to 0, `sum` is initialized to 0, and an empty `HashMap` `sumIndex` is created.
2. `sumIndex.put(0, -1)` initializes the `HashMap` with a key-value pair of `0` and `-1`. This is to handle the case where a subarray starts from the beginning of the array and has a sum of 0.
3. The loop starts with `i = 0`:
   - `sum = 1` (after adding `arr[0] = 1`)
   - The `HashMap` doesn't contain the key `1`, so `sumIndex.put(1, 0)` adds the key-value pair `1` and `0` to the `HashMap`.
4. `i = 1`:
   - `sum = 0` (after adding `arr[1] = -1`)
   - The `HashMap` contains the key `0`, so `maxLength = Math.max(maxLength, 2)` updates `maxLength` to 2 (since `i - sumIndex.get(0) + 1 = 2 - (-1) + 1 = 2`).
5. `i = 2`:
   - `sum = 3` (after adding `arr[2] = 3`)
   - The `HashMap` doesn't contain the key `3`, so `sumIndex.put(3, 2)` adds the key-value pair `3` and `2` to the `HashMap`.
6. `i = 3`:
   - `sum = 0` (after adding `arr[3] = -3`)
   - The `HashMap` contains the key `0`, so `maxLength = Math.max(maxLength, 4)` updates `maxLength` to 4 (since `i - sumIndex.get(0) + 1 = 4 - (-1) + 1 = 4`).
7. The loop continues, and the `HashMap` is updated with the cumulative sums and their indices.
8. After iterating through the entire array, the `maxLength` of 4 is returned, which corresponds to the subarray `[3, -3, 2, -2]` with a sum of 0.

Java code:

```java
import java.util.*;
public class Solution {
    public static int getLongestZeroSumSubarrayLength(int[] arr) {
        int maxLength = 0;
        int n = arr.length;
        int sum = 0;

        // Create a HashMap to store the cumulative sum and its index
        Map<Integer, Integer> sumIndex = new HashMap<>();

        // Initialize the HashMap with 0 as the first index
        sumIndex.put(0, -1);

        for (int i = 0; i < n; i++) {
            sum += arr[i];

            // If the current sum exists in the HashMap,
            // it means there is a subarray with sum 0 ending at index i
            if (sumIndex.containsKey(sum)) {
                maxLength = Math.max(maxLength, i - sumIndex.get(sum));
            } else {
                // Otherwise, store the current sum and its index in the HashMap
                sumIndex.put(sum, i);
            }
        }

        return maxLength;
    }
}
```

**Possible Optimizations:**

The given code is already optimized and has a time complexity of O(n) and a space complexity of O(n). However, there is a slight optimization that can be made to handle the case where the entire array has a sum of 0.

Here's the optimized code:

```java
public class Solution {
    public static int getLongestZeroSumSubarrayLength(int[] arr) {
        int maxLength = 0;
        int n = arr.length;
        int sum = 0;

        // Create a HashMap to store the cumulative sum and its index
        Map<Integer, Integer> sumIndex = new HashMap<>();

        // Handle the case where the entire array has a sum of 0
        sumIndex.put(0, -1);

        for (int i = 0; i < n; i++) {
            sum += arr[i];

            // If the current sum exists in the HashMap,
            // it means there is a subarray with sum 0 ending at index i
            if (sumIndex.containsKey(sum)) {
                maxLength = Math.max(maxLength, i - sumIndex.get(sum));
            } else {
                // Otherwise, store the current sum and its index in the HashMap
                sumIndex.put(sum, i);
            }
        }

        // Handle the case where the entire array has a sum of 0
        if (sumIndex.containsKey(0)) {
            maxLength = Math.max(maxLength, n);
        }

        return maxLength;
    }
}
```

In this optimized code, we handle the case where the entire array has a sum of 0 by checking if the `HashMap` contains the key `0` after iterating through the array. If it does, we update `maxLength` with the maximum value between the current `maxLength` and the length of the entire array `n`.

This optimization ensures that if the entire array has a sum of 0, the code correctly returns the length of the entire array as the length of the longest subarray with sum 0.

**31. Maximum Product Subarray**

[Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/description/)

Given an integer array nums, find a
subarray
that has the largest product, and return the product.

The test cases are generated so that the answer will fit in a 32-bit integer.

Example 1:

Input: nums = [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
Example 2:

Input: nums = [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.

The given code is a solution to the "Maximum Product Subarray" problem, which finds the maximum product of a contiguous subarray within an integer array.

**Pseudocode with Explanation (Time Complexity and Space Complexity):**

```
1. Initialize max, min, and ans with the first element of the array
2. Iterate through the array from index 1 to the end:
    a. Store the current max value in a temporary variable temp
    b. Update max with the maximum of the following three values:
        i. The current max multiplied by the current element
        ii. The current min multiplied by the current element
        iii. The current element
    c. Update min with the minimum of the following three values:
        i. The previous max (temp) multiplied by the current element
        ii. The current min multiplied by the current element
        iii. The current element
    d. If the current max is greater than the current ans, update ans with max
3. Return ans
```

**Time Complexity:** O(n), where n is the length of the input array. We iterate through the array once.

**Space Complexity:** O(1), as we are using constant extra space to store max, min, ans, and temp.

**Explanation with Example:**

Let's consider the example `nums = [2, 3, -2, 4]`.

1. Initially, `max = 2`, `min = 2`, and `ans = 2`.
2. Iteration 1 (`i = 1`):
   - `temp = 2` (storing the previous max value)
   - `max = Math.max(2 * 3, 2 * 3, 3) = 6` (updating max)
   - `min = Math.min(2 * 3, 2 * 3, 3) = 3` (updating min)
   - `ans = 6` (updating ans since max is greater than the previous ans)
3. Iteration 2 (`i = 2`):
   - `temp = 6` (storing the previous max value)
   - `max = Math.max(6 * (-2), 3 * (-2), -2) = 6` (updating max)
   - `min = Math.min(6 * (-2), 3 * (-2), -2) = -12` (updating min)
   - `ans = 6` (ans remains unchanged)
4. Iteration 3 (`i = 3`):
   - `temp = 6` (storing the previous max value)
   - `max = Math.max(6 * 4, (-12) * 4, 4) = 24` (updating max)
   - `min = Math.min(6 * 4, (-12) * 4, 4) = -48` (updating min)
   - `ans = 24` (updating ans since max is greater than the previous ans)
5. The loop terminates, and the maximum product subarray is 24, corresponding to the subarray `[2, 3, -2, 4]`.

Java code:

```java
class Solution {
    public int maxProduct(int[] nums) {

        int max = nums[0], min = nums[0], ans = nums[0];

        for (int i = 1; i < nums.length; i++) {

            int temp = max;  // store the max because before updating min your max will already be updated

            max = Math.max(Math.max(max * nums[i], min * nums[i]), nums[i]);
            min = Math.min(Math.min(temp * nums[i], min * nums[i]), nums[i]);

            if (max > ans) {
                ans = max;
            }
        }

        return ans;

    }
}
```

**Possible Optimizations:**

The given code is already optimized and has a time complexity of O(n) and a space complexity of O(1). There are no significant optimizations that can be made without changing the overall time complexity.

However, here's an alternative implementation that might be slightly more readable:

```java
class Solution {
    public int maxProduct(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int maxSoFar = nums[0];
        int minSoFar = nums[0];
        int result = maxSoFar;

        for (int i = 1; i < nums.length; i++) {
            int currMax = Math.max(Math.max(maxSoFar * nums[i], minSoFar * nums[i]), nums[i]);
            minSoFar = Math.min(Math.min(maxSoFar * nums[i], minSoFar * nums[i]), nums[i]);
            maxSoFar = currMax;
            result = Math.max(result, maxSoFar);
        }

        return result;
    }
}
```

In this implementation, we first handle the edge case where the input array is null or empty. Then, we initialize `maxSoFar` and `minSoFar` with the first element of the array, and `result` with `maxSoFar`.

Inside the loop, we update `currMax` with the maximum of the three possible cases: `maxSoFar * nums[i]`, `minSoFar * nums[i]`, and `nums[i]`. We then update `minSoFar` with the minimum of the three possible cases, and `maxSoFar` with the updated `currMax`. Finally, we update `result` with the maximum of `result` and `maxSoFar`.

This implementation follows the same logic as the given code but might be easier to read and understand for some developers.

**32. Merge Sorted Array**

You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

Example 1:

Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.
Example 2:

Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
Explanation: The arrays we are merging are [1] and [].
The result of the merge is [1].
Example 3:

Input: nums1 = [0], m = 0, nums2 = [1], n = 1
Output: [1]
Explanation: The arrays we are merging are [] and [1].
The result of the merge is [1].
Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.

The given code is a Java implementation of the "Merge Two Sorted Arrays Without Extra Space" problem. It merges two sorted arrays `a` and `b` into a single sorted array by utilizing the gap method (also known as the shell sort algorithm).

**Pseudocode with Explanation (Time Complexity and Space Complexity):**

```
1. Initialize n and m with the lengths of arrays a and b, respectively
2. Initialize len as the sum of n and m
3. Initialize gap as (len/2) + (len%2)
4. While gap is greater than 0:
    a. Initialize left and right pointers
    b. While right is less than len:
        i. If left is within the bounds of a and right is out of bounds of a:
            Swap elements at indices left of a and right-n of b
        ii. If left is out of bounds of a:
            Swap elements at indices left-n and right-n of b
        iii. Otherwise:
            Swap elements at indices left and right of a
        iv. Increment left and right
    c. If gap is 1, break out of the loop
    d. Update gap as (gap/2) + (gap%2)
5. Return (arrays a and b are now merged and sorted)
```

**Time Complexity:** O(m _ n _ log(m + n)), where m and n are the lengths of the input arrays a and b, respectively. The time complexity is derived from the shell sort algorithm, which performs multiple iterations with decreasing gap sizes, and each iteration has a time complexity of O(m + n).

**Space Complexity:** O(1), as the merge is performed in-place without using any additional data structures.

**Explanation with Example:**

Let's consider the example `a = [1, 3, 5, 7]` and `b = [0, 2, 4, 6, 8]`.

1. Initially, `n = 4`, `m = 5`, and `len = 9`.
2. `gap = (9/2) + (9%2) = 5`.
3. Iteration 1 (`gap = 5`):
   - `left = 0`, `right = 5`
   - Swap `a[0]` (1) and `b[0]` (0), as `a[0] > b[0]`.
   - `left = 1`, `right = 6`
   - Swap `a[1]` (3) and `b[1]` (2), as `a[1] > b[1]`.
   - `left = 2`, `right = 7`
   - No swap is needed, as `a[2] < b[2]`.
   - `left = 3`, `right = 8`
   - Swap `a[3]` (7) and `b[3]` (6), as `a[3] > b[3]`.
   - After this iteration, `a = [0, 2, 5, 6]` and `b = [1, 3, 4, 7, 8]`.
4. Iteration 2 (`gap = 2`):
   - `left = 0`, `right = 2`
   - Swap `a[0]` (0) and `a[2]` (5), as `a[0] > a[2]`.
   - `left = 1`, `right = 3`
   - No swap is needed, as `a[1] < a[3]`.
   - `left = 2`, `right = 4`
   - Swap `b[0]` (1) and `b[2]` (4), as `b[0] > b[2]`.
   - `left = 3`, `right = 5`
   - No swap is needed, as `b[1] < b[3]`.
   - After this iteration, `a = [0, 2, 5, 6]` and `b = [1, 3, 4, 7, 8]`.
5. Iteration 3 (`gap = 1`):
   - `left = 0`, `right = 1`
   - No swap is needed, as `a[0] < a[1]`.
   - `left = 1`, `right = 2`
   - Swap `a[1]` (2) and `a[2]` (5), as `a[1] > a[2]`.
   - `left = 2`, `right = 3`
   - No swap is needed, as `a[2] < a[3]`.
   - `left = 3`, `right = 4`
   - Swap `b[0]` (1) and `b[1]` (3), as `b[0] > b[1]`.
   - `left = 4`, `right = 5`
   - No swap is needed, as `b[2] < b[3]`.
   - After this iteration, `a = [0, 2, 5, 6]` and `b = [1, 3, 4, 7, 8]`.
6. The loop terminates, and the arrays `a` and `b` are now merged and sorted: `[0, 1, 2, 3, 4, 5, 6, 7, 8]`.

Java code:

```java
class Solution {
     public static void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m - 1;
        int j = n - 1;
        int k = m + n - 1;

        while (i >= 0 && j >= 0) {
            if (nums1[i] > nums2[j]) {
                nums1[k] = nums1[i];
                i--;
            } else {
                nums1[k] = nums2[j];
                j--;
            }
            k--;
        }

        while (i >= 0) {
            nums1[k] = nums1[i];
            i--;
            k--;
        }

        while (j >= 0) {
            nums1[k] = nums2[j];
            j--;
            k--;
        }
    }
}
```

**Possible Optimizations:**

The given code is already optimized for the problem of merging two sorted arrays without extra space. However, there is an alternative approach that can be considered:

**Alternative Approach: Gap Method with Optimized Gap Sequence**

Instead of using the gap sequence `(gap/2) + (gap%2)`, which is not as efficient, we can use a more optimized gap sequence proposed by Robert Sedgewick. This sequence provides better performance for the shell sort algorithm.

The optimized gap sequence is:

```
9, 5, 3, 1
```

Here's the optimized code using this gap sequence:

```java
public class Solution {
    public static void mergeTwoSortedArraysWithoutExtraSpace(long[] a, long[] b) {
        int n = a.length;
        int m = b.length;
        int len = n + m;
        int[] gaps = {9, 5, 3, 1}; // Optimized gap sequence

        for (int gap : gaps) {
            int left = 0;
            int right = left + gap;
            while (right < len) {
                if (left < n && right >= n) {
                    swap(a, b, left, right - n);
                } else if (left >= n) {
                    swap(b, b, left - n, right - n);
                } else {
                    swap(a, a, left, right);
                }
                left++;
                right++;
            }
        }
    }

    public static void swap(long[] a, long[] b, int x, int y) {
        if (a[x] > b[y]) {
            long temp = a[x];
            a[x] = b[y];
            b[y] = temp;
        }
    }
}
```

In this optimized code, we use a hardcoded array `gaps` containing the optimized gap sequence `[9, 5, 3, 1]`. The rest of the code remains the same, but it performs fewer iterations due to the optimized gap sequence.

This optimization may provide better performance for larger input sizes, as the gap sequence is more efficient than the `(gap/2) + (gap%2)` sequence used in the original code.

## 7-05-2024

**33. 4 Sum**

[4 Sum (CodeStudio)](https://www.naukri.com/code360/problems/4sum_5713771?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

[4 Sum (Leetcode)](https://leetcode.com/problems/4sum/description/)

You are given an array ‘NUMS’ of length ‘N’. You are also given an integer ‘TARGET’.

Return an array of all the unique quadruplets [ ‘NUMS[ a ]’, ‘NUMS[ b ]’, ‘NUMS[ c ]’, ‘NUMS[ d ]’ ] with the following conditions:

i. 0 <= a, b, c, d < ‘N’ and a, b, c, and d are distinct.

ii. NUMS[ a ] + NUMS[ b ] + NUMS[ c ] +NUMS[ d ] = TARGET

Return the array in any order.

Note:

(NUMS[ a ], NUMS[ b ], NUMS[ c ], NUMS[ d ]), (NUMS[ a ], NUMS[ d ], NUMS[ c ], NUMS[ b ]), (NUMS[ a ], NUMS[ c ], NUMS[ b ], NUMS[ d ])... all of them are treated or considered the same quadruplets.

Two quadruplets are different if there is any integer in one quadruplet which is not in the other.

The solution will be verified by the number of valid quadruplets returned. In the output, only the number of valid quadruplets will be printed.

Example:
Input: ‘N’ = 5, ‘TARGET’ = 5, ‘NUMS’ = [ 1, 2, 1, 0, 1 ]

Output: 1.

There is only one unique quadruplet with sum = 5 and that is [1, 2, 1, 1].

**Pseudocode with Explanation (Time Complexity and Space Complexity):**

```
1. Sort the input array nums in ascending order
2. Initialize an empty list ans to store the quadruplets
3. Iterate through the array with a variable i from 0 to length - 4
    a. If i > 0 and nums[i] is the same as nums[i-1], skip this iteration (to avoid duplicates)
    b. Iterate through the array with a variable j from i + 1 to length - 3
        i. If j > i + 1 and nums[j] is the same as nums[j-1], skip this iteration (to avoid duplicates)
        ii. Initialize two pointers, l = j + 1 and r = length - 1
        iii. While l < r:
            1. Calculate the sum of nums[i], nums[j], nums[l], and nums[r]
            2. If the sum is equal to the target:
                a. Add the quadruplet [nums[i], nums[j], nums[l], nums[r]] to ans
                b. Move l and r inwards until they point to different values (to avoid duplicates)
            3. If the sum is less than the target, increment l (to increase the sum)
            4. If the sum is greater than the target, decrement r (to decrease the sum)
4. Return ans
```

**Time Complexity:** O(n^3), where n is the length of the input array `nums`. The sorting step takes O(n log n), and the nested loops have a time complexity of O(n^3).

**Space Complexity:** O(n), where n is the length of the input array `nums`. In the worst case, the output list `ans` could contain O(n^3) quadruplets, but the space required for the sorted array and the pointers is O(n).

**Explanation with Example:**

Let's consider the example `nums = [1, 0, -1, 0, -2, 2]` and `target = 0`.

1. The array is sorted: `nums = [-2, -1, 0, 0, 1, 2]`.
2. An empty list `ans` is initialized to store the quadruplets.
3. The outer loop starts with `i = 0` and `nums[i] = -2`.
   - The inner loop starts with `j = 1` and `nums[j] = -1`.
   - `l = 2` and `r = 5` (initially pointing to the third and last elements).
   - While `l < r`:
     - `sum = nums[i] + nums[j] + nums[l] + nums[r] = -2 + (-1) + 0 + 2 = -1 < 0`, so `l` is incremented to 3.
     - `sum = nums[i] + nums[j] + nums[l] + nums[r] = -2 + (-1) + 0 + 1 = -2 < 0`, so `l` is incremented to 4.
     - `sum = nums[i] + nums[j] + nums[l] + nums[r] = -2 + (-1) + 1 + 1 = -1 < 0`, so `l` is incremented to 5, which is not less than `r`, so the inner loop terminates.
4. The inner loop continues with `j = 2` and `nums[j] = 0`.
   - `l = 3` and `r = 5` (initially pointing to the fourth and last elements).
   - While `l < r`:
     - `sum = nums[i] + nums[j] + nums[l] + nums[r] = -2 + 0 + 0 + 2 = 0`, so the quadruplet `[-2, 0, 0, 2]` is added to `ans`. `l` is incremented to 4, and `r` is decremented to 4, which is not less than `l`, so the inner loop terminates.
5. The outer loop continues with `i = 1` and `nums[i] = -1`.
   - The inner loop starts with `j = 2` and `nums[j] = 0`.
   - `l = 3` and `r = 5` (initially pointing to the fourth and last elements).
   - While `l < r`:
     - `sum = nums[i] + nums[j] + nums[l] + nums[r] = -1 + 0 + 0 + 2 = 1 > 0`, so `r` is decremented to 4.
     - `sum = nums[i] + nums[j] + nums[l] + nums[r] = -1 + 0 + 0 + 1 = 0`, so the quadruplet `[-1, 0, 0, 1]` is added to `ans`. `l` is incremented to 4, and `r` is decremented to 3, which is not less than `l`, so the inner loop terminates.
6. The outer loop continues with `i = 2` and `nums[i] = 0`, but since `nums[i]` is the same as `nums[i-1]`, this iteration is skipped to avoid duplicates.
7. The outer loop continues with `i = 3` and `nums[i] = 0`, but since `nums[i]` is the same as `nums[i-1]`, this iteration is skipped to avoid duplicates.
8. The outer loop continues with `i = 4` and `nums[i] = 1`.
   - The inner loop starts with `j = 5` and `nums[j] = 2`.
   - `l = 6` and `r = 6` (initially pointing to the last element).
   - While `l < r`: This condition is false, so the inner loop is not executed.
9. The outer loop terminates, and the list `ans` containing the quadruplets `[-2, 0, 0, 2]` and `[-1, 0, 0, 1]` is returned.

Java code:

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target)
    {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(nums);
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            if (i > 0 && nums[i] == nums[i - 1])
                continue;
            for (int j = i + 1; j < n; j++) {
                if (j > i + 1 && nums[j] == nums[j - 1])
                    continue;
                int l = j + 1, r = n - 1;
                while (l < r) {
                    long sum = (long) nums[i] + nums[j] + nums[l] + nums[r];
                    if (sum == target) {
                        ans.add(Arrays.asList(nums[i], nums[j], nums[l], nums[r]));
                        l++;
                        r--;
                        while (l < r && nums[l] == nums[l - 1])
                            l++;
                        while (l < r && nums[r] == nums[r + 1])
                            r--;
                    } else if (sum < target)
                        l++;
                    else
                        r--;
                }
            }
        }
        return ans;

    }
}
```

**Possible Optimizations:**

The given code is already optimized for the "4Sum" problem, as it avoids duplicates and has an optimal time complexity of O(n^3). However, there is a potential optimization that can be made to reduce the time complexity further for certain input distributions.

**Optimization: Using a Hashmap**

If the input array contains many duplicate elements, we can use a HashMap to store the frequency of each element. This way, we can skip over duplicate elements more efficiently and reduce the time complexity in some cases.

Here's the optimized code using a HashMap:

```java
public List<List<Integer>> fourSum(int[] nums, int target) {
    List<List<Integer>> ans = new ArrayList<>();
    int n = nums.length;
    if (n < 4) return ans;

    // Store the frequency of each element in a HashMap
    Map<Integer, Integer> freq = new HashMap<>();
    for (int num : nums) {
        freq.put(num, freq.getOrDefault(num, 0) + 1);
    }

    // Sort the array
    Arrays.sort(nums);

    for (int i = 0; i < n - 3; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue; // Skip duplicates for i
        int target1 = target - nums[i];
        for (int j = i + 1; j < n - 2; j++) {
            if (j > i + 1 && nums[j] == nums[j - 1]) continue; // Skip duplicates for j
            int target2 = target1 - nums[j];
            int l = j + 1, r = n - 1;
            while (l < r) {
                int sum = nums[l] + nums[r];
                if (sum == target2) {
                    ans.add(Arrays.asList(nums[i], nums[j], nums[l], nums[r]));
                    while (l < r && nums[l] == nums[l + 1]) l++; // Skip duplicates for l
                    while (l < r && nums[r] == nums[r - 1]) r--; // Skip duplicates for r
                    l++;
                }
            }
        }
    }
    return ans;
}
```

**34. Subarrays with XOR ‘K’**

[Count number of subarrays with given xor K (CodeStudio)](https://www.naukri.com/code360/problems/subarrays-with-xor-k_6826258?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

Given an array ‘A’ consisting of ‘N’ integers and an integer ‘B’, find the number of subarrays of array ‘A’ whose bitwise XOR( ⊕ ) of all elements is equal to ‘B’.

A subarray of an array is obtained by removing some(zero or more) elements from the front and back of the array.

Example:
Input: ‘N’ = 4 ‘B’ = 2
‘A’ = [1, 2, 3, 2]

Output: 3

Explanation: Subarrays have bitwise xor equal to ‘2’ are: [1, 2, 3, 2], [2], [2].

**Pseudocode with Explanation (Time Complexity and Space Complexity):**

```
1. Initialize n with the length of the input array a
2. Initialize a HashMap mpp to store the cumulative XOR and its frequency
3. Initialize xor to 0 (to keep track of the cumulative XOR)
4. Initialize count to 0 (to store the count of subarrays with sum k)
5. Put 0 and 1 in the HashMap mpp (to handle the case where the subarray starts from the beginning and has a sum of k)
6. Iterate through the array a:
    a. Update xor by performing XOR with the current element a[i]
    b. Calculate x as xor ^ k (this is the cumulative XOR we need to find in the HashMap)
    c. If x is present in the HashMap:
        i. Increment count by the frequency of x in the HashMap
    d. If xor is present in the HashMap:
        i. Get the current frequency of xor from the HashMap
        ii. Increment the frequency by 1 and update the HashMap with the new frequency
    e. If xor is not present in the HashMap:
        i. Put xor and 1 in the HashMap (as this is the first occurrence of this cumulative XOR)
7. Return count
```

**Time Complexity:** O(n), where n is the length of the input array `a`. We iterate through the array once, and the HashMap operations (get and put) have an average time complexity of O(1).

**Space Complexity:** O(n), where n is the length of the input array `a`. In the worst case, when all elements are distinct, the HashMap will store all elements and their frequencies, resulting in a space complexity of O(n).

**Explanation with Example:**

Let's consider the example `a = [1, 2, 3]` and `k = 3`.

1. Initially, `n = 3`, `mpp = {}`, `xor = 0`, and `count = 0`.
2. `mpp.put(0, 1)` initializes the HashMap with `0` as the key and `1` as the value.
3. Iteration 1 (`i = 0`):
   - `xor = 0 ^ 1 = 1`
   - `x = 1 ^ 3 = 2`
   - The HashMap doesn't contain the key `2`, so `count` remains unchanged.
   - The HashMap doesn't contain the key `1`, so `mpp.put(1, 1)` adds the key-value pair `1` and `1` to the HashMap.
4. Iteration 2 (`i = 1`):
   - `xor = 1 ^ 2 = 3`
   - `x = 3 ^ 3 = 0`
   - The HashMap contains the key `0`, so `count += mpp.getOrDefault(0, 0) = count += 1 = 1`.
   - The HashMap contains the key `3`, so `mpp.put(3, mpp.getOrDefault(3, 0) + 1) = mpp.put(3, 1 + 1) = mpp.put(3, 2)` updates the frequency of `3` to `2`.
5. Iteration 3 (`i = 2`):
   - `xor = 3 ^ 3 = 0`
   - `x = 0 ^ 3 = 3`
   - The HashMap contains the key `3`, so `count += mpp.getOrDefault(3, 0) = count += 2 = 3`.
   - The HashMap contains the key `0`, so `mpp.put(0, mpp.getOrDefault(0, 0) + 1) = mpp.put(0, 1 + 1) = mpp.put(0, 2)` updates the frequency of `0` to `2`.
6. The loop terminates, and the count of subarrays with sum `k = 3` is `3`.

Java Code:

```java
 public static int subarraysWithSumK(int []a, int b) {
        int n = a.length;
        HashMap<Integer,Integer> mpp = new HashMap<>();
        int xor =0, count =0;
        mpp.put(0,1);
        for(int i=0;i<n;i++){
            xor ^= a[i];
            int x = xor^b;
            if(mpp.containsKey(x)) count += mpp.getOrDefault(x,0);
            if(mpp.containsKey(xor)){
                int val = mpp.getOrDefault(xor,0);
                mpp.put(xor,val+1);
            }
            else
            mpp.put(xor,1);
        }
        return count;
    }
```

**Possible Optimizations:**

The given code is already optimized and has a time complexity of O(n) and a space complexity of O(n). However, there is a potential optimization that can be made to reduce the space complexity in some cases.

**Optimization: Using a Single Integer Variable Instead of a HashMap**

If the input array contains only non-negative integers, we can use a single integer variable to store the cumulative XOR instead of a HashMap. This optimization reduces the space complexity to O(1) but works only for non-negative input arrays.

Here's the optimized code using a single integer variable:

```java
public static int subarraysWithSumK(int[] a, int k) {
    int n = a.length;
    int xor = 0, count = 0;
    int[] freq = new int[n + 1]; // Frequency array to store the count of each cumulative XOR
    freq[0] = 1; // Initialize the frequency of 0 to 1

    for (int i = 0; i < n; i++) {
        xor ^= a[i];
        int x = xor ^ k;
        if (x >= 0 && x < n) {
            count += freq[x];
        }
        freq[xor]++;
    }

    return count;
}
```

In this optimized code, we use an integer array `freq` of size `n + 1` to store the frequency of each cumulative XOR. We initialize `freq[0]` to `1` to handle the case where the subarray starts from the beginning and has a sum of `k`.

During the loop, we update `xor` by performing XOR with the current element `a[i]`. We calculate `x` as `xor ^ k`, which represents the cumulative XOR we need to find in the frequency array. If `x` is within the bounds of the frequency array (i.e., non-negative and less than `n`), we increment `count` by the frequency of `x` in the frequency array. Finally, we increment the frequency of the current cumulative XOR (`xor`) in the frequency array.

This optimization works only for non-negative input arrays because the cumulative XOR will always be non-negative. If the input array contains negative integers, the cumulative XOR can be negative, and we won't be able to store and retrieve its frequency using an integer array efficiently.

The time complexity of this optimized solution remains O(n), but the space complexity is reduced to O(1) (or O(min(n, max_element_in_array + 1)) to be more precise) for non-negative input arrays.

**35. Missing and repeating numbers**

[Missing and repeating numbers (CodeStudio)](https://www.naukri.com/code360/problems/missing-and-repeating-numbers_6828164?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf)

You are given an array of ‘N’ integers where each integer value is between ‘1’ and ‘N’. Each integer appears exactly once except for ‘P’, which appears exactly twice, and ‘Q’, which is missing.

Your task is to find ‘P’ and ‘Q’ and return them respectively.

Detailed explanation ( Input/output format, Notes, Images )
Constraints:
2 <= N <= 5 \* 10^4
1 <= data <= N

Where ‘N’ is the size of the array and ‘data’ denotes the value of the elements of the array.

**Pseudocode with Explanation (Time Complexity and Space Complexity):**

```
1. Initialize an array ans of size 2 with -1 as the initial values
2. Initialize n with the length of the input array a
3. Initialize p and q with -1 (to store the repeating and missing numbers, respectively)
4. Iterate through the array a:
    a. Calculate index as Math.abs(a[i]) - 1 (since array elements are in the range [1, n])
    b. If a[index] is positive:
        i. Make a[index] negative by multiplying it with -1
        ii. Set p to index + 1 (as this is the repeating number)
5. Iterate through the array a again:
    a. If a[i] is positive and not equal to p:
        i. Set q to i + 1 (as this is the missing number)
6. Set ans[0] to p and ans[1] to q
7. Return ans
```

**Time Complexity:** O(n), where n is the length of the input array `a`. We iterate through the array twice, but the overall time complexity is O(n).

**Space Complexity:** O(1), as we are using constant extra space to store the result in the `ans` array and the auxiliary variables `p` and `q`.

**Explanation with Example:**

Let's consider the example `a = [1, 3, 3]`.

1. Initially, `ans = [-1, -1]`, `n = 3`, `p = -1`, and `q = -1`.
2. Iteration 1 (`i = 0`):
   - `index = Math.abs(a[0]) - 1 = Math.abs(1) - 1 = 0`
   - `a[index] = a[0] = -1` (since `a[0]` is positive, we make it negative)
3. Iteration 2 (`i = 1`):
   - `index = Math.abs(a[1]) - 1 = Math.abs(3) - 1 = 2`
   - `a[index] = a[2] = -3` (since `a[2]` is already negative, we don't change it)
   - `p = 3` (since `a[2]` is negative, we set `p` to the repeating number)
4. Iteration 3 (`i = 2`):
   - `index = Math.abs(a[2]) - 1 = Math.abs(3) - 1 = 2`
   - `a[index] = a[2] = -3` (since `a[2]` is already negative, we don't change it)
5. Iteration 1 of the second loop (`i = 0`):
   - `a[0] = -1` (negative)
   - `p != 1` (since `p = 3`)
6. Iteration 2 of the second loop (`i = 1`):
   - `a[1] = 3` (positive)
   - `p != 2` (since `p = 3`)
   - `q = 2` (since `a[1]` is positive and not equal to `p`, we set `q` to the missing number)
7. Iteration 3 of the second loop (`i = 2`):
   - `a[2] = -3` (negative)
   - `p != 3` (since `p = 3`)
8. `ans[0] = 3` (repeating number) and `ans[1] = 2` (missing number)
9. The array `ans = [3, 2]` is returned.

Java code:

```java
public static int[] findMissingRepeatingNumbers(int []a) {
        int[] ans = {-1,-1};
       int n=a.length;
       int p=-1,q=-1;
       for(int i=0;i<n;i++){
           int index = Math.abs(a[i])-1;
           a[index] = -1*a[index];
           if(a[index]>0){
               p=index+1;
           }
       }
       for(int i=0;i<n;i++){
           if(a[i]>0 && p!= i+1){
               q=i+1;
           }
       }
       ans[0]=p;
       ans[1]=q;
       return ans;
    }
```

**Possible Optimizations:**

The given code is already optimized and has a time complexity of O(n) and a space complexity of O(1). It uses a neat trick to mark the elements as visited by negating them and then uses the negated values to find the missing and repeating numbers.

However, there is a slight optimization that can be made to handle edge cases more gracefully:

```java
public static int[] findMissingRepeatingNumbers(int[] a) {
    int[] ans = {-1, -1};
    int n = a.length;
    int p = -1, q = -1;

    for (int i = 0; i < n; i++) {
        int index = Math.abs(a[i]) - 1;
        if (a[index] < 0) {
            p = Math.abs(a[i]);
        } else {
            a[index] = -a[index];
        }
    }

    for (int i = 0; i < n; i++) {
        if (a[i] > 0) {
            q = i + 1;
        }
    }

    ans[0] = p;
    ans[1] = q;
    return ans;
}
```

In this optimized code, we handle the case where an element is negative in the input array. If we encounter a negative element, we set `p` to the absolute value of that element, as it is the repeating number.

The main advantage of this optimization is that it handles edge cases more gracefully. For example, if the input array is `[-1, -1]`, the original code would incorrectly set `p` to `2`, while the optimized code would correctly set `p` to `1`.

The time complexity and space complexity of this optimized code remain O(n) and O(1), respectively, but it provides better handling of edge cases involving negative numbers in the input array.

**36. Number of Inversions**

[Number of Inversions](https://www.naukri.com/code360/problems/number-of-inversions_6840276?utm_source=striver&utm_medium=website&utm_campaign=a_zcoursetuf&leftPanelTabValue=PROBLEM)

There is an integer array ‘A’ of size ‘N’.

Number of inversions in an array can be defined as the number of pairs of ‘i’, ‘j’ such that ‘i’ < ‘j’ and ‘A[i]’ > ‘A[j]’.

You must return the number of inversions in the array.

For example,
Input:
A = [5, 3, 2, 1, 4], N = 5
Output:
7
Explanation:
The pairs satisfying the condition for inversion are (1, 2), (1, 3), (1, 4), (1, 5), (2, 3), (2, 4), and (3, 4).
The number of inversions in the array is 7.

**Pseudocode with Explanation (Time Complexity and Space Complexity):**

```
1. Initialize i and j as 0 and i + 1, respectively
2. Initialize count as 0 (to store the number of inversions)
3. While i is less than n and j is less than n:
    a. If a[i] is greater than a[j] and i is less than j:
        i. Increment count by 1
    b. Increment j by 1
    c. If j is equal to n:
        i. Increment i by 1
        ii. Set j to i + 1
4. Return count
```

**Time Complexity:** O(n^2), where n is the length of the input array `a`. The nested loops iterate through all possible pairs of elements, resulting in a time complexity of O(n^2).

**Space Complexity:** O(1), as the code uses constant extra space to store the variables `i`, `j`, and `count`.

**Explanation with Example:**

Let's consider the example `a = [3, 1, 2]` and `n = 3`.

1. Initially, `i = 0`, `j = 1`, and `count = 0`.
2. Iteration 1:
   - `a[i] = 3` and `a[j] = 1`
   - `a[i] > a[j]` and `i < j`, so `count` is incremented to 1
   - `j` is incremented to 2
3. Iteration 2:
   - `a[i] = 3` and `a[j] = 2`
   - `a[i] > a[j]` and `i < j`, so `count` is incremented to 2
   - `j` is incremented to 3
   - `j = 3` is equal to `n`, so `i` is incremented to 1, and `j` is set to `i + 1 = 2`
4. Iteration 3:
   - `a[i] = 1` and `a[j] = 2`
   - `a[i] < a[j]` and `i < j`, so `count` remains unchanged
   - `j` is incremented to 3
   - `j = 3` is equal to `n`, so the loop terminates
5. The function returns `count = 2`, which is the number of inversions in the array `[3, 1, 2]`.

```java
public class Solution {
    public static int numberOfInversions(int []a, int n) {
        int i=0;
        int j=i+1;
        int count=0;

        while(i<n&& j<n)
        {
                if(a[i]>a[j] && i<j)
                {
                    count++;
                }
                j++;
                if(j==n)
                {
                    i++;
                    j=i+1;
                }
        }
        return count;
    }
}
```

**Possible Optimizations:**

The given code has a time complexity of O(n^2), which is not optimal for large input sizes. There is a more efficient way to find the number of inversions in an array using the Merge Sort algorithm. The optimized solution has a time complexity of O(n log n) and a space complexity of O(n).

Here's the optimized code using the Merge Sort algorithm:

```java
public static int numberOfInversions(int[] a, int n) {
    int[] temp = new int[n];
    return mergeSort(a, temp, 0, n - 1);
}

private static int mergeSort(int[] a, int[] temp, int left, int right) {
    int mid, inversions = 0;

    if (right > left) {
        mid = (right + left) / 2;
        inversions += mergeSort(a, temp, left, mid); // Inversions in the left subarray
        inversions += mergeSort(a, temp, mid + 1, right); // Inversions in the right subarray
        inversions += merge(a, temp, left, mid + 1, right); // Inversions in the merged subarray
    }

    return inversions;
}

private static int merge(int[] a, int[] temp, int left, int mid, int right) {
    int i, j, k, inversions = 0;

    i = left;
    j = mid;
    k = left;

    while ((i <= mid - 1) && (j <= right)) {
        if (a[i] <= a[j]) {
            temp[k++] = a[i++];
        } else {
            temp[k++] = a[j++];
            inversions += (mid - i); // Count the inversions
        }
    }

    while (i <= mid - 1) {
        temp[k++] = a[i++];
    }

    while (j <= right) {
        temp[k++] = a[j++];
    }

    for (i = left; i <= right; i++) {
        a[i] = temp[i];
    }

    return inversions;
}
```

In this optimized solution, we use the Merge Sort algorithm to sort the array while counting the number of inversions. The `mergeSort` function recursively divides the array into two halves, sorts them, and then merges them while counting the inversions.

The `merge` function combines the two sorted subarrays while counting the inversions. If an element from the right subarray is smaller than an element from the left subarray, it means there are `(mid - i)` inversions involving the element from the left subarray.

The time complexity of this optimized solution is O(n log n), which is more efficient than the previous solution's O(n^2) time complexity, especially for large input sizes. The space complexity is O(n) due to the temporary array used for merging.

This optimization significantly improves the performance of the algorithm for finding the number of inversions in an array.
 
## 8-05-2023

**37. Binary Search**

Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.

You must write an algorithm with O(log n) runtime complexity.

Example 1:

Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
Example 2:

Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1

The given code is an implementation of the Binary Search algorithm, which is used to find the index of a target element in a sorted array.

**Pseudocode with Explanation (Time Complexity and Space Complexity):**

```
1. Initialize l as 0 (the leftmost index of the array)
2. Initialize h as the length of the array - 1 (the rightmost index of the array)
3. While l is less than or equal to h:
    a. Calculate the middle index mid as (l + h) / 2
    b. If the element at the middle index (nums[mid]) is equal to the target:
        i. Return mid (as the target element is found)
    c. If the element at the middle index (nums[mid]) is greater than the target:
        i. Update h to mid - 1 (as the target element must be in the left subarray)
    d. Otherwise:
        i. Update l to mid + 1 (as the target element must be in the right subarray)
4. If the loop completes without finding the target, return -1 (as the target element is not present in the array)
```

**Time Complexity:** O(log n), where n is the length of the input array `nums`. In each iteration, the search space is halved, resulting in a logarithmic time complexity.

**Space Complexity:** O(1), as the code uses constant extra space to store the variables `l`, `h`, and `mid`.

**Explanation with Example:**

Let's consider the example `nums = [1, 3, 5, 7, 9]` and `target = 5`.

1. Initially, `l = 0` and `h = 4` (since the length of the array is 5).
2. Iteration 1:
   - `mid = (0 + 4) / 2 = 2`
   - `nums[mid] = nums[2] = 5`
   - `nums[mid] == target`, so the function returns `mid = 2` (the index of the target element).
3. The function terminates and returns 2, which is the index of the target element 5 in the array.

Now, let's consider another example `nums = [1, 3, 5, 7, 9]` and `target = 6`.

1. Initially, `l = 0` and `h = 4`.
2. Iteration 1:
   - `mid = (0 + 4) / 2 = 2`
   - `nums[mid] = nums[2] = 5`
   - `nums[mid] < target`, so `l` is updated to `mid + 1 = 3`.
3. Iteration 2:
   - `mid = (3 + 4) / 2 = 3`
   - `nums[mid] = nums[3] = 7`
   - `nums[mid] > target`, so `h` is updated to `mid - 1 = 2`.
4. Iteration 3:
   - `mid = (3 + 2) / 2 = 2`
   - `nums[mid] = nums[2] = 5`
   - `nums[mid] < target`, so `l` is updated to `mid + 1 = 3`.
5. Iteration 4:
   - `mid = (3 + 2) / 2 = 2` (the same as the previous iteration)
   - `l = 3` and `h = 2`, so the loop terminates as `l > h`.
6. The function returns -1, as the target element 6 is not present in the array.


Java Code:

```java
public int search(int[] nums, int target) {
    int l = 0;
    int h = nums.length - 1;
    
    while (l <= h) {
        int mid = (h + l) / 2; 
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] > target) {
            h = mid - 1;
        } else {
            l = mid + 1;
        }
    }
    
    return -1;
}
```

**Possible Optimizations:**

The given code is already an optimized implementation of the Binary Search algorithm. However, there is a slight optimization that can be made to handle the case where the sum of `l` and `h` overflows the maximum value of an integer.

Here's the optimized code:

```java
public int search(int[] nums, int target) {
    int l = 0;
    int h = nums.length - 1;
    
    while (l <= h) {
        int mid = l + (h - l) / 2; // Handles the case when (l + h) overflows
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] > target) {
            h = mid - 1;
        } else {
            l = mid + 1;
        }
    }
    
    return -1;
}
```

In this optimized code, we calculate the middle index `mid` as `l + (h - l) / 2` instead of `(l + h) / 2`. This ensures that the calculation does not overflow even when `l` and `h` are large integers.

The time complexity and space complexity of this optimized solution remain the same: O(log n) and O(1), respectively. However, this optimization provides better handling of edge cases involving large integers and prevents potential integer overflow issues.

## 9-05-2024

**38. Implement Lower Bound**

[Implement Lower Bound](https://www.geeksforgeeks.org/problems/floor-in-a-sorted-array-1587115620/1?track=DSASP-Searching&amp%253BbatchId=154&utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=floor-in-a-sorted-array)

Given a sorted array arr[] of size N without duplicates, and given a value x. Floor of x is defined as the largest element K in arr[] such that K is smaller than or equal to x. Find the index of K(0-based indexing).

Example 1:

Input:
N = 7, x = 0 

arr[] = {1,2,8,10,11,12,19}

Output: -1

Explanation: No element less 
than 0 is found. So output 
is "-1".

Example 2:

Input:
N = 7, x = 5 

arr[] = {1,2,8,10,11,12,19}

Output: 1

Explanation: Largest Number less than 5 is
2 (i.e K = 2), whose index is 1(0-based 
indexing).

The given code is an implementation of the Lower Bound function in Java, which finds the index of the smallest element in a sorted array that is greater than or equal to a given target value `x`.

**Pseudocode with Explanation (Time Complexity and Space Complexity):**

```
1. Initialize low as 0 (the leftmost index of the array)
2. Initialize high as n - 1 (the rightmost index of the array)
3. Initialize ans as n (a value greater than the maximum possible index)
4. While low is less than or equal to high:
    a. Calculate the middle index mid as (low + high) / 2
    b. If the element at the middle index (arr[mid]) is greater than or equal to x:
        i. Update ans to mid (since this is a potential lower bound)
        ii. Update high to mid - 1 (to look for a smaller index on the left)
    c. Otherwise:
        i. Update low to mid + 1 (to look for a greater value on the right)
5. Return ans (the lower bound index)
```

**Time Complexity:** O(log n), where n is the length of the input array `arr`. In each iteration, the search space is halved, resulting in a logarithmic time complexity.

**Space Complexity:** O(1), as the code uses constant extra space to store the variables `low`, `high`, `ans`, and `mid`.

**Explanation with Example:**

Let's consider the example `arr = [3, 5, 8, 15, 19]`, `n = 5`, and `x = 9`.

1. Initially, `low = 0`, `high = 4`, and `ans = 5`.
2. Iteration 1:
   - `mid = (0 + 4) / 2 = 2`
   - `arr[mid] = arr[2] = 8`
   - `arr[mid] < x`, so `low` is updated to `mid + 1 = 3`.
3. Iteration 2:
   - `mid = (3 + 4) / 2 = 3`
   - `arr[mid] = arr[3] = 15`
   - `arr[mid] >= x`, so `ans` is updated to `mid = 3`, and `high` is updated to `mid - 1 = 2`.
4. Iteration 3:
   - `mid = (3 + 2) / 2 = 2`
   - `arr[mid] = arr[2] = 8`
   - `arr[mid] < x`, so `low` is updated to `mid + 1 = 3`.
5. Iteration 4:
   - `mid = (3 + 2) / 2 = 2` (the same as the previous iteration)
   - `low = 3` and `high = 2`, so the loop terminates as `low > high`.
6. The function returns `ans = 3`, which is the index of the smallest element in the array that is greater than or equal to `x = 9`.

Java code:

```java

import java.util.*;

public class tUf {

    public static int lowerBound(int []arr, int n, int x) {
        int low = 0, high = n - 1;
        int ans = n;

        while (low <= high) {
            int mid = (low + high) / 2;
            // maybe an answer
            if (arr[mid] >= x) {
                ans = mid;
                //look for smaller index on the left
                high = mid - 1;
            } else {
                low = mid + 1; // look on the right
            }
        }
        return ans;
    }

    public static void main(String[] args) {
        int[] arr = {3, 5, 8, 15, 19};
        int n = 5, x = 9;
        int ind = lowerBound(arr, n, x);
        System.out.println("The lower bound is the index: " + ind);
    }
} 
```

**Possible Optimizations:**

The given code is already an optimized implementation of the Lower Bound function. However, there is a slight optimization that can be made to handle the case where the sum of `low` and `high` overflows the maximum value of an integer.

Here's the optimized code:

```java
import java.util.*;

public class tUf {

    public static int lowerBound(int[] arr, int n, int x) {
        int low = 0, high = n;
        
        while (low < high) {
            int mid = low + (high - low) / 2; // Handles the case when (low + high) overflows
            
            if (arr[mid] >= x) {
                high = mid;
            } else {
                low = mid + 1;
            }
        }
        
        return high < n && arr[high] < x ? n : high;
    }

    public static void main(String[] args) {
        int[] arr = {3, 5, 8, 15, 19};
        int n = 5, x = 9;
        
        int ind = lowerBound(arr, n, x);
        System.out.println("The lower bound is the index: " + ind);
    }
}
```

In this optimized code, we calculate the middle index `mid` as `low + (high - low) / 2` instead of `(low + high) / 2`. This ensures that the calculation does not overflow even when `low` and `high` are large integers.

Additionally, we handle the case where the target value `x` is greater than all elements in the array. If `high` is less than `n` and the element at `high` is still less than `x`, we return `n` as the lower bound index. Otherwise, we return `high`.

The time complexity and space complexity of this optimized solution remain the same: O(log n) and O(1), respectively. However, this optimization provides better handling of edge cases involving large integers and prevents potential integer overflow issues.

**39. Implement Upper Bound**

[Implement Upper Bound](https://www.geeksforgeeks.org/problems/ceil-the-floor2802/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=ceil-the-floor)

Given an unsorted array Arr[] of N integers and an integer X, find floor and ceiling of X in Arr[0..N-1].

Ceil of X is the smallest element which is greater than or equal to X. Ceil of X doesn’t exist if X is greater than greatest element of Arr[].

Example 1:

Input:
N = 8, X = 7

Arr[] = {5, 6, 8, 9, 6, 5, 5, 6}

Output: 6 8

Explanation:
Floor of 7 is 6 and ceil of 7 
is 8.

Example 2:

Input:
N = 8, X = 10

Arr[] = {5, 6, 8, 9, 6, 5, 5, 6}

Output: 9 -1

Explanation:
Floor of 10 is 9 but ceil of 10 is not 
possible.

The given code is an implementation of the Upper Bound function in Java, which finds the index of the smallest element in a sorted array that is strictly greater than a given target value `x`.

**Pseudocode with Explanation (Time Complexity and Space Complexity):**

```
1. Initialize low as 0 (the leftmost index of the array)
2. Initialize high as n - 1 (the rightmost index of the array)
3. Initialize ans as n (a value greater than the maximum possible index)
4. While low is less than or equal to high:
    a. Calculate the middle index mid as (low + high) / 2
    b. If the element at the middle index (arr[mid]) is strictly greater than x:
        i. Update ans to mid (since this is a potential upper bound)
        ii. Update high to mid - 1 (to look for a smaller index on the left)
    c. Otherwise:
        i. Update low to mid + 1 (to look for a greater value on the right)
5. Return ans (the upper bound index)
```

**Time Complexity:** O(log n), where n is the length of the input array `arr`. In each iteration, the search space is halved, resulting in a logarithmic time complexity.

**Space Complexity:** O(1), as the code uses constant extra space to store the variables `low`, `high`, `ans`, and `mid`.

**Explanation with Example:**

Let's consider the example `arr = [3, 5, 8, 9, 15, 19]`, `n = 6`, and `x = 9`.

1. Initially, `low = 0`, `high = 5`, and `ans = 6`.
2. Iteration 1:
   - `mid = (0 + 5) / 2 = 2`
   - `arr[mid] = arr[2] = 8`
   - `arr[mid] <= x`, so `low` is updated to `mid + 1 = 3`.
3. Iteration 2:
   - `mid = (3 + 5) / 2 = 4`
   - `arr[mid] = arr[4] = 15`
   - `arr[mid] > x`, so `ans` is updated to `mid = 4`, and `high` is updated to `mid - 1 = 3`.
4. Iteration 3:
   - `mid = (3 + 3) / 2 = 3`
   - `arr[mid] = arr[3] = 9`
   - `arr[mid] <= x`, so `low` is updated to `mid + 1 = 4`.
5. Iteration 4:
   - `mid = (4 + 3) / 2 = 3` (the same as the previous iteration)
   - `low = 4` and `high = 3`, so the loop terminates as `low > high`.
6. The function returns `ans = 4`, which is the index of the smallest element in the array that is strictly greater than `x = 9`.

```java
import java.util.*;

public class tUf {

    public static int upperBound(int[] arr, int x, int n) {
        int low = 0, high = n - 1;
        int ans = n;

        while (low <= high) {
            int mid = (low + high) / 2;
            // maybe an answer
            if (arr[mid] > x) {
                ans = mid;
                //look for smaller index on the left
                high = mid - 1;
            } else {
                low = mid + 1; // look on the right
            }
        }
        return ans;
    }

    public static void main(String[] args) {
        int[] arr = {3, 5, 8, 9, 15, 19};
        int n = 6, x = 9;
        int ind = upperBound(arr, x, n);
        System.out.println("The upper bound is the index: " + ind);
    }
}
```

**Possible Optimizations:**

The given code is already an optimized implementation of the Upper Bound function. However, there is a slight optimization that can be made to handle the case where the sum of `low` and `high` overflows the maximum value of an integer.

Here's the optimized code:

```java
import java.util.*;

public class tUf {

    public static int upperBound(int[] arr, int x, int n) {
        int low = 0, high = n;
        
        while (low < high) {
            int mid = low + (high - low) / 2; // Handles the case when (low + high) overflows
            
            if (arr[mid] > x) {
                high = mid;
            } else {
                low = mid + 1;
            }
        }
        
        return high == n ? n : arr[high] > x ? high : n;
    }

    public static void main(String[] args) {
        int[] arr = {3, 5, 8, 9, 15, 19};
        int n = 6, x = 9;
        
        int ind = upperBound(arr, x, n);
        System.out.println("The upper bound is the index: " + ind);
    }
}
```

In this optimized code, we calculate the middle index `mid` as `low + (high - low) / 2` instead of `(low + high) / 2`. This ensures that the calculation does not overflow even when `low` and `high` are large integers.

Additionally, we handle the case where the target value `x` is greater than or equal to all elements in the array. If `high` is equal to `n`, we return `n` as the upper bound index. Otherwise, if the element at `high` is strictly greater than `x`, we return `high`; otherwise, we return `n`.

The time complexity and space complexity of this optimized solution remain the same: O(log n) and O(1), respectively. However, this optimization provides better handling of edge cases involving large integers and prevents potential integer overflow issues.


**40. Search Insert Position**

[Search Insert Position](https://leetcode.com/problems/search-insert-position/description/)

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.

Example 1:

Input: nums = [1,3,5,6], target = 5
Output: 2
Example 2:

Input: nums = [1,3,5,6], target = 2
Output: 1
Example 3:

Input: nums = [1,3,5,6], target = 7
Output: 4

The above code is an implementation of the binary search algorithm in Java. Binary search is an efficient algorithm used to find the position of a target element in a sorted array.

Pseudo-code:

```
BinarySearch(arr, target)
    low = 0
    high = length(arr) - 1
    
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        else if arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    
    return low
```

Explanation:
1. The algorithm takes a sorted array `arr` and a target element `target` as input.
2. It initializes two pointers `low` and `high` to the first and last indices of the array, respectively.
3. The algorithm enters a loop that continues until `low` is greater than `high`.
4. In each iteration of the loop, it calculates the middle index `mid` as the average of `low` and `high`.
5. If the element at `mid` is equal to the target, the algorithm returns `mid` as the position of the target element.
6. If the element at `mid` is less than the target, the algorithm updates `low` to `mid + 1`, effectively searching in the right half of the array.
7. If the element at `mid` is greater than the target, the algorithm updates `high` to `mid - 1`, effectively searching in the left half of the array.
8. If the target element is not found in the array, the algorithm returns `low`, which is the correct position to insert the target element to maintain the sorted order of the array.

Time Complexity: The time complexity of the binary search algorithm is O(log n), where n is the length of the sorted array. This is because the algorithm halves the search space in each iteration, resulting in a logarithmic time complexity.

Space Complexity: The space complexity of the binary search algorithm is O(1), as it uses a constant amount of extra space to store the `low`, `high`, and `mid` pointers, regardless of the size of the input array.

Example:
Let's consider the array `nums = [1, 3, 5, 6]` and the target element `target = 5`.

Iteration 1:
- `low = 0`, `high = 3`
- `mid = (0 + 3) // 2 = 1`
- `nums[mid] = 3 < target`, so `low = mid + 1 = 2`

Iteration 2:
- `low = 2`, `high = 3`
- `mid = (2 + 3) // 2 = 2`
- `nums[mid] = 5 == target`, so the algorithm returns `mid = 2`, which is the position of the target element.

```java
class Solution {
    public int searchInsert(int[] nums, int target) 
    {
        int low = 0;
        int high = nums.length - 1;
        int ans = nums.length;
        while(low <= high)
        {
            int mid = (high+low)/2;
            if(nums[mid] >= target)
            {
                ans = mid;
                high = mid - 1;
            }
            else
            {
                low = mid + 1;
            }
        }
        return ans;
    }
}
```

Optimization:

The given code is already optimized for finding the insertion position of the target element in a sorted array. However, if the goal is solely to find the position of the target element (if it exists in the array), a minor optimization can be made by returning `mid` instead of `ans` when the target is found. This would eliminate the need for the `ans` variable and slightly simplify the code.

Optimized code:

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;
        
        while (low <= high) {
            int mid = (high + low) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        
        return low;
    }
}
```

This optimized code has the same time and space complexities as the original code, but it returns the position of the target element directly if it is found in the array.

**41. Floor/Ceil in Sorted Array**

[Floor/Ceil in Sorted Array](https://www.naukri.com/code360/problems/ceiling-in-a-sorted-array_1825401)

You're given a sorted array 'a' of 'n' integers and an integer 'x'.

Find the floor and ceiling of 'x' in 'a[0..n-1]'.

Note:
Floor of 'x' is the largest element in the array which is smaller than or equal to 'x'.
Ceiling of 'x' is the smallest element in the array greater than or equal to 'x'.

Example:
Input: 
n=6, x=5, a=[3, 4, 7, 8, 8, 10]   

Output:
4

Explanation:
The floor and ceiling of 'x' = 5 are 4 and 7, respectively.

The given code defines two functions, `findFloor` and `findCeil`, which use the binary search algorithm to find the floor and ceiling values of a given number `x` in a sorted array `arr` of size `n`.

The `findFloor` function returns the greatest element in the array that is less than or equal to `x`, while the `findCeil` function returns the smallest element in the array that is greater than or equal to `x`. If no such elements exist, the functions return `-1`.

The `getFloorAndCeil` function calls both `findFloor` and `findCeil` and returns an array containing the floor and ceiling values.

Pseudo-code:

```
FindFloor(arr, n, x):
    low = 0
    high = n - 1
    ans = -1

    while low <= high:
        mid = (low + high) // 2
        if arr[mid] <= x:
            ans = arr[mid]
            low = mid + 1  # Search for a smaller index on the left
        else:
            high = mid - 1  # Search on the right

    return ans

FindCeil(arr, n, x):
    low = 0
    high = n - 1
    ans = -1

    while low <= high:
        mid = (low + high) // 2
        if arr[mid] >= x:
            ans = arr[mid]
            high = mid - 1  # Search for a smaller index on the left
        else:
            low = mid + 1  # Search on the right

    return ans

GetFloorAndCeil(arr, n, x):
    floor = FindFloor(arr, n, x)
    ceil = FindCeil(arr, n, x)
    return [floor, ceil]
```

Explanation (with an example):
Let's consider the array `arr = [3, 4, 4, 7, 8, 10]` and the target value `x = 5`.

1. The `findFloor` function is called with `arr`, `n = 6`, and `x = 5`.
   - Iteration 1:
     - `low = 0`, `high = 5`
     - `mid = (0 + 5) // 2 = 2`
     - `arr[mid] = 4 <= x`, so `ans = 4`, `low = mid + 1 = 3`
   - Iteration 2:
     - `low = 3`, `high = 5`
     - `mid = (3 + 5) // 2 = 4`
     - `arr[mid] = 8 > x`, so `high = mid - 1 = 3`
   - The loop terminates as `low > high`.
   - The function returns `ans = 4`, which is the floor value of `x = 5`.

2. The `findCeil` function is called with `arr`, `n = 6`, and `x = 5`.
   - Iteration 1:
     - `low = 0`, `high = 5`
     - `mid = (0 + 5) // 2 = 2`
     - `arr[mid] = 4 < x`, so `low = mid + 1 = 3`
   - Iteration 2:
     - `low = 3`, `high = 5`
     - `mid = (3 + 5) // 2 = 4`
     - `arr[mid] = 8 >= x`, so `ans = 8`, `high = mid - 1 = 3`
   - The loop terminates as `low > high`.
   - The function returns `ans = 8`, which is the ceil value of `x = 5`.

3. The `getFloorAndCeil` function calls `findFloor` and `findCeil` and returns an array `[4, 8]`, containing the floor and ceil values of `x = 5`.

Time Complexity:
The time complexity of both `findFloor` and `findCeil` is O(log n), where n is the size of the input array. This is because the binary search algorithm halves the search space in each iteration, resulting in a logarithmic time complexity.

Space Complexity:
The space complexity of both `findFloor` and `findCeil` is O(1), as they use a constant amount of extra space to store the `low`, `high`, `mid`, and `ans` variables, regardless of the size of the input array.

Java code :

```java
import java.util.*;

public class tUf {
    static int findFloor(int[] arr, int n, int x) {
        int low = 0, high = n - 1;
        int ans = -1;

        while (low <= high) {
            int mid = (low + high) / 2;
            // maybe an answer
            if (arr[mid] <= x) {
                ans = arr[mid];
                //look for smaller index on the left
                low = mid + 1;
            } else {
                high = mid - 1; // look on the right
            }
        }
        return ans;
    }

    static int findCeil(int[] arr, int n, int x) {
        int low = 0, high = n - 1;
        int ans = -1;

        while (low <= high) {
            int mid = (low + high) / 2;
            // maybe an answer
            if (arr[mid] >= x) {
                ans = arr[mid];
                //look for smaller index on the left
                high = mid - 1;
            } else {
                low = mid + 1; // look on the right
            }
        }
        return ans;
    }
    public static int[] getFloorAndCeil(int[] arr, int n, int x) {
        int f = findFloor(arr, n, x);
        int c = findCeil(arr, n, x);
        return new int[] {f, c};
    }
    public static void main(String[] args) {
        int[] arr = {3, 4, 4, 7, 8, 10};
        int n = 6, x = 5;
        int[] ans = getFloorAndCeil(arr, n, x);
        System.out.println("The floor and ceil are: " + ans[0]
                           + " " + ans[1]);
    }
} 

```

Optimization:
The given code is already optimized for finding the floor and ceiling values in a sorted array using the binary search algorithm. However, a minor optimization can be made to the `getFloorAndCeil` function to avoid redundant computations.

Instead of calling `findFloor` and `findCeil` separately, we can modify the `findFloor` function to also return the ceiling value when it is not equal to `-1`. This way, we can combine the two functions into one and reduce the overall time complexity.

Optimized code:

```java
import java.util.*;

public class tUf {

    static int[] findFloorAndCeil(int[] arr, int n, int x) {
        int low = 0, high = n - 1;
        int floor = -1, ceil = -1;

        while (low <= high) {
            int mid = (low + high) / 2;

            if (arr[mid] == x) {
                floor = ceil = arr[mid];
                break;
            } else if (arr[mid] < x) {
                floor = arr[mid];
                low = mid + 1;
            } else {
                ceil = arr[mid];
                high = mid - 1;
            }
        }

        return new int[] { floor, ceil };
    }

    public static void main(String[] args) {
        int[] arr = { 3, 4, 4, 7, 8, 10 };
        int n = 6, x = 5;
        int[] ans = findFloorAndCeil(arr, n, x);
        System.out.println("The floor and ceil are: " + ans[0] + " " + ans[1]);
    }
}
```

In the optimized code, the `findFloorAndCeil` function performs a single binary search and updates the `floor` and `ceil` variables accordingly. If the target value `x` is found in the array, both `floor` and `ceil` are set to `x`.

The time complexity of the optimized `findFloorAndCeil` function is O(log n), where n is the size of the input array, since it performs a single binary search. The space complexity remains O(1), as it uses a constant amount of extra space to store the `low`, `high`, `floor`, and `ceil` variables.

## 10-05-2024

**42. Find First and Last Position of Element in Sorted Array**

[Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)

The above code is a Java implementation of a solution to the "Find First and Last Position of Element in Sorted Array" problem on LeetCode. The problem asks to find the starting and ending indices of the target element in a sorted array. If the target element is not present in the array, the function should return `[-1, -1]`.

The solution uses two helper functions, `findFirst` and `findLast`, to find the first and last occurrences of the target element, respectively.

Pseudo-code:

```
FindFirstAndLastPosition(nums, target):
    first = FindFirst(nums, target)
    last = FindLast(nums, target)
    return [first, last]

FindFirst(nums, target):
    left = 0
    right = length(nums) - 1
    first = -1

    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            if mid == 0 or nums[mid - 1] != target:
                first = mid
                break
            else:
                right = mid - 1  # Look for the leftmost occurrence
        else if nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return first

FindLast(nums, target):
    left = 0
    right = length(nums) - 1
    last = -1

    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            if mid == length(nums) - 1 or nums[mid + 1] != target:
                last = mid
                break
            else:
                left = mid + 1  # Look for the rightmost occurrence
        else if nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return last
```

Explanation (with an example):
Let's consider the array `nums = [5, 7, 7, 8, 8, 10]` and the target `target = 8`.

1. The `searchRange` function is called with `nums` and `target = 8`.
2. Inside `searchRange`, it calls `findFirst(nums, 8)`.
   - Iteration 1:
     - `left = 0`, `right = 5`
     - `mid = (0 + 5) // 2 = 2`
     - `nums[mid] = 7 < target`, so `left = mid + 1 = 3`
   - Iteration 2:
     - `left = 3`, `right = 5`
     - `mid = (3 + 5) // 2 = 4`
     - `nums[mid] = 8 == target`, and since `mid != 0` and `nums[mid - 1] == 8`, `right = mid - 1 = 3`
   - Iteration 3:
     - `left = 3`, `right = 3`
     - `mid = (3 + 3) // 2 = 3`
     - `nums[mid] = 8 == target`, and since `mid != 0` and `nums[mid - 1] != 8`, `first = mid = 3`, and the loop breaks.
   - The `findFirst` function returns `3`, which is the index of the first occurrence of `8`.

3. Inside `searchRange`, it calls `findLast(nums, 8)`.
   - Iteration 1:
     - `left = 0`, `right = 5`
     - `mid = (0 + 5) // 2 = 2`
     - `nums[mid] = 7 < target`, so `left = mid + 1 = 3`
   - Iteration 2:
     - `left = 3`, `right = 5`
     - `mid = (3 + 5) // 2 = 4`
     - `nums[mid] = 8 == target`, and since `mid != nums.length - 1` and `nums[mid + 1] == 8`, `left = mid + 1 = 5`
   - Iteration 3:
     - `left = 5`, `right = 5`
     - `mid = (5 + 5) // 2 = 5`
     - `nums[mid] = 10 > target`, so `right = mid - 1 = 4`
   - Iteration 4:
     - `left = 4`, `right = 4`
     - `mid = (4 + 4) // 2 = 4`
     - `nums[mid] = 8 == target`, and since `mid == nums.length - 2` and `nums[mid + 1] != 8`, `last = mid = 4`, and the loop breaks.
   - The `findLast` function returns `4`, which is the index of the last occurrence of `8`.

4. The `searchRange` function returns `[3, 4]`, which are the starting and ending indices of the target element `8` in the array.

Time Complexity:
The time complexity of both `findFirst` and `findLast` is O(log n), where n is the length of the input array. This is because they use the binary search algorithm, which halves the search space in each iteration, resulting in a logarithmic time complexity.

Space Complexity:
The space complexity of both `findFirst` and `findLast` is O(1), as they use a constant amount of extra space to store the `left`, `right`, `mid`, and `first`/`last` variables, regardless of the size of the input array.

Java code:

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int first = findFirst(nums, target);
        int last = findLast(nums, target);
        return new int[]{first, last};
    }

    private int findFirst(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        int first = -1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                if (mid == 0 || nums[mid - 1] != target) {
                    first = mid;
                    break;
                } else {
                    right = mid - 1;
                }
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return first;
    }

    private int findLast(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        int last = -1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                if (mid == nums.length - 1 || nums[mid + 1] != target) {
                    last = mid;
                    break;
                } else {
                    left = mid + 1;
                }
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return last;
    }
}
```

Optimization:
The given code is already optimized for finding the first and last occurrences of the target element in a sorted array using the binary search algorithm. However, there is a potential optimization that can be made to reduce the overall time complexity.

Instead of calling `findFirst` and `findLast` separately, we can combine them into a single function that performs a single binary search and keeps track of the first and last occurrences simultaneously. This approach can slightly improve the time complexity by reducing the number of iterations required.

Optimized code:

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        int[] result = { -1, -1 };

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] == target) {
                result[0] = mid;
                right = mid - 1; // Find the leftmost occurrence
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        left = 0;
        right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] == target) {
                result[1] = mid;
                left = mid + 1; // Find the rightmost occurrence
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return result;
    }
}
```

In the optimized code, the `searchRange` function performs two binary searches: one to find the leftmost occurrence of the target element and the other to find the rightmost occurrence. The `result` array is used to store the starting and ending indices of the target element.

The time complexity of the optimized `searchRange` function is O(log n), where n is the length of the input array, as it performs two binary searches. However, the constant factor is slightly smaller than the original implementation, as it avoids redundant computations.

The space complexity remains O(1), as it uses a constant amount of extra space to store the `left`, `right`, and `result` variables.


**43. Count Occurrences in Sorted Array**

[Count Occurrences in Sorted Array](https://www.geeksforgeeks.org/problems/number-of-occurrence2259/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=number-of-occurrence)

Given a sorted array Arr of size N and a number X, you need to find the number of occurrences of X in Arr.

Example 1:

Input:
N = 7, X = 2

Arr[] = {1, 1, 2, 2, 2, 2, 3}

Output: 4

Explanation: 2 occurs 4 times in the
given array.

Example 2:

Input:
N = 7, X = 4

Arr[] = {1, 1, 2, 2, 2, 2, 3}

Output: 0

Explanation: 4 is not present in the
given array.

The above code is a Java implementation of a solution to find the count of occurrences of a given element `x` in a sorted array `arr` of size `n`.

The solution uses a modified version of the binary search algorithm to find the first and last occurrences of the element `x` in the array. Once the first and last occurrences are known, it calculates the count by subtracting the first occurrence index from the last occurrence index and adding one.

Pseudo-code:

```
CountOccurrences(arr, n, x):
    start = 0
    end = n - 1
    firstOccurrence = -1
    lastOccurrence = -1

    // Find the first occurrence of x
    while start <= end:
        mid = (start + end) // 2
        if arr[mid] == x:
            firstOccurrence = mid
            end = mid - 1  # Continue searching in the left half
        else if x > arr[mid]:
            start = mid + 1
        else:
            end = mid - 1

    // Find the last occurrence of x
    start = 0
    end = n - 1
    while start <= end:
        mid = (start + end) // 2
        if arr[mid] == x:
            lastOccurrence = mid
            start = mid + 1  # Continue searching in the right half
        else if x > arr[mid]:
            start = mid + 1
        else:
            end = mid - 1

    // Calculate the count
    if firstOccurrence != -1 and lastOccurrence != -1:
        count = lastOccurrence - firstOccurrence + 1
    else:
        count = 0

    return count
```

Explanation (with an example):
Let's consider the array `arr = [1, 2, 2, 3, 3, 3, 4]` and the target element `x = 3`.

1. The `count` function is called with `arr`, `n = 7`, and `x = 3`.
2. Finding the first occurrence of `x = 3`:
   - Iteration 1:
     - `start = 0`, `end = 6`
     - `mid = (0 + 6) // 2 = 3`
     - `arr[mid] = 3 == x`, so `firstOccurrence = mid = 3`, `end = mid - 1 = 2`
   - Iteration 2:
     - `start = 0`, `end = 2`
     - `mid = (0 + 2) // 2 = 1`
     - `arr[mid] = 2 < x`, so `start = mid + 1 = 2`
   - Iteration 3:
     - `start = 2`, `end = 2`
     - `mid = (2 + 2) // 2 = 2`
     - `arr[mid] = 2 < x`, so `start = mid + 1 = 3`
   - The loop terminates as `start > end`.
   - The first occurrence of `x = 3` is found at index `3`.

3. Finding the last occurrence of `x = 3`:
   - Iteration 1:
     - `start = 0`, `end = 6`
     - `mid = (0 + 6) // 2 = 3`
     - `arr[mid] = 3 == x`, so `lastOccurrence = mid = 3`, `start = mid + 1 = 4`
   - Iteration 2:
     - `start = 4`, `end = 6`
     - `mid = (4 + 6) // 2 = 5`
     - `arr[mid] = 3 == x`, so `lastOccurrence = mid = 5`, `start = mid + 1 = 6`
   - Iteration 3:
     - `start = 6`, `end = 6`
     - `mid = (6 + 6) // 2 = 6`
     - `arr[mid] = 4 > x`, so `end = mid - 1 = 5`
   - The loop terminates as `start > end`.
   - The last occurrence of `x = 3` is found at index `5`.

4. Calculating the count:
   - `firstOccurrence = 3`, `lastOccurrence = 5`
   - `count = lastOccurrence - firstOccurrence + 1 = 5 - 3 + 1 = 3`
   - The function returns `3`, which is the count of occurrences of `x = 3` in the array.

Time Complexity:
The time complexity of the `count` function is O(log n), where n is the length of the input array. This is because it uses a modified version of the binary search algorithm twice, and the time complexity of binary search is O(log n).

Space Complexity:
The space complexity of the `count` function is O(1), as it uses a constant amount of extra space to store the `start`, `end`, `firstOccurrence`, `lastOccurrence`, and `count` variables, regardless of the size of the input array.

Java code:

```java
class Solution {
    int count(int arr[], int n, int x) {
    int start = 0;
    int end = n - 1;

    int firstOccurrence = -1; // Initialize with -1 to handle cases where 'x' is not found
    int lastOccurrence = -1; // Initialize with -1 to handle cases where 'x' is not found

    // Finding the first occurrence of 'x'
    while (start <= end) {
        int mid = start + (end - start) / 2;

        if (arr[mid] == x) {
            firstOccurrence = mid;
            end = mid - 1; // Continue searching in the left half for the first occurrence
        } else if (x > arr[mid]) {
            start = mid + 1;
        } else {
            end = mid - 1;
        }
    }

    // Finding the last occurrence of 'x'
    start = 0; // Reset start
    end = n - 1; // Reset end
    while (start <= end) {
        int mid = start + (end - start) / 2;

        if (arr[mid] == x) {
            lastOccurrence = mid;
            start = mid + 1; // Continue searching in the right half for the last occurrence
        } else if (x > arr[mid]) {
            start = mid + 1;
        } else {
            end = mid - 1;
        }
    }

    // Calculating the count of occurrences
    int count = 0;
    if (firstOccurrence != -1 && lastOccurrence != -1) {
        count = lastOccurrence - firstOccurrence + 1;
    }

    return count;
}
}
```

Optimization:
The given code is already optimized for finding the count of occurrences of an element in a sorted array using a modified version of the binary search algorithm. However, there is a potential optimization that can be made to reduce the overall time complexity further.

Instead of performing two separate binary searches to find the first and last occurrences of the element, we can combine them into a single binary search by keeping track of the leftmost and rightmost indices where the target element is found. This approach can slightly improve the time complexity by reducing the number of iterations required.

Optimized code:

```java
class Solution {
    int count(int[] arr, int n, int x) {
        int start = 0;
        int end = n - 1;
        int firstOccurrence = -1;
        int lastOccurrence = -1;

        while (start <= end) {
            int mid = start + (end - start) / 2;

            if (arr[mid] == x) {
                firstOccurrence = mid;
                lastOccurrence = mid;

                // Expand the range for firstOccurrence and lastOccurrence
                int left = mid - 1;
                int right = mid + 1;

                while (left >= 0 && arr[left] == x) {
                    firstOccurrence = left;
                    left--;
                }

                while (right < n && arr[right] == x) {
                    lastOccurrence = right;
                    right++;
                }

                break;
            } else if (x > arr[mid]) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }

        int count = 0;
        if (firstOccurrence != -1 && lastOccurrence != -1) {
            count = lastOccurrence - firstOccurrence + 1;
        }

        return count;
    }
}
```

In the optimized code, the `count` function performs a single binary search to find the middle index where the target element `x` is found (if it exists). Once the middle index is found, it expands the range to the left and right to find the leftmost and rightmost indices where `x` is found, respectively.

The time complexity of the optimized `count` function is O(log n + k), where n is the length of the input array, and k is the count of occurrences of the target element `x`. The additional k factor is due to the expansion step, which iterates to find the leftmost and rightmost indices of `x`.

The space complexity remains O(1), as it uses a constant amount of extra space to store the `start`, `end`, `firstOccurrence`, `lastOccurrence`, and `count` variables.

## 14-05-2024

**44. Search in a rotated array 1**

[Search in a rotated array 1](https://leetcode.com/problems/search-in-rotated-sorted-array/)

There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].

Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with O(log n) runtime complexity.

Example 1:

Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
Example 2:

Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
Example 3:

Input: nums = [1], target = 0
Output: -1

The above code is a Java implementation of the solution to the "Search in Rotated Sorted Array" problem on LeetCode. The problem asks to search for a target element in a rotated sorted array, and return its index if found. If the target element is not present in the array, the function should return `-1`.

The solution uses a modified version of the binary search algorithm to handle the rotation in the sorted array. It first checks if the middle element is the target, and if not, it determines which half of the array is sorted based on the values at the low and middle indices. It then checks if the target falls within the sorted half and updates the low and high pointers accordingly.

Pseudo-code:

```
SearchRotatedSortedArray(nums, target):
    low = 0
    high = length(nums) - 1

    while low <= high:
        mid = (low + high) // 2

        if nums[mid] == target:
            return mid

        # If the left half is sorted
        if nums[low] <= nums[mid]:
            # If the target falls within the left sorted half
            if nums[low] <= target < nums[mid]:
                high = mid - 1
            else:
                low = mid + 1

        # If the right half is sorted
        else:
            # If the target falls within the right sorted half
            if nums[mid] < target <= nums[high]:
                low = mid + 1
            else:
                high = mid - 1

    return -1
```

Explanation (with an example):
Let's consider the array `nums = [4, 5, 6, 7, 0, 1, 2]` and the target `target = 0`.

1. The `search` function is called with `nums` and `target = 0`.
2. Iteration 1:
   - `low = 0`, `high = 6`
   - `mid = (0 + 6) // 2 = 3`
   - `nums[mid] = 7 != target`
   - `nums[low] = 4 <= nums[mid] = 7`, so the left half is sorted
   - `nums[low] = 4 <= target = 0`, but `target = 0 < nums[mid] = 7`, so `high = mid - 1 = 2`

3. Iteration 2:
   - `low = 0`, `high = 2`
   - `mid = (0 + 2) // 2 = 1`
   - `nums[mid] = 5 != target`
   - `nums[low] = 4 <= nums[mid] = 5`, so the left half is sorted
   - `nums[low] = 4 <= target = 0`, but `target = 0 < nums[mid] = 5`, so `high = mid - 1 = 0`

4. Iteration 3:
   - `low = 0`, `high = 0`
   - `mid = (0 + 0) // 2 = 0`
   - `nums[mid] = 4 != target`
   - `nums[low] = 4 <= nums[mid] = 4`, so the left half is sorted
   - `nums[low] = 4 > target = 0`, so `low = mid + 1 = 1`

5. Iteration 4:
   - `low = 1`, `high = 0`
   - The loop terminates as `low > high`.

6. Since the target element `0` is not found in the array, the function returns `-1`.

Time Complexity:
The time complexity of the `search` function is O(log n), where n is the length of the input array. This is because it uses a modified version of the binary search algorithm, which halves the search space in each iteration, resulting in a logarithmic time complexity.

Space Complexity:
The space complexity of the `search` function is O(1), as it uses a constant amount of extra space to store the `low`, `high`, and `mid` variables, regardless of the size of the input array.

Java code:

```java
class Solution {
    public int search(int[] nums, int target) 
    {
        int low = 0;
        int high = nums.length-1;
        while (low <= high)
        {
            int mid = (low+high)/2;
            if(nums[mid]==target)
            {
                return mid;
            }
            else if(nums[low] <= nums[mid])
            {
                if (nums[low]<= target && target <= nums[mid])
                {
                    high = mid - 1;
                }
                else
                {
                    low = mid + 1;
                }
            }
            else 
            {
                if(nums[mid]<= target && target <= nums[high])
                {
                    low = mid + 1;
                }
                else
                {
                    high = mid - 1;
                }
            }
        }
        return -1; 
    }
}
```

Optimization:
The given code is already optimized for searching in a rotated sorted array using a modified version of the binary search algorithm. However, there is a potential optimization that can be made to simplify the code and make it more readable.

Instead of checking the sorted half of the array based on the values at the low and middle indices, we can directly compare the middle element with the low and high elements to determine the sorted half. This approach can make the code more concise and easier to understand.

Optimized code:

```java
class Solution {
    public int search(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {
                return mid;
            }

            // If the left half is sorted
            if (nums[low] <= nums[mid]) {
                // If the target falls within the left sorted half
                if (nums[low] <= target && target < nums[mid]) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            }
            // If the right half is sorted
            else {
                // If the target falls within the right sorted half
                if (nums[mid] < target && target <= nums[high]) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }
        }

        return -1;
    }
}
```

In the optimized code, the check for the sorted half is simplified by directly comparing the middle element with the low and high elements. If `nums[low] <= nums[mid]`, the left half is sorted, and if `nums[mid] < nums[high]`, the right half is sorted.

The time complexity and space complexity of the optimized code remain O(log n) and O(1), respectively, as the underlying algorithm is still the modified binary search.

**45. Search in a rotated array 2**

[Search in a rotated array 2](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/description/)

There is an integer array nums sorted in non-decreasing order (not necessarily with distinct values).

Before being passed to your function, nums is rotated at an unknown pivot index k (0 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,4,4,5,6,6,7] might be rotated at pivot index 5 and become [4,5,6,6,7,0,1,2,4,4].

Given the array nums after the rotation and an integer target, return true if target is in nums, or false if it is not in nums.

You must decrease the overall operation steps as much as possible.

Example 1:

Input: nums = [2,5,6,0,0,1,2], 

target = 0

Output: true

Example 2:

Input: nums = [2,5,6,0,0,1,2], 

target = 3

Output: false

The above code is a Java implementation of the solution to the "Search in Rotated Sorted Array II" problem on LeetCode. This problem is a variation of the "Search in Rotated Sorted Array" problem, where the input array may contain duplicates.

The solution uses a modified version of the binary search algorithm to handle the rotation and duplicates in the sorted array. It first checks if the middle element is the target, and if not, it checks for the case where the low, middle, and high elements are all equal (due to duplicates). If this is the case, it moves the low and high pointers inward to skip the duplicates. Otherwise, it determines which half of the array is sorted based on the values at the low and middle indices, and checks if the target falls within the sorted half, updating the low and high pointers accordingly.

Pseudo-code:

```
SearchRotatedSortedArrayWithDuplicates(nums, target):
    low = 0
    high = length(nums) - 1

    while low <= high:
        mid = (low + high) // 2

        if nums[mid] == target:
            return True

        # If duplicates are found at low, mid, and high
        if nums[low] == nums[mid] == nums[high]:
            low += 1
            high -= 1

        # If the left half is sorted
        elif nums[low] <= nums[mid]:
            # If the target falls within the left sorted half
            if nums[low] <= target < nums[mid]:
                high = mid - 1
            else:
                low = mid + 1

        # If the right half is sorted
        else:
            # If the target falls within the right sorted half
            if nums[mid] < target <= nums[high]:
                low = mid + 1
            else:
                high = mid - 1

    return False
```

Explanation (with an example):
Let's consider the array `nums = [3, 1, 1, 1, 1, 1, 3]` and the target `target = 3`.

1. The `search` function is called with `nums` and `target = 3`.
2. Iteration 1:
   - `low = 0`, `high = 6`
   - `mid = (0 + 6) // 2 = 3`
   - `nums[mid] = 1 != target`
   - `nums[low] = 3 > nums[mid] = 1`, so the left half is not sorted
   - `nums[mid] = 1 < target = 3 <= nums[high] = 3`, so `low = mid + 1 = 4`

3. Iteration 2:
   - `low = 4`, `high = 6`
   - `mid = (4 + 6) // 2 = 5`
   - `nums[mid] = 1 != target`
   - `nums[low] = 1 == nums[mid] = 1 == nums[high] = 3`, so `low = low + 1 = 5`, `high = high - 1 = 5`

4. Iteration 3:
   - `low = 5`, `high = 5`
   - `mid = (5 + 5) // 2 = 5`
   - `nums[mid] = 1 != target`
   - `nums[low] = 1 == nums[mid] = 1 == nums[high] = 1`, so `low = low + 1 = 6`, `high = high - 1 = 4`

5. Iteration 4:
   - `low = 6`, `high = 4`
   - The loop terminates as `low > high`.

6. Since the target element `3` is found in the array, the function returns `True`.

Time Complexity:
The time complexity of the `search` function is O(n) in the worst case, where n is the length of the input array. This is because, in the worst case, when the entire array consists of duplicates, the algorithm needs to skip all the duplicates, resulting in a linear time complexity.

Space Complexity:
The space complexity of the `search` function is O(1), as it uses a constant amount of extra space to store the `low`, `high`, and `mid` variables, regardless of the size of the input array.

```java
class Solution {
    public boolean search(int[] nums, int target) 
    {
        int low = 0;
        int high = nums.length-1;
        while (low <= high)
        {
            int mid = (low+high)/2;
            if(nums[mid]==target)
            {
                return true;
            }
            else if(nums[mid] == nums[low] && nums[mid] == nums[high])
            {
                low = low + 1;
                high = high - 1;
            }
            else if(nums[low] <= nums[mid])
            {
                if (nums[low]<= target && target <= nums[mid])
                {
                    high = mid - 1;
                }
                else
                {
                    low = mid + 1;
                }
            }
            else 
            {
                if(nums[mid]<= target && target <= nums[high])
                {
                    low = mid + 1;
                }
                else
                {
                    high = mid - 1;
                }
            }
        }
        return false; 
    }
}
```

Optimization:
The given code is already optimized for searching in a rotated sorted array with duplicates using a modified version of the binary search algorithm. However, there is a potential optimization that can be made to improve the time complexity in certain cases.

Instead of blindly skipping all duplicates when `nums[low] == nums[mid] == nums[high]`, we can check if the target element is equal to the duplicate value. If it is, we can simply return `True` since the target element is present in the array.

Optimized code:

```java
class Solution {
    public boolean search(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {
                return true;
            }

            // If duplicates are found at low, mid, and high
            if (nums[low] == nums[mid] && nums[mid] == nums[high]) {
                // If the target is equal to the duplicate value, return true
                if (nums[mid] == target) {
                    return true;
                }
                low++;
                high--;
            }
            // If the left half is sorted
            else if (nums[low] <= nums[mid]) {
                // If the target falls within the left sorted half
                if (nums[low] <= target && target < nums[mid]) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            }
            // If the right half is sorted
            else {
                // If the target falls within the right sorted half
                if (nums[mid] < target && target <= nums[high]) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }
        }

        return false;
    }
}
```

In the optimized code, when `nums[low] == nums[mid] == nums[high]`, it checks if the target is equal to the duplicate value. If it is, the function returns `true` since the target element is present in the array.

The time complexity of the optimized `search` function is O(n) in the worst case, where n is the length of the input array. However, in certain cases where the target element is equal to the duplicate value, the time complexity can be improved to O(log n), as the algorithm can skip the duplicates and converge more quickly.

The space complexity remains O(1), as it uses a constant amount of extra space to store the `low`, `high`, and `mid` variables.

**46. Find Minimum in Rotated Sorted Array**

[Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)

Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array nums = [0,1,2,4,5,6,7] might become:

[4,5,6,7,0,1,2] if it was rotated 4 times.
[0,1,2,4,5,6,7] if it was rotated 7 times.
Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]].

Given the sorted rotated array nums of unique elements, return the minimum element of this array.

You must write an algorithm that runs in O(log n) time.

Example 1:

Input: nums = [3,4,5,1,2]

Output: 1

Explanation: The original array was [1,2,3,4,5] rotated 3 times.

Example 2:

Input: nums = [4,5,6,7,0,1,2]

Output: 0

Explanation: The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.

Example 3:

Input: nums = [11,13,15,17]

Output: 11

Explanation: The original array was [11,13,15,17] and it was rotated 4 times. 

The above code is a Java implementation of a solution to find the minimum element in a rotated sorted array. The problem assumes that the input array is a sorted array that has been rotated around a pivot point, and the task is to find the minimum element in the rotated array.

Pseudo-code:

```
FindMinimumInRotatedSortedArray(nums):
    n = length(nums)
    high = n - 1
    low = 0
    ans = MAX_VALUE

    while low <= high:
        mid = (low + high) // 2

        # If the array is not rotated (sorted)
        if nums[low] <= nums[high]:
            ans = min(ans, nums[low])
            break

        # If the left half is sorted
        if nums[low] <= nums[mid]:
            ans = min(ans, nums[low])
            low = mid + 1
        # If the right half is sorted
        else:
            ans = min(ans, nums[mid])
            high = mid - 1

    return ans
```

Explanation (with an example):
Let's consider the array `nums = [4, 5, 6, 7, 0, 1, 2]`.

1. The `findMin` function is called with `nums`.
2. Iteration 1:
   - `low = 0`, `high = 6`
   - `mid = (0 + 6) // 2 = 3`
   - `nums[low] = 4 > nums[high] = 2`, so the array is rotated
   - `nums[low] = 4 <= nums[mid] = 7`, so the left half is sorted
   - `ans = min(MAX_VALUE, 4) = 4`, `low = mid + 1 = 4`

3. Iteration 2:
   - `low = 4`, `high = 6`
   - `mid = (4 + 6) // 2 = 5`
   - `nums[low] = 0 > nums[high] = 2`, so the array is rotated
   - `nums[low] = 0 < nums[mid] = 1`, so the right half is sorted
   - `ans = min(4, 0) = 0`, `high = mid - 1 = 4`

4. Iteration 3:
   - `low = 4`, `high = 4`
   - `mid = (4 + 4) // 2 = 4`
   - `nums[low] = 0 <= nums[high] = 0`, so the array is not rotated (sorted)
   - `ans = min(0, 0) = 0`, and the loop breaks

5. The function returns `ans = 0`, which is the minimum element in the rotated sorted array.

Time Complexity:
The time complexity of the `findMin` function is O(log n), where n is the length of the input array. This is because it uses a modified version of the binary search algorithm, which halves the search space in each iteration, resulting in a logarithmic time complexity.

Space Complexity:
The space complexity of the `findMin` function is O(1), as it uses a constant amount of extra space to store the `low`, `high`, `mid`, `ans`, and `n` variables, regardless of the size of the input array.

Java code:

```java
class Solution {
    public int findMin(int[] nums) 
    {
        int n = nums.length;
        int high = nums.length - 1;
        int low = 0;
        int ans = Integer.MAX_VALUE;
        while (low <= high)
        {
            int mid = (low+high)/2;
            if(nums[low]<=nums[high])
            {
                ans = ans = Math.min(ans, nums[low]);
                break;
            }
            if(nums[low]<= nums[mid])
            {
                ans = Math.min(ans, nums[low]);
                low = mid + 1;
            }
            else
            {
                ans = Math.min(ans, nums[mid]);
                high = mid - 1;
            }
        }
       return ans;
    }
}
```

Optimization:
The given code is already optimized for finding the minimum element in a rotated sorted array using a modified version of the binary search algorithm. However, there is a potential optimization that can be made to simplify the code and make it more readable.

Instead of checking if the array is sorted or rotated and then updating the `low` and `high` pointers accordingly, we can directly compare the middle element with the low and high elements to determine which half of the array is sorted, and update the pointers based on that.

Optimized code:

```java
class Solution {
    public int findMin(int[] nums) {
        int low = 0;
        int high = nums.length - 1;

        while (low < high) {
            int mid = low + (high - low) / 2;

            // If the middle element is greater than the rightmost element,
            // the minimum element lies in the right half
            if (nums[mid] > nums[high]) {
                low = mid + 1;
            }
            // If the middle element is less than or equal to the rightmost element,
            // the minimum element lies in the left half or at the middle
            else {
                high = mid;
            }
        }

        return nums[low];
    }
}
```

In the optimized code, the `findMin` function compares the middle element with the rightmost element (`nums[high]`) instead of checking if the array is sorted or rotated. If `nums[mid] > nums[high]`, the minimum element lies in the right half of the array, so the `low` pointer is updated to `mid + 1`. Otherwise, the minimum element lies in the left half or at the middle, so the `high` pointer is updated to `mid`.

The time complexity and space complexity of the optimized code remain O(log n) and O(1), respectively, as the underlying algorithm is still the modified binary search.

**47. Find out how many times has an array been rotated**

[Find out how many times has an array been rotated](https://www.geeksforgeeks.org/problems/rotation4723/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=rotation)

Given an ascending sorted rotated array arr of distinct integers of size n. The array is right-rotated k times. Find the value of k.

Example 1:

Input:

n = 5

arr[] = {5, 1, 2, 3, 4}

Output: 1

Explanation: The given array is 5 1 2 3 4. 
The original sorted array is 1 2 3 4 5. 
We can see that the array was rotated 
1 times to the right.

Example 2:

Input:

n = 5

arr[] = {1, 2, 3, 4, 5}

Output: 0

Explanation: The given array is not rotated.

The above code is a Java implementation of a solution to find the number of rotations in a rotated sorted array. The problem assumes that the input array is a sorted array that has been rotated around a pivot point, and the task is to find the number of rotations performed on the array.

Pseudo-code:

```
FindNumberOfRotations(arr, n):
    low = 0
    high = n - 1

    while low < high:
        mid = (low + high) // 2

        # If the middle element is greater than the rightmost element,
        # the minimum element lies in the right half
        if arr[mid] > arr[high]:
            low = mid + 1
        # If the middle element is less than or equal to the rightmost element,
        # the minimum element lies in the left half or at the middle
        else:
            high = mid

    # The low index now points to the minimum element
    # The number of rotations is the index of the minimum element
    return low
```

Explanation (with an example):
Let's consider the array `arr = [5, 6, 7, 8, 9, 10, 1, 2, 3, 4]`.

1. The `findKRotation` function is called with `arr` and `n = 10`.
2. Iteration 1:
   - `low = 0`, `high = 9`
   - `mid = (0 + 9) // 2 = 4`
   - `arr[mid] = 9 < arr[high] = 4`, so the minimum element lies in the left half or at the middle
   - `high = mid = 4`

3. Iteration 2:
   - `low = 0`, `high = 4`
   - `mid = (0 + 4) // 2 = 2`
   - `arr[mid] = 7 < arr[high] = 9`, so the minimum element lies in the left half or at the middle
   - `high = mid = 2`

4. Iteration 3:
   - `low = 0`, `high = 2`
   - `mid = (0 + 2) // 2 = 1`
   - `arr[mid] = 6 < arr[high] = 7`, so the minimum element lies in the left half or at the middle
   - `high = mid = 1`

5. Iteration 4:
   - `low = 0`, `high = 1`
   - `mid = (0 + 1) // 2 = 0`
   - `arr[mid] = 5 > arr[high] = 6`, so the minimum element lies in the right half
   - `low = mid + 1 = 1`

6. Iteration 5:
   - `low = 1`, `high = 1`
   - The loop terminates as `low == high`.

7. The function returns `low = 1`, which is the index of the minimum element `6` in the rotated sorted array.

Since the array is rotated around the pivot point, the number of rotations performed is equal to the index of the minimum element. In this case, the number of rotations is `1`.

Time Complexity:
The time complexity of the `findKRotation` function is O(log n), where n is the length of the input array. This is because it uses a modified version of the binary search algorithm, which halves the search space in each iteration, resulting in a logarithmic time complexity.

Space Complexity:
The space complexity of the `findKRotation` function is O(1), as it uses a constant amount of extra space to store the `low`, `high`, and `mid` variables, regardless of the size of the input array.

Java code:

```java
class Solution {
    int findKRotation(int arr[], int n) 
    {
        int low = 0;
        int high = n - 1;
        while (low < high) {
            int mid = low + (high - low) / 2;

            // If the middle element is greater than the rightmost element,
            // the minimum element lies in the right half
            if (arr[mid] > arr[high]) {
                low = mid + 1;
            }
            // If the middle element is less than or equal to the rightmost element,
            // the minimum element lies in the left half or at the middle
            else {
                high = mid;
            }
        }

        return low;
    }
}
```

Optimization:
The given code is already optimized for finding the number of rotations in a rotated sorted array using a modified version of the binary search algorithm. However, there is a potential optimization that can be made to handle the case when the input array is not rotated (sorted).

In the given implementation, the algorithm assumes that the input array is rotated and performs the binary search to find the minimum element. However, if the input array is not rotated (sorted), the minimum element will be at the first index, and the algorithm will still perform unnecessary comparisons.

To optimize for this case, we can add a check at the beginning to verify if the array is sorted or not. If it is sorted, we can directly return 0 as the number of rotations.

Optimized code:

```java
class Solution {
    int findKRotation(int[] arr, int n) {
        // Check if the array is sorted (not rotated)
        if (arr[0] < arr[n - 1]) {
            return 0; // No rotations
        }

        int low = 0;
        int high = n - 1;

        while (low < high) {
            int mid = low + (high - low) / 2;

            // If the middle element is greater than the rightmost element,
            // the minimum element lies in the right half
            if (arr[mid] > arr[high]) {
                low = mid + 1;
            }
            // If the middle element is less than or equal to the rightmost element,
            // the minimum element lies in the left half or at the middle
            else {
                high = mid;
            }
        }

        // The low index now points to the minimum element
        // The number of rotations is the index of the minimum element
        return low;
    }
}
```

In the optimized code, before performing the binary search, we check if `arr[0] < arr[n - 1]`. If this condition is true, it means the array is sorted (not rotated), and we can directly return 0 as the number of rotations.

If the array is rotated, the algorithm proceeds with the binary search to find the minimum element, and the number of rotations is the index of the minimum element, as in the original implementation.

The time complexity of the optimized `findKRotation` function is O(log n) in the case of a rotated array, and O(1) in the case of a sorted array. The space complexity remains O(1) in both cases.

## 16-5-2024

**48. Single Element in a Sorted Array**

[Single Element in a Sorted Array](https://leetcode.com/problems/single-element-in-a-sorted-array/description/)

You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.

Return the single element that appears only once.

Your solution must run in O(log n) time and O(1) space.

Example 1:

Input: nums = [1,1,2,3,3,4,4,8,8]

Output: 2

Example 2:

Input: nums = [3,3,7,7,10,11,11]

Output: 10

Pseudo-code:

```
FindSingleNonDuplicate(nums):
    n = length(nums)

    # Base cases
    if n == 1:
        return nums[0]
    if nums[0] != nums[1]:
        return nums[0]
    if nums[n - 1] != nums[n - 2]:
        return nums[n - 1]

    low = 1
    high = n - 2

    while low <= high:
        mid = (low + high) // 2

        # Check if the middle element is the single non-duplicate element
        if nums[mid] != nums[mid + 1] and nums[mid] != nums[mid - 1]:
            return nums[mid]

        # If the middle element is part of the first pair in the duplicate group
        if (mid % 2 == 1 and nums[mid] == nums[mid - 1]) or (mid % 2 == 0 and nums[mid] == nums[mid + 1]):
            low = mid + 1  # Search in the right half
        else:
            high = mid - 1  # Search in the left half

    return -1  # Should never reach this point
```

Explanation (with an example):
Let's consider the array `nums = [1, 1, 2, 3, 3, 4, 4, 8, 8]`.

1. The `singleNonDuplicate` function is called with `nums`.
2. Since `nums[0] == nums[1]` and `nums[n - 1] == nums[n - 2]`, the function proceeds to the binary search.
3. Iteration 1:
   - `low = 1`, `high = 7`
   - `mid = (1 + 7) // 2 = 4`
   - `nums[mid] = 3 != nums[mid + 1] = 3 and nums[mid] != nums[mid - 1] = 2`, so the single non-duplicate element is not at the middle
   - `mid % 2 = 0` and `nums[mid] != nums[mid + 1]`, so the single non-duplicate element is in the right half
   - `low = mid + 1 = 5`

4. Iteration 2:
   - `low = 5`, `high = 7`
   - `mid = (5 + 7) // 2 = 6`
   - `nums[mid] = 4 != nums[mid + 1] = 8 and nums[mid] != nums[mid - 1] = 4`, so the single non-duplicate element is not at the middle
   - `mid % 2 = 0` and `nums[mid] != nums[mid + 1]`, so the single non-duplicate element is in the right half
   - `low = mid + 1 = 7`

5. Iteration 3:
   - `low = 7`, `high = 7`
   - `mid = (7 + 7) // 2 = 7`
   - `nums[mid] = 8 != nums[mid + 1] = -1 (out of bounds) and nums[mid] != nums[mid - 1] = 8`, so the single non-duplicate element is found at index 7
   - The function returns `nums[mid] = 8`.

Time Complexity:
The time complexity of the `singleNonDuplicate` function is O(log n), where n is the length of the input array. This is because it uses a modified version of the binary search algorithm, which halves the search space in each iteration, resulting in a logarithmic time complexity.

Space Complexity:
The space complexity of the `singleNonDuplicate` function is O(1), as it uses a constant amount of extra space to store the `low`, `high`, `mid`, and `n` variables, regardless of the size of the input array.

Java code:

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        
    int n = nums.length;
    
    if (n == 1) {
        return nums[0];
    }
    
    
    if (nums[0] != nums[1]) {
        return nums[0];
    }
    if (nums[n - 1] != nums[n - 2]) {
        return nums[n - 1];
    }
    
    int low = 1;
    int high = n - 2;
    
    while (low <= high) {
        int mid = (low + high) / 2;
        
        
        if (nums[mid] != nums[mid + 1] && nums[mid] != nums[mid - 1]) {
            return nums[mid];
        }
        
        
        if ((mid % 2 == 1 && nums[mid] == nums[mid - 1]) || 
            (mid % 2 == 0 && nums[mid] == nums[mid + 1])) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return -1;
}

}
```

Optimization:
The given code is already optimized for finding the single non-duplicate element in a sorted array using a modified version of the binary search algorithm. However, there is a potential optimization that can be made to simplify the code and make it more readable.

Instead of checking if the middle element is part of the first pair in the duplicate group using the modulo operator, we can directly compare the middle element with its neighbors to determine which half of the array contains the single non-duplicate element.

Optimized code:

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int n = nums.length;

        // Base cases
        if (n == 1) {
            return nums[0];
        }
        if (nums[0] != nums[1]) {
            return nums[0];
        }
        if (nums[n - 1] != nums[n - 2]) {
            return nums[n - 1];
        }

        int low = 1;
        int high = n - 2;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            // Check if the middle element is the single non-duplicate element
            if (nums[mid] != nums[mid + 1] && nums[mid] != nums[mid - 1]) {
                return nums[mid];
            }

            // If the left neighbor is different from the middle element
            if (nums[mid] != nums[mid - 1]) {
                high = mid - 1; // Search in the left half
            } else {
                low = mid + 1; // Search in the right half
            }
        }

        return -1; // Should never reach this point
    }
}
```

In the optimized code, instead of checking if the middle element is part of the first pair in the duplicate group, we directly compare `nums[mid]` with `nums[mid - 1]`. If they are different, it means the single non-duplicate element is in the left half, so we update `high` to `mid - 1`. Otherwise, the single non-duplicate element is in the right half, so we update `low` to `mid + 1`.

The time complexity and space complexity of the optimized code remain O(log n) and O(1), respectively, as the underlying algorithm is still the modified binary search.

**49. Find Peak Element**

[Find Peak Element](https://leetcode.com/problems/find-peak-element/description/)

A peak element is an element that is strictly greater than its neighbors.

Given a 0-indexed integer array nums, find a peak element, and return its index. If the array contains multiple peaks, return the index to any of the peaks.

You may imagine that nums[-1] = nums[n] = -∞. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.

You must write an algorithm that runs in O(log n) time.

Example 1:

Input: nums = [1,2,3,1]

Output: 2

Explanation: 3 is a peak element and your function should return the index number 2.

Example 2:

Input: nums = [1,2,1,3,5,6,4]

Output: 5

Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.

The above code is a Java implementation of a solution to the "Find Peak Element" problem on LeetCode. The problem asks to find the index of a peak element in a given array of integers, where a peak element is an element that is strictly greater than its neighbors.

Pseudo-code:

```
FindPeakElement(nums):
    n = length(nums)

    # Base cases
    if n == 1:
        return 0  # Single element is a peak
    if nums[0] > nums[1]:
        return 0  # First element is a peak
    if nums[n - 1] > nums[n - 2]:
        return n - 1  # Last element is a peak

    low = 1
    high = n - 2

    while low <= high:
        mid = (low + high) // 2

        # Check if the middle element is a peak
        if nums[mid] > nums[mid - 1] and nums[mid] > nums[mid + 1]:
            return mid

        # If the left neighbor is smaller, search in the right half
        if nums[mid] > nums[mid - 1]:
            low = mid + 1
        # If the right neighbor is smaller, search in the left half
        else:
            high = mid - 1

    # Should never reach this point
    return 0
```

Explanation (with an example):
Let's consider the array `nums = [1, 2, 3, 1]`.

1. The `findPeakElement` function is called with `nums`.
2. Since `n = 4`, `nums[0] = 1 < nums[1] = 2`, and `nums[n - 1] = 1 < nums[n - 2] = 3`, the function proceeds to the binary search.
3. Iteration 1:
   - `low = 1`, `high = 2`
   - `mid = (1 + 2) // 2 = 1`
   - `nums[mid] = 2 < nums[mid + 1] = 3`, so `nums[mid]` is not a peak element
   - `nums[mid] < nums[mid + 1]`, so the function searches in the right half
   - `low = mid + 1 = 2`

4. Iteration 2:
   - `low = 2`, `high = 2`
   - `mid = (2 + 2) // 2 = 2`
   - `nums[mid] = 3 > nums[mid - 1] = 2 and nums[mid] > nums[mid + 1] = 1`, so `nums[mid]` is a peak element
   - The function returns `mid = 2`.

Time Complexity:
The time complexity of the `findPeakElement` function is O(log n), where n is the length of the input array. This is because it uses a modified version of the binary search algorithm, which halves the search space in each iteration, resulting in a logarithmic time complexity.

Space Complexity:
The space complexity of the `findPeakElement` function is O(1), as it uses a constant amount of extra space to store the `low`, `high`, `mid`, and `n` variables, regardless of the size of the input array.

Java code:

```java
class Solution {
    public int findPeakElement(int[] nums) {
        int n = nums.length;
        
        if (n == 1) return 0;
        
        if (nums[0] > nums[1]) return 0;
        
        if (nums[n-1] > nums[n-2]) return n-1;
        
        int low = 1;
        int high = n - 2;
        
        while (low <= high) {
            int mid = (low + high) / 2;
            
            if (nums[mid] > nums[mid - 1] && nums[mid] > nums[mid + 1]) {
                return mid;
            }
        
            else if (nums[mid] > nums[mid - 1]) {
                low = mid + 1;
            }
          
            else {
                high = mid - 1;
            }
        }
        return 0;
    }
}
```

Optimization:
The given code is already optimized for finding a peak element in an array using a modified version of the binary search algorithm. However, there is a potential optimization that can be made to simplify the code and make it more readable.

Instead of checking if the middle element is a peak element by comparing it with both its neighbors, we can directly compare it with its right neighbor. If the right neighbor is smaller, it means the middle element is a peak element or the peak element is in the left half. Otherwise, the peak element is in the right half.

Optimized code:

```java
class Solution {
    public int findPeakElement(int[] nums) {
        int n = nums.length;

        // Base cases
        if (n == 1) {
            return 0;  // Single element is a peak
        }
        if (nums[0] > nums[1]) {
            return 0;  // First element is a peak
        }
        if (nums[n - 1] > nums[n - 2]) {
            return n - 1;  // Last element is a peak
        }

        int low = 0;
        int high = n - 1;

        while (low < high) {
            int mid = low + (high - low) / 2;

            // If the right neighbor is smaller, the peak is on the left side
            if (nums[mid] > nums[mid + 1]) {
                high = mid;
            }
            // Otherwise, the peak is on the right side
            else {
                low = mid + 1;
            }
        }

        return low;
    }
}
```

In the optimized code, the function only compares the middle element with its right neighbor. If `nums[mid] > nums[mid + 1]`, it means the middle element is a peak element or the peak element is in the left half, so the function updates `high` to `mid`. Otherwise, the peak element is in the right half, so the function updates `low` to `mid + 1`.

The time complexity of the optimized `findPeakElement` function remains O(log n), where n is the length of the input array, as it still uses a modified version of the binary search algorithm. The space complexity remains O(1), as it uses a constant amount of extra space to store the `low`, `high`, and `n` variables.

## 17-05-2024

**50. Square root of a number**

[Square root of a number](https://www.geeksforgeeks.org/problems/square-root/0?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=square-root)

Given an integer x, find the square root of x. If x is not a perfect square, then return floor(√x).

Example 1:

Input:

x = 5

Output: 2

Explanation: Since, 5 is not a perfect 
square, floor of square_root of 5 is 2.

Example 2:

Input:

x = 4

Output: 2

Explanation: Since, 4 is a perfect 
square, so its square root is 2.

Pseudo-code:

```
FloorSqrt(x):
    if x == 0 or x == 1:
        return x

    low = 1
    high = x
    result = 0

    while low <= high:
        mid = (low + high) // 2
        midSquare = mid * mid

        if midSquare == x:
            return mid  # Exact square root found

        if midSquare < x:
            low = mid + 1
            result = mid  # Store the mid as the potential answer
        else:
            high = mid - 1

    return result
```

Explanation (with an example):
Let's consider `x = 15`.

1. The `floorSqrt` function is called with `x = 15`.
2. Iteration 1:
   - `low = 1`, `high = 15`
   - `mid = (1 + 15) // 2 = 8`
   - `midSquare = 8 * 8 = 64 > 15`, so the square root is in the left half
   - `high = mid - 1 = 7`

3. Iteration 2:
   - `low = 1`, `high = 7`
   - `mid = (1 + 7) // 2 = 4`
   - `midSquare = 4 * 4 = 16 < 15`, so the square root is in the right half
   - `low = mid + 1 = 5`, `result = mid = 4`

4. Iteration 3:
   - `low = 5`, `high = 7`
   - `mid = (5 + 7) // 2 = 6`
   - `midSquare = 6 * 6 = 36 > 15`, so the square root is in the left half
   - `high = mid - 1 = 5`

5. Iteration 4:
   - `low = 5`, `high = 5`
   - `mid = (5 + 5) // 2 = 5`
   - `midSquare = 5 * 5 = 25 < 15`, so the square root is in the right half
   - `low = mid + 1 = 6`, `result = mid = 5`

6. The loop terminates as `low > high`.
7. The function returns `result = 5`, which is the floor of the square root of `x = 15`.

Time Complexity:
The time complexity of the `floorSqrt` function is O(log x), where x is the input value. This is because it uses a modified version of the binary search algorithm, which halves the search space in each iteration, resulting in a logarithmic time complexity.

Space Complexity:
The space complexity of the `floorSqrt` function is O(1), as it uses a constant amount of extra space to store the `low`, `high`, `mid`, `midSquare`, and `result` variables, regardless of the size of the input value.

Java Code:

```java
long floorSqrt(long x) {
        if (x == 0 || x == 1) {
            return x;
        }

        long low = 1, high = x, result = 0;
        
        while (low <= high) {
            long mid = (low + high) / 2;
            long midSquare = mid * mid;

            // Check if mid is the perfect square root
            if (midSquare == x) {
                return mid;
            }

            // If midSquare is less than x, then the square root is in the right half
            if (midSquare < x) {
                low = mid + 1;
                result = mid;  // Store the mid as the potential answer
            } else {
                // If midSquare is greater than x, then the square root is in the left half
                high = mid - 1;
            }
        }
        return result;
    }
```

Optimization:
The given code is already optimized for finding the floor of the square root of a non-negative integer using a modified version of the binary search algorithm. However, there is a potential optimization that can be made to reduce the number of iterations in certain cases.

Instead of initializing `low` to 1 and `high` to `x`, we can use a better initial range for the binary search. We can set `low` to 1 and `high` to the minimum of `x` and `46340` (since the square root of `46340 * 46340 = 2^31 - 1`, which is the maximum value representable by a signed 32-bit integer).

Optimized code:

```java
long floorSqrt(long x) {
    if (x == 0 || x == 1) {
        return x;
    }

    long low = 1;
    long high = Math.min(x, 46340); // Use a better initial range for binary search
    long result = 0;

    while (low <= high) {
        long mid = low + (high - low) / 2;
        long midSquare = mid * mid;

        if (midSquare == x) {
            return mid;
        } else if (midSquare < x) {
            low = mid + 1;
            result = mid;
        } else {
            high = mid - 1;
        }
    }

    return result;
}
```

In the optimized code, we set `high` to `Math.min(x, 46340)` instead of `x`. This ensures that the initial range for the binary search is smaller, potentially reducing the number of iterations required to find the floor of the square root.

The time complexity of the optimized `floorSqrt` function remains O(log x), where x is the input value. However, for larger values of `x`, the optimization can lead to a constant factor improvement in the running time.

The space complexity remains O(1), as it uses a constant amount of extra space to store the variables.