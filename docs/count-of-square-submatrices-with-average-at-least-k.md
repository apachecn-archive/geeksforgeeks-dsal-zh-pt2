# 平均值至少为 K 的正方形子矩阵的计数

> 原文:[https://www . geeksforgeeks . org/平方计数至少为 k 的子矩阵/](https://www.geeksforgeeks.org/count-of-square-submatrices-with-average-at-least-k/)

给定一个大小为 **NxM** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**arr【】【】**和一个整数 **K** ，任务是找出给定矩阵中元素平均值大于或等于 **K** 的正方形子矩阵的个数。

**示例:**

> **输入:** K = 4，arr[][] = {{2，2，3}，{3，4，5}，{4，5，5}}
> **输出:** 7
> **解释:**
> 以下正方形子矩阵的平均值大于或等于 K:
> 
> 1.  取位置{(2，2)}的元素形成的(1×1)维的正方形子矩阵。子矩阵的平均值等于 4。
> 2.  取位置为{(2，3)}的元素形成的维数为(1×1)的正方形子矩阵。子矩阵的平均值等于 5。
> 3.  取位置{(3，1)}的元素形成的(1×1)维的正方形子矩阵。子矩阵的平均值等于 4。
> 4.  取位置为{(3，2)}的元素形成的维数为(1×1)的正方形子矩阵。子矩阵的平均值等于 5。
> 5.  取位置为{(3，3)}的元素形成的维数为(1×1)的正方形子矩阵。子矩阵的平均值等于 5。
> 6.  取位置{(2，1)、(2，2)、(3，1)、(3，2)}的元素形成的(2×2)维的正方形子矩阵。子矩阵的平均值等于(3+4+4+5 = 16)/4 = 4。
> 7.  取位置{(2，2)，(2，3)，(3，2)，(3，2)，(3，3，3)的元素形成的(2×2)维的正方形子矩阵。子矩阵的平均值等于(4+5+5+5 = 19)/4 = 4.75。
> 
> 因此，总共有 7 个平均大于或等于 k 的正方形子矩阵。
> 
> **输入:** K = 3，arr[][] = {{1，1，1}，{1，1，1}}
> **输出:** 0

**天真方法:**最简单的方法是生成所有可能的正方形子矩阵，并检查[子正方形所有元素的和](https://www.geeksforgeeks.org/given-n-x-n-square-matrix-find-sum-sub-squares-size-k-x-k/)是否大于或等于 **K** 乘以子矩阵的大小。

***时间复杂度:**O(N<sup>3</sup>* M<sup>3</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以使用[前缀和矩阵](https://www.geeksforgeeks.org/prefix-sum-2d-array/)进行优化，这导致子矩阵和的时间计算恒定。按照以下步骤解决问题:

*   初始化一个变量，说**计数**为 **0** 存储平均值大于等于 **K** 的子矩阵的计数。
*   计算矩阵 **arr[][]** 的[前缀和，并将其存储在向量的](https://www.geeksforgeeks.org/prefix-sum-2d-array/)[向量中](https://www.geeksforgeeks.org/vector-of-vectors-in-c-stl-with-examples/)表示 **pre[][]** 。
*   [使用变量 **i** 和 **j** 遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)的每个元素，并执行以下步骤:
    *   初始化两个变量，说 **l** 为 **i** 和 **r** 为 **j** 。
    *   [迭代直到](https://www.geeksforgeeks.org/loops-in-c-and-cpp/) **l** 和 **r** 大于 **0** ，在每次迭代中执行以下步骤:
        *   计算右下顶点为 **(i，j)** 、左上顶点为 **(l，r)** 的正方形子矩阵之和并存储在一个变量中，比如**和**，即**和=****pre[I][j]–pre[l-1][r]–pre[l][r-1]+pre[l-1][r-1]**。
            *   现在如果 **K*(i-l+1)*(j-r+1)** 的值等于**和**，那么将**计数**增加 **1** 。
            *   将 **l** 和 **r** 减少 **1** 。
*   最后，完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 1000

// Function to count submatrixes with
// average greater than or equals to K
int cntMatrices(vector<vector<int> > arr, int N, int M,
                int K)
{

    // Stores count of submatrices
    int cnt = 0;

    // Stores the prefix sum of matrix
    vector<vector<int> > pre(N + 1, vector<int>(M + 1, 0));

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {

        // Iterate over the range
        // [1, M]
        for (int j = 1; j <= M; j++) {

            // Update the prefix sum
            pre[i][j] = arr[i - 1][j - 1] + pre[i - 1][j]
                        + pre[i][j - 1] - pre[i - 1][j - 1];
        }
    }

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {

        // Iterate over the range
        // [1, M]
        for (int j = 1; j <= M; j++) {

            // Iterate until l and r
            // are greater than 0
            for (int l = i, r = j; l > 0 && r > 0;
                 l--, r--) {

                // Update count
                int sum1 = (K * (i - l + 1) * (i - r + 1));

                // Stores sum of submatrix
                // with bottom right corner
                // as (i, j) and top left
                // corner as (l, r)
                int sum2 = pre[i][j] - pre[l - 1][r]
                           - pre[l][r - 1]
                           + pre[l - 1][r - 1];

                // If sum1 is less than or
                // equal to sum2
                if (sum1 <= sum2)

                    // Increment cnt by 1
                    cnt++;
            }
        }
    }

    // Return cnt as the answer
    return cnt;
}

// Driver Code
int main()
{
    // Given Input
    vector<vector<int> > arr
        = { { 2, 2, 3 }, { 3, 4, 5 }, { 4, 5, 5 } };
    int K = 4;
    int N = arr.size();
    int M = arr[0].size();

    // Function Call
    cout << cntMatrices(arr, N, M, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int MAX = 1000;

// Function to count submatrixes with
// average greater than or equals to K
static int cntMatrices(int[][] arr, int N,
                    int M, int K)
{

    // Stores count of submatrices
    int cnt = 0;

    // Stores the prefix sum of matrix
    int[][] pre = new int[N + 1][M + 1];

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
    {

        // Iterate over the range
        // [1, M]
        for(int j = 1; j <= M; j++)
        {

            // Update the prefix sum
            pre[i][j] = arr[i - 1][j - 1] + pre[i - 1][j] +
                            pre[i][j - 1] - pre[i - 1][j - 1];
        }
    }

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
    {

        // Iterate over the range
        // [1, M]
        for(int j = 1; j <= M; j++)
        {

            // Iterate until l and r
            // are greater than 0
            for(int l = i, r = j;
                    l > 0 && r > 0; l--, r--)
            {

                // Update count
                int sum1 = (K * (i - l + 1) *
                                (i - r + 1));

                // Stores sum of submatrix
                // with bottom right corner
                // as (i, j) and top left
                // corner as (l, r)
                int sum2 = pre[i][j] - pre[l - 1][r] -
                       pre[l][r - 1] + pre[l - 1][r - 1];

                // If sum1 is less than or
                // equal to sum2
                if (sum1 <= sum2)

                    // Increment cnt by 1
                    cnt++;
            }
        }
    }

    // Return cnt as the answer
    return cnt;
}

// Driver Code
public static void main(String args[])
{

    // Given Input
    int[][] arr = { { 2, 2, 3 },
                    { 3, 4, 5 },
                    { 4, 5, 5 } };
    int K = 4;
    int N = arr.length;
    int M = arr[0].length;

    // Function Call
    System.out.println( cntMatrices(arr, N, M, K));
}
}

// This code is contributed by avijitmondal1998
```

## 蟒蛇 3

```
# Python3 program for the above approach
# define MAX 1000

# Function to count submatrixes with
# average greater than or equals to K
def cntMatrices(arr, N, M, K):

    # Stores count of submatrices
    cnt = 0

    # Stores the prefix sum of matrix
    pre = [[0 for i in range(M + 1)]
              for i in range(N + 1)]

    # Iterate over the range [1, N]
    for i in range(1, N + 1):

        # Iterate over the range
        # [1, M]
        for j in range(1, M + 1):

            # Update the prefix sum
            pre[i][j] = (arr[i - 1][j - 1] +
                         pre[i - 1][j] +
                         pre[i][j - 1] -
                         pre[i - 1][j - 1])

    # Iterate over the range [1, N]
    for i in range(1, N + 1):

        # Iterate over the range
        # [1, M]
        for j in range(1, M + 1):

            # Iterate until l and r
            # are greater than 0
            l, r = i, j
            while l > 0 and r > 0:

                # Update count
                sum1 = (K * (i - l + 1) * (i - r + 1))

                # Stores sum of submatrix
                # with bottom right corner
                # as (i, j) and top left
                # corner as (l, r)
                sum2 = (pre[i][j] -
                        pre[l - 1][r] - pre[l][r - 1] +
                        pre[l - 1][r - 1])

                # If sum1 is less than or
                # equal to sum2
                if (sum1 <= sum2):

                    # Increment cnt by 1
                    cnt += 1

                l -= 1
                r -= 1

    # Return cnt as the answer
    return cnt

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ [ 2, 2, 3 ],
            [ 3, 4, 5 ],
            [ 4, 5, 5 ] ]
    K = 4
    N = len(arr)
    M = len(arr[0])

    # Function Call
    print(cntMatrices(arr, N, M, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  static int MAX = 1000;

  // Function to count submatrixes with
  // average greater than or equals to K
  static int cntMatrices(int[,] arr, int N,
                         int M, int K)
  {

    // Stores count of submatrices
    int cnt = 0;

    // Stores the prefix sum of matrix
    int[,] pre = new int[N + 1, M + 1];

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
    {

      // Iterate over the range
      // [1, M]
      for(int j = 1; j <= M; j++)
      {

        // Update the prefix sum
        pre[i, j] = arr[i - 1, j - 1] + pre[i - 1, j] +
          pre[i, j - 1] - pre[i - 1, j - 1];
      }
    }

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
    {

      // Iterate over the range
      // [1, M]
      for(int j = 1; j <= M; j++)
      {

        // Iterate until l and r
        // are greater than 0
        for(int l = i, r = j;
            l > 0 && r > 0; l--, r--)
        {

          // Update count
          int sum1 = (K * (i - l + 1) *
                      (i - r + 1));

          // Stores sum of submatrix
          // with bottom right corner
          // as (i, j) and top left
          // corner as (l, r)
          int sum2 = pre[i, j] - pre[l - 1, r] -
            pre[l, r - 1] + pre[l - 1, r - 1];

          // If sum1 is less than or
          // equal to sum2
          if (sum1 <= sum2)

            // Increment cnt by 1
            cnt++;
        }
      }
    }

    // Return cnt as the answer
    return cnt;
  }

  // Driver code
  public static void Main(string[] args)
  {

    // Given Input
    int[,] arr = { { 2, 2, 3 },
                  { 3, 4, 5 },
                  { 4, 5, 5 } };
    int K = 4;
    int N = arr.GetLength(0);
    int M = arr.GetLength(0);

    // Function Call
    Console.WriteLine( cntMatrices(arr, N, M, K));
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
// Javascript program for the above approach
let MAX = 1000

// Function to count submatrixes with
// average greater than or equals to K
function cntMatrices(arr, N, M, K) {

    // Stores count of submatrices
    let cnt = 0;

    // Stores the prefix sum of matrix

    let pre = new Array(N + 1).fill(0).map(() => new Array(M + 1).fill(0))

    // Iterate over the range [1, N]
    for (let i = 1; i <= N; i++) {

        // Iterate over the range
        // [1, M]
        for (let j = 1; j <= M; j++) {

            // Update the prefix sum
            pre[i][j] = arr[i - 1][j - 1] + pre[i - 1][j]
                + pre[i][j - 1] - pre[i - 1][j - 1];
        }
    }

    // Iterate over the range [1, N]
    for (let i = 1; i <= N; i++) {

        // Iterate over the range
        // [1, M]
        for (let j = 1; j <= M; j++) {

            // Iterate until l and r
            // are greater than 0
            for (let l = i, r = j; l > 0 && r > 0;
                l--, r--) {

                // Update count
                let sum1 = (K * (i - l + 1) * (i - r + 1));

                // Stores sum of submatrix
                // with bottom right corner
                // as (i, j) and top left
                // corner as (l, r)
                let sum2 = pre[i][j] - pre[l - 1][r]
                    - pre[l][r - 1]
                    + pre[l - 1][r - 1];

                // If sum1 is less than or
                // equal to sum2
                if (sum1 <= sum2)

                    // Increment cnt by 1
                    cnt++;
            }
        }
    }

    // Return cnt as the answer
    return cnt;
}

// Driver Code

// Given Input
let arr = [[2, 2, 3], [3, 4, 5], [4, 5, 5]];
let K = 4;
let N = arr.length;
let M = arr[0].length;

// Function Call
document.write(cntMatrices(arr, N, M, K));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
7
```

***时间复杂度:** O(M * N * (min(N，M))*
***辅助空间:** O(M * N)*