# 一个高度的最大可能高度，使得相邻的基质细胞最多有 1 个高度差

> 原文:[https://www . geeksforgeeks . org/最大可能高度-相邻矩阵单元的最大高度差-1/](https://www.geeksforgeeks.org/maximum-height-of-an-elevation-possible-such-that-adjacent-matrix-cells-have-a-difference-of-at-most-height-1/)

给定大小为 **M x N** 的矩阵**mat】[][]**，该矩阵表示一个区域的地形图， **0** 表示陆地， **1** 表示高程，任务是通过为每个像元分配非负高度来最大化矩阵中的高度，使得一个像元的高度为 **0** ，并且两个相邻像元的绝对高度差必须至多为 1。

**示例:**

> **输入:** mat[][] = {{1，0，0}，{0，1，0}，{0，0，1}}
> **输出:** {{0，1，2}，{1，0，1}，{2，1，0}
> 
> **输入:** mat[][] = {{0，0，1}，{1，0，0}，{0，0，0}}
> **输出:** {{1，1，0}，{0，1，1}，{1，2，2}}

**进场:**思路是用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 。按照以下步骤解决问题:

*   初始化一个尺寸为 **M x N** 的 [2d 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)、**高度**来存储最终的输出矩阵。
*   初始化[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)、**对<对< int、int > > q** 的[队列](https://www.geeksforgeeks.org/queue-data-structure/)，存储 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 的对索引。
*   [遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)并将地块单元的高度标记为 **0** 并入队，也标记为已访问。
*   执行 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) :
    *   从队列中取出一个单元格，并检查其所有 4 个相邻的单元格，如果其中任何一个单元格未被访问，则将该单元格的高度标记为当前单元格的 1 +高度。
    *   将所有未访问的相邻单元格标记为已访问。
    *   除非[队列](https://www.geeksforgeeks.org/queue-data-structure/)变空，否则重复此操作。
*   [打印最终高度矩阵。](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define M 3
#define N 3

// Utility function to find the matrix
// having the maximum height
void findHeightMatrixUtil(int mat[][N],
                          int height[M][N])
{
    // Stores index pairs for bfs
    queue<pair<int, int> > q;

    // Stores info about the visited cells
    int vis[M][N] = { 0 };

    // Traverse the matrix
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            if (mat[i][j] == 1) {
                q.push({ i, j });
                height[i][j] = 0;
                vis[i][j] = 1;
            }
        }
    }

    // Breadth First Search
    while (q.empty() == 0) {

        pair<int, int> k = q.front();
        q.pop();

        // x & y are the row & column
        // of current cell
        int x = k.first, y = k.second;

        // Check all the 4 adjacent cells
        // and marking them as visited
        // if not visited yet also marking
        // their height as 1 + height of cell (x, y)

        if (x > 0 && vis[x - 1][y] == 0) {
            height[x - 1][y] = height[x][y] + 1;
            vis[x - 1][y] = 1;
            q.push({ x - 1, y });
        }

        if (y > 0 && vis[x][y - 1] == 0) {
            height[x][y - 1] = height[x][y] + 1;
            vis[x][y - 1] = 1;
            q.push({ x, y - 1 });
        }

        if (x < M - 1 && vis[x + 1][y] == 0) {
            height[x + 1][y] = height[x][y] + 1;
            vis[x + 1][y] = 1;
            q.push({ x + 1, y });
        }

        if (y < N - 1 && vis[x][y + 1] == 0) {
            height[x][y + 1] = height[x][y] + 1;
            vis[x][y + 1] = 1;
            q.push({ x, y + 1 });
        }
    }
}

// Function to find the matrix having
// the maximum height
void findHeightMatrix(int mat[][N])
{
    // Stores output matrix
    int height[M][N];

    // Calling the helper function
    findHeightMatrixUtil(mat, height);

    // Print the final output matrix
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++)
            cout << height[i][j] << " ";

        cout << endl;
    }
}

