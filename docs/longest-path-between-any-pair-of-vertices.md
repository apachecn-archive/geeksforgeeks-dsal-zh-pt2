# 任意一对顶点之间的最长路径

> 原文:[https://www . geesforgeks . org/任意对顶点之间的最长路径/](https://www.geeksforgeeks.org/longest-path-between-any-pair-of-vertices/)

我们得到了一张通过电缆线路相互连接的城市地图，这样在任何两个城市之间都没有循环。对于给定的城市地图，我们需要找到任意两个城市之间电缆的最大长度。

```
Input : n = 6  
        1 2 3  // Cable length from 1 to 2 (or 2 to 1) is 3
        2 3 4
        2 6 2
        6 4 6
        6 5 5
Output: maximum length of cable = 12
```

**方法 1(简单 DFS)**
我们为给定的城市地图创建无向图，并对每个城市进行 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 以找到电缆的最大长度。在遍历时，我们寻找到达当前城市的总电缆长度，如果它的相邻城市未被访问，则为它调用 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，但是如果当前节点访问了所有相邻城市，则如果 max_length 的先前值小于总电缆长度的当前值，则更新 max_length 的值。

## C++

```
// C++ program to find the longest cable length
// between any two cities.
#include<bits/stdc++.h>
using namespace std;

// visited[] array to make nodes visited
// src is starting node for DFS traversal
// prev_len is sum of cable length till current node
// max_len is pointer which stores the maximum length
// of cable value after DFS traversal
void DFS(vector< pair<int,int> > graph[], int src,
         int prev_len, int *max_len,
         vector <bool> &visited)
{
    // Mark the src node visited
    visited[src] = 1;

    // curr_len is for length of cable from src
    // city to its adjacent city
    int curr_len = 0;

    // Adjacent is pair type which stores
    // destination city and cable length
    pair < int, int > adjacent;

    // Traverse all adjacent
    for (int i=0; i<graph[src].size(); i++)
    {
        // Adjacent element
        adjacent = graph[src][i];

        // If node or city is not visited
        if (!visited[adjacent.first])
        {
            // Total length of cable from src city
            // to its adjacent
            curr_len = prev_len + adjacent.second;

            // Call DFS for adjacent city
            DFS(graph, adjacent.first, curr_len,
                max_len,  visited);
        }

        // If total cable length till now greater than
        // previous length then update it
        if ((*max_len) < curr_len)
            *max_len = curr_len;

        // make curr_len = 0 for next adjacent
        curr_len = 0;
    }
}

// n is number of cities or nodes in graph
// cable_lines is total cable_lines among the cities
// or edges in graph
int longestCable(vector<pair<int,int> > graph[],
                                          int n)
{
    // maximum length of cable among the connected
    // cities
    int max_len = INT_MIN;

    // call DFS for each city to find maximum
    // length of cable
    for (int i=1; i<=n; i++)
    {
        // initialize visited array with 0
        vector< bool > visited(n+1, false);

        // Call DFS for src vertex i
        DFS(graph, i, 0, &max_len, visited);
    }

    return max_len;
}

// driver program to test the input
int main()
{
    // n is number of cities
    int n = 6;

    vector< pair<int,int> > graph[n+1];

    // create undirected graph
    // first edge
    graph[1].push_back(make_pair(2, 3));
    graph[2].push_back(make_pair(1, 3));

    // second edge
    graph[2].push_back(make_pair(3, 4));
    graph[3].push_back(make_pair(2, 4));

    // third edge
    graph[2].push_back(make_pair(6, 2));
    graph[6].push_back(make_pair(2, 2));

    // fourth edge
    graph[4].push_back(make_pair(6, 6));
    graph[6].push_back(make_pair(4, 6));

    // fifth edge
    graph[5].push_back(make_pair(6, 5));
    graph[6].push_back(make_pair(5, 5));

    cout << "Maximum length of cable = "
         << longestCable(graph, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest cable length
// between any two cities.
import java.util.*;
public class GFG
{

    // visited[] array to make nodes visited
    // src is starting node for DFS traversal
    // prev_len is sum of cable length till current node
    // max_len is pointer which stores the maximum length
    // of cable value after DFS traversal

    // Class containing left and
    // right child of current
    // node and key value
    static class pair {

        public int x, y;
        public pair(int f, int s)
        {
            x = f;
            y = s;
        }
    }

    // maximum length of cable among the connected
    // cities
    static int max_len = Integer.MIN_VALUE;

    static void DFS(Vector<Vector<pair>> graph, int src,
                    int prev_len, boolean[] visited)
    {

        // Mark the src node visited
        visited[src] = true;

        // curr_len is for length of cable
        // from src city to its adjacent city
        int curr_len = 0;

        // Adjacent is pair type which stores
        // destination city and cable length
        pair adjacent;

        // Traverse all adjacent
        for(int i = 0; i < graph.get(src).size(); i++)
        {
            // Adjacent element
            adjacent = graph.get(src).get(i);

            // If node or city is not visited
            if (!visited[adjacent.x])
            {
                // Total length of cable from
                // src city to its adjacent
                curr_len = prev_len + adjacent.y;

                // Call DFS for adjacent city
                DFS(graph, adjacent.x, curr_len, visited);
            }

            // If total cable length till
            // now greater than previous
            // length then update it
            if (max_len < curr_len)
            {
                max_len = curr_len;
            }

            // make curr_len = 0 for next adjacent
            curr_len = 0;
        }
    }

    // n is number of cities or nodes in graph
    // cable_lines is total cable_lines among the cities
    // or edges in graph
    static int longestCable(Vector<Vector<pair>> graph, int n)
    {
        // call DFS for each city to find maximum
        // length of cable
        for (int i=1; i<=n; i++)
        {
            // initialize visited array with 0
            boolean[] visited = new boolean[n+1];

            // Call DFS for src vertex i
            DFS(graph, i, 0, visited);
        }

        return max_len;
    }

    public static void main(String[] args) {
        // n is number of cities
        int n = 6;

        Vector<Vector<pair>> graph = new Vector<Vector<pair>>();
        for(int i = 0; i < n + 1; i++)
        {
            graph.add(new Vector<pair>());
        }

        // create undirected graph
        // first edge
        graph.get(1).add(new pair(2, 3));
        graph.get(2).add(new pair(1, 3));

        // second edge
        graph.get(2).add(new pair(3, 4));
        graph.get(3).add(new pair(2, 4));

        // third edge
        graph.get(2).add(new pair(6, 2));
        graph.get(6).add(new pair(2, 2));

        // fourth edge
        graph.get(4).add(new pair(6, 6));
        graph.get(6).add(new pair(4, 6));

        // fifth edge
        graph.get(5).add(new pair(6, 5));
        graph.get(6).add(new pair(5, 5));

        System.out.print("Maximum length of cable = "
             + longestCable(graph, n));
    }
}

// This code is contributed by suresh07.
```

## 蟒蛇 3

```
# Python3 program to find the longest
# cable length between any two cities.

# visited[] array to make nodes visited
# src is starting node for DFS traversal
# prev_len is sum of cable length till
# current node max_len is pointer which
# stores the maximum length of cable
# value after DFS traversal
def DFS(graph, src, prev_len,
        max_len, visited):

    # Mark the src node visited
    visited[src] = 1

    # curr_len is for length of cable
    # from src city to its adjacent city
    curr_len = 0

    # Adjacent is pair type which stores
    # destination city and cable length
    adjacent = None

    # Traverse all adjacent
    for i in range(len(graph[src])):

        # Adjacent element
        adjacent = graph[src][i]

        # If node or city is not visited
        if (not visited[adjacent[0]]):

            # Total length of cable from
            # src city to its adjacent
            curr_len = prev_len + adjacent[1]

            # Call DFS for adjacent city
            DFS(graph, adjacent[0], curr_len,
                            max_len, visited)

        # If total cable length till
        # now greater than previous
        # length then update it
        if (max_len[0] < curr_len):
            max_len[0] = curr_len

        # make curr_len = 0 for next adjacent
        curr_len = 0

# n is number of cities or nodes in
# graph cable_lines is total cable_lines 
# among the cities or edges in graph
def longestCable(graph, n):

    # maximum length of cable among
    # the connected cities
    max_len = [-999999999999]

    # call DFS for each city to find
    # maximum length of cable
    for i in range(1, n + 1):

        # initialize visited array with 0
        visited = [False] * (n + 1)

        # Call DFS for src vertex i
        DFS(graph, i, 0, max_len, visited)

    return max_len[0]

# Driver Code
if __name__ == '__main__':

    # n is number of cities
    n = 6

    graph = [[] for i in range(n + 1)]

    # create undirected graph
    # first edge
    graph[1].append([2, 3])
    graph[2].append([1, 3])

    # second edge
    graph[2].append([3, 4])
    graph[3].append([2, 4])

    # third edge
    graph[2].append([6, 2])
    graph[6].append([2, 2])

    # fourth edge
    graph[4].append([6, 6])
    graph[6].append([4, 6])

    # fifth edge
    graph[5].append([6, 5])
    graph[6].append([5, 5])

    print("Maximum length of cable =",
               longestCable(graph, n))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find the longest cable length
// between any two cities.
using System;
using System.Collections.Generic;
class GFG {

    // visited[] array to make nodes visited
    // src is starting node for DFS traversal
    // prev_len is sum of cable length till current node
    // max_len is pointer which stores the maximum length
    // of cable value after DFS traversal

    // maximum length of cable among the connected
    // cities
    static int max_len = Int32.MinValue;

    static void DFS(List<List<Tuple<int,int>>> graph, int src, int prev_len, bool[] visited)
    {
        // Mark the src node visited
        visited[src] = true;

        // curr_len is for length of cable
        // from src city to its adjacent city
        int curr_len = 0;

        // Adjacent is pair type which stores
        // destination city and cable length
        Tuple<int,int> adjacent;

        // Traverse all adjacent
        for(int i = 0; i < graph[src].Count; i++)
        {
            // Adjacent element
            adjacent = graph[src][i];

            // If node or city is not visited
            if (!visited[adjacent.Item1])
            {
                // Total length of cable from
                // src city to its adjacent
                curr_len = prev_len + adjacent.Item2;

                // Call DFS for adjacent city
                DFS(graph, adjacent.Item1, curr_len, visited);
            }

            // If total cable length till
            // now greater than previous
            // length then update it
            if (max_len < curr_len)
            {
                max_len = curr_len;
            }

            // make curr_len = 0 for next adjacent
            curr_len = 0;
        }
    }

    // n is number of cities or nodes in graph
    // cable_lines is total cable_lines among the cities
    // or edges in graph
    static int longestCable(List<List<Tuple<int,int>>> graph, int n)
    {
        // call DFS for each city to find maximum
        // length of cable
        for (int i=1; i<=n; i++)
        {
            // initialize visited array with 0
            bool[] visited = new bool[n+1];

            // Call DFS for src vertex i
            DFS(graph, i, 0, visited);
        }

        return max_len;
    }

  static void Main() {
    // n is number of cities
    int n = 6;

    List<List<Tuple<int,int>>> graph = new List<List<Tuple<int,int>>>();
    for(int i = 0; i < n + 1; i++)
    {
        graph.Add(new List<Tuple<int,int>>());
    }

    // create undirected graph
    // first edge
    graph[1].Add(new Tuple<int,int>(2, 3));
    graph[2].Add(new Tuple<int,int>(1, 3));

    // second edge
    graph[2].Add(new Tuple<int,int>(3, 4));
    graph[3].Add(new Tuple<int,int>(2, 4));

    // third edge
    graph[2].Add(new Tuple<int,int>(6, 2));
    graph[6].Add(new Tuple<int,int>(2, 2));

    // fourth edge
    graph[4].Add(new Tuple<int,int>(6, 6));
    graph[6].Add(new Tuple<int,int>(4, 6));

    // fifth edge
    graph[5].Add(new Tuple<int,int>(6, 5));
    graph[6].Add(new Tuple<int,int>(5, 5));

    Console.Write("Maximum length of cable = "
         + longestCable(graph, n));
  }
}

// This code is contributed by decode2207.
```

## java 描述语言

```
<script>
    // Javascript program to find the longest cable length
    // between any two cities.

    // visited[] array to make nodes visited
    // src is starting node for DFS traversal
    // prev_len is sum of cable length till current node
    // max_len is pointer which stores the maximum length
    // of cable value after DFS traversal

    // maximum length of cable among the connected
    // cities
    let max_len = Number.MIN_VALUE;

    function DFS(graph, src, prev_len, visited)
    {
        // Mark the src node visited
        visited[src] = true;

        // curr_len is for length of cable
        // from src city to its adjacent city
        let curr_len = 0;

        // Adjacent is pair type which stores
        // destination city and cable length
        let adjacent = [];

        // Traverse all adjacent
        for(let i = 0; i < graph[src].length; i++)
        {
            // Adjacent element
            adjacent = graph[src][i];

            // If node or city is not visited
            if (!visited[adjacent[0]])
            {
                // Total length of cable from
                // src city to its adjacent
                curr_len = prev_len + adjacent[1];

                // Call DFS for adjacent city
                DFS(graph, adjacent[0], curr_len, visited);
            }

            // If total cable length till
            // now greater than previous
            // length then update it
            if (max_len < curr_len)
            {
                max_len = curr_len;
            }

            // make curr_len = 0 for next adjacent
            curr_len = 0;
        }
    }

    // n is number of cities or nodes in graph
    // cable_lines is total cable_lines among the cities
    // or edges in graph
    function longestCable(graph, n)
    {
        // call DFS for each city to find maximum
        // length of cable
        for (let i=1; i<=n; i++)
        {
            // initialize visited array with 0
            let visited = new Array(n+1);
            visited.fill(false);

            // Call DFS for src vertex i
            DFS(graph, i, 0, visited);
        }

        return max_len;
    }

    // n is number of cities
    let n = 6;

    let graph = [];
    for(let i = 0; i < n + 1; i++)
    {
        graph.push([]);
    }

    // create undirected graph
    // first edge
    graph[1].push([2, 3]);
    graph[2].push([1, 3]);

    // second edge
    graph[2].push([3, 4]);
    graph[3].push([2, 4]);

    // third edge
    graph[2].push([6, 2]);
    graph[6].push([2, 2]);

    // fourth edge
    graph[4].push([6, 6]);
    graph[6].push([4, 6]);

    // fifth edge
    graph[5].push([6, 5]);
    graph[6].push([5, 5]);

    document.write("Maximum length of cable = " +
               longestCable(graph, n));

    // This code is contributed by divyesh072019.
</script>
```

**输出:**

```
Maximum length of cable = 12
```

**时间复杂度:** O(V * (V + E))

**方法 2(高效:仅在图有向时有效)**
如果给定的图是有向图而不是无向图，我们可以在 O(V+E)时间内解决上述问题。以下是步骤。
**1)** 创建一个距离数组 dist[]并将其所有条目初始化为负无穷大
**2)** 按照[拓扑顺序](https://www.geeksforgeeks.org/topological-sorting/)对所有顶点进行排序。
**(3)**按照拓扑顺序对每个顶点 u 进行以下操作。
…..对 u 的每个相邻顶点 v 执行以下操作
………..if (dist[v] < dist[u] +权重(u，v))
…………dist[v]= dist[u]+权重(u，v)
**4)** 从 dist[]

返回最大值由于没有负权重，按拓扑顺序处理顶点将始终产生最长路径 dist[]的数组，这样 dist[u]表示最长路径以顶点“u”结束。
上述方法的实施可以从[这里的](https://www.geeksforgeeks.org/find-longest-path-directed-acyclic-graph/)很容易地采用。这里的区别是，没有负权重边，我们需要整体最长路径(不是从源顶点开始的最长路径)。最后，我们返回 dist[]中所有值的最大值。
时间复杂度:O(V + E)
本文由 [**沙莎克·米什拉(古鲁)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。本文由 GeeksForGeeks 团队审阅。如果你有更好的方法解决这个问题，请分享。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。