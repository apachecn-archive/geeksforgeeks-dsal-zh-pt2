# 长度为 k 的最大和子序列

> 原文:[https://www . geesforgeks . org/maximum-sum-subsequence-of-length-k/](https://www.geeksforgeeks.org/maximum-sum-subsequence-of-length-k/)

给定一个数组序列【A <sub>1</sub> ，A <sub>2</sub> …A <sub>n</sub> 】，任务是找到长度为 k 的递增子序列 S 的最大可能和，使得 S<sub>1</sub><= S<sub>2</sub><= S<sub>3</sub>……<= S<sub>k</sub>。

**示例:**

> **输入:**
> n = 8k = 3
> A =【8 5 9 10 5 6 21 8】
> **输出:** 40
> 最大可能和的长度 3 的可能递增子序列是 9 10 21
> 
> **输入:**
> n = 9k = 4
> A =【2 5 3 9 15 33 6 18 20】
> T5】输出: 62
> 最大可能和长度 4 的可能递增子序列为 9 15 18 20

有一点很明显，用动态规划很容易解决，这个问题是[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的简单变异。如果您不知道如何计算最长的递增子序列，请查看链接中的实现。

**天真法:**
在蛮力法中，首先我们会尝试找到长度为 k 的所有子序列，并检查它们是否在增加。当所有元素都按递增顺序排列时，最坏的情况下可能会出现 <sup>n</sup> C <sub>k</sub> 这样的序列。现在我们将找到这种序列的最大可能和。
时间复杂度为 0((<sup>n</sup>C<sub>k</sub>)* n)。

**有效方法:**
我们将使用二维 dp 数组，其中 dp[i][l]表示长度为 l 的最大和子序列，取 0 到 I 的数组值，子序列以索引“I”结束。“l”的范围是从 0 到 k-1。当 j < i 时，使用内环上较长的递增子序列的方法，我们将检查 arr[j] < arr[i]是否用于检查子序列是否递增。

这个问题可以分为几个子问题:

> dp[i][1]=arr[i]对于长度 1，最大递增子序列等于数组值
> dp[i][l+1]=对于 1 到 k-1 之间的任何长度 l
> ，最大值(dp[i][l+1]，dp[j][l]+arr[i])

这意味着，如果对于第 I 个位置和长度为 l+1 的子序列，在 j (j < i) of length l for which sum of dp[j][l] + arr[i] is more than its initial calculated value then update that value. 
处存在一些子序列，那么最后我们将找到 dp[i][k]的最大值，即对于每个‘I’，如果 k 长度的子序列导致比更新所需 ans 更多的和。

**下面是实现代码:**

## C++

```
/*C++ program to calculate the maximum sum of
increasing subsequence of length k*/
#include <bits/stdc++.h>
using namespace std;
int MaxIncreasingSub(int arr[], int n, int k)
{
    // In the implementation dp[n][k] represents
    // maximum sum subsequence of length k and the
    // subsequence is ending at index n.
    int dp[n][k + 1], ans = -1;

    // Initializing whole multidimensional
    // dp array with value -1
    memset(dp, -1, sizeof(dp));

    // For each ith position increasing subsequence
    // of length 1 is equal to that array ith value
    // so initializing dp[i][1] with that array value
    for (int i = 0; i < n; i++) {
        dp[i][1] = arr[i];
    }

    // Starting from 1st index as we have calculated
    // for 0th index. Computing optimized dp values
    // in bottom-up manner
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {

            // check for increasing subsequence
            if (arr[j] < arr[i]) {
                for (int l = 1; l <= k - 1; l++) {

                    // Proceed if value is pre calculated
                    if (dp[j][l] != -1) {

                        // Check for all the subsequences
                        // ending at any j<i and try including
                        // element at index i in them for
                        // some length l. Update the maximum
                        // value for every length.
                        dp[i][l + 1] = max(dp[i][l + 1],
                                          dp[j][l] + arr[i]);
                    }
                }
            }
        }
    }

    // The final result would be the maximum
    // value of dp[i][k] for all different i.
    for (int i = 0; i < n; i++) {
        if (ans < dp[i][k])
            ans = dp[i][k];
    }

    // When no subsequence of length k is
    // possible sum would be considered zero
    return (ans == -1) ? 0 : ans;
}

// Driver function
int main()
{
    int n = 8, k = 3;
    int arr[n] = { 8, 5, 9, 10, 5, 6, 21, 8 };
    int ans = MaxIncreasingSub(arr, n, k);
    cout << ans << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*Java program to calculate the maximum sum of
increasing subsequence of length k*/
import java.util.*;

class GFG
{

static int MaxIncreasingSub(int arr[], int n, int k)
{
    // In the implementation dp[n][k] represents
    // maximum sum subsequence of length k and the
    // subsequence is ending at index n.
    int dp[][]=new int[n][k + 1], ans = -1;

    // Initializing whole multidimensional
    // dp array with value -1
    for(int i = 0; i < n; i++)
        for(int j = 0; j < k + 1; j++)
            dp[i][j]=-1;

    // For each ith position increasing subsequence
    // of length 1 is equal to that array ith value
    // so initializing dp[i][1] with that array value
    for (int i = 0; i < n; i++)
    {
        dp[i][1] = arr[i];
    }

    // Starting from 1st index as we have calculated
    // for 0th index. Computing optimized dp values
    // in bottom-up manner
    for (int i = 1; i < n; i++)
    {
        for (int j = 0; j < i; j++)
        {

            // check for increasing subsequence
            if (arr[j] < arr[i])
            {
                for (int l = 1; l <= k - 1; l++)
                {

                    // Proceed if value is pre calculated
                    if (dp[j][l] != -1)
                    {

                        // Check for all the subsequences
                        // ending at any j<i and try including
                        // element at index i in them for
                        // some length l. Update the maximum
                        // value for every length.
                        dp[i][l + 1] = Math.max(dp[i][l + 1],
                                        dp[j][l] + arr[i]);
                    }
                }
            }
        }
    }

    // The final result would be the maximum
    // value of dp[i][k] for all different i.
    for (int i = 0; i < n; i++)
    {
        if (ans < dp[i][k])
            ans = dp[i][k];
    }

    // When no subsequence of length k is
    // possible sum would be considered zero
    return (ans == -1) ? 0 : ans;
}

// Driver code
public static void main(String args[])
{
    int n = 8, k = 3;
    int arr[] = { 8, 5, 9, 10, 5, 6, 21, 8 };
    int ans = MaxIncreasingSub(arr, n, k);
    System.out.println(ans );

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python program to calculate the maximum sum
# of increasing subsequence of length k

def MaxIncreasingSub(arr, n, k):

    # In the implementation dp[n][k] represents
    # maximum sum subsequence of length k and the
    # subsequence is ending at index n.
    dp = [-1]*n
    ans = -1

    # Initializing whole multidimensional
    # dp array with value - 1
    for i in range(n):
        dp[i] = [-1]*(k+1)

    # For each ith position increasing subsequence
    # of length 1 is equal to that array ith value
    # so initializing dp[i][1] with that array value
    for i in range(n):
        dp[i][1] = arr[i]

    # Starting from 1st index as we have calculated
    # for 0th index. Computing optimized dp values
    # in bottom-up manner
    for i in range(1,n):
        for j in range(i):

            # check for increasing subsequence
            if arr[j] < arr[i]:
                for l in range(1,k):

                    # Proceed if value is pre calculated
                    if dp[j][l] != -1:

                        # Check for all the subsequences
                        # ending at any j < i and try including
                        # element at index i in them for
                        # some length l. Update the maximum
                        # value for every length.
                        dp[i][l+1] = max(dp[i][l+1],
                                        dp[j][l] + arr[i])

    # The final result would be the maximum
    # value of dp[i][k] for all different i.
    for i in range(n):
        if ans < dp[i][k]:
            ans = dp[i][k]

    # When no subsequence of length k is
    # possible sum would be considered zero
    return (0 if ans == -1 else ans)

# Driver Code
if __name__ == "__main__":

    n, k = 8, 3
    arr = [8, 5, 9, 10, 5, 6, 21, 8]
    ans = MaxIncreasingSub(arr, n, k)
    print(ans)

# This code is contributed by
# sanjeev2552
```

## C#

```
/*C# program to calculate the maximum sum of
increasing subsequence of length k*/
using System;

class GFG
{

static int MaxIncreasingSub(int []arr, int n, int k)
{
    // In the implementation dp[n,k] represents
    // maximum sum subsequence of length k and the
    // subsequence is ending at index n.
    int [,]dp=new int[n, k + 1];
    int ans = -1;

    // Initializing whole multidimensional
    // dp array with value -1
    for(int i = 0; i < n; i++)
        for(int j = 0; j < k + 1; j++)
            dp[i, j]=-1;

    // For each ith position increasing subsequence
    // of length 1 is equal to that array ith value
    // so initializing dp[i,1] with that array value
    for (int i = 0; i < n; i++)
    {
        dp[i, 1] = arr[i];
    }

    // Starting from 1st index as we have calculated
    // for 0th index. Computing optimized dp values
    // in bottom-up manner
    for (int i = 1; i < n; i++)
    {
        for (int j = 0; j < i; j++)
        {

            // check for increasing subsequence
            if (arr[j] < arr[i])
            {
                for (int l = 1; l <= k - 1; l++)
                {

                    // Proceed if value is pre calculated
                    if (dp[j, l] != -1)
                    {

                        // Check for all the subsequences
                        // ending at any j<i and try including
                        // element at index i in them for
                        // some length l. Update the maximum
                        // value for every length.
                        dp[i, l + 1] = Math.Max(dp[i, l + 1],
                                        dp[j, l] + arr[i]);
                    }
                }
            }
        }
    }

    // The final result would be the maximum
    // value of dp[i,k] for all different i.
    for (int i = 0; i < n; i++)
    {
        if (ans < dp[i, k])
            ans = dp[i, k];
    }

    // When no subsequence of length k is
    // possible sum would be considered zero
    return (ans == -1) ? 0 : ans;
}

// Driver code
public static void Main(String []args)
{
    int n = 8, k = 3;
    int []arr = { 8, 5, 9, 10, 5, 6, 21, 8 };
    int ans = MaxIncreasingSub(arr, n, k);
    Console.WriteLine(ans );
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to calculate the
// maximum sum of increasing subsequence
// of length k
function MaxIncreasingSub(arr, n, k)
{

    // In the implementation dp[n][k]
    // represents maximum sum subsequence
    // of length k and the subsequence is
    // ending at index n.
    let dp = new Array(n);
    for(let i = 0; i < dp.length; i++)
    {
        dp[i] = new Array(2);
    }
    let ans = -1;

    // Initializing whole multidimensional
    // dp array with value -1
    for(let i = 0; i < n; i++)
        for(let j = 0; j < k + 1; j++)
            dp[i][j] = -1;

    // For each ith position increasing
    // subsequence of length 1 is equal
    // to that array ith value so
    // initializing dp[i][1] with that
    // array value
    for(let i = 0; i < n; i++)
    {
        dp[i][1] = arr[i];
    }

    // Starting from 1st index as we
    // have calculated for 0th index.
    // Computing optimized dp values
    // in bottom-up manner
    for(let i = 1; i < n; i++)
    {
        for(let j = 0; j < i; j++)
        {

            // Check for increasing subsequence
            if (arr[j] < arr[i])
            {
                for(let l = 1; l <= k - 1; l++)
                {

                    // Proceed if value is pre calculated
                    if (dp[j][l] != -1)
                    {

                        // Check for all the subsequences
                        // ending at any j<i and try including
                        // element at index i in them for
                        // some length l. Update the maximum
                        // value for every length.
                        dp[i][l + 1] = Math.max(dp[i][l + 1],
                                                dp[j][l] +
                                               arr[i]);
                    }
                }
            }
        }
    }

    // The final result would be the maximum
    // value of dp[i][k] for all different i.
    for(let i = 0; i < n; i++)
    {
        if (ans < dp[i][k])
            ans = dp[i][k];
    }

    // When no subsequence of length k is
    // possible sum would be considered zero
    return(ans == -1) ? 0 : ans;
}

// Driver Code
let n = 8, k = 3;
let arr = [ 8, 5, 9, 10, 5, 6, 21, 8 ];
let ans = MaxIncreasingSub(arr, n, k);

document.write(ans);

// This code is contributed by code_hunt

</script>
```

**Output:** 

```
40
```

**时间复杂度:**o(n^2*k)
T3】空间复杂度: O(n^2)