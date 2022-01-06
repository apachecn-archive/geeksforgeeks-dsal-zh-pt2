# 最大团问题|递归解

> 原文:[https://www . geesforgeks . org/maximum-clique-problem-recursive-solution/](https://www.geeksforgeeks.org/maximal-clique-problem-recursive-solution/)

给定一个有 **N** 节点和 **E** 边的小图，任务是在给定的图中找到最大**团**。团是给定图的完全子图。这意味着所述子图中的所有节点彼此直接相连，或者在子图中的任意两个节点之间存在边。最大团是给定图的包含最大节点数的完全子图。
**举例:**

> **输入:** N = 4，边[][] = {{1，2}，{2，3}，{3，1}，{4，3}，{4，1}，{4，2}}
> **输出:** 4
> **输入:** N = 5，边[][] = {{1，2}，{2，3}，{3，1}，{4，3}，{4，5}，{5，3}}

****方法:**思路是用递归来解决问题。** 

*   **当一条边被添加到当前列表中时，检查通过将该边添加到当前列表中，它是否仍然形成团。**
*   **顶点被添加，直到列表没有形成团。然后，该列表被回溯以找到形成小团体的更大的子集。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;

// Stores the vertices
int store[MAX], n;

// Graph
int graph[MAX][MAX];

// Degree of the vertices
int d[MAX];

// Function to check if the given set of
// vertices in store array is a clique or not
bool is_clique(int b)
{

    // Run a loop for all set of edges
    for (int i = 1; i < b; i++) {
        for (int j = i + 1; j < b; j++)

            // If any edge is missing
            if (graph[store[i]][store[j]] == 0)
                return false;
    }
    return true;
}

// Function to find all the sizes
// of maximal cliques
int maxCliques(int i, int l)
{
    // Maximal clique size
    int max_ = 0;

    // Check if any vertices from i+1
    // can be inserted
    for (int j = i + 1; j <= n; j++) {

        // Add the vertex to store
        store[l] = j;

        // If the graph is not a clique of size k then
        // it cannot be a clique by adding another edge
        if (is_clique(l + 1)) {

            // Update max
            max_ = max(max_, l);

            // Check if another edge can be added
            max_ = max(max_, maxCliques(j, l + 1));
        }
    }
    return max_;
}

// Driver code
int main()
{
    int edges[][2] = { { 1, 2 }, { 2, 3 }, { 3, 1 },
                       { 4, 3 }, { 4, 1 }, { 4, 2 } };
    int size = sizeof(edges) / sizeof(edges[0]);
    n = 4;

    for (int i = 0; i < size; i++) {
        graph[edges[i][0]][edges[i][1]] = 1;
        graph[edges[i][1]][edges[i][0]] = 1;
        d[edges[i][0]]++;
        d[edges[i][1]]++;
    }

    cout << maxCliques(0, 1);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int MAX = 100, n;

// Stores the vertices
static int []store = new int[MAX];

// Graph
static int [][]graph = new int[MAX][MAX];

// Degree of the vertices
static int []d = new int[MAX];

// Function to check if the given set of
// vertices in store array is a clique or not
static boolean is_clique(int b)
{

    // Run a loop for all set of edges
    for (int i = 1; i < b; i++)
    {
        for (int j = i + 1; j < b; j++)

            // If any edge is missing
            if (graph[store[i]][store[j]] == 0)
                return false;
    }
    return true;
}

// Function to find all the sizes
// of maximal cliques
static int maxCliques(int i, int l)
{
    // Maximal clique size
    int max_ = 0;

    // Check if any vertices from i+1
    // can be inserted
    for (int j = i + 1; j <= n; j++)
    {

        // Add the vertex to store
        store[l] = j;

        // If the graph is not a clique of size k then
        // it cannot be a clique by adding another edge
        if (is_clique(l + 1))
        {

            // Update max
            max_ = Math.max(max_, l);

            // Check if another edge can be added
            max_ = Math.max(max_, maxCliques(j, l + 1));
        }
    }
    return max_;
}

// Driver code
public static void main(String[] args)
{
    int [][]edges = { { 1, 2 }, { 2, 3 }, { 3, 1 },
                    { 4, 3 }, { 4, 1 }, { 4, 2 } };
    int size = edges.length;
    n = 4;

    for (int i = 0; i < size; i++)
    {
        graph[edges[i][0]][edges[i][1]] = 1;
        graph[edges[i][1]][edges[i][0]] = 1;
        d[edges[i][0]]++;
        d[edges[i][1]]++;
    }
    System.out.print(maxCliques(0, 1));
}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 implementation of the approach
MAX = 100;
n = 0;

# Stores the vertices
store = [0] * MAX;

# Graph
graph = [[0 for i in range(MAX)] for j in range(MAX)];

# Degree of the vertices
d = [0] * MAX;

# Function to check if the given set of
# vertices in store array is a clique or not
def is_clique(b):

    # Run a loop for all set of edges
    for i in range(1, b):
        for j in range(i + 1, b):

            # If any edge is missing
            if (graph[store[i]][store[j]] == 0):
                return False;

    return True;

# Function to find all the sizes
# of maximal cliques
def maxCliques(i, l):

    # Maximal clique size
    max_ = 0;

    # Check if any vertices from i+1
    # can be inserted
    for j in range(i + 1, n + 1):

        # Add the vertex to store
        store[l] = j;

        # If the graph is not a clique of size k then
        # it cannot be a clique by adding another edge
        if (is_clique(l + 1)):

            # Update max
            max_ = max(max_, l);

            # Check if another edge can be added
            max_ = max(max_, maxCliques(j, l + 1));

    return max_;

# Driver code
if __name__ == '__main__':
    edges = [[ 1, 2 ],[ 2, 3 ],[ 3, 1 ],
           [ 4, 3 ],[ 4, 1 ],[ 4, 2 ]];
    size = len(edges);
    n = 4;

    for i in range(size):
        graph[edges[i][0]][edges[i][1]] = 1;
        graph[edges[i][1]][edges[i][0]] = 1;
        d[edges[i][0]] += 1;
        d[edges[i][1]] += 1;

    print(maxCliques(0, 1));

# This code is contributed by PrinciRaj1992
```

## **C#**

```
// C# implementation of the approach
using System;

class GFG
{

static int MAX = 100, n;

// Stores the vertices
static int []store = new int[MAX];

// Graph
static int [,]graph = new int[MAX,MAX];

// Degree of the vertices
static int []d = new int[MAX];

// Function to check if the given set of
// vertices in store array is a clique or not
static bool is_clique(int b)
{

    // Run a loop for all set of edges
    for (int i = 1; i < b; i++)
    {
        for (int j = i + 1; j < b; j++)

            // If any edge is missing
            if (graph[store[i],store[j]] == 0)
                return false;
    }
    return true;
}

// Function to find all the sizes
// of maximal cliques
static int maxCliques(int i, int l)
{
    // Maximal clique size
    int max_ = 0;

    // Check if any vertices from i+1
    // can be inserted
    for (int j = i + 1; j <= n; j++)
    {

        // Add the vertex to store
        store[l] = j;

        // If the graph is not a clique of size k then
        // it cannot be a clique by adding another edge
        if (is_clique(l + 1))
        {

            // Update max
            max_ = Math.Max(max_, l);

            // Check if another edge can be added
            max_ = Math.Max(max_, maxCliques(j, l + 1));
        }
    }
    return max_;
}

// Driver code
public static void Main(String[] args)
{
    int [,]edges = { { 1, 2 }, { 2, 3 }, { 3, 1 },
                    { 4, 3 }, { 4, 1 }, { 4, 2 } };
    int size = edges.GetLength(0);
    n = 4;

    for (int i = 0; i < size; i++)
    {
        graph[edges[i, 0], edges[i, 1]] = 1;
        graph[edges[i, 1], edges[i, 0]] = 1;
        d[edges[i, 0]]++;
        d[edges[i, 1]]++;
    }
    Console.Write(maxCliques(0, 1));
}
}

// This code is contributed by PrinciRaj1992
```

## **java 描述语言**

```
<script>
    // Javascript implementation of the approach

    let MAX = 100, n;

    // Stores the vertices
    let store = new Array(MAX);
    store.fill(0);

    // Graph
    let graph = new Array(MAX);
    for(let i = 0; i < MAX; i++)
    {
        graph[i] = new Array(MAX);
        for(let j = 0; j < MAX; j++)
        {
            graph[i][j] = 0;
        }
    }

    // Degree of the vertices
    let d = new Array(MAX);
    d.fill(0);

    // Function to check if the given set of
    // vertices in store array is a clique or not
    function is_clique(b)
    {

        // Run a loop for all set of edges
        for (let i = 1; i < b; i++)
        {
            for (let j = i + 1; j < b; j++)

                // If any edge is missing
                if (graph[store[i]][store[j]] == 0)
                    return false;
        }
        return true;
    }

    // Function to find all the sizes
    // of maximal cliques
    function maxCliques(i, l)
    {
        // Maximal clique size
        let max_ = 0;

        // Check if any vertices from i+1
        // can be inserted
        for (let j = i + 1; j <= n; j++)
        {

            // Add the vertex to store
            store[l] = j;

            // If the graph is not a clique of size k then
            // it cannot be a clique by adding another edge
            if (is_clique(l + 1))
            {

                // Update max
                max_ = Math.max(max_, l);

                // Check if another edge can be added
                max_ = Math.max(max_, maxCliques(j, l + 1));
            }
        }
        return max_;
    }

    let edges = [ [ 1, 2 ], [ 2, 3 ], [ 3, 1 ],
                    [ 4, 3 ], [ 4, 1 ], [ 4, 2 ] ];
    let size = edges.length;
    n = 4;

    for (let i = 0; i < size; i++)
    {
        graph[edges[i][0]][edges[i][1]] = 1;
        graph[edges[i][1]][edges[i][0]] = 1;
        d[edges[i][0]]++;
        d[edges[i][1]]++;
    }
    document.write(maxCliques(0, 1));

// This code is contributed by suresh07.
</script>
```

****Output:** 

```
4
```**