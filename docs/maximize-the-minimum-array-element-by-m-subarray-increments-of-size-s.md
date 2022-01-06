# 通过大小为 S 的 M 个子阵列增量最大化最小阵列元素

> 原文:[https://www . geeksforgeeks . org/最大化最小数组元素乘 m 子数组大小增量 s/](https://www.geeksforgeeks.org/maximize-the-minimum-array-element-by-m-subarray-increments-of-size-s/)

给定一个由 **N** 个整数和两个整数 **S** 和 **M** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是通过将大小为 **S** 的任意[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)递增 **1** 、 **M** 次来最大化[最小数组元素](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)。

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6}，S = 2，M = 3
> **输出:** 3
> **解释:**
> 下面是执行的操作:
> **操作 1:** 选择子阵列{1，2}，递增后，arr[]变为= {2，3，4，5，6}。
> **操作 2:** 选择子阵列{2，3}，递增后，arr[]变为= {3，4，3，4，5，6}。
> **操作 3:** 选择子阵列{3，4}，递增后，arr[]变为= {4，5，3，4，5，6}。
> 经过以上操作，数组的最小元素为 3。
> 
> **输入:** arr[] = {3，5，2，7，3}，S = 3，M = 3
> **输出:** 4
> **解释:**
> 下面是执行的操作:
> **操作 1:** 选择子阵列{3，5，2}，递增后，arr[]变为= {4，6，3，7，3}。
> **操作 2:** 选择子阵列{4，6，3}，递增后，arr[]变成= {5，7，4，7，3}。
> **操作 3:** 选择子阵列{4，7，3}，递增后，arr[]变成= {5，7，5，8，4}。
> 经过以上操作，数组的最小元素为 4。

