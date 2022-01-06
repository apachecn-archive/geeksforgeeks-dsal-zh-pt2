# 二叉树中具有相同值的最长路径

> 原文:[https://www . geesforgeks . org/最长路径-值-二叉树/](https://www.geeksforgeeks.org/longest-path-values-binary-tree/)

给定一棵二叉树，找出路径中每个节点具有相同值的最长路径的长度。此路径可能会也可能不会穿过根。两个节点之间的路径长度由它们之间的边数来表示。
**例:**

```
Input :
              2
             / \
            7   2
           / \   \
          1   1   2
Output : 2

Input :
              4
             / \
            4   4
           / \   \
          4   9   5
Output : 3
```

这个想法是递归遍历给定的二叉树。我们可以从它的根在两个方向(左和右)上想到任何路径(具有相同值的节点)。然后，对于每个节点，我们想知道向左延伸的最大可能长度和向右延伸的最大可能长度是多少。如果节点->left 存在，并且与节点具有相同的值，则从节点延伸的最长长度将是 1 +长度(节点->left)。对于节点->右例也是如此。
当我们计算长度时，每个候选答案将是从该节点开始的两个方向的长度之和。我们不断更新这些答案，并返回最大值。

## C++

```
// C++ program to find the length of longest
// path with same values in a binary tree.
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to
left child and a pointer to right child */
struct Node {
  int val;
  struct Node *left, *right;
};

/* Function to print the longest path
   of same values */
int length(Node *node, int *ans) {
  if (!node)
    return 0;

  // Recursive calls to check for subtrees
  int left = length(node->left, ans);
  int right = length(node->right, ans);

  // Variables to store maximum lengths in two directions
  int Leftmax = 0, Rightmax = 0;

  // If curr node and it's left child has same value
  if (node->left && node->left->val == node->val)
    Leftmax += left + 1; 

  // If curr node and it's right child has same value
  if (node->right && node->right->val == node->val)
    Rightmax += right + 1;

  *ans = max(*ans, Leftmax + Rightmax);
  return max(Leftmax, Rightmax);
}

/* Driver function to find length of
   longest same value path*/
int longestSameValuePath(Node *root) {
  int ans = 0;
  length(root, &ans);
  return ans;
}

/* Helper function that allocates a
new node with the given data and
NULL left and right pointers. */
Node *newNode(int data) {
  Node *temp = new Node;
  temp->val = data;
  temp->left = temp->right = NULL;
  return temp;
}

// Driver code
int main() {
  /* Let us construct a Binary Tree
        4
       / \
      4   4
     / \   \
    4   9   5 */

  Node *root = NULL;
  root = newNode(4);
  root->left = newNode(4);
  root->right = newNode(4);
  root->left->left = newNode(4);
  root->left->right = newNode(9);
  root->right->right = newNode(5);
  cout << longestSameValuePath(root);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of longest
// path with same values in a binary tree.
class GFG
{
static int ans;

/* A binary tree node has data, pointer to
left child and a pointer to right child */
static class Node
{
    int val;
    Node left, right;
};

/* Function to print the longest path
of same values */
static int length(Node node)
{
    if (node == null)
        return 0;

    // Recursive calls to check for subtrees
    int left = length(node.left);
    int right = length(node.right);

    // Variables to store maximum lengths
    // in two directions
    int Leftmax = 0, Rightmax = 0;

    // If curr node and it's left child
    // has same value
    if (node.left != null &&
        node.left.val == node.val)
        Leftmax += left + 1;

    // If curr node and it's right child
    // has same value
    if (node.right != null &&
        node.right.val == node.val)
        Rightmax += right + 1;

    ans = Math.max(ans, Leftmax + Rightmax);
    return Math.max(Leftmax, Rightmax);
}

// Function to find length of
// longest same value path
static int longestSameValuePath(Node root)
{
    ans = 0;
    length(root);
    return ans;
}

/* Helper function that allocates a
new node with the given data and
null left and right pointers. */
static Node newNode(int data)
{
    Node temp = new Node();
    temp.val = data;
    temp.left = temp.right = null;
    return temp;
}

// Driver code
public static void main(String[] args)
{

    /* Let us cona Binary Tree
            4
        / \
        4 4
        / \ \
        4 9 5 */
    Node root = null;
    root = newNode(4);
    root.left = newNode(4);
    root.right = newNode(4);
    root.left.left = newNode(4);
    root.left.right = newNode(9);
    root.right.right = newNode(5);
    System.out.print(longestSameValuePath(root));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find the length of longest
# path with same values in a binary tree.

# Helper function that allocates a
# new node with the given data and
# None left and right pointers.
class newNode:
  def __init__(self, data):
      self.val = data
      self.left = self.right = None

# Function to print the longest path
# of same values
def length(node, ans):
  if (not node):
    return 0

  # Recursive calls to check for subtrees
  left = length(node.left, ans)
  right = length(node.right, ans)

  # Variables to store maximum lengths
  # in two directions
  Leftmax = 0
  Rightmax = 0

  # If curr node and it's left child has same value
  if (node.left and node.left.val == node.val): 
    Leftmax += left + 1 

  # If curr node and it's right child has same value
  if (node.right and node.right.val == node.val):
    Rightmax += right + 1

  ans[0] = max(ans[0], Leftmax + Rightmax)
  return max(Leftmax, Rightmax)

# Driver function to find length of
# longest same value path
def longestSameValuePath(root):
  ans = [0]
  length(root, ans)
  return ans[0]

# Driver code
if __name__ == '__main__':

  # Let us construct a Binary Tree
  #      4
  #     / \
  #    4   4
  #   / \   \
  #  4   9   5
  root = None
  root = newNode(4)
  root.left = newNode(4)
  root.right = newNode(4)
  root.left.left = newNode(4)
  root.left.right = newNode(9)
  root.right.right = newNode(5)
  print(longestSameValuePath(root))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find the length of longest
// path with same values in a binary tree.
using System;

class GFG
{
static int ans;

/* A binary tree node has data, pointer to
left child and a pointer to right child */
public class Node
{
    public int val;
    public Node left, right;
};

/* Function to print the longest path
of same values */
static int length(Node node)
{
    if (node == null)
        return 0;

    // Recursive calls to check for subtrees
    int left = length(node.left);
    int right = length(node.right);

    // Variables to store maximum lengths
    // in two directions
    int Leftmax = 0, Rightmax = 0;

    // If curr node and it's left child
    // has same value
    if (node.left != null &&
        node.left.val == node.val)
        Leftmax += left + 1;

    // If curr node and it's right child
    // has same value
    if (node.right != null &&
        node.right.val == node.val)
        Rightmax += right + 1;

    ans = Math.Max(ans, Leftmax + Rightmax);
    return Math.Max(Leftmax, Rightmax);
}

// Function to find length of
// longest same value path
static int longestSameValuePath(Node root)
{
    ans = 0;
    length(root);
    return ans;
}

/* Helper function that allocates a
new node with the given data and
null left and right pointers. */
static Node newNode(int data)
{
    Node temp = new Node();
    temp.val = data;
    temp.left = temp.right = null;
    return temp;
}

// Driver code
public static void Main(String[] args)
{

    /* Let us cona Binary Tree
            4
        / \
        4 4
        / \ \
        4 9 5 */
    Node root = null;
    root = newNode(4);
    root.left = newNode(4);
    root.right = newNode(4);
    root.left.left = newNode(4);
    root.left.right = newNode(9);
    root.right.right = newNode(5);
    Console.Write(longestSameValuePath(root));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program to find the length of longest
    // path with same values in a binary tree.

    let ans;

    /* A binary tree node has data, pointer to
    left child and a pointer to right child */
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.val = data;
        }
    }

    /* Function to print the longest path
    of same values */
    function length(node)
    {
        if (node == null)
            return 0;

        // Recursive calls to check for subtrees
        let left = length(node.left);
        let right = length(node.right);

        // Variables to store maximum lengths
        // in two directions
        let Leftmax = 0, Rightmax = 0;

        // If curr node and it's left child
        // has same value
        if (node.left != null &&
            node.left.val == node.val)
            Leftmax += left + 1;

        // If curr node and it's right child
        // has same value
        if (node.right != null &&
            node.right.val == node.val)
            Rightmax += right + 1;

        ans = Math.max(ans, Leftmax + Rightmax);
        return Math.max(Leftmax, Rightmax);
    }

    // Function to find length of
    // longest same value path
    function longestSameValuePath(root)
    {
        ans = 0;
        length(root);
        return ans;
    }

    /* Helper function that allocates a
    new node with the given data and
    null left and right pointers. */
    function newNode(data)
    {
        let temp = new Node(data);
        temp.val = data;
        temp.left = temp.right = null;
        return temp;
    }

    /* Let us cona Binary Tree
         4
        / \
        4 4
       / \ \
       4 9 5 */
    let root = null;
    root = newNode(4);
    root.left = newNode(4);
    root.right = newNode(4);
    root.left.left = newNode(4);
    root.left.right = newNode(9);
    root.right.right = newNode(5);
    document.write(longestSameValuePath(root));

</script>
```

**输出:**

```
3
```

**复杂度分析:**

*   时间复杂度:O(n)，其中 n 是树中的节点数，因为每个节点处理一次。
*   辅助空间:O(h)，其中 h 是树的高度，因为递归可以达到深度 h