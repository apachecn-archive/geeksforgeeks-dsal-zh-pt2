# 图的两个顶点之间的最小边数

> 原文:[https://www . geesforgeks . org/图的两个顶点之间的最小边数/](https://www.geeksforgeeks.org/minimum-number-of-edges-between-two-vertices-of-a-graph/)

给你一个有 N 个顶点和 M 条边的无向图 G(V，E)。我们需要找到给定顶点对(u，v)之间的最小边数。

**示例:**

```
Input : For given graph G. Find minimum number
        of edges between (1, 5).
```

![](img/3b5b85b2d29e360f2965840445327224.png)

```
Output : 2
Explanation: (1, 2) and (2, 5) are the only
edges resulting into shortest path between 1
and 5.
```

想法是从一个给定的输入顶点(u)执行 BFS。在 BFS 的时候保持一个距离[n]的数组，并为所有顶点初始化为零。现在，假设在 BFS 期间，顶点 x 从队列中弹出，同时我们将所有相邻的非访问顶点(I)推回到队列中，我们应该更新**距离[i] =距离[x]+1；**。
最后，距离[v]给出了 u 和 v 之间的最小边数。

**算法:**

```
int minEdgeBFS(int u, int v, int n)
{
    // visited[n] for keeping track of visited
    // node in BFS
    bool visited[n] = {0};

    // Initialize distances as 0
    int distance[n] = {0};

    // queue to do BFS.
    queue  Q;
    distance[u] = 0;

    Q.push(u);
    visited[u] = true;
    while (!Q.empty())
    {
        int x = Q.front();
        Q.pop();

        for (int i=0; i<edges[x].size(); i++)
        {
            if (visited[edges[x][i]])
                continue;

            // update distance for i
            distance[edges[x][i]] = distance[x] + 1;
            Q.push(edges[x][i]);
            visited[edges[x][i]] = 1;
        }
    }
    return distance[v];
}
```

## C++

```
// C++ program to find minimum edge
// between given two vertex of Graph
#include<bits/stdc++.h>
using namespace std;

// function for finding minimum no. of edge
// using BFS
int minEdgeBFS(vector <int> edges[], int u,
                              int v, int n)
{
    // visited[n] for keeping track of visited
    // node in BFS
    vector<bool> visited(n, 0);

    // Initialize distances as 0
    vector<int> distance(n, 0);

    // queue to do BFS.
    queue <int> Q;
    distance[u] = 0;

    Q.push(u);
    visited[u] = true;
    while (!Q.empty())
    {
        int x = Q.front();
        Q.pop();

        for (int i=0; i<edges[x].size(); i++)
        {
            if (visited[edges[x][i]])
                continue;

            // update distance for i
            distance[edges[x][i]] = distance[x] + 1;
            Q.push(edges[x][i]);
            visited[edges[x][i]] = 1;
        }
    }
    return distance[v];
}

// function for addition of edge
void addEdge(vector <int> edges[], int u, int v)
{
   edges[u].push_back(v);
   edges[v].push_back(u);
}

// Driver function
int main()
{
    // To store adjacency list of graph
    int n = 9;
    vector <int> edges[9];
    addEdge(edges, 0, 1);
    addEdge(edges, 0, 7);
    addEdge(edges, 1, 7);
    addEdge(edges, 1, 2);
    addEdge(edges, 2, 3);
    addEdge(edges, 2, 5);
    addEdge(edges, 2, 8);
    addEdge(edges, 3, 4);
    addEdge(edges, 3, 5);
    addEdge(edges, 4, 5);
    addEdge(edges, 5, 6);
    addEdge(edges, 6, 7);
    addEdge(edges, 7, 8);
    int u = 0;
    int v = 5;
    cout << minEdgeBFS(edges, u, v, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum edge
// between given two vertex of Graph

import java.util.LinkedList;
import java.util.Queue;
import java.util.Vector;

class Test
{
    // Method for finding minimum no. of edge
    // using BFS
    static int minEdgeBFS(Vector <Integer> edges[], int u,
                                  int v, int n)
    {
        // visited[n] for keeping track of visited
        // node in BFS
        Vector<Boolean> visited = new Vector<Boolean>(n);

        for (int i = 0; i < n; i++) {
            visited.addElement(false);
        }

        // Initialize distances as 0
        Vector<Integer> distance = new Vector<Integer>(n);

        for (int i = 0; i < n; i++) {
            distance.addElement(0);
        }

        // queue to do BFS.
        Queue<Integer> Q = new LinkedList<>();
        distance.setElementAt(0, u);

        Q.add(u);
        visited.setElementAt(true, u);
        while (!Q.isEmpty())
        {
            int x = Q.peek();
            Q.poll();

            for (int i=0; i<edges[x].size(); i++)
            {
                if (visited.elementAt(edges[x].get(i)))
                    continue;

                // update distance for i
                distance.setElementAt(distance.get(x) + 1,edges[x].get(i));
                Q.add(edges[x].get(i));
                visited.setElementAt(true,edges[x].get(i));
            }
        }
        return distance.get(v);
    }

    // method for addition of edge
    static void addEdge(Vector <Integer> edges[], int u, int v)
    {
       edges[u].add(v);
       edges[v].add(u);
    }

    // Driver method
    public static void main(String args[])
    {
        // To store adjacency list of graph
        int n = 9;
        Vector <Integer> edges[] = new Vector[9];

        for (int i = 0; i < edges.length; i++) {
            edges[i] = new Vector<>();
        }

        addEdge(edges, 0, 1);
        addEdge(edges, 0, 7);
        addEdge(edges, 1, 7);
        addEdge(edges, 1, 2);
        addEdge(edges, 2, 3);
        addEdge(edges, 2, 5);
        addEdge(edges, 2, 8);
        addEdge(edges, 3, 4);
        addEdge(edges, 3, 5);
        addEdge(edges, 4, 5);
        addEdge(edges, 5, 6);
        addEdge(edges, 6, 7);
        addEdge(edges, 7, 8);
        int u = 0;
        int v = 5;
        System.out.println(minEdgeBFS(edges, u, v, n));
    }
}
// This code is contributed by Gaurav Miglani
```

## 蟒蛇 3

```
# Python3 program to find minimum edge
# between given two vertex of Graph
import queue

# function for finding minimum
# no. of edge using BFS
def minEdgeBFS(edges, u, v, n):

    # visited[n] for keeping track
    # of visited node in BFS
    visited = [0] * n

    # Initialize distances as 0
    distance = [0] * n

    # queue to do BFS.
    Q = queue.Queue()
    distance[u] = 0

    Q.put(u)
    visited[u] = True
    while (not Q.empty()):
        x = Q.get()

        for i in range(len(edges[x])):
            if (visited[edges[x][i]]):
                continue

            # update distance for i
            distance[edges[x][i]] = distance[x] + 1
            Q.put(edges[x][i])
            visited[edges[x][i]] = 1
    return distance[v]

# function for addition of edge
def addEdge(edges, u, v):
    edges[u].append(v)
    edges[v].append(u)

# Driver  Code
if __name__ == '__main__':

    # To store adjacency list of graph
    n = 9
    edges = [[] for i in range(n)]
    addEdge(edges, 0, 1)
    addEdge(edges, 0, 7)
    addEdge(edges, 1, 7)
    addEdge(edges, 1, 2)
    addEdge(edges, 2, 3)
    addEdge(edges, 2, 5)
    addEdge(edges, 2, 8)
    addEdge(edges, 3, 4)
    addEdge(edges, 3, 5)
    addEdge(edges, 4, 5)
    addEdge(edges, 5, 6)
    addEdge(edges, 6, 7)
    addEdge(edges, 7, 8)
    u = 0
    v = 5
    print(minEdgeBFS(edges, u, v, n))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find minimum edge
// between given two vertex of Graph
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Method for finding minimum no. of edge
// using BFS
static int minEdgeBFS(ArrayList []edges, int u,
                                  int v, int n)
{

    // visited[n] for keeping track of visited
    // node in BFS
    ArrayList visited = new ArrayList();
    for(int i = 0; i < n; i++)
    {
        visited.Add(false);
    }

    // Initialize distances as 0
    ArrayList distance = new ArrayList();
    for(int i = 0; i < n; i++)
    {
        distance.Add(0);
    }

    // queue to do BFS.
    Queue Q = new Queue();

    distance[u] = 0;

    Q.Enqueue(u);

    visited[u] = true;

    while (Q.Count != 0)
    {
        int x = (int)Q.Dequeue();

        for(int i = 0; i < edges[x].Count; i++)
        {
            if ((bool)visited[(int)edges[x][i]])
                continue;

            // Update distance for i
            distance[(int)edges[x][i]] = (int)distance[x] + 1;
            Q.Enqueue((int)edges[x][i]);
            visited[(int)edges[x][i]] = true;
        }
    }
    return (int)distance[v];
}

// Method for addition of edge
static void addEdge(ArrayList []edges,
                    int u, int v)
{
    edges[u].Add(v);
    edges[v].Add(u);
}

// Driver code
public static void Main(string []args)
{

    // To store adjacency list of graph
    int n = 9;
    ArrayList []edges = new ArrayList[9];

    for(int i = 0; i < 9; i++)
    {
        edges[i] = new ArrayList();
    }

    addEdge(edges, 0, 1);
    addEdge(edges, 0, 7);
    addEdge(edges, 1, 7);
    addEdge(edges, 1, 2);
    addEdge(edges, 2, 3);
    addEdge(edges, 2, 5);
    addEdge(edges, 2, 8);
    addEdge(edges, 3, 4);
    addEdge(edges, 3, 5);
    addEdge(edges, 4, 5);
    addEdge(edges, 5, 6);
    addEdge(edges, 6, 7);
    addEdge(edges, 7, 8);

    int u = 0;
    int v = 5;

    Console.Write(minEdgeBFS(edges, u, v, n));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript program to find minimum edge
// between given two vertex of Graph

// Method for finding minimum no. of edge
// using BFS
function  minEdgeBFS(edges,u,v,n)
{
    // visited[n] for keeping track of visited
        // node in BFS
        let visited = [];

        for (let i = 0; i < n; i++) {
            visited.push(false);
        }

        // Initialize distances as 0
        let distance = [];

        for (let i = 0; i < n; i++) {
            distance.push(0);
        }

        // queue to do BFS.
        let Q = [];
        distance[u] = 0;

        Q.push(u);
        visited[u] = true;
        while (Q.length!=0)
        {
            let x = Q.shift();

            for (let i=0; i<edges[x].length; i++)
            {
                if (visited[edges[x][i]])
                    continue;

                // update distance for i
                distance[edges[x][i]] = distance[x] + 1;
                Q.push(edges[x][i]);
                visited[edges[x][i]]= true;
            }
        }
        return distance[v];
}

// method for addition of edge
function addEdge(edges,u,v)
{
    edges[u].push(v);
       edges[v].push(u);
}

// Driver method
// To store adjacency list of graph
let n = 9;
let edges = new Array(9);

for (let i = 0; i < edges.length; i++) {
    edges[i] = [];
}

addEdge(edges, 0, 1);
addEdge(edges, 0, 7);
addEdge(edges, 1, 7);
addEdge(edges, 1, 2);
addEdge(edges, 2, 3);
addEdge(edges, 2, 5);
addEdge(edges, 2, 8);
addEdge(edges, 3, 4);
addEdge(edges, 3, 5);
addEdge(edges, 4, 5);
addEdge(edges, 5, 6);
addEdge(edges, 6, 7);
addEdge(edges, 7, 8);
let u = 0;
let v = 5;
document.write(minEdgeBFS(edges, u, v, n));

// This code is contributed by rag2127

</script>
```

**输出:**

```
3
```

本文由[Shivam prad Han(anuj _ charm)](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。