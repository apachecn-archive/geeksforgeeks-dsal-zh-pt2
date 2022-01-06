# 大小为 K 且和小于 X 的最大和子阵

> 原文:[https://www . geeksforgeeks . org/大小为 k 的最大和子数组的和小于 x/](https://www.geeksforgeeks.org/maximum-sum-subarray-of-size-k-with-sum-less-than-x/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和两个整数 **K** 和 **X** ，任务是在所有大小为 **K** 的[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)中找到和小于 **X** 的最大和。

**示例:**

> **输入:** arr[] = {20，2，3，10，5}，K = 3，X = 20
> **输出:** 18
> **说明:**最大和小于 20 的 3 号子阵为{3，10，5}。因此，所需输出为 18。
> 
> **输入:** arr[] = {-5，8，7，2，10，1，20，-4，6，9}，K = 5，X = 30
> **输出:** 29
> **说明:**最大和小于 30 的 5 号子阵为{2，10，1，20，-4}。因此，所需输出为 29。

**天真法:**解决问题最简单的方法是[生成所有大小为 **K** 的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，检查其和是否小于 **X** 。打印所有此类子阵列中获得的最大总和。

***时间复杂度:** O(N * K)*
***辅助空间:** O(1)*

**高效方法:**按照以下步骤使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)解决问题:

1.  初始化一个变量 **sum_K** 来存储第一个 **K** 数组元素的和。
2.  如果 **sum_K** 小于 **X** ，则用 **sum_K** 初始化 **Max_Sum** 。
3.  [从 **(K + 1) <sup>第</sup>** 索引遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下操作:
    1.  在每次迭代中，减去先前 **K** 长度子阵列的第一个元素，并将当前元素添加到 **sum_K** 中。
    2.  如果 **sum_K** 小于 **X** ，则将 **sum_K** 与 **Max_Sum** 进行比较，并相应更新 **Max_Sum** 。
4.  最后打印 **Max_Sum** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum sum
// among all subarrays of size K
// with the sum less than X
void maxSumSubarr(int A[], int N,
                  int K, int X)
{

    // Initialize sum_K to 0
    int sum_K = 0;

    // Calculate sum of first K elements
    for (int i = 0; i < K; i++) {

        sum_K += A[i];
    }

    int Max_Sum = 0;

    // If sum_K is less than X
    if (sum_K < X) {

        // Initialize MaxSum with sum_K
        Max_Sum = sum_K;
    }

    // Iterate over the array from
    // (K + 1)-th index
    for (int i = K; i < N; i++) {

        // Subtract the first element
        // from the previous K elements
        // and add the next element
        sum_K -= (A[i - K] - A[i]);

        // If sum_K is less than X
        if (sum_K < X) {

            // Update the Max_Sum
            Max_Sum = max(Max_Sum, sum_K);
        }
    }

    cout << Max_Sum << endl;
}

// Driver Code
int main()
{
    int arr[] = { -5, 8, 7, 2, 10,
                  1, 20, -4, 6, 9 };
    int K = 5;
    int X = 30;

    // Size of Array
    int N = sizeof(arr)
            / sizeof(arr[0]);

    // Function Call
    maxSumSubarr(arr, N, K, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to calculate maximum sum
// among all subarrays of size K
// with the sum less than X
private static void maxSumSubarr(int A[], int N,
                                 int K, int X)
{

    // Initialize sum_K to 0
    int sum_K = 0;

    // Calculate sum of first K elements
    for(int i = 0; i < K; i++)
    {
        sum_K += A[i];
    }

    int Max_Sum = 0;

    // If sum_K is less than X
    if (sum_K < X)
    {

        // Initialize MaxSum with sum_K
        Max_Sum = sum_K;
    }

    // Iterate over the array from
    // (K + 1)-th index
    for(int i = K; i < N; i++)
    {

        // Subtract the first element
        // from the previous K elements
        // and add the next element
        sum_K -= (A[i - K] - A[i]);

        // If sum_K is less than X
        if (sum_K < X)
        {

            // Update the Max_Sum
            Max_Sum = Math.max(Max_Sum, sum_K);
        }
    }

    System.out.println(Max_Sum);
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { -5, 8, 7, 2, 10,
                  1, 20, -4, 6, 9 };
    int K = 5;
    int X = 30;

    // Size of Array
    int N = arr.length;

    // Function Call
    maxSumSubarr(arr, N, K, X);
}
}

// This code is contributed by jithin
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate maximum sum
# among all subarrays of size K
# with the sum less than X
def maxSumSubarr(A, N, K, X):

    # Initialize sum_K to 0
    sum_K = 0

    # Calculate sum of first K elements
    for i in range(0, K):
        sum_K += A[i]

    Max_Sum = 0

    # If sum_K is less than X
    if (sum_K < X):

        # Initialize MaxSum with sum_K
        Max_Sum = sum_K

    # Iterate over the array from
    # (K + 1)-th index
    for i in range(K, N):

        # Subtract the first element
        # from the previous K elements
        # and add the next element
        sum_K -= (A[i - K] - A[i])

        # If sum_K is less than X
        if (sum_K < X):

            # Update the Max_Sum
            Max_Sum = max(Max_Sum, sum_K)

    print(Max_Sum)

# Driver Code
arr = [ -5, 8, 7, 2, 10,
         1, 20, -4, 6, 9 ]
K = 5
X = 30

# Size of Array
N = len(arr)

# Function Call
maxSumSubarr(arr, N, K, X)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate maximum sum
// among all subarrays of size K
// with the sum less than X
private static void maxSumSubarr(int []A, int N,
                                 int K, int X)
{

    // Initialize sum_K to 0
    int sum_K = 0;

    // Calculate sum of first K elements
    for(int i = 0; i < K; i++)
    {
        sum_K += A[i];
    }

    int Max_Sum = 0;

    // If sum_K is less than X
    if (sum_K < X)
    {

        // Initialize MaxSum with sum_K
        Max_Sum = sum_K;
    }

    // Iterate over the array from
    // (K + 1)-th index
    for(int i = K; i < N; i++)
    {

        // Subtract the first element
        // from the previous K elements
        // and add the next element
        sum_K -= (A[i - K] - A[i]);

        // If sum_K is less than X
        if (sum_K < X)
        {

            // Update the Max_Sum
            Max_Sum = Math.Max(Max_Sum, sum_K);
        }
    }
    Console.WriteLine(Max_Sum);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { -5, 8, 7, 2, 10,
                   1, 20, -4, 6, 9 };
    int K = 5;
    int X = 30;

    // Size of Array
    int N = arr.Length;

    // Function Call
    maxSumSubarr(arr, N, K, X);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to implement the above approach

// Function to calculate maximum sum
// among all subarrays of size K
// with the sum less than X
function maxSumSubarr(A, N, K, X)
{

    // Initialize sum_K to 0
    let sum_K = 0;

    // Calculate sum of first K elements
    for (let i = 0; i < K; i++) {

        sum_K += A[i];
    }

    let Max_Sum = 0;

    // If sum_K is less than X
    if (sum_K < X) {

        // Initialize MaxSum with sum_K
        Max_Sum = sum_K;
    }

    // Iterate over the array from
    // (K + 1)-th index
    for (let i = K; i < N; i++) {

        // Subtract the first element
        // from the previous K elements
        // and add the next element
        sum_K -= (A[i - K] - A[i]);

        // If sum_K is less than X
        if (sum_K < X) {

            // Update the Max_Sum
            Max_Sum = Math.max(Max_Sum, sum_K);
        }
    }
    document.write(Max_Sum);
}

// Driver Code

    let arr = [ -5, 8, 7, 2, 10,
                  1, 20, -4, 6, 9 ];
    let K = 5;
    let X = 30;

    // Size of Array
    let N = arr.length;

    // Function Call
    maxSumSubarr(arr, N, K, X);

    // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
29
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)