# 使用堆

合并 O(1)个额外空间中的两个排序数组

> 原文:[https://www . geesforgeks . org/merge-two-sorted-arrays-in-O1-extra-space-use-heap/](https://www.geeksforgeeks.org/merge-two-sorted-arrays-in-o1-extra-space-using-heap/)

给定大小为 **N** 和 **M** 的两个[排序数组](https://www.geeksforgeeks.org/search-insert-and-delete-in-a-sorted-array/)、 **arr[]** 、 **brr[]** ，任务是**合并两个给定数组**，使得它们形成组合两个数组元素的整数排序序列。

**示例:**

> **输入:** arr[] = {10}，brr[] = {2，3}
> **输出** : 2 3 10
> **说明:**从两个数组中取所有元素得到的合并排序数组为{2，3，10}。
> 因此，要求的输出是 2 3 10。
> 
> **输入:** arr[] = {1，5，9，10，15，20}，brr[] = {2，3，8，13}
> **输出:** 1 2 3 5 8 9 10 13 15 20

**简单方法:**参考[合并两个排序的数组](https://www.geeksforgeeks.org/merge-two-sorted-arrays/)获得合并两个给定数组的最简单方法。
***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*

**空间优化方法:**参考[合并两个有 O(1)个额外空间的排序数组](https://www.geeksforgeeks.org/merge-two-sorted-arrays-o1-extra-space/)合并两个给定的数组而不使用任何额外的内存。
***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*

**高效空间优化方法:**参考[高效合并两个有 O(1)个额外空间的排序数组](https://www.geeksforgeeks.org/efficiently-merging-two-sorted-arrays-with-o1-extra-space/)来合并两个给定的数组而不使用任何额外的内存。
***时间复杂度:**O((N+M)* log(N+M))*
***辅助空间:** O(1)*

[**堆**](https://www.geeksforgeeks.org/binary-heap/)**–基于方法:**使用[堆](https://www.geeksforgeeks.org/binary-heap/)可以解决问题。思路是遍历 **arr[]** 数组，比较 **arr[i]** 与 **brr[0]** 的值，检查 **arr[i]** 是否大于 **brr[0]** 。如果发现为真，则**交换(arr[i]、brr[0]**，并在 **brr[]** 上执行 [heapify](https://www.geeksforgeeks.org/building-heap-from-array/) 操作。按照以下步骤解决问题:

*   [遍历数组 arr[]](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) ，将 **arr[i]** 的值与 brr[0]进行比较，检查 **arr[i]** 是否大于 **brr[0]** 。如果发现为真，则**交换(arr[i]、brr[0])**，并在 **brr[]** 上执行 [heapify](https://www.geeksforgeeks.org/building-heap-from-array/) 操作。
*   最后，[对数组](https://www.geeksforgeeks.org/sort-c-stl/) **brr[]** 进行排序，打印两个数组。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to perform min heapify
// on array brr[]
void minHeapify(int brr[], int i, int M)
{

    // Stores index of left child
    // of i.
    int left = 2 * i + 1;

    // Stores index of right child
    // of i.
    int right = 2 * i + 2;

    // Stores index of the smallest element
    // in (arr[i], arr[left], arr[right])
    int smallest = i;

    // Check if arr[left] less than
    // arr[smallest]
    if (left < M && brr[left] < brr[smallest]) {

        // Update smallest
        smallest = left;
    }

    // Check if arr[right] less than
    // arr[smallest]
    if (right < M && brr[right] < brr[smallest]) {

        // Update smallest
        smallest = right;
    }

    // if i is not the index
    // of smallest element
    if (smallest != i) {

        // Swap arr[i] and arr[smallest]
        swap(brr[i], brr[smallest]);

        // Perform heapify on smallest
        minHeapify(brr, smallest, M);
    }
}

// Function to merge two sorted arrays
void merge(int arr[], int brr[],
           int N, int M)
{

    // Traverse the array arr[]
    for (int i = 0; i < N; ++i) {

        // Check if current element
        // is less than brr[0]
        if (arr[i] > brr[0]) {

            // Swap arr[i] and brr[0]
            swap(arr[i], brr[0]);

            // Perform heapify on brr[]
            minHeapify(brr, 0, M);
        }
    }

    // Sort array brr[]
    sort(brr, brr + M);
}

// Function to print array elements
void printArray(int arr[], int N)
{

    // Traverse array arr[]
    for (int i = 0; i < N; i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{
    int arr[] = { 2, 23, 35, 235, 2335 };
    int brr[] = { 3, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = sizeof(brr) / sizeof(brr[0]);

    // Function call to merge
    // two array
    merge(arr, brr, N, M);

    // Print first array
    printArray(arr, N);

    // Print Second array.
    printArray(brr, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to perform
// min heapify on array
// brr[]
static void minHeapify(int brr[],
                       int i, int M)
{
  // Stores index of left
  // child of i.
  int left = 2 * i + 1;

  // Stores index of right
  // child of i.
  int right = 2 * i + 2;

  // Stores index of the smallest
  // element in (arr[i], arr[left],
  // arr[right])
  int smallest = i;

  // Check if arr[left] less than
  // arr[smallest]
  if (left < M && brr[left] <
      brr[smallest])
  {
    // Update smallest
    smallest = left;
  }

  // Check if arr[right] less
  // than arr[smallest]
  if (right < M && brr[right] <
      brr[smallest])
  {
    // Update smallest
    smallest = right;
  }

  // if i is not the index
  // of smallest element
  if (smallest != i)
  {
    // Swap arr[i] and
    // arr[smallest]
    int temp = brr[i];
    brr[i] =  brr[smallest];
    brr[smallest] = temp;

    // Perform heapify on smallest
    minHeapify(brr, smallest, M);
  }
}

// Function to merge two
// sorted arrays
static void merge(int arr[], int brr[],
                  int N, int M)
{
  // Traverse the array arr[]
  for (int i = 0; i < N; ++i)
  {
    // Check if current element
    // is less than brr[0]
    if (arr[i] > brr[0])
    {
      // Swap arr[i] and brr[0]
      int temp = arr[i];
      arr[i] = brr[0];
      brr[0] = temp;

      // Perform heapify on brr[]
      minHeapify(brr, 0, M);
    }
  }

  // Sort array brr[]
  Arrays.sort(brr);
}

// Function to print array
// elements
static void printArray(int arr[],
                       int N)
{
  // Traverse array arr[]
  for (int i = 0; i < N; i++)
    System.out.print(arr[i] + " ");
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {2, 23, 35, 235, 2335};
  int brr[] = {3, 5};
  int N = arr.length;
  int M = brr.length;

  // Function call to merge
  // two array
  merge(arr, brr, N, M);

  // Print first array
  printArray(arr, N);

  // Print Second array.
  printArray(brr, M);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to perform min heapify
# on array brr[]
def minHeapify(brr, i, M):

    # Stores index of left child
    # of i.
    left = 2 * i + 1

    # Stores index of right child
    # of i.
    right = 2 * i + 2

    # Stores index of the smallest element
    # in (arr[i], arr[left], arr[right])
    smallest = i

    # Check if arr[left] less than
    # arr[smallest]
    if (left < M and brr[left] < brr[smallest]):

        # Update smallest
        smallest = left

    # Check if arr[right] less than
    # arr[smallest]
    if (right < M and brr[right] < brr[smallest]):

        # Update smallest
        smallest = right

    # If i is not the index
    # of smallest element
    if (smallest != i):

        # Swap arr[i] and arr[smallest]
        brr[i], brr[smallest] = brr[smallest], brr[i]

        # Perform heapify on smallest
        minHeapify(brr, smallest, M)

# Function to merge two sorted arrays
def merge(arr, brr, N, M):

    # Traverse the array arr[]
    for i in range(N):

        # Check if current element
        # is less than brr[0]
        if (arr[i] > brr[0]):

            # Swap arr[i] and brr[0]
            arr[i], brr[0] = brr[0], arr[i]

            # Perform heapify on brr[]
            minHeapify(brr, 0, M)

    # Sort array brr[]
    brr.sort()

# Function to print array elements
def printArray(arr, N):

    # Traverse array arr[]
    for i in range(N):
        print(arr[i], end = " ")

# Driver code
if __name__ == '__main__':

    arr = [ 2, 23, 35, 235, 2335 ]
    brr = [3, 5]
    N = len(arr)
    M = len(brr)

    # Function call to merge
    # two array
    merge(arr, brr, N, M)

    # Print first array
    printArray(arr, N)

    # Print Second array.
    printArray(brr, M)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to perform
// min heapify on array
// brr[]
static void minHeapify(int []brr,
                       int i, int M)
{

  // Stores index of left
  // child of i.
  int left = 2 * i + 1;

  // Stores index of right
  // child of i.
  int right = 2 * i + 2;

  // Stores index of the smallest
  // element in (arr[i], arr[left],
  // arr[right])
  int smallest = i;

  // Check if arr[left] less than
  // arr[smallest]
  if (left < M && brr[left] <
      brr[smallest])
  {

    // Update smallest
    smallest = left;
  }

  // Check if arr[right] less
  // than arr[smallest]
  if (right < M && brr[right] <
      brr[smallest])
  {

    // Update smallest
    smallest = right;
  }

  // If i is not the index
  // of smallest element
  if (smallest != i)
  {

    // Swap arr[i] and
    // arr[smallest]
    int temp = brr[i];
    brr[i] =  brr[smallest];
    brr[smallest] = temp;

    // Perform heapify on smallest
    minHeapify(brr, smallest, M);
  }
}

// Function to merge two
// sorted arrays
static void merge(int []arr, int[]brr,
                  int N, int M)
{

  // Traverse the array []arr
  for(int i = 0; i < N; ++i)
  {

    // Check if current element
    // is less than brr[0]
    if (arr[i] > brr[0])
    {

      // Swap arr[i] and brr[0]
      int temp = arr[i];
      arr[i] = brr[0];
      brr[0] = temp;

      // Perform heapify on brr[]
      minHeapify(brr, 0, M);
    }
  }

  // Sort array brr[]
  Array.Sort(brr);
}

// Function to print array
// elements
static void printArray(int []arr,
                       int N)
{

  // Traverse array []arr
  for(int i = 0; i < N; i++)
    Console.Write(arr[i] + " ");
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = { 2, 23, 35, 235, 2335 };
  int []brr = {3, 5};
  int N = arr.Length;
  int M = brr.Length;

  // Function call to merge
  // two array
  merge(arr, brr, N, M);

  // Print first array
  printArray(arr, N);

  // Print Second array.
  printArray(brr, M);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to perform min heapify
// on array brr[]
function minHeapify(brr, i, M)
{

    // Stores index of left child
    // of i.
    let left = 2 * i + 1;

    // Stores index of right child
    // of i.
    let right = 2 * i + 2;

    // Stores index of the smallest element
    // in (arr[i], arr[left], arr[right])
    let smallest = i;

    // Check if arr[left] less than
    // arr[smallest]
    if (left < M && brr[left] < brr[smallest]) {

        // Update smallest
        smallest = left;
    }

    // Check if arr[right] less than
    // arr[smallest]
    if (right < M && brr[right] < brr[smallest]) {

        // Update smallest
        smallest = right;
    }

    // if i is not the index
    // of smallest element
    if (smallest != i) {

        // Swap arr[i] and arr[smallest]
        let temp = brr[i];
        brr[i] =  brr[smallest];
        brr[smallest] = temp;

        // Perform heapify on smallest
        minHeapify(brr, smallest, M);
    }
}

// Function to merge two sorted arrays
function merge(arr, brr,
        N, M)
{

    // Traverse the array arr[]
    for (let i = 0; i < N; ++i) {

        // Check if current element
        // is less than brr[0]
        if (arr[i] > brr[0]) {

            // Swap arr[i] and brr[0]
            let temp = arr[i];
              arr[i] = brr[0];
              brr[0] = temp;

            // Perform heapify on brr[]
            minHeapify(brr, 0, M);
        }
    }

    // Sort array brr[]
    brr.sort();
}

// Function to print array elements
function printArray(arr, N)
{

    // Traverse array arr[]
    for (let i = 0; i < N; i++)
        document.write(arr[i] + " ");
}

// Driver Code

    let arr = [ 2, 23, 35, 235, 2335 ];
    let brr = [ 3, 5 ];
    let N = arr.length;
    let M = brr.length;

    // Function call to merge
    // two array
    merge(arr, brr, N, M);

    // Print first array
    printArray(arr, N);

    // Print Second array.
    printArray(brr, M);

//This code is contributed by Mayank Tyagi
</script>
```

**Output:** 

```
2 3 5 23 35 235 2335
```

***时间复杂度:**O((N+M)* log(M))*
***辅助空间:** O(1)*

**有效方法:**参考[合并两个排序的数组](https://www.geeksforgeeks.org/merge-two-sorted-arrays/)来有效合并两个给定的数组。
***时间复杂度:** O(N + M)*
***辅助空间:** O(N + M)*