# 从一个图中找到一组最多 N/2 个节点，使得所有剩余的节点都直接连接到所选节点之一

> 原文:[https://www . geesforgeks . org/find-一组最多 n-2 个节点-从一个图中-这样-所有剩余的节点-直接连接到一个选择的节点/](https://www.geeksforgeeks.org/find-a-set-of-at-most-n-2-nodes-from-a-graph-such-that-all-remaining-nodes-are-directly-connected-to-one-of-the-chosen-nodes/)

给定一个整数 **N** ，表示无向图中存在的节点的数量，每个节点的值从 **1** 到 **N，**和一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **边【】【】**表示由一条边连接的一对顶点，任务是找到一组至多 **N/2** 个节点，使得不存在于该组中的节点与任意一个节点相邻的[相连](https://www.geeksforgeeks.org/strongly-connected-components/)

**示例:**

> ***输入:** N = 4，Edges[][2] = {{2，3}，{1，3}，{4，2}，{1，2}}*
> ***输出:** 3 2*
> ***解释:**上图中指定的连接如下:*
> *1*
> */\*
> *2–3*
> 
> ***输入:** N = 5，边[][2] = {{2，1}、{3，1}、{3，2}、{4，1}、{4，2}、{4，3}、{5，1}、{5，2}、{5，3}、{5，4}}*
> ***输出:** 1*

**方法:**给定的问题可以基于以下观察来解决:

*   假设一个节点是**源**节点，那么每个顶点到**源**节点的距离将是[奇数或偶数](https://www.geeksforgeeks.org/3-ways-check-number-odd-even-without-using-modulus-operator-set-2-can-merge-httpswww-geeksforgeeks-orgcheck-whether-given-number-even-odd/)。
*   根据奇偶校验将节点分成两个不同的集合，其中至少一个集合的大小不会超过 **N/2** 。由于某些奇偶校验的每个节点都连接到至少一个相反奇偶校验的节点，因此满足选择**最多 N/2 个**节点的标准。

按照以下步骤解决问题:

*   假设任意顶点为**源**节点。
*   初始化两个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)，比如**偶校验**和**偶校验**，分别存储距离源节点的**偶**和**奇**距离的节点。
*   对给定的图执行 [BFS 遍历](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)，根据顶点与**源**的距离的奇偶性，将顶点分成两个不同的集合:
    *   如果每个连接的节点到**源**节点的距离为**奇数，**则[将当前节点插入集合](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/) **奇偶校验**中。
    *   如果每个连接节点到**源**节点的距离为**偶数，**则[将当前节点插入集合](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/) **偶数**中。
*   完成上述步骤后，[以最小尺寸打印集合](https://www.geeksforgeeks.org/print-the-element-at-a-given-index-in-a-set-in-cpp/)的元素。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to add an edge
// to the adjacency list
void addEdge(vector<vector<int> >& adj,
             int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// Function to perform BFS
// traversal on a given graph
vector<vector<int> > BFS(
    int N, int source,
    vector<vector<int> > adjlist)
{
    // Stores the distance of each
    // node from the source node
    int dist[N + 1];

    vector<vector<int> > vertex_set;

    // Update the distance of all
    // vertices from source as -1
    memset(dist, -1, sizeof dist);

    // Assign two separate vectors
    // for parity odd and even parities
    vertex_set.assign(2, vector<int>(0));

    // Perform BFS Traversal
    queue<int> Q;

    // Push the source node
    Q.push(source);
    dist = 0;

    // Iterate until queue becomes empty
    while (!Q.empty()) {

        // Get the front node
        // present in the queue
        int u = Q.front();
        Q.pop();

        // Push the node into vertex_set
        vertex_set[dist[u] % 2].push_back(u);

        // Check if the adjacent
        // vertices are visited
        for (int i = 0;
             i < (int)adjlist[u].size(); i++) {

            // Adjacent node
            int v = adjlist[u][i];

            // If the node v is unvisited
            if (dist[v] == -1) {

                // Update the distance
                dist[v] = dist[u] + 1;

                // Enqueue the node v
                Q.push(v);
            }
        }
    }

    // Return the possible set of nodes
    return vertex_set;
}

// Function to find a set of vertices
// of at most N/2 nodes such that each
// unchosen node is connected adjacently
// to one of the nodes in the set
void findSet(int N,
             vector<vector<int> > adjlist)
{
    // Source vertex
    int source = 1;

    // Store the vertex set
    vector<vector<int> > vertex_set
        = BFS(N, source, adjlist);

    // Stores the index
    // with minimum size
    int in = 0;

    if (vertex_set[1].size()
        < vertex_set[0].size())
        in = 1;

    // Print the nodes present in the set
    for (int node : vertex_set[in]) {
        cout << node << " ";
    }
}

// Driver Code
int main()
{
    int N = 5;
    int M = 8;
    vector<vector<int> > adjlist;
    adjlist.assign(N + 1, vector<int>(0));

    // Graph Formation
    addEdge(adjlist, 2, 5);
    addEdge(adjlist, 2, 1);
    addEdge(adjlist, 5, 1);
    addEdge(adjlist, 4, 5);
    addEdge(adjlist, 1, 4);
    addEdge(adjlist, 2, 4);
    addEdge(adjlist, 3, 4);
    addEdge(adjlist, 3, 5);

    // Function Call to print the
    // set of at most N / 2 nodes
    findSet(N, adjlist);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import deque

# Function to add an edge
# to the adjacency list
def addEdge(adj, u, v):
    adj[u].append(v)
    adj[v].append(u)
    return adj

# Function to perform BFS
# traversal on a given graph
def BFS(N, source, adjlist):

    # Stores the distance of each
    # node from the source node
    dist = [-1]*(N + 1)
    vertex_set = [[] for i in range(2)]

    # Perform BFS Traversal
    Q = deque()

    # Push the source node
    Q.append(source)
    dist = 0

    # Iterate until queue becomes empty
    while len(Q) > 0:

        # Get the front node
        # present in the queue
        u = Q.popleft()

        # Push the node into vertex_set
        vertex_set[dist[u] % 2].append(u)

        # Check if the adjacent
        # vertices are visited
        for i in range(len(adjlist[u])):

            # Adjacent node
            v = adjlist[u][i]

            # If the node v is unvisited
            if (dist[v] == -1):

                # Update the distance
                dist[v] = dist[u] + 1

                # Enqueue the node v
                Q.append(v)

    # Return the possible set of nodes
    return vertex_set

# Function to find a set of vertices
# of at most N/2 nodes such that each
# unchosen node is connected adjacently
# to one of the nodes in the set
def findSet(N, adjlist):

    # Source vertex
    source = 1

    # Store the vertex set
    vertex_set = BFS(N, source, adjlist)

    # Stores the index
    # with minimum size
    inn = 0

    if (len(vertex_set[1]) < len(vertex_set[0])):
        inn = 1

    # Print the nodes present in the set
    for node in vertex_set[inn]:
        print(node, end=" ")

# Driver Code
if __name__ == '__main__':
    N = 5
    M = 8
    adjlist = [[] for i in range(N+1)]

    # Graph Formation
    adjlist = addEdge(adjlist, 2, 5)
    adjlist = addEdge(adjlist, 2, 1)
    adjlist = addEdge(adjlist, 5, 1)
    adjlist = addEdge(adjlist, 4, 5)
    adjlist = addEdge(adjlist, 1, 4)
    adjlist = addEdge(adjlist, 2, 4)
    adjlist = addEdge(adjlist, 3, 4)
    adjlist = addEdge(adjlist, 3, 5)

    # Function Call to print the
    # set of at most N / 2 nodes
    findSet(N, adjlist)

# This code is contributed by mohit kumar 29.
```

**Output:** 

```
1 3
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(N + M)*