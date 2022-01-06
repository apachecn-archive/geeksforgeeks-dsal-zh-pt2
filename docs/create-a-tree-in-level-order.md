# 按照层级顺序创建一棵树

> 原文:[https://www.geeksforgeeks.org/create-a-tree-in-level-order/](https://www.geeksforgeeks.org/create-a-tree-in-level-order/)

给定一个元素数组，任务是按级别顺序插入这些元素并构建一个树。

```
Input : arr[] = {10, 20, 30, 40, 50, 60}
Output :         10
              /      \
             20       30
            /  \     /
          40    50  60
```

任务是从一个给定的数组构建一整棵树。要在已构建的树中按级别顺序插入，请参见[按级别顺序插入二叉树](https://www.geeksforgeeks.org/insertion-in-a-binary-tree-in-level-order/)
任务是将数据按级别顺序存储在二叉树中。
为此，我们将按照以下步骤进行:
1。每当向二叉树中添加一个新节点时，该节点的地址就会被推入队列。
2。一个节点地址将留在队列中，直到它的两个子节点都没有被填满。
3。一旦两个子节点都填满，父节点就会从队列中弹出。
下面是执行上述数据输入的代码。

## C++

```
// CPP program to construct a binary tree in level order.
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int key;
    Node* left;
    Node* right;
};

// Function to create a node with 'value' as the data
// stored in it.
// Both the children of this new Node are initially null.
struct Node* newNode(int value)
{
    Node* n = new Node;
    n->key = value;
    n->left = NULL;
    n->right = NULL;
    return n;
}

struct Node* insertValue(struct Node* root, int value,
                         queue<Node *>& q)
{
    Node* node = newNode(value);
    if (root == NULL)
        root = node;

    // The left child of the current Node is
    // used if it is available.
    else if (q.front()->left == NULL)
        q.front()->left = node;

    // The right child of the current Node is used
    // if it is available. Since the left child of this
    // node has already been used, the Node is popped
    // from the queue after using its right child.
    else {
        q.front()->right = node;
        q.pop();
    }

    // Whenever a new Node is added to the tree, its
    // address is pushed into the queue.
    // So that its children Nodes can be used later.
    q.push(node);
    return root;
}

// This function mainly calls insertValue() for
// all array elements. All calls use same queue.
Node* createTree(int arr[], int n)
{
    Node* root = NULL;
    queue<Node*> q;
    for (int i = 0; i < n; i++)
      root = insertValue(root, arr[i], q);
    return root;
}

// This is used to verify the logic.
void levelOrder(struct Node* root)
{
    if (root == NULL)
        return;
    queue<Node*> n;
    n.push(root);
    while (!n.empty()) {
        cout << n.front()->key << " ";
        if (n.front()->left != NULL)
            n.push(n.front()->left);
        if (n.front()->right != NULL)
            n.push(n.front()->right);
        n.pop();
    }
}

// Driver code
int main()
{
    int arr[] = { 10, 20, 30, 40, 50, 60 };
    int n = sizeof(arr) / sizeof(arr[0]);
    Node* root = createTree(arr, n);
    levelOrder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to cona
// binary tree in level
// order.
import java.util.*;
class GFG{

static class Node
{
  int key;
  Node left;
  Node right;
};

static Node root = null;

static Queue<Node> q =
       new LinkedList<>();

// Function to create a node
// with 'value' as the data
// stored in it.
// Both the children of this
// new Node are initially null.
static Node newNode(int value)
{
  Node n = new Node();
  n.key = value;
  n.left = null;
  n.right = null;
  return n;
}

static void insertValue(int value)
{
  Node node = newNode(value);
  if (root == null)
    root = node;

  // The left child of the
  // current Node is used
  // if it is available.
  else if (q.peek().left == null)
    q.peek().left = node;

  // The right child of the current
  // Node is used if it is available.
  // Since the left child of this
  // node has already been used, the
  // Node is popped from the queue
  // after using its right child.
  else
  {
    q.peek().right = node;
    q.remove();
  }

  // Whenever a new Node is added
  // to the tree, its address is
  // pushed into the queue. So that
  // its children Nodes can be used
  // later.
  q.add(node);

}

// This function mainly calls
// insertValue() for all array
// elements. All calls use same
// queue.
static void createTree(int arr[],
                       int n)
{
  for (int i = 0; i < n; i++)
    insertValue(arr[i]);
}

// This is used to verify
// the logic.
static void levelOrder(Node root)
{
  if (root == null)
    return;
  Queue<Node> n =
        new LinkedList<>();
  n.add(root);
  while (!n.isEmpty())
  {
    System.out.print(n.peek().key +
                     " ");
    if (n.peek().left != null)
      n.add(n.peek().left);
    if (n.peek().right != null)
      n.add(n.peek().right);
    n.remove();
  }
}

// Driver code
public static void main(String[] args)
{
  int arr[] = {10, 20, 30,
               40, 50, 60};
  int n = arr.length;
  createTree(arr, n);
  levelOrder(root);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to construct
# a binary tree in level order.

# Importing Queue for use in
# Level Order Traversal
from collections import deque

# Node class for holding the Binary Tree
class node:
    def __init__(self, data = None):
        self.data = data
        self.left = None
        self.right = None

Q = deque()

# Helper function helps us in adding data
# to the tree in Level Order
def insertValue(data, root):
    newnode = node(data)
    if Q:
        temp = Q[0]
    if root == None:
        root = newnode

    # The left child of the current Node is
    # used if it is available.
    elif temp.left == None:
        temp.left = newnode

    # The right child of the current Node is used
    # if it is available. Since the left child of this
    # node has already been used, the Node is popped
    # from the queue after using its right child.
    elif temp.right == None:
        temp.right = newnode
        atemp = Q.popleft()

    # Whenever a new Node is added to the tree,
    # its address is pushed into the queue.
    # So that its children Nodes can be used later.
    Q.append(newnode)
    return root

# Function which calls add which is responsible
# for adding elements one by one
def createTree(a, root):
    for i in range(len(a)):
        root = insertValue(a[i], root)
    return root

# Function for printing level order traversal
def levelOrder(root):
    Q = deque()
    Q.append(root)
    while Q:
        temp = Q.popleft()
        print(temp.data, end = ' ')
        if temp.left != None:
            Q.append(temp.left)
        if temp.right != None:
            Q.append(temp.right)

# Driver Code
a = [ 10, 20, 30, 40, 50, 60 ]
root = None
root = createTree(a, root)

levelOrder(root)

# This code is contributed by code_freak
```

## C#

```
// C# program to cona
// binary tree in level
// order.
using System;
using System.Collections.Generic;
class GFG {

    class Node
    {
        public int key;
        public Node left, right;
    };

    static Node root = null;

    static List<Node> q = new List<Node>();

    // Function to create a node
    // with 'value' as the data
    // stored in it.
    // Both the children of this
    // new Node are initially null.
    static Node newNode(int value)
    {
      Node n = new Node();
      n.key = value;
      n.left = null;
      n.right = null;
      return n;
    }

    static void insertValue(int value)
    {
      Node node = newNode(value);
      if (root == null)
        root = node;

      // The left child of the
      // current Node is used
      // if it is available.
      else if (q[0].left == null)
        q[0].left = node;

      // The right child of the current
      // Node is used if it is available.
      // Since the left child of this
      // node has already been used, the
      // Node is popped from the queue
      // after using its right child.
      else
      {
        q[0].right = node;
        q.RemoveAt(0);
      }

      // Whenever a new Node is added
      // to the tree, its address is
      // pushed into the queue. So that
      // its children Nodes can be used
      // later.
      q.Add(node);

    }

    // This function mainly calls
    // insertValue() for all array
    // elements. All calls use same
    // queue.
    static void createTree(int[] arr, int n)
    {
      for (int i = 0; i < n; i++)
        insertValue(arr[i]);
    }

    // This is used to verify
    // the logic.
    static void levelOrder(Node root)
    {
      if (root == null)
        return;

      List<Node> n = new List<Node>();
      n.Add(root);
      while (n.Count > 0)
      {
        Console.Write(n[0].key + " ");
        if (n[0].left != null)
          n.Add(n[0].left);
        if (n[0].right != null)
          n.Add(n[0].right);
        n.RemoveAt(0);
      }
    }

  // Driver code
  static void Main() {
    int[] arr = {10, 20, 30, 40, 50, 60};
    int n = arr.Length;
    createTree(arr, n);
    levelOrder(root);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// Javascript program to cona
// binary tree in level
// order.

// Binary Tree node
class Node
{
    constructor(value)
    {
        this.left = null;
        this.right = null;
        this.key = value;
    }
}

let root = null;
let q = [];

// Function to create a node
// with 'value' as the data
// stored in it.
// Both the children of this
// new Node are initially null.
function newNode(value)
{
    let n = new Node(value);
    return n;
}

function insertValue(value)
{
    let node = newNode(value);
    if (root == null)
        root = node;

    // The left child of the
    // current Node is used
    // if it is available.
    else if (q[0].left == null)
        q[0].left = node;

    // The right child of the current
    // Node is used if it is available.
    // Since the left child of this
    // node has already been used, the
    // Node is popped from the queue
    // after using its right child.
    else
    {
        q[0].right = node;
        q.shift();
    }

    // Whenever a new Node is added
    // to the tree, its address is
    // pushed into the queue. So that
    // its children Nodes can be used
    // later.
    q.push(node);

}

// This function mainly calls
// insertValue() for all array
// elements. All calls use same
// queue.
function createTree(arr, n)
{
    for(let i = 0; i < n; i++)
        insertValue(arr[i]);
}

// This is used to verify
// the logic.
function levelOrder(root)
{
    if (root == null)
        return;

    let n = [];
    n.push(root);

    while (n.length > 0)
    {
        document.write(n[0].key + " ");
        if (n[0].left != null)
            n.push(n[0].left);
        if (n[0].right != null)
            n.push(n[0].right);

        n.shift();
    }
}

// Driver code
let arr = [ 10, 20, 30, 40, 50, 60 ];
let n = arr.length;

createTree(arr, n);
levelOrder(root);

// This code is contributed by suresh07

</script>
```

**Output:** 

```
10 20 30 40 50 60
```

时间复杂度:0(n)