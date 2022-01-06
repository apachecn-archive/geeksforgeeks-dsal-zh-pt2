# 仅允许一次插入操作时最长的连续子序列

> 原文:[https://www . geeksforgeeks . org/long-consecuetive-subsequence-当只允许一个插入操作时/](https://www.geeksforgeeks.org/longest-consecuetive-subsequence-when-only-one-insert-operation-is-allowed/)

给定长度为 **N** 的正整数序列。唯一允许的操作是在序列中的任何位置插入任意值的单个整数。任务是找到包含递增顺序的连续值的最大长度的子序列。

**示例:**

> **输入:** arr[] = {2，1，4，5}
> **输出:** 4
> 在 3 <sup>rd</sup> 位置插入值为 3 的元素。(基于 1 的索引)
> 新序列变成{2，1，3，4，5}
> 最长的连续子序列将是{2，3，4，5}
> 
> **输入:** arr[] = {2，1，2，3，5，7 }
> T3】输出: 5

**方法:**思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。
让 **dp[val][0]** 成为所需子序列的长度，该子序列以等于 val 的元素结束，并且该元素尚未插入。假设 **dp[val][1]** 是所需子序列的长度，该子序列以等于 val 的元素结束，并且已经插入了某个元素。
现在将问题分解为如下子问题:
要计算 dp[val][0]，由于没有插入任何元素，子序列的长度将从之前的值
增加 1**DP[val][0]= 1+DP[val–1][0]**。

要计算 dp[val][1]，请考虑以下两种情况:

1.  当元素已经为(val-1)插入时，长度将从 dp[ val-1 ][ 1 ]增加 1
2.  当元素尚未插入时，可以插入值为(val-1)的元素。因此，从 dp[ val-2 ][ 0 ]开始，长度将增加 2。

以上两种情况取最大值。
**DP[val][1]= max(1+DP[val–1][1]，2+DP[val–2][0])**。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the length of longest
// consecuetive subsequence after inserting an element
int LongestConsSeq(int arr[], int N)
{

    // Variable to find maximum value of the array
    int maxval = 1;

    // Calculating maximum value of the array
    for (int i = 0; i < N; i += 1) {

        maxval = max(maxval, arr[i]);
    }

    // Declaring the DP table
    int dp[maxval + 1][2] = { 0 };

    // Variable to store the maximum length
    int ans = 1;

    // Iterating for every value present in the array
    for (int i = 0; i < N; i += 1) {

        // Recurrence for dp[val][0]
        dp[arr[i]][0] = (1 + dp[arr[i] - 1][0]);

        // No value can be inserted before 1,
        // hence the element value should be
        // greater than 1 for this recurrance relation
        if (arr[i] >= 2)

            // Recurrence for dp[val][1]
            dp[arr[i]][1] = max(1 + dp[arr[i] - 1][1],
                                2 + dp[arr[i] - 2][0]);
        else

            // Maximum length of consecutive sequence
            // ending at 1 is equal to 1
            dp[arr[i]][1] = 1;

        // Update the ans variable with
        // the new maximum length possible
        ans = max(ans, dp[arr[i]][1]);
    }

    // Return the ans
    return ans;
}

// Driver code
int main()
{
    // Input array
    int arr[] = { 2, 1, 4, 5 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << LongestConsSeq(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG
{
    // Function to return the length of longest
    // consecuetive subsequence after inserting an element
    static int LongestConsSeq(int [] arr, int N)
    {

        // Variable to find maximum value of the array
        int maxval = 1;

        // Calculating maximum value of the array
        for (int i = 0; i < N; i += 1)
        {
            maxval = Math. max(maxval, arr[i]);
        }

        // Declaring the DP table
        int [][] dp = new int[maxval + 1][2];

        // Variable to store the maximum length
        int ans = 1;

        // Iterating for every value present in the array
        for (int i = 0; i < N; i += 1)
        {

            // Recurrence for dp[val][0]
            dp[arr[i]][0] = (1 + dp[arr[i] - 1][0]);

            // No value can be inserted before 1,
            // hence the element value should be
            // greater than 1 for this recurrance relation
            if (arr[i] >= 2)

                // Recurrence for dp[val][1]
                dp[arr[i]][1] = Math.max(1 + dp[arr[i] - 1][1],
                                    2 + dp[arr[i] - 2][0]);
            else

                // Maximum length of consecutive sequence
                // ending at 1 is equal to 1
                dp[arr[i]][1] = 1;

            // Update the ans variable with
            // the new maximum length possible
            ans = Math.max(ans, dp[arr[i]][1]);
        }

        // Return the ans
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {

        // Input array
        int [] arr = { 2, 1, 4, 5 };

        int N = arr.length;

        System.out.println(LongestConsSeq(arr, N));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to return the length of longest
# consecuetive subsequence after inserting an element
def LongestConsSeq(arr, N):

    # Variable to find maximum value of the array
    maxval = 1

    # Calculating maximum value of the array
    for i in range(N):

        maxval = max(maxval, arr[i])

    # Declaring the DP table
    dp=[[ 0 for i in range(2)] for i in range(maxval + 1)]

    # Variable to store the maximum length
    ans = 1

    # Iterating for every value present in the array
    for i in range(N):

        # Recurrence for dp[val][0]
        dp[arr[i]][0] = 1 + dp[arr[i] - 1][0]

        # No value can be inserted before 1,
        # hence the element value should be
        # greater than 1 for this recurrance relation
        if (arr[i] >= 2):

            # Recurrence for dp[val][1]
            dp[arr[i]][1] = max(1 + dp[arr[i] - 1][1],
                                2 + dp[arr[i] - 2][0])
        else:

            # Maximum length of consecutive sequence
            # ending at 1 is equal to 1
            dp[arr[i]][1] = 1

        # Update the ans variable with
        # the new maximum length possible
        ans = max(ans, dp[arr[i]][1])

    # Return the ans
    return ans

# Driver code

arr=[2, 1, 4, 5]

N = len(arr)

print(LongestConsSeq(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
    // Function to return the length of longest
    // consecuetive subsequence after inserting an element
    static int LongestConsSeq(int [] arr, int N)
    {

        // Variable to find maximum value of the array
        int maxval = 1;

        // Calculating maximum value of the array
        for (int i = 0; i < N; i += 1)
        {

            maxval =Math.Max(maxval, arr[i]);
        }

        // Declaring the DP table
        int [ , ] dp = new int[maxval + 1, 2];

        // Variable to store the maximum length
        int ans = 1;

        // Iterating for every value present in the array
        for (int i = 0; i < N; i += 1)
        {

            // Recurrence for dp[val][0]
            dp[arr[i], 0] = (1 + dp[arr[i] - 1, 0]);

            // No value can be inserted before 1,
            // hence the element value should be
            // greater than 1 for this recurrance relation
            if (arr[i] >= 2)

                // Recurrence for dp[val][1]
                dp[arr[i], 1] = Math.Max(1 + dp[arr[i] - 1, 1],
                                    2 + dp[arr[i] - 2, 0]);
            else

                // Maximum length of consecutive sequence
                // ending at 1 is equal to 1
                dp[arr[i], 1] = 1;

            // Update the ans variable with
            // the new maximum length possible
            ans = Math.Max(ans, dp[arr[i], 1]);
        }

        // Return the ans
        return ans;
    }

    // Driver code
    public static void Main ()
    {

        // Input array
        int [] arr = new int [] { 2, 1, 4, 5 };

        int N = arr.Length;

        Console.WriteLine(LongestConsSeq(arr, N));
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to return the length of
// longest consecuetive subsequence
// after inserting an element
function LongestConsSeq(arr, N)
{

    // Variable to find maximum value of the array
    let maxval = 1;

    // Calculating maximum value of the array
    for(let i = 0; i < N; i += 1)
    {
        maxval = Math. max(maxval, arr[i]);
    }

    // Declaring the DP table
    let dp = new Array(maxval + 1);
      for(let i = 0; i < dp.length; i++)
    {
        dp[i] = new Array(2);
        for(let j = 0; j < 2; j++)
            dp[i][j] = 0;
    }

    // Variable to store the maximum length
    let ans = 1;

    // Iterating for every value present in the array
    for(let i = 0; i < N; i += 1)
    {

        // Recurrence for dp[val][0]
        dp[arr[i]][0] = (1 + dp[arr[i] - 1][0]);

        // No value can be inserted before 1,
        // hence the element value should be
        // greater than 1 for this recurrance relation
        if (arr[i] >= 2)

            // Recurrence for dp[val][1]
            dp[arr[i]][1] = Math.max(1 + dp[arr[i] - 1][1],
                                     2 + dp[arr[i] - 2][0]);
        else

            // Maximum length of consecutive sequence
            // ending at 1 is equal to 1
            dp[arr[i]][1] = 1;

        // Update the ans variable with
        // the new maximum length possible
        ans = Math.max(ans, dp[arr[i]][1]);
    }

    // Return the ans
    return ans;
}

// Driver code
let arr = [ 2, 1, 4, 5 ];
let N = arr.length;

document.write(LongestConsSeq(arr, N));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(N)
T3】空间复杂度: O(最大值)，其中最大值是数组中存在的最大值。