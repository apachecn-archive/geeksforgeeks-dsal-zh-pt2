# 通过替换 0 来最大化矩阵和，使得矩阵保持排序状态

> 原文:[https://www . geesforgeks . org/maximum-matrix-sum-by-replacement-0s-so-matrix-retain-sorted/](https://www.geeksforgeeks.org/maximize-matrix-sum-by-replacing-0s-such-that-matrix-remains-sorted/)

给定维度为 **N*M** 的[矩阵](https://www.geeksforgeeks.org/category/data-structures/matrix/)**mat【】【】【】**，该矩阵按**行**和**列**排序，任务是通过用任意值替换矩阵中的所有 **0s** 找到矩阵元素的和，使得矩阵保持按**行**和**列**排序。如果不可能，则打印【T18 "-" 1 "。

**注意:** **0s** 只会出现在内部细胞中。即既不在第一行或列中，也不在最后一行或列中。

**示例:**

> **输入:** mat[][] = {{3，4，5，6}，{4，0，7，8}，{6，8，0，10}，{7，9，10，12}}
> **输出:** 116
> **说明:**
> 替换零后形成的新矩阵为:
> 【【3，4，5，6】，
> 【4，7，8】，
> 【6】
> 
> **输入:** mat[][] = {{1，2，4}，{2，0，5}，{5，6，7 } }
> T3】输出: 37

**方法:**为了对矩阵进行排序，也为了最大化和，可以用小于或等于其行或列中下一个元素的数字来替换零。由于要更改的零值取决于其下一行和下一列的值，因此应该从矩阵的末尾开始替换。因此，[从头到尾遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)，用 **min(mat[i][j + 1]，mat[i + 1][j])** 替换 **mat[i][j]** 为零的单元格，同时检查新矩阵是否排序。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// the given matrix after replacing 0s
// with any element
int findMaximumSum(int* mat, int n, int m)
{
    // Traverse the given matrix from
    // the end
    for (int i = n - 2; i > 0; i--) {
        for (int j = m - 2; j > 0; j--) {

            // If  the element is 0
            if (mat[i * m + j] == 0) {

                // Replace the 0s
                mat[i * m + j]
                    = min(mat[i * m + (j + 1)],
                          mat[(i + 1) * m + j]);
            }
        }
    }

    // Stores the sum of matrix elements
    int sum = 0;

    // Traverse the matrix mat[][]
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // Updating the sum
            sum += mat[i * m + j];

            // Checking if not sorted
            if ((i + 1 < n
                 && mat[i * m + j]
                        > mat[(i + 1) * m + j])
                || (j + 1 < m
                    && mat[i * m + j]
                           > mat[i * m + (j + 1)])) {
                return -1;
            }
        }
    }

    // Return the maximum value of the sum
    return sum;
}

// Driver Code
int main()
{
    int N = 3, M = 3;
    int mat[N][M]
        = { { 1, 2, 4 }, { 2, 0, 5 }, { 5, 6, 7 } };
    cout << findMaximumSum((int*)mat, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Driver Code
    public static void main(String[] args)
    {
        int[][] mat
            = { { 1, 2, 4 }, { 2, 0, 5 }, { 5, 6, 7 } };
        System.out.println(findMaximumSum(mat));
    }

    // Function to find the maximum sum of
    // the given matrix after replacing 0s
    // with any element
    public static int findMaximumSum(int[][] mat)
    {
        int N = mat.length;
        int M = mat[0].length;

        // Traverse the given matrix from
        // the end
        for (int i = N - 2; i > 0; i--) {
            for (int j = M - 2; j > 0; j--) {

                // If  the element is 0
                if (mat[i][j] == 0) {

                    // Replace the 0's
                    mat[i][j] = Math.min(mat[i][j + 1],
                                         mat[i + 1][j]);
                }
            }
        }

        // Stores the sum of matrix elements
        int sum = 0;

        // Traverse the matrix mat[][]
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {

                // Updating the sum
                sum += mat[i][j];

                // Checking if not sorted
                if ((i + 1 < N && mat[i][j] > mat[i + 1][j])
                    || (j + 1 < M
                        && mat[i][j] > mat[i][j + 1]))
                    return -1;
            }
        }

        // Return the maximum value of the sum
        return sum;
    }
}

