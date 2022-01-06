# 树上的扩展不相交集并

> 原文:[https://www . geeksforgeeks . org/extended-disjoint-set-union-on-trees/](https://www.geeksforgeeks.org/extended-disjoint-set-union-on-trees/)

**先决条件:** [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 、 [Trees](https://www.geeksforgeeks.org/generic-treesn-array-trees/) 、 [DSU](https://www.geeksforgeeks.org/union-find/)
给定一棵具有从值 **1 到 N** 的 **N** 个节点的树和表示与每个节点相关联的编号的 **E** 个边和数组**arr【】**。还会给你 **Q** 查询，其中包含 2 个整数 **{V，F}** 。对于每个查询，都有一个顶点为 **V** 的子树，任务是检查该子树中与每个节点相关联的数字计数是否为 **F** 。如果是，则打印**真**否则打印**假**。
**例:**

> **输入:** N = 8，E = { {1，2}，{1，3}，{2，4}，{2，5}，{5，8}，{5，6}，{6，7} }，arr[] = { 11，2，7，1，-3，-1，-1，-3 }，Q = 3，query[]= { { 2，3 }，{5，2}，{7， 1} }
> **输出:**
> 假
> 真
> 真
> **说明:**
> 查询 1:子树 2
> 中无数字出现 3 次查询 2:子树 5
> 中数字-1 和-3 出现 2 次查询 3:子树 7
> **中数字-1 出现 1 次输入:** N = 11，E = { {1，2}，{1，3}，{2 arr[] = { 2，-1，-12，-1，6，14，7，-1，-2，13，12 }，Q = 2，查询[] = { {2，2 }，{4，2} }
> **输出:**
> 假
> 真
> **解释:**
> 查询 1:没有数字在子树 2 中恰好出现 2 次
> 查询 2:数字-1 在子树 4
> 中出现 2 次

**天真方法:**想法是使用 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 遍历树并计算与子树的每个顶点相关联的数字的频率， **V** 并将结果存储在散列表中。遍历之后，我们只需要遍历 hashmap 来检查给定的频数是否存在。
以下是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;

@SuppressWarnings("unchecked")
public class Main {

    // To store edges of tree
    static ArrayList<Integer> adj[];

    // To store number associated
    // with vertex
    static int num[];

    // To store frequency of number
    static HashMap<Integer, Integer> freq;

    // Function to add edges in tree
    static void add(int u, int v)
    {
        adj[u].add(v);
        adj[v].add(u);
    }

    // Function returns boolean value
    // representing is there any number
    // present in subtree qv having
    // frequency qc
    static boolean query(int qv, int qc)
    {

        freq = new HashMap<>();

        // Start from root
        int v = 1;

        // DFS Call
        if (qv == v) {
            dfs(v, 0, true, qv);
        }
        else
            dfs(v, 0, false, qv);

        // Check for frequency
        for (int fq : freq.values()) {
            if (fq == qc)
                return true;
        }
        return false;
    }

    // Function to implement DFS
    static void dfs(int v, int p,
                    boolean isQV, int qv)
    {
        if (isQV) {

            // If we are on subtree qv,
            // then increment freq of
            // num[v] in freq
            freq.put(num[v],
                     freq.getOrDefault(num[v], 0) + 1);
        }

        // Recursive DFS Call for
        // adjacency list of node u
        for (int u : adj[v]) {
            if (p != u) {
                if (qv == u) {
                    dfs(u, v, true, qv);
                }
                else
                    dfs(u, v, isQV, qv);
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Nodes
        int n = 8;
        adj = new ArrayList[n + 1];
        for (int i = 1; i <= n; i++)
            adj[i] = new ArrayList<>();

        // Given edges of tree
        // (root=1)
        add(1, 2);
        add(1, 3);
        add(2, 4);
        add(2, 5);
        add(5, 8);
        add(5, 6);
        add(6, 7);

        // Number assigned to each vertex
        num = new int[] { -1, 11, 2, 7, 1, -3, -1, -1, -3 };

        // Total number of queries
        int q = 3;

        // Function Call to find each query
        System.out.println(query(2, 3));
        System.out.println(query(5, 2));
        System.out.println(query(7, 1));
    }
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# To store edges of tree
adj=[]

# To store number associated
# with vertex
num=[]

# To store frequency of number
freq=dict()

# Function to add edges in tree
def add(u, v):
    adj[u].append(v)
    adj[v].append(u)

# Function returns boolean value
# representing is there any number
# present in subtree qv having
# frequency qc
def query(qv, qc):
    freq.clear()

    # Start from root
    v = 1

    # DFS Call
    if (qv == v) :
        dfs(v, 0, True, qv)

    else:
        dfs(v, 0, False, qv)

    # Check for frequency
    if qc in freq.values() :
        return True

    return False

# Function to implement DFS
def dfs(v, p, isQV, qv):
    if (isQV) :

        # If we are on subtree qv,
        # then increment freq of
        # num[v] in freq
        freq[num[v]]=freq.get(num[v], 0) + 1

    # Recursive DFS Call for
    # adjacency list of node u
    for u in adj[v]:
        if (p != u) :
            if (qv == u) :
                dfs(u, v, True, qv)

            else:
                dfs(u, v, isQV, qv)

# Driver Code
if __name__ == '__main__':

    # Given Nodes
    n = 8
    for _ in range(n+1):
        adj.append([])

    # Given edges of tree
    # (root=1)
    add(1, 2)
    add(1, 3)
    add(2, 4)
    add(2, 5)
    add(5, 8)
    add(5, 6)
    add(6, 7)

    # Number assigned to each vertex
    num = [-1, 11, 2, 7, 1, -3, -1, -1, -3]

    # Total number of queries
    q = 3

    # Function Call to find each query
    print(query(2, 3))
    print(query(5, 2))
    print(query(7, 1))
```

**Output:** 

```
false
true
true
```

***时间复杂度:** O(N * Q)因为在每个查询中，都需要遍历树。*
***辅助空间:** O(N + E + Q)*
**高效途径:**思路是用[扩展不相交集并集](https://www.geeksforgeeks.org/disjoint-set-data-structures/)到上述途径:

1.  创建一个数组，**size【】**来存储子树的大小。
2.  创建一个散列表， **map[]** ，即 map[V][X] =子树中数量为 **X** 的顶点总数， **V** 。
3.  通过调用 dfsSize()使用 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 遍历计算每个子树的大小。
4.  使用 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 遍历通过调用 dfs(V，p)，计算地图【V】的值。
5.  在遍历中，要计算**地图【V】**，选择除父顶点 **p** 外尺寸最大( **bigU** )的 **V** 的相邻顶点。

6.  对于连接操作，将地图[bigU]的引用传递给地图[V]，即**地图[V] =地图[bigU]** 。
7.  并且最后合并所有相邻顶点的地图， **u** 到**地图【V】**，除了父顶点， **p** 和 **bigU** 顶点。
8.  现在，检查**地图【V】**是否包含频率 F。如果是，则打印**真**否则打印**假**。

下面是高效方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.awt.*;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;
import java.util.Map.Entry;

@SuppressWarnings("unchecked")
public class Main {

    // To store edges
    static ArrayList<Integer> adj[];

    // num[v] = number assigned
    // to vertex v
    static int num[];

    // map[v].get(c) = total vertices
    // in subtree v having number c
    static Map<Integer, Integer> map[];

    // size[v]=size of subtree v
    static int size[];

    static HashMap<Point, Boolean> ans;
    static ArrayList<Integer> qv[];

    // Function to add edges
    static void add(int u, int v)
    {
        adj[u].add(v);
        adj[v].add(u);
    }

    // Function to find subtree size
    // of every vertex using dfsSize()
    static void dfsSize(int v, int p)
    {
        size[v]++;

        // Traverse dfsSize recursively
        for (int u : adj[v]) {
            if (p != u) {
                dfsSize(u, v);
                size[v] += size[u];
            }
        }
    }

    // Function to implement DFS Traversal
    static void dfs(int v, int p)
    {
        int mx = -1, bigU = -1;

        // Find adjacent vertex with
        // maximum size
        for (int u : adj[v]) {
            if (u != p) {
                dfs(u, v);
                if (size[u] > mx) {
                    mx = size[u];
                    bigU = u;
                }
            }
        }

        if (bigU != -1) {

            // Passing referencing
            map[v] = map[bigU];
        }
        else {

            // If no adjacent vertex
            // present initialize map[v]
            map[v] = new HashMap<Integer, Integer>();
        }

        // Update frequency of current number
        map[v].put(num[v],
                   map[v].getOrDefault(num[v], 0) + 1);

        // Add all adjacent vertices
        // maps to map[v]
        for (int u : adj[v]) {

            if (u != bigU && u != p) {

                for (Entry<Integer, Integer>
                         pair : map[u].entrySet()) {
                    map[v].put(
                        pair.getKey(),
                        pair.getValue()
                            + map[v]
                                  .getOrDefault(
                                      pair.getKey(), 0));
                }
            }
        }

        // Store all queries related
        // to vertex v
        for (int freq : qv[v]) {
            ans.put(new Point(v, freq),
                    map[v].containsValue(freq));
        }
    }

    // Function to find answer for
    // each queries
    static void solveQuery(Point queries[],
                           int N, int q)
    {
        // Add all queries to qv
        // where i<qv[v].size()
        qv = new ArrayList[N + 1];
        for (int i = 1; i <= N; i++)
            qv[i] = new ArrayList<>();

        for (Point p : queries) {
            qv[p.x].add(p.y);
        }

        // Get sizes of all subtrees
        size = new int[N + 1];

        // calculate size[]
        dfsSize(1, 0);

        // Map will be used to store
        // answers for current vertex
        // on dfs
        map = new HashMap[N + 1];

        // To store answer of queries
        ans = new HashMap<>();

        // DFS Call
        dfs(1, 0);

        for (Point p : queries) {

            // Print answer for each query
            System.out.println(ans.get(p));
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 8;
        adj = new ArrayList[N + 1];
        for (int i = 1; i <= N; i++)
            adj[i] = new ArrayList<>();

        // Given edges (root=1)
        add(1, 2);
        add(1, 3);
        add(2, 4);
        add(2, 5);
        add(5, 8);
        add(5, 6);
        add(6, 7);

        // Store number given to vertices
        // set num[0]=-1 because
        // there is no vertex 0
        num
            = new int[] { -1, 11, 2, 7, 1,
                          -3, -1, -1, -3 };

        // Queries
        int q = 3;

        // To store queries
        Point queries[] = new Point[q];

        // Given Queries
        queries[0] = new Point(2, 3);
        queries[1] = new Point(5, 2);
        queries[2] = new Point(7, 1);

        // Function Call
        solveQuery(queries, N, q);
    }
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# To store edges of tree
adj=[]

# To store number associated
# with vertex
num=[]

# mp[v] = total vertices
# in subtree v having number c
mp=dict()

# size[v]=size of subtree v
size=[]

ans=dict()

qv=[]

# Function to add edges in tree
def add(u, v):
    adj[u].append(v)
    adj[v].append(u)

# Function to find subtree size
# of every vertex using dfsSize()
def dfsSize(v, p):
    size[v]+=1

    # Traverse dfsSize recursively
    for u in adj[v] :
        if (p != u) :
            dfsSize(u, v)
            size[v] += size[u]

# Function to implement DFS Traversal
def dfs(v, p):
    global ans
    mx = -1; bigU = -1

    # Find adjacent vertex with
    # maximum size
    for u in adj[v]:
        if (u != p) :
            dfs(u, v)
            if (size[u] > mx) :
                mx = size[u]
                bigU = u       

    if (bigU != -1) :

        # Passing referencing
        mp[v] = mp[bigU]

    else :

        # If no adjacent vertex
        # present initialize mp[v]
        mp[v] = dict()

    # Update frequency of current number
    mp[v][num[v]]=mp[v].get(num[v], 0) + 1

    # Add all adjacent vertices
    # maps to mp[v]
    for u in adj[v] :
        if u not in (bigU,p) :
            for pair in mp[u].items():
                mp[v][pair[0]]=pair[1]+mp[v].get(pair[0], 0)

    # Store all queries related
    # to vertex v
    for freq in qv[v] :
        ans[(v, freq)]=freq in mp[v]

# Function to find answer for
# each queries
def solveQuery(queries, N, q):
    global size,mp,qv,ans
    # Add all queries to qv
    # where i<qv[v].size()
    qv = []
    for i in range(N+1):
        qv.append([])

    for p in queries:
        qv[p[0]].append(p[1])

    # Get sizes of all subtrees   
    size = [0]*(N + 1)

    # calculate size[]
    dfsSize(1, 0)

    # mp will be used to store
    # answers for current vertex
    # on dfs
    mp = dict()

    # To store answer of queries
    ans = dict()

    # DFS Call
    dfs(1, 0)

    for p in queries:

        # Print answer for each query
        print(ans[p])

# Driver Code
if __name__ == '__main__':
    N = 8
    adj = []
    for i in range(N+1):
        adj.append([])

    # Given edges (root=1)
    add(1, 2)
    add(1, 3)
    add(2, 4)
    add(2, 5)
    add(5, 8)
    add(5, 6)
    add(6, 7)

    # Store number given to vertices
    # set num[0]=-1 because
    # there is no vertex 0
    num = [-1, 11, 2, 7, 1,-3, -1, -1, -3]

    # Queries
    q = 3

    # To store queries
    queries=[]

    # Given Queries
    queries.append((2, 3))
    queries.append((5, 2))
    queries.append((7, 1))

    # Function Call
    solveQuery(queries, N, q)
```

**Output:** 

```
false
true
true
```

***时间复杂度:**O(N * logN<sup>2</sup>)*
***辅助空间:** O(N + E + Q)*