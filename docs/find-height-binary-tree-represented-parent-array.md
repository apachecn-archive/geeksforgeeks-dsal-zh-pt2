# 求父数组表示的二叉树高度

> 原文:[https://www . geesforgeks . org/find-height-二叉树-表示-parent-array/](https://www.geeksforgeeks.org/find-height-binary-tree-represented-parent-array/)

一个给定的数组以这样一种方式表示一棵树，即数组值给出该特定索引的父节点。根节点索引的值总是-1。找到树的高度。
二叉树的高度是从根到最深叶节点的路径上的节点数，这个数既包括根，也包括叶。

```
Input: parent[] = {1 5 5 2 2 -1 3}
Output: 4
The given array represents following Binary Tree 
         5
        /  \
       1    2
      /    / \
     0    3   4
         /
        6 

Input: parent[] = {-1, 0, 0, 1, 1, 3, 5};
Output: 5
The given array represents following Binary Tree 
         0
       /   \
      1     2
     / \
    3   4
   /
  5 
 /
6
```

[<u>推荐:请先在</u> **<u>【练习】</u>** <u>上解决，再继续解决。</u>](https://practice.geeksforgeeks.org/problems/height-using-parent-array4103/1/)

来源:[亚马逊面试体验|设置 128(针对 SDET)](https://www.geeksforgeeks.org/amazon-interview-experience-set-128-sdet/)
**我们强烈建议尽量减少你的浏览器，先自己试试这个。**
A **简单的解决方法**就是先构造树，然后找到构造的二叉树的高度。该树可以递归地构建，首先搜索当前根，然后循环找到的索引，并使它们成为根的左右子树。这个解决方案需要 O(n <sup>2</sup> )，因为我们必须线性搜索每个节点。
一个**高效的解决方案**可以在 O(n)时间内解决上述问题。其思想是首先计算每个节点的深度，并将其存储在深度[]数组中。一旦我们有了所有节点的深度，我们就返回了所有深度的最大值。
1)找出所有节点的深度，填入一个辅助数组深度[]。
2)返回深度[]的最大值。
以下是查找索引 I 处节点深度的步骤。
1)如果是根，深度[i]为 1。
2)如果评估父项[i]的深度，则深度[i]为深度[父项[i]] + 1。
3)如果未评估父项[i]的深度，则针对父项重复进行，并将深度[i]指定为深度[父项[i]] + 1(同上)。
以下是上述思路的实现。

## C++

