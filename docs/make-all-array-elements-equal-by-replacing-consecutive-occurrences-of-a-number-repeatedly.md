# 通过重复替换一个数字的连续出现使所有数组元素相等

> 原文:[https://www . geeksforgeeks . org/通过重复替换连续出现的数字来使所有数组元素相等/](https://www.geeksforgeeks.org/make-all-array-elements-equal-by-replacing-consecutive-occurrences-of-a-number-repeatedly/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是通过以下操作找到使所有数组元素**等于**所需的**最小**操作数:

1.  在 **1** 到 **N** 之间选择任意**号。**
2.  从数组中选择一个元素，
3.  用**选择的**号替换所有连续相等的元素。

**示例:**

> **输入:** arr[] = {1，2，5，2，1}，N = 5
> **输出:** 2
> **说明:**以下是使 arr[]中所有元素相等所需的操作。
> {1，2， **2** ，2，1}，拾取 **2** 并将其替换为所有连续的 **5** s.
> {1， **1** ， **1** ， **1** ，1}，拾取 **1** 并将其替换为所有连续的 **2** s.
> 因此，操作次数
> 
> **输入:** arr[] = {4，4，7，4，7，7，3，3}，N = 7
> **输出:** 3

**方法:**这个问题可以用**动态规划**解决。其思想是将子区间内消失元素的顺序考虑到极致。在子区间**【l，r】**内，位置 **r** 处的元素将首次消失。并且，在那个时间点，将有消失元素的子区间**【I，r】**。那些**【I，r】**在最少的步骤中被删除。否则，我们可以减少步骤数。此外，在上一步中，位置 **r** 处的元素是存在的。所以，有两种可能的情况:

*   线段**【I，r-1】**已经被删除了⇢的意思是在 **r** 位置删除了单个元素，但是这意味着我们可以先删除**【l，r-1】**线段，然后在 **r** 位置删除单个元素。
*   线段**【I+1，r-1】**已经被删除了⇢意味着两个元素同时被删除:在位置 r 和 I。它们必须是相同的元素。

删除初始数组中所有连续的重复项。利用上述思路，使 **dp[l][r]** —删除**【l，r】**范围内的所有元素需要多少步。那么，答案是**(DP[0][n-1]–1)**在从零开始的索引中，只需删除整个数组减去一步。

*   **dp[][]** 的基数为 **dp[i][i] = 1** 。
*   对于 **l < r** ，**DP【l】【r】**最初设置为**DP【l】【r-1】+1**。
*   对于位置 **i** 处与位置 **r** 处元素颜色相同的每个元素，如果 dp[l][i-1] + dp[i，r] 更好，则更新 **dp[l][r]。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of
// operations required to make all the
// array elements equal
int minOperations(vector<int> arr, int N)
{
    vector<int> p(N + 1, -1);
    int j = 0;

    for (int i = 1; i < N; ++i) {
        if (arr[i] != arr[j]) {
            ++j;
            arr[j] = arr[i];
        }
    }

    N = j + 1;
    arr.resize(N);

    vector<vector<int> > dp(N, vector<int>(N));
    vector<int> b(N, -1);

    for (int j = 0; j < N; ++j) {
        dp[j][j] = 1;

        b[j] = p[arr[j]];
        p[arr[j]] = j;

        for (int i = j - 1; i >= 0; --i) {
            int d = dp[i][j - 1] + 1;

            for (int k = b[j]; k > i; k = b[k]) {
                d = min(d, dp[i][k - 1] + dp[k][j]);
            }
            if (arr[i] == arr[j]) {
                d = min(d, dp[i + 1][j]);
            }
            dp[i][j] = d;
        }
    }
    // Return the answer
    return dp[0][N - 1] - 1;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 5, 2, 1 };
    int N = arr.size();

    cout << minOperations(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG
{

    // Function to find the minimum number of
    // operations required to make all the
    // array elements equal
    static int minOperations(int[] arr, int N)
    {
        int p[] = new int[N + 1];
        Arrays.fill(p, -1);
        int j = 0;

        for (int i = 1; i < N; ++i) {
            if (arr[i] != arr[j]) {
                ++j;
                arr[j] = arr[i];
            }
        }

        N = j + 1;
        int[][] dp = new int[N][N];
        int[] b = new int[N];
        Arrays.fill(b, -1);

        for (j = 0; j < N; ++j) {
            dp[j][j] = 1;

            b[j] = p[arr[j]];
            p[arr[j]] = j;

            for (int i = j - 1; i >= 0; --i) {
                int d = dp[i][j - 1] + 1;

                for (int k = b[j]; k > i; k = b[k]) {
                    d = Math.min(d,
                                 dp[i][k - 1] + dp[k][j]);
                }
                if (arr[i] == arr[j]) {
                    d = Math.min(d, dp[i + 1][j]);
                }
                dp[i][j] = d;
            }
        }

        // Return the answer
        return dp[0][N - 1] - 1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 2, 5, 2, 1 };
        int N = arr.length;

        System.out.println(minOperations(arr, N));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the minimum number of
# operations required to make all the
# array elements equal
def minOperations(arr, N):

    p = [-1 for _ in range(N + 1)]
    j = 0

    for i in range(1, N):
        if (arr[i] != arr[j]):
            j += 1
            arr[j] = arr[i]

    N = j + 1
    arr = arr[:N]

    dp = [[0 for _ in range(N)] for _ in range(N)]
    b = [-1 for _ in range(N)]

    for j in range(0, N):
        dp[j][j] = 1

        b[j] = p[arr[j]]
        p[arr[j]] = j

        for i in range(j-1, -1, -1):
            d = dp[i][j - 1] + 1

            k = b[j]
            while k > i:
                d = min(d, dp[i][k - 1] + dp[k][j])
                k = b[k]

            if (arr[i] == arr[j]):
                d = min(d, dp[i + 1][j])

            dp[i][j] = d

        # Return the answer
    return dp[0][N - 1] - 1

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 5, 2, 1]
    N = len(arr)

    print(minOperations(arr, N))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# code for the above approach
using System;
using System.Collections;
class GFG
{

    // Function to find the minimum number of
    // operations required to make all the
    // array elements equal
    static int minOperations(int[] arr, int N)
    {
        int[] p = new int[N + 1];
        Array.Fill(p, -1);
        int j = 0;

        for (int i = 1; i < N; ++i)
        {
            if (arr[i] != arr[j])
            {
                ++j;
                arr[j] = arr[i];
            }
        }

        N = j + 1;
        int[,] dp = new int[N, N];
        int[] b = new int[N];
        Array.Fill(b, -1);

        for (j = 0; j < N; ++j)
        {
            dp[j, j] = 1;

            b[j] = p[arr[j]];
            p[arr[j]] = j;

            for (int i = j - 1; i >= 0; --i)
            {
                int d = dp[i, j - 1] + 1;

                for (int k = b[j]; k > i; k = b[k])
                {
                    d = Math.Min(d, dp[i, k - 1] + dp[k, j]);
                }
                if (arr[i] == arr[j])
                {
                    d = Math.Min(d, dp[i + 1, j]);
                }
                dp[i, j] = d;
            }
        }

        // Return the answer
        return dp[0, N - 1] - 1;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 2, 5, 2, 1 };
        int N = arr.Length;

        Console.Write(minOperations(arr, N));
    }
}

// This code is contributed by gfgking
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum number of
// operations required to make all the
// array elements equal
function minOperations(arr, N) {
  let p = new Array(N + 1).fill(-1);
  let j = 0;

  for (let i = 1; i < N; ++i) {
    if (arr[i] != arr[j]) {
      ++j;
      arr[j] = arr[i];
    }
  }

  N = j + 1;
  arr.slice(0, N);

  let dp = new Array(N).fill(0).map(() => new Array(N))
  let b = new Array(N).fill(-1);

  for (let j = 0; j < N; ++j) {
    dp[j][j] = 1;

    b[j] = p[arr[j]];
    p[arr[j]] = j;

    for (let i = j - 1; i >= 0; --i) {
      let d = dp[i][j - 1] + 1;

      for (let k = b[j]; k > i; k = b[k]) {
        d = Math.min(d, dp[i][k - 1] + dp[k][j]);
      }
      if (arr[i] == arr[j]) {
        d = Math.min(d, dp[i + 1][j]);
      }
      dp[i][j] = d;
    }
  }
  // Return the answer
  return dp[0][N - 1] - 1;
}

// Driver Code

let arr = [1, 2, 5, 2, 1];
let N = arr.length;

document.write(minOperations(arr, N));

// This code is contributed by gfgking.
</script>
```

**Output**

```
2
```

**时间复杂度:**O(N<sup>3</sup>)
T5】辅助空间: O(N <sup>2</sup>