// Driver Code
int main()
{
    // Given matrix
    int mat[][N]
        = { { 0, 0 }, { 0, 1 } };

    // Function call to find
    // the matrix having
    // the maximum height
    findHeightMatrix(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG{

static final int M = 3;
static final int N = 3;
static class pair
{
    int first, second;
    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }
}

// Utility function to find the matrix
// having the maximum height
static void findHeightMatrixUtil(int mat[][],
                          int height[][])
{
    // Stores index pairs for bfs
    Queue<pair > q = new LinkedList<>();

    // Stores info about the visited cells
    int [][]vis = new int[M][N];

    // Traverse the matrix
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            if (mat[i][j] == 1) {
                q.add(new pair( i, j ));
                height[i][j] = 0;
                vis[i][j] = 1;
            }
        }
    }

    // Breadth First Search
    while (q.isEmpty() == false) {

        pair k = q.peek();
        q.remove();

        // x & y are the row & column
        // of current cell
        int x = k.first, y = k.second;

        // Check all the 4 adjacent cells
        // and marking them as visited
        // if not visited yet also marking
        // their height as 1 + height of cell (x, y)

        if (x > 0 && vis[x - 1][y] == 0) {
            height[x - 1][y] = height[x][y] + 1;
            vis[x - 1][y] = 1;
            q.add(new pair( x - 1, y ));
        }

        if (y > 0 && vis[x][y - 1] == 0) {
            height[x][y - 1] = height[x][y] + 1;
            vis[x][y - 1] = 1;
            q.add(new pair( x, y - 1 ));
        }

        if (x < M - 1 && vis[x + 1][y] == 0) {
            height[x + 1][y] = height[x][y] + 1;
            vis[x + 1][y] = 1;
            q.add(new pair( x + 1, y ));
        }

        if (y < N - 1 && vis[x][y + 1] == 0) {
            height[x][y + 1] = height[x][y] + 1;
            vis[x][y + 1] = 1;
            q.add(new pair( x, y + 1 ));
        }
    }
}

// Function to find the matrix having
// the maximum height
static void findHeightMatrix(int mat[][])
{
    // Stores output matrix
    int [][]height = new int[M][N];

    // Calling the helper function
    findHeightMatrixUtil(mat, height);

    // Print the final output matrix
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++)
            System.out.print(height[i][j]+ " ");

        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{
    // Given matrix
    int mat[][]
        = { { 0, 0,0 }, { 0, 1,0 },{ 0, 0,0 } };

    // Function call to find
    // the matrix having
    // the maximum height
    findHeightMatrix(mat);

}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

static readonly int M = 3;
static readonly int N = 3;
class pair
{
    public int first, second;
    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }
}

// Utility function to find the matrix
// having the maximum height
static void findHeightMatrixUtil(int [,]mat,
                          int [,]height)
{

    // Stores index pairs for bfs
    Queue<pair > q = new Queue<pair>();

    // Stores info about the visited cells
    int [,]vis = new int[M,N];

    // Traverse the matrix
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            if (mat[i,j] == 1) {
                q.Enqueue(new pair( i, j ));
                height[i,j] = 0;
                vis[i,j] = 1;
            }
        }
    }

    // Breadth First Search
    while (q.Count != 0 )
    {

        pair k = q.Peek();
        q.Dequeue();

        // x & y are the row & column
        // of current cell
        int x = k.first, y = k.second;

        // Check all the 4 adjacent cells
        // and marking them as visited
        // if not visited yet also marking
        // their height as 1 + height of cell (x, y)

        if (x > 0 && vis[x - 1, y] == 0) {
            height[x - 1, y] = height[x, y] + 1;
            vis[x - 1, y] = 1;
            q.Enqueue(new pair( x - 1, y ));
        }

        if (y > 0 && vis[x, y - 1] == 0) {
            height[x, y - 1] = height[x, y] + 1;
            vis[x, y - 1] = 1;
            q.Enqueue(new pair( x, y - 1 ));
        }

        if (x < M - 1 && vis[x + 1, y] == 0) {
            height[x + 1, y] = height[x, y] + 1;
            vis[x + 1, y] = 1;
            q.Enqueue(new pair( x + 1, y ));
        }

        if (y < N - 1 && vis[x, y + 1] == 0) {
            height[x, y + 1] = height[x, y] + 1;
            vis[x, y + 1] = 1;
            q.Enqueue(new pair( x, y + 1 ));
        }
    }
}

