# 通过后序遍历和叶节点数组

创建二叉树

> 原文:[https://www . geesforgeks . org/create-a-二叉树-从-后-顺序-遍历-和-叶-节点-数组/](https://www.geeksforgeeks.org/create-a-binary-tree-from-post-order-traversal-and-leaf-node-array/)

给定两个数组，第一个包含后序遍历序列，第二个包含第一个数组中对应的节点是叶节点还是非叶节点的信息，创建一个二叉树并返回它的根，打印它的有序遍历。(可能有多棵树，但你必须只形成一棵树)
**示例:**

```
Input: 
postorder = {40, 20, 50, 60, 30, 10} 
isLeaf = {true, false, true, true, false, false}
Output: 20 40 10 50 30 60
Explanation:
Generated Binary tree
        10
      /    \
    20      30
      \     /  \
      40   50  60

Input:
postorder = {20, 18, 25, 100, 81, 15, 7} 
isLeaf = {true, false, true, true, false, false, false}
Output: 7 18 20 15 25 81 100
Explanation:
Generated Binary tree
       7
        \
        15
      /   \
    18     81
      \    /  \
      20  25  100
```

**方法:**
思路是先用后序序列中的最后一个键构造二叉树的根节点。然后使用给定的布尔数组，我们发现根节点是内部节点还是叶节点。如果根节点是内部节点，我们递归地构造它的左右子树。
以下是上述办法的实施:

## C++

```
// C++ implementation for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// struct to store
// tree nodes
struct Tree {
    int val;
    Tree* leftchild;
    Tree* rightchild;
    Tree(int _val, Tree* _leftchild, Tree* _rightchild)
    {
        val = _val;
        leftchild = _leftchild;
        rightchild = _rightchild;
    }
};

// Function to generate binary tree
// from given postorder traversal sequence
// and leaf or non-leaf node information.
struct Tree* createBinaryTree(int post[], bool isLeaf[], int& n)
{
  // Base condition
  if (n < 0){
    return NULL;
  }
  struct Tree* root = new Tree(post[n], NULL, NULL);
  bool isInternalNode = !isLeaf[n];
  n--;
  // If internal node
  // creating left and
  // right child
  if (isInternalNode) {
    root->rightchild = createBinaryTree(post, isLeaf, n);
    root->leftchild = createBinaryTree(post, isLeaf, n);
  }
  return root;
}

// Function to print
// in-order traversal
// of a binary tree.
void inorder(struct Tree* root)
{
  if (root == NULL){
    return;
  }
  inorder(root->leftchild);
  cout << root->val << " ";
  inorder(root->rightchild);
}

// Driver code
int main()
{
  int post[] = { 40, 20, 50, 60, 30, 10 };
  bool isLeaf[] = { true, false, true, true, false, false };
  int n = sizeof(post) / sizeof(post[0]) - 1;

  struct Tree* root = createBinaryTree(post, isLeaf, n);
  inorder(root);

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for
// the above approach
class GFG
{

static int n;

// to store tree nodes
static class Tree
{
    int val;
    Tree leftchild;
    Tree rightchild;
    Tree(int _val, Tree _leftchild,
                   Tree _rightchild)
    {
        val = _val;
        leftchild = _leftchild;
        rightchild = _rightchild;
    }
};

// Function to generate binary tree
// from given postorder traversal sequence
// and leaf or non-leaf node information.
static Tree createBinaryTree(int post[],
                             boolean isLeaf[])
{
    // Base condition
    if (n < 0)
    {
        return null;
    }
    Tree root = new Tree(post[n], null, null);
    boolean isInternalNode = !isLeaf[n];
    n--;

    // If internal node creating left and
    // right child
    if (isInternalNode)
    {
        root.rightchild = createBinaryTree(post, isLeaf);
        root.leftchild = createBinaryTree(post, isLeaf);
    }
    return root;
}

// Function to print in-order traversal
// of a binary tree.
static void inorder(Tree root)
{
    if (root == null)
    {
        return;
    }
    inorder(root.leftchild);
    System.out.print(root.val + " ");
    inorder(root.rightchild);
}

// Driver code
public static void main(String[] args)
{
    int post[] = { 40, 20, 50, 60, 30, 10 };
    boolean isLeaf[] = { true, false, true,
                         true, false, false };
    n = post.length - 1;

    Tree root = createBinaryTree(post, isLeaf);
    inorder(root);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation of above algorithm

# Utility class to create a node
class Tree:
    def __init__(self, key):
        self.val = key
        self.leftchild = self.rightchild = None

n = 0

# Function to generate binary tree
# from given postorder traversal sequence
# and leaf or non-leaf node information.
def createBinaryTree( post, isLeaf):
    global n

    # Base condition
    if (n < 0):
        return None

    root = Tree(post[n])
    isInternalNode = not isLeaf[n]
    n = n - 1

    # If internal node
    # creating left and
    # right child
    if (isInternalNode):
        root.rightchild = createBinaryTree(post, isLeaf)
        root.leftchild = createBinaryTree(post, isLeaf)

    return root

# Function to print
# in-order traversal
# of a binary tree.
def inorder( root):

    if (root == None):
        return

    inorder(root.leftchild)
    print( root.val ,end = " ")
    inorder(root.rightchild)

# Driver code

post = [40, 20, 50, 60, 30, 10]
isLeaf = [True, False, True, True, False, False ]
n = len(post)-1

root = createBinaryTree(post, isLeaf)
inorder(root)

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
static int n;

// to store tree nodes
public class Tree
{
    public int val;
    public Tree leftchild;
    public Tree rightchild;
    public Tree(int _val, Tree _leftchild,
                          Tree _rightchild)
    {
        val = _val;
        leftchild = _leftchild;
        rightchild = _rightchild;
    }
};

// Function to generate binary tree
// from given postorder traversal sequence
// and leaf or non-leaf node information.
static Tree createBinaryTree(int []post,
                         Boolean []isLeaf)
{
    // Base condition
    if (n < 0)
    {
        return null;
    }
    Tree root = new Tree(post[n], null, null);
    Boolean isInternalNode = !isLeaf[n];
    n--;

    // If internal node creating left and
    // right child
    if (isInternalNode)
    {
        root.rightchild = createBinaryTree(post,
                                           isLeaf);
        root.leftchild = createBinaryTree(post,
                                          isLeaf);
    }
    return root;
}

// Function to print in-order traversal
// of a binary tree.
static void inorder(Tree root)
{
    if (root == null)
    {
        return;
    }
    inorder(root.leftchild);
    Console.Write(root.val + " ");
    inorder(root.rightchild);
}

// Driver code
public static void Main(String[] args)
{
    int []post = { 40, 20, 50, 60, 30, 10 };
    Boolean []isLeaf = { true, false, true,
                         true, false, false };
    n = post.Length - 1;

    Tree root = createBinaryTree(post, isLeaf);
    inorder(root);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

var n;

// to store tree nodes
class Tree
{
    constructor(_val, _leftchild, _rightchild)
    {
        this.val = _val;
        this.leftchild = _leftchild;
        this.rightchild = _rightchild;
    }
};

// Function to generate binary tree
// from given postorder traversal sequence
// and leaf or non-leaf node information.
function createBinaryTree(post, isLeaf)
{
    // Base condition
    if (n < 0)
    {
        return null;
    }
    var root = new Tree(post[n], null, null);
    var isInternalNode = !isLeaf[n];
    n--;

    // If internal node creating left and
    // right child
    if (isInternalNode)
    {
        root.rightchild = createBinaryTree(post,
                                           isLeaf);
        root.leftchild = createBinaryTree(post,
                                          isLeaf);
    }
    return root;
}

// Function to print in-order traversal
// of a binary tree.
function inorder(root)
{
    if (root == null)
    {
        return;
    }
    inorder(root.leftchild);
    document.write(root.val + " ");
    inorder(root.rightchild);
}

// Driver code
var post = [40, 20, 50, 60, 30, 10];
var isLeaf = [true, false, true,
                     true, false, false ];
n = post.length - 1;

var root = createBinaryTree(post, isLeaf);
inorder(root);

</script>
```

**Output:** 

```
20 40 10 50 30 60
```

**时间复杂度** : O(N)。
**辅助空间** : O(N)。