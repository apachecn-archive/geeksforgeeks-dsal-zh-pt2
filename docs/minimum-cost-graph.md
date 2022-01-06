# 最小成本图

> 原文:[https://www.geeksforgeeks.org/minimum-cost-graph/](https://www.geeksforgeeks.org/minimum-cost-graph/)

给定二维平面上表示为 **(x <sub>i</sub> 、y <sub>i</sub> )** 的 N 个节点。如果节点之间的曼哈顿距离为 **1** ，则称这些节点是相连的。您可以连接两个没有连接的节点，代价是它们之间的欧氏距离。任务是连接图，使得每个节点都有一条从任何节点开始的最小代价的路径。

**示例:**

> **输入:** N = 3，边[][] = {{1，1}，{1，1}，{2，2}，{3，2}}
> **输出:** 1.41421
> 因为(2，2)和(2，3)已经连接。
> 所以我们尝试将(1，1)与(2，2)
> 连接，或者将(1，1)与(2，3)连接，但是将(1，1)与(2，2)
> 连接会产生最小的成本。
> 
> **输入:** N = 3，边[][] = {{1，1}，{2，2}，{3，3 } }
> T3】输出: 2.82843

**方法:**强力方法是将每一个节点与每一个其他节点连接起来，对于其他 **N** 节点也是如此，但是在最坏的情况下，时间复杂度将是 **N <sup>N</sup>** 。
另一种方法是用欧氏距离求每一对顶点的代价，那些连通的顶点对的代价为 **0** 。
在知道每对的成本后，我们将对最小生成树应用 [Kruskal 算法](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/)，它将产生连接图的最小成本。请注意，对于 Kruskal 算法，您必须具备[不相交集并(DSU)](https://www.geeksforgeeks.org/disjoint-set-data-structures/) 的知识。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Max number of nodes given
const int N = 500 + 10;

// arr is the parent array
// sz is the size of the
// subtree in DSU
int arr[N], sz[N];

// Function to initialize the parent
// and size array for DSU
void initialize()
{
    for (int i = 1; i < N; ++i) {
        arr[i] = i;
        sz[i] = 1;
    }
}

// Function to return the
// parent of the node
int root(int i)
{
    while (arr[i] != i)
        i = arr[i];
    return i;
}

// Function to perform the
// merge operation
void Union(int a, int b)
{
    a = root(a);
    b = root(b);

    if (a != b) {
        if (sz[a] < sz[b])
            swap(a, b);

        sz[a] += sz[b];
        arr[b] = a;
    }
}

// Function to return the minimum cost required
double minCost(vector<pair<int, int> >& p)
{

    // Number of points
    int n = (int)p.size();

    // To store the cost of every possible pair
    // as { cost, {to, from}}.
    vector<pair<double, pair<int, int> > > cost;

    // Calculating the cost of every possible pair
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            if (i != j) {

                // Getting Manhattan distance
                int x = abs(p[i].first - p[j].first)
                        + abs(p[i].second - p[j].second);

                // If the distance is 1 the cost is 0
                // or already connected
                if (x == 1) {
                    cost.push_back({ 0, { i + 1, j + 1 } });
                    cost.push_back({ 0, { j + 1, i + 1 } });
                }
                else {

                    // Calculating the euclidean distance
                    int a = p[i].first - p[j].first;
                    int b = p[i].second - p[j].second;
                    a *= a;
                    b *= b;
                    double d = sqrt(a + b);
                    cost.push_back({ d, { i + 1, j + 1 } });
                    cost.push_back({ d, { j + 1, i + 1 } });
                }
            }
        }
    }

    // Krushkal Algorithm for Minimum
    // spanning tree
    sort(cost.begin(), cost.end());

    // To initialize the size and
    // parent array
    initialize();

    double ans = 0.00;
    for (auto i : cost) {
        double c = i.first;
        int a = i.second.first;
        int b = i.second.second;

        // If the parents are different
        if (root(a) != root(b)) {
            Union(a, b);
            ans += c;
        }
    }

    return ans;
}

