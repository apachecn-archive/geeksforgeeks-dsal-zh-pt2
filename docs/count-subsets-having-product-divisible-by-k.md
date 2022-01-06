# 计数乘积可被 K 整除的子集

> 原文:[https://www . geesforgeks . org/count-subset-having-product-可被-k 除尽/](https://www.geeksforgeeks.org/count-subsets-having-product-divisible-by-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是计算给定[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)中[子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)的数量，元素的乘积可被 **K** 整除

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 60
> **输出:** 4
> **解释:**元素乘积可被 K 整除的子集为{ {1，2，3，4，5}，{2，3，4，5}，{3，4，5}，{1，3，4，5}
> 
> **输入:** arr[] = {1，2，3，4，5，6}，K = 60
> T3】输出: 16

**天真方法:**解决这个问题最简单的方法是[生成所有可能的子集](https://www.geeksforgeeks.org/find-distinct-subsets-given-set/)，对于每个子集，检查其元素的乘积是否能被 **K** 整除。如果发现为真，则增加**计数**。最后，打印**计数**。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**优化上述方法的思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。下面是递归关系和基本情况:

> **递归关系:**
> cntsubdvk(N，rem)= cntsubdvk(N–1，(rem * arr[N–1])% K)+cntsubdvk(N–1，rem)。
> cntsubdvk(N，rem)存储乘积可被 K 整除的子集的计数。
> rem:存储 K 除子集所有元素乘积时的余数。
> 
> **基本情况:**
> 如果 **N == 0 且 rem == 0** 则返回 **1** 。
> 如果 **N == 0 且 rem！= 0** 然后返回 **0** 。

按照以下步骤解决问题:

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如**DP【N】【rem】**来计算并存储上述递归关系的所有子问题的值。
*   最后，返回**DP【N】【rem】**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the subsets whose
// product of elements is divisible by K
int cntSubDivK(int arr[], int N, int K,
               int rem, vector<vector<int> >& dp)
{
    // If count of elements
    // in the array is 0
    if (N == 0) {

        // If rem is 0, then return 1
        // Otherwise, return 0
        return rem == 0;
    }

    // If already computed
    // subproblem occurred
    if (dp[N][rem] != -1) {
        return dp[N][rem];
    }

    // Stores count of subsets having product
    // divisible by K when arr[N - 1]
    // present in the subset
    int X = cntSubDivK(arr, N - 1, K,
                       (rem * arr[N - 1]) % K, dp);

    // Stores count of subsets having product
    // divisible by K when arr[N - 1] not
    // present in the subset
    int Y = cntSubDivK(arr, N - 1, K,
                       rem, dp);

    // Return total subset
    return X + Y;
}

// Utility Function to count the subsets whose
// product of elements is divisible by K
int UtilCntSubDivK(int arr[], int N, int K)
{

    // Initialize a 2D array to store values
    // of overlapping subproblems
    vector<vector<int> > dp(N + 1,
                            vector<int>(K + 1, -1));

    return cntSubDivK(arr, N, K, 1, dp);
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int K = 60;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << UtilCntSubDivK(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count the subsets whose
// product of elements is divisible by K
static int cntSubDivK(int arr[], int N, int K,
                      int rem, int[][]dp)
{

    // If count of elements
    // in the array is 0
    if (N == 0)
    {

        // If rem is 0, then return 1
        // Otherwise, return 0
        return rem == 0 ? 1 : 0;
    }

    // If already computed
    // subproblem occurred
    if (dp[N][rem] != -1)
    {
        return dp[N][rem];
    }

    // Stores count of subsets having product
    // divisible by K when arr[N - 1]
    // present in the subset
    int X = cntSubDivK(arr, N - 1, K,
                       (rem * arr[N - 1]) % K, dp);

    // Stores count of subsets having product
    // divisible by K when arr[N - 1] not
    // present in the subset
    int Y = cntSubDivK(arr, N - 1, K,
                       rem, dp);

    // Return total subset
    return X + Y;
}

// Utility Function to count the subsets whose
// product of elements is divisible by K
static int UtilCntSubDivK(int arr[], int N, int K)
{

    // Initialize a 2D array to store values
    // of overlapping subproblems
    int [][]dp = new int[N + 1][K + 1];

    for(int i = 0; i < N + 1; i++)
    {
        for(int j = 0; j < K + 1; j++)
            dp[i][j] = -1;
    }
    return cntSubDivK(arr, N, K, 1, dp);
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int K = 60;
    int N = arr.length;

    System.out.println(UtilCntSubDivK(arr, N, K));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 program to
# implement the above
# approach

# Function to count the
# subsets whose product
# of elements is divisible
# by K
def cntSubDivK(arr, N, K,
               rem, dp):

    # If count of elements
    # in the array is 0
    if (N == 0):

        # If rem is 0, then
        # return 1 Otherwise,
        # return 0
        return rem == 0

    # If already computed
    # subproblem occurred
    if (dp[N][rem] != -1):
        return dp[N][rem]

    # Stores count of subsets
    # having product divisible
    # by K when arr[N - 1]
    # present in the subset
    X = cntSubDivK(arr, N - 1, K,
                   (rem * arr[N - 1]) % K, dp)

    # Stores count of subsets having
    # product divisible by K when
    # arr[N - 1] not present in
    # the subset
    Y = cntSubDivK(arr, N - 1,
                   K, rem, dp)

    # Return total subset
    return X + Y

# Utility Function to count
# the subsets whose product of
# elements is divisible by K
def UtilCntSubDivK(arr, N, K):

    # Initialize a 2D array to
    # store values of overlapping
    # subproblems
    dp = [[-1 for x in range(K + 1)]
              for y in range(N + 1)]

    return cntSubDivK(arr, N,
                      K, 1, dp)

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 3,
           4, 5, 6]
    K = 60
    N = len(arr)
    print(UtilCntSubDivK(arr, N, K))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to count the subsets whose
// product of elements is divisible by K
static int cntSubDivK(int[] arr, int N, int K,
                      int rem, int[,] dp)
{

    // If count of elements
    // in the array is 0
    if (N == 0)
    {

        // If rem is 0, then return 1
        // Otherwise, return 0
        return rem == 0 ? 1 : 0;
    }

    // If already computed
    // subproblem occurred
    if (dp[N, rem] != -1)
    {
        return dp[N, rem];
    }

    // Stores count of subsets having product
    // divisible by K when arr[N - 1]
    // present in the subset
    int X = cntSubDivK(arr, N - 1, K,
                      (rem * arr[N - 1]) % K, dp);

    // Stores count of subsets having product
    // divisible by K when arr[N - 1] not
    // present in the subset
    int Y = cntSubDivK(arr, N - 1, K,
                       rem, dp);

    // Return total subset
    return X + Y;
}

// Utility Function to count the subsets whose
// product of elements is divisible by K
static int UtilCntSubDivK(int[] arr, int N, int K)
{

    // Initialize a 2D array to store values
    // of overlapping subproblems
    int[,] dp = new int[N + 1, K + 1];

    for(int i = 0; i < N + 1; i++)
    {
        for(int j = 0; j < K + 1; j++)
            dp[i, j] = -1;
    }
    return cntSubDivK(arr, N, K, 1, dp);
}

// Driver code
static void Main()
{
    int[] arr = { 1, 2, 3, 4, 5, 6 };
    int K = 60;
    int N = arr.Length;

    Console.WriteLine(UtilCntSubDivK(arr, N, K));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to count the subsets whose
// product of elements is divisible by K
function cntSubDivK(arr, N, K, rem, dp)
{

    // If count of elements
    // in the array is 0
    if (N == 0)
    {

        // If rem is 0, then return 1
        // Otherwise, return 0
        return rem == 0 ? 1 : 0;
    }

    // If already computed
    // subproblem occurred
    if (dp[N][rem] != -1)
    {
        return dp[N][rem];
    }

    // Stores count of subsets having product
    // divisible by K when arr[N - 1]
    // present in the subset
    let X = cntSubDivK(arr, N - 1, K,
                 (rem * arr[N - 1]) % K, dp);

    // Stores count of subsets having product
    // divisible by K when arr[N - 1] not
    // present in the subset
    let Y = cntSubDivK(arr, N - 1, K,
                       rem, dp);

    // Return total subset
    return X + Y;
}

// Utility Function to count the subsets whose
// product of elements is divisible by K
function UtilCntSubDivK(arr, N, K)
{

    // Initialize a 2D array to store values
    // of overlapping subproblems
    let dp = new Array(N + 1);

    // Loop to create 2D array using 1D array
    for(var i = 0; i < dp.length; i++)
    {
        dp[i] = new Array(2);
    }

    for(let i = 0; i < N + 1; i++)
    {
        for(let j = 0; j < K + 1; j++)
            dp[i][j] = -1;
    }
    return cntSubDivK(arr, N, K, 1, dp);
}

// Driver Code
let arr = [ 1, 2, 3, 4, 5, 6 ];
let K = 60;
let N = arr.length;

document.write(UtilCntSubDivK(arr, N, K));

// This code is contribute by target_2

</script>
```

**Output:** 

```
16
```

***时间复杂度:** O(N * K)*
***空间复杂度:** O(N * K)*