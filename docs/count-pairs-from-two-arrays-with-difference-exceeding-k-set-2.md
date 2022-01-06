# 从两个差值超过 K 的数组中计数对|集合 2

> 原文:[https://www . geesforgeks . org/count-pairs-from-two-array-with-exclusive-k-set-2/](https://www.geeksforgeeks.org/count-pairs-from-two-arrays-with-difference-exceeding-k-set-2/)

给定两个整数数组**arr【】**和**brr【】**，分别由大小不同的元素 **N** 和 **M** 和一个整数 **K** 组成，任务是找到对的计数 **(arr[i]** ， **brr[j])** ，使得**(brr[j]–arr[I])>K .**

**示例:**

> **输入:** arr[] = {5，9，1，8}，brr[] = {10，12，7，4，2，3}，K = 3
> **输出:** 6
> **说明:**
> 满足给定条件的可能对有:{(5，10)，(5，12)，(1，10)，(1，12)，(1，7)，(8，12)}。
> 因此，要求输出为 6。
> 
> **输入:** arr[] = {2，10}，brr[] = {5，7}，K = 2
> **输出:** 2
> **解释:**
> 满足给定条件的可能对为:{(2，5)，(2，7)}。
> 因此，要求的输出为 2。

**天真的做法:**参考本文[之前的帖子](https://www.geeksforgeeks.org/count-pairs-from-two-arrays-with-difference-exceeding-k/)了解解决这个问题最简单的方法。
***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*

[**两个指针**](https://www.geeksforgeeks.org/two-pointers-technique/) **进场:**关于这个问题的[两个指针](https://www.geeksforgeeks.org/tag/two-pointer-algorithm/)解决方案，请参考本文[之前的帖子](https://www.geeksforgeeks.org/count-pairs-from-two-arrays-with-difference-exceeding-k/)。
***时间复杂度:**O(N * log(N)+M * log(M))*
***辅助空间:** O(1)*

**高效方法:**思路是[排序](https://www.geeksforgeeks.org/sort-c-stl/)小数组，[遍历大数组](https://www.geeksforgeeks.org/iterating-arrays-java/)对于每个元素，使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)在小数组中找到合适的元素进行配对。按照以下步骤解决问题:

*   初始化一个变量**计数**来存储对的计数。
*   如果 **arr[]** 尺寸小于 **brr[]** ，则执行以下操作。
    *   [排序阵](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **arr[]** 和[遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **brr[]。**
    *   在**arr【】**中找到**(brr[j]–k)**的[下界](https://www.geeksforgeeks.org/lower_bound-in-cpp/)，因为在 arr【】中小于**brr[j]–k 的数字将与 **brr[j]完美配对。****
    *   将**下限指数**与计数相加。
*   如果 **brr[]** 尺寸小于 **arr[]** ，则执行以下操作。
    *   对数组 **brr[]** 进行排序，遍历 **arr[]** 。
    *   求**brr【】**中 **(arr[i] + k)** 的[上限，因为**brr【】**中大于 **arr[i]+k** 的数字将与 **arr[i]完美配对。**](https://www.geeksforgeeks.org/set-upper_bound-function-in-c-stl/)
    *   将**(brr[]的大小–上限索引)**与计数相加。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count pairs that satisfy
// the given conditions
int countPairs(int v1[], int v2[],
               int n, int m, int k)
{
    // Stores the count of pairs
    int count = 0;

    // If v1[] is smaller than v2[]
    if (n <= m) {

        // Sort the array v1[]
        sort(v1, v1 + n);

        // Traverse the array v2[]
        for (int j = 0; j < m; j++) {

            // Returns the address of
            // the first number which
            // is >= v2[j] - k
            int index
                = lower_bound(v1, v1 + n,
                              v2[j] - k)
                  - v1;

            // Increase the count by all
            // numbers less than v2[j] - k
            count += index;
        }
    }

    // Otherwise
    else {

        // Sort the array v2[]
        sort(v2, v2 + m);

        // Traverse the array v1[]
        for (int i = 0; i < n; i++) {

            // Returns the address of
            // the first number which
            // is > v1[i] + k
            int index
                = upper_bound(v2, v2 + m,
                              v1[i] + k)
                  - v2;

            // Increase the count by all
            // numbers greater than v1[i] + k
            count += m - index;
        }
    }

    // Return the total count of pairs
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 5, 9, 1, 8 };
    int brr[] = { 10, 12, 7, 4, 2, 3 };

    int K = 3;

    int N = sizeof(arr)
            / sizeof(arr[0]);

    int M = sizeof(brr)
            / sizeof(brr[0]);

    cout << countPairs(arr, brr,
                       N, M, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to count pairs
// that satisfy the given
// conditions
static int countPairs(int v1[], int v2[],
                      int n, int m, int k)
{
  // Stores the count of pairs
  int count = 0;

  // If v1[] is smaller than v2[]
  if (n <= m)
  {
    // Sort the array v1[]
    Arrays.sort(v1);

    // Traverse the array v2[]
    for (int j = 0; j < m; j++)
    {
      // Returns the address of
      // the first number which
      // is >= v2[j] - k
      int index = lowerBound(v1, 0, n,
                             v2[j] - k);

      // Increase the count by all
      // numbers less than v2[j] - k
      count += index;
    }
  }

  // Otherwise
  else
  {
    // Sort the array v2[]
    Arrays.sort(v2);

    // Traverse the array v1[]
    for (int i = 0; i < n; i++)
    {
      // Returns the address of
      // the first number which
      // is > v1[i] + k
      int index = upperBound(v2, 0, m,
                             v1[i] + k);

      // Increase the count by all
      // numbers greater than v1[i] + k
      count += m - index;
    }
  }

  // Return the total count of pairs
  return count;
}

static int lowerBound(int[] a, int low,
                      int high, int element)
{
  while(low < high)
  {
    int middle = low +
                 (high - low) / 2;

    if(element > a[middle])
      low = middle + 1;
    else
      high = middle;
  }
  return low;
}

static int upperBound(int[] a, int low,
                      int high, int element)
{
  while(low < high)
  {
    int middle = low +
                 (high - low) / 2;

    if(a[middle] > element)
      high = middle;
    else
      low = middle + 1;
  }
  return low;
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {5, 9, 1, 8};
  int brr[] = {10, 12, 7,
               4, 2, 3};
  int K = 3;
  int N = arr.length;
  int M = brr.length;
  System.out.print(countPairs(arr, brr,
                              N, M, K));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach
from bisect import bisect_left, bisect_right

# Function to count pairs that satisfy
# the given conditions
def countPairs(v1, v2, n, m, k):

    # Stores the count of pairs
    count = 0

    # If v1[] is smaller than v2[]
    if (n <= m):

        # Sort the array v1[]
        v1 = sorted(v1)

        # Traverse the array v2[]
        for j in range(m):

            # Returns the address of
            # the first number which
            # is >= v2[j] - k
            index = bisect_left(v1, v2[j] - k)

            # Increase the count by all
            # numbers less than v2[j] - k
            count += index

    # Otherwise
    else:

        # Sort the array v2[]
        v2 = sorted(v2)

        # Traverse the array v1[]
        for i in range(n):

            # Returns the address of
            # the first number which
            # is > v1[i] + k
            index = bisect_right(v2, v1[i] + k)

            # Increase the count by all
            # numbers greater than v1[i] + k
            count += m - index

    # Return the total count of pairs
    return count

# Driver Code
if __name__ == '__main__':

    arr = [ 5, 9, 1, 8 ]
    brr = [ 10, 12, 7, 4, 2, 3]

    K = 3

    N = len(arr)
    M = len(brr)

    print(countPairs(arr, brr, N, M, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to count pairs
// that satisfy the given
// conditions
static int countPairs(int []v1, int []v2,
                      int n, int m, int k)
{
  // Stores the count of pairs
  int count = 0;

  // If v1[] is smaller than v2[]
  if (n <= m)
  {
    // Sort the array v1[]
    Array.Sort(v1);

    // Traverse the array v2[]
    for (int j = 0; j < m; j++)
    {
      // Returns the address of
      // the first number which
      // is >= v2[j] - k
      int index = lowerBound(v1, 0, n,
                             v2[j] - k);

      // Increase the count by all
      // numbers less than v2[j] - k
      count += index;
    }
  }

  // Otherwise
  else
  {
    // Sort the array v2[]
    Array.Sort(v2);

    // Traverse the array v1[]
    for (int i = 0; i < n; i++)
    {
      // Returns the address of
      // the first number which
      // is > v1[i] + k
      int index = upperBound(v2, 0, m,
                             v1[i] + k);

      // Increase the count by all
      // numbers greater than v1[i] + k
      count += m - index;
    }
  }

  // Return the total count
  // of pairs
  return count;
}

static int lowerBound(int[] a, int low,
                      int high, int element)
{
  while(low < high)
  {
    int middle = low +
                 (high - low) / 2;

    if(element > a[middle])
      low = middle + 1;
    else
      high = middle;
  }
  return low;
}

static int upperBound(int[] a, int low,
                      int high, int element)
{
  while(low < high)
  {
    int middle = low +
                 (high - low) / 2;

    if(a[middle] > element)
      high = middle;
    else
      low = middle + 1;
  }
  return low;
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {5, 9, 1, 8};
  int []brr = {10, 12, 7,
               4, 2, 3};
  int K = 3;
  int N = arr.Length;
  int M = brr.Length;
  Console.Write(countPairs(arr, brr,
                              N, M, K));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to count pairs
// that satisfy the given
// conditions
function countPairs(v1, v2, n, m, k)
{
  // Stores the count of pairs
  let count = 0;

  // If v1[] is smaller than v2[]
  if (n <= m)
  {
    // Sort the array v1[]
    v1.sort();

    // Traverse the array v2[]
    for (let j = 0; j < m; j++)
    {
      // Returns the address of
      // the first number which
      // is >= v2[j] - k
      let index = lowerBound(v1, 0, n,
                             v2[j] - k);

      // Increase the count by all
      // numbers less than v2[j] - k
      count += index;
    }
  }

  // Otherwise
  else
  {
    // Sort the array v2[]
    v2.sort();

    // Traverse the array v1[]
    for (let i = 0; i < n; i++)
    {
      // Returns the address of
      // the first number which
      // is > v1[i] + k
      let index = upperBound(v2, 0, m,
                             v1[i] + k);

      // Increase the count by all
      // numbers greater than v1[i] + k
      count += m - index;
    }
  }

  // Return the total count of pairs
  return count;
}

function lowerBound(a, low,
                      high, element)
{
  while(low < high)
  {
    let middle = low +
                 (high - low) / 2;

    if(element > a[middle])
      low = middle + 1;
    else
      high = middle;
  }
  return low;
}

function upperBound(a, low,
                   high, element)
{
  while(low < high)
  {
    let middle = low +
                 (high - low) / 2;

    if(a[middle] > element)
      high = middle;
    else
      low = middle + 1;
  }
  return low;
}

// Driver Code

    let arr = [5, 9, 1, 8];
    let brr = [10, 12, 7,
               4, 2, 3];
  let K = 3;
  let N = arr.length;
  let M = brr.length;
  document.write(countPairs(arr, brr,
                              N, M, K));

</script>
```

**Output:** 

```
6
```

***时间复杂度:** O((N+M) * min(log(N)，log(M))*
***辅助空间:** O(1)*