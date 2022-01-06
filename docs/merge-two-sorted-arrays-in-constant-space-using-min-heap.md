# 使用最小堆

在恒定空间合并两个排序的数组

> 原文:[https://www . geeksforgeeks . org/merge-two-sorted-arrays-in-constant-space-use-min-heap/](https://www.geeksforgeeks.org/merge-two-sorted-arrays-in-constant-space-using-min-heap/)

给定两个排序数组，我们需要将它们与 O(1)个额外空间合并成一个排序数组，此时 N 是第一个数组的大小，M 是第二个数组的大小。

**例**:

```
Input: arr1[] = {10};
       arr2[] = {2, 3};
Output: arr1[] = {2}
        arr2[] = {3, 10}  

Input: arr1[] = {1, 5, 9, 10, 15, 20};
       arr2[] = {2, 3, 8, 13};
Output: arr1[] = {1, 2, 3, 5, 8, 9}
        arr2[] = {10, 13, 15, 20} 

```

我们已经讨论了在常数空间中解决上述问题的另外两种方法:

*   [将两个排序后的数组合并为 O(1)个额外空间](https://www.geeksforgeeks.org/merge-two-sorted-arrays-o1-extra-space/)。
*   [用 O(1)个额外空间高效合并两个排序数组](https://www.geeksforgeeks.org/efficiently-merging-two-sorted-arrays-with-o1-extra-space/)。

在本文中，我们将讨论使用堆数据结构概念的另一种方法，而不会占用额外的空间来合并两个排序数组。

以下是详细的步骤方法:

1.  想法是首先将第二个数组转换成最小堆。这可以在 O(M)时间复杂度内完成。
2.  将第二个数组转换为最小堆后:
    *   开始遍历第一个数组，并将第一个数组的当前元素与创建的 min_heap 的顶部进行比较。
    *   如果第一个数组中的当前元素大于堆顶部，则将第一个数组的当前元素与堆的根交换，并堆化 min_heap 的根。
    *   对第一个数组的每个元素执行上述操作后，第一个数组现在将包含排序合并数组的前 N 个元素。
3.  现在，保留在 min_heap 或第二个数组中的元素是排序合并数组的最后 M 个元素。
4.  要按排序顺序排列它们，请在第二个数组上应用就地堆。

**注**:我们使用了 C++中可用的内置 STL 函数，将数组转换为 min_heap，对堆进行排序等。建议先阅读–[c++ STL 中的 Heap | make _ Heap()，push_heap()，pop_heap()，sort_heap()](https://www.geeksforgeeks.org/heap-using-stl-c/) 再进入程序。

下面是上述方法的实现:

```
// C++ program to merge two sorted arrays in
// constant space

#include <bits/stdc++.h>
using namespace std;

// Function to merge two sorted arrays in
// constant space
void mergeArrays(int* a, int n, int* b, int m)
{

    // Convert second array into a min_heap
    // using make_heap() STL function [takes O(m)]
    make_heap(b, b + m, greater<int>());

    // Start traversing the first array
    for (int i = 0; i < n; i++) {

        // If current element is greater than root
        // of min_heap
        if (a[i] > b[0]) {

            // Pop minimum element from min_heap using
            // pop_heap() STL function
            // The pop_heap() function removes the minimum element from
            // heap and moves it to the end of the container
            // converted to heap and reduces heap size by 1
            pop_heap(b, b + m, greater<int>());

            // Swapping the elements
            int tmp = a[i];
            a[i] = b[m - 1];
            b[m - 1] = tmp;

            // Apply push_heap() function on the container
            // or array to again reorder it in the
            // form of min_heap
            push_heap(b, b + m, greater<int>());
        }
    }

    // Convert the second array again into max_heap
    // because sort_heap() on min heap sorts the array
    // in decreasing order
    // This step is [O(m)]
    make_heap(b, b + m); // It's a max_heap

    // Sort the second array using sort_heap() function
    sort_heap(b, b + m);
}

// Driver Code
int main()
{

    int ar1[] = { 1, 5, 9, 10, 15, 20 };
    int ar2[] = { 2, 3, 8, 13 };
    int m = sizeof(ar1) / sizeof(ar1[0]);
    int n = sizeof(ar2) / sizeof(ar2[0]);
    mergeArrays(ar1, m, ar2, n);

    cout << "After Merging :- \nFirst Array: ";
    for (int i = 0; i < m; i++)
        cout << ar1[i] << " ";
    cout << "\nSecond Array: ";
    for (int i = 0; i < n; i++)
        cout << ar2[i] << " ";

    return 0;
}
```

**Output:**

```
After Merging :- 
First Array: 1 2 3 5 8 9 
Second Array: 10 13 15 20

```

**时间复杂度**:O(N * logM+M * logN)
T3】辅助空间 : O(1)