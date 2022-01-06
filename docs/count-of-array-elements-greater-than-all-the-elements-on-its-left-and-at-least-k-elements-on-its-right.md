# 数组元素的数量大于其左侧所有元素和其右侧至少 K 个元素

> 原文:[https://www . geesforgeks . org/数组元素计数-大于其左边的所有元素和至少其右边的 k 个元素/](https://www.geeksforgeeks.org/count-of-array-elements-greater-than-all-the-elements-on-its-left-and-at-least-k-elements-on-its-right/)

给定一个由 **N** 个不同整数组成的数组**A【】**，任务是找出**严格大于其前面所有元素且严格大于其右边至少 **K** 个元素的元素数。**

**示例:**

> **输入:** A[] = {2，5，1，7，3，4，0}，K = 3
> **输出:** 2
> **说明:**
> 满足给定条件的数组元素只有:
> 
> *   **5** :大于其左侧的所有元素{2}和其右侧的至少 K(= 3)个元素{1，3，4，0}
> *   **7** :大于其左侧的所有元素{2，5，1}和其右侧的至少 K(= 3)个元素{3，4，0}
> 
> 因此，计数为 2。
> 
> **输入:** A[] = {11，2，4，7，5，9，6，3}，K = 2
> **输出:** 1

**天真法:**
解决这个问题最简单的方法就是遍历数组，对于每个元素，遍历它左边的所有元素，检查它们是否都小于它，遍历它右边的所有元素，检查是否至少有 **K** 个元素小于它。对于每个满足条件的元素，增加**计数**。最后，打印**计数**的值。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效途径:**
使用[自平衡 BST](https://www.geeksforgeeks.org/self-balancing-binary-search-trees-comparisons/) 可以进一步优化上述途径。请遵循以下步骤:

*   从右向左遍历数组，将所有元素逐个插入 [AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)
*   使用 AVL 树生成一个数组**count small[]**，该数组包含每个数组元素右边的较小元素的计数。
*   遍历数组，对于每一个 **i <sup>第</sup>元素**，检查它是否是到目前为止获得的最大值，**count small【I】**是否大于或等于 **K** 。
*   如果是，增加**计数**。
*   打印**的最终值，计**为答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of an AVL Tree Node
struct node {
    int key;
    struct node* left;
    struct node* right;
    int height;
    // Size of the tree rooted
    // with this node
    int size;
};

// Utility function to get maximum
// of two integers
int max(int a, int b);

// Utility function to get height
// of the tree rooted with N
int height(struct node* N)
{
    if (N == NULL)
        return 0;
    return N->height;
}

// Utility function to find size of
// the tree rooted with N
int size(struct node* N)
{
    if (N == NULL)
        return 0;
    return N->size;
}

// Utility function to get maximum
// of two integers
int max(int a, int b)
{
    return (a > b) ? a : b;
}

// Helper function to allocates a
// new node with the given key
struct node* newNode(int key)
{
    struct node* node
        = (struct node*)
            malloc(sizeof(struct node));
    node->key = key;
    node->left = NULL;
    node->right = NULL;
    node->height = 1;
    node->size = 1;
    return (node);
}

// Utility function to right rotate
// subtree rooted with y
struct node* rightRotate(struct node* y)
{
    struct node* x = y->left;
    struct node* T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left),
                    height(y->right))
                + 1;
    x->height = max(height(x->left),
                    height(x->right))
                + 1;

    // Update sizes
    y->size = size(y->left)
              + size(y->right) + 1;
    x->size = size(x->left)
              + size(x->right) + 1;

    // Return new root
    return x;
}

// Utility function to left rotate
// subtree rooted with x
struct node* leftRotate(struct node* x)
{
    struct node* y = x->right;
    struct node* T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left),
                    height(x->right))
                + 1;
    y->height = max(height(y->left),
                    height(y->right))
                + 1;

    // Update sizes
    x->size = size(x->left)
              + size(x->right) + 1;
    y->size = size(y->left)
              + size(y->right) + 1;

    // Return new root
    return y;
}

