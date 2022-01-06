# 给定范围内二进制数组中两个 1 之间的最大距离

> 原文:[https://www . geesforgeks . org/给定范围内二进制数组中两个 1 之间的最大距离/](https://www.geeksforgeeks.org/maximum-distance-between-two-1s-in-a-binary-array-in-a-given-range/)

给定大小为 **N** 的二进制数组和**【l，r】**的范围，任务是在这个给定范围内找到两个 1 之间的最大距离。
**例:**

> **输入:** arr = {1，0，0，1}，l = 0，r = 3
> **输出:** 3
> 在从 0 到 3 的给定范围内，第一个 1 位于索引 0，最后一个位于索引 3。
> 因此，最大距离= 3–0 = 3。
> 
> **输入:** arr = {1，1，0，1，0，1，0，1，0，1，0，1，1，0}，l = 3，r = 9
> T3】输出: 6

**方法:**我们将创建一个[线段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)来解决这个问题。

1.  段树中的每个节点将具有最左边 1 和最右边 1 的索引，以及一个整数，该整数包含在[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/) {l，r}中值为 1 的任何元素之间的最大距离。
2.  现在，在这个段树中，我们可以合并左节点和右节点，如下所示:
    *   如果左节点无效，返回右节点。
    *   如果右节点无效，返回左节点。
    *   如果一个节点包含至少一个 0 或至少一个 1，则该节点有效。
    *   如果左节点和右节点都有效，那么:
        Let，
        *   l1 =的最左边索引(-1，如果 0 不存在于该间隔中)
        *   r1 =最右边的索引 1 (-1，如果 0 在该间隔中不存在)
        *   max1 =两个 1 之间的最大距离
        *   合并节点中 max1 的值将是左右节点中 max1 的最大值，以及右节点中最右边索引 1 和左节点中最左边索引 1 之间的差值。
        *   如果不是-1，合并节点中 l1 的值将是左节点的 l1，否则是右节点的 l1。
        *   如果不是-1，合并节点中 r1 的值将是右节点的 r1，否则是左节点的 r1。
3.  然后，最后为了找到答案，我们只需要调用给定范围{l，r}的查询函数。

下面是上述方法的实现:

## C++

```
// C++ program to find the maximum
// distance between two elements
// with value 1 within a subarray (l, r)

#include <bits/stdc++.h>
using namespace std;

// Structure for each node
// in the segment tree
struct node {
    int l1, r1;
    int max1;
} seg[100001];

// A utility function for
// merging two nodes
node task(node l, node r)
{
    node x;

    x.l1 = (l.l1 != -1) ? l.l1 : r.l1;
    x.r1 = (r.r1 != -1) ? r.r1 : l.r1;
    x.max1 = max(l.max1, r.max1);

    if (l.l1 != -1 && r.r1 != -1)
        x.max1 = max(x.max1, r.r1 - l.l1);

    return x;
}

// A recursive function that constructs
// Segment Tree for given string
void build(int qs, int qe, int ind, int arr[])
{
    // If start is equal to end then
    // insert the array element
    if (qs == qe) {
        if (arr[qs] == 1) {
            seg[ind].l1 = seg[ind].r1 = qs;
            seg[ind].max1 = INT_MIN;
        }
        else {
            seg[ind].l1 = seg[ind].r1 = -1;
            seg[ind].max1 = INT_MIN;
        }

        return;
    }
    int mid = (qs + qe) >> 1;

    // Build the segment tree
    // for range qs to mid
    build(qs, mid, ind << 1, arr);

    // Build the segment tree
    // for range mid+1 to qe
    build(mid + 1, qe, ind << 1 | 1, arr);

    // merge the two child nodes
    // to obtain the parent node
    seg[ind] = task(
        seg[ind << 1],
        seg[ind << 1 | 1]);
}

// Query in a range qs to qe
node query(int qs, int qe,
           int ns, int ne, int ind)
{
    node x;
    x.l1 = x.r1 = -1;
    x.max1 = INT_MIN;

    // If the range lies in this segment
    if (qs <= ns && qe >= ne)
        return seg[ind];

    // If the range is out of the bounds
    // of this segment
    if (ne < qs || ns > qe || ns > ne)
        return x;

    // Else query for the right and left
    // child node of this subtree
    // and merge them
    int mid = (ns + ne) >> 1;

    node l = query(qs, qe, ns,
                   mid, ind << 1);
    node r = query(qs, qe,
                   mid + 1, ne,
                   ind << 1 | 1);

    x = task(l, r);
    return x;
}

// Driver code
int main()
{

    int arr[] = { 1, 1, 0,
                  1, 0, 1,
                  0, 1, 0,
                  1, 0, 1,
                  1, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int l = 3, r = 9;

    // Build the segment tree
    build(0, n - 1, 1, arr);

    // Query in range 3 to 9
    node ans = query(l, r, 0, n - 1, 1);
    cout << ans.max1 << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// distance between two elements
// with value 1 within a subarray (l, r)
import java.util.*;

class GFG{

// Structure for each node
// in the segment tree
static class node {
    int l1, r1;
    int max1;
}
static node []seg = new node[100001];

// A utility function for
// merging two nodes
static node task(node l, node r)
{
    node x = new node();

    x.l1 = (l.l1 != -1) ? l.l1 : r.l1;
    x.r1 = (r.r1 != -1) ? r.r1 : l.r1;
    x.max1 = Math.max(l.max1, r.max1);

    if (l.l1 != -1 && r.r1 != -1)
        x.max1 = Math.max(x.max1, r.r1 - l.l1);

    return x;
}

// A recursive function that constructs
// Segment Tree for given String
static void build(int qs, int qe, int ind, int arr[])
{
    // If start is equal to end then
    // insert the array element
    if (qs == qe) {
        if (arr[qs] == 1) {
            seg[ind].l1 = seg[ind].r1 = qs;
            seg[ind].max1 = Integer.MIN_VALUE;
        }
        else {
            seg[ind].l1 = seg[ind].r1 = -1;
            seg[ind].max1 = Integer.MIN_VALUE;
        }

        return;
    }
    int mid = (qs + qe) >> 1;

    // Build the segment tree
    // for range qs to mid
    build(qs, mid, ind << 1, arr);

    // Build the segment tree
    // for range mid+1 to qe
    build(mid + 1, qe, ind << 1 | 1, arr);

    // merge the two child nodes
    // to obtain the parent node
    seg[ind] = task(
        seg[ind << 1],
        seg[ind << 1 | 1]);
}

// Query in a range qs to qe
static node query(int qs, int qe,
           int ns, int ne, int ind)
{
    node x = new node();
    x.l1 = x.r1 = -1;
    x.max1 = Integer.MIN_VALUE;

    // If the range lies in this segment
    if (qs <= ns && qe >= ne)
        return seg[ind];

    // If the range is out of the bounds
    // of this segment
    if (ne < qs || ns > qe || ns > ne)
        return x;

    // Else query for the right and left
    // child node of this subtree
    // and merge them
    int mid = (ns + ne) >> 1;

    node l = query(qs, qe, ns,
                   mid, ind << 1);
    node r = query(qs, qe,
                   mid + 1, ne,
                   ind << 1 | 1);

    x = task(l, r);
    return x;
}

// Driver code
public static void main(String[] args)
{

    for(int i= 0; i < 100001; i++)
        seg[i] = new node();
    int arr[] = { 1, 1, 0,
                  1, 0, 1,
                  0, 1, 0,
                  1, 0, 1,
                  1, 0 };
    int n = arr.length;
    int l = 3, r = 9;

    // Build the segment tree
    build(0, n - 1, 1, arr);

    // Query in range 3 to 9
    node ans = query(l, r, 0, n - 1, 1);
    System.out.print(ans.max1+ "\n");

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# distance between two elements
# with value 1 within a subarray (l, r)
import sys

# Structure for each node
# in the segment tree
class node():

    def __init__(self):

        self.l1 = 0
        self.r1 = 0
        self.max1 = 0

seg = [node() for i in range(100001)]

# A utility function for
# merging two nodes
def task(l, r):

    x = node()

    x.l1 = l.l1 if (l.l1 != -1) else r.l1
    x.r1 = r.r1 if (r.r1 != -1)  else l.r1

    x.max1 = max(l.max1, r.max1)

    # If both the nodes are valid
    if (l.r1 != -1 and r.l1 != -1):
        x.max1 = max(x.max1, r.r1 - l.l1)

    return x

# A recursive function that constructs
# Segment Tree for given string
def build(qs, qe, ind, arr):

    # If start is equal to end then
    # insert the array element
    if (qs == qe):

        if (arr[qs] == 1):
            seg[ind].l1 = seg[ind].r1 = qs
            seg[ind].max1 = -sys.maxsize

        else:
            seg[ind].l1 = seg[ind].r1 = -1
            seg[ind].max1 = -sys.maxsize

        return

    mid = (qs + qe) >> 1

    # Build the segment tree
    # for range qs to mid
    build(qs, mid, ind << 1, arr)

    # Build the segment tree
    # for range mid+1 to qe
    build(mid + 1, qe, ind << 1 | 1, arr)

    # Merge the two child nodes
    # to obtain the parent node
    seg[ind] = task(seg[ind << 1],
                    seg[ind << 1 | 1])

# Query in a range qs to qe
def query(qs, qe, ns, ne, ind):

    x = node()
    x.l1 = x.r1 = -1
    x.max1 = -sys.maxsize

    # If the range lies in this segment
    if (qs <= ns and qe >= ne):
        return seg[ind]

    # If the range is out of the bounds
    # of this segment
    if (ne < qs or ns > qe or ns > ne):
        return x

    # Else query for the right and left
    # child node of this subtree
    # and merge them
    mid = (ns + ne) >> 1

    l = query(qs, qe, ns, mid, ind << 1)
    r = query(qs, qe, mid + 1, ne, ind << 1 | 1)

    x = task(l, r)

    return x

# Driver code
if __name__=="__main__":

    arr = [ 1, 1, 0, 1, 0, 1, 0,
            1, 0, 1, 0, 1, 1, 0 ]

    n = len(arr)

    l = 3
    r = 9

    # Build the segment tree
    build(0, n - 1, 1, arr)

    # Query in range 3 to 9
    ans = query(l, r, 0, n - 1, 1)

    print(ans.max1)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find the maximum
// distance between two elements
// with value 1 within a subarray (l, r)
using System;

class GFG{

// Structure for each node
// in the segment tree
class node {
    public int l1, r1;
    public int max1;
}
static node []seg = new node[100001];

// A utility function for
// merging two nodes
static node task(node l, node r)
{
    node x = new node();

    x.l1 = (l.l1 != -1) ? l.l1 : r.l1;
    x.r1 = (r.r1 != -1) ? r.r1 : l.r1;
    x.max1 = Math.Max(l.max1, r.max1);

    if (l.l1 != -1 && r.r1 != -1)
        x.max1 = Math.Max(x.max1, r.r1 - l.l1);

    return x;
}

// A recursive function that constructs
// Segment Tree for given String
static void build(int qs, int qe, int ind, int []arr)
{
    // If start is equal to end then
    // insert the array element
    if (qs == qe) {
        if (arr[qs] == 1) {
            seg[ind].l1 = seg[ind].r1 = qs;
            seg[ind].max1 = int.MinValue;
        }
        else {
            seg[ind].l1 = seg[ind].r1 = -1;
            seg[ind].max1 = int.MinValue;
        }

        return;
    }
    int mid = (qs + qe) >> 1;

    // Build the segment tree
    // for range qs to mid
    build(qs, mid, ind << 1, arr);

    // Build the segment tree
    // for range mid+1 to qe
    build(mid + 1, qe, ind << 1 | 1, arr);

    // merge the two child nodes
    // to obtain the parent node
    seg[ind] = task(
        seg[ind << 1],
        seg[ind << 1 | 1]);
}

// Query in a range qs to qe
static node query(int qs, int qe,
           int ns, int ne, int ind)
{
    node x = new node();
    x.l1 = x.r1 = -1;
    x.max1 = int.MinValue;

    // If the range lies in this segment
    if (qs <= ns && qe >= ne)
        return seg[ind];

    // If the range is out of the bounds
    // of this segment
    if (ne < qs || ns > qe || ns > ne)
        return x;

    // Else query for the right and left
    // child node of this subtree
    // and merge them
    int mid = (ns + ne) >> 1;

    node l = query(qs, qe, ns,
                   mid, ind << 1);
    node r = query(qs, qe,
                   mid + 1, ne,
                   ind << 1 | 1);

    x = task(l, r);
    return x;
}

// Driver code
public static void Main(String[] args)
{

    for(int i = 0; i < 100001; i++)
        seg[i] = new node();
    int []arr = { 1, 1, 0,
                  1, 0, 1,
                  0, 1, 0,
                  1, 0, 1,
                  1, 0 };
    int n = arr.Length;
    int l = 3, r = 9;

    // Build the segment tree
    build(0, n - 1, 1, arr);

    // Query in range 3 to 9
    node ans = query(l, r, 0, n - 1, 1);
    Console.Write(ans.max1+ "\n");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to find the maximum
// distance between two elements
// with value 1 within a subarray (l, r)

// Structure for each node
// in the segment tree
class node {
    constructor()
    {
        this.l1 = 0;
        this.r1 = 0;
        this.max1 =0;
    }
}

var seg = Array(100001);

// A utility function for
// merging two nodes
function task(l, r)
{
    var x = new node();

    x.l1 = (l.l1 != -1) ? l.l1 : r.l1;
    x.r1 = (r.r1 != -1) ? r.r1 : l.r1;
    x.max1 = Math.max(l.max1, r.max1);

    if (l.l1 != -1 && r.r1 != -1)
        x.max1 = Math.max(x.max1, r.r1 - l.l1);

    return x;
}

// A recursive function that constructs
// Segment Tree for given String
function build(qs, qe, ind, arr)
{
    // If start is equal to end then
    // insert the array element
    if (qs == qe) {
        if (arr[qs] == 1) {
            seg[ind].l1 = seg[ind].r1 = qs;
            seg[ind].max1 = -1000000000;
        }
        else {
            seg[ind].l1 = seg[ind].r1 = -1;
            seg[ind].max1 = -1000000000;
        }

        return;
    }
    var mid = (qs + qe) >> 1;

    // Build the segment tree
    // for range qs to mid
    build(qs, mid, ind << 1, arr);

    // Build the segment tree
    // for range mid+1 to qe
    build(mid + 1, qe, ind << 1 | 1, arr);

    // merge the two child nodes
    // to obtain the parent node
    seg[ind] = task(
        seg[ind << 1],
        seg[ind << 1 | 1]);
}

// Query in a range qs to qe
function query(qs, qe, ns, ne, ind)
{
    var x = new node();
    x.l1 = x.r1 = -1;
    x.max1 = -1000000000;

    // If the range lies in this segment
    if (qs <= ns && qe >= ne)
        return seg[ind];

    // If the range is out of the bounds
    // of this segment
    if (ne < qs || ns > qe || ns > ne)
        return x;

    // Else query for the right and left
    // child node of this subtree
    // and merge them
    var mid = (ns + ne) >> 1;

    var l = query(qs, qe, ns,
                   mid, ind << 1);
    var r = query(qs, qe,
                   mid + 1, ne,
                   ind << 1 | 1);

    x = task(l, r);
    return x;
}

// Driver code
for(var i = 0; i < 100001; i++)
    seg[i] = new node();
var arr = [1, 1, 0,
              1, 0, 1,
              0, 1, 0,
              1, 0, 1,
              1, 0];
var n = arr.length;
var l = 3, r = 9;

// Build the segment tree
build(0, n - 1, 1, arr);

// Query in range 3 to 9
var ans = query(l, r, 0, n - 1, 1);
document.write(ans.max1+ "<br>");

</script>
```

**Output:** 

```
6
```