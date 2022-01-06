# 最大化不属于最长递增子序列的所有元素的总和

> 原文:[https://www . geeksforgeeks . org/最大化所有元素的总和-不是最长递增子序列的一部分/](https://www.geeksforgeeks.org/maximize-sum-of-all-elements-which-are-not-a-part-of-the-longest-increasing-subsequence/)

给定一个数组 **arr[]** ，任务是找出不属于最长递增子序列的所有元素的最大和。

**示例:**

> **输入:** arr[] = {4，6，1，2，3，8}
> **输出:** 10
> **说明:**
> 元素为 4 和 6
> 
> **输入:** arr[] = {5，4，3，2，1}
> **输出:** 14
> **说明:**
> 元素为 5，4，3，2

**进场:**

*   其思想是用最小和找到最长的递增子序列，然后从所有元素的和中减去它。
*   为此，我们将使用 [LIS 的概念，使用动态编程](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)，存储总和以及子序列的长度，并相应地更新最小总和。

下面是上述方法的实现。

## C++

```
// C++ program to find the Maximum sum of
// all elements which are not a part of
// longest increasing sub sequence

#include <bits/stdc++.h>
using namespace std;

// Function to find maximum sum
int findSum(int* arr, int n)
{
    int totalSum = 0;

    // Find total sum of array
    for (int i = 0; i < n; i++) {
        totalSum += arr[i];
    }

    // Maintain a 2D array
    int dp[2][n];
    for (int i = 0; i < n; i++) {
        dp[0][i] = 1;
        dp[1][i] = arr[i];
    }

    // Update the dp array along
    // with sum in the second row
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (arr[i] > arr[j]) {
                // In case of greater length
                // Update the length along
                // with sum
                if (dp[0][i] < dp[0][j] + 1) {
                    dp[0][i] = dp[0][j] + 1;
                    dp[1][i] = dp[1][j]
                               + arr[i];
                }

                // In case of equal length
                // find length update length
                // with minimum sum
                else if (dp[0][i]
                         == dp[0][j] + 1) {
                    dp[1][i]
                        = min(dp[1][i],
                              dp[1][j]
                                  + arr[i]);
                }
            }
        }
    }
    int maxm = 0;
    int subtractSum = 0;

    // Find the sum that need to
    // be subtracted from total sum
    for (int i = 0; i < n; i++) {
        if (dp[0][i] > maxm) {
            maxm = dp[0][i];
            subtractSum = dp[1][i];
        }
        else if (dp[0][i] == maxm) {
            subtractSum = min(subtractSum,
                              dp[1][i]);
        }
    }

    // Return the sum
    return totalSum - subtractSum;
}

// Driver code
int main()
{
    int arr[] = { 4, 6, 1, 2, 3, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Maximum sum of
// all elements which are not a part of
// longest increasing sub sequence
class GFG{

// Function to find maximum sum
static int findSum(int []arr, int n)
{
    int totalSum = 0;

    // Find total sum of array
    for(int i = 0; i < n; i++)
    {
       totalSum += arr[i];
    }

    // Maintain a 2D array
    int [][]dp = new int[2][n];
    for(int i = 0; i < n; i++)
    {
       dp[0][i] = 1;
       dp[1][i] = arr[i];
    }

    // Update the dp array along
    // with sum in the second row
    for(int i = 1; i < n; i++)
    {
       for(int j = 0; j < i; j++)
       {
          if (arr[i] > arr[j])
          {

              // In case of greater length
              // Update the length along
              // with sum
              if (dp[0][i] < dp[0][j] + 1)
              {
                  dp[0][i] = dp[0][j] + 1;
                  dp[1][i] = dp[1][j] + arr[i];
              }

              // In case of equal length
              // find length update length
              // with minimum sum
              else if (dp[0][i] == dp[0][j] + 1)
              {
                  dp[1][i] = Math.min(dp[1][i],
                                      dp[1][j] + arr[i]);
              }
          }
       }
    }
    int maxm = 0;
    int subtractSum = 0;

    // Find the sum that need to
    // be subtracted from total sum
    for(int i = 0; i < n; i++)
    {
       if (dp[0][i] > maxm)
       {
           maxm = dp[0][i];
           subtractSum = dp[1][i];
       }
       else if (dp[0][i] == maxm)
       {
           subtractSum = Math.min(subtractSum, dp[1][i]);
       }
    }

    // Return the sum
    return totalSum - subtractSum;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 6, 1, 2, 3, 8 };
    int n = arr.length;

    System.out.print(findSum(arr, n));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to find the maximum sum 
# of all elements which are not a part of
# longest increasing sub sequence

# Function to find maximum sum
def findSum(arr, n):

    totalSum = 0

    # Find total sum of array
    for i in range(n):
        totalSum += arr[i]

    # Maintain a 2D array
    dp = [[0] * n for i in range(2)]

    for i in range(n):
        dp[0][i] = 1
        dp[1][i] = arr[i]

    # Update the dp array along
    # with sum in the second row
    for i in range(1, n):
        for j in range(i):
            if (arr[i] > arr[j]):

                # In case of greater length
                # update the length along
                # with sum
                if (dp[0][i] < dp[0][j] + 1):
                    dp[0][i] = dp[0][j] + 1
                    dp[1][i] = dp[1][j] + arr[i]

                # In case of equal length
                # find length update length
                # with minimum sum
                elif (dp[0][i] == dp[0][j] + 1):
                    dp[1][i] = min(dp[1][i],
                                   dp[1][j] +
                                     arr[i])

    maxm = 0
    subtractSum = 0

    # Find the sum that need to
    # be subtracted from total sum
    for i in range(n):
        if (dp[0][i] > maxm):
            maxm = dp[0][i]
            subtractSum = dp[1][i]

        elif (dp[0][i] == maxm):
            subtractSum = min(subtractSum,
                              dp[1][i])

    # Return the sum
    return totalSum - subtractSum

# Driver code
arr = [ 4, 6, 1, 2, 3, 8 ]
n = len(arr)

print(findSum(arr, n))

# This code is contributed by himanshu77
```

## C#

```
// C# program to find the Maximum sum of
// all elements which are not a part of
// longest increasing sub sequence
using System;
class GFG{

// Function to find maximum sum
static int findSum(int []arr, int n)
{
    int totalSum = 0;

    // Find total sum of array
    for(int i = 0; i < n; i++)
    {
        totalSum += arr[i];
    }

    // Maintain a 2D array
    int [,]dp = new int[2, n];
    for(int i = 0; i < n; i++)
    {
        dp[0, i] = 1;
        dp[1, i] = arr[i];
    }

    // Update the dp array along
    // with sum in the second row
    for(int i = 1; i < n; i++)
    {
        for(int j = 0; j < i; j++)
        {
            if (arr[i] > arr[j])
            {

                // In case of greater length
                // Update the length along
                // with sum
                if (dp[0, i] < dp[0, j] + 1)
                {
                    dp[0, i] = dp[0, j] + 1;
                    dp[1, i] = dp[1, j] + arr[i];
                }

                // In case of equal length
                // find length update length
                // with minimum sum
                else if (dp[0, i] == dp[0, j] + 1)
                {
                    dp[1, i] = Math.Min(dp[1, i],
                                        dp[1, j] + arr[i]);
                }
            }
        }
    }
    int maxm = 0;
    int subtractSum = 0;

    // Find the sum that need to
    // be subtracted from total sum
    for(int i = 0; i < n; i++)
    {
        if (dp[0, i] > maxm)
        {
            maxm = dp[0, i];
            subtractSum = dp[1, i];
        }
        else if (dp[0, i] == maxm)
        {
            subtractSum = Math.Min(subtractSum, dp[1, i]);
        }
    }

    // Return the sum
    return totalSum - subtractSum;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 6, 1, 2, 3, 8 };
    int n = arr.Length;

    Console.Write(findSum(arr, n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to find the Maximum sum of
// all elements which are not a part of
// longest increasing sub sequence

// Function to find maximum sum
function findSum(arr, n)
{
    var totalSum = 0;

    // Find total sum of array
    for(var i = 0; i < n; i++)
    {
        totalSum += arr[i];
    }

    // Maintain a 2D array
    var dp = Array.from(Array(2), () => Array(n));
    for(var i = 0; i < n; i++)
    {
        dp[0][i] = 1;
        dp[1][i] = arr[i];
    }

    // Update the dp array along
    // with sum in the second row
    for(var i = 1; i < n; i++)
    {
        for(var j = 0; j < i; j++)
        {
            if (arr[i] > arr[j])
            {

                // In case of greater length
                // Update the length along
                // with sum
                if (dp[0][i] < dp[0][j] + 1)
                {
                    dp[0][i] = dp[0][j] + 1;
                    dp[1][i] = dp[1][j] + arr[i];
                }

                // In case of equal length
                // find length update length
                // with minimum sum
                else if (dp[0][i] == dp[0][j] + 1)
                {
                    dp[1][i] = Math.min(dp[1][i],
                               dp[1][j] + arr[i]);
                }
            }
        }
    }
    var maxm = 0;
    var subtractSum = 0;

    // Find the sum that need to
    // be subtracted from total sum
    for(var i = 0; i < n; i++)
    {
        if (dp[0][i] > maxm)
        {
            maxm = dp[0][i];
            subtractSum = dp[1][i];
        }
        else if (dp[0][i] == maxm)
        {
            subtractSum = Math.min(subtractSum,
                                   dp[1][i]);
        }
    }

    // Return the sum
    return totalSum - subtractSum;
}

// Driver code
var arr = [ 4, 6, 1, 2, 3, 8 ];
var n = arr.length;

document.write( findSum(arr, n));

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(N <sup>2</sup> )其中 N 是数组 arr 的长度[]*
***辅助空间:** O(N)*