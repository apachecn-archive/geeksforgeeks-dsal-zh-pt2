# 二元矩阵中给定维数的子矩阵中存在的最小 1 个数

> 原文:[https://www . geeksforgeeks . org/二进制矩阵中给定维数的子矩阵中存在的最小 1 个数/](https://www.geeksforgeeks.org/minimum-number-of-1s-present-in-a-submatrix-of-given-dimensions-in-a-binary-matrix/)

给定一个大小为 **N × M** 的 [2D 二进制矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **mat[][]** 和两个整数 **A，B** ，任务是找出维度子矩阵 **A × B** 或 **B × A** 中存在的最少数量的 **1** 。

**示例:**

> **输入:**
> mat[][] = {{1，1，1}，
> {1，1，1}，
> {1，1，1}}
> A = 2，B = 1
> **输出:** 2
> **说明:**任何大小为 2×1 或 1×2 的子矩阵都会有 2 个 1。
> 
> **输入:**
> mat[][] = {{1，1，0，1，1，1，0，0}，
> {0，1，0，1，1，1，1，1}，
> {1，1，0，0，1，0，0，0，1}，
> {0，1，1，1，1，0，1，0}，
> {0，1，1，0，1，0，1}，
> {0，1，1 1，0，1，0，1}，
> {1，1，0，1，1，0，1，1}}
> A = 4，B = 9
> **输出:** 20
> **说明:**
> 维度为 9 × 4 的从(0，0)到(8，3)的子矩阵中存在 20 个 1，这是该矩阵的最小可能。

**方法:**解决问题的思路是打印所有可能的维度 A * B and B * A 的子矩阵，对于每个子矩阵，统计其中存在的 **1** 的个数。

按照以下步骤解决给定的问题:

*   初始化一个变量，说**最小值，**存储 **1** s 的最小计数
*   遍历矩阵**mat【】【】**的每个单元格 **(i，j)** ，对于每个 **(i，j)** :
    *   如果 **i + A** 小于等于 **N** ， **j + B** 小于等于 **M** ，则执行以下操作:
        *   初始化一个变量，说**计数，**将 **1** s 的计数存储在子矩阵 **{mat[i][j]，mat[i + A][j + B]}** 中。
        *   遍历子矩阵的每个单元，并将 **1** 的数量存储在变量**计数中。**
        *   检查计数值是否小于当前最小值。如果发现为真，则更新最小值等于**计数**。
    *   如果 **i + B** 小于等于 **N** ， **j + A** 小于等于 **M** ，则执行以下操作:
        *   初始化一个变量，说**计数，**将 **1** 的计数存储在子矩阵 **{mat[i][j]，mat[i + B][j + A]}** 中。
        *   遍历子矩阵的每个单元格，并将 **1** 的数量存储在**计数中。**
        *   检查计数值是否小于当前最小值。如果发现为真，则更新最小值等于**计数**。
*   最后打印**最小值**作为最终结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define P 51

// Function to count number of 1s
// present in a sub matrix from
// (start_i, start_j) to (end_i, end_j)
int count1s(int start_i, int start_j,
            int end_i, int end_j, int mat[][P])
{

    // Stores the number of 1s
    // present in current submatrix
    int count = 0;

    // Traverse the submatrix
    for (int x = start_i; x < end_i; x++) {
        for (int y = start_j; y < end_j; y++) {

            // If mat[x][y] is equal to 1
            if (mat[x][y] == 1)

                // Increase count by 1
                count++;
        }
    }

    // Return the total count of 1s
    return count;
}

// Function to find the minimum number of 1s
// present in a sub-matrix of size A * B or B * A
int findMinimumCount(int N, int M, int A, int B,
                     int mat[][P])
{

    // Stores the minimum count of 1s
    int minimum = 1e9;

    // Iterate i from 0 to N
    for (int i = 0; i < N; i++) {

        // Iterate j from 0 to M
        for (int j = 0; j < M; j++) {

            // If a valid sub matrix of size
            // A * B from (i, j) is possible
            if (i + A <= N && j + B <= M) {

                // Count the number of 1s
                // present in the sub matrix
                // of size A * B from (i, j)
                int count
                    = count1s(i, j, i + A, j + B, mat);

                // Update minimum if count is
                // less than the current minimum
                minimum = min(count, minimum);
            }

            // If a valid sub matrix of size
            // B * A from (i, j) is possible
            if (i + B <= N && j + A <= M) {

                // Count the number of 1s in the
                // sub matrix of size B * A from (i, j)
                int count
                    = count1s(i, j, i + B, j + A, mat);

                // Update minimum if count is
                // less than the current minimum
                minimum = min(count, minimum);
            }
        }
    }

    // Return minimum as the final result
    return minimum;
}

// Driver Code
int main()
{
    // Given Input
    int A = 2, B = 2;
    int N = 3, M = 4;
    int mat[P][P] = { { 1, 0, 1, 0 },
                      { 0, 1, 0, 1 },
                      { 1, 0, 1, 0 } };

    // Function call to find the minimum number
    // of 1s in a submatrix of size A * B or B * A
    cout << findMinimumCount(N, M, A, B, mat);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count number of 1s
// present in a sub matrix from
// (start_i, start_j) to (end_i, end_j)
static int count1s(int start_i, int start_j,
                   int end_i, int end_j,
                   int[][] mat)
{

    // Stores the number of 1s
    // present in current submatrix
    int count = 0;

    // Traverse the submatrix
    for(int x = start_i; x < end_i; x++)
    {
        for(int y = start_j; y < end_j; y++)
        {

            // If mat[x][y] is equal to 1
            if (mat[x][y] == 1)

                // Increase count by 1
                count++;
        }
    }

    // Return the total count of 1s
    return count;
}

// Function to find the minimum number of 1s
// present in a sub-matrix of size A * B or B * A
static int findMinimumCount(int N, int M, int A,
                            int B, int[][] mat)
{

    // Stores the minimum count of 1s
    int minimum = (int) 1e9;

    // Iterate i from 0 to N
    for(int i = 0; i < N; i++)
    {

        // Iterate j from 0 to M
        for(int j = 0; j < M; j++)
        {

            // If a valid sub matrix of size
            // A * B from (i, j) is possible
            if (i + A <= N && j + B <= M)
            {

                // Count the number of 1s
                // present in the sub matrix
                // of size A * B from (i, j)
                int count = count1s(i, j, i + A,
                                    j + B, mat);

                // Update minimum if count is
                // less than the current minimum
                minimum = Math.min(count, minimum);
            }

            // If a valid sub matrix of size
            // B * A from (i, j) is possible
            if (i + B <= N && j + A <= M)
            {

                // Count the number of 1s in the
                // sub matrix of size B * A from (i, j)
                int count = count1s(i, j, i + B,
                                    j + A, mat);

                // Update minimum if count is
                // less than the current minimum
                minimum = Math.min(count, minimum);
            }
        }
    }

    // Return minimum as the final result
    return minimum;
}

// Driver code
public static void main(String[] args)
{

    // Given Input
    int A = 2, B = 2;
    int N = 3, M = 4;
    int[][] mat = { { 1, 0, 1, 0 },
                    { 0, 1, 0, 1 },
                    { 1, 0, 1, 0 } };

    // Function call to find the minimum number
    // of 1s in a submatrix of size A * B or B * A
    System.out.println(findMinimumCount(N, M, A, B, mat));
}
}

// This code is contributed by user_qa7r
```

## 蟒蛇 3

```
# Python3 program for the above approach
P = 51

# Function to count number of 1s
# present in a sub matrix from
# (start_i, start_j) to (end_i, end_j)
def count1s(start_i, start_j,
            end_i, end_j, mat):

    # Stores the number of 1s
    # present in current submatrix
    count = 0

    # Traverse the submatrix
    for x in range(start_i, end_i):
        for y in range(start_j, end_j):

            # If mat[x][y] is equal to 1
            if (mat[x][y] == 1):

                # Increase count by 1
                count += 1

    # Return the total count of 1s
    return count

# Function to find the minimum number of 1s
# present in a sub-matrix of size A * B or B * A
def findMinimumCount(N, M, A, B, mat):

    # Stores the minimum count of 1s
    minimum = 1e9

    # Iterate i from 0 to N
    for i in range(N):

        # Iterate j from 0 to M
        for j in range(M):

            # If a valid sub matrix of size
            # A * B from (i, j) is possible
            if (i + A <= N and j + B <= M):

                # Count the number of 1s
                # present in the sub matrix
                # of size A * B from (i, j)
                count = count1s(i, j, i + A, j + B, mat)

                # Update minimum if count is
                # less than the current minimum
                minimum = min(count, minimum)

            # If a valid sub matrix of size
            # B * A from (i, j) is possible
            if (i + B <= N and j + A <= M):

                # Count the number of 1s in the
                # sub matrix of size B * A from (i, j)
                count = count1s(i, j, i + B, j + A, mat)

                # Update minimum if count is
                # less than the current minimum
                minimum = min(count, minimum)

    # Return minimum as the final result
    return minimum

# Driver Code
if __name__ == "__main__":
    # Given Input
    A = 2
    B = 2
    N = 3
    M = 4
    mat = [[1, 0, 1, 0],
           [0, 1, 0, 1],
           [1, 0, 1, 0]]

    # Function call to find the minimum number
    # of 1s in a submatrix of size A * B or B * A
    print(findMinimumCount(N, M, A, B, mat))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count number of 1s
// present in a sub matrix from
// (start_i, start_j) to (end_i, end_j)
static int count1s(int start_i, int start_j,
                   int end_i, int end_j,
                   List<List<int>> mat)
{

    // Stores the number of 1s
    // present in current submatrix
    int count = 0;

    // Traverse the submatrix
    for(int x = start_i; x < end_i; x++)
    {
        for(int y = start_j; y < end_j; y++)
        {

            // If mat[x][y] is equal to 1
            if (mat[x][y] == 1)

                // Increase count by 1
                count++;
        }
    }

    // Return the total count of 1s
    return count;
}

// Function to find the minimum number of 1s
// present in a sub-matrix of size A * B or B * A
static void findMinimumCount(int N, int M, int A, int B,
                             List<List<int>> mat)
{

    // Stores the minimum count of 1s
    int minimum = 1000000;

    // Iterate i from 0 to N
    for(int i = 0; i < N; i++)
    {

        // Iterate j from 0 to M
        for(int j = 0; j < M; j++)
        {

            // If a valid sub matrix of size
            // A * B from (i, j) is possible
            if ((i + A <= N) && (j + B <= M))
            {

                // Count the number of 1s
                // present in the sub matrix
                // of size A * B from (i, j)
                int count = count1s(i, j, i + A,
                                    j + B, mat);

                // Update minimum if count is
                // less than the current minimum
                minimum = Math.Min(count, minimum);
            }

            // If a valid sub matrix of size
            // B * A from (i, j) is possible
            if ((i + B <= N) && (j + A <= M))
            {

                // Count the number of 1s in the
                // sub matrix of size B * A from (i, j)
                int count = count1s(i, j, i + B,
                                    j + A, mat);

                // Update minimum if count is
                // less than the current minimum
                minimum = Math.Min(count, minimum);
            }
        }
    }

    // Return minimum as the final result
    Console.WriteLine(minimum);
}

// Driver Code
public static void Main()
{

    // Given Input
    int A = 2, B = 2;
    int N = 3, M = 4;

    List<List<int>> mat = new List<List<int>>();
    mat.Add(new List<int>(new int[]{1, 0, 1, 0}));
    mat.Add(new List<int>(new int[]{0, 1, 0, 1}));
    mat.Add(new List<int>(new int[]{1, 0, 1, 0}));

    // Function call to find the minimum number
    // of 1s in a submatrix of size A * B or B * A
    findMinimumCount(N, M, A, B, mat);
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count number of 1s
// present in a sub matrix from
// (start_i, start_j) to (end_i, end_j)
function count1s(start_i, start_j,
                 end_i, end_j, mat)
{

    // Stores the number of 1s
    // present in current submatrix
    let count = 0;

    // Traverse the submatrix
    for(let x = start_i; x < end_i; x++)
    {
        for(let y = start_j; y < end_j; y++)
        {

            // If mat[x][y] is equal to 1
            if (mat[x][y] == 1)

                // Increase count by 1
                count++;
        }
    }

    // Return the total count of 1s
    return count;
}

// Function to find the minimum number of 1s
// present in a sub-matrix of size A * B or B * A
function findMinimumCount(N, M, A, B, mat)
{

    // Stores the minimum count of 1s
    let minimum = 1e9;

    // Iterate i from 0 to N
    for(let i = 0; i < N; i++)
    {

        // Iterate j from 0 to M
        for(let j = 0; j < M; j++)
        {

            // If a valid sub matrix of size
            // A * B from (i, j) is possible
            if (i + A <= N && j + B <= M)
            {

                // Count the number of 1s
                // present in the sub matrix
                // of size A * B from (i, j)
                let count = count1s(i, j, i + A,
                                    j + B, mat);

                // Update minimum if count is
                // less than the current minimum
                minimum = Math.min(count, minimum);
            }

            // If a valid sub matrix of size
            // B * A from (i, j) is possible
            if (i + B <= N && j + A <= M)
            {

                // Count the number of 1s in the
                // sub matrix of size B * A from (i, j)
                let count = count1s(i, j, i + B,
                                    j + A, mat);

                // Update minimum if count is
                // less than the current minimum
                minimum = Math.min(count, minimum);
            }
        }
    }

    // Return minimum as the final result
    return minimum;
}

// Driver code

// Given Input
let A = 2, B = 2;
let N = 3, M = 4;
let mat = [ [ 1, 0, 1, 0 ],
            [ 0, 1, 0, 1 ],
            [ 1, 0, 1, 0 ] ];

// Function call to find the minimum number
// of 1s in a submatrix of size A * B or B * A
document.write(findMinimumCount(N, M, A, B, mat));

// This code is contributed by target_2

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*