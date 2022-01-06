# 长度为 K 的非重叠子阵列的最大和

> 原文:[https://www . geeksforgeeks . org/最大不重叠长度子阵列-Atmos-k/](https://www.geeksforgeeks.org/maximum-sum-of-non-overlapping-subarrays-of-length-atmost-k/)

给定长度为 N 的整数阵列“arr”和整数“k”，选择一些不重叠的子阵列，使得每个子阵列的长度最多为**【k】，没有两个子阵列相邻，并且所选子阵列的所有元素的总和最大。
**例:**** 

```
**Input :** arr[] = {-1, 2, -3, 4, 5}, k = 2
**Output :** 11
Sub-arrays that maximizes sum will be {{2}, {4, 5}}.
Thus, the answer will be 2+4+5 = 11.

**Input :**arr[] = {1, 1, 1, 1, 1}, k = 1
**Output :** 3
```

****朴素方法**:一个简单的方法是递归生成所有可能满足上述条件的元素子集，找到和最大的子集。
**时间复杂度** : O(2 <sup>N</sup> )
**高效方法:**更好的方法是使用**动态编程**。
假设我们在指数‘I’处。
让 dp[i]定义为满足上述条件的子阵列{i，n-1}的所有可能子集的元素的最大和。
我们将有‘K+1’个可能的选择，即** 

1.  **拒绝“I”并求解“i+1”。**
2.  **选择子阵列{i}并求解“i+2”**
3.  **选择子阵列{i，i+1}并求解“i+3”**

**因此，递归关系将为:** 

```
dp[i] = max(dp[i+1], arr[i]+dp[i+2], arr[i]+arr[i+1]+dp[i+3],
        ...arr[i]+arr[i+1]+arr[i+2]...+arr[i+k-1] + dp[i+k+1])
```

**以下是上述方法的实现:** 

## **C++**

```
// C++ program to implement above approach
#include <bits/stdc++.h>
#define maxLen 10
using namespace std;

// Variable to store states of dp
int dp[maxLen];

// Variable to check if a given state has been solved
bool visit[maxLen];

// Function to find the maximum sum subsequence
// such that no two elements are adjacent
int maxSum(int arr[], int i, int n, int k)
{
    // Base case
    if (i >= n)
        return 0;

    // To check if a state has been solved
    if (visit[i])
        return dp[i];
    visit[i] = 1;

    // Variable to store
    // prefix sum for sub-array
    // {i, j}
    int tot = 0;
    dp[i] = maxSum(arr, i + 1, n, k);

    // Required recurrence relation
    for (int j = i; j < i + k and j < n; j++) {
        tot += arr[j];
        dp[i] = max(dp[i], tot +
                     maxSum(arr, j + 2, n, k));
    }

    // Returning the value
    return dp[i];
}

// Driver code
int main()
{
    // Input array
    int arr[] = { -1, 2, -3, 4, 5 };

    int k = 2;

    int n = sizeof(arr) / sizeof(int);

    cout << maxSum(arr, 0, n, k);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to implement above approach
import java.io.*;

class GFG
{

    static int maxLen = 10;

    // Variable to store states of dp
    static int dp[] = new int[maxLen];

    // Variable to check
    // if a given state has been solved
    static boolean []visit = new boolean[maxLen];

    // Function to find the maximum sum subsequence
    // such that no two elements are adjacent
    static int maxSum(int arr[], int i,
                    int n, int k)
    {
        // Base case
        if (i >= n)
            return 0;

        // To check if a state has been solved
        if (visit[i])
            return dp[i];
        visit[i] = true;

        // Variable to store
        // prefix sum for sub-array
        // {i, j}
        int tot = 0;
        dp[i] = maxSum(arr, i + 1, n, k);

        // Required recurrence relation
        for (int j = i; j < (i + k) &&
                            (j < n); j++)
        {
            tot += arr[j];
            dp[i] = Math.max(dp[i], tot +
                    maxSum(arr, j + 2, n, k));
        }

        // Returning the value
        return dp[i];
    }

    // Driver code
    public static void main (String[] args)
    {

        // Input array
        int arr[] = { -1, 2, -3, 4, 5 };

        int k = 2;

        int n = arr.length;

        System.out.println(maxSum(arr, 0, n, k));
    }
}

// This code is contributed by ajit.
```

## **蟒蛇 3**

```
# Python3 program to implement above approach
maxLen = 10

# Variable to store states of dp
dp = [0]*maxLen;

# Variable to check if a given state has been solved
visit = [0]*maxLen;

# Function to find the maximum sum subsequence
# such that no two elements are adjacent
def maxSum(arr, i, n, k) :

    # Base case
    if (i >= n) :
        return 0;

    # To check if a state has been solved
    if (visit[i]) :
        return dp[i];

    visit[i] = 1;

    # Variable to store
    # prefix sum for sub-array
    # {i, j}
    tot = 0;
    dp[i] = maxSum(arr, i + 1, n, k);

    # Required recurrence relation
    j = i
    while (j < i + k and j < n) :
        tot += arr[j];
        dp[i] = max(dp[i], tot +
                    maxSum(arr, j + 2, n, k));

        j += 1

    # Returning the value
    return dp[i];

# Driver code
if __name__ == "__main__" :

    # Input array
    arr = [ -1, 2, -3, 4, 5 ];

    k = 2;

    n = len(arr);

    print(maxSum(arr, 0, n, k));

# This code is contributed by AnkitRai01
```

## **C#**

```
// C# program to implement above approach
using System;

class GFG
{
static int maxLen = 10;

// Variable to store states of dp
static int []dp = new int[maxLen];

// Variable to check
// if a given state has been solved
static bool []visit = new bool[maxLen];

// Function to find the maximum sum subsequence
// such that no two elements are adjacent
static int maxSum(int []arr, int i,
                  int n, int k)
{
    // Base case
    if (i >= n)
        return 0;

    // To check if a state has been solved
    if (visit[i])
        return dp[i];
    visit[i] = true;

    // Variable to store
    // prefix sum for sub-array
    // {i, j}
    int tot = 0;
    dp[i] = maxSum(arr, i + 1, n, k);

    // Required recurrence relation
    for (int j = i; j < (i + k) &&
                        (j < n); j++)
    {
        tot += arr[j];
        dp[i] = Math.Max(dp[i], tot +
                  maxSum(arr, j + 2, n, k));
    }

    // Returning the value
    return dp[i];
}

// Driver code
static public void Main ()
{

    // Input array
    int []arr = { -1, 2, -3, 4, 5 };

    int k = 2;

    int n = arr.Length;

    Console.WriteLine (maxSum(arr, 0, n, k));
}
}

// This code is contributed by ajit.
```

## **java 描述语言**

```
<script>
    // Javascript program to implement above approach

    let maxLen = 10;

    // Variable to store states of dp
    let dp = new Array(maxLen);

    // Variable to check
    // if a given state has been solved
    let visit = new Array(maxLen);

    // Function to find the maximum sum subsequence
    // such that no two elements are adjacent
    function maxSum(arr, i, n, k)
    {
        // Base case
        if (i >= n)
            return 0;

        // To check if a state has been solved
        if (visit[i])
            return dp[i];
        visit[i] = true;

        // Variable to store
        // prefix sum for sub-array
        // {i, j}
        let tot = 0;
        dp[i] = maxSum(arr, i + 1, n, k);

        // Required recurrence relation
        for (let j = i; j < (i + k) &&
                            (j < n); j++)
        {
            tot += arr[j];
            dp[i] = Math.max(dp[i], tot +
                      maxSum(arr, j + 2, n, k));
        }

        // Returning the value
        return dp[i];
    }

    // Input array
    let arr = [ -1, 2, -3, 4, 5 ];

    let k = 2;

    let n = arr.length;

    document.write(maxSum(arr, 0, n, k));

</script>
```

****Output:** 

```
11
```** 

****时间复杂度:** O(n*k)**