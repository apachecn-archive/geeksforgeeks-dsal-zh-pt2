# 前缀和数组元素交替符号所需的最小增量或减量

> 原文:[https://www . geeksforgeeks . org/最小增量-或-减量-前缀-总和-数组-元素-交替符号/](https://www.geeksforgeeks.org/minimum-increments-or-decrements-required-to-signs-of-prefix-sum-array-elements-alternating/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过 **1** 找到数组元素的最小增量/减量数，使数组的[前缀和的符号交替出现。](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)

**示例:**

> **输入:** arr[] = {1，-3，1，0}
> **输出:** 4
> **解释:**
> 以下是对给定数组元素执行的操作:
> 
> 1.  将数组元素 arr[1](= -3)递增 1 会将数组修改为{1，-2，1，0}。
> 2.  将数组元素 arr[2](= 1)递增 1 会将数组修改为{1，-2，2，0}。
> 3.  将数组元素 arr[3](= 0)减 1 会将数组修改为{1，-2，2，-1}。
> 4.  将数组元素 arr[3](= -1)减 1 会将数组修改为{1，-2，2，-2}。
> 
> 经过以上运算，修改后数组的前缀和为{1，-1，1，-1}，符号顺序交替。因此，所需的最小操作数是 4。
> 
> **输入:** arr[] = {3，-6，4，-5，7}
> **输出:** 0

**方法:**给定的问题可以通过使用给定的操作以两种顺序修改数组元素来解决，即**正、负、正、…** 或**负、正、负、…、**并打印所需的两个操作中的最小值。按照以下步骤解决给定的问题:

*   对于情况 1:按照**负、正、负:**的顺序修改数组元素
    1.  初始化变量 **current_prefix_1** 为 **0** ，存储数组的前缀和。
    2.  初始化变量**小操作案例 1** 为 **0** ，存储所需的最小操作数。
    3.  [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下步骤:
        *   将 **current_prefix_1** 增加**arr【I】**。
        *   如果 **current_prefix_1** 或奇偶校验的值为-ve，则通过 **abs(奇偶校验–current _ prefix _ 1)**增加最小操作次数。
        *   将奇偶性乘以 **(-1)** 。
*   类似地，如案例 1 中所讨论的，找到前缀和的顺序所需的最小操作数**正、负、正、…** ，并将其存储在变量**小操作案例 2** 中。
*   完成上述步骤后，打印最小的**次操作案例 1** 和**次操作案例 2** 作为所需的结果操作。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of increments/decrements of array
// elements by 1 to make signs of
// prefix sum array elements alternating
int minimumOperations(int A[], int N)
{
    // Case 1\. neg - pos - neg
    int cur_prefix_1 = 0;

    // Stores the current sign of
    // the prefix sum of array
    int parity = -1;

    // Stores minimum number of operations
    // for Case 1
    int minOperationsCase1 = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        cur_prefix_1 += A[i];

        // Checking both conditions
        if (cur_prefix_1 == 0
            || parity * cur_prefix_1 < 0) {

            minOperationsCase1
                += abs(parity - cur_prefix_1);

            // Update the  current prefix1 to
            // currentPrefixSum
            cur_prefix_1 = parity;
        }
        parity *= -1;
    }

    // Case 2\. pos - neg - pos
    int cur_prefix_2 = 0;

    // Stores the prefix sum of array
    parity = 1;

    // Stores minimum number of operations
    // for Case 1
    int minOperationsCase2 = 0;

    for (int i = 0; i < N; i++) {

        cur_prefix_2 += A[i];

        // Checking both conditions
        if (cur_prefix_2 == 0
            || parity * cur_prefix_2 < 0) {

            minOperationsCase2
                += abs(parity - cur_prefix_2);

            // Update the current prefix2 to
            // currentPrefixSum
            cur_prefix_2 = parity;
        }

        parity *= -1;
    }

    return min(minOperationsCase1,
               minOperationsCase2);
}

// Driver Code
int main()
{
    int A[] = { 1, -3, 1, 0 };
    int N = sizeof(A) / sizeof(A[0]);
    cout << minimumOperations(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for above approach
import java.util.*;

class GFG{

// Function to find the minimum number
// of increments/decrements of array
// elements by 1 to make signs of
// prefix sum array elements alternating
static int minimumOperations(int A[], int N)
{
    // Case 1\. neg - pos - neg
    int cur_prefix_1 = 0;

    // Stores the current sign of
    // the prefix sum of array
    int parity = -1;

    // Stores minimum number of operations
    // for Case 1
    int minOperationsCase1 = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        cur_prefix_1 += A[i];

        // Checking both conditions
        if (cur_prefix_1 == 0
            || parity * cur_prefix_1 < 0) {

            minOperationsCase1
                += Math.abs(parity - cur_prefix_1);

            // Update the  current prefix1 to
            // currentPrefixSum
            cur_prefix_1 = parity;
        }
        parity *= -1;
    }

    // Case 2\. pos - neg - pos
    int cur_prefix_2 = 0;

    // Stores the prefix sum of array
    parity = 1;

    // Stores minimum number of operations
    // for Case 1
    int minOperationsCase2 = 0;

    for (int i = 0; i < N; i++) {

        cur_prefix_2 += A[i];

        // Checking both conditions
        if (cur_prefix_2 == 0
            || parity * cur_prefix_2 < 0) {

            minOperationsCase2
                += Math.abs(parity - cur_prefix_2);

            // Update the current prefix2 to
            // currentPrefixSum
            cur_prefix_2 = parity;
        }

        parity *= -1;
    }

    return Math.min(minOperationsCase1,
               minOperationsCase2);
}

// Driver Code
public static void main(String[] args)

{
    int A[] = { 1, -3, 1, 0 };
    int N = A.length;
    System.out.print(minimumOperations(A, N));
}
}

// This code is contributed by avijitmondal1998.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum number
# of increments/decrements of array
# elements by 1 to make signs of
# prefix sum array elements alternating
def minimumOperations(A, N) :

    # Case 1\. neg - pos - neg
    cur_prefix_1 = 0

    # Stores the current sign of
    # the prefix sum of array
    parity = -1

    # Stores minimum number of operations
    # for Case 1
    minOperationsCase1 = 0

    # Traverse the array
    for i in range(N) :

        cur_prefix_1 += A[i]

        # Checking both conditions
        if (cur_prefix_1 == 0
            or parity * cur_prefix_1 < 0) :

            minOperationsCase1 += abs(parity - cur_prefix_1)

            # Update the  current prefix1 to
            # currentPrefixSum
            cur_prefix_1 = parity

        parity *= -1

    # Case 2\. pos - neg - pos
    cur_prefix_2 = 0

    # Stores the prefix sum of array
    parity = 1

    # Stores minimum number of operations
    # for Case 1
    minOperationsCase2 = 0

    for i in range(N) :

        cur_prefix_2 += A[i]

        # Checking both conditions
        if (cur_prefix_2 == 0
            or parity * cur_prefix_2 < 0) :

            minOperationsCase2 += abs(parity - cur_prefix_2)

            # Update the current prefix2 to
            # currentPrefixSum
            cur_prefix_2 = parity

        parity *= -1

    return min(minOperationsCase1,
               minOperationsCase2)

# Driver Code

A = [ 1, -3, 1, 0 ]
N = len(A)
print(minimumOperations(A, N))

# This code is contributed by splevel62.
```

## C#

```
// C# code for above approach
using System;
public class GFG
{

// Function to find the minimum number
// of increments/decrements of array
// elements by 1 to make signs of
// prefix sum array elements alternating
static int minimumOperations(int []A, int N)
{

    // Case 1\. neg - pos - neg
    int cur_prefix_1 = 0;

    // Stores the current sign of
    // the prefix sum of array
    int parity = -1;

    // Stores minimum number of operations
    // for Case 1
    int minOperationsCase1 = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        cur_prefix_1 += A[i];

        // Checking both conditions
        if (cur_prefix_1 == 0
            || parity * cur_prefix_1 < 0) {

            minOperationsCase1
                += Math.Abs(parity - cur_prefix_1);

            // Update the  current prefix1 to
            // currentPrefixSum
            cur_prefix_1 = parity;
        }
        parity *= -1;
    }

    // Case 2\. pos - neg - pos
    int cur_prefix_2 = 0;

    // Stores the prefix sum of array
    parity = 1;

    // Stores minimum number of operations
    // for Case 1
    int minOperationsCase2 = 0;

    for (int i = 0; i < N; i++) {

        cur_prefix_2 += A[i];

        // Checking both conditions
        if (cur_prefix_2 == 0
            || parity * cur_prefix_2 < 0) {

            minOperationsCase2
                += Math.Abs(parity - cur_prefix_2);

            // Update the current prefix2 to
            // currentPrefixSum
            cur_prefix_2 = parity;
        }

        parity *= -1;
    }

    return Math.Min(minOperationsCase1,
               minOperationsCase2);
}

// Driver Code
public static void Main(String[] args)

{
    int []A = { 1, -3, 1, 0 };
    int N = A.Length;
    Console.Write(minimumOperations(A, N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum number
// of increments/decrements of array
// elements by 1 to make signs of
// prefix sum array elements alternating
function minimumOperations(A, N)
{

  // Case 1\. neg - pos - neg
  let cur_prefix_1 = 0;

  // Stores the current sign of
  // the prefix sum of array
  let parity = -1;

  // Stores minimum number of operations
  // for Case 1
  let minOperationsCase1 = 0;

  // Traverse the array
  for (let i = 0; i < N; i++) {
    cur_prefix_1 += A[i];

    // Checking both conditions
    if (cur_prefix_1 == 0 || parity * cur_prefix_1 < 0) {
      minOperationsCase1 += Math.abs(parity - cur_prefix_1);

      // Update the  current prefix1 to
      // currentPrefixSum
      cur_prefix_1 = parity;
    }
    parity *= -1;
  }

  // Case 2\. pos - neg - pos
  let cur_prefix_2 = 0;

  // Stores the prefix sum of array
  parity = 1;

  // Stores minimum number of operations
  // for Case 1
  let minOperationsCase2 = 0;

  for (let i = 0; i < N; i++) {
    cur_prefix_2 += A[i];

    // Checking both conditions
    if (cur_prefix_2 == 0 || parity * cur_prefix_2 < 0) {
      minOperationsCase2 += Math.abs(parity - cur_prefix_2);

      // Update the current prefix2 to
      // currentPrefixSum
      cur_prefix_2 = parity;
    }

    parity *= -1;
  }

  return Math.min(minOperationsCase1, minOperationsCase2);
}

// Driver Code
let A = [1, -3, 1, 0];
let N = A.length;
document.write(minimumOperations(A, N));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)