```
// C++ program to find height using parent array
#include <bits/stdc++.h>
using namespace std;

// This function fills depth of i'th element in parent[].
// The depth is filled in depth[i].
void fillDepth(int parent[], int i, int depth[])
{
    // If depth[i] is already filled
    if (depth[i])
        return;

    // If node at index i is root
    if (parent[i] == -1) {
        depth[i] = 1;
        return;
    }

    // If depth of parent is not evaluated before, then
    // evaluate depth of parent first
    if (depth[parent[i]] == 0)
        fillDepth(parent, parent[i], depth);

    // Depth of this node is depth of parent plus 1
    depth[i] = depth[parent[i]] + 1;
}

// This function returns height of binary tree represented
// by parent array
int findHeight(int parent[], int n)
{
    // Create an array to store depth of all nodes/ and
    // initialize depth of every node as 0 (an invalid
    // value). Depth of root is 1
    int depth[n];
    for (int i = 0; i < n; i++)
        depth[i] = 0;

    // fill depth of all nodes
    for (int i = 0; i < n; i++)
        fillDepth(parent, i, depth);

    // The height of binary tree is maximum of all depths.
    // Find the maximum value in depth[] and assign it to
    // ht.
    int ht = depth[0];
    for (int i = 1; i < n; i++)
        if (ht < depth[i])
            ht = depth[i];
    return ht;
}

// Driver program to test above functions
int main()
{
    // int parent[] = {1, 5, 5, 2, 2, -1, 3};
    int parent[] = { -1, 0, 0, 1, 1, 3, 5 };

    int n = sizeof(parent) / sizeof(parent[0]);
    cout << "Height is " << findHeight(parent, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find height using parent array
class BinaryTree {

    // This function fills depth of i'th element in
    // parent[].  The depth is filled in depth[i].
    void fillDepth(int parent[], int i, int depth[])
    {

        // If depth[i] is already filled
        if (depth[i] != 0) {
            return;
        }

        // If node at index i is root
        if (parent[i] == -1) {
            depth[i] = 1;
            return;
        }

        // If depth of parent is not evaluated before, then
        // evaluate depth of parent first
        if (depth[parent[i]] == 0) {
            fillDepth(parent, parent[i], depth);
        }

        // Depth of this node is depth of parent plus 1
        depth[i] = depth[parent[i]] + 1;
    }

    // This function returns height of binary tree
    // represented by parent array
    int findHeight(int parent[], int n)
    {

        // Create an array to store depth of all nodes/ and
        // initialize depth of every node as 0 (an invalid
        // value). Depth of root is 1
        int depth[] = new int[n];
        for (int i = 0; i < n; i++) {
            depth[i] = 0;
        }

        // fill depth of all nodes
        for (int i = 0; i < n; i++) {
            fillDepth(parent, i, depth);
        }

        // The height of binary tree is maximum of all
        // depths. Find the maximum value in depth[] and
        // assign it to ht.
        int ht = depth[0];
        for (int i = 1; i < n; i++) {
            if (ht < depth[i]) {
                ht = depth[i];
            }
        }
        return ht;
    }

    // Driver program to test above functions
    public static void main(String args[])
    {

        BinaryTree tree = new BinaryTree();

        // int parent[] = {1, 5, 5, 2, 2, -1, 3};
        int parent[] = new int[] { -1, 0, 0, 1, 1, 3, 5 };

        int n = parent.length;
        System.out.println("Height is  "
                           + tree.findHeight(parent, n));
    }
}
```

## 计算机编程语言

