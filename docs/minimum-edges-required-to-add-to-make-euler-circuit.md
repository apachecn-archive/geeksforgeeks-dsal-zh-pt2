# 形成欧拉回路所需添加的最小边数

> 原文:[https://www . geesforgeks . org/minimum-edges-需要添加到 make-euler-circuit/](https://www.geeksforgeeks.org/minimum-edges-required-to-add-to-make-euler-circuit/)

给定一个由 **n 个**节点和 **m 个**边组成的无向图。任务是找到在给定图形中制作[欧拉回路](https://www.geeksforgeeks.org/eulerian-path-and-circuit/)所需的最小边。

**示例:**

```
Input : n = 3, 
        m = 2
        Edges[] = {{1, 2}, {2, 3}}
Output : 1

By connecting 1 to 3, we can create a Euler Circuit.

```

对于图中存在的欧拉回路，我们要求每个节点都应该有偶数度，因为这样就有一条边可以用来在进入节点后退出节点。

现在，可以有两种情况:
**1。图中有一个连通分支**
在这种情况下，如果图中的所有节点都是偶数度，那么我们说图已经有一个欧拉回路，我们不需要在其中添加任何边。但是如果有奇数度的节点，我们需要增加边。
图中可以有偶数个奇数度顶点。这可以很容易地通过以下事实来证明:来自偶数度节点的度数和来自奇数度节点的度数之和应该与总是偶数的总度数相匹配，因为每个边都对这个和贡献两个。现在，如果我们在图中随机配对奇数度节点，并在它们之间添加一条边，我们可以使所有节点都具有偶数度，从而使欧拉回路存在。

**2。图中有断开的分量**
我们先把分量标为奇数和偶数。奇数分量是那些至少有一个奇数度节点的分量。取所有偶数分量，从每个分量中选择一个随机顶点，并线性排列。现在我们在相邻顶点之间添加一条边。所以我们连接了偶分量，做了一个等价的奇分量，它有两个奇数度的节点。
现在处理奇数分量，即至少有一个奇数度节点的分量。我们可以用边连接所有这些奇数分量，边的数量等于断开分量的数量。这可以通过将组件按循环顺序放置，并从每个组件中选取两个奇数度节点，然后使用这些节点连接到任一侧的组件来实现。现在我们已经讨论了单个连接组件。

以下是该方法的实现:

## C++

```
// C++ program to find minimum edge required
// to make Euler Circuit
#include <bits/stdc++.h>
using namespace std;

// Depth-First Search to find a connected
// component
void dfs(vector<int> g[], int vis[], int odd[],
                    int deg[],  int comp, int v)
{
    vis[v] = 1;

    if (deg[v]%2 == 1)
        odd[comp]++;

    for (int u : g[v])
        if (vis[u] == 0)
            dfs(g, vis, odd, deg, comp, u);
}

// Return minimum edge required to make Euler
// Circuit
int minEdge(int n, int m, int s[], int d[])
{
    // g : to store adjacency list
    //     representation of graph.
    // e : to store list of even degree vertices
    // o : to store list of odd degree vertices
    vector<int> g[n+1], e, o;

    int deg[n+1];  // Degrees of vertices
    int vis[n+1];  // To store visited in DFS
    int odd[n+1];  // Number of odd nodes in components
    memset(deg, 0, sizeof(deg));
    memset(vis, 0, sizeof(vis));
    memset(odd, 0, sizeof(odd));

    for (int i = 0; i < m; i++)
    {
        g[s[i]].push_back(d[i]);
        g[d[i]].push_back(s[i]);
        deg[s[i]]++;
        deg[d[i]]++;
    }

    // 'ans' is result and 'comp' is component id
    int ans = 0, comp = 0;
    for (int i = 1; i <= n; i++)
    {
        if (vis[i]==0)
        {
            comp++;
            dfs(g, vis, odd, deg, comp, i);

            // Checking if connected component
            // is odd.
            if (odd[comp] == 0)
                e.push_back(comp);

            // Checking if connected component
            // is even.
            else
                o.push_back(comp);
        }
    }

    // If whole graph is a single connected
    // component with even degree.
    if (o.size() == 0 && e.size() == 1)
        return 0;

    // If all connected component is even
    if (o.size() == 0)
        return e.size();

    // If graph have atleast one even connected
    // component
    if (e.size() != 0)
        ans += e.size();

    // For all the odd connected component.
    for (int i : o)
        ans += odd[i]/2;

    return ans;
}

// Driven Program
int main()
{
    int n = 3, m = 2;
    int source[] = { 1, 2 };
    int destination[] = { 2, 3 };

    cout << minEdge(n, m, source, destination) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum edge
// required to make Euler Circuit
import java.io.*;
import java.util.*;

class GFG 
{

    // Depth-First Search to find 
    // a connected component
    static void dfs(Vector<Integer>[] g, int[] vis, 
                              int[] odd, int[] deg,
                              int comp, int v) 
    {
        vis[v] = 1;
        if (deg[v] % 2 == 1)
            odd[comp]++;
        for (int u : g[v])
            if (vis[u] == 0)
                dfs(g, vis, odd, deg, comp, u);
    }

    // Return minimum edge required 
    // to make Euler Circuit
    static int minEdge(int n, int m, 
                       int[] s, int[] d)
    {

        // g : to store adjacency list
        //     representation of graph.
        // e : to store list of even degree vertices
        // o : to store list of odd degree vertices
        @SuppressWarnings("unchecked")
        Vector<Integer>[] g = new Vector[n + 1];
        Vector<Integer> e = new Vector<>();
        Vector<Integer> o = new Vector<>();

        for (int i = 0; i < n + 1; i++)
            g[i] = new Vector<>();

        // Degrees of vertices
        int[] deg = new int[n + 1]; 

        // To store visited in DFS
        int[] vis = new int[n + 1];

        // Number of odd nodes in components
        int[] odd = new int[n + 1]; 
        Arrays.fill(deg, 0);
        Arrays.fill(vis, 0);
        Arrays.fill(odd, 0);

        for (int i = 0; i < m; i++) 
        {
            g[s[i]].add(d[i]);
            g[d[i]].add(s[i]);
            deg[s[i]]++;
            deg[d[i]]++;
        }

        // 'ans' is result and 
        // 'comp' is component id
        int ans = 0, comp = 0;
        for (int i = 1; i <= n; i++) 
        {
            if (vis[i] == 0) 
            {
                comp++;
                dfs(g, vis, odd, deg, comp, i);

                // Checking if connected component
                // is odd.
                if (odd[comp] == 0)
                    e.add(comp);

                // Checking if connected component
                // is even.
                else
                    o.add(comp);
            }
        }

        // If whole graph is a single connected
        // component with even degree.
        if (o.size() == 0 && e.size() == 1)
            return 0;

        // If all connected component is even
        if (o.size() == 0)
            return e.size();

        // If graph have atleast one 
        // even connected component
        if (e.size() != 0)
            ans += e.size();

        // For all the odd connected component.
        for (int i : o)
            ans += odd[i] / 2;

        return ans;
    }

    // Driver Code
    public static void main(String[] args) throws IOException
    {
        int n = 3, m = 2;
        int[] source = { 1, 2 };
        int[] destination = { 2, 3 };

        System.out.println(minEdge(n, m, source, 
                                   destination));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find minimum edge 
# required to make Euler Circuit

# Depth-First Search to find a 
# connected component 
def dfs(g, vis, odd, deg, comp, v):
    vis[v] = 1

    if (deg[v] % 2 == 1): 
        odd[comp] += 1

    for u in range(len(g[v])):
        if (vis[u] == 0):
            dfs(g, vis, odd, deg, comp, u)

# Return minimum edge required to
# make Euler Circuit 
def minEdge(n, m, s, d):

    # g : to store adjacency list 
    #      representation of graph. 
    # e : to store list of even degree vertices 
    # o : to store list of odd degree vertices 
    g = [[] for i in range(n + 1)]
    e = []
    o = []

    deg = [0] * (n + 1) # Degrees of vertices 
    vis = [0] * (n + 1) # To store visited in DFS 
    odd = [0] * (n + 1) # Number of odd nodes
                        # in components 

    for i in range(m):
        g[s[i]].append(d[i]) 
        g[d[i]].append(s[i]) 
        deg[s[i]] += 1
        deg[d[i]] += 1

    # 'ans' is result and 'comp' 
    # is component id 
    ans = 0
    comp = 0
    for i in range(1, n + 1):
        if (vis[i] == 0):
            comp += 1
            dfs(g, vis, odd, deg, comp, i) 

            # Checking if connected component 
            # is odd. 
            if (odd[comp] == 0): 
                e.append(comp) 

            # Checking if connected component 
            # is even. 
            else:
                o.append(comp)

    # If whole graph is a single connected 
    # component with even degree. 
    if (len(o) == 0 and len(e) == 1): 
        return 0

    # If all connected component is even 
    if (len(o) == 0): 
        return len(e) 

    # If graph have atleast one 
    # even connected component 
    if (len(e) != 0): 
        ans += len(e)

    # For all the odd connected component. 
    for i in range(len(o)):
        ans += odd[i] // 2

    return ans

# Driver Code
if __name__ == '__main__':

    n = 3
    m = 2
    source = [ 1, 2 ]
    destination = [ 2, 3]

    print(minEdge(n, m, source, destination))

# This code is contributed by PranchalK
```

**Output:**

```
1

```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。