// Function to obtain Balance factor
// of node N
int getBalance(struct node* N)
{
    if (N == NULL)
        return 0;

    return height(N->left)
           - height(N->right);
}

// Function to insert a new key to the
// tree rooted with node
struct node* insert(struct node* node, int key,
                    int* count)
{
    // Perform the normal BST rotation
    if (node == NULL)
        return (newNode(key));

    if (key < node->key)
        node->left
            = insert(node->left, key, count);
    else {
        node->right
            = insert(node->right, key, count);

        // Update count of smaller elements
        *count = *count + size(node->left) + 1;
    }

    // Update height and size of the ancestor
    node->height = max(height(node->left),
                       height(node->right))
                   + 1;
    node->size = size(node->left)
                 + size(node->right) + 1;

    // Get the balance factor of the ancestor
    int balance = getBalance(node);

    // Left Left Case
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->key) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->key) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    return node;
}

// Function to generate an array which contains
// count of smaller elements on the right
void constructLowerArray(int arr[],
                         int countSmaller[],
                         int n)
{
    int i, j;
    struct node* root = NULL;

    for (i = 0; i < n; i++)
        countSmaller[i] = 0;

    // Insert all elements in the AVL Tree
    // and get the count of smaller elements
    for (i = n - 1; i >= 0; i--) {
        root = insert(root, arr[i],
                      &countSmaller[i]);
    }
}

// Function to find the number
// of elements which are greater
// than all elements on its left
// and K elements on its right
int countElements(int A[], int n, int K)
{

    int count = 0;

    // Stores the count of smaller
    // elements on its right
    int* countSmaller
        = (int*)malloc(sizeof(int) * n);
    constructLowerArray(A, countSmaller, n);

    int maxi = INT_MIN;
    for (int i = 0; i <= (n - K - 1); i++) {
        if (A[i] > maxi && countSmaller[i] >= K) {
            count++;
            maxi = A[i];
        }
    }

    return count;
}

