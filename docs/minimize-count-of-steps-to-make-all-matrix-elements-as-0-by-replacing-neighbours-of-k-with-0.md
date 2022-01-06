# 通过将 K 的邻居替换为 0 来最小化使所有矩阵元素为 0 的步数

> 原文:[https://www . geesforgeks . org/通过用 0 替换 k 的邻居来最小化将所有矩阵元素设为 0 的步骤数/](https://www.geeksforgeeks.org/minimize-count-of-steps-to-make-all-matrix-elements-as-0-by-replacing-neighbours-of-k-with-0/)

给定一个大小为 **M*N** 的[二维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **矩阵[][]** 和一个整数 **K.** 对于**矩阵[][]** 中 **K** 的每次出现，替换 **K** 以及其**左侧**、**右侧**、**顶部**和**底部的所有非零相邻元素程序必须重复这个过程，直到矩阵中的所有值都变为零。任务是找到将给定数组**矩阵[][]** 转换为 **0 所需的最小步数。**如果不可能，那么打印 **-1。****

> **注意:**一步定义为选择值为 **K** 的索引，并将其值与其相邻单元格一起更改为 **0** ，直到所有单元格变为 **0** 或索引超出范围。

**示例:**

> **输入:** M = 5，N = 5，
> 矩阵[5][5] = {{5，6，0，5，6}，
> {1，8，8，0，2}，
> {5，5，5，0，6}，
> {4，5，5，5，5，0}，
> {8，8，8，8，8}}，
> K = 6
> **输出:**2
> T12 顶部和底部变为零，即
> 5**6**0 0
> 1 8 8 0 0 0
> 5 5 5—>0 0 0
> 4 5 5 0 0 0 0
> 8 8 8 0 0 0 0
> 因此，在执行第一次出现 6 的过程后， 矩阵变为
> 0 0 0 5 6
> 0 0 0 0 2
> 0 0 0 0 6
> 0 0 0 0 0
> 0 0 0 0 0
> 第二次出现的 6 在矩阵[0][4]中找到，因此左、右、上、下的所有非零相邻元素都变为 0 在执行第二次出现的 6 的过程后， 矩阵变为
> 0 0 0 0 0
> 0 0 0 0 0 0
> 0 0 0 0 0
> 0 0 0 0
> 0 0 0 0 0
> 现在，矩阵中的所有单元格值都变为 0。 因此输出为 2
> 
> **输入:** M = 4，N = 5，
> 矩阵[4][5] = {{5，0，0，5，6}，
> {1，0，8，1，0}，
> {0，5，0，0，6}，
> {4，5，0，5，2}}，
> K = 5
> **输出:** 4

**方法:**思路是[在所有四个方向**左、右、上**和下**上**遍历矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)，在找到值为 **K 的单元格后，**使用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)将所有相邻元素的值更改为 **0。**按照以下步骤解决此问题:

*   将变量**interactions _ count**初始化为 **0**
*   [使用变量**行**迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M)** ，并执行以下任务:
    *   [使用变量 **col** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下任务:
        *   如果**矩阵【行】【列】**等于 **K，**，则使用递归执行 [DFS，将所有可能的元素值更改为 **0** 。同时将**迭代次数**的值增加 **1。**](https://www.geeksforgeeks.org/dfs-traversal-of-a-tree-using-recursion/)
*   执行上述步骤后，检查是否有任何单元格的值不为零。如果是，则打印 **-1，**否则打印**迭代 _ 计数**的值作为答案。

下面是上述方法的实现

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to implement DFS
void traverse(int M, int N, vector<vector<int> >& matrix,
              int row, int col)
{

    // Check the boundary conditions
    if (row >= 0 && row < M && col >= 0 && col < N) {
        if (matrix[row][col] == 0) {
            return;
        }

        // Change that non-zero
        // adjacent element to zero
        matrix[row][col] = 0;

        // Traverse the matrix in left
        traverse(M, N, matrix, row, col - 1);

        // Traverse the matrix in Right
        traverse(M, N, matrix, row, col + 1);

        // Traverse the matrix in Top
        traverse(M, N, matrix, row - 1, col);

        //// Traverse the matrix in Bottom
        traverse(M, N, matrix, row + 1, col);
    }
}

void findCount(int M, int N, vector<vector<int> >& matrix,
               int K)
{

    int iterations_count = 0;

    // Traverse the matrix and find any element
    // equals K, if any elements is found
    // increment the interations_count variable
    // and pass the element to the traverse function
    for (int row = 0; row < M; row++) {
        for (int col = 0; col < N; col++) {
            if (K == matrix[row][col]) {
                iterations_count++;
                traverse(M, N, matrix, row, col);
            }
        }
    }

    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            if (matrix[i][j] != 0) {
                iterations_count = -1;
            }
        }
    }

    // Print the iterations count
    cout << iterations_count;
}

int main()
{

    // Initialize the values of M and N
    int M = 5, N = 5;

    // Assigning the elements of 5*5 matrix
    vector<vector<int> > matrix = { { 5, 6, 0, 5, 6 },
                                    { 1, 8, 8, 0, 2 },
                                    { 5, 5, 5, 0, 6 },
                                    { 4, 5, 5, 5, 0 },
                                    { 8, 8, 8, 8, 8 } };

    // Assign K as 6
    int K = 6;

    findCount(M, N, matrix, K);
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

// Function to implement DFS
static void traverse(int M, int N,int matrix[][],int row, int col)
{

    // Check the boundary conditions
    if (row >= 0 && row < M
        && col >= 0 && col < N) {
        if (matrix[row][col] == 0) {
            return;
        }

        // Change that non-zero
        // adjacent element to zero
        matrix[row][col] = 0;

        // Traverse the matrix in left
        traverse(M, N, matrix, row, col - 1);

        // Traverse the matrix in Right
        traverse(M, N, matrix, row, col + 1);

        // Traverse the matrix in Top
        traverse(M, N, matrix, row - 1, col);

        //// Traverse the matrix in Bottom
        traverse(M, N, matrix, row + 1, col);
    }
}

static void findCount(int M, int N, int matrix[][],int K)
{

    int iterations_count = 0;

    // Traverse the matrix and find any element
    // equals K, if any elements is found
    // increment the interations_count variable
    // and pass the element to the traverse function
    for (int row = 0; row < M; row++) {
        for (int col = 0; col < N; col++) {
            if (K == matrix[row][col]) {
                iterations_count++;
                traverse(M, N, matrix, row, col);
            }
        }
    }

    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            if (matrix[i][j] != 0) {
                iterations_count = -1;
            }
        }
    }

    // Print the iterations count
    System.out.print(iterations_count);
}

