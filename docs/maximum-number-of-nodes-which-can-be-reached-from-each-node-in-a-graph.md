# 图中每个节点可达到的最大节点数。

> 原文:[https://www . geeksforgeeks . org/图中每个节点可到达的最大节点数/](https://www.geeksforgeeks.org/maximum-number-of-nodes-which-can-be-reached-from-each-node-in-a-graph/)

给定一个有 N 个节点和 K 条双向边的图，找出可以从某个特定节点到达的节点数。如果我们可以使用任意数量的边从 X 开始到 Y 结束，那么两个节点 X 和 Y 被称为是可达的。

**注意:一个节点可以自己到达。**

```
Input : N = 7
       1            5
        \          / \
         2        6 __ 7
          \  
           3
            \
             4

Output :4 4 4 4 3 3 3 
From node 1 ,nodes {1,2,3,4} can be visited
hence the answer is equal to 4
From node 5,nodes {5,6,7} can be visited.
hence the answer is equal to 3.
Similarly, print the count for every node.

Input : N = 8
      1              7
    /   \             \
   2     3              8   
    \   / \
      5    6
Output :6 6 6 6 6 6 2 2
```

**方法:**
要找到从特定节点可到达的节点数量，需要观察的一件事是，只有当节点 X 到节点 Y 处于同一连接组件中时，我们才能从节点 X 到达节点 Y。
由于图形是双向的，因此连接组件中的任何节点都可以连接到相同连接组件中的任何其他节点。因此，对于特定的节点，可到达的节点数将是该特定组件中的节点数。使用深度优先搜索来找到答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
vector<vector<int>> graph;

// Function to perform the DFS calculating the
// count of the elements in a connected component
void dfs(int curr, int& cnt, vector<int>& 
             visited, vector<int>& duringdfs)
{
    visited[curr] = 1;

    // Number of nodes in this component
    ++cnt;

    // Stores the nodes which belong
    // to current component
    duringdfs.push_back(curr);
    for (auto& child : graph[curr]) {

        // If the child is not visited
        if (visited[child] == 0) {
            dfs(child, cnt, visited, duringdfs);
        }
    }
}

// Function to return the desired
// count for every node in the graph
void MaximumVisit(int n, int k)
{
    // To keep track of nodes we visit
    vector<int> visited(n+1,0);

      // No of connected elements for each node  
      vector<int> ans(n+1);

    vector<int> duringdfs;
    for (int i = 1; i <= n; ++i) {
        duringdfs.clear();
        int cnt = 0;

        // If a node is not visited, perform a DFS as
        // this node belongs to a different component
        // which is not yet visited
        if (visited[i] == 0) {
            cnt = 0;
            dfs(i, cnt, visited, duringdfs);
        }

        // Now store the count of all the visited
        // nodes for any particular component.
        for (auto& x : duringdfs) {
            ans[x] = cnt;
        }
    }

    // Print the result
    for (int i = 1; i <= n; ++i) {
        cout << ans[i] << " ";
    }
    cout << endl;
    return;
}

// Function to build the graph
void MakeGraph(){
    graph[1].push_back(2);
    graph[2].push_back(1);
    graph[2].push_back(3);
    graph[3].push_back(2);
    graph[3].push_back(4);
    graph[4].push_back(3);
    graph[5].push_back(6);
    graph[6].push_back(5);
    graph[6].push_back(7);
    graph[7].push_back(6);
    graph[5].push_back(7);
    graph[7].push_back(5);
}

// Driver code
int main()
{
    int N = 7, K = 6;

      graph.resize(N+1);
    // Build the graph
    MakeGraph();

    MaximumVisit(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
import java.util.*;

class GFG
{

    static final int maxx = 100005;
    @SuppressWarnings("unchecked")
    static Vector<Integer>[] graph = new Vector[maxx];
    static Vector<Integer> duringdfs = new Vector<>();
    static int cnt = 0;

    // Function to perform the DFS calculating the
    // count of the elements in a connected component
    static void dfs(int curr, int[] visited)
    {
        visited[curr] = 1;

        // Number of nodes in this component
        ++cnt;

        // Stores the nodes which belong
        // to current component
        duringdfs.add(curr);
        for (int child : graph[curr])
        {

            // If the child is not visited
            if (visited[child] == 0)
                dfs(child, visited);
        }
    }

    // Function to return the desired
    // count for every node in the graph
    static void maximumVisit(int n, int k)
    {

        // To keep track of nodes we visit
        int[] visited = new int[maxx];

        // Mark every node unvisited
        Arrays.fill(visited, 0);

        int[] ans = new int[maxx];

        // No of connected elements for each node
        Arrays.fill(ans, 0);

        for (int i = 1; i <= n; i++)
        {
            duringdfs.clear();

            // If a node is not visited, perform a DFS as
            // this node belongs to a different component
            // which is not yet visited
            if (visited[i] == 0)
            {
                cnt = 0;
                dfs(i, visited);
            }

            // Now store the count of all the visited
            // nodes for any particular component.
            for (int x : duringdfs)
                ans[x] = cnt;
        }

        // Print the result
        for (int i = 1; i <= n; i++)
            System.out.print(ans[i] + " ");
        System.out.println();
        return;
    }

    // Function to build the graph
    static void makeGraph()
    {
        // Initializing graph
        for (int i = 0; i < maxx; i++)
            graph[i] = new Vector<>();

        graph[1].add(2);
        graph[2].add(1);
        graph[2].add(3);
        graph[3].add(2);
        graph[3].add(4);
        graph[4].add(3);
        graph[5].add(6);
        graph[6].add(5);
        graph[6].add(7);
        graph[7].add(6);
        graph[5].add(7);
        graph[7].add(5);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 7, K = 6;

        // Build the graph
        makeGraph();

        maximumVisit(N, K);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
maxx = 100005
graph = [[] for i in range(maxx)]

# Function to perform the DFS calculating the 
# count of the elements in a connected component
def dfs(curr, cnt, visited, duringdfs):

    visited[curr] = 1

    # Number of nodes in this component
    cnt += 1

    # Stores the nodes which belong 
    # to current component
    duringdfs.append(curr)

    for child in graph[curr]:

        # If the child is not visited
        if (visited[child] == 0):
            cnt, duringdfs = dfs(child, cnt,
                                 visited, duringdfs)

    return cnt, duringdfs

# Function to return the desired 
# count for every node in the graph
def MaximumVisit(n, k):

    # To keep track of nodes we visit
    visited = [0 for i in range(maxx)]

    ans = [0 for i in range(maxx)]

    duringdfs = []

    for i in range(1, n + 1):
        duringdfs.clear()

        cnt = 0

        # If a node is not visited, perform a DFS as 
        # this node belongs to a different component
        # which is not yet visited
        if (visited[i] == 0):
            cnt = 0
            cnt, duringdfs = dfs(i, cnt,
                                 visited, duringdfs)

        # Now store the count of all the visited
        # nodes for any particular component.
        for x in duringdfs:
            ans[x] = cnt

    # Print the result
    for i in range(1, n + 1):
        print(ans[i], end = ' ')

    print()

    return

# Function to build the graph
def MakeGraph():

    graph[1].append(2)
    graph[2].append(1)
    graph[2].append(3)
    graph[3].append(2)
    graph[3].append(4)
    graph[4].append(3)
    graph[5].append(6)
    graph[6].append(5)
    graph[6].append(7)
    graph[7].append(6)
    graph[5].append(7)
    graph[7].append(5)

# Driver code
if __name__=='__main__':

    N = 7
    K = 6

    # Build the graph
    MakeGraph()

    MaximumVisit(N, K)

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;

class GFG{

static int maxx = 100005;

static ArrayList[] graph = new ArrayList[maxx];
static ArrayList duringdfs = new ArrayList();
static int cnt = 0;

// Function to perform the DFS calculating the
// count of the elements in a connected component
static void dfs(int curr, int[] visited)
{
    visited[curr] = 1;

    // Number of nodes in this component
    ++cnt;

    // Stores the nodes which belong
    // to current component
    duringdfs.Add(curr);

    foreach(int child in graph[curr])
    {

        // If the child is not visited
        if (visited[child] == 0)
            dfs(child, visited);
    }
}

// Function to return the desired
// count for every node in the graph
static void maximumVisit(int n, int k)
{

    // To keep track of nodes we visit
    int[] visited = new int[maxx];

    // Mark every node unvisited
    Array.Fill(visited, 0);

    int[] ans = new int[maxx];

    // No of connected elements for each node
    Array.Fill(ans, 0);

    for(int i = 1; i <= n; i++)
    {
        duringdfs.Clear();

        // If a node is not visited, perform
        // a DFS as this node belongs to a
        // different component which is not
        // yet visited
        if (visited[i] == 0)
        {
            cnt = 0;
            dfs(i, visited);
        }

        // Now store the count of all the visited
        // nodes for any particular component.
        foreach(int x in duringdfs)
            ans[x] = cnt;
    }

    // Print the result
    for(int i = 1; i <= n; i++)
        Console.Write(ans[i] + " ");

    Console.WriteLine();
    return;
}

// Function to build the graph
static void makeGraph()
{

    // Initializing graph
    for(int i = 0; i < maxx; i++)
        graph[i] = new ArrayList();

    graph[1].Add(2);
    graph[2].Add(1);
    graph[2].Add(3);
    graph[3].Add(2);
    graph[3].Add(4);
    graph[4].Add(3);
    graph[5].Add(6);
    graph[6].Add(5);
    graph[6].Add(7);
    graph[7].Add(6);
    graph[5].Add(7);
    graph[7].Add(5);
}

// Driver Code
public static void Main(string[] args)
{
    int N = 7, K = 6;

    // Build the graph
    makeGraph();

    maximumVisit(N, K);
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    let maxx = 100005;

    let graph = new Array(maxx);
    for(let i = 0; i < maxx; i++)
    {
        graph[i] = [];
    }
    let duringdfs = [];
    let cnt = 0;

    // Function to perform the DFS calculating the
    // count of the elements in a connected component
    function dfs(curr, visited)
    {
        visited[curr] = 1;

        // Number of nodes in this component
        ++cnt;

        // Stores the nodes which belong
        // to current component
        duringdfs.push(curr);

        for(let child = 0; child < graph[curr].length; child++)
        {

            // If the child is not visited
            if (visited[graph[curr][child]] == 0)
                dfs(graph[curr][child], visited);
        }
    }

    // Function to return the desired
    // count for every node in the graph
    function maximumVisit(n, k)
    {

        // To keep track of nodes we visit
        let visited = new Array(maxx);

        // Mark every node unvisited
        visited.fill(0);

        let ans = new Array(maxx);

        // No of connected elements for each node
        ans.fill(0);

        for(let i = 1; i <= n; i++)
        {
            duringdfs = [];

            // If a node is not visited, perform
            // a DFS as this node belongs to a
            // different component which is not
            // yet visited
            if (visited[i] == 0)
            {
                cnt = 0;
                dfs(i, visited);
            }

            // Now store the count of all the visited
            // nodes for any particular component.
            for(let x = 0; x < duringdfs.length; x++)
                ans[duringdfs[x]] = cnt;
        }

        // Print the result
        for(let i = 1; i <= n; i++)
            document.write(ans[i] + " ");

        document.write("</br>");
        return;
    }

    // Function to build the graph
    function makeGraph()
    {

        // Initializing graph
        for(let i = 0; i < maxx; i++)
            graph[i] = [];

        graph[1].push(2);
        graph[2].push(1);
        graph[2].push(3);
        graph[3].push(2);
        graph[3].push(4);
        graph[4].push(3);
        graph[5].push(6);
        graph[6].push(5);
        graph[6].push(7);
        graph[7].push(6);
        graph[5].push(7);
        graph[7].push(5);
    }

    let N = 7, K = 6;

    // Build the graph
    makeGraph();

    maximumVisit(N, K);

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
4 4 4 4 3 3 3
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)