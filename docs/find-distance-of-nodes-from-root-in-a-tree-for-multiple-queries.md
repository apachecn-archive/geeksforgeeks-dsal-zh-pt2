# 在一棵树中为多个查询找到节点到根的距离

> 原文:[https://www . geesforgeks . org/find-多查询从根到树的节点距离/](https://www.geeksforgeeks.org/find-distance-of-nodes-from-root-in-a-tree-for-multiple-queries/)

给定一棵具有从 0 到 N–1 编号的 **N** 顶点的树和包含树中节点的 **Q** 查询，任务是为多个查询找到给定节点到根节点的距离。将第 0 个节点视为根节点，并将根节点与自身的距离取为 0。
**例:**

```
Tree:
      0
     /  \
    1    2
    |   / \
    3  4   5
Input: 2
Output: 1
Explanation:
Distance of node 2 from root is 1

Input: 3
Output: 2
Explanation:
Distance of node 3 from root is 2
```

**方法:**
首先将根节点的距离指定为 0。然后，使用广度优先遍历(BFS)遍历树。将节点 N 的子节点标记为已访问时，也将这些子节点的距离指定为距离[N] + 1。最后，对于不同的查询，打印节点的距离数组的值。
以下是上述办法的实施:

## C++

```
// C++ implementation for
// the above approach
#include <bits/stdc++.h>
using namespace std;

const int sz = 1e5;

// Adjacency list representation
// of the tree
vector<int> tree[sz + 1];

// Boolean array to mark all the
// vertices which are visited
bool vis[sz + 1];

// Array of vector where ith index
// stores the path from the root
// node to the ith node
int dis[sz + 1];

// Function to create an
// edge between two vertices
void addEdge(int a, int b)
{
    // Add a to b's list
    tree[a].push_back(b);

    // Add b to a's list
    tree[b].push_back(a);
}

// Modified Breadth-First Function
void bfs(int node)
{
    // Create a queue of {child, parent}
    queue<pair<int, int> > qu;

    // Push root node in the front of
    qu.push({ node, 0 });
    dis[0] = 0;

    while (!qu.empty()) {
        pair<int, int> p = qu.front();

        // Dequeue a vertex from queue
        qu.pop();
        vis[p.first] = true;

        // Get all adjacent vertices of the dequeued
        // vertex s. If any adjacent has not
        // been visited then enqueue it
        for (int child : tree[p.first]) {
            if (!vis[child]) {
                dis[child] = dis[p.first] + 1;
                qu.push({ child, p.first });
            }
        }
    }
}

// Driver code
int main()
{
    // Number of vertices
    int n = 6;

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(2, 4);
    addEdge(2, 5);

    // Calling modified bfs function
    bfs(0);

    int q[] = { 2, 4 };

    for (int i = 0; i < 2; i++) {
        cout << dis[q[i]] << '\n';
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for
// the above approach
import java.util.*;

class GFG
{
static int sz = (int) 1e5;

// Adjacency list representation
// of the tree
static Vector<Integer> []tree = new Vector[sz + 1];

// Boolean array to mark all the
// vertices which are visited
static boolean []vis = new boolean[sz + 1];

// Array of vector where ith index
// stores the path from the root
// node to the ith node
static int []dis = new int[sz + 1];

static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to create an
// edge between two vertices
static void addEdge(int a, int b)
{

    // Add a to b's list
    tree[a].add(b);

    // Add b to a's list
    tree[b].add(a);
}

// Modified Breadth-First Function
static void bfs(int node)
{
    // Create a queue of {child, parent}
    Queue<pair> qu = new LinkedList<>();

    // Push root node in the front of
    qu.add(new pair(node, 0 ));
    dis[0] = 0;

    while (!qu.isEmpty())
    {
        pair p = qu.peek();

        // Dequeue a vertex from queue
        qu.remove();
        vis[p.first] = true;

        // Get all adjacent vertices of the dequeued
        // vertex s. If any adjacent has not
        // been visited then enqueue it
        for (int child : tree[p.first])
        {
            if (!vis[child])
            {
                dis[child] = dis[p.first] + 1;
                qu.add(new pair(child, p.first));
            }
        }
    }
}

// Driver code
public static void main(String[] args)
{

    // Number of vertices
    int n = 6;
    for (int i = 0; i < sz + 1; i++)
        tree[i] = new Vector<Integer>();

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(2, 4);
    addEdge(2, 5);

    // Calling modified bfs function
    bfs(0);

    int q[] = { 2, 3 };

    for (int i = 0; i < 2; i++)
    {
        System.out.println(dis[q[i]]);
    }
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation for
# the above approach

from collections import deque

sz = int(1e5)

# Adjacency list representation
# of the tree
tree = [0] * (sz + 1)
for i in range(sz + 1):
    tree[i] = []

# Boolean array to mark all the
# vertices which are visited
vis = [False] * (sz + 1)

# Array of vector where ith index
# stores the path from the root
# node to the ith node
dis = [0] * sz

# Function to create an
# edge between two vertices
def addEdge(a: int, b: int):
    global tree

    # Add a to b's list
    tree[a].append(b)

    # Add b to a's list
    tree[b].append(a)

# Modified Breadth-First Function
def bfs(node: int):
    global dis, vis

    # Create a queue of {child, parent}
    qu = deque()

    # Push root node in the front of
    qu.append((node, 0))
    dis[0] = 0

    while qu:
        p = qu[0]

        # Dequeue a vertex from queue
        qu.popleft()
        vis[p[0]] = True

        # Get all adjacent vertices of the dequeued
        # vertex s. If any adjacent has not
        # been visited then enqueue it
        for child in tree[p[0]]:
            if not vis[child]:
                dis[child] = dis[p[0]] + 1
                qu.append((child, p[0]))

# Driver Code
if __name__ == "__main__":

    # Number of vertices
    n = 6

    addEdge(0, 1)
    addEdge(0, 2)
    addEdge(1, 3)
    addEdge(2, 4)
    addEdge(2, 5)

    # Calling modified bfs function
    bfs(0)

    q = [2, 4]

    for i in range(2):
        print(dis[q[i]])

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation for
// the above approach
using System;
using System.Collections.Generic;

class GFG
{
static int sz = (int) 1e5;

// Adjacency list representation
// of the tree
static List<int> []tree = new List<int>[sz + 1];

// Boolean array to mark all the
// vertices which are visited
static Boolean []vis = new Boolean[sz + 1];

// Array of vector where ith index
// stores the path from the root
// node to the ith node
static int []dis = new int[sz + 1];

public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to create an
// edge between two vertices
static void addEdge(int a, int b)
{

    // Add a to b's list
    tree[a].Add(b);

    // Add b to a's list
    tree[b].Add(a);
}

// Modified Breadth-First Function
static void bfs(int node)
{
    // Create a queue of {child, parent}
    Queue<pair> qu = new Queue<pair>();

    // Push root node in the front of
    qu.Enqueue(new pair(node, 0 ));
    dis[0] = 0;

    while (qu.Count != 0)
    {
        pair p = qu.Peek();

        // Dequeue a vertex from queue
        qu.Dequeue();
        vis[p.first] = true;

        // Get all adjacent vertices of the dequeued
        // vertex s. If any adjacent has not
        // been visited then enqueue it
        foreach (int child in tree[p.first])
        {
            if (!vis[child])
            {
                dis[child] = dis[p.first] + 1;
                qu.Enqueue(new pair(child, p.first));
            }
        }
    }
}

// Driver code
public static void Main(String[] args)
{

    // Number of vertices
    for (int i = 0; i < sz + 1; i++)
        tree[i] = new List<int>();

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(2, 4);
    addEdge(2, 5);

    // Calling modified bfs function
    bfs(0);

    int []q = { 2, 3 };

    for (int i = 0; i < 2; i++)
    {
        Console.WriteLine(dis[q[i]]);
    }
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript implementation for the above approach

    let sz = 1e5;

    // Adjacency list representation
    // of the tree
    let tree = new Array(sz + 1);

    // Boolean array to mark all the
    // vertices which are visited
    let vis = new Array(sz + 1);

    // Array of vector where ith index
    // stores the path from the root
    // node to the ith node
    let dis = new Array(sz + 1);

    // Function to create an
    // edge between two vertices
    function addEdge(a, b)
    {

        // Add a to b's list
        tree[a].push(b);

        // Add b to a's list
        tree[b].push(a);
    }

    // Modified Breadth-First Function
    function bfs(node)
    {
        // Create a queue of {child, parent}
        let qu = [];

        // Push root node in the front of
        qu.push([node, 0]);
        dis[0] = 0;

        while (qu.length > 0)
        {
            let p = qu[0];

            // Dequeue a vertex from queue
            qu.shift();
            vis[p[0]] = true;

            // Get all adjacent vertices of the dequeued
            // vertex s. If any adjacent has not
            // been visited then enqueue it
            for (let child = 0; child < tree[p[0]].length; child++)
            {
                if (!vis[tree[p[0]][child]])
                {
                    dis[tree[p[0]][child]] = dis[p[0]] + 1;
                    qu.push([tree[p[0]][child], p[0]]);
                }
            }
        }
    }

    // Number of vertices
    let n = 6;
    for (let i = 0; i < sz + 1; i++)
        tree[i] = [];

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(2, 4);
    addEdge(2, 5);

    // Calling modified bfs function
    bfs(0);

    let q = [ 2, 3 ];

    for (let i = 0; i < 2; i++)
    {
        document.write(dis[q[i]] + "</br>");
    }

</script>
```

**Output:** 

```
1
2
```