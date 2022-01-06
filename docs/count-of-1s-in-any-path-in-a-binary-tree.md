# 二叉树中任意路径的 1 计数

> 原文:[https://www . geeksforgeeks . org/二进制树中任意路径的 1 个数/](https://www.geeksforgeeks.org/count-of-1s-in-any-path-in-a-binary-tree/)

给定一个 0 和 1 的二叉树，任务是在树的任何路径中找到 1 的最大数量。路径可以在树中的任何节点开始和结束。
**例**:

```
Input: 
       1
      / \
     0   1
    / \
   1   1
      / \
     1   0

Output: 4
```

**进场:**

1.  创建了一个函数 countUntil，它返回该节点下任何垂直路径中的最大计数 1。
2.  该路径必须是单个路径，并且该路径必须包括节点及其自身的至多一个子节点。即计数直到返回**左子级**或**右子级**中的最大计数 1，并且如果其值为 1，**也将其自身包含在计数中**。
3.  因此，从任何节点**count 直到(节点- >左)+count 直到(节点- >右)+ node- >** 值将给出包含该节点及其左右路径的路径中的 1 的数量，并且不考虑该节点的祖先。
4.  取所有节点的最大值将给出所需的答案。

以下是上述方法的实施

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// A binary tree node
struct Node {
    int data;
    struct Node *left, *right;
};

// A utility function to allocate a new node
struct Node* newNode(int data)
{
    struct Node* newNode = new Node;
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return (newNode);
}

// This function updates overall count of 1 in 'res'
// And returns count 1s going through root.
int countUntil(Node* root, int& res)
{
    // Base Case
    if (root == NULL)
        return 0;

    // l and r store count of 1s going through left and
    // right child of root respectively
    int l = countUntil(root->left, res);
    int r = countUntil(root->right, res);

    // maxCount represents the count of 1s when the Node under
    // consideration is the root of the maxCount path and no
    // ancestors of the root are there in maxCount path
    int maxCount;

    // if the value at node is 1 then its
    // count will be considered
    // including the leftCount and the rightCount
    if (root->data == 1)
        maxCount = l + r + 1;
    else
        maxCount = l + r;

    // Store the Maximum Result.
    res = max(res, maxCount);

    // return max count in a single path.
    // This path must include at-most one child
    // of the root as well as itself

    // if the value at node is 1
    // then its count will be considered
    // including the maximum of leftCount or the rightCount
    if (root->data == 1)
        return max(l, r) + 1;
    else
        return max(l, r);
}

// Returns maximum count of 1 in any path
// in tree with given root
int findMaxCount(Node* root)
{
    // Initialize result
    int res = INT_MIN;

    // Compute and return result
    countUntil(root, res);
    return res;
}

// Driver program
int main(void)
{
    struct Node* root = newNode(1);
    root->left = newNode(0);
    root->right = newNode(1);
    root->left->left = newNode(1);
    root->left->right = newNode(1);
    root->left->right->left = newNode(1);
    root->left->right->right = newNode(0);
    cout << findMaxCount(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // A binary tree node
    static class Node
    {
        int data;
        Node left, right;
    };

    static int res;

    // A utility function to allocate a new node
    static Node newNode(int data)
    {
        Node newNode = new Node();
        newNode.data = data;
        newNode.left = newNode.right = null;
        return (newNode);
    }

    // This function updates overall count of 1 in 'res'
    // And returns count 1s going through root.
    static int countUntil(Node root)
    {
        // Base Case
        if (root == null)
            return 0;

        // l and r store count of 1s going through left and
        // right child of root respectively
        int l = countUntil(root.left);
        int r = countUntil(root.right);

        // maxCount represents the count of 1s when the Node under
        // consideration is the root of the maxCount path and no
        // ancestors of the root are there in maxCount path
        int maxCount;

        // if the value at node is 1 then its
        // count will be considered
        // including the leftCount and the rightCount
        if (root.data == 1)
            maxCount = l + r + 1;
        else
            maxCount = l + r;

        // Store the Maximum Result.
        res = Math.max(res, maxCount);

        // return max count in a single path.
        // This path must include at-most one child
        // of the root as well as itself

        // if the value at node is 1
        // then its count will be considered
        // including the maximum of leftCount or the rightCount
        if (root.data == 1)
            return Math.max(l, r) + 1;
        else
            return Math.max(l, r);
    }

    // Returns maximum count of 1 in any path
    // in tree with given root
    static int findMaxCount(Node root)
    {
        // Initialize result
        res = Integer.MIN_VALUE;

        // Compute and return result
        countUntil(root);
        return res;
    }

    // Driver program
    public static void main(String[] args)
    {
        Node root = newNode(1);
        root.left = newNode(0);
        root.right = newNode(1);
        root.left.left = newNode(1);
        root.left.right = newNode(1);
        root.left.right.left = newNode(1);
        root.left.right.right = newNode(0);
        System.out.print(findMaxCount(root));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of the above approach

# A binary tree node
class Node:
    def __init__(self):
        self.data = 0
        self.left = None
        self.right = None

# A utility function to allocate a new node
def newNode(data):

    newNode = Node()
    newNode.data = data
    newNode.left = newNode.right = None
    return (newNode)

res = 0

# This function updates overall count of 1 in 'res'
# And returns count 1s going through root.
def countUntil( root):
    global res

    # Base Case
    if (root == None):
        return 0

    # l and r store count of 1s going through left and
    # right child of root respectively
    l = countUntil(root.left)
    r = countUntil(root.right)

    # maxCount represents the count of 1s when the Node under
    # consideration is the root of the maxCount path and no
    # ancestors of the root are there in maxCount path
    maxCount = 0

    # if the value at node is 1 then its
    # count will be considered
    # including the leftCount and the rightCount
    if (root.data == 1):
        maxCount = l + r + 1
    else:
        maxCount = l + r

    # Store the Maximum Result.
    res = max(res, maxCount)

    # return max count in a single path.
    # This path must include at-most one child
    # of the root as well as itself

    # if the value at node is 1
    # then its count will be considered
    # including the maximum of leftCount or the rightCount
    if (root.data == 1):
        return max(l, r) + 1
    else:
        return max(l, r)

# Returns maximum count of 1 in any path
# in tree with given root
def findMaxCount(root):

    global res

    # Initialize result
    res = -999999

    # Compute and return result
    countUntil(root)
    return res

# Driver program

root = newNode(1)
root.left = newNode(0)
root.right = newNode(1)
root.left.left = newNode(1)
root.left.right = newNode(1)
root.left.right.left = newNode(1)
root.left.right.right = newNode(0)
print(findMaxCount(root))

# This code is contributed by Arnab Kundu
```

## C#

```

// C# implementation of the above approach
using System;

class GFG
{

    // A binary tree node
    class Node
    {
        public int data;
        public Node left, right;
    };

    static int res;

    // A utility function to allocate a new node
    static Node newNode(int data)
    {
        Node newNode = new Node();
        newNode.data = data;
        newNode.left = newNode.right = null;
        return (newNode);
    }

    // This function updates overall count of 1 in 'res'
    // And returns count 1s going through root.
    static int countUntil(Node root)
    {
        // Base Case
        if (root == null)
            return 0;

        // l and r store count of 1s going through left and
        // right child of root respectively
        int l = countUntil(root.left);
        int r = countUntil(root.right);

        // maxCount represents the count of 1s when the Node under
        // consideration is the root of the maxCount path and no
        // ancestors of the root are there in maxCount path
        int maxCount;

        // if the value at node is 1 then its
        // count will be considered
        // including the leftCount and the rightCount
        if (root.data == 1)
            maxCount = l + r + 1;
        else
            maxCount = l + r;

        // Store the Maximum Result.
        res = Math.Max(res, maxCount);

        // return max count in a single path.
        // This path must include at-most one child
        // of the root as well as itself

        // if the value at node is 1
        // then its count will be considered
        // including the maximum of leftCount or the rightCount
        if (root.data == 1)
            return Math.Max(l, r) + 1;
        else
            return Math.Max(l, r);
    }

    // Returns maximum count of 1 in any path
    // in tree with given root
    static int findMaxCount(Node root)
    {
        // Initialize result
        res = int.MinValue;

        // Compute and return result
        countUntil(root);
        return res;
    }

    // Driver program
    public static void Main(String[] args)
    {
        Node root = newNode(1);
        root.left = newNode(0);
        root.right = newNode(1);
        root.left.left = newNode(1);
        root.left.right = newNode(1);
        root.left.right.left = newNode(1);
        root.left.right.right = newNode(0);
        Console.Write(findMaxCount(root));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach
// A binary tree node
class Node
{
    constructor()
    {
        this.left = null;
        this.data = 0;
        this.right = null;
    }
};
var res = 0;
// A utility function to allocate a new node
function newNode(data)
{
    var newNode = new Node();
    newNode.data = data;
    newNode.left = newNode.right = null;
    return (newNode);
}
// This function updates overall count of 1 in 'res'
// And returns count 1s going through root.
function countUntil(root)
{
    // Base Case
    if (root == null)
        return 0;
    // l and r store count of 1s going through left and
    // right child of root respectively
    var l = countUntil(root.left);
    var r = countUntil(root.right);
    // maxCount represents the count of 1s when the Node under
    // consideration is the root of the maxCount path and no
    // ancestors of the root are there in maxCount path
    var maxCount;
    // if the value at node is 1 then its
    // count will be considered
    // including the leftCount and the rightCount
    if (root.data == 1)
        maxCount = l + r + 1;
    else
        maxCount = l + r;
    // Store the Maximum Result.
    res = Math.max(res, maxCount);
    // return max count in a single path.
    // This path must include at-most one child
    // of the root as well as itself
    // if the value at node is 1
    // then its count will be considered
    // including the maximum of leftCount or the rightCount
    if (root.data == 1)
        return Math.max(l, r) + 1;
    else
        return Math.max(l, r);
}
// Returns maximum count of 1 in any path
// in tree with given root
function findMaxCount(root)
{
    // Initialize result
    res = -1000000000;
    // Compute and return result
    countUntil(root);
    return res;
}
// Driver program
var root = newNode(1);
root.left = newNode(0);
root.right = newNode(1);
root.left.left = newNode(1);
root.left.right = newNode(1);
root.left.right.left = newNode(1);
root.left.right.right = newNode(0);
document.write(findMaxCount(root));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(n)
其中 n 为二叉树中的节点数。