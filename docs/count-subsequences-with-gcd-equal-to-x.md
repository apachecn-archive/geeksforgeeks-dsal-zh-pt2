# 计算 GCD 等于 X 的子序列

> 原文:[https://www . geesforgeks . org/count-subseries-with-gcd-equal-to-x/](https://www.geeksforgeeks.org/count-subsequences-with-gcd-equal-to-x/)

给定一个由 **N** 个整数和一个正整数 **X** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是用 GCD 精确地计数子序列 **X** 。

**示例:**

> **输入:** arr[] = {6，4，30} X = 2
> **输出:** 3
> **解释:**GCD =(2)的子序列为{ {6，4，30}，{4，30}，{6，4} }。因此，答案是 3。
> 
> **输入:** arr[] = {6，6，6} X = 3
> **输出:** 0

**方法:**给定问题可以借助 [**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/) 解决。按照以下步骤解决给定的问题。

*   定义一个二维 dp 表 **dp[i][j]** ，该表将使用 GCD(= **j** 表示有效子序列的数量，直到索引 **i** 。
*   对于每个迭代，我们有两个选择:
    *   **取当前元素:**DP 表可以更新为 **dp[i + 1][gcd(j，arr[i])] += dp[i][j]** 。
    *   **跳过当前元素:**DP 表可以更新为 **dp[i+1][j] += dp[i][j]** 。
*   基本情况是 **dp[0][0] = 1** 。
*   由于两个数的 gcd 永远不能大于两个数，所以 **j** 的值将达到[数组中的最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。所以可以迭代求解，最终答案为 **dp[N][X]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the total subsequences
// having GCD = X
int totalValidSubsequences(
    vector<int> arr, int X, int N)
{
    // Find the maximum element of
    // the array
    int mx = *max_element(
        arr.begin(), arr.end());

    // Check if X is greater than mx
    if (X > mx) {
        return 0;
    }
    // Make a 2-d dp table of
    // size [n+1, mx + 1]
    vector<vector<int> > dp(
        N + 1, vector<int>(mx + 1, 0));

    // Base Case
    dp[0][0] = 1;

    for (int i = 0; i < N; i++) {

        // Iterate through all possible
        // indexes
        for (int j = 0; j <= mx; j++) {

            // Iterate through all
            // possible values

            // Case 1\. Skip the element
            dp[i + 1][j] += dp[i][j];

            // Case 2\. Skip the current element
            dp[i + 1][__gcd(j, arr[i])] += dp[i][j];
        }
    }

    // Return the answer dp[N][X]
    return dp[N][X];
}

// Driver Code
int main()
{
    vector<int> arr = { 6, 4, 30 };
    int X = 2;
    int N = arr.size();
    cout << totalValidSubsequences(arr, X, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.Arrays;
import java.util.Collections;

class GFG {

       // Function to find maximum in arr[]
     static int max(int[] arr)
     {

         // Initialize maximum element
         int max = arr[0];

         // Traverse array elements from second and
         // compare every element with current max 
         for (int i = 1; i < arr.length; i++)
             if (arr[i] > max)
                 max = arr[i];

         return max;
     }

      // Recursive function to return gcd of a and b
      static int gcd(int a, int b)
    {
      if (b == 0)
        return a;
      return gcd(b, a % b);
    }

    // Function to find the total subsequences
    // having GCD = X
    static int totalValidSubsequences(int[] arr,
                                      int X, int N)
    {
        // Find the maximum element of
        // the array
        int mx = max(arr);

        // Check if X is greater than mx
        if (X > mx) {
            return 0;
        }
        // Make a 2-d dp table of
        // size [n+1, mx + 1]
        int dp[][] = new int[N + 1][mx + 1];

        // Base Case
        dp[0][0] = 1;

        for (int i = 0; i < N; i++) {

            // Iterate through all possible
            // indexes
            for (int j = 0; j <= mx; j++) {

                // Iterate through all
                // possible values

                // Case 1\. Skip the element
                dp[i + 1][j] += dp[i][j];

                // Case 2\. Skip the current element
                dp[i + 1][gcd(j, arr[i])] += dp[i][j];
            }
        }

        // Return the answer dp[N][X]
        return dp[N][X];
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 6, 4, 30 };
           int X = 2;
        int N = arr.length;
           System.out.println(totalValidSubsequences(arr, X, N));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from math import gcd

# Function to find the total subsequences
# having GCD = X
def totalValidSubsequences(arr, X, N):

    # Find the maximum element of
    # the array
    mx = max(arr)

    # Check if X is greater than mx
    if (X > mx):
        return 0
    # Make a 2-d dp table of
    # size [n+1, mx + 1]
    dp = [[0 for i in range(mx+1)] for j in range(N + 1)]

    # Base Case
    dp[0][0] = 1

    for i in range(N):

        # Iterate through all possible
        # indexes
        for j in range(mx+1):

            # Iterate through all
            # possible values

            # Case 1\. Skip the element
            dp[i + 1][j] += dp[i][j]

            # Case 2\. Skip the current element
            dp[i + 1][gcd(j, arr[i])] += dp[i][j]

    # Return the answer dp[N][X]
    return dp[N][X]

# Driver Code
if __name__ == '__main__':
    arr = [6, 4, 30]
    X = 2
    N = len(arr)
    print(totalValidSubsequences(arr, X, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

       // Function to find maximum in arr[]
static int max(int []arr)
{

  // Initialize maximum element
  int max = arr[0];

  // Traverse array elements from second and
  // compare every element with current max 
  for (int i = 1; i < arr.Length; i++)
             if (arr[i] > max)
                 max = arr[i];

         return max;
}

// Recursive function to return gcd of a and b
static int gcd(int a, int b)
{
 if (b == 0)
        return a;
      return gcd(b, a % b);
}

// Function to find the total subsequences
// having GCD = X
static int totalValidSubsequences(int[] arr,
                                      int X, int N)
    {
        // Find the maximum element of
        // the array
        int mx = max(arr);

        // Check if X is greater than mx
        if (X > mx) {
            return 0;
        }
        // Make a 2-d dp table of
        // size [n+1, mx + 1]
        int[,] dp = new int[N + 1, mx + 1];

        // Base Case
        dp[0, 0] = 1;

        for (int i = 0; i < N; i++) {

            // Iterate through all possible
            // indexes
            for (int j = 0; j <= mx; j++) {

                // Iterate through all
                // possible values

                // Case 1\. Skip the element
                dp[i + 1, j] += dp[i, j];

                // Case 2\. Skip the current element
                dp[i + 1, gcd(j, arr[i])] += dp[i, j];
            }
        }

        // Return the answer dp[N][X]
        return dp[N, X];
    }

// Driver Code
public static void Main()
{
   int[] arr = { 6, 4, 30 };
           int X = 2;
        int N = arr.Length;
           Console.Write(totalValidSubsequences(arr, X, N));
}
}

// This code is contributed by _saurabh_jaiswal
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach
       // Recursive function to return gcd of a and b
       function __gcd(a, b) {
           if (b == 0)
               return a;
           return __gcd(b, a % b);
       }

       // Function to find the total subsequences
       // having GCD = X
       function totalValidSubsequences(
           arr, X, N)
       {
           // Find the maximum element of
           // the array
           let mx = arr[0];

           for (let i = 1; i < arr.length; i++) {
               mx = Math.max(mx, arr[i]);
           }

           // Check if X is greater than mx
           if (X > mx) {
               return 0;
           }
           // Make a 2-d dp table of
           // size [n+1, mx + 1]

           let dp = new Array(N + 1);
           for (let i = 0; i < N + 1; i++) {
               dp[i] = new Array(mx + 1).fill(0)
           }

           // Base Case
           dp[0][0] = 1;

           for (let i = 0; i < N; i++) {

               // Iterate through all possible
               // indexes
               for (let j = 0; j <= mx; j++) {

                   // Iterate through all
                   // possible values

                   // Case 1\. Skip the element
                   dp[i + 1][j] += dp[i][j];

                   // Case 2\. Skip the current element
                   dp[i + 1][__gcd(j, arr[i])] += dp[i][j];
               }
           }

           // Return the answer dp[N][X]
           return dp[N][X];
       }

       // Driver Code
       let arr = [6, 4, 30];
       let X = 2;
       let N = arr.length;
       document.write(totalValidSubsequences(arr, X, N));

    // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*M)，其中 **M** 为* [*阵的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(N*M)*