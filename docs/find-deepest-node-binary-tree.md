# 找到二叉树中最深的节点

> 原文:[https://www . geesforgeks . org/find-deep-node-二叉树/](https://www.geeksforgeeks.org/find-deepest-node-binary-tree/)

给定一棵二叉树，找到其中最深的节点。
**例:**

```
Input : Root of below tree
            1
          /   \
         2      3
        / \    / \ 
       4   5  6   7
                   \
                    8
Output : 8

Input : Root of below tree
            1
          /   \
         2      3
               / 
              6  
Output : 6
```

**方法 1:** 思想是对给定的二叉树进行有序遍历。在进行有序遍历时，我们也传递当前节点的级别。我们记录到目前为止看到的最大水平和到目前为止看到的最深节点的值。

## C++

```
// A C++ program to find value of the deepest node
// in a given binary tree
#include <bits/stdc++.h>
using namespace std;

// A tree node
struct Node
{
    int data;
    struct Node *left, *right;
};

// Utility function to create a new node
Node *newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// maxLevel : keeps track of maximum level seen so far.
// res :  Value of deepest node so far.
// level : Level of root
void find(Node *root, int level, int &maxLevel, int &res)
{
    if (root != NULL)
    {
        find(root->left, ++level, maxLevel, res);

        // Update level and rescue
        if (level > maxLevel)
        {
            res = root->data;
            maxLevel = level;
        }

        find(root->right, level, maxLevel, res);
    }
}

// Returns value of deepest node
int deepestNode(Node *root)
{
    // Initialize result and max level
    int res = -1;
    int maxLevel = -1;

    // Updates value "res" and "maxLevel"
    // Note that res and maxLen are passed
    // by reference.
    find(root, 0, maxLevel, res);
    return res;
}

// Driver program
int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->right->left = newNode(5);
    root->right->right = newNode(6);
    root->right->left->right = newNode(7);
    root->right->right->right = newNode(8);
    root->right->left->right->left = newNode(9);
    cout << deepestNode(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find value of the deepest node
// in a given binary tree
class GFG
{

    // A tree node
    static class Node
    {

        int data;
        Node left, right;

        Node(int key)
        {
            data = key;
            left = null;
            right = null;
        }
    }
    static int maxLevel = -1;
    static int res = -1;

    // maxLevel : keeps track of maximum level seen so far.
    // res : Value of deepest node so far.
    // level : Level of root
    static void find(Node root, int level)
    {
        if (root != null)
        {
            find(root.left, ++level);

            // Update level and rescue
            if (level > maxLevel)
            {
                res = root.data;
                maxLevel = level;
            }

            find(root.right, level);
        }
    }

    // Returns value of deepest node
    static int deepestNode(Node root)
    {
        // Initialize result and max level
        /* int res = -1;
        int maxLevel = -1; */

        // Updates value "res" and "maxLevel"
        // Note that res and maxLen are passed
        // by reference.
        find(root, 0);
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {

        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.right.left = new Node(5);
        root.right.right = new Node(6);
        root.right.left.right = new Node(7);
        root.right.right.right = new Node(8);
        root.right.left.right.left = new Node(9);
        System.out.println(deepestNode(root));
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
"""Python3 program to find value of the
deepest node in a given binary tree"""

# A Binary Tree Node
# Utility function to create a
# new tree node
class newNode:

    # Constructor to create a newNode
    def __init__(self, data):
        self.data= data
        self.left = None
        self.right = None
        self.visited = False

# maxLevel : keeps track of maximum
# level seen so far.
# res : Value of deepest node so far.
# level : Level of root
def find(root, level, maxLevel, res):

    if (root != None):
        level += 1
        find(root.left, level, maxLevel, res)

        # Update level and rescue
        if (level > maxLevel[0]):

            res[0] = root.data
            maxLevel[0] = level

        find(root.right, level, maxLevel, res)

# Returns value of deepest node
def deepestNode(root) :

    # Initialize result and max level
    res = [-1]
    maxLevel = [-1]

    # Updates value "res" and "maxLevel"
    # Note that res and maxLen are passed
    # by reference.
    find(root, 0, maxLevel, res)
    return res[0]

# Driver Code
if __name__ == '__main__':
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.right.left = newNode(5)
    root.right.right = newNode(6)
    root.right.left.right = newNode(7)
    root.right.right.right = newNode(8)
    root.right.left.right.left = newNode(9)
    print(deepestNode(root))

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
// C# program to find value of the deepest node
// in a given binary tree
using System;

class GFG
{

    // A tree node
    public class Node
    {

        public int data;
        public Node left, right;

        public Node(int key)
        {
            data = key;
            left = null;
            right = null;
        }
    }
    static int maxLevel = -1;
    static int res = -1;

    // maxLevel : keeps track of maximum level seen so far.
    // res : Value of deepest node so far.
    // level : Level of root
    static void find(Node root, int level)
    {
        if (root != null)
        {
            find(root.left, ++level);

            // Update level and rescue
            if (level > maxLevel)
            {
                res = root.data;
                maxLevel = level;
            }

            find(root.right, level);
        }
    }

    // Returns value of deepest node
    static int deepestNode(Node root)
    {
        // Initialize result and max level
        /* int res = -1;
        int maxLevel = -1; */

        // Updates value "res" and "maxLevel"
        // Note that res and maxLen are passed
        // by reference.
        find(root, 0);
        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {

        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.right.left = new Node(5);
        root.right.right = new Node(6);
        root.right.left.right = new Node(7);
        root.right.right.right = new Node(8);
        root.right.left.right.left = new Node(9);
        Console.WriteLine(deepestNode(root));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find value of the deepest node
// in a given binary tree

class Node
{
    constructor(key)
    {
        this.data = key;
            this.left = null;
            this.right = null;
    }
}

let maxLevel = -1;
let res = -1;

// maxLevel : keeps track of maximum level seen so far.
    // res : Value of deepest node so far.
    // level : Level of root
function find(root,level)
{
    if (root != null)
        {
            find(root.left, ++level);

            // Update level and rescue
            if (level > maxLevel)
            {
                res = root.data;
                maxLevel = level;
            }

            find(root.right, level);
        }
}

// Returns value of deepest node
function deepestNode(root)
{
    // Initialize result and max level
        /* int res = -1;
        int maxLevel = -1; */

        // Updates value "res" and "maxLevel"
        // Note that res and maxLen are passed
        // by reference.
        find(root, 0);
        return res;
}

// Driver code
let root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.right.left = new Node(5);
root.right.right = new Node(6);
root.right.left.right = new Node(7);
root.right.right.right = new Node(8);
root.right.left.right.left = new Node(9);
document.write(deepestNode(root));

// This code is contributed by rag2127

</script>
```

**输出:**

```
 9
```

**时间复杂度:**O(n)
T3】方法二:这里的思路是找到给定树的高度，然后打印最底层的节点。

## C++

```
// A C++ program to find value of the
// deepest node in a given binary tree
#include <bits/stdc++.h>
using namespace std;

// A tree node with constructor
class Node
{
public:
    int data;
    Node *left, *right;

    // constructor   
    Node(int key)
    {
        data = key;
        left = NULL;
        right = NULL;
    }
};

// Utility function to find height
// of a tree, rooted at 'root'.
int height(Node* root)
{
  if(!root) return 0;

  int leftHt = height(root->left);
  int rightHt = height(root->right);

  return max(leftHt, rightHt) + 1;
}

// levels : current Level
// Utility function to print all
// nodes at a given level.
void deepestNode(Node* root, int levels)
{
    if(!root) return;

    if(levels == 1)
    cout << root->data;

    else if(levels > 1)
    {
        deepestNode(root->left, levels - 1);
        deepestNode(root->right, levels - 1);
    }
}

// Driver program
int main()
{
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->right->left = new Node(5);
    root->right->right = new Node(6);
    root->right->left->right = new Node(7);
    root->right->right->right = new Node(8);
    root->right->left->right->left = new Node(9);

    // Calculating height of tree
    int levels = height(root);

    // Printing the deepest node
    deepestNode(root, levels);

    return 0;
}

// This code is contributed by decode2207.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find value of the
// deepest node in a given binary tree
class GFG
{

// A tree node with constructor
static class Node
{
    int data;
    Node left, right;

    // constructor
    Node(int key)
    {
        data = key;
        left = null;
        right = null;
    }
};

// Utility function to find height
// of a tree, rooted at 'root'.
static int height(Node root)
{
    if(root == null) return 0;

    int leftHt = height(root.left);
    int rightHt = height(root.right);

    return Math.max(leftHt, rightHt) + 1;
}

// levels : current Level
// Utility function to print all
// nodes at a given level.
static void deepestNode(Node root,
                        int levels)
{
    if(root == null) return;

    if(levels == 1)
    System.out.print(root.data + " ");

    else if(levels > 1)
    {
        deepestNode(root.left, levels - 1);
        deepestNode(root.right, levels - 1);
    }
}

// Driver Codede
public static void main(String args[])
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.right.left = new Node(5);
    root.right.right = new Node(6);
    root.right.left.right = new Node(7);
    root.right.right.right = new Node(8);
    root.right.left.right.left = new Node(9);

    // Calculating height of tree
    int levels = height(root);

    // Printing the deepest node
    deepestNode(root, levels);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# A Python3 program to find value of the
# deepest node in a given binary tree
class new_Node:
    def __init__(self, key):
        self.data = key
        self.left = self.right = None

# Utility function to find height
# of a tree, rooted at 'root'.
def height(root):
    if(not root):
        return 0

    leftHt = height(root.left)
    rightHt = height(root.right)

    return max(leftHt, rightHt) + 1

# levels : current Level
# Utility function to print all
# nodes at a given level.
def deepestNode(root, levels):
    if(not root):
        return

    if(levels == 1):
        print(root.data)
    elif(levels > 1):
        deepestNode(root.left, levels - 1)
        deepestNode(root.right, levels - 1)

# Driver Code
if __name__ == '__main__':

    root = new_Node(1)
    root.left = new_Node(2)
    root.right = new_Node(3)
    root.left.left = new_Node(4)
    root.right.left = new_Node(5)
    root.right.right = new_Node(6)
    root.right.left.right = new_Node(7)
    root.right.right.right = new_Node(8)
    root.right.left.right.left = new_Node(9)

    # Calculating height of tree
    levels = height(root)

    # Printing the deepest node
    deepestNode(root, levels)

# This code is contributed by PranchalK
```

## C#

```
// C# program to find value of the
// deepest node in a given binary tree
using System;

class GFG
{

// A tree node with constructor
public class Node
{
    public int data;
    public Node left, right;

    // constructor
    public Node(int key)
    {
        data = key;
        left = null;
        right = null;
    }
};

// Utility function to find height
// of a tree, rooted at 'root'.
static int height(Node root)
{
    if(root == null) return 0;

    int leftHt = height(root.left);
    int rightHt = height(root.right);

    return Math.Max(leftHt, rightHt) + 1;
}

// levels : current Level
// Utility function to print all
// nodes at a given level.
static void deepestNode(Node root,
                        int levels)
{
    if(root == null) return;

    if(levels == 1)
    Console.Write(root.data + " ");

    else if(levels > 1)
    {
        deepestNode(root.left, levels - 1);
        deepestNode(root.right, levels - 1);
    }
}

// Driver Code
public static void Main(String []args)
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.right.left = new Node(5);
    root.right.right = new Node(6);
    root.right.left.right = new Node(7);
    root.right.right.right = new Node(8);
    root.right.left.right.left = new Node(9);

    // Calculating height of tree
    int levels = height(root);

    // Printing the deepest node
    deepestNode(root, levels);
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// A Javascript program to find value of the
// deepest node in a given binary tree

// A tree node with constructor
class Node
{
    // constructor
    constructor(key)
    {
        this.data = key;
        this.left = null;
        this.right = null;
    }
}

// Utility function to find height
// of a tree, rooted at 'root
function height(root)
{
    if(root == null) return 0;

    let leftHt = height(root.left);
    let rightHt = height(root.right);

    return Math.max(leftHt, rightHt) + 1;
}

// levels : current Level
// Utility function to print all
// nodes at a given level.
function deepestNode(root,levels)
{
    if(root == null) return;

    if(levels == 1)
    document.write(root.data + " ");

    else if(levels > 1)
    {
        deepestNode(root.left, levels - 1);
        deepestNode(root.right, levels - 1);
    }
}

// Driver Codede
let root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.right.left = new Node(5);
root.right.right = new Node(6);
root.right.left.right = new Node(7);
root.right.right.right = new Node(8);
root.right.left.right.left = new Node(9);

// Calculating height of tree
let levels = height(root);

// Printing the deepest node
deepestNode(root, levels);

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
9
```

**时间复杂度:** O(n)
感谢 **Parth Patekar** 提出上述方法。

**方法 3** :从队列中按级别顺序处理的最后一个节点是二叉树中最深的节点。

## C++

```
// A C++ program to find value of the
// deepest node in a given binary tree
#include <bits/stdc++.h>
using namespace std;

// A tree node with constructor
class Node
{
public:
    int data;
    Node *left, *right;

    // constructor  
    Node(int key)
    {
        data = key;
        left = NULL;
        right = NULL;
    }
};

// Function to return the deepest node
Node* deepestNode(Node* root)
{
    Node* tmp = NULL;
    if (root == NULL)
        return NULL;

    // Creating a Queue
    queue<Node*> q;
    q.push(root);

    // Iterates until queue become empty
    while (q.size() > 0)
    {
        tmp = q.front();
        q.pop();
        if (tmp->left != NULL)
            q.push(tmp->left);
        if (tmp->right != NULL)
            q.push(tmp->right);
    }
    return tmp;
}

int main()
{
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->right->left = new Node(5);
    root->right->right = new Node(6);
    root->right->left->right = new Node(7);
    root->right->right->right = new Node(8);
    root->right->left->right->left = new Node(9);

    Node* deepNode = deepestNode(root);
    cout << (deepNode->data);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

// A Java program to find value of the
// deepest node in a given binary tree

// A tree node with constructor
public class Node
{
    int data;
    Node left, right;

    // constructor
    Node(int key)
    {
        data = key;
        left = null;
        right = null;
    }
};

class Gfg
{

    // Function to return the deepest node
    public static Node deepestNode(Node root)
    {
        Node tmp = null;
        if (root == null)
            return null;

        // Creating a Queue
        Queue<Node> q = new LinkedList<Node>();
        q.offer(root);

        // Iterates until queue become empty
        while (!q.isEmpty())
        {
            tmp = q.poll();
            if (tmp.left != null)
                q.offer(tmp.left);
            if (tmp.right != null)
                q.offer(tmp.right);
        }
        return tmp;
    }

    public static void main(String[] args)
    {

        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.right.left = new Node(5);
        root.right.right = new Node(6);
        root.right.left.right = new Node(7);
        root.right.right.right = new Node(8);
        root.right.left.right.left = new Node(9);

        Node deepNode = deepestNode(root);
        System.out.println(deepNode.data);
    }
}

// Code is contributed by mahi_07
```

## 蟒蛇 3

```
# A Python3 program to find value of the
# deepest node in a given binary tree by method 3
from collections import deque

class new_Node:
    def __init__(self, key):
        self.data = key
        self.left = self.right = None

def deepestNode(root):
    if root == None:
        return 0
    q = deque()
    q.append(root)
    node = None
    while len(q) != 0:
        node = q.popleft()
        if node.left is not None:
            q.append(node.left)
        if node.right is not None:
            q.append(node.right)
    return node.data

# Driver Code
if __name__ == '__main__':

    root = new_Node(1)
    root.left = new_Node(2)
    root.right = new_Node(3)
    root.left.left = new_Node(4)
    root.right.left = new_Node(5)
    root.right.right = new_Node(6)
    root.right.left.right = new_Node(7)
    root.right.right.right = new_Node(8)
    root.right.left.right.left = new_Node(9)

    # Calculating height of tree
    levels = deepestNode(root)

    # Printing the deepest node
    print(levels)

# This code is contributed by Aprajita Chhawi
```

## C#

```
// A C# program to find value of the
// deepest node in a given binary tree
using System;
using System.Collections.Generic;

// A tree node with constructor
public class Node
{
  public
    int data;
  public
    Node left, right;

  // constructor
  public
    Node(int key)
  {
    data = key;
    left = null;
    right = null;
  }
};

class Gfg
{

  // Function to return the deepest node
  public static Node deepestNode(Node root)
  {
    Node tmp = null;
    if (root == null)
      return null;

    // Creating a Queue
    Queue<Node> q = new Queue<Node>();
    q.Enqueue(root);

    // Iterates until queue become empty
    while (q.Count != 0)
    {
      tmp = q.Peek();
      q.Dequeue();
      if (tmp.left != null)
        q.Enqueue(tmp.left);
      if (tmp.right != null)
        q.Enqueue(tmp.right);
    }
    return tmp;
  }

  // Driver code
  public static void Main(String[] args)
  {

    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.right.left = new Node(5);
    root.right.right = new Node(6);
    root.right.left.right = new Node(7);
    root.right.right.right = new Node(8);
    root.right.left.right.left = new Node(9);

    Node deepNode = deepestNode(root);
    Console.WriteLine(deepNode.data);
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// A Javascript program to find value of the
// deepest node in a given binary tree

// A tree node with constructor
class Node
{
    constructor(key)
    {
        this.data = key;
        this.left = null;
        this.right = null;
    }
}

// Function to return the deepest node
function deepestNode(root)
{
    let  tmp = null;
        if (root == null)
            return null;

        // Creating a Queue
        let q = [];
        q.push(root);

        // Iterates until queue become empty
        while (q.length!=0)
        {
            tmp = q.shift();
            if (tmp.left != null)
                q.push(tmp.left);
            if (tmp.right != null)
                q.push(tmp.right);
        }
        return tmp;
}

let root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.right.left = new Node(5);
root.right.right = new Node(6);
root.right.left.right = new Node(7);
root.right.right.right = new Node(8);
root.right.left.right.left = new Node(9);

let deepNode = deepestNode(root);
document.write(deepNode.data);

// This code is contributed by unknown2108
</script>
```

**Output**

```
9
```

**时间复杂度:** O(n)

**空间复杂度:** O(n)

？list = plqm 7 alhxfyshcxd 7r 1j0ky 9 ZG _ gbb 1 dbk〖t0〗]

本文由**拉克什·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。