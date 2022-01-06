# 查找是否有一条来自源的长度超过 k 的路径

> 原文:[https://www . geeksforgeeks . org/find-if-有一个长度超过 k 的源路径/](https://www.geeksforgeeks.org/find-if-there-is-a-path-of-more-than-k-length-from-a-source/)

给定一个图，图中的一个源顶点和一个数字 k，找出是否有一个简单的路径(没有任何循环)从给定的源开始，到任何其他顶点结束，这样从源到那个顶点的距离至少是' k '长度。

```
Example:
Input  : Source s = 0, k = 58
Output : True
There exists a simple path 0 -> 7 -> 1
-> 2 -> 8 -> 6 -> 5 -> 3 -> 4
Which has a total distance of 60 km which
is more than 58.

Input  : Source s = 0, k = 62
Output : False

In the above graph, the longest simple
path has distance 61 (0 -> 7 -> 1-> 2
 -> 3 -> 4 -> 5-> 6 -> 8, so output 
should be false for any input greater 
than 61.
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
需要注意的一点是，简单地做 BFS 或 DFS 并在每一步选择最长的边是行不通的。原因是，较短的边可以产生较长的路径，因为通过它连接的权重较高的边。
想法是使用回溯。我们从给定的源开始，探索从当前顶点开始的所有路径。我们跟踪当前距离源的距离。如果距离变得大于 k，我们返回 true。如果一条路径产生的距离不超过 k，我们就回溯。
我们如何确保道路是简单的，我们不会循环往复？其思想是跟踪数组中的当前路径顶点。每当我们向路径添加顶点时，我们都会检查它是否已经存在于当前路径中。如果它存在，我们忽略边缘。
以下是上述想法的实现。

## C++

```
// Program to find if there is a simple path with
// weight more than k
#include<bits/stdc++.h>
using namespace std;

// iPair ==>  Integer Pair
typedef pair<int, int> iPair;

// This class represents a dipathted graph using
// adjacency list representation
class Graph
{
    int V;    // No. of vertices

    // In a weighted graph, we need to store vertex
    // and weight pair for every edge
    list< pair<int, int> > *adj;
    bool pathMoreThanKUtil(int src, int k, vector<bool> &path);

public:
    Graph(int V);  // Constructor

    // function to add an edge to graph
    void addEdge(int u, int v, int w);
    bool pathMoreThanK(int src, int k);
};

// Returns true if graph has path more than k length
bool Graph::pathMoreThanK(int src, int k)
{
    // Create a path array with nothing included
    // in path
    vector<bool> path(V, false);

    // Add source vertex to path
    path[src] = 1;

    return pathMoreThanKUtil(src, k, path);
}

// Prints shortest paths from src to all other vertices
bool Graph::pathMoreThanKUtil(int src, int k, vector<bool> &path)
{
    // If k is 0 or negative, return true;
    if (k <= 0)
        return true;

    // Get all adjacent vertices of source vertex src and
    // recursively explore all paths from src.
    list<iPair>::iterator i;
    for (i = adj[src].begin(); i != adj[src].end(); ++i)
    {
        // Get adjacent vertex and weight of edge
        int v = (*i).first;
        int w = (*i).second;

        // If vertex v is already there in path, then
        // there is a cycle (we ignore this edge)
        if (path[v] == true)
            continue;

        // If weight of is more than k, return true
        if (w >= k)
            return true;

        // Else add this vertex to path
        path[v] = true;

        // If this adjacent can provide a path longer
        // than k, return true.
        if (pathMoreThanKUtil(v, k-w, path))
            return true;

        // Backtrack
        path[v] = false;
    }

    // If no adjacent could produce longer path, return
    // false
    return false;
}

// Allocates memory for adjacency list
Graph::Graph(int V)
{
    this->V = V;
    adj = new list<iPair> [V];
}

// Utility function to an edge (u, v) of weight w
void Graph::addEdge(int u, int v, int w)
{
    adj[u].push_back(make_pair(v, w));
    adj[v].push_back(make_pair(u, w));
}

// Driver program to test methods of graph class
int main()
{
    // create the graph given in above fugure
    int V = 9;
    Graph g(V);

    //  making above shown graph
    g.addEdge(0, 1, 4);
    g.addEdge(0, 7, 8);
    g.addEdge(1, 2, 8);
    g.addEdge(1, 7, 11);
    g.addEdge(2, 3, 7);
    g.addEdge(2, 8, 2);
    g.addEdge(2, 5, 4);
    g.addEdge(3, 4, 9);
    g.addEdge(3, 5, 14);
    g.addEdge(4, 5, 10);
    g.addEdge(5, 6, 2);
    g.addEdge(6, 7, 1);
    g.addEdge(6, 8, 6);
    g.addEdge(7, 8, 7);

    int src = 0;
    int k = 62;
    g.pathMoreThanK(src, k)? cout << "Yes\n" :
                             cout << "No\n";

    k = 60;
    g.pathMoreThanK(src, k)? cout << "Yes\n" :
                             cout << "No\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find if there is a simple path with
// weight more than k
import java.util.*;
public class GFG{

  static class AdjListNode {
    int v;
    int weight;

    AdjListNode(int _v, int _w)
    {
      v = _v;
      weight = _w;
    }
    int getV() { return v; }
    int getWeight() { return weight; }
  }

  // This class represents a dipathted graph using
  // adjacency list representation
  static class Graph
  {
    int V; // No. of vertices

    // In a weighted graph, we need to store vertex
    // and weight pair for every edge
    ArrayList<ArrayList<AdjListNode>> adj;

    // Allocates memory for adjacency list
    Graph(int V)
    {
      this.V = V;
      adj = new ArrayList<ArrayList<AdjListNode>>(V);

      for(int i = 0; i < V; i++)
      {
        adj.add(new ArrayList<AdjListNode>());
      }
    }

    // Utility function to an edge (u, v) of weight w
    void addEdge(int u, int v, int weight)
    {
      AdjListNode node1 = new AdjListNode(v, weight);
      adj.get(u).add(node1); // Add v to u's list

      AdjListNode node2 = new AdjListNode(u, weight);
      adj.get(v).add(node2); // Add u to v's list
    }

    // Returns true if graph has path more than k length
    boolean pathMoreThanK(int src, int k)
    {

      // Create a path array with nothing included
      // in path
      boolean path[] = new boolean[V];

      Arrays.fill(path, false);

      // Add source vertex to path
      path[src] = true;

      return pathMoreThanKUtil(src, k, path);
    }

    // Prints shortest paths from src to all other vertices
    boolean pathMoreThanKUtil(int src, int k, boolean[] path)
    { 

      // If k is 0 or negative, return true;
      if (k <= 0)
        return true;

      // Get all adjacent vertices of source vertex src and
      // recursively explore all paths from src.
      ArrayList<AdjListNode> it = adj.get(src);

      int index = 0;
      for(int i = 0; i < adj.get(src).size(); i++)
      {
        AdjListNode vertex = adj.get(src).get(i);

        // Get adjacent vertex and weight of edge
        int v = vertex.v;
        int w = vertex.weight;

        // increase theindex
        index++;

        // If vertex v is already there in path, then
        // there is a cycle (we ignore this edge)
        if (path[v] == true)
          continue;

        // If weight of is more than k, return true
        if (w >= k)
          return true;

        // Else add this vertex to path
        path[v] = true;

        // If this adjacent can provide a path longer
        // than k, return true.
        if (pathMoreThanKUtil(v, k-w, path))
          return true;

        // Backtrack
        path[v] = false;
      }

      // If no adjacent could produce longer path, return
      // false
      return false;
    }

  }

  // Driver program to test methods of graph class
  public static void main(String[] args)
  {

    // create the graph given in above fugure
    int V = 9;
    Graph g = new Graph(V);

    // making above shown graph
    g.addEdge(0, 1, 4);
    g.addEdge(0, 7, 8);
    g.addEdge(1, 2, 8);
    g.addEdge(1, 7, 11);
    g.addEdge(2, 3, 7);
    g.addEdge(2, 8, 2);
    g.addEdge(2, 5, 4);
    g.addEdge(3, 4, 9);
    g.addEdge(3, 5, 14);
    g.addEdge(4, 5, 10);
    g.addEdge(5, 6, 2);
    g.addEdge(6, 7, 1);
    g.addEdge(6, 8, 6);
    g.addEdge(7, 8, 7);

    int src = 0;
    int k = 62;

    if(g.pathMoreThanK(src, k))
      System.out.println("YES");
    else
      System.out.println("NO");

    k = 60;
    if(g.pathMoreThanK(src, k))
      System.out.println("YES");
    else
      System.out.println("NO");

  }
}

// This code is contributed by adityapande88.
```

## 蟒蛇 3

```
# Program to find if there is a simple path with
# weight more than k

# This class represents a dipathted graph using
# adjacency list representation
class Graph:
    # Allocates memory for adjacency list
    def __init__(self, V):
        self.V = V
        self.adj = [[] for i in range(V)]

    # Returns true if graph has path more than k length
    def pathMoreThanK(self,src, k):
        # Create a path array with nothing included
        # in path
        path = [False]*self.V

        # Add source vertex to path
        path[src] = 1

        return self.pathMoreThanKUtil(src, k, path)

    # Prints shortest paths from src to all other vertices
    def pathMoreThanKUtil(self,src, k, path):
        # If k is 0 or negative, return true
        if (k <= 0):
            return True

        # Get all adjacent vertices of source vertex src and
        # recursively explore all paths from src.
        i = 0
        while i != len(self.adj[src]):
            # Get adjacent vertex and weight of edge
            v = self.adj[src][i][0]
            w = self.adj[src][i][1]
            i += 1

            # If vertex v is already there in path, then
            # there is a cycle (we ignore this edge)
            if (path[v] == True):
                continue

            # If weight of is more than k, return true
            if (w >= k):
                return True

            # Else add this vertex to path
            path[v] = True

            # If this adjacent can provide a path longer
            # than k, return true.
            if (self.pathMoreThanKUtil(v, k-w, path)):
                return True

            # Backtrack
            path[v] = False

        # If no adjacent could produce longer path, return
        # false
        return False

    # Utility function to an edge (u, v) of weight w
    def addEdge(self,u, v, w):
        self.adj[u].append([v, w])
        self.adj[v].append([u, w])

# Driver program to test methods of graph class
if __name__ == '__main__':

    # create the graph given in above fugure
    V = 9
    g = Graph(V)

    #  making above shown graph
    g.addEdge(0, 1, 4)
    g.addEdge(0, 7, 8)
    g.addEdge(1, 2, 8)
    g.addEdge(1, 7, 11)
    g.addEdge(2, 3, 7)
    g.addEdge(2, 8, 2)
    g.addEdge(2, 5, 4)
    g.addEdge(3, 4, 9)
    g.addEdge(3, 5, 14)
    g.addEdge(4, 5, 10)
    g.addEdge(5, 6, 2)
    g.addEdge(6, 7, 1)
    g.addEdge(6, 8, 6)
    g.addEdge(7, 8, 7)

    src = 0
    k = 62
    if g.pathMoreThanK(src, k):
        print("Yes")
    else:
        print("No")

    k = 60
    if g.pathMoreThanK(src, k):
        print("Yes")
    else:
        print("No")
```

**输出:**

```
No
Yes
```

**练习:**
修改上面的解，找到给定来源的最长路径的权重。
**时间复杂度:** O(n！)
**说明:**
从源节点开始，我们逐一访问所有路径，检查每条路径的总权重是否大于 k。因此，最糟糕的情况是当可能路径的数量最大时。当每个节点都连接到其他节点时，就是这种情况。
从源节点开始，我们有 n-1 个相邻节点。路径连接任意两个节点所需的时间是 2。一个用于连接源和下一个相邻顶点。一个用于断开源和旧的相邻顶点之间的连接。
从 n-1 个相邻节点中选择一个节点后，剩下 n-2 个相邻节点(因为源节点已经包含在路径中)，以此类推，在选择节点的每一步，我们的问题都减少了 1 个节点。
我们可以用递归关系的形式写为:F(n) = n*(2+F(n-1))
这扩展为:2n + 2n*(n-1) + 2n*(n-1)*(n-2) + ……。+ 2n(n-1)(n-2)(n-3)…..1
由于 n 乘以 2n(n-1)(n-2)(n-3)….1 大于给定的表达式，所以我们可以有把握地说时间复杂度为:n*2*n！
这里在问题中定义了第一个节点，因此时间复杂度变成了
F(n-1) = 2(n-1)*(n-1)！= 2*n*(n-1)！–2 * 1 *(n-1)！= 2*n！-2*(n-1)！= O(n！)
本文由**希瓦姆·古普塔**供稿。时间复杂性的解释来自**普拉纳夫·南比亚尔**。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息