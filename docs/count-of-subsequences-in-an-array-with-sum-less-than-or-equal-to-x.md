# 总和小于或等于 X 的数组中子序列的计数

> 原文:[https://www . geeksforgeeks . org/总和小于或等于 x 的数组中子序列计数/](https://www.geeksforgeeks.org/count-of-subsequences-in-an-array-with-sum-less-than-or-equal-to-x/)

给定一个大小为 **N** 的整数数组 **arr[]** 和一个整数 **X** ，任务是计算该数组中子序列的数量，使其和小于或等于 **X** 。
**注:**1<=**N**<= 1000，1 < = **X** < = 1000，其中 **N** 为数组大小。

**示例:**

> **输入:** arr[] = {84，87，73}，X = 100
> **输出:** 3
> **说明:**和小于等于 100 的三个子序列分别为{84}、{87}和{73}。
> 
> **输入:** arr[] = {25，13，40}，X = 50
> **输出:** 4
> **说明:**和小于等于 50 的四个子序列分别为{25}、{13}、{40}和{25，13}。

**天真方法:**生成数组的所有子序列，检查总和是否小于或等于 X.
***时间复杂度:** O(2 <sup>N</sup> )*

**有效方法:**使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)生成子序列的计数。为了解决问题，请按照以下步骤操作:

*   对于任何索引 **ind** ，如果***arr【ind】**≤**X***，则包括和不包括当前索引处元素的子序列计数:

> ***count subseries(ind，X)*****=*****count subseries(ind+1，X)*** (不含)+***count subseries(ind+1，X–arr[ind])***(含)

*   否则，计算不包括当前索引的子序列:

> ***count subseries(ind，X)*****=*****count subseries(ind+1，X)*** (不含)

*   最后，从函数返回的最终计数中减去 1，因为它也计算一个空的子序列。

下面是上述方法的实现:

## C++

