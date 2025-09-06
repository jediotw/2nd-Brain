# Sorting Algorithms | Saurabh Choudhary
  

| Algorithm                 | Best Time Complexity | Average Time Complexity | Worst Time Complexity | Space Complexity | Stable | In-place |
| ------------------------- | -------------------- | ----------------------- | --------------------- | ---------------- | ------ | -------- |
| **Bubble Sort**           | O(n)                 | O(n²)                   | O(n²)                 | O(1)             | Yes    | Yes      |
| **Direct Insertion Sort** | O(n)                 | O(n²)                   | O(n²)                 | O(1)             | Yes    | Yes      |
| **Binary Insertion Sort** | O(n)                 | O(n²)                   | O(n²)                 | O(1)             | Yes    | Yes      |
| **Selection Sort**        | O(n²)                | O(n²)                   | O(n²)                 | O(1)             | No     | Yes      |
| **Shell Sort**            | O(n)                 | O(n^1.3)                | O(n²)                 | O(1)             | No     | Yes      |
| **Merge Sort**            | O(n log n)           | O(n log n)              | O(n log n)            | O(n)             | Yes    | No       |
| **Quick Sort**            | O(n log n)           | O(n log n)              | O(n²)                 | O(log n)         | No     | Yes      |
| **Heap Sort**             | O(n log n)           | O(n log n)              | O(n log n)            | O(1)             | No     | Yes      |
| **Bucket Sort**           | O(n)                 | O(n log(n/m))           | O(n²)                 | O(n)             | Yes    | No       |
| **Counting Sort**         | O(n + k)             | O(n + k)                | O(n + k)              | O(k)             | Yes    | No       |
| **Radix Sort**            | O(nk)                | O(nk)                   | O(nk)                 | O(n + k)         | Yes    | No       |


* * *

Contents

* * *

