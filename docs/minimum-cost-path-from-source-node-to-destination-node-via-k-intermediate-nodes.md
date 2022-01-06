# 通过 K 个中间节点从源节点到目的节点的最小成本路径

> 原文:[https://www . geesforgeks . org/最低成本-从源节点到目标节点的路径-via-k-中间节点/](https://www.geeksforgeeks.org/minimum-cost-path-from-source-node-to-destination-node-via-k-intermediate-nodes/)

给定一个由 **N** 顶点和 **M** 加权边组成的[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)和一个数组**边[][]** ，每行代表由边和边的权重连接的两个顶点，任务是找到从给定源顶点 **src** 到给定目的顶点 **dst** 的权重总和最小的路径，该路径由 **K** 中间顶点组成。如果不存在这样的路径，则打印 **-1** 。

**示例:**

> **输入:** N = 3，M = 3，src = 0，dst = 2，K = 1，边[] = {{0，1，100}，{1，2，100}，{0，2，500}}
> **输出:** 200
> **解释:**路径 0 - > 1 - > 2 是连接 src (= 0)的最小加权和(= 100 + 100 = 200)
> 
> **输入:** N = 3，M = 3，src = 0，dst = 2，K = 0，边[] = { { 0，1，100 }，{ 1，2，100 }，{ 0，2，500 } }
> **输出:** 500
> **说明:**权重为 500 的直边 0 - > 2 为所需路径。

**方式:**给定的问题可以使用[优先队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)和执行 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 来解决。按照以下步骤解决此问题:

1.  初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-class-in-java-2/)来存储元组**{到达该顶点的成本，顶点，停靠次数}** 。
2.  推 **{0，src，k+1}** 作为第一个起点。
3.  弹出优先队列的[顶元素。如果所有的站都用尽了，那么重复这个步骤。](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)
4.  如果到达目的地，则打印**到达当前顶点的成本。**
5.  否则，找到这个顶点的邻居，它需要最小的代价才能到达那个顶点。[将其推入**优先队列**](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/) **。**
6.  从步骤 **2** 开始重复。
7.  如果执行上述步骤后没有找到路径，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost path
// from the source vertex to destination
// vertex via K intermediate vertices
int leastWeightedSumPath(int n,
                         vector<vector<int> >& edges,
                         int src, int dst, int K)
{
    // Initialize the adjacency list
    unordered_map<int,
                  vector<pair<int, int> > >
        graph;

    // Generate the adjacency list
    for (vector<int>& edge : edges) {
        graph[edge[0]].push_back(
            make_pair(edge[1], edge[2]));
    }

    // Initialize the minimum priority queue
    priority_queue<vector<int>, vector<vector<int> >,
                   greater<vector<int> > >
        pq;

    // Stores the minimum cost to
    // travel between vertices via
    // K intermediate nodes
    vector<vector<int> > costs(n,
                               vector<int>(
                                   K + 2, INT_MAX));

    costs[src][K + 1] = 0;

    // Push the starting vertex,
    // cost to reach and the number
    // of remaining vertices
    pq.push({ 0, src, K + 1 });

    while (!pq.empty()) {
        // Pop the top element
        // of the stack
        auto top = pq.top();

        pq.pop();

        // If destination is reached
        if (top[1] == dst)

            // Return the cost
            return top[0];

        // If all stops are exhausted
        if (top[2] == 0)
            continue;

        // Find the neighbour with minimum cost
        for (auto neighbor : graph[top[1]]) {

            // Pruning
            if (costs[neighbor.first][top[2] - 1]
                < neighbor.second + top[0]) {
                continue;
            }

            // Update cost
            costs[neighbor.first][top[2] - 1]
                = neighbor.second + top[0];

            // Update priority queue
            pq.push({ neighbor.second + top[0],
                      neighbor.first, top[2] - 1 });
        }
    }

    // If no path exists
    return -1;
}

