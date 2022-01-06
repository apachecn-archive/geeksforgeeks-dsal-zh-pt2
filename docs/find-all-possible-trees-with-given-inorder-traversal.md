# 用给定的有序遍历找到所有可能的二叉树

> 原文:[https://www . geesforgeks . org/find-all-可能性-trees-with-given-in-order-traversation/](https://www.geeksforgeeks.org/find-all-possible-trees-with-given-inorder-traversal/)

给定一个表示有序遍历的数组，用给定的有序遍历找到所有可能的二叉树，并打印它们的前序遍历。
**例:**

```
Input:   in[] = {3, 2};
Output:  Preorder traversals of different possible Binary Trees are:
         3 2
         2 3
Below are different possible binary trees
    3        2
     \      /
      2    3

Input:   in[] = {4, 5, 7};
Output:  Preorder traversals of different possible Binary Trees are:
          4 5 7 
          4 7 5 
          5 4 7 
          7 4 5 
          7 5 4 
Below are different possible binary trees
  4         4           5         7       7
   \          \       /   \      /       /
    5          7     4     7    4       5
     \        /                  \     /
      7      5                    5   4 
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
让给定的有序遍历成为[] 中的**。在给定的遍历中，【I】**中**的左子树中的所有节点必须出现在它之前，右子树中的所有节点必须出现在它之后。因此，当我们将 in[i]视为根时，从 in[0]到 in[i-1]的所有元素都将在左子树中，而 in[i+1]到 n-1 将在右子树中。如果 in[0]到 in[i-1]可以形成 **x** 不同的树，in[i+1]到 in[n-1]可以从 **y** 不同的树，那么当 in[i]作为根时，我们将拥有 **x*y** 的总树。所以我们简单地从 0 迭代到 n-1 求根。对于[i]中的每个节点，递归地寻找不同的左右子树。如果我们仔细观察，可以注意到计数基本上是[第 n 个加泰罗尼亚数字](https://www.geeksforgeeks.org/program-nth-catalan-number/)。我们已经讨论了寻找第 n 个加泰罗尼亚数字[的不同方法。
想法是维护所有二叉树的根列表。递归构造所有可能的左右子树。为每对左右子树创建一棵树，并将树添加到列表中。下面是详细的算法。](https://www.geeksforgeeks.org/program-nth-catalan-number/)** 

```
1) Initialize list of Binary Trees as empty.  
2) For every element in[i] where i varies from 0 to n-1,
    do following
......a)  Create a new node with key as 'arr[i]', 
          let this node be 'node'
......b)  Recursively construct list of all left subtrees.
......c)  Recursively construct list of all right subtrees.
3) Iterate for all left subtrees
   a) For current leftsubtree, iterate for all right subtrees
        Add current left and right subtrees to 'node' and add
        'node' to list.
```

## C++

```
// C++ program to find binary tree with given inorder
// traversal
#include <bits/stdc++.h>
using namespace std;

// Node structure
struct Node
{
    int key;
    struct Node *left, *right;
};

