# 查找单值子树的计数

> 原文:[https://www . geeksforgeeks . org/find-单个子树计数/](https://www.geeksforgeeks.org/find-count-of-singly-subtrees/)

给定一棵二叉树，编写一个程序来计算单值子树的数量。单值子树是所有节点具有相同值的子树。预期时间复杂度为 0(n)。
例:

```
Input: root of below tree
              5
             / \
            1   5
           / \   \
          5   5   5
Output: 4
There are 4 subtrees with single values.

Input: root of below tree
              5
             / \
            4   5
           / \   \
          4   4   5                
Output: 5
There are five subtrees with single values.
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
一**简单的解决方法**就是遍历树。对于每个遍历的节点，检查该节点下的所有值是否相同。如果相同，则递增计数。这个解的时间复杂度为 O(n <sup>2</sup> )。
一个**高效的解决方案**是以自下而上的方式遍历树。对于每一个被访问的子树，如果它下面的子树是单值的并且递增计数，则返回 true。因此，我们的想法是在递归调用中使用 count 作为引用参数，并使用返回值来确定左右子树是否是单值的。
以下是以上思路的实现。

## C++

```
// C++ program to find count of single valued subtrees
#include<bits/stdc++.h>
using namespace std;

// A Tree node
struct Node
{
    int data;
    struct Node* left, *right;
};

// Utility function to create a new node
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return (temp);
}

// This function increments count by number of single
// valued subtrees under root. It returns true if subtree
// under root is Singly, else false.
bool countSingleRec(Node* root, int &count)
{
    // Return false to indicate NULL
    if (root == NULL)
       return true;

    // Recursively count in left and right subtrees also
    bool left = countSingleRec(root->left, count);
    bool right = countSingleRec(root->right, count);

    // If any of the subtrees is not singly, then this
    // cannot be singly.
    if (left == false || right == false)
       return false;

    // If left subtree is singly and non-empty, but data
    // doesn't match
    if (root->left && root->data != root->left->data)
        return false;

    // Same for right subtree
    if (root->right && root->data != root->right->data)
        return false;

    // If none of the above conditions is true, then
    // tree rooted under root is single valued, increment
    // count and return true.
    count++;
    return true;
}

// This function mainly calls countSingleRec()
// after initializing count as 0
int countSingle(Node* root)
{
    // Initialize result
    int count = 0;

    // Recursive function to count
    countSingleRec(root, count);

    return count;
}

