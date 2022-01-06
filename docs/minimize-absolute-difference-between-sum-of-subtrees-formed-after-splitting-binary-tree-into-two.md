# 将二叉树拆分为两个后形成的子树之和的绝对差最小化

> 原文:[https://www . geeksforgeeks . org/minimum-subtrees 之和的绝对差-拆分后形成-二叉树一分为二/](https://www.geeksforgeeks.org/minimize-absolute-difference-between-sum-of-subtrees-formed-after-splitting-binary-tree-into-two/)

给定由 **N** 节点组成的**二叉树**，任务是通过移除一条边将二叉树分割成两个**子树**，使得子树之和的绝对差最小。

**示例:**

> **输入:**1
> /\
> 2 3
> /\ \
> 4 5 8
> /\
> 6 7
> **输出:** 6
> **解释:**在顶点 3 和 8 之间拆分树。创建的子树的和为 21 和 15
> 
> **输入**:1
> /\
> 2 3
> /\/\
> 4 5 6 7
> 
> **输出** : 4
> **说明:**在顶点 1 和 3 之间拆分树。创建的子树的和为 16 和 12

**方法:**给定的问题可以通过以下步骤解决:

*   将变量 **minDiff** 初始化为将存储答案的最大整数值
*   使用后序遍历来存储当前节点、左子树和右子树在当前节点中的总和
*   使用前序遍历，在每次递归调用时，如果拆分在以下两者之间，则查找子树的和:
    *   当前节点和左侧子节点
    *   当前节点和右子节点
*   更新 **minDiff** 如果在任何递归调用中子树的差小于 **minDiff**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

struct Node {
    Node* left;
    Node* right;
    int val;

    Node(int val)
    {
        this->val = val;
        this->left = nullptr;
        this->right = nullptr;
    }
};

int postOrder(Node* root)
{
    if (root == nullptr)
        return 0;
    root->val += postOrder(root->left) + postOrder(root->right);
    return root->val;
}

void preOrder(Node* root, int minDiff[])
{
    if (root == nullptr)
        return;

    // Absolute difference in subtrees
    // if left edge is broken
    int leftDiff = abs(root->left->val - (root->val - root->left->val));

    // Absolute difference in subtrees
    // if right edge is broken
    int rightDiff = abs(root->right->val - (root->val - root->right->val));

    // Update minDiff if a difference
    // lesser than it is found
    minDiff[0] = min(minDiff[0], min(leftDiff, rightDiff));

    return;
}

// Function to calculate minimum absolute
// difference of subtrees after
// splitting the tree into two parts
int minAbsDiff(Node* root)
{

    // Reference variable
    // to store the answer
    int minDiff[1];

    minDiff[0] = INT_MAX;

    // Function to store sum of values
    // of current node, left subtree and
    // right subtree in place of
    // current node's value
    postOrder(root);

    // Function to perform every
    // possible split and calculate
    // absolute difference of subtrees
    preOrder(root, minDiff);

    return minDiff[0];
}

int main()
{
    // Construct the tree
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->left = new Node(6);
    root->right->right = new Node(7);

    // Print the output
    cout << minAbsDiff(root);

    return 0;
}

// This code is contributed by mukesh07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.lang.Math;
import java.io.*;

class GFG {

    static class Node {
        Node left, right;
        int val;
        public Node(int val)
        {
            this.val = val;
            this.left = this.right = null;
        }
    }

    // Function to calculate minimum absolute
    // difference of subtrees after
    // splitting the tree into two parts
    public static int minAbsDiff(Node root)
    {

        // Reference variable
        // to store the answer
        int[] minDiff = new int[1];

        minDiff[0] = Integer.MAX_VALUE;

        // Function to store sum of values
        // of current node, left subtree and
        // right subtree in place of
        // current node's value
        postOrder(root);

        // Function to perform every
        // possible split and calculate
        // absolute difference of subtrees
        preOrder(root, minDiff);

        return minDiff[0];
    }

    public static int postOrder(Node root)
    {
        if (root == null)
            return 0;
        root.val += postOrder(root.left)
                    + postOrder(root.right);
        return root.val;
    }

    public static void preOrder(Node root,
                                int[] minDiff)
    {
        if (root == null)
            return;

        // Absolute difference in subtrees
        // if left edge is broken
        int leftDiff
            = Math.abs(root.left.val
                       - (root.val - root.left.val));

        // Absolute difference in subtrees
        // if right edge is broken
        int rightDiff
            = Math.abs(root.right.val
                       - (root.val - root.right.val));

        // Update minDiff if a difference
        // lesser than it is found
        minDiff[0]
            = Math.min(minDiff[0],
                       Math.min(leftDiff, rightDiff));

        return;
    }

    // Driver code
    public static void main(String[] args)
    {
        // Construct the tree
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);

        // Print the output
        System.out.println(minAbsDiff(root));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation for the above approach
import sys

# Structure of Node
class Node:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

# Function to calculate minimum absolute
# difference of subtrees after
# splitting the tree into two parts
def minAbsDiff(root):

    # Reference variable
    # to store the answer
    minDiff = [0]*(1)

    minDiff[0] = sys.maxsize

    # Function to store sum of values
    # of current node, left subtree and
    # right subtree in place of
    # current node's value
    postOrder(root)

    # Function to perform every
    # possible split and calculate
    # absolute difference of subtrees
    preOrder(root, minDiff)

    return minDiff[0]

def postOrder(root):
    if (root == None):
        return 0
    root.val += postOrder(root.left) + postOrder(root.right)
    return root.val

def preOrder(root, minDiff):
    if (root == None):
        return

    # Absolute difference in subtrees
    # if left edge is broken
    leftDiff = abs(root.left.val - (root.val - root.left.val))

    # Absolute difference in subtrees
    # if right edge is broken
    rightDiff = abs(root.right.val - (root.val - root.right.val))

    # Update minDiff if a difference
    # lesser than it is found
    minDiff[0] = min(minDiff[0], min(leftDiff, rightDiff))

    return

# Construct the tree
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.left = Node(6)
root.right.right = Node(7)

# Print the output
print(minAbsDiff(root))

# This code is contributed by rameshtravel07.
```

## C#

```
// C# implementation for the above approach
using System;

public class GFG {

    class Node {
        public Node left, right;
        public int val;
    }

  static Node newNode(int data)
    {
        Node newNode = new Node();
        newNode.val = data;
        newNode.left= null;
        newNode.right = null;
        return newNode;
    }

    // Function to calculate minimum absolute
    // difference of subtrees after
    // splitting the tree into two parts
    static int minAbsDiff(Node root)
    {

        // Reference variable
        // to store the answer
        int[] minDiff = new int[1];

        minDiff[0] = Int32.MaxValue;

        // Function to store sum of values
        // of current node, left subtree and
        // right subtree in place of
        // current node's value
        postOrder(root);

        // Function to perform every
        // possible split and calculate
        // absolute difference of subtrees
        preOrder(root, minDiff);

        return minDiff[0];
    }

   static int postOrder(Node root)
    {
        if (root == null)
            return 0;
        root.val += postOrder(root.left)
                    + postOrder(root.right);
        return root.val;
    }

   static void preOrder(Node root,
                                int[] minDiff)
    {
        if (root == null)
            return;

        // Absolute difference in subtrees
        // if left edge is broken
        int leftDiff
            = Math.Abs(root.left.val
                       - (root.val - root.left.val));

        // Absolute difference in subtrees
        // if right edge is broken
        int rightDiff
            = Math.Abs(root.right.val
                       - (root.val - root.right.val));

        // Update minDiff if a difference
        // lesser than it is found
        minDiff[0]
            = Math.Min(minDiff[0],
                       Math.Min(leftDiff, rightDiff));

        return;
    }

    // Driver code
    public static void Main()
    {
        // Construct the tree
        Node root =  newNode(1);
        root.left =  newNode(2);
        root.right =  newNode(3);
        root.left.left =  newNode(4);
        root.left.right =  newNode(5);
        root.right.left =  newNode(6);
        root.right.right =  newNode(7);

        // Print the output
        Console.Write(minAbsDiff(root));
    }
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
    // Javascript implementation for the above approach

    // Structure of Node
    class Node
    {
        constructor(val) {
           this.left = null;
           this.right = null;
           this.val = val;
        }
    }

    // Function to calculate minimum absolute
    // difference of subtrees after
    // splitting the tree into two parts
    function minAbsDiff(root)
    {

        // Reference variable
        // to store the answer
        let minDiff = new Array(1);

        minDiff[0] = Number.MAX_VALUE;

        // Function to store sum of values
        // of current node, left subtree and
        // right subtree in place of
        // current node's value
        postOrder(root);

        // Function to perform every
        // possible split and calculate
        // absolute difference of subtrees
        preOrder(root, minDiff);

        return minDiff[0];
    }

    function postOrder(root)
    {
        if (root == null)
            return 0;
        root.val += postOrder(root.left)
                    + postOrder(root.right);
        return root.val;
    }

    function preOrder(root, minDiff)
    {
        if (root == null)
            return;

        // Absolute difference in subtrees
        // if left edge is broken
        let leftDiff
            = Math.abs(root.left.val
                       - (root.val - root.left.val));

        // Absolute difference in subtrees
        // if right edge is broken
        let rightDiff
            = Math.abs(root.right.val
                       - (root.val - root.right.val));

        // Update minDiff if a difference
        // lesser than it is found
        minDiff[0]
            = Math.min(minDiff[0],
                       Math.min(leftDiff, rightDiff));

        return;
    }

    // Construct the tree
    let root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.left = new Node(6);
    root.right.right = new Node(7);

    // Print the output
    document.write(minAbsDiff(root));

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
4
```

**时间复杂度** : O(N)
**辅助空间** : O(1)