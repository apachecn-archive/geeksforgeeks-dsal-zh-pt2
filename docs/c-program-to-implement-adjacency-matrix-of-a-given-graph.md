# 实现给定图的邻接矩阵的 C 程序

> 原文:[https://www . geesforgeks . org/c-程序到实现-给定图的邻接矩阵/](https://www.geeksforgeeks.org/c-program-to-implement-adjacency-matrix-of-a-given-graph/)

给定一个 2D [数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **形式的 **N** 顶点 1 到 **N** 和 **M** 边的无向图，其每行由两个数字 **X** 和 **Y** 组成，表示 X 和 Y 之间有一条边，任务是编写 C 程序创建给定图的[邻接矩阵。](https://www.geeksforgeeks.org/convert-adjacency-matrix-to-adjacency-list-representation-of-graph/)**

**示例:**

> **输入:** N = 5，M = 4，arr[][] = { { 1，2 }，{ 2，3 }，{ 4，5 }，{ 1，5 } }
> T3】输出:T5】0 1 0 0 1
> 1 0 1 0 0 0
> 0 1 0 0 0
> 0 0 0 1
> 1 0 1 0 0 0
> 
> **输入:** N = 3，M = 4，arr[][] = { { 1，2 }，{ 2，3 }，{ 3，1 }，{ 2，2 } }
> **输出:**
> 0 1
> 1 1 1
> 1 1 0

**方法:**想法是使用大小为 **NxN** 的正方形矩阵来创建邻接矩阵。以下是步骤:

1.  创建一个大小为 NxN 的 2D 数组(比如 **Adj[N+1][N+1]** )，并将该矩阵的所有值初始化为零。
2.  对于 arr[][](比如 **X 和 Y** )中的每条边，将**调整【X】【Y】**和**调整【Y】【X】**处的值更新为 1，表示 X 和 Y 之间有一条边
3.  对 **arr[][]** 中的所有对进行上述操作后，显示邻接矩阵。

下面是上述方法的实现:

```
// C program for the above approach
#include <stdio.h>

// N vertices and M Edges
int N, M;

// Function to create Adjacency Matrix
void createAdjMatrix(int Adj[][N + 1],
                     int arr[][2])
{

    // Initialise all value to this
    // Adjacency list to zero
    for (int i = 0; i < N + 1; i++) {

        for (int j = 0; j < N + 1; j++) {
            Adj[i][j] = 0;
        }
    }

    // Traverse the array of Edges
    for (int i = 0; i < M; i++) {

        // Find X and Y of Edges
        int x = arr[i][0];
        int y = arr[i][1];

        // Update value to 1
        Adj[x][y] = 1;
        Adj[y][x] = 1;
    }
}

// Function to print the created
// Adjacency Matrix
void printAdjMatrix(int Adj[][N + 1])
{

    // Traverse the Adj[][]
    for (int i = 1; i < N + 1; i++) {
        for (int j = 1; j < N + 1; j++) {

            // Print the value at Adj[i][j]
            printf("%d ", Adj[i][j]);
        }
        printf("\n");
    }
}

// Driver Code
int main()
{

    // Number of vertices
    N = 5;

    // Given Edges
    int arr[][2]
        = { { 1, 2 }, { 2, 3 }, 
            { 4, 5 }, { 1, 5 } };

    // Number of Edges
    M = sizeof(arr) / sizeof(arr[0]);

    // For Adjacency Matrix
    int Adj[N + 1][N + 1];

    // Function call to create
    // Adjacency Matrix
    createAdjMatrix(Adj, arr);

    // Print Adjacency Matrix
    printAdjMatrix(Adj);

    return 0;
}
```

**Output:**

```
0 1 0 0 1 
1 0 1 0 0 
0 1 0 0 0 
0 0 0 0 1 
1 0 0 1 0

```

***时间复杂度:** O(N <sup>2</sup> )* ，其中 N 是图中的顶点数。