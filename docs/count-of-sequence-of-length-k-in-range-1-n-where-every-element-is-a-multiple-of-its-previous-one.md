# 长度为 K 的序列在[1，N]范围内的计数，其中每个元素都是其前一个元素的倍数

> 原文:[https://www . geeksforgeeks . org/长度为 1-n 的 k 序列计数，其中每个元素都是其前一个元素的倍数/](https://www.geeksforgeeks.org/count-of-sequence-of-length-k-in-range-1-n-where-every-element-is-a-multiple-of-its-previous-one/)

给定两个整数 **N** 和 **K，**，任务是从范围**【1，N】**中找出 **K** 元素的序列数，其中每个元素都是前一个元素的倍数。

**示例:**

> **输入:** N = 4，K = 3
> **输出:** 13
> **解释:**具有 3 个元素的整数 1、2、3、4 可以组成的序列是:{1、1、1}、{2、2、2}、{3、3、3}、{4、4、4}、{1、1、2}、{1、2、2}、{1、2、4}、{1、1、3}、{1、3
> 
> **输入:** N = 9，K = 5
> T3】输出: 111

**方法:**给定的问题可以通过[递归](https://www.geeksforgeeks.org/recursion/)和[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)来解决。按照以下步骤解决问题:

*   创建一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **dp[][]** ，它存储[记忆的状态](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)，其中 **dp[i][j]** 表示长度为 **i** 的序列的计数，其中 **j** 是它们的第一个元素。
*   创建[递归函数](https://www.geeksforgeeks.org/recursive-functions/)**countsquencheutil()**，以序列长度和起始元素为自变量，将下一个元素设置为当前元素的**倍数**，递归调用剩余序列。
*   将计算出的状态的答案存储在 **dp[][]** 数组中，如果某个状态的值已经计算过，则返回该值。
*   创建一个函数 **countSequence()** ，该函数遍历序列中所有可能的起始元素，并调用递归函数来计算具有该起始元素的 **K** 元素的序列。
*   在变量**和**中保持每个起始元素的计算计数之和，这是要求的值。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Initialize the dp matrix
int static dp[1001][1001];

// Function to find the count of sequences of K
// elements with first element as m where every
// element is a multiple of the previous one
int countSequenceUtil(int k, int m, int n)
{
    // Base case
    if (k == 1) {
        return 1;
    }

    // If the value already exists
    // in the DP then return it
    if (dp[k][m] != -1) {
        return dp[k][m];
    }

    // Variable to store the count
    int res = 0;

    for (int i = 1; i <= (n / m); i++) {

        // Recursive Call
        res += countSequenceUtil(k - 1,
                                 m * i, n);
    }

    // Store the calculated
    // answer and return it
    return dp[k][m] = res;
}

// Function to find count of sequences of K
// elements in the range [1, n] where every
// element is a multiple of the previous one
int countSequence(int N, int K)
{
    // Initializing all values
    // of dp with -1
    memset(dp, -1, sizeof(dp));

    // Variable to store
    // the total count
    int ans = 0;

    // Iterate from 1 to N
    for (int i = 1; i <= N; i++) {
        ans += countSequenceUtil(K, i, N);
    }

    // Return ans
    return ans;
}

// Driver Code
int main()
{
    int N = 9;
    int K = 5;

    cout << countSequence(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

// Initialize the dp matrix
static int dp[][] = new int[1001][1001];

// Function to find the count of sequences of K
// elements with first element as m where every
// element is a multiple of the previous one
static int countSequenceUtil(int k, int m, int n)
{
    // Base case
    if (k == 1) {
        return 1;
    }

    // If the value already exists
    // in the DP then return it
    if (dp[k][m] != -1) {
        return dp[k][m];
    }

    // Variable to store the count
    int res = 0;

    for (int i = 1; i <= (n / m); i++) {

        // Recursive Call
        res += countSequenceUtil(k - 1,
                                 m * i, n);
    }

    // Store the calculated
    // answer and return it
    return dp[k][m] = res;
}

// Function to find count of sequences of K
// elements in the range [1, n] where every
// element is a multiple of the previous one
static int countSequence(int N, int K)
{

    // Initializing all values
    // of dp with -1
     for(int i=0;i<dp.length;i++)
     {
       for(int j=0;j<dp[i].length;j++)
       {
         dp[i][j]=-1;
       }
     }

    // Variable to store
    // the total count
    int ans = 0;

    // Iterate from 1 to N
    for (int i = 1; i <= N; i++) {
        ans += countSequenceUtil(K, i, N);
    }

    // Return ans
    return ans;
}

// Driver Code
    public static void main (String[] args) {
      int N = 9;
    int K = 5;

        System.out.println(countSequence(N, K));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python implementation for the above approach

# Initialize the dp matrix
dp = [[-1 for i in range(1001)] for j in range(1001)]

# Function to find the count of sequences of K
# elements with first element as m where every
# element is a multiple of the previous one
def countSequenceUtil(k, m, n):

    # Base case
    if (k == 1):
        return 1

    # If the value already exists
    # in the DP then return it
    if (dp[k][m] != -1):
        return dp[k][m]

    # Variable to store the count
    res = 0

    for i in range(1, (n // m) + 1):

        # Recursive Call
        res += countSequenceUtil(k - 1,
                                 m * i, n)

    # Store the calculated
    # answer and return it
    dp[k][m] = res

    return dp[k][m]

# Function to find count of sequences of K
# elements in the range [1, n] where every
# element is a multiple of the previous one
def countSequence(N, K):

    # Variable to store
    # the total count
    ans = 0

    # Iterate from 1 to N
    for i in range(1, N + 1):
        ans += countSequenceUtil(K, i, N)

    # Return ans
    return ans

# Driver Code
N = 9
K = 5

print(countSequence(N, K))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Initialize the dp matrix
    static int[, ] dp = new int[1001, 1001];

    // Function to find the count of sequences of K
    // elements with first element as m where every
    // element is a multiple of the previous one
    static int countSequenceUtil(int k, int m, int n)
    {

        // Base case
        if (k == 1) {
            return 1;
        }

        // If the value already exists
        // in the DP then return it
        if (dp[k, m] != -1) {
            return dp[k, m];
        }

        // Variable to store the count
        int res = 0;

        for (int i = 1; i <= (n / m); i++) {

            // Recursive Call
            res += countSequenceUtil(k - 1, m * i, n);
        }

        // Store the calculated
        // answer and return it
        return dp[k, m] = res;
    }

    // Function to find count of sequences of K
    // elements in the range [1, n] where every
    // element is a multiple of the previous one
    static int countSequence(int N, int K)
    {

        // Initializing all values
        // of dp with -1
        for (int i = 0; i < dp.GetLength(0); i++) {
            for (int j = 0; j < dp.GetLength(1); j++) {
                dp[i, j] = -1;
            }
        }

        // Variable to store
        // the total count
        int ans = 0;

        // Iterate from 1 to N
        for (int i = 1; i <= N; i++) {
            ans += countSequenceUtil(K, i, N);
        }

        // Return ans
        return ans;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int N = 9;
        int K = 5;

        Console.WriteLine(countSequence(N, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
    // JavaScript implementation for the above approach

    // Initialize the dp matrix
    let dp = new Array(1001).fill(-1).map(() => new Array(1001).fill(-1));

    // Function to find the count of sequences of K
    // elements with first element as m where every
    // element is a multiple of the previous one
    const countSequenceUtil = (k, m, n) => {

        // Base case
        if (k == 1) {
            return 1;
        }

        // If the value already exists
        // in the DP then return it
        if (dp[k][m] != -1) {
            return dp[k][m];
        }

        // Variable to store the count
        let res = 0;

        for (let i = 1; i <= parseInt(n / m); i++) {

            // Recursive Call
            res += countSequenceUtil(k - 1,
                m * i, n);
        }

        // Store the calculated
        // answer and return it
        return dp[k][m] = res;
    }

    // Function to find count of sequences of K
    // elements in the range [1, n] where every
    // element is a multiple of the previous one
    const countSequence = (N, K) => {

        // Variable to store
        // the total count
        let ans = 0;

        // Iterate from 1 to N
        for (let i = 1; i <= N; i++) {
            ans += countSequenceUtil(K, i, N);
        }

        // Return ans
        return ans;
    }

    // Driver Code
    let N = 9;
    let K = 5;

    document.write(countSequence(N, K));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
111
```

***时间复杂度:**O(N * K * log N)*
T5**辅助空间:** O(N*K)