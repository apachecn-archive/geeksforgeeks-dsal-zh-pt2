# 求布尔矩阵中最大区域的长度

> 原文:[https://www . geesforgeks . org/find-length-maximum-region-boolean-matrix/](https://www.geeksforgeeks.org/find-length-largest-region-boolean-matrix/)

考虑一个有行和列的矩阵，其中每个单元格包含“0”或“1”，任何包含“1”的单元格称为填充单元格。如果两个像元在水平、垂直或对角方向上相邻，则称它们是相连的。如果一个或多个填充单元格也连接在一起，它们将形成一个区域。找出最大区域的长度。

**示例:**

```
Input : M[][5] = { 0 0 1 1 0
                   1 0 1 1 0
                   0 1 0 0 0
                   0 0 0 0 1 }
Output : 6 
In the following example, there are 
2 regions one with length 1 and the 
other as 6\. So largest region: 6

Input : M[][5] = { 0 0 1 1 0
                   0 0 1 1 0
                   0 0 0 0 0
                   0 0 0 0 1 }
Output: 4
In the following example, there are 
2 regions one with length 1 and the 
other as 4\. So largest region: 4
```

问于:[亚马逊采访](https://www.geeksforgeeks.org/amazon-interview-experience-set-328-for-sde-1/)

**<u>解决方案:</u>** 这个想法是基于问题或者[在布尔 2D 矩阵](https://www.geeksforgeeks.org/find-number-of-islands/)中寻找岛屿的数量

**进场:**

1.  2D 矩阵中的一个单元最多可以连接到 8 个邻居。
2.  因此在 DFS 中，对该单元的 8 个邻居进行递归调用。
3.  保留一个访问过的哈希映射来跟踪所有访问过的单元格。
4.  还要跟踪每个 DFS 中被访问的 1，并更新最大长度区域。

下面是上述想法的实现。

## C++

```
// Program to find the length of the largest
// region in boolean 2D-matrix
#include <bits/stdc++.h>
using namespace std;
#define ROW 4
#define COL 5

// A function to check if
// a given cell (row, col)
// can be included in DFS
int isSafe(int M[][COL], int row, int col,
           bool visited[][COL])
{
    // row number is in range,
    // column number is in
    // range and value is 1
    // and not yet visited
    return (row >= 0) && (row < ROW) && (col >= 0)
           && (col < COL)
           && (M[row][col] && !visited[row][col]);
}

// A utility function to
// do DFS for a 2D boolean
// matrix. It only considers
// the 8 neighbours as
// adjacent vertices
void DFS(int M[][COL], int row, int col,
         bool visited[][COL], int& count)
{
    // These arrays are used
    // to get row and column
    // numbers of 8 neighbours
    // of a given cell
    static int rowNbr[] = { -1, -1, -1, 0, 0, 1, 1, 1 };
    static int colNbr[] = { -1, 0, 1, -1, 1, -1, 0, 1 };

    // Mark this cell as visited
    visited[row][col] = true;

    // Recur for all connected neighbours
    for (int k = 0; k < 8; ++k)
    {
        if (isSafe(M, row + rowNbr[k],
                   col + colNbr[k],
                   visited))
        {
            // Increment region length by one
            count++;
            DFS(M, row + rowNbr[k], col + colNbr[k],
                visited, count);
        }
    }
}

// The main function that returns
// largest  length region
// of a given boolean 2D matrix
int largestRegion(int M[][COL])
{
    // Make a bool array to mark visited cells.
    // Initially all cells are unvisited
    bool visited[ROW][COL];
    memset(visited, 0, sizeof(visited));

    // Initialize result as 0 and travesle through the
    // all cells of given matrix
    int result = INT_MIN;
    for (int i = 0; i < ROW; ++i)
    {
        for (int j = 0; j < COL; ++j)
        {
            // If a cell with value 1 is not
            if (M[i][j] && !visited[i][j])
            {
                // visited yet, then new region found
                int count = 1;
                DFS(M, i, j, visited, count);

                // maximum region
                result = max(result, count);
            }
        }
    }
    return result;
}

// Driver code
int main()
{
    int M[][COL] = { { 0, 0, 1, 1, 0 },
                     { 1, 0, 1, 1, 0 },
                     { 0, 1, 0, 0, 0 },
                     { 0, 0, 0, 0, 1 } };

    // Function call
    cout << largestRegion(M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of the largest
// region in boolean 2D-matrix
import java.io.*;
import java.util.*;

class GFG {
    static int ROW, COL, count;

    // A function to check if a given cell (row, col)
    // can be included in DFS
    static boolean isSafe(int[][] M, int row, int col,
                          boolean[][] visited)
    {
        // row number is in range, column number is in
        // range and value is 1 and not yet visited
        return (
            (row >= 0) && (row < ROW) && (col >= 0)
            && (col < COL)
            && (M[row][col] == 1 && !visited[row][col]));
    }

    // A utility function to do DFS for a 2D boolean
    // matrix. It only considers the 8 neighbours as
    // adjacent vertices
    static void DFS(int[][] M, int row, int col,
                    boolean[][] visited)
    {
        // These arrays are used to get row and column
        // numbers of 8 neighbours of a given cell
        int[] rowNbr = { -1, -1, -1, 0, 0, 1, 1, 1 };
        int[] colNbr = { -1, 0, 1, -1, 1, -1, 0, 1 };

        // Mark this cell as visited
        visited[row][col] = true;

        // Recur for all connected neighbours
        for (int k = 0; k < 8; k++)
        {
            if (isSafe(M, row + rowNbr[k], col + colNbr[k],
                       visited))
            {
                // increment region length by one
                count++;
                DFS(M, row + rowNbr[k], col + colNbr[k],
                    visited);
            }
        }
    }

    // The main function that returns largest length region
    // of a given boolean 2D matrix
    static int largestRegion(int[][] M)
    {
        // Make a boolean array to mark visited cells.
        // Initially all cells are unvisited
        boolean[][] visited = new boolean[ROW][COL];

        // Initialize result as 0 and traverse through the
        // all cells of given matrix
        int result = 0;
        for (int i = 0; i < ROW; i++)
        {
            for (int j = 0; j < COL; j++)
            {

                // If a cell with value 1 is not
                if (M[i][j] == 1 && !visited[i][j])
                {

                    // visited yet, then new region found
                    count = 1;
                    DFS(M, i, j, visited);

                    // maximum region
                    result = Math.max(result, count);
                }
            }
        }
        return result;
    }

    // Driver code
    public static void main(String args[])
    {
        int M[][] = { { 0, 0, 1, 1, 0 },
                      { 1, 0, 1, 1, 0 },
                      { 0, 1, 0, 0, 0 },
                      { 0, 0, 0, 0, 1 } };
        ROW = 4;
        COL = 5;

        // Function call
        System.out.println(largestRegion(M));
    }
}

// This code is contributed by rachana soma
```

## 蟒蛇 3

```
# Python3 program to find the length of the
# largest region in boolean 2D-matrix

# A function to check if a given cell
# (row, col) can be included in DFS

def isSafe(M, row, col, visited):
    global ROW, COL

    # row number is in range, column number is in
    # range and value is 1 and not yet visited
    return ((row >= 0) and (row < ROW) and
            (col >= 0) and (col < COL) and
            (M[row][col] and not visited[row][col]))

# A utility function to do DFS for a 2D
# boolean matrix. It only considers
# the 8 neighbours as adjacent vertices

def DFS(M, row, col, visited, count):

    # These arrays are used to get row and column
    # numbers of 8 neighbours of a given cell
    rowNbr = [-1, -1, -1, 0, 0, 1, 1, 1]
    colNbr = [-1, 0, 1, -1, 1, -1, 0, 1]

    # Mark this cell as visited
    visited[row][col] = True

    # Recur for all connected neighbours
    for k in range(8):
        if (isSafe(M, row + rowNbr[k],
                   col + colNbr[k], visited)):

            # increment region length by one
            count[0] += 1
            DFS(M, row + rowNbr[k],
                col + colNbr[k], visited, count)

# The main function that returns largest
# length region of a given boolean 2D matrix

def largestRegion(M):
    global ROW, COL

    # Make a bool array to mark visited cells.
    # Initially all cells are unvisited
    visited = [[0] * COL for i in range(ROW)]

    # Initialize result as 0 and travesle
    # through the all cells of given matrix
    result = -999999999999
    for i in range(ROW):
        for j in range(COL):

            # If a cell with value 1 is not
            if (M[i][j] and not visited[i][j]):

                # visited yet, then new region found
                count = [1]
                DFS(M, i, j, visited, count)

                # maximum region
                result = max(result, count[0])
    return result

# Driver Code
ROW = 4
COL = 5

M = [[0, 0, 1, 1, 0],
     [1, 0, 1, 1, 0],
     [0, 1, 0, 0, 0],
     [0, 0, 0, 0, 1]]

# Function call
print(largestRegion(M))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find the length of
// the largest region in boolean 2D-matrix
using System;

class GFG
{
    static int ROW, COL, count;

    // A function to check if a given cell
    // (row, col) can be included in DFS
    static Boolean isSafe(int[, ] M, int row, int col,
                          Boolean[, ] visited)
    {
        // row number is in range, column number is in
        // range and value is 1 and not yet visited
        return (
            (row >= 0) && (row < ROW) && (col >= 0)
            && (col < COL)
            && (M[row, col] == 1 && !visited[row, col]));
    }

    // A utility function to do DFS for a 2D boolean
    // matrix. It only considers the 8 neighbours as
    // adjacent vertices
    static void DFS(int[, ] M, int row, int col,
                    Boolean[, ] visited)
    {
        // These arrays are used to get row and column
        // numbers of 8 neighbours of a given cell
        int[] rowNbr = { -1, -1, -1, 0, 0, 1, 1, 1 };
        int[] colNbr = { -1, 0, 1, -1, 1, -1, 0, 1 };

        // Mark this cell as visited
        visited[row, col] = true;

        // Recur for all connected neighbours
        for (int k = 0; k < 8; k++)
        {
            if (isSafe(M, row + rowNbr[k],
                       col + colNbr[k],
                       visited))
            {
                // increment region length by one
                count++;
                DFS(M, row + rowNbr[k], col + colNbr[k],
                    visited);
            }
        }
    }

    // The main function that returns
    // largest length region of
    // a given boolean 2D matrix
    static int largestRegion(int[, ] M)
    {
        // Make a boolean array to mark visited cells.
        // Initially all cells are unvisited
        Boolean[, ] visited = new Boolean[ROW, COL];

        // Initialize result as 0 and traverse
        // through the all cells of given matrix
        int result = 0;
        for (int i = 0; i < ROW; i++)
        {
            for (int j = 0; j < COL; j++)
            {
                // If a cell with value 1 is not
                if (M[i, j] == 1 && !visited[i, j])
                {
                    // visited yet,
                    // then new region found
                    count = 1;
                    DFS(M, i, j, visited);

                    // maximum region
                    result = Math.Max(result, count);
                }
            }
        }
        return result;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[, ] M = { { 0, 0, 1, 1, 0 },
                      { 1, 0, 1, 1, 0 },
                      { 0, 1, 0, 0, 0 },
                      { 0, 0, 0, 0, 1 } };
        ROW = 4;
        COL = 5;

        // Function call
        Console.WriteLine(largestRegion(M));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find the length of the largest
// region in boolean 2D-matrix

let ROW, COL, count;

// A function to check if a given cell (row, col)
    // can be included in DFS
function isSafe(M,row,col,visited)
{
    // row number is in range, column number is in
        // range and value is 1 and not yet visited
        return (
            (row >= 0) && (row < ROW) && (col >= 0)
            && (col < COL)
            && (M[row][col] == 1 && !visited[row][col]));
}

// A utility function to do DFS for a 2D boolean
    // matrix. It only considers the 8 neighbours as
    // adjacent vertices
function DFS(M,row,col,visited)
{
    // These arrays are used to get row and column
        // numbers of 8 neighbours of a given cell
        let rowNbr = [ -1, -1, -1, 0, 0, 1, 1, 1 ];
        let colNbr = [ -1, 0, 1, -1, 1, -1, 0, 1 ];

        // Mark this cell as visited
        visited[row][col] = true;

        // Recur for all connected neighbours
        for (let k = 0; k < 8; k++)
        {
            if (isSafe(M, row + rowNbr[k], col + colNbr[k],
                       visited))
            {
                // increment region length by one
                count++;
                DFS(M, row + rowNbr[k], col + colNbr[k],
                    visited);
            }
        }
}

// The main function that returns largest length region
    // of a given boolean 2D matrix
function largestRegion(M)
{
    // Make a boolean array to mark visited cells.
        // Initially all cells are unvisited
        let visited = new Array(ROW);
         for(let i=0;i<ROW;i++)
        {
            visited[i]=new Array(COL);
            for(let j=0;j<COL;j++)
            {
                visited[i][j]=false;
            }
        }

        // Initialize result as 0 and traverse through the
        // all cells of given matrix
        let result = 0;
        for (let i = 0; i < ROW; i++)
        {
            for (let j = 0; j < COL; j++)
            {

                // If a cell with value 1 is not
                if (M[i][j] == 1 && !visited[i][j])
                {

                    // visited yet, then new region found
                    count = 1;
                    DFS(M, i, j, visited);

                    // maximum region
                    result = Math.max(result, count);
                }
            }
        }
        return result;
}

// Driver code
let M=[[ 0, 0, 1, 1, 0 ],
                      [ 1, 0, 1, 1, 0 ],
                      [ 0, 1, 0, 0, 0 ],
                      [ 0, 0, 0, 0, 1 ] ];

ROW = 4;
COL = 5;

// Function call
document.write(largestRegion(M));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
6
```

**复杂度分析:**

*   **时间复杂度:** O(ROW * COL)。
    最坏的情况下，所有的小区都会被访问，所以时间复杂度为 0(ROW * COL)。
*   **辅助空间:** O(ROW * COL)。
    为了存储被访问的节点，需要 O(ROW * COL)空间。

本文由 [**尼尚·辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。