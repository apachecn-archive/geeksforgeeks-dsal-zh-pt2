# 通过节点求和(递归和迭代)合并两个二叉树

> 原文:[https://www . geesforgeks . org/merge-two-二叉树-node-sum/](https://www.geeksforgeeks.org/merge-two-binary-trees-node-sum/)

给定两个二叉树。我们需要把它们合并成一棵新的二叉树。合并规则是，如果两个节点重叠，则将节点值相加，作为合并节点的新值。否则，非空节点将被用作新树的节点。

**示例:**

```
Input: 
     Tree 1            Tree 2                  
       2                 3                             
      / \               / \                            
     1   4             6   1                        
    /                   \   \                      
   5                     2   7                  

Output: Merged tree:
         5
        / \
       7   5
      / \   \ 
     5   2   7
```

注意:合并过程必须从两棵树的根节点开始。

**递归算法:**

1.  以有序的方式遍历树
2.  检查两个树节点是否都为空
    1.  如果没有，则更新该值
3.  左侧子树重复出现
4.  右子树重复出现
5.  返回更新树的根

## C++

```
// C++ program to Merge Two Binary Trees
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct Node
{
    int data;
    struct Node *left, *right;
};

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
Node *newNode(int data)
{
    Node *new_node = new Node;
    new_node->data = data;
    new_node->left = new_node->right = NULL;
    return new_node;
}

/* Given a binary tree, print its nodes in inorder*/
void inorder(Node * node)
{
    if (!node)
        return;

    /* first recur on left child */
    inorder(node->left);

    /* then print the data of node */
    printf("%d ", node->data);

    /* now recur on right child */
    inorder(node->right);
}

/* Function to merge given two binary trees*/
Node *MergeTrees(Node * t1, Node * t2)
{
    if (!t1)
        return t2;
    if (!t2)
        return t1;
    t1->data += t2->data;
    t1->left = MergeTrees(t1->left, t2->left);
    t1->right = MergeTrees(t1->right, t2->right);
    return t1;
}

// Driver code
int main()
{
    /* Let us construct the first Binary Tree
            1
          /   \
         2     3
        / \     \
       4   5     6
    */

    Node *root1 = newNode(1);
    root1->left = newNode(2);
    root1->right = newNode(3);
    root1->left->left = newNode(4);
    root1->left->right = newNode(5);
    root1->right->right = newNode(6);

    /* Let us construct the second Binary Tree
           4
         /   \
        1     7
       /     /  \
      3     2    6   */
    Node *root2 = newNode(4);
    root2->left = newNode(1);
    root2->right = newNode(7);
    root2->left->left = newNode(3);
    root2->right->left = newNode(2);
    root2->right->right = newNode(6);

    Node *root3 = MergeTrees(root1, root2);
    printf("The Merged Binary Tree is:\n");
    inorder(root3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Merge Two Binary Trees

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
class Node
{
    int data;
    Node left, right;

    public Node(int data, Node left, Node right) {
        this.data = data;
        this.left = left;
        this.right = right;
    }

     /* Helper method that allocates a new node with the
     given data and NULL left and right pointers. */
     static Node newNode(int data)
     {
         return new Node(data, null, null);
     }

     /* Given a binary tree, print its nodes in inorder*/
     static void inorder(Node node)
     {
         if (node == null)
             return;

         /* first recur on left child */
         inorder(node.left);

         /* then print the data of node */
         System.out.printf("%d ", node.data);

         /* now recur on right child */
         inorder(node.right);
     }

     /* Method to merge given two binary trees*/
     static Node MergeTrees(Node t1, Node t2)
     {
         if (t1 == null)
             return t2;
         if (t2 == null)
             return t1;
         t1.data += t2.data;
         t1.left = MergeTrees(t1.left, t2.left);
         t1.right = MergeTrees(t1.right, t2.right);
         return t1;
     }

     // Driver method
     public static void main(String[] args)
     {
         /* Let us construct the first Binary Tree
                 1
               /   \
              2     3
             / \     \
            4   5     6
         */

         Node root1 = newNode(1);
         root1.left = newNode(2);
         root1.right = newNode(3);
         root1.left.left = newNode(4);
         root1.left.right = newNode(5);
         root1.right.right = newNode(6);

         /* Let us construct the second Binary Tree
                4
              /   \
             1     7
            /     /  \
           3     2    6   */
         Node root2 = newNode(4);
         root2.left = newNode(1);
         root2.right = newNode(7);
         root2.left.left = newNode(3);
         root2.right.left = newNode(2);
         root2.right.right = newNode(6);

         Node root3 = MergeTrees(root1, root2);
         System.out.printf("The Merged Binary Tree is:\n");
         inorder(root3);
     }
}
// This code is contributed by Gaurav Miglani
```

## 蟒蛇 3

```
# Python3 program to Merge Two Binary Trees

# Helper class that allocates a new node
# with the given data and None left and
# right pointers.
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Given a binary tree, prints nodes
# in inorder
def inorder(node):
    if (not node):
        return

    # first recur on left child
    inorder(node.left)

    # then print the data of node
    print(node.data, end = " ")

    # now recur on right child
    inorder(node.right)

# Function to merge given two
# binary trees
def MergeTrees(t1, t2):
    if (not t1):
        return t2
    if (not t2):
        return t1
    t1.data += t2.data
    t1.left = MergeTrees(t1.left, t2.left)
    t1.right = MergeTrees(t1.right, t2.right)
    return t1

# Driver code
if __name__ == '__main__':

    # Let us construct the first Binary Tree
    #     1
    #     / \
    #     2     3
    # / \     \
    # 4 5     6
    root1 = newNode(1)
    root1.left = newNode(2)
    root1.right = newNode(3)
    root1.left.left = newNode(4)
    root1.left.right = newNode(5)
    root1.right.right = newNode(6)

    # Let us construct the second Binary Tree
    #     4
    #     / \
    # 1     7
    # /     / \
    # 3     2 6
    root2 = newNode(4)
    root2.left = newNode(1)
    root2.right = newNode(7)
    root2.left.left = newNode(3)
    root2.right.left = newNode(2)
    root2.right.right = newNode(6)

    root3 = MergeTrees(root1, root2)
    print("The Merged Binary Tree is:")
    inorder(root3)

# This code is contributed by PranchalK
```

## C#

```
// C# program to Merge Two Binary Trees
using System;

/* A binary tree node has data, pointer
to left child and a pointer to right child */
public class Node
{
public int data;
public Node left, right;

public Node(int data, Node left,
                      Node right)
{
    this.data = data;
    this.left = left;
    this.right = right;
}

/* Helper method that allocates a new
node with the given data and NULL left
and right pointers. */
public static Node newNode(int data)
{
    return new Node(data, null, null);
}

/* Given a binary tree, print its
   nodes in inorder*/
public static void inorder(Node node)
{
    if (node == null)
    {
        return;
    }

    /* first recur on left child */
    inorder(node.left);

    /* then print the data of node */
    Console.Write("{0:D} ", node.data);

    /* now recur on right child */
    inorder(node.right);
}

/* Method to merge given two binary trees*/
public static Node MergeTrees(Node t1, Node t2)
{
    if (t1 == null)
    {
        return t2;
    }
    if (t2 == null)
    {
        return t1;
    }
    t1.data += t2.data;
    t1.left = MergeTrees(t1.left, t2.left);
    t1.right = MergeTrees(t1.right, t2.right);
    return t1;
}

// Driver Code
public static void Main(string[] args)
{
    /* Let us construct the first Binary Tree
            1
        / \
        2     3
        / \     \
        4 5     6
    */

    Node root1 = newNode(1);
    root1.left = newNode(2);
    root1.right = newNode(3);
    root1.left.left = newNode(4);
    root1.left.right = newNode(5);
    root1.right.right = newNode(6);

    /* Let us construct the second Binary Tree
            4
        / \
        1     7
        /     / \
    3     2 6 */
    Node root2 = newNode(4);
    root2.left = newNode(1);
    root2.right = newNode(7);
    root2.left.left = newNode(3);
    root2.right.left = newNode(2);
    root2.right.right = newNode(6);

    Node root3 = MergeTrees(root1, root2);
    Console.Write("The Merged Binary Tree is:\n");
    inorder(root3);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to Merge Two Binary Trees
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

// Helper method that allocates a new
// node with the given data and NULL
// left and right pointers.
function newNode(data)
{
    return new Node(data);
}

// Given a binary tree, print its
// nodes in inorder
function inorder(node)
{
    if (node == null)
        return;

    // First recur on left child
    inorder(node.left);

    // Then print the data of node
    document.write(node.data + " ");

    // Now recur on right child
    inorder(node.right);
}

// Method to merge given two binary trees
function MergeTrees(t1, t2)
{
    if (t1 == null)
        return t2;
    if (t2 == null)
        return t1;

    t1.data += t2.data;
    t1.left = MergeTrees(t1.left, t2.left);
    t1.right = MergeTrees(t1.right, t2.right);
    return t1;
}

// Driver code
/* Let us construct the first Binary Tree
             1
           /   \
          2     3
         / \     \
        4   5     6
     */
let root1 = newNode(1);
root1.left = newNode(2);
root1.right = newNode(3);
root1.left.left = newNode(4);
root1.left.right = newNode(5);
root1.right.right = newNode(6);

/* Let us construct the second Binary Tree
              4
            /   \
           1     7
          /     /  \
         3     2    6   */
let root2 = newNode(4);
root2.left = newNode(1);
root2.right = newNode(7);
root2.left.left = newNode(3);
root2.right.left = newNode(2);
root2.right.right = newNode(6);

let root3 = MergeTrees(root1, root2);
document.write("The Merged Binary Tree is:" + "</br>");
inorder(root3);

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
The Merged Binary Tree is:
7 3 5 5 2 10 12
```

**复杂度分析:**

*   时间复杂度:O(n)
    总共需要遍历 n 个节点。这里，n 代表两个给定树的最小节点数。
*   辅助空间:O(n)
    在树倾斜的情况下，递归树的深度可以达到。一般情况下，深度为 0(对数)。

**迭代算法:**

1.  创建堆栈
2.  将两个树的根节点推到堆栈上。
3.  当堆栈不为空时，执行以下步骤:
    1.  从堆栈顶部弹出一个节点对
    2.  对于移除的每个节点对，添加对应于两个节点的值，并更新第一个树中对应节点的值
    3.  如果第一个树的左子树存在，将两个树的左子树(对)推到堆栈上。
    4.  如果第一棵树的左子树不存在，则将第二棵树的左子树追加到第一棵树的当前节点
    5.  对正确的孩子也要这样做。
    6.  如果两个当前节点都为空，则继续从堆栈中弹出下一个节点。
4.  返回更新树的根

## C++

```
// C++ program to Merge Two Binary Trees
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
struct Node
{
    int data;
    struct Node *left, *right;
};

// Structure to store node pair onto stack
struct snode
{
    Node *l, *r;
};

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
Node *newNode(int data)
{
    Node *new_node = new Node;
    new_node->data = data;
    new_node->left = new_node->right = NULL;
    return new_node;
}

/* Given a binary tree, print its nodes in inorder*/
void inorder(Node * node)
{
    if (! node)
        return;

    /* first recur on left child */
    inorder(node->left);

    /* then print the data of node */
    printf("%d ", node->data);

    /* now recur on right child */
    inorder(node->right);
}

/* Function to merge given two binary trees*/

Node* MergeTrees(Node* t1, Node* t2)
{
    if (! t1)
        return t2;
    if (! t2)
        return t1;
    stack<snode> s;
    snode temp;
    temp.l = t1;
    temp.r = t2;
    s.push(temp);
    snode n;
    while (! s.empty())
    {
        n = s.top();
        s.pop();
        if (n.l == NULL|| n.r == NULL)
            continue;
        n.l->data += n.r->data;
        if (n.l->left == NULL)
            n.l->left = n.r->left;
        else
        {
            snode t;
            t.l = n.l->left;
            t.r = n.r->left;
            s.push(t);
        }
        if (n.l->right == NULL)
            n.l->right = n.r->right;
        else
        {
            snode t;
            t.l = n.l->right;
            t.r = n.r->right;
            s.push(t);
        }
    }
    return t1;
}

// Driver code
int main()
{
    /* Let us construct the first Binary Tree
            1
          /   \
         2     3
        / \     \
       4   5     6
    */

    Node *root1 = newNode(1);
    root1->left = newNode(2);
    root1->right = newNode(3);
    root1->left->left = newNode(4);
    root1->left->right = newNode(5);
    root1->right->right = newNode(6);

    /* Let us construct the second Binary Tree
           4
         /   \
        1     7
       /     /  \
      3     2    6   */
    Node *root2 = newNode(4);
    root2->left = newNode(1);
    root2->right = newNode(7);
    root2->left->left = newNode(3);
    root2->right->left = newNode(2);
    root2->right->right = newNode(6);

    Node *root3 = MergeTrees(root1, root2);
    printf("The Merged Binary Tree is:\n");
    inorder(root3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Merge Two Binary Trees
import java.util.*;

class GFG{

/* A binary tree node has data, pointer to left child
and a pointer to right child */
static class Node
{
    int data;
    Node left, right;
};

// Structure to store node pair onto stack
static class snode
{
    Node l, r;
};

/* Helper function that allocates a new node with the
given data and null left and right pointers. */
static Node newNode(int data)
{
    Node new_node = new Node();
    new_node.data = data;
    new_node.left = new_node.right = null;
    return new_node;
}

/* Given a binary tree, print its nodes in inorder*/
static void inorder(Node  node)
{
    if (node == null)
        return;

    /* first recur on left child */
    inorder(node.left);

    /* then print the data of node */
    System.out.printf("%d ", node.data);

    /* now recur on right child */
    inorder(node.right);
}

/* Function to merge given two binary trees*/

static Node MergeTrees(Node t1, Node t2)
{
    if ( t1 == null)
        return t2;
    if ( t2 == null)
        return t1;
    Stack<snode> s = new Stack<>();
    snode temp = new snode();
    temp.l = t1;
    temp.r = t2;
    s.add(temp);
    snode n;
    while (! s.isEmpty())
    {
        n = s.peek();
        s.pop();
        if (n.l == null|| n.r == null)
            continue;
        n.l.data += n.r.data;
        if (n.l.left == null)
            n.l.left = n.r.left;
        else
        {
            snode t = new snode();
            t.l = n.l.left;
            t.r = n.r.left;
            s.add(t);
        }
        if (n.l.right == null)
            n.l.right = n.r.right;
        else
        {
            snode t = new snode();
            t.l = n.l.right;
            t.r = n.r.right;
            s.add(t);
        }
    }
    return t1;
}

// Driver code
public static void main(String[] args)
{
    /* Let us construct the first Binary Tree
            1
          /   \
         2     3
        / \     \
       4   5     6
    */

    Node root1 = newNode(1);
    root1.left = newNode(2);
    root1.right = newNode(3);
    root1.left.left = newNode(4);
    root1.left.right = newNode(5);
    root1.right.right = newNode(6);

    /* Let us construct the second Binary Tree
           4
         /   \
        1     7
       /     /  \
      3     2    6   */
    Node root2 = newNode(4);
    root2.left = newNode(1);
    root2.right = newNode(7);
    root2.left.left = newNode(3);
    root2.right.left = newNode(2);
    root2.right.right = newNode(6);

    Node root3 = MergeTrees(root1, root2);
    System.out.printf("The Merged Binary Tree is:\n");
    inorder(root3);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to Merge Two Binary Trees

''' A binary tree node has data, pointer to left child
and a pointer to right child '''
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Structure to store node pair onto stack
class snode:

    def __init__(self, l, r):

        self.l = l
        self.r = r

''' Helper function that allocates a new node with the
given data and None left and right pointers. '''
def newNode(data):

    new_node = Node(data)
    return new_node

''' Given a binary tree, print its nodes in inorder'''
def inorder(node):

    if (not node):
        return;

    ''' first recur on left child '''
    inorder(node.left);

    ''' then print the data of node '''
    print(node.data, end=' ');

    ''' now recur on right child '''
    inorder(node.right);

''' Function to merge given two binary trees'''

def MergeTrees(t1, t2):

    if (not t1):
        return t2;
    if (not t2):
        return t1;
    s = []

    temp = snode(t1, t2)

    s.append(temp);
    n = None

    while (len(s) != 0):

        n = s[-1]
        s.pop();

        if (n.l == None or n.r == None):
            continue;

        n.l.data += n.r.data;
        if (n.l.left == None):
            n.l.left = n.r.left;
        else:
            t=snode(n.l.left, n.r.left)
            s.append(t);

        if (n.l.right == None):
            n.l.right = n.r.right;
        else:

            t=snode(n.l.right, n.r.right)
            s.append(t);

    return t1;

# Driver code
if __name__=='__main__':

    ''' Let us construct the first Binary Tree
            1
          /   \
         2     3
        / \     \
       4   5     6
    '''

    root1 = newNode(1);
    root1.left = newNode(2);
    root1.right = newNode(3);
    root1.left.left = newNode(4);
    root1.left.right = newNode(5);
    root1.right.right = newNode(6);

    ''' Let us construct the second Binary Tree
           4
         /   \
        1     7
       /     /  \
      3     2    6   '''

    root2 = newNode(4);
    root2.left = newNode(1);
    root2.right = newNode(7);
    root2.left.left = newNode(3);
    root2.right.left = newNode(2);
    root2.right.right = newNode(6);

    root3 = MergeTrees(root1, root2);
    print("The Merged Binary Tree is:");
    inorder(root3);

# This code is contributed by rutvik76
```

## C#

```
// C# program to Merge Two Binary Trees
using System;
using System.Collections.Generic;

class GFG{

// A binary tree node has data, pointer
// to left child and a pointer to right
// child
public class Node
{
    public int data;
    public Node left, right;
};

// Structure to store node pair onto stack
public class snode
{
    public Node l, r;
};

// Helper function that allocates a new
// node with the given data and null
// left and right pointers.
static Node newNode(int data)
{
    Node new_node = new Node();
    new_node.data = data;
    new_node.left = new_node.right = null;
    return new_node;
}

// Given a binary tree, print its
// nodes in inorder
static void inorder(Node  node)
{
    if (node == null)
        return;

    // First recur on left child
    inorder(node.left);

    // Then print the data of node
    Console.Write(node.data + " ");

    // Now recur on right child
    inorder(node.right);
}

// Function to merge given two binary trees
static Node MergeTrees(Node t1, Node t2)
{
    if ( t1 == null)
        return t2;
    if ( t2 == null)
        return t1;

    Stack<snode> s = new Stack<snode>();
    snode temp = new snode();
    temp.l = t1;
    temp.r = t2;
    s.Push(temp);
    snode n;

    while (s.Count != 0)
    {
        n = s.Peek();
        s.Pop();

        if (n.l == null|| n.r == null)
            continue;

        n.l.data += n.r.data;

        if (n.l.left == null)
            n.l.left = n.r.left;
        else
        {
            snode t = new snode();
            t.l = n.l.left;
            t.r = n.r.left;
            s.Push(t);
        }

        if (n.l.right == null)
            n.l.right = n.r.right;
        else
        {
            snode t = new snode();
            t.l = n.l.right;
            t.r = n.r.right;
            s.Push(t);
        }
    }
    return t1;
}

// Driver code
public static void Main(String[] args)
{
    /* Let us construct the first Binary Tree
            1
          /   \
         2     3
        / \     \
       4   5     6
    */
    Node root1 = newNode(1);
    root1.left = newNode(2);
    root1.right = newNode(3);
    root1.left.left = newNode(4);
    root1.left.right = newNode(5);
    root1.right.right = newNode(6);

    /* Let us construct the second Binary Tree
           4
         /   \
        1     7
       /     /  \
      3     2    6   */
    Node root2 = newNode(4);
    root2.left = newNode(1);
    root2.right = newNode(7);
    root2.left.left = newNode(3);
    root2.right.left = newNode(2);
    root2.right.right = newNode(6);

    Node root3 = MergeTrees(root1, root2);

    Console.Write("The Merged Binary Tree is:\n");

    inorder(root3);
}
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

// JavaScript program to Merge Two Binary Trees

/* A binary tree node has data, pointer to left child
and a pointer to right child */
class Node
{
    constructor()
    {
        this.data=0;
        this.left=this.right=null;
    }
}

// Structure to store node pair onto stack
class snode
{
    constructor()
    {
        this.l=null;
        this.r=null;
    }
}

/* Helper function that allocates a new node with the
given data and null left and right pointers. */
function newNode(data)
{
    let new_node = new Node();
    new_node.data = data;
    new_node.left = new_node.right = null;
    return new_node;
}

/* Given a binary tree, print its nodes in inorder*/
function inorder(node)
{
    if (node == null)
        return;

    /* first recur on left child */
    inorder(node.left);

    /* then print the data of node */
    document.write(node.data+" ");

    /* now recur on right child */
    inorder(node.right);
}

/* Function to merge given two binary trees*/
function MergeTrees(t1,t2)
{
    if ( t1 == null)
        return t2;
    if ( t2 == null)
        return t1;
    let s = [];
    let temp = new snode();
    temp.l = t1;
    temp.r = t2;
    s.push(temp);
    let n;
    while ( s.length!=0)
    {
        n = s.pop();

        if (n.l == null|| n.r == null)
            continue;
        n.l.data += n.r.data;
        if (n.l.left == null)
            n.l.left = n.r.left;
        else
        {
            let t = new snode();
            t.l = n.l.left;
            t.r = n.r.left;
            s.push(t);
        }
        if (n.l.right == null)
            n.l.right = n.r.right;
        else
        {
            let t = new snode();
            t.l = n.l.right;
            t.r = n.r.right;
            s.push(t);
        }
    }
    return t1;
}

// Driver code
/* Let us construct the first Binary Tree
            1
          /   \
         2     3
        / \     \
       4   5     6
    */

let root1 = newNode(1);
root1.left = newNode(2);
root1.right = newNode(3);
root1.left.left = newNode(4);
root1.left.right = newNode(5);
root1.right.right = newNode(6);

/* Let us construct second Binary Tree
           4
         /   \
        1     7
       /     /  \
      3     2    6   */
let root2 = newNode(4);
root2.left = newNode(1);
root2.right = newNode(7);
root2.left.left = newNode(3);
root2.right.left = newNode(2);
root2.right.right = newNode(6);

let root3 = MergeTrees(root1, root2);
document.write("The Merged Binary Tree is:<br>");
inorder(root3);

// This code is contributed by unknown2108

</script>
```

**输出:**

```
The Merged Binary Tree is:
7 3 5 5 2 10 12
```

**复杂度分析:**

*   时间复杂度:O(n)
    总共需要遍历 n 个节点。这里，n 代表两个给定树的最小节点数。
*   辅助空间:O(n)
    在树倾斜的情况下，堆栈的深度可以达到 n。

本文由 **Aakash Pal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。