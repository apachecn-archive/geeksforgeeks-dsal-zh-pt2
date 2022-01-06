# 二叉树中节点的级序前置

> 原文:[https://www . geesforgeks . org/level-order-二叉树中节点的前身/](https://www.geeksforgeeks.org/level-order-predecessor-of-a-node-in-binary-tree/)

给定一棵二叉树和二叉树中的一个节点，找到给定节点的 level order preference。也就是说，在树的级别顺序遍历中出现在给定节点之前的节点。
**注**:任务不仅仅是打印节点的数据，你还要从树中返回完整的节点。
T4【示例】T5:

```
Consider the following binary tree
              20            
           /      \         
          10       26       
         /  \     /   \     
       4     18  24    27   
            /  \
           14   19
          /  \
         13  15

Levelorder traversal of given tree is:
20, 10, 26, 4, 18, 24, 27, 14, 19, 13, 15

Input : 19
Output : 14

Input : 4
Output : 26
```

**接近** :

1.  检查根是否为空，即树是否为空。如果为真，则返回空值。
2.  检查给定的节点是否是根节点。如果为真，则没有根的前身，因此返回空。
3.  否则，使用队列和临时指针 **prev** 在树上执行级别顺序遍历，以在遍历期间保持最后一个节点。
4.  在级别顺序遍历的每一步，检查当前节点是否与给定节点匹配。
5.  如果为真，停止进一步遍历，返回存储在指针 **prev** 中的节点，因为它是在遍历期间当前节点之前访问的节点。

以下是上述方法的实现:

## C++

```
// CPP program to find Levelorder
// Predecessor of given node in the
// Binary Tree

#include <bits/stdc++.h>
using namespace std;

// Tree Node
struct Node {
    struct Node *left, *right;
    int value;
};

// Utility function to create a
// new node with given value
struct Node* newNode(int value)
{
    Node* temp = new Node;
    temp->left = temp->right = NULL;
    temp->value = value;

    return temp;
}

// Function to find the Level Order Predecessor
// of a given Node in Binary Tree
Node* levelOrderPredecessor(Node* root, Node* key)
{
    // Base Case
    if (root == NULL)
        return NULL;

    // If root equals to key
    if (root == key) {

        // There is no Predecessor of
        // root node
        return NULL;
    }

    // Create an empty queue for level
    // order traversal
    queue<Node*> q;

    // Enqueue Root
    q.push(root);

    // Temporary node to keep track of the
    // last node
    Node* prev = NULL;

    while (!q.empty()) {
        Node* nd = q.front();
        q.pop();

        if (nd == key)
            break;
        else
            prev = nd;

        if (nd->left != NULL) {
            q.push(nd->left);
        }

        if (nd->right != NULL) {
            q.push(nd->right);
        }
    }

    return prev;
}

// Driver code
int main()
{
    struct Node* root = newNode(20);
    root->left = newNode(10);
    root->left->left = newNode(4);
    root->left->right = newNode(18);
    root->right = newNode(26);
    root->right->left = newNode(24);
    root->right->right = newNode(27);
    root->left->right->left = newNode(14);
    root->left->right->left->left = newNode(13);
    root->left->right->left->right = newNode(15);
    root->left->right->right = newNode(19);

    struct Node* key = root->left->right->right;

    struct Node* res = levelOrderPredecessor(root, key);

    if (res)
        cout << "LevelOrder Predecessor of " << key->value
             << " is " << res->value;
    else
        cout << "LevelOrder Predecessor of " << key->value
             << " is "
             << "NULL";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Levelorder
// Predecessor of given node in the
// Binary Tree
import java.util.*;
class GfG {

// Tree Node
static class Node {
    Node left, right;
    int value;
}

// Utility function to create a
// new node with given value
static Node newNode(int value)
{
    Node temp = new Node();
    temp.left = null;
    temp.right = null;
    temp.value = value;

    return temp;
}

// Function to find the Level Order Predecessor
// of a given Node in Binary Tree
static Node levelOrderPredecessor(Node root, Node key)
{
    // Base Case
    if (root == null)
        return null;

    // If root equals to key
    if (root == key) {

        // There is no Predecessor of
        // root node
        return null;
    }

    // Create an empty queue for level
    // order traversal
    Queue<Node> q = new LinkedList<Node> ();

    // Enqueue Root
    q.add(root);

    // Temporary node to keep track of the
    // last node
    Node prev = null;

    while (!q.isEmpty()) {
        Node nd = q.peek();
        q.remove();

        if (nd == key)
            break;
        else
            prev = nd;

        if (nd.left != null) {
            q.add(nd.left);
        }

        if (nd.right != null) {
            q.add(nd.right);
        }
    }

    return prev;
}

// Driver code
public static void main(String[] args)
{
    Node root = newNode(20);
    root.left = newNode(10);
    root.left.left = newNode(4);
    root.left.right = newNode(18);
    root.right = newNode(26);
    root.right.left = newNode(24);
    root.right.right = newNode(27);
    root.left.right.left = newNode(14);
    root.left.right.left.left = newNode(13);
    root.left.right.left.right = newNode(15);
    root.left.right.right = newNode(19);

    Node key = root.left.right.right;

    Node res = levelOrderPredecessor(root, key);

    if (res != null)
        System.out.println("LevelOrder Predecessor of " + key.value + " is " + res.value);
    else
        System.out.println("LevelOrder Predecessor of " + key.value+ " is null");

}
}
```

## 蟒蛇 3

```
"""Python3 program to find Level order
Predecessor of given node in the
Binary Tree"""

# A Binary Tree Node
# Utility function to create a
# new tree node
class newNode:

    # Constructor to create a newNode
    def __init__(self, data):
        self.value = data
        self.left = None
        self.right = self.parent = None

# Function to find the Level Order Predecessor
# of a given Node in Binary Tree
def levelOrderPredecessor(root, key) :

    # Base Case
    if (root == None) :
        return None

    # If root equals to key
    if (root == key):

        # There is no Predecessor of
        # root node
        return None

    # Create an empty queue for level
    # order traversal
    q = []

    # Enqueue Root
    q.append(root)

    # Temporary node to keep track
    # of the last node
    prev = None

    while (len(q)):
        nd = q[0]
        q.pop(0)

        if (nd == key) :
            break
        else:
            prev = nd

        if (nd.left != None):
            q.append(nd.left)

        if (nd.right != None):
            q.append(nd.right)
    return prev

# Driver Code
if __name__ == '__main__':

    root = newNode(20)
    root.left = newNode(10)
    root.left.left = newNode(4)
    root.left.right = newNode(18)
    root.right = newNode(26)
    root.right.left = newNode(24)
    root.right.right = newNode(27)
    root.left.right.left = newNode(14)
    root.left.right.left.left = newNode(13)
    root.left.right.left.right = newNode(15)
    root.left.right.right = newNode(19)

    key = root.left.right.right

    res = levelOrderPredecessor(root, key)

    if (res) :
        print("LevelOrder Predecessor of",
               key.value, "is", res.value)
    else:
        print("LevelOrder Predecessor of",
                  key.value, "is", "None")

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
// C# program to find Levelorder
// Predecessor of given node in the
// Binary Tree
using System;
using System.Collections.Generic;

class GfG
{

    // Tree Node
    class Node
    {
        public Node left, right;
        public int value;
    }

    // Utility function to create a
    // new node with given value
    static Node newNode(int value)
    {
        Node temp = new Node();
        temp.left = null;
        temp.right = null;
        temp.value = value;

        return temp;
    }

    // Function to find the Level Order Predecessor
    // of a given Node in Binary Tree
    static Node levelOrderPredecessor(Node root, Node key)
    {
        // Base Case
        if (root == null)
            return null;

        // If root equals to key
        if (root == key)
        {

            // There is no Predecessor of
            // root node
            return null;
        }

        // Create an empty queue for level
        // order traversal
        Queue<Node> q = new Queue<Node> ();

        // Enqueue Root
        q.Enqueue(root);

        // Temporary node to keep track of the
        // last node
        Node prev = null;

        while (q.Count!=0)
        {
            Node nd = q.Peek();
            q.Dequeue();

            if (nd == key)
                break;
            else
                prev = nd;

            if (nd.left != null)
            {
                q.Enqueue(nd.left);
            }

            if (nd.right != null)
            {
                q.Enqueue(nd.right);
            }
        }

        return prev;
    }

    // Driver code
    public static void Main(String[] args)
    {
        Node root = newNode(20);
        root.left = newNode(10);
        root.left.left = newNode(4);
        root.left.right = newNode(18);
        root.right = newNode(26);
        root.right.left = newNode(24);
        root.right.right = newNode(27);
        root.left.right.left = newNode(14);
        root.left.right.left.left = newNode(13);
        root.left.right.left.right = newNode(15);
        root.left.right.right = newNode(19);

        Node key = root.left.right.right;

        Node res = levelOrderPredecessor(root, key);

        if (res != null)
            Console.WriteLine("LevelOrder Predecessor of " +
                                key.value + " is " + res.value);
        else
            Console.WriteLine("LevelOrder Predecessor of " +
                                key.value+ " is null");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

    // JavaScript program to find Levelorder
    // Predecessor of given node in the
    // Binary Tree 

    // Tree Node
    class Node
    {
        constructor(value) {
           this.left = null;
           this.right = null;
           this.value = value;
        }
    }

    // Utility function to create a
    // new node with given value
    function newNode(value)
    {
        let temp = new Node(value);
        return temp;
    }

    // Function to find the Level Order Predecessor
    // of a given Node in Binary Tree
    function levelOrderPredecessor(root, key)
    {
        // Base Case
        if (root == null)
            return null;

        // If root equals to key
        if (root == key) {

            // There is no Predecessor of
            // root node
            return null;
        }

        // Create an empty queue for level
        // order traversal
        let q = [];

        // Enqueue Root
        q.push(root);

        // Temporary node to keep track of the
        // last node
        let prev = null;

        while (q.length > 0) {
            let nd = q[0];
            q.shift();

            if (nd == key)
                break;
            else
                prev = nd;

            if (nd.left != null) {
                q.push(nd.left);
            }

            if (nd.right != null) {
                q.push(nd.right);
            }
        }

        return prev;
    }

    let root = newNode(20);
    root.left = newNode(10);
    root.left.left = newNode(4);
    root.left.right = newNode(18);
    root.right = newNode(26);
    root.right.left = newNode(24);
    root.right.right = newNode(27);
    root.left.right.left = newNode(14);
    root.left.right.left.left = newNode(13);
    root.left.right.left.right = newNode(15);
    root.left.right.right = newNode(19);

    let key = root.left.right.right;

    let res = levelOrderPredecessor(root, key);

    if (res != null)
        document.write("LevelOrder Predecessor of " +
        key.value + " is " + res.value);
    else
        document.write("LevelOrder Predecessor of " +
        key.value+ " is null");

</script>
```

**Output:** 

```
LevelOrder Predecessor of 19 is 14
```