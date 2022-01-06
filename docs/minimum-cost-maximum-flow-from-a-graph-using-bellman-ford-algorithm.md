# 使用贝尔曼福特算法的最小成本最大流量图

> 原文:[https://www . geesforgeks . org/最小成本-最大流量-使用贝尔曼-福特算法的图表/](https://www.geeksforgeeks.org/minimum-cost-maximum-flow-from-a-graph-using-bellman-ford-algorithm/)

给定一个源节点 **S、**一个宿节点 **T** ，两个矩阵 **Cap[ ][ ]** 和 **Cost[ ][ ]** 表示一个图，其中 **Cap[i][j]** 是从节点 **i** 到节点 **j** 的有向边的容量，而 **cost[i][j]** 是从节点**沿着有向边发送一个单元流的成本**

> **最小成本最大流量:**从给定图表中输送最大可能流量所需的最小成本(每单位流量)。

**示例:**

> **输入:** S = 0，T = 4，cap[ ][ ] = {{0，3，4，5，0}，{0，0，2，0，0，0，4，1}，{0，0，0，0，0，10}，{0，0，0，0，0，0，0}}，
> 成本[ ][ ] = {{0，1，0，0，0，0}，{0，0，0，0，0}，{0，0，0，0，0，0，0}
> 
> **输入:** S = 0，T = 4，成本[][] = { { 0，1，0，0，2 }，{ 0，0，0，3，0 }，{ 0，0，0，0，0，1 }，{ 0，0，0，0，1 }，{ 0，0，0，0，0，0 } }
> cap[][] = { { 0，3，1，0，3 }，{ 0，0，2，0，0 }，{ 0，0，0，0，1，6 }，{ 0

**方法:**
成本网络中的负循环是循环的，循环中所有边的成本之和是负的。可以使用[贝尔曼·福特算法](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)检测到它们。它们应该被消除，因为实际上，不能允许流过这样的循环。考虑一个**负成本周期**，如果所有的流程都要经过这个周期，那么每完成一个周期，总成本总是在降低。这将导致无限循环的愿望**最小化总成本**。因此，只要成本网络包含负周期，它就意味着成本可以进一步最小化(通过流经周期的另一侧，而不是当前考虑的一侧)。一旦检测到负循环，则通过使[瓶颈容量](https://en.wikipedia.org/wiki/Bottleneck_(production)#:~:text=In%20production%20and%20project%20management, customers%2C%20and%20low%20employee%20morale.)流过循环中的所有边来消除。

现在，看看什么是供需节点:

> **供应节点:**这些是添加到流中并产生流的正节点。
> **需求节点:**这些是从流量中减去的负节点。
> **每个节点的供应(或需求)** =引出节点的总流量–引入节点的总流量

通过向循环中的所有边发送瓶颈容量来解决给定的问题，以处理负循环。此外，由于它涉及需求节点，调用[贝尔曼福特算法](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)。

按照以下步骤解决问题:

*   将一个边的**容量和该边**的**成本存储在两个独立的数组中。**
*   给定源节点 **S** 和宿节点 **T** 、拾取边 **p <sub>i</sub>** 、需求节点 **d <sub>a</sub>** 以及节点之间的距离 **dist** ，搜索是否可能有从 **S** 到 **T** 的流动。
*   如果存在流量，计算距离，**值= dist+pi–pi[k]–成本[k]** 。
*   将 **dist[ ]** 中的距离值与**值**进行比较，并持续更新，直到获得**最小流量**。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;

public class MinCostMaxFlow {

    // Stores the found edges
    boolean found[];

    // Stores the number of nodes
    int N;

    // Stores the capacity
    // of each edge
    int cap[][];

    int flow[][];

    // Stores the cost per
    // unit flow of each edge
    int cost[][];

    // Stores the distance from each node
    // and picked edges for each node
    int dad[], dist[], pi[];

    static final int INF
        = Integer.MAX_VALUE / 2 - 1;

    // Function to check if it is possible to
    // have a flow from the src to sink
    boolean search(int src, int sink)
    {

        // Initialise found[] to false
        Arrays.fill(found, false);

        // Initialise the dist[] to INF
        Arrays.fill(dist, INF);

        // Distance from the source node
        dist[src] = 0;

        // Iterate untill src reaches N
        while (src != N) {

            int best = N;
            found[src] = true;

            for (int k = 0; k < N; k++) {

                // If already found
                if (found[k])
                    continue;

                // Evaluate while flow
                // is still in supply
                if (flow[k][src] != 0) {

                    // Obtain the total value
                    int val
                        = dist[src] + pi[src]
                          - pi[k] - cost[k][src];

                    // If dist[k] is > minimum value
                    if (dist[k] > val) {

                        // Update
                        dist[k] = val;
                        dad[k] = src;
                    }
                }

                if (flow[src][k] < cap[src][k]) {

                    int val = dist[src] + pi[src]
                              - pi[k] + cost[src][k];

                    // If dist[k] is > minimum value
                    if (dist[k] > val) {

                        // Update
                        dist[k] = val;
                        dad[k] = src;
                    }
                }

                if (dist[k] < dist[best])
                    best = k;
            }

            // Update src to best for
            // next iteration
            src = best;
        }

        for (int k = 0; k < N; k++)
            pi[k]
                = Math.min(pi[k] + dist[k],
                           INF);

        // Return the value obtained at sink
        return found[sink];
    }

    // Function to obtain the maximum Flow
    int[] getMaxFlow(int cap[][], int cost[][],
                     int src, int sink)
    {

        this.cap = cap;
        this.cost = cost;

        N = cap.length;
        found = new boolean[N];
        flow = new int[N][N];
        dist = new int[N + 1];
        dad = new int[N];
        pi = new int[N];

        int totflow = 0, totcost = 0;

        // If a path exist from src to sink
        while (search(src, sink)) {

            // Set the default amount
            int amt = INF;
            for (int x = sink; x != src; x = dad[x])

                amt = Math.min(amt,
                               flow[x][dad[x]] != 0
                                   ? flow[x][dad[x]]
                                   : cap[dad[x]][x]
                                         - flow[dad[x]][x]);

            for (int x = sink; x != src; x = dad[x]) {

                if (flow[x][dad[x]] != 0) {
                    flow[x][dad[x]] -= amt;
                    totcost -= amt * cost[x][dad[x]];
                }
                else {
                    flow[dad[x]][x] += amt;
                    totcost += amt * cost[dad[x]][x];
                }
            }
            totflow += amt;
        }

        // Return pair total cost and sink
        return new int[] { totflow, totcost };
    }

    // Driver Code
    public static void main(String args[])
    {

        // Creating an object flow
        MinCostMaxFlow flow = new MinCostMaxFlow();

        int s = 0, t = 4;

        int cap[][] = { { 0, 3, 1, 0, 3 },
                        { 0, 0, 2, 0, 0 },
                        { 0, 0, 0, 1, 6 },
                        { 0, 0, 0, 0, 2 },
                        { 0, 0, 0, 0, 0 } };

        int cost[][] = { { 0, 1, 0, 0, 2 },
                         { 0, 0, 0, 3, 0 },
                         { 0, 0, 0, 0, 0 },
                         { 0, 0, 0, 0, 1 },
                         { 0, 0, 0, 0, 0 } };

        int ret[] = flow.getMaxFlow(cap, cost, s, t);

        System.out.println(ret[0] + " " + ret[1]);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from sys import maxsize
from typing import List

# Stores the found edges
found = []

# Stores the number of nodes
N = 0

# Stores the capacity
# of each edge
cap = []

flow = []

# Stores the cost per
# unit flow of each edge
cost = []

# Stores the distance from each node
# and picked edges for each node
dad = []
dist = []
pi = []

INF = maxsize // 2 - 1

# Function to check if it is possible to
# have a flow from the src to sink
def search(src: int, sink: int) -> bool:

    # Initialise found[] to false
    found = [False for _ in range(N)]

    # Initialise the dist[] to INF
    dist = [INF for _ in range(N + 1)]

    # Distance from the source node
    dist[src] = 0

    # Iterate untill src reaches N
    while (src != N):
        best = N
        found[src] = True

        for k in range(N):

            # If already found
            if (found[k]):
                continue

            # Evaluate while flow
            # is still in supply
            if (flow[k][src] != 0):

                # Obtain the total value
                val = (dist[src] + pi[src] -
                           pi[k] - cost[k][src])

                # If dist[k] is > minimum value
                if (dist[k] > val):

                    # Update
                    dist[k] = val
                    dad[k] = src

            if (flow[src][k] < cap[src][k]):
                val = (dist[src] + pi[src] -
                           pi[k] + cost[src][k])

                # If dist[k] is > minimum value
                if (dist[k] > val):

                    # Update
                    dist[k] = val
                    dad[k] = src

            if (dist[k] < dist[best]):
                best = k

        # Update src to best for
        # next iteration
        src = best

    for k in range(N):
        pi[k] = min(pi[k] + dist[k], INF)

    # Return the value obtained at sink
    return found[sink]

# Function to obtain the maximum Flow
def getMaxFlow(capi: List[List[int]],
              costi: List[List[int]],
              src: int, sink: int) -> List[int]:

    global cap, cost, found, dist, pi, N, flow, dad
    cap = capi
    cost = costi

    N = len(capi)
    found = [False for _ in range(N)]
    flow = [[0 for _ in range(N)]
               for _ in range(N)]
    dist = [INF for _ in range(N + 1)]
    dad = [0 for _ in range(N)]
    pi = [0 for _ in range(N)]

    totflow = 0
    totcost = 0

    # If a path exist from src to sink
    while (search(src, sink)):

        # Set the default amount
        amt = INF
        x = sink

        while x != src:
            amt = min(
                amt, flow[x][dad[x]] if
                (flow[x][dad[x]] != 0) else
                  cap[dad[x]][x] - flow[dad[x]][x])
            x = dad[x]

        x = sink

        while x != src:
            if (flow[x][dad[x]] != 0):
                flow[x][dad[x]] -= amt
                totcost -= amt * cost[x][dad[x]]

            else:
                flow[dad[x]][x] += amt
                totcost += amt * cost[dad[x]][x]

            x = dad[x]

        totflow += amt

    # Return pair total cost and sink
    return [totflow, totcost]

# Driver Code
if __name__ == "__main__":

    s = 0
    t = 4

    cap = [ [ 0, 3, 1, 0, 3 ],
            [ 0, 0, 2, 0, 0 ],
            [ 0, 0, 0, 1, 6 ],
            [ 0, 0, 0, 0, 2 ],
            [ 0, 0, 0, 0, 0 ] ]

    cost = [ [ 0, 1, 0, 0, 2 ],
             [ 0, 0, 0, 3, 0 ],
             [ 0, 0, 0, 0, 0 ],
             [ 0, 0, 0, 0, 1 ],
             [ 0, 0, 0, 0, 0 ] ]

    ret = getMaxFlow(cap, cost, s, t)

    print("{} {}".format(ret[0], ret[1]))

# This code is contributed by sanjeev2552
```

**Output:** 

```
6 8
```

***时间复杂度:** O(V <sup>2</sup> * E <sup>2</sup> )其中 V 为顶点数，E 为边数。*
***辅助空间:** O(V)*