// Driver Code
int main()
{
    int n = 3, src = 0, dst = 2, k = 1;
    vector<vector<int> > edges
        = { { 0, 1, 100 },
            { 1, 2, 100 },
            { 0, 2, 500 } };

    // Function Call to find the path
    // from src to dist via k nodes
    // having least sum of weights
    cout << leastWeightedSumPath(n, edges,
                                 src, dst, k);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum cost path
# from the source vertex to destination
# vertex via K intermediate vertices
def leastWeightedSumPath(n, edges, src, dst, K):
    graph = [[] for i in range(3)]

    # Generate the adjacency list
    for edge in edges:
        graph[edge[0]].append([edge[1], edge[2]])

    # Initialize the minimum priority queue
    pq = []

    # Stores the minimum cost to
    # travel between vertices via
    # K intermediate nodes
    costs = [[10**9 for i in range(K + 2)] for i in range(n)]

    costs[src][K + 1] = 0

    # Push the starting vertex,
    # cost to reach and the number
    # of remaining vertices
    pq.append([ 0, src, K + 1 ])

    pq = sorted(pq)[::-1]

    while (len(pq) > 0):

        # Pop the top element
        # of the stack
        top = pq[-1]

        del pq[-1]

        # If destination is reached
        if (top[1] == dst):

            # Return the cost
            return top[0]

        # If all stops are exhausted
        if (top[2] == 0):
            continue

        # Find the neighbour with minimum cost
        for neighbor in graph[top[1]]:

            # Pruning
            if (costs[neighbor[0]][top[2] - 1] < neighbor[1] + top[0]):
                continue

            # Update cost
            costs[neighbor[0]][top[2] - 1] = neighbor[1]+ top[0]

            # Update priority queue
            pq.append([neighbor[1]+ top[0],neighbor[0], top[2] - 1])
        pq = sorted(pq)[::-1]

    # If no path exists
    return -1

# Driver Code
if __name__ == '__main__':
    n, src, dst, k = 3, 0, 2, 1
    edges = [ [ 0, 1, 100 ],
            [ 1, 2, 100 ],
            [ 0, 2, 500 ] ]

    # Function Call to find the path
    # from src to dist via k nodes
    # having least sum of weights
    print (leastWeightedSumPath(n, edges, src, dst, k))

# This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum cost path
// from the source vertex to destination
// vertex via K intermediate vertices
function leastWeightedSumPath(n, edges, src, dst, K)
{

    // Initialize the adjacency list
    var graph = new Map();

    // Generate the adjacency list
    for (var edge of edges) {
        if(!graph.has(edge[0]))
            graph.set(edge[0], new Array())
        var tmp = graph.get(edge[0]);
        tmp.push([edge[1], edge[2]]);
        graph.set(edge[0],tmp);
    }

    // Initialize the minimum priority queue
    var pq = [];

    // Stores the minimum cost to
    // travel between vertices via
    // K intermediate nodes
    var costs = Array.from(Array(n+1), ()=>Array(K+2).fill(1000000000));
    costs[src][K + 1] = 0;

    // Push the starting vertex,
    // cost to reach and the number
    // of remaining vertices
    pq.push([ 0, src, K + 1 ]);

    while (pq.length!=0) {
        // Pop the top element
        // of the stack
        var top = pq[pq.length-1];

        pq.pop();

        // If destination is reached
        if (top[1] == dst)

            // Return the cost
            return top[0];

        // If all stops are exhausted
        if (top[2] == 0)
            continue;

        if(graph.has(top[1]))
        {
        // Find the neighbour with minimum cost
        for (var neighbor of graph.get(top[1])) {

            // Pruning
            if (costs[neighbor[0]][top[2] - 1]
                < neighbor[1] + top[0]) {
                continue;
            }

            // Update cost
            costs[neighbor[0]][top[2] - 1]
                = neighbor[1] + top[0];

            // Update priority queue
            pq.push([neighbor[1] + top[0],
                      neighbor[0], top[2] - 1 ]);
        }
        }
        pq.sort((a,b)=>{
            if(a[0]==b[0])
             return b[1]-a[1]
            return b[0]-a[0];
        });
    }

    // If no path exists
    return -1;
}

// Driver Code
var n = 3, src = 0, dst = 2, k = 1;
var edges
    = [ [ 0, 1, 100 ],
        [ 1, 2, 100 ],
        [ 0, 2, 500 ] ];
// Function Call to find the path
// from src to dist via k nodes
// having least sum of weights
document.write(leastWeightedSumPath(n, edges,
                             src, dst, k));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
200
```

***时间复杂度:**O(N * log N)*
T5**辅助空间** : O(N)