# 二叉树的最大宽度

> 原文:[https://www . geesforgeks . org/二叉树最大宽度/](https://www.geeksforgeeks.org/maximum-width-of-a-binary-tree/)

给定一棵二叉树，写一个函数得到给定树的最大宽度。树的宽度是所有级别宽度的最大值。

让我们考虑下面的示例树。

```
         1
        /  \
       2    3
     /  \     \
    4    5     8 
              /  \
             6    7
```

上图中，1 级
宽度为 1，2 级
宽度为 2，3 级
宽度为 3，4 级
宽度为 2。
所以树的最大宽度是 3。

**方法 1(使用层级顺序遍历)**
该方法主要涉及两个功能。一种是统计给定级别的节点数(getWidth)，另一种是得到树的最大宽度(getMaxWidth)。getMaxWidth()利用 getWidth()获取从根开始的所有级别的宽度。

```
/*Function to print level order traversal of tree*/
getMaxWidth(tree)
maxWdth = 0
for i = 1 to height(tree)
  width =   getWidth(tree, i);
  if(width > maxWdth) 
      maxWdth  = width
return maxWidth
```

```
/*Function to get width of a given level */
getWidth(tree, level)
if tree is NULL then return 0;
if level is 1, then return 1;  
else if level greater than 1, then
    return getWidth(tree->left, level-1) + 
    getWidth(tree->right, level-1);
```

下面是上述想法的实现:

## C++

```
// C++ program to calculate width of binary tree
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
class node {
public:
    int data;
    node* left;
    node* right;
};

/*Function prototypes*/
int getWidth(node* root, int level);
int height(node* node);
node* newNode(int data);

/* Function to get the maximum width of a binary tree*/
int getMaxWidth(node* root)
{
    int maxWidth = 0;
    int width;
    int h = height(root);
    int i;

    /* Get width of each level and compare
        the width with maximum width so far */
    for (i = 1; i <= h; i++) {
        width = getWidth(root, i);
        if (width > maxWidth)
            maxWidth = width;
    }

    return maxWidth;
}

/* Get width of a given level */
int getWidth(node* root, int level)
{

    if (root == NULL)
        return 0;

    if (level == 1)
        return 1;

    else if (level > 1)
        return getWidth(root->left, level - 1)
               + getWidth(root->right, level - 1);
}

/* UTILITY FUNCTIONS */
/* Compute the "height" of a tree -- the number of
    nodes along the longest path from the root node
    down to the farthest leaf node.*/
int height(node* node)
{
    if (node == NULL)
        return 0;
    else {
        /* compute the height of each subtree */
        int lHeight = height(node->left);
        int rHeight = height(node->right);
        /* use the larger one */

        return (lHeight > rHeight) ? (lHeight + 1)
                                   : (rHeight + 1);
    }
}

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
node* newNode(int data)
{
    node* Node = new node();
    Node->data = data;
    Node->left = NULL;
    Node->right = NULL;
    return (Node);
}

/* Driver code*/
int main()
{
    node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(8);
    root->right->right->left = newNode(6);
    root->right->right->right = newNode(7);

    /*
    Constructed binary tree is:
            1
            / \
        2 3
        / \ \
        4 5 8
                / \
                6 7
    */

    // Function call
    cout << "Maximum width is " << getMaxWidth(root)
         << endl;
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to calculate width of binary tree
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node {
    int data;
    struct node* left;
    struct node* right;
};

/*Function prototypes*/
int getWidth(struct node* root, int level);
int height(struct node* node);
struct node* newNode(int data);

/* Function to get the maximum width of a binary tree*/
int getMaxWidth(struct node* root)
{
    int maxWidth = 0;
    int width;
    int h = height(root);
    int i;

    /* Get width of each level and compare
       the width with maximum width so far */
    for (i = 1; i <= h; i++) {
        width = getWidth(root, i);
        if (width > maxWidth)
            maxWidth = width;
    }

    return maxWidth;
}

/* Get width of a given level */
int getWidth(struct node* root, int level)
{

    if (root == NULL)
        return 0;

    if (level == 1)
        return 1;

    else if (level > 1)
        return getWidth(root->left, level - 1)
               + getWidth(root->right, level - 1);
}

/* UTILITY FUNCTIONS */
/* Compute the "height" of a tree -- the number of
    nodes along the longest path from the root node
    down to the farthest leaf node.*/
int height(struct node* node)
{
    if (node == NULL)
        return 0;
    else {
        /* compute the height of each subtree */
        int lHeight = height(node->left);
        int rHeight = height(node->right);
        /* use the larger one */

        return (lHeight > rHeight) ? (lHeight + 1)
                                   : (rHeight + 1);
    }
}
/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct node* newNode(int data)
{
    struct node* node
        = (struct node*)malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return (node);
}
/* Driver code*/
int main()
{
    struct node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(8);
    root->right->right->left = newNode(6);
    root->right->right->right = newNode(7);

    /*
     Constructed binary tree is:
            1
          /  \
         2    3
       /  \     \
      4   5     8
                /  \
               6   7
    */

    // Function call
    printf("Maximum width is %d \n", getMaxWidth(root));
    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate width of binary tree

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
class Node {
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree {
    Node root;

    /* Function to get the maximum width of a binary tree*/
    int getMaxWidth(Node node)
    {
        int maxWidth = 0;
        int width;
        int h = height(node);
        int i;

        /* Get width of each level and compare
           the width with maximum width so far */
        for (i = 1; i <= h; i++) {
            width = getWidth(node, i);
            if (width > maxWidth)
                maxWidth = width;
        }

        return maxWidth;
    }

    /* Get width of a given level */
    int getWidth(Node node, int level)
    {
        if (node == null)
            return 0;

        if (level == 1)
            return 1;
        else if (level > 1)
            return getWidth(node.left, level - 1)
                + getWidth(node.right, level - 1);
        return 0;
    }

    /* UTILITY FUNCTIONS */

    /* Compute the "height" of a tree -- the number of
     nodes along the longest path from the root node
     down to the farthest leaf node.*/
    int height(Node node)
    {
        if (node == null)
            return 0;
        else {
            /* compute the height of each subtree */
            int lHeight = height(node.left);
            int rHeight = height(node.right);

            /* use the larger one */
            return (lHeight > rHeight) ? (lHeight + 1)
                                       : (rHeight + 1);
        }
    }

    /* Driver code */
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();

        /*
        Constructed binary tree is:
              1
            /  \
           2    3
         /  \    \
        4   5     8
                 /  \
                6   7
         */
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.right = new Node(8);
        tree.root.right.right.left = new Node(6);
        tree.root.right.right.right = new Node(7);

        // Function call
        System.out.println("Maximum width is "
                           + tree.getMaxWidth(tree.root));
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to find the maximum width of
# binary tree using Level Order Traversal.

# A binary tree node

class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to get the maximum width of a binary tree

def getMaxWidth(root):
    maxWidth = 0
    h = height(root)
    # Get width of each level and compare the
    # width with maximum width so far
    for i in range(1, h+1):
        width = getWidth(root, i)
        if (width > maxWidth):
            maxWidth = width
    return maxWidth

# Get width of a given level

def getWidth(root, level):
    if root is None:
        return 0
    if level == 1:
        return 1
    elif level > 1:
        return (getWidth(root.left, level-1) +
                getWidth(root.right, level-1))

# UTILITY FUNCTIONS
# Compute the "height" of a tree -- the number of
# nodes along the longest path from the root node
# down to the farthest leaf node.

def height(node):
    if node is None:
        return 0
    else:

        # compute the height of each subtree
        lHeight = height(node.left)
        rHeight = height(node.right)

        # use the larger one
        return (lHeight+1) if (lHeight > rHeight) else (rHeight+1)

# Driver code
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.right = Node(8)
root.right.right.left = Node(6)
root.right.right.right = Node(7)

"""
Constructed binary tree is:
    1
    / \
    2 3
    / \     \
4 5 8
        / \
        6 7
"""
# Function call
print "Maximum width is %d" % (getMaxWidth(root))

# This code is contributed by Naveen Aili
```

## C#

```
// C# program to calculate width of binary tree
using System;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
public class Node {
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

public class BinaryTree {
    public Node root;

    /* Function to get the maximum width of a binary tree*/
    public virtual int getMaxWidth(Node node)
    {
        int maxWidth = 0;
        int width;
        int h = height(node);
        int i;

        /* Get width of each level and compare
        the width with maximum width so far */
        for (i = 1; i <= h; i++) {
            width = getWidth(node, i);
            if (width > maxWidth) {
                maxWidth = width;
            }
        }

        return maxWidth;
    }

    /* Get width of a given level */
    public virtual int getWidth(Node node, int level)
    {
        if (node == null) {
            return 0;
        }

        if (level == 1) {
            return 1;
        }
        else if (level > 1) {
            return getWidth(node.left, level - 1)
                + getWidth(node.right, level - 1);
        }
        return 0;
    }

    /* UTILITY FUNCTIONS */

    /* Compute the "height" of a tree -- the number of
    nodes along the longest path from the root node
    down to the farthest leaf node.*/
    public virtual int height(Node node)
    {
        if (node == null) {
            return 0;
        }
        else {
            /* compute the height of each subtree */
            int lHeight = height(node.left);
            int rHeight = height(node.right);

            /* use the larger one */
            return (lHeight > rHeight) ? (lHeight + 1)
                                       : (rHeight + 1);
        }
    }

    /* Driver code */
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();

        /*
        Constructed binary tree is:
            1
            / \
        2 3
        / \ \
        4 5     8
                / \
                6 7
        */
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.right = new Node(8);
        tree.root.right.right.left = new Node(6);
        tree.root.right.right.right = new Node(7);

        // Function call
        Console.WriteLine("Maximum width is "
                          + tree.getMaxWidth(tree.root));
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to calculate width of binary tree

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
class Node {
    constructor(val) {
        this.data = val;
        this.left = null;
        this.right = null;
    }
}
    var root;

    /* Function to get the maximum width of a binary tree*/
    function getMaxWidth(node)
    {
        var maxWidth = 0;
        var width;
        var h = height(node);
        var i;

        /* Get width of each level and compare
           the width with maximum width so far */
        for (i = 1; i <= h; i++) {
            width = getWidth(node, i);
            if (width > maxWidth)
                maxWidth = width;
        }

        return maxWidth;
    }

    /* Get width of a given level */
    function getWidth(node , level)
    {
        if (node == null)
            return 0;

        if (level == 1)
            return 1;
        else if (level > 1)
            return getWidth(node.left, level - 1)
                + getWidth(node.right, level - 1);
        return 0;
    }

    /* UTILITY FUNCTIONS */

    /* Compute the "height" of a tree -- the number of
     nodes along the longest path from the root node
     down to the farthest leaf node.*/
    function height(node)
    {
        if (node == null)
            return 0;
        else {
            /* compute the height of each subtree */
            var lHeight = height(node.left);
            var rHeight = height(node.right);

            /* use the larger one */
            return (lHeight > rHeight) ? (lHeight + 1)
                                       : (rHeight + 1);
        }
    }

    /* Driver code */

        /*
        Constructed binary tree is:
              1
            /  \
           2    3
         /  \    \
        4   5     8
                 /  \
                6   7
         */
        root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.right = new Node(8);
        root.right.right.left = new Node(6);
        root.right.right.right = new Node(7);

        // Function call
        document.write("Maximum width is "
                           + getMaxWidth(root));
// This code is contributed by todaysgaurav

</script>
```

**Output**

```
Maximum width is 3
```

**时间复杂度:最坏情况下** O(n <sup>2</sup> )。
我们可以使用基于队列的层次顺序遍历来优化该方法的时间复杂度。在最坏的情况下，基于队列的级别顺序遍历将花费 O(n)个时间。感谢 [Nitish](https://www.geeksforgeeks.org/archives/7447/comment-page-1#comment-1202) 、 [DivyaC](https://www.geeksforgeeks.org/archives/7447/comment-page-1#comment-1143) 和 [tech.login.id2](https://www.geeksforgeeks.org/archives/7447/comment-page-1#comment-1783) 对本次优化的建议。查看他们关于使用基于队列的遍历实现的评论。

**方法 2(使用带队列的级别顺序遍历)**
在该方法中，我们将当前级别的所有子节点存储在队列中，然后在完成特定级别的级别顺序遍历后，统计节点总数。由于队列现在包含了下一级的所有节点，所以我们可以通过查找队列的大小很容易地找出下一级的节点总数。然后，我们对连续的级别遵循相同的过程。我们存储并更新在每个级别找到的最大节点数。

下面是上述想法的实现:

## C++

```
// A queue based C++ program to find maximum width
// of a Binary Tree
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Function to find the maximum width of the tree
// using level order traversal
int maxWidth(struct Node* root)
{
    // Base case
    if (root == NULL)
        return 0;

    // Initialize result
    int result = 0;

    // Do Level order traversal keeping track of number
    // of nodes at every level.
    queue<Node*> q;
    q.push(root);
    while (!q.empty()) {
        // Get the size of queue when the level order
        // traversal for one level finishes
        int count = q.size();

        // Update the maximum node count value
        result = max(count, result);

        // Iterate for all the nodes in the queue currently
        while (count--) {
            // Dequeue an node from queue
            Node* temp = q.front();
            q.pop();

            // Enqueue left and right children of
            // dequeued node
            if (temp->left != NULL)
                q.push(temp->left);
            if (temp->right != NULL)
                q.push(temp->right);
        }
    }

    return result;
}

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Driver code
int main()
{
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(8);
    root->right->right->left = newNode(6);
    root->right->right->right = newNode(7);

    /*   Constructed Binary tree is:
                 1
               /   \
             2      3
           /  \      \
          4    5      8
                    /   \
                   6     7    */

    // Function call
    cout << "Maximum width is " << maxWidth(root) << endl;
    return 0;
}

// This code is contributed by Nikhil Kumar
// Singh(nickzuck_007)
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate maximum width
// of a binary tree using queue
import java.util.LinkedList;
import java.util.Queue;

public class maxwidthusingqueue
{
    /* A binary tree node has data, pointer to
       left child and a pointer to right child */
    static class node
    {
        int data;
        node left, right;

        public node(int data) { this.data = data; }
    }

    // Function to find the maximum width of
    // the tree using level order traversal
    static int maxwidth(node root)
    {
        // Base case
        if (root == null)
            return 0;

        // Initialize result
        int maxwidth = 0;

        // Do Level order traversal keeping
        // track of number of nodes at every level
        Queue<node> q = new LinkedList<>();
        q.add(root);
        while (!q.isEmpty())
        {
            // Get the size of queue when the level order
            // traversal for one level finishes
            int count = q.size();

            // Update the maximum node count value
            maxwidth = Math.max(maxwidth, count);

            // Iterate for all the nodes in
            // the queue currently
            while (count-- > 0) {
                // Dequeue an node from queue
                node temp = q.remove();

                // Enqueue left and right children
                // of dequeued node
                if (temp.left != null)
                {
                    q.add(temp.left);
                }
                if (temp.right != null)
                {
                    q.add(temp.right);
                }
            }
        }
        return maxwidth;
    }

    // Function call
    public static void main(String[] args)
    {
        node root = new node(1);
        root.left = new node(2);
        root.right = new node(3);
        root.left.left = new node(4);
        root.left.right = new node(5);
        root.right.right = new node(8);
        root.right.right.left = new node(6);
        root.right.right.right = new node(7);

        /*   Constructed Binary tree is:
        1
      /   \
    2      3
  /  \      \
 4    5      8
           /   \
          6     7    */

        // Function call
        System.out.println("Maximum width = "
                           + maxwidth(root));
    }
}

// This code is contributed by Rishabh Mahrsee
```

## 计算机编程语言

```
# Python program to find the maximum width of binary
# tree using Level Order Traversal with queue.

# A binary tree node

class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to get the maximum width of a binary tree

def getMaxWidth(root):
    # base case
    if root is None:
        return 0
    q = []
    maxWidth = 0

    q.insert(0, root)

    while (q != []):
        # Get the size of queue when the level order
        # traversal for one level finishes
        count = len(q)

        # Update the maximum node count value
        maxWidth = max(count, maxWidth)

        while (count is not 0):
            count = count-1
            temp = q[-1]
            q.pop()
            if temp.left is not None:
                q.insert(0, temp.left)

            if temp.right is not None:
                q.insert(0, temp.right)

    return maxWidth

# Driver program to test above function
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.right = Node(8)
root.right.right.left = Node(6)
root.right.right.right = Node(7)

"""
Constructed binary tree is:
       1
      / \
     2   3
    / \    \
   4   5   8
          / \
         6   7
"""
# Function call
print "Maximum width is %d" % (getMaxWidth(root))

# This code is contributed by Naveen Aili
```

## C#

```
// C# program to calculate maximum width
// of a binary tree using queue
using System;
using System.Collections.Generic;

public class maxwidthusingqueue
{
    /* A binary tree node has data, pointer to
    left child and a pointer to right child */
    public class node
    {
        public int data;
        public node left, right;

        public node(int data) { this.data = data; }
    }

    // Function to find the maximum width of
    // the tree using level order traversal
    static int maxwidth(node root)
    {
        // Base case
        if (root == null)
            return 0;

        // Initialize result
        int maxwidth = 0;

        // Do Level order traversal keeping
        // track of number of nodes at every level
        Queue<node> q = new Queue<node>();
        q.Enqueue(root);
        while (q.Count != 0)
        {
            // Get the size of queue when the level order
            // traversal for one level finishes
            int count = q.Count;

            // Update the maximum node count value
            maxwidth = Math.Max(maxwidth, count);

            // Iterate for all the nodes in
            // the queue currently
            while (count-- > 0) {
                // Dequeue an node from queue
                node temp = q.Dequeue();

                // Enqueue left and right children
                // of dequeued node
                if (temp.left != null)
                {
                    q.Enqueue(temp.left);
                }
                if (temp.right != null)
                {
                    q.Enqueue(temp.right);
                }
            }
        }
        return maxwidth;
    }

    // Driver code
    public static void Main(String[] args)
    {
        node root = new node(1);
        root.left = new node(2);
        root.right = new node(3);
        root.left.left = new node(4);
        root.left.right = new node(5);
        root.right.right = new node(8);
        root.right.right.left = new node(6);
        root.right.right.right = new node(7);

        /* Constructed Binary tree is:
        1
      /   \
     2     3
    / \     \
    4 5     8
           / \
           6 7 */

        Console.WriteLine("Maximum width = "
                          + maxwidth(root));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

    // JavaScript program to calculate maximum width
    // of a binary tree using queue

    class node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to find the maximum width of
    // the tree using level order traversal
    function maxwidth(root)
    {
        // Base case
        if (root == null)
            return 0;

        // Initialize result
        let maxwidth = 0;

        // Do Level order traversal keeping
        // track of number of nodes at every level
        let q = [];
        q.push(root);
        while (q.length > 0)
        {
            // Get the size of queue when the level order
            // traversal for one level finishes
            let count = q.length;

            // Update the maximum node count value
            maxwidth = Math.max(maxwidth, count);

            // Iterate for all the nodes in
            // the queue currently
            while (count-- > 0) {
                // Dequeue an node from queue
                let temp = q.shift();

                // Enqueue left and right children
                // of dequeued node
                if (temp.left != null)
                {
                    q.push(temp.left);
                }
                if (temp.right != null)
                {
                    q.push(temp.right);
                }
            }
        }
        return maxwidth;
    }

    let root = new node(1);
    root.left = new node(2);
    root.right = new node(3);
    root.left.left = new node(4);
    root.left.right = new node(5);
    root.right.right = new node(8);
    root.right.right.left = new node(6);
    root.right.right.right = new node(7);

    /*   Constructed Binary tree is:
          1
        /   \
      2      3
    /  \      \
   4    5      8
             /   \
            6     7    */

    // Function call
    document.write("Maximum width is "
                       + maxwidth(root));

</script>
```

**Output**

```
Maximum width is 3
```

**复杂度分析:**

**时间复杂度:** O(N)，其中 N 为树中节点总数。在水平顺序遍历中，树的每个节点都被处理一次，因此如果树中总共有 N 个节点，由于水平顺序遍历而导致的复杂性是 O(N)。因此，时间复杂度为 O(N)。

**辅助空间:** O(w)，其中 w 为树的最大宽度。
在水平顺序遍历中，保持一个队列，它在任何时刻的最大大小都可以达到二叉树的最大宽度。

**方法 3(使用 Preorder 遍历)**
在这个方法中，我们创建一个大小等于树高的临时数组 count[]。我们将计数中的所有值初始化为 0。我们使用前序遍历遍历树，并以计数填充条目，这样计数数组包含二叉树中每一层的节点计数。

下面是上述想法的实现:

## C++

```
// C++ program to calculate width of binary tree
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
class node {
public:
    int data;
    node* left;
    node* right;
};

// A utility function to get
// height of a binary tree
int height(node* node);

// A utility function to allocate
// a new node with given data
node* newNode(int data);

// A utility function that returns
// maximum value in arr[] of size n
int getMax(int arr[], int n);

// A function that fills count array
// with count of nodes at every
// level of given binary tree
void getMaxWidthRecur(node* root, int count[], int level);

/* Function to get the maximum
width of a binary tree*/
int getMaxWidth(node* root)
{
    int width;
    int h = height(root);

    // Create an array that will
    // store count of nodes at each level
    int* count = new int[h];

    int level = 0;

    // Fill the count array using preorder traversal
    getMaxWidthRecur(root, count, level);

    // Return the maximum value from count array
    return getMax(count, h);
}

// A function that fills count array
// with count of nodes at every
// level of given binary tree
void getMaxWidthRecur(node* root, int count[], int level)
{
    if (root) {
        count[level]++;
        getMaxWidthRecur(root->left, count, level + 1);
        getMaxWidthRecur(root->right, count, level + 1);
    }
}

/* UTILITY FUNCTIONS */
/* Compute the "height" of a tree -- the number of
    nodes along the longest path from the root node
    down to the farthest leaf node.*/
int height(node* node)
{
    if (node == NULL)
        return 0;
    else {
        /* compute the height of each subtree */
        int lHeight = height(node->left);
        int rHeight = height(node->right);
        /* use the larger one */

        return (lHeight > rHeight) ? (lHeight + 1)
                                   : (rHeight + 1);
    }
}

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
node* newNode(int data)
{
    node* Node = new node();
    Node->data = data;
    Node->left = NULL;
    Node->right = NULL;
    return (Node);
}

// Return the maximum value from count array
int getMax(int arr[], int n)
{
    int max = arr[0];
    int i;
    for (i = 0; i < n; i++) {
        if (arr[i] > max)
            max = arr[i];
    }
    return max;
}

/* Driver code*/
int main()
{
    node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(8);
    root->right->right->left = newNode(6);
    root->right->right->right = newNode(7);

    cout << "Maximum width is " << getMaxWidth(root)
         << endl;
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
// C program to calculate width of binary tree
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node {
    int data;
    struct node* left;
    struct node* right;
};

// A utility function to get height of a binary tree
int height(struct node* node);

// A utility function to allocate a new node with given data
struct node* newNode(int data);

// A utility function that returns maximum value in arr[] of
// size n
int getMax(int arr[], int n);

// A function that fills count array with count of nodes at
// every level of given binary tree
void getMaxWidthRecur(struct node* root, int count[],
                      int level);

/* Function to get the maximum width of a binary tree*/
int getMaxWidth(struct node* root)
{
    int width;
    int h = height(root);

    // Create an array that will store count of nodes at
    // each level
    int* count = (int*)calloc(sizeof(int), h);

    int level = 0;

    // Fill the count array using preorder traversal
    getMaxWidthRecur(root, count, level);

    // Return the maximum value from count array
    return getMax(count, h);
}

// A function that fills count array with count of nodes at
// every level of given binary tree
void getMaxWidthRecur(struct node* root, int count[],
                      int level)
{
    if (root) {
        count[level]++;
        getMaxWidthRecur(root->left, count, level + 1);
        getMaxWidthRecur(root->right, count, level + 1);
    }
}

/* UTILITY FUNCTIONS */
/* Compute the "height" of a tree -- the number of
    nodes along the longest path from the root node
    down to the farthest leaf node.*/
int height(struct node* node)
{
    if (node == NULL)
        return 0;
    else {
        /* compute the height of each subtree */
        int lHeight = height(node->left);
        int rHeight = height(node->right);
        /* use the larger one */

        return (lHeight > rHeight) ? (lHeight + 1)
                                   : (rHeight + 1);
    }
}
/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct node* newNode(int data)
{
    struct node* node
        = (struct node*)malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return (node);
}

// Return the maximum value from count array
int getMax(int arr[], int n)
{
    int max = arr[0];
    int i;
    for (i = 0; i < n; i++) {
        if (arr[i] > max)
            max = arr[i];
    }
    return max;
}

/* Driver program to test above functions*/
int main()
{
    struct node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(8);
    root->right->right->left = newNode(6);
    root->right->right->right = newNode(7);

    /*
     Constructed binary tree is:
            1
          /  \
         2    3
       /  \     \
      4   5     8
                /  \
               6   7
    */
    printf("Maximum width is %d \n", getMaxWidth(root));
    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate width of binary tree

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
class Node {
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree {
    Node root;

    /* Function to get the maximum width of a binary tree*/
    int getMaxWidth(Node node)
    {
        int width;
        int h = height(node);

        // Create an array that will store count of nodes at
        // each level
        int count[] = new int[10];

        int level = 0;

        // Fill the count array using preorder traversal
        getMaxWidthRecur(node, count, level);

        // Return the maximum value from count array
        return getMax(count, h);
    }

    // A function that fills count array with count of nodes
    // at every level of given binary tree
    void getMaxWidthRecur(Node node, int count[], int level)
    {
        if (node != null) {
            count[level]++;
            getMaxWidthRecur(node.left, count, level + 1);
            getMaxWidthRecur(node.right, count, level + 1);
        }
    }

    /* UTILITY FUNCTIONS */

    /* Compute the "height" of a tree -- the number of
     nodes along the longest path from the root node
     down to the farthest leaf node.*/
    int height(Node node)
    {
        if (node == null)
            return 0;
        else {
            /* compute the height of each subtree */
            int lHeight = height(node.left);
            int rHeight = height(node.right);

            /* use the larger one */
            return (lHeight > rHeight) ? (lHeight + 1)
                                       : (rHeight + 1);
        }
    }

    // Return the maximum value from count array
    int getMax(int arr[], int n)
    {
        int max = arr[0];
        int i;
        for (i = 0; i < n; i++) {
            if (arr[i] > max)
                max = arr[i];
        }
        return max;
    }

    /* Driver program to test above functions */
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();

        /*
        Constructed binary tree is:
              1
            /  \
           2    3
          / \    \
         4   5    8
                 / \
                6   7 */
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.right = new Node(8);
        tree.root.right.right.left = new Node(6);
        tree.root.right.right.right = new Node(7);

        System.out.println("Maximum width is "
                           + tree.getMaxWidth(tree.root));
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to find the maximum width of
# binary tree using Preorder Traversal.

# A binary tree node

class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to get the maximum width of a binary tree

def getMaxWidth(root):
    h = height(root)
    # Create an array that will store count of nodes at each level
    count = [0] * h

    level = 0
    # Fill the count array using preorder traversal
    getMaxWidthRecur(root, count, level)

    # Return the maximum value from count array
    return getMax(count, h)

# A function that fills count array with count of nodes at every
# level of given binary tree

def getMaxWidthRecur(root, count, level):
    if root is not None:
        count[level] += 1
        getMaxWidthRecur(root.left, count, level+1)
        getMaxWidthRecur(root.right, count, level+1)

# UTILITY FUNCTIONS
# Compute the "height" of a tree -- the number of
# nodes along the longest path from the root node
# down to the farthest leaf node.

def height(node):
    if node is None:
        return 0
    else:
        # compute the height of each subtree
        lHeight = height(node.left)
        rHeight = height(node.right)
        # use the larger one
        return (lHeight+1) if (lHeight > rHeight) else (rHeight+1)

# Return the maximum value from count array

def getMax(count, n):
    max = count[0]
    for i in range(1, n):
        if (count[i] > max):
            max = count[i]
    return max

# Driver program to test above function
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.right = Node(8)
root.right.right.left = Node(6)
root.right.right.right = Node(7)

"""
Constructed binary tree is:
       1
      / \
     2   3
    / \   \
   4   5   8
          / \
         6   7
"""

print "Maximum width is %d" % (getMaxWidth(root))

# This code is contributed by Naveen Aili
```

## C#

```
// C# program to calculate width of binary tree
using System;

/* A binary tree node has data,
pointer to left child and
a pointer to right child */
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
    Node root;

    /* Function to get the maximum
    width of a binary tree*/
    int getMaxWidth(Node node)
    {
        int width;
        int h = height(node);

        // Create an array that will store
        // count of nodes at each level
        int[] count = new int[10];

        int level = 0;

        // Fill the count array using preorder traversal
        getMaxWidthRecur(node, count, level);

        // Return the maximum value from count array
        return getMax(count, h);
    }

    // A function that fills count
    // array with count of nodes at every
    // level of given binary tree
    void getMaxWidthRecur(Node node, int[] count, int level)
    {
        if (node != null)
        {
            count[level]++;
            getMaxWidthRecur(node.left, count, level + 1);
            getMaxWidthRecur(node.right, count, level + 1);
        }
    }

    /* UTILITY FUNCTIONS */

    /* Compute the "height" of a tree -- the number of
    nodes along the longest path from the root node
    down to the farthest leaf node.*/
    int height(Node node)
    {
        if (node == null)
            return 0;
        else
        {
            /* compute the height of each subtree */
            int lHeight = height(node.left);
            int rHeight = height(node.right);

            /* use the larger one */
            return (lHeight > rHeight) ? (lHeight + 1)
                                       : (rHeight + 1);
        }
    }

    // Return the maximum value from count array
    int getMax(int[] arr, int n)
    {
        int max = arr[0];
        int i;
        for (i = 0; i < n; i++)
        {
            if (arr[i] > max)
                max = arr[i];
        }
        return max;
    }

    /* Driver program to test above functions */
    public static void Main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.right = new Node(8);
        tree.root.right.right.left = new Node(6);
        tree.root.right.right.right = new Node(7);

        Console.WriteLine("Maximum width is "
                          + tree.getMaxWidth(tree.root));
    }
}

// This code is contributed Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program to calculate width of binary tree

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
class Node {
    constructor(val) {
        this.data = val;
        this.left = null;
        this.right = null;
    }
}
var root;

    /* Function to get the maximum width of a binary tree*/
    function getMaxWidth(node)
    {
        var width;
        var h = height(node);

        // Create an array that will store count of nodes at
        // each level
        var count = Array(10).fill(0);

        var level = 0;

        // Fill the count array using preorder traversal
        getMaxWidthRecur(node, count, level);

        // Return the maximum value from count array
        return getMax(count, h);
    }

    // A function that fills count array with count of nodes
    // at every level of given binary tree
    function getMaxWidthRecur(node , count , level)
    {
        if (node != null) {
            count[level]++;
            getMaxWidthRecur(node.left, count, level + 1);
            getMaxWidthRecur(node.right, count, level + 1);
        }
    }

    /* UTILITY FUNCTIONS */

    /* Compute the "height" of a tree -- the number of
     nodes avar the longest path from the root node
     down to the farthest leaf node.*/
    function height(node)
    {
        if (node == null)
            return 0;
        else {
            /* compute the height of each subtree */
            var lHeight = height(node.left);
            var rHeight = height(node.right);

            /* use the larger one */
            return (lHeight > rHeight) ? (lHeight + 1)
                                       : (rHeight + 1);
        }
    }

    // Return the maximum value from count array
    function getMax(arr , n)
    {
        var max = arr[0];
        var i;
        for (i = 0; i < n; i++) {
            if (arr[i] > max)
                max = arr[i];
        }
        return max;
    }

    /* Driver program to test above functions */

        /*
        Constructed binary tree is:
              1
            /  \
           2    3
          / \    \
         4   5    8
                 / \
                6   7 */
        root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.right = new Node(8);
        root.right.right.left = new Node(6);
        root.right.right.right = new Node(7);

        document.write("Maximum width is "
                           + getMaxWidth(root));

// This code is contributed by Rajput-Ji
</script>
```

**Output**

```
Maximum width is 3
```

**时间复杂度:** O(n)

？list = plqm 7 alhxfyshcxd 7r 1j0ky 9 ZG _ gbb 1 dbk〖t0〗]

感谢[Raja](https://www.geeksforgeeks.org/archives/7447/comment-page-1#comment-4345)[jagdish](https://www.geeksforgeeks.org/archives/7447/comment-page-1#comment-4098)提出这个方法。
如果发现以上代码/算法不正确，请写评论，或者找到更好的方法解决同样的问题。