# 最大化从数组中移除的元素的相邻元素的乘积之和

> 原文:[https://www . geeksforgeeks . org/从数组中移除元素的相邻元素乘积之和最大化/](https://www.geeksforgeeks.org/maximize-sum-of-product-of-neighbouring-elements-of-the-element-removed-from-array/)

给定一个大小为 **N** 的数组 **A[]** ，任务是找到这个数组的最大可能得分。通过对数组执行以下操作来计算数组的分数，直到数组的大小大于 2:

*   选择一个索引 **i** ，这样 **1 < i < N** 。
*   分数中加入 **A[i-1] * A[i+1]**
*   从阵列中移除 **A[i]** 。

**示例:**

> **输入:** A[] = {1，2，3，4}
> **输出:** 12
> **说明:**
> 第一次操作，选择 i = 2。分数将增加 A[1] * A[3] = 2 * 4 = 8。删除 A[2]后的新数组将是{1，2，4}。
> 在第一个操作中，选择 i = 1。分数将增加 A[0] * A[2] = 1 * 4 = 4。删除 A[2]后的新数组将是{1，4}。
> 由于 N < = 2，因此无法再进行操作。
> 总分将为 8 + 4 = 12，这是所有可能选择中的最大值。
> 
> **输入:** {1，55}
> **输出:** 0
> **说明:**不可能有有效招式。

**方法:**给定的问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)基于以下观察来解决:

*   考虑一个 2D 阵列，比如说 **dp[][]** ，其中 **dp[i][j]** 代表子阵列中从索引 **i** 到 **j** 的最大可能得分。
*   以递增的顺序遍历范围**【1，N-1】**中所有长度 **len** 的子阵列，其中 **i** 表示当前长度子阵列的开始，而 **j** 表示结束索引。
*   可以观察到，对于从 **i** 到 **j** 的子阵列，除了 **i** 和 **j** 之外，最后剩余元素 k 的指数可以在**【I+1，j-1】**的范围内。因此，迭代所有可能的 **k** 值。因此，差压关系可以表述如下:

> **dp[i][j] =范围内所有 k 的最大值(dp[i][j]，DP[I][k]+DP[k][j]+A[I]* A[j])****【I+1，j-1】**

*   最终答案将是 **dp[0][N-1]。**

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the dp state where dp[i][j]
// represents the maximum possible score
// in the subarray from index i to j
int dp[101][101];

// Function to calculate maximum possible
// score using the given operations
int maxMergingScore(int A[], int N)
{
    // Iterate through all possible
    // lengths of the subarray
    for (int len = 1; len < N; ++len) {

        // Iterate through all the
        // possible starting indices i
        // having length len
        for (int i = 0; i + len < N; ++i) {

            // Stores the rightmost index
            // of the current subarray
            int j = i + len;

            // Initial dp[i][j] will be 0.
            dp[i][j] = 0;

            // Iterate through all possible
            // values of k in range [i+1, j-1]
            for (int k = i + 1; k < j; ++k) {
                dp[i][j] = max(
                    dp[i][j],
                    dp[i][k] + dp[k][j]
                        + A[i] * A[j]);
            }
        }
    }

    // Return the answer
    return dp[0][N - 1];
}

