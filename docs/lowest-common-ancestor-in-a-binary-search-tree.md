# 二叉查找树的最低共同祖先。

> 原文:[https://www . geesforgeks . org/二进制搜索树中最低共同祖先/](https://www.geeksforgeeks.org/lowest-common-ancestor-in-a-binary-search-tree/)

给定二叉查找树中两个值 n1 和 n2 的值，找到最下面的**L****C**ommon**A**ncestor(LCA)。您可以假设这两个值都存在于树中。

**示例:**

```
Tree: 
```

![](img/84da68a965d0c736f63b82d5c549c244.png)

```
Input: LCA of 10 and 14
Output:  12
Explanation: 12 is the closest node to both 10 and 14 
which is a ancestor of both the nodes.

Input: LCA of 8 and 14
Output:  8
Explanation: 8 is the closest node to both 8 and 14 
which is a ancestor of both the nodes.

Input: LCA of 10 and 22
Output:  20
Explanation: 20 is the closest node to both 10 and 22 
which is a ancestor of both the nodes.
```

**以下是** **对 LCA 的定义来自** [**维基百科**](http://en.wikipedia.org/wiki/Lowest_common_ancestor) **:**

> 让 T 成为一棵扎根的树。两个节点 n1 和 n2 之间的最低公共祖先被定义为 T 中同时具有 n1 和 n2 作为后代的最低节点(这里我们允许一个节点是其自身的后代)。
> T 中 n1 和 n2 的 LCA 是距离根最远的 n1 和 n2 的共享祖先。最低共同祖先的计算可能是有用的，例如，作为确定树中节点对之间距离的过程的一部分:从 n1 到 n2 的距离可以计算为从根到 n1 的距离加上从根到 n2 的距离，减去从根到它们最低共同祖先的距离的两倍。(来源[维基](http://en.wikipedia.org/wiki/Lowest_common_ancestor)

**方法:**对于二叉查找树，当从上到下遍历树时，位于两个数字 n1 和 n2 之间的第一个节点是节点的 LCA，即深度最低的第一个节点 n 位于 n1 和 n2 之间(n1 < =n < =n2) n1 < n2。所以递归遍历 BST，如果节点的值大于 n1 和 n2，那么 LCA 位于节点的左侧，如果它小于 n1 和 n2，那么 LCA 位于右侧。否则，根是 LCA(假设 n1 和 n2 都存在于 BST 中)。

**算法:**

1.  创建一个递归函数，该函数接受一个节点和两个值 n1 和 n2。
2.  如果当前节点的值小于 n1 和 n2，则 LCA 位于右子树中。调用右子树的递归函数。
3.  如果当前节点的值大于 n1 和 n2，则 LCA 位于左子树中。调用左子树的递归函数。
4.  如果以上两种情况都为假，则返回当前节点作为生命周期评价。

**实施:**

## C++

```
// A recursive CPP program to find
// LCA of two nodes n1 and n2.
#include <bits/stdc++.h>
using namespace std;

class node
{
    public:
    int data;
    node* left, *right;
};

/* Function to find LCA of n1 and n2.
The function assumes that both
n1 and n2 are present in BST */
node *lca(node* root, int n1, int n2)
{
    if (root == NULL) return NULL;

    // If both n1 and n2 are smaller
    // than root, then LCA lies in left
    if (root->data > n1 && root->data > n2)
        return lca(root->left, n1, n2);

    // If both n1 and n2 are greater than
    // root, then LCA lies in right
    if (root->data < n1 && root->data < n2)
        return lca(root->right, n1, n2);

    return root;
}

/* Helper function that allocates
a new node with the given data.*/
node* newNode(int data)
{
    node* Node = new node();
    Node->data = data;
    Node->left = Node->right = NULL;
    return(Node);
}

/* Driver code*/
int main()
{
    // Let us construct the BST
    // shown in the above figure
    node *root = newNode(20);
    root->left = newNode(8);
    root->right = newNode(22);
    root->left->left = newNode(4);
    root->left->right = newNode(12);
    root->left->right->left = newNode(10);
    root->left->right->right = newNode(14);

    int n1 = 10, n2 = 14;
    node *t = lca(root, n1, n2);
    cout << "LCA of " << n1 << " and " << n2 << " is " << t->data<<endl;

    n1 = 14, n2 = 8;
    t = lca(root, n1, n2);
    cout<<"LCA of " << n1 << " and " << n2 << " is " << t->data << endl;

    n1 = 10, n2 = 22;
    t = lca(root, n1, n2);
    cout << "LCA of " << n1 << " and " << n2 << " is " << t->data << endl;
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// A recursive C program to find LCA of two nodes n1 and n2.
#include <stdio.h>
#include <stdlib.h>

struct node
{
    int data;
    struct node* left, *right;
};

/* Function to find LCA of n1 and n2\. The function assumes that both
   n1 and n2 are present in BST */
struct node *lca(struct node* root, int n1, int n2)
{
    if (root == NULL) return NULL;

    // If both n1 and n2 are smaller than root, then LCA lies in left
    if (root->data > n1 && root->data > n2)
        return lca(root->left, n1, n2);

    // If both n1 and n2 are greater than root, then LCA lies in right
    if (root->data < n1 && root->data < n2)
        return lca(root->right, n1, n2);

    return root;
}

/* Helper function that allocates a new node with the given data.*/
struct node* newNode(int data)
{
    struct node* node = (struct node*)malloc(sizeof(struct node));
    node->data  = data;
    node->left  = node->right = NULL;
    return(node);
}

/* Driver program to test lca() */
int main()
{
    // Let us construct the BST shown in the above figure
    struct node *root        = newNode(20);
    root->left               = newNode(8);
    root->right              = newNode(22);
    root->left->left         = newNode(4);
    root->left->right        = newNode(12);
    root->left->right->left  = newNode(10);
    root->left->right->right = newNode(14);

    int n1 = 10, n2 = 14;
    struct node *t = lca(root, n1, n2);
    printf("LCA of %d and %d is %d \n", n1, n2, t->data);

    n1 = 14, n2 = 8;
    t = lca(root, n1, n2);
    printf("LCA of %d and %d is %d \n", n1, n2, t->data);

    n1 = 10, n2 = 22;
    t = lca(root, n1, n2);
    printf("LCA of %d and %d is %d \n", n1, n2, t->data);

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to print lca of two nodes

// A binary tree node
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    /* Function to find LCA of n1 and n2\. The function assumes that both
       n1 and n2 are present in BST */
    Node lca(Node node, int n1, int n2)
    {
        if (node == null)
            return null;

        // If both n1 and n2 are smaller than root, then LCA lies in left
        if (node.data > n1 && node.data > n2)
            return lca(node.left, n1, n2);

        // If both n1 and n2 are greater than root, then LCA lies in right
        if (node.data < n1 && node.data < n2)
            return lca(node.right, n1, n2);

        return node;
    }

    /* Driver program to test lca() */
    public static void main(String args[])
    {
        // Let us construct the BST shown in the above figure
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(20);
        tree.root.left = new Node(8);
        tree.root.right = new Node(22);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(12);
        tree.root.left.right.left = new Node(10);
        tree.root.left.right.right = new Node(14);

        int n1 = 10, n2 = 14;
        Node t = tree.lca(tree.root, n1, n2);
        System.out.println("LCA of " + n1 + " and " + n2 + " is " + t.data);

        n1 = 14;
        n2 = 8;
        t = tree.lca(tree.root, n1, n2);
        System.out.println("LCA of " + n1 + " and " + n2 + " is " + t.data);

        n1 = 10;
        n2 = 22;
        t = tree.lca(tree.root, n1, n2);
        System.out.println("LCA of " + n1 + " and " + n2 + " is " + t.data);

    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# A recursive python program to find LCA of two nodes
# n1 and n2

# A Binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to find LCA of n1 and n2\. The function assumes
# that both n1 and n2 are present in BST
def lca(root, n1, n2):

    # Base Case
    if root is None:
        return None

    # If both n1 and n2 are smaller than root, then LCA
    # lies in left
    if(root.data > n1 and root.data > n2):
        return lca(root.left, n1, n2)

    # If both n1 and n2 are greater than root, then LCA
    # lies in right
    if(root.data < n1 and root.data < n2):
        return lca(root.right, n1, n2)

    return root

# Driver program to test above function

# Let us construct the BST shown in the figure
root = Node(20)
root.left = Node(8)
root.right = Node(22)
root.left.left = Node(4)
root.left.right = Node(12)
root.left.right.left = Node(10)
root.left.right.right = Node(14)

n1 = 10 ; n2 = 14
t = lca(root, n1, n2)
print "LCA of %d and %d is %d" %(n1, n2, t.data)

n1 = 14 ; n2 = 8
t = lca(root, n1, n2)
print "LCA of %d and %d is %d" %(n1, n2 , t.data)

n1 = 10 ; n2 = 22
t = lca(root, n1, n2)
print "LCA of %d and %d is %d" %(n1, n2, t.data)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;

// Recursive C#  program to print lca of two nodes

// A binary tree node
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

    /* Function to find LCA of n1 and n2\. The function assumes that both
       n1 and n2 are present in BST */
    public virtual Node lca(Node node, int n1, int n2)
    {
        if (node == null)
        {
            return null;
        }

        // If both n1 and n2 are smaller than root, then LCA lies in left
        if (node.data > n1 && node.data > n2)
        {
            return lca(node.left, n1, n2);
        }

        // If both n1 and n2 are greater than root, then LCA lies in right
        if (node.data < n1 && node.data < n2)
        {
            return lca(node.right, n1, n2);
        }

        return node;
    }

    /* Driver program to test lca() */
    public static void Main(string[] args)
    {
        // Let us construct the BST shown in the above figure
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(20);
        tree.root.left = new Node(8);
        tree.root.right = new Node(22);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(12);
        tree.root.left.right.left = new Node(10);
        tree.root.left.right.right = new Node(14);

        int n1 = 10, n2 = 14;
        Node t = tree.lca(tree.root, n1, n2);
        Console.WriteLine("LCA of " + n1 + " and " + n2 + " is " + t.data);

        n1 = 14;
        n2 = 8;
        t = tree.lca(tree.root, n1, n2);
        Console.WriteLine("LCA of " + n1 + " and " + n2 + " is " + t.data);

        n1 = 10;
        n2 = 22;
        t = tree.lca(tree.root, n1, n2);
        Console.WriteLine("LCA of " + n1 + " and " + n2 + " is " + t.data);

    }
}

  //  This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Recursive JavaScript program to print lca of two nodes

// A binary tree node
class Node
{
    constructor(item)
    {
        this.data=item;
        this.left=this.right=null;
    }
}

let root;

function lca(node,n1,n2)
{
    if (node == null)
            return null;

        // If both n1 and n2 are smaller than root,
        // then LCA lies in left
        if (node.data > n1 && node.data > n2)
            return lca(node.left, n1, n2);

        // If both n1 and n2 are greater than root,
        // then LCA lies in right
        if (node.data < n1 && node.data < n2)
            return lca(node.right, n1, n2);

        return node;
}

/* Driver program to test lca() */
 // Let us construct the BST shown in the above figure
root = new Node(20);
root.left = new Node(8);
root.right = new Node(22);
root.left.left = new Node(4);
root.left.right = new Node(12);
root.left.right.left = new Node(10);
root.left.right.right = new Node(14);

let n1 = 10, n2 = 14;
let t = lca(root, n1, n2);
document.write("LCA of " + n1 + " and " + n2 + " is " +
t.data+"<br>");

n1 = 14;
n2 = 8;
t = lca(root, n1, n2);
document.write("LCA of " + n1 + " and " + n2 + " is " +
t.data+"<br>");

n1 = 10;
n2 = 22;
t = lca(root, n1, n2);
document.write("LCA of " + n1 + " and " + n2 + " is " +
t.data+"<br>");

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
LCA of 10 and 14 is 12 
LCA of 14 and 8 is 8 
LCA of 10 and 22 is 20 
```

**复杂度分析:**

*   **时间复杂度:** O(h)。
    上述解的时间复杂度为 O(h)，其中 h 为树的高度。
*   **空间复杂度:** O(h)。
    如果忽略递归栈空间，上述解的空间复杂度不变。

**迭代实现:**上面的解决方案使用了递归。递归解决方案需要函数调用堆栈形式的额外空间。因此可以实现一个迭代的解决方案，它不占用函数调用栈形式的空间。

**实施:**

## C++

```
// A recursive CPP program to find
// LCA of two nodes n1 and n2.
#include <bits/stdc++.h>
using namespace std;

class node
{
    public:
    int data;
    node* left, *right;
};

/* Function to find LCA of n1 and n2.
The function assumes that both n1 and n2
are present in BST */
node *lca(node* root, int n1, int n2)
{
    while (root != NULL)
    {
        // If both n1 and n2 are smaller than root,
        // then LCA lies in left
        if (root->data > n1 && root->data > n2)
        root = root->left;

        // If both n1 and n2 are greater than root,
        // then LCA lies in right
        else if (root->data < n1 && root->data < n2)
        root = root->right;

        else break;
    }
    return root;
}

/* Helper function that allocates
a new node with the given data.*/
node* newNode(int data)
{
    node* Node = new node();
    Node->data = data;
    Node->left = Node->right = NULL;
    return(Node);
}

/* Driver code*/
int main()
{
    // Let us construct the BST
    // shown in the above figure
    node *root = newNode(20);
    root->left = newNode(8);
    root->right = newNode(22);
    root->left->left = newNode(4);
    root->left->right = newNode(12);
    root->left->right->left = newNode(10);
    root->left->right->right = newNode(14);

    int n1 = 10, n2 = 14;
    node *t = lca(root, n1, n2);
    cout << "LCA of " << n1 << " and " << n2 << " is " << t->data<<endl;

    n1 = 14, n2 = 8;
    t = lca(root, n1, n2);
    cout<<"LCA of " << n1 << " and " << n2 << " is " << t->data << endl;

    n1 = 10, n2 = 22;
    t = lca(root, n1, n2);
    cout << "LCA of " << n1 << " and " << n2 << " is " << t->data << endl;
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// A recursive C program to find LCA of two nodes n1 and n2.
#include <stdio.h>
#include <stdlib.h>

struct node
{
    int data;
    struct node* left, *right;
};

/* Function to find LCA of n1 and n2\. The function assumes that both
n1 and n2 are present in BST */
struct node *lca(struct node* root, int n1, int n2)
{
    while (root != NULL)
    {
        // If both n1 and n2 are smaller than root, then LCA lies in left
        if (root->data > n1 && root->data > n2)
        root = root->left;

        // If both n1 and n2 are greater than root, then LCA lies in right
        else if (root->data < n1 && root->data < n2)
        root = root->right;

        else break;
    }
    return root;
}

/* Helper function that allocates a new node with the given data.*/
struct node* newNode(int data)
{
    struct node* node = (struct node*)malloc(sizeof(struct node));
    node->data = data;
    node->left = node->right = NULL;
    return(node);
}

/* Driver program to test lca() */
int main()
{
    // Let us construct the BST shown in the above figure
    struct node *root     = newNode(20);
    root->left             = newNode(8);
    root->right             = newNode(22);
    root->left->left         = newNode(4);
    root->left->right     = newNode(12);
    root->left->right->left = newNode(10);
    root->left->right->right = newNode(14);

    int n1 = 10, n2 = 14;
    struct node *t = lca(root, n1, n2);
    printf("LCA of %d and %d is %d \n", n1, n2, t->data);

    n1 = 14, n2 = 8;
    t = lca(root, n1, n2);
    printf("LCA of %d and %d is %d \n", n1, n2, t->data);

    n1 = 10, n2 = 22;
    t = lca(root, n1, n2);
    printf("LCA of %d and %d is %d \n", n1, n2, t->data);

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to print lca of two nodes

// A binary tree node
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

/* Function to find LCA of n1 and n2.
The function assumes that both
n1 and n2 are present in BST */
static Node lca(Node root, int n1, int n2)
{
    while (root != null)
    {
        // If both n1 and n2 are smaller
        // than root, then LCA lies in left
        if (root.data > n1 &&
            root.data > n2)
        root = root.left;

        // If both n1 and n2 are greater
        // than root, then LCA lies in right
        else if (root.data < n1 &&
                 root.data < n2)
        root = root.right;

        else break;
    }
    return root;
}

    /* Driver program to test lca() */
    public static void main(String args[])
    {
        // Let us construct the BST shown in the above figure
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(20);
        tree.root.left = new Node(8);
        tree.root.right = new Node(22);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(12);
        tree.root.left.right.left = new Node(10);
        tree.root.left.right.right = new Node(14);

        int n1 = 10, n2 = 14;
        Node t = tree.lca(tree.root, n1, n2);
        System.out.println("LCA of " + n1 + " and " + n2 + " is " + t.data);

        n1 = 14;
        n2 = 8;
        t = tree.lca(tree.root, n1, n2);
        System.out.println("LCA of " + n1 + " and " + n2 + " is " + t.data);

        n1 = 10;
        n2 = 22;
        t = tree.lca(tree.root, n1, n2);
        System.out.println("LCA of " + n1 + " and " + n2 + " is " + t.data);

    }
}
// This code is contributed by SHUBHAMSINGH10
```

## 计算机编程语言

```
# A recursive python program to find LCA of two nodes
# n1 and n2

# A Binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to find LCA of n1 and n2.
# The function assumes that both
#   n1 and n2 are present in BST
def lca(root, n1, n2):
    while root:
        # If both n1 and n2 are smaller than root,
        # then LCA lies in left
        if root.data > n1 and root.data > n2:
            root = root.left

        # If both n1 and n2 are greater than root,
        # then LCA lies in right
        elif root.data < n1 and root.data < n2:
            root = root.right

        else:
            break

    return root

# Driver program to test above function
# Let us construct the BST shown in the figure
root = Node(20)
root.left = Node(8)
root.right = Node(22)
root.left.left = Node(4)
root.left.right = Node(12)
root.left.right.left = Node(10)
root.left.right.right = Node(14)

n1 = 10 ; n2 = 14
t = lca(root, n1, n2)
print "LCA of %d and %d is %d" %(n1, n2, t.data)

n1 = 14 ; n2 = 8
t = lca(root, n1, n2)
print "LCA of %d and %d is %d" %(n1, n2 , t.data)

n1 = 10 ; n2 = 22
t = lca(root, n1, n2)
print "LCA of %d and %d is %d" %(n1, n2, t.data)
# This Code is Contributed by Sumit Bhardwaj (Timus)
```

## C#

```
using System;

// Recursive C# program to print lca of two nodes

// A binary tree node
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

/* Function to find LCA of n1 and n2.
The function assumes that both
n1 and n2 are present in BST */
public virtual Node lca(Node root, int n1, int n2)
{
    while (root != null)
    {
        // If both n1 and n2 are smaller than
        // root, then LCA lies in left
        if (root.data > n1 && root.data > n2)
        root = root.left;

        // If both n1 and n2 are greater than
        // root, then LCA lies in right
        else if (root.data < n1 && root.data < n2)
        root = root.right;

        else break;
    }
    return root;
}

    /* Driver program to test lca() */
    public static void Main(string[] args)
    {
        // Let us construct the BST shown in the above figure
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(20);
        tree.root.left = new Node(8);
        tree.root.right = new Node(22);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(12);
        tree.root.left.right.left = new Node(10);
        tree.root.left.right.right = new Node(14);

        int n1 = 10, n2 = 14;
        Node t = tree.lca(tree.root, n1, n2);
        Console.WriteLine(
            "LCA of " + n1 + " and " + n2
            + " is " + t.data);

        n1 = 14;
        n2 = 8;
        t = tree.lca(tree.root, n1, n2);
        Console.WriteLine(
            "LCA of " + n1 + " and " + n2
            + " is " + t.data);

        n1 = 10;
        n2 = 22;
        t = tree.lca(tree.root, n1, n2);
        Console.WriteLine(
            "LCA of " + n1 + " and " + n2
            + " is " + t.data);
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Recursive Javascript program to
// print lca of two nodes

// A binary tree node
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = null;
        this.right = null;
    }
}

var root = null;

/* Function to find LCA of n1 and n2.
The function assumes that both
n1 and n2 are present in BST */
function lca(root, n1, n2)
{
    while (root != null)
    {

        // If both n1 and n2 are smaller than
        // root, then LCA lies in left
        if (root.data > n1 && root.data > n2)
            root = root.left;

        // If both n1 and n2 are greater than
        // root, then LCA lies in right
        else if (root.data < n1 && root.data < n2)
            root = root.right;

        else break;
    }
    return root;
}

// Driver code

// Let us construct the BST shown
// in the above figure
root = new Node(20);
root.left = new Node(8);
root.right = new Node(22);
root.left.left = new Node(4);
root.left.right = new Node(12);
root.left.right.left = new Node(10);
root.left.right.right = new Node(14);

var n1 = 10, n2 = 14;
var t = lca(root, n1, n2);
document.write("LCA of " + n1 + " and " + n2 +
               " is " + t.data + "<br>");

n1 = 14;
n2 = 8;
t = lca(root, n1, n2);
document.write("LCA of " + n1 + " and " + n2 +
               " is " + t.data+ "<br>");

n1 = 10;
n2 = 22;
t = lca(root, n1, n2);
document.write("LCA of " + n1 + " and " + n2 +
               " is " + t.data+ "<br>");

// This code is contributed by rrrtnx

</script>
```

**Output**

```
LCA of 10 and 14 is 12 
LCA of 14 and 8 is 8 
LCA of 10 and 22 is 20 
```

**复杂度分析:**

*   **时间复杂度:** O(h)。
    上述解的时间复杂度为 O(h)，其中 h 为树的高度。
*   **空间复杂度:** O(1)。
    上述解的空间复杂度是不变的。

https://www.youtube.com/watch?v=zlTsz

-apm4U

你可能也想看下面的文章:

[二叉树中最低的共同祖先](https://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/)

[使用父指针的生命周期评价](https://www.geeksforgeeks.org/lowest-common-ancestor-in-a-binary-tree-set-2-using-parent-pointer/)

[使用 RMQ 在二叉树中找到生命周期评价](https://www.geeksforgeeks.org/find-lca-in-binary-tree-using-rmq/)

**练习**
以上函数假设 n1 和 n2 都在 BST 中。如果 n1 和 n2 不存在，则它们可能返回不正确的结果。如果 BST 中不存在 n1 或 n2 或两者，扩展上述解决方案以返回空值。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。