*   [Bubble Sort](#bubble-sort)
*   [Insertion Sort](#insertion-sort)
    *   [Direct Insertion Sort](#direct-insertion-sort)
    *   [Binary Insertion Sort](#binary-insertion-sort)
    *   [Shell Sort (Hill Sort)](#shell-sort-hill-sort)
*   [Selection Sort](#selection-sort)
*   [Merge Sort](#merge-sort)
*   [Quick Sort](#quick-sort)
*   [Heap Sort](#heap-sort)
*   [Linear Sort](#linear-sort)
    *   [Bucket Sort](#bucket-sort)
    *   [Counting Sort](#counting-sort)
    *   [Radix Sort](#radix-sort)

* * *

Bubble Sort[](#bubble-sort)
---------------------------

**Mechanism:** Bubble Sort is a simple sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The process is repeated until the list is sorted.

[![](https://www.cwblogs.com/assets/img/note/algorithm/sort1.jpg)](/assets/img/note/algorithm/sort1.jpg)

**Advantages:**

*   Simple and easy to understand.
*   Works well for small datasets or nearly sorted arrays.

**Disadvantages:**

*   Inefficient for large datasets with a time complexity of O(n^2).

``

Insertion Sort[](#insertion-sort)
---------------------------------

### Direct Insertion Sort[](#direct-insertion-sort)

**Mechanism:** This algorithm iteratively takes one element from the unsorted portion and finds its appropriate place in the sorted portion of the array.

[![](https://www.cwblogs.com/assets/img/note/algorithm/sort2.jpg)](/assets/img/note/algorithm/sort2.jpg)

**Advantages:**

*   Simple implementation.
*   Efficient for (nearly) sorted data sets.

**Disadvantages:**

*   Poor efficiency on large, unsorted data sets.

``

> **Why is insertion sort more popular than bubble sort** since both bubble sort and insertion sort have the same time complexity O(n^2) and are stable sorting algorithms?
> 
> *   **Because data swapping in a bubbling sort is more complex** than data movement in an insertion sort (bubbling requires 3 assignment operations, while insertion only requires 1)

### Binary Insertion Sort[](#binary-insertion-sort)

**Mechanism:** Similar to direct insertion but uses binary search to find the proper location for insertion, reducing comparisons.

[![](https://www.cwblogs.com/assets/img/note/algorithm/sort2.jpg)](/assets/img/note/algorithm/sort2.jpg) _same as the direct insertion sort (except that it’s faster to find the insertion position)_

**Advantages:**

*   Reduced number of comparisons.

**Disadvantages:**

*   More complex than direct insertion sort.
*   Movement of elements is still costly.

``

> **Why is the time complexity of binary insertion sort still n2?**
> 
> *   Although the number of comparisons is reduced, the number of swaps is not, and all the elements still need to be shifted after the position is found.

### Shell Sort (Hill Sort)
[](#shell-sort-hill-sort)

**Mechanism:** An extension of insertion sort that allows the exchange of far apart elements to improve speed. Shell sort improves the efficiency of insertion sort by moving larger elements in advance to reduce the number of reverse order pairs.

[![](https://www.cwblogs.com/assets/img/note/algorithm/sort7.jpg)](/assets/img/note/algorithm/sort7.jpg) _from: http://stoimen.com/2012/02/27/computer-algorithms-shell-sort/_

**Advantages:**

*   Better handling of large data sets compared to simple insertion.

**Disadvantages:**

*   Gap sequence choice is critical for performance.
    *   Initially Shell proposed to take `gap = n/2` and `gap = gap/2` up to `gap = 1`. Later Knuth proposed to take `gap = gap/3 + 1`. Neither claim has been proved.

``

Selection Sort[](#selection-sort)
---------------------------------

**Mechanism:** Repeatedly finding the minimum element (considering ascending order) from the unsorted part and putting it at the beginning.

[![](https://www.cwblogs.com/assets/img/note/algorithm/sort3.jpg)](/assets/img/note/algorithm/sort3.jpg)

**Advantages:**

*   Simplicity and ease of understanding.

**Disadvantages:**

*   Inefficient on large lists.

``

> **Is selection sort a stable sorting algorithm?**
> 
> *   **No.** Selection sort has to find the smallest of the remaining unsorted elements each time and swap places with the previous element, which breaks stability. For example, if you sort a set of 5, 8, 5, 2, 9 using the selection sort algorithm, the first time you find the smallest element, 2, and swap places with the first 5, the order of the first 5 and the middle 5 changes, so it is unstable.
>     *   **It is for this reason that Selection Sort is slightly inferior to Bubble Sort and Insertion Sort.**

Merge Sort[](#merge-sort)
-------------------------

**Mechanism:** Merge Sort is a **divide-and-conquer** algorithm that divides the input array into two halves, calls itself for the two halves, and then merges the two sorted halves.

[![](https://www.cwblogs.com/assets/img/note/algorithm/sort4.jpg)](/assets/img/note/algorithm/sort4.jpg)

**Advantages:**

*   Stable sorting algorithm.
*   Consistently runs in O(n log n) time.

**Disadvantages:**

*   Requires additional space proportional to the array size.
*   Slightly more complex than other simple sorting algorithms.

``

Quick Sort[](#quick-sort)
-------------------------

**Mechanism:** Quick Sort is a **divide-and-conquer** algorithm. It picks an element as a pivot and partitions the given array around the picked pivot. There are different versions of quickSort that pick pivot in different ways.

[![](https://www.cwblogs.com/assets/img/note/algorithm/sort5.jpg)](/assets/img/note/algorithm/sort5.jpg)

**Advantages:**

*   One of the fastest sorting algorithms for average cases.
*   Space-efficient and does not require additional storage.

**Disadvantages:**

*   Worst-case time complexity can be O(n^2), although this is rare.
*   Not stable, meaning it may change the relative order of elements with equal keys.

``

[![](https://www.cwblogs.com/assets/img/note/algorithm/sort6.jpg)](/assets/img/note/algorithm/sort6.jpg) _partition(int arr\[\], int low, int high)_

* * *

We can use `partition()` in the quick sort algorithm to **find the K largest element in an unordered array in O(n)** time complexity.

``

Heap Sort[](#heap-sort)
-----------------------

**Mechanism:** Builds a max heap from the data, then repeatedly extracts the maximum element from the heap and rebuilds the heap until all elements are sorted.

[![](https://www.cwblogs.com/assets/img/note/algorithm/sort8.jpg)](/assets/img/note/algorithm/sort8.jpg)

**Advantages:**

*   Good for large data sets, with consistent performance.

**Disadvantages:**

*   Relatively complex algorithm, not stable.

``

> **In practice, why does Quick Sort perform better than Heap Sort?**
> 
> 1.  **Data access** of Heap Sort is **worse** than Quick Sort.
>     *   For quick sort, data is accessed sequentially. Whereas, for heap sort, the data is accessed in jumps. This is not friendly to the CPU cache.
> 2.  In general, Heap Sort has **more data swaps** than Quick Sort.

Linear Sort[](#linear-sort)
---------------------------

Linear Sort refers to a **sorting algorithm that has a linear time complexity (`O(n)`, `O(n + k)`, `O(nk)`)**.

### Bucket Sort[](#bucket-sort)

**Mechanism:** Distributes elements into several “buckets” and sorts these individually.

[![](https://www.cwblogs.com/assets/img/note/algorithm/sort9.png)](/assets/img/note/algorithm/sort9.png)

**Advantages:**

*   Fast when the input is uniformly distributed.
*   It Can be applied to external sorting.
    *   External sorting means that the sorted data is stored in an external disk. (Due to the relatively large amount of data and limited memory, it is not possible to load all the data into internal memory)

**Disadvantages:**

*   The requirements for the data to be sorted are very demanding (Ideally, the data is distributed evenly across the buckets).
*   Performance depends on data distribution and bucket count.

``

### Counting Sort[](#counting-sort)

**Mechanism:** Counts the occurrences of each value to sort. Counting sort is actually a special case of bucket sorting (Assign a bucket to each possible value so that the data values in each bucket are the same, eliminating the need to sort the buckets).

[![](https://www.cwblogs.com/assets/img/note/algorithm/sort10.jpg)](/assets/img/note/algorithm/sort10.jpg)

**Advantages:**

*   Linear time complexity in the suitable context.

**Disadvantages:**

*   Not suitable for data with large range relative to the number of elements.
*   Not an in-place algorithm.

``

### Radix Sort[](#radix-sort)

**Mechanism:** Sorts numbers digit by digit, starting from the least significant digit to the most significant.

[![](https://www.cwblogs.com/assets/img/note/algorithm/sort11.jpg)](/assets/img/note/algorithm/sort11.jpg)

**Advantages:**

*   Can be faster than comparison-based algorithms for large data sets.

**Disadvantages:**

*   Only works for integer keys or types that can be represented as such.
*   Depends on another stable sort algorithm (like counting sort) for sorting digits.

``

* * *

