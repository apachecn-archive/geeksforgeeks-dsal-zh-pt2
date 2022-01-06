# 仅使用单个递归函数

计算加起来等于给定值 x 的子树

> 原文:[https://www . geesforgeks . org/count-subtrass-sum-给定值-x/](https://www.geeksforgeeks.org/count-subtress-sum-given-value-x/)

给定一个包含 **n 个**节点的二叉树。问题是仅使用单个递归函数来计算总节点数据和等于给定值的子树。

**示例:**

```
Input : 
             5
           /   \  
        -10     3
        /  \   /  \
       9    8 -4   7

       x = 7

Output : 2
There are 2 subtrees with sum 7.

1st one is leaf node:
7.

2nd one is:

 -10
 /   \
 9     8
```

**来源:** [微软面试心得|第 157 集。](https://www.geeksforgeeks.org/microsoft-interview-experience-set-157-campus/)

**进场:**

```
countSubtreesWithSumX(root, count, x)
    if !root then
        return 0

    ls = countSubtreesWithSumX(root->left, count, x)
    rs = countSubtreesWithSumX(root->right, count, x)
    sum = ls + rs + root->data

    if sum == x then
    count++
    return sum

countSubtreesWithSumXUtil(root, x)
    if !root then
        return 0

    Initialize count = 0
    ls = countSubtreesWithSumX(root->left, count, x)
    rs = countSubtreesWithSumX(root->right, count, x)

    if (ls + rs + root->data) == x
        count++
    return count
```

## C++

```
// C++ implementation to count subtrees that
// sum up to a given value x
#include <bits/stdc++.h>

using namespace std;

// structure of a node of binary tree
struct Node {
    int data;
    Node *left, *right;
};

// function to get a new node
Node* getNode(int data)
{
    // allocate space
    Node* newNode = (Node*)malloc(sizeof(Node));

    // put in the data
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// function to count subtrees that
// sum up to a given value x
int countSubtreesWithSumX(Node* root,
                          int& count, int x)
{
    // if tree is empty
    if (!root)
        return 0;

    // sum of nodes in the left subtree
    int ls = countSubtreesWithSumX(root->left, count, x);

    // sum of nodes in the right subtree
    int rs = countSubtreesWithSumX(root->right, count, x);

    // sum of nodes in the subtree rooted
    // with 'root->data'
    int sum = ls + rs + root->data;

    // if true
    if (sum == x)
        count++;

    // return subtree's nodes sum
    return sum;
}

// utility function to count subtrees that
// sum up to a given value x
int countSubtreesWithSumXUtil(Node* root, int x)
{
    // if tree is empty
    if (!root)
        return 0;

    int count = 0;

    // sum of nodes in the left subtree
    int ls = countSubtreesWithSumX(root->left, count, x);

    // sum of nodes in the right subtree
    int rs = countSubtreesWithSumX(root->right, count, x);

    // if tree's nodes sum == x
    if ((ls + rs + root->data) == x)
        count++;

    // required count of subtrees
    return count;
}

// Driver program to test above
int main()
{
    /* binary tree creation   
                5
              /   \ 
           -10     3
           /  \   /  \
          9    8 -4   7
    */
    Node* root = getNode(5);
    root->left = getNode(-10);
    root->right = getNode(3);
    root->left->left = getNode(9);
    root->left->right = getNode(8);
    root->right->left = getNode(-4);
    root->right->right = getNode(7);

    int x = 7;

    cout << "Count = "
         << countSubtreesWithSumXUtil(root, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if
// there is a subtree with
// given sum
import java.util.*;
class GFG
{

// structure of a node
// of binary tree
static class Node
{
    int data;
    Node left, right;
}

static class INT
{
    int v;
    INT(int a)
    {
        v = a;
    }
}

// function to get a new node
static Node getNode(int data)
{
    // allocate space
    Node newNode = new Node();

    // put in the data
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;
}

// function to count subtrees that
// sum up to a given value x
static int countSubtreesWithSumX(Node root,
                          INT count, int x)
{
    // if tree is empty
    if (root == null)
        return 0;

    // sum of nodes in the left subtree
    int ls = countSubtreesWithSumX(root.left,
                                   count, x);

    // sum of nodes in the right subtree
    int rs = countSubtreesWithSumX(root.right,
                                   count, x);

    // sum of nodes in the subtree
    // rooted with 'root.data'
    int sum = ls + rs + root.data;

    // if true
    if (sum == x)
        count.v++;

    // return subtree's nodes sum
    return sum;
}

// utility function to
// count subtrees that
// sum up to a given value x
static int countSubtreesWithSumXUtil(Node root,
                                     int x)
{
    // if tree is empty
    if (root == null)
        return 0;

    INT count = new INT(0);

    // sum of nodes in the left subtree
    int ls = countSubtreesWithSumX(root.left,
                                   count, x);

    // sum of nodes in the right subtree
    int rs = countSubtreesWithSumX(root.right,
                                   count, x);

    // if tree's nodes sum == x
    if ((ls + rs + root.data) == x)
        count.v++;

    // required count of subtrees
    return count.v;
}

// Driver Code
public static void main(String args[])
{
    /* binary tree creation    
                5
            / \
        -10     3
        / \ / \
        9 8 -4 7
    */
    Node root = getNode(5);
    root.left = getNode(-10);
    root.right = getNode(3);
    root.left.left = getNode(9);
    root.left.right = getNode(8);
    root.right.left = getNode(-4);
    root.right.right = getNode(7);

    int x = 7;

    System.out.println("Count = " +
           countSubtreesWithSumXUtil(root, x));
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation to count subtrees
# that Sum up to a given value x

# class to get a new node
class getNode:
    def __init__(self, data):

        # put in the data
        self.data = data
        self.left = self.right = None

# function to count subtrees that
# Sum up to a given value x
def countSubtreesWithSumX(root, count, x):

    # if tree is empty
    if (not root):
        return 0

    # Sum of nodes in the left subtree
    ls = countSubtreesWithSumX(root.left,
                               count, x)

    # Sum of nodes in the right subtree
    rs = countSubtreesWithSumX(root.right,
                               count, x)

    # Sum of nodes in the subtree
    # rooted with 'root.data'
    Sum = ls + rs + root.data

    # if true
    if (Sum == x):
        count[0] += 1

    # return subtree's nodes Sum
    return Sum

# utility function to count subtrees
# that Sum up to a given value x
def countSubtreesWithSumXUtil(root, x):

    # if tree is empty
    if (not root):
        return 0

    count = [0]

    # Sum of nodes in the left subtree
    ls = countSubtreesWithSumX(root.left,
                               count, x)

    # Sum of nodes in the right subtree
    rs = countSubtreesWithSumX(root.right,
                               count, x)

    # if tree's nodes Sum == x
    if ((ls + rs + root.data) == x):
        count[0] += 1

    # required count of subtrees
    return count[0]

# Driver Code
if __name__ == '__main__':

    # binary tree creation    
    #         5
    #         / \
    #     -10     3
    #     / \ / \
    #     9 8 -4 7
    root = getNode(5)
    root.left = getNode(-10)
    root.right = getNode(3)
    root.left.left = getNode(9)
    root.left.right = getNode(8)
    root.right.left = getNode(-4)
    root.right.right = getNode(7)

    x = 7

    print("Count =",
           countSubtreesWithSumXUtil(root, x))

# This code is contributed by PranchalK
```

## C#

```
using System;

// c# program to find if
// there is a subtree with
// given sum
public class GFG
{

// structure of a node
// of binary tree
public class Node
{
    public int data;
    public Node left, right;
}

public class INT
{
    public int v;
    public INT(int a)
    {
        v = a;
    }
}

// function to get a new node
public static Node getNode(int data)
{
    // allocate space
    Node newNode = new Node();

    // put in the data
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;
}

// function to count subtrees that
// sum up to a given value x
public static int countSubtreesWithSumX(Node root,
                                    INT count, int x)
{
    // if tree is empty
    if (root == null)
    {
        return 0;
    }

    // sum of nodes in the left subtree
    int ls = countSubtreesWithSumX(root.left, count, x);

    // sum of nodes in the right subtree
    int rs = countSubtreesWithSumX(root.right, count, x);

    // sum of nodes in the subtree
    // rooted with 'root.data'
    int sum = ls + rs + root.data;

    // if true
    if (sum == x)
    {
        count.v++;
    }

    // return subtree's nodes sum
    return sum;
}

// utility function to
// count subtrees that
// sum up to a given value x
public static int countSubtreesWithSumXUtil(Node root, int x)
{
    // if tree is empty
    if (root == null)
    {
        return 0;
    }

    INT count = new INT(0);

    // sum of nodes in the left subtree
    int ls = countSubtreesWithSumX(root.left, count, x);

    // sum of nodes in the right subtree
    int rs = countSubtreesWithSumX(root.right, count, x);

    // if tree's nodes sum == x
    if ((ls + rs + root.data) == x)
    {
        count.v++;
    }

    // required count of subtrees
    return count.v;
}

// Driver Code
public static void Main(string[] args)
{
    /* binary tree creation    
                5
            / \
        -10     3
        / \ / \
        9 8 -4 7
    */
    Node root = getNode(5);
    root.left = getNode(-10);
    root.right = getNode(3);
    root.left.left = getNode(9);
    root.left.right = getNode(8);
    root.right.left = getNode(-4);
    root.right.right = getNode(7);

    int x = 7;

    Console.WriteLine("Count = " + countSubtreesWithSumXUtil(root, x));
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // Javascript program to find if
    // there is a subtree with given sum

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    let v;

    // function to get a new node
    function getNode(data)
    {
        // allocate space
        let newNode = new Node(data);
        return newNode;
    }

    // function to count subtrees that
    // sum up to a given value x
    function countSubtreesWithSumX(root, x)
    {
        // if tree is empty
        if (root == null)
            return 0;

        // sum of nodes in the left subtree
        let ls = countSubtreesWithSumX(root.left, x);

        // sum of nodes in the right subtree
        let rs = countSubtreesWithSumX(root.right, x);

        // sum of nodes in the subtree
        // rooted with 'root.data'
        let sum = ls + rs + root.data;

        // if true
        if (sum == x)
            v++;

        // return subtree's nodes sum
        return sum;
    }

    // utility function to
    // count subtrees that
    // sum up to a given value x
    function countSubtreesWithSumXUtil(root, x)
    {
        // if tree is empty
        if (root == null)
            return 0;

        v = 0;

        // sum of nodes in the left subtree
        let ls = countSubtreesWithSumX(root.left, x);

        // sum of nodes in the right subtree
        let rs = countSubtreesWithSumX(root.right, x);

        // if tree's nodes sum == x
        if ((ls + rs + root.data) == x)
            v++;

        // required count of subtrees
        return v;
    }

    /* binary tree creation   
                5
            / \
        -10     3
        / \ / \
        9 8 -4 7
    */
    let root = getNode(5);
    root.left = getNode(-10);
    root.right = getNode(3);
    root.left.left = getNode(9);
    root.left.right = getNode(8);
    root.right.left = getNode(-4);
    root.right.right = getNode(7);

    let x = 7;

    document.write("Count = " +
           countSubtreesWithSumXUtil(root, x));

// This code is contributed by decode2207.
</script>
```

**输出:**

```
Count = 2
```

**时间复杂度:** O(n)。

**另一种方法:**

```
countSubtreesWithSumXUtil(root, x)

 Initialize static count = 0
 Initialize static *ptr = root
    if !root then
        return 0

    Initialize static count = 0
    ls+ = countSubtreesWithSumXUtil(root->left, count, x)
    rs+ = countSubtreesWithSumXUtil(root->right, count, x)

    if (ls + rs + root->data) == x
        count++

    if(ptr!=root)
       return ls + root->data + rs
    else
    return count
```

## C++

```
// C++ program to find if
// there is a subtree with
// given sum
#include <bits/stdc++.h>

using namespace std;

// Structure of a node of binary tree
struct Node {
    int data;
    Node *left, *right;
};

// Function to get a new node
Node* getNode(int data)
{
    // Allocate space
    Node* newNode = (Node*)malloc(sizeof(Node));

    // Put in the data
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// Utility function to count subtrees that
// sum up to a given value x
int countSubtreesWithSumXUtil(Node* root, int x)
{
    static int count=0;
    static Node* ptr=root;
    int l=0,r=0;
    if(root==NULL)
    return 0;

    l+=countSubtreesWithSumXUtil(root->left,x);

    r+=countSubtreesWithSumXUtil(root->right,x);

    if(l+r+root->data==x)
    count++;

    if(ptr!=root)
        return l+root->data+r;

    return count;

}

// Driver code
int main()
{
    /* binary tree creation
              5
            /  \
          -10   3
          / \  / \
          9 8 -4 7
    */
    Node* root = getNode(5);
    root->left = getNode(-10);
    root->right = getNode(3);
    root->left->left = getNode(9);
    root->left->right = getNode(8);
    root->right->left = getNode(-4);
    root->right->right = getNode(7);

    int x = 7;

    cout << "Count = "
        << countSubtreesWithSumXUtil(root, x);

    return 0;
}
// This code is contributed by Sadik Ali
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if
// there is a subtree with
// given sum
import java.io.*;

// Node class to create new node
class Node
{
    int data;
    Node left;
    Node right;
    Node(int data)
    {
        this.data = data;
    }
}

class GFG
{
    static int count = 0;
    static Node ptr;

    // Utility function to count subtrees that
    // sum up to a given value x
    int countSubtreesWithSumXUtil(Node root, int x)
    {
        int l = 0, r = 0;
        if(root == null) return 0;
        l += countSubtreesWithSumXUtil(root.left, x);
        r += countSubtreesWithSumXUtil(root.right, x);
        if(l + r + root.data == x) count++;
        if(ptr != root) return l + root.data + r;
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        /* binary tree creation
            5
        / \
        -10 3
        / \ / \
        9 8 -4 7
        */
        Node root = new Node(5);
        root.left = new Node(-10);
        root.right = new Node(3);
        root.left.left = new Node(9);
        root.left.right = new Node(8);
        root.right.left = new Node(-4);
        root.right.right = new Node(7);
        int x = 7;
        ptr = root; // assigning global value of ptr
        System.out.println("Count = " +
               new GFG().countSubtreesWithSumXUtil(root, x));
    }
}

// This code is submitted by Devarshi_Singh
```

## 蟒蛇 3

```
# Python3 program to find if there is
# a subtree with given sum

# Structure of a node of binary tree
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Function to get a new node
def getNode(data):

    # Allocate space
    newNode = Node(data)
    return newNode

count = 0
ptr = None

# Utility function to count subtrees that
# sum up to a given value x
def countSubtreesWithSumXUtil(root, x):

    global count, ptr

    l = 0
    r = 0

    if (root == None):
        return 0  

    l += countSubtreesWithSumXUtil(root.left, x)
    r += countSubtreesWithSumXUtil(root.right, x)

    if (l + r + root.data == x):
        count += 1

    if (ptr != root):
        return l + root.data + r

    return count

# Driver code
if __name__=='__main__':

    ''' binary tree creation
              5
            /  \
          -10   3
          / \  / \
          9 8 -4 7
    '''

    root = getNode(5)
    root.left = getNode(-10)
    root.right = getNode(3)
    root.left.left = getNode(9)
    root.left.right = getNode(8)
    root.right.left = getNode(-4)
    root.right.right = getNode(7)

    x = 7
    ptr = root

    print("Count = " + str(countSubtreesWithSumXUtil(
        root, x)))

# This code is contributed by pratham76
```

## C#

```
// C# program to find if
// there is a subtree with
// given sum
using System;

// Node class to
// create new node
public class Node
{
  public int data;
  public Node left;
  public Node right;
  public Node(int data)
  {
    this.data = data;
  }
}

class GFG{

static int count = 0;
static Node ptr;

// Utility function to count subtrees
// that sum up to a given value x
int countSubtreesWithSumXUtil(Node root,
                              int x)
{
  int l = 0, r = 0;
  if(root == null) return 0;
  l += countSubtreesWithSumXUtil(root.left, x);
  r += countSubtreesWithSumXUtil(root.right, x);
  if(l + r + root.data == x) count++;
  if(ptr != root) return l + root.data + r;
  return count;
}

// Driver Code
public static void Main(string[] args)
{
  /* binary tree creation
            5
        / \
        -10 3
        / \ / \
        9 8 -4 7
        */
  Node root = new Node(5);
  root.left = new Node(-10);
  root.right = new Node(3);
  root.left.left = new Node(9);
  root.left.right = new Node(8);
  root.right.left = new Node(-4);
  root.right.right = new Node(7);
  int x = 7;

  // Assigning global value of ptr
  ptr = root;
  Console.Write("Count = " +
          new GFG().countSubtreesWithSumXUtil(root, x));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

    // JavaScript program to find if
    // there is a subtree with
    // given sum

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    let count = 0;
    let ptr;

    // Utility function to count subtrees that
    // sum up to a given value x
    function countSubtreesWithSumXUtil(root, x)
    {
        let l = 0, r = 0;
        if(root == null) return 0;
        l += countSubtreesWithSumXUtil(root.left, x);
        r += countSubtreesWithSumXUtil(root.right, x);
        if(l + r + root.data == x) count++;
        if(ptr != root) return l + root.data + r;
        return count;
    }

    /* binary tree creation
           5
          / \
          -10 3
          / \ / \
          9 8 -4 7
          */
    let root = new Node(5);
    root.left = new Node(-10);
    root.right = new Node(3);
    root.left.left = new Node(9);
    root.left.right = new Node(8);
    root.right.left = new Node(-4);
    root.right.right = new Node(7);
    let x = 7;
    ptr = root; // assigning global value of ptr
    document.write("Count = " + countSubtreesWithSumXUtil(root, x));

</script>
```

**输出:**

```
Count = 2
```

**时间复杂度:** O(n)。