# 最大化从根顶点和彩色顶点沿路径出现的未着色顶点的数量

> 原文:[https://www . geesforgeks . org/最大化从根顶点到彩色顶点的路径上出现的未着色顶点数/](https://www.geeksforgeeks.org/maximize-the-number-of-uncolored-vertices-appearing-along-the-path-from-root-vertex-and-the-colored-vertices/)

给定一棵树，其 **N** 个顶点编号为 1 到 N，顶点 **1 作为根**顶点，**N–1**条边。我们必须精确地着色 **k** 个顶点，并且**计算根顶点和每个着色顶点之间未着色的顶点的数量**。如果根顶点没有着色，我们必须把它包括在计数中。最大化从根顶点到彩色顶点的路径之间的未着色顶点数的任务。

**示例:**

```
Input :

           1
         / |  \
       /   |    \
     2     3      4
          / \      \
         /   \      \
        5     6      7

k = 4 
Output : 7
Explanation:
If we color vertex 2, 5, 6 and 7, 
the number of uncolored vertices between the path
from root to colored vertices is maximum which is 7.

Input :

          1
         / \
        /   \
       2     3
      /
     /
    4

k = 1
Output : 2

```

**方法:**
为了解决上述问题，我们观察到，如果一个顶点被选择为未着色，那么它的父顶点必须被选择为未着色。然后我们可以计算，如果我们选择一条特定的路径到达彩色顶点，我们会得到多少未着色的顶点。只需计算根到每个顶点之间的顶点数与当前顶点下方出现的顶点数之差。取所有差值中最大的 k，计算总和。使用第 n 个元素 stl 得到一个 O(n)解。

下面是上述方法的实现:

## C++

```
// C++ program to Maximize the number
// of uncolored vertices occurring between
// the path from root vertex and the colored vertices
#include <bits/stdc++.h>
using namespace std;

// Comparator function
bool cmp(int a, int b)
{
    return a > b;
}

class graph
{
    vector<vector<int> > g;
    vector<int> depth;
    vector<int> subtree;
    int* diff;

public:
    // Constructor
    graph(int n)
    {
        g = vector<vector<int> >(n + 1);

        depth = vector<int>(n + 1);

        subtree = vector<int>(n + 1);

        diff = new int[n + 1];
    }

    // Function to push edges
    void push(int a, int b)
    {
        g[a].push_back(b);

        g[b].push_back(a);
    }

    // function for dfs traversal
    int dfs(int v, int p)
    {

        // Store depth of vertices
        depth[v] = depth[p] + 1;

        subtree[v] = 1;

        for (auto i : g[v]) {
            if (i == p)
                continue;

            // Calculate number of vertices
            // in subtree of all vertices
            subtree[v] += dfs(i, v);
        }

        // Computing the difference
        diff[v] = depth[v] - subtree[v];

        return subtree[v];
    }

    // Function that print maximum number of
    // uncolored vertices occur between root vertex
    // and all colored vertices
    void solution(int n, int k)
    {

        // Computing first k largest difference
        nth_element(diff + 1, diff + k, diff + n + 1, cmp);

        int sum = 0;

        for (int i = 1; i <= k; i++) {
            sum += diff[i];
        }

        // Print the result
        cout << sum << "\n";
    }
};

// Driver Code
int main()
{

    int N = 7;
    int k = 4;

    // initialise graph
    graph g(N);

    g.push(1, 2);
    g.push(1, 3);
    g.push(1, 4);
    g.push(3, 5);
    g.push(3, 6);
    g.push(4, 7);

    g.dfs(1, 0);

    g.solution(N, k);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to Maximize the number
# of uncolored vertices occurring between
# the path from root vertex and the colored vertices
g = []
depth = []
subtree = []
diff = []

# Constructor
def graph(n):
    global g, depth, subtree, diff
    g = [[] for i in range(n + 1)]
    depth = [0]*(n + 1)
    subtree = [0]*(n + 1)
    diff = [0]*(n + 1)

# Function to push edges
def push(a, b):
    global g
    g[a].append(b)
    g[b].append(a)

# function for dfs traversal
def dfs(v, p):
    global depth, subtree, g, diff

    # Store depth of vertices
    depth[v] = depth[p] + 1
    subtree[v] = 1
    for i in g[v]:
        if (i == p):
            continue

        # Calculate number of vertices
        # in subtree of all vertices
        subtree[v] += dfs(i, v)

    # Computing the difference
    diff[v] = depth[v] - subtree[v]
    return subtree[v]

# Function that prmaximum number of
# uncolored vertices occur between root vertex
# and all colored vertices
def solution(n, k):
    global diff

    # Computing first k largest difference
    diff = sorted(diff)[::-1]

    # nth_element(diff + 1, diff + k, diff + n + 1, cmp)
    sum = 2
    for i in range(1, k + 1):
        sum += diff[i]

    # Print the result
    print (sum)

# Driver Code
if __name__ == '__main__':
    N = 7
    k = 4

    # initialise graph
    graph(N)
    push(1, 2)
    push(1, 3)
    push(1, 4)
    push(3, 5)
    push(3, 6)
    push(4, 7)
    dfs(1, 0)
    solution(N, k)

# This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>
// Javascript program to Maximize the number
// of uncolored vertices occurring between
// the path from root vertex and the colored vertices

let g = [];
let depth = [];
let subtree = [];
let diff = [];

function graph(n)
{
    g = new Array(n + 1);

        depth = Array(n + 1);

        subtree = Array(n + 1);

        diff = new Array(n + 1);

       for(let i = 0; i < (n + 1); i++)
    {
        g[i] = [];
        depth[i] = 0;
        subtree[i] = 0;
        diff[i] = 0;
    }
}

//Function to push edges
function push(a, b)
{
    g[a].push(b);

        g[b].push(a);
}
// function for dfs traversal
function  dfs(v, p)
{
    // Store depth of vertices
        depth[v] = depth[p] + 1;

        subtree[v] = 1;

        for (let i=0;i< g[v].length;i++) {
            if (g[v][i] == p)
                continue;

            // Calculate number of vertices
            // in subtree of all vertices
            subtree[v] += dfs(g[v][i], v);
        }

        // Computing the difference
        diff[v] = depth[v] - subtree[v];

        return subtree[v];
}

// Function that prmaximum number of
// uncolored vertices occur between root vertex
// and all colored vertices
function solution(n, k)
{
    diff.sort(function(a,b){return b-a;});

    let sum = 2,i;
    for(i = 1; i < k + 1; i++)
    {
        sum += diff[i];
    }

    document.write(sum);

}

// Driver Code
let N = 7,
    k = 4;
graph(N)
push(1, 2)
push(1, 3)
push(1, 4)
push(3, 5)
push(3, 6)
push(4, 7)
dfs(1, 0)
solution(N, k)

// This code is contributed by patel2127
</script>
```

**Output:** 

```
7
```

**时间复杂度:** O(N)