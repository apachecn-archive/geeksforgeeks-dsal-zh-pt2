# 删除二叉树中的最后一个叶节点

> 原文:[https://www . geesforgeks . org/delete-二进制树中的最后一个叶节点/](https://www.geeksforgeeks.org/delete-the-last-leaf-node-in-a-binary-tree/)

给定一棵二叉树，任务是找到并**删除**最后一个叶节点。
叶节点是一个没有子节点的节点。最后一个叶节点将是在[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)期间按顺序最后遍历的节点。问题陈述是识别这个最后访问的节点并删除这个特定的节点。
**示例:**

```

Input: 
Given Tree is: 
          6
       /     \
      5       4
    /   \       \
   1     2       5 

Level Order Traversal is: 6 5 4 1 2 5
Output: 
After deleting the last node (5),
the tree would look like as follows. 

          6
       /     \
      5       4
    /   \  
   1     2 
Level Order Traversal is: 6 5 4 1 2

Input: 
Given tree is: 
           1
        /     \
      3        10
    /   \     /   \
   2     15   4     5                        
        /                    
       1    
Level Order Traversal is: 1 3 10 2 15 4 5 1
Output: 
After deleting the last node (1),
the tree would look like as follows.

           1
        /     \
      3        10
    /   \     /   \
   2     15   4     5                        

Level Order Traversal is: 1 3 10 2 15 4 5
```

这个问题与[删除值为 X 的叶节点](https://www.geeksforgeeks.org/delete-leaf-nodes-value-x/)略有不同，在[中，我们马上得到要删除的最后一个叶节点(X)的值，基于这个值，我们执行检查，并将父节点标记为空以将其删除。
这种方法将识别树的最后一层上的最后一个当前叶节点，并将其删除。
**方法 1:** 遍历最后一级节点，跟踪父节点和遍历的节点。
这种方法将遍历每个节点，直到我们到达给定二叉树的最后一级。遍历时，我们跟踪最后遍历的节点及其父节点。
遍历完成后，检查父节点是否有右子节点，如果有，设置为空。如果没有，将左指针设置为空
下面是该方法的实现:](https://www.geeksforgeeks.org/delete-leaf-nodes-value-x/) 

## C++

```
// CPP implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Tree Node
class Node
{
public:
    int data;
    Node *left, *right;

    Node(int data) : data(data) {}
};

// Method to perform inorder traversal
void inorder(Node *root)
{
    if (root == NULL)
        return;

    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

// To keep track of last processed
// nodes parent and node itself.
Node *lastNode, *parentOfLastNode;

// Method to get the height of the tree
int height(Node *root)
{
    if (root == NULL)
        return 0;

    int lheight = height(root->left) + 1;
    int rheight = height(root->right) + 1;

    return max(lheight, rheight);
}

// Method to keep track of parents
// of every node
void getLastNodeAndItsParent(Node *root, int level, Node *parent)
{
    if (root == NULL)
        return;

    // The last processed node in
    // Level Order Traversal has to
    // be the node to be deleted.
    // This will store the last
    // processed node and its parent.
    if (level == 1)
    {
        lastNode = root;
        parentOfLastNode = parent;
    }
    getLastNodeAndItsParent(root->left, level - 1, root);
    getLastNodeAndItsParent(root->right, level - 1, root);
}

// Method to delete last leaf node
void deleteLastNode(Node *root)
{
    int levelOfLastNode = height(root);
    getLastNodeAndItsParent(root, levelOfLastNode, NULL);

    if (lastNode and parentOfLastNode)
    {
        if (parentOfLastNode->right)
            parentOfLastNode->right = NULL;
        else
            parentOfLastNode->left = NULL;
    }
    else
        cout << "Empty Tree\n";
}

// Driver Code
int main()
{
    Node *root = new Node(6);
    root->left = new Node(5);
    root->right = new Node(4);
    root->left->left = new Node(1);
    root->left->right = new Node(2);
    root->right->right = new Node(5);

    cout << "Inorder traversal before deletion of last node :\n";
    inorder(root);

    deleteLastNode(root);

    cout << "\nInorder traversal after deletion of last node :\n";
    inorder(root);

    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of the approach
public class DeleteLastNode {

    // Tree Node
    static class Node {

        Node left, right;
        int data;

        Node(int data)
        {
            this.data = data;
        }
    }

    // Method to perform inorder traversal
    public void inorder(Node root)
    {
        if (root == null)
            return;

        inorder(root.left);
        System.out.print(root.data + " ");
        inorder(root.right);
    }

    // To keep track of last processed
    // nodes parent and node itself.
    public static Node lastNode;
    public static Node parentOfLastNode;

    // Method to get the height of the tree
    public int height(Node root)
    {

        if (root == null)
            return 0;

        int lheight = height(root.left) + 1;
        int rheight = height(root.right) + 1;

        return Math.max(lheight, rheight);
    }

    // Method to delete last leaf node
    public void deleteLastNode(Node root)
    {

        int levelOfLastNode = height(root);

        // Get all nodes at last level
        getLastNodeAndItsParent(root,
                                levelOfLastNode,
                                null);

        if (lastNode != null
            && parentOfLastNode != null) {

            if (parentOfLastNode.right != null)
                parentOfLastNode.right = null;
            else
                parentOfLastNode.left = null;
        }
        else
            System.out.println("Empty Tree");
    }

    // Method to keep track of parents
    // of every node
    public void getLastNodeAndItsParent(Node root,
                                        int level,
                                        Node parent)
    {

        if (root == null)
            return;

        // The last processed node in
        // Level Order Traversal has to
        // be the node to be deleted.
        // This will store the last
        // processed node and its parent.
        if (level == 1) {
            lastNode = root;
            parentOfLastNode = parent;
        }
        getLastNodeAndItsParent(root.left,
                                level - 1,
                                root);
        getLastNodeAndItsParent(root.right,
                                level - 1,
                                root);
    }

    // Driver Code
    public static void main(String[] args)
    {

        Node root = new Node(6);
        root.left = new Node(5);
        root.right = new Node(4);
        root.left.left = new Node(1);
        root.left.right = new Node(2);
        root.right.right = new Node(5);

        DeleteLastNode deleteLastNode = new DeleteLastNode();

        System.out.println("Inorder traversal "
                           + "before deletion "
                           + "of last node : ");

        deleteLastNode.inorder(root);

        deleteLastNode.deleteLastNode(root);

        System.out.println("\nInorder traversal "
                           + "after deletion of "
                           + "last node : ");
        deleteLastNode.inorder(root);
    }
}
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Tree Node
    public class Node
    {
        public Node left, right;
        public int data;

        public Node(int data)
        {
            this.data = data;
        }
    }

    // Method to perform inorder traversal
    public void inorder(Node root)
    {
        if (root == null)
            return;

        inorder(root.left);
        Console.Write(root.data + " ");
        inorder(root.right);
    }

    // To keep track of last processed
    // nodes parent and node itself.
    public static Node lastNode;
    public static Node parentOfLastNode;

    // Method to get the height of the tree
    public int height(Node root)
    {
        if (root == null)
            return 0;

        int lheight = height(root.left) + 1;
        int rheight = height(root.right) + 1;

        return Math.Max(lheight, rheight);
    }

    // Method to delete last leaf node
    public void deleteLastNode(Node root)
    {
        int levelOfLastNode = height(root);

        // Get all nodes at last level
        getLastNodeAndItsParent(root,
                                levelOfLastNode,
                                null);

        if (lastNode != null &&
            parentOfLastNode != null)
        {
            if (parentOfLastNode.right != null)
                parentOfLastNode.right = null;
            else
                parentOfLastNode.left = null;
        }
        else
            Console.WriteLine("Empty Tree");
    }

    // Method to keep track of parents
    // of every node
    public void getLastNodeAndItsParent(Node root,
                                        int level,
                                        Node parent)
    {
        if (root == null)
            return;

        // The last processed node in
        // Level Order Traversal has to
        // be the node to be deleted.
        // This will store the last
        // processed node and its parent.
        if (level == 1)
        {
            lastNode = root;
            parentOfLastNode = parent;
        }
        getLastNodeAndItsParent(root.left,
                                level - 1,
                                root);
        getLastNodeAndItsParent(root.right,
                                level - 1,
                                root);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        Node root = new Node(6);
        root.left = new Node(5);
        root.right = new Node(4);
        root.left.left = new Node(1);
        root.left.right = new Node(2);
        root.right.right = new Node(5);

        GFG deleteLastNode = new GFG();

        Console.WriteLine("Inorder traversal " +
                            "before deletion " +
                             "of last node : ");

        deleteLastNode.inorder(root);

        deleteLastNode.deleteLastNode(root);

        Console.WriteLine("\nInorder traversal " +
                            "after deletion of " +
                                  "last node : ");
        deleteLastNode.inorder(root);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Tree Node
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// Method to perform inorder traversal
function inorder(root)
{
    if (root == null)
        return;
    inorder(root.left);
    document.write(root.data + " ");
    inorder(root.right);
}
// To keep track of last processed
// nodes parent and node itself.
var lastNode = null;
var parentOfLastNode = null;
// Method to get the height of the tree
function height(root)
{
    if (root == null)
        return 0;
    var lheight = height(root.left) + 1;
    var rheight = height(root.right) + 1;
    return Math.max(lheight, rheight);
}

// Method to delete last leaf node
function deleteLastNode(root)
{
    var levelOfLastNode = height(root);
    // Get all nodes at last level
    getLastNodeAndItsParent(root,
                            levelOfLastNode,
                            null);
    if (lastNode != null &&
        parentOfLastNode != null)
    {
        if (parentOfLastNode.right != null)
            parentOfLastNode.right = null;
        else
            parentOfLastNode.left = null;
    }
    else
        Console.WriteLine("Empty Tree");
}
// Method to keep track of parents
// of every node
function getLastNodeAndItsParent(root, level, parent)
{
    if (root == null)
        return;
    // The last processed node in
    // Level Order Traversal has to
    // be the node to be deleted.
    // This will store the last
    // processed node and its parent.
    if (level == 1)
    {
        lastNode = root;
        parentOfLastNode = parent;
    }
    getLastNodeAndItsParent(root.left,
                            level - 1,
                            root);
    getLastNodeAndItsParent(root.right,
                            level - 1,
                            root);
}

// Driver Code
var root = new Node(6);
root.left = new Node(5);
root.right = new Node(4);
root.left.left = new Node(1);
root.left.right = new Node(2);
root.right.right = new Node(5);
document.write("Inorder traversal " +
                    "before deletion " +
                     "of last node :<br>");
inorder(root);
deleteLastNode(root);
document.write("<br>Inorder traversal " +
                    "after deletion of " +
                          "last node :<br>");
inorder(root);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
Inorder traversal before deletion of last node : 
1 5 2 6 4 5 
Inorder traversal after deletion of last node : 
1 5 2 6 4
```