// Driver Code
int main()
{
    int N = 4;
    int A[] = { 1, 2, 3, 4 };

    // Function Call
    cout << maxMergingScore(A, N) << endl;

    N = 2;
    int B[] = { 1, 55 };

    // Function Call
    cout << maxMergingScore(B, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

  // Stores the dp state where dp[i][j]
  // represents the maximum possible score
  // in the subarray from index i to j
  static int maxMergingScore(int A[], int N)
  {
    int[][] dp = new int[101][101];
    for(int i = 0; i < 101; i++)
    {
      {
        for(int j = 0; j < 101; j++)
          dp[i][j] = 0;
      }
    }

    // Iterate through all possible
    // lengths of the subarray
    for (int len = 1; len < N; ++len) {

      // Iterate through all the
      // possible starting indices i
      // having length len
      for (int i = 0; i + len < N; ++i) {

        // Stores the rightmost index
        // of the current subarray
        int j = i + len;

        // Initial dp[i][j] will be 0.
        dp[i][j] = 0;

        // Iterate through all possible
        // values of k in range [i+1, j-1]
        for (int k = i + 1; k < j; ++k) {
          dp[i][j] = Math.max(
            dp[i][j],
            dp[i][k] + dp[k][j]
            + A[i] * A[j]);
        }
      }
    }

    // Return the answer
    return dp[0][N - 1];
  }

  // Driver Code
  public static void main(String[] args)
  {
    int N = 4;
    int A[] = { 1, 2, 3, 4 };

    // Function Call
    System.out.println(maxMergingScore(A, N) );

    N = 2;
    int B[] = { 1, 55 };

    // Function Call
    System.out.println(maxMergingScore(B, N) );
  }
}

// This code is contributed by dwivediyash
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

  // Stores the dp state where dp[i][j]
  // represents the maximum possible score
  // in the subarray from index i to j
  static int maxMergingScore(int []A, int N)
  {
    int[,] dp = new int[101,101];
    for(int i = 0; i < 101; i++)
    {
      {
        for(int j = 0; j < 101; j++)
          dp[i, j] = 0;
      }
    }

    // Iterate through all possible
    // lengths of the subarray
    for (int len = 1; len < N; ++len) {

      // Iterate through all the
      // possible starting indices i
      // having length len
      for (int i = 0; i + len < N; ++i) {

        // Stores the rightmost index
        // of the current subarray
        int j = i + len;

        // Initial dp[i][j] will be 0.
        dp[i,j] = 0;

        // Iterate through all possible
        // values of k in range [i+1, j-1]
        for (int k = i + 1; k < j; ++k) {
          dp[i,j] = Math.Max(
            dp[i,j],
            dp[i,k] + dp[k,j]
            + A[i] * A[j]);
        }
      }
    }

    // Return the answer
    return dp[0,N - 1];
  }

  // Driver Code
    static public void Main (){

    int N = 4;
    int []A = { 1, 2, 3, 4 };

    // Function Call
    Console.WriteLine(maxMergingScore(A, N) );

    N = 2;
    int[] B = { 1, 55 };

    // Function Call
    Console.WriteLine(maxMergingScore(B, N) );
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python 3 implementation for the above approach

# Stores the dp state where dp[i][j]
# represents the maximum possible score
# in the subarray from index i to j

# Function to calculate maximum possible
# score using the given operations
def maxMergingScore(A, N):

    # Iterate through all possible
    # len1gths of the subarray
    dp = [[0 for i in range(101)] for j in range(101)]
    for len1 in range(1,N,1):

        # Iterate through all the
        # possible starting indices i
        # having len1gth len1
        for i in range(0, N - len1, 1):

            # Stores the rightmost index
            # of the current subarray
            j = i + len1

            # Initial dp[i][j] will be 0.
            dp[i][j] = 0

            # Iterate through all possible
            # values of k in range [i+1, j-1]
            for k in range(i + 1, j, 1):
                dp[i][j] = max(dp[i][j],dp[i][k] + dp[k][j] + A[i] * A[j])

    # Return the answer
    return dp[0][N - 1]

# Driver Code
if __name__ == '__main__':
    N = 4
    A = [1, 2, 3, 4]

    # Function Call
    print(maxMergingScore(A, N))

    N = 2
    B = [1, 55]

    # Function Call
    print(maxMergingScore(B, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Stores the dp state where dp[i][j]
        // represents the maximum possible score
        // in the subarray from index i to j
        let dp = Array(101).fill().map(() => Array(101));

        // Function to calculate maximum possible
        // score using the given operations
        function maxMergingScore(A, N)
        {

            // Iterate through all possible
            // lengths of the subarray
            for (let len = 1; len < N; ++len) {

                // Iterate through all the
                // possible starting indices i
                // having length len
                for (let i = 0; i + len < N; ++i) {

                    // Stores the rightmost index
                    // of the current subarray
                    let j = i + len;

                    // Initial dp[i][j] will be 0.
                    dp[i][j] = 0;

                    // Iterate through all possible
                    // values of k in range [i+1, j-1]
                    for (let k = i + 1; k < j; ++k) {
                        dp[i][j] = Math.max(
                            dp[i][j],
                            dp[i][k] + dp[k][j]
                            + A[i] * A[j]);
                    }
                }
            }

            // Return the answer
            return dp[0][N - 1];
        }

        // Driver Code
        let N = 4;
        let A = [1, 2, 3, 4];

        // Function Call
        document.write(maxMergingScore(A, N) + "<br>");

        N = 2;
        let B = [1, 55];

        // Function Call
        document.write(maxMergingScore(B, N) + "<br>");

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
12
0
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*