// This code is contributed by Kdheeraj.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the maximum sum of
#  the given matrix after replacing 0s
#  with any element
def findMaximumSum(mat, n, m):

    # Traverse the given matrix from
    # the end
    for i in range(n-2, 0, -1):
        for j in range(m-2, 0, -1):

            # If  the element is 0
            if (mat[i][j] == 0):

                # Replace the 0s
                mat[i][j] = min(mat[i][(j + 1)], mat[(i + 1)][j])

    # Stores the sum of matrix elements
    sum = 0

    # Traverse the matrix mat[][]
    for i in range(0, n):
        for j in range(0, m):

            # Updating the sum
            sum += mat[i][j]

            # Checking if not sorted
            if ((i + 1 < n and mat[i][j] > mat[(i + 1)][j]) or (j + 1 < m and mat[i][j] > mat[i][(j + 1)])):
                return -1

    # Return the maximum value of the sum
    return sum

# driver code
N = 3
M = 3
mat = [[1, 2, 4], [2, 0, 5], [5, 6, 7]]
print(findMaximumSum(mat, N, M))

# This code is contributed by amreshkumar3
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find the maximum sum of
    // the given matrix after replacing 0s
    // with any element
    static int findMaximumSum(int[, ] mat, int n, int m)
    {

        // Traverse the given matrix from
        // the end
        for (int i = n - 2; i > 0; i--) {
            for (int j = m - 2; j > 0; j--) {

                // If  the element is 0
                if (mat[i, j] == 0) {

                    // Replace the 0s
                    mat[i, j] = Math.Min(mat[i, (j + 1)],
                                         mat[(i + 1), j]);
                }
            }
        }

        // Stores the sum of matrix elements
        int sum = 0;

        // Traverse the matrix mat[][]
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {

                // Updating the sum
                sum += mat[i, j];

                // Checking if not sorted
                if ((i + 1 < n
                     && mat[i, j] > mat[(i + 1), j])
                    || (j + 1 < m
                        && mat[i, j] > mat[i, (j + 1)])) {
                    return -1;
                }
            }
        }

        // Return the maximum value of the sum
        return sum;
    }

    // Driver Code
    public static void Main()
    {
        int N = 3, M = 3;
        int[, ] mat
            = { { 1, 2, 4 }, { 2, 0, 5 }, { 5, 6, 7 } };
        Console.WriteLine(findMaximumSum(mat, N, M));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to find the maximum sum of
       // the given matrix after replacing 0s
       // with any element
       function findMaximumSum(mat, n, m)
       {

           // Traverse the given matrix from
           // the end
           for (let i = n - 2; i > 0; i--) {
               for (let j = m - 2; j > 0; j--) {

                   // If  the element is 0
                   if (mat[i][j] == 0) {

                       // Replace the 0s
                       mat[i][j]
                           = Math.min(mat[i][j + 1],
                               mat[i + 1][j]);
                   }
               }
           }

           // Stores the sum of matrix elements
           let sum = 0;

           // Traverse the matrix mat[][]
           for (let i = 0; i < n; i++) {
               for (let j = 0; j < m; j++) {

                   // Updating the sum
                   sum += mat[i][j];

                   // Checking if not sorted
                   if ((i + 1 < n
                       && mat[i][j]
                       > mat[i + 1][j])
                       || (j + 1 < m
                           && mat[i][j]
                           > mat[i][(j + 1)])) {
                       return -1;
                   }
               }
           }

           // Return the maximum value of the sum
           return sum;
       }

       // Driver Code

       let N = 3, M = 3;
       let mat
           = [[1, 2, 4], [2, 0, 5], [5, 6, 7]];
       document.write(findMaximumSum(mat, N, M));

    // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
37
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*