```
// C++ Program to count number
// of subsequences in an array
// with sum less than or equal to X
#include <bits/stdc++.h>
using namespace std;

// Utility function to return the count
// of subsequence in an array with sum
// less than or equal to X
int countSubsequenceUtil(
    int ind, int sum,
    int* A, int N,
    vector<vector<int> >& dp)
{
    // Base condition
    if (ind == N)
        return 1;

    // Return if the sub-problem
    // is already calculated
    if (dp[ind][sum] != -1)
        return dp[ind][sum];

    // Check if the current element is
    // less than or equal to sum
    if (A[ind] <= sum) {
        // Count subsequences excluding
        // the current element
        dp[ind][sum]
            = countSubsequenceUtil(
                  ind + 1,
                  sum, A, N, dp)
              +

              // Count subsequences including
              // the current element
              countSubsequenceUtil(
                  ind + 1,
                  sum - A[ind],
                  A, N, dp);
    }

    else {
        // Exclude current element
        dp[ind][sum]
            = countSubsequenceUtil(
                ind + 1,
                sum, A,
                N, dp);
    }

    // Return the result
    return dp[ind][sum];
}

// Function to return the count of subsequence
// in an array with sum less than or equal to X
int countSubsequence(int* A, int N, int X)
{
    // Initialize a DP array
    vector<vector<int> > dp(
        N,
        vector<int>(X + 1, -1));

    // Return the result
    return countSubsequenceUtil(0, X, A,
                                N, dp)
           - 1;
}

// Driver Code
int main()
{
    int arr[] = { 25, 13, 40 }, X = 50;

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << countSubsequence(arr, N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number
// of subsequences in an array
// with sum less than or equal to X
class GFG{

// Utility function to return the count
// of subsequence in an array with sum
// less than or equal to X
static int countSubsequenceUtil(int ind, int sum,
                                int []A, int N,
                                int [][]dp)
{

    // Base condition
    if (ind == N)
        return 1;

    // Return if the sub-problem
    // is already calculated
    if (dp[ind][sum] != -1)
        return dp[ind][sum];

    // Check if the current element is
    // less than or equal to sum
    if (A[ind] <= sum)
    {

        // Count subsequences excluding
        // the current element
        dp[ind][sum] = countSubsequenceUtil(
                           ind + 1, sum,
                           A, N, dp) +

                       // Count subsequences
                       // including the current
                       // element
                       countSubsequenceUtil(
                           ind + 1,
                           sum - A[ind],
                           A, N, dp);
    }
    else
    {

        // Exclude current element
        dp[ind][sum] = countSubsequenceUtil(
                           ind + 1, sum,
                           A, N, dp);
    }

    // Return the result
    return dp[ind][sum];
}

// Function to return the count of subsequence
// in an array with sum less than or equal to X
static int countSubsequence(int[] A, int N, int X)
{

    // Initialize a DP array
    int [][]dp = new int[N][X + 1];
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < X + 1; j++)
        {
            dp[i][j] = -1;
        }
    }

    // Return the result
    return countSubsequenceUtil(0, X, A,
                                N, dp) - 1;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 25, 13, 40 }, X = 50;
    int N = arr.length;

    System.out.print(countSubsequence(arr, N, X));
}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program to count number
// of subsequences in an array
// with sum less than or equal to X
using System;

class GFG{

// Utility function to return the count
// of subsequence in an array with sum
// less than or equal to X
static int countSubsequenceUtil(int ind, int sum,
                                int []A, int N,
                                int [,]dp)
{

    // Base condition
    if (ind == N)
        return 1;

    // Return if the sub-problem
    // is already calculated
    if (dp[ind, sum] != -1)
        return dp[ind, sum];

    // Check if the current element is
    // less than or equal to sum
    if (A[ind] <= sum)
    {

        // Count subsequences excluding
        // the current element
        dp[ind, sum] = countSubsequenceUtil(
                           ind + 1, sum,
                           A, N, dp) +

                       // Count subsequences
                       // including the current
                       // element
                       countSubsequenceUtil(
                           ind + 1,
                           sum - A[ind],
                           A, N, dp);
    }
    else
    {

        // Exclude current element
        dp[ind, sum] = countSubsequenceUtil(
                           ind + 1, sum,
                           A, N, dp);
    }

    // Return the result
    return dp[ind, sum];
}

// Function to return the count of subsequence
// in an array with sum less than or equal to X
static int countSubsequence(int[] A, int N, int X)
{

    // Initialize a DP array
    int [,]dp = new int[N, X + 1];
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < X + 1; j++)
        {
            dp[i, j] = -1;
        }
    }

    // Return the result
    return countSubsequenceUtil(0, X, A,
                                N, dp) - 1;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 25, 13, 40 };
    int X = 50;
    int N = arr.Length;

    Console.Write(countSubsequence(arr, N, X));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to count number
// of subsequences in an array
// with sum less than or equal to X

// Utility function to return the count
// of subsequence in an array with sum
// less than or equal to X
function countSubsequenceUtil(ind, sum, A, N, dp)
{

    // Base condition
    if (ind == N)
        return 1;

    // Return if the sub-problem
    // is already calculated
    if (dp[ind][sum] != -1)
        return dp[ind][sum];

    // Check if the current element is
    // less than or equal to sum
    if (A[ind] <= sum)
    {

        // Count subsequences excluding
        // the current element
        dp[ind][sum] = countSubsequenceUtil(
                           ind + 1, sum,
                           A, N, dp) +

                       // Count subsequences
                       // including the current
                       // element
                       countSubsequenceUtil(
                           ind + 1,
                           sum - A[ind],
                           A, N, dp);
    }
    else
    {

        // Exclude current element
        dp[ind][sum] = countSubsequenceUtil(
                           ind + 1, sum,
                           A, N, dp);
    }

    // Return the result
    return dp[ind][sum];
}

// Function to return the count of subsequence
// in an array with sum less than or equal to X
function countSubsequence(A, N, X)
{

    // Initialize a DP array
    let dp = new Array(N);
    for(var i = 0; i < dp.length; i++)
    {
        dp[i] = new Array(2);
    }

    for(let i = 0; i < N; i++)
    {
        for(let j = 0; j < X + 1; j++)
        {
            dp[i][j] = -1;
        }
    }

    // Return the result
    return countSubsequenceUtil(0, X, A,
                                N, dp) - 1;
}

// Driver Code
let arr = [ 25, 13, 40 ], X = 50;
let N = arr.length;

document.write(countSubsequence(arr, N, X));

// This code is contributed by susmitakundugoaldanga

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*X)*

***辅助空间:**O(N * X)*T4】