# 在二叉树中创建奇数和偶数的循环

> 原文:[https://www . geeksforgeeks . org/create-loops-of-the-loops-of-of-the-of-the-loops-in-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-](https://www.geeksforgeeks.org/create-loops-of-even-and-odd-values-in-a-binary-tree/)

给定一棵二叉树，其节点结构包含数据部分、左右指针和任意指针(abtr)。节点的值可以是任何正整数。问题是在二叉树中创建奇数和偶数循环。奇数循环是连接所有奇数节点的循环，类似地，偶数循环是连接偶数节点的循环。为了创建这样的循环，使用每个节点的 abtr 指针。奇数节点(具有奇数的节点)的 abtr 指针指向树中的某个其他奇数节点。一个循环必须以这样一种方式创建，即我们可以从任何节点遍历该节点所属的循环中的所有节点。
示例:

```
Consider the binary tree given below 

       1             
    /     \          
   2        3            
 /   \     /  \       
4     5   6    7   

Now with the help of abtr pointers of node, 
we connect odd and even nodes as:

Odd loop
1 -> 5 -> 3 -> 7 -> 1(again pointing to first node
                      in the loop)               

Even loop
2 -> 4 -> 6 -> 2(again pointing to first node
                 in the loop)

Nodes in the respective loop can be arranged in
any order. But from any node in the loop we should 
be able to traverse all the nodes in the loop.
```

**进场:**以下步骤为:

1.  将具有偶数和奇数的节点的指针分别添加到**偶数 _ptrs** 和**奇数 _ptrs** 数组中。通过任何树遍历，我们可以获得相应的节点指针。
2.  对于**偶数 _ptrs** 和**奇数 _ptrs** 阵列，执行:
    *   由于数组包含节点指针，考虑第 I 个索引处的元素，让它成为**节点**，并且分配的节点- > abtr =第(i+1)个索引处的元素。
    *   对于数组的最后一个元素，节点->abtr =索引 0 处的元素。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation to create odd and even loops
// in a binary tree
#include <bits/stdc++.h>

using namespace std;

// structure of a node
struct Node
{
    int data;
    Node *left, *right, *abtr;
};

// Utility function to create a new node
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = node->abtr = NULL;
    return node;
}

// preorder traversal to place the node pointer
// in the respective even_ptrs or odd_ptrs list
void preorderTraversal(Node *root, vector<Node*> *even_ptrs,
                       vector<Node*> *odd_ptrs)
{
    if (!root)
        return;

    // place node ptr in even_ptrs list if
    // node contains even number 
    if (root->data % 2 == 0)   
        (*even_ptrs).push_back(root);

    // else place node ptr in odd_ptrs list
    else
        (*odd_ptrs).push_back(root);

    preorderTraversal(root->left, even_ptrs, odd_ptrs);
    preorderTraversal(root->right, even_ptrs, odd_ptrs);
}

// function to create the even and odd loops
void createLoops(Node *root)
{

    vector<Node*> even_ptrs, odd_ptrs;
    preorderTraversal(root, &even_ptrs, &odd_ptrs);

    int i;

    // forming even loop
    for (i=1; i<even_ptrs.size(); i++)
        even_ptrs[i-1]->abtr = even_ptrs[i];

    // for the last element
    even_ptrs[i-1]->abtr = even_ptrs[0];   

    // Similarly forming odd loop
    for (i=1; i<odd_ptrs.size(); i++)
        odd_ptrs[i-1]->abtr = odd_ptrs[i];
    odd_ptrs[i-1]->abtr = odd_ptrs[0];
}

// traversing the loop from any random
// node in the loop
void traverseLoop(Node *start)
{
    Node *curr = start;
    do
    {
        cout << curr->data << " ";
        curr = curr->abtr;
    } while (curr != start);
}