// Driver Code
public static void main(String []args)
{

    // Initialize the values of M and N
    int M = 5, N = 5;

    // Assigning the elements of 5*5 matrix
    int matrix[][] = {
            { 5, 6, 0, 5, 6 },
            { 1, 8, 8, 0, 2 },
            { 5, 5, 5, 0, 6 },
            { 4, 5, 5, 5, 0 },
            { 8, 8, 8, 8, 8 } };

    // Assign K as 6
    int K = 6;

    findCount(M, N, matrix, K);

}

}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# python program for the above approach

# Function to implement DFS
def traverse(M,  N, matrix, row, col):

    # Check the boundary conditions
    if (row >= 0 and row < M and col >= 0 and col < N):
        if (matrix[row][col] == 0):
            return

        # Change that non-zero
        # adjacent element to zero
        matrix[row][col] = 0

        # Traverse the matrix in left
        traverse(M, N, matrix, row, col - 1)

        # Traverse the matrix in Right
        traverse(M, N, matrix, row, col + 1)

        # Traverse the matrix in Top
        traverse(M, N, matrix, row - 1, col)

        # Traverse the matrix in Bottom
        traverse(M, N, matrix, row + 1, col)

def findCount(M, N, matrix, K):
    iterations_count = 0

    # Traverse the matrix and find any element
    # equals K, if any elements is found
    # increment the interations_count variable
    # and pass the element to the traverse function
    for row in range(0, M):
        for col in range(0, N):
            if (K == matrix[row][col]):
                iterations_count += 1
                traverse(M, N, matrix, row, col)

    for i in range(0, M):
        for j in range(0, N):
            if (matrix[i][j] != 0):
                iterations_count = -1

    # Print the iterations count
    print(iterations_count)

