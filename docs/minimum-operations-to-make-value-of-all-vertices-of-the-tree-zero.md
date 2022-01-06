# 使树的所有顶点的值为零的最小运算

> 原文:[https://www . geesforgeks . org/最小操作使树的所有顶点的值为零/](https://www.geeksforgeeks.org/minimum-operations-to-make-value-of-all-vertices-of-the-tree-zero/)

给定一棵树，其中每个顶点都存储了一个值。任务是找到使存储在树的所有顶点中的值等于零所需的最小操作数。
每个操作包括以下 2 个步骤:

1.  选择一个子树，使子树包含顶点 1。
2.  将子树的所有顶点的值增加/减少 1。

**考虑以下树** :

![](img/f078298a607b16ce8e70a9a3f7c36118.png)

**注**:顶点中的数字表示顶点数，A[V]表示顶点的值，如上所述。
对于下面的树，我们执行以下 3 个操作，使所有顶点
的值等于零:

![](img/8c8cddce8616f23445570982c6a3ebe5.png)

**注**:黑色的顶点代表选中的子树。
我们可以用动态规划来解决这个问题。
让 dp[i][0]表示选择任何以 **i** 为根的子树的操作数，所有顶点的值增加 1。
类似地，dp[i][1]表示选择以 **i** 为根的任何子树并且所有顶点的值减少 1 的操作数。
对于所有的叶子，我们可以很容易地计算出 dp[i][0]和 dp[i][1]如果说一个叶子节点 V 是这样的，对于某个叶子节点 U A[V]= 0，即 dp[i][1] = A[V]和 dp[i][0] = 0
现在如果我们在某个非叶子节点比如说 V，我们看它的所有子节点， 如果对 V 的子节点 I 应用 X <sub>i</sub> 次增加操作，那么我们需要对节点 V 的所有子节点 I 应用 max(X <sub>i</sub> ，对以 V 为根的任何子树进行增加操作。同样，我们对节点 V 的减少操作也是如此。
答案是节点 1 的增加和减少操作的总和，因为这些操作只应用于具有节点 1 的子树。
以下是上述方法的实施:

## C++

```
// CPP program to find the Minimum Operations
// to modify values of all tree vertices to zero
#include <bits/stdc++.h>

using namespace std;

// A utility function to add an edge in an
// undirected graph
void addEdge(vector<int> adj[], int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// A utility function to print the adjacency list
// representation of graph
void printGraph(vector<int> adj[], int V)
{
    for (int v = 0; v < V; ++v) {
        cout << "\n Adjacency list of vertex "
             << v << "\n head ";
        for (auto x : adj[v])
            cout << "-> " << x;
        printf("\n");
    }
}

// Utility Function for findMinOperation()
void findMinOperationUtil(int dp[][2], vector<int> adj[],
                          int A[], int src, int parent)
{
    // Base Case for current node
    dp[src][0] = dp[src][1] = 0;

    // iterate over the adjacency list for src
    for (auto V : adj[src]) {
        if (V == parent)
            continue;

        // calculate DP table for each child V
        findMinOperationUtil(dp, adj, A, V, src);

        // Number of Increase Type operations for node src
        // is equal to maximum of number of increase operations
        // required by each of its child
        dp[src][0] = max(dp[src][0], dp[V][0]);

        // Number of Decrease Type operations for node src
        // is equal to maximum of number of decrease operations
        // required by each of its child
        dp[src][1] = max(dp[src][1], dp[V][1]);
    }

    // After performing operations for subtree rooted at src
    // A[src] changes by the net difference of increase and
    // decrease type operations
    A[src - 1] += dp[src][0] - dp[src][1];

    // for negative value of node src
    if (A[src - 1] > 0) {
        dp[src][1] += A[src - 1];
    }
    else {
        dp[src][0] += abs(A[src - 1]);
    }
}

// Returns the minimum operations required to make
// value of all vertices equal to zero, uses
// findMinOperationUtil()
int findMinOperation(vector<int> adj[], int A[], int V)
{

    // Initialise DP table
    int dp[V + 1][2];
    memset(dp, 0, sizeof dp);

    // find dp[1][0] and dp[1][1]
    findMinOperationUtil(dp, adj, A, 1, 0);

    int minOperations = dp[1][0] + dp[1][1];
    return minOperations;
}

// Driver code
int main()
{
    int V = 5;

    // Build the Graph/Tree
    vector<int> adj[V + 1];
    addEdge(adj, 1, 2);
    addEdge(adj, 1, 3);

    int A[] = { 1, -1, 1 };
    int minOperations = findMinOperation(adj, A, V);
    cout << minOperations;

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find the Minimum Operations
# to modify values of all tree vertices to zero

# A utility function to add an
# edge in an undirected graph
def addEdge(adj, u, v):

    adj[u].append(v)
    adj[v].append(u)

# A utility function to print the adjacency
# list representation of graph
def printGraph(adj, V):

    for v in range(0, V):
        print("Adjacency list of vertex", v)
        print("head", end = " ")

        for x in adj[v]:
            print("->", x, end = "")
        print()

# Utility Function for findMinOperation()
def findMinOperationUtil(dp, adj, A, src, parent):

    # Base Case for current node
    dp[src][0] = dp[src][1] = 0

    # Iterate over the adjacency list for src
    for V in adj[src]:
        if V == parent:
            continue

        # calculate DP table for each child V
        findMinOperationUtil(dp, adj, A, V, src)

        # Number of Increase Type operations for node src
        # is equal to maximum of number of increase operations
        # required by each of its child
        dp[src][0] = max(dp[src][0], dp[V][0])

        # Number of Decrease Type operations for node
        # src is equal to maximum of number of decrease
        # operations required by each of its child
        dp[src][1] = max(dp[src][1], dp[V][1])

    # After performing operations for subtree rooted
    # at src A[src] changes by the net difference of
    # increase and decrease type operations
    A[src - 1] += dp[src][0] - dp[src][1]

    # for negative value of node src
    if A[src - 1] > 0:
        dp[src][1] += A[src - 1]

    else:
        dp[src][0] += abs(A[src - 1])

# Returns the minimum operations required to
# make value of all vertices equal to zero,
# uses findMinOperationUtil()
def findMinOperation(adj, A, V):

    # Initialise DP table
    dp = [[0, 0] for i in range(V + 1)]

    # find dp[1][0] and dp[1][1]
    findMinOperationUtil(dp, adj, A, 1, 0)

    minOperations = dp[1][0] + dp[1][1]
    return minOperations

# Driver code
if __name__ == "__main__":

    V = 5

    # Build the Graph/Tree
    adj = [[] for i in range(V + 1)]
    addEdge(adj, 1, 2)
    addEdge(adj, 1, 3)

    A = [1, -1, 1]
    minOperations = findMinOperation(adj, A, V)
    print(minOperations)

# This code is contributed by Rituraj Jain
```

## java 描述语言

```
<script>

// JavaScript program to find the Minimum Operations
// to modify values of all tree vertices to zero

// A utility function to add an edge in an
// undirected graph
function addEdge(adj, u, v)
{
    adj[u].push(v);
    adj[v].push(u);
}

// A utility function to print the adjacency list
// representation of graph
function printGraph(adj, V)
{
    for(var v = 0; v < V; ++v) {
        document.write( "<br> Adjacency list of vertex "
            + v+ "<br> head ");
        for (var x of adj[v])
            document.write("-> "+ x);
        document.write("<br>");
    }
}

// Utility Function for findMinOperation()
function findMinOperationUtil(dp, adj, A, src, parent)
{
    // Base Case for current node
    dp[src][0] = dp[src][1] = 0;

    // iterate over the adjacency list for src
    for (var V of adj[src]) {
        if (V == parent)
            continue;

        // calculate DP table for each child V
        findMinOperationUtil(dp, adj, A, V, src);

        // Number of Increase Type operations for node src
        // is equal to maximum of number of increase operations
        // required by each of its child
        dp[src][0] = Math.max(dp[src][0], dp[V][0]);

        // Number of Decrease Type operations for node src
        // is equal to maximum of number of decrease operations
        // required by each of its child
        dp[src][1] = Math.max(dp[src][1], dp[V][1]);
    }

    // After performing operations for subtree rooted at src
    // A[src] changes by the net difference of increase and
    // decrease type operations
    A[src - 1] += dp[src][0] - dp[src][1];

    // for negative value of node src
    if (A[src - 1] > 0) {
        dp[src][1] += A[src - 1];
    }
    else {
        dp[src][0] += Math.abs(A[src - 1]);
    }
}

// Returns the minimum operations required to make
// value of all vertices equal to zero, uses
// findMinOperationUtil()
function findMinOperation(adj, A, V)
{

    // Initialise DP table
    var dp = Array.from(Array(V+1), ()=>Array(2).fill(0));

    // find dp[1][0] and dp[1][1]
    findMinOperationUtil(dp, adj, A, 1, 0);

    var minOperations = dp[1][0] + dp[1][1];
    return minOperations;
}

// Driver code

var V = 5;

// Build the Graph/Tree
var adj = Array.from(Array(V+1), ()=>Array());
addEdge(adj, 1, 2);
addEdge(adj, 1, 3);
var A = [1, -1, 1];
var minOperations = findMinOperation(adj, A, V);
document.write( minOperations);

</script>
```

**Output:** 

```
3
```

**时间复杂度** : O(V)，其中 V 为树中节点数。
**辅助空间** : O(V)，其中 V 为树中节点数。