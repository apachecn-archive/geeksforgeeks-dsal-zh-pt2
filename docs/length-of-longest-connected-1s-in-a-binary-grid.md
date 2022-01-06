# 二进制网格中最长连接 1 的长度

> 原文:[https://www . geeksforgeeks . org/最长连接长度二进制网格中的 1s/](https://www.geeksforgeeks.org/length-of-longest-connected-1s-in-a-binary-grid/)

给定一个大小为 **N*M** 的网格，仅由 **0** 和 **1** 组成，任务是在给定的网格中找到最长连接的 **1s** 的长度。我们只能从网格的任何当前单元格向左、向右、向上或向下移动。

**示例:**

> **输入:** N = 3，M = 3，网格[][] = { {0，0，0}，{0，1，0}，{0，0，0} }
> **输出:** 1
> **解释:**
> 最长的可能路线是 1，因为从矩阵的(1，1)位置不能有任何移动。
> 
> **输入:** N = 6，M = 7，网格[][] = { {0，0，0，0，0，0，0}，{0，1，0，1，0，0，0}，{0，1，0，0，0，0}，{0，1，0，1，0，1，1，0}，{0，1，1，1，1，0}，{0，0，0，0，0，0，0}}
> **输出:【T4 1) - > (4，1) - > (4，2) - > (4，3) - > (4，4) - > (4，5)-(T16】(3，5)。**

**方法:**思路是在当前单元格值为 **1** 的网格上做 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，递归调用当前单元格值为 **1** 的所有四个方向，更新连通 **1** 的最大长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define row 6
#define col 7
using namespace std;

int vis[row + 1][col + 1], id;
int diameter = 0, length = 0;

// Keeps a track of directions
// that is up, down, left, right
int dx[] = { -1, 1, 0, 0 };
int dy[] = { 0, 0, -1, 1 };

// Function to perform the dfs traversal
void dfs(int a, int b, int lis[][col],
         int& x, int& y)
{

    // Mark the current node as visited
    vis[a][b] = id;

    // Increment length from this node
    length++;

    // Update the diameter length
    if (length > diameter) {
        x = a;
        y = b;
        diameter = length;
    }
    for (int j = 0; j < 4; j++) {

        // Move to next cell in x-direction
        int cx = a + dx[j];

        // Move to next cell in y-direction
        int cy = b + dy[j];

        // Check if cell is invalid
        // then continue
        if (cx < 0 || cy < 0 || cx >= row
            || cy >= col || lis[cx][cy] == 0
            || vis[cx][cy]) {
            continue;
        }

        // Perform DFS on new cell
        dfs(cx, cy, lis, x, y);
    }

    vis[a][b] = 0;

    // Decrement the length
    length--;
}

// Function to find the maximum length of
// connected 1s in the given grid
void findMaximumLength(int lis[][col])
{

    int x, y;

    // Increment the id
    id++;
    length = 0;
    diameter = 0;

    // Traverse the grid[]
    for (int i = 0; i < row; i++) {

        for (int j = 0; j < col; j++) {

            if (lis[i][j] != 0) {

                // Find start point of
                // start dfs call
                dfs(i, j, lis, x, y);
                i = row;
                break;
            }
        }
    }

    id++;
    length = 0;
    diameter = 0;

    // DFS Traversal from cell (x, y)
    dfs(x, y, lis, x, y);

    // Print the maximum length
    cout << diameter;
}

// Driver Code
int main()
{
    // Given grid[][]
    int grid[][col] = { { 0, 0, 0, 0, 0, 0, 0 },
                        { 0, 1, 0, 1, 0, 0, 0 },
                        { 0, 1, 0, 1, 0, 0, 0 },
                        { 0, 1, 0, 1, 0, 1, 0 },
                        { 0, 1, 1, 1, 1, 1, 0 },
                        { 0, 0, 0, 1, 0, 0, 0 } };

    // Function Call
    findMaximumLength(grid);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static final int row = 6;
static final int col = 7;
static int [][]vis = new int[row + 1][col + 1];
static int id;
static int diameter = 0, length = 0;
static int x = 0, y = 0;

// Keeps a track of directions
// that is up, down, left, right
static int dx[] = { -1, 1, 0, 0 };
static int dy[] = { 0, 0, -1, 1 };

// Function to perform the dfs traversal
static void dfs(int a, int b, int lis[][])
{

    // Mark the current node as visited
    vis[a][b] = id;

    // Increment length from this node
    length++;

    // Update the diameter length
    if (length > diameter)
    {
        x = a;
        y = b;
        diameter = length;
    }

    for(int j = 0; j < 4; j++)
    {

       // Move to next cell in x-direction
       int cx = a + dx[j];

       // Move to next cell in y-direction
       int cy = b + dy[j];

       // Check if cell is invalid
       // then continue
       if (cx < 0 || cy < 0 ||
           cx >= row || cy >= col ||
           lis[cx][cy] == 0 || vis[cx][cy] > 0)
       {
           continue;
       }

       // Perform DFS on new cell
       dfs(cx, cy, lis);
    }

    vis[a][b] = 0;

    // Decrement the length
    length--;
}

// Function to find the maximum length of
// connected 1s in the given grid
static void findMaximumLength(int lis[][])
{

    // Increment the id
    id++;
    length = 0;
    diameter = 0;

    // Traverse the grid[]
    for(int i = 0; i < row; i++)
    {
       for(int j = 0; j < col; j++)
       {
          if (lis[i][j] != 0)
          {

              // Find start point of
              // start dfs call
              dfs(i, j, lis);
              i = row;
              break;
          }
       }
    }

    id++;
    length = 0;
    diameter = 0;

    // DFS Traversal from cell (x, y)
    dfs(x, y, lis);

    // Print the maximum length
    System.out.print(diameter);
}

// Driver Code
public static void main(String[] args)
{

    // Given grid[][]
    int grid[][] = { { 0, 0, 0, 0, 0, 0, 0 },
                     { 0, 1, 0, 1, 0, 0, 0 },
                     { 0, 1, 0, 1, 0, 0, 0 },
                     { 0, 1, 0, 1, 0, 1, 0 },
                     { 0, 1, 1, 1, 1, 1, 0 },
                     { 0, 0, 0, 1, 0, 0, 0 } };

    // Function Call
    findMaximumLength(grid);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach
row = 6
col = 7

vis = [[0 for i in range(col + 1)]
          for j in range(row + 1)]
id = 0
diameter = 0
length = 0

# Keeps a track of directions
# that is up, down, left, right
dx = [ -1, 1, 0, 0 ]
dy = [ 0, 0, -1, 1 ]

# Function to perform the dfs traversal
def dfs(a, b, lis, x, y):

    global id, length, diameter

    # Mark the current node as visited
    vis[a][b] = id

    # Increment length from this node
    length += 1

    # Update the diameter length
    if (length > diameter):
        x = a
        y = b
        diameter = length

    for j in range(4):

        # Move to next cell in x-direction
        cx = a + dx[j]

        # Move to next cell in y-direction
        cy = b + dy[j]

        # Check if cell is invalid
        # then continue
        if (cx < 0 or cy < 0 or
            cx >= row or cy >= col or
            lis[cx][cy] == 0 or vis[cx][cy]):
            continue

        # Perform DFS on new cell
        dfs(cx, cy, lis, x, y)

    vis[a][b] = 0

    # Decrement the length
    length -= 1

    return x, y

# Function to find the maximum length of
# connected 1s in the given grid
def findMaximumLength(lis):

    global id, length, diameter

    x = 0
    y = 0

    # Increment the id
    id += 1

    length = 0
    diameter = 0

    # Traverse the grid[]
    for i in range(row):
        for j in range(col):
            if (lis[i][j] != 0):

                # Find start point of
                # start dfs call
                x, y = dfs(i, j, lis, x, y)
                i = row
                break

    id += 1
    length = 0
    diameter = 0

    # DFS Traversal from cell (x, y)
    x, y = dfs(x, y, lis, x, y)

    # Print the maximum length
    print(diameter)

# Driver Code
if __name__=="__main__":

    # Given grid[][]
    grid = [ [ 0, 0, 0, 0, 0, 0, 0 ],
             [ 0, 1, 0, 1, 0, 0, 0 ],
             [ 0, 1, 0, 1, 0, 0, 0 ],
             [ 0, 1, 0, 1, 0, 1, 0 ],
             [ 0, 1, 1, 1, 1, 1, 0 ],
             [ 0, 0, 0, 1, 0, 0, 0 ] ]

    # Function Call
    findMaximumLength(grid)

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static readonly int row = 6;
static readonly int col = 7;
static int [,]vis = new int[row + 1, col + 1];
static int id;
static int diameter = 0, length = 0;
static int x = 0, y = 0;

// Keeps a track of directions
// that is up, down, left, right
static int []dx = { -1, 1, 0, 0 };
static int []dy = { 0, 0, -1, 1 };

// Function to perform the dfs traversal
static void dfs(int a, int b, int [,]lis)
{

    // Mark the current node as visited
    vis[a, b] = id;

    // Increment length from this node
    length++;

    // Update the diameter length
    if (length > diameter)
    {
        x = a;
        y = b;
        diameter = length;
    }

    for(int j = 0; j < 4; j++)
    {

        // Move to next cell in x-direction
        int cx = a + dx[j];

        // Move to next cell in y-direction
        int cy = b + dy[j];

        // Check if cell is invalid
        // then continue
        if (cx < 0 || cy < 0 ||
            cx >= row || cy >= col ||
            lis[cx, cy] == 0 || vis[cx, cy] > 0)
        {
            continue;
        }

        // Perform DFS on new cell
        dfs(cx, cy, lis);
    }
    vis[a, b] = 0;

    // Decrement the length
    length--;
}

// Function to find the maximum length of
// connected 1s in the given grid
static void findMaximumLength(int [,]lis)
{

    // Increment the id
    id++;
    length = 0;
    diameter = 0;

    // Traverse the grid[]
    for(int i = 0; i < row; i++)
    {
        for(int j = 0; j < col; j++)
        {
            if (lis[i, j] != 0)
            {

                // Find start point of
                // start dfs call
                dfs(i, j, lis);
                i = row;
                break;
            }
        }
    }

    id++;
    length = 0;
    diameter = 0;

    // DFS Traversal from cell (x, y)
    dfs(x, y, lis);

    // Print the maximum length
    Console.Write(diameter);
}

// Driver Code
public static void Main(String[] args)
{

    // Given grid[,]
    int [,]grid = { { 0, 0, 0, 0, 0, 0, 0 },
                    { 0, 1, 0, 1, 0, 0, 0 },
                    { 0, 1, 0, 1, 0, 0, 0 },
                    { 0, 1, 0, 1, 0, 1, 0 },
                    { 0, 1, 1, 1, 1, 1, 0 },
                    { 0, 0, 0, 1, 0, 0, 0 } };

    // Function Call
    findMaximumLength(grid);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

let row = 6;
 let col = 7;
let vis = new Array(row + 1);
// Loop to create 2D array using 1D array
for (var i = 0; i < vis.length; i++) {
    vis[i] = new Array(2);
}

let id = 0;
let diameter = 0, length = 0;
let x = 0, y = 0;

// Keeps a track of directions
// that is up, down, left, right
let dx = [ -1, 1, 0, 0 ];
let dy = [ 0, 0, -1, 1 ];

// Function to perform the dfs traversal
function dfs(a, b, lis)
{

    // Mark the current node as visited
    vis[a][b] = id;

    // Increment length from this node
    length++;

    // Update the diameter length
    if (length > diameter)
    {
        x = a;
        y = b;
        diameter = length;
    }

    for(let j = 0; j < 4; j++)
    {

       // Move to next cell in x-direction
       let cx = a + dx[j];

       // Move to next cell in y-direction
       let cy = b + dy[j];

       // Check if cell is invalid
       // then continue
       if (cx < 0 || cy < 0 ||
           cx >= row || cy >= col ||
           lis[cx][cy] == 0 || vis[cx][cy] > 0)
       {
           continue;
       }

       // Perform DFS on new cell
       dfs(cx, cy, lis);
    }

    vis[a][b] = 0;

    // Decrement the length
    length--;
}

// Function to find the maximum length of
// connected 1s in the given grid
function findMaximumLength(lis)
{

    // Increment the id
    id++;
    length = 0;
    diameter = 0;

    // Traverse the grid[]
    for(let i = 0; i < row; i++)
    {
       for(let j = 0; j < col; j++)
       {
          if (lis[i][j] != 0)
          {

              // Find start point of
              // start dfs call
              dfs(i, j, lis);
              i = row;
              break;
          }
       }
    }

    id++;
    length = 0;
    diameter = 0;

    // DFS Traversal from cell (x, y)
    dfs(x, y, lis);

    // Print the maximum length
    document.write(diameter);
}

// Driver code

   // Given grid[][]
    let grid = [[ 0, 0, 0, 0, 0, 0, 0 ],
                     [ 0, 1, 0, 1, 0, 0, 0 ],
                     [ 0, 1, 0, 1, 0, 0, 0 ],
                     [ 0, 1, 0, 1, 0, 1, 0 ],
                     [ 0, 1, 1, 1, 1, 1, 0 ],
                     [ 0, 0, 0, 1, 0, 0, 0 ]];

    // Function Call
    findMaximumLength(grid);

 // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
9
```

**时间复杂度:** *O(行+列)*