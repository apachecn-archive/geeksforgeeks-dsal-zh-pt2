# 求二叉树中从根到给定节点的距离

> 原文:[https://www . geesforgeks . org/find-distance-root-given-node-二叉树/](https://www.geeksforgeeks.org/find-distance-root-given-node-binary-tree/)

给定二叉树的根和其中的一个键 x，求给定键到根的距离。距离是指两个节点之间的边数。

**示例:**

```
Input : x = 45,
        Root of below tree
        5
      /    \
    10      15
    / \    /  \
  20  25  30   35
       \
       45
Output : Distance = 3             
There are three edges on path
from root to 45.

For more understanding of question,
in above tree distance of 35 is two
and distance of 10 is 1.
```

**方法:**思路是从根开始遍历树。检查 x 是否出现在根或左子树或右子树中。我们将距离初始化为-1，并将这三种情况的距离加 1。

## C++

```
// C++ program to find distance of a given
// node from root.
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node
{
    int data;
    Node *left, *right;
};

// A utility function to create a new Binary
// Tree Node
Node *newNode(int item)
{
    Node *temp = new Node;
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

// Returns -1 if x doesn't exist in tree. Else
// returns distance of x from root
int findDistance(Node *root, int x)
{
    // Base case
    if (root == NULL)
      return -1;

    // Initialize distance
    int dist = -1;

    // Check if x is present at root or in left
    // subtree or right subtree.
    if ((root->data == x) ||
        (dist = findDistance(root->left, x)) >= 0 ||
        (dist = findDistance(root->right, x)) >= 0)
        return dist + 1;

    return dist;
}

// Driver Program to test above functions
int main()
{
    Node *root = newNode(5);
    root->left = newNode(10);
    root->right = newNode(15);
    root->left->left = newNode(20);
    root->left->right = newNode(25);
    root->left->right->right = newNode(45);
    root->right->left = newNode(30);
    root->right->right = newNode(35);

    cout << findDistance(root, 45);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find distance of a given
// node from root.
import java.util.*;
class GfG {

// A Binary Tree Node
static class Node
{
    int data;
    Node left, right;
}

// A utility function to create a new Binary
// Tree Node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.data = item;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Returns -1 if x doesn't exist in tree. Else
// returns distance of x from root
static int findDistance(Node root, int x)
{
    // Base case
    if (root == null)
    return -1;

    // Initialize distance
    int dist = -1;

    // Check if x is present at root or in left
    // subtree or right subtree.
    if ((root.data == x) ||
        (dist = findDistance(root.left, x)) >= 0 ||
        (dist = findDistance(root.right, x)) >= 0)
        return dist + 1;

    return dist;
}

// Driver Program to test above functions
public static void main(String[] args)
{
    Node root = newNode(5);
    root.left = newNode(10);
    root.right = newNode(15);
    root.left.left = newNode(20);
    root.left.right = newNode(25);
    root.left.right.right = newNode(45);
    root.right.left = newNode(30);
    root.right.right = newNode(35);

    System.out.println(findDistance(root, 45));
}
}
```

## 蟒蛇 3

```
# Python3 program to find distance of
# a given node from root.

# A class to create a new Binary
# Tree Node
class newNode:
    def __init__(self, item):
        self.data = item
        self.left = self.right = None

# Returns -1 if x doesn't exist in tree.
# Else returns distance of x from root
def findDistance(root, x):

    # Base case
    if (root == None):
        return -1

    # Initialize distance
    dist = -1

    # Check if x is present at root or
    # in left subtree or right subtree.
    if (root.data == x):
        return dist + 1
    else:
        dist = findDistance(root.left, x)
        if dist >= 0:
            return dist + 1
        else:
            dist = findDistance(root.right, x)
            if dist >= 0:
                return dist + 1

    return dist

# Driver Code
if __name__ == '__main__':

    root = newNode(5)
    root.left = newNode(10)
    root.right = newNode(15)
    root.left.left = newNode(20)
    root.left.right = newNode(25)
    root.left.right.right = newNode(45)
    root.right.left = newNode(30)
    root.right.right = newNode(35)

    print(findDistance(root, 45))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find distance of a given
// node from root.
using System;

class GfG
{

    // A Binary Tree Node
    class Node
    {
        public int data;
        public Node left, right;
    }

    // A utility function to create 
    // a new Binary Tree Node
    static Node newNode(int item)
    {
        Node temp = new Node();
        temp.data = item;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    // Returns -1 if x doesn't exist in tree. Else
    // returns distance of x from root
    static int findDistance(Node root, int x)
    {
        // Base case
        if (root == null)
        return -1;

        // Initialize distance
        int dist = -1;

        // Check if x is present at root or in left
        // subtree or right subtree.
        if ((root.data == x) ||
            (dist = findDistance(root.left, x)) >= 0 ||
            (dist = findDistance(root.right, x)) >= 0)
            return dist + 1;

        return dist;
    }

    // Driver code
    public static void Main(String[] args)
    {
        Node root = newNode(5);
        root.left = newNode(10);
        root.right = newNode(15);
        root.left.left = newNode(20);
        root.left.right = newNode(25);
        root.left.right.right = newNode(45);
        root.right.left = newNode(30);
        root.right.right = newNode(35);

        Console.WriteLine(findDistance(root, 45));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find distance
// of a given node from root.

// A Binary Tree Node
class Node
{

    // A utility function to create a
    // new Binary Tree Node
    constructor(data)
    {
        this.data = data;
        this.left = this.right = null;
    }
}

// Returns -1 if x doesn't exist in tree. Else
// returns distance of x from root
function findDistance(root, x)
{

    // Base case
    if (root == null)
        return -1;

    // Initialize distance
    let dist = -1;

    // Check if x is present at root or in left
    // subtree or right subtree.
    if ((root.data == x) ||
        (dist = findDistance(root.left, x)) >= 0 ||
        (dist = findDistance(root.right, x)) >= 0)
        return dist + 1;

    return dist;
}

// Driver code
let root = new Node(5);
root.left = new Node(10);
root.right = new Node(15);
root.left.left = new Node(20);
root.left.right = new Node(25);
root.left.right.right = new Node(45);
root.right.left = new Node(30);
root.right.right = new Node(35);

document.write(findDistance(root, 45));

// This code is contributed by rag2127

</script>
```

**输出:**

```
3
```

**时间复杂度:** O(N)

**辅助空间:** O(1)

本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。