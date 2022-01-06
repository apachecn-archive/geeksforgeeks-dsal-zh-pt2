# 在二叉树中找到最近的叶子

> 原文:[https://www . geesforgeks . org/find-最近的叶子-二叉树/](https://www.geeksforgeeks.org/find-closest-leaf-binary-tree/)

给定一棵二叉树和一个关键字“k”，找到离“k”最近的叶子的距离。

示例:

```
              A
            /    \    
           B       C
                 /   \  
                E     F   
               /       \
              G         H
             / \       /
            I   J     K

Closest leaf to 'H' is 'K', so distance is 1 for 'H'
Closest leaf to 'C' is 'B', so distance is 2 for 'C'
Closest leaf to 'E' is either 'I' or 'J', so distance is 2 for 'E' 
Closest leaf to 'B' is 'B' itself, so distance is 0 for 'B' 
```

这里要注意的要点是，最接近的键可以是给定键的后代，也可以通过祖先之一到达。

这个想法是预先遍历给定的树，并在一个数组中跟踪祖先。当我们到达给定的键时，我们计算以给定键为根的子树中最近的叶子的距离。我们还逐一遍历所有祖先，找到以祖先为根的子树中最近的叶子的距离。我们比较所有距离并返回最小值。

下面是上述方法的实现。

## C++

```
// A C++ program to find the closest leaf of a given key in Binary Tree
#include <bits/stdc++.h>
using namespace std;

/* A binary tree Node has key, pocharer to left and right children */
struct Node
{
    char key;
    struct Node* left, *right;
};

/* Helper function that allocates a new node with the
   given data and NULL left and right pocharers. */
Node *newNode(char k)
{
    Node *node = new Node;
    node->key = k;
    node->right = node->left = NULL;
    return node;
}

// A utility function to find minimum of x and y
int getMin(int x, int y)
{
    return (x < y)? x :y;
}

// A utility function to find distance of closest leaf of the tree
// rooted under given root
int closestDown(struct Node *root)
{
    // Base cases
    if (root == NULL)
        return INT_MAX;
    if (root->left == NULL && root->right == NULL)
        return 0;

    // Return minimum of left and right, plus one
    return 1 + getMin(closestDown(root->left), closestDown(root->right));
}

// Returns distance of the closest leaf to a given key 'k'.  The array
// ancestors is used to keep track of ancestors of current node and
// 'index' is used to keep track of current index in 'ancestors[]'
int findClosestUtil(struct Node *root, char k, struct Node *ancestors[],
                                               int index)
{
    // Base case
    if (root == NULL)
        return INT_MAX;

    // If key found
    if (root->key == k)
    {
        //  Find the closest leaf under the subtree rooted with given key
        int res = closestDown(root);

        // Traverse all ancestors and update result if any parent node
        // gives smaller distance
        for (int i = index-1; i>=0; i--)
            res = getMin(res, index - i + closestDown(ancestors[i]));
        return res;
    }

    // If key node found, store current node and recur for left and
    // right childrens
    ancestors[index] = root;
    return getMin(findClosestUtil(root->left, k, ancestors, index+1),
                  findClosestUtil(root->right, k, ancestors, index+1));

}

// The main function that returns distance of the closest key to 'k'. It
// mainly uses recursive function findClosestUtil() to find the closes
// distance.
int findClosest(struct Node *root, char k)
{
    // Create an array to store ancestors
    // Assumption: Maximum height of tree is 100
    struct Node *ancestors[100];

    return findClosestUtil(root, k, ancestors, 0);
}

/* Driver program to test above functions*/
int main()
{
    // Let us construct the BST shown in the above figure
    struct Node *root        = newNode('A');
    root->left               = newNode('B');
    root->right              = newNode('C');
    root->right->left        = newNode('E');
    root->right->right       = newNode('F');
    root->right->left->left  = newNode('G');
    root->right->left->left->left  = newNode('I');
    root->right->left->left->right = newNode('J');
    root->right->right->right      = newNode('H');
    root->right->right->right->left = newNode('K');

    char k = 'H';
    cout << "Distance of the closest key from " << k << " is "
         << findClosest(root, k) << endl;
    k = 'C';
    cout << "Distance of the closest key from " << k << " is "
         << findClosest(root, k) << endl;
    k = 'E';
    cout << "Distance of the closest key from " << k << " is "
         << findClosest(root, k) << endl;
    k = 'B';
    cout << "Distance of the closest key from " << k << " is "
         << findClosest(root, k) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find closest leaf of a given key in Binary Tree

/* Class containing left and right child of current
   node and key value*/
class Node
{
    int data;
    Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    // A utility function to find minimum of x and y
    int getMin(int x, int y)
    {
        return (x < y) ? x : y;
    }

    // A utility function to find distance of closest leaf of the tree
    // rooted under given root
    int closestDown(Node node)
    {
        // Base cases
        if (node == null)
            return Integer.MAX_VALUE;
        if (node.left == null && node.right == null)
            return 0;

        // Return minimum of left and right, plus one
        return 1 + getMin(closestDown(node.left), closestDown(node.right));
    }

    // Returns distance of the closest leaf to a given key 'k'.  The array
    // ancestors is used to keep track of ancestors of current node and
    // 'index' is used to keep track of current index in 'ancestors[]'
    int findClosestUtil(Node node, char k, Node ancestors[], int index)
    {
        // Base case
        if (node == null)
            return Integer.MAX_VALUE;

        // If key found
        if (node.data == k)
        {
            //  Find the closest leaf under the subtree rooted with given key
            int res = closestDown(node);

            // Traverse all ancestors and update result if any parent node
            // gives smaller distance
            for (int i = index - 1; i >= 0; i--)
                res = getMin(res, index - i + closestDown(ancestors[i]));
            return res;
        }

        // If key node found, store current node and recur for left and
        // right childrens
        ancestors[index] = node;
        return getMin(findClosestUtil(node.left, k, ancestors, index + 1),
                findClosestUtil(node.right, k, ancestors, index + 1));

    }

    // The main function that returns distance of the closest key to 'k'. It
    // mainly uses recursive function findClosestUtil() to find the closes
    // distance.
    int findClosest(Node node, char k)
    {
        // Create an array to store ancestors
        // Assumption: Maximum height of tree is 100
        Node ancestors[] = new Node[100];

        return findClosestUtil(node, k, ancestors, 0);
    }

    // Driver program to test for above functions
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node('A');
        tree.root.left = new Node('B');
        tree.root.right = new Node('C');
        tree.root.right.left = new Node('E');
        tree.root.right.right = new Node('F');
        tree.root.right.left.left = new Node('G');
        tree.root.right.left.left.left = new Node('I');
        tree.root.right.left.left.right = new Node('J');
        tree.root.right.right.right = new Node('H');
        tree.root.right.right.right.left = new Node('H');

        char k = 'H';
        System.out.println("Distance of the closest key from " + k + " is "
                            + tree.findClosest(tree.root, k));
        k = 'C';
        System.out.println("Distance of the closest key from " + k + " is "
                            + tree.findClosest(tree.root, k));
        k = 'E';
        System.out.println("Distance of the closest key from " + k + " is "
                            + tree.findClosest(tree.root, k));
        k = 'B';
        System.out.println("Distance of the closest key from " + k + " is "
                             + tree.findClosest(tree.root, k));

    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to find closest leaf of a
# given key in binary tree

INT_MAX = 2**32

# A binary tree node
class Node:
    # Constructor to create a binary tree
    def __init__(self ,key):
        self.key = key
        self.left  = None
        self.right = None

def closestDown(root):
    #Base Case
    if root is None:
        return INT_MAX
    if root.left is None and root.right is None:
        return 0

    # Return minimum of left and right plus one
    return 1 + min(closestDown(root.left),
                   closestDown(root.right))

# Returns distance of the closes leaf to a given key k
# The array ancestors us used to keep track of ancestors
# of current node and 'index' is used to keep track of
# current index in 'ancestors[i]'
def findClosestUtil(root, k, ancestors, index):
    # Base Case
    if root is None:
        return INT_MAX

    # if key found
    if root.key == k:
        # Find closest leaf under the subtree rooted
        # with given key
        res = closestDown(root)

        # Traverse ll ancestors and update result if any
        # parent node gives smaller distance
        for i in reversed(range(0,index)):
            res = min(res, index-i+closestDown(ancestors[i]))
        return res

    # if key node found, store current node and recur for left
    # and right childrens
    ancestors[index] = root
    return min(
        findClosestUtil(root.left, k,ancestors, index+1),
        findClosestUtil(root.right, k, ancestors, index+1))

# The main function that return distance of the clses key to
# 'key'. It mainly uses recursive function findClosestUtil()
# to find the closes distance
def findClosest(root, k):
    # Create an array to store ancestors
    # Assumption: Maximum height of tree is 100
    ancestors = [None for i in range(100)]

    return findClosestUtil(root, k, ancestors, 0)

# Driver program to test above function
root = Node('A')
root.left = Node('B')
root.right = Node('C');
root.right.left = Node('E');
root.right.right  = Node('F');
root.right.left.left = Node('G');
root.right.left.left.left  = Node('I');
root.right.left.left.right = Node('J');
root.right.right.right  = Node('H');
root.right.right.right.left = Node('K');

k = 'H';
print "Distance of the closest key from "+ k + " is",
print findClosest(root, k)

k = 'C'
print "Distance of the closest key from " + k + " is",
print findClosest(root, k)

k = 'E'
print "Distance of the closest key from " + k + " is",
print findClosest(root, k)

k = 'B'
print "Distance of the closest key from " + k + " is",
print findClosest(root, k)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;

// C# program to find closest leaf of a given key in Binary Tree

/* Class containing left and right child of current 
   node and key value*/
public class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

public class BinaryTree
{
    public Node root;

    // A utility function to find minimum of x and y
    public virtual int getMin(int x, int y)
    {
        return (x < y) ? x : y;
    }

    // A utility function to find distance of closest leaf of the tree
    // rooted under given root
    public virtual int closestDown(Node node)
    {
        // Base cases
        if (node == null)
        {
            return int.MaxValue;
        }
        if (node.left == null && node.right == null)
        {
            return 0;
        }

        // Return minimum of left and right, plus one
        return 1 + getMin(closestDown(node.left), closestDown(node.right));
    }

    // Returns distance of the closest leaf to a given key 'k'.  The array
    // ancestors is used to keep track of ancestors of current node and
    // 'index' is used to keep track of current index in 'ancestors[]'
    public virtual int findClosestUtil(Node node, char k, Node[] ancestors, int index)
    {
        // Base case
        if (node == null)
        {
            return int.MaxValue;
        }

        // If key found
        if ((char)node.data == k)
        {
            //  Find the closest leaf under the subtree rooted with given key
            int res = closestDown(node);

            // Traverse all ancestors and update result if any parent node
            // gives smaller distance
            for (int i = index - 1; i >= 0; i--)
            {
                res = getMin(res, index - i + closestDown(ancestors[i]));
            }
            return res;
        }

        // If key node found, store current node and recur for left and
        // right childrens
        ancestors[index] = node;
        return getMin(findClosestUtil(node.left, k, ancestors, index + 1), findClosestUtil(node.right, k, ancestors, index + 1));

    }

    // The main function that returns distance of the closest key to 'k'. It
    // mainly uses recursive function findClosestUtil() to find the closes
    // distance.
    public virtual int findClosest(Node node, char k)
    {
        // Create an array to store ancestors
        // Assumption: Maximum height of tree is 100
        Node[] ancestors = new Node[100];

        return findClosestUtil(node, k, ancestors, 0);
    }

    // Driver program to test for above functions
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node('A');
        tree.root.left = new Node('B');
        tree.root.right = new Node('C');
        tree.root.right.left = new Node('E');
        tree.root.right.right = new Node('F');
        tree.root.right.left.left = new Node('G');
        tree.root.right.left.left.left = new Node('I');
        tree.root.right.left.left.right = new Node('J');
        tree.root.right.right.right = new Node('H');
        tree.root.right.right.right.left = new Node('H');

        char k = 'H';
        Console.WriteLine("Distance of the closest key from " + k + " is " + tree.findClosest(tree.root, k));
        k = 'C';
        Console.WriteLine("Distance of the closest key from " + k + " is " + tree.findClosest(tree.root, k));
        k = 'E';
        Console.WriteLine("Distance of the closest key from " + k + " is " + tree.findClosest(tree.root, k));
        k = 'B';
        Console.WriteLine("Distance of the closest key from " + k + " is " + tree.findClosest(tree.root, k));

    }
}

  //  This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to find closest
// leaf of a given key in Binary Tree

/* Class containing left and right child of current 
   node and key value*/
class Node
{
  constructor(item)
  {
    this.data = item;
    this.left = null;
    this.right= null;
  }
}

var root = null;

// A utility function to find minimum of x and y
function getMin(x, y)
{
    return (x < y) ? x : y;
}

// A utility function to find distance of closest leaf of the tree
// rooted under given root
function closestDown(node)
{
    // Base cases
    if (node == null)
    {
        return 1000000000;
    }
    if (node.left == null && node.right == null)
    {
        return 0;
    }
    // Return minimum of left and right, plus one
    return 1 +
    getMin(closestDown(node.left), closestDown(node.right));
}
// Returns distance of the closest
// leaf to a given key 'k'.  The array
// ancestors is used to keep track of
// ancestors of current node and
// 'index' is used to keep track of
// current index in 'ancestors[]'
function findClosestUtil(node, k, ancestors, index)
{
    // Base case
    if (node == null)
    {
        return 1000000000;
    }
    // If key found
    if (node.data == k)
    {
        //  Find the closest leaf under the
        // subtree rooted with given key
        var res = closestDown(node);
        // Traverse all ancestors and update
        // result if any parent node
        // gives smaller distance
        for (var i = index - 1; i >= 0; i--)
        {
            res = getMin(res, index - i +
            closestDown(ancestors[i]));
        }
        return res;
    }
    // If key node found, store current
    // node and recur for left and
    // right childrens
    ancestors[index] = node;
    return getMin(findClosestUtil(node.left, k,
    ancestors, index + 1),
    findClosestUtil(node.right, k, ancestors,
    index + 1));
}
// The main function that returns
// distance of the closest key to 'k'. It
// mainly uses recursive function
// findClosestUtil() to find the closes
// distance.
function findClosest(node, k)
{
    // Create an array to store ancestors
    // Assumption: Maximum height of tree is 100
    var ancestors = Array(100).fill(null);
    return findClosestUtil(node, k, ancestors, 0);
}
// Driver program to test for above functions
root = new Node('A');
root.left = new Node('B');
root.right = new Node('C');
root.right.left = new Node('E');
root.right.right = new Node('F');
root.right.left.left = new Node('G');
root.right.left.left.left = new Node('I');
root.right.left.left.right = new Node('J');
root.right.right.right = new Node('H');
root.right.right.right.left = new Node('H');
var k = 'H';
document.write(
"Distance of the closest key from " + k
+ " is " + findClosest(root, k) + "<br>");
k = 'C';
document.write(
"Distance of the closest key from " +
k + " is " + findClosest(root, k)+ "<br>");
k = 'E';
document.write(
"Distance of the closest key from " + k
+ " is " + findClosest(root, k)+ "<br>");
k = 'B';
document.write(
"Distance of the closest key from " + k
+ " is " + findClosest(root, k)+ "<br>");

</script>
```

**输出:**

```
Distance of the closest key from H is 1
Distance of the closest key from C is 2
Distance of the closest key from E is 2
Distance of the closest key from B is 0 
```

通过将左/右信息也存储在祖先数组中，可以优化上述代码。其思想是，如果给定的键位于祖先的左子树中，那么就没有必要调用 closestDown()。此外，遍历祖先数组的循环可以优化为不遍历比当前结果距离更远的祖先。

**练习:**
把上面的解延伸打印出来的不仅仅是距离，还有最接近叶子的关键也。
本文由舒巴姆供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息