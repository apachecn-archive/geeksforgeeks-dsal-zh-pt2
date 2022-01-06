# 二叉树中最深的右叶节点|迭代方法

> 原文:[https://www . geesforgeks . org/最深-右-叶-节点-二叉树-迭代-方法/](https://www.geeksforgeeks.org/deepest-right-leaf-node-binary-tree-iterative-approach/)

给定一棵二叉树，找到最深的叶子节点，它是它的父节点的右子节点。例如，考虑下面的树。最深的右叶节点是值为 10 的节点。
**例:**

```
Input : 
       1
     /   \
    2     3
     \   /  \  
      4 5    6
         \    \
          7    8
         /      \
        9        10

Output : 10
```

这个想法类似于[层次顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)
的方法 2，逐层遍历树，同时将右子节点推到队列中，检查是否是叶节点，如果是叶节点，则更新结果，由于我们是逐层遍历，最后存储的右叶将是最深的右叶节点。

## C++

```
// CPP program to find deepest right leaf
// node of binary tree
#include <bits/stdc++.h>
using namespace std;

// tree node
struct Node {
    int data;
    Node *left, *right;
};

// returns a new tree Node
Node* newNode(int data)
{
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// return the deepest right leaf node
// of binary tree
Node* getDeepestRightLeafNode(Node* root)
{
    if (!root)
        return NULL;

    // create a queue for level order traversal
    queue<Node*> q;
    q.push(root);

    Node* result = NULL;

    // traverse until the queue is empty
    while (!q.empty()) {
        Node* temp = q.front();
        q.pop();

        if (temp->left) {
            q.push(temp->left);
        }

        // Since we go level by level, the last
        // stored right leaf node is deepest one
        if (temp->right){
            q.push(temp->right);
            if (!temp->right->left && !temp->right->right)
                result = temp->right;
        }
    }
    return result;
}

// driver program
int main()
{
    // construct a tree
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->right = newNode(4);
    root->right->left = newNode(5);
    root->right->right = newNode(6);
    root->right->left->right = newNode(7);
    root->right->right->right = newNode(8);
    root->right->left->right->left = newNode(9);
    root->right->right->right->right = newNode(10);

    Node* result = getDeepestRightLeafNode(root);
    if (result)
        cout << "Deepest Right Leaf Node :: "
             << result->data << endl;
    else
        cout << "No result, right leaf not found\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find deepest right leaf
// node of binary tree
import java.util.*;

class GFG
{

// tree node
static class Node
{
    int data;
    Node left, right;
};

// returns a new tree Node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// return the deepest right leaf node
// of binary tree
static Node getDeepestRightLeafNode(Node root)
{
    if (root == null)
        return null;

    // create a queue for level order traversal
    Queue<Node> q = new LinkedList<>();
    q.add(root);

    Node result = null;

    // traverse until the queue is empty
    while (!q.isEmpty())
    {
        Node temp = q.peek();
        q.poll();

        if (temp.left != null)
        {
            q.add(temp.left);
        }

        // Since we go level by level, the last
        // stored right leaf node is deepest one
        if (temp.right != null)
        {
            q.add(temp.right);
            if (temp.right.left == null && temp.right.right == null)
                result = temp.right;
        }
    }
    return result;
}

// Driver code
public static void main(String[] args)
{

    // construct a tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.right = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(6);
    root.right.left.right = newNode(7);
    root.right.right.right = newNode(8);
    root.right.left.right.left = newNode(9);
    root.right.right.right.right = newNode(10);

    Node result = getDeepestRightLeafNode(root);
    if (result != null)
        System.out.println("Deepest Right Leaf Node :: "
            + result.data);
    else
        System.out.println("No result, right leaf not found\n");
    }
}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to find closest
# value in Binary search Tree

_MIN = -2147483648
_MAX = 2147483648

# Helper function that allocates a new
# node with the given data and None 
# left and right poers.                                    
class newnode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# utility function to return level
# of given node
def getDeepestRightLeafNode(root) :

    if (not root):
        return None

    # create a queue for level
    # order traversal
    q = []
    q.append(root)

    result = None

    # traverse until the queue is empty
    while (len(q)):
        temp = q[0]
        q.pop(0)

        if (temp.left):
            q.append(temp.left)

        # Since we go level by level, the last
        # stored right leaf node is deepest one
        if (temp.right):
            q.append(temp.right)
            if (not temp.right.left and
                not temp.right.right):
                result = temp.right

    return result

# Driver Code
if __name__ == '__main__':

    # create a binary tree
    root = newnode(1)
    root.left = newnode(2)
    root.right = newnode(3)
    root.left.right = newnode(4)
    root.right.left = newnode(5)
    root.right.right = newnode(6)
    root.right.left.right = newnode(7)
    root.right.right.right = newnode(8)
    root.right.left.right.left = newnode(9)
    root.right.right.right.right = newnode(10)

    result = getDeepestRightLeafNode(root)
    if result:
        print("Deepest Right Leaf Node ::",
                               result.data)
    else:
        print("No result, right leaf not found")

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to find deepest right leaf
// node of binary tree
using System;
using System.Collections.Generic;

class GFG
{

// tree node
public class Node
{
    public int data;
    public Node left, right;
};

// returns a new tree Node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// return the deepest right leaf node
// of binary tree
static Node getDeepestRightLeafNode(Node root)
{
    if (root == null)
        return null;

    // Create a queue for level order traversal
    Queue<Node> q = new Queue<Node>();
    q.Enqueue(root);

    Node result = null;

    // Traverse until the queue is empty
    while (q.Count!=0)
    {
        Node temp = q.Peek();
        q.Dequeue();

        if (temp.left != null)
        {
            q.Enqueue(temp.left);
        }

        // Since we go level by level, the last
        // stored right leaf node is deepest one
        if (temp.right != null)
        {
            q.Enqueue(temp.right);
            if (temp.right.left == null && temp.right.right == null)
                result = temp.right;
        }
    }
    return result;
}

// Driver code
public static void Main(String[] args)
{

    // construct a tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.right = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(6);
    root.right.left.right = newNode(7);
    root.right.right.right = newNode(8);
    root.right.left.right.left = newNode(9);
    root.right.right.right.right = newNode(10);

    Node result = getDeepestRightLeafNode(root);
    if (result != null)
        Console.WriteLine("Deepest Right Leaf Node :: "
            + result.data);
    else
        Console.WriteLine("No result, right leaf not found\n");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

    // JavaScript program to find deepest right leaf
    // node of binary tree

    /* A binary tree node has data, pointer to
    left child and a pointer to right child */
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // returns a new tree Node
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    // return the deepest right leaf node
    // of binary tree
    function getDeepestRightLeafNode(root)
    {
        if (root == null)
            return null;

        // create a queue for level order traversal
        let q = [];
        q.push(root);

        let result = null;

        // traverse until the queue is empty
        while (q.length > 0)
        {
            let temp = q[0];
            q.shift();

            if (temp.left != null)
            {
                q.push(temp.left);
            }

            // Since we go level by level, the last
            // stored right leaf node is deepest one
            if (temp.right != null)
            {
                q.push(temp.right);
                if (temp.right.left == null &&
                    temp.right.right == null)
                    result = temp.right;
            }
        }
        return result;
    }

    // construct a tree
    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.right = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(6);
    root.right.left.right = newNode(7);
    root.right.right.right = newNode(8);
    root.right.left.right.left = newNode(9);
    root.right.right.right.right = newNode(10);

    let result = getDeepestRightLeafNode(root);
    if (result != null)
        document.write("Deepest Right Leaf Node :: "
            + result.data);
    else
        document.write("No result, right leaf not found");

</script>
```

**输出:**

```
Deepest Right Leaf Node :: 10
```

**时间复杂度:** O(n)

**–**[**曼德普·辛格**](https://github.com/msdeep14)