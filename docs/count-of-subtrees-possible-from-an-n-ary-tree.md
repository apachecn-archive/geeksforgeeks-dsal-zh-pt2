# N 元树中可能的子树的数量

> 原文:[https://www . geesforgeks . org/子树计数-可能来自 n 元树/](https://www.geeksforgeeks.org/count-of-subtrees-possible-from-an-n-ary-tree/)

给定由具有值 **0** 到**(N–1)**的 **N** 节点组成的 [N 元树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)，任务是找到给定树中存在的[子树](https://www.geeksforgeeks.org/sub-tree-nodes-tree-using-dfs/)的总数。由于计数可能很大，所以打印**计数** [模 100000007](https://www.geeksforgeeks.org/modulo-1097-1000000007/)。

**示例:**

> **输入:**N = 3
> 0
> /
> 1
> /
> 2
> **输出:** 7
> **说明:**
> 子树节点总数为{}、{0}、{1}、{2}、{0，1}、{1，2}、{0，1，2}。
> 
> **输入:**N = 2
> 0
> /
> 1
> T6】输出: 4

**方法:**解决给定问题的方法是在给定的树上执行 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)。按照以下步骤解决问题:

*   初始化一个变量，比如说**计数**为 **0** ，以存储给定树中存在的子树总数的计数。
*   声明一个函数 **DFS(int src，int parent)** 来计算节点 **src** 的子树数量，并执行以下操作:
    *   初始化一个变量，说 **res** 为 **1** 。
    *   遍历当前节点的[邻接表](https://www.geeksforgeeks.org/graph-and-its-representations/)，如果[邻接表](https://www.geeksforgeeks.org/graph-and-its-representations/)中的节点，说 **X** 和**父**节点不一样，那么[递归调用](https://www.geeksforgeeks.org/recursion/)节点的 DFS 函数 **X** 和节点 **src** 作为**父**节点作为 **DFS(X，src)** 。
    *   让返回到上述递归调用的值为**值**，然后将 **res** 的值更新为 **(res *(值+ 1)) % (10 <sup>9</sup> + 7)** 。
    *   将**的值更新为**(计数+ res) % (10 <sup>9</sup> + 7)** 。**
    *   从每次递归调用中返回 **res** 的值。
*   为根节点 **1** 调用函数 **DFS()** 。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
#define MAX 300004
using namespace std;

// Adjacency list to
// represent the graph
vector<int> graph[MAX];
int mod = 1e9 + 7;

// Stores the count of subtrees
// possible from given N-ary Tree
int ans = 0;

// Utility function to count the number of
// subtrees possible from given N-ary Tree
int countSubtreesUtil(int cur, int par)
{
    // Stores the count of subtrees
    // when cur node is the root
    int res = 1;

    // Traverse the adjacency list
    for (int i = 0;
         i < graph[cur].size(); i++) {

        // Iterate over every ancestor
        int v = graph[cur][i];

        if (v == par)
            continue;

        // Calculate product of the number
        // of subtrees for each child node
        res = (res
               * (countSubtreesUtil(
                      v, cur)
                  + 1))
              % mod;
    }

    // Update the value of ans
    ans = (ans + res) % mod;

    // Return the resultant count
    return res;
}

// Function to count the number of
// subtrees in the given tree
void countSubtrees(int N,
                   vector<pair<int, int> >& adj)
{
    // Initialize an adjacency matrix
    for (int i = 0; i < N - 1; i++) {
        int a = adj[i].first;
        int b = adj[i].second;

        // Add the edges
        graph[a].push_back(b);
        graph[b].push_back(a);
    }

    // Function Call to count the
    // number of subtrees possible
    countSubtreesUtil(1, 1);

    // Print count of subtrees
    cout << ans + 1;
}

// Driver Code
int main()
{
    int N = 3;

    vector<pair<int, int> > adj
        = { { 0, 1 }, { 1, 2 } };

    countSubtrees(N, adj);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of above approach
import java.util.*;

class GFG{

static int MAX = 300004;

// Adjacency list to
// represent the graph
static ArrayList<ArrayList<Integer>> graph;
static long mod = (long)1e9 + 7;

// Stores the count of subtrees
// possible from given N-ary Tree
static int ans = 0;

// Utility function to count the number of
// subtrees possible from given N-ary Tree
static int countSubtreesUtil(int cur, int par)
{

    // Stores the count of subtrees
    // when cur node is the root
    int res = 1;

    // Traverse the adjacency list
    for(int i = 0;
            i < graph.get(cur).size(); i++)
    {

        // Iterate over every ancestor
        int v = graph.get(cur).get(i);

        if (v == par)
            continue;

        // Calculate product of the number
        // of subtrees for each child node
        res = (int)((res * (countSubtreesUtil(
                 v, cur) + 1)) % mod);
    }

    // Update the value of ans
    ans = (int)((ans + res) % mod);

    // Return the resultant count
    return res;
}

// Function to count the number of
// subtrees in the given tree
static void countSubtrees(int N, int[][] adj)
{

    // Initialize an adjacency matrix
    for(int i = 0; i < N - 1; i++)
    {
        int a = adj[i][0];
        int b = adj[i][1];

        // Add the edges
        graph.get(a).add(b);
        graph.get(b).add(a);
    }

    // Function Call to count the
    // number of subtrees possible
    countSubtreesUtil(1, 1);

    // Print count of subtrees
   System.out.println(ans + 1);
}

// Driver code
public static void main(String[] args)
{
    int N = 3;

    int[][] adj = { { 0, 1 }, { 1, 2 } };

    graph = new ArrayList<>();

    for(int i = 0; i < MAX; i++)
        graph.add(new ArrayList<>());

    countSubtrees(N, adj);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program of the above approach
MAX = 300004

# Adjacency list to
# represent the graph
graph = [[] for i in range(MAX)]
mod = 10**9 + 7

# Stores the count of subtrees
# possible from given N-ary Tree
ans = 0

# Utility function to count the number of
# subtrees possible from given N-ary Tree
def countSubtreesUtil(cur, par):
    global mod, ans

    # Stores the count of subtrees
    # when cur node is the root
    res = 1

    # Traverse the adjacency list
    for i in range(len(graph[cur])):

        # Iterate over every ancestor
        v = graph[cur][i]

        if (v == par):
            continue

        # Calculate product of the number
        # of subtrees for each child node
        res = (res * (countSubtreesUtil(v, cur)+ 1)) % mod

    # Update the value of ans
    ans = (ans + res) % mod

    # Return the resultant count
    return res

# Function to count the number of
# subtrees in the given tree
def countSubtrees(N, adj):

    # Initialize an adjacency matrix
    for i in range(N-1):
        a = adj[i][0]
        b = adj[i][1]

        # Add the edges
        graph[a].append(b)
        graph[b].append(a)

    # Function Call to count the
    # number of subtrees possible
    countSubtreesUtil(1, 1)

    # Prcount of subtrees
    print (ans + 1)

# Driver Code
if __name__ == '__main__':
    N = 3

    adj = [ [ 0, 1 ], [ 1, 2 ] ]

    countSubtrees(N, adj)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program of above approach
using System;
using System.Collections.Generic;

public class GFG
{

    static int MAX = 300004;

    // Adjacency list to
    // represent the graph
    static List<List<int>> graph;
    static long mod = (long) 1e9 + 7;

    // Stores the count of subtrees
    // possible from given N-ary Tree
    static int ans = 0;

    // Utility function to count the number of
    // subtrees possible from given N-ary Tree
    static int countSubtreesUtil(int cur, int par) {

        // Stores the count of subtrees
        // when cur node is the root
        int res = 1;

        // Traverse the adjacency list
        for (int i = 0; i < graph[cur].Count; i++) {

            // Iterate over every ancestor
            int v = graph[cur][i];

            if (v == par)
                continue;

            // Calculate product of the number
            // of subtrees for each child node
            res = (int) ((res * (countSubtreesUtil(v, cur) + 1)) % mod);
        }

        // Update the value of ans
        ans = (int) ((ans + res) % mod);

        // Return the resultant count
        return res;
    }

    // Function to count the number of
    // subtrees in the given tree
    static void countSubtrees(int N, int[,] adj) {

        // Initialize an adjacency matrix
        for (int i = 0; i < N - 1; i++) {
            int a = adj[i,0];
            int b = adj[i,1];

            // Add the edges
            graph[a].Add(b);
            graph[b].Add(a);
        }

        // Function Call to count the
        // number of subtrees possible
        countSubtreesUtil(1, 1);

        // Print count of subtrees
        Console.WriteLine(ans + 1);
    }

    // Driver code
    public static void Main(String[] args) {
        int N = 3;

        int[,] adj = { { 0, 1 }, { 1, 2 } };

        graph = new List<List<int>>();

for (int i = 0; i < MAX; i++)
            graph.Add(new List<int>());
        countSubtrees(N, adj);
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program of the above approach

var MAX = 300004;

// Adjacency list to
// represent the graph
var graph = Array.from(Array(MAX),()=>new Array());
var mod = 1000000007;

// Stores the count of subtrees
// possible from given N-ary Tree
var ans = 0;

// Utility function to count the number of
// subtrees possible from given N-ary Tree
function countSubtreesUtil(cur, par)
{
    // Stores the count of subtrees
    // when cur node is the root
    var res = 1;

    // Traverse the adjacency list
    for (var i = 0;
         i < graph[cur].length; i++) {

        // Iterate over every ancestor
        var v = graph[cur][i];

        if (v == par)
            continue;

        // Calculate product of the number
        // of subtrees for each child node
        res = (res
               * (countSubtreesUtil(
                      v, cur)
                  + 1))
              % mod;
    }

    // Update the value of ans
    ans = (ans + res) % mod;

    // Return the resultant count
    return res;
}

// Function to count the number of
// subtrees in the given tree
function countSubtrees(N, adj)
{
    // Initialize an adjacency matrix
    for (var i = 0; i < N - 1; i++) {
        var a = adj[i][0];
        var b = adj[i][1];

        // Add the edges
        graph[a].push(b);
        graph[b].push(a);
    }

    // Function Call to count the
    // number of subtrees possible
    countSubtreesUtil(1, 1);

    // Print count of subtrees
    document.write( ans + 1);
}

// Driver Code
var N = 3;
var adj
    = [[ 0, 1 ], [1, 2 ]];
countSubtrees(N, adj);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)