# 二叉树中最左边的叶节点

> 原文:[https://www . geeksforgeeks . org/二叉树最左叶节点/](https://www.geeksforgeeks.org/deepest-left-leaf-node-in-a-binary-tree/)

给定一棵二叉树，找到最深的叶子节点，它是它的父节点的左子节点。例如，考虑下面的树。最左边的叶子节点是值为 9 的节点。

```
       1
     /   \
    2     3
  /      /  \  
 4      5    6
        \     \
         7     8
        /       \
       9         10 
```

其思想是递归遍历给定的二叉树，并在遍历时保持“级别”，这将在树中存储当前节点的级别。如果当前节点是左叶，那么检查它的级别是否超过目前为止看到的最深左叶的级别。如果级别更高，则更新结果。如果当前节点不是叶子，则递归地在左右子树中找到最大深度，并返回两个深度中的最大值。感谢 [Coder011](https://www.geeksforgeeks.org/amazon-interview-set-54-on-campus-for-sde/) 提出这个方法。

## C++

```
// A C++ program to find the deepest left leaf in a given binary tree
#include <bits/stdc++.h>
using namespace std;

struct Node
{
    int val;
    struct Node *left, *right;
};

Node *newNode(int data)
{
    Node *temp = new Node;
    temp->val = data;
    temp->left = temp->right =  NULL;
    return temp;
}

// A utility function to find deepest leaf node.
// lvl:  level of current node.
// maxlvl: pointer to the deepest left leaf node found so far
// isLeft: A bool indicate that this node is left child of its parent
// resPtr: Pointer to the result
void deepestLeftLeafUtil(Node *root, int lvl, int *maxlvl,
                         bool isLeft, Node **resPtr)
{
    // Base case
    if (root == NULL)
        return;

    // Update result if this node is left leaf and its level is more
    // than the maxl level of the current result
    if (isLeft && !root->left && !root->right && lvl > *maxlvl)
    {
        *resPtr = root;
        *maxlvl = lvl;
        return;
    }

    // Recur for left and right subtrees
    deepestLeftLeafUtil(root->left, lvl+1, maxlvl, true, resPtr);
    deepestLeftLeafUtil(root->right, lvl+1, maxlvl, false, resPtr);
}

// A wrapper over deepestLeftLeafUtil().
Node* deepestLeftLeaf(Node *root)
{
    int maxlevel = 0;
    Node *result = NULL;
    deepestLeftLeafUtil(root, 0, &maxlevel, false, &result);
    return result;
}

// Driver program to test above function
int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->right->left = newNode(5);
    root->right->right = newNode(6);
    root->right->left->right = newNode(7);
    root->right->right->right = newNode(8);
    root->right->left->right->left = newNode(9);
    root->right->right->right->right = newNode(10);

    Node *result = deepestLeftLeaf(root);
    if (result)
        cout << "The deepest left child is " << result->val;
    else
        cout << "There is no left leaf in the given tree";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find
// the deepest left leaf
// in a binary tree

// A Binary Tree node
class Node
{
    int data;
    Node left, right;

    // Constructor
    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

// Class to evaluate pass
// by reference
class Level
{
    // maxlevel: gives the
    // value of level of
    // maximum left leaf
    int maxlevel = 0;
}

class BinaryTree
{
    Node root;

    // Node to store resultant
    // node after left traversal
    Node result;

    // A utility function to
    // find deepest leaf node.
    // lvl: level of current node.
    // isLeft: A bool indicate
    // that this node is left child
    void deepestLeftLeafUtil(Node node,
                             int lvl,
                             Level level,
                             boolean isLeft)
    {
        // Base case
        if (node == null)
            return;

        // Update result if this node
        // is left leaf and its level
        // is more than the maxl level
        // of the current result
        if (isLeft != false &&
            node.left == null &&
            node.right == null &&
            lvl > level.maxlevel)
        {
            result = node;
            level.maxlevel = lvl;
        }

        // Recur for left and right subtrees
        deepestLeftLeafUtil(node.left, lvl + 1,
                            level, true);
        deepestLeftLeafUtil(node.right, lvl + 1,
                            level, false);
    }

    // A wrapper over deepestLeftLeafUtil().
    void deepestLeftLeaf(Node node)
    {
        Level level = new Level();
        deepestLeftLeafUtil(node, 0, level, false);
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.right.left = new Node(5);
        tree.root.right.right = new Node(6);
        tree.root.right.left.right = new Node(7);
        tree.root.right.right.right = new Node(8);
        tree.root.right.left.right.left = new Node(9);
        tree.root.right.right.right.right = new Node(10);

        tree.deepestLeftLeaf(tree.root);
        if (tree.result != null)
            System.out.println("The deepest left child"+
                               " is " + tree.result.data);
        else
            System.out.println("There is no left leaf in"+
                               " the given tree");
    }
}

// This code has been contributed by Mayank Jaiswal(mayank_24)
```

## 计算机编程语言

```
# Python program to find the deepest left leaf in a given
# Binary tree

# A binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

# A utility function to find deepest leaf node.
# lvl:  level of current node.
# maxlvl: pointer to the deepest left leaf node found so far
# isLeft: A bool indicate that this node is left child
# of its parent
# resPtr: Pointer to the result
def deepestLeftLeafUtil(root, lvl, maxlvl, isLeft):

    # Base CAse
    if root is None:
        return

    # Update result if this node is left leaf and its
    # level is more than the max level of the current result
    if(isLeft is True):
        if (root.left == None and root.right == None):
            if lvl > maxlvl[0] :
                deepestLeftLeafUtil.resPtr = root
                maxlvl[0] = lvl
                return

    # Recur for left and right subtrees
    deepestLeftLeafUtil(root.left, lvl+1, maxlvl, True)
    deepestLeftLeafUtil(root.right, lvl+1, maxlvl, False)

# A wrapper for left and right subtree
def deepestLeftLeaf(root):
    maxlvl = [0]
    deepestLeftLeafUtil.resPtr = None
    deepestLeftLeafUtil(root, 0, maxlvl, False)
    return deepestLeftLeafUtil.resPtr

# Driver program to test above function
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.right.left = Node(5)
root.right.right = Node(6)
root.right.left.right = Node(7)
root.right.right.right = Node(8)
root.right.left.right.left = Node(9)
root.right.right.right.right= Node(10)

result = deepestLeftLeaf(root)

if result is None:
    print "There is not left leaf in the given tree"
else:
    print "The deepst left child is", result.val

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;

// A C# program to find
// the deepest left leaf
// in a binary tree

// A Binary Tree node
public class Node
{
    public int data;
    public Node left, right;

    // Constructor
    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

// Class to evaluate pass
// by reference
public class Level
{
    // maxlevel: gives the
    // value of level of
    // maximum left leaf
    public int maxlevel = 0;
}

public class BinaryTree
{
    public Node root;

    // Node to store resultant
    // node after left traversal
    public Node result;

    // A utility function to
    // find deepest leaf node.
    // lvl: level of current node.
    // isLeft: A bool indicate
    // that this node is left child
    public virtual void deepestLeftLeafUtil(Node node, int lvl,
                                        Level level, bool isLeft)
    {
        // Base case
        if (node == null)
        {
            return;
        }

        // Update result if this node
        // is left leaf and its level
        // is more than the maxl level
        // of the current result
        if (isLeft != false && node.left == null && node.right == null
                            && lvl > level.maxlevel)
        {
            result = node;
            level.maxlevel = lvl;
        }

        // Recur for left and right subtrees
        deepestLeftLeafUtil(node.left, lvl + 1, level, true);
        deepestLeftLeafUtil(node.right, lvl + 1, level, false);
    }

    // A wrapper over deepestLeftLeafUtil().
    public virtual void deepestLeftLeaf(Node node)
    {
        Level level = new Level();
        deepestLeftLeafUtil(node, 0, level, false);
    }

    // Driver program to test above functions
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.right.left = new Node(5);
        tree.root.right.right = new Node(6);
        tree.root.right.left.right = new Node(7);
        tree.root.right.right.right = new Node(8);
        tree.root.right.left.right.left = new Node(9);
        tree.root.right.right.right.right = new Node(10);

        tree.deepestLeftLeaf(tree.root);
        if (tree.result != null)
        {
            Console.WriteLine("The deepest left child is " + tree.result.data);
        }
        else
        {
            Console.WriteLine("There is no left leaf in the given tree");
        }
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// A Javascript program to find
// the deepest left leaf
// in a binary tree
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

let maxlevel = 0;
let root;

// Node to store resultant
// node after left traversal
let result;

// A utility function to
// find deepest leaf node.
// lvl: level of current node.
// isLeft: A bool indicate
// that this node is left child
function deepestLeftLeafUtil(node, lvl, isLeft)
{

    // Base case
    if (node == null)
        return;

    // Update result if this node
    // is left leaf and its level
    // is more than the maxl level
    // of the current result
    if (isLeft != false &&
        node.left == null &&
        node.right == null &&
        lvl > maxlevel)
    {
        result = node;
        maxlevel = lvl;
    }

    // Recur for left and right subtrees
    deepestLeftLeafUtil(node.left, lvl + 1, true);
    deepestLeftLeafUtil(node.right, lvl + 1, false);
}

// A wrapper over deepestLeftLeafUtil().
function deepestLeftLeaf(node)
{
    deepestLeftLeafUtil(node, 0, false);
}

// Driver code
root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.right.left = new Node(5);
root.right.right = new Node(6);
root.right.left.right = new Node(7);
root.right.right.right = new Node(8);
root.right.left.right.left = new Node(9);
root.right.right.right.right = new Node(10);

deepestLeftLeaf(root);
if (result != null)
  document.write("The deepest left child"+
                 " is " + result.data + "</br>");
else
  document.write("There is no left leaf in"+
                 " the given tree");

// This code is contributed by decode2207

</script>
```

**输出:**

```
The deepest left child is 9
```

**时间复杂度:**函数对树做简单遍历，所以复杂度为 O(n)。
本文由**阿沛·拉提**供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息