// Driver program to test
int main()
{
    /* Let us construct the below tree
            5
          /   \
        4      5
      /  \      \
     4    4      5 */
    Node* root        = newNode(5);
    root->left        = newNode(4);
    root->right       = newNode(5);
    root->left->left  = newNode(4);
    root->left->right = newNode(4);
    root->right->right = newNode(5);

    cout << "Count of Single Valued Subtrees is "
         << countSingle(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of single valued subtrees

/* Class containing left and right child of current
 node and key value*/
class Node
{
    int data;
    Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class Count
{
    int count = 0;
}

class BinaryTree
{
    Node root; 
    Count ct = new Count();

    // This function increments count by number of single
    // valued subtrees under root. It returns true if subtree
    // under root is Singly, else false.
    boolean countSingleRec(Node node, Count c)
    {
        // Return false to indicate NULL
        if (node == null)
            return true;

        // Recursively count in left and right subtrees also
        boolean left = countSingleRec(node.left, c);
        boolean right = countSingleRec(node.right, c);

        // If any of the subtrees is not singly, then this
        // cannot be singly.
        if (left == false || right == false)
            return false;

        // If left subtree is singly and non-empty, but data
        // doesn't match
        if (node.left != null && node.data != node.left.data)
            return false;

        // Same for right subtree
        if (node.right != null && node.data != node.right.data)
            return false;

        // If none of the above conditions is true, then
        // tree rooted under root is single valued, increment
        // count and return true.
        c.count++;
        return true;
    }

    // This function mainly calls countSingleRec()
    // after initializing count as 0
    int countSingle()
    {
        return countSingle(root);
    }

    int countSingle(Node node)
    {
        // Recursive function to count
        countSingleRec(node, ct);
        return ct.count;
    }

    // Driver program to test above functions
    public static void main(String args[])
    {
           /* Let us construct the below tree
                5
              /   \
            4      5
          /  \      \
         4    4      5 */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(5);
        tree.root.left = new Node(4);
        tree.root.right = new Node(5);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(4);
        tree.root.right.right = new Node(5);

        System.out.println("The count of single valued sub trees is : "
                                            + tree.countSingle());
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to find the count of single valued subtrees

# Node Structure
class Node:
    # Utility function to create a new node
    def __init__(self ,data):
        self.data = data
        self.left = None
        self.right = None

# This function increments count by number of single
# valued subtrees under root. It returns true if subtree
# under root is Singly, else false.
def countSingleRec(root , count):
    # Return False to indicate None
    if root is None :
        return True

    # Recursively count in left and right subtrees also
    left = countSingleRec(root.left , count)
    right = countSingleRec(root.right , count)

    # If any of the subtrees is not singly, then this
    # cannot be singly
    if left == False or right  == False :
        return False

    # If left subtree is singly and non-empty , but data
    # doesn't match
    if root.left and root.data != root.left.data:
        return False

    # same for right subtree
    if root.right and root.data != root.right.data:
        return False

    # If none of the above conditions is True, then
    # tree rooted under root is single valued,increment
    # count and return true
    count[0] += 1
    return True

# This function mainly class countSingleRec()
# after initializing count as 0
def countSingle(root):
    # initialize result
    count = [0]

    # Recursive function to count
    countSingleRec(root , count)

    return count[0]

# Driver program to test

"""Let us construct the below tree
            5
          /   \
        4       5
       /  \      \
      4    4      5
"""
root = Node(5)
root.left = Node(4)
root.right = Node(5)
root.left.left = Node(4)
root.left.right = Node(4)
root.right.right = Node(5)
countSingle(root)
print "Count of Single Valued Subtrees is" , countSingle(root)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;

// C# program to find count of single valued subtrees

/* Class containing left and right child of current 
 node and key value*/
public class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

public class Count
{
    public int count = 0;
}

public class BinaryTree
{
    public Node root;
    public Count ct = new Count();

    // This function increments count by number of single 
    // valued subtrees under root. It returns true if subtree 
    // under root is Singly, else false.
    public virtual bool countSingleRec(Node node, Count c)
    {
        // Return false to indicate NULL
        if (node == null)
        {
            return true;
        }

        // Recursively count in left and right subtrees also
        bool left = countSingleRec(node.left, c);
        bool right = countSingleRec(node.right, c);

        // If any of the subtrees is not singly, then this
        // cannot be singly.
        if (left == false || right == false)
        {
            return false;
        }

        // If left subtree is singly and non-empty, but data
        // doesn't match
        if (node.left != null && node.data != node.left.data)
        {
            return false;
        }

        // Same for right subtree
        if (node.right != null && node.data != node.right.data)
        {
            return false;
        }

        // If none of the above conditions is true, then
        // tree rooted under root is single valued, increment
        // count and return true.
        c.count++;
        return true;
    }

    // This function mainly calls countSingleRec()
    // after initializing count as 0
    public virtual int countSingle()
    {
        return countSingle(root);
    }

    public virtual int countSingle(Node node)
    {
        // Recursive function to count
        countSingleRec(node, ct);
        return ct.count;
    }

    // Driver program to test above functions
    public static void Main(string[] args)
    {
           /* Let us construct the below tree
                5
              /   \
            4      5
          /  \      \
         4    4      5 */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(5);
        tree.root.left = new Node(4);
        tree.root.right = new Node(5);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(4);
        tree.root.right.right = new Node(5);

        Console.WriteLine("The count of single valued sub trees is : " + tree.countSingle());
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// javascript program to find count of single valued subtrees

/* Class containing left and right child of current
 node and key value*/
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = this.right = null;
    }
}

class Count
{
constructor(){
    this.count = 0;
    }
}

var root; 
    var ct = new Count();

    // This function increments count by number of single
    // valued subtrees under root. It returns true if subtree
    // under root is Singly, else false.
    function countSingleRec( node,  c)
    {
        // Return false to indicate NULL
        if (node == null)
            return true;

        // Recursively count in left and right subtrees also
        var left = countSingleRec(node.left, c);
        var right = countSingleRec(node.right, c);

        // If any of the subtrees is not singly, then this
        // cannot be singly.
        if (left == false || right == false)
            return false;

        // If left subtree is singly and non-empty, but data
        // doesn't match
        if (node.left != null && node.data != node.left.data)
            return false;

        // Same for right subtree
        if (node.right != null && node.data != node.right.data)
            return false;

        // If none of the above conditions is true, then
        // tree rooted under root is single valued, increment
        // count and return true.
        c.count++;
        return true;
    }

    // This function mainly calls countSingleRec()
    // after initializing count as 0
    function countSingle()
    {
        return countSingle(root);
    }

    function countSingle( node)
    {
        // Recursive function to count
        countSingleRec(node, ct);
        return ct.count;
    }

    // Driver program to test above functions

           /* Let us construct the below tree
                5
              /   \
            4      5
          /  \      \
         4    4      5 */

        root = new Node(5);
        root.left = new Node(4);
        root.right = new Node(5);
        root.left.left = new Node(4);
        root.left.right = new Node(4);
        root.right.right = new Node(5);

        document.write("The count of single valued sub trees is : "
                                            + countSingle(root));

// This code contributed by aashish1995
</script>
```

**输出:**

```
Count of Single Valued Subtrees is 5
```

这个解决方案的时间复杂度是 O(n)，其中 n 是给定二叉树中的节点数。

感谢 Gaurav Ahirwar 提出上述解决方案。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。