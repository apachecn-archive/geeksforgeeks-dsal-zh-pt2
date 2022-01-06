# 有向无环图中的最长路径|集合 2

> 原文:[https://www . geesforgeks . org/最长路径-有向-无环-图-集-2/](https://www.geeksforgeeks.org/longest-path-directed-acyclic-graph-set-2/)

给定一个加权有向无环图和其中的一个源顶点，求从源顶点到给定图中所有其他顶点的最长距离。

我们已经讨论了如何在集合 1 中找到有向无环图中的最长路径。在这篇文章中，我们将讨论另一个有趣的解决方案来寻找 DAG 的最长路径，该方案使用算法来寻找 DAG 中的[最短路径。
思路是**对路径的权重求反，在图**中找到最短路径。加权图 G 中两个给定顶点 s 和 t 之间的最长路径与图 G’中的最短路径是一样的，图 G’是通过将每一个权重变为其否定而从 G 中得到的。因此，如果最短路径可以在 G '中找到，那么最长路径也可以在 G 中找到。
下面是寻找最长路径的分步过程–](https://www.geeksforgeeks.org/shortest-path-for-directed-acyclic-graphs/)

我们将给定图的每条边的权重改为它的否定，并将到所有顶点的距离初始化为无穷大，到源的距离初始化为 0，然后我们找到表示图的线性排序的图的拓扑排序。当我们按照拓扑顺序考虑一个顶点 u 时，保证我们已经考虑了它的每一条引入边。也就是说，我们已经找到了到该顶点的最短路径，我们可以使用该信息来更新其所有相邻顶点的较短路径。一旦我们有了拓扑顺序，我们就按照拓扑顺序逐一处理所有顶点。对于每个正在处理的顶点，我们使用当前顶点到源顶点的最短距离及其边权重来更新其相邻顶点的距离。即

```
for every adjacent vertex v of every vertex u in topological order
    if (dist[v] > dist[u] + weight(u, v))
    dist[v] = dist[u] + weight(u, v)
```

一旦我们找到了从源顶点开始的所有最短路径，最长路径将只是最短路径的否定。

下面是上述方法的实现:

## C++

```
// A C++ program to find single source longest distances
// in a DAG
#include <bits/stdc++.h>
using namespace std;

// Graph is represented using adjacency list. Every node of
// adjacency list contains vertex number of the vertex to
// which edge connects. It also contains weight of the edge
class AdjListNode
{
    int v;
    int weight;
public:
    AdjListNode(int _v, int _w)
    {
        v = _v;
        weight = _w;
    }
    int getV()
    {
        return v;
    }
    int getWeight()
    {
        return weight;
    }
};

// Graph class represents a directed graph using adjacency
// list representation
class Graph
{
    int V; // No. of vertices

    // Pointer to an array containing adjacency lists
    list<AdjListNode>* adj;

    // This function uses DFS
    void longestPathUtil(int, vector<bool> &, stack<int> &);
public:
    Graph(int); // Constructor
    ~Graph();   // Destructor

    // function to add an edge to graph
    void addEdge(int, int, int);

    void longestPath(int);
};

Graph::Graph(int V) // Constructor
{
    this->V = V;
    adj = new list<AdjListNode>[V];
}

Graph::~Graph() // Destructor
{
    delete[] adj;
}

void Graph::addEdge(int u, int v, int weight)
{
    AdjListNode node(v, weight);
    adj[u].push_back(node); // Add v to u's list
}

// A recursive function used by longestPath. See below
// link for details.
// https://www.geeksforgeeks.org/topological-sorting/
void Graph::longestPathUtil(int v, vector<bool> &visited,
                            stack<int> &Stack)
{
    // Mark the current node as visited
    visited[v] = true;

    // Recur for all the vertices adjacent to this vertex
    for (AdjListNode node : adj[v])
    {
        if (!visited[node.getV()])
            longestPathUtil(node.getV(), visited, Stack);
    }

    // Push current vertex to stack which stores topological
    // sort
    Stack.push(v);
}

// The function do Topological Sort and finds longest
// distances from given source vertex
void Graph::longestPath(int s)
{
    // Initialize distances to all vertices as infinite and
    // distance to source as 0
    int dist[V];
    for (int i = 0; i < V; i++)
        dist[i] = INT_MAX;
    dist[s] = 0;

    stack<int> Stack;

    // Mark all the vertices as not visited
    vector<bool> visited(V, false);

    for (int i = 0; i < V; i++)
        if (visited[i] == false)
            longestPathUtil(i, visited, Stack);

    // Process vertices in topological order
    while (!Stack.empty())
    {
        // Get the next vertex from topological order
        int u = Stack.top();
        Stack.pop();

        if (dist[u] != INT_MAX)
        {
            // Update distances of all adjacent vertices
            // (edge from u -> v exists)
            for (AdjListNode v : adj[u])
            {
                // consider negative weight of edges and
                // find shortest path
                if (dist[v.getV()] > dist[u] + v.getWeight() * -1)
                    dist[v.getV()] = dist[u] + v.getWeight() * -1;
            }
        }
    }

    // Print the calculated longest distances
    for (int i = 0; i < V; i++)
    {
        if (dist[i] == INT_MAX)
            cout << "INT_MIN ";
        else
            cout << (dist[i] * -1) << " ";
    }
}

// Driver code
int main()
{
    Graph g(6);

    g.addEdge(0, 1, 5);
    g.addEdge(0, 2, 3);
    g.addEdge(1, 3, 6);
    g.addEdge(1, 2, 2);
    g.addEdge(2, 4, 4);
    g.addEdge(2, 5, 2);
    g.addEdge(2, 3, 7);
    g.addEdge(3, 5, 1);
    g.addEdge(3, 4, -1);
    g.addEdge(4, 5, -2);

    int s = 1;

    cout << "Following are longest distances from "
         << "source vertex " << s << " \n";
    g.longestPath(s);

    return 0;
}
```

## 蟒蛇 3

```
# A Python3 program to find single source
# longest distances in a DAG
import sys

def addEdge(u, v, w):

    global adj
    adj[u].append([v, w])

# A recursive function used by longestPath.
# See below link for details.
# https:#www.geeksforgeeks.org/topological-sorting/
def longestPathUtil(v):

    global visited, adj,Stack
    visited[v] = 1

    # Recur for all the vertices adjacent
    # to this vertex
    for node in adj[v]:
        if (not visited[node[0]]):
            longestPathUtil(node[0])

    # Push current vertex to stack which
    # stores topological sort
    Stack.append(v)

# The function do Topological Sort and finds
# longest distances from given source vertex
def longestPath(s):

    # Initialize distances to all vertices
    # as infinite and
    global visited, Stack, adj,V
    dist = [sys.maxsize for i in range(V)]
    # for (i = 0 i < V i++)
    #     dist[i] = INT_MAX
    dist[s] = 0

    for i in range(V):
        if (visited[i] == 0):
            longestPathUtil(i)

    # print(Stack)
    while (len(Stack) > 0):

        # Get the next vertex from topological order
        u = Stack[-1]
        del Stack[-1]

        if (dist[u] != sys.maxsize):

            # Update distances of all adjacent vertices
            # (edge from u -> v exists)
            for v in adj[u]:

                # Consider negative weight of edges and
                # find shortest path
                if (dist[v[0]] > dist[u] + v[1] * -1):
                    dist[v[0]] = dist[u] + v[1] * -1

    # Print the calculated longest distances
    for i in range(V):
        if (dist[i] == sys.maxsize):
            print("INT_MIN ", end = " ")
        else:
            print(dist[i] * (-1), end = " ")

# Driver code
if __name__ == '__main__':

    V = 6
    visited = [0 for i in range(7)]
    Stack = []
    adj = [[] for i in range(7)]

    addEdge(0, 1, 5)
    addEdge(0, 2, 3)
    addEdge(1, 3, 6)
    addEdge(1, 2, 2)
    addEdge(2, 4, 4)
    addEdge(2, 5, 2)
    addEdge(2, 3, 7)
    addEdge(3, 5, 1)
    addEdge(3, 4, -1)
    addEdge(4, 5, -2)

    s = 1

    print("Following are longest distances from source vertex", s)

    longestPath(s)

# This code is contributed by mohit kumar 29
```

**输出:**

```
Following are longest distances from source vertex 1 
INT_MIN 0 2 9 8 10 
```

**时间复杂度**:拓扑排序的时间复杂度为 O(V + E)。在找到拓扑顺序后，该算法处理所有顶点，对于每个顶点，它对所有相邻的顶点运行一个循环。由于图中相邻顶点的总数为 0(E)，因此内循环运行 0(V+E)次。因此，该算法的整体时间复杂度为 O(V + E)。

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。