```
# Python program to find height using parent array

# This functio fills depth of i'th element in parent[]
# The depth is filled in depth[i]

def fillDepth(parent, i, depth):

    # If depth[i] is already filled
    if depth[i] != 0:
        return

    # If node at index i is root
    if parent[i] == -1:
        depth[i] = 1
        return

    # If depth of parent is not evaluated before,
    # then evaluate depth of parent first
    if depth[parent[i]] == 0:
        fillDepth(parent, parent[i], depth)

    # Depth of this node is depth of parent plus 1
    depth[i] = depth[parent[i]] + 1

# This function reutns height of binary tree represented
# by parent array

def findHeight(parent):
    n = len(parent)
    # Create an array to store depth of all nodes and
    # initialize depth of every node as 0
    # Depth of root is 1
    depth = [0 for i in range(n)]

    # fill depth of all nodes
    for i in range(n):
        fillDepth(parent, i, depth)

    # The height of binary tree is maximum of all
    # depths. Find the maximum in depth[] and assign
    # it to ht
    ht = depth[0]
    for i in range(1, n):
        ht = max(ht, depth[i])

    return ht

# Driver program to test above function
parent = [-1, 0, 0, 1, 1, 3, 5]
print "Height is %d" % (findHeight(parent))

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;

// C# program to find height using parent array
public class BinaryTree {

    // This function fills depth of i'th element in
    // parent[].  The depth is filled in depth[i].
    public virtual void fillDepth(int[] parent, int i,
                                  int[] depth)
    {

        // If depth[i] is already filled
        if (depth[i] != 0) {
            return;
        }

        // If node at index i is root
        if (parent[i] == -1) {
            depth[i] = 1;
            return;
        }

        // If depth of parent is not evaluated before, then
        // evaluate depth of parent first
        if (depth[parent[i]] == 0) {
            fillDepth(parent, parent[i], depth);
        }

        // Depth of this node is depth of parent plus 1
        depth[i] = depth[parent[i]] + 1;
    }

    // This function returns height of binary tree
    // represented by parent array
    public virtual int findHeight(int[] parent, int n)
    {

        // Create an array to store depth of all nodes/ and
        // initialize depth of every node as 0 (an invalid
        // value). Depth of root is 1
        int[] depth = new int[n];
        for (int i = 0; i < n; i++) {
            depth[i] = 0;
        }

        // fill depth of all nodes
        for (int i = 0; i < n; i++) {
            fillDepth(parent, i, depth);
        }

        // The height of binary tree is maximum of all
        // depths. Find the maximum value in depth[] and
        // assign it to ht.
        int ht = depth[0];
        for (int i = 1; i < n; i++) {
            if (ht < depth[i]) {
                ht = depth[i];
            }
        }
        return ht;
    }

    // Driver program to test above functions
    public static void Main(string[] args)
    {

        BinaryTree tree = new BinaryTree();

        // int parent[] = {1, 5, 5, 2, 2, -1, 3};
        int[] parent = new int[] { -1, 0, 0, 1, 1, 3, 5 };

        int n = parent.Length;
        Console.WriteLine("Height is  "
                          + tree.findHeight(parent, n));
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// javascript program to find height using parent array

    // This function fills depth of i'th element in parent. The depth is
    // filled in depth[i].
    function fillDepth(parent , i , depth) {

        // If depth[i] is already filled
        if (depth[i] != 0) {
            return;
        }

        // If node at index i is root
        if (parent[i] == -1) {
            depth[i] = 1;
            return;
        }

        // If depth of parent is not evaluated before, then evaluate
        // depth of parent first
        if (depth[parent[i]] == 0) {
            fillDepth(parent, parent[i], depth);
        }

        // Depth of this node is depth of parent plus 1
        depth[i] = depth[parent[i]] + 1;
    }

    // This function returns height of binary tree represented by
    // parent array
    function findHeight(parent , n) {

        // Create an array to store depth of all nodes/ and
        // initialize depth of every node as 0 (an invalid
        // value). Depth of root is 1
        var depth = Array(n).fill(0);
        for (i = 0; i < n; i++) {
            depth[i] = 0;
        }

        // fill depth of all nodes
        for (i = 0; i < n; i++) {
            fillDepth(parent, i, depth);
        }

        // The height of binary tree is maximum of all depths.
        // Find the maximum value in depth and assign it to ht.
        var ht = depth[0];
        for (i = 1; i < n; i++) {
            if (ht < depth[i]) {
                ht = depth[i];
            }
        }
        return ht;
    }

    // Driver program to test above functions

        // var parent = [1, 5, 5, 2, 2, -1, 3];
        var parent =[-1, 0, 0, 1, 1, 3, 5 ];

        var n = parent.length;
        document.write("Height is  " + findHeight(parent, n));

// This code contributed by gauravrajput1
</script>
```

## java 描述语言

```
<script>

// javascript program to find height using parent array

function fillDepth(parent, index, depth, obj) {

    let max = depth;

    if (obj[index]) {
        for (let i = 0; i < obj[index].length; i++) {
            max = Math.max(max, fillDepth(parent, obj[index][i], depth + 1, obj))
        }
    }
    return max;
}

// This function returns height of binary tree represented by
// parent array
function findHeight(parent, n) {

    let root_index;

    for (let i = 0; i < n; i++) {
        if (parent[i] === -1) {
            root_index = i;
        }
    }

    let obj = {};

    for (let i = 0; i < n; i++) {
        if (obj[parent[i]]) {
            let arr = obj[parent[i]];
            arr.push(i)
            obj[parent[i]] = arr;
        }
        else {
            obj[parent[i]] = [i];
        }
    }

    return fillDepth(parent, root_index, 1, obj);
}

// Driver program to test above functions

// var parent = [1, 5, 5, 2, 2, -1, 3];
var parent = [-1, 0, 0, 1, 1, 3, 5];

var n = parent.length;
document.write("Height is " + findHeight(parent, n));

// This code contributed by gaurav2146

</script>
```

**输出:**

```
Height is 5
```

请注意，这个程序的时间复杂度似乎超过了 O(n)。如果我们仔细观察，我们可以观察到每个节点的深度只评估一次。
本文由**西达尔特**供稿。如果你发现任何不正确的地方，请写评论，或者分享更多关于上面讨论的主题的信息。