// Driver Code
int main()
{

    int A[] = { 2, 5, 1, 7, 3, 4, 0 };
    int n = sizeof(A) / sizeof(int);
    int K = 3;

    cout << countElements(A, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Structure of an AVL Tree Node
static class Node
{
    int key;
    Node left;
    Node right;
    int height;

    // Size of the tree rooted
    // with this Node
    int size;

    public Node(int key)
    {
        this.key = key;
        this.left = this.right = null;
        this.size = this.height = 1;
    }
};

// Helper class to pass Integer
// as referencee
static class RefInteger
{
    Integer value;

    public RefInteger(Integer value)
    {
        this.value = value;
    }
}

// Utility function to get height
// of the tree rooted with N
static int height(Node N)
{
    if (N == null)
        return 0;

    return N.height;
}

// Utility function to find size of
// the tree rooted with N
static int size(Node N)
{
    if (N == null)
        return 0;

    return N.size;
}

// Utility function to get maximum
// of two integers
static int max(int a, int b)
{
    return (a > b) ? a : b;
}

// Utility function to right rotate
// subtree rooted with y
static Node rightRotate(Node y)
{
    Node x = y.left;
    Node T2 = x.right;

    // Perform rotation
    x.right = y;
    y.left = T2;

    // Update heights
    y.height = max(height(y.left),
                   height(y.right)) + 1;
    x.height = max(height(x.left),
                   height(x.right)) + 1;

    // Update sizes
    y.size = size(y.left) +
             size(y.right) + 1;
    x.size = size(x.left) +
             size(x.right) + 1;

    // Return new root
    return x;
}

// Utility function to left rotate
// subtree rooted with x
static Node leftRotate(Node x)
{
    Node y = x.right;
    Node T2 = y.left;

    // Perform rotation
    y.left = x;
    x.right = T2;

    // Update heights
    x.height = max(height(x.left),
                   height(x.right)) + 1;
    y.height = max(height(y.left),
                   height(y.right)) + 1;

    // Update sizes
    x.size = size(x.left) +
             size(x.right) + 1;
    y.size = size(y.left) +
             size(y.right) + 1;

    // Return new root
    return y;
}

// Function to obtain Balance factor
// of Node N
static int getBalance(Node N)
{
    if (N == null)
        return 0;

    return height(N.left) -
           height(N.right);
}

// Function to insert a new key to the
// tree rooted with Node
static Node insert(Node Node, int key,
                   RefInteger count)
{

    // Perform the normal BST rotation
    if (Node == null)
        return (new Node(key));

    if (key < Node.key)
        Node.left = insert(Node.left,
                           key, count);
    else
    {
        Node.right = insert(Node.right,
                            key, count);

        // Update count of smaller elements
        count.value = count.value +
                  size(Node.left) + 1;
    }

    // Update height and size of the ancestor
    Node.height = max(height(Node.left),
                      height(Node.right)) + 1;
    Node.size = size(Node.left) +
                size(Node.right) + 1;

    // Get the balance factor of the ancestor
    int balance = getBalance(Node);

    // Left Left Case
    if (balance > 1 && key < Node.left.key)
        return rightRotate(Node);

    // Right Right Case
    if (balance < -1 && key > Node.right.key)
        return leftRotate(Node);

    // Left Right Case
    if (balance > 1 && key > Node.left.key)
    {
        Node.left = leftRotate(Node.left);
        return rightRotate(Node);
    }

    // Right Left Case
    if (balance < -1 && key < Node.right.key)
    {
        Node.right = rightRotate(Node.right);
        return leftRotate(Node);
    }
    return Node;
}

// Function to generate an array which
// contains count of smaller elements
// on the right
static void constructLowerArray(int arr[],
     RefInteger[] countSmaller, int n)
{
    int i, j;
    Node root = null;

    for(i = 0; i < n; i++)
        countSmaller[i] = new RefInteger(0);

    // Insert all elements in the AVL Tree
    // and get the count of smaller elements
    for(i = n - 1; i >= 0; i--)
    {
        root = insert(root, arr[i],
                   countSmaller[i]);
    }
}

// Function to find the number
// of elements which are greater
// than all elements on its left
// and K elements on its right
static int countElements(int A[], int n,
                         int K)
{
    int count = 0;

    // Stores the count of smaller
    // elements on its right
    RefInteger[] countSmaller = new RefInteger[n];
    constructLowerArray(A, countSmaller, n);

    int maxi = Integer.MIN_VALUE;
    for(int i = 0; i <= (n - K - 1); i++)
    {
        if (A[i] > maxi &&
            countSmaller[i].value >= K)
        {
            count++;
            maxi = A[i];
        }
    }
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 2, 5, 1, 7, 3, 4, 0 };
    int n = A.length;
    int K = 3;

    System.out.println(countElements(A, n, K));
}
}

// This code is contributed by sanjeev2552
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Structure of an AVL Tree Node
public class Node
{
    public int key;
    public Node left;
    public Node right;
    public int height;

    // Size of the tree rooted
    // with this Node
    public int size;

    public Node(int key)
    {
        this.key = key;
        this.left = this.right = null;
        this.size = this.height = 1;
    }
};

// Helper class to pass int
// as referencee
public class Refint
{
    public int value;

    public Refint(int value)
    {
        this.value = value;
    }
}

// Utility function to get height
// of the tree rooted with N
static int height(Node N)
{
    if (N == null)
        return 0;

    return N.height;
}

// Utility function to find size of
// the tree rooted with N
static int size(Node N)
{
    if (N == null)
        return 0;

    return N.size;
}

// Utility function to get maximum
// of two integers
static int max(int a, int b)
{
    return (a > b) ? a : b;
}