// A utility function to create a new tree Node
struct Node *newNode(int item)
{
    struct Node *temp = new Node;
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to do preorder traversal of BST
void preorder(Node *root)
{
    if (root != NULL)
    {
        printf("%d ", root->key);
        preorder(root->left);
        preorder(root->right);
    }
}

// Function for constructing all possible trees with
// given inorder traversal stored in an array from
// arr[start] to arr[end]. This function returns a
// vector of trees.
vector<Node *> getTrees(int arr[], int start, int end)
{
    // List to store all possible trees
    vector<Node *> trees;

    /* if start > end then subtree will be empty so
    returning NULL in the list */
    if (start > end)
    {
        trees.push_back(NULL);
        return trees;
    }

    /* Iterating through all values from start to end
        for constructing left and right subtree
        recursively */
    for (int i = start; i <= end; i++)
    {
        /* Constructing left subtree */
        vector<Node *> ltrees = getTrees(arr, start, i-1);

        /* Constructing right subtree */
        vector<Node *> rtrees = getTrees(arr, i+1, end);

        /* Now looping through all left and right subtrees
        and connecting them to ith root below */
        for (int j = 0; j < ltrees.size(); j++)
        {
            for (int k = 0; k < rtrees.size(); k++)
            {
                // Making arr[i] as root
                Node * node = newNode(arr[i]);

                // Connecting left subtree
                node->left = ltrees[j];

                // Connecting right subtree
                node->right = rtrees[k];

                // Adding this tree to list
                trees.push_back(node);
            }
        }
    }
    return trees;
}

// Driver Program to test above functions
int main()
{
    int in[] = {4, 5, 7};
    int n = sizeof(in) / sizeof(in[0]);

    vector<Node *> trees = getTrees(in, 0, n-1);

    cout << "Preorder traversals of different "
         << "possible Binary Trees are \n";
    for (int i = 0; i < trees.size(); i++)
    {
        preorder(trees[i]);
        printf("\n");
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find binary tree with given inorder
// traversal
import java.util.Vector;

/* Class containing left and right child of current
 node and key value*/
class Node {
    int data;
    Node left, right;

    public Node(int item) {
        data = item;
        left = null;
        right = null;
    }
}

/* Class to print Level Order Traversal */
class BinaryTree {

    Node root;

    // A utility function to do preorder traversal of BST
    void preOrder(Node node) {
        if (node != null) {
            System.out.print(node.data + " "    );
            preOrder(node.left);
            preOrder(node.right);
        }
    }

    // Function for constructing all possible trees with
    // given inorder traversal stored in an array from
    // arr[start] to arr[end]. This function returns a
    // vector of trees.
    Vector<Node> getTrees(int arr[], int start, int end) {

        // List to store all possible trees
        Vector<Node> trees= new Vector<Node>();

        /* if start > end then subtree will be empty so
         returning NULL in the list */
        if (start > end) {
            trees.add(null);
            return trees;
        }

        /* Iterating through all values from start to end
         for constructing left and right subtree
         recursively */
        for (int i = start; i <= end; i++) {
            /* Constructing left subtree */
            Vector<Node> ltrees = getTrees(arr, start, i - 1);

            /* Constructing right subtree */
            Vector<Node> rtrees = getTrees(arr, i + 1, end);

            /* Now looping through all left and right subtrees
             and connecting them to ith root below */
            for (int j = 0; j < ltrees.size(); j++) {
                for (int k = 0; k < rtrees.size(); k++) {

                    // Making arr[i] as root
                    Node node = new Node(arr[i]);

                    // Connecting left subtree
                    node.left = ltrees.get(j);

                    // Connecting right subtree
                    node.right = rtrees.get(k);

                    // Adding this tree to list
                    trees.add(node);
                }
            }
        }
        return trees;
    }

    public static void main(String args[]) {
        int in[] = {4, 5, 7};
        int n = in.length;
        BinaryTree tree = new BinaryTree();
        Vector<Node> trees = tree.getTrees(in, 0, n - 1);
        System.out.println("Preorder traversal of different "+
                           " binary trees are:");
        for (int i = 0; i < trees.size(); i++) {
            tree.preOrder(trees.get(i));
            System.out.println("");
        }
    }
}
```

## 计算机编程语言

```
# Python program to find binary tree with given
# inorder traversal

# Node Structure
class Node:

    # Utility to create a new node
    def __init__(self , item):
        self.key = item
        self.left = None
        self.right = None

# A utility function to do preorder traversal of BST
def preorder(root):
    if root is not None:
        print root.key,
        preorder(root.left)
        preorder(root.right)

# Function for constructing all possible trees with
# given inorder traversal stored in an array from
# arr[start] to arr[end]. This function returns a
# vector of trees.
def getTrees(arr , start , end):

    # List to store all possible trees
    trees = []

    """ if start > end then subtree will be empty so
    returning NULL in the list """
    if start > end :
        trees.append(None)
        return trees

    """ Iterating through all values from start to end
        for constructing left and right subtree
        recursively """
    for i in range(start , end+1):

        # Constructing left subtree
        ltrees = getTrees(arr , start , i-1)

        # Constructing right subtree
        rtrees = getTrees(arr , i+1 , end)

        """ Looping through all left and right subtrees
        and connecting to ith root below"""
        for j in ltrees :
            for k in rtrees :

                # Making arr[i]  as root
                node  = Node(arr[i])

                # Connecting left subtree
                node.left = j 

                # Connecting right subtree
                node.right = k

                # Adding this tree to list
                trees.append(node)
    return trees

# Driver program to test above function
inp = [4 , 5, 7]
n = len(inp)

trees = getTrees(inp , 0 , n-1)

print "Preorder traversals of different possible\
 Binary Trees are "
for i in trees :
    preorder(i);
    print ""

# This program is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to find binary tree
// with given inorder traversal
using System;
using System.Collections.Generic;

/* Class containing left and right
   child of current node and key value*/
public class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = null;
        right = null;
    }
}

/* Class to print Level Order Traversal */
class GFG
{
public Node root;

// A utility function to do
// preorder traversal of BST
public virtual void preOrder(Node node)
{
    if (node != null)
    {
        Console.Write(node.data + " ");
        preOrder(node.left);
        preOrder(node.right);
    }
}

// Function for constructing all possible
// trees with given inorder traversal
// stored in an array from arr[start] to
// arr[end]. This function returns a
// vector of trees.
public virtual List<Node> getTrees(int[] arr,
                                   int start,
                                   int end)
{

    // List to store all possible trees
    List<Node> trees = new List<Node>();

    /* if start > end then subtree will be
    empty so returning NULL in the list */
    if (start > end)
    {
        trees.Add(null);
        return trees;
    }

    /* Iterating through all values from
    start to end for constructing left
    and right subtree recursively */
    for (int i = start; i <= end; i++)
    {
        /* Constructing left subtree */
        List<Node> ltrees = getTrees(arr, start, i - 1);

        /* Constructing right subtree */
        List<Node> rtrees = getTrees(arr, i + 1, end);

        /* Now looping through all left and
        right subtrees and connecting them
        to ith root below */
        for (int j = 0; j < ltrees.Count; j++)
        {
            for (int k = 0; k < rtrees.Count; k++)
            {

                // Making arr[i] as root
                Node node = new Node(arr[i]);

                // Connecting left subtree
                node.left = ltrees[j];

                // Connecting right subtree
                node.right = rtrees[k];

                // Adding this tree to list
                trees.Add(node);
            }
        }
    }
    return trees;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = new int[] {4, 5, 7};
    int n = arr.Length;
    GFG tree = new GFG();
    List<Node> trees = tree.getTrees(arr, 0, n - 1);
    Console.WriteLine("Preorder traversal of different " +
                                    " binary trees are:");
    for (int i = 0; i < trees.Count; i++)
    {
        tree.preOrder(trees[i]);
        Console.WriteLine("");
    }
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to find binary tree
// with given inorder traversal

/* Class containing left and right
   child of current node and key value*/
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = null;
        this.right = null;
    }
}

/* Class to print Level Order Traversal */

var root = null;

// A utility function to do
// preorder traversal of BST
function preOrder(node)
{
    if (node != null)
    {
        document.write(node.data + " ");
        preOrder(node.left);
        preOrder(node.right);
    }
}

// Function for constructing all possible
// trees with given inorder traversal
// stored in an array from arr[start] to
// arr[end]. This function returns a
// vector of trees.
function getTrees(arr, start, end)
{

    // List to store all possible trees
    var trees = [];

    /* if start > end then subtree will be
    empty so returning NULL in the list */
    if (start > end)
    {
        trees.push(null);
        return trees;
    }

    /* Iterating through all values from
    start to end for constructing left
    and right subtree recursively */
    for (var i = start; i <= end; i++)
    {
        /* Constructing left subtree */
        var ltrees = getTrees(arr, start, i - 1);

        /* Constructing right subtree */
        var rtrees = getTrees(arr, i + 1, end);

        /* Now looping through all left and
        right subtrees and connecting them
        to ith root below */
        for (var j = 0; j < ltrees.length; j++)
        {
            for (var k = 0; k < rtrees.length; k++)
            {

                // Making arr[i] as root
                var node = new Node(arr[i]);

                // Connecting left subtree
                node.left = ltrees[j];

                // Connecting right subtree
                node.right = rtrees[k];

                // Adding this tree to list
                trees.push(node);
            }
        }
    }
    return trees;
}

// Driver Code
var arr = [4, 5, 7];
var n = arr.length;
var trees = getTrees(arr, 0, n - 1);
document.write("Preorder traversal of different " +
                                " binary trees are:<br>");
for(var i = 0; i < trees.length; i++)
{
    preOrder(trees[i]);
    document.write("<br>");
}

// This code is contributed by rrrtnx.

</script>
```

**输出:**

```
Preorder traversals of different possible Binary Trees are 
4 5 7 
4 7 5 
5 4 7 
7 4 5 
7 5 4
```

感谢乌卡什提出上述解决方案。
这个问题类似于这里讨论的问题。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息