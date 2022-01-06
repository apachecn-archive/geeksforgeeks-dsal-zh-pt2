# 计算从矩阵中移除对的方法，以便剩余的元素可以垂直或水平成对分组

> 原文:[https://www . geesforgeks . org/count-way-to-remove-pairs-from-a-matrix-so-剩余元素可以垂直或水平成对分组/](https://www.geeksforgeeks.org/count-ways-to-remove-pairs-from-a-matrix-such-that-remaining-elements-can-be-grouped-in-vertical-or-horizontal-pairs/)

给定一个整数 **K** 和一个正方形[矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**mat【】【】【】**大小为 **N * N** 且元素范围为**【1，K】**的矩阵，任务是计算移除不同矩阵元素对的方法，以便剩余元素可以垂直或水平排列成**对**。

**示例:**

> **输入:** mat[][] = {{1，2}，{3，4}}，K = 4
> **输出:** 4
> **解释:**
> 删除行{1，2}。因此，剩余的元素是{3，4}，它们可以排列成 2 个水平组。
> 类似地，移除对(1，3)、(3，4)和(2，4)也可以形成这样的布置。
> 
> **输入:** mat[][] = {{1，2，3}，{2，2，2}，{1，2，2}}，K = 3
> **输出:** 0

**方法:**该想法基于以下观察:

*   如果 N 是奇数，那么无论去掉哪一对，剩下的矩阵都不能被较小的矩阵覆盖。这是因为，当移除任何一对矩阵时，剩余的元素将是奇数，不可能使用 2×1 或 1×2 大小的矩阵来覆盖它们。
*   对于其他情况，只有当行索引、 **i** 和列索引、 **a** 的 **j** 之和为偶数且 **b** 之和为奇数时，才能在移除一对 **(a，b)** 后覆盖剩余的矩阵，反之亦然。

按照以下步骤解决问题:

*   [如果矩阵的大小是奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，那么打印 **0** 因为不可能有排列。
*   否则，检查以下内容:
    *   将变量**和**初始化为 **0** ，以存储所需的对的数量。
    *   初始化一个辅助矩阵， **dp[][]** 大小为 **K×2** ， **dp[i][0]** 表示行索引和列索引之和为偶数的矩阵 **mat[][]** 中 **i** 的出现次数， **dp[i][1]** 表示行索引和列索引之和为偶数的矩阵 **mat[][]** 中 **i** 的出现次数
    *   [使用行索引 **i** 和列索引 **j** 逐行遍历矩阵 mat**[]【**如果 **i** 和 **j** 的和为偶数，则将**DP[mat[I][j]–1][0]**增加 1，否则将**DP[mat[I][j]–1][1]**增加 **1**](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)
    *   使用变量 **i** 迭代范围**【0，K–1】**，并使用变量 **j** 嵌套迭代范围**【I+1，K–1】**:
        *   将 **dp[i][0] * dp[j][1]** 的值加到 **ans** 上，因为两个块的值不同，且 **(i + j)** 的值为奇数，而 **(i + j)** 的值为偶数。
        *   将 **dp[i][1] * dp[j][0]** 的值加到 **ans** 上，因为两个块的值不同， **(i + j)** 的值为偶数，而 **(i + j)** 的值为奇数
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count ways to remove pairs
// such that the remaining elements can
// be arranged in pairs vertically or horizontally
void numberofpairs(vector<vector<int> > v,
                   int k)
{
    // Store the size of matrix
    int n = v.size();

    // If N is odd, then no
    // such pair exists
    if (n % 2 == 1) {
        cout << 0;
        return;
    }

    // Store the number of
    // required pairs
    int ans = 0;

    // Initialize an auxiliary
    // matrix and fill it with 0s
    int dp[k][2];

    for (int i = 0; i < k; i++) {
        for (int j = 0; j < 2; j++) {
            dp[i][j] = 0;
        }
    }

    // Traverse the matrix v[][]
    for (int i = 0; i < n; i++) {

        for (int j = 0; j < n; j++) {

            // Check if i+j is odd or even
            if ((i + j) % 2 == 0)

                // Increment the value
                // dp[v[i][j]-1][0] by 1
                dp[v[i][j] - 1][0]++;
            else

                // Increment the value
                // dp[v[i][j]-1][1] by 1
                dp[v[i][j] - 1][1]++;
        }
    }

    // Iterate in range[0, k-1] using i
    for (int i = 0; i < k; i++) {

        // Iterate in range[i+1, k-1] using j
        for (int j = i + 1; j < k; j++) {

            // Update the ans
            ans += dp[i][0] * dp[j][1];
            ans += dp[i][1] * dp[j][0];
        }
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    vector<vector<int> > mat = { { 1, 2 }, { 3, 4 } };
    int K = 4;
    numberofpairs(mat, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG{

// Function to count ways to remove pairs
// such that the remaining elements can
// be arranged in pairs vertically or horizontally
static void numberofpairs(int[][] v, int k)
{

    // Store the size of matrix
    int n = v.length;

    // If N is odd, then no
    // such pair exists
    if (n % 2 == 1) {
        System.out.println(0);
        return;
    }

    // Store the number of
    // required pairs
    int ans = 0;

    // Initialize an auxiliary
    // matrix and fill it with 0s
    int dp[][] = new int[k][2];

    for (int i = 0; i < k; i++) {
        for (int j = 0; j < 2; j++) {
            dp[i][j] = 0;
        }
    }

    // Traverse the matrix v[][]
    for (int i = 0; i < n; i++) {

        for (int j = 0; j < n; j++) {

            // Check if i+j is odd or even
            if ((i + j) % 2 == 0)

                // Increment the value
                // dp[v[i][j]-1][0] by 1
                dp[v[i][j] - 1][0]++;
            else

                // Increment the value
                // dp[v[i][j]-1][1] by 1
                dp[v[i][j] - 1][1]++;
        }
    }

    // Iterate in range[0, k-1] using i
    for (int i = 0; i < k; i++) {

        // Iterate in range[i+1, k-1] using j
        for (int j = i + 1; j < k; j++) {

            // Update the ans
            ans += dp[i][0] * dp[j][1];
            ans += dp[i][1] * dp[j][0];
        }
    }

    // Print the answer
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{
    int[][] mat = { { 1, 2 }, { 3, 4 } };
    int K = 4;
    numberofpairs(mat, K);
}
}

// This code is contributed by susmitakundogoaldanga.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count ways to remove pairs
# such that the remaining elements can
# be arranged in pairs vertically or horizontally
def numberofpairs(v, k) :

    # Store the size of matrix
    n = len(v)

    # If N is odd, then no
    # such pair exists
    if (n % 2 == 1) :
        print(0)
        return

    # Store the number of
    # required pairs
    ans = 0

    # Initialize an auxiliary
    # matrix and fill it with 0s
    dp = [[0 for i in range(2)] for j in range(k)]

    for i in range(k) :
        for j in range(2) :
            dp[i][j] = 0

    # Traverse the matrix v[][]
    for i in range(n) :
        for j in range(n) :

            # Check if i+j is odd or even
            if ((i + j) % 2 == 0) :

                # Increment the value
                # dp[v[i][j]-1][0] by 1
                dp[v[i][j] - 1][0] += 1
            else :

                # Increment the value
                # dp[v[i][j]-1][1] by 1
                dp[v[i][j] - 1][1] += 1

    # Iterate in range[0, k-1] using i
    for i in range(k) :

        # Iterate in range[i+1, k-1] using j
        for j in range(i + 1, k) :

            # Update the ans
            ans += dp[i][0] * dp[j][1]
            ans += dp[i][1] * dp[j][0]

    # Print the answer
    print(ans)

    # Driver code
mat = [ [ 1, 2 ], [ 3, 4 ] ]
K = 4
numberofpairs(mat, K)

# This code is contributed by divyeshrabdiya07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to count ways to remove pairs
    // such that the remaining elements can
    // be arranged in pairs vertically or horizontally
    static void numberofpairs(List<List<int> > v,
                       int k)
    {

        // Store the size of matrix
        int n = v.Count;

        // If N is odd, then no
        // such pair exists
        if (n % 2 == 1) {
            Console.Write(0);
            return;
        }

        // Store the number of
        // required pairs
        int ans = 0;

        // Initialize an auxiliary
        // matrix and fill it with 0s
        int[,] dp = new int[k, 2];

        for (int i = 0; i < k; i++) {
            for (int j = 0; j < 2; j++) {
                dp[i, j] = 0;
            }
        }

        // Traverse the matrix v[][]
        for (int i = 0; i < n; i++) {

            for (int j = 0; j < n; j++) {

                // Check if i+j is odd or even
                if ((i + j) % 2 == 0)

                    // Increment the value
                    // dp[v[i][j]-1][0] by 1
                    dp[v[i][j] - 1, 0]++;
                else

                    // Increment the value
                    // dp[v[i][j]-1][1] by 1
                    dp[v[i][j] - 1, 1]++;
            }
        }

        // Iterate in range[0, k-1] using i
        for (int i = 0; i < k; i++) {

            // Iterate in range[i+1, k-1] using j
            for (int j = i + 1; j < k; j++) {

                // Update the ans
                ans += dp[i, 0] * dp[j, 1];
                ans += dp[i, 1] * dp[j, 0];
            }
        }

        // Print the answer
        Console.Write(ans);
    }

  // Driver code
  static void Main()
  {
    List<List<int> > mat = new List<List<int>>();
    mat.Add(new List<int>(new int[]{1, 2}));
    mat.Add(new List<int>(new int[]{3, 4}));
    int K = 4;
    numberofpairs(mat, K);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to count ways to remove pairs
    // such that the remaining elements can
    // be arranged in pairs
    // vertically or horizontally
    function numberofpairs(v, k)
    {

        // Store the size of matrix
        let n = v.length;

        // If N is odd, then no
        // such pair exists
        if (n % 2 == 1) {
            document.write(0);
            return;
        }

        // Store the number of
        // required pairs
        let ans = 0;

        // Initialize an auxiliary
        // matrix and fill it with 0s
        let dp = new Array(k);

        for (let i = 0; i < k; i++) {
            dp[i] = new Array(2);
            for (let j = 0; j < 2; j++) {
                dp[i][j] = 0;
            }
        }

        // Traverse the matrix v[][]
        for (let i = 0; i < n; i++) {

            for (let j = 0; j < n; j++) {

                // Check if i+j is odd or even
                if ((i + j) % 2 == 0)

                    // Increment the value
                    // dp[v[i][j]-1][0] by 1
                    dp[v[i][j] - 1][0]++;
                else

                    // Increment the value
                    // dp[v[i][j]-1][1] by 1
                    dp[v[i][j] - 1][1]++;
            }
        }

        // Iterate in range[0, k-1] using i
        for (let i = 0; i < k; i++) {

            // Iterate in range[i+1, k-1] using j
            for (let j = i + 1; j < k; j++) {

                // Update the ans
                ans += dp[i][0] * dp[j][1];
                ans += dp[i][1] * dp[j][0];
            }
        }

        // Print the answer
        document.write(ans + "</br>");
    }

    let mat = [ [ 1, 2 ], [ 3, 4 ] ];
    let K = 4;
    numberofpairs(mat, K);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>+K<sup>2</sup>)*
***辅助空间:** O(K)*