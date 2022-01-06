# 最大化由给定矩阵两行相同索引元素的最大值生成的数组最小值

> 原文:[https://www . geeksforgeeks . org/给定矩阵两行最大化最大化相同索引元素生成的最小数组/](https://www.geeksforgeeks.org/maximize-minimum-of-array-generated-by-maximums-of-same-indexed-elements-of-two-rows-of-a-given-matrix/)

给定一个由 **N** 行和 **M** 列组成的[矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**mat【】【】【】**，任务是选择任意两行 **(i，j) (0 ≤ i，j≤N–1)**并构建一个大小为 **M** 的新数组**A【】**，其中**A【k】= max(mat[I][k]，mat[j][k])**

**示例:**

> **输入:** mat[][] = {{5，0，3，1，2}，{1，8，9，1，3}，{1，2，3，4，5}，{9，1，0，3，7}，{2，3，0，6，3}，{6，4，1，7，0}}
> **输出:** 3
> **解释:**
> 选择两行 i = 0 和 j = 4。那么，A[] = {5，3，3，6，3}，min(A[])就是 3，这是最大可能。
> 
> **输入:** mat[][] = {{2，13，41，5}，{91，11，10，13}，{12，3，28，6}}
> **输出:** 13
> **解释:**
> 选择两行 i = 0 和 j = 1。那么，A[] = {91，13，41，13}，min(A[])就是 13，这是最大可能。

**方法:**按照以下步骤解决问题:

*   用 [INT_MAX](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 初始化一个变量 **global_max** ，该变量存储由任意两行 **mat[][]** 构成的数组的最小值的最大值。
*   遍历所有可能的行组合 **i** 和 **j** ，[找到由它们构成的数组的最小值](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)作为 **row_min。**
*   在每次迭代中，将 **global_max** 更新为 **row_min** 和自身的最大值。
*   完成上述步骤后，打印 **global_max** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum of
// minimum of array constructed from
// any two rows of the given matrix
int getMaximum(int N, int M,
               vector<vector<int> > mat)
{
    // Initialize global max as INT_MIN
    int global_max = INT_MIN;

    // Iterate through the rows
    for (int i = 0; i < N; i++) {

        // Iterate through remaining rows
        for (int j = i + 1; j < N; j++) {

            // Initialize row_min as INT_MAX
            int row_min = INT_MAX;

            // Iterate through the column
            // values of two rows
            for (int k = 0; k < M; k++) {

                // Find max of two elements
                int m = max(mat[i][k],
                            mat[j][k]);

                // Update the row_min
                row_min = min(row_min, m);
            }

            // Update the global_max
            global_max = max(global_max,
                             row_min);
        }
    }

    // Print the global max
    return global_max;
}

// Driver Code
int main()
{

    // Given matrix mat[][]
    vector<vector<int> > mat
        = { { 5, 0, 3, 1, 2 },
            { 1, 8, 9, 1, 3 },
            { 1, 2, 3, 4, 5 },
            { 9, 1, 0, 3, 7 },
            { 2, 3, 0, 6, 3 },
            { 6, 4, 1, 7, 0 } };

    // Given number of rows and columns
    int N = 6, M = 5;

    // Function Call
    cout << getMaximum(N, M, mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the maximum of
// minimum of array constructed from
// any two rows of the given matrix
static int getMaximum(int N, int M, int[][] mat)
{

    // Initialize global max as INT_MIN
    int global_max = Integer.MIN_VALUE;

    // Iterate through the rows
    for(int i = 0; i < N; i++)
    {

        // Iterate through remaining rows
        for(int j = i + 1; j < N; j++)
        {

            // Initialize row_min as INT_MAX
            int row_min = Integer.MAX_VALUE;

            // Iterate through the column
            // values of two rows
            for(int k = 0; k < M; k++)
            {

                // Find max of two elements
                int m = Math.max(mat[i][k],
                                 mat[j][k]);

                // Update the row_min
                row_min = Math.min(row_min, m);
            }

            // Update the global_max
            global_max = Math.max(global_max,
                                  row_min);
        }
    }

    // Print the global max
    return global_max;
}

// Driver Code
public static void main(String[] args)
{

    // Given matrix mat[][]
    int[][] mat = { { 5, 0, 3, 1, 2 },
                    { 1, 8, 9, 1, 3 },
                    { 1, 2, 3, 4, 5 },
                    { 9, 1, 0, 3, 7 },
                    { 2, 3, 0, 6, 3 },
                    { 6, 4, 1, 7, 0 } };

    // Given number of rows and columns
    int N = 6, M = 5;

    // Function Call
    System.out.println(getMaximum(N, M, mat));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the maximum of
# minimum of array constructed from
# any two rows of the given matrix
def getMaximum(N, M, mat):

    # Initialize global max as INT_MIN
    global_max = -1 * (sys.maxsize)

    # Iterate through the rows
    for i in range(0, N):

        # Iterate through remaining rows
        for j in range(i + 1, N):

            # Initialize row_min as INT_MAX
            row_min = sys.maxsize

            # Iterate through the column
            # values of two rows
            for k in range(0, M):

                # Find max of two elements
                m = max(mat[i][k], mat[j][k])

                # Update the row_min
                row_min = min(row_min, m)

            # Update the global_max
            global_max = max(global_max,
                             row_min)

    # Print the global max
    return global_max

# Driver Code
if __name__ == '__main__':

    # Given matrix mat[][]
    mat = [ [ 5, 0, 3, 1, 2 ],
            [ 1, 8, 9, 1, 3 ],
            [ 1, 2, 3, 4, 5 ],
            [ 9, 1, 0, 3, 7 ],
            [ 2, 3, 0, 6, 3 ],
            [ 6, 4, 1, 7, 0 ] ]

    # Given number of rows and columns
    N = 6
    M = 5

    # Function Call
    print(getMaximum(N, M, mat))

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum of
// minimum of array constructed from
// any two rows of the given matrix
static int getMaximum(int N, int M, int[,] mat)
{

    // Initialize global max as INT_MIN
    int global_max = int.MinValue;

    // Iterate through the rows
    for(int i = 0; i < N; i++)
    {

        // Iterate through remaining rows
        for(int j = i + 1; j < N; j++)
        {

            // Initialize row_min as INT_MAX
            int row_min = int.MaxValue;

            // Iterate through the column
            // values of two rows
            for(int k = 0; k < M; k++)
            {

                // Find max of two elements
                int m = Math.Max(mat[i, k],
                                 mat[j, k]);

                // Update the row_min
                row_min = Math.Min(row_min, m);
            }

            // Update the global_max
            global_max = Math.Max(global_max,
                                  row_min);
        }
    }

    // Print the global max
    return global_max;
}

// Driver Code
public static void Main()
{

    // Given matrix mat[][]
    int[,] mat = { { 5, 0, 3, 1, 2 },
                   { 1, 8, 9, 1, 3 },
                   { 1, 2, 3, 4, 5 },
                   { 9, 1, 0, 3, 7 },
                   { 2, 3, 0, 6, 3 },
                   { 6, 4, 1, 7, 0 } };

    // Given number of rows and columns
    int N = 6, M = 5;

    // Function Call
    Console.WriteLine(getMaximum(N, M, mat));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum of
// minimum of array constructed from
// any two rows of the given matrix
function getMaximum(N, M, mat)
{

    // Initialize global max as let_MIN
    let global_max = Number.MIN_VALUE;

    // Iterate through the rows
    for(let i = 0; i < N; i++)
    {

        // Iterate through remaining rows
        for(let j = i + 1; j < N; j++)
        {

            // Initialize row_min as let_MAX
            let row_min = Number.MAX_VALUE;

            // Iterate through the column
            // values of two rows
            for(let k = 0; k < M; k++)
            {

                // Find max of two elements
                let m = Math.max(mat[i][k],
                                 mat[j][k]);

                // Update the row_min
                row_min = Math.min(row_min, m);
            }

            // Update the global_max
            global_max = Math.max(global_max,
                                  row_min);
        }
    }

    // Prlet the global max
    return global_max;
}

// Driver code

// Given matrix mat[][]
let mat = [ [ 5, 0, 3, 1, 2 ],
            [ 1, 8, 9, 1, 3 ],
            [ 1, 2, 3, 4, 5 ],
            [ 9, 1, 0, 3, 7 ],
            [ 2, 3, 0, 6, 3 ],
            [ 6, 4, 1, 7, 0 ] ];

// Given number of rows and columns
let N = 6, M = 5;

// Function Call
document.write(getMaximum(N, M, mat));

// This code is contributed by avijitmondal1998

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(M * N<sup>2</sup>)*
***辅助空间:** O(1)*