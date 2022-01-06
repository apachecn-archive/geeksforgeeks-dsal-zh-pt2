# 合并两个额外空间有限的 BSTs】

> 原文:[https://www . geesforgeks . org/merge-two-bsts-with-limited-extra-space/](https://www.geeksforgeeks.org/merge-two-bsts-with-limited-extra-space/)

给定两个二分搜索法树，以排序的形式打印两个树的元素。预期的时间复杂度是 O(m+n)，其中 m 是第一棵树中的节点数，n 是第二棵树中的节点数。最大允许辅助空间为 O(第一棵树的高度+第二棵树的高度)。
**例:**

```
First BST 
       3
    /     \
   1       5
Second BST
    4
  /   \
2       6
Output: 1 2 3 4 5 6

First BST 
          8
         / \
        2   10
       /
      1
Second BST 
          5
         / 
        3  
       /
      0
Output: 0 1 2 3 5 8 10 
```

来源:谷歌面试问题

之前也讨论过类似的问题。让我们首先讨论已经讨论过的[之前的帖子](https://www.geeksforgeeks.org/merge-two-balanced-binary-search-trees/)的方法，该帖子是针对平衡 BST 的。这里也可以应用方法 1，但是在最坏的情况下，时间复杂度将是 O(n^2)。这里也可以应用方法 2，但是所需的额外空间将是 O(n)，这违反了本问题中给出的约束。这里可以应用方法 3，但是对于不平衡的 BST，方法 3 的步骤 3 不能在 O(n)中完成。
感谢[库马尔](https://www.geeksforgeeks.org/forums/users/gautam5669/)提出以下解决方案。
思路是使用[迭代顺序遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)。我们为两个 BST 使用两个辅助堆栈。因为我们需要以排序的形式打印元素，所以无论何时我们从任何树中获得一个较小的元素，我们都会打印它。如果元素更大，那么我们就把它推回到堆栈中，用于下一次迭代。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Structure of a BST Node
class node
{
    public:
    int data;
    node *left;
    node *right;
};

//.................... START OF STACK RELATED STUFF....................
// A stack node
class snode
{
    public:
    node *t;
    snode *next;
};

// Function to add an element k to stack
void push(snode **s, node *k)
{
    snode *tmp = new snode();

    //perform memory check here
    tmp->t = k;
    tmp->next = *s;
    (*s) = tmp;
}

// Function to pop an element t from stack
node *pop(snode **s)
{
    node *t;
    snode *st;
    st=*s;
    (*s) = (*s)->next;
    t = st->t;
    free(st);
    return t;
}

// Function to check whether the stack is empty or not
int isEmpty(snode *s)
{
    if (s == NULL )
        return 1;

    return 0;
}
//.................... END OF STACK RELATED STUFF....................

/* Utility function to create a new Binary Tree node */
node* newNode (int data)
{
    node *temp = new node;
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

/* A utility function to print Inorder traversal of a Binary Tree */
void inorder(node *root)
{
    if (root != NULL)
    {
        inorder(root->left);
        cout<<root->data<<" ";
        inorder(root->right);
    }
}

// The function to print data of two BSTs in sorted order
void merge(node *root1, node *root2)
{
    // s1 is stack to hold nodes of first BST
    snode *s1 = NULL;

    // Current node of first BST
    node *current1 = root1;

    // s2 is stack to hold nodes of second BST
    snode *s2 = NULL;

    // Current node of second BST
    node *current2 = root2;

    // If first BST is empty, then output is inorder
    // traversal of second BST
    if (root1 == NULL)
    {
        inorder(root2);
        return;
    }
    // If second BST is empty, then output is inorder
    // traversal of first BST
    if (root2 == NULL)
    {
        inorder(root1);
        return ;
    }

    // Run the loop while there are nodes not yet printed.
    // The nodes may be in stack(explored, but not printed)
    // or may be not yet explored
    while (current1 != NULL || !isEmpty(s1) ||
        current2 != NULL || !isEmpty(s2))
    {
        // Following steps follow iterative Inorder Traversal
        if (current1 != NULL || current2 != NULL )
        {
            // Reach the leftmost node of both BSTs and push ancestors of
            // leftmost nodes to stack s1 and s2 respectively
            if (current1 != NULL)
            {
                push(&s1, current1);
                current1 = current1->left;
            }
            if (current2 != NULL)
            {
                push(&s2, current2);
                current2 = current2->left;
            }

        }
        else
        {
            // If we reach a NULL node and either of the stacks is empty,
            // then one tree is exhausted, print the other tree
            if (isEmpty(s1))
            {
                while (!isEmpty(s2))
                {
                    current2 = pop (&s2);
                    current2->left = NULL;
                    inorder(current2);
                }
                return ;
            }
            if (isEmpty(s2))
            {
                while (!isEmpty(s1))
                {
                    current1 = pop (&s1);
                    current1->left = NULL;
                    inorder(current1);
                }
                return ;
            }

            // Pop an element from both stacks and compare the
            // popped elements
            current1 = pop(&s1);
            current2 = pop(&s2);

            // If element of first tree is smaller, then print it
            // and push the right subtree. If the element is larger,
            // then we push it back to the corresponding stack.
            if (current1->data < current2->data)
            {
                cout<<current1->data<<" ";
                current1 = current1->right;
                push(&s2, current2);
                current2 = NULL;
            }
            else
            {
                cout<<current2->data<<" ";
                current2 = current2->right;
                push(&s1, current1);
                current1 = NULL;
            }
        }
    }
}

/* Driver program to test above functions */
int main()
{
    node *root1 = NULL, *root2 = NULL;

    /* Let us create the following tree as first tree
            3
        / \
        1 5
    */
    root1 = newNode(3);
    root1->left = newNode(1);
    root1->right = newNode(5);

    /* Let us create the following tree as second tree
            4
        / \
        2 6
    */
    root2 = newNode(4);
    root2->left = newNode(2);
    root2->right = newNode(6);

    // Print sorted nodes of both trees
    merge(root1, root2);

    return 0;
}

//This code is contributed by rathbhupendra
```

## C

```
#include<stdio.h>
#include<stdlib.h>

// Structure of a BST Node
struct node
{
    int data;
    struct node *left;
    struct node *right;
};

//.................... START OF STACK RELATED STUFF....................
// A stack node
struct snode
{
    struct node  *t;
    struct snode *next;
};

// Function to add an element k to stack
void push(struct snode **s, struct node *k)
{
    struct snode *tmp = (struct snode *) malloc(sizeof(struct snode));

    //perform memory check here
    tmp->t = k;
    tmp->next = *s;
    (*s) = tmp;
}

// Function to pop an element t from stack
struct node *pop(struct snode **s)
{
    struct  node *t;
    struct snode *st;
    st=*s;
    (*s) = (*s)->next;
    t = st->t;
    free(st);
    return t;
}

// Function to check whether the stack is empty or not
int isEmpty(struct snode *s)
{
    if (s == NULL )
        return 1;

    return 0;
}
//.................... END OF STACK RELATED STUFF....................

/* Utility function to create a new Binary Tree node */
struct node* newNode (int data)
{
    struct node *temp = (struct node*)malloc(sizeof(struct node));
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

/* A utility function to print Inorder traversal of a Binary Tree */
void inorder(struct node *root)
{
    if (root != NULL)
    {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

// The function to print data of two BSTs in sorted order
void  merge(struct node *root1, struct node *root2)
{
    // s1 is stack to hold nodes of first BST
    struct snode *s1 = NULL;

    // Current node of first BST
    struct node  *current1 = root1;

    // s2 is stack to hold nodes of second BST
    struct snode *s2 = NULL;

    // Current node of second BST
    struct node  *current2 = root2;

    // If first BST is empty, then output is inorder
    // traversal of second BST
    if (root1 == NULL)
    {
        inorder(root2);
        return;
    }
    // If second BST is empty, then output is inorder
    // traversal of first BST
    if (root2 == NULL)
    {
        inorder(root1);
        return ;
    }

    // Run the loop while there are nodes not yet printed.
    // The nodes may be in stack(explored, but not printed)
    // or may be not yet explored
    while (current1 != NULL || !isEmpty(s1) ||
          current2 != NULL || !isEmpty(s2))
    {
        // Following steps follow iterative Inorder Traversal
        if (current1 != NULL || current2 != NULL )
        {
            // Reach the leftmost node of both BSTs and push ancestors of
            // leftmost nodes to stack s1 and s2 respectively
            if (current1 != NULL)
            {
                push(&s1, current1);
                current1 = current1->left;
            }
            if (current2 != NULL)
            {
                push(&s2, current2);
                current2 = current2->left;
            }

        }
        else
        {
            // If we reach a NULL node and either of the stacks is empty,
            // then one tree is exhausted, ptint the other tree
            if (isEmpty(s1))
            {
                while (!isEmpty(s2))
                {
                    current2 = pop (&s2);
                    current2->left = NULL;
                    inorder(current2);
                }
                return ;
            }
            if (isEmpty(s2))
            {
                while (!isEmpty(s1))
                {
                    current1 = pop (&s1);
                    current1->left = NULL;
                    inorder(current1);
                }
                return ;
            }

            // Pop an element from both stacks and compare the
            // popped elements
            current1 = pop(&s1);
            current2 = pop(&s2);

            // If element of first tree is smaller, then print it
            // and push the right subtree. If the element is larger,
            // then we push it back to the corresponding stack.
            if (current1->data < current2->data)
            {
                printf("%d ", current1->data);
                current1 = current1->right;
                push(&s2, current2);
                current2 = NULL;
            }
            else
            {
                printf("%d ", current2->data);
                current2 = current2->right;
                push(&s1, current1);
                current1 = NULL;
            }
        }
    }
}

/* Driver program to test above functions */
int main()
{
    struct node  *root1 = NULL, *root2 = NULL;

    /* Let us create the following tree as first tree
            3
          /  \
         1    5
     */
    root1 = newNode(3);
    root1->left = newNode(1);
    root1->right = newNode(5);

    /* Let us create the following tree as second tree
            4
          /  \
         2    6
     */
    root2 = newNode(4);
    root2->left = newNode(2);
    root2->right = newNode(6);

    // Print sorted nodes of both trees
    merge(root1, root2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
public class Merge2BST
{

    /* A utility function to print
    Inorder traversal of a Binary Tree */
    static void inorder(Node root)
    {
        if (root != null)
        {
            inorder(root.left);
            System.out.print(root.data + " ");
            inorder(root.right);
        }
    }

    // The function to print data of two BSTs in sorted order
    static void merge(Node root1, Node root2)
    {
        // s1 is stack to hold nodes of first BST
        SNode s1 = new SNode();

        // Current node of first BST
        Node current1 = root1;

        // s2 is stack to hold nodes of second BST
        SNode s2 = new SNode();

        // Current node of second BST
        Node current2 = root2;

        // If first BST is empty, then output is inorder
        // traversal of second BST
        if (root1 == null)
        {
            inorder(root2);
            return;
        }

        // If second BST is empty, then output is inorder
        // traversal of first BST
        if (root2 == null)
        {
            inorder(root1);
            return ;
        }

        // Run the loop while there are nodes not yet printed.
        // The nodes may be in stack(explored, but not printed)
        // or may be not yet explored
        while (current1 != null || !s1.isEmpty() ||
            current2 != null || !s2.isEmpty())
        {

            // Following steps follow iterative Inorder Traversal
            if (current1 != null || current2 != null )
            {
                // Reach the leftmost node of both BSTs and push ancestors of
                // leftmost nodes to stack s1 and s2 respectively
                if (current1 != null)
                {

                    s1.push( current1);
                    current1 = current1.left;
                }
                if (current2 != null)
                {
                    s2.push( current2);
                    current2 = current2.left;
                }

            }
            else
            {

                // If we reach a NULL node and either of the stacks is empty,
                // then one tree is exhausted, ptint the other tree
                if (s1.isEmpty())
                {
                    while (!s2.isEmpty())
                    {
                        current2 = s2.pop ();
                        current2.left = null;
                        inorder(current2);
                    }
                    return ;
                }
                if (s2.isEmpty())
                {
                    while (!s1.isEmpty())
                    {
                        current1 = s1.pop ();
                        current1.left = null;
                        inorder(current1);
                    }
                    return ;
                }

                // Pop an element from both stacks and compare the
                // popped elements
                current1 = s1.pop();

                current2 = s2.pop();

                // If element of first tree is smaller, then print it
                // and push the right subtree. If the element is larger,
                // then we push it back to the corresponding stack.
                if (current1.data < current2.data)
                {
                    System.out.print(current1.data + " ");
                    current1 = current1.right;
                    s2.push( current2);
                    current2 = null;
                }
                else
                {
                    System.out.print(current2.data + " ");
                    current2 = current2.right;
                    s1.push( current1);
                    current1 = null;
                }
            }
        }
        System.out.println(s1.t);
        System.out.println(s2.t);
    }

    /* Driver code */
    public static void main(String[]args)
    {
        Node root1 = null, root2 = null;

        /* Let us create the following tree as first tree
                3
            / \
            1 5
        */
        root1 = new Node(3) ;
        root1.left = new Node(1);
        root1.right = new Node(5);

        /* Let us create the following tree as second tree
                4
            / \
            2 6
        */
        root2 = new Node(4) ;
        root2.left = new Node(2);
        root2.right = new Node(6);

        // Print sorted nodes of both trees
        merge(root1, root2);
    }
}

// Structure of a BST Node
class Node
{

    int data;
    Node left;
    Node right;
    public Node(int data)
    {
        // TODO Auto-generated constructor stub
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// A stack node
class SNode
{
    SNode head;
    Node t;
    SNode next;

    // Function to add an element k to stack
    void push(Node k)
    {
        SNode tmp = new SNode();

        // Perform memory check here
        tmp.t = k;
        tmp.next = this.head;
        this.head = tmp;
    }

    // Function to pop an element t from stack
    Node pop()
    {

        SNode st;
        st = this.head;
        head = head.next;

        return st.t;
    }

    // Function to check whether the stack is empty or not
    boolean isEmpty( )
    {
        if (this.head == null )
            return true;

        return false;
    }
}

// This code is contributed by nidhisebastian008
```

## 蟒蛇 3

```
# Class to create a new Tree Node
class newNode:
    def __init__(self, data: int):
        self.data = data
        self.left = None
        self.right = None

def inorder(root: newNode):

    if root:
        inorder(root.left)
        print(root.data, end=" ")
        inorder(root.right)

def merge(root1: newNode, root2: newNode):

    # s1 is stack to hold nodes of first BST
    s1 = []

    # Current node of first BST
    current1 = root1

    # s2 is stack to hold nodes of first BST
    s2 = []

    # Current node of second BST
    current2 = root2

    # If first BST is empty then the output is the
    # inorder traversal of the second BST
    if not root1:
        return inorder(root2)

    # If the second BST is empty then the output is the
    # inorder traversal of the first BST
    if not root2:
        return inorder(root1)

    # Run the loop while there are nodes not yet printed.
    # The nodes may be in stack(explored, but not printed)
    # or may be not yet explored
    while current1 or s1 or current2 or s2:

        # Following steps follow iterative Inorder Traversal
        if current1 or current2:

            # Reach the leftmost node of both BSTs and push ancestors of
            # leftmost nodes to stack s1 and s2 respectively
            if current1:
                s1.append(current1)
                current1 = current1.left

            if current2:
                s2.append(current2)
                current2 = current2.left

        else:

            # If we reach a NULL node and either of the stacks is empty,
            # then one tree is exhausted, ptint the other tree

            if not s1:
                while s2:
                    current2 = s2.pop()
                    current2.left = None
                    inorder(current2)
                    return
            if not s2:
                while s1:
                    current1 = s1.pop()
                    current1.left = None
                    inorder(current1)
                    return

            # Pop an element from both stacks and compare the
            # popped elements
            current1 = s1.pop()
            current2 = s2.pop()

            # If element of first tree is smaller, then print it
            # and push the right subtree. If the element is larger,
            # then we push it back to the corresponding stack.
            if current1.data < current2.data:
                print(current1.data, end=" ")
                current1 = current1.right
                s2.append(current2)
                current2 = None

            else:
                print(current2.data, end=" ")
                current2 = current2.right
                s1.append(current1)
                current1 = None

# Driver code

def main():

    # Let us create the following tree as first tree
    #     3
    #     / \
    # 1 5

    root1 = newNode(3)
    root1.left = newNode(1)
    root1.right = newNode(5)

    # Let us create the following tree as second tree
    #     4
    #     / \
    # 2 6
    #

    root2 = newNode(4)
    root2.left = newNode(2)
    root2.right = newNode(6)

    merge(root1, root2)

if __name__ == "__main__":
    main()

# This code is contributed by Koushik Reddy Bukkasamudram
```

## C#

```
// C# program to implement the
// above approach
using System;
class Merge2BST{

/* A utility function to print
   Inorder traversal of a Binary
   Tree */
static void inorder(Node root)
{
  if (root != null)
  {
    inorder(root.left);
    Console.Write(root.data + " ");
    inorder(root.right);
  }
}

// The function to print data
// of two BSTs in sorted order
static void merge(Node root1,
                  Node root2)
{
  // s1 is stack to hold nodes
  // of first BST
  SNode s1 = new SNode();

  // Current node of first BST
  Node current1 = root1;

  // s2 is stack to hold nodes
  // of second BST
  SNode s2 = new SNode();

  // Current node of second BST
  Node current2 = root2;

  // If first BST is empty, then
  // output is inorder traversal
  // of second BST
  if (root1 == null)
  {
    inorder(root2);
    return;
  }

  // If second BST is empty,
  // then output is inorder
  // traversal of first BST
  if (root2 == null)
  {
    inorder(root1);
    return ;
  }

  // Run the loop while there
  // are nodes not yet printed.
  // The nodes may be in stack
  // (explored, but not printed)
  // or may be not yet explored
  while (current1 != null ||
         !s1.isEmpty() ||
         current2 != null ||
         !s2.isEmpty())
  {
    // Following steps follow
    // iterative Inorder Traversal
    if (current1 != null ||
        current2 != null)
    {
      // Reach the leftmost node of
      // both BSTs and push ancestors
      // of leftmost nodes to stack
      // s1 and s2 respectively
      if (current1 != null)
      {
        s1.push(current1);
        current1 = current1.left;
      }
      if (current2 != null)
      {
        s2.push(current2);
        current2 = current2.left;
      }
    }
    else
    {
      // If we reach a NULL node and
      // either of the stacks is empty,
      // then one tree is exhausted,
      // print the other tree
      if (s1.isEmpty())
      {
        while (!s2.isEmpty())
        {
          current2 = s2.pop ();
          current2.left = null;
          inorder(current2);
        }
        return;
      }
      if (s2.isEmpty())
      {
        while (!s1.isEmpty())
        {
          current1 = s1.pop ();
          current1.left = null;
          inorder(current1);
        }
        return;
      }

      // Pop an element from both
      // stacks and compare the
      // popped elements
      current1 = s1.pop();

      current2 = s2.pop();

      // If element of first tree is
      // smaller, then print it
      // and push the right subtree.
      // If the element is larger,
      // then we push it back to the
      // corresponding stack.
      if (current1.data < current2.data)
      {
        Console.Write(current1.data + " ");
        current1 = current1.right;
        s2.push( current2);
        current2 = null;
      }
      else
      {
        Console.Write(current2.data + " ");
        current2 = current2.right;
        s1.push( current1);
        current1 = null;
      }
    }
  }
  Console.Write(s1.t + "\n");
  Console.Write(s2.t + "\n");
}

// Driver code
public static void Main(string[]args)
{
  Node root1 = null,
       root2 = null;

  /* Let us create the
     following tree as
     first tree

             3
            / \
            1 5
  */
  root1 = new Node(3) ;
  root1.left = new Node(1);
  root1.right = new Node(5);

  /* Let us create the following
     tree as second tree

             4
            / \
            2 6
  */
  root2 = new Node(4) ;
  root2.left = new Node(2);
  root2.right = new Node(6);

  // Print sorted nodes of
  // both trees
  merge(root1, root2);
}
}

// Structure of a BST Node
class Node{     

public int data;
public Node left;
public Node right;

public Node(int data)
{
  // TODO Auto-generated
  // constructor stub
  this.data = data;
  this.left = null;
  this.right = null;
}
}

// A stack node
class SNode{

SNode head;
public Node t;
SNode next;

// Function to add an element
// k to stack
public void push(Node k)
{
  SNode tmp = new SNode();

  // Perform memory check here
  tmp.t = k;
  tmp.next = this.head;
  this.head = tmp;
}

// Function to pop an element
// t from stack
public Node pop()
{
  SNode st;
  st = this.head;
  head = head.next;

  return st.t;
}

// Function to check whether
// the stack is empty or not
public bool isEmpty()
{
  if (this.head == null )
    return true;

  return false;
}
}

// This code is contributed by Rutvik_56
```

## java 描述语言

```
<script>

      // JavaScript program to implement the
      // above approach

      // Structure of a BST Node
      class Node {
        constructor(data) {
          // TODO Auto-generated
          // constructor stub
          this.data = data;
          this.left = null;
          this.right = null;
        }
      }

      // A stack node
      class SNode {
        constructor() {
          this.head = null;
          this.t = null;
          this.next = null;
        }

        // Function to add an element
        // k to stack
        push(k) {
          var tmp = new SNode();

          // Perform memory check here
          tmp.t = k;
          tmp.next = this.head;
          this.head = tmp;
        }

        // Function to pop an element
        // t from stack
        pop() {
          var st;
          st = this.head;
          this.head = this.head.next;

          return st.t;
        }

        // Function to check whether
        // the stack is empty or not
        isEmpty() {
          if (this.head == null) return true;

          return false;
        }
      }

      /* A utility function to print
        Inorder traversal of a Binary
        Tree */
      function inorder(root) {
        if (root != null) {
          inorder(root.left);
          document.write(root.data + " ");
          inorder(root.right);
        }
      }

      // The function to print data
      // of two BSTs in sorted order
      function merge(root1, root2) {
        // s1 is stack to hold nodes
        // of first BST
        var s1 = new SNode();

        // Current node of first BST
        var current1 = root1;

        // s2 is stack to hold nodes
        // of second BST
        var s2 = new SNode();

        // Current node of second BST
        var current2 = root2;

        // If first BST is empty, then
        // output is inorder traversal
        // of second BST
        if (root1 == null) {
          inorder(root2);
          return;
        }

        // If second BST is empty,
        // then output is inorder
        // traversal of first BST
        if (root2 == null) {
          inorder(root1);
          return;
        }

        // Run the loop while there
        // are nodes not yet printed.
        // The nodes may be in stack
        // (explored, but not printed)
        // or may be not yet explored
        while (
          current1 != null ||
          !s1.isEmpty() ||
          current2 != null ||
          !s2.isEmpty()
        ) {
          // Following steps follow
          // iterative Inorder Traversal
          if (current1 != null || current2 != null) {
            // Reach the leftmost node of
            // both BSTs and push ancestors
            // of leftmost nodes to stack
            // s1 and s2 respectively
            if (current1 != null) {
              s1.push(current1);
              current1 = current1.left;
            }
            if (current2 != null) {
              s2.push(current2);
              current2 = current2.left;
            }
          } else {
            // If we reach a NULL node and
            // either of the stacks is empty,
            // then one tree is exhausted,
            // print the other tree
            if (s1.isEmpty()) {
              while (!s2.isEmpty()) {
                current2 = s2.pop();
                current2.left = null;
                inorder(current2);
              }
              return;
            }
            if (s2.isEmpty()) {
              while (!s1.isEmpty()) {
                current1 = s1.pop();
                current1.left = null;
                inorder(current1);
              }
              return;
            }

            // Pop an element from both
            // stacks and compare the
            // popped elements
            current1 = s1.pop();

            current2 = s2.pop();

            // If element of first tree is
            // smaller, then print it
            // and push the right subtree.
            // If the element is larger,
            // then we push it back to the
            // corresponding stack.
            if (current1.data < current2.data) {
              document.write(current1.data + " ");
              current1 = current1.right;
              s2.push(current2);
              current2 = null;
            } else {
              document.write(current2.data + " ");
              current2 = current2.right;
              s1.push(current1);
              current1 = null;
            }
          }
        }
        document.write(s1.t + "<br>");
        document.write(s2.t + "<br>");
      }

      // Driver code
      var root1 = null,
        root2 = null;

      /* Let us create the
    following tree as
    first tree

            3
            / \
            1 5
*/
      root1 = new Node(3);
      root1.left = new Node(1);
      root1.right = new Node(5);

      /* Let us create the following
    tree as second tree

            4
            / \
            2 6
*/
      root2 = new Node(4);
      root2.left = new Node(2);
      root2.right = new Node(6);

      // Print sorted nodes of
      // both trees
      merge(root1, root2);

</script>
```

**Output:** 

```
1 2 3 4 5 6
```

**时间复杂度:** O(m+n)
**辅助空间:** O(第一棵树的高度+第二棵树的高度)
发现有不正确的地方请写评论，或者想分享以上讨论话题的更多信息。