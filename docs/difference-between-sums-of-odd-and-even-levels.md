# 二叉树奇数层和偶数层节点的和之差

> 原文:[https://www . geeksforgeeks . org/奇数和偶数电平之和之差/](https://www.geeksforgeeks.org/difference-between-sums-of-odd-and-even-levels/)

给定一棵二叉树，求奇数层节点的和与偶数层节点的和之差。将 root 视为 1 级，将 root 的左右子级视为 2 级，以此类推。
例如，在下面的树中，奇数层的节点之和为(5 + 1 + 4 + 8)，为 18。偶数层节点的和为(2 + 6 + 3 + 7 + 9)即 27。以下树的输出应该是 18–27，也就是-9。

```
      5
    /   \
   2     6
 /  \     \  
1    4     8
    /     / \ 
   3     7   9  
```

一个简单明了的方法就是**使用** [**等级顺序遍历**](https://www.geeksforgeeks.org/level-order-tree-traversal/) 。在遍历中，检查当前节点的级别，如果是奇数，用当前节点的数据增加奇数和，否则增加偶数和。最后返回奇数和偶数和的差。该方法的实施见下文。
[C 实现基于层次顺序遍历的方法寻找差异](http://ideone.com/845ZFY)。
此方法由[曼德普·辛格提供。](https://auth.geeksforgeeks.org/user/msdeep14)对于**迭代方法**，只需逐级遍历树(级序遍历)，将偶数级节点值之和存储在 evenSum 中，其余存储在变量 oddSum 中，最后返回差值。
下面是该方法的简单实现。

## C++

```
// CPP program to find
// difference between
// sums of odd level
// and even level nodes
// of binary tree
#include <bits/stdc++.h>
using namespace std;

// tree node
struct Node
{
    int data;
    Node *left, *right;
};

// returns a new
// tree Node
Node* newNode(int data)
{
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// return difference of
// sums of odd level
// and even level
int evenOddLevelDifference(Node* root)
{
    if (!root)
        return 0;

    // create a queue for
    // level order traversal
    queue<Node*> q;
    q.push(root);

    int level = 0;
    int evenSum = 0, oddSum = 0;

    // traverse until the
    // queue is empty
    while (!q.empty())
    {
        int size = q.size();
        level += 1;

        // traverse for
        // complete level
        while(size > 0)
        {
            Node* temp = q.front();
            q.pop();

            // check if level no.
            // is even or odd and
            // accordingly update
            // the evenSum or oddSum
            if(level % 2 == 0)
                evenSum += temp->data;
            else
                oddSum += temp->data;

            // check for left child
            if (temp->left)
            {
                q.push(temp->left);
            }

            // check for right child
            if (temp->right)
            {
                q.push(temp->right);
            }
            size -= 1;
        }
    }

    return (oddSum - evenSum);
}

// driver program
int main()
{
    // construct a tree
    Node* root = newNode(5);
    root->left = newNode(2);
    root->right = newNode(6);
    root->left->left = newNode(1);
    root->left->right = newNode(4);
    root->left->right->left = newNode(3);
    root->right->right = newNode(8);
    root->right->right->right = newNode(9);
    root->right->right->left = newNode(7);

    int result = evenOddLevelDifference(root);
    cout << "difference between sums is :: ";
    cout << result << endl;
    return 0;
}

// This article is contributed by Mandeep Singh.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find 
// difference between 
// sums of odd level 
// and even level nodes 
// of binary tree
import java.io.*;
import java.util.*;
// User defined node class
class Node {
      int data;
      Node left, right;

      // Constructor to create a new tree node
      Node(int key)
      {
           data  = key;
           left = right = null;
      }
}
class GFG {
      // return difference of
      // sums of odd level  and even level
      static int evenOddLevelDifference(Node root)
      {
             if (root == null)
                 return 0;

             // create a queue for
             // level order traversal
             Queue<Node> q = new LinkedList<>();
             q.add(root);

             int level = 0;
             int evenSum = 0, oddSum = 0;

             // traverse until the
             // queue is empty
             while (q.size() != 0) {
                   int size = q.size();
                   level++;

                   // traverse for complete level
                   while (size > 0) {
                          Node temp = q.remove();

                          // check if level no.
                          // is even or odd and
                          // accordingly update
                          // the evenSum or oddSum
                          if (level % 2 == 0)
                              evenSum += temp.data;
                          else
                              oddSum += temp.data;

                          // check for left child
                          if (temp.left != null)
                              q.add(temp.left);

                          // check for right child
                          if (temp.right != null)
                              q.add(temp.right);
                          size--;
                   }
             }
             return (oddSum - evenSum); 
      }

      // Driver code
      public static void main(String args[])
      {
             // construct a tree
             Node root = new Node(5);
             root.left = new Node(2);
             root.right = new Node(6);
             root.left.left = new Node(1);
             root.left.right = new Node(4);
             root.left.right.left = new Node(3);
             root.right.right = new Node(8);
             root.right.right.right = new Node(9);
             root.right.right.left = new Node(7);

             System.out.println("difference between sums is " +
                                evenOddLevelDifference(root));
      }
}
// This code is contributed by rachana soma
```

## 蟒蛇 3

```
# Python3 program to find maximum product
# of a level in Binary Tree

# Helper function that allocates a new
# node with the given data and None
# left and right poers.                                    
class newNode:

    # Construct to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# return difference of sums of odd
# level and even level
def evenOddLevelDifference(root):

    if (not root):
        return 0

    # create a queue for
    # level order traversal
    q = []
    q.append(root)

    level = 0
    evenSum = 0
    oddSum = 0

    # traverse until the queue is empty
    while (len(q)):

        size = len(q)
        level += 1

        # traverse for complete level
        while(size > 0):

            temp = q[0] #.front()
            q.pop(0)

            # check if level no. is even or
            # odd and accordingly update
            # the evenSum or oddSum
            if(level % 2 == 0):
                evenSum += temp.data
            else:
                oddSum += temp.data

            # check for left child
            if (temp.left) :

                q.append(temp.left)

            # check for right child
            if (temp.right):

                q.append(temp.right)

            size -= 1

    return (oddSum - evenSum)

# Driver Code
if __name__ == '__main__':

    """
    Let us create Binary Tree shown
    in above example """
    root = newNode(5)
    root.left = newNode(2)
    root.right = newNode(6)
    root.left.left = newNode(1)
    root.left.right = newNode(4)
    root.left.right.left = newNode(3)
    root.right.right = newNode(8)
    root.right.right.right = newNode(9)
    root.right.right.left = newNode(7)

    result = evenOddLevelDifference(root)
    print("Difference between sums is", result)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to find
// difference between
// sums of odd level
// and even level nodes
// of binary tree
using System;
using System.Collections.Generic;

// User defined node class
public class Node
{
    public int data;
    public Node left, right;

    // Constructor to create a new tree node
    public Node(int key)
    {
        data = key;
        left = right = null;
    }
}

public class GFG
{
    // return difference of
    // sums of odd level and even level
    static int evenOddLevelDifference(Node root)
    {
            if (root == null)
                return 0;

            // create a queue for
            // level order traversal
            Queue<Node> q = new Queue<Node>();
            q.Enqueue(root);

            int level = 0;
            int evenSum = 0, oddSum = 0;

            // traverse until the
            // queue is empty
            while (q.Count != 0)
            {
                int size = q.Count;
                level++;

                // traverse for complete level
                while (size > 0)
                {
                        Node temp = q.Dequeue();

                        // check if level no.
                        // is even or odd and
                        // accordingly update
                        // the evenSum or oddSum
                        if (level % 2 == 0)
                            evenSum += temp.data;
                        else
                            oddSum += temp.data;

                        // check for left child
                        if (temp.left != null)
                            q.Enqueue(temp.left);

                        // check for right child
                        if (temp.right != null)
                            q.Enqueue(temp.right);
                        size--;
                }
            }
            return (oddSum - evenSum);
    }

    // Driver code
    public static void Main(String []args)
    {
            // construct a tree
            Node root = new Node(5);
            root.left = new Node(2);
            root.right = new Node(6);
            root.left.left = new Node(1);
            root.left.right = new Node(4);
            root.left.right.left = new Node(3);
            root.right.right = new Node(8);
            root.right.right.right = new Node(9);
            root.right.right.left = new Node(7);

            Console.WriteLine("difference between sums is " +
                                evenOddLevelDifference(root));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find 
// difference between 
// sums of odd level 
// and even level nodes 
// of binary tree

// User defined node class
class Node
{
    constructor(key)
    {
        this.data  = key;
        this.left = this.right = null;
    }
}

 // return difference of
      // sums of odd level  and even level
function evenOddLevelDifference(root)
{
    if (root == null)
                 return 0;

             // create a queue for
             // level order traversal
             let q = [];
             q.push(root);

             let level = 0;
             let evenSum = 0, oddSum = 0;

             // traverse until the
             // queue is empty
             while (q.length != 0) {
                   let size = q.length;
                   level++;

                   // traverse for complete level
                   while (size > 0) {
                          let temp = q.shift();

                          // check if level no.
                          // is even or odd and
                          // accordingly update
                          // the evenSum or oddSum
                          if (level % 2 == 0)
                              evenSum += temp.data;
                          else
                              oddSum += temp.data;

                          // check for left child
                          if (temp.left != null)
                              q.push(temp.left);

                          // check for right child
                          if (temp.right != null)
                              q.push(temp.right);
                          size--;
                   }
             }
             return (oddSum - evenSum); 
}

 // Driver code
let root = new Node(5);
             root.left = new Node(2);
             root.right = new Node(6);
             root.left.left = new Node(1);
             root.left.right = new Node(4);
             root.left.right.left = new Node(3);
             root.right.right = new Node(8);
             root.right.right.right = new Node(9);
             root.right.right.left = new Node(7);

             document.write("difference between sums is " +
                                evenOddLevelDifference(root)+"<br>");

// This code is contributed by rag2127
</script>
```

**输出:**

```
difference between sums is -9
```

问题也可以通过简单的递归遍历来解决**。我们可以递归计算所需的差值，即根数据的值减去左子树和右子树的差值。
以下是本办法的实施情况。** 

## C++

```
// A recursive program to find difference
// between sum of nodes at odd level
// and sum at even level
#include <bits/stdc++.h>
using namespace std;

// Binary Tree node
class node
{
    public:
    int data;
    node* left, *right;
};

// A utility function to allocate
// a new tree node with given data
node* newNode(int data)
{
    node* Node = new node();
    Node->data = data;
    Node->left = Node->right = NULL;
    return (Node);
}

// The main function that return
// difference between odd and even
// level nodes
int getLevelDiff(node *root)
{
// Base case
if (root == NULL)
        return 0;

// Difference for root is root's data - difference for
// left subtree - difference for right subtree
return root->data - getLevelDiff(root->left) -
                    getLevelDiff(root->right);
}

// Driver code
int main()
{
    node *root = newNode(5);
    root->left = newNode(2);
    root->right = newNode(6);
    root->left->left = newNode(1);
    root->left->right = newNode(4);
    root->left->right->left = newNode(3);
    root->right->right = newNode(8);
    root->right->right->right = newNode(9);
    root->right->right->left = newNode(7);
    cout<<getLevelDiff(root)<<" is the required difference\n";
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// A recursive program to find difference between sum of nodes at
// odd level and sum at even level
#include <stdio.h>
#include <stdlib.h>

// Binary Tree node
struct node
{
    int data;
    struct node* left, *right;
};

// A utility function to allocate a new tree node with given data
struct node* newNode(int data)
{
    struct node* node = (struct node*)malloc(sizeof(struct node));
    node->data = data;
    node->left =  node->right = NULL;
    return (node);
}

// The main function that return difference between odd and even level
// nodes
int getLevelDiff(struct node *root)
{
   // Base case
   if (root == NULL)
         return 0;

   // Difference for root is root's data - difference for
   // left subtree - difference for right subtree
   return root->data - getLevelDiff(root->left) -
                                         getLevelDiff(root->right);
}

// Driver program to test above functions
int main()
{
    struct node *root = newNode(5);
    root->left = newNode(2);
    root->right = newNode(6);
    root->left->left  = newNode(1);
    root->left->right = newNode(4);
    root->left->right->left = newNode(3);
    root->right->right = newNode(8);
    root->right->right->right = newNode(9);
    root->right->right->left = newNode(7);
    printf("%d is the required difference\n", getLevelDiff(root));
    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A recursive java program to find difference between sum of nodes at
// odd level and sum at even level

// A binary tree node
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right;
    }
}

class BinaryTree
{
    // The main function that return difference between odd and even level
    // nodes
    Node root;

    int getLevelDiff(Node node)
    {
        // Base case
        if (node == null)
            return 0;

        // Difference for root is root's data - difference for
        // left subtree - difference for right subtree
        return node.data - getLevelDiff(node.left) -
                                              getLevelDiff(node.right);
    }

    // Driver program to test above functions
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(5);
        tree.root.left = new Node(2);
        tree.root.right = new Node(6);
        tree.root.left.left = new Node(1);
        tree.root.left.right = new Node(4);
        tree.root.left.right.left = new Node(3);
        tree.root.right.right = new Node(8);
        tree.root.right.right.right = new Node(9);
        tree.root.right.right.left = new Node(7);
        System.out.println(tree.getLevelDiff(tree.root) + 
                                             " is the required difference");

    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# A recursive program to find difference between sum of nodes
# at odd level and sum at even level

# A Binary Tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# The main function that returns difference between odd and
# even level nodes
def getLevelDiff(root):

    # Base Case
    if root is None:
        return 0

    # Difference for root is root's data - difference for
    # left subtree - difference for right subtree
    return (root.data - getLevelDiff(root.left)-
        getLevelDiff(root.right))

# Driver program to test above function
root = Node(5)
root.left = Node(2)
root.right = Node(6)
root.left.left = Node(1)
root.left.right = Node(4)
root.left.right.left = Node(3)
root.right.right = Node(8)
root.right.right.right = Node(9)
root.right.right.left = Node(7)
print "%d is the required difference" %(getLevelDiff(root))

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;

// A recursive C# program to find
// difference between sum of nodes at
// odd level and sum at even level

// A binary tree node
public class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right;
    }
}

public class BinaryTree
{
    // The main function that return difference
    // between odd and even level nodes
    public Node root;

    public virtual int getLevelDiff(Node node)
    {
        // Base case
        if (node == null)
        {
            return 0;
        }

        // Difference for root is root's
        // data - difference for left subtree
        //  - difference for right subtree
        return node.data - getLevelDiff(node.left)
                        - getLevelDiff(node.right);
    }

    // Driver program to test above functions
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(5);
        tree.root.left = new Node(2);
        tree.root.right = new Node(6);
        tree.root.left.left = new Node(1);
        tree.root.left.right = new Node(4);
        tree.root.left.right.left = new Node(3);
        tree.root.right.right = new Node(8);
        tree.root.right.right.right = new Node(9);
        tree.root.right.right.left = new Node(7);
        Console.WriteLine(tree.getLevelDiff(tree.root)
                        + " is the required difference");

    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// A recursive javascript program to find difference between sum of nodes at
// odd level and sum at even level

// A binary tree node
class Node
{
    constructor(item)
    {
        this.data = item;
        this.left = this.right = null;
    }
}

// The main function that return difference between odd and even level
    // nodes
let root;

function getLevelDiff(node)
{

    // Base case
        if (node == null)
            return 0;

        // Difference for root is root's data - difference for
        // left subtree - difference for right subtree
        return node.data - getLevelDiff(node.left) -
                                              getLevelDiff(node.right);
}

// Driver program to test above functions
root = new Node(5);
root.left = new Node(2);
root.right = new Node(6);
root.left.left = new Node(1);
root.left.right = new Node(4);
root.left.right.left = new Node(3);
root.right.right = new Node(8);
root.right.right.right = new Node(9);
root.right.right.left = new Node(7);
document.write(getLevelDiff(root) +
                   " is the required difference");

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
-9 is the required difference
```

两种方法的时间复杂度都是 O(n)，但第二种方法简单易实现。

本文由 [**钱德拉·普拉卡什**](https://www.facebook.com/chandra.prakash.52643?fref=ts) 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。