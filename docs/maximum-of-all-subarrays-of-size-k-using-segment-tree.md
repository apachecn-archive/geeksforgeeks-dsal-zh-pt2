# 使用段树

的所有 K 尺寸子阵列的最大值

> 原文:[https://www . geeksforgeeks . org/最大尺寸 k 子阵列使用段树/](https://www.geeksforgeeks.org/maximum-of-all-subarrays-of-size-k-using-segment-tree/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是为每个大小为 **K** 的相邻子数组找到最大值。

**示例:**

> **输入:** arr[] = {1，2，3，1，4，5，2，3，6}，K = 3
> **输出:** 3 3 4 5 5 5 6
> **解释**:
> 1，2，3 的最大值为 3
> 2，3，1 的最大值为 3
> 3，1，4 的最大值为 4
> 1，4，5 的最大值为 5
> 4，5，2 的最大值为 5
> 
> **输入:** arr[] = {8，5，10，7，9，4，15，12，90，13}，K = 4
> **输出:** 10 10 10 15 15 90 90
> **解释:**
> 前 4 个元素的最大值为 10，同样的，后 4 个
> 元素(即从索引 1 到 4)为 10，所以生成的序列
> 为 10 10 10

**逼近** :
思路是用[段树](https://www.geeksforgeeks.org/segment-tree-set-2-range-maximum-query-node-update/)来回答 k 大小所有子阵的最大值

1.  **段树的表示**
    *   叶节点是输入数组的元素。
    *   每个内部节点代表其所有子节点的最大值。
2.  **从给定数组构建段树:**
    *   我们从片段 arr[0]开始。。。n-1]，并且每次我们将当前段分成两半(如果它还没有变成长度为 1 的段)，然后在两半上调用相同的过程，并且对于每个这样的段，我们将最大值存储在段树节点中。
    *   构建的段树的所有层都将被完全填充，除了最后一层。此外，该树将是一个完整的二叉树，因为我们总是在每一层将片段分成两半。
    *   由于构造的树总是一棵有 n 片叶子的完全二叉树，因此将有 n–1 个内部节点。因此总节点数将为 2 * n–1。
    *   段树高度为*原木 <sub>2</sub> n* 。
    *   由于树是用数组表示的，并且父索引和子索引之间的关系必须保持，因此为段树分配的内存大小将是*2 *(2<sup>ceil(log</sup><sub><sup>2</sup></sub><sup>n)</sup>)-1*。

下面是上述方法的实现。

## C++

```
// C++  program to answer Maximum
// of allsubarrays of size k
// using segment tree
#include <bits/stdc++.h>
using namespace std;

#define MAX 1000000

// Size of segment
// tree = 2^{log(MAX)+1}
int st[3 * MAX];

// A utility function to get the
// middle index of given range.
int getMid(int s, int e)
{
    return s + (e - s) / 2;
}
// A recursive function that
// constructs Segment Tree for
// array[s...e]. node is index
// of current node in segment
// tree st
void constructST(int node, int s,
                 int e, int arr[])
{
    // If there is one element in
    // array, store it in current
    // node of segment tree and return
    if (s == e) {
        st[node] = arr[s];
        return;
    }
    // If there are more than
    // one elements, then recur
    // for left and right subtrees
    // and store the max of
    // values in this node
    int mid = getMid(s, e);

    constructST(2 * node, s,
                mid, arr);
    constructST(2 * node + 1,
                mid + 1, e,
                arr);
    st[node] = max(st[2 * node],
                   st[2 * node + 1]);
}

/* A recursive function to get the
   maximum of range[l, r] The
   following parameters for
   this function:

st     -> Pointer to segment tree
node   -> Index of current node in
          the segment tree .
s & e  -> Starting and ending indexes
          of the segment represented
          by current node, i.e., st[node]
l & r  -> Starting and ending indexes
          of range query
 */
int getMax(int node, int s,
           int e, int l,
           int r)
{
    // If segment of this node
    // does not belong to
    // given range
    if (s > r || e < l)
        return INT_MIN;

    // If segment of this node
    // is completely part of
    // given range, then return
    // the max of segment
    if (s >= l && e <= r)
        return st[node];

    // If segment of this node
    // is partially the part
    // of given range
    int mid = getMid(s, e);

    return max(getMax(2 * node,
                      s, mid,
                      l, r),
               getMax(2 * node + 1,
                      mid + 1, e,
                      l, r));
}

// Function to print the max
// of all subarrays of size k
void printKMax(int n, int k)
{
    for (int i = 0; i < n; i++) {
        if ((k - 1 + i) < n)
            cout << getMax(1, 0, n - 1,
                           i, k - 1 + i)
                 << " ";
        else
            break;
    }
}

// Driver code
int main()
{
    int k = 4;
    int arr[] = { 8, 5, 10, 7, 9, 4, 15,
                  12, 90, 13 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function to construct the
    // segment tree
    constructST(1, 0, n - 1, arr);

    printKMax(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to answer Maximum
// of allsubarrays of size k
// using segment tree
import java.io.*;
import java.util.*;

class GFG{

static int MAX = 1000000;

// Size of segment
// tree = 2^{log(MAX)+1}
static int[] st = new int[3 * MAX];

// A utility function to get the
// middle index of given range.
static int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

// A recursive function that
// constructs Segment Tree for
// array[s...e]. node is index
// of current node in segment
// tree st
static void constructST(int node, int s,
                        int e, int[] arr)
{

    // If there is one element in
    // array, store it in current
    // node of segment tree and return
    if (s == e)
    {
        st[node] = arr[s];
        return;
    }

    // If there are more than
    // one elements, then recur
    // for left and right subtrees
    // and store the max of
    // values in this node
    int mid = getMid(s, e);

    constructST(2 * node, s, mid, arr);
    constructST(2 * node + 1,
                mid + 1, e, arr);

    st[node] = Math.max(st[2 * node],
                        st[2 * node + 1]);
}

/* A recursive function to get the
   maximum of range[l, r] The
   following parameters for
   this function:

st     -> Pointer to segment tree
node   -> Index of current node in
          the segment tree .
s & e  -> Starting and ending indexes
          of the segment represented
          by current node, i.e., st[node]
l & r  -> Starting and ending indexes
          of range query
 */
static int getMax(int node, int s, int e,
                            int l, int r)
{

    // If segment of this node
    // does not belong to
    // given range
    if (s > r || e < l)
        return Integer.MIN_VALUE;

    // If segment of this node
    // is completely part of
    // given range, then return
    // the max of segment
    if (s >= l && e <= r)
        return st[node];

    // If segment of this node
    // is partially the part
    // of given range
    int mid = getMid(s, e);

    return Math.max(getMax(2 * node, s,
                           mid, l, r),
                    getMax(2 * node + 1,
                           mid + 1, e, l, r));
}

// Function to print the max
// of all subarrays of size k
static void printKMax(int n, int k)
{
    for(int i = 0; i < n; i++)
    {
        if ((k - 1 + i) < n)
            System.out.print(getMax(1, 0, n - 1,
                                    i, k - 1 + i) + " ");
        else
            break;
    }
}

// Driver code
public static void main(String[] args)
{
    int k = 4;
    int[] arr = { 8, 5, 10, 7, 9,
                  4, 15, 12, 90, 13 };
    int n = arr.length;

    // Function to construct the
    // segment tree
    constructST(1, 0, n - 1, arr);

    printKMax(n, k);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program to answer maximum
# of all subarrays of size k
# using segment tree
import sys

MAX = 1000000

# Size of segment
# tree = 2^{log(MAX)+1}
st = [0] * (3 * MAX)

# A utility function to get the
# middle index of given range.
def getMid(s, e):
    return s + (e - s) // 2

# A recursive function that
# constructs Segment Tree for
# array[s...e]. node is index
# of current node in segment
# tree st
def constructST(node, s, e, arr):

    # If there is one element in
    # array, store it in current
    # node of segment tree and return
    if (s == e):
        st[node] = arr[s]
        return

    # If there are more than
    # one elements, then recur
    # for left and right subtrees
    # and store the max of
    # values in this node
    mid = getMid(s, e)
    constructST(2 * node, s, mid, arr)
    constructST(2 * node + 1, mid + 1, e, arr)
    st[node] = max(st[2 * node], st[2 * node + 1])

''' A recursive function to get the
maximum of range[l, r] The
following parameters for
this function:

st     -> Pointer to segment tree
node -> Index of current node in
        the segment tree .
s & e -> Starting and ending indexes
        of the segment represented
        by current node, i.e., st[node]
l & r -> Starting and ending indexes
        of range query
'''
def getMax(node, s, e, l, r):

    # If segment of this node
    # does not belong to
    # given range
    if (s > r or e < l):
        return (-sys.maxsize - 1)

    # If segment of this node
    # is completely part of
    # given range, then return
    # the max of segment
    if (s >= l and e <= r):
        return st[node]

    # If segment of this node
    # is partially the part
    # of given range
    mid = getMid(s, e)

    return max(getMax(2 * node, s, mid, l, r),
               getMax(2 * node + 1, mid + 1, e, l, r))

# Function to print the max
# of all subarrays of size k
def printKMax(n, k):

    for i in range(n):
        if ((k - 1 + i) < n):
            print(getMax(1, 0, n - 1, i,
                               k - 1 + i), end = " ")
        else:
            break

# Driver code
if __name__ == "__main__":

    k = 4
    arr = [ 8, 5, 10, 7, 9, 4, 15, 12, 90, 13 ]
    n = len(arr)

    # Function to construct the
    # segment tree
    constructST(1, 0, n - 1, arr)

    printKMax(n, k)

# This code is contributed by chitranayal
```

## C#

```
// C# program to answer Maximum
// of allsubarrays of size k
// using segment tree
using System;

class GFG{

static int MAX = 1000000;

// Size of segment
// tree = 2^{log(MAX)+1}
static int[] st = new int[3 * MAX];

// A utility function to get the
// middle index of given range.
static int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

// A recursive function that
// constructs Segment Tree for
// array[s...e]. node is index
// of current node in segment
// tree st
static void constructST(int node, int s,
                        int e, int[] arr)
{

    // If there is one element in
    // array, store it in current
    // node of segment tree and return
    if (s == e)
    {
        st[node] = arr[s];
        return;
    }

    // If there are more than
    // one elements, then recur
    // for left and right subtrees
    // and store the max of
    // values in this node
    int mid = getMid(s, e);

    constructST(2 * node, s, mid, arr);
    constructST(2 * node + 1, mid + 1, e, arr);

    st[node] = Math.Max(st[2 * node],
                        st[2 * node + 1]);
}

/* A recursive function to get the
   maximum of range[l, r] The
   following parameters for
   this function:

st     -> Pointer to segment tree
node   -> Index of current node in
          the segment tree .
s & e  -> Starting and ending indexes
          of the segment represented
          by current node, i.e., st[node]
l & r  -> Starting and ending indexes
          of range query
 */
static int getMax(int node, int s, int e,
                            int l, int r)
{

    // If segment of this node
    // does not belong to
    // given range
    if (s > r || e < l)
        return int.MinValue;

    // If segment of this node
    // is completely part of
    // given range, then return
    // the max of segment
    if (s >= l && e <= r)
        return st[node];

    // If segment of this node
    // is partially the part
    // of given range
    int mid = getMid(s, e);

    return Math.Max(getMax(2 * node, s,
                           mid, l, r),
                    getMax(2 * node + 1,
                           mid + 1, e, l, r));
}

// Function to print the max
// of all subarrays of size k
static void printKMax(int n, int k)
{
    for(int i = 0; i < n; i++)
    {
        if ((k - 1 + i) < n)
            Console.Write(getMax(1, 0, n - 1,
                                 i, k - 1 + i) + " ");
        else
            break;
    }
}

// Driver code
public static void Main()
{
    int k = 4;
    int[] arr = { 8, 5, 10, 7, 9,
                  4, 15, 12, 90, 13 };
    int n = arr.Length;

    // Function to construct the
    // segment tree
    constructST(1, 0, n - 1, arr);

    printKMax(n, k);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program to answer Maximum
// of allsubarrays of size k
// using segment tree

var MAX = 1000000;

// Size of segment
// tree = 2^{log(MAX)+1}
var st = Array(3*MAX);

// A utility function to get the
// middle index of given range.
function getMid(s, e)
{
    return s + parseInt((e - s) / 2);
}
// A recursive function that
// constructs Segment Tree for
// array[s...e]. node is index
// of current node in segment
// tree st
function constructST(node, s, e, arr)
{
    // If there is one element in
    // array, store it in current
    // node of segment tree and return
    if (s == e) {
        st[node] = arr[s];
        return;
    }
    // If there are more than
    // one elements, then recur
    // for left and right subtrees
    // and store the max of
    // values in this node
    var mid = getMid(s, e);

    constructST(2 * node, s,
                mid, arr);
    constructST(2 * node + 1,
                mid + 1, e,
                arr);
    st[node] = Math.max(st[2 * node],
                   st[2 * node + 1]);
}

/* A recursive function to get the
   maximum of range[l, r] The
   following parameters for
   this function:

st     -> Pointer to segment tree
node   -> Index of current node in
          the segment tree .
s & e  -> Starting and ending indexes
          of the segment represented
          by current node, i.e., st[node]
l & r  -> Starting and ending indexes
          of range query
 */
function getMax(node, s, e, l, r)
{
    // If segment of this node
    // does not belong to
    // given range
    if (s > r || e < l)
        return -1000000000;

    // If segment of this node
    // is completely part of
    // given range, then return
    // the max of segment
    if (s >= l && e <= r)
        return st[node];

    // If segment of this node
    // is partially the part
    // of given range
    var mid = getMid(s, e);

    return Math.max(getMax(2 * node,
                      s, mid,
                      l, r),
               getMax(2 * node + 1,
                      mid + 1, e,
                      l, r));
}

// Function to print the max
// of all subarrays of size k
function printKMax(n, k)
{
    for (var i = 0; i < n; i++) {
        if ((k - 1 + i) < n)
            document.write( getMax(1, 0, n - 1,
                           i, k - 1 + i)
                 + " ");
        else
            break;
    }
}

// Driver code
var k = 4;
var arr = [8, 5, 10, 7, 9, 4, 15,
              12, 90, 13];
var n = arr.length;
// Function to construct the
// segment tree
constructST(1, 0, n - 1, arr);
printKMax(n, k);

</script>
```

**Output:** 

```
10 10 10 15 15 90 90
```

**时间复杂度:** O(N * log K)
**相关文章:** [滑动窗口最大值(K 大小所有子阵列的最大值)](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/?ref=rp)