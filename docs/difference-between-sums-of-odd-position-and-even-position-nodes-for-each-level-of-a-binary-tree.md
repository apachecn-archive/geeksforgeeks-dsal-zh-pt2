# 二叉树每一级的奇数位置和偶数位置节点的和之差

> 原文:[https://www . geeksforgeeks . org/二叉树每级奇数位置和偶数位置节点之和之差/](https://www.geeksforgeeks.org/difference-between-sums-of-odd-position-and-even-position-nodes-for-each-level-of-a-binary-tree/)

给定一棵二叉树，任务是找到奇数和偶数定位节点的和之间的绝对差。如果节点在当前级别中的位置分别为奇数和偶数，则称其为奇数和偶数位置。**注意**每行的第一个元素被认为是奇数位置。
**例:**

```
Input:
      5
    /   \
   2     6
 /  \     \  
1    4     8
    /     / \ 
   3     7   9
Output: 11
Level     oddPositionNodeSum  evenPositionNodeSum
0             5                  0
1             2                  6
2             9                  4
3             12                 7
Difference = |(5 + 2 + 9 + 12) - (0 + 6 + 4 + 7)| = |28 - 17| = 11

Input:
      5
    /   \
   2     3
Output: 4
```

**方法:**逐级寻找偶数和奇数位置的节点之和，使用[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。逐级遍历树时，将每行的第一个元素的标记**标记为真，并将它切换到同一行的下一个元素。如果 **oddPosition** 标志为真，则将节点数据添加到 **oddPositionNodeSum** 中，否则将节点数据添加到 **evenPositionNodeSum** 中。完成树遍历后，在树遍历结束时找到它们的差值的绝对值。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node *left, *right;
};

// Iterative method to perform level
// order traversal line by line
int nodeSumDiff(Node* root)
{

    // Base Case
    if (root == NULL)
        return 0;

    int evenPositionNodeSum = 0;
    int oddPositionNodeSum = 0;

    // Create an empty queue for level
    // order traversal
    queue<Node*> q;

    // Enqueue root element
    q.push(root);

    while (1) {

        // nodeCount (queue size) indicates
        // number of nodes in the current level
        int nodeCount = q.size();
        if (nodeCount == 0)
            break;

        // Mark 1st node as even positioned
        bool oddPosition = true;

        // Dequeue all the nodes of current level
        // and Enqueue all the nodes of next level
        while (nodeCount > 0) {
            Node* node = q.front();

            // Depending upon node position
            // add value to their respective sum
            if (oddPosition)
                oddPositionNodeSum += node->data;
            else
                evenPositionNodeSum += node->data;

            q.pop();
            if (node->left != NULL)
                q.push(node->left);
            if (node->right != NULL)
                q.push(node->right);
            nodeCount--;

            // Switch the even position flag
            oddPosition = !oddPosition;
        }
    }

    // Return the absolute difference
    return abs(oddPositionNodeSum - evenPositionNodeSum);
}

// Utility method to create a node
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
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->left->right->left = newNode(8);
    root->left->right->right = newNode(9);
    root->left->right->right->right = newNode(10);

    cout << nodeSumDiff(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    static class Node
    {
        int data;
        Node left, right;
    };

    // Iterative method to perform level
    // order traversal line by line
    static int nodeSumDiff(Node root)
    {

        // Base Case
        if (root == null)
            return 0;

        int evenPositionNodeSum = 0;
        int oddPositionNodeSum = 0;

        // Create an empty queue for level
        // order traversal
        Queue<Node> q = new LinkedList<>();

        // Enqueue root element
        q.add(root);

        while (1 == 1)
        {

            // nodeCount (queue size) indicates
            // number of nodes in the current level
            int nodeCount = q.size();
            if (nodeCount == 0)
                break;

            // Mark 1st node as even positioned
            boolean oddPosition = true;

            // Dequeue all the nodes of current level
            // and Enqueue all the nodes of next level
            while (nodeCount > 0)
            {
                Node node = q.peek();

                // Depending upon node position
                // add value to their respective sum
                if (oddPosition)
                    oddPositionNodeSum += node.data;
                else
                    evenPositionNodeSum += node.data;

                q.remove();
                if (node.left != null)
                    q.add(node.left);
                if (node.right != null)
                    q.add(node.right);
                nodeCount--;

                // Switch the even position flag
                oddPosition = !oddPosition;
            }
        }

        // Return the absolute difference
        return Math.abs(oddPositionNodeSum - evenPositionNodeSum);
    }

    // Utility method to create a node
    static Node newNode(int data)
    {
        Node node = new Node();
        node.data = data;
        node.left = node.right = null;
        return (node);
    }

    // Driver code
    public static void main(String[] args)
    {
        Node root = newNode(1);
        root.left = newNode(2);
        root.right = newNode(3);
        root.left.left = newNode(4);
        root.left.right = newNode(5);
        root.right.left = newNode(6);
        root.right.right = newNode(7);
        root.left.right.left = newNode(8);
        root.left.right.right = newNode(9);
        root.left.right.right.right = newNode(10);

        System.out.print(nodeSumDiff(root));

    }
}

// This code is contributed by PrinciRaj1992
```

## 计算机编程语言

```
# Python implementation of the approach

# Node of a linked list
class Node:
    def __init__(self, data = None,
                left = None, right = None):
        self.left = left
        self.right = right
        self.data = data

# Iterative method to perform level
# order traversal line by line
def nodeSumDiff( root):

    # Base Case
    if (root == None):
        return 0

    evenPositionNodeSum = 0
    oddPositionNodeSum = 0

    # Create an empty queue for level
    # order traversal
    q = []

    # Enqueue root element
    q.append(root)

    while (True):

        # nodeCount (queue size) indicates
        # number of nodes in the current level
        nodeCount = len(q)
        if (nodeCount == 0):
            break

        # Mark 1st node as even positioned
        oddPosition = True

        # Dequeue all the nodes of current level
        # and Enqueue all the nodes of next level
        while (nodeCount > 0):
            node = q[0]

            # Depending upon node position
            # add value to their respective sum
            if (oddPosition):
                oddPositionNodeSum += node.data
            else:
                evenPositionNodeSum += node.data

            q.pop(0)
            if (node.left != None):
                q.append(node.left)
            if (node.right != None):
                q.append(node.right)
            nodeCount = nodeCount - 1

            # Switch the even position flag
            oddPosition = not oddPosition

    # Return the absolute difference
    return abs(oddPositionNodeSum - evenPositionNodeSum)

# Utility method to create a node
def newNode(data):
    node = Node()
    node.data = data
    node.left = node.right = None
    return (node)

# Driver code
root = newNode(1)
root.left = newNode(2)
root.right = newNode(3)
root.left.left = newNode(4)
root.left.right = newNode(5)
root.right.left = newNode(6)
root.right.right = newNode(7)
root.left.right.left = newNode(8)
root.left.right.right = newNode(9)
root.left.right.right.right = newNode(10)

print(nodeSumDiff(root))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    public class Node
    {
        public int data;
        public Node left, right;
    };

    // Iterative method to perform level
    // order traversal line by line
    static int nodeSumDiff(Node root)
    {

        // Base Case
        if (root == null)
            return 0;

        int evenPositionNodeSum = 0;
        int oddPositionNodeSum = 0;

        // Create an empty queue for level
        // order traversal
        Queue<Node> q = new Queue<Node>();

        // Enqueue root element
        q.Enqueue(root);

        while (1 == 1)
        {

            // nodeCount (queue size) indicates
            // number of nodes in the current level
            int nodeCount = q.Count;
            if (nodeCount == 0)
                break;

            // Mark 1st node as even positioned
            bool oddPosition = true;

            // Dequeue all the nodes of current level
            // and Enqueue all the nodes of next level
            while (nodeCount > 0)
            {
                Node node = q.Peek();

                // Depending upon node position
                // add value to their respective sum
                if (oddPosition)
                    oddPositionNodeSum += node.data;
                else
                    evenPositionNodeSum += node.data;

                q.Dequeue();
                if (node.left != null)
                    q.Enqueue(node.left);
                if (node.right != null)
                    q.Enqueue(node.right);
                nodeCount--;

                // Switch the even position flag
                oddPosition = !oddPosition;
            }
        }

        // Return the absolute difference
        return Math.Abs(oddPositionNodeSum - evenPositionNodeSum);
    }

    // Utility method to create a node
    static Node newNode(int data)
    {
        Node node = new Node();
        node.data = data;
        node.left = node.right = null;
        return (node);
    }

    // Driver code
    public static void Main(String[] args)
    {
        Node root = newNode(1);
        root.left = newNode(2);
        root.right = newNode(3);
        root.left.left = newNode(4);
        root.left.right = newNode(5);
        root.right.left = newNode(6);
        root.right.right = newNode(7);
        root.left.right.left = newNode(8);
        root.left.right.right = newNode(9);
        root.left.right.right.right = newNode(10);

        Console.Write(nodeSumDiff(root));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Iterative method to perform level
    // order traversal line by line
    function nodeSumDiff(root)
    {

        // Base Case
        if (root == null)
            return 0;

        let evenPositionNodeSum = 0;
        let oddPositionNodeSum = 0;

        // Create an empty queue for level
        // order traversal
        let q = [];

        // Enqueue root element
        q.push(root);

        while (1 == 1)
        {

            // nodeCount (queue size) indicates
            // number of nodes in the current level
            let nodeCount = q.length;
            if (nodeCount == 0)
                break;

            // Mark 1st node as even positioned
            let oddPosition = true;

            // Dequeue all the nodes of current level
            // and Enqueue all the nodes of next level
            while (nodeCount > 0)
            {
                let node = q[0];

                // Depending upon node position
                // add value to their respective sum
                if (oddPosition)
                    oddPositionNodeSum += node.data;
                else
                    evenPositionNodeSum += node.data;

                q.shift();
                if (node.left != null)
                    q.push(node.left);
                if (node.right != null)
                    q.push(node.right);
                nodeCount--;

                // Switch the even position flag
                oddPosition = !oddPosition;
            }
        }

        // Return the absolute difference
        return Math.abs(oddPositionNodeSum - evenPositionNodeSum);
    }

    // Utility method to create a node
    function newNode(data)
    {
        let node = new Node(data);
        return (node);
    }

    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.left.right.left = newNode(8);
    root.left.right.right = newNode(9);
    root.left.right.right.right = newNode(10);

    document.write(nodeSumDiff(root));

</script>
```

**Output:** 

```
7
```