# 欧拉游|使用线段树的子树和

> 原文:[https://www . geesforgeks . org/Euler-tour-subtree-sum-using-segment-tree/](https://www.geeksforgeeks.org/euler-tour-subtree-sum-using-segment-tree/)

**欧拉巡树(ETT)** 是一种将有根树表示为数字序列的方法。当使用[深度搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)遍历树时，将每个节点插入一个向量中两次，一次在进入该向量时，下一次在访问其所有子节点后。这个方法对于解决子树问题非常有用，其中一个问题就是**子树和。**

**先决条件:** [分段树(给定范围之和)](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)

**天真方法:**
考虑一棵有 6 个顶点相连的有根树，如下图所示。对不同的查询应用 DFS。
**与每个节点相关联的权重写在括号内。**

![](img/488ae39bed80c2cc6a501a4108f2023a.png)

**查询:**
1。节点 1 的所有子树之和。
2。将节点 6 的值更新为 10。
3。节点 2 的所有子树之和。

**答案:**
1。6 + 5 + 4 + 3 + 2 + 1 = 21
2。

![](img/cb45a3c5032f7038ed45f6b9bd68d3d6.png)

3.10 + 5 + 2 = 17
**时间复杂度分析:**
这样的查询可以使用 **O(n)** 时间复杂度中的搜索深度(dfs)来执行。

**高效方法:**
通过使用欧拉巡回技术将根树转换成段树，可以将这种查询的时间复杂度降低到 **O(log(n))** 时间。所以，当查询数为 q 时，总复杂度变为 **O(q*5log(n))** 。

**欧拉漫游:**
在欧拉漫游技术中，每个顶点都被添加到向量中两次，一次是下降到向量中，一次是离开向量。
借助前面的例子让我们理解:

![](img/488ae39bed80c2cc6a501a4108f2023a.png)

在给定的根树上使用欧拉巡回技术执行深度搜索(DFS)时，如此形成的向量为:

```
s[]={1, 2, 6, 6, 5, 5, 2, 3, 4, 4, 3, 1}
```

## C++

```
// DFS function to traverse the tree
int dfs(int root)
{
    s.push_back(root);
    if (v[root].size() == 0)
        return root;

    for (int i = 0; i & lt; v[root].size(); i++) {
        int temp = dfs(v[root][i]);
        s.push_back(temp);
    }
    return root;
}
```

## java 描述语言

```
<script>

// DFS function to traverse the tree
function dfs(root)
{
    s.push(root);
    if (v[root].length == 0)
        return root;

    for (var i = 0; i & lt; v[root].length; i++) {
        var temp = dfs(v[root][i]);
        s.push(temp);
    }
    return root;
}

// This code is contributed by itsok.
</script>
```

现在，使用向量 s[ ]来 [**创建线段树**](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/) 。

下面是向量 s[ ]的线段树的表示。

![](img/cd3fbff06e03242a81e10e9d189a3c43.png)

对于输出和更新查询，存储根树的每个节点的进入时间和退出时间(作为索引范围)。

```
s[]={1, 2, 6, 6, 5, 5, 2, 3, 4, 4, 3, 1}

Node  Entry time  Exit time
   1        1           12
   2        2           7
   3        8           11
   4        9           10
   5        5           6
   6        3           4
```

**类型 1 的查询:**
查找段树上的范围和进行输出查询，范围为根树节点的退出时间和进入时间。推断答案总是预期答案的两倍，因为每个节点在段树中被添加了两次。所以把答案减少一半。

**类型 2 的查询:**
更新查询，在根树节点的进入时间和退出时间更新段树的叶节点。

**以下是上述方法的实施:**

## C++

```
// C++ program for implementation of
// Euler Tour | Subtree Sum.
#include <bits/stdc++.h>
using namespace std;

vector<int> v[1001];
vector<int> s;
int seg[1001] = { 0 };

// Value/Weight of each node of tree,
// value of 0th(no such node) node is 0.
int ar[] = { 0, 1, 2, 3, 4, 5, 6 };

int vertices = 6;
int edges = 5;

// A recursive function that constructs
// Segment Tree for array ar[] = { }.
// 'pos' is index of current node
// in segment tree seg[].
int segment(int low, int high, int pos)
{
    if (high == low) {
        seg[pos] = ar[s[low]];
    }
    else {
        int mid = (low + high) / 2;
        segment(low, mid, 2 * pos);
        segment(mid + 1, high, 2 * pos + 1);
        seg[pos] = seg[2 * pos] + seg[2 * pos + 1];
    }
}

/* Return sum of elements in range
   from index l to r . It uses the
   seg[] array created using segment()
   function. 'pos' is index of current
   node in segment tree seg[].
*/
int query(int node, int start,
          int end, int l, int r)
{
    if (r < start || end < l) {
        return 0;
    }

    if (l <= start && end <= r) {
        return seg[node];
    }

    int mid = (start + end) / 2;
    int p1 = query(2 * node, start,
                   mid, l, r);
    int p2 = query(2 * node + 1, mid + 1,
                   end, l, r);

    return (p1 + p2);
}

/* A recursive function to update the
   nodes which have the given index in
   their range. The following are
   parameters pos --> index of current
   node in segment tree seg[]. idx -->
   index of the element to be updated.
   This index is in input array.
   val --> Value to be change at node idx
*/
int update(int pos, int low, int high,
           int idx, int val)
{
    if (low == high) {
        seg[pos] = val;
    }
    else {
        int mid = (low + high) / 2;

        if (low <= idx && idx <= mid) {
            update(2 * pos, low, mid,
                   idx, val);
        }
        else {
            update(2 * pos + 1, mid + 1,
                   high, idx, val);
        }

        seg[pos] = seg[2 * pos] + seg[2 * pos + 1];
    }
}

/* A recursive function to form array
    ar[] from a directed tree .
*/
int dfs(int root)
{
    // pushing each node in vector s
    s.push_back(root);
    if (v[root].size() == 0)
        return root;

    for (int i = 0; i < v[root].size(); i++) {
        int temp = dfs(v[root][i]);
        s.push_back(temp);
    }
    return root;
}

// Driver program to test above functions
int main()
{
    // Edges between the nodes
    v[1].push_back(2);
    v[1].push_back(3);
    v[2].push_back(6);
    v[2].push_back(5);
    v[3].push_back(4);

    // Calling dfs function.
    int temp = dfs(1);
    s.push_back(temp);

    // Storing entry time and exit
    // time of each node
    vector<pair<int, int> > p;

    for (int i = 0; i <= vertices; i++)
        p.push_back(make_pair(0, 0));

    for (int i = 0; i < s.size(); i++) {
        if (p[s[i]].first == 0)
            p[s[i]].first = i + 1;
        else
            p[s[i]].second = i + 1;
    }

    // Build segment tree from array ar[].
    segment(0, s.size() - 1, 1);

    // query of type 1 return the
    // sum of subtree at node 1.
    int node = 1;
    int e = p[node].first;
    int f = p[node].second;

    int ans = query(1, 1, s.size(), e, f);

    // print the sum of subtree
    cout << "Subtree sum of node " << node << " is : " << (ans / 2) << endl;

    // query of type 2 return update
    // the subtree at node 6.
    int val = 10;
    node = 6;

    e = p[node].first;
    f = p[node].second;
    update(1, 1, s.size(), e, val);
    update(1, 1, s.size(), f, val);

    // query of type 1 return the
    // sum of subtree at node 2.
    node = 2;

    e = p[node].first;
    f = p[node].second;

    ans = query(1, 1, s.size(), e, f);

    // print the sum of subtree
    cout << "Subtree sum of node " << node << " is : " << (ans / 2) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementation of
// Euler Tour | Subtree Sum.
import java.util.ArrayList;

class Graph{

static class Pair
{
    int first, second;

    public Pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

@SuppressWarnings("unchecked")
static ArrayList<Integer>[] v = new ArrayList[1001];
static ArrayList<Integer> s = new ArrayList<>();
static int[] seg = new int[1001];

// Value/Weight of each node of tree,
// value of 0th(no such node) node is 0.
static int ar[] = { 0, 1, 2, 3, 4, 5, 6 };

static int vertices = 6;
static int edges = 5;

// A recursive function that constructs
// Segment Tree for array ar[] = { }.
// 'pos' is index of current node
// in segment tree seg[].
static void segment(int low, int high, int pos)
{
    if (high == low)
    {
        seg[pos] = ar[s.get(low)];
    }
    else
    {
        int mid = (low + high) / 2;
        segment(low, mid, 2 * pos);
        segment(mid + 1, high, 2 * pos + 1);
        seg[pos] = seg[2 * pos] + seg[2 * pos + 1];
    }
}

// Return sum of elements in range from index
// l to r. It uses the seg[] array created
// using segment() function. 'pos' is index
// of current node in segment tree seg[].
static int query(int node, int start,
                 int end, int l, int r)
{
    if (r < start || end < l)
    {
        return 0;
    }

    if (l <= start && end <= r)
    {
        return seg[node];
    }

    int mid = (start + end) / 2;
    int p1 = query(2 * node, start,
                       mid, l, r);
    int p2 = query(2 * node + 1, mid + 1,
                       end, l, r);

    return (p1 + p2);
}

/*
 * A recursive function to update the nodes which
 * have the given index in their range.
 * The following are parameters
 * pos --> index of current node in segment tree seg[].
 * idx --> index of the element to be updated.
 *         This index is in input array.
 * val --> Value to be change at node idx
 */
static void update(int pos, int low, int high,
                   int idx, int val)
{
    if (low == high)
    {
        seg[pos] = val;
    }
    else
    {
        int mid = (low + high) / 2;

        if (low <= idx && idx <= mid)
        {
            update(2 * pos, low, mid,
                       idx, val);
        }
        else
        {
            update(2 * pos + 1, mid + 1,
                       high, idx, val);
        }

        seg[pos] = seg[2 * pos] +
                   seg[2 * pos + 1];
    }
}

// A recursive function to form array
// ar[] from a directed tree.
static int dfs(int root)
{

    // Pushing each node in ArrayList s
    s.add(root);

    if (v[root].size() == 0)
        return root;

    for(int i = 0; i < v[root].size(); i++)
    {
        int temp = dfs(v[root].get(i));
        s.add(temp);
    }
    return root;
}

// Driver code
public static void main(String[] args)
{
    for(int i = 0; i < 1001; i++)
    {
        v[i] = new ArrayList<>();
    }

    // Edges between the nodes
    v[1].add(2);
    v[1].add(3);
    v[2].add(6);
    v[2].add(5);
    v[3].add(4);

    // Calling dfs function.
    int temp = dfs(1);
    s.add(temp);

    // Storing entry time and exit
    // time of each node
    ArrayList<Pair> p = new ArrayList<>();

    for(int i = 0; i <= vertices; i++)
        p.add(new Pair(0, 0));

    for(int i = 0; i < s.size(); i++)
    {
        if (p.get(s.get(i)).first == 0)
            p.get(s.get(i)).first = i + 1;
        else
            p.get(s.get(i)).second = i + 1;
    }

    // Build segment tree from array ar[].
    segment(0, s.size() - 1, 1);

    // Query of type 1 return the
    // sum of subtree at node 1.
    int node = 1;
    int e = p.get(node).first;
    int f = p.get(node).second;

    int ans = query(1, 1, s.size(), e, f);

    // Print the sum of subtree
    System.out.println("Subtree sum of node " +
                       node + " is : " + (ans / 2));

    // Query of type 2 return update
    // the subtree at node 6.
    int val = 10;
    node = 6;

    e = p.get(node).first;
    f = p.get(node).second;
    update(1, 1, s.size(), e, val);
    update(1, 1, s.size(), f, val);

    // Query of type 1 return the
    // sum of subtree at node 2.
    node = 2;

    e = p.get(node).first;
    f = p.get(node).second;

    ans = query(1, 1, s.size(), e, f);

    // Print the sum of subtree
    System.out.println("Subtree sum of node " +
                       node + " is : " + (ans / 2));
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program for implementation of
# Euler Tour | Subtree Sum.
v = [[] for i in range(1001)]
s = []
seg = [0]*1001

# Value/Weight of each node of tree,
# value of 0th(no such node) node is 0.
ar = [0, 1, 2, 3, 4, 5, 6]

vertices = 6
edges = 5

# A recursive function that constructs
# Segment Tree for array ar = .
# 'pos' is index of current node
# in segment tree seg.
def segment(low, high, pos):
    if (high == low):
        seg[pos] = ar[s[low]]
    else:
        mid = (low + high) // 2
        segment(low, mid, 2 * pos)
        segment(mid + 1, high, 2 * pos + 1)
        seg[pos] = seg[2 * pos] + seg[2 * pos + 1]

''' Return sum of elements in range
from index l to r . It uses the
seg array created using segment()
function. 'pos' is index of current
node in segment tree seg.
'''
def query(node, start,end, l, r):
    if (r < start or end < l):
        return 0

    if (l <= start and end <= r):
        return seg[node]

    mid = (start + end) // 2
    p1 = query(2 * node, start,mid, l, r)
    p2 = query(2 * node + 1, mid + 1, end, l, r)

    return (p1 + p2)

''' A recursive function to update the
nodes which have the given index in
their range. The following are
parameters pos --> index of current
node in segment tree seg. idx -->
index of the element to be updated.
This index is in input array.
val --> Value to be change at node idx
'''
def update(pos, low, high, idx, val):
    if (low == high):
        seg[pos] = val
    else:
        mid = (low + high) // 2
        if (low <= idx and idx <= mid):
            update(2 * pos, low, mid,idx, val)
        else:
            update(2 * pos + 1, mid + 1, high, idx, val)

        seg[pos] = seg[2 * pos] + seg[2 * pos + 1]

''' A recursive function to form array
    ar from a directed tree .
'''
def dfs(root):

    # pushing each node in vector s
    s.append(root)
    if (len(v[root]) == 0):
        return root

    for i in range(len(v[root])):
        temp = dfs(v[root][i])
        s.append(temp)

    return root

# Edges between the nodes
v[1].append(2)
v[1].append(3)
v[2].append(6)
v[2].append(5)
v[3].append(4)

# Calling dfs function.
temp = dfs(1)
s.append(temp)

# Storing entry time and exit
# time of each node
p = []

for i in range(vertices + 1):
    p.append([0, 0])

for i in range(len(s)):
    if (p[s[i]][0] == 0):
        p[s[i]][0] = i + 1
    else:
        p[s[i]][1] = i + 1

# Build segment tree from array ar.
segment(0, len(s) - 1, 1)

# query of type 1 return the
# sum of subtree at node 1.
node = 1
e = p[node][0]
f = p[node][1]

ans = query(1, 1, len(s), e, f)

# print the sum of subtree
print("Subtree sum of node", node, "is :", ans // 2)

# query of type 2 return update
# the subtree at node 6.
val = 10
node = 6

e = p[node][0]
f = p[node][1]
update(1, 1, len(s), e, val)
update(1, 1, len(s), f, val)

# query of type 1 return the
# sum of subtree at node 2.
node = 2

e = p[node][0]
f = p[node][1]

ans = query(1, 1, len(s), e, f)

# print the sum of subtree
print("Subtree sum of node",node,"is :",ans // 2)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program for implementation of
// Euler Tour | Subtree Sum.
using System;
using System.Collections.Generic;
class GFG {

    static List<List<int>> v = new List<List<int>>();
    static List<int> s = new List<int>();
    static int[] seg = new int[1001];

    // Value/Weight of each node of tree,
    // value of 0th(no such node) node is 0.
    static int[] ar = { 0, 1, 2, 3, 4, 5, 6 };

    static int vertices = 6;

    // A recursive function that constructs
    // Segment Tree for array ar[] = { }.
    // 'pos' is index of current node
    // in segment tree seg[].
    static void segment(int low, int high, int pos)
    {
        if (high == low)
        {
            seg[pos] = ar[s[low]];
        }
        else
        {
            int mid = (low + high) / 2;
            segment(low, mid, 2 * pos);
            segment(mid + 1, high, 2 * pos + 1);
            seg[pos] = seg[2 * pos] + seg[2 * pos + 1];
        }
    }

    // Return sum of elements in range from index
    // l to r. It uses the seg[] array created
    // using segment() function. 'pos' is index
    // of current node in segment tree seg[].
    static int query(int node, int start,
                     int end, int l, int r)
    {
        if (r < start || end < l)
        {
            return 0;
        }

        if (l <= start && end <= r)
        {
            return seg[node];
        }

        int mid = (start + end) / 2;
        int p1 = query(2 * node, start,
                           mid, l, r);
        int p2 = query(2 * node + 1, mid + 1,
                           end, l, r);

        return (p1 + p2);
    }

    /*
     * A recursive function to update the nodes which
     * have the given index in their range.
     * The following are parameters
     * pos --> index of current node in segment tree seg[].
     * idx --> index of the element to be updated.
     *         This index is in input array.
     * val --> Value to be change at node idx
     */
    static void update(int pos, int low, int high,
                       int idx, int val)
    {
        if (low == high)
        {
            seg[pos] = val;
        }
        else
        {
            int mid = (low + high) / 2;

            if (low <= idx && idx <= mid)
            {
                update(2 * pos, low, mid,
                           idx, val);
            }
            else
            {
                update(2 * pos + 1, mid + 1,
                           high, idx, val);
            }

            seg[pos] = seg[2 * pos] +
                       seg[2 * pos + 1];
        }
    }

    // A recursive function to form array
    // ar[] from a directed tree.
    static int dfs(int root)
    {

        // Pushing each node in ArrayList s
        s.Add(root);

        if (v[root].Count == 0)
            return root;

        for(int i = 0; i < v[root].Count; i++)
        {
            int temp = dfs(v[root][i]);
            s.Add(temp);
        }
        return root;
    }

  static void Main() {
    for(int i = 0; i < 1001; i++)
    {
        v.Add(new List<int>());
    }

    // Edges between the nodes
    v[1].Add(2);
    v[1].Add(3);
    v[2].Add(6);
    v[2].Add(5);
    v[3].Add(4);

    // Calling dfs function.
    int temp = dfs(1);
    s.Add(temp);

    // Storing entry time and exit
    // time of each node
    List<Tuple<int,int>> p = new List<Tuple<int,int>>();

    for(int i = 0; i <= vertices; i++)
        p.Add(new Tuple<int,int>(0, 0));

    for(int i = 0; i < s.Count; i++)
    {
        if (p[s[i]].Item1 == 0)
        {
            p[s[i]] = new Tuple<int,int>(i + 1, p[s[i]].Item2);
        }
        else
            p[s[i]] = new Tuple<int,int>(p[s[i]].Item1, i + 1);
    }

    // Build segment tree from array ar[].
    segment(0, s.Count - 1, 1);

    // Query of type 1 return the
    // sum of subtree at node 1.
    int node = 1;
    int e = p[node].Item1;
    int f = p[node].Item2;

    int ans = query(1, 1, s.Count, e, f);

    // Print the sum of subtree
    Console.WriteLine("Subtree sum of node " +
                       node + " is : " + (ans / 2));

    // Query of type 2 return update
    // the subtree at node 6.
    int val = 10;
    node = 6;

    e = p[node].Item1;
    f = p[node].Item2;
    update(1, 1, s.Count, e, val);
    update(1, 1, s.Count, f, val);

    // Query of type 1 return the
    // sum of subtree at node 2.
    node = 2;

    e = p[node].Item1;
    f = p[node].Item2;

    ans = query(1, 1, s.Count, e, f);

    // Print the sum of subtree
    Console.WriteLine("Subtree sum of node " +
                       node + " is : " + (ans / 2));
  }
}

// This code is contributed by rameshtravel07.
```

## java 描述语言

```
<script>

// Javascript program for implementation of
// Euler Tour | Subtree Sum.
let v = new Array(1001);
let s = [];
let seg = new Array(1001);
seg.fill(0);

// Value/Weight of each node of tree,
// value of 0th(no such node) node is 0.
let ar = [ 0, 1, 2, 3, 4, 5, 6 ];

let vertices = 6;
let edges = 5;

// A recursive function that constructs
// Segment Tree for array ar[] = { }.
// 'pos' is index of current node
// in segment tree seg[].
function segment(low, high, pos)
{
    if (high == low)
    {
        seg[pos] = ar[s[low]];
    }
    else
    {
        let mid = parseInt((low + high) / 2, 10);
        segment(low, mid, 2 * pos);
        segment(mid + 1, high, 2 * pos + 1);
        seg[pos] = seg[2 * pos] + seg[2 * pos + 1];
    }
}

/* Return sum of elements in range
   from index l to r . It uses the
   seg[] array created using segment()
   function. 'pos' is index of current
   node in segment tree seg[].
*/
function query(node, start, end, l, r)
{
    if (r < start || end < l)
    {
        return 0;
    }

    if (l <= start && end <= r)
    {
        return seg[node];
    }

    let mid = parseInt((start + end) / 2, 10);
    let p1 = query(2 * node, start, mid, l, r);
    let p2 = query(2 * node + 1, mid + 1,
                       end, l, r);

    return (p1 + p2);
}

/* A recursive function to update the
   nodes which have the given index in
   their range. The following are
   parameters pos --> index of current
   node in segment tree seg[]. idx -->
   index of the element to be updated.
   This index is in input array.
   val --> Value to be change at node idx
*/
function update(pos, low, high, idx, val)
{
    if (low == high)
    {
        seg[pos] = val;
    }
    else
    {
        let mid = parseInt((low + high) / 2, 10);

        if (low <= idx && idx <= mid)
        {
            update(2 * pos, low, mid, idx, val);
        }
        else
        {
            update(2 * pos + 1, mid + 1,
                   high, idx, val);
        }
        seg[pos] = seg[2 * pos] +
                   seg[2 * pos + 1];
    }
}

/* A recursive function to form array
    ar[] from a directed tree .
*/
function dfs(root)
{

    // Pushing each node in vector s
    s.push(root);
    if (v[root].length == 0)
        return root;

    for(let i = 0; i < v[root].length; i++)
    {
        let temp = dfs(v[root][i]);
        s.push(temp);
    }
    return root;
}

// Driver code
for(let i = 0; i < v.length; i++)
{
    v[i] = [];
}

// Edges between the nodes
v[1].push(2);
v[1].push(3);
v[2].push(6);
v[2].push(5);
v[3].push(4);

// Calling dfs function.
let temp = dfs(1);
s.push(temp);

// Storing entry time and exit
// time of each node
let p = [];

for(let i = 0; i <= vertices; i++)
    p.push([0, 0]);

for(let i = 0; i < s.length; i++)
{
    if (p[s[i]][0] == 0)
        p[s[i]][0] = i + 1;
    else
        p[s[i]][1] = i + 1;
}

// Build segment tree from array ar[].
segment(0, s.length - 1, 1);

// query of type 1 return the
// sum of subtree at node 1.
let node = 1;
let e = p[node][0];
let f = p[node][1];

let ans = query(1, 1, s.length, e, f);

// Print the sum of subtree
document.write("Subtree sum of node " + node +
               " is : " + parseInt(ans / 2, 10) +
               "</br>");

// Query of type 2 return update
// the subtree at node 6.
let val = 10;
node = 6;

e = p[node][0];
f = p[node][1];
update(1, 1, s.length, e, val);
update(1, 1, s.length, f, val);

// Query of type 1 return the
// sum of subtree at node 2.
node = 2;

e = p[node][0];
f = p[node][1];

ans = query(1, 1, s.length, e, f);

// Print the sum of subtree
document.write("Subtree sum of node " + node +
               " is : " + parseInt(ans / 2, 10) +
               "</br>");

// This code is contributed by decode2207

</script>
```

**Output:** 

```
Subtree sum of node 1 is : 21
Subtree sum of node 2 is : 17
```

**时间复杂度:** O(q*log(n))