# 最小化要移除的数组元素的数量，使得至少 K 个元素等于它们的索引值

> 原文:[https://www . geesforgeks . org/最小化要移除的数组元素的数量，以便至少 k 个元素等于它们的索引值/](https://www.geeksforgeeks.org/minimize-count-of-array-elements-to-be-removed-such-that-at-least-k-elements-are-equal-to-their-index-values/)

给定一个由 **N** 个整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】***(基于 1 的索引)*，任务是找到必须移除的最小数组元素数，使得**至少有 K 个** [数组元素等于它们的索引值](https://www.geeksforgeeks.org/count-index-pairs-equal-elements-array/)。如果不可能，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {5，1，3，2，3} K = 2
> **输出:** 2
> **说明:**
> 以下是所需的移除操作:
> 
> *   移除 arr[1]会将数组修改为{1，3，2，3} -> 1 元素等于其索引值。
> *   移除 arr[3]会将数组修改为{1，2，3} -> 3 个元素等于它们的索引值。
> 
> 在上述操作之后，3 个(> = K)元素等于它们的索引值，所需的最小删除量是 2。
> 
> **输入:** arr[] = {2，3，4} K = 1
> **输出:** -1

**方法:**上述问题可以借助[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。按照以下步骤解决给定的问题。

*   初始化二维 **dp** 表，使得**DP【I】【j】**将表示当总共存在 j 个元素时，值等于其索引的最大元素。
*   **dp** 表中的所有值最初都用 **0s** 填充。
*   对于范围**【0，N-1】**中的每个 **i** 和范围**【0，I】**中的 **j** 进行迭代，有两种选择。
    *   **删除当前元素，**DP 表可以更新为 **dp[i+1][j] = max(dp[i+1][j]，dp[i][j])** 。
    *   **保留当前元素，**则 dp 表可以更新为:**DP[I+1][j+1]= max(DP[I+1][j+1]，dp[i][j] + (arr[i+1] == j+1))** 。
*   现在对于范围【than，0】中的每个 **j** 检查**DP【N】【j】的值是否大于或等于 K** 。如果找到，取最小值并返回答案。
*   否则，在最后返回 **-1** 。这意味着没有找到可能的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to minimize the removals of
// array elements such that atleast K
// elements are equal to their indices
int MinimumRemovals(int a[], int N, int K)
{
    // Store the array as 1-based indexing
    // Copy of first array
    int b[N + 1];
    for (int i = 0; i < N; i++) {
        b[i + 1] = a[i];
    }

    // Make a dp-table of (N*N) size
    int dp[N + 1][N + 1];

    // Fill the dp-table with zeroes
    memset(dp, 0, sizeof(dp));
    for (int i = 0; i < N; i++) {
        for (int j = 0; j <= i; j++) {

            // Delete the current element
            dp[i + 1][j] = max(
                dp[i + 1][j], dp[i][j]);

            // Take the current element
            dp[i + 1][j + 1] = max(
                dp[i + 1][j + 1],
                dp[i][j] + ((b[i + 1] == j + 1) ? 1 : 0));
        }
    }

    // Check for the minimum removals
    for (int j = N; j >= 0; j--) {
        if (dp[N][j] >= K) {
            return (N - j);
        }
    }
    return -1;
}

// Driver Code
int main()
{
    int arr[] = { 5, 1, 3, 2, 3 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << MinimumRemovals(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to minimize the removals of
    // array elements such that atleast K
    // elements are equal to their indices
    static int MinimumRemovals(int a[], int N, int K)
    {
        // Store the array as 1-based indexing
        // Copy of first array
        int b[] = new int[N + 1];
        for (int i = 0; i < N; i++) {
            b[i + 1] = a[i];
        }

        // Make a dp-table of (N*N) size
        int dp[][] = new int[N + 1][N + 1];

        for (int i = 0; i < N; i++) {
            for (int j = 0; j <= i; j++) {

                // Delete the current element
                dp[i + 1][j] = Math.max(dp[i + 1][j], dp[i][j]);

                // Take the current element
                dp[i + 1][j + 1] = Math.max(
                    dp[i + 1][j + 1],
                    dp[i][j]
                        + ((b[i + 1] == j + 1) ? 1 : 0));
            }
        }

        // Check for the minimum removals
        for (int j = N; j >= 0; j--) {
            if (dp[N][j] >= K) {
                return (N - j);
            }
        }
        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 5, 1, 3, 2, 3 };
        int K = 2;
        int N = arr.length;
        System.out.println(MinimumRemovals(arr, N, K));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to minimize the removals of
# array elements such that atleast K
# elements are equal to their indices
def MinimumRemovals(a, N, K):

    # Store the array as 1-based indexing
    # Copy of first array
    b = [0 for i in range(N + 1)]
    for i in range(N):
        b[i + 1] = a[i]

    # Make a dp-table of (N*N) size
    dp = [[0 for i in range(N+1)] for j in range(N+1)]

    for i in range(N):
        for j in range(i + 1):

            # Delete the current element
            dp[i + 1][j] = max(dp[i + 1][j], dp[i][j])

            # Take the current element
            dp[i + 1][j + 1] = max(dp[i + 1][j + 1],dp[i][j] + (1 if (b[i + 1] == j + 1) else 0))

    # Check for the minimum removals
    j = N
    while(j >= 0):
        if(dp[N][j] >= K):
            return (N - j)
        j -= 1
    return -1

# Driver Code
if __name__ == '__main__':
    arr = [5, 1, 3, 2, 3]
    K = 2
    N = len(arr)
    print(MinimumRemovals(arr, N, K))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# code for the above approach
using System;

public class GFG
{

    // Function to minimize the removals of
    // array elements such that atleast K
    // elements are equal to their indices
    static int MinimumRemovals(int[] a, int N, int K)
    {

        // Store the array as 1-based indexing
        // Copy of first array
        int[] b = new int[N + 1];
        for (int i = 0; i < N; i++) {
            b[i + 1] = a[i];
        }

        // Make a dp-table of (N*N) size
        int[, ] dp = new int[N + 1, N + 1];

        for (int i = 0; i < N; i++) {
            for (int j = 0; j <= i; j++) {

                // Delete the current element
                dp[i + 1, j]
                    = Math.Max(dp[i + 1, j], dp[i, j]);

                // Take the current element
                dp[i + 1, j + 1] = Math.Max(
                    dp[i + 1, j + 1],
                    dp[i, j]
                        + ((b[i + 1] == j + 1) ? 1 : 0));
            }
        }

        // Check for the minimum removals
        for (int j = N; j >= 0; j--) {
            if (dp[N, j] >= K) {
                return (N - j);
            }
        }
        return -1;
    }

    static public void Main()
    {

        // Code
        int[] arr = { 5, 1, 3, 2, 3 };
        int K = 2;
        int N = arr.Length;
        Console.Write(MinimumRemovals(arr, N, K));
    }
}

// This code is contributed by Potta Lokesh
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to minimize the removals of
// array elements such that atleast K
// elements are equal to their indices
function MinimumRemovals(a, N, K)
{

    // Store the array as 1-based indexing
    // Copy of first array
    let b = new Array(N + 1);
    for (let i = 0; i < N; i++) {
        b[i + 1] = a[i];
    }

    // Make a dp-table of (N*N) size
    let dp = new Array(N + 1).fill(0).map(() => new Array(N + 1).fill(0));

    for (let i = 0; i < N; i++) {
        for (let j = 0; j <= i; j++) {

            // Delete the current element
            dp[i + 1][j] = Math.max(
                dp[i + 1][j], dp[i][j]);

            // Take the current element
            dp[i + 1][j + 1] = Math.max(
                dp[i + 1][j + 1],
                dp[i][j] + ((b[i + 1] == j + 1) ? 1 : 0));
        }
    }

    // Check for the minimum removals
    for (let j = N; j >= 0; j--) {
        if (dp[N][j] >= K) {
            return (N - j);
        }
    }
    return -1;
}

// Driver Code

    let arr = [ 5, 1, 3, 2, 3 ];
    let K = 2;
    let N = arr.length
    document.write(MinimumRemovals(arr, N, K));

    // This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*