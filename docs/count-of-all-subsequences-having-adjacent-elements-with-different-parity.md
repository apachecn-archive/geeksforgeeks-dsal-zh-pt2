# 具有不同奇偶性的相邻元素的所有子序列的计数

> 原文:[https://www . geeksforgeeks . org/所有子序列的计数-具有不同奇偶校验的相邻元素/](https://www.geeksforgeeks.org/count-of-all-subsequences-having-adjacent-elements-with-different-parity/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是从给定的数组中找到非空子序列的数量，使得子序列中没有两个相邻的元素具有相同的**奇偶性**。

**示例:**

> **输入:**arr[]=【5，6，9，7】
> **输出:** 9
> **解释:**
> 给定数组的所有这样的子序列将是 **{5}、{6}、{9}、{7}、{5，6}、{6，7}、{6，9}、{5，6，9}、{5，6，7}** 。
> **输入:** arr[] = [2，3，4，8]
> **输出:** 9

**天真法:**生成所有非空子序列，选择具有交替的**奇偶**或**奇偶**数的子序列，对所有这样的子序列进行计数，得到答案。
***时间复杂度:**O(2<sup>N</sup>)*
**高效途径:**
以上途径可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。按照以下步骤解决问题:

*   考虑尺寸矩阵 **(N+1)*(2)** 。
*   **dp[i][0]** 存储子序列的计数，直到以**甚至**元素结束的 **i <sup>第</sup>索引**。
*   **dp[i][1]** 存储子序列的计数，直到以**奇数**元素结束的 **i <sup>第</sup>索引**。
*   因此，对于每个 **i <sup>第</sup>元素**，检查该元素是偶数还是奇数，并通过包括和排除 **i <sup>第</sup>元素**来继续。
*   因此，如果第 i <sup>个</sup>元素是奇数，则递归关系为:

> DP[I][1]= DP[I–1][0](通过考虑以偶数元素结尾的所有子序列直到(I–1)<sup>第</sup>索引)+1+DP[I–1][1](不包括第 i <sup>第</sup>元素)来包括第 i <sup>元素)</sup>

*   类似地，如果第 i <sup>个</sup>元素是偶数:

> DP[I][0]= DP[I–1][1](通过考虑所有以奇数元素结尾的子序列直到(I–1)<sup>第</sup>索引)+1+DP[I–1][0](不包括 i <sup>第</sup>元素)来包括 i <sup>第</sup>元素)

*   最后，包含所有以偶数元素结尾的子序列的 dp[n][0]和包含所有以奇数元素结尾的子序列的 dp[n][1]的和就是需要的答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find required subsequences
int validsubsequences(int arr[], int n)
{
    // dp[i][0]: Stores the number of
    // subsequences till i-th index
    // ending with even element
    // dp[i][1]: Stores the number of
    // subsequences till i-th index
    // ending with odd element
    long long int dp[n + 1][2];

    // Initialise the dp[][] with 0.
    for (int i = 0; i < n + 1; i++) {
        dp[i][0] = 0;
        dp[i][1] = 0;
    }

    for (int i = 1; i <= n; i++) {

        // If odd element is
        // encountered
        if (arr[i - 1] % 2) {

            // Considering i-th element
            // will be present in
            // the subsequence
            dp[i][1] += 1;

            // Appending i-th element to all
            // non-empty subsequences
            // ending with even element
            // till (i-1)th indexes
            dp[i][1] += dp[i - 1][0];

            // Considering ith element will
            // not be present in
            // the subsequence
            dp[i][1] += dp[i - 1][1];

            dp[i][0] += dp[i - 1][0];
        }
        else {

            // Considering i-th element
            // will be present in
            // the subsequence
            dp[i][0] += 1;

            // Appending i-th element to all
            // non-empty subsequences
            // ending with odd element
            // till (i-1)th indexes
            dp[i][0] += dp[i - 1][1];

            // Considering ith element will
            // not be present in
            // the subsequence
            dp[i][0] += dp[i - 1][0];
            dp[i][1] += dp[i - 1][1];
        }
    }

    // Count of all valid subsequences
    return dp[n][0] + dp[n][1];
}