// Driver code
int main()
{

    // Vector pairs of points
    vector<pair<int, int> > points = {
        { 1, 1 },
        { 2, 2 },
        { 2, 3 }
    };

    // Function calling and printing
    // the answer
    cout << minCost(points);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

// Max number of nodes given
static int N = 500 + 10;

static class pair
{
    double c;
    int first, second;

    pair(double c, int first, int second)
    {
        this.c = c;
        this.first = first;
        this.second = second;
    }
}

// arr is the parent array
// sz is the size of the
// subtree in DSU
static int[] arr = new int[N],
              sz = new int[N];

// Function to initialize the parent
// and size array for DSU
static void initialize()
{
    for(int i = 1; i < N; ++i)
    {
        arr[i] = i;
        sz[i] = 1;
    }
}

// Function to return the
// parent of the node
static int root(int i)
{
    while (arr[i] != i)
        i = arr[i];

    return i;
}

// Function to perform the
// merge operation
static void union(int a, int b)
{
    a = root(a);
    b = root(b);

    if (a != b)
    {
        if (sz[a] < sz[b])
        {
            int tmp = a;
            a = b;
            b = tmp;
        }

        sz[a] += sz[b];
        arr[b] = a;
    }
}

// Function to return the minimum
// cost required
static double minCost(int[][] p)
{

    // Number of points
    int n = (int)p.length;

    // To store the cost of every possible pair
    // as { cost, {to, from}}.
    ArrayList<pair> cost = new ArrayList<>();

    // Calculating the cost of every possible pair
    for(int i = 0; i < n; ++i)
    {
        for(int j = 0; j < n; ++j)
        {
            if (i != j)
            {

                // Getting Manhattan distance
                int x = Math.abs(p[i][0] - p[j][0]) +
                        Math.abs(p[i][1] - p[j][1]);

                // If the distance is 1 the cost is 0
                // or already connected
                if (x == 1)
                {
                    cost.add(new pair( 0, i + 1,
                                          j + 1 ));
                    cost.add(new pair( 0, j + 1,
                                          i + 1 ));
                }
                else
                {

                    // Calculating the euclidean
                    // distance
                    int a = p[i][0] - p[j][0];
                    int b = p[i][1] - p[j][1];
                    a *= a;
                    b *= b;

                    double d = Math.sqrt(a + b);
                    cost.add(new pair(d, i + 1,
                                         j + 1 ));
                    cost.add(new pair(d, j + 1,
                                         i + 1));
                }
            }
        }
    }

    // Krushkal Algorithm for Minimum
    // spanning tree
    Collections.sort(cost, new Comparator<>()
    {
        public int compare(pair a, pair b)
        {
            if(a.c <= b.c)
                return -1;
            else
                return 1;
        }
    });

    // To initialize the size and
    // parent array
    initialize();

    double ans = 0.00;
    for(pair i : cost)
    {
        double c = i.c;
        int a = i.first;
        int b = i.second;

        // If the parents are different
        if (root(a) != root(b))
        {
            union(a, b);
            ans += c;
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{

    // Vector pairs of points
    int[][] points = { { 1, 1 },
                       { 2, 2 },
                       { 2, 3 }};

    // Function calling and printing
    // the answer
    System.out.format("%.5f", minCost(points));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Max number of nodes given
N = 500 + 10

# arr is the parent array
# sz is the size of the
# subtree in DSU
arr = [i for i in range(N)]
sz = [0] * N

# Function to return the
# parent of the node
def root(i):
    while arr[i] != i:
        i = arr[i]
    return i

# Function to perform the
# merge operation
def Union(a, b):
    a = root(a)
    b = root(b)

    if a != b:
        if sz[a] < sz[b]:
            a, b = b, a

        sz[a] += sz[b]
        arr[b] = a

# Function to return the minimum cost required
def minCost():
    global points
    # Number of points
    n = len(points)

    # To store the cost of every possible pair
    # as : cost, :to, from.
    cost = []

    # Calculating the cost of every possible pair
    for i in range(n):
        for j in range(n):
            if i != j:

                # Getting Manhattan distance
                x = abs(points[i][0] - points[j][0]) + abs(points[i][1] - points[j][1])

                # If the distance is 1 the cost is 0
                # or already connected
                if x == 1:
                    cost.append((0, (i + 1, j + 1)))
                    cost.append((0, (j + 1, i + 1)))

                else:

                    # Calculating the euclidean distance
                    a = points[i][0] - points[j][0]
                    b = points[i][1] - points[j][1]
                    a *= a
                    b *= b
                    d = (a + b)**0.5
                    cost.append((d, (i + 1, j + 1)))
                    cost.append((d, (j + 1, i + 1)))

    # Krushkal Algorithm for Minimum
    # spanning tree
    cost.sort()

    ans = 0.00
    for i in cost:
        c = i[0]
        a = i[1][0]
        b = i[1][1]

        # If the parents are different
        if root(a) != root(b):
            Union(a, b)
            ans += c

    return ans

# Driver code
if __name__ == "__main__":

    # Vector pairs of points
    points = [(1, 1), (2, 2), (2, 3)]

    # Function calling and printing
    # the answer
    print(minCost())
```

**Output:** 

```
1.41421
```

**时间复杂度:**O(N * N)
T3】辅助空间: O(N*N)