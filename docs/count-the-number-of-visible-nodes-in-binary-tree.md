# 统计二叉树中可见节点的数量

> 原文:[https://www . geesforgeks . org/count-二叉树中可见节点的数量/](https://www.geeksforgeeks.org/count-the-number-of-visible-nodes-in-binary-tree/)

给定一棵二叉树，任务是找到给定二叉树中可见节点的数量。如果在从根节点到节点 N 的路径中，没有大于 N 的值的节点，
**示例:**

```
Input:
      5
     /  \
   3     10
  /  \   /
20   21 1

Output: 4 
Explanation:
There are 4 visible nodes. 
They are:
5: In the path 5 -> 3, 5 is the highest node value.
20: In the path 5 -> 3 -> 20, 20 is the highest node value.
21: In the path 5 -> 3 -> 21, 21 is the highest node value.
10: In the path 5 -> 10 -> 1, 10 is the highest node value. 

Input:
      -1
        \
         -2
           \
            -3
Output: 1
```

**方法:**思路是先遍历树。由于我们需要看到给定路径中的最大值，[预序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)用于遍历给定的二叉树。遍历树时，我们需要跟踪到目前为止看到的节点的最大值。如果当前节点大于或等于最大值，则增加可见节点的计数，并用当前节点值更新最大值。
以下是上述办法的实施情况:

## C++

```
// C++ implementation to
// count the number of
// visible nodes in the
// binary tree
#include <bits/stdc++.h>
using namespace std;

// Node containing the
// left and right child of
// current node and the key value
struct Node
{
    int data;
    Node *left, *right;
};

/* Utility that allocates a
new node with the given key and
NULL left and right pointers. */
struct Node* newnode(int data)
{
    struct Node* node = new (struct Node);
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Variable to keep the track
// of visible nodes
int countNode = 0;

// Function to perform the preorder traversal
// for the given tree
void preOrder(Node* node, int mx)
{
    // Base case
    if (node == NULL)
    {
        return;
    }

    // If the current node value is greater
    // or equal to the max value,
    // then update count variable
    // and also update max variable
    if (node->data >= mx)
    {
        countNode++;
        mx = max(node->data, mx);
    }

    // Traverse to the left
    preOrder(node->left, mx);

    // Traverse to the right
    preOrder(node->right, mx);
}

// Driver code
int main()
{
    struct Node* root = newnode(5);

    /*
            5
           /  \
         3     10
        /  \   /
       20   21 1
*/

    root->left = newnode(3);
    root->right = newnode(10);

    root->left->left = newnode(20);
    root->left->right = newnode(21);

    root->right->left = newnode(1);

    preOrder(root, INT_MIN);

    cout << countNode;
}

// This code is contributed by gauravrajput1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// number of visible nodes in
// the binary tree

// Class containing the left and right
// child of current node and the
// key value
class Node {
    int data;
    Node left, right;

    // Constructor of the class
    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

public class GFG {
    Node root;

    // Variable to keep the track
    // of visible nodes
    static int count;

    // Function to perform the preorder traversal
    // for the given tree
    static void preOrder(Node node, int max)
    {

        // Base case
        if (node == null) {
            return;
        }

        // If the current node value is greater
        // or equal to the max value,
        // then update count variable
        // and also update max variable
        if (node.data >= max) {
            count++;
            max = Math.max(node.data, max);
        }

        // Traverse to the left
        preOrder(node.left, max);

        // Traverse to the right
        preOrder(node.right, max);
    }

    // Driver code
    public static void main(String[] args)
    {
        GFG tree = new GFG();

        /*
                5
               /  \
             3     10
            /  \   /
           20   21 1
*/

        tree.root = new Node(5);
        tree.root.left = new Node(3);
        tree.root.right = new Node(10);

        tree.root.left.left = new Node(20);
        tree.root.left.right = new Node(21);

        tree.root.right.left = new Node(1);

        count = 0;
        preOrder(tree.root, Integer.MIN_VALUE);

        System.out.println(count);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation to
# count the number of
# visible nodes in the
# binary tree

import sys
# Node containing the
# left and right child of
# current node and the key value

class newNode:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

''' Utility that allocates a
new node with the given key and
None left and right pointers. */
'''

# Variable to keep the track
# of visible nodes
countNode = 0

# Function to perform the
# preorder traversal for the
# given tree
def preOrder(node, mx):

    global countNode

    # Base case
    if (node == None):
        return

    # If the current node value
    # is greater or equal to the
    # max value, then update count
    # variable and also update max
    # variable
    if (node.data >= mx):
        countNode += 1
        mx = max(node.data, mx)

    # Traverse to the left
    preOrder(node.left, mx)

    # Traverse to the right
    preOrder(node.right, mx)

# Driver code
if __name__ == '__main__':

    root = newNode(5)

    ''' /*
            5
           /  \
         3     10
        /  /   /
       20   21 1
    */
    '''
    root.left = newNode(3)
    root.right = newNode(10)
    root.left.left = newNode(20)
    root.left.right = newNode(21)
    root.right.left = newNode(1)
    preOrder(root, -sys.maxsize-1)
    print(countNode)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# implementation to count the
// number of visible nodes in
// the binary tree
using System;

// Class containing the left and right
// child of current node and the
// key value
class Node
{
    public int data;
    public Node left, right;

    // Constructor of the class
    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class GFG{

Node root;

// Variable to keep the track
// of visible nodes
static int count;

// Function to perform the preorder
// traversal for the given tree
static void preOrder(Node node, int max)
{

    // Base case
    if (node == null)
    {
        return;
    }

    // If the current node value is greater
    // or equal to the max value,
    // then update count variable
    // and also update max variable
    if (node.data >= max)
    {
        count++;
        max = Math.Max(node.data, max);
    }

    // Traverse to the left
    preOrder(node.left, max);

    // Traverse to the right
    preOrder(node.right, max);
}

// Driver code
static public void Main(String[] args)
{
    GFG tree = new GFG();

/*
         5
        / \
      3       10
     / \   /
    20 21 1
*/

    tree.root = new Node(5);
    tree.root.left = new Node(3);
    tree.root.right = new Node(10);

    tree.root.left.left = new Node(20);
    tree.root.left.right = new Node(21);
    tree.root.right.left = new Node(1);

    count = 0;
    preOrder(tree.root, int.MinValue);
    Console.WriteLine(count);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
    // Javascript implementation to count the
    // number of visible nodes in the binary tree

    // Class containing the left and right
    // child of current node and the
    // key value
    class Node
    {
       constructor(item) {
           this.left = null;
           this.right = null;
           this.data = item;
        }
    }

    let root;

    // Variable to keep the track
    // of visible nodes
    let count;

    // Function to perform the preorder traversal
    // for the given tree
    function preOrder(node, max)
    {

        // Base case
        if (node == null) {
            return;
        }

        // If the current node value is greater
        // or equal to the max value,
        // then update count variable
        // and also update max variable
        if (node.data >= max) {
            count++;
            max = Math.max(node.data, max);
        }

        // Traverse to the left
        preOrder(node.left, max);

        // Traverse to the right
        preOrder(node.right, max);
    }

    /*
                  5
                 /  \
               3     10
              /  \   /
             20   21 1
      */

    root = new Node(5);
    root.left = new Node(3);
    root.right = new Node(10);

    root.left.left = new Node(20);
    root.left.right = new Node(21);

    root.right.left = new Node(1);

    count = 0;
    preOrder(root, Number.MIN_VALUE);

    document.write(count);

 // This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
4
```

**复杂度分析:**
**时间复杂度:** *O(N)* 其中 N 是二叉树中的节点数。
**辅助空间:** *O(H)* 其中 H 为二叉树的高度。