# 二叉树中节点的级序后继

> 原文:[https://www . geesforgeks . org/level-order-二叉树中节点的后继者/](https://www.geeksforgeeks.org/level-order-successor-of-a-node-in-binary-tree/)

给定一棵二叉树和二叉树中的一个节点，找到给定节点的 Levelorder 后继节点。也就是说，在树的级别顺序遍历中出现在给定节点之后的节点。

**注意**:任务不仅仅是打印节点的数据，你还要从树中返回完整的节点。

**示例**:

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

Input : 24
Output : 27

Input : 4
Output : 18 
```

**接近**:

1.  检查根是否为空，即树是否为空。如果为真，则返回空值。
2.  检查给定的节点是否是根节点。如果为真:
    *   检查根的左子项是否存在，如果为真则返回根的左子项。
    *   否则，检查是否有合适的孩子，返回。
    *   如果根是唯一的节点。返回空值。
3.  否则，使用队列对树执行级别顺序遍历。
4.  在级别顺序遍历的每一步，检查当前节点是否与给定节点匹配。
5.  如果为真，则停止进一步遍历，并返回队列顶部的元素，这将是级别顺序遍历中的下一个节点。

下面是上述方法的实现:

## C++

```
// CPP program to find Levelorder
// successor of given node in the
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

// Function to find the Level Order Successor
// of a given Node in Binary Tree
Node* levelOrderSuccessor(Node* root, Node* key)
{
    // Base Case
    if (root == NULL)
        return NULL;

    // If root equals to key
    if (root == key) {

        // If left child exists it will be
        // the Postorder Successor
        if (root->left)
            return root->left;

        // Else if right child exists it will be
        // the Postorder Successor
        else if (root->right)
            return root->right;
        else
            return NULL; // No Successor
    }

    // Create an empty queue for level
    // order traversal
    queue<Node*> q;

    // Enqueue Root
    q.push(root);

    while (!q.empty()) {
        Node* nd = q.front();
        q.pop();

        if (nd->left != NULL) {
            q.push(nd->left);
        }

        if (nd->right != NULL) {
            q.push(nd->right);
        }

        if (nd == key)
            break;
    }

    return q.front();
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

    struct Node* key = root->right->left; // node 24

    struct Node* res = levelOrderSuccessor(root, key);

    if (res)
        cout << "LevelOrder successor of "
             << key->value << " is " << res->value;
    else
        cout << "LevelOrder successor of "
             << key->value << " is "  << "NULL";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Levelorder
// successor of given node in the
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

// Function to find the Level Order Successor
// of a given Node in Binary Tree
static Node levelOrderSuccessor(Node root, Node key)
{
    // Base Case
    if (root == null)
        return null;

    // If root equals to key
    if (root == key) {

        // If left child exists it will be
        // the Postorder Successor
        if (root.left != null)
            return root.left;

        // Else if right child exists it will be
        // the Postorder Successor
        else if (root.right != null)
            return root.right;
        else
            return null; // No Successor
    }

    // Create an empty queue for level
    // order traversal
    Queue<Node> q = new LinkedList<Node> ();

    // Enqueue Root
    q.add(root);

    while (!q.isEmpty()) {
        Node nd = q.peek();
        q.remove();

        if (nd.left != null) {
            q.add(nd.left);
        }

        if (nd.right != null) {
            q.add(nd.right);
        }

        if (nd == key)
            break;
    }

    return q.peek();
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

    Node key = root.right.left; // node 24

Node res = levelOrderSuccessor(root, key);

    if (res != null)
        System.out.println("LevelOrder successor of "
                        +key.value + " is " + res.value);
    else
        System.out.println("LevelOrder successor of "
                            +key.value + " is NULL");

}
}
```

## 蟒蛇 3

```
# Python3 program to find Level
# order successor of given node
# in the Binary Tree

# Node definition
class Node:

    def __init__(self, value):
        self.left = None
        self.right = None
        self.value = value

# Function to find the Level
# Order Successor of a given
# Node in Binary Tree
def levelOrderSuccessor(root, key):

    # Base Case
    if root == None:
        return None

    # If root equals to key
    elif root == key:

        # If left child exists, it will
        # be the PostOrder Successor
        if root.left:
            return root.left

        # Else if right child exists, it
        # will be the PostOrder Successor
        elif root.right:
            return root.right

        # No Successor
        else:
            return None

    # Create an empty queue for
    # level order traversal
    q = []

    # Enqueue Root
    q.append(root)

    while len(q) != 0:
        nd = q.pop(0)

        if nd.left != None:
            q.append(nd.left)

        if nd.right != None:
            q.append(nd.right)

        if nd == key:
            break

    return q[0]

# Driver Code
if __name__ == "__main__":

    root = Node(20)
    root.left = Node(10)
    root.left.left = Node(4)
    root.left.right = Node(18)
    root.right = Node(26)
    root.right.left = Node(24)
    root.right.right = Node(27)
    root.left.right.left = Node(14)
    root.left.right.left.left = Node(13)
    root.left.right.left.right = Node(15)
    root.left.right.right = Node(19)

    key = root.right.left # node 24

    res = levelOrderSuccessor(root, key)

    if res:
        print("LevelOrder successor of " +
                 str(key.value) + " is " +
                 str(res.value))

    else:
        print("LevelOrder successor of " +
              str(key.value) + " is NULL")

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to find Levelorder
// successor of given node in the
// Binary Tree
using System;
using System.Collections.Generic;

class GfG
{

// Tree Node
public class Node
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

// Function to find the Level Order Successor
// of a given Node in Binary Tree
static Node levelOrderSuccessor(Node root, Node key)
{
    // Base Case
    if (root == null)
        return null;

    // If root equals to key
    if (root == key)
    {

        // If left child exists it will be
        // the Postorder Successor
        if (root.left != null)
            return root.left;

        // Else if right child exists it will be
        // the Postorder Successor
        else if (root.right != null)
            return root.right;
        else
            return null; // No Successor
    }

    // Create an empty queue for level
    // order traversal
    LinkedList<Node> q = new LinkedList<Node> ();

    // Enqueue Root
    q.AddLast(root);

    while (q.Count != 0)
    {
        Node nd = q.First.Value;
        q.RemoveFirst();

        if (nd.left != null)
        {
            q.AddLast(nd.left);
        }

        if (nd.right != null)
        {
            q.AddLast(nd.right);
        }

        if (nd == key)
            break;
    }

    return q.First.Value;
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

    Node key = root.right.left; // node 24

    Node res = levelOrderSuccessor(root, key);

    if (res != null)
        Console.WriteLine("LevelOrder successor of "
                        +key.value + " is " + res.value);
    else
        Console.WriteLine("LevelOrder successor of "
                            +key.value + " is NULL");

}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program to find Levelorder
    // successor of given node in the
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

    // Function to find the Level Order Successor
    // of a given Node in Binary Tree
    function levelOrderSuccessor(root, key)
    {
        // Base Case
        if (root == null)
            return null;

        // If root equals to key
        if (root == key) {

            // If left child exists it will be
            // the Postorder Successor
            if (root.left != null)
                return root.left;

            // Else if right child exists it will be
            // the Postorder Successor
            else if (root.right != null)
                return root.right;
            else
                return null; // No Successor
        }

        // Create an empty queue for level
        // order traversal
        let q = [];

        // Enqueue Root
        q.push(root);

        while (q.length > 0) {
            let nd = q[0];
            q.shift();

            if (nd.left != null) {
                q.push(nd.left);
            }

            if (nd.right != null) {
                q.push(nd.right);
            }

            if (nd == key)
                break;
        }

        return q[0];
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

    let key = root.right.left; // node 24

    let res = levelOrderSuccessor(root, key);

    if (res != null)
      document.write("LevelOrder successor of "
                         +key.value + " is " + res.value);
    else
      document.write("LevelOrder successor of "
                         +key.value + " is NULL");

</script>
```

**Output:** 

```
LevelOrder successor of 24 is 27
```