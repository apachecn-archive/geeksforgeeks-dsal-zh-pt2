# O(n)中二叉树的直径【一种新方法】

> 原文:[https://www . geesforgeks . org/新方法二叉树直径/](https://www.geeksforgeeks.org/diameter-of-a-binary-tree-in-on-a-new-method/)

树的直径是树中两片叶子之间最长路径上的节点数。下图显示了两棵树，每棵树的直径为 9，形成最长路径末端的树叶是彩色的(请注意，同一直径的树中可能有多个路径)。

![](img/9d48a23cb8c0194cbc883d75b6c17790.png)

**示例:**

```
Input :     1
          /   \
        2      3
      /  \
    4     5

Output : 4

Input :     1
          /   \
        2      3
      /  \ .    \
    4     5 .    6

Output : 5
```

我们在下面的帖子中讨论了一个解决方案。
[二叉树的直径](https://www.geeksforgeeks.org/diameter-of-a-binary-tree/)
本文讨论了一种新的简单的 O(n)方法。树的直径只能通过使用高度函数来计算，因为树的直径只不过是每个节点的最大值(left_height + right_height + 1)。所以我们需要为每个节点计算这个值(left_height + right_height + 1)并更新结果。时间复杂性–O(n)

## C++

```
// Simple C++ program to find diameter
// of a binary tree.
#include <bits/stdc++.h>
using namespace std;

/* Tree node structure used in the program */
struct Node {
    int data;
    Node* left, *right;
};

/* Function to find height of a tree */
int height(Node* root, int& ans)
{
    if (root == NULL)
        return 0;

    int left_height = height(root->left, ans);

    int right_height = height(root->right, ans);

    // update the answer, because diameter of a
    // tree is nothing but maximum value of
    // (left_height + right_height + 1) for each node
    ans = max(ans, 1 + left_height + right_height);

    return 1 + max(left_height, right_height);
}

/* Computes the diameter of binary tree with given root. */
int diameter(Node* root)
{
    if (root == NULL)
        return 0;
    int ans = INT_MIN; // This will store the final answer
    height(root, ans);
    return ans;
}

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

    printf("Diameter is %d\n", diameter(root));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to find diameter
// of a binary tree.
class GfG {

/* Tree node structure used in the program */
static class Node
{
    int data;
    Node left, right;
}

static class A
{
    int ans = Integer.MIN_VALUE;
}

/* Function to find height of a tree */
static int height(Node root, A a)
{
    if (root == null)
        return 0;

    int left_height = height(root.left, a);

    int right_height = height(root.right, a);

    // update the answer, because diameter of a
    // tree is nothing but maximum value of
    // (left_height + right_height + 1) for each node
    a.ans = Math.max(a.ans, 1 + left_height +
                    right_height);

    return 1 + Math.max(left_height, right_height);
}

/* Computes the diameter of binary
tree with given root. */
static int diameter(Node root)
{
    if (root == null)
        return 0;

    // This will store the final answer
    A a = new A();
    int height_of_tree = height(root, a);
    return a.ans;
}

static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;

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

    System.out.println("Diameter is " + diameter(root));
}
}

// This code is contributed by Prerna Saini.
```

## 蟒蛇 3

```
# Simple Python3 program to find diameter
# of a binary tree.

class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Function to find height of a tree
def height(root, ans):
    if (root == None):
        return 0

    left_height = height(root.left, ans)

    right_height = height(root.right, ans)

    # update the answer, because diameter
    # of a tree is nothing but maximum
    # value of (left_height + right_height + 1)
    # for each node
    ans[0] = max(ans[0], 1 + left_height +
                             right_height)

    return 1 + max(left_height,
                   right_height)

# Computes the diameter of binary
# tree with given root.
def diameter(root):
    if (root == None):
        return 0
    ans = [-999999999999] # This will store
                          # the final answer
    height_of_tree = height(root, ans)
    return ans[0]

# Driver code
if __name__ == '__main__':
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)

    print("Diameter is", diameter(root))

# This code is contributed by PranchalK
```

## C#

```
// Simple C# program to find diameter
// of a binary tree.
using System;

class GfG
{

/* Tree node structure used in the program */
class Node
{
    public int data;
    public Node left, right;
}

class A
{
    public int ans = int.MinValue;
}

/* Function to find height of a tree */
static int height(Node root, A a)
{
    if (root == null)
        return 0;

    int left_height = height(root.left, a);

    int right_height = height(root.right, a);

    // update the answer, because diameter of a
    // tree is nothing but maximum value of
    // (left_height + right_height + 1) for each node
    a.ans = Math.Max(a.ans, 1 + left_height +
                    right_height);

    return 1 + Math.Max(left_height, right_height);
}

/* Computes the diameter of binary
tree with given root. */
static int diameter(Node root)
{
    if (root == null)
        return 0;

    // This will store the final answer
    A a = new A();
    int height_of_tree = height(root, a);
    return a.ans;
}

static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;

    return (node);
}

// Driver code
public static void Main()
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    Console.WriteLine("Diameter is " + diameter(root));
}
}

/* This code is contributed by Rajput-Ji*/
```

## java 描述语言

```
<script>

    // Simple Javascript program to find
    // diameter of a binary tree.

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    let ans = Number.MIN_VALUE;

    /* Function to find height of a tree */
    function height(root)
    {
        if (root == null)
            return 0;

        let left_height = height(root.left);

        let right_height = height(root.right);

        // update the answer, because diameter of a
        // tree is nothing but maximum value of
        // (left_height + right_height + 1) for each node
        ans = Math.max(ans, 1 + left_height +
                        right_height);

        return 1 + Math.max(left_height, right_height);
    }

    /* Computes the diameter of binary
    tree with given root. */
    function diameter(root)
    {
        if (root == null)
            return 0;

        // This will store the final answer
        let height_of_tree = height(root);
        return ans;
    }

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

    document.write("Diameter is " + diameter(root));

</script>
```

**Output**

```
Diameter is 4
```

本文由 [**Pooja Kamal**](https://www.facebook.com/pooja.kamal.338) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。