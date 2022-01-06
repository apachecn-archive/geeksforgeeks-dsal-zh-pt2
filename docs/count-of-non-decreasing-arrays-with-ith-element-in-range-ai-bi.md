# 元素在范围[A[i]，B[i]]

内的非递减数组的计数

> 原文:[https://www . geeksforgeeks . org/带范围内元素的非递减数组计数-ai-bi/](https://www.geeksforgeeks.org/count-of-non-decreasing-arrays-with-ith-element-in-range-ai-bi/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** ，这两个数组都由 **N** 个整数组成，任务是找到大小为 **N** 的非递减数组的数量，这些数组可以被形成为使得每个数组元素位于**【A[I]，B[I]】**的范围内。

**示例:**

> **输入:** A[] = {1，1}，B[] = {2，3}
> T3】输出 : 5
> **解释:**
> 有效数组的总数为{1，1}、{1，2}、{1，3}、{2，2}、{2，3 }。因此，此类数组的数量为 5。
> 
> **输入:** A[] = {3，4，5}，B[] = {4，5，6 }
> T3】输出: 8

**方法:**给定的问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)和[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)来解决。按照以下步骤解决问题:

*   用值 **0** 初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **dp[][]** ，其中 **dp[i][j]** 表示到位置 **i** 的总有效数组，当前元素为 **j** 。将 **dp[0][0]** 初始化为 **1** 。
*   用值 **0** 初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **pref[][]** ，以存储数组的[前缀和。](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，B【N–1】】**，并将**pref【0】【I】**的值设置为 **1** 。
*   使用变量 **i** 迭代范围**【1，N】**，并执行以下步骤:
    *   使用变量 **j** 迭代范围**【A[I–1]、B[I–1]】**，并将 **dp[i][j]** 的值增加**pref[I–1][j]**，将 **pref[i][j]** 的值增加 **dp[i][j]** 。
    *   使用变量 **j** 迭代范围**【0，B【N–1】】**，如果 **j** 大于 **0** ，则通过将 **pref[i][j]** 的值增加**pref[I][j–1]**来更新前缀和表。
*   将变量**和**初始化为 **0** ，以存储形成的数组的结果计数。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【A[N–1]、B[N–1]】**，并将 **dp[N][i]** 的值添加到变量 **ans** 中。
*   执行上述步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the total number
// of possible valid arrays
int totalValidArrays(int a[], int b[],
                     int N)
{
    // Make a 2D DP table
    int dp[N + 1][b[N - 1] + 1];

    // Make a 2D prefix sum table
    int pref[N + 1][b[N - 1] + 1];

    // Initialize all values to 0
    memset(dp, 0, sizeof(dp)),
        memset(pref, 0, sizeof(pref));

    // Base Case
    dp[0][0] = 1;

    // Initialize the prefix values
    for (int i = 0; i <= b[N - 1]; i++) {
        pref[0][i] = 1;
    }

    // Iterate over the range and update
    // the dp table accordingly
    for (int i = 1; i <= N; i++) {
        for (int j = a[i - 1];
             j <= b[i - 1]; j++) {
            dp[i][j] += pref[i - 1][j];

            // Add the dp values to the
            // prefix sum
            pref[i][j] += dp[i][j];
        }

        // Update the prefix sum table
        for (int j = 0; j <= b[N - 1]; j++) {
            if (j > 0) {
                pref[i][j] += pref[i][j - 1];
            }
        }
    }

    // Find the result count of
    // arrays formed
    int ans = 0;
    for (int i = a[N - 1];
         i <= b[N - 1]; i++) {
        ans += dp[N][i];
    }

    // Return the total count of arrays
    return ans;
}

// Driver Code
int main()
{
    int A[] = { 1, 1 };
    int B[] = { 2, 3 };
    int N = sizeof(A) / sizeof(A[0]);

    cout << totalValidArrays(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to count the total number
    // of possible valid arrays
    static int totalValidArrays(int a[], int b[],
                         int N)
    {
        // Make a 2D DP table
        int dp[][] = new int[N + 1][b[N - 1] + 1];

        // Make a 2D prefix sum table
        int pref[][] = new int[N + 1][b[N - 1] + 1];

        // Initialize all values to 0
        for (int i = 0; i < N + 1; i++)
            for (int j = 0; j < b[N - 1] + 1; j++)
                dp[i][j] = 0;

        for (int i = 0; i < N + 1; i++)
            for (int j = 0; j < b[N - 1] + 1; j++)
                pref[i][j] = 0;       

        // Base Case
        dp[0][0] = 1;

        // Initialize the prefix values
        for (int i = 0; i <= b[N - 1]; i++) {
            pref[0][i] = 1;
        }

        // Iterate over the range and update
        // the dp table accordingly
        for (int i = 1; i <= N; i++) {
            for (int j = a[i - 1];
                 j <= b[i - 1]; j++) {
                dp[i][j] += pref[i - 1][j];

                // Add the dp values to the
                // prefix sum
                pref[i][j] += dp[i][j];
            }

            // Update the prefix sum table
            for (int j = 0; j <= b[N - 1]; j++) {
                if (j > 0) {
                    pref[i][j] += pref[i][j - 1];
                }
            }
        }

        // Find the result count of
        // arrays formed
        int ans = 0;
        for (int i = a[N - 1];
             i <= b[N - 1]; i++) {
            ans += dp[N][i];
        }

        // Return the total count of arrays
        return ans;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int A[] = { 1, 1 };
        int B[] = { 2, 3 };
        int N = A.length;

        System.out.println(totalValidArrays(A, B, N));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# python program for the above approach

# Function to count the total number
# of possible valid arrays
def totalValidArrays(a, b, N):

    # Make a 2D DP table
    dp = [[0 for _ in range(b[N - 1] + 1)] for _ in range(N + 1)]

    # Make a 2D prefix sum table
    pref = [[0 for _ in range(b[N - 1] + 1)] for _ in range(N + 1)]

    # Base Case
    dp[0][0] = 1

    # Initialize the prefix values
    for i in range(0, b[N - 1] + 1):
        pref[0][i] = 1

    # Iterate over the range and update
    # the dp table accordingly
    for i in range(1, N + 1):
        for j in range(a[i - 1], b[i - 1] + 1):
            dp[i][j] += pref[i - 1][j]

            # Add the dp values to the
            # prefix sum
            pref[i][j] += dp[i][j]

        # Update the prefix sum table
        for j in range(0, b[N - 1] + 1):
            if (j > 0):
                pref[i][j] += pref[i][j - 1]

    # Find the result count of
    # arrays formed
    ans = 0
    for i in range(a[N - 1], b[N - 1] + 1):
        ans += dp[N][i]

    # Return the total count of arrays
    return ans

# Driver Code
if __name__ == "__main__":

    A = [1, 1]
    B = [2, 3]
    N = len(A)

    print(totalValidArrays(A, B, N))

    # This code is contributed by rakeshsahni
```

## C#

```
// C#  program for the above approach
using System;
class GFG
{

  // Function to count the total number
  // of possible valid arrays
  static int totalValidArrays(int[] a, int[] b, int N)
  {
    // Make a 2D DP table
    int[,] dp = new int[N + 1, b[N - 1] + 1];

    // Make a 2D prefix sum table
    int[,] pref = new int[N + 1, b[N - 1] + 1];

    // Initialize all values to 0
    for (int i = 0; i < N + 1; i++)
      for (int j = 0; j < b[N - 1] + 1; j++)
        dp[i, j] = 0;

    for (int i = 0; i < N + 1; i++)
      for (int j = 0; j < b[N - 1] + 1; j++)
        pref[i, j] = 0;       

    // Base Case
    dp[0, 0] = 1;

    // Initialize the prefix values
    for (int i = 0; i <= b[N - 1]; i++) {
      pref[0, i] = 1;
    }

    // Iterate over the range and update
    // the dp table accordingly
    for (int i = 1; i <= N; i++) {
      for (int j = a[i - 1];
           j <= b[i - 1]; j++) {
        dp[i, j] += pref[i - 1, j];

        // Add the dp values to the
        // prefix sum
        pref[i, j] += dp[i, j];
      }

      // Update the prefix sum table
      for (int j = 0; j <= b[N - 1]; j++) {
        if (j > 0) {
          pref[i, j] += pref[i, j - 1];
        }
      }
    }

    // Find the result count of
    // arrays formed
    int ans = 0;
    for (int i = a[N - 1];
         i <= b[N - 1]; i++) {
      ans += dp[N, i];
    }

    // Return the total count of arrays
    return ans;
  }

  // Driver Code
  public static void Main ()
  {  
    int[] A = { 1, 1 };
    int[] B = { 2, 3 };
    int N = A.Length;

    Console.WriteLine(totalValidArrays(A, B, N));
  }
}

// This code is contributed by Saurabh
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to count the total number
    // of possible valid arrays
    const totalValidArrays = (a, b, N) => {
        // Make a 2D DP table
        let dp = new Array(N + 1).fill(0).map(() => new Array(b[N - 1] + 1).fill(0));

        // Make a 2D prefix sum table
        let pref = new Array(N + 1).fill(0).map(() => new Array(b[N - 1] + 1).fill(0));

        // Base Case
        dp[0][0] = 1;

        // Initialize the prefix values
        for (let i = 0; i <= b[N - 1]; i++) {
            pref[0][i] = 1;
        }

        // Iterate over the range and update
        // the dp table accordingly
        for (let i = 1; i <= N; i++) {
            for (let j = a[i - 1];
                j <= b[i - 1]; j++) {
                dp[i][j] += pref[i - 1][j];

                // Add the dp values to the
                // prefix sum
                pref[i][j] += dp[i][j];
            }

            // Update the prefix sum table
            for (let j = 0; j <= b[N - 1]; j++) {
                if (j > 0) {
                    pref[i][j] += pref[i][j - 1];
                }
            }
        }

        // Find the result count of
        // arrays formed
        let ans = 0;
        for (let i = a[N - 1];
            i <= b[N - 1]; i++) {
            ans += dp[N][i];
        }

        // Return the total count of arrays
        return ans;
    }

    // Driver Code
    let A = [1, 1];
    let B = [2, 3];
    let N = A.length;

    document.write(totalValidArrays(A, B, N));

// This code is contributed by rakeshsahni

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N*M)，其中 M 是数组 B[]的最后一个元素。*
***辅助空间:** O(N*M)，其中 M 是数组 B[]的最后一个元素。*