**方法:**思路是[找到数组的最小元素](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/) **M** 次，将大小为 **S** 的子数组从该最小元素增加 **1** 。按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **M** 的次数，每次迭代执行以下操作:
    *   [找到数组的最小元素](https://www.geeksforgeeks.org/maximum-and-minimum-in-an-array/) **arr[]** 。让最小元素的第一个指标为 **idx** 。
    *   将当前最小元素增加 **1** 。
    *   现在取两个指针**左 dx** 为**idx–1**和**右 dx** 为 **idx + 1** 。
    *   如果**left dx**处的元素少于**right dx**处的元素，则增加**A【left ndex】1**并减少**left ndex 1**。否则，将 **A【右索引】增加 1** ，**右索引增加 1** 。继续此步骤，直到处理完**(S–1)**元素。
*   在上述迭代之后，打印更新的数组的最小元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return index of minimum
// element in the array
int min(int a[], int n)
{
    // Initialize a[0] as minValue
    int minIndex = 0, minValue = a[0], i;

    // Traverse the array
    for (i = 1; i < n; i++) {

        // If a[i] < existing minValue
        if (a[i] < minValue) {
            minValue = a[i];
            minIndex = i;
        }
    }

    // Return the minimum index
    return minIndex;
}

// Function that maximize the minimum
// element of array after incrementing
// subarray of size S by 1, M times
int maximizeMin(int A[], int N,
                int S, int M)
{
    int minIndex, left, right, i, j;

    // Iterating through the array
    // for M times
    for (i = 0; i < M; i++) {

        // Find minimum element index
        minIndex = min(A, N);

        // Increment the minimum value
        A[minIndex]++;

        // Storing the left index
        // and right index
        left = minIndex - 1;
        right = minIndex + 1;

        // Incrementing S - 1 minimum
        // elements to the left and
        // right of minValue
        for (j = 0; j < S - 1; j++) {

            // Reached extreme left
            if (left == -1)
                A[right++]++;

            // Reached extreme right
            else if (right == N)
                A[left--]++;

            else {

                // Left value is minimum
                if (A[left] < A[right])
                    A[left--]++;

                // Right value is minimum
                else
                    A[right++]++;
            }
        }
    }

    // Find the minValue in A[] after
    // M operations
    minIndex = min(A, N);

    // Return the minimum value
    return A[minIndex];
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int S = 2, M = 3;

    // Function Call
    cout << maximizeMin(arr, N, S, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class solution{

// Function to return index
// of minimum element in the
// array
static int min1(int a[], int n)
{
  // Initialize a[0] as
  // minValue
  int minIndex = 0,
      minValue = a[0], i;

  // Traverse the array
  for (i = 1; i < n; i++)
  {
    // If a[i] < existing
    // minValue
    if (a[i] < minValue)
    {
      minValue = a[i];
      minIndex = i;
    }
  }

  // Return the minimum index
  return minIndex;
}

// Function that maximize the minimum
// element of array after incrementing
// subarray of size S by 1, M times
static int maximizeMin(int A[], int N,
                       int S, int M)
{
  int minIndex, left, right, i, j;

  // Iterating through the
  // array or M times
  for (i = 0; i < M; i++)
  {
    // Find minimum element
    // index
    minIndex = min1(A, N);

    // Increment the minimum
    // value
    A[minIndex]++;

    // Storing the left index
    // and right index
    left = minIndex - 1;
    right = minIndex + 1;

    // Incrementing S - 1 minimum
    // elements to the left and
    // right of minValue
    for (j = 0; j < S - 1; j++)
    {
      // Reached extreme left
      if (left == -1)
        A[right++]++;

      // Reached extreme right
      else if (right == N)
        A[left--]++;

      else
      {
        // Left value is minimum
        if (A[left] < A[right])
          A[left--]++;

        // Right value is minimum
        else
          A[right++]++;
      }
    }
  }

  // Find the minValue in A[] after
  // M operations
  minIndex = min1(A, N);

  // Return the minimum value
  return A[minIndex];
}

// Driver Code
public static void main(String args[])
{
  int []arr = {1, 2, 3,
               4, 5, 6};
  int N = arr.length;
  int S = 2, M = 3;

  // Function Call
  System.out.print(maximizeMin(arr, N, S, M));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return index of minimum
# element in the array
def min(a, n):

    # Initialize a[0] as minValue
    minIndex = 0
    minValue = a[0]

    # Traverse the array
    for i in range(1, n):

        # If a[i] < existing minValue
        if (a[i] < minValue):
            minValue = a[i]
            minIndex = i

    # Return the minimum index
    return minIndex

# Function that maximize the minimum
# element of array after incrementing
# subarray of size S by 1, M times
def maximizeMin(A, N, S, M):

    minIndex, left, right = 0, 0, 0

    # Iterating through the array
    # for M times
    for i in range(M):

        # Find minimum element index
        minIndex = min(A, N)

        # Increment the minimum value
        A[minIndex] += 1

        # Storing the left index
        # and right index
        left = minIndex - 1
        right = minIndex + 1

        # Incrementing S - 1 minimum
        # elements to the left and
        # right of minValue
        for j in range(S - 1):

            # Reached extreme left
            if (left == -1):
                A[right] += 1
                right += 1

            # Reached extreme right
            elif (right == N):
                A[left] += 1
                left -= 1

            else:

                # Left value is minimum
                if (A[left] < A[right]):
                    A[left] += 1
                    left -= 1

                # Right value is minimum
                else:
                    A[right] += 1
                    right += 1

    # Find the minValue in A[] after
    # M operations
    minIndex = min(A, N)

    # Return the minimum value
    return A[minIndex]

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 4, 5, 6 ]
    N = len(arr)
    S = 2
    M = 3

    #Function Call
    print(maximizeMin(arr, N, S, M))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to return index
// of minimum element in the
// array
static int min1(int[] a,
                int n)
{
  // Initialize a[0] as
  // minValue
  int minIndex = 0,
      minValue = a[0], i;

  // Traverse the array
  for (i = 1; i < n; i++)
  {
    // If a[i] < existing
    // minValue
    if (a[i] < minValue)
    {
      minValue = a[i];
      minIndex = i;
    }
  }

  // Return the minimum
  // index
  return minIndex;
}

// Function that maximize the
// minimum element of array
// after incrementing subarray
// of size S by 1, M times
static int maximizeMin(int[] A, int N,
                       int S, int M)
{
  int minIndex, left, right, i, j;

  // Iterating through the
  // array or M times
  for (i = 0; i < M; i++)
  {
    // Find minimum element
    // index
    minIndex = min1(A, N);

    // Increment the minimum
    // value
    A[minIndex]++;

    // Storing the left index
    // and right index
    left = minIndex - 1;
    right = minIndex + 1;

    // Incrementing S - 1 minimum
    // elements to the left and
    // right of minValue
    for (j = 0; j < S - 1; j++)
    {
      // Reached extreme left
      if (left == -1)
        A[right++]++;

      // Reached extreme right
      else if (right == N)
        A[left--]++;

      else
      {
        // Left value is minimum
        if (A[left] < A[right])
          A[left--]++;

        // Right value is minimum
        else
          A[right++]++;
      }
    }
  }

  // Find the minValue in A[] after
  // M operations
  minIndex = min1(A, N);

  // Return the minimum value
  return A[minIndex];
}

// Driver code
static void Main()
{
  int[] arr = {1, 2, 3,
               4, 5, 6};
  int N = arr.Length;
  int S = 2, M = 3;

  // Function Call
  Console.Write(maximizeMin(arr, N,
                            S, M));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to return index
// of minimum element in the
// array
function min1(a, n)
{
  // Initialize a[0] as
  // minValue
  let minIndex = 0,
      minValue = a[0], i;

  // Traverse the array
  for (i = 1; i < n; i++)
  {
    // If a[i] < existing
    // minValue
    if (a[i] < minValue)
    {
      minValue = a[i];
      minIndex = i;
    }
  }

  // Return the minimum index
  return minIndex;
}

// Function that maximize the minimum
// element of array after incrementing
// subarray of size S by 1, M times
function maximizeMin(A, N, S, M)
{
  let minIndex, left, right, i, j;

  // Iterating through the
  // array or M times
  for (i = 0; i < M; i++)
  {
    // Find minimum element
    // index
    minIndex = min1(A, N);

    // Increment the minimum
    // value
    A[minIndex]++;

    // Storing the left index
    // and right index
    left = minIndex - 1;
    right = minIndex + 1;

    // Incrementing S - 1 minimum
    // elements to the left and
    // right of minValue
    for (j = 0; j < S - 1; j++)
    {
      // Reached extreme left
      if (left == -1)
        A[right++]++;

      // Reached extreme right
      else if (right == N)
        A[left--]++;

      else
      {
        // Left value is minimum
        if (A[left] < A[right])
          A[left--]++;

        // Right value is minimum
        else
          A[right++]++;
      }
    }
  }

  // Find the minValue in A[] after
  // M operations
  minIndex = min1(A, N);

  // Return the minimum value
  return A[minIndex];
}

// Driver Code

    let arr = [1, 2, 3,
               4, 5, 6];
  let N = arr.length;
  let S = 2, M = 3;

  // Function Call
  document.write(maximizeMin(arr, N, S, M));

</script>
```

**Output:** 

```
3
```

**时间复杂度:***O(M * N)*
T5】辅助空间: *O(1)*