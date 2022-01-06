# 根据给定条件从给定位置逃离给定矩阵的移动次数

> 原文:[https://www . geeksforgeeks . org/基于给定条件从给定位置移动到转义给定矩阵的次数/](https://www.geeksforgeeks.org/count-of-moves-to-escape-given-matrix-from-given-position-based-on-given-conditions/)

给定一个 **N x M** [矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**mat【】【】**我们最初站在索引为 **(i，j)** 的单元格，任务是找到逃离给定矩阵所需的操作数，在每个操作中**mat【x】【y】**都可以从**mat【I】【j】**到达，这样 **x** 就代表了该单元格中 **0 的计数**

**示例**:

> **输入** : mat[][] = {{5，13，8，1}，{7，9，2，15}，{12，4，8，3}}，i = 0，j = 0
> **输出** : 4
> **解释**:最初当前位置是 mat[0][0] = 5。因此，从 5 可到达的索引是 mat[1][2]，因为 5 中 0 的计数是 1，5 中 1 的计数是 2。因此，第一次跳跃是从 mat[0][0] = > mat[1][2]开始的。同样，跳跃的顺序如下:mat[0][0]=>mat[1][2]=>mat[1][1]=>mat[2][2]=>mat[3][1]。由于给定矩阵中不存在索引(3，1)，因此所需的操作数为 4。
> 
> **输入** : mat[][] = {{1，2，3}，{4，5，6}，{7，8，9}}，i = 1，j = 2
> **输出** : -1
> **解释**:无法从索引中逃离矩阵。

**逼近**:借助[布莱恩·克尼根的算法](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)和[内置的对数函数](https://www.geeksforgeeks.org/log-function-cpp/)，可以解决给定的问题。以下是要遵循的步骤:

*   创建一个变量 **Jump** ，它存储所需的跳转操作次数，以逃离给定的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)。最初，**跳跃= 0** 。
*   如果初始单元格已经超出给定矩阵的范围，则返回 **0** 。
*   计算 **mat[i][j]** 二进制表示中 **0 的**和 **1 的**的计数。
*   跳到下一个有效索引，将 **mat[i][j]** 设置为 **-1** 。另外，将**跳跃**的值增加 **1** 。
*   跳跃后检查 **mat[i][j] = -1** 的当前值。这意味着当前索引已经被访问过了，因此创建了一个永无止境的循环。因此，返回 **-1** 。
*   重复上述过程，直到当前索引已被访问或超出给定矩阵的范围。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#define Max 100
using namespace std;

// Function to find total count of
// set bits in any number
int brianKernighan(int N)
{
    int Count = 0;
    while (N) {
        N = N & (N - 1);
        Count += 1;
    }
    return Count;
}

// Function to find left most Set bit
// position in any number
int getMsbIndex(int N)
{
    return ((int)log2(N) + 1);
}

// Function to find the number of
// jumps to escape the matrix from
// the given index [i, j]
int countJumps(int Mat[][Max],
               int N, int M,
               int i, int j)
{
    // Initialize the variable Jump
    int C0, C1, Jump = 0;

    while (i < N && j < M) {

        // When the element is already visited
        // then a closed loop is formed and
        // it is impossible to escape then
        // return -1.
        if (Mat[i][j] == -1)
            return -1;

        // Calculate Count of 1 in Mat[i][j]
        C1 = brianKernighan(Mat[i][j]);

        // Calculate Count of 0 in Mat[i][j]
        C0 = getMsbIndex(Mat[i][j]) - C1;

        // Set the element Mat[i][j] visited
        Mat[i][j] = -1;

        // Set i and j to count if 0 and 1
        i = C0, j = C1;

        // Increment Jump by 1
        Jump++;
    }

    // Return number of Jumps to escape
    // the matrix if it is possible to
    // escape
    return Jump;
}

// Driver Code
int main()
{
    int N = 3, M = 4;
    int i = 0, j = 0;
    int Mat[][Max] = { { 5, 13, 8, 1 },
                       { 7, 9, 2, 15 },
                       { 12, 4, 8, 3 } };

    cout << countJumps(Mat, N, M, i, j);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

// Function to find total count of
// set bits in any number
static int brianKernighan(int N)
{
    int Count = 0;
    while (N != 0) {
        N = N & (N - 1);
        Count += 1;
    }
    return Count;
}

// Function to find left most Set bit
// position in any number
static int getMsbIndex(int N)
{
    return ((int)(Math.log(N) / Math.log(2)) + 1);
}

// Function to find the number of
// jumps to escape the matrix from
// the given index [i, j]
static int countJumps(int Mat[][],
               int N, int M,
               int i, int j)
{

    // Initialize the variable Jump
    int C0, C1, Jump = 0;

    while (i < N && j < M) {

        // When the element is already visited
        // then a closed loop is formed and
        // it is impossible to escape then
        // return -1.
        if (Mat[i][j] == -1)
            return -1;

        // Calculate Count of 1 in Mat[i][j]
        C1 = brianKernighan(Mat[i][j]);

        // Calculate Count of 0 in Mat[i][j]
        C0 = getMsbIndex(Mat[i][j]) - C1;

        // Set the element Mat[i][j] visited
        Mat[i][j] = -1;

        // Set i and j to count if 0 and 1
        i = C0; j = C1;

        // Increment Jump by 1
        Jump++;
    }

    // Return number of Jumps to escape
    // the matrix if it is possible to
    // escape
    return Jump;
}

// Driver Code
public static void main (String[] args) {

    int N = 3, M = 4;
    int i = 0, j = 0;
    int Mat[][] = { { 5, 13, 8, 1 },
                       { 7, 9, 2, 15 },
                       { 12, 4, 8, 3 } };

    System.out.println(countJumps(Mat, N, M, i, j));
}
}

// This code is contributed by target_2.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach
import math as Math
Max = 100

# Function to find total count of
# set bits in any number
def brianKernighan(N):
    Count = 0
    while (N):
        N = N & (N - 1)
        Count += 1
    return Count

# Function to find left most Set bit
# position in any number
def getMsbIndex(N):
    return Math.floor(Math.log2(N) + 1)

# Function to find the number of
# jumps to escape the matrix from
# the given index [i, j]
def countJumps(Mat, N, M, i, j):

    # Initialize the variable Jump
    Jump = 0

    while (i < N and j < M):

        # When the element is already visited
        # then a closed loop is formed and
        # it is impossible to escape then
        # return -1.
        if (Mat[i][j] == -1):
            return -1

        # Calculate Count of 1 in Mat[i][j]
        C1 = brianKernighan(Mat[i][j])

        # Calculate Count of 0 in Mat[i][j]
        C0 = getMsbIndex(Mat[i][j]) - C1

        # Set the element Mat[i][j] visited
        Mat[i][j] = -1

        # Set i and j to count if 0 and 1
        i = C0
        j = C1

        # Increment Jump by 1
        Jump += 1

    # Return number of Jumps to escape
    # the matrix if it is possible to
    # escape
    return Jump

# Driver Code
N = 3
M = 4
i = 0
j = 0
Mat = [[5, 13, 8, 1],
       [7, 9, 2, 15],
       [12, 4, 8, 3]]

print(countJumps(Mat, N, M, i, j))

# This code is contributed by gfgking.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find total count of
// set bits in any number
static int brianKernighan(int N)
{
    int Count = 0;
    while (N != 0) {
        N = N & (N - 1);
        Count += 1;
    }
    return Count;
}

// Function to find left most Set bit
// position in any number
static int getMsbIndex(int N)
{
    return ((int)(Math.Log(N) / Math.Log(2)) + 1);
}

// Function to find the number of
// jumps to escape the matrix from
// the given index [i, j]
static int countJumps(int[,] Mat,
               int N, int M,
               int i, int j)
{

    // Initialize the variable Jump
    int C0, C1, Jump = 0;

    while (i < N && j < M) {

        // When the element is already visited
        // then a closed loop is formed and
        // it is impossible to escape then
        // return -1.
        if (Mat[i, j] == -1)
            return -1;

        // Calculate Count of 1 in Mat[i][j]
        C1 = brianKernighan(Mat[i, j]);

        // Calculate Count of 0 in Mat[i][j]
        C0 = getMsbIndex(Mat[i, j]) - C1;

        // Set the element Mat[i][j] visited
        Mat[i, j] = -1;

        // Set i and j to count if 0 and 1
        i = C0; j = C1;

        // Increment Jump by 1
        Jump++;
    }

    // Return number of Jumps to escape
    // the matrix if it is possible to
    // escape
    return Jump;
}

// Driver Code
public static void Main()
{
    int N = 3, M = 4;
    int i = 0, j = 0;
    int[,] Mat = {{ 5, 13, 8, 1 },
                       { 7, 9, 2, 15 },
                       { 12, 4, 8, 3 } };

    Console.Write(countJumps(Mat, N, M, i, j));
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

        // JavaScript Program to implement
        // the above approach   
        var Max = 100

        // Function to find total count of
        // set bits in any number
        function brianKernighan(N) {
            let Count = 0;
            while (N) {
                N = N & (N - 1);
                Count += 1;
            }
            return Count;
        }

        // Function to find left most Set bit
        // position in any number
        function getMsbIndex(N) {
            return Math.floor(Math.log2(N) + 1);
        }

        // Function to find the number of
        // jumps to escape the matrix from
        // the given index [i, j]
        function countJumps(Mat,
            N, M,
            i, j) {
            // Initialize the variable Jump
            let C0, C1, Jump = 0;

            while (i < N && j < M) {

                // When the element is already visited
                // then a closed loop is formed and
                // it is impossible to escape then
                // return -1.
                if (Mat[i][j] == -1)
                    return -1;

                // Calculate Count of 1 in Mat[i][j]
                C1 = brianKernighan(Mat[i][j]);

                // Calculate Count of 0 in Mat[i][j]
                C0 = getMsbIndex(Mat[i][j]) - C1;

                // Set the element Mat[i][j] visited
                Mat[i][j] = -1;

                // Set i and j to count if 0 and 1
                i = C0, j = C1;

                // Increment Jump by 1
                Jump++;
            }

            // Return number of Jumps to escape
            // the matrix if it is possible to
            // escape
            return Jump;
        }

        // Driver Code
        let N = 3, M = 4;
        let i = 0, j = 0;
        let Mat = [[5, 13, 8, 1],
        [7, 9, 2, 15],
        [12, 4, 8, 3]];

        document.write(countJumps(Mat, N, M, i, j));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
4
```

***时间** **复杂度**:O(N * M * log(M * N))*
***辅助** **空间** : O(1)*