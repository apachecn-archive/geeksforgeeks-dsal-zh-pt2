# 给定数量的因子树

> 原文:[https://www . geesforgeks . org/factor-tree-of-a-number/](https://www.geeksforgeeks.org/factor-tree-of-a-given-number/)

因子树是理解一个数的因子的直观方法。它显示了所有的因素是如何从这个数字中推导出来的。这是一个特殊的图表，你可以找到一个数字的因子，然后是这些数字的因子，等等，直到你不能再因子。两端都是原数的质因数。
示例:

```
Input : v = 48
Output : Root of below tree
   48
   /\
  2  24
     /\
    2  12
       /\
      2  6
         /\
        2  3
```

因子树是递归创建的。使用二叉树。

1.  我们从一个数开始，找到可能的最小除数。
2.  然后，我们用最小除数除父数。
3.  我们将除数和商都存储为父数的两个子数。
4.  两个子对象都被递归地发送到函数中。
5.  如果找不到小于该数一半的除数，则两个子代存储为空。

## C++

```
// C++ program to construct Factor Tree for
// a given number
#include<bits/stdc++.h>
using namespace std;

// Tree node
struct Node
{
    struct Node *left, *right;
    int key;
};

// Utility function to create a new tree Node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return temp;
}

// Constructs factor tree for given value and stores
// root of tree at given reference.
void createFactorTree(struct Node **node_ref, int v)
{
    (*node_ref) = newNode(v);

    // the number is factorized
    for (int i = 2 ; i < v/2 ; i++)
    {
        if (v % i != 0)
          continue;

        // If we found a factor, we construct left
        // and right subtrees and return. Since we
        // traverse factors starting from smaller
        // to greater, left child will always have
        // smaller factor
        createFactorTree(&((*node_ref)->left), i);
        createFactorTree(&((*node_ref)->right), v/i);
        return;
    }
}

// Iterative method to find the height of Binary Tree
void printLevelOrder(Node *root)
{
    // Base Case
    if (root == NULL)  return;

    queue<Node *> q;
    q.push(root);

    while (q.empty() == false)
    {
        // Print front of queue and remove
        // it from queue
        Node *node = q.front();
        cout << node->key << " ";
        q.pop();
        if (node->left != NULL)
            q.push(node->left);
        if (node->right != NULL)
            q.push(node->right);
    }
}

// driver program
int main()
{
    int val = 48;// sample value
    struct Node *root = NULL;
    createFactorTree(&root, val);
    cout << "Level order traversal of "
            "constructed factor tree";
    printLevelOrder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to conFactor Tree for
// a given number
import java.util.*;
class GFG
{

  // Tree node
  static class Node
  {
    Node left, right;
    int key;
  };
  static Node root;

  // Utility function to create a new tree Node
  static Node newNode(int key)
  {
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return temp;
  }

  // Constructs factor tree for given value and stores
  // root of tree at given reference.
  static Node createFactorTree(Node node_ref, int v)
  {
    (node_ref) = newNode(v);

    // the number is factorized
    for (int i = 2 ; i < v/2 ; i++)
    {
      if (v % i != 0)
        continue;

      // If we found a factor, we conleft
      // and right subtrees and return. Since we
      // traverse factors starting from smaller
      // to greater, left child will always have
      // smaller factor
      node_ref.left = createFactorTree(((node_ref).left), i);
      node_ref.right =  createFactorTree(((node_ref).right), v/i);
      return node_ref;
    }
    return node_ref;
  }

  // Iterative method to find the height of Binary Tree
  static void printLevelOrder(Node root)
  {

    // Base Case
    if (root == null)  return;
    Queue<Node > q = new LinkedList<>();
    q.add(root);
    while (q.isEmpty() == false)
    {

      // Print front of queue and remove
      // it from queue
      Node node = q.peek();
      System.out.print(node.key + " ");
      q.remove();
      if (node.left != null)
        q.add(node.left);
      if (node.right != null)
        q.add(node.right);
    }
  }

  // Driver program
  public static void main(String[] args)
  {
    int val = 48;// sample value
    root = null;
    root = createFactorTree(root, val);
    System.out.println("Level order traversal of "+
                       "constructed factor tree");
    printLevelOrder(root);
  }
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program to conFactor Tree for
// a given number
using System;
using System.Collections.Generic;

public class GFG
{

  // Tree node
  public
    class Node
    {
      public
        Node left, right;
      public
        int key;
    };
  static Node root;

  // Utility function to create a new tree Node
  static Node newNode(int key)
  {
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return temp;
  }

  // Constructs factor tree for given value and stores
  // root of tree at given reference.
  static Node createFactorTree(Node node_ref, int v)
  {
    (node_ref) = newNode(v);

    // the number is factorized
    for (int i = 2 ; i < v/2 ; i++)
    {
      if (v % i != 0)
        continue;

      // If we found a factor, we conleft
      // and right subtrees and return. Since we
      // traverse factors starting from smaller
      // to greater, left child will always have
      // smaller factor
      node_ref.left = createFactorTree(((node_ref).left), i);
      node_ref.right =  createFactorTree(((node_ref).right), v/i);
      return node_ref;
    }
    return node_ref;
  }

  // Iterative method to find the height of Binary Tree
  static void printLevelOrder(Node root)
  {

    // Base Case
    if (root == null)  return;
    Queue<Node > q = new Queue<Node>();
    q.Enqueue(root);
    while (q.Count != 0)
    {

      // Print front of queue and remove
      // it from queue
      Node node = q.Peek();
      Console.Write(node.key + " ");
      q.Dequeue();
      if (node.left != null)
        q.Enqueue(node.left);
      if (node.right != null)
        q.Enqueue(node.right);
    }
  }

  // Driver program
  public static void Main(String[] args)
  {
    int val = 48;// sample value
    root = null;
    root = createFactorTree(root, val);
    Console.WriteLine("Level order traversal of "+
                      "constructed factor tree");
    printLevelOrder(root);
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
    // Javascript program to conFactor Tree for
    // a given number

    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.key = key;
        }
    }

    let root;

    // Utility function to create a new tree Node
    function newNode(key)
    {
      let temp = new Node(key);
      return temp;
    }

    // Constructs factor tree for given value and stores
    // root of tree at given reference.
    function createFactorTree(node_ref, v)
    {
      (node_ref) = newNode(v);

      // the number is factorized
      for (let i = 2 ; i < parseInt(v/2, 10) ; i++)
      {
        if (v % i != 0)
          continue;

        // If we found a factor, we conleft
        // and right subtrees and return. Since we
        // traverse factors starting from smaller
        // to greater, left child will always have
        // smaller factor
        node_ref.left = createFactorTree(((node_ref).left), i);
        node_ref.right =  createFactorTree(((node_ref).right), parseInt(v/i, 10));
        return node_ref;
      }
      return node_ref;
    }

    // Iterative method to find the height of Binary Tree
    function printLevelOrder(root)
    {

      // Base Case
      if (root == null)  return;
      let q = [];
      q.push(root);
      while (q.length > 0)
      {

        // Print front of queue and remove
        // it from queue
        let node = q[0];
        document.write(node.key + " ");
        q.shift();
        if (node.left != null)
          q.push(node.left);
        if (node.right != null)
          q.push(node.right);
      }
    }

    let val = 48;// sample value
    root = null;
    root = createFactorTree(root, val);
    document.write("Level order traversal of "+
                       "constructed factor tree" + "</br>");
    printLevelOrder(root);

   // This code is contributed by suresh07.
</script>
```

输出:

```
Level order traversal of constructed factor tree
48 2 24 2 12 2 6 2 3 
```

本文由**掌门人 Dey** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。