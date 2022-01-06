# 最大化从给定数组生成的成对乘积的和

> 原文:[https://www . geeksforgeeks . org/最大化从给定数组生成的成对乘积之和/](https://www.geeksforgeeks.org/maximize-sum-of-pairwise-products-generated-from-the-given-arrays/)

给定三个长度分别为 **N1** 、 **N2** 和 **N3** 的数组 **arr1[]、arr2[]** 和 **arr3[]** ，任务是通过将从不同数组中获取的对的乘积相加来找到最大可能和。

**注意:**每个数组元素可以是单个对的一部分。

**示例:**

> **输入:** arr1[] = {3，5}，arr2[] = {2，1}，arr3[] = {4，3，5}
> **输出:** 43
> **解释**
> 将数组按降序排序后，得到如下修改:arr1[] = {5，3}，arr2[] = {2，1}，arr3[] = {5，4，3}。
> 因此，最大化乘积=(arr 1[0]* arr 3[0])+(arr 1[1]* arr 3[1])+(arr 2[0]* arr 3[2])=(5 * 5+3 * 4+2 * 3)= 43
> 
> **输入:** arr1[] = {3，5，9，8，7}，arr2[] = {6}，arr3[] = {3，5}
> **输出:** 115
> **解释**
> 对数组进行降序排序，得到如下修改:arr1[] = {9，8，7，5，3}，arr2[] = {6}，arr3[] = {5，3}。
> 因此，最大化乘积=(arr 1[0]* arr 2[0])+(arr 1[1]* arr 3[0])+(arr 1[2]* arr 3[1])=(9 * 6+8 * 5+7 * 3)= 155

**方法:**给定的问题可以通过使用 3D 记忆表来存储所有可能的对组合的最大和来解决。假设 I、j、k 分别是从数组 arr1[]、arr2[]和 arr3[]中取出的元素数，以形成对，那么记忆表 DP[][][]]将在 dp[i][j][k]中存储从这种元素组合生成的乘积的最大可能和。
按照以下步骤解决问题-

