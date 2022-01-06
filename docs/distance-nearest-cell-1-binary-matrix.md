# 二进制矩阵中具有 1 的最近像元的距离

> 原文:[https://www . geesforgeks . org/distance-near-cell-1-binary-matrix/](https://www.geeksforgeeks.org/distance-nearest-cell-1-binary-matrix/)

给定一个二进制矩阵**N×M**，至少包含一个值 1。任务是为每个单元找到矩阵中最近的 1 的距离。距离计算为**| I<sub>1</sub>–I<sub>2</sub>|+| j<sub>1</sub>–j<sub>2</sub>|**，其中 i <sub>1</sub> ，j <sub>1</sub> 为当前单元格的行号和列号，i <sub>2</sub> ，j <sub>2</sub> 为值为 1 的最近单元格的行号和列号。

**示例:**

```
Input : N = 3, M = 4
        mat[][] = { 0, 0, 0, 1,
                    0, 0, 1, 1,
                    0, 1, 1, 0 }
Output : 3 2 1 0
         2 1 0 0
         1 0 0 1
Explanation:
For cell at (0, 0), nearest 1 is at (0, 3),
so distance = (0 - 0) + (3 - 0) = 3.
Similarly, all the distance can be calculated.

Input : N = 3, M = 3
        mat[][] = { 1, 0, 0, 
            0, 0, 1, 
            0, 1, 1 }
Output :
       0 1 1 
       1 1 0 
       1 0 0 
Explanation:
For cell at (0, 1), nearest 1 is at (0, 0), so distance
is 1\. Similarly, all the distance can be calculated.
```

**<u>方法 1</u> :** 该方法使用简单的蛮力方法来得出解决方案。

*   **方法:**思路是遍历矩阵求每个像元的最小距离，求最小距离遍历矩阵求包含 1 的像元，计算两个像元之间的距离并存储最小距离。
*   **算法:**
    1.  从头到尾遍历矩阵(使用两个嵌套循环)
    2.  对于每个元素，找到包含 1 的最近的元素。为了找到最近的元素，遍历矩阵并找到最小距离。
    3.  填充矩阵中的最小距离。

**实施:**

## C++

```
// C++ program to find distance of nearest
// cell having 1 in a binary matrix.
#include<bits/stdc++.h>
#define N 3
#define M 4
using namespace std;

// Print the distance of nearest cell
// having 1 for each cell.
void printDistance(int mat[N][M])
{
    int ans[N][M];

    // Initialize the answer matrix with INT_MAX.
    for (int i = 0; i < N; i++)
        for (int j = 0; j < M; j++)
            ans[i][j] = INT_MAX;

    // For each cell
    for (int i = 0; i < N; i++)
        for (int j = 0; j < M; j++)
        {
            // Traversing the whole matrix
            // to find the minimum distance.
            for (int k = 0; k < N; k++)
                for (int l = 0; l < M; l++)
                {
                    // If cell contain 1, check
                    // for minimum distance.
                    if (mat[k][l] == 1)
                        ans[i][j] = min(ans[i][j],
                             abs(i-k) + abs(j-l));
                }
        }

    // Printing the answer.
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
            cout << ans[i][j] << " ";

        cout << endl;
    }
}

// Driven Program
int main()
{
    int mat[N][M] =
    {
        0, 0, 0, 1,
        0, 0, 1, 1,
        0, 1, 1, 0
    };

    printDistance(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find distance of nearest
// cell having 1 in a binary matrix.

import java.io.*;

class GFG {

    static int N = 3;
    static int M = 4;

    // Print the distance of nearest cell
    // having 1 for each cell.
    static void printDistance(int mat[][])
    {
        int ans[][] = new int[N][M];

        // Initialize the answer matrix with INT_MAX.
        for (int i = 0; i < N; i++)
            for (int j = 0; j < M; j++)
                ans[i][j] = Integer.MAX_VALUE;

        // For each cell
        for (int i = 0; i < N; i++)
            for (int j = 0; j < M; j++)
            {
                // Traversing the whole matrix
                // to find the minimum distance.
                for (int k = 0; k < N; k++)
                    for (int l = 0; l < M; l++)
                    {
                        // If cell contain 1, check
                        // for minimum distance.
                        if (mat[k][l] == 1)
                            ans[i][j] =
                              Math.min(ans[i][j],
                                   Math.abs(i-k)
                                   + Math.abs(j-l));
                    }
            }

        // Printing the answer.
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < M; j++)
                System.out.print( ans[i][j] + " ");

            System.out.println();
        }
    }

    // Driven Program
    public static void main (String[] args)
    {
        int mat[][] = { {0, 0, 0, 1},
                        {0, 0, 1, 1},
                        {0, 1, 1, 0} };

        printDistance(mat);
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to find distance of
# nearest cell having 1 in a binary matrix.

# Print distance of nearest cell
# having 1 for each cell.
def printDistance(mat):
    global N, M
    ans = [[None] * M for i in range(N)]

    # Initialize the answer matrix
    # with INT_MAX.
    for i in range(N):
        for j in range(M):
            ans[i][j] = 999999999999

    # For each cell
    for i in range(N):
        for j in range(M):

            # Traversing the whole matrix
            # to find the minimum distance.
            for k in range(N):
                for l in range(M):

                    # If cell contain 1, check
                    # for minimum distance.
                    if (mat[k][l] == 1):
                        ans[i][j] = min(ans[i][j],
                                    abs(i - k) + abs(j - l))

    # Printing the answer.
    for i in range(N):
        for j in range(M):
            print(ans[i][j], end = " ")
        print()

# Driver Code
N = 3
M = 4
mat = [[0, 0, 0, 1],
       [0, 0, 1, 1],
       [0, 1, 1, 0]]

printDistance(mat)

# This code is contributed by PranchalK
```

## C#

```
// C# program to find the distance of nearest
// cell having 1 in a binary matrix.

using System;

class GFG {

    static int N = 3;
    static int M = 4;

    // Print the distance of nearest cell
    // having 1 for each cell.
    static void printDistance(int [,]mat)
    {
        int [,]ans = new int[N,M];

        // Initialise the answer matrix with int.MaxValue.
        for (int i = 0; i < N; i++)
            for (int j = 0; j < M; j++)
                ans[i,j] = int.MaxValue;

        // For each cell
        for (int i = 0; i < N; i++)
            for (int j = 0; j < M; j++)
            {
                // Traversing thewhole matrix
                // to find the minimum distance.
                for (int k = 0; k < N; k++)
                    for (int l = 0; l < M; l++)
                    {
                        // If cell contain 1, check
                        // for minimum distance.
                        if (mat[k,l] == 1)
                            ans[i,j] =
                            Math.Min(ans[i,j],
                                Math.Abs(i-k)
                                + Math.Abs(j-l));
                    }
            }

        // Printing the answer.
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < M; j++)
                Console.Write( ans[i,j] + " ");

            Console.WriteLine();
        }
    }

    // Driven Program
    public static void Main ()
    {
        int [,]mat = { {0, 0, 0, 1},
                        {0, 0, 1, 1},
                        {0, 1, 1, 0} };

        printDistance(mat);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find distance of nearest
// cell having 1 in a binary matrix.
$N = 3;
$M = 4;

// Print the distance of nearest cell
// having 1 for each cell.
function printDistance( $mat)
{
    global $N,$M;
    $ans = array(array());

    // Initialize the answer
    // matrix with INT_MAX.
    for($i = 0; $i < $N; $i++)
        for ( $j = 0; $j < $M; $j++)
            $ans[$i][$j] = PHP_INT_MAX;

    // For each cell
    for ( $i = 0; $i < $N; $i++)
        for ( $j = 0; $j < $M; $j++)
        {

            // Traversing the whole matrix
            // to find the minimum distance.
            for ($k = 0; $k < $N; $k++)
                for ( $l = 0; $l < $M; $l++)
                {

                    // If cell contain 1, check
                    // for minimum distance.
                    if ($mat[$k][$l] == 1)
                        $ans[$i][$j] = min($ans[$i][$j],
                            abs($i-$k) + abs($j - $l));
                }
        }

    // Printing the answer.
    for ( $i = 0; $i < $N; $i++)
    {
        for ( $j = 0; $j < $M; $j++)
            echo $ans[$i][$j] , " ";

    echo "\n";
    }
}

    // Driver Code
    $mat = array(array(0, 0, 0, 1),
                 array(0, 0, 1, 1),
                 array(0, 1, 1, 0));

    printDistance($mat);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to find distance of nearest
// cell having 1 in a binary matrix.

    let N = 3;
    let M = 4;

// Print the distance of nearest cell
    // having 1 for each cell.
function printDistance(mat)
{
    let ans= new Array(N);
    for(let i=0;i<N;i++)
    {
        ans[i]=new Array(M);
        for(let j = 0; j < M; j++)
        {
            ans[i][j] = Number.MAX_VALUE;
        }
    }

    // For each cell
        for (let i = 0; i < N; i++)
            for (let j = 0; j < M; j++)
            {
                // Traversing the whole matrix
                // to find the minimum distance.
                for (let k = 0; k < N; k++)
                    for (let l = 0; l < M; l++)
                    {
                        // If cell contain 1, check
                        // for minimum distance.
                        if (mat[k][l] == 1)
                            ans[i][j] =
                              Math.min(ans[i][j],
                                   Math.abs(i-k)
                                   + Math.abs(j-l));
                    }
            }

        // Printing the answer.
        for (let i = 0; i < N; i++)
        {
            for (let j = 0; j < M; j++)
                document.write( ans[i][j] + " ");

            document.write("<br>");
        }

}

// Driven Program
let mat = [[0, 0, 0, 1],
       [0, 0, 1, 1],
       [0, 1, 1, 0]]
printDistance(mat);

// This code is contributed by patel2127
</script>
```

**输出:**

```
3 2 1 0
2 1 0 0
1 0 0 1
```

**复杂度分析:**

*   **时间复杂度:** O(N <sup>2</sup> *M <sup>2</sup> )。
    对于矩阵中的每个元素，遍历矩阵，有 N*M 个元素，因此时间复杂度为 O(N <sup>2</sup> *M <sup>2</sup> )。
*   **空间复杂度:** O(1)。
    不需要额外空间。

**<u>方法 2:</u>** 该方法使用 [BFS 或广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)技术来得出解决方案。

*   **方法:**思路是使用多源广度优先搜索。将每个像元视为一个节点，任何两个相邻像元之间的每个边界都是一条边。从 1 到 N*M 对每个单元进行编号。现在，将队列中矩阵中对应单元值为 1 的所有节点推入。使用这个队列应用 BFS 来寻找相邻节点的最小距离。
*   **算法:**
    1.  创建一个图形，将从 1 到 M*N 的值分配给所有顶点。目的是存储位置和相邻信息。
    2.  创建一个空队列。
    3.  遍历所有矩阵元素并在队列中插入全 1 的位置。
    4.  现在使用上面创建的队列对图进行 BFS 遍历。
    5.  运行一个循环，直到队列的大小大于 0，然后提取队列的前节点并移除它，并插入其所有相邻的和未标记的元素。将最小距离更新为当前节点+1 的距离，并将元素插入队列。

**实施:**

## C++

```
// C++ program to find distance of nearest
// cell having 1 in a binary matrix.
#include<bits/stdc++.h>
#define MAX 500
#define N 3
#define M 4
using namespace std;

// Making a class of graph with bfs function.
class graph
{
private:
    vector<int> g[MAX];
    int n,m;

public:
    graph(int a, int b)
    {
        n = a;
        m = b;
    }

    // Function to create graph with N*M nodes
    // considering each cell as a node and each
    // boundary as an edge.
    void createGraph()
    {
        int k = 1;  // A number to be assigned to a cell

        for (int i = 1; i <= n; i++)
        {
            for (int j = 1; j <= m; j++)
            {
                // If last row, then add edge on right side.
                if (i == n)
                {
                    // If not bottom right cell.
                    if (j != m)
                    {
                        g[k].push_back(k+1);
                        g[k+1].push_back(k);
                    }
                }

                // If last column, then add edge toward down.
                else if (j == m)
                {
                    g[k].push_back(k+m);
                    g[k+m].push_back(k);
                }

                // Else makes an edge in all four directions.
                else
                {
                    g[k].push_back(k+1);
                    g[k+1].push_back(k);
                    g[k].push_back(k+m);
                    g[k+m].push_back(k);
                }

                k++;
            }
        }
    }

    // BFS function to find minimum distance
    void bfs(bool visit[], int dist[], queue<int> q)
    {
        while (!q.empty())
        {
            int temp = q.front();
            q.pop();

            for (int i = 0; i < g[temp].size(); i++)
            {
                if (visit[g[temp][i]] != 1)
                {
                    dist[g[temp][i]] =
                    min(dist[g[temp][i]], dist[temp]+1);

                    q.push(g[temp][i]);
                    visit[g[temp][i]] = 1;
                }
            }
        }
    }

    // Printing the solution.
    void print(int dist[])
    {
        for (int i = 1, c = 1; i <= n*m; i++, c++)
        {
            cout << dist[i] << " ";

            if (c%m == 0)
                cout << endl;
        }
    }
};

// Find minimum distance
void findMinDistance(bool mat[N][M])
{
    // Creating a graph with nodes values assigned
    // from 1 to N x M and matrix adjacent.
    graph g1(N, M);
    g1.createGraph();

    // To store minimum distance
    int dist[MAX];

    // To mark each node as visited or not in BFS
    bool visit[MAX] = { 0 };

    // Initialising the value of distance and visit.
    for (int i = 1; i <= M*N; i++)
    {
        dist[i] = INT_MAX;
        visit[i] = 0;
    }

    // Inserting nodes whose value in matrix
    // is 1 in the queue.
    int k = 1;
    queue<int> q;
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {
            if (mat[i][j] == 1)
            {
                dist[k] = 0;
                visit[k] = 1;
                q.push(k);
            }
            k++;
        }
    }

    // Calling for Bfs with given Queue.
    g1.bfs(visit, dist, q);

    // Printing the solution.
    g1.print(dist);
}

// Driven Program
int main()
{
    bool mat[N][M] =
    {
        0, 0, 0, 1,
        0, 0, 1, 1,
        0, 1, 1, 0
    };

    findMinDistance(mat);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find distance of nearest
# cell having 1 in a binary matrix.
from collections import deque

MAX = 500
N = 3
M = 4

# Making a class of graph with bfs function.
g = [[] for i in range(MAX)]
n, m = 0, 0

# Function to create graph with N*M nodes
# considering each cell as a node and each
# boundary as an edge.
def createGraph():

    global g, n, m

    # A number to be assigned to a cell
    k = 1 

    for i in range(1, n + 1):
        for j in range(1, m + 1):

            # If last row, then add edge on right side.
            if (i == n):

                # If not bottom right cell.
                if (j != m):
                    g[k].append(k + 1)
                    g[k + 1].append(k)

            # If last column, then add edge toward down.
            elif (j == m):
                g[k].append(k+m)
                g[k + m].append(k)

            # Else makes an edge in all four directions.
            else:
                g[k].append(k + 1)
                g[k + 1].append(k)
                g[k].append(k+m)
                g[k + m].append(k)

            k += 1

# BFS function to find minimum distance
def bfs(visit, dist, q):

    global g
    while (len(q) > 0):
        temp = q.popleft()

        for i in g[temp]:
            if (visit[i] != 1):
                dist[i] = min(dist[i], dist[temp] + 1)
                q.append(i)
                visit[i] = 1

    return dist

# Printing the solution.
def prt(dist):

    c = 1
    for i in range(1, n * m + 1):
        print(dist[i], end = " ")
        if (c % m == 0):
            print()

        c += 1

# Find minimum distance
def findMinDistance(mat):

    global g, n, m

    # Creating a graph with nodes values assigned
    # from 1 to N x M and matrix adjacent.
    n, m = N, M
    createGraph()

    # To store minimum distance
    dist = [0] * MAX

    # To mark each node as visited or not in BFS
    visit = [0] * MAX

    # Initialising the value of distance and visit.
    for i in range(1, M * N + 1):
        dist[i] = 10**9
        visit[i] = 0

    # Inserting nodes whose value in matrix
    # is 1 in the queue.
    k = 1
    q =  deque()
    for i in range(N):
        for j in range(M):
            if (mat[i][j] == 1):
                dist[k] = 0
                visit[k] = 1
                q.append(k)

            k += 1

    # Calling for Bfs with given Queue.
    dist = bfs(visit, dist, q)

    # Printing the solution.
    prt(dist)

# Driver code
if __name__ == '__main__':

    mat = [ [ 0, 0, 0, 1 ],
            [ 0, 0, 1, 1 ],
            [ 0, 1, 1, 0 ] ]

    findMinDistance(mat)

# This code is contributed by mohit kumar 29
```

**输出:**

```
3 2 1 0 
2 1 0 0 
1 0 0 1 
```

**复杂度分析:**

*   **时间复杂度:** O(N*M)。
    在 BFS 遍历中，每个元素只遍历一次，因此时间复杂度为 0(M * N)。
*   **空间复杂度:** O(M*N)。
    要存储矩阵中的每个元素，需要 O(M*N)空间。

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。