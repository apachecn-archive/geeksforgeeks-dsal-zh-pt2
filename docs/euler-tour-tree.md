# 欧拉树之旅

> 原文:[https://www.geeksforgeeks.org/euler-tour-tree/](https://www.geeksforgeeks.org/euler-tour-tree/)

树是连通图的推广，它有 N 个节点，正好有 N-1 条边，即每对顶点之间有一条边。求邻接表表示的树的欧拉游。
示例:
输入:

![](img/6888cd7aecbeaadb07f748bcf69b7065.png)

输出:1 2 3 2 4 2 1
输入:

![](img/04281a82f60049b469618610ce545360.png)

产出:1 5 4 2 4 3 4 5 1

**欧拉漫游**被定义为一种遍历树的方式，这样当我们访问它时，每个顶点都被添加到漫游中(或者从父顶点向下移动，或者从子顶点返回)。我们从根开始，并在访问所有顶点后回到根。
**它需要正好 2*N-1 个顶点来存储欧拉游。**

**逼近**:我们将在树上运行 DFS(深度优先搜索)算法为:

![](img/e9ba64d389920acb46f9372339bb51ab.png)

(1) **访问根节点，即 1**
vis[1]=1，欧拉[0]=1
为所有未访问的相邻节点运行 DFS()(2)
(2)**访问节点 2**
vis[2]=1，欧拉[1]=2
为所有未访问的相邻节点(3，4)
(3) **访问节点 3**
vis[3]=1 欧拉[4]=4
所有相邻节点都已经被访问，返回父节点
并添加父节点到欧拉游，欧拉[5]=2
(5) **访问节点 2**
所有相邻节点都已经被访问，返回父节点
并添加父节点到欧拉游，欧拉[6]=1
(6) **访问节点 1**
所有相邻节点都已经被访问，节点 1 是根节点
所以
类似地，例如例 2:

![](img/7f6906e6c73e267c3d3c6c9ba95d0863.png)

## C++

```
// C++ program to print Euler tour of a
// tree.
#include <bits/stdc++.h>
using namespace std;

#define MAX 1001

// Adjacency list representation of tree
vector<int> adj[MAX];

// Visited array to keep track visited
// nodes on tour
int vis[MAX];

// Array to store Euler Tour
int Euler[2 * MAX];

// Function to add edges to tree
void add_edge(int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// Function to store Euler Tour of tree
void eulerTree(int u, int &index)
{
    vis[u] = 1;
    Euler[index++] = u;
    for (auto it : adj[u]) {
        if (!vis[it]) {
            eulerTree(it, index);
            Euler[index++] = u;
        }
    }
}

// Function to print Euler Tour of tree
void printEulerTour(int root, int N)
{
    int index = 0; 
    eulerTree(root, index);
    for (int i = 0; i < (2*N-1); i++)
        cout << Euler[i] << " ";
}

// Driver code
int main()
{
    int N = 4;

    add_edge(1, 2);
    add_edge(2, 3);
    add_edge(2, 4);

    // Consider 1 as root and print
    // Euler tour
    printEulerTour(1, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print Euler tour of a
// tree.
import java.util.*;

class GFG{

static final int MAX = 1001;
static int index = 0;

// Adjacency list representation of tree
static ArrayList<
       ArrayList<Integer>> adj = new ArrayList<>();

// Visited array to keep track visited
// nodes on tour
static int vis[] = new int[MAX];

// Array to store Euler Tour
static int Euler[] = new int[2 * MAX];

// Function to add edges to tree
static void add_edge(int u, int v)
{
    adj.get(u).add(v);
    adj.get(v).add(u);
}

// Function to store Euler Tour of tree
static void eulerTree(int u)
{
    vis[u] = 1;
    Euler[index++] = u;

    for(int it : adj.get(u))
    {
        if (vis[it] == 0)
        {
            eulerTree(it);
            Euler[index++] = u;
        }
    }
}

// Function to print Euler Tour of tree
static void printEulerTour(int root, int N)
{
    eulerTree(root);
    for(int i = 0; i < (2 * N - 1); i++)
        System.out.print(Euler[i] + " ");
}

// Driver code
public static void main(String[] args)
{
    int N = 4;

    for(int i = 0; i <= N; i++)
        adj.add(new ArrayList<>());

    add_edge(1, 2);
    add_edge(2, 3);
    add_edge(2, 4);

    // Consider 1 as root and print
    // Euler tour
    printEulerTour(1, N);
}
}

// This code is contributed by jrishabh99
```

## java 描述语言

```
<script>

// Javascript program to print Euler tour of a
// tree.
var MAX = 1001;

// Adjacency list representation of tree
var adj = Array.from(Array(MAX), () => Array());

// Visited array to keep track visited
// nodes on tour
var vis = Array(MAX);

// Array to store Euler Tour
var Euler = Array(2 * MAX);

// Function to add edges to tree
function add_edge(u, v)
{
    adj[u].push(v);
    adj[v].push(u);
}

// Function to store Euler Tour of tree
function eulerTree(u, index)
{
    vis[u] = 1;
    Euler[index++] = u;

    for(var it of adj[u])
    {
        if (!vis[it])
        {
            index = eulerTree(it, index);
            Euler[index++] = u;
        }
    }
    return index;
}

// Function to print Euler Tour of tree
function printEulerTour(root, N)
{
    var index = 0; 
    index = eulerTree(root, index);
    for(var i = 0; i < (2 * N - 1); i++)
        document.write(Euler[i] + " ");
}

// Driver code
var N = 4;
add_edge(1, 2);
add_edge(2, 3);
add_edge(2, 4);

// Consider 1 as root and print
// Euler tour
printEulerTour(1, N);

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
1 2 3 2 4 2 1
```

辅助空间:O(N)
时间复杂度:O(N)