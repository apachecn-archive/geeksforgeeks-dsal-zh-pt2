# 使用给定操作形成的缩减阵列的最小长度

> 原文:[https://www . geeksforgeeks . org/使用给定操作形成的最小长度缩减数组/](https://www.geeksforgeeks.org/minimum-length-of-the-reduced-array-formed-using-given-operations/)

给定一个长度为 **N** 的数组 **arr** ，任务是通过执行以下操作来最小化其长度:

*   移除任何相邻的相等对(即如果 **arr[i] = arr[i+1]** )，并用单个实例 **arr[i] + 1** 替换它。
*   每个操作都将数组长度减 1。
*   重复操作，直到不能再减少。

**例:**

> **输入:** arr = {3，3，4，4，4，3，3}
> **输出:** 2
> **解释:**
> 合并前两个 3s，用 4 替换。已更新数组:{4，4，4，4，3，3}
> 合并前两个 4，并用 5 替换它们。已更新数组:{5，4，4，3，3}
> 合并两个 4，并用 5 替换。更新的数组:{5，5，3，3}
> 合并两个 5s，用 6 替换。已更新数组:{6，3，3}
> 合并两个 3s，并用 4 替换它们。更新的数组:{6，4}
> 因此，缩减数组的最小长度= 2
> **输入:** arr = {4，3，2，2，3}
> **输出:** 2
> **解释:**
> 将两个 2s 合并并用 3 替换。已更新数组:{4，3，3，3}
> 合并前两个 3s，并用 4 替换它们。已更新数组:{4，4，3}
> 合并两个 4，并用 5 替换。更新的数组:{5，3}
> 因此，缩减数组的最小长度= 2

**方法:**上述问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。可以观察到，最终阵列中的每个元素将是相应段上的多个元素替换的结果。因此，我们的目标是在段上找到数组的最小分区，其中每个段可以通过一系列操作转换为单个元素。
让我们定义如下[动态编程表](https://www.geeksforgeeks.org/dynamic-programming/)状态:

> **dp[i][j] =当从索引 I 到 j 的子阵列通过一系列操作减少时的单个剩余元素的值**
> 或者当子阵列不能减少到单个元素时等于-1。

**用于计算 dp[i][j]:**

*   如果 i = j， **dp[i][j] = a[i]**
*   从[i，j-1]迭代，让遍历索引为 k (i <= k < j). For any k if **dp[i][k] = dp[k+1][j]** ，这意味着子阵[i，j]可以分为两部分，两部分的最终值相同，所以这两部分可以合并，即 **dp[i][j] = dp[i][k] + 1** 。

**为了计算最小分区**，我们将创建另一个 *dp 表*，其中存储最终结果。该表有以下状态:

> **dp1[i] =子阵列[1: i]**
> 的最小划分，这是在执行上述操作之后直到 I 的最小阵列大小。

**以下是上述方法的实施:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation to find the
// minimum length of the array

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// length of minimized array
int minimalLength(int a[], int n)
{

    // Creating the required dp tables
    int dp[n + 1][n + 1], dp1[n];
    int i, j, k;

    // Initialising the dp table by -1
    memset(dp, -1, sizeof(dp));

    for (int size = 1; size <= n; size++) {
        for (i = 0; i < n - size + 1; i++) {
            j = i + size - 1;

            // base case
            if (i == j)
                dp[i][j] = a[i];
            else {
                for (k = i; k < j; k++) {

                    // Check if the two subarray
                    // can be combined
                    if (dp[i][k] != -1
                        && dp[i][k] == dp[k + 1][j])

                        dp[i][j] = dp[i][k] + 1;
                }
            }
        }
    }

    // Initialising dp1 table with max value
    for (i = 0; i < n; i++)
        dp1[i] = 1e7;

    for (i = 0; i < n; i++) {
        for (j = 0; j <= i; j++) {

            // Check if the subarray can be
            // reduced to a single element
            if (dp[j][i] != -1) {
                if (j == 0)
                    dp1[i] = 1;

                // Minimal partition
                // of [1: j-1] + 1
                else
                    dp1[i] = min(
                        dp1[i],
                        dp1[j - 1] + 1);
            }
        }
    }

    return dp1[n - 1];
}

// Driver code
int main()
{

    int n = 7;
    int a[n] = { 3, 3, 4, 4, 4, 3, 3 };

    cout << minimalLength(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum length of the array
import java.util.*;

class GFG{

// Function to find the
// length of minimized array
static int minimalLength(int a[], int n)
{

    // Creating the required dp tables
    int [][]dp = new int[n + 1][n + 1];
    int []dp1 = new int[n];
    int i, j, k;

    // Initialising the dp table by -1
    for (i = 0; i < n + 1; i++) {
        for (j = 0; j < n + 1; j++) {
            dp[i][j] = -1;
        }
    }

    for (int size = 1; size <= n; size++) {
        for (i = 0; i < n - size + 1; i++) {
            j = i + size - 1;

            // base case
            if (i == j)
                dp[i][j] = a[i];
            else {
                for (k = i; k < j; k++) {

                    // Check if the two subarray
                    // can be combined
                    if (dp[i][k] != -1
                        && dp[i][k] == dp[k + 1][j])

                        dp[i][j] = dp[i][k] + 1;
                }
            }
        }
    }

    // Initialising dp1 table with max value
    for (i = 0; i < n; i++)
        dp1[i] = (int) 1e7;

    for (i = 0; i < n; i++) {
        for (j = 0; j <= i; j++) {

            // Check if the subarray can be
            // reduced to a single element
            if (dp[j][i] != -1) {
                if (j == 0)
                    dp1[i] = 1;

                // Minimal partition
                // of [1: j-1] + 1
                else
                    dp1[i] = Math.min(
                        dp1[i],
                        dp1[j - 1] + 1);
            }
        }
    }

    return dp1[n - 1];
}

// Driver code
public static void main(String[] args)
{

    int n = 7;
    int a[] = { 3, 3, 4, 4, 4, 3, 3 };

    System.out.print(minimalLength(a, n));

}
}

// This code contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum length of the array
import numpy as np

# Function to find the
# length of minimized array
def minimalLength(a, n) :

    # Creating the required dp tables
    # Initialising the dp table by -1
    dp = np.ones((n + 1,n + 1)) * -1;
    dp1 = [0]*n;

    for size in range(1, n + 1) :
        for i in range( n - size + 1) :
            j = i + size - 1;

            # base case
            if (i == j) :
                dp[i][j] = a[i];
            else :
                for k in range(i,j) :

                    # Check if the two subarray
                    # can be combined
                    if (dp[i][k] != -1 and dp[i][k] == dp[k + 1][j]) :

                        dp[i][j] = dp[i][k] + 1;

    # Initialising dp1 table with max value
    for i in range(n) :
        dp1[i] = int(1e7);

    for i in range(n) :
        for j in range(i + 1) :

            # Check if the subarray can be
            # reduced to a single element
            if (dp[j][i] != -1) :
                if (j == 0) :
                    dp1[i] = 1;

                # Minimal partition
                # of [1: j-1] + 1
                else :
                    dp1[i] = min(
                        dp1[i],
                        dp1[j - 1] + 1);

    return dp1[n - 1];

# Driver code
if __name__ == "__main__" :

    n = 7;
    a = [ 3, 3, 4, 4, 4, 3, 3 ];
    print(minimalLength(a, n));

    # This code is contributed by Yash_R
```

## C#

```
// C# implementation to find the
// minimum length of the array
using System;

class GFG{

    // Function to find the
    // length of minimized array
    static int minimalLength(int []a, int n)
    {

        // Creating the required dp tables
        int [,]dp = new int[n + 1, n + 1];
        int []dp1 = new int[n];
        int i, j, k;

        // Initialising the dp table by -1
        for (i = 0; i < n + 1; i++) {
            for (j = 0; j < n + 1; j++) {
                dp[i, j] = -1;
            }
        }

        for (int size = 1; size <= n; size++) {
            for (i = 0; i < n - size + 1; i++) {
                j = i + size - 1;

                // base case
                if (i == j)
                    dp[i, j] = a[i];
                else {
                    for (k = i; k < j; k++) {

                        // Check if the two subarray
                        // can be combined
                        if (dp[i, k] != -1
                            && dp[i, k] == dp[k + 1, j])

                            dp[i, j] = dp[i, k] + 1;
                    }
                }
            }
        }

        // Initialising dp1 table with max value
        for (i = 0; i < n; i++)
            dp1[i] = (int) 1e7;

        for (i = 0; i < n; i++) {
            for (j = 0; j <= i; j++) {

                // Check if the subarray can be
                // reduced to a single element
                if (dp[j, i] != -1) {
                    if (j == 0)
                        dp1[i] = 1;

                    // Minimal partition
                    // of [1: j-1] + 1
                    else
                        dp1[i] = Math.Min(
                            dp1[i],
                            dp1[j - 1] + 1);
                }
            }
        }

        return dp1[n - 1];
    }

    // Driver code
    public static void Main(string[] args)
    {

        int n = 7;
        int []a = { 3, 3, 4, 4, 4, 3, 3 };

        Console.Write(minimalLength(a, n));
    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// minimum length of the array

// Function to find the
// length of minimized array
function minimalLength(a, n)
{

    // Creating the required dp t0ables
    // Initialising the dp table by -1
    var i, j, k;
    var dp = Array(n+1).fill(Array(n+1).fill(-1));
    var dp1 = Array(n).fill(0);

    for (var size = 1; size <= n; size++) {
        for (i = 0; i < n - size + 1; i++) {
            j = i + size - 1;

            // base case
            if (i == j)
                dp[i][j] = a[i];
            else {
                for (k = i; k < j; k++) {

                    // Check if the two subarray
                    // can be combined
                    if (dp[i][k] != -1
                        && dp[i][k] == dp[k + 1][j])

                        dp[i][j] = dp[i][k] + 1;
                }
            }
        }
    }

    // Initialising dp1 table with max value
    for (i = 0; i < n; i++)
        dp1[i] = 1000000000;

    for (i = 0; i < n; i++)
    {
        for (j = 0; j <= i; j++)
        {

            // Check if the subarray can be
            // reduced to a single element
            if (dp[j][i] != -1) {
                if (j == 0)
                    dp1[i] = 2;

                // Minimal partition
                // of [1: j-1] + 1
                else
                    dp1[i] = Math.min(dp1[i], dp1[j - 1] + 1);
            }
        }
    }
    return dp1[n - 1];
}

// Driver code
var n = 7;
var a = [ 3, 3, 4, 4, 4, 3, 3 ];
document.write(minimalLength(a, n));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N <sup>3</sup> )*