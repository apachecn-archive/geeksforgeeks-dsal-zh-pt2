# 使用图表

对不同组进行计数

> 原文:[https://www . geeksforgeeks . org/不同组的计数使用图/](https://www.geeksforgeeks.org/count-of-different-groups-using-graph/)

给定一个图，其中 **N** 个节点的值为 **P** 或 **M** 。同样给定 **K** 对整数作为 **(x，y)** 表示图中的边，这样如果 **a** 连接到 **b** 并且 **b** 连接到 **c** ，那么 **a** 和 **c** 也将被连接。

单个连接的组件称为组。该组可以同时具有 **P** 和 **M** 值。如果 **P** 值大于 **M** 值，则该组被称为 **P** 受影响，类似于 **M** 。如果**的 P**和**的 M**的数量相等，则称为中性组。任务是找出 **P** 受影响， **M** 受影响，**中性**组的数量。

**示例:**

> **输入:**节点[] = {P，M，P，M，P}，边[][] = {
> {1，3}，
> {4，5}，
> {3，5}}
> **输出:**
> P = 1
> M = 1
> N = 0
> 将有两组索引
> {1，3，4，5}和{2}。
> 第一组受 P 影响，
> 第二组受 M 影响。
> 
> **输入:**节点[] = {P，M，P，M，P}，边[][] = {
> {1，3}，
> {4，5}}
> **输出:**
> P = 1
> M = 2
> N = 0

**方法:**构造一个有邻接表的图，从 **1 到 N** 循环，做 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 检查 P 和 M 的计数比较容易
另一种方法是使用 [DSU](https://www.geeksforgeeks.org/disjoint-set-union-trees-set-1/) 稍加修改，大小数组将为**对**，这样就可以同时保持 **M 和 P** 的计数。在这种方法中，不需要构造图，因为合并操作将处理连接的组件。请注意，您应该了解 DSU 的大小/排名，以便进行优化。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// To store the parents
// of the current node
vector<int> par;

// To store the size of M and P
vector<pair<int, int> > sz;

// Function for initialization
void init(vector<char>& nodes)
{

    // Size of the graph
    int n = (int)nodes.size();

    par.clear();
    sz.clear();
    par.resize(n + 1);
    sz.resize(n + 1);

    for (int i = 0; i <= n; ++i) {
        par[i] = i;

        if (i > 0) {

            // If the node is P
            if (nodes[i - 1] == 'P')
                sz[i] = { 0, 1 };

            // If the node is M
            else
                sz[i] = { 1, 0 };
        }
    }
}

// To find the parent of
// the current node
int parent(int i)
{
    while (par[i] != i)
        i = par[i];
    return i;
}

// Merge function
void union(int a, int b)
{
    a = parent(a);
    b = parent(b);

    if (a == b)
        return;

    // Total size by adding number of M and P
    int sz_a = sz[a].first + sz[a].second;
    int sz_b = sz[b].first + sz[b].second;

    if (sz_a < sz_b)
        swap(a, b);

    par[b] = a;
    sz[a].first += sz[b].first;
    sz[a].second += sz[b].second;
    return;
}

// Function to calculate the influenced value
void influenced(vector<char>& nodes,
                vector<pair<int, int> > connect)
{

    // Number of nodes
    int n = (int)nodes.size();

    // Initialization function
    init(nodes);

    // Size of the connected vector
    int k = connect.size();

    // Performing union operation
    for (int i = 0; i < k; ++i) {
        union(connect[i].first, connect[i].second);
    }

    // ne = Number of neutal groups
    // ma = Number of M influenced groups
    // pe = Number of P influenced groups
    int ne = 0, ma = 0, pe = 0;

    for (int i = 1; i <= n; ++i) {
        int x = parent(i);

        if (x == i) {
            if (sz[i].first == sz[i].second) {
                ne++;
            }
            else if (sz[i].first > sz[i].second) {
                ma++;
            }
            else {
                pe++;
            }
        }
    }

    cout << "P = " << pe << "\nM = "
         << ma << "\nN = " << ne << "\n";
}

// Driver code
int main()
{

    // Nodes at each index ( 1 - base indexing )
    vector<char> nodes = { 'P', 'M', 'P', 'M', 'P' };

    // Connected Pairs
    vector<pair<int, int> > connect = {
        { 1, 3 },
        { 3, 5 },
        { 4, 5 }
    };

    influenced(nodes, connect);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG{

// To store the parents
// of the current node
static ArrayList<Integer> par = new ArrayList<Integer>();

// To store the size of M and P
static ArrayList<
       ArrayList<Integer>> sz = new ArrayList<
                                    ArrayList<Integer>>();

// Function for initialization
static void init(ArrayList<Character> nodes)
{

    // Size of the graph
    int n = nodes.size();
    for(int i = 0; i <= n; ++i)
    {
        par.add(i);

        if (i == 0)
        {
            sz.add(new ArrayList<Integer>(
                Arrays.asList(0, 0)));
        }

        if (i > 0)
        {

            // If the node is P
            if (nodes.get(i - 1) == 'P')
            {
                sz.add(new ArrayList<Integer>(
                    Arrays.asList(0, 1)));
            }

            // If the node is M
            else
            {
                sz.add(new ArrayList<Integer>(
                    Arrays.asList(1, 0)));
            }
        }
    }
}

// To find the parent of
// the current node
static int parent(int i)
{
    while (par.get(i) != i)
    {
        i = par.get(i);
    }
    return i;
}

// Merge function
static void union(int a, int b)
{
    a = parent(a);
    b = parent(b);

    if (a == b)
    {
        return;
    }

    // Total size by adding number
    // of M and P
    int sz_a = sz.get(a).get(0) +
               sz.get(a).get(1);
    int sz_b = sz.get(b).get(0) +
               sz.get(b).get(1);

    if (sz_a < sz_b)
    {
        int temp = a;
        a = b;
        b = temp;
    }
    par.set(b, a);

    sz.get(a).set(0, sz.get(a).get(0) +
                     sz.get(b).get(0));
    sz.get(a).set(1, sz.get(a).get(1) +
                     sz.get(b).get(1));
    return;
}

// Function to calculate the influenced value
static void influenced(ArrayList<Character> nodes,
             ArrayList<ArrayList<Integer>> connect)
{

    // Number of nodes
    int n = nodes.size();

    // Initialization function
    init(nodes);

    // Size of the connected vector
    int k = connect.size();

    // Performing union operation
    for(int i = 0; i < k; ++i)
    {
        union(connect.get(i).get(0),
             connect.get(i).get(1));
    }

    // ne = Number of neutal groups
    // ma = Number of M influenced groups
    // pe = Number of P influenced groups
    int ne = 0, ma = 0, pe = 0;
    for(int i = 1; i <= n; ++i)
    {
        int x = parent(i);

        if (x == i)
        {
            if (sz.get(i).get(0) ==
                sz.get(i).get(1))
            {
                ne++;
            }
            else if (sz.get(i).get(0) >
                     sz.get(i).get(1))
            {
                ma++;
            }
            else
            {
                pe++;
            }
        }
    }
    System.out.println("P = " + pe +
                     "\nM = " + ma +
                     "\nN = " + ne);
}

// Driver code
public static void main(String[] args)
{

    // Nodes at each index ( 1 - base indexing )
    ArrayList<Character> nodes = new ArrayList<Character>();
    nodes.add('P');
    nodes.add('M');
    nodes.add('P');
    nodes.add('M');
    nodes.add('P');

    // Connected Pairs
    ArrayList<
    ArrayList<Integer>> connect = new ArrayList<
                                      ArrayList<Integer>>();
    connect.add(new ArrayList<Integer>(
        Arrays.asList(1, 3)));
    connect.add(new ArrayList<Integer>(
        Arrays.asList(3, 5)));
    connect.add(new ArrayList<Integer>(
        Arrays.asList(4, 5)));

    influenced(nodes, connect);
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# To store the parents
# of the current node
par = []

# To store the size of M and P
sz = []

# Function for initialization
def init(nodes):

    # Size of the graph
    n = len(nodes)
    for i in range(n + 1):
        par.append(0)
        sz.append(0)

    for i in range(n + 1):
        par[i] = i

        if (i > 0):

            # If the node is P
            if (nodes[i - 1] == 'P'):
                sz[i] = [0, 1]

            # If the node is M
            else:
                sz[i] = [1, 0]

# To find the parent of
# the current node
def parent(i):
    while (par[i] != i):
        i = par[i]
    return i

# Merge function
def union(a, b):
    a = parent(a)
    b = parent(b)

    if (a == b):
        return

    # Total size by adding number of M and P
    sz_a = sz[a][0] + sz[a][1]
    sz_b = sz[b][0] + sz[b][1]

    if (sz_a < sz_b):
        a, b = b, a

    par[b] = a
    sz[a][0] += sz[b][0]
    sz[a][1] += sz[b][1]
    return

# Function to calculate the influenced value
def influenced(nodes,connect):

    # Number of nodes
    n = len(nodes)

    # Initialization function
    init(nodes)

    # Size of the connected vector
    k = len(connect)

    # Performing union operation
    for i in range(k):
        union(connect[i][0], connect[i][1])

    # ne = Number of neutal groups
    # ma = Number of M influenced groups
    # pe = Number of P influenced groups
    ne = 0
    ma = 0
    pe = 0

    for i in range(1, n + 1):
        x = parent(i)

        if (x == i):
            if (sz[i][0] == sz[i][1]):
                ne += 1
            elif (sz[i][0] > sz[i][1]):
                ma += 1
            else:
                pe += 1

    print("P =",pe,"\nM =",ma,"\nN =",ne)

# Driver code

# Nodes at each index ( 1 - base indexing )
nodes = [ 'P', 'M', 'P', 'M', 'P' ]

# Connected Pairs
connect = [ [ 1, 3 ],
            [ 3, 5 ],
            [ 4, 5 ] ]

influenced(nodes, connect)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG{

// To store the parents
// of the current node
static List<int> par = new List<int>();

// To store the size of M and P
static List<List<int>> sz = new List<List<int>>();

// Function for initialization
static void init(List<char> nodes)
{

    // Size of the graph
    int n = nodes.Count;
    for(int i = 0; i <= n; ++i)
    {
        par.Add(i);

        if (i == 0)
        {
            sz.Add(new List<int>(){0, 0});
        }

        if (i > 0)
        {

            // If the node is P
            if (nodes[i - 1] == 'P')
            {
                sz.Add(new List<int>(){0, 1});

            }

            // If the node is M
            else
            {
                sz.Add(new List<int>(){1, 0});
            }
        }
    }
}

// To find the parent of
// the current node
static int parent(int i)
{
    while (par[i] != i)
    {
        i = par[i];
    }
    return i;
}

// Merge function
static void union(int a, int b)
{
    a = parent(a);
    b = parent(b);

    if (a == b)
    {
        return;
    }

    // Total size by adding number
    // of M and P
    int sz_a = sz[a][0] + sz[a][1];
    int sz_b = sz[b][0] + sz[b][1];

    if (sz_a < sz_b)
    {
        int temp = a;
        a = b;
        b = temp;
    }

    par[b] = a;
    sz[a][0] += sz[b][0];
    sz[a][1] += sz[b][1];
    return;
}

// Function to calculate the influenced value
static void influenced(List<char> nodes,
                       List<List<int>> connect)
{

    // Number of nodes
    int n = nodes.Count;

    // Initialization function
    init(nodes);

    // Size of the connected vector
    int k = connect.Count;

    // Performing union operation
    for(int i = 0; i < k; ++i)
    {
        union(connect[i][0], connect[i][1]);
    }

    // ne = Number of neutal groups
    // ma = Number of M influenced groups
    // pe = Number of P influenced groups
    int ne = 0, ma = 0, pe = 0;
    for(int i = 1; i <= n; ++i)
    {
        int x = parent(i);

        if (x == i)
        {
            if (sz[i][0] == sz[i][1])
            {
                ne++;
            }
            else if (sz[i][0] > sz[i][1])
            {
                ma++;
            }
            else
            {
                pe++;
            }
        }
    }
    Console.WriteLine("P = " + pe + "\nM = " +
                      ma + "\nN = " + ne);
}

// Driver code
static public void Main()
{

    // Nodes at each index ( 1 - base indexing )
    List<char> nodes = new List<char>(){'P', 'M', 'P', 'M', 'P'};

    // Connected Pairs
    List<List<int>> connect = new List<List<int>>();
    connect.Add(new List<int>(){1, 3});
    connect.Add(new List<int>(){3, 5});
    connect.Add(new List<int>(){4, 5});

    influenced(nodes, connect);
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// To store the parents
// of the current node
let par = [];

// To store the size of M and P
let sz = [];

// Function for initialization
function init(nodes)
{
    // Size of the graph
    let n = nodes.length;
    for(let i = 0; i <= n; ++i)
    {
        par.push(i);

        if (i == 0)
        {
            sz.push([0,0]);
        }

        if (i > 0)
        {

            // If the node is P
            if (nodes[i - 1] == 'P')
            {
                sz.push([0,1]);
            }

            // If the node is M
            else
            {
                sz.push([1,0]);
            }
        }
    }
}

// To find the parent of
// the current node
function parent(i)
{
    while (par[i] != i)
    {
        i = par[i];
    }
    return i;
}

// Merge function
function union(a,b)
{
    a = parent(a);
    b = parent(b);

    if (a == b)
    {
        return;
    }

    // Total size by adding number
    // of M and P
    let sz_a = sz[a][0] +
               sz[a][1];
    let sz_b = sz[b][0] +
               sz[b][1];

    if (sz_a < sz_b)
    {
        let temp = a;
        a = b;
        b = temp;
    }
    par[b] = a;

    sz[a][0] = sz[a][0] +
                     sz[b][0];
    sz[a][1] = sz[a][1] +
                     sz[b][1];
    return;
}

// Function to calculate the influenced value
function influenced(nodes,connect)
{
    // Number of nodes
    let n = nodes.length;

    // Initialization function
    init(nodes);

    // Size of the connected vector
    let k = connect.length;

    // Performing union operation
    for(let i = 0; i < k; ++i)
    {
        union(connect[i][0],
             connect[i][1]);
    }

    // ne = Number of neutal groups
    // ma = Number of M influenced groups
    // pe = Number of P influenced groups
    let ne = 0, ma = 0, pe = 0;
    for(let i = 1; i <= n; ++i)
    {
        let x = parent(i);

        if (x == i)
        {
            if (sz[i][0] ==
                sz[i][1])
            {
                ne++;
            }
            else if (sz[i][0] >
                     sz[i][1])
            {
                ma++;
            }
            else
            {
                pe++;
            }
        }
    }
    document.write("P = " + pe +
                     "<br>M = " + ma +
                     "<br>N = " + ne);
}

// Driver code
// Nodes at each index ( 1 - base indexing )
let nodes =[];
nodes.push('P');
nodes.push('M');
nodes.push('P');
nodes.push('M');
nodes.push('P');

// Connected Pairs
let connect = [];
connect.push([1,3]);
connect.push([3,5]);
connect.push([4,5]);

influenced(nodes, connect);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
P = 1
M = 1
N = 0
```

**时间复杂度:** O(N)。
**辅助空间** : O(N)。