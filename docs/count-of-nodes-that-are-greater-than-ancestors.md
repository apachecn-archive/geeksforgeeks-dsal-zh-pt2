# 大于祖先的节点数

> 原文:[https://www . geesforgeks . org/大于祖先的节点数/](https://www.geeksforgeeks.org/count-of-nodes-that-are-greater-than-ancestors/)

给定一棵树的根，任务是找到大于其所有祖先的节点数。
**例:**

```
Input: 
  4
 / \
5   2
   / \
  3   6
Output: 3
The nodes are 4, 5 and 6.

Input: 
   10
  /  \
 8    6
  \    \
   3    5
  /
 1
Output: 1
```

**方法:**使用 [dfs](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 可以解决问题。在每个函数调用中，传递一个变量 **maxx** ，它存储了到目前为止遍历的所有节点中的最大值，每个大于 **maxx** 的节点都是满足给定条件的节点。因此，增加计数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Structure for the node of the tree
struct Tree {
    int val;
    Tree* left;
    Tree* right;
    Tree(int _val)
    {
        val = _val;
        left = NULL;
        right = NULL;
    }
};

// Dfs Function
void dfs(Tree* node, int maxx, int& count)
{
    // Base case
    if (node == NULL) {
        return;
    }
    else {

        // Increment the count if the current
        // node's value is greater than the
        // maximum value in it's ancestors
        if (node->val > maxx)
            count++;

        // Left traversal
        dfs(node->left, max(maxx, node->val), count);

        // Right traversal
        dfs(node->right, max(maxx, node->val), count);
    }
}

// Driver code
int main()
{

    Tree* root = new Tree(4);
    root->left = new Tree(5);
    root->right = new Tree(2);
    root->right->left = new Tree(3);
    root->right->right = new Tree(6);

    // To store the required count
    int count = 0;

    dfs(root, INT_MIN, count);

    cout << count;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int count;

// Structure for the node of the tree
static class Tree
{
    int val;
    Tree left;
    Tree right;
    Tree(int _val)
    {
        val = _val;
        left = null;
        right = null;
    }
};

// Dfs Function
static void dfs(Tree node, int maxx)
{
    // Base case
    if (node == null)
    {
        return;
    }
    else
    {

        // Increment the count if the current
        // node's value is greater than the
        // maximum value in it's ancestors
        if (node.val > maxx)
            count++;

        // Left traversal
        dfs(node.left, Math.max(maxx, node.val));

        // Right traversal
        dfs(node.right, Math.max(maxx, node.val));
    }
}

// Driver code
public static void main(String[] args)
{
    Tree root = new Tree(4);
    root.left = new Tree(5);
    root.right = new Tree(2);
    root.right.left = new Tree(3);
    root.right.right = new Tree(6);

    // To store the required count
    count = 0;

    dfs(root, Integer.MIN_VALUE);

    System.out.print(count);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
from collections import deque

# A Tree node
class Tree:

    def __init__(self, x):

        self.val = x
        self.left = None
        self.right = None

count = 0

# Dfs Function
def dfs(node, maxx):

    global count

    # Base case
    if (node == None):
        return
    else:

        # Increment the count if
        # the current node's value
        # is greater than the maximum
        # value in it's ancestors
        if (node.val > maxx):
            count += 1

        # Left traversal
        dfs(node.left,
            max(maxx,
                node.val))

        # Right traversal
        dfs(node.right,
            max(maxx,
                node.val))

# Driver code
if __name__ == '__main__':

    root = Tree(4)
    root.left = Tree(5)
    root.right = Tree(2)
    root.right.left = Tree(3)
    root.right.right = Tree(6)

    # To store the required
    # count
    count = 0

    dfs(root,
        -10 ** 9)
    print(count)

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int count;

// Structure for the node of the tree
public class Tree
{
    public int val;
    public Tree left;
    public Tree right;
    public Tree(int _val)
    {
        val = _val;
        left = null;
        right = null;
    }
};

// Dfs Function
static void dfs(Tree node, int maxx)
{
    // Base case
    if (node == null)
    {
        return;
    }
    else
    {

        // Increment the count if the current
        // node's value is greater than the
        // maximum value in it's ancestors
        if (node.val > maxx)
            count++;

        // Left traversal
        dfs(node.left, Math.Max(maxx, node.val));

        // Right traversal
        dfs(node.right, Math.Max(maxx, node.val));
    }
}

// Driver code
public static void Main(String[] args)
{
    Tree root = new Tree(4);
    root.left = new Tree(5);
    root.right = new Tree(2);
    root.right.left = new Tree(3);
    root.right.right = new Tree(6);

    // To store the required count
    count = 0;

    dfs(root, int.MinValue);

    Console.Write(count);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

let count=0;
// Structure for the node of the tree
class Tree
{
    constructor(val)
    {
        this.val=val;
        this.left=this.right=null;
    }
}

// Dfs Function
function dfs(node,maxx)
{
    // Base case
    if (node == null)
    {
        return;
    }
    else
    {

        // Increment the count if the current
        // node's value is greater than the
        // maximum value in it's ancestors
        if (node.val > maxx)
            count++;

        // Left traversal
        dfs(node.left, Math.max(maxx, node.val));

        // Right traversal
        dfs(node.right, Math.max(maxx, node.val));
    }
}

// Driver code
let root = new Tree(4);
root.left = new Tree(5);
root.right = new Tree(2);
root.right.left = new Tree(3);
root.right.right = new Tree(6);

// To store the required count
count = 0;

dfs(root, Number.MIN_VALUE);

document.write(count);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
3
```