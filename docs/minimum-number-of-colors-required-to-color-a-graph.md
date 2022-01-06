# 给图形上色所需的最小颜色数

> 原文:[https://www . geeksforgeeks . org/最小颜色数-图表所需颜色数/](https://www.geeksforgeeks.org/minimum-number-of-colors-required-to-color-a-graph/)

给定一个有 **N** 个顶点和 **E** 条边的图。给定的边为 **U[]** 和 **V[]** ，使得对于每个索引 I， **U[i]** 连接到 **V[i]** 。任务是找到给定图形着色所需的最小颜色数。
**示例**

> **输入:** N = 5，M = 6，U[] = { 1，2，3，1，2，3 }，V[] = { 3，3，4，4，5，5 }；
> **输出:** 3
> **说明:**
> 对于上图节点 1、3、5 不能有相同的颜色。因此计数为 3。

**进场:**
我们将守两阵**计数[]** 和**颜色[]** 。数组**count【】**将存储每个节点的边数，**colors【】**将存储每个节点的颜色。将每个顶点的计数初始化为 0，将每个顶点的颜色初始化为 1。
**步骤:**

1.  为给定的边集制作一个邻接表，并记录每个节点的边数
2.  迭代所有节点，将节点插入无边的队列 **Q** 中。
3.  当 **Q** 不为空时，执行以下操作:
    *   从队列中弹出元素。
    *   对于连接到弹出节点的所有节点:
        1.  减少弹出节点的当前边缘计数。
        2.  如果当前节点的颜色小于或等于其父节点(弹出的节点)的颜色，则更新当前节点的颜色= 1 +弹出节点的颜色
        3.  如果计数为零，则将该节点插入队列 **Q** 。
4.  **colors【】**数组中的最大元素将给出给定图形着色所需的最小颜色数。

以下是上述方法的实现:

## C++

```
// C++ program to find the minimum
// number of colors needed to color
// the graph
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum
// number of color required
void minimumColors(int N, int E,
                   int U[], int V[])
{

    // Create array of vectors
    // to make adjacency list
    vector<int> adj[N];

    // Initialise colors array to 1
    // and count array to 0
    vector<int> count(N, 0);
    vector<int> colors(N, 1);

    // Create adjacency list of
    // a graph
    for (int i = 0; i < N; i++) {
        adj[V[i] - 1].push_back(U[i] - 1);
        count[U[i] - 1]++;
    }

    // Declare queue Q
    queue<int> Q;

    // Traverse count[] and insert
    // in Q if count[i] = 0;
    for (int i = 0; i < N; i++) {
        if (count[i] == 0) {
            Q.push(i);
        }
    }

    // Traverse queue and update
    // the count of colors
    // adjacent node
    while (!Q.empty()) {
        int u = Q.front();
        Q.pop();

        // Traverse node u
        for (auto x : adj[u]) {
            count[x]--;

            // If count[x] = 0
            // insert in Q
            if (count[x] == 0) {
                Q.push(x);
            }

            // If colors of child
            // node is less than
            // parent node, update
            // the count by 1
            if (colors[x] <= colors[u]) {
                colors[x] = 1 + colors[u];
            }
        }
    }

    // Stores the minimumColors
    // requires to color the graph.
    int minColor = -1;

    // Find the maximum of colors[]
    for (int i = 0; i < N; i++) {
        minColor = max(minColor, colors[i]);
    }

    // Print the minimum no. of
    // colors required.
    cout << minColor << endl;
}

// Driver function
int main()
{
    int N = 5, E = 6;
    int U[] = { 1, 2, 3, 1, 2, 3 };
    int V[] = { 3, 3, 4, 4, 5, 5 };

    minimumColors(N, E, U, V);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// number of colors needed to color
// the graph
import java.util.*;

class GFG
{

// Function to count the minimum
// number of color required
static void minimumColors(int N, int E,
                int U[], int V[])
{

    // Create array of vectors
    // to make adjacency list
    Vector<Integer> []adj = new Vector[N];

    // Initialise colors array to 1
    // and count array to 0
    int []count = new int[N];
    int []colors = new int[N];
    for (int i = 0; i < N; i++) {
        adj[i] = new Vector<Integer>();
        colors[i] = 1;
    }

    // Create adjacency list of
    // a graph
    for (int i = 0; i < N; i++) {
        adj[V[i] - 1].add(U[i] - 1);
        count[U[i] - 1]++;
    }

    // Declare queue Q
    Queue<Integer> Q = new LinkedList<>();

    // Traverse count[] and insert
    // in Q if count[i] = 0;
    for (int i = 0; i < N; i++) {
        if (count[i] == 0) {
            Q.add(i);
        }
    }

    // Traverse queue and update
    // the count of colors
    // adjacent node
    while (!Q.isEmpty()) {
        int u = Q.peek();
        Q.remove();

        // Traverse node u
        for (int x : adj[u]) {
            count[x]--;

            // If count[x] = 0
            // insert in Q
            if (count[x] == 0) {
                Q.add(x);
            }

            // If colors of child
            // node is less than
            // parent node, update
            // the count by 1
            if (colors[x] <= colors[u]) {
                colors[x] = 1 + colors[u];
            }
        }
    }

    // Stores the minimumColors
    // requires to color the graph.
    int minColor = -1;

    // Find the maximum of colors[]
    for (int i = 0; i < N; i++) {
        minColor = Math.max(minColor, colors[i]);
    }

    // Print the minimum no. of
    // colors required.
    System.out.print(minColor +"\n");
}

// Driver function
public static void main(String[] args)
{
    int N = 5, E = 6;
    int U[] = { 1, 2, 3, 1, 2, 3 };
    int V[] = { 3, 3, 4, 4, 5, 5 };

    minimumColors(N, E, U, V);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# number of colors needed to color
# the graph
from collections import deque

# Function to count the minimum
# number of color required
def minimumColors(N, E, U, V):

    # Create array of vectors
    # to make adjacency list
    adj = [[] for i in range(N)]

    # Initialise colors array to 1
    # and count array to 0
    count = [0]*N
    colors = [1]*(N)

    # Create adjacency list of
    # a graph
    for i in range(N):
        adj[V[i] - 1].append(U[i] - 1)
        count[U[i] - 1] += 1

    # Declare queue Q
    Q = deque()

    # Traverse count[] and insert
    # in Q if count[i] = 0
    for i in range(N):
        if (count[i] == 0):
            Q.append(i)

    # Traverse queue and update
    # the count of colors
    # adjacent node
    while len(Q) > 0:
        u = Q.popleft()

        # Traverse node u
        for x in adj[u]:
            count[x] -= 1

            # If count[x] = 0
            # insert in Q
            if (count[x] == 0):
                Q.append(x)

            # If colors of child
            # node is less than
            # parent node, update
            # the count by 1
            if (colors[x] <= colors[u]):
                colors[x] = 1 + colors[u]

    # Stores the minimumColors
    # requires to color the graph.
    minColor = -1

    # Find the maximum of colors[]
    for i in range(N):
        minColor = max(minColor, colors[i])

    # Print the minimum no. of
    # colors required.
    print(minColor)

# Driver function
N = 5
E = 6
U = [1, 2, 3, 1, 2, 3]
V = [3, 3, 4, 4, 5, 5]

minimumColors(N, E, U, V)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the minimum
// number of colors needed to color
// the graph
using System;
using System.Collections.Generic;

class GFG
{

// Function to count the minimum
// number of color required
static void minimumColors(int N, int E,
                int []U, int []V)
{

    // Create array of vectors
    // to make adjacency list
    List<int> []adj = new List<int>[N];

    // Initialise colors array to 1
    // and count array to 0
    int []count = new int[N];
    int []colors = new int[N];
    for (int i = 0; i < N; i++) {
        adj[i] = new List<int>();
        colors[i] = 1;
    }

    // Create adjacency list of
    // a graph
    for (int i = 0; i < N; i++) {
        adj[V[i] - 1].Add(U[i] - 1);
        count[U[i] - 1]++;
    }

    // Declare queue Q
    List<int> Q = new List<int>();

    // Traverse []count and insert
    // in Q if count[i] = 0;
    for (int i = 0; i < N; i++) {
        if (count[i] == 0) {
            Q.Add(i);
        }
    }

    // Traverse queue and update
    // the count of colors
    // adjacent node
    while (Q.Count!=0) {
        int u = Q[0];
        Q.RemoveAt(0);

        // Traverse node u
        foreach (int x in adj[u]) {
            count[x]--;

            // If count[x] = 0
            // insert in Q
            if (count[x] == 0) {
                Q.Add(x);
            }

            // If colors of child
            // node is less than
            // parent node, update
            // the count by 1
            if (colors[x] <= colors[u]) {
                colors[x] = 1 + colors[u];
            }
        }
    }

    // Stores the minimumColors
    // requires to color the graph.
    int minColor = -1;

    // Find the maximum of colors[]
    for (int i = 0; i < N; i++) {
        minColor = Math.Max(minColor, colors[i]);
    }

    // Print the minimum no. of
    // colors required.
    Console.Write(minColor +"\n");
}

// Driver function
public static void Main(String[] args)
{
    int N = 5, E = 6;
    int []U = { 1, 2, 3, 1, 2, 3 };
    int []V = { 3, 3, 4, 4, 5, 5 };

    minimumColors(N, E, U, V);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find the minimum
// number of colors needed to color
// the graph

// Function to count the minimum
// number of color required
function minimumColors(N,E,U,V)
{
    // Create array of vectors
    // to make adjacency list
    let adj = new Array(N);

    // Initialise colors array to 1
    // and count array to 0
    let count = new Array(N);
    let colors = new Array(N);
    for (let i = 0; i < N; i++) {
        adj[i] = [];
        colors[i] = 1;
        count[i]=0;
    }

    // Create adjacency list of
    // a graph
    for (let i = 0; i < N; i++) {
        adj[V[i] - 1].push(U[i] - 1);
        count[U[i] - 1]++;
    }

    // Declare queue Q
    let Q = [];

    // Traverse count[] and insert
    // in Q if count[i] = 0;
    for (let i = 0; i < N; i++) {
        if (count[i] == 0) {
            Q.push(i);
        }
    }

    // Traverse queue and update
    // the count of colors
    // adjacent node
    while (Q.length!=0) {
        let u = Q.shift();

        // Traverse node u
        for (let x=0;x<adj[u].length;x++) {
            count[adj[u][x]]--;

            // If count[x] = 0
            // insert in Q
            if (count[adj[u][x]] == 0) {
                Q.push(adj[u][x]);
            }

            // If colors of child
            // node is less than
            // parent node, update
            // the count by 1
            if (colors[adj[u][x]] <= colors[u]) {
                colors[adj[u][x]] = 1 + colors[u];
            }
        }
    }

    // Stores the minimumColors
    // requires to color the graph.
    let minColor = -1;

    // Find the maximum of colors[]
    for (let i = 0; i < N; i++) {
        minColor = Math.max(minColor, colors[i]);
    }

    // Print the minimum no. of
    // colors required.
    document.write(minColor +"\n");
}

// Driver function
let N = 5, E = 6;
let U = [ 1, 2, 3, 1, 2, 3 ];
let V = [ 3, 3, 4, 4, 5, 5 ];

minimumColors(N, E, U, V);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N+E)，其中 N =顶点数，E =边数