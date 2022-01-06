# 从给定的二叉树创建镜像树

> 原文:[https://www . geeksforgeeks . org/从给定的二叉树创建镜像树/](https://www.geeksforgeeks.org/create-a-mirror-tree-from-the-given-binary-tree/)

给定一棵二叉树，任务是创建一棵新的二叉树，它是给定二叉树的镜像。

**示例:**

```
Input:
        5
       / \
      3   6
     / \
    2   4
Output:
Inorder of original tree: 2 3 4 5 6 
Inorder of mirror tree: 6 5 4 3 2
Mirror tree will be:
  5
 / \
6   3
   / \
  4   2

Input:
        2
       / \
      1   8
     /     \
    12      9
Output:
Inorder of original tree: 12 1 2 8 9 
Inorder of mirror tree: 9 8 2 1 12
```

**方法:**编写一个递归函数，将两个节点作为参数，一个是原始树，另一个是新创建的树。现在，对于原始树的每个传递的节点，在镜像树中创建一个对应的节点，然后对子节点递归调用相同的方法，但是传递原始树节点的左子节点和镜像树节点的右子节点，以及原始树节点的右子节点和镜像树节点的左子节点。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// A binary tree node has data, pointer to
// left child and a pointer to right child
typedef struct treenode {
    int val;
    struct treenode* left;
    struct treenode* right;
} node;

// Helper function that allocates a new node with the
// given data and NULL left and right pointers
node* createNode(int val)
{
    node* newNode = (node*)malloc(sizeof(node));
    newNode->val = val;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// Helper function to print Inorder traversal
void inorder(node* root)
{
    if (root == NULL)
        return;
    inorder(root->left);
    cout <<" "<< root->val;
    inorder(root->right);
}

// mirrorify function takes two trees,
// original tree and a mirror tree
// It recurses on both the trees,
// but when original tree recurses on left,
// mirror tree recurses on right and
// vice-versa
void mirrorify(node* root, node** mirror)
{
    if (root == NULL) {
        mirror = NULL;
        return;
    }

    // Create new mirror node from original tree node
    *mirror = createNode(root->val);
    mirrorify(root->left, &((*mirror)->right));
    mirrorify(root->right, &((*mirror)->left));
}

// Driver code
int main()
{

    node* tree = createNode(5);
    tree->left = createNode(3);
    tree->right = createNode(6);
    tree->left->left = createNode(2);
    tree->left->right = createNode(4);

    // Print inorder traversal of the input tree
    cout <<"Inorder of original tree: ";
    inorder(tree);
    node* mirror = NULL;
    mirrorify(tree, &mirror);

    // Print inorder traversal of the mirror tree
    cout <<"\nInorder of mirror tree: ";
    inorder(mirror);

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C implementation of the approach
#include <malloc.h>
#include <stdio.h>

// A binary tree node has data, pointer to
// left child and a pointer to right child
typedef struct treenode {
    int val;
    struct treenode* left;
    struct treenode* right;
} node;

// Helper function that allocates a new node with the
// given data and NULL left and right pointers
node* createNode(int val)
{
    node* newNode = (node*)malloc(sizeof(node));
    newNode->val = val;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// Helper function to print Inorder traversal
void inorder(node* root)
{
    if (root == NULL)
        return;
    inorder(root->left);
    printf("%d ", root->val);
    inorder(root->right);
}

// mirrorify function takes two trees,
// original tree and a mirror tree
// It recurses on both the trees,
// but when original tree recurses on left,
// mirror tree recurses on right and
// vice-versa
void mirrorify(node* root, node** mirror)
{
    if (root == NULL) {
        mirror = NULL;
        return;
    }

    // Create new mirror node from original tree node
    *mirror = createNode(root->val);
    mirrorify(root->left, &((*mirror)->right));
    mirrorify(root->right, &((*mirror)->left));
}

// Driver code
int main()
{

    node* tree = createNode(5);
    tree->left = createNode(3);
    tree->right = createNode(6);
    tree->left->left = createNode(2);
    tree->left->right = createNode(4);

    // Print inorder traversal of the input tree
    printf("Inorder of original tree: ");
    inorder(tree);
    node* mirror = NULL;
    mirrorify(tree, &mirror);

    // Print inorder traversal of the mirror tree
    printf("\nInorder of mirror tree: ");
    inorder(mirror);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Comparator;

class GFG
{

// A binary tree node has data, pointer to
// left child and a pointer to right child
static class node
{
    int val;
    node left;
    node right;
}

// Helper function that allocates
// a new node with the given data
// and null left and right pointers
static node createNode(int val)
{
    node newNode = new node();
    newNode.val = val;
    newNode.left = null;
    newNode.right = null;
    return newNode;
}

// Helper function to print Inorder traversal
static void inorder(node root)
{
    if (root == null)
        return;
    inorder(root.left);
    System.out.print(root.val);
    inorder(root.right);
}

// mirrorify function takes two trees,
// original tree and a mirror tree
// It recurses on both the trees,
// but when original tree recurses on left,
// mirror tree recurses on right and
// vice-versa
static node mirrorify(node root)
{
    if (root == null)
    {
        return null;

    }

    // Create new mirror node from original tree node
    node mirror = createNode(root.val);
    mirror.right = mirrorify(root.left);
    mirror.left = mirrorify(root.right);
    return mirror;
}

// Driver code
public static void main(String args[])
{

    node tree = createNode(5);
    tree.left = createNode(3);
    tree.right = createNode(6);
    tree.left.left = createNode(2);
    tree.left.right = createNode(4);

    // Print inorder traversal of the input tree
    System.out.print("Inorder of original tree: ");
    inorder(tree);
    node mirror = null;
    mirror = mirrorify(tree);

    // Print inorder traversal of the mirror tree
    System.out.print("\nInorder of mirror tree: ");
    inorder(mirror);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# A binary tree node has data,
# pointer to left child and
# a pointer to right child
# Linked list node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Helper function that allocates
# a new node with the given data
# and None left and right pointers
def createNode(val):
    newNode = Node(0)
    newNode.val = val
    newNode.left = None
    newNode.right = None
    return newNode

# Helper function to print Inorder traversal
def inorder(root):
    if (root == None):
        return
    inorder(root.left)
    print( root.val, end = " ")
    inorder(root.right)

# mirrorify function takes two trees,
# original tree and a mirror tree
# It recurses on both the trees,
# but when original tree recurses on left,
# mirror tree recurses on right and
# vice-versa
def mirrorify(root, mirror):

    if (root == None) :
        mirror = None
        return mirror

    # Create new mirror node
    # from original tree node
    mirror = createNode(root.val)
    mirror.right = mirrorify(root.left,
                           ((mirror).right))
    mirror.left = mirrorify(root.right,
                          ((mirror).left))
    return mirror

# Driver Code
if __name__=='__main__':

    tree = createNode(5)
    tree.left = createNode(3)
    tree.right = createNode(6)
    tree.left.left = createNode(2)
    tree.left.right = createNode(4)

    # Print inorder traversal of the input tree
    print("Inorder of original tree: ")
    inorder(tree)
    mirror = None
    mirror = mirrorify(tree, mirror)

    # Print inorder traversal of the mirror tree
    print("\nInorder of mirror tree: ")
    inorder(mirror)

# This code is contributed by Arnab Kundu
```

## C#

```
// c# implementation of the approach
using System;
public class GFG
{

// A binary tree node has data, pointer to
// left child and a pointer to right child
public class node
{
    public int val;
    public node left;
    public node right;
}

// Helper function that allocates
// a new node with the given data
// and null left and right pointers
public static node createNode(int val)
{
    node newNode = new node();
    newNode.val = val;
    newNode.left = null;
    newNode.right = null;
    return newNode;
}

// Helper function to print Inorder traversal
public static void inorder(node root)
{
    if (root == null)
    {
        return;
    }
    inorder(root.left);
    Console.Write("{0:D} ", root.val);
    inorder(root.right);
}

// mirrorify function takes two trees,
// original tree and a mirror tree
// It recurses on both the trees,
// but when original tree recurses on left,
// mirror tree recurses on right and
// vice-versa
public static node mirrorify(node root)
{
    if (root == null)
    {
        return null;

    }

    // Create new mirror node from original tree node
    node mirror = createNode(root.val);
    mirror.right = mirrorify(root.left);
    mirror.left = mirrorify(root.right);
    return mirror;
}

// Driver code
public static void Main(string[] args)
{

    node tree = createNode(5);
    tree.left = createNode(3);
    tree.right = createNode(6);
    tree.left.left = createNode(2);
    tree.left.right = createNode(4);

    // Print inorder traversal of the input tree
    Console.Write("Inorder of original tree: ");
    inorder(tree);
    node mirror = null;
    mirror = mirrorify(tree);

    // Print inorder traversal of the mirror tree
    Console.Write("\nInorder of mirror tree: ");
    inorder(mirror);
}
}
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// A binary tree node has data, pointer to
// left child and a pointer to right child
class node
{
    constructor()
    {
        this.val=0;
        this.left=this.right=null;
    }
}

// Helper function that allocates
// a new node with the given data
// and null left and right pointers
function createNode(val)
{
    let newNode = new node();
    newNode.val = val;
    newNode.left = null;
    newNode.right = null;
    return newNode;
}

// Helper function to print Inorder traversal
function inorder(root)
{
    if (root == null)
        return;
    inorder(root.left);
    document.write(root.val+" ");
    inorder(root.right);
}

// mirrorify function takes two trees,
// original tree and a mirror tree
// It recurses on both the trees,
// but when original tree recurses on left,
// mirror tree recurses on right and
// vice-versa
function mirrorify(root)
{
    if (root == null)
    {
        return null;

    }

    // Create new mirror node from original tree node
    let mirror = createNode(root.val);
    mirror.right = mirrorify(root.left);
    mirror.left = mirrorify(root.right);
    return mirror;
}

// Driver code
let tree = createNode(5);
tree.left = createNode(3);
tree.right = createNode(6);
tree.left.left = createNode(2);
tree.left.right = createNode(4);

// Print inorder traversal of the input tree
document.write("Inorder of original tree: ");
inorder(tree);
let mirror = null;
mirror = mirrorify(tree);

// Print inorder traversal of the mirror tree
document.write("<br>Inorder of mirror tree: ");
inorder(mirror);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
Inorder of original tree: 2 3 4 5 6 
Inorder of mirror tree: 6 5 4 3 2 
```

**方法 2:**
为了改变其镜像树中的原始树，然后我们简单地交换每个节点的左右链接。如果该节点是叶节点，则什么也不做。

## C++

```
#include <iostream>
using namespace std;

typedef struct treenode {
    int val;
    struct treenode* left;
    struct treenode* right;
} node;

// Helper function that
// allocates a new node with the
// given data and NULL left and right pointers
node* createNode(int val)
{
    node* newNode = (node*)malloc(sizeof(node));
    newNode->val = val;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// Function to print the inrder traversal
void inorder(node* root)
{
    if (root == NULL)
        return;
    inorder(root->left);
    printf("%d ", root->val);
    inorder(root->right);
}

// Function to convert to  mirror tree
treenode* mirrorTree(node* root)
{
    // Base Case
    if (root == NULL)
        return root;
    node* t = root->left;
    root->left = root->right;
    root->right = t;

    if (root->left)
        mirrorTree(root->left);
    if (root->right)
        mirrorTree(root->right);

  return root;
}

// Driver Code
int main()
{

    node* tree = createNode(5);
    tree->left = createNode(3);
    tree->right = createNode(6);
    tree->left->left = createNode(2);
    tree->left->right = createNode(4);
    printf("Inorder of original tree: ");
    inorder(tree);

    // Function call
    mirrorTree(tree);

    printf("\nInorder of Mirror tree: ");
    inorder(tree);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

static class Node
{
    int val;
    Node left;
    Node right;
}

// Helper function that allocates
// a new node with the given data
// and null left and right references
public static Node createNode(int val)
{
    Node newNode = new Node();
    newNode.val = val;
    newNode.left = null;
    newNode.right = null;
    return newNode;
}

// Function to print the inorder traversal
public static void inOrder(Node root)
{
    if (root == null)
        return;

    inOrder(root.left);
    System.out.print(root.val + " ");
    inOrder(root.right);
}

// Function to convert to mirror tree
// by swapping the left and right links.
public static Node mirrorTree(Node root)
{
    if (root == null)
        return null;

    Node left = mirrorTree(root.left);
    Node right = mirrorTree(root.right);

    root.left = right;
    root.right = left;

    return root;
}

// Driver Code
public static void main(String args[])
{
    Node tree = createNode(5);
    tree.left = createNode(3);
    tree.right = createNode(6);
    tree.left.left = createNode(2);
    tree.left.right = createNode(4);
    System.out.print("Inorder of original tree: ");
    inOrder(tree);

    // Function call
    mirrorTree(tree);

    System.out.print("\nInorder of mirror tree: ");
    inOrder(tree);
}
}

// This code is contributed by Ryan Ranaut
```

## 蟒蛇 3

```
# code
class Node:
   def __init__(self,data):
       self.left = None
       self.right = None
       self.data = data

def inOrder(root):
   if root is not None:
       inOrder(root.left)
       print (root.data, end = ' ')
       inOrder(root.right)

#we recursively call the mirror function which swaps the right subtree with the left subtree.
def mirror(root):
    if root is None:
        return
    mirror(root.left)
    mirror(root.right)
    root.left, root.right = root.right, root.left

root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.right.left = Node(5)

print("The inorder traversal of the tree before mirroring:",end=' ')
print(inOrder(root))
# 4 2 1 5 3
print()
mirror(root)
print("The inorder traversal of the tree after mirroring:",end=' ')
print(inOrder(root))
# 3 5 1 2 4
```

## C#

```
using System;

public class GFG{

public class Node
{
    public int val;
    public Node left;
    public Node right;
}

// Helper function that allocates
// a new node with the given data
// and null left and right references
public static Node createNode(int val)
{
    Node newNode = new Node();
    newNode.val = val;
    newNode.left = null;
    newNode.right = null;
    return newNode;
}

// Function to print the inorder traversal
public static void inOrder(Node root)
{
    if (root == null)
        return;

    inOrder(root.left);
    Console.Write(root.val + " ");
    inOrder(root.right);
}

// Function to convert to mirror tree
// by swapping the left and right links.
public static Node mirrorTree(Node root)
{
    if (root == null)
        return null;

    Node left = mirrorTree(root.left);
    Node right = mirrorTree(root.right);

    root.left = right;
    root.right = left;

    return root;
}

// Driver Code
public static void Main(String []args)
{
    Node tree = createNode(5);
    tree.left = createNode(3);
    tree.right = createNode(6);
    tree.left.left = createNode(2);
    tree.left.right = createNode(4);
    Console.Write("Inorder of original tree: ");
    inOrder(tree);

    // Function call
    mirrorTree(tree);

    Console.Write("\nInorder of mirror tree: ");
    inOrder(tree);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

class Node
{
    constructor()
    {
        this.val=0;
        this.left=this.right=null;
    }
}

// Helper function that allocates
// a new node with the given data
// and null left and right references
function createNode(val)
{
    let newNode = new Node();
    newNode.val = val;
    newNode.left = null;
    newNode.right = null;
    return newNode;
}

// Function to print the inorder traversal
function inOrder(root)
{
    if (root == null)
        return;

    inOrder(root.left);
    document.write(root.val + " ");
    inOrder(root.right);
}

// Function to convert to mirror tree
// by swapping the left and right links.
function mirrorTree(root)
{
    if (root == null)
        return null;

    let left = mirrorTree(root.left);
    let right = mirrorTree(root.right);

    root.left = right;
    root.right = left;

    return root;
}

// Driver Code
    let tree = createNode(5);
    tree.left = createNode(3);
    tree.right = createNode(6);
    tree.left.left = createNode(2);
    tree.left.right = createNode(4);
    document.write("Inorder of original tree: " );
    inOrder(tree);

    // Function call
    mirrorTree(tree);

    document.write("<br>" +"\nInorder of mirror tree: ");
    inOrder(tree);

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
Inorder of original tree: 2 3 4 5 6 
Inorder of Mirror tree: 6 5 4 3 2 
```