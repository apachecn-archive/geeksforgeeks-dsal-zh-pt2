# 使用插入排序对数组进行排序所需的计数交换

> 原文:[https://www . geesforgeks . org/count-swaps-required-to-sort-a-array-use-insert-sort/](https://www.geeksforgeeks.org/count-swaps-required-to-sort-an-array-using-insertion-sort/)

给定一个大小为**N**(*1≤N≤10<sup>5</sup>*)的[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[]** ，任务是使用[插入排序](https://www.geeksforgeeks.org/insertion-sort/)算法计算[排序数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)所需的交换次数。

**示例:**

> **输入:** A[] = {2，1，3，1，2}
> **输出:** 4
> **说明:**
> 
> 步骤 1: arr[0]保持在初始位置。
> 第二步:arr[1]向左移动 1 位。计数= 1。
> 第三步:arr[2]保持在初始位置。
> 第四步:arr[3]向左移动两个位置。计数= 2。
> 第五步:arr[5]向右移动 1 位。计数= 1。
> 
> **输入:** A[]={12，15，1，5，6，14，11}
> **输出:** 10

**方式:**问题可以使用**分治算法** ( [合并排序](https://www.geeksforgeeks.org/merge-sort/))解决。按照以下步骤解决问题:

*   将数组分成两半，并递归遍历这两半。
*   对每一半进行排序，并计算所需的交换次数。
*   最后，打印所需的交换总数。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores the sorted
// array elements
int temp[100000];

// Function to count the number of
// swaps required to merge two sorted
// subarray in a sorted form
long int merge(int A[], int left,
               int mid, int right)
{

    // Stores the count of swaps
    long int swaps = 0;

    int i = left, j = mid, k = left;

    while (i < mid && j <= right) {

        if (A[i] <= A[j]) {
            temp[k] = A[i];
            k++, i++;
        }
        else {
            temp[k] = A[j];
            k++, j++;
            swaps += mid - i;
        }
    }
    while (i < mid) {
        temp[k] = A[i];
        k++, i++;
    }

    while (j <= right) {
        temp[k] = A[j];
        k++, j++;
    }

    while (left <= right) {
        A[left] = temp[left];
        left++;
    }

    return swaps;
}

// Function to count the total number
// of swaps required to sort the array
long int mergeInsertionSwap(int A[],
                            int left, int right)
{
    // Stores the total count
    // of swaps required
    long int swaps = 0;
    if (left < right) {

        // Find the middle index
        // splitting the two halves
        int mid = left + (right - left) / 2;

        // Count the number of swaps
        // required to sort the left subarray
        swaps += mergeInsertionSwap(A, left, mid);

        // Count the number of swaps
        // required to sort the right subarray
        swaps += mergeInsertionSwap(A, mid + 1, right);

        // Count the number of swaps required
        // to sort the two sorted subarrays
        swaps += merge(A, left, mid + 1, right);
    }
    return swaps;
}

// Driver Code
int main()
{
    int A[] = { 2, 1, 3, 1, 2 };
    int N = sizeof(A) / sizeof(A[0]);
    cout << mergeInsertionSwap(A, 0, N - 1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Stores the sorted
  // array elements
  static int temp[] = new int[100000];

  // Function to count the number of
  // swaps required to merge two sorted
  // subarray in a sorted form
  static int merge(int A[], int left,
                   int mid, int right)
  {

    // Stores the count of swaps
    int swaps = 0;
    int i = left, j = mid, k = left;
    while (i < mid && j <= right)
    {
      if (A[i] <= A[j])
      {
        temp[k] = A[i];
        k++; i++;
      }
      else
      {
        temp[k] = A[j];
        k++; j++;
        swaps += mid - i;
      }
    }
    while (i < mid)
    {
      temp[k] = A[i];
      k++; i++;
    }

    while (j <= right)
    {
      temp[k] = A[j];
      k++; j++;
    }

    while (left <= right)
    {
      A[left] = temp[left];
      left++;
    }
    return swaps;
  }

  // Function to count the total number
  // of swaps required to sort the array
  static int mergeInsertionSwap(int A[],
                                int left, int right)
  {
    // Stores the total count
    // of swaps required
    int swaps = 0;
    if (left < right)
    {

      // Find the middle index
      // splitting the two halves
      int mid = left + (right - left) / 2;

      // Count the number of swaps
      // required to sort the left subarray
      swaps += mergeInsertionSwap(A, left, mid);

      // Count the number of swaps
      // required to sort the right subarray
      swaps += mergeInsertionSwap(A, mid + 1, right);

      // Count the number of swaps required
      // to sort the two sorted subarrays
      swaps += merge(A, left, mid + 1, right);
    }
    return swaps;
  }

  // Driver code
  public static void main(String[] args)
  {
    int A[] = { 2, 1, 3, 1, 2 };
    int N = A.length;
    System.out.println(mergeInsertionSwap(A, 0, N - 1));
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Stores the sorted
# array elements
temp = [0] * 100000

# Function to count the number of
# swaps required to merge two sorted
# subarray in a sorted form
def merge(A, left, mid, right):

    # Stores the count of swaps
    swaps = 0

    i, j, k = left, mid, left

    while (i < mid and j <= right):

        if (A[i] <= A[j]):
            temp[k] = A[i]
            k, i = k + 1, i + 1
        else:
            temp[k] = A[j]
            k, j = k + 1, j + 1
            swaps += mid - i

    while (i < mid):
        temp[k] = A[i]
        k, i = k + 1, i + 1

    while (j <= right):
        temp[k] = A[j]
        k, j = k + 1, j + 1

    while (left <= right):
        A[left] = temp[left]
        left += 1

    return swaps

# Function to count the total number
# of swaps required to sort the array
def mergeInsertionSwap(A, left, right):

    # Stores the total count
    # of swaps required
    swaps = 0

    if (left < right):

        # Find the middle index
        # splitting the two halves
        mid = left + (right - left) // 2

        # Count the number of swaps
        # required to sort the left subarray
        swaps += mergeInsertionSwap(A, left, mid)

        # Count the number of swaps
        # required to sort the right subarray
        swaps += mergeInsertionSwap(A, mid + 1, right)

        # Count the number of swaps required
        # to sort the two sorted subarrays
        swaps += merge(A, left, mid + 1, right)

    return swaps

# Driver Code
if __name__ == '__main__':

    A = [ 2, 1, 3, 1, 2 ]
    N = len(A)

    print (mergeInsertionSwap(A, 0, N - 1))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

 // Stores the sorted
  // array elements
  static int[] temp = new int[100000];

  // Function to count the number of
  // swaps required to merge two sorted
  // subarray in a sorted form
  static int merge(int[] A, int left,
                   int mid, int right)
  {

    // Stores the count of swaps
    int swaps = 0;
    int i = left, j = mid, k = left;
    while (i < mid && j <= right)
    {
      if (A[i] <= A[j])
      {
        temp[k] = A[i];
        k++; i++;
      }
      else
      {
        temp[k] = A[j];
        k++; j++;
        swaps += mid - i;
      }
    }
    while (i < mid)
    {
      temp[k] = A[i];
      k++; i++;
    }

    while (j <= right)
    {
      temp[k] = A[j];
      k++; j++;
    }

    while (left <= right)
    {
      A[left] = temp[left];
      left++;
    }
    return swaps;
  }

  // Function to count the total number
  // of swaps required to sort the array
  static int mergeInsertionSwap(int[] A,
                                int left, int right)
  {

    // Stores the total count
    // of swaps required
    int swaps = 0;
    if (left < right)
    {

      // Find the middle index
      // splitting the two halves
      int mid = left + (right - left) / 2;

      // Count the number of swaps
      // required to sort the left subarray
      swaps += mergeInsertionSwap(A, left, mid);

      // Count the number of swaps
      // required to sort the right subarray
      swaps += mergeInsertionSwap(A, mid + 1, right);

      // Count the number of swaps required
      // to sort the two sorted subarrays
      swaps += merge(A, left, mid + 1, right);
    }
    return swaps;
  }

  // Driver Code
  static public void Main()
  {
    int[] A = { 2, 1, 3, 1, 2 };
    int N = A.Length;
    Console.WriteLine(mergeInsertionSwap(A, 0, N - 1));
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
// javascript program of the above approach

  // Stores the sorted
  // array elements
  let temp = new Array(100000).fill(0);

  // Function to count the number of
  // swaps required to merge two sorted
  // subarray in a sorted form
  function merge(A, left,
                    mid, right)
  {

    // Stores the count of swaps
    let swaps = 0;
    let i = left, j = mid, k = left;
    while (i < mid && j <= right)
    {
      if (A[i] <= A[j])
      {
        temp[k] = A[i];
        k++; i++;
      }
      else
      {
        temp[k] = A[j];
        k++; j++;
        swaps += mid - i;
      }
    }
    while (i < mid)
    {
      temp[k] = A[i];
      k++; i++;
    }

    while (j <= right)
    {
      temp[k] = A[j];
      k++; j++;
    }

    while (left <= right)
    {
      A[left] = temp[left];
      left++;
    }
    return swaps;
  }

  // Function to count the total number
  // of swaps required to sort the array
  function mergeInsertionSwap(A, left, right)
  {
    // Stores the total count
    // of swaps required
    let swaps = 0;
    if (left < right)
    {

      // Find the middle index
      // splitting the two halves
      let mid = left + (right - left) / 2;

      // Count the number of swaps
      // required to sort the left subarray
      swaps += mergeInsertionSwap(A, left, mid);

      // Count the number of swaps
      // required to sort the right subarray
      swaps += mergeInsertionSwap(A, mid + 1, right);

      // Count the number of swaps required
      // to sort the two sorted subarrays
      swaps += merge(A, left, mid + 1, right);
    }
    return swaps;
  }

    // Driver Code

        let A = [ 2, 1, 3, 1, 2 ];
    let N = A.length;
    document.write(mergeInsertionSwap(A, 0, N - 1));

// This code is contributed by target_2.
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*