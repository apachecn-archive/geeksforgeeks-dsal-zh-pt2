# 为满足给定条件而添加到图形中的最小边数

> 原文:[https://www . geeksforgeeks . org/满足给定条件的图的最小添加边数/](https://www.geeksforgeeks.org/minimum-number-of-edges-to-be-added-to-a-graph-to-satisfy-the-given-condition/)

给定一个由从 **0** 到**N–1**和 **M** 条成对 **{a，b}** 的边组成的**图**，任务是找到要添加到图中的最小边数，以便如果存在从任何节点 **a** 到节点 **b** 的路径， 那么也应该有从节点 **a** 到节点**【a+1，a + 2，a + 3，…，b–1】**的路径。

**示例:**

> **输入:** N = 7，M = 3，Edges[][] = {{1，5}，{2，4}，{3，4}}
> **输出:** 1
> **说明:**
> 有一条从 1 到 5 的路径。所以应该有从 1 到 2，3 和 4 的路径。
> 添加一条边{1，2}就足以到达图的其他两个节点。
> 
> **输入:** N = 8，M = 3 边[][] = {{1，2}，{2，3}，{3，4 } }
> T3】输出: 0

**方法:**
想法是使用[不相交集合或联合寻找](https://www.geeksforgeeks.org/union-find/)。不相交集合中的每个组件都应该有连续的节点。这可以通过维护*最大 _ 节点[]* 和*最小 _ 节点[]* 数组来分别存储每个组件中节点的最大值和最小值来实现。按照以下步骤解决问题:

*   为不相交集合并集创建一个结构。
*   将**答案**初始化为 0，遍历图中所有节点，得到当前节点的分量。
*   如果组件是**未访问的**，那么将其标记为已访问。
*   现在，从该组件的最小值迭代到最大值，检查节点是否与当前节点在同一个组件中，并将它们组合成一个组件，并将**答案**增加 *1* 。
*   最后打印**答案**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
#define MOD 1000000007

#define int long long int
using namespace std;

// Disjoint Set Union
struct dsu {

    // Stores the parent
    // of each node
    vector<int> parent;

    // Storing maximum value
    // in each component
    vector<int> maximum_node;

    // Stores the minimum value
    // in each component
    vector<int> minimum_node;

    // Stores the visited nodes
    vector<int> visited;

    // Function to initialize the
    // values in vectors
    void init(int n)
    {
        // Initialize the size of
        // vectors as n
        parent.resize(n);
        maximum_node.resize(n);
        minimum_node.resize(n);
        visited.resize(n);

        for (int i = 0; i < n; i++) {

            // Initially every component
            // has only one node
            parent[i] = i;
            maximum_node[i] = i;
            minimum_node[i] = i;

            // Mark unvisited
            visited[i] = 0;
        }
    }

    // Function to get identifier node
    // (superparent) for each component
    int getsuperparent(int x)
    {

        // If parent of a node is that
        // node itself then the node is
        // superparent of that component
        return x == parent[x]
                   ? x
                   : parent[x]
                     = getsuperparent(parent[x]);
    }

    // Function to perform union of two
    // different components
    void unite(int x, int y)
    {

        int superparent_x = getsuperparent(x);
        int superparent_y = getsuperparent(y);

        // Set superparent of y as the
        // parent of superparent of x
        parent[superparent_x] = superparent_y;

        // Update the maximum node
        // in the component containing y
        maximum_node[superparent_y]
            = max(maximum_node[superparent_y],
                  maximum_node[superparent_x]);

        // Update the minimum node
        // in the component containing y
        minimum_node[superparent_y]
            = min(minimum_node[superparent_y],
                  minimum_node[superparent_x]);
    }
} G;

// Function to find the minimum number
// of edges to be added to the Graph
int minimumEdgesToBeAdded(int n)
{
    // Stores the answer
    int answer = 0;

    // Iterate over all nodes
    for (int i = 0; i < n; i++) {

        // Get the superparent of
        // the current node
        int temp = G.getsuperparent(i);

        // If the node is not visited
        if (!G.visited[temp]) {

            // Set the node as visited
            G.visited[temp] = 1;

            // Iterate from the minimum
            // value to maximum value in
            // the current component
            for (int j = G.minimum_node[temp];
                 j <= G.maximum_node[temp]; j++) {

                // If the nodes are in
                // different components
                if (G.getsuperparent(j)
                    != G.getsuperparent(i)) {

                    // Unite them
                    G.unite(i, j);

                    // Increment the answer
                    answer++;
                }
            }
        }
    }

    // Return the answer
    return answer;
}

// Driver Code
int32_t main()
{
    int N = 7, M = 3;

    G.init(N);

    // Insert edges
    G.unite(1, 5);
    G.unite(2, 4);
    G.unite(3, 4);

    cout << minimumEdgesToBeAdded(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static final int MOD = 1000000007;

// Disjoint Set Union
static class dsu
{
    public dsu(){}

    // Stores the parent
    // of each node
    int[] parent;

    // Storing maximum value
    // in each component
    int[] maximum_node;

    // Stores the minimum value
    // in each component
    int[] minimum_node;

    // Stores the visited nodes
    int[] visited;

    // Function to initialize the
    // values in vectors
    void init(int n)
    {

        // Initialize the size of
        // vectors as n
        parent = new int[n];
        maximum_node = new int[n];
        minimum_node = new int[n];
        visited = new int[n];

        for(int i = 0; i < n; i++)
        {

            // Initially every component
            // has only one node
            parent[i] = i;
            maximum_node[i] = i;
            minimum_node[i] = i;

            // Mark unvisited
            visited[i] = 0;
        }
    }

    // Function to get identifier node
    // (superparent) for each component
    int getsuperparent(int x)
    {

        // If parent of a node is that
        // node itself then the node is
        // superparent of that component
        if(x == parent[x])
            return x;
        else
        {
            parent[x] = getsuperparent(parent[x]);
            return parent[x];
        }
    }

    // Function to perform union of two
    // different components
    void unite(int x, int y)
    {
        int superparent_x = getsuperparent(x);
        int superparent_y = getsuperparent(y);

        // Set superparent of y as the
        // parent of superparent of x
        parent[superparent_x] = superparent_y;

        // Update the maximum node
        // in the component containing y
        maximum_node[superparent_y] = Math.max(
        maximum_node[superparent_y],
        maximum_node[superparent_x]);

        // Update the minimum node
        // in the component containing y
        minimum_node[superparent_y] = Math.min(
        minimum_node[superparent_y],
        minimum_node[superparent_x]);
    }
};

static dsu G = new dsu();

// Function to find the minimum number
// of edges to be added to the Graph
static int minimumEdgesToBeAdded(int n)
{

    // Stores the answer
    int answer = 0;

    // Iterate over all nodes
    for(int i = 0; i < n; i++)
    {

        // Get the superparent of
        // the current node
        int temp = G.getsuperparent(i);

        // If the node is not visited
        if (G.visited[temp] == 0)
        {

            // Set the node as visited
            G.visited[temp] = 1;

            // Iterate from the minimum
            // value to maximum value in
            // the current component
            for(int j = G.minimum_node[temp];
                   j <= G.maximum_node[temp]; j++)
            {

                // If the nodes are in
                // different components
                if (G.getsuperparent(j) !=
                    G.getsuperparent(i))
                {

                    // Unite them
                    G.unite(i, j);

                    // Increment the answer
                    answer++;
                }
            }
        }
    }

    // Return the answer
    return answer;
}

// Driver Code
public static void main(String[] args)
{
    int N = 7;

    G.init(N);

    // Insert edges
    G.unite(1, 5);
    G.unite(2, 4);
    G.unite(3, 4);

    System.out.print(minimumEdgesToBeAdded(N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
MOD = 1000000007

# Disjoint Set Union
class dsu:

    # Function to initialize the
    # values in vectors
    def __init__(self, n: int) -> None:

        # Stores the parent
        # of each node
        self.parent = [i for i in range(n)]

        # Storing maximum value
        # in each component
        self.maximum_node = [i for i in range(n)]

        # Stores the minimum value
        # in each component
        self.minimum_node = [i for i in range(n)]

        # Stores the visited nodes
        self.visited = [0] * n

    # Function to get identifier node
    # (superparent) for each component
    def getsuperparent(self, x: int) -> int:

        # If parent of a node is that
        # node itself then the node is
        # superparent of that component
        if x == self.parent[x]:
            return x
        else:
            self.parent[x] = self.getsuperparent(
                self.parent[x])
            return self.parent[x]

    # Function to perform union of two
    # different components
    def unite(self, x: int, y: int) -> None:

        superparent_x = self.getsuperparent(x)
        superparent_y = self.getsuperparent(y)

        # Set superparent of y as the
        # parent of superparent of x
        self.parent[superparent_x] = superparent_y

        # Update the maximum node
        # in the component containing y
        self.maximum_node[superparent_y] = max(
            self.maximum_node[superparent_y],
            self.maximum_node[superparent_x])

        # Update the minimum node
        # in the component containing y
        self.minimum_node[superparent_y] = min(
            self.minimum_node[superparent_y],
            self.minimum_node[superparent_x])

# Function to find the minimum number
# of edges to be added to the Graph
def minimumEdgesToBeAdded(n: int) -> int:

    global G

    # Stores the answer
    answer = 0

    # Iterate over all nodes
    for i in range(n):

        # Get the superparent of
        # the current node
        temp = G.getsuperparent(i)

        # If the node is not visited
        if (not G.visited[temp]):

            # Set the node as visited
            G.visited[temp] = 1

            # Iterate from the minimum
            # value to maximum value in
            # the current component
            for j in range(G.minimum_node[temp],
                           G.maximum_node[temp] + 1):

                # If the nodes are in
                # different components
                if (G.getsuperparent(j) !=
                    G.getsuperparent(i)):

                    # Unite them
                    G.unite(i, j)

                    # Increment the answer
                    answer += 1

    # Return the answer
    return answer

# Driver Code
if __name__ == "__main__":

    N = 7
    M = 3

    G = dsu(N)

    # Insert edges
    G.unite(1, 5)
    G.unite(2, 4)
    G.unite(3, 4)

    print(minimumEdgesToBeAdded(N))

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

//static readonly int MOD = 1000000007;

// Disjoint Set Union
class dsu
{
    public dsu(){}

    // Stores the parent
    // of each node
    public int[] parent;

    // Storing maximum value
    // in each component
    public int[] maximum_node;

    // Stores the minimum value
    // in each component
    public int[] minimum_node;

    // Stores the visited nodes
    public int[] visited;

    // Function to initialize the
    // values in vectors
    public void init(int n)
    {

        // Initialize the size of
        // vectors as n
        parent = new int[n];
        maximum_node = new int[n];
        minimum_node = new int[n];
        visited = new int[n];

        for(int i = 0; i < n; i++)
        {

            // Initially every component
            // has only one node
            parent[i] = i;
            maximum_node[i] = i;
            minimum_node[i] = i;

            // Mark unvisited
            visited[i] = 0;
        }
    }

    // Function to get identifier node
    // (superparent) for each component
    public int getsuperparent(int x)
    {

        // If parent of a node is that
        // node itself then the node is
        // superparent of that component
        if(x == parent[x])
            return x;
        else
        {
            parent[x] = getsuperparent(parent[x]);
            return parent[x];
        }
    }

    // Function to perform union of two
    // different components
    public void unite(int x, int y)
    {
        int superparent_x = getsuperparent(x);
        int superparent_y = getsuperparent(y);

        // Set superparent of y as the
        // parent of superparent of x
        parent[superparent_x] = superparent_y;

        // Update the maximum node
        // in the component containing y
        maximum_node[superparent_y] = Math.Max(
        maximum_node[superparent_y],
        maximum_node[superparent_x]);

        // Update the minimum node
        // in the component containing y
        minimum_node[superparent_y] = Math.Min(
        minimum_node[superparent_y],
        minimum_node[superparent_x]);
    }
};

static dsu G = new dsu();

// Function to find the minimum number
// of edges to be added to the Graph
static int minimumEdgesToBeAdded(int n)
{

    // Stores the answer
    int answer = 0;

    // Iterate over all nodes
    for(int i = 0; i < n; i++)
    {

        // Get the superparent of
        // the current node
        int temp = G.getsuperparent(i);

        // If the node is not visited
        if (G.visited[temp] == 0)
        {

            // Set the node as visited
            G.visited[temp] = 1;

            // Iterate from the minimum
            // value to maximum value in
            // the current component
            for(int j = G.minimum_node[temp];
                   j <= G.maximum_node[temp]; j++)
            {

                // If the nodes are in
                // different components
                if (G.getsuperparent(j) !=
                    G.getsuperparent(i))
                {

                    // Unite them
                    G.unite(i, j);

                    // Increment the answer
                    answer++;
                }
            }
        }
    }

    // Return the answer
    return answer;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 7;

    G.init(N);

    // Insert edges
    G.unite(1, 5);
    G.unite(2, 4);
    G.unite(3, 4);

    Console.Write(minimumEdgesToBeAdded(N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

var MOD = 1000000007;

// Stores the parent
// of each node
var parent = [];
// Storing maximum value
// in each component
var maximum_node = [];
// Stores the minimum value
// in each component
var minimum_node = [];
// Stores the visited nodes
var visited = [];
// Function to initialize the
// values in vectors
function init(n)
{

    // Initialize the size of
    // vectors as n
    parent = Array(n);
    maximum_node = Array(n);
    minimum_node = Array(n);
    visited = Array(n);
    for(var i = 0; i < n; i++)
    {

        // Initially every component
        // has only one node
        parent[i] = i;
        maximum_node[i] = i;
        minimum_node[i] = i;
        // Mark unvisited
        visited[i] = 0;
    }
}
// Function to get identifier node
// (superparent) for each component
function getsuperparent(x)
{
    // If parent of a node is that
    // node itself then the node is
    // superparent of that component
    if(x == parent[x])
        return x;
    else
    {
        parent[x] = getsuperparent(parent[x]);
        return parent[x];
    }
}
// Function to perform union of two
// different components
function unite(x, y)
{
    var superparent_x = getsuperparent(x);
    var superparent_y = getsuperparent(y);
    // Set superparent of y as the
    // parent of superparent of x
    parent[superparent_x] = superparent_y;
    // Update the maximum node
    // in the component containing y
    maximum_node[superparent_y] = Math.max(
        maximum_node[superparent_y],
        maximum_node[superparent_x]);
    // Update the minimum node
    // in the component containing y
    minimum_node[superparent_y] = Math.min(
        minimum_node[superparent_y],
        minimum_node[superparent_x]);
}

// Function to find the minimum number
// of edges to be added to the Graph
function minimumEdgesToBeAdded(n)
{

    // Stores the answer
    var answer = 0;

    // Iterate over all nodes
    for(var i = 0; i < n; i++)
    {

        // Get the superparent of
        // the current node
        var temp = getsuperparent(i);

        // If the node is not visited
        if (visited[temp] == 0)
        {

            // Set the node as visited
            visited[temp] = 1;

            // Iterate from the minimum
            // value to maximum value in
            // the current component
            for(var j = minimum_node[temp];
                   j <= maximum_node[temp]; j++)
            {

                // If the nodes are in
                // different components
                if (getsuperparent(j) !=
                    getsuperparent(i))
                {

                    // Unite them
                    unite(i, j);

                    // Increment the answer
                    answer++;
                }
            }
        }
    }

    // Return the answer
    return answer;
}

// Driver Code
var N = 7;
init(N);
// Insert edges
unite(1, 5);
unite(2, 4);
unite(3, 4);
document.write(minimumEdgesToBeAdded(N));

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N)，其中 N 为图中节点数。*
***辅助空间:** O(N)*