// Utility function to right rotate
// subtree rooted with y
static Node rightRotate(Node y)
{
    Node x = y.left;
    Node T2 = x.right;

    // Perform rotation
    x.right = y;
    y.left = T2;

    // Update heights
    y.height = max(height(y.left),
                   height(y.right)) + 1;
    x.height = max(height(x.left),
                   height(x.right)) + 1;

    // Update sizes
    y.size = size(y.left) +
             size(y.right) + 1;
    x.size = size(x.left) +
             size(x.right) + 1;

    // Return new root
    return x;
}

// Utility function to left rotate
// subtree rooted with x
static Node leftRotate(Node x)
{
    Node y = x.right;
    Node T2 = y.left;

    // Perform rotation
    y.left = x;
    x.right = T2;

    // Update heights
    x.height = max(height(x.left),
                   height(x.right)) + 1;
    y.height = max(height(y.left),
                   height(y.right)) + 1;

    // Update sizes
    x.size = size(x.left) +
             size(x.right) + 1;
    y.size = size(y.left) +
             size(y.right) + 1;

    // Return new root
    return y;
}

// Function to obtain Balance factor
// of Node N
static int getBalance(Node N)
{
    if (N == null)
        return 0;

    return height(N.left) -
           height(N.right);
}

// Function to insert a new key to the
// tree rooted with Node
static Node insert(Node Node, int key,
                   Refint count)
{

    // Perform the normal BST rotation
    if (Node == null)
        return (new Node(key));

    if (key < Node.key)
        Node.left = insert(Node.left,
                           key, count);
    else
    {
        Node.right = insert(Node.right,
                            key, count);

        // Update count of smaller elements
        count.value = count.value +
                  size(Node.left) + 1;
    }

    // Update height and size of the ancestor
    Node.height = max(height(Node.left),
                      height(Node.right)) + 1;
    Node.size = size(Node.left) +
                size(Node.right) + 1;

    // Get the balance factor of the ancestor
    int balance = getBalance(Node);

    // Left Left Case
    if (balance > 1 && key < Node.left.key)
        return rightRotate(Node);

    // Right Right Case
    if (balance < -1 && key > Node.right.key)
        return leftRotate(Node);

    // Left Right Case
    if (balance > 1 && key > Node.left.key)
    {
        Node.left = leftRotate(Node.left);
        return rightRotate(Node);
    }

    // Right Left Case
    if (balance < -1 && key < Node.right.key)
    {
        Node.right = rightRotate(Node.right);
        return leftRotate(Node);
    }
    return Node;
}

// Function to generate an array which
// contains count of smaller elements
// on the right
static void constructLowerArray(int []arr,
         Refint[] countSmaller, int n)
{
    int i;
    //int j;
    Node root = null;

    for(i = 0; i < n; i++)
        countSmaller[i] = new Refint(0);

    // Insert all elements in the AVL Tree
    // and get the count of smaller elements
    for(i = n - 1; i >= 0; i--)
    {
        root = insert(root, arr[i],
                   countSmaller[i]);
    }
}

// Function to find the number
// of elements which are greater
// than all elements on its left
// and K elements on its right
static int countElements(int []A, int n,
                         int K)
{
    int count = 0;

    // Stores the count of smaller
    // elements on its right
    Refint[] countSmaller = new Refint[n];
    constructLowerArray(A, countSmaller, n);

    int maxi = int.MinValue;
    for(int i = 0; i <= (n - K - 1); i++)
    {
        if (A[i] > maxi &&
            countSmaller[i].value >= K)
        {
            count++;
            maxi = A[i];
        }
    }
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 2, 5, 1, 7, 3, 4, 0 };
    int n = A.Length;
    int K = 3;

    Console.WriteLine(countElements(A, n, K));
}
}

// This code is contributed by Princi Singh
```

**Output:** 

```
2
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*