// Driver program to test above
int main()
{
    // Binary tree formation
    struct Node* root = NULL;
    root = newNode(1);                   /*          1          */
    root->left = newNode(2);             /*       /    \        */
    root->right = newNode(3);            /*      2       3      */
    root->left->left = newNode(4);       /*    /  \    /   \    */
    root->left->right = newNode(5);      /*   4    5  6     7   */
    root->right->left = newNode(6);
    root->right->right = newNode(7);

    createLoops(root);

    // traversing odd loop from any
    // random odd node
    cout << "Odd nodes: ";
    traverseLoop(root->right);

    cout << endl << "Even nodes: ";
    // traversing even loop from any
    // random even node
    traverseLoop(root->left);   

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to create odd and even loops
// in a binary tree
import java.util.*;
class GFG
{

// structure of a node
static class Node
{
    int data;
    Node left, right, abtr;
};

// Utility function to create a new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = node.abtr = null;
    return node;
}
static Vector<Node> even_ptrs = new Vector<>();
static Vector<Node> odd_ptrs = new Vector<>();

// preorder traversal to place the node pointer
// in the respective even_ptrs or odd_ptrs list
static void preorderTraversal(Node root)
{
    if (root == null)
        return;

    // place node ptr in even_ptrs list if
    // node contains even number 
    if (root.data % 2 == 0)   
        (even_ptrs).add(root);

    // else place node ptr in odd_ptrs list
    else
        (odd_ptrs).add(root);

    preorderTraversal(root.left);
    preorderTraversal(root.right);
}

// function to create the even and odd loops
static void createLoops(Node root)
{
    preorderTraversal(root);  
    int i;

    // forming even loop
    for (i = 1; i < even_ptrs.size(); i++)
        even_ptrs.get(i - 1).abtr = even_ptrs.get(i);

    // for the last element
    even_ptrs.get(i - 1).abtr = even_ptrs.get(0);   

    // Similarly forming odd loop
    for (i = 1; i < odd_ptrs.size(); i++)
        odd_ptrs.get(i - 1).abtr = odd_ptrs.get(i);
    odd_ptrs.get(i - 1).abtr = odd_ptrs.get(0);
}

// traversing the loop from any random
// node in the loop
static void traverseLoop(Node start)
{
    Node curr = start;
    do
    {
        System.out.print(curr.data + " ");
        curr = curr.abtr;
    } while (curr != start);
}

// Driver code
public static void main(String[] args)
{

    // Binary tree formation
    Node root = null;
    root = newNode(1);                   /*          1          */
    root.left = newNode(2);             /*       /    \        */
    root.right = newNode(3);            /*      2       3      */
    root.left.left = newNode(4);       /*    /  \    /   \    */
    root.left.right = newNode(5);      /*   4    5  6     7   */
    root.right.left = newNode(6);
    root.right.right = newNode(7);  
    createLoops(root);

    // traversing odd loop from any
    // random odd node
    System.out.print("Odd nodes: ");
    traverseLoop(root.right);  
    System.out.print( "\nEven nodes: ");

    // traversing even loop from any
    // random even node
    traverseLoop(root.left);   
}
}

// This code is contributed by aashish1995
```

## 蟒蛇 3

```
# Python3 implementation to create odd and even loops
# in a binary tree

# structure of a node
class Node:
    def __init__(self, x):
        self.data = x
        self.left = None
        self.right = None
        self.abtr = None

even_ptrs  = []
odd_ptrs = []

# preorder traversal to place the node pointer
# in the respective even_ptrs or odd_ptrs list
def preorderTraversal(root):
    global even_ptrs, odd_ptrs

    if (not root):
        return

    # place node ptr in even_ptrs list if
    # node contains even number
    if (root.data % 2 == 0):
        even_ptrs.append(root)

    # else place node ptr in odd_ptrs list
    else:
        odd_ptrs.append(root)

    preorderTraversal(root.left)
    preorderTraversal(root.right)

# function to create the even and odd loops
def createLoops(root):
    preorderTraversal(root)

    # forming even loop
    i = 1
    while i < len(even_ptrs):
        even_ptrs[i - 1].abtr = even_ptrs[i]
        i += 1

    # for the last element
    even_ptrs[i - 1].abtr = even_ptrs[0]

    # Similarly forming odd loop
    i = 1
    while i < len(odd_ptrs):
        odd_ptrs[i - 1].abtr = odd_ptrs[i]
        i += 1
    odd_ptrs[i - 1].abtr = odd_ptrs[0]

#traversing the loop from any random
#node in the loop
def traverseLoop(start):
    curr = start

    while True and curr:
        print(curr.data, end = " ")
        curr = curr.abtr

        if curr == start:
            break
    print()

# Driver program to test above
if __name__ == '__main__':

    # Binary tree formation
    root = None
    root = Node(1)                 #/*         1         */
    root.left = Node(2)        #     /*     / \     */
    root.right = Node(3)         #/*     2     3     */
    root.left.left = Node(4)     #/* / \ / \ */
    root.left.right = Node(5)     #/* 4 5 6     7 */
    root.right.left = Node(6)
    root.right.right = Node(7)

    createLoops(root)

    # traversing odd loop from any
    # random odd node
    print("Odd nodes:", end = " ")
    traverseLoop(root.right)

    print("Even nodes:", end = " ")

    # traversing even loop from any
    # random even node
    traverseLoop(root.left)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to create odd and even loops
// in a binary tree
using System;
using System.Collections.Generic;
class GFG
{

  // structure of a node
  public
    class Node
    {
      public
        int data;
      public
        Node left, right, abtr;
    };

