# 删除值为 k 的叶节点

> 原文:[https://www . geesforgeks . org/delete-leaf-nodes-with-value-k/](https://www.geeksforgeeks.org/delete-leaf-nodes-with-value-k/)

给定一棵二叉树，k 值，删除所有 k 值的叶子节点，如果一个节点删除后变成叶子，那么如果它有 k 值就应该被删除
示例:

```
Input :     4
         /     \
        5       5
       /  \    /
      3    1  5 

Output :    4
         /     
        5       
       /  \    
      3    1  
```

1.使用 PostOrder 遍历。
2。当我们遇到叶节点时，我们检查它是否是叶节点。
3。如果是叶节点且值等于 k，则删除它。
4。否则，为其他节点递归。

## C++

```
// C++ program to delete leaf nodes with
// value equal to k.
#include<bits/stdc++.h>
using namespace std;

struct Node
{
    int data;
    struct Node *left, *right;
};

struct Node* newNode(int data)
{
    struct Node* newNode = new Node;
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return (newNode);
}

// Function to delete leaf Node with value
// equal to k
Node* LeafNodesWithValueK(Node* root, int k)
{
    if (root == NULL)
        return nullptr;

    root->left = LeafNodesWithValueK(root->left, k);
    root->right = LeafNodesWithValueK(root->right, k);

    // If the node is leaf, and its
        // value is equal to k

    if (root->data == k &&
        root->left == NULL &&
        root->right == NULL)
    {
        return nullptr;
    }
    return root;
}

void postOrder(Node* root)
{
    if (root == NULL)
        return;

    cout << root->data << " ";

    postOrder(root->left);
    postOrder(root->right);
}

// Driver code
int main()
{
    struct Node* root = newNode(4);
    root->left = newNode(5);
    root->right = newNode(5);
    root->left->left = newNode(3);
    root->left->right = newNode(1);
    root->right->right = newNode(5);

    cout << "Nodes in postorder before deletion \n";
    postOrder(root);
    cout << "\n";

    int k = 5;
    LeafNodesWithValueK(root, k);
    cout << "Nodes in post order after " 
            "required deletion \n";
    postOrder(root);
    return 0;
}

// This code is contributed by Stream_Cipher
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to delete leaf nodes with
// value equal to k.

class Node {
    int data;
    Node left;
    Node right;

    public Node(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

public class LeafNodesWithValueK {

    // Function to delete leaf Node with value
    // equal to k
    static Node delLeafValueK(Node root, int k)
    {
        if (root == null)
            return null;

        root.left = delLeafValueK(root.left, k);
        root.right = delLeafValueK(root.right, k);

        // If the node is leaf, and its
        // value is equal to k
        if ((root.left == null &&
             root.right == null) &&
             root.data == k)
            return null;

        return root;
    }

    static void postOrder(Node root)
    {
       if (root == null)
          return;
       System.out.print(root.data + " ");
       postOrder(root.left);
       postOrder(root.right);
    }

    // Driver Code
    public static void main(String[] args)
    {
        Node root = new Node(4);
        root.left = new Node(5);
        root.right = new Node(5);
        root.left.left = new Node(3);
        root.left.right = new Node(1);
        root.right.left = new Node(5);

        System.out.println("Nodes in postorder before deletion");
        postOrder(root);
        System.out.println();
        System.out.println("Nodes in post order after required deletion");
        int k = 5;
        delLeafValueK(root, k);
        postOrder(root);
        System.out.println();
    }
}
```

## C#

```
// C# program to delete leaf nodes with
// value equal to k.
using System;

public class Node
{
    public int data;
    public Node left;
    public Node right;

    public Node(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

public class LeafNodesWithValueK
{

    // Function to delete leaf Node with value
    // equal to k
    static Node delLeafValueK(Node root, int k)
    {
        if (root == null)
            return null;

        root.left = delLeafValueK(root.left, k);
        root.right = delLeafValueK(root.right, k);

        // If the node is leaf, and its
        // value is equal to k
        if ((root.left == null &&
            root.right == null) &&
            root.data == k)
            return null;

        return root;
    }

    static void postOrder(Node root)
    {
        if (root == null)
            return;
        Console.Write(root.data + " ");
        postOrder(root.left);
        postOrder(root.right);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        Node root = new Node(4);
        root.left = new Node(5);
        root.right = new Node(5);
        root.left.left = new Node(3);
        root.left.right = new Node(1);
        root.right.left = new Node(5);

        Console.WriteLine("Nodes in postorder before deletion");
        postOrder(root);
        Console.WriteLine();
        Console.WriteLine("Nodes in post order after required deletion");
        int k = 5;
        delLeafValueK(root, k);
        postOrder(root);
        Console.WriteLine();
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to delete leaf nodes with
// value equal to k.

class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }

}

// Function to delete leaf Node with value
// equal to k
function delLeafValueK(root, k)
{
    if (root == null)
        return null;
    root.left = delLeafValueK(root.left, k);
    root.right = delLeafValueK(root.right, k);
    // If the node is leaf, and its
    // value is equal to k
    if ((root.left == null &&
        root.right == null) &&
        root.data == k)
        return null;
    return root;
}
function postOrder(root)
{
    if (root == null)
        return;
    document.write(root.data + " ");
    postOrder(root.left);
    postOrder(root.right);
}

// Driver Code
var root = new Node(4);
root.left = new Node(5);
root.right = new Node(5);
root.left.left = new Node(3);
root.left.right = new Node(1);
root.right.left = new Node(5);
document.write("Nodes in postorder before deletion<br>");
postOrder(root);
document.write("<br>");
document.write("Nodes in post order after required deletion<br>");
var k = 5;
delLeafValueK(root, k);
postOrder(root);
document.write("<br>");

</script>
```

**Output:** 

```
Nodes in postorder before deletion
4 5 3 1 5 5 
Nodes in post order after required deletion
4 5 3 1
```