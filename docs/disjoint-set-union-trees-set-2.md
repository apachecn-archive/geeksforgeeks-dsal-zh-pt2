# 树上不相交的集合并集|集合 2

> 原文:[https://www . geesforgeks . org/disjoint-set-union-trees-set-2/](https://www.geeksforgeeks.org/disjoint-set-union-trees-set-2/)

给定一棵树，子树的代价定义为|S|*and(S)，其中|S|是子树的大小，AND(S)是子树中所有节点索引的按位 AND，任务是找到可能的子树的最大代价。
**先决条件:** [不相交集合并集](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)
示例:

```
Input : Number of nodes = 4
        Edges = (1, 2), (3, 4), (1, 3)
Output : Maximum cost = 4
Explanation : 
Subtree with singe node {4} gives the maximum cost.

Input : Number of nodes = 6
        Edges = (1, 2), (2, 3), (3, 4), (3, 5), (5, 6)
Output : Maximum cost = 8
Explanation : 
Subtree with nodes {5, 6} gives the maximum cost.
```

**方法:**策略是固定 and，找到一个子树的最大大小，使得所有索引的 AND 等于给定的 AND。假设我们把 AND 固定为 A。在 A 的二进制表示中，如果 ith 位是“1”，那么所需子树的所有索引(节点)在二进制表示中的 ith 位置都应该是“1”。如果 ith 位为“0”，则索引的 ith 位置为“0”或“1”。这意味着子树的所有元素都是 a 的超级掩码。a 的所有超级掩码都可以在 O(2^k 生成)时间，其中“k”是 a 中“0”的位数。
现在，可以使用树上的 DSU 找到给定和“a”的子树的最大大小。假设，‘u’是 A 的超级掩码，‘p[u]’是 u 的父级，如果 p[u]也是 A 的超级掩码，那么，我们必须通过合并 u 和 p[u]的分量来更新 DSU。同时，我们还必须跟踪子树的最大大小。DSU 帮助我们做这件事。如果我们看看下面的代码，会更清楚。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP code to find maximum possible cost
#include <bits/stdc++.h>
using namespace std;

#define N 100010

// Edge structure
struct Edge {
    int u, v;
};

/* v : Adjacency list representation of Graph
    p : stores parents of nodes */
vector<int> v[N];
int p[N];

// Weighted union-find with path compression
struct wunionfind {
    int id[N], sz[N];
    void initial(int n)
    {
        for (int i = 1; i <= n; i++)
            id[i] = i, sz[i] = 1;
    }

    int Root(int idx)
    {
        int i = idx;
        while (i != id[i])
            id[i] = id[id[i]], i = id[i];

        return i;
    }

    void Union(int a, int b)
    {
        int i = Root(a), j = Root(b);
        if (i != j) {
            if (sz[i] >= sz[j]) {
                id[j] = i, sz[i] += sz[j];
                sz[j] = 0;
            }
            else {
                id[i] = j, sz[j] += sz[i];
                sz[i] = 0;
            }
        }
    }
};

wunionfind W;

// DFS is called to generate parent of
// a node from adjacency list representation
void dfs(int u, int parent)
{
    for (int i = 0; i < v[u].size(); i++) {
        int j = v[u][i];
        if (j != parent) {
            p[j] = u;
            dfs(j, u);
        }
    }
}

// Utility function for Union
int UnionUtil(int n)
{
    int ans = 0;

    // Fixed 'i' as AND
    for (int i = 1; i <= n; i++) {
        int maxi = 1;

        // Generating supermasks of 'i'
        for (int x = i; x <= n; x = (i | (x + 1))) {
            int y = p[x];

            // Checking whether p[x] is
            // also a supermask of i.
            if ((y & i) == i) {
                W.Union(x, y);

                // Keep track of maximum
                // size of subtree
                maxi = max(maxi, W.sz[W.Root(x)]);
            }
        }

        // Storing maximum cost of
        // subtree with a given AND
        ans = max(ans, maxi * i);

        // Separating components which are merged
        // during Union operation for next AND value.
        for (int x = i; x <= n; x = (i | (x + 1))) {
            W.sz[x] = 1;
            W.id[x] = x;
        }
    }

    return ans;
}

// Driver code
int main()
{
    int n, i;

    // Number of nodes
    n = 6;

    W.initial(n);

    Edge e[] = { { 1, 2 }, { 2, 3 }, { 3, 4 },
                 { 3, 5 }, { 5, 6 } };

    int q = sizeof(e) / sizeof(e[0]);

    // Taking edges as input and put
    // them in adjacency list representation
    for (i = 0; i < q; i++) {
        int x, y;
        x = e[i].u, y = e[i].v;
        v[x].push_back(y);
        v[y].push_back(x);
    }

    // Initializing parent vertex of '1' as '1'
    p[1] = 1;

    // Call DFS to generate 'p' array
    dfs(1, -1);

    int ans = UnionUtil(n);

        printf("Maximum Cost = %d\n", ans);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 code to find maximum possible cost
N = 100010

# Edge structure
class Edge:

    def __init__(self, u, v):
        self.u = u
        self.v = v

''' v : Adjacency list representation of Graph
    p : stores parents of nodes '''

v=[[] for i in range(N)];
p=[0 for i in range(N)];

# Weighted union-find with path compression
class wunionfind:

    def __init__(self):

        self.id = [0 for i in range(1, N + 1)]
        self.sz = [0 for i in range(1, N + 1)]

    def initial(self, n):

        for i in range(1, n + 1):
            self.id[i] = i
            self.sz[i] = 1

    def Root(self, idx):

        i = idx;

        while (i != self.id[i]):
            self.id[i] = self.id[self.id[i]]
            i = self.id[i];

        return i;

    def Union(self, a, b):

        i = self.Root(a)
        j = self.Root(b);

        if (i != j):
            if (self.sz[i] >= self.sz[j]):
                self.id[j] = i
                self.sz[i] += self.sz[j];
                self.sz[j] = 0;
            else:
                self.id[i] = j
                self.sz[j] += self.sz[i];
                self.sz[i] = 0

W = wunionfind()

# DFS is called to generate parent of
# a node from adjacency list representation
def dfs(u, parent):

    for i in range(0, len(v[u])):

        j = v[u][i];

        if(j != parent):
            p[j] = u;
            dfs(j, u);

# Utility function for Union
def UnionUtil(n):

    ans = 0;

    # Fixed 'i' as AND
    for i in range(1, n + 1):

        maxi = 1;

        # Generating supermasks of 'i'
        x = i
        while x<=n:

            y = p[x];

            # Checking whether p[x] is
            # also a supermask of i.
            if ((y & i) == i):
                W.Union(x, y);

                # Keep track of maximum
                # size of subtree
                maxi = max(maxi, W.sz[W.Root(x)]);

            x = (i | (x + 1))

        # Storing maximum cost of
        # subtree with a given AND
        ans = max(ans, maxi * i);

        # Separating components which are merged
        # during Union operation for next AND value.
        x = i
        while x <= n:
            W.sz[x] = 1;
            W.id[x] = x;
            x = (i | (x + 1))

    return ans;

# Driver code
if __name__=='__main__':

    # Number of nodes
    n = 6;

    W.initial(n);

    e = [ Edge( 1, 2 ), Edge( 2, 3 ), Edge( 3, 4 ),
                 Edge( 3, 5 ), Edge( 5, 6 ) ];

    q = len(e)

    # Taking edges as input and put
    # them in adjacency list representation
    for i in range(q):

        x = e[i].u
        y = e[i].v;
        v[x].append(y);
        v[y].append(x);

    # Initializing parent vertex of '1' as '1'
    p[1] = 1;

    # Call DFS to generate 'p' array
    dfs(1, -1);

    ans = UnionUtil(n);

    print("Maximum Cost =", ans)

# This code is contributed by rutvik_56   
```

**Output:** 

```
Maximum Cost = 8
```

**时间复杂度:**DSU 联合需要 O(1)时间。生成所有超级任务需要 O(3^k 时间，其中 k 是“0”的最大位数。DFS 取 0(n)。总的时间复杂度是 O(3^k+n).