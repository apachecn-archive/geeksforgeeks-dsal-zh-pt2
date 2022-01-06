# 使用拓扑排序检测有向图中的循环

> 原文:[https://www . geesforgeks . org/detect-cycle-in-directed-graph-use-topology-sort/](https://www.geeksforgeeks.org/detect-cycle-in-directed-graph-using-topological-sort/)

给定一个由 **N** 顶点和 **M** 边组成的**有向图**和一组**边【】【】**，任务是使用[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)检查该图是否包含循环。

> 有向图的拓扑排序是其顶点的线性排序，使得对于从顶点 **U** 到顶点 **V** 的每个**有向边 U - > V** ，在排序中 **U 在 V** 之前。

**示例:**

> **输入** : N = 4，M = 6，边[][] = {{0，1}，{1，2}，{2，0}，{0，2}，{2，3}，{3，3}}
> **输出:**是
> **说明:**
> 给定图形中存在一个循环 **0 - > 2 - > 0**
> 
> **输入:** N = 4，M = 3，边[][] = {{0，1}，{1，2}，{2，3}，{0，2}}
> **输出:**否

**方法:**
在**拓扑排序**中，思路是先访问**父节点**，再访问**子节点**。如果给定的图包含一个**循环**，那么至少有一个**节点**既是父节点又是子节点，因此这将打破**拓扑顺序**。因此**拓扑排序**后，检查每个**有向边**是否遵循顺序。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// n -> is number of edges in graph
// m -> is number of node in graph
int   n, m ;

// Stack to store the
// visited vertices in
// the Topological Sort
stack<int> s;

// Store Topological Order
vector<int> tsort;

// Adjacency list to store edges
vector<int> adj[int(1e5) + 1];

// To ensure visited vertex
vector<int> visited(int(1e5) + 1);

// Function to perform DFS
void dfs(int u)
{
    // Set the vertex as visited
    visited[u] = 1;

    for (auto it : adj[u]) {

        // Visit connected vertices
        if (visited[it] == 0)
            dfs(it);
    }

    // Push into the stack on
    // complete visit of vertex
    s.push(u);
}

// Function to check and return
// if a cycle exists or not
bool check_cycle()
{
    // Stores the position of
    // vertex in topological order
    unordered_map<int, int> pos;
    int index = 0;

    // Pop all elements from stack
    while (!s.empty()) {
        pos[s.top()] = index;

        // Push element to get
        // Topological Order
        tsort.push_back(s.top());

        index += 1;

        // Pop from the stack
        s.pop();
    }

    for (int i = 0; i < n; i++) {
        for (auto it : adj[i]) {

            // If parent vertex
            // does not appear first
            if (pos[i] > pos[it]) {

                // Cycle exists
                return true;
            }
        }
    }

    // Return false if cycle
    // does not exist
    return false;
}

// Function to add edges
// from u -> v
void addEdge(int u, int v)
{
    adj[u].push_back(v);
}

// Driver Code
int main()
{
    n = 4, m = 5;

    // Insert edges
    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 2);
    addEdge(2, 0);
    addEdge(2, 3);

    for (int i = 0; i < n; i++) {
        if (visited[i] == 0) {
            dfs(i);
        }
    }

    // If cycle exist
    if (check_cycle())
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static int t, n, m, a;

// Stack to store the
// visited vertices in
// the Topological Sort
static Stack<Integer> s;

// Store Topological Order
static ArrayList<Integer> tsort;

// Adjacency list to store edges
static ArrayList<ArrayList<Integer>> adj;

// To ensure visited vertex
static int[] visited = new int[(int)1e5 + 1];

// Function to perform DFS
static void dfs(int u)
{

    // Set the vertex as visited
    visited[u] = 1;

    for(Integer it : adj.get(u))
    {

        // Visit connected vertices
        if (visited[it] == 0)
            dfs(it);
    }

    // Push into the stack on
    // complete visit of vertex
    s.push(u);
}

// Function to check and return
// if a cycle exists or not
static boolean check_cycle()
{

    // Stores the position of
    // vertex in topological order
    Map<Integer, Integer> pos = new HashMap<>();

    int ind = 0;

    // Pop all elements from stack
    while (!s.isEmpty())
    {
        pos.put(s.peek(), ind);

        // Push element to get
        // Topological Order
        tsort.add(s.peek());

        ind += 1;

        // Pop from the stack
        s.pop();
    }

    for(int i = 0; i < n; i++)
    {
        for(Integer it : adj.get(i))
        {

            // If parent vertex
            // does not appear first
            if (pos.get(i) > pos.get(it))
            {

                // Cycle exists
                return true;
            }
        }
    }

    // Return false if cycle
    // does not exist
    return false;
}

// Function to add edges
// from u to v
static void addEdge(int u, int v)
{
    adj.get(u).add(v);
}

// Driver code   
public static void main (String[] args)
{
    n = 4; m = 5;

    s = new Stack<>();
    adj = new ArrayList<>();
    tsort = new ArrayList<>();

    for(int i = 0; i < 4; i++)
        adj.add(new ArrayList<>());

    // Insert edges
    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 2);
    addEdge(2, 0);
    addEdge(2, 3);

    for(int i = 0; i < n; i++)
    {
        if (visited[i] == 0)
        {
            dfs(i);
        }
    }

    // If cycle exist
    if (check_cycle())
       System.out.println("Yes");
    else
       System.out.println("No");
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
t = 0
n = 0
m = 0
a = 0

# Stack to store the
# visited vertices in
# the Topological Sort
s = []

# Store Topological Order
tsort = []

# Adjacency list to store edges
adj = [[] for i in range(100001)]

# To ensure visited vertex
visited = [False for i in range(100001)]

# Function to perform DFS
def dfs(u):

    # Set the vertex as visited
    visited[u] = 1

    for it in adj[u]:

        # Visit connected vertices
        if (visited[it] == 0):
            dfs(it)

    # Push into the stack on
    # complete visit of vertex
    s.append(u)

# Function to check and return
# if a cycle exists or not
def check_cycle():

    # Stores the position of
    # vertex in topological order
    pos = dict()

    ind = 0

    # Pop all elements from stack
    while (len(s) != 0):
        pos[s[-1]] = ind

        # Push element to get
        # Topological Order
        tsort.append(s[-1])

        ind += 1

        # Pop from the stack
        s.pop()

    for i in range(n):
        for it in adj[i]:
            first = 0 if i not in pos else pos[i]
            second = 0 if it not in pos else pos[it]

            # If parent vertex
            # does not appear first
            if (first > second):

                # Cycle exists
                return True

    # Return false if cycle
    # does not exist
    return False

# Function to add edges
# from u to v
def addEdge(u, v):

    adj[u].append(v)

# Driver Code
if __name__ == "__main__":

    n = 4
    m = 5

    # Insert edges
    addEdge(0, 1)
    addEdge(0, 2)
    addEdge(1, 2)
    addEdge(2, 0)
    addEdge(2, 3)

    for i in range(n):
        if (visited[i] == False):
            dfs(i)

    # If cycle exist
    if (check_cycle()):
        print('Yes')
    else:
        print('No')

# This code is contributed by rutvik_56
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

static int n;

// Stack to store the
// visited vertices in
// the Topological Sort
static Stack<int> s;

// Store Topological Order
static ArrayList tsort;

// Adjacency list to store edges
static ArrayList adj;

// To ensure visited vertex
static int[] visited = new int[100001];

// Function to perform DFS
static void dfs(int u)
{

    // Set the vertex as visited
    visited[u] = 1;

    foreach(int it in (ArrayList)adj[u])
    {

        // Visit connected vertices
        if (visited[it] == 0)
            dfs(it);
    }

    // Push into the stack on
    // complete visit of vertex
    s.Push(u);
}

// Function to check and return
// if a cycle exists or not
static bool check_cycle()
{

    // Stores the position of
    // vertex in topological order
    Dictionary<int,
               int> pos = new Dictionary<int,
                                         int>();

    int ind = 0;

    // Pop all elements from stack
    while (s.Count != 0)
    {
        pos.Add(s.Peek(), ind);

        // Push element to get
        // Topological Order
        tsort.Add(s.Peek());

        ind += 1;

        // Pop from the stack
        s.Pop();
    }

    for(int i = 0; i < n; i++)
    {
        foreach(int it in (ArrayList)adj[i])
        {

            // If parent vertex
            // does not appear first
            if (pos[i] > pos[it])
            {

                // Cycle exists
                return true;
            }
        }
    }

    // Return false if cycle
    // does not exist
    return false;
}

// Function to add edges
// from u to v
static void addEdge(int u, int v)
{
    ((ArrayList)adj[u]).Add(v);
}

// Driver code   
public static void Main(string[] args)
{
    n = 4;

    s = new Stack<int>();
    adj = new ArrayList();
    tsort = new ArrayList();

    for(int i = 0; i < 4; i++)
        adj.Add(new ArrayList());

    // Insert edges
    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 2);
    addEdge(2, 0);
    addEdge(2, 3);

    for(int i = 0; i < n; i++)
    {
        if (visited[i] == 0)
        {
            dfs(i);
        }
    }

    // If cycle exist
    if (check_cycle())
       Console.WriteLine("Yes");
    else
       Console.WriteLine("No");
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

var t, n, m, a;

// Stack to store the
// visited vertices in
// the Topological Sort
var s = [];

// Store Topological Order
var tsort = [];

// Adjacency list to store edges
var adj = Array.from(Array(100001), ()=>Array());

// To ensure visited vertex
var visited = Array(100001).fill(0);

//( Function to perform )DFS
function dfs(u)
{
    // Set the vertex as visited
    visited[u] = 1;

    adj[u].forEach(it => {

        // Visit connected vertices
        if (visited[it] == 0)
            dfs(it);
    });

    // Push into the stack on
    // complete visit of vertex
    s.push(u);
}

// Function to check and return
// if a cycle exists or not
function check_cycle()
{
    // Stores the position of
    // vertex in topological order
    var pos = new Map();
    var ind = 0;

    // Pop all elements from stack
    while (s.length!=0) {
        pos.set(s[s.length-1], ind);

        // Push element to get
        // Topological Order
        tsort.push(s[s.length-1]);

        ind += 1;

        // Pop from the stack
        s.pop();
    }
    var ans = false;
    for (var i = 0; i < n; i++) {
        adj[i].forEach(it => {

            // If parent vertex
            // does not appear first
            if ((pos.has(i)?pos.get(i):0) >
            (pos.has(it)?pos.get(it):0))
            {

                // Cycle exists
                ans = true;
            }
        });
    };

    // Return false if cycle
    // does not exist
    return ans;
}

// Function to add edges
// from u to v
function addEdge(u, v)
{
    adj[u].push(v);
}

// Driver Code

n = 4, m = 5;

// Insert edges
addEdge(0, 1);
addEdge(0, 2);
addEdge(1, 2);
addEdge(2, 0);
addEdge(2, 3);
for (var i = 0; i < n; i++) {
    if (visited[i] == 0) {
        dfs(i);
    }
}
// If cycle exist
if (check_cycle())
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(N)*