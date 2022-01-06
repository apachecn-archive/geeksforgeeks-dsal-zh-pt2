# 一个数组中最长的子数组，它是另一个数组中的子序列

> 原文:[https://www . geesforgeks . org/最长数组子数组是另一个数组中的子序列/](https://www.geeksforgeeks.org/longest-subarray-of-an-array-which-is-a-subsequence-in-another-array/)

给定两个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr 1【】**和**arr 2【】**，任务是找到**arr 1【】**中最长的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，它是**arr 2【】**的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。

**示例:**

> **输入:** arr1[] = {4，2，3，1，5，6}，arr2[] = {3，1，4，6，5，2}
> **输出:** 3
> **解释:**arr 1[]的最长子阵列是 arr2[]中的子序列，它是{3，1，5}
> 
> **输入:** arr1[] = {3，2，4，7，1，5，6，8，10，9}，arr2[] = {9，2，4，3，1，5，6，8，10，7}
> **输出:** 5
> **解释:**arr 1[]中最长的子阵列是 arr2[]中的子序列，它是{1，5，6，8，10}。

**方法:**思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决这个问题。按照以下步骤解决问题:

*   初始化一个 **DP[][]** 表，其中 **DP[i][j]** 存储最长子阵列的长度，直到 **arr1[]** 中的第 i <sup>个</sup>索引，这是 **arr2[]** 中的一个子序列，直到第 **j 个<sup>个</sup>** 索引。
*   现在，[遍历两个数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下操作:
    *   **情况 1:** 如果 **arr1[i]** 和 **arr2[j]** 相等，则将 **1** 添加到**DP[I–1][j–1]**中，因为 **arr1[i]** 和 **arr2[j]** 贡献了最长子阵列所需的长度。
    *   **情况 2:** 如果 **arr1[i]** 和 **arr2[j]** 不相等，则设置**DP[I][j]= DP[I–1][j]**。
*   最后，打印 **DP[][]** 表中出现的最大值作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

    // Function to find the length of the
    // longest subarray in arr1[] which
    // is a subsequence in arr2[]
    int LongSubarrSeq(int arr1[], int arr2[], int M, int N)
    {
        // Length of the array arr1[]

        // Length of the required
        // longest subarray
        int maxL = 0;

        // Initialize DP[]array
        int DP[M + 1][N + 1];

        // Traverse array arr1[]
        for (int i = 1; i <= M; i++)
        {

            // Traverse array arr2[]
            for (int j = 1; j <= N; j++)
            {
                if (arr1[i - 1] == arr2[j - 1])
                {

                    // arr1[i - 1] contributes to
                    // the length of the subarray
                    DP[i][j] = 1 + DP[i - 1][j - 1];
                }

                // Otherwise
                else
                {

                    DP[i][j] = DP[i][j - 1];
                }
            }
        }

        // Find the maximum value
        // present in DP[][]
        for (int i = 1; i <= M; i++)
        {
            for (int j = 1; j <= N; j++)
            {
                maxL = max(maxL, DP[i][j]);
            }
        }

        // Return the result
        return maxL;
    }

// Driver Code
int main()
{
    int arr1[] = { 4, 2, 3, 1, 5, 6 };
    int M = sizeof(arr1) / sizeof(arr1[0]);

    int arr2[] = { 3, 1, 4, 6, 5, 2 };
    int N = sizeof(arr2) / sizeof(arr2[0]);

    // Function call to find the length
    // of the longest required subarray
    cout << LongSubarrSeq(arr1, arr2, M, N) <<endl;
    return 0;
}

// This code is contributed by code_hunt.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program
// for the above approach

import java.io.*;

class GFG {

    // Function to find the length of the
    // longest subarray in arr1[] which
    // is a subsequence in arr2[]
    private static int LongSubarrSeq(
        int[] arr1, int[] arr2)
    {
        // Length of the array arr1[]
        int M = arr1.length;

        // Length of the array arr2[]
        int N = arr2.length;

        // Length of the required
        // longest subarray
        int maxL = 0;

        // Initialize DP[]array
        int[][] DP = new int[M + 1][N + 1];

        // Traverse array arr1[]
        for (int i = 1; i <= M; i++) {

            // Traverse array arr2[]
            for (int j = 1; j <= N; j++) {

                if (arr1[i - 1] == arr2[j - 1]) {

                    // arr1[i - 1] contributes to
                    // the length of the subarray
                    DP[i][j] = 1 + DP[i - 1][j - 1];
                }

                // Otherwise
                else {

                    DP[i][j] = DP[i][j - 1];
                }
            }
        }

        // Find the maximum value
        // present in DP[][]
        for (int i = 1; i <= M; i++) {

            for (int j = 1; j <= N; j++) {

                maxL = Math.max(maxL, DP[i][j]);
            }
        }

        // Return the result
        return maxL;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr1 = { 4, 2, 3, 1, 5, 6 };
        int[] arr2 = { 3, 1, 4, 6, 5, 2 };

        // Function call to find the length
        // of the longest required subarray
        System.out.println(LongSubarrSeq(arr1, arr2));
    }
}
```

## 蟒蛇 3

```
# Python program
# for the above approach

# Function to find the length of the
# longest subarray in arr1 which
# is a subsequence in arr2
def LongSubarrSeq(arr1, arr2):

    # Length of the array arr1
    M = len(arr1);

    # Length of the array arr2
    N = len(arr2);

    # Length of the required
    # longest subarray
    maxL = 0;

    # Initialize DParray
    DP = [[0 for i in range(N + 1)] for j in range(M + 1)];

    # Traverse array arr1
    for i in range(1, M + 1):

        # Traverse array arr2
        for j in range(1, N + 1):
            if (arr1[i - 1] == arr2[j - 1]):

                # arr1[i - 1] contributes to
                # the length of the subarray
                DP[i][j] = 1 + DP[i - 1][j - 1];

            # Otherwise
            else:

                DP[i][j] = DP[i][j - 1];

    # Find the maximum value
    # present in DP
    for i in range(M + 1):

        # Traverse array arr2
        for j in range(1, N + 1):
            maxL = max(maxL, DP[i][j]);

    # Return the result
    return maxL;

# Driver Code
if __name__ == '__main__':
    arr1 = [4, 2, 3, 1, 5, 6];
    arr2 = [3, 1, 4, 6, 5, 2];

    # Function call to find the length
    # of the longest required subarray
    print(LongSubarrSeq(arr1, arr2));

    # This code contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the length of the
// longest subarray in arr1[] which
// is a subsequence in arr2[]
private static int LongSubarrSeq(int[] arr1,
                                 int[] arr2)
{

    // Length of the array arr1[]
    int M = arr1.Length;

    // Length of the array arr2[]
    int N = arr2.Length;

    // Length of the required
    // longest subarray
    int maxL = 0;

    // Initialize DP[]array
    int[,] DP = new int[M + 1, N + 1];

    // Traverse array arr1[]
    for(int i = 1; i <= M; i++)
    {

        // Traverse array arr2[]
        for(int j = 1; j <= N; j++)
        {
            if (arr1[i - 1] == arr2[j - 1])
            {

                // arr1[i - 1] contributes to
                // the length of the subarray
                DP[i, j] = 1 + DP[i - 1, j - 1];
            }

            // Otherwise
            else
            {
                DP[i, j] = DP[i, j - 1];
            }
        }
    }

    // Find the maximum value
    // present in DP[][]
    for(int i = 1; i <= M; i++)
    {
        for(int j = 1; j <= N; j++)
        {
            maxL = Math.Max(maxL, DP[i, j]);
        }
    }

    // Return the result
    return maxL;
}

// Driver Code
static public void Main()
{
    int[] arr1 = { 4, 2, 3, 1, 5, 6 };
    int[] arr2 = { 3, 1, 4, 6, 5, 2 };

    // Function call to find the length
    // of the longest required subarray
    Console.WriteLine(LongSubarrSeq(arr1, arr2));
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>
// javascript program of the above approach

    // Function to find the length of the
    // longest subarray in arr1[] which
    // is a subsequence in arr2[]
    function LongSubarrSeq(
        arr1, arr2)
    {
        // Length of the array arr1[]
        let M = arr1.length;

        // Length of the array arr2[]
        let N = arr2.length;

        // Length of the required
        // longest subarray
        let maxL = 0;

        // Initialize DP[]array
        let DP = new Array(M + 1);

        // Loop to create 2D array using 1D array
        for (var i = 0; i < DP.length; i++) {
            DP[i] = new Array(2);
        }

        for (var i = 0; i < DP.length; i++) {
            for (var j = 0; j < DP.length; j++) {
            DP[i][j] = 0;
        }
        }

        // Traverse array arr1[]
        for (let i = 1; i <= M; i++) {

            // Traverse array arr2[]
            for (let j = 1; j <= N; j++) {

                if (arr1[i - 1] == arr2[j - 1]) {

                    // arr1[i - 1] contributes to
                    // the length of the subarray
                    DP[i][j] = 1 + DP[i - 1][j - 1];
                }

                // Otherwise
                else {

                    DP[i][j] = DP[i][j - 1];
                }
            }
        }

        // Find the maximum value
        // present in DP[][]
        for (let i = 1; i <= M; i++) {

            for (let j = 1; j <= N; j++) {

                maxL = Math.max(maxL, DP[i][j]);
            }
        }

        // Return the result
        return maxL;
    }

    // Driver Code

        let arr1 = [ 4, 2, 3, 1, 5, 6 ];
        let arr2 = [ 3, 1, 4, 6, 5, 2 ];

        // Function call to find the length
        // of the longest required subarray
        document.write(LongSubarrSeq(arr1, arr2));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(M * N)*
***辅助空间:** O(M * N)*