// Driver Code
int main()
{
    int arr[] = { 5, 6, 9, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << validsubsequences(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program implementation
// of the approach
import java.util.*;
import java.io.*;

class GFG{

// Function to find required subsequences    
static int validsubsequences(int arr[], int n)
{

    // dp[i][0]: Stores the number of
    // subsequences till i-th index
    // ending with even element
    // dp[i][1]: Stores the number of
    // subsequences till i-th index
    // ending with odd element
    long dp[][] = new long [n + 1][2];

    // Initialise the dp[][] with 0.
    for(int i = 0; i < n + 1; i++)
    {
        dp[i][0] = 0;
        dp[i][1] = 0;
    }

    for(int i = 1; i <= n; i++)
    {

        // If odd element is
        // encountered
        if (arr[i - 1] % 2 != 0)
        {

            // Considering i-th element
            // will be present in
            // the subsequence
            dp[i][1] += 1;

            // Appending i-th element to all
            // non-empty subsequences
            // ending with even element
            // till (i-1)th indexes
            dp[i][1] += dp[i - 1][0];

            // Considering ith element will
            // not be present in
            // the subsequence
            dp[i][1] += dp[i - 1][1];
            dp[i][0] += dp[i - 1][0];
        }
        else
        {

            // Considering i-th element
            // will be present in
            // the subsequence
            dp[i][0] += 1;

            // Appending i-th element to all
            // non-empty subsequences
            // ending with odd element
            // till (i-1)th indexes
            dp[i][0] += dp[i - 1][1];

            // Considering ith element will
            // not be present in
            // the subsequence
            dp[i][0] += dp[i - 1][0];
            dp[i][1] += dp[i - 1][1];
        }
    }

    // Count of all valid subsequences
    return (int)(dp[n][0] + dp[n][1]);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 5, 6, 9, 7 };
    int n = arr.length;

    System.out.print(validsubsequences(arr, n));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach

# Function to find required subsequences
def validsubsequences(arr, n):

    # dp[i][0]: Stores the number of
    # subsequences till i-th index
    # ending with even element
    # dp[i][1]: Stores the number of
    # subsequences till i-th index
    # ending with odd element

    # Initialise the dp[][] with 0.
    dp = [[0 for i in range(2)]
             for j in range(n + 1)]

    for i in range(1, n + 1):

        # If odd element is
        # encountered
        if(arr[i - 1] % 2):

            # Considering i-th element
            # will be present in
            # the subsequence
            dp[i][1] += 1

            # Appending i-th element to all
            # non-empty subsequences
            # ending with even element
            # till (i-1)th indexes
            dp[i][1] += dp[i - 1][0]

            # Considering ith element will
            # not be present in
            # the subsequence
            dp[i][1] += dp[i - 1][1]
            dp[i][0] += dp[i - 1][0]

        else:

            # Considering i-th element
            # will be present in
            # the subsequence
            dp[i][0] += 1

            # Appending i-th element to all
            # non-empty subsequences
            # ending with odd element
            # till (i-1)th indexes
            dp[i][0] += dp[i - 1][1]

            # Considering ith element will
            # not be present in
            # the subsequence
            dp[i][0] += dp[i - 1][0]
            dp[i][1] += dp[i - 1][1]

    # Count of all valid subsequences
    return dp[n][0] + dp[n][1]

# Driver code
if __name__ == '__main__':

    arr = [ 5, 6, 9, 7 ]
    n = len(arr)

    print(validsubsequences(arr, n))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program implementation
// of the approach
using System;

class GFG{

// Function to find required subsequences    
static int validsubsequences(int[] arr, int n)
{

    // dp[i][0]: Stores the number of
    // subsequences till i-th index
    // ending with even element
    // dp[i][1]: Stores the number of
    // subsequences till i-th index
    // ending with odd element
    long[,] dp = new long [n + 1, 2];

    // Initialise the dp[][] with 0.
    for(int i = 0; i < n + 1; i++)
    {
        dp[i, 0] = 0;
        dp[i, 1] = 0;
    }

    for(int i = 1; i <= n; i++)
    {

        // If odd element is
        // encountered
        if (arr[i - 1] % 2 != 0)
        {

            // Considering i-th element
            // will be present in
            // the subsequence
            dp[i, 1] += 1;

            // Appending i-th element to all
            // non-empty subsequences
            // ending with even element
            // till (i-1)th indexes
            dp[i, 1] += dp[i - 1, 0];

            // Considering ith element will
            // not be present in
            // the subsequence
            dp[i, 1] += dp[i - 1, 1];
            dp[i, 0] += dp[i - 1, 0];
        }
        else
        {

            // Considering i-th element
            // will be present in
            // the subsequence
            dp[i, 0] += 1;

            // Appending i-th element to all
            // non-empty subsequences
            // ending with odd element
            // till (i-1)th indexes
            dp[i, 0] += dp[i - 1, 1];

            // Considering ith element will
            // not be present in
            // the subsequence
            dp[i, 0] += dp[i - 1, 0];
            dp[i, 1] += dp[i - 1, 1];
        }
    }

    // Count of all valid subsequences
    return (int)(dp[n, 0] + dp[n, 1]);
}

// Driver code
public static void Main()
{
    int[] arr = { 5, 6, 9, 7 };
    int n = arr.Length;

    Console.Write(validsubsequences(arr, n));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find required subsequences    
function validsubsequences(arr, n)
{

    // dp[i][0]: Stores the number of
    // subsequences till i-th index
    // ending with even element
    // dp[i][1]: Stores the number of
    // subsequences till i-th index
    // ending with odd element
    let dp = new Array(n + 1);
    for (var i = 0; i < dp.length; i++) {
    dp[i] = new Array(2);
    }

    // Initialise the dp[][] with 0.
    for(let i = 0; i < n + 1; i++)
    {
        dp[i][0] = 0;
        dp[i][1] = 0;
    }

    for(let i = 1; i <= n; i++)
    {

        // If odd element is
        // encountered
        if (arr[i - 1] % 2 != 0)
        {

            // Considering i-th element
            // will be present in
            // the subsequence
            dp[i][1] += 1;

            // Appending i-th element to all
            // non-empty subsequences
            // ending with even element
            // till (i-1)th indexes
            dp[i][1] += dp[i - 1][0];

            // Considering ith element will
            // not be present in
            // the subsequence
            dp[i][1] += dp[i - 1][1];
            dp[i][0] += dp[i - 1][0];
        }
        else
        {

            // Considering i-th element
            // will be present in
            // the subsequence
            dp[i][0] += 1;

            // Appending i-th element to all
            // non-empty subsequences
            // ending with odd element
            // till (i-1)th indexes
            dp[i][0] += dp[i - 1][1];

            // Considering ith element will
            // not be present in
            // the subsequence
            dp[i][0] += dp[i - 1][0];
            dp[i][1] += dp[i - 1][1];
        }
    }

    // Count of all valid subsequences
    return (dp[n][0] + dp[n][1]);
}

// Driver Code

    let arr = [ 5, 6, 9, 7 ];
    let n = arr.length;

    document.write(validsubsequences(arr, n));

</script>
```

**Output:** 

```
9
```

***时间复杂度:** O(N)*
***辅助空间复杂度:** O(N)*