  // Utility function to create a new node
  static Node newNode(int data)
  {
    Node node = new Node();
    node.data = data;
    node.left = node.right = node.abtr = null;
    return node;
  }
  static List<Node> even_ptrs = new List<Node>();
  static List<Node> odd_ptrs = new List<Node>();

  // preorder traversal to place the node pointer
  // in the respective even_ptrs or odd_ptrs list
  static void preorderTraversal(Node root)
  {
    if (root == null)
      return;

    // place node ptr in even_ptrs list if
    // node contains even number 
    if (root.data % 2 == 0)   
      (even_ptrs).Add(root);

    // else place node ptr in odd_ptrs list
    else
      (odd_ptrs).Add(root);
    preorderTraversal(root.left);
    preorderTraversal(root.right);
  }

  // function to create the even and odd loops
  static void createLoops(Node root)
  {
    preorderTraversal(root);  
    int i;

    // forming even loop
    for (i = 1; i < even_ptrs.Count; i++)
      even_ptrs[i - 1].abtr = even_ptrs[i];

    // for the last element
    even_ptrs[i - 1].abtr = even_ptrs[0];   

    // Similarly forming odd loop
    for (i = 1; i < odd_ptrs.Count; i++)
      odd_ptrs[i - 1].abtr = odd_ptrs[i];
    odd_ptrs[i - 1].abtr = odd_ptrs[0];
  }

  // traversing the loop from any random
  // node in the loop
  static void traverseLoop(Node start)
  {
    Node curr = start;
    do
    {
      Console.Write(curr.data + " ");
      curr = curr.abtr;
    } while (curr != start);
  }

  // Driver code
  public static void Main(String[] args)
  {

    // Binary tree formation
    Node root = null;
    root = newNode(1);                   /*          1          */
    root.left = newNode(2);             /*       /    \        */
    root.right = newNode(3);            /*      2       3      */
    root.left.left = newNode(4);       /*    /  \    /   \    */
    root.left.right = newNode(5);      /*   4    5  6     7   */
    root.right.left = newNode(6);
    root.right.right = newNode(7);  
    createLoops(root);

    // traversing odd loop from any
    // random odd node
    Console.Write("Odd nodes: ");
    traverseLoop(root.right);  
    Console.Write( "\nEven nodes: ");

    // traversing even loop from any
    // random even node
    traverseLoop(root.left);   
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript implementation to
// create odd and even loops
// in a binary tree

// structure of a node
class Node
{
    // Utility function to create a new node
    constructor(data)
    {
        this.data=data;
        this.left=this.right=this.abtr =null;
    }

}

let even_ptrs = [];
let odd_ptrs = [];

// preorder traversal to place the node pointer
// in the respective even_ptrs or odd_ptrs list
function preorderTraversal(root)
{
    if (root == null)
        return;

    // place node ptr in even_ptrs list if
    // node contains even number
    if (root.data % 2 == 0)  
        (even_ptrs).push(root);

    // else place node ptr in odd_ptrs list
    else
        (odd_ptrs).push(root);

    preorderTraversal(root.left);
    preorderTraversal(root.right);
}

// function to create the even and odd loops
function createLoops(root)
{
    preorderTraversal(root); 
    let i;

    // forming even loop
    for (i = 1; i < even_ptrs.length; i++)
        even_ptrs[i-1].abtr = even_ptrs[i];

    // for the last element
    even_ptrs[i-1].abtr = even_ptrs[0];  

    // Similarly forming odd loop
    for (i = 1; i < odd_ptrs.length; i++)
        odd_ptrs[i-1].abtr = odd_ptrs[i];
    odd_ptrs[i-1].abtr = odd_ptrs[0];
}

// traversing the loop from any random
// node in the loop
function traverseLoop(start)
{
    let curr = start;
    do
    {
        document.write(curr.data + " ");
        curr = curr.abtr;
    } while (curr != start);
}

// Driver code

        /*          1          */
        /*       /    \        */
        /*      2       3      */
        /*    /  \    /   \    */
        /*   4    5  6     7   */

// Binary tree formation
let root = null;
root = new Node(1);                  
root.left = new Node(2);            
root.right = new Node(3);           
root.left.left = new Node(4);      
root.left.right = new Node(5);     
root.right.left = new Node(6);
root.right.right = new Node(7); 
createLoops(root);

// traversing odd loop from any
// random odd node
document.write("Odd nodes: ");
traverseLoop(root.right); 
document.write( "<br>Even nodes: ");

// traversing even loop from any
// random even node
traverseLoop(root.left);  

// This code is contributed by patel2127

</script>
```

**输出:**

```
Odd nodes: 3 7 1 5
Even nodes: 2 4 6
```

时间复杂度:等于任意递归树遍历的时间复杂度为 O(n)
本文由**阿尤什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。