# 查找有向图中两个顶点之间是否有路径

> 原文:[https://www . geeksforgeeks . org/find-如果给定图形中的两个顶点之间存在路径/](https://www.geeksforgeeks.org/find-if-there-is-a-path-between-two-vertices-in-a-given-graph/)

给定一个有向图和其中的两个顶点，检查是否有从第一个给定顶点到第二个给定顶点的路径。
**例:**

```
Consider the following Graph:

Input : (u, v) = (1, 3)
Output: Yes
Explanation: There is a path from 1 to 3, 1 -> 2 -> 3

Input : (u, v) = (3, 6)
Output: No
Explanation: There is no path from 3 to 6
```

**方法:**可以使用[广度优先搜索(BFS)](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 或[深度优先搜索(DFS)](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 来寻找两个顶点之间的路径。在 BFS 以第一个顶点为源，遵循标准的 BFS。如果在我们的遍历中找到了第二个顶点，那么返回 true，否则返回 false。
**算法:**

1.  下面的实现使用了 BFS。
2.  创建一个队列和一个最初用 0 填充的访问数组，大小为 V，其中 V 是顶点数。
3.  在队列中插入起始节点，即在队列中推送 u，并将 u 标记为已访问。
4.  运行循环，直到队列不为空。
5.  将队列的前一个元素出列。迭代其所有相邻元素。如果任何相邻元素是目标，则返回 true。推送队列中所有相邻和未访问的顶点，并将它们标记为已访问。
6.  返回 false，因为目的地不在 BFS。

**实现:**使用 BFS 从第一个顶点寻找第二个顶点可达性的 C++、Java 和 Python 代码。

## C++

```
// C++ program to check if there is exist a path between two vertices
// of a graph.
#include<iostream>
#include <list>
using namespace std;

// This class represents a directed graph using adjacency list
// representation
class Graph
{
    int V;    // No. of vertices
    list<int> *adj;    // Pointer to an array containing adjacency lists
public:
    Graph(int V);  // Constructor
    void addEdge(int v, int w); // function to add an edge to graph
    bool isReachable(int s, int d); 
};

Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
}

void Graph::addEdge(int v, int w)
{
    adj[v].push_back(w); // Add w to v’s list.
}

// A BFS based function to check whether d is reachable from s.
bool Graph::isReachable(int s, int d)
{
    // Base case
    if (s == d)
      return true;

    // Mark all the vertices as not visited
    bool *visited = new bool[V];
    for (int i = 0; i < V; i++)
        visited[i] = false;

    // Create a queue for BFS
    list<int> queue;

    // Mark the current node as visited and enqueue it
    visited[s] = true;
    queue.push_back(s);

    // it will be used to get all adjacent vertices of a vertex
    list<int>::iterator i;

    while (!queue.empty())
    {
        // Dequeue a vertex from queue and print it
        s = queue.front();
        queue.pop_front();

        // Get all adjacent vertices of the dequeued vertex s
        // If a adjacent has not been visited, then mark it visited
        // and enqueue it
        for (i = adj[s].begin(); i != adj[s].end(); ++i)
        {
            // If this adjacent node is the destination node, then
            // return true
            if (*i == d)
                return true;

            // Else, continue to do BFS
            if (!visited[*i])
            {
                visited[*i] = true;
                queue.push_back(*i);
            }
        }
    }

    // If BFS is complete without visiting d
    return false;
}

// Driver program to test methods of graph class
int main()
{
    // Create a graph given in the above diagram
    Graph g(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    int u = 1, v = 3;
    if(g.isReachable(u, v))
        cout<< "\n There is a path from " << u << " to " << v;
    else
        cout<< "\n There is no path from " << u << " to " << v;

    u = 3, v = 1;
    if(g.isReachable(u, v))
        cout<< "\n There is a path from " << u << " to " << v;
    else
        cout<< "\n There is no path from " << u << " to " << v;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if there is exist a path between two vertices
// of a graph.
import java.io.*;
import java.util.*;
import java.util.LinkedList;

// This class represents a directed graph using adjacency list
// representation
class Graph
{
    private int V;   // No. of vertices
    private LinkedList<Integer> adj[]; //Adjacency List

    //Constructor
    Graph(int v)
    {
        V = v;
        adj = new LinkedList[v];
        for (int i=0; i<v; ++i)
            adj[i] = new LinkedList();
    }

    //Function to add an edge into the graph
    void addEdge(int v,int w)  {   adj[v].add(w);   }

    //prints BFS traversal from a given source s
    Boolean isReachable(int s, int d)
    {
        LinkedList<Integer>temp;

        // Mark all the vertices as not visited(By default set
        // as false)
        boolean visited[] = new boolean[V];

        // Create a queue for BFS
        LinkedList<Integer> queue = new LinkedList<Integer>();

        // Mark the current node as visited and enqueue it
        visited[s]=true;
        queue.add(s);

        // 'i' will be used to get all adjacent vertices of a vertex
        Iterator<Integer> i;
        while (queue.size()!=0)
        {
            // Dequeue a vertex from queue and print it
            s = queue.poll();

            int n;
            i = adj[s].listIterator();

            // Get all adjacent vertices of the dequeued vertex s
            // If a adjacent has not been visited, then mark it
            // visited and enqueue it
            while (i.hasNext())
            {
                n = i.next();

                // If this adjacent node is the destination node,
                // then return true
                if (n==d)
                    return true;

                // Else, continue to do BFS
                if (!visited[n])
                {
                    visited[n] = true;
                    queue.add(n);
                }
            }
        }

        // If BFS is complete without visited d
        return false;
    }

    // Driver method
    public static void main(String args[])
    {
        // Create a graph given in the above diagram
        Graph g = new Graph(4);
        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 2);
        g.addEdge(2, 0);
        g.addEdge(2, 3);
        g.addEdge(3, 3);

        int u = 1;
        int v = 3;
        if (g.isReachable(u, v))
            System.out.println("There is a path from " + u +" to " + v);
        else
            System.out.println("There is no path from " + u +" to " + v);;

        u = 3;
        v = 1;
        if (g.isReachable(u, v))
            System.out.println("There is a path from " + u +" to " + v);
        else
            System.out.println("There is no path from " + u +" to " + v);;
    }
}
// This code is contributed by Aakash Hasija
```

## 计算机编程语言

```
# program to check if there is exist a path between two vertices
# of a graph

from collections import defaultdict

#This class represents a directed graph using adjacency list representation
class Graph:

    def __init__(self,vertices):
        self.V= vertices #No. of vertices
        self.graph = defaultdict(list) # default dictionary to store graph

    # function to add an edge to graph
    def addEdge(self,u,v):
        self.graph[u].append(v)

     # Use BFS to check path between s and d
    def isReachable(self, s, d):
        # Mark all the vertices as not visited
        visited =[False]*(self.V)

        # Create a queue for BFS
        queue=[]

        # Mark the source node as visited and enqueue it
        queue.append(s)
        visited[s] = True

        while queue:

            #Dequeue a vertex from queue
            n = queue.pop(0)

            # If this adjacent node is the destination node,
            # then return true
             if n == d:
                 return True

            #  Else, continue to do BFS
            for i in self.graph[n]:
                if visited[i] == False:
                    queue.append(i)
                    visited[i] = True
         # If BFS is complete without visited d
         return False

# Create a graph given in the above diagram
g = Graph(4)
g.addEdge(0, 1)
g.addEdge(0, 2)
g.addEdge(1, 2)
g.addEdge(2, 0)
g.addEdge(2, 3)
g.addEdge(3, 3)

u =1; v = 3

if g.isReachable(u, v):
    print("There is a path from %d to %d" % (u,v))
else :
    print("There is no path from %d to %d" % (u,v))

u = 3; v = 1
if g.isReachable(u, v) :
    print("There is a path from %d to %d" % (u,v))
else :
    print("There is no path from %d to %d" % (u,v))

#This code is contributed by Neelam Yadav
```

## C#

```
// C# program to check if there is
// exist a path between two vertices
// of a graph.
using System;
using System.Collections;
using System.Collections.Generic;

// This class represents a directed
// graph using adjacency list
// representation
class Graph
{
  private int V; // No. of vertices
  private LinkedList<int>[] adj; //Adjacency List

  // Constructor
  Graph(int v)
  {
    V = v;
    adj = new LinkedList<int>[v];
    for (int i = 0; i < v; ++i)
      adj[i] = new LinkedList<int>();
  }

  // Function to add an edge into the graph
  void addEdge(int v, int w)
  {
    adj[v].AddLast(w);
  }

  // prints BFS traversal from a given source s
  bool isReachable(int s, int d)
  {
    // LinkedList<int> temp = new LinkedList<int>();

    // Mark all the vertices as not visited(By default set
    // as false)
    bool[] visited = new bool[V];

    // Create a queue for BFS
    LinkedList<int> queue = new LinkedList<int>();

    // Mark the current node as visited and enqueue it
    visited[s] = true;
    queue.AddLast(s);

    // 'i' will be used to get all adjacent vertices of a vertex
    IEnumerator i;     
    while (queue.Count != 0)
    {

      // Dequeue a vertex from queue and print it
      s = queue.First.Value;
      queue.RemoveFirst();
      int n;
      i = adj[s].GetEnumerator();

      // Get all adjacent vertices of the dequeued vertex s
      // If a adjacent has not been visited, then mark it
      // visited and enqueue it
      while (i.MoveNext())
      {
        n = (int)i.Current;

        // If this adjacent node is the destination node,
        // then return true
        if (n == d)
          return true;

        // Else, continue to do BFS
        if (!visited[n])
        {
          visited[n] = true;
          queue.AddLast(n);
        }
      }
    }

    // If BFS is complete without visited d
    return false;
  }

  // Driver method
  public static void Main(string[] args)
  {

    // Create a graph given in the above diagram
    Graph g = new Graph(4);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);
    int u = 1;
    int v = 3;
    if (g.isReachable(u, v))
      Console.WriteLine("There is a path from " + u + " to " + v);
    else
      Console.WriteLine("There is no path from " + u + " to " + v);
    u = 3;
    v = 1;
    if (g.isReachable(u, v))
      Console.WriteLine("There is a path from " + u + " to " + v);
    else
      Console.WriteLine("There is no path from " + u + " to " + v);
  }
}

// This code is contributed by sanjeev2552
```

## java 描述语言

```
<script>
// Javascript program to check if there is exist a path between two vertices
// of a graph.
let  V;
let adj;

function Graph( v)
{
        V = v;
        adj = new Array(v);
        for (let i = 0; i < v; ++i)
            adj[i] = [];
}

// Function to add an edge into the graph
function addEdge(v,w)
{
    adj[v].push(w);
}

// prints BFS traversal from a given source s
function isReachable(s,d)
{
    let temp;

        // Mark all the vertices as not visited(By default set
        // as false)
        let visited = new Array(V);
         for(let i = 0; i < V; i++)
            visited[i] = false;

        // Create a queue for BFS
        let queue = [];

        // Mark the current node as visited and enqueue it
        visited[s] = true;
        queue.push(s);

        while (queue.length != 0)
        {
            // Dequeue a vertex from queue and print it
            n = queue.shift();

            if(n == d)
                return true;
            for(let i = 0; i < adj[n].length; i++)
            {
                if (visited[adj[n][i]] == false)
                {
                    queue.push(adj[n][i]);
                    visited[adj[n][i]] = true;
                }
            }

        }

        // If BFS is complete without visited d
        return false;
}

// Driver method
Graph(4);
addEdge(0, 1);
addEdge(0, 2);
addEdge(1, 2);
addEdge(2, 0);
addEdge(2, 3);
addEdge(3, 3);

let u = 1;
let v = 3;
if (isReachable(u, v))
    document.write("There is a path from " + u +" to " + v+"<br>");
else
    document.write("There is no path from " + u +" to " + v+"<br>");

u = 3;
v = 1;
if (isReachable(u, v))
    document.write("There is a path from " + u +" to " + v+"<br>");
else
    document.write("There is no path from " + u +" to " + v+"<br>");

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
There is a path from 1 to 3
There is no path from 3 to 1
```

**复杂度分析:**

*   **时间复杂度:** O(V+E)，其中 V 是图中的顶点数，E 是图中的边数。
*   **空间竞争:** O(V)。
    队列中可以有五个元素。所以需要的空间是 O(V)。

**BFS 和 DFS 之间的权衡:**广度优先搜索对于找到节点之间的最短路径非常有用，深度优先搜索可能会在进入近邻之前非常深入地遍历一个相邻节点。
*作为练习，尝试问题的扩展版本，其中也需要两个顶点之间的完整路径。*
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息。