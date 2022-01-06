# 给定二叉树中左子树平均值至少为 K 的节点数

> 原文:[https://www . geesforgeks . org/给定二叉树中至少有 k 个平均左子树的节点数/](https://www.geeksforgeeks.org/count-of-nodes-with-average-of-left-subtree-at-least-k-in-a-given-binary-tree/)

给定一个 [**二叉树**](https://www.geeksforgeeks.org/binary-tree-data-structure/) 和一个数 **K，**任务是计算其左子树中的值的平均值大于或等于 **K** 的节点数。

**示例:**

> ***输入:*** K=5
> 树:
> 2
> /\
> 5 4
> /\/\
> 5 6 6 2
> \/
> 5 4
> ***输出:*** 3
> ***解释:***
> 2——0 级
> /\
> 5—4
> 
> 根节点 2 的左左子树平均值=(5+5+5)/3 = 5
> 1 级节点 4 的左左子树平均值=(6+4)/2 = 5
> 1 级节点 5 的左左子树平均值= (5+5) / 2 = 5
> 因此，这 3 个节点满足给定条件。
> 
> **输入:** K = 4，
> 树:1
> /
> 2
> /
> 3
> /
> 4
> **输出:** 1

**方法:**按照以下步骤解决这个问题:

1.  创建一个全局变量**和**来存储答案，并用 **0** 初始化它。
2.  创建一个函数 **countHelper** ，该函数将接受一个树**节点**和整数 **K** 作为参数，并将返回该节点的子树中的一对节点和节点数。
3.  现在，在这个函数的初始调用中传递**根**节点和 **K** 。
4.  在这个递归函数的每次调用中:
    1.  检查当前节点是否是叶节点。如果是叶节点，只需返回 **{0，0}** ，因为该节点下的节点数和都是 **0** 。
    2.  现在，调用左右子树。
    3.  检查对于当前节点，**(左右子树之和/左右子树中的节点数)> =K** ，如果是增量 **ans** 乘以 **1** 。
5.  递归功能结束后，打印**和**。

下面是上述方法的实现。

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a tree node
class Node {
public:
    int data;
    Node *left, *right;
    Node(int d)
    {
        data = d;
        left = right = NULL;
    }
};

// Global variable to store the node count
int ans = 0;

// Function to count the nodes in a tree
// with average of all left nodes
// greater than or equal to K .
pair<int, int> countHelper(Node* root,
                           int K)
{

    // For leaf Node
    if (!root->left and !root->right) {
        return { root->data, 1 };
    }

    pair<int, int> left = { 0, 0 },
                   right = { 0, 0 };

    // For left subtree
    if (root->left) {
        left = countHelper(root->left, K);
    }

    // For right subtree
    if (root->right) {
        right = countHelper(root->right, K);
    }
    if (left.second != 0
        and left.first / left.second >= K) {
        ans += 1;
    }

    return { left.first + right.first + root->data,
             left.second + right.second + 1 };
}

// Function to call the initial
// instance of function countHelper
void countNodes(Node* root, int K)
{
    countHelper(root, K);
    cout << ans;
}

// Driver Code
int main()
{
    // Given Tree
    Node* root = new Node(2);
    root->left = new Node(5);
    root->right = new Node(4);
    root->left->left = new Node(5);
    root->left->right = new Node(6);
    root->right->left = new Node(6);
    root->right->right = new Node(2);
    root->left->left->right = new Node(5);
    root->right->left->left = new Node(4);

    int K = 5;

    countNodes(root, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

static class pair
{
    int first, second;
    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Structure of a tree node
static class Node {
    int data;
    Node left, right;
    Node(int d)
    {
        data = d;
        left = right = null;
    }
};

// Global variable to store the node count
static int ans = 0;

// Function to count the nodes in a tree
// with average of all left nodes
// greater than or equal to K .
static pair countHelper(Node root,
                           int K)
{

    // For leaf Node
    if (root.left==null && root.right==null) {
        return new pair( root.data, 1 );
    }

    pair left = new pair( 0, 0 ),
                   right = new pair( 0, 0 );

    // For left subtree
    if (root.left!=null) {
        left = countHelper(root.left, K);
    }

    // For right subtree
    if (root.right!=null) {
        right = countHelper(root.right, K);
    }
    if (left.second != 0
        && left.first / left.second >= K) {
        ans += 1;
    }

    return new pair( left.first + right.first + root.data,
             left.second + right.second + 1 );
}

// Function to call the initial
// instance of function countHelper
static void countNodes(Node root, int K)
{
    countHelper(root, K);
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{

    // Given Tree
    Node root = new Node(2);
    root.left = new Node(5);
    root.right = new Node(4);
    root.left.left = new Node(5);
    root.left.right = new Node(6);
    root.right.left = new Node(6);
    root.right.right = new Node(2);
    root.left.left.right = new Node(5);
    root.right.left.left = new Node(4);

    int K = 5;

    countNodes(root, K);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python code for the above approach
class pair:
    def __init__(self, first, second):
        self.first = first;
        self.second = second;

# Structure of a tree node
class Node:
    def __init__(self, d):
        self.data = d;
        self.left = self.right = None;

# Global variable to store the node count
ans = 0;

# Function to count the nodes in a tree
# with average of all left nodes
# greater than or equal to K .
def countHelper(root, K):

    # For leaf Node
    if (root.left == None and root.right == None):
        return pair(root.data, 1);

    left = pair(0, 0)
    right = pair(0, 0)

    # For left subtree
    if (root.left != None):
        left = countHelper(root.left, K);

    # For right subtree
    if (root.right != None):
        right = countHelper(root.right, K);

    if (left.second != 0 and left.first / left.second >= K):
        global ans;
        ans += 1;

    return pair(left.first + right.first + root.data, left.second + right.second + 1);

# Function to call the initial
# instance of function countHelper
def countNodes(root, K):
    countHelper(root, K);
    print(ans);

# Driver Code
# Given Tree
root = Node(2);
root.left = Node(5);
root.right = Node(4);
root.left.left = Node(5);
root.left.right = Node(6);
root.right.left = Node(6);
root.right.right = Node(2);
root.left.left.right = Node(5);
root.right.left.left = Node(4);

K = 5;

countNodes(root, K);

# This code is contributed by Saurabh Jaiswal.
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;

public class GFG{

  class pair
  {
    public int first, second;
    public pair(int first, int second) 
    {
      this.first = first;
      this.second = second;
    }   
  }

  // Structure of a tree node
  class Node {
    public int data;
    public Node left, right;
    public Node(int d)
    {
      data = d;
      left = right = null;
    }
  };

  // Global variable to store the node count
  static int ans = 0;

  // Function to count the nodes in a tree
  // with average of all left nodes
  // greater than or equal to K .
  static pair countHelper(Node root,
                          int K)
  {

    // For leaf Node
    if (root.left==null && root.right==null) {
      return new pair( root.data, 1 );
    }

    pair left = new pair( 0, 0 ),
    right = new pair( 0, 0 );

    // For left subtree
    if (root.left!=null) {
      left = countHelper(root.left, K);
    }

    // For right subtree
    if (root.right!=null) {
      right = countHelper(root.right, K);
    }
    if (left.second != 0
        && left.first / left.second >= K) {
      ans += 1;
    }

    return new pair( left.first + right.first + root.data,
                    left.second + right.second + 1 );
  }

  // Function to call the initial
  // instance of function countHelper
  static void countNodes(Node root, int K)
  {
    countHelper(root, K);
    Console.Write(ans);
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given Tree
    Node root = new Node(2);
    root.left = new Node(5);
    root.right = new Node(4);
    root.left.left = new Node(5);
    root.left.right = new Node(6);
    root.right.left = new Node(6);
    root.right.right = new Node(2);
    root.left.left.right = new Node(5);
    root.right.left.left = new Node(4);

    int K = 5;

    countNodes(root, K);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript code for the above approach

class pair {
    constructor(first, second) {
        this.first = first;
        this.second = second;
    }
}

// Structure of a tree node
class Node {

    constructor(d) {
        this.data = d;
        this.left = this.right = null;
    }
};

// Global variable to store the node count
let ans = 0;

// Function to count the nodes in a tree
// with average of all left nodes
// greater than or equal to K .
function countHelper(root, K) {

    // For leaf Node
    if (root.left == null && root.right == null) {
        return new pair(root.data, 1);
    }

    let left = new pair(0, 0),
        right = new pair(0, 0);

    // For left subtree
    if (root.left != null) {
        left = countHelper(root.left, K);
    }

    // For right subtree
    if (root.right != null) {
        right = countHelper(root.right, K);
    }
    if (left.second != 0
        && left.first / left.second >= K) {
        ans += 1;
    }

    return new pair(left.first + right.first + root.data, left.second + right.second + 1);
}

// Function to call the initial
// instance of function countHelper
function countNodes(root, K) {
    countHelper(root, K);
    document.write(ans);
}

// Driver Code
// Given Tree
let root = new Node(2);
root.left = new Node(5);
root.right = new Node(4);
root.left.left = new Node(5);
root.left.right = new Node(6);
root.right.left = new Node(6);
root.right.right = new Node(2);
root.left.left.right = new Node(5);
root.right.left.left = new Node(4);

let K = 5;

countNodes(root, K);

// This code is contributed by Saurabh Jaiswal
</script>
```

**Output**

```
3
```

**时间复杂度:** O(N)其中 N 是树中的节点数
T3】辅助空间: O(N)