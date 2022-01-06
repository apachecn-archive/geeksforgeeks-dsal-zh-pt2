# 创建一个具有左-子右-兄弟表示的树

> 原文:[https://www . geeksforgeeks . org/creating-tree-left-child-right-同胞表示/](https://www.geeksforgeeks.org/creating-tree-left-child-right-sibling-representation/)

[左-子右-同级表示](https://www.geeksforgeeks.org/left-child-right-sibling-representation-tree/)是 n 元树的不同表示，其中一个节点只保存两个引用，首先是对其第一个子节点的引用，另一个是对其紧接的下一个同级节点的引用，而不是保存对每个子节点的引用。这种新的转换不仅消除了对节点拥有的子节点数量的高级知识的需求，而且将引用的数量限制为最多两个，从而使编码变得更加容易。

```
At each node, link children of same parent from left to right.
Parent should be linked with only first child.
```

**示例:**

```
Left Child Right Sibling tree representation
      10
      |  
      2 -> 3 -> 4 -> 5
      |    |  
      6    7 -> 8 -> 9
```

先决条件:[树的左-子右-兄弟表示](https://www.geeksforgeeks.org/left-child-right-sibling-representation-tree/)

下面是实现。

## C++

```
// C++ program to create a tree with left child
// right sibling representation.
#include<bits/stdc++.h>
using namespace std;

struct Node
{
    int data;
    struct Node *next;
    struct Node *child;
};

// Creating new Node
Node* newNode(int data)
{
    Node *newNode = new Node;
    newNode->next = newNode->child = NULL;
    newNode->data = data;
    return newNode;
}

// Adds a sibling to a list with starting with n
Node *addSibling(Node *n, int data)
{
    if (n == NULL)
        return NULL;

    while (n->next)
        n = n->next;

    return (n->next = newNode(data));
}

// Add child Node to a Node
Node *addChild(Node * n, int data)
{
    if (n == NULL)
        return NULL;

    // Check if child list is not empty.
    if (n->child)
        return addSibling(n->child, data);
    else
        return (n->child = newNode(data));
}

// Traverses tree in depth first order
void traverseTree(Node * root)
{
    if (root == NULL)
        return;

    while (root)
    {
        cout << " " << root->data;
        if (root->child)
            traverseTree(root->child);
        root = root->next;
    }
}

//Driver code

int main()
{
    /*   Let us create below tree
    *           10
    *     /   /    \   \
    *    2  3      4   5
    *              |   /  | \
    *              6   7  8  9   */

    // Left child right sibling
    /*  10
    *    |
    *    2 -> 3 -> 4 -> 5
    *              |    |
    *              6    7 -> 8 -> 9  */
    Node *root = newNode(10);
    Node *n1  = addChild(root, 2);
    Node *n2  = addChild(root, 3);
    Node *n3  = addChild(root, 4);
    Node *n4  = addChild(n3, 6);
    Node *n5  = addChild(root, 5);
    Node *n6  = addChild(n5, 7);
    Node *n7  = addChild(n5, 8);
    Node *n8  = addChild(n5, 9);
    traverseTree(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to create a tree with left child
// right sibling representation.

class GFG {

    static class NodeTemp
    {
        int data;
        NodeTemp next, child;
        public NodeTemp(int data)
        {
            this.data = data;
            next = child = null;
        }
    }

    // Adds a sibling to a list with starting with n
    static public NodeTemp addSibling(NodeTemp node, int data)
    {
        if(node == null)
            return null;
        while(node.next != null)
            node = node.next;
        return(node.next = new NodeTemp(data));
    }

    // Add child Node to a Node
    static public NodeTemp addChild(NodeTemp node,int data)
    {
        if(node == null)
            return null;

        // Check if child is not empty.
        if(node.child != null)
            return(addSibling(node.child,data));
        else
            return(node.child = new NodeTemp(data));
    }

    // Traverses tree in depth first order
    static public void traverseTree(NodeTemp root)
    {
        if(root == null)
            return;
        while(root != null)
        {
            System.out.print(root.data + " ");
            if(root.child != null)
                traverseTree(root.child);
            root = root.next;
        }
    }

    // Driver code
    public static void main(String args[])
    {

        /*   Let us create below tree
        *           10
        *     /   /    \   \
        *    2  3      4   5
        *              |   /  | \
        *              6   7  8  9   */

        // Left child right sibling
        /*  10
        *    |
        *    2 -> 3 -> 4 -> 5
        *              |    |
        *              6    7 -> 8 -> 9  */

        NodeTemp root = new NodeTemp(10);
        NodeTemp n1 = addChild(root,2);
        NodeTemp n2 = addChild(root,3);
        NodeTemp n3 = addChild(root,4);
        NodeTemp n4 = addChild(n3,6);
        NodeTemp n5 = addChild(root,5);
        NodeTemp n6 = addChild(n5,7);
        NodeTemp n7 = addChild(n5,8);
        NodeTemp n8 = addChild(n5,9);

        traverseTree(root);
    }
}

// This code is contributed by M.V.S.Surya Teja.
```

## 蟒蛇 3

```
# Python3 program to create a tree with
# left child right sibling representation.

# Creating new Node
class newNode:
    def __init__(self, data):
        self.Next = self.child = None
        self.data = data

# Adds a sibling to a list with
# starting with n
def addSibling(n, data):
    if (n == None):
        return None

    while (n.Next):
        n = n.Next
    n.Next = newNode(data)
    return n.Next

# Add child Node to a Node
def addChild(n, data):
    if (n == None):
        return None

    # Check if child list is not empty.
    if (n.child):
        return addSibling(n.child, data)
    else:
        n.child = newNode(data)
        return n.child

# Traverses tree in depth first order
def traverseTree(root):
    if (root == None):
        return

    while (root):
        print(root.data, end = " ")
        if (root.child):
            traverseTree(root.child)
        root = root.Next

# Driver code
if __name__ == '__main__':

    # Let us create below tree
    #         10
    #     / / \ \
    # 2 3     4 5
    #             | / | \
    #             6 7 8 9

    # Left child right sibling
    # 10
    # |
    # 2 -> 3 -> 4 -> 5
    #             | |
    #             6 7 -> 8 -> 9
    root = newNode(10)
    n1 = addChild(root, 2)
    n2 = addChild(root, 3)
    n3 = addChild(root, 4)
    n4 = addChild(n3, 6)
    n5 = addChild(root, 5)
    n6 = addChild(n5, 7)
    n7 = addChild(n5, 8)
    n8 = addChild(n5, 9)
    traverseTree(root)

# This code is contributed by pranchalK
```

## C#

```
// C# program to create a tree with left
// child right sibling representation.
using System;

class GFG
{
public class NodeTemp
{
    public int data;
    public NodeTemp next, child;
    public NodeTemp(int data)
    {
        this.data = data;
        next = child = null;
    }
}

// Adds a sibling to a list with
// starting with n
public static NodeTemp addSibling(NodeTemp node,
                                  int data)
{
    if (node == null)
    {
        return null;
    }
    while (node.next != null)
    {
        node = node.next;
    }
    return (node.next = new NodeTemp(data));
}

// Add child Node to a Node
public static NodeTemp addChild(NodeTemp node,
                                int data)
{
    if (node == null)
    {
        return null;
    }

    // Check if child is not empty.
    if (node.child != null)
    {
        return (addSibling(node.child,data));
    }
    else
    {
        return (node.child = new NodeTemp(data));
    }
}

// Traverses tree in depth first order
public static void traverseTree(NodeTemp root)
{
    if (root == null)
    {
        return;
    }
    while (root != null)
    {
        Console.Write(root.data + " ");
        if (root.child != null)
        {
            traverseTree(root.child);
        }
        root = root.next;
    }
}

// Driver code
public static void Main(string[] args)
{

    /* Let us create below tree
    *         10
    *     / / \ \
    * 2 3     4 5
    *             | / | \
    *             6 7 8 9 */

    // Left child right sibling
    /* 10
    * |
    * 2 -> 3 -> 4 -> 5
    *             | |
    *             6 7 -> 8 -> 9 */

    NodeTemp root = new NodeTemp(10);
    NodeTemp n1 = addChild(root, 2);
    NodeTemp n2 = addChild(root, 3);
    NodeTemp n3 = addChild(root, 4);
    NodeTemp n4 = addChild(n3, 6);
    NodeTemp n5 = addChild(root, 5);
    NodeTemp n6 = addChild(n5, 7);
    NodeTemp n7 = addChild(n5, 8);
    NodeTemp n8 = addChild(n5, 9);

    traverseTree(root);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to create a tree with left child
// right sibling representation.

    class NodeTemp
    {
        constructor(data)
        {
            this.data=data;
            this.next = this.child = null;
        }
    }

    // Adds a sibling to a list with starting with n
    function addSibling(node,data)
    {
        if(node == null)
            return null;
        while(node.next != null)
            node = node.next;
        return(node.next = new NodeTemp(data));
    }

    // Add child Node to a Node
    function addChild(node,data)
    {
        if(node == null)
            return null;

        // Check if child is not empty.
        if(node.child != null)
            return(addSibling(node.child,data));
        else
            return(node.child = new NodeTemp(data));

    }

    // Traverses tree in depth first order
    function traverseTree(root)
    {
        if(root == null)
            return;
        while(root != null)
        {
            document.write(root.data + " ");
            if(root.child != null)
                traverseTree(root.child);
            root = root.next;
        }
    }

    // Driver code

    /*   Let us create below tree
        *           10
        *     /   /    \   \
        *    2  3      4   5
        *              |   /  | \
        *              6   7  8  9   */

        // Left child right sibling
        /*  10
        *    |
        *    2 -> 3 -> 4 -> 5
        *              |    |
        *              6    7 -> 8 -> 9  */

        let root = new NodeTemp(10);
        let n1 = addChild(root,2);
        let n2 = addChild(root,3);
        let n3 = addChild(root,4);
        let n4 = addChild(n3,6);
        let n5 = addChild(root,5);
        let n6 = addChild(n5,7);
        let n7 = addChild(n5,8);
        let n8 = addChild(n5,9);

        traverseTree(root);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
10 2 3 4 6 5 7 8 9
```

**层级顺序遍历:**上面的代码谈到了深度优先遍历。我们也可以对这样的表示进行级序遍历。

## C++

```
// C++ program to create a tree with left child
// right sibling representation.
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    struct Node* next;
    struct Node* child;
};

// Creating new Node
Node* newNode(int data)
{
    Node* newNode = new Node;
    newNode->next = newNode->child = NULL;
    newNode->data = data;
    return newNode;
}

// Adds a sibling to a list with starting with n
Node* addSibling(Node* n, int data)
{
    if (n == NULL)
        return NULL;

    while (n->next)
        n = n->next;

    return (n->next = newNode(data));
}

// Add child Node to a Node
Node* addChild(Node* n, int data)
{
    if (n == NULL)
        return NULL;

    // Check if child list is not empty.
    if (n->child)
        return addSibling(n->child, data);
    else
        return (n->child = newNode(data));
}

// Traverses tree in level order
void traverseTree(Node* root)
{
    // Corner cases
    if (root == NULL)
        return;

    cout << root->data << " ";

    if (root->child == NULL)
        return;

    // Create a queue and enque root
    queue<Node*> q;
    Node* curr = root->child;
    q.push(curr);

    while (!q.empty()) {

        // Take out an item from the queue
        curr = q.front();
        q.pop();

        // Print next level of taken out item and enque
        // next level's children
        while (curr != NULL) {
            cout << curr->data << " ";
            if (curr->child != NULL) {
                q.push(curr->child);
            }
            curr = curr->next;
        }
    }
}

// Driver code
int main()
{
    Node* root = newNode(10);
    Node* n1 = addChild(root, 2);
    Node* n2 = addChild(root, 3);
    Node* n3 = addChild(root, 4);
    Node* n4 = addChild(n3, 6);
    Node* n5 = addChild(root, 5);
    Node* n6 = addChild(n5, 7);
    Node* n7 = addChild(n5, 8);
    Node* n8 = addChild(n5, 9);
    traverseTree(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to create a tree with left child
// right sibling representation.
import java.util.*;
class GFG
{
  static class Node
  {
    int data;
    Node next;
    Node child;
  };

  // Creating new Node
  static Node newNode(int data)
  {
    Node newNode = new Node();
    newNode.next = newNode.child = null;
    newNode.data = data;
    return newNode;
  }

  // Adds a sibling to a list with starting with n
  static Node addSibling(Node n, int data)
  {
    if (n == null)
      return null;
    while (n.next != null)
      n = n.next;
    return (n.next = newNode(data));
  }

  // Add child Node to a Node
  static Node addChild(Node n, int data)
  {
    if (n == null)
      return null;

    // Check if child list is not empty.
    if (n.child != null)
      return addSibling(n.child, data);
    else
      return (n.child = newNode(data));
  }

  // Traverses tree in level order
  static void traverseTree(Node root)
  {
    // Corner cases
    if (root == null)
      return;
    System.out.print(root.data+ " ");
    if (root.child == null)
      return;

    // Create a queue and enque root
    Queue<Node> q = new LinkedList<>();
    Node curr = root.child;
    q.add(curr);

    while (!q.isEmpty())
    {

      // Take out an item from the queue
      curr = q.peek();
      q.remove();

      // Print next level of taken out item and enque
      // next level's children
      while (curr != null)
      {
        System.out.print(curr.data + " ");
        if (curr.child != null)
        {
          q.add(curr.child);
        }
        curr = curr.next;
      }
    }
  }

  // Driver code
  public static void main(String[] args)
  {
    Node root = newNode(10);
    Node n1 = addChild(root, 2);
    Node n2 = addChild(root, 3);
    Node n3 = addChild(root, 4);
    Node n4 = addChild(n3, 6);
    Node n5 = addChild(root, 5);
    Node n6 = addChild(n5, 7);
    Node n7 = addChild(n5, 8);
    Node n8 = addChild(n5, 9);
    traverseTree(root);
  }
}

// This code is contributed by aashish1995
```

## 蟒蛇 3

```
# Python3 program to create a tree with
# left child right sibling representation
from collections import deque

class Node:

    def __init__(self, x):

        self.data = x
        self.next = None
        self.child = None

# Adds a sibling to a list with
# starting with n
def addSibling(n, data):

    if (n == None):
        return None

    while (n.next):
        n = n.next

    n.next = Node(data)
    return n

# Add child Node to a Node
def addChild(n, data):

    if (n == None):
        return None

    # Check if child list is not empty
    if (n.child):
        return addSibling(n.child, data)
    else:
        n.child = Node(data)
        return n

# Traverses tree in level order
def traverseTree(root):

    # Corner cases
    if (root == None):
        return

    print(root.data, end = " ")

    if (root.child == None):
        return

    # Create a queue and enque root
    q = deque()
    curr = root.child
    q.append(curr)

    while (len(q) > 0):

        # Take out an item from the queue
        curr = q.popleft()
        #q.pop()

        # Print next level of taken out
        # item and enque next level's children
        while (curr != None):
            print(curr.data, end = " ")

            if (curr.child != None):
                q.append(curr.child)

            curr = curr.next

# Driver code
if __name__ == '__main__':

    root = Node(10)
    n1 = addChild(root, 2)
    n2 = addChild(root, 3)
    n3 = addChild(root, 4)
    n4 = addChild(n3, 6)
    n5 = addChild(root, 5)
    n6 = addChild(n5, 7)
    n7 = addChild(n5, 8)
    n8 = addChild(n5, 9)

    traverseTree(root)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to create a tree with left child
// right sibling representation.
using System;
using System.Collections.Generic;
class GFG
{
  public
    class Node
    {
      public
        int data;
      public
        Node next;
      public
        Node child;
    };

  // Creating new Node
  static Node newNode(int data)
  {
    Node newNode = new Node();
    newNode.next = newNode.child = null;
    newNode.data = data;
    return newNode;
  }

  // Adds a sibling to a list with starting with n
  static Node addSibling(Node n, int data)
  {
    if (n == null)
      return null;
    while (n.next != null)
      n = n.next;
    return (n.next = newNode(data));
  }

  // Add child Node to a Node
  static Node addChild(Node n, int data)
  {
    if (n == null)
      return null;

    // Check if child list is not empty.
    if (n.child != null)
      return addSibling(n.child, data);
    else
      return (n.child = newNode(data));
  }

  // Traverses tree in level order
  static void traverseTree(Node root)
  {

    // Corner cases
    if (root == null)
      return;
    Console.Write(root.data + " ");
    if (root.child == null)
      return;

    // Create a queue and enque root
    Queue<Node> q = new Queue<Node>();
    Node curr = root.child;
    q.Enqueue(curr);
    while (q.Count != 0)
    {

      // Take out an item from the queue
      curr = q.Peek();
      q.Dequeue();

      // Print next level of taken out item and enque
      // next level's children
      while (curr != null)
      {
        Console.Write(curr.data + " ");
        if (curr.child != null)
        {
          q.Enqueue(curr.child);
        }
        curr = curr.next;
      }
    }
  }

  // Driver code
  public static void Main(String[] args)
  {
    Node root = newNode(10);
    Node n1 = addChild(root, 2);
    Node n2 = addChild(root, 3);
    Node n3 = addChild(root, 4);
    Node n4 = addChild(n3, 6);
    Node n5 = addChild(root, 5);
    Node n6 = addChild(n5, 7);
    Node n7 = addChild(n5, 8);
    Node n8 = addChild(n5, 9);
    traverseTree(root);
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to create a
// tree with left child
// right sibling representation.

    class Node
    {
    // Creating new Node
        constructor(data)
        {
            this.data=data;
            this.next = this.child = null;
        }
    }

// Adds a sibling to a list with starting with n
function addSibling(n,data)
{
    if (n == null)
      return null;
    while (n.next != null)
      n = n.next;
    return (n.next = new Node(data));
}

// Add child Node to a Node
function addChild(n,data)
{
    if (n == null)
      return null;

    // Check if child list is not empty.
    if (n.child != null)
      return addSibling(n.child, data);
    else
      return (n.child = new Node(data));
}

// Traverses tree in level order
function traverseTree(root)
{
    // Corner cases
    if (root == null)
      return;
    document.write(root.data+ " ");
    if (root.child == null)
      return;

    // Create a queue and enque root
    let q = [];
    let curr = root.child;
    q.push(curr);

    while (q.length!=0)
    {

      // Take out an item from the queue
      curr = q[0];
      q.shift();

      // Print next level of taken out item and enque
      // next level's children
      while (curr != null)
      {
        document.write(curr.data + " ");
        if (curr.child != null)
        {
          q.push(curr.child);
        }
        curr = curr.next;
      }
    }
}

// Driver code
let root = new Node(10);
let n1 = addChild(root, 2);
let n2 = addChild(root, 3);
let n3 = addChild(root, 4);
let n4 = addChild(n3, 6);
let n5 = addChild(root, 5);
let n6 = addChild(n5, 7);
let n7 = addChild(n5, 8);
let n8 = addChild(n5, 9);
traverseTree(root);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
10 2 3 4 5 6 7 8 9
```

本文由 **SAKSHI TIWARI** 供稿。如果你喜欢极客(我们知道你喜欢！)并愿意投稿，也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者将文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。