// Function to find the matrix having
// the maximum height
static void findHeightMatrix(int [,]mat)
{
    // Stores output matrix
    int [,]height = new int[M, N];

    // Calling the helper function
    findHeightMatrixUtil(mat, height);

    // Print the readonly output matrix
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++)
            Console.Write(height[i,j]+ " ");

        Console.WriteLine();
    }
}

// Driver Code
public static void Main(String[] args)
{
    // Given matrix
    int [,]mat
        = { { 0, 0,0 }, { 0, 1,0 },{ 0, 0,0 } };

    // Function call to find
    // the matrix having
    // the maximum height
    findHeightMatrix(mat);

}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

var M = 3;
var N = 3;

// Utility function to find the matrix
// having the maximum height
function findHeightMatrixUtil(mat, height)
{
    // Stores index pairs for bfs
    var q = [];

    // Stores info about the visited cells
    var vis = Array.from(Array(M), ()=>Array(N).fill(0));

    // Traverse the matrix
    for (var i = 0; i < M; i++) {
        for (var j = 0; j < N; j++) {
            if (mat[i][j] == 1) {
                q.push([i, j]);
                height[i][j] = 0;
                vis[i][j] = 1;
            }
        }
    }

    // Breadth First Search
    while (q.length != 0) {

        var k = q[0];
        q.shift();

        // x & y are the row & column
        // of current cell
        var x = k[0], y = k[1];

        // Check all the 4 adjacent cells
        // and marking them as visited
        // if not visited yet also marking
        // their height as 1 + height of cell (x, y)

        if (x > 0 && vis[x - 1][y] == 0) {
            height[x - 1][y] = height[x][y] + 1;
            vis[x - 1][y] = 1;
            q.push([x - 1, y]);
        }

        if (y > 0 && vis[x][y - 1] == 0) {
            height[x][y - 1] = height[x][y] + 1;
            vis[x][y - 1] = 1;
            q.push([x, y - 1]);
        }

        if (x < M - 1 && vis[x + 1][y] == 0) {
            height[x + 1][y] = height[x][y] + 1;
            vis[x + 1][y] = 1;
            q.push([x + 1, y]);
        }

        if (y < N - 1 && vis[x][y + 1] == 0) {
            height[x][y + 1] = height[x][y] + 1;
            vis[x][y + 1] = 1;
            q.push([x, y + 1]);
        }
    }
    return height;
}

// Function to find the matrix having
// the maximum height
function findHeightMatrix(mat)
{
    // Stores output matrix
    var height = Array.from(Array(M), ()=>Array(N).fill(0));

    // Calling the helper function
    height = findHeightMatrixUtil(mat, height);

    // Print the final output matrix
    for (var i = 0; i < M; i++) {
        for (var j = 0; j < N; j++)
            document.write( height[i][j] + " ");

        document.write("<br>");
    }
}

// Driver Code
// Given matrix
var mat = [ [ 0, 0,0], [0, 1,0 ],[0, 0,0 ]];
// Function call to find
// the matrix having
// the maximum height
findHeightMatrix(mat);

</script>
```

**Output:** 

```
2 1 2 
1 0 1 
2 1 2
```

***时间复杂度:** O(M * N)*
***辅助空间:** O(M * N)*