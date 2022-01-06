# 双树

> 原文:[https://www.geeksforgeeks.org/double-tree/](https://www.geeksforgeeks.org/double-tree/)

编写一个程序，将给定的树转换成它的双树。要创建给定树的双树，请为每个节点创建一个新的副本，并将该副本作为原始节点的左子节点插入。
所以树…

```
    2
   / \
  1   3
```

已更改为…

```
       2
      / \
     2   3
    /   /
   1   3
  /
 1
```

还有那棵树

```
            1
          /   \
        2      3
      /  \
    4     5
```

已更改为

```
               1
             /   \
           1      3
          /      /
        2       3
      /  \
     2    5
    /    /
   4   5
  /   
 4    
```

**算法:**
以后置的方式递归地将树转换为双树。对于每个节点，先转换节点的左子树，再转换右子树，最后创建节点的重复节点，并固定节点的左子和左子的左子。
实施:

## C++

```
// C++ program to convert binary tree to double tree
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
class node
{
    public:
    int data;
    node* left;
    node* right;
};

/* function to create a new
node of tree and returns pointer */
node* newNode(int data);

/* Function to convert a tree to double tree */
void doubleTree(node* Node)
{
    node* oldLeft;

    if (Node == NULL) return;

    /* do the subtrees */
    doubleTree(Node->left);
    doubleTree(Node->right);

    /* duplicate this node to its left */
    oldLeft = Node->left;
    Node->left = newNode(Node->data);
    Node->left->left = oldLeft;
}

/* UTILITY FUNCTIONS TO TEST doubleTree() FUNCTION */
/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
node* newNode(int data)
{
    node* Node = new node();
    Node->data = data;
    Node->left = NULL;
    Node->right = NULL;

    return(Node);
}

/* Given a binary tree, print its nodes in inorder*/
void printInorder(node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    cout << node->data << " ";
    printInorder(node->right);
}

/* Driver code*/
int main()
{

    /* Constructed binary tree is
                1
            / \
            2 3
        / \
        4 5
    */
    node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);

    cout << "Inorder traversal of the original tree is \n";
    printInorder(root);

    doubleTree(root);

    cout << "\nInorder traversal of the double tree is \n";
    printInorder(root);

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node
{
    int data;
    struct node* left;
    struct node* right;
};

/* function to create a new node of tree and returns pointer */
struct node* newNode(int data);

/* Function to convert a tree to double tree */
void doubleTree(struct node* node)
{
  struct node* oldLeft;

  if (node==NULL) return;

  /* do the subtrees */
  doubleTree(node->left);
  doubleTree(node->right);

  /* duplicate this node to its left */
  oldLeft = node->left;
  node->left = newNode(node->data);
  node->left->left = oldLeft;
}

/* UTILITY FUNCTIONS TO TEST doubleTree() FUNCTION */
 /* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct node* newNode(int data)
{
  struct node* node = (struct node*)
                       malloc(sizeof(struct node));
  node->data = data;
  node->left = NULL;
  node->right = NULL;

  return(node);
}

/* Given a binary tree, print its nodes in inorder*/
void printInorder(struct node* node)
{
  if (node == NULL)
    return;
  printInorder(node->left);
  printf("%d ", node->data);
  printInorder(node->right);
}

/* Driver program to test above functions*/
int main()
{

  /* Constructed binary tree is
            1
          /   \
        2      3
      /  \
    4     5
  */
  struct node *root = newNode(1);
  root->left        = newNode(2);
  root->right       = newNode(3);
  root->left->left  = newNode(4);
  root->left->right = newNode(5);

  printf("Inorder traversal of the original tree is \n");
  printInorder(root);

  doubleTree(root);

  printf("\n Inorder traversal of the double tree is \n"); 
  printInorder(root);

  getchar();
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert binary tree to double tree

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
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

    /* Function to convert a tree to double tree */
    void doubleTree(Node node)
    {
        Node oldleft;

        if (node == null)
            return;

        /* do the subtrees */
        doubleTree(node.left);
        doubleTree(node.right);

        /* duplicate this node to its left */
        oldleft = node.left;
        node.left = new Node(node.data);
        node.left.left = oldleft;
    }

    /* Given a binary tree, print its nodes in inorder*/
    void printInorder(Node node)
    {
        if (node == null)
            return;
        printInorder(node.left);
        System.out.print(node.data + " ");
        printInorder(node.right);
    }

    /* Driver program to test the above functions */
    public static void main(String args[])
    {
        /* Constructed binary tree is
              1
            /   \
           2     3
         /  \
        4    5
        */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);

        System.out.println("Original tree is : ");
        tree.printInorder(tree.root);
        tree.doubleTree(tree.root);
        System.out.println("");
        System.out.println("Inorder traversal of double tree is : ");
        tree.printInorder(tree.root);
    }
}

// This code has been contributed by Mayank Jaiswal(mayank_24)
```

## C#

```
// C# program to convert binary tree
// to double tree

/* A binary tree node has data,
pointer to left child and
a pointer to right child */
using System;

class Node
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

    /* Function to convert a tree to double tree */
    void doubleTree(Node node)
    {
        Node oldleft;

        if (node == null)
            return;

        /* do the subtrees */
        doubleTree(node.left);
        doubleTree(node.right);

        /* duplicate this node to its left */
        oldleft = node.left;
        node.left = new Node(node.data);
        node.left.left = oldleft;
    }

    /* Given a binary tree, print its nodes in inorder*/
    void printInorder(Node node)
    {
        if (node == null)
            return;
        printInorder(node.left);
        Console.Write(node.data + " ");
        printInorder(node.right);
    }

    // Driver Code
    public static void Main(String []args)
    {
        /* Constructed binary tree is
            1
            / \
        2     3
        / \
        4 5
        */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);

        Console.WriteLine("Original tree is : ");
        tree.printInorder(tree.root);
        tree.doubleTree(tree.root);
        Console.WriteLine("");
        Console.WriteLine("Inorder traversal of " +
                              "double tree is : ");
        tree.printInorder(tree.root);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to convert binary tree to var tree

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

    /* Function to convert a tree to var tree */
    function doubleTree(node)
    {
        var oldleft;

        if (node == null)
            return;

        /* do the subtrees */
        doubleTree(node.left);
        doubleTree(node.right);

        /* duplicate this node to its left */
        oldleft = node.left;
        node.left = new Node(node.data);
        node.left.left = oldleft;
    }

    /* Given a binary tree, print its nodes in inorder*/
    function printInorder(node)
    {
        if (node == null)
            return;
        printInorder(node.left);
        document.write(node.data + " ");
        printInorder(node.right);
    }

    /* Driver program to test the above functions */

        /* Constructed binary tree is
              1
            /   \
           2     3
         /  \
        4    5
        */
        root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);

        document.write("Original tree is :<br/> ");
        printInorder(root);
        doubleTree(root);
        document.write("<br/>");
        document.write("Inorder traversal of double tree is : <br/>");
        printInorder(root);

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
Original tree is : 
4 2 5 1 3 
Inorder traversal of double tree is : 
4 4 2 2 5 5 1 1 3 3 
```

**时间复杂度:** O(n)，其中 n 是树中的节点数。

参考文献:
[【http://cslibrary.stanford.edu/110/BinaryTrees.html】](http://cslibrary.stanford.edu/110/BinaryTrees.html)
如发现以上代码/算法有 bug，请写评论，或寻找其他方法解决同样问题。