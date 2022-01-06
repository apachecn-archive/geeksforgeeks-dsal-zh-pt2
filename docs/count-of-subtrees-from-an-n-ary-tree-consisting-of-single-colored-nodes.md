# 由单一颜色节点组成的 N 元树的子树计数

> 原文:[https://www . geesforgeks . org/由单色节点组成的 n 元树的子树计数/](https://www.geeksforgeeks.org/count-of-subtrees-from-an-n-ary-tree-consisting-of-single-colored-nodes/)

给定由 **N** 节点组成的 [N 元树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)和由表单 **(X，Y)** 的**N–1**条边组成的矩阵**边【】【】**表示节点 **X** 和节点 **Y** 之间的边，以及由值:
组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**col【】**

*   **0:** 未着色节点。
*   **1:** 红色节点。
*   **2:** 蓝色节点。

任务是找到给定树的子树的数量，该树仅由单色节点组成。
**例:**

> **输入:**
> N = 5，col[] = {2，0，0，1，2}，
> 边[][] = {{1，2}，{2，3}，{2，4}，{2，5}}
> **输出:** 1
> **解释:**
> 节点 4 的子树为{4}没有蓝色顶点，只包含一个红色顶点。
> **输入:**
> N = 5，col[] = {1，0，0，0，2}，
> 边[][] = {{1，2}，{2，3}，{3，4}，{4，5}}
> **输出:** 4
> **说明:**
> 下面是给定属性的子树:
> 
> 1.  根节点值为 2 {2，3，4，5}的子树
> 2.  根节点值为 3 {3，4，5}的子树
> 3.  根节点值为 4 {4，5}的子树
> 4.  根节点值为 5 {5}的子树

**方法:**给定的问题可以使用[深度优先搜索遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)来解决。其思想是使用给定树的 DFS 计算每个子树中红色和蓝色节点的数量。一旦计算出来，计算只包含**蓝色**彩色节点和只包含**红色**彩色节点的子树的数量。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to implement DFS traversal
void Solution_dfs(int v, int color[], int red,
                  int blue, int* sub_red,
                  int* sub_blue, int* vis,
                  map<int, vector<int> >& adj,
                  int* ans)
{

    // Mark node v as visited
    vis[v] = 1;

    // Traverse Adj_List of node v
    for (int i = 0; i < adj[v].size();
         i++) {

        // If current node is not visited
        if (vis[adj[v][i]] == 0) {

            // DFS call for current node
            Solution_dfs(adj[v][i], color,
                         red, blue,
                         sub_red, sub_blue,
                         vis, adj, ans);

            // Count the total red and blue
            // nodes of children of its subtree
            sub_red[v] += sub_red[adj[v][i]];
            sub_blue[v] += sub_blue[adj[v][i]];
        }
    }

    if (color[v] == 1) {
        sub_red[v]++;
    }

    // Count the no. of red and blue
    // nodes in the subtree
    if (color[v] == 2) {
        sub_blue[v]++;
    }

    // If subtree contains all
    // red node & no blue node
    if (sub_red[v] == red
        && sub_blue[v] == 0) {
        (*ans)++;
    }

    // If subtree contains all
    // blue node & no red node
    if (sub_red[v] == 0
        && sub_blue[v] == blue) {
        (*ans)++;
    }
}

// Function to count the number of
// nodes with red color
int countRed(int color[], int n)
{
    int red = 0;
    for (int i = 0; i < n; i++) {
        if (color[i] == 1)
            red++;
    }
    return red;
}

// Function to count the number of
// nodes with blue color
int countBlue(int color[], int n)
{
    int blue = 0;
    for (int i = 0; i < n; i++) {
        if (color[i] == 2)
            blue++;
    }
    return blue;
}

// Function to create a Tree with
// given vertices
void buildTree(int edge[][2],
               map<int, vector<int> >& m,
               int n)
{
    int u, v, i;

    // Traverse the edge[] array
    for (i = 0; i < n - 1; i++) {

        u = edge[i][0] - 1;
        v = edge[i][1] - 1;

        // Create adjacency list
        m[u].push_back(v);
        m[v].push_back(u);
    }
}

// Function to count the number of
// subtree with the given condition
void countSubtree(int color[], int n,
                  int edge[][2])
{

    // For creating adjacency list
    map<int, vector<int> > adj;
    int ans = 0;

    // To store the count of subtree
    // with only blue and red color
    int sub_red[n + 3] = { 0 };
    int sub_blue[n + 3] = { 0 };

    // visited array for DFS Traversal
    int vis[n + 3] = { 0 };

    // Count the number of red
    // node in the tree
    int red = countRed(color, n);

    // Count the number of blue
    // node in the tree
    int blue = countBlue(color, n);

    // Function Call to build tree
    buildTree(edge, adj, n);

    // DFS Traversal
    Solution_dfs(0, color, red, blue,
                 sub_red, sub_blue,
                 vis, adj, &ans);

    // Print the final count
    cout << ans;
}
// Driver Code
int main()
{
    int N = 5;
    int color[] = { 1, 0, 0, 0, 2 };
    int edge[][2] = { { 1, 2 },
                      { 2, 3 },
                      { 3, 4 },
                      { 4, 5 } };

    countSubtree(color, N, edge);

    return 0;
}
```

## 蟒蛇 3

```
# Function to implement DFS traversal
def Solution_dfs(v, color, red, blue, sub_red, sub_blue, vis, adj, ans):

    # Mark node v as visited
    vis[v] = 1;

    # Traverse Adj_List of node v
    for i in range(len(adj[v])):

        # If current node is not visited
        if (vis[adj[v][i]] == 0):

            # DFS call for current node
            ans=Solution_dfs(adj[v][i], color,red, blue,sub_red, sub_blue,vis, adj, ans);

            # Count the total red and blue
            # nodes of children of its subtree
            sub_red[v] += sub_red[adj[v][i]];
            sub_blue[v] += sub_blue[adj[v][i]];

    if (color[v] == 1):
        sub_red[v] += 1;

    # Count the no. of red and blue
    # nodes in the subtree
    if (color[v] == 2):
        sub_blue[v] += 1;

    # If subtree contains all
    # red node & no blue node
    if (sub_red[v] == red and sub_blue[v] == 0):
        (ans) += 1;

    # If subtree contains all
    # blue node & no red node
    if (sub_red[v] == 0 and sub_blue[v] == blue):
        (ans) += 1;

    return ans

# Function to count the number of
# nodes with red color
def countRed(color, n):

    red = 0;

    for i in range(n):

        if (color[i] == 1):
            red += 1;

    return red;

# Function to count the number of
# nodes with blue color
def countBlue(color, n):

    blue = 0;

    for i in range(n):

        if (color[i] == 2):
            blue += 1

    return blue;

# Function to create a Tree with
# given vertices
def buildTree(edge, m, n):

    u, v, i = 0, 0, 0

    # Traverse the edge[] array
    for i in range(n - 1):

        u = edge[i][0] - 1;
        v = edge[i][1] - 1;

        # Create adjacency list
        if u not in m:
            m[u] = []

        if v not in m:
            m[v] = []

        m[u].append(v)
        m[v].append(u);

# Function to count the number of
# subtree with the given condition
def countSubtree(color, n, edge):

    # For creating adjacency list
    adj = dict()
    ans = 0;

    # To store the count of subtree
    # with only blue and red color
    sub_red = [0 for i in range(n + 3)]
    sub_blue = [0 for i in range(n + 3)]

    # visited array for DFS Traversal
    vis = [0 for i in range(n + 3)]

    # Count the number of red
    # node in the tree
    red = countRed(color, n);

    # Count the number of blue
    # node in the tree
    blue = countBlue(color, n);

    # Function Call to build tree
    buildTree(edge, adj, n);

    # DFS Traversal
    ans=Solution_dfs(0, color, red, blue,sub_red, sub_blue, vis, adj, ans);

    # Print the final count
    print(ans, end = '')

# Driver Code
if __name__=='__main__':

    N = 5;
    color = [ 1, 0, 0, 0, 2 ]
    edge = [ [ 1, 2 ], [ 2, 3 ], [ 3, 4 ], [ 4, 5 ] ];

    countSubtree(color, N, edge);

# This code is contributed by rutvik_56
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*