*   [](https://www.geeksforgeeks.org/merge-sort-with-o1-extra-space-merge-and-on-lg-n-time/)**给定数组按降序排序。**
*   **初始化 dp 表 **dp[][][]** ，其中 **dp[i][j][k]** 存储从第一个数组中取 **i** 个最大数字，从第二个数组中取 **j** 个最大数字，从第三个数组中取 **k** 个最大数字得到的最大和。**
*   **对于分别来自三个阵列的每一个 **i** 、 **j** 和 **k <sup>th</sup>** 元素，检查所有可能的对，并通过考虑每一对来计算最大可能和，并将获得的最大和记忆起来以供进一步计算。**
*   **最后，打印 **dp[][][]** 矩阵返回的最大可能和。**

**下面是上述方法的实现:**

## **C++**

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

#define maxN 201

// Variables which represent
// the size of the array
int n1, n2, n3;

// Stores the results
int dp[maxN][maxN][maxN];

// Function to return the
// maximum possible sum
int getMaxSum(int i, int j,
              int k, int arr1[],
              int arr2[], int arr3[])
{
    // Stores the count of
    // arrays processed
    int cnt = 0;

    if (i >= n1)
        cnt++;

    if (j >= n2)
        cnt++;

    if (k >= n3)
        cnt++;

    // If more than two arrays
    // have been processed
    if (cnt >= 2)
        return 0;

    // If an already computed
    // subproblem occurred
    if (dp[i][j][k] != -1)
        return dp[i][j][k];

    int ans = 0;

    // Explore all the possible pairs
    if (i < n1 && j < n2)

        // Recursive function call
        ans = max(ans,
                  getMaxSum(i + 1, j + 1, k,
                            arr1, arr2, arr3)
                      + arr1[i] * arr2[j]);

    if (i < n1 && k < n3)
        ans = max(ans,
                  getMaxSum(i + 1, j, k + 1,
                            arr1, arr2, arr3)
                      + arr1[i] * arr3[k]);

    if (j < n2 && k < n3)
        ans = max(ans,
                  getMaxSum(i, j + 1, k + 1,
                            arr1, arr2, arr3)
                      + arr2[j] * arr3[k]);

    // Memoize the maximum
    dp[i][j][k] = ans;

    // Returning the value
    return dp[i][j][k];
}

// Function to return the maximum sum of
// products of pairs possible
int maxProductSum(int arr1[], int arr2[],
                  int arr3[])
{
    // Initialising the dp array to -1
    memset(dp, -1, sizeof(dp));

    // Sort the arrays in descending order
    sort(arr1, arr1 + n1);
    reverse(arr1, arr1 + n1);

    sort(arr2, arr2 + n2);
    reverse(arr2, arr2 + n2);

    sort(arr3, arr3 + n3);
    reverse(arr3, arr3 + n3);

    return getMaxSum(0, 0, 0,
                     arr1, arr2, arr3);
}

// Driver Code
int main()
{
    n1 = 2;
    int arr1[] = { 3, 5 };

    n2 = 2;
    int arr2[] = { 2, 1 };

    n3 = 3;
    int arr3[] = { 4, 3, 5 };

    cout << maxProductSum(arr1, arr2, arr3);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for above approach
import java.util.*;
import java.lang.*;

class GFG{

static final int maxN = 201;

// Variables which represent
// the size of the array
static int n1, n2, n3;

// Stores the results
static int[][][] dp = new int[maxN][maxN][maxN];

// Function to return the
// maximum possible sum
static int getMaxSum(int i, int j,
                     int k, int arr1[],
                     int arr2[], int arr3[])
{

    // Stores the count of
    // arrays processed
    int cnt = 0;

    if (i >= n1)
        cnt++;

    if (j >= n2)
        cnt++;

    if (k >= n3)
        cnt++;

    // If more than two arrays
    // have been processed
    if (cnt >= 2)
        return 0;

    // If an already computed
    // subproblem occurred
    if (dp[i][j][k] != -1)
        return dp[i][j][k];

    int ans = 0;

    // Explore all the possible pairs
    if (i < n1 && j < n2)

        // Recursive function call
        ans = Math.max(ans,
                       getMaxSum(i + 1, j + 1, k,
                                arr1, arr2, arr3) +
                                arr1[i] * arr2[j]);

    if (i < n1 && k < n3)
        ans = Math.max(ans,
                       getMaxSum(i + 1, j, k + 1,
                                 arr1, arr2, arr3) +
                                 arr1[i] * arr3[k]);

    if (j < n2 && k < n3)
        ans = Math.max(ans,
                       getMaxSum(i, j + 1, k + 1,
                                 arr1, arr2, arr3) +
                                 arr2[j] * arr3[k]);

    // Memoize the maximum
    dp[i][j][k] = ans;

    // Returning the value
    return dp[i][j][k];
}

static void reverse(int[] tmp)
{
    int i, k, t;
    int n = tmp.length;

        for(i = 0; i < n/ 2; i++)
        {
            t = tmp[i];
            tmp[i] = tmp[n - i - 1];
            tmp[n - i - 1] = t;
        }
}

// Function to return the maximum sum of
// products of pairs possible
static int maxProductSum(int arr1[], int arr2[],
                         int arr3[])
{

    // Initialising the dp array to -1
    for(int i = 0; i < dp.length; i++)
        for(int j = 0; j < dp[0].length; j++)
            for(int k = 0; k < dp[j][0].length; k++)
                dp[i][j][k] = -1;

    // Sort the arrays in descending order
    Arrays.sort(arr1);
    reverse(arr1);

    Arrays.sort(arr2);
    reverse(arr2);

    Arrays.sort(arr3);
    reverse(arr3);

    return getMaxSum(0, 0, 0,
                     arr1, arr2, arr3);
}

// Driver Code
public static void main (String[] args)
{
    n1 = 2;
    int arr1[] = { 3, 5 };

    n2 = 2;
    int arr2[] = { 2, 1 };

    n3 = 3;
    int arr3[] = { 4, 3, 5 };

    System.out.println(maxProductSum(arr1, arr2, arr3));
}
}

// This code is contributed by offbeat
```

## **蟒蛇 3**

```
# Python3 program for
# the above approach
maxN = 201;

# Variables which represent
# the size of the array
n1, n2, n3 = 0, 0, 0;

# Stores the results
dp = [[[0 for i in range(maxN)]
          for j in range(maxN)]
          for j in range(maxN)];

# Function to return the
# maximum possible sum
def getMaxSum(i, j, k,
              arr1, arr2, arr3):

    # Stores the count of
    # arrays processed
    cnt = 0;

    if (i >= n1):
        cnt += 1;

    if (j >= n2):
        cnt += 1;

    if (k >= n3):
        cnt += 1;

    # If more than two arrays
    # have been processed
    if (cnt >= 2):
        return 0;

    # If an already computed
    # subproblem occurred
    if (dp[i][j][k] != -1):
        return dp[i][j][k];

    ans = 0;

    # Explore all the possible pairs
    if (i < n1 and j < n2):

        # Recursive function call
        ans = max(ans, getMaxSum(i + 1, j + 1,
                                 k, arr1,
                                 arr2, arr3) +
                       arr1[i] * arr2[j]);

    if (i < n1 and k < n3):
        ans = max(ans, getMaxSum(i + 1, j,
                                 k + 1, arr1,
                                 arr2, arr3) +
                       arr1[i] * arr3[k]);

    if (j < n2 and k < n3):
        ans = max(ans, getMaxSum(i, j + 1,
                                 k + 1, arr1,
                                 arr2, arr3) +
                       arr2[j] * arr3[k]);

    # Memoize the maximum
    dp[i][j][k] = ans;

    # Returning the value
    return dp[i][j][k];

def reverse(tmp):
    i, k, t = 0, 0, 0;
    n = len(tmp);

    for i in range(n // 2):
        t = tmp[i];
        tmp[i] = tmp[n - i - 1];
        tmp[n - i - 1] = t;

# Function to return the maximum sum of
# products of pairs possible
def maxProductSum(arr1, arr2, arr3):
    # Initialising the dp array to -1
    for i in range(len(dp)):
        for j in range(len(dp[0])):
            for k in range(len(dp[j][0])):
                dp[i][j][k] = -1;

    # Sort the arrays in descending order
    arr1.sort();
    reverse(arr1);

    arr2.sort();
    reverse(arr2);

    arr3.sort();
    reverse(arr3);

    return getMaxSum(0, 0, 0,
                     arr1, arr2, arr3);

# Driver Code
if __name__ == '__main__':
  n1 = 2;
  arr1 = [3, 5];

  n2 = 2;
  arr2 = [2, 1];

  n3 = 3;
  arr3 = [4, 3, 5];

  print(maxProductSum(arr1, arr2, arr3));

# This code is contributed by Rajput-Ji
```

## **C#**

```
// C# program for above approach
using System;

class GFG{

const int maxN = 201;

// Variables which represent
// the size of the array
static int n1, n2, n3;

// Stores the results
static int[,,] dp = new int[maxN, maxN, maxN];

// Function to return the
// maximum possible sum
static int getMaxSum(int i, int j,
                     int k, int []arr1,
                     int []arr2, int []arr3)
{

    // Stores the count of
    // arrays processed
    int cnt = 0;

    if (i >= n1)
        cnt++;

    if (j >= n2)
        cnt++;

    if (k >= n3)
        cnt++;

    // If more than two arrays
    // have been processed
    if (cnt >= 2)
        return 0;

    // If an already computed
    // subproblem occurred
    if (dp[i, j, k] != -1)
        return dp[i, j, k];

    int ans = 0;

    // Explore all the possible pairs
    if (i < n1 && j < n2)

        // Recursive function call
        ans = Math.Max(ans,
                       getMaxSum(i + 1, j + 1, k,
                                 arr1, arr2, arr3) +
                                 arr1[i] * arr2[j]);

    if (i < n1 && k < n3)
        ans = Math.Max(ans,
                       getMaxSum(i + 1, j, k + 1,
                                 arr1, arr2, arr3) +
                                 arr1[i] * arr3[k]);

    if (j < n2 && k < n3)
        ans = Math.Max(ans,
                       getMaxSum(i, j + 1, k + 1,
                                 arr1, arr2, arr3) +
                                 arr2[j] * arr3[k]);

    // Memoize the maximum
    dp[i, j, k] = ans;

    // Returning the value
    return dp[i, j, k];
}

static void reverse(int[] tmp)
{
    int i, t;
    int n = tmp.Length;

    for(i = 0; i < n / 2; i++)
    {
        t = tmp[i];
        tmp[i] = tmp[n - i - 1];
        tmp[n - i - 1] = t;
    }
}

// Function to return the maximum sum of
// products of pairs possible
static int maxProductSum(int []arr1, int []arr2,
                         int []arr3)
{

    // Initialising the dp array to -1
    for(int i = 0; i < maxN; i++)
        for(int j = 0; j < maxN; j++)
            for(int k = 0; k < maxN; k++)
                dp[i, j, k] = -1;

    // Sort the arrays in descending order
    Array.Sort(arr1);
    reverse(arr1);

    Array.Sort(arr2);
    reverse(arr2);

    Array.Sort(arr3);
    reverse(arr3);

    return getMaxSum(0, 0, 0,
                     arr1, arr2, arr3);
}

// Driver Code
public static void Main (string[] args)
{
    n1 = 2;
    int []arr1 = { 3, 5 };

    n2 = 2;
    int []arr2 = { 2, 1 };

    n3 = 3;
    int []arr3 = { 4, 3, 5 };

    Console.Write(maxProductSum(arr1, arr2, arr3));
}
}

// This code is contributed by rutvik_56
```

## **java 描述语言**

```
<script>

// JavaScript Program to implement
// the above approach

var maxN = 201;

// Variables which represent
// the size of the array
var n1, n2, n3;

// Stores the results
var dp = Array.from(Array(maxN), ()=>Array(maxN));
for(var i =0; i<maxN; i++)
        for(var j =0; j<maxN; j++)
            dp[i][j] = new Array(maxN).fill(-1);

// Function to return the
// maximum possible sum
function getMaxSum(i, j, k, arr1, arr2, arr3)
{
    // Stores the count of
    // arrays processed
    var cnt = 0;

    if (i >= n1)
        cnt++;

    if (j >= n2)
        cnt++;

    if (k >= n3)
        cnt++;

    // If more than two arrays
    // have been processed
    if (cnt >= 2)
        return 0;

    // If an already computed
    // subproblem occurred
    if (dp[i][j][k] != -1)
        return dp[i][j][k];

    var ans = 0;

    // Explore all the possible pairs
    if (i < n1 && j < n2)

        // Recursive function call
        ans = Math.max(ans,
                  getMaxSum(i + 1, j + 1, k,
                            arr1, arr2, arr3)
                      + arr1[i] * arr2[j]);

    if (i < n1 && k < n3)
        ans = Math.max(ans,
                  getMaxSum(i + 1, j, k + 1,
                            arr1, arr2, arr3)
                      + arr1[i] * arr3[k]);

    if (j < n2 && k < n3)
        ans = Math.max(ans,
                  getMaxSum(i, j + 1, k + 1,
                            arr1, arr2, arr3)
                      + arr2[j] * arr3[k]);

    // Memoize the maximum
    dp[i][j][k] = ans;

    // Returning the value
    return dp[i][j][k];
}

// Function to return the maximum sum of
// products of pairs possible
function maxProductSum(arr1, arr2, arr3)
{

    // Sort the arrays in descending order
    arr1.sort();
    arr1.reverse();
    arr2.sort();
    arr2.reverse();
    arr3.sort();
    arr3.reverse();

    return getMaxSum(0, 0, 0,
                     arr1, arr2, arr3);
}

// Driver Code
n1 = 2;
var arr1 = [3, 5];
n2 = 2;
var arr2 = [2, 1];
n3 = 3;
var arr3 = [4, 3, 5];
document.write( maxProductSum(arr1, arr2, arr3));

</script>
```

****Output:** 

```
43
```** 

*****时间复杂度:**O((N1 * N2 * N3))*
***辅助空间:** O(N1 * N2 * N3)***