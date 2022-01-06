# 使用快速排序分区

合并 O(1)个额外空间中的两个排序数组

> 原文:[https://www . geesforgeks . org/merge-two-sorted-arrays-in-O1-extra-space-use-quick sort-partition/](https://www.geeksforgeeks.org/merge-two-sorted-arrays-in-o1-extra-space-using-quicksort-partition/)

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

[**分区**](https://www.geeksforgeeks.org/hoares-vs-lomuto-partition-scheme-quicksort/)**–基于方法:**思路是将最终排序数组的 **(N + 1) <sup>第</sup>** 元素作为一个枢轴元素，围绕枢轴元素进行[快速排序分区](https://www.geeksforgeeks.org/quick-sort/)。最后，将最终排序数组的第一个 **N** 小元素存储到数组中， **arr[]** 最后一个 **M** 大元素以任意顺序存储到数组中， **brr[]** 分别对这两个数组进行排序。按照以下步骤解决问题:

1.  初始化一个变量，比如说**索引**来存储最终排序数组的每个元素的索引。
2.  找到最终排序数组的 **(N + 1) <sup>第</sup>** 元素作为枢纽元素。
3.  围绕枢轴元素执行[快速分类分区](https://www.geeksforgeeks.org/quick-sort/)。
4.  最后，分别对数组 **arr[]** 和 **brr[]** 进行排序。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform the partition
// around the pivot element
void partition(int arr[], int N,
               int brr[], int M,
               int Pivot)
{
    // Stores index of each element
    // of the array, arr[]
    int l = N - 1;

    // Stores index of each element
    // of the array, brr[]
    int r = 0;

    // Traverse both the array
    while (l >= 0 && r < M) {

        // If pivot is
        // smaller than arr[l]
        if (arr[l] < Pivot)
            l--;

        // If Pivot is
        // greater than brr[r]
        else if (brr[r] > Pivot)
            r++;

        // If either arr[l] > Pivot
        // or brr[r] < Pivot
        else {
            swap(arr[l], brr[r]);
            l--;
            r++;
        }
    }
}

// Function to merge
// the two sorted array
void Merge(int arr[], int N,
           int brr[], int M)
{
    // Stores index of each element
    // of the array arr[]
    int l = 0;

    // Stores index of each element
    // of the array brr[]
    int r = 0;

    // Stores index of each element
    // the final sorted array
    int index = -1;

    // Stores the pivot element
    int Pivot = 0;

    // Traverse both the array
    while (index < N && l < N && r < M) {

        if (arr[l] < brr[r]) {
            Pivot = arr[l++];
        }
        else {
            Pivot = brr[r++];
        }
        index++;
    }

    // If pivot element is not found
    // or index < N
    while (index < N && l < N) {
        Pivot = arr[l++];
        index++;
    }

    // If pivot element is not found
    // or index < N
    while (index < N && r < M) {
        Pivot = brr[r++];
        index++;
    }

    // Place the first N elements of
    // the sorted array into arr[]
    // and the last M elements of
    // the sorted array into brr[]
    partition(arr, N, brr,
              M, Pivot);

    // Sort both the arrays
    sort(arr, arr + N);

    sort(brr, brr + M);

    // Print the first N elements
    // in sorted order
    for (int i = 0; i < N; i++)
        cout << arr[i] << " ";

    // Print the last M elements
    // in sorted order
    for (int i = 0; i < M; i++)
        cout << brr[i] << " ";
}

// Driver Code
int main()
{
    int arr[] = { 1, 5, 9 };
    int brr[] = { 2, 4, 7, 10 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = sizeof(brr) / sizeof(brr[0]);
    Merge(arr, N, brr, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to perform the partition
// around the pivot element
static void partition(int arr[], int N,
                      int brr[], int M,
                      int Pivot)
{
  // Stores index of each element
  // of the array, arr[]
  int l = N - 1;

  // Stores index of each element
  // of the array, brr[]
  int r = 0;

  // Traverse both the array
  while (l >= 0 && r < M)
  {
    // If pivot is
    // smaller than arr[l]
    if (arr[l] < Pivot)
      l--;

    // If Pivot is
    // greater than brr[r]
    else if (brr[r] > Pivot)
      r++;

    // If either arr[l] > Pivot
    // or brr[r] < Pivot
    else
    {
      int t = arr[l];
      arr[l] = brr[r];
      brr[r] = t;
      l--;
      r++;
    }
  }
}

// Function to merge
// the two sorted array
static void Merge(int arr[], int N,
                  int brr[], int M)
{
  // Stores index of each element
  // of the array arr[]
  int l = 0;

  // Stores index of each element
  // of the array brr[]
  int r = 0;

  // Stores index of each element
  // the final sorted array
  int index = -1;

  // Stores the pivot element
  int Pivot = 0;

  // Traverse both the array
  while (index < N && l < N &&
         r < M)
  {
    if (arr[l] < brr[r])
    {
      Pivot = arr[l++];
    }
    else
    {
      Pivot = brr[r++];
    }
    index++;
  }

  // If pivot element is not found
  // or index < N
  while (index < N && l < N)
  {
    Pivot = arr[l++];
    index++;
  }

  // If pivot element is not
  // found or index < N
  while (index < N && r < M)
  {
    Pivot = brr[r++];
    index++;
  }

  // Place the first N elements of
  // the sorted array into arr[]
  // and the last M elements of
  // the sorted array into brr[]
  partition(arr, N, brr,
            M, Pivot);

  // Sort both the arrays
  Arrays.sort(arr);

  Arrays.sort(brr);

  // Print the first N elements
  // in sorted order
  for (int i = 0; i < N; i++)
    System.out.print(arr[i] + " ");

  // Print the last M elements
  // in sorted order
  for (int i = 0; i < M; i++)
    System.out.print(brr[i] + " ");
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {1, 5, 9};
  int brr[] = {2, 4, 7, 10};
  int N = arr.length;
  int M = brr.length;
  Merge(arr, N, brr, M);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to perform the partition
# around the pivot element
def partition(arr, N, brr, M, Pivot):

    # Stores index of each element
    # of the array, arr[]
    l = N - 1

    # Stores index of each element
    # of the array, brr[]
    r = 0

    # Traverse both the array
    while (l >= 0 and r < M):

        # If pivot is smaller
        # than arr[l]
        if (arr[l] < Pivot):
            l -= 1

        # If Pivot is greater
        # than brr[r]
        elif (brr[r] > Pivot):
            r += 1

        # If either arr[l] > Pivot
        # or brr[r] < Pivot
        else:
            arr[l], brr[r] = brr[r], arr[l]
            l -= 1
            r += 1

# Function to merge
# the two sorted array
def Merge(arr, N, brr, M):

    # Stores index of each element
    # of the array arr[]
    l = 0

    # Stores index of each element
    # of the array brr[]
    r = 0

    # Stores index of each element
    # the final sorted array
    index = -1

    # Stores the pivot element
    Pivot = 0

    # Traverse both the array
    while (index < N and l < N and r < M):
        if (arr[l] < brr[r]):
            Pivot = arr[l]
            l += 1
        else:
            Pivot = brr[r]
            r += 1

        index += 1

    # If pivot element is not found
    # or index < N
    while (index < N and l < N):
        Pivot = arr[l]
        l += 1
        index += 1

    # If pivot element is not found
    # or index < N
    while (index < N and r < M):
        Pivot = brr[r]
        r += 1
        index += 1

    # Place the first N elements of
    # the sorted array into arr[]
    # and the last M elements of
    # the sorted array into brr[]
    partition(arr, N, brr, M, Pivot)

    # Sort both the arrays
    arr = sorted(arr)

    brr = sorted(brr)

    # Print the first N elements
    # in sorted order
    for i in range(N):
        print(arr[i], end = " ")

    # Print the last M elements
    # in sorted order
    for i in range(M):
        print(brr[i], end = " ")

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 5, 9 ]
    brr = [ 2, 4, 7, 10 ]
    N = len(arr)
    M = len(brr)

    Merge(arr, N, brr, M)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to perform the
// partition around the pivot
// element
static void partition(int []arr, int N,
                      int []brr, int M,
                      int Pivot)
{
  // Stores index of each element
  // of the array, []arr
  int l = N - 1;

  // Stores index of each element
  // of the array, brr[]
  int r = 0;

  // Traverse both the array
  while (l >= 0 && r < M)
  {
    // If pivot is
    // smaller than arr[l]
    if (arr[l] < Pivot)
      l--;

    // If Pivot is
    // greater than brr[r]
    else if (brr[r] > Pivot)
      r++;

    // If either arr[l] > Pivot
    // or brr[r] < Pivot
    else
    {
      int t = arr[l];
      arr[l] = brr[r];
      brr[r] = t;
      l--;
      r++;
    }
  }
}

// Function to merge
// the two sorted array
static void Merge(int []arr, int N,
                  int []brr, int M)
{
  // Stores index of each element
  // of the array []arr
  int l = 0;

  // Stores index of each element
  // of the array brr[]
  int r = 0;

  // Stores index of each element
  // the readonly sorted array
  int index = -1;

  // Stores the pivot element
  int Pivot = 0;

  // Traverse both the array
  while (index < N && l < N &&
         r < M)
  {
    if (arr[l] < brr[r])
    {
      Pivot = arr[l++];
    }
    else
    {
      Pivot = brr[r++];
    }
    index++;
  }

  // If pivot element is not found
  // or index < N
  while (index < N && l < N)
  {
    Pivot = arr[l++];
    index++;
  }

  // If pivot element is not
  // found or index < N
  while (index < N && r < M)
  {
    Pivot = brr[r++];
    index++;
  }

  // Place the first N elements of
  // the sorted array into []arr
  // and the last M elements of
  // the sorted array into brr[]
  partition(arr, N, brr,
            M, Pivot);

  // Sort both the arrays
    Array.Sort(arr);
    Array.Sort(brr);

  // Print the first N elements
  // in sorted order
  for (int i = 0; i < N; i++)
    Console.Write(arr[i] + " ");

  // Print the last M elements
  // in sorted order
  for (int i = 0; i < M; i++)
    Console.Write(brr[i] + " ");
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {1, 5, 9};
  int []brr= {2, 4, 7, 10};
  int N = arr.Length;
  int M = brr.Length;
  Merge(arr, N, brr, M);
}
}

// This code is contributed by shikhasingrajput
```

**Output**

```
1 2 4 5 7 9 10 
```

***时间复杂度:**O((N+M)log(N+M))*
***辅助空间:** O(1)*

**有效方法:**参考[合并两个排序的数组](https://www.geeksforgeeks.org/merge-two-sorted-arrays/)来有效合并两个给定的数组。
***时间复杂度:** O(N + M)*
***辅助空间:** O(N + M)*