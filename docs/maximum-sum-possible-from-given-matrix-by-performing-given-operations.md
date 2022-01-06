# 通过执行给定操作从给定矩阵中获得的最大可能和

> 原文:[https://www . geeksforgeeks . org/通过执行给定操作从给定矩阵中获得最大可能总和/](https://www.geeksforgeeks.org/maximum-sum-possible-from-given-matrix-by-performing-given-operations/)

给定维度为 **2 * N** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **arr[][]** ，任务是通过从每列中最多选择一个元素来最大化可能的总和，从而不会从同一行中选择两个连续的元素。

**示例:**

> **输入:** arr[][] = {{1，50，21，5}，{2，10，10，5}}
> **输出:** 67
> **说明:**可以选择元素 arr[1][0]( = 2)、arr[0][1]( = 50)、arr[0][2]( = 10)和 arr[0][3]( = 5)。因此，总和= 2 + 50 + 10 + 5 = 67。
> 
> **输入:** arr[][] = {{9，5，3，7，3}，{50，8，1，50，5}}
> **输出:** 108
> **说明:**可以选择元素 arr[1][0]( = 50)、arr[0][1]( = 5)、arr[1][3]( = 50)和 arr[0][4]( = 3)。因此，sum = 50 + 5 + 50 + 3 = 108。

[**动态规划**](http://www.geeksforgeeks.org/dynamic-programming/) **方法:**使用[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)可以解决问题。按照以下步骤解决问题:

*   初始化一个数组 **dp[][]** 来存储以下转换状态:

> **dp[0][i] = max(dp[1][i+1]，DP[0][I+2])+arr[0][I]**
> **DP[1][I]= max(DP[0][I+1]，dp[1][i+2]) + arr[1][i]**
> 其中， **dp[j][i]** 存储从最后一列开始到达单元格 **arr[j][i]** 的最大可能总和，其中 0 【T10
> 
> **基案:**
> DP[0][n-1]= arr[0][n-1]
> DP[1][n-1]= arr[1][n-1]

*   从**(n–2)<sup>第</sup>** 列遍历到 **0 <sup>第</sup>** 列，对于每行，将 **dp[j][i]** 更新为**DP[j][I]= max(DP[(j ^ 1)][I+1]，dp[j][i+2]) + arr[j][i]** ，其中 **^** 表示[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。
*   遍历完成后，打印 **max(dp[0][0]，dp[1][0])** 作为最大可能和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
#include <vector>
using namespace std;

// Function to print the maximum sum
void maxSum(vector<vector<int> > arr,
            int n, int m)
{

    // Dp table
    vector<vector<int> > dp(n);

    // Initializing dp array with 0s
    for (int i = 0; i < 2; i++) {
        dp[i] = vector<int>(m);
        for (int j = 0; j < m; j++) {
            dp[i][j] = 0;
        }
    }

    // Base case
    dp[0][m - 1] = arr[0][m - 1];
    dp[1][m - 1] = arr[1][m - 1];

    // Traverse each column
    for (int j = m - 2; j >= 0; j--) {

        // Update answer for both rows
        for (int i = 0; i < 2; i++) {
            if (i == 1) {
                dp[i][j] = max(
                    arr[i][j] + dp[0][j + 1],
                    arr[i][j] + dp[0][j + 2]);
            }
            else {
                dp[i][j] = max(
                    arr[i][j] + dp[1][j + 1],
                    arr[i][j] + dp[1][j + 2]);
            }
        }
    }

    // Print the maximum sum
    cout << max(dp[0][0], dp[1][0]);
}

// Driver Code
int main()
{

    // Given array
    vector<vector<int> > arr
        = { { 1, 50, 21, 5 },
            { 2, 10, 10, 5 } };

    // Number of Columns
    int N = arr[0].size();

    // Function calls
    maxSum(arr, 2, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to print the maximum sum
static void maxSum(int[][] arr, int n, int m)
{

    // Dp table
    int[][] dp = new int[n][m + 1];

    // Initializing dp array with 0s
    for(int i = 0; i < 2; i++)
    {
        for(int j = 0; j <= m; j++)
        {
            dp[i][j] = 0;
        }
    }

    // Base case
    dp[0][m - 1] = arr[0][m - 1];
    dp[1][m - 1] = arr[1][m - 1];

    // Traverse each column
    for(int j = m - 2; j >= 0; j--)
    {

        // Update answer for both rows
        for (int i = 0; i < 2; i++)
        {
            if (i == 1)
            {
                dp[i][j] = Math.max(
                    arr[i][j] + dp[0][j + 1],
                    arr[i][j] + dp[0][j + 2]);
            }
            else
            {
                dp[i][j] = Math.max(
                    arr[i][j] + dp[1][j + 1],
                    arr[i][j] + dp[1][j + 2]);
            }
        }
    }

    // Print the maximum sum
    System.out.println(Math.max(dp[0][0],
                                dp[1][0]));
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int[][] arr = { { 1, 50, 21, 5 },
                    { 2, 10, 10, 5 } };

    // Number of Columns
    int N = arr[0].length;

    // Function calls
    maxSum(arr, 2, N);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the maximum sum
def maxSum(arr, n, m):

    # Dp table
    dp = [[0 for i in range(m + 1)]
             for i in range(2)]

    # Initializing dp array with 0s
    # for (i = 0 i < 2 i++) {
    #     dp[i] = vector<int>(m)
    #     for (j = 0 j < m j++) {
    #         dp[i][j] = 0
    #     }
    # }

    # Base case
    dp[0][m - 1] = arr[0][m - 1]
    dp[1][m - 1] = arr[1][m - 1]

    # Traverse each column
    for j in range(m - 2, -1, -1):

        # Update answer for both rows
        for i in range(2):
            if (i == 1):
                dp[i][j] = max(arr[i][j] + dp[0][j + 1],
                               arr[i][j] + dp[0][j + 2])
            else:
                dp[i][j] = max(arr[i][j] + dp[1][j + 1],
                               arr[i][j] + dp[1][j + 2])

    # Print the maximum sum
    print(max(dp[0][0], dp[1][0]))

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ [ 1, 50, 21, 5 ],
            [ 2, 10, 10, 5 ] ]

    # Number of Columns
    N = len(arr[0])

    # Function calls
    maxSum(arr, 2, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to print the maximum sum
static void maxSum(int[, ] arr, int n, int m)
{

    // Dp table
    int[, ] dp = new int[n, m + 1];

    // Initializing dp array with 0s
    for(int i = 0; i < 2; i++)
    {
        for(int j = 0; j <= m; j++)
        {
            dp[i, j] = 0;
        }
    }

    // Base case
    dp[0, m - 1] = arr[0, m - 1];
    dp[1, m - 1] = arr[1, m - 1];

    // Traverse each column
    for(int j = m - 2; j >= 0; j--)
    {

        // Update answer for both rows
        for(int i = 0; i < 2; i++)
        {
            if (i == 1)
            {
                dp[i, j] = Math.Max(
                    arr[i, j] + dp[0, j + 1],
                    arr[i, j] + dp[0, j + 2]);
            }
            else
            {
                dp[i, j] = Math.Max(
                    arr[i, j] + dp[1, j + 1],
                    arr[i, j] + dp[1, j + 2]);
            }
        }
    }

    // Print the maximum sum
    Console.WriteLine(Math.Max(dp[0, 0],
                               dp[1, 0]));
}

// Driver Code
public static void Main()
{

    // Given array
    int[, ] arr = { { 1, 50, 21, 5 },
                    { 2, 10, 10, 5 } };

    // Number of Columns
    int N = arr.GetLength(1);

    // Function calls
    maxSum(arr, 2, N);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to print the maximum sum
function maxSum(arr, n, m)
{

    // Dp table
    let dp = new Array(n);

    // Loop to create 2D array using 1D array
    for (var i = 0; i < dp.length; i++) {
        dp[i] = new Array(2);
    }

    // Initializing dp array with 0s
    for(let i = 0; i < 2; i++)
    {
        for(let j = 0; j <= m; j++)
        {
            dp[i][j] = 0;
        }
    }

    // Base case
    dp[0][m - 1] = arr[0][m - 1];
    dp[1][m - 1] = arr[1][m - 1];

    // Traverse each column
    for(let j = m - 2; j >= 0; j--)
    {

        // Update answer for both rows
        for (let i = 0; i < 2; i++)
        {
            if (i == 1)
            {
                dp[i][j] = Math.max(
                    arr[i][j] + dp[0][j + 1],
                    arr[i][j] + dp[0][j + 2]);
            }
            else
            {
                dp[i][j] = Math.max(
                    arr[i][j] + dp[1][j + 1],
                    arr[i][j] + dp[1][j + 2]);
            }
        }
    }

    // Print the maximum sum
    document.write(Math.max(dp[0][0],
                            dp[1][0]));
}

// Driver Code

     // Given array
    let arr = [[ 1, 50, 21, 5 ],
               [ 2, 10, 10, 5 ]];

    // Number of Columns
    let N = arr[0].length;

    // Function calls
    maxSum(arr, 2, N);

</script>
```

**Output:** 

```
67
```

***时间复杂度:** O(N)，其中 **N** 为列数。*
***辅助空间:** O(N)*

**高效方法:**按照以下步骤优化上述方法

1.  初始化两个变量 **r1** 和 **r2** ，分别存储 1 <sup>st</sup> 和 2 <sup>nd</sup> 行的最大和。
2.  遍历行的长度，即 **0 到 N–1**，对于每个元素 **arr[i]** ，将 **r1** 更新为 **r1 = max(r1，r2 + arr[0][i])** 并将 **r2** 更新为 **r2 = max(r2，r1 + arr[1][i])** 。
3.  遍历后，打印 **max(r1，r2)** 作为最大和。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the maximum sum
// possible by selecting at most one
// element from each column such that
// no consecutive pairs are selected
// from a single row
void maxSum(vector<vector<int> > arr, int n)
{

    // Initialize variables
    int r1 = 0, r2 = 0;

    // Traverse each column
    for(int i = 0; i < n; i++)
    {

        // r1, r2 = max(r1, r2 + arr[0][i]),
        // max(r2, r1 + arr[1][i])
        int temp = r1;

        r1 = max(r1, r2 + arr[0][i]);
        r2 = max(r2, temp + arr[1][i]);
    }

    // Print answer
    cout << max(r1, r2);
}

// Driver Code
int main()
{
    vector<vector<int>> arr = { { 1, 50, 21, 5 },
                                { 2, 10, 10, 5 } };

    // Numberof columns
    int n = arr[0].size();

    maxSum(arr, n);

    return 0;
}

// This code is contributed by akhilsaini
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to print the maximum sum
// possible by selecting at most one
// element from each column such that
// no consecutive pairs are selected
// from a single row
static void maxSum(int[][] arr, int n)
{

    // Initialize variables
    int r1 = 0, r2 = 0;

    // Traverse each column
    for(int i = 0; i < n; i++)
    {
        int temp = r1;

        r1 = Math.max(r1, r2 + arr[0][i]);
        r2 = Math.max(r2, temp + arr[1][i]);
    }

    // Print answer
    System.out.println(Math.max(r1, r2));
}

// Driver Code
public static void main(String args[])
{
    int[][] arr = { { 1, 50, 21, 5 },
                    { 2, 10, 10, 5 } };

    // Numberof columns
    int n = arr[0].length;

    maxSum(arr, n);
}
}

// This code is contributed by akhilsaini
```

## 计算机编程语言

```
# Python code for the above approach

# Function to print the maximum sum
# possible by selecting at most one
# element from each column such that
# no consecutive pairs are selected
# from a single row

def maxSum(arr, n):

    # Initialize variables
    r1 = r2 = 0

    # Traverse each column
    for i in range(n):
        r1, r2 = max(r1, r2 + arr[0][i]), max(r2, r1 + arr[1][i])

        # Print answer
    print(max(r1, r2))

# Driver Code

arr = [[1, 50, 21, 5], [2, 10, 10, 5]]

# Numberof columns
n = len(arr[0])

maxSum(arr, n)
```

## C#

```
// C# code for the above approach
using System;

class GFG{

// Function to print the maximum sum
// possible by selecting at most one
// element from each column such that
// no consecutive pairs are selected
// from a single row
static void maxSum(int[, ] arr, int n)
{

    // Initialize variables
    int r1 = 0, r2 = 0;

    // Traverse each column
    for(int i = 0; i < n; i++)
    {
        int temp = r1;

        r1 = Math.Max(r1, r2 + arr[0, i]);
        r2 = Math.Max(r2, temp + arr[1, i]);
    }

    // Print answer
    Console.WriteLine(Math.Max(r1, r2));
}

// Driver Code
public static void Main()
{
    int[, ] arr = { { 1, 50, 21, 5 },
                    { 2, 10, 10, 5 } };

    // Numberof columns
    int n = arr.GetLength(1);

    maxSum(arr, n);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript code for the above approach   

// Function to print the maximum sum
    // possible by selecting at most one
    // element from each column such that
    // no consecutive pairs are selected
    // from a single row
    function maxSum(arr , n) {

        // Initialize variables
        var r1 = 0, r2 = 0;

        // Traverse each column
        for (i = 0; i < n; i++) {
            var temp = r1;

            r1 = Math.max(r1, r2 + arr[0][i]);
            r2 = Math.max(r2, temp + arr[1][i]);
        }

        // Print answer
        document.write(Math.max(r1, r2));
    }

    // Driver Code

        var arr = [ [ 1, 50, 21, 5 ],
        [ 2, 10, 10, 5 ] ];

        // Numberof columns
        var n = arr[0].length;

        maxSum(arr, n);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
67
```

***时间复杂度:** O(N)，其中 N 为列数。*
***辅助空间:** O(1)*