# Driver Code
if __name__ == "__main__":

    # Initialize the values of M and N
    M = 5
    N = 5

    # Assigning the elements of 5*5 matrix
    matrix = [[5, 6, 0, 5, 6],
              [1, 8, 8, 0, 2],
              [5, 5, 5, 0, 6],
              [4, 5, 5, 5, 0],
              [8, 8, 8, 8, 8]]

    # Assign K as 6
    K = 6
    findCount(M, N, matrix, K)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Function to implement DFS
    static void traverse(int M, int N,int [,]matrix,int row, int col)
    {

        // Check the boundary conditions
        if (row >= 0 && row < M
            && col >= 0 && col < N) {
            if (matrix[row, col] == 0) {
                return;
            }

            // Change that non-zero
            // adjacent element to zero
            matrix[row, col] = 0;

            // Traverse the matrix in left
            traverse(M, N, matrix, row, col - 1);

            // Traverse the matrix in Right
            traverse(M, N, matrix, row, col + 1);

            // Traverse the matrix in Top
            traverse(M, N, matrix, row - 1, col);

            //// Traverse the matrix in Bottom
            traverse(M, N, matrix, row + 1, col);
        }
    }

    static void findCount(int M, int N, int [,]matrix,int K)
    {

        int iterations_count = 0;

        // Traverse the matrix and find any element
        // equals K, if any elements is found
        // increment the interations_count variable
        // and pass the element to the traverse function
        for (int row = 0; row < M; row++) {
            for (int col = 0; col < N; col++) {
                if (K == matrix[row, col]) {
                    iterations_count++;
                    traverse(M, N, matrix, row, col);
                }
            }
        }

        for (int i = 0; i < M; i++) {
            for (int j = 0; j < N; j++) {
                if (matrix[i,j] != 0) {
                    iterations_count = -1;
                }
            }
        }

        // Print the iterations count
        Console.WriteLine(iterations_count);
    }

// Driver Code
public static void Main(String []args)
{

    // Initialize the values of M and N
    int M = 5, N = 5;

    // Assigning the elements of 5*5 matrix
    int [,]matrix = {
            { 5, 6, 0, 5, 6 },
            { 1, 8, 8, 0, 2 },
            { 5, 5, 5, 0, 6 },
            { 4, 5, 5, 5, 0 },
            { 8, 8, 8, 8, 8 } };

    // Assign K as 6
    int K = 6;

    findCount(M, N, matrix, K);

}

}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// JavaScript program for the above approach
// Function to implement DFS
function traverse( M, N, matrix,
              row, col)
{
    // Check the boundary conditions
    if (row >= 0 && row < M
        && col >= 0 && col < N) {
        if (matrix[row][col] == 0) {
            return;
        }

        // Change that non-zero
        // adjacent element to zero
        matrix[row][col] = 0;

        // Traverse the matrix in left
        traverse(M, N, matrix, row, col - 1);

        // Traverse the matrix in Right
        traverse(M, N, matrix, row, col + 1);

        // Traverse the matrix in Top
        traverse(M, N, matrix, row - 1, col);

        //// Traverse the matrix in Bottom
        traverse(M, N, matrix, row + 1, col);
    }
}

function findCount(M, N,
                matrix,
                K)
{

    let iterations_count = 0;

    // Traverse the matrix and find any element
    // equals K, if any elements is found
    // increment the interations_count variable
    // and pass the element to the traverse function
    for (let row = 0; row < M; row++) {
        for (let col = 0; col < N; col++) {
            if (K == matrix[row][col]) {
                iterations_count++;
                traverse(M, N, matrix, row, col);
            }
        }
    }

    for (let i = 0; i < M; i++) {
        for (let j = 0; j < N; j++) {
            if (matrix[i][j] != 0) {
                iterations_count = -1;
            }
        }
    }

    // Print the iterations count
    document.write(iterations_count);

}

// Driver Code

    // Initialize the values of M and N
    let M = 5, N = 5;

    // Assigning the elements of 5*5 matrix
    let matrix
        = [[ 5, 6, 0, 5, 6 ],
            [ 1, 8, 8, 0, 2 ],
            [ 5, 5, 5, 0, 6 ],
            [ 4, 5, 5, 5, 0 ],
            [ 8, 8, 8, 8, 8]];

    // Assign K as 6
    let K = 6;

    findCount(M, N, matrix, K);

// This code is contributed by rohitsingh07052.
</script>
```

**Output**

```
2
```

***时间复杂度:** O(M*N)*
***辅助空间:** O(1)*