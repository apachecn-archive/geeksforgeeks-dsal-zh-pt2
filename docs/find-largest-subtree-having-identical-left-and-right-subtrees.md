# 找到左右子树相同的最大子树

> 原文:[https://www . geesforgeks . org/find-最大子树-具有相同的左右子树/](https://www.geeksforgeeks.org/find-largest-subtree-having-identical-left-and-right-subtrees/)

给定一棵二叉树，找到最大的子树，它的左右子树相同。预期复杂性为 0(n)。

例如，

```
Input: 
            50
         /      \
        10       60
       /  \     /   \
      5   20   70    70
               / \   / \
             65  80 65  80
Output: 
 Largest subtree is rooted at node 60
```

一个简单的解决方案是考虑每个节点，使用这里讨论的方法递归地检查左右子树是否相同。跟踪此类节点的最大大小。

我们可以保存递归调用。其思想是对给定的二叉树进行后序遍历，对于每个节点，我们存储其左右子树的结构。为了存储左右子树的结构，我们使用了一个字符串。我们使用分隔符将字符串中的左右子树节点与当前节点分开。对于每个遇到的节点，如果它的左右子树结构相似，我们会更新到目前为止找到的最大的子树。

以下是上述想法的实施–

## C++

```
// C++ program to find the largest subtree
// having identical left and right subtree
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left
  child and a pointer to right child */
struct Node
{
    int data;
    Node* left, * right;
};

/* Helper function that allocates a new node with
  the given data and NULL left and right pointers. */
Node* newNode(int data)
{
    Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Sets maxSize to size of largest subtree with
// identical left and right.  maxSize is set with
// size of the maximum sized subtree. It returns
// size of subtree rooted with current node. This
// size is used to keep track of maximum size.
int largestSubtreeUtil(Node* root, string& str,
                    int& maxSize, Node*& maxNode)
{
    if (root == NULL)
        return 0;

    // string to store structure of left and
    // right subtrees
    string left = "", right = "";

    // traverse left subtree and finds its size
    int ls = largestSubtreeUtil(root->left, left,
                               maxSize, maxNode);

    // traverse right subtree and finds its size
    int rs = largestSubtreeUtil(root->right, right,
                               maxSize, maxNode);

    // if left and right subtrees are similar
    // update maximum subtree if needed (Note that
    // left subtree may have a bigger value than
    // right and vice versa)
    int size = ls + rs + 1;
    if (left.compare(right) == 0)
    {
       if (size > maxSize)
       {
            maxSize  = size;
            maxNode = root;
       }
    }

    // append left subtree data
    str.append("|").append(left).append("|");

    // append current node data
    str.append("|").append(to_string(root->data)).append("|");

    // append right subtree data
    str.append("|").append(right).append("|");

    return size;
}

// function to find the largest subtree
// having identical left and right subtree
int largestSubtree(Node* node, Node*& maxNode)
{
    int maxSize = 0;
    string str = "";
    largestSubtreeUtil(node, str, maxSize, maxNode);

    return maxSize;
}

/* Driver program to test above functions*/
int main()
{
    /* Let us construct the following Tree
                50
              /     \
             10      60
            / \     /  \
            5 20   70   70
                   / \  / \
                  65 80 65 80   */
    Node* root = newNode(50);
    root->left = newNode(10);
    root->right = newNode(60);
    root->left->left = newNode(5);
    root->left->right = newNode(20);
    root->right->left = newNode(70);
    root->right->left->left = newNode(65);
    root->right->left->right = newNode(80);
    root->right->right = newNode(70);
    root->right->right->left = newNode(65);
    root->right->right->right = newNode(80);

    Node *maxNode = NULL;
    int maxSize = largestSubtree(root, maxNode);

    cout << "Largest Subtree is rooted at node "
         << maxNode->data << "\nand its size is "
         << maxSize;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest subtree
// having identical left and right subtree
class GFG
{

/* A binary tree node has data, pointer to left
child and a pointer to right child */
static class Node
{
    int data;
    Node left, right;
};

/* Helper function that allocates a new node with
the given data and null left and right pointers. */
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}
static class string
{
    String str;
}
static int maxSize;
static Node maxNode;

static class pair
{
    int first;
    String second;
    pair(int a, String b)
    {
        first = a;
        second = b;
    }
}

// Sets maxSize to size of largest subtree with
// identical left and right. maxSize is set with
// size of the maximum sized subtree. It returns
// size of subtree rooted with current node. This
// size is used to keep track of maximum size.
static pair largestSubtreeUtil(Node root, String str)
{
    if (root == null)
        return new pair(0, str);

    // string to store structure of left and
    // right subtrees
    String left ="", right="";

    // traverse left subtree and finds its size
    pair ls1 = largestSubtreeUtil(root.left, left);
    left = ls1.second;
    int ls = ls1.first;

    // traverse right subtree and finds its size
    pair rs1 = largestSubtreeUtil(root.right, right);
    right = rs1.second;
    int rs = rs1.first;

    // if left and right subtrees are similar
    // update maximum subtree if needed (Note that
    // left subtree may have a bigger value than
    // right and vice versa)
    int size = ls + rs + 1;
    if (left.equals(right))
    {
    if (size > maxSize)
    {
            maxSize = size;
            maxNode = root;
    }
    }

    // append left subtree data
    str += "|"+left+"|";

    // append current node data
    str += "|"+root.data+"|";

    // append right subtree data
    str += "|"+right+"|";

    return new pair(size, str);
}

// function to find the largest subtree
// having identical left and right subtree
static int largestSubtree(Node node)
{
    maxSize = 0;
    largestSubtreeUtil(node,"");

    return maxSize;
}

/* Driver program to test above functions*/
public static void main(String args[])
{
    /* Let us construct the following Tree
                50
            /     \
            10     60
            / \     / \
            5 20 70 70
                / \ / \
                65 80 65 80 */
    Node root = newNode(50);
    root.left = newNode(10);
    root.right = newNode(60);
    root.left.left = newNode(5);
    root.left.right = newNode(20);
    root.right.left = newNode(70);
    root.right.left.left = newNode(65);
    root.right.left.right = newNode(80);
    root.right.right = newNode(70);
    root.right.right.left = newNode(65);
    root.right.right.right = newNode(80);

    maxNode = null;
    maxSize = largestSubtree(root);

    System.out.println( "Largest Subtree is rooted at node "
        + maxNode.data + "\nand its size is "
        + maxSize);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find the largest subtree
# having identical left and right subtree

# Helper class that allocates a new node
# with the given data and None left and
# right pointers.
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Sets maxSize to size of largest subtree with
# identical left and right. maxSize is set with
# size of the maximum sized subtree. It returns
# size of subtree rooted with current node. This
# size is used to keep track of maximum size.
def largestSubtreeUtil(root, Str,
                       maxSize, maxNode):
    if (root == None):
        return 0

    # string to store structure of left
    # and right subtrees
    left = [""]
    right = [""]

    # traverse left subtree and finds its size
    ls = largestSubtreeUtil(root.left, left,
                            maxSize, maxNode)

    # traverse right subtree and finds its size
    rs = largestSubtreeUtil(root.right, right,
                            maxSize, maxNode)

    # if left and right subtrees are similar
    # update maximum subtree if needed (Note
    # that left subtree may have a bigger
    # value than right and vice versa)
    size = ls + rs + 1
    if (left[0] == right[0]):
        if (size > maxSize[0]):
            maxSize[0] = size
            maxNode[0] = root

    # append left subtree data
    Str[0] = Str[0] + "|" + left[0] + "|"

    # append current node data
    Str[0] = Str[0] + "|" + str(root.data) + "|"

    # append right subtree data
    Str[0] = Str[0] + "|" + right[0] + "|"

    return size

# function to find the largest subtree
# having identical left and right subtree
def largestSubtree(node, maxNode):
    maxSize = [0]
    Str = [""]
    largestSubtreeUtil(node, Str, maxSize,
                                  maxNode)

    return maxSize

# Driver Code
if __name__ == '__main__':

    # Let us construct the following Tree
    #         50
    #         /     \
    #         10     60
    #     / \     / \
    #     5 20 70 70
    #             / \ / \
    #             65 80 65 80
    root = newNode(50)
    root.left = newNode(10)
    root.right = newNode(60)
    root.left.left = newNode(5)
    root.left.right = newNode(20)
    root.right.left = newNode(70)
    root.right.left.left = newNode(65)
    root.right.left.right = newNode(80)
    root.right.right = newNode(70)
    root.right.right.left = newNode(65)
    root.right.right.right = newNode(80)

    maxNode = [None]
    maxSize = largestSubtree(root, maxNode)

    print("Largest Subtree is rooted at node ",
                               maxNode[0].data)
    print("and its size is ", maxSize)

# This code is contributed by PranchalK
```

## C#

```
// C# program to find the largest subtree
// having identical left and right subtree
using System;

class GFG{

// A binary tree node has data, pointer to
// left child and a pointer to right child
public class Node
{
    public int data;
    public Node left, right;
};

// Helper function that allocates a new node
// with the given data and null left and
// right pointers.
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return(node);
}

static int maxSize;
static Node maxNode;

public class pair
{
    public int first;
    public string second;

    public pair(int a, string b)
    {
        first = a;
        second = b;
    }
}

// Sets maxSize to size of largest subtree with
// identical left and right. maxSize is set with
// size of the maximum sized subtree. It returns
// size of subtree rooted with current node. This
// size is used to keep track of maximum size.
static pair largestSubtreeUtil(Node root, string str)
{
    if (root == null)
        return new pair(0, str);

    // String to store structure of left and
    // right subtrees
    string left = "", right = "";

    // Traverse left subtree and finds its size
    pair ls1 = largestSubtreeUtil(root.left, left);
    left = ls1.second;
    int ls = ls1.first;

    // Traverse right subtree and finds its size
    pair rs1 = largestSubtreeUtil(root.right, right);
    right = rs1.second;
    int rs = rs1.first;

    // If left and right subtrees are similar
    // update maximum subtree if needed (Note
    // that left subtree may have a bigger
    // value than right and vice versa)
    int size = ls + rs + 1;

    if (left.Equals(right))
    {
        if (size > maxSize)
        {
            maxSize = size;
            maxNode = root;
        }
    }

    // Append left subtree data
    str += "|" + left + "|";

    // Append current node data
    str += "|" + root.data + "|";

    // Append right subtree data
    str += "|" + right + "|";

    return new pair(size, str);
}

// Function to find the largest subtree
// having identical left and right subtree
static int largestSubtree(Node node)
{
    maxSize = 0;
    largestSubtreeUtil(node, "");

    return maxSize;
}

// Driver code
public static void Main(string []args)
{

    /* Let us construct the following Tree
              50
            /     \
           10     60
           / \     / \
          5  20 70  70
               / \  / \
              65 80 65 80
    */
    Node root = newNode(50);
    root.left = newNode(10);
    root.right = newNode(60);
    root.left.left = newNode(5);
    root.left.right = newNode(20);
    root.right.left = newNode(70);
    root.right.left.left = newNode(65);
    root.right.left.right = newNode(80);
    root.right.right = newNode(70);
    root.right.right.left = newNode(65);
    root.right.right.right = newNode(80);

    maxNode = null;
    maxSize = largestSubtree(root);

    Console.Write("Largest Subtree is rooted at node " +
                  maxNode.data + "\nand its size is " +
                  maxSize);
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>
// Javascript program to find the largest subtree
// having identical left and right subtree

// A binary tree node has data, pointer to
// left child and a pointer to right child
class Node
{
  constructor()
  {
    this.data = 0;
    this.left = null;
    this.right = null;
  }
};

// Helper function that allocates a new node
// with the given data and null left and
// right pointers.
function newNode(data)
{
    var node = new Node();
    node.data = data;
    node.left = node.right = null;
    return(node);
}

var maxSize = 0;
var maxNode = null;

class pair
{
  constructor(a, b)
  {
    this.first = a;
    this.second = b;
  }
}

// Sets maxSize to size of largest subtree with
// identical left and right. maxSize is set with
// size of the maximum sized subtree. It returns
// size of subtree rooted with current node. This
// size is used to keep track of maximum size.
function largestSubtreeUtil(root, str)
{
    if (root == null)
        return new pair(0, str);

    // String to store structure of left and
    // right subtrees
    var left = "", right = "";

    // Traverse left subtree and finds its size
    var ls1 = largestSubtreeUtil(root.left, left);
    left = ls1.second;
    var ls = ls1.first;

    // Traverse right subtree and finds its size
    var rs1 = largestSubtreeUtil(root.right, right);
    right = rs1.second;
    var rs = rs1.first;

    // If left and right subtrees are similar
    // update maximum subtree if needed (Note
    // that left subtree may have a bigger
    // value than right and vice versa)
    var size = ls + rs + 1;

    if (left == right)
    {
        if (size > maxSize)
        {
            maxSize = size;
            maxNode = root;
        }
    }

    // Append left subtree data
    str += "|" + left + "|";

    // Append current node data
    str += "|" + root.data + "|";

    // Append right subtree data
    str += "|" + right + "|";

    return new pair(size, str);
}

// Function to find the largest subtree
// having identical left and right subtree
function largestSubtree(node)
{
    maxSize = 0;
    largestSubtreeUtil(node, "");

    return maxSize;
}

// Driver code
/* Let us construct the following Tree
          50
        /     \
       10     60
       / \     / \
      5  20 70  70
           / \  / \
          65 80 65 80
*/
var root = newNode(50);
root.left = newNode(10);
root.right = newNode(60);
root.left.left = newNode(5);
root.left.right = newNode(20);
root.right.left = newNode(70);
root.right.left.left = newNode(65);
root.right.left.right = newNode(80);
root.right.right = newNode(70);
root.right.right.left = newNode(65);
root.right.right.right = newNode(80);
maxNode = null;
maxSize = largestSubtree(root);
document.write("Largest Subtree is rooted at node " +
              maxNode.data + "<br>and its size is " +
              maxSize);

// This code is contributed by itsok.
</script>
```

**输出:**

```
Largest Subtree is rooted at node 60 
and its size is 7
```

最坏的情况时间复杂度仍然是 O(n <sup>2</sup> )，因为我们需要 O(n)个时间来比较两个字符串。

**进一步优化:**
我们可以使用[二叉树的简洁编码](https://www.geeksforgeeks.org/succinct-encoding-of-binary-tree/)来优化上述程序中使用的空间。

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息