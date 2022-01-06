# 通过给子序列中的元素指定交替的正负符号而可能达到的最大总和

> 原文:[https://www . geesforgeks . org/通过将正负符号交替赋给子序列中的元素来获得最大可能总和/](https://www.geeksforgeeks.org/maximum-sum-possible-by-assigning-alternate-positive-and-negative-sign-to-elements-in-a-subsequence/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是从给定的数组中找到子序列的最大和，使得子序列中的元素交替被赋予正负符号。

> 子序列= {a，b，c，d，e，… }，
> 上述子序列之和=(a–b+ c–d+e–…)

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出** : 4
> **解释** :
> 具有最大和的子序列为{4}。
> 和为 4。
> 
> **输入** : arr[]= {1，2，3，4，1，2 }
> **输出** : 5
> **解释** :
> 具有最大和的子序列是{4，1，2 }。
> 总和= 4 -1 + 2 = 5。

**天真方法:**最简单的方法是[生成给定数组的所有子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，然后找到每个子序列的和，并打印所有子序列和中的最大值。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。初始化大小为 **N*2** 的辅助空间 **dp[][]** ，以存储[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。在每个[递归](https://www.geeksforgeeks.org/recursion/)调用中，将 **arr[i]** 或 **(-1)*arr[i]** 与相应的**标志**变量相加，该变量表示当前元素是正的还是负的。以下是步骤:

*   创建一个大小为 **N*2 和**的**2D**T2【DP】[]数组，用 **-1** 初始化数组。
*   传递变量**标志**，该标志表示在下一项中必须选择的元素的符号。**例如**，在子序列中， **{a，b，c}** ，那么最大子序列可以是**(a–b+ c)**或**(b–c)**或**c . I**n 对于所有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)，一次又一次地存储在 **dp[][]** 数组中并使用循环状态。
*   如果**标志为 0** ，则当前元素被认为是**正元素**，如果**标志为 1** ，则当前元素被认为是**负元素**。
*   将每个结果存储到 **dp[][]** 数组中。
*   经过上述步骤后，将 **dp[N][flag]** 的值打印为最大值。

**以下是上述方法的实现:**

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// maximum sum subsequence
int findMax(vector<int>& a, int dp[][2],
            int i, int flag)
{
    // Base Case
    if (i == (int)a.size()) {
        return 0;
    }

    // If current state is already
    // calculated then use it
    if (dp[i][flag] != -1) {
        return dp[i][flag];
    }

    int ans;

    // If current element is positive
    if (flag == 0) {

        // Update ans and recursively
        // call with update value of flag
        ans = max(findMax(a, dp, i + 1, 0),
                  a[i]
                      + findMax(a, dp,
                                i + 1, 1));
    }

    // Else current element is negative
    else {

        // Update ans and recursively
        // call with update value of flag
        ans = max(findMax(a, dp, i + 1, 1),
                  -1 * a[i]
                      + findMax(a, dp,
                                i + 1, 0));
    }

    // Return maximum sum subsequence
    return dp[i][flag] = ans;
}

// Function that finds the maximum
// sum of element of the subsequence
// with alternate +ve and -ve signs
void findMaxSumUtil(vector<int>& arr,
                    int N)
{
    // Create auxiliary array dp[][]
    int dp[N][2];

    // Initialize dp[][]
    memset(dp, -1, sizeof dp);

    // Function Call
    cout << findMax(arr, dp, 0, 0);
}

// Driver Code
int main()
{
    // Given array arr[]
    vector<int> arr = { 1, 2, 3, 4, 1, 2 };

    int N = arr.size();

    // Function Call
    findMaxSumUtil(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Arrays;

class GFG{

// Function to find the
// maximum sum subsequence
static int findMax(int[] a, int dp[][],
                   int i, int flag)
{

    // Base Case
    if (i == (int)a.length)
    {
        return 0;
    }

    // If current state is already
    // calculated then use it
    if (dp[i][flag] != -1)
    {
        return dp[i][flag];
    }

    int ans;

    // If current element is positive
    if (flag == 0)
    {

        // Update ans and recursively
        // call with update value of flag
        ans = Math.max(findMax(a, dp, i + 1, 0),
                a[i] + findMax(a, dp, i + 1, 1));
    }

    // Else current element is negative
    else
    {

        // Update ans and recursively
        // call with update value of flag
        ans = Math.max(findMax(a, dp, i + 1, 1),
           -1 * a[i] + findMax(a, dp, i + 1, 0));
    }

    // Return maximum sum subsequence
    return dp[i][flag] = ans;
}

// Function that finds the maximum
// sum of element of the subsequence
// with alternate +ve and -ve signs
static void findMaxSumUtil(int[] arr,
                           int N)
{

    // Create auxiliary array dp[][]
    int dp[][] = new int[N][2];

    // Initialize dp[][]
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < 2; j++)
        {
            dp[i][j] = -1;
        }
    }

    // Function Call
    System.out.println(findMax(arr, dp, 0, 0));
}

// Driver Code
public static void main (String[] args)
{

    // Given array arr[]
    int[] arr = { 1, 2, 3, 4, 1, 2 };

    int N = arr.length;

    // Function call
    findMaxSumUtil(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the
# maximum sum subsequence
def findMax(a, dp, i, flag):

    # Base Case
    if (i == len(a)):
        return 0

    # If current state is already
    # calculated then use it
    if (dp[i][flag] != -1):
        return dp[i][flag]

    ans = 0

    # If current element is positive
    if (flag == 0):

        # Update ans and recursively
        # call with update value of flag
        ans = max(findMax(a, dp, i + 1, 0),
           a[i] + findMax(a, dp, i + 1, 1))

    # Else current element is negative
    else:

        # Update ans and recursively
        # call with update value of flag
        ans = max(findMax(a, dp, i + 1, 1),
      -1 * a[i] + findMax(a, dp, i + 1, 0))

    # Return maximum sum subsequence
    dp[i][flag] = ans

    return ans

# Function that finds the maximum
# sum of element of the subsequence
# with alternate +ve and -ve signs
def findMaxSumUtil(arr, N):

    # Create auxiliary array dp[][]
    dp = [[-1 for i in range(2)]
              for i in range(N)]

    # Function call
    print(findMax(arr, dp, 0, 0))

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 2, 3, 4, 1, 2 ]

    N = len(arr)

    # Function call
    findMaxSumUtil(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG {

// Function to find the
// maximum sum subsequence
static int findMax(int[] a, int[,] dp,
                   int i, int flag)
{

    // Base Case
    if (i == (int)a.Length)
    {
        return 0;
    }

    // If current state is already
    // calculated then use it
    if (dp[i, flag] != -1)
    {
        return dp[i, flag];
    }

    int ans;

    // If current element is positive
    if (flag == 0)
    {

        // Update ans and recursively
        // call with update value of flag
        ans = Math.Max(findMax(a, dp, i + 1, 0),
                a[i] + findMax(a, dp, i + 1, 1));
    }

    // Else current element is negative
    else
    {

        // Update ans and recursively
        // call with update value of flag
        ans = Math.Max(findMax(a, dp, i + 1, 1),
           -1 * a[i] + findMax(a, dp, i + 1, 0));
    }

    // Return maximum sum subsequence
    return dp[i, flag] = ans;
}

// Function that finds the maximum
// sum of element of the subsequence
// with alternate +ve and -ve signs
static void findMaxSumUtil(int[] arr,
                           int N)
{

    // Create auxiliary array dp[][]
    int[,] dp = new int[N, 2];

    // Initialize dp[][]
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < 2; j++)
        {
            dp[i, j] = -1;
        }
    }

    // Function Call
    Console.WriteLine(findMax(arr, dp, 0, 0));
}

// Driver Code
public static void Main()
{

    // Given array arr[]
    int[] arr = { 1, 2, 3, 4, 1, 2 };

    int N = arr.Length;

    // Function call
    findMaxSumUtil(arr, N);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the
// maximum sum subsequence
function findMax(a, dp, i, flag)
{

    // Base Case
    if (i == a.length)
    {
        return 0;
    }

    // If current state is already
    // calculated then use it
    if (dp[i][flag] != -1)
    {
        return dp[i][flag];
    }

    let ans;

    // If current element is positive
    if (flag == 0)
    {

        // Update ans and recursively
        // call with update value of flag
        ans = Math.max(findMax(a, dp, i + 1, 0),
                a[i] + findMax(a, dp, i + 1, 1));
    }

    // Else current element is negative
    else
    {

        // Update ans and recursively
        // call with update value of flag
        ans = Math.max(findMax(a, dp, i + 1, 1),
           -1 * a[i] + findMax(a, dp, i + 1, 0));
    }

    // Return maximum sum subsequence
    return dp[i][flag] = ans;
}

// Function that finds the maximum
// sum of element of the subsequence
// with alternate +ve and -ve signs
function findMaxSumUtil(arr, N)
{

    // Create auxiliary array dp[][]
    let dp = new Array(N);

    // Loop to create 2D array using 1D array
    for(var i = 0; i < dp.length; i++)
    {
        dp[i] = new Array(2);
    }

    // Initialize dp[][]
    for(let i = 0; i < N; i++)
    {
        for(let j = 0; j < 2; j++)
        {
            dp[i][j] = -1;
        }
    }

    // Function Call
    document.write(findMax(arr, dp, 0, 0));
}

// Driver code

// Given array arr[]
let arr = [ 1, 2, 3, 4, 1, 2 ];

let N = arr.length;

// Function call
findMaxSumUtil(arr, N);

// This code is contributed by splevel62

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)