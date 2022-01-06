# 对 BST 中总和大于 K 的对进行计数

> 原文:[https://www . geesforgeks . org/count-pairs-in-BST-with-sum-大于-k/](https://www.geeksforgeeks.org/count-pairs-in-bst-with-sum-greater-than-k/)

给定一个包含 N 个不同节点的二叉查找树和一个值 T2。任务是统计给定二叉查找树中的配对，其和大于给定值 **K** 。

**示例:**

```
Input:  
        5      
       / \      
      3   7      
     / \ / \  
    2  4 6  8   

     k = 11
Output: 6
Explanation:
There are 6 pairs which are (4, 8), (5, 7), (5, 8), (6, 7), (6, 8) and (7, 8).

Input: 

         8      
        / \      
       3   9      
       \   / \  
        5 6  18   

       k = 23
Output: 3
Explanation:
There are 3 pairs which are (6, 18), (8, 18) and (9, 18).
```

**天真方法:**
为了解决上面提到的问题，我们必须在数组中存储 BST 的有序遍历，然后运行两个循环来生成所有对，并逐一检查当前对的和是否大于 k。

**高效方法:**
如果我们将 BST 的有序遍历存储在一个数组中，并将数组的初始和最后一个索引放在 l 和 r 变量中，以找到有序数组中的总对，则上述方法可以得到优化。最初指定 l 为 0，r 为 n-1。考虑一个变量，并将其初始化为零。这个可变的结果将是我们的最终答案。现在迭代直到 l < r，如果当前左和当前右的和大于 K，则从 l+1 到 r 的所有元素与其形成一对，否则不会，因此，增加当前左。最后，返回结果。

下面是上述方法的实现:

## C++

```
// C++ program to Count
// pair in BST whose Sum
// is greater than K

#include <bits/stdc++.h>
using namespace std;

// Structure of each node of BST
struct node {
    int key;
    struct node *left, *right;
};

// Function to create a new BST node
node* newNode(int item)
{
    node* temp = new node();

    temp->key = item;
    temp->left = temp->right = NULL;

    return temp;
}

/* Function to insert a new
node with given key in BST */
struct node* insert(struct node* node, int key)
{

    // check if the tree is empty
    if (node == NULL)
        return newNode(key);

    if (key < node->key)

        node->left = insert(node->left, key);

    else if (key > node->key)

        node->right = insert(node->right, key);

    /* return the (unchanged) node pointer */
    return node;
}

// Function to return the size of the tree
int sizeOfTree(node* root)
{
    if (root == NULL) {
        return 0;
    }

    // Calculate left size recursively
    int left = sizeOfTree(root->left);

    // Calculate right size recursively
    int right = sizeOfTree(root->right);

    // Return total size recursively
    return (left + right + 1);
}

// Function to store inorder traversal of BST
void storeInorder(node* root, int inOrder[],
                  int& index)
{

    // Base condition
    if (root == NULL) {
        return;
    }

    // Left recursive call
    storeInorder(root->left, inOrder, index);

    // Store elements in inorder array
    inOrder[index++] = root->key;

    // Right recursive call
    storeInorder(root->right, inOrder, index);
}

// function to count the pair of BST
// whose sum is greater than k
int countPairUtil(int inOrder[], int j, int k)
{
    int i = 0;
    int pair = 0;
    while (i < j) {

        // check if sum of value at index
        // i and j is greater than k
        if (inOrder[i] + inOrder[j] > k) {
            pair += j - i;

            j--;
        }
        else {
            i++;
        }
    }

    // Return number of total pair
    return pair;
}

// Function to count the
// pair of BST whose sum is
// greater than k
int countPair(node* root, int k)
{

    // Store the size of BST
    int numNode = sizeOfTree(root);

    // Auxiliary array for storing
    // the inorder traversal of BST
    int inOrder[numNode + 1];

    int index = 0;

    storeInorder(root, inOrder, index);

    // Function call to count the pair
    return countPairUtil(inOrder, index - 1, k);
}

// Driver code
int main()
{

    // create tree
    struct node* root = NULL;
    root = insert(root, 5);
    insert(root, 3);
    insert(root, 2);
    insert(root, 4);
    insert(root, 7);
    insert(root, 6);
    insert(root, 8);

    int k = 11;

    // Print the number of pair
    cout << countPair(root, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count
// pair in BST whose Sum
// is greater than K
class GFG{

// Structure of each node of BST
static class node {
    int key;
    node left, right;
};
static int index;

// Function to create a new BST node
static node newNode(int item)
{
    node temp = new node();

    temp.key = item;
    temp.left = temp.right = null;

    return temp;
}

/* Function to insert a new
node with given key in BST */
static node insert(node node, int key)
{

    // check if the tree is empty
    if (node == null)
        return newNode(key);

    if (key < node.key)

        node.left = insert(node.left, key);

    else if (key > node.key)

        node.right = insert(node.right, key);

    /* return the (unchanged) node pointer */
    return node;
}

// Function to return the size of the tree
static int sizeOfTree(node root)
{
    if (root == null) {
        return 0;
    }

    // Calculate left size recursively
    int left = sizeOfTree(root.left);

    // Calculate right size recursively
    int right = sizeOfTree(root.right);

    // Return total size recursively
    return (left + right + 1);
}

// Function to store inorder traversal of BST
static void storeInorder(node root, int inOrder[])
{

    // Base condition
    if (root == null) {
        return;
    }

    // Left recursive call
    storeInorder(root.left, inOrder);

    // Store elements in inorder array
    inOrder[index++] = root.key;

    // Right recursive call
    storeInorder(root.right, inOrder);
}

// function to count the pair of BST
// whose sum is greater than k
static int countPairUtil(int inOrder[], int j, int k)
{
    int i = 0;
    int pair = 0;
    while (i < j) {

        // check if sum of value at index
        // i and j is greater than k
        if (inOrder[i] + inOrder[j] > k) {
            pair += j - i;

            j--;
        }
        else {
            i++;
        }
    }

    // Return number of total pair
    return pair;
}

// Function to count the
// pair of BST whose sum is
// greater than k
static int countPair(node root, int k)
{

    // Store the size of BST
    int numNode = sizeOfTree(root);

    // Auxiliary array for storing
    // the inorder traversal of BST
    int []inOrder = new int[numNode + 1];

    index = 0;

    storeInorder(root, inOrder);

    // Function call to count the pair
    return countPairUtil(inOrder, index - 1, k);
}

// Driver code
public static void main(String[] args)
{

    // create tree
    node root = null;
    root = insert(root, 5);
    insert(root, 3);
    insert(root, 2);
    insert(root, 4);
    insert(root, 7);
    insert(root, 6);
    insert(root, 8);

    int k = 11;

    // Print the number of pair
    System.out.print(countPair(root, k));

}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to count pair in
# BST whose sum is greater than K
index = 0

# Structure of each node of BST
class newNode:

    # Function to create a new BST node
    def __init__(self, item):

        self.key = item
        self.left = None
        self.right = None

# Function to insert a new
# node with given key in BST
def insert(node, key):

    # Check if the tree is empty
    if (node == None):
        return newNode(key)

    if (key < node.key):
        node.left = insert(node.left, key)

    elif(key > node.key):
        node.right = insert(node.right, key)

    # Return the (unchanged) node pointer
    return node

# Function to return the size of the tree
def sizeOfTree(root):

    if (root == None):
        return 0

    # Calculate left size recursively
    left = sizeOfTree(root.left)

    # Calculate right size recursively
    right = sizeOfTree(root.right)

    # Return total size recursively
    return (left + right + 1)

# Function to store inorder traversal of BST
def storeInorder(root, inOrder):

    global index

    # Base condition
    if (root == None):
        return

    # Left recursive call
    storeInorder(root.left, inOrder)

    # Store elements in inorder array
    inOrder[index] = root.key
    index += 1

    # Right recursive call
    storeInorder(root.right, inOrder)

# Function to count the pair of BST
# whose sum is greater than k
def countPairUtil(inOrder, j, k):

    i = 0
    pair = 0

    while (i < j):

        # Check if sum of value at index
        # i and j is greater than k
        if (inOrder[i] + inOrder[j] > k):
            pair += j - i
            j -= 1
        else:
            i += 1

    # Return number of total pair
    return pair

# Function to count the
# pair of BST whose sum is
# greater than k
def countPair(root, k):

    global index

    # Store the size of BST
    numNode = sizeOfTree(root)

    # Auxiliary array for storing
    # the inorder traversal of BST
    inOrder = [0 for i in range(numNode + 1)]

    storeInorder(root, inOrder)

    # Function call to count the pair
    return countPairUtil(inOrder, index - 1, k)

# Driver code
if __name__ == '__main__':

    # Create tree
    root = None
    root = insert(root, 5)
    insert(root, 3)
    insert(root, 2)
    insert(root, 4)
    insert(root, 7)
    insert(root, 6)
    insert(root, 8)

    k = 11

    # Print the number of pair
    print(countPair(root, k))

# This code is contributed by ipg2016107
```

## C#

```
// C# program to Count
// pair in BST whose Sum
// is greater than K
using System;

class GFG{

// Structure of each node of BST
class node {
    public int key;
    public node left, right;
};
static int index;

// Function to create a new BST node
static node newNode(int item)
{
    node temp = new node();

    temp.key = item;
    temp.left = temp.right = null;

    return temp;
}

/* Function to insert a new
node with given key in BST */
static node insert(node node, int key)
{

    // check if the tree is empty
    if (node == null)
        return newNode(key);

    if (key < node.key)

        node.left = insert(node.left, key);

    else if (key > node.key)

        node.right = insert(node.right, key);

    /* return the (unchanged) node pointer */
    return node;
}

// Function to return the size of the tree
static int sizeOfTree(node root)
{
    if (root == null) {
        return 0;
    }

    // Calculate left size recursively
    int left = sizeOfTree(root.left);

    // Calculate right size recursively
    int right = sizeOfTree(root.right);

    // Return total size recursively
    return (left + right + 1);
}

// Function to store inorder traversal of BST
static void storeInorder(node root, int []inOrder)
{

    // Base condition
    if (root == null) {
        return;
    }

    // Left recursive call
    storeInorder(root.left, inOrder);

    // Store elements in inorder array
    inOrder[index++] = root.key;

    // Right recursive call
    storeInorder(root.right, inOrder);
}

// function to count the pair of BST
// whose sum is greater than k
static int countPairUtil(int []

                         inOrder, int j, int k)
{
    int i = 0;
    int pair = 0;
    while (i < j) {

        // check if sum of value at index
        // i and j is greater than k
        if (inOrder[i] + inOrder[j] > k) {
            pair += j - i;

            j--;
        }
        else {
            i++;
        }
    }

    // Return number of total pair
    return pair;
}

// Function to count the
// pair of BST whose sum is
// greater than k
static int countPair(node root, int k)
{

    // Store the size of BST
    int numNode = sizeOfTree(root);

    // Auxiliary array for storing
    // the inorder traversal of BST
    int []inOrder = new int[numNode + 1];

    index = 0;

    storeInorder(root, inOrder);

    // Function call to count the pair
    return countPairUtil(inOrder, index - 1, k);
}

// Driver code
public static void Main(String[] args)
{

    // create tree
    node root = null;
    root = insert(root, 5);
    insert(root, 3);
    insert(root, 2);
    insert(root, 4);
    insert(root, 7);
    insert(root, 6);
    insert(root, 8);

    int k = 11;

    // Print the number of pair
    Console.Write(countPair(root, k));

}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript program to Count
    // pair in BST whose Sum
    // is greater than K

    // Structure of each node of BST
    class node {
        constructor(item) {
           this.left = null;
           this.right = null;
           this.key = item;
        }
    }
    let index;

    // Function to create a new BST node
    function newNode(item)
    {
        let temp = new node(item);
        return temp;
    }

    /* Function to insert a new
    node with given key in BST */
    function insert(node, key)
    {

        // check if the tree is empty
        if (node == null)
            return newNode(key);

        if (key < node.key)

            node.left = insert(node.left, key);

        else if (key > node.key)

            node.right = insert(node.right, key);

        /* return the (unchanged) node pointer */
        return node;
    }

    // Function to return the size of the tree
    function sizeOfTree(root)
    {
        if (root == null) {
            return 0;
        }

        // Calculate left size recursively
        let left = sizeOfTree(root.left);

        // Calculate right size recursively
        let right = sizeOfTree(root.right);

        // Return total size recursively
        return (left + right + 1);
    }

    // Function to store inorder traversal of BST
    function storeInorder(root, inOrder)
    {

        // Base condition
        if (root == null) {
            return;
        }

        // Left recursive call
        storeInorder(root.left, inOrder);

        // Store elements in inorder array
        inOrder[index++] = root.key;

        // Right recursive call
        storeInorder(root.right, inOrder);
    }

    // function to count the pair of BST
    // whose sum is greater than k
    function countPairUtil(inOrder, j, k)
    {
        let i = 0;
        let pair = 0;
        while (i < j) {

            // check if sum of value at index
            // i and j is greater than k
            if (inOrder[i] + inOrder[j] > k) {
                pair += j - i;

                j--;
            }
            else {
                i++;
            }
        }

        // Return number of total pair
        return pair;
    }

    // Function to count the
    // pair of BST whose sum is
    // greater than k
    function countPair(root, k)
    {

        // Store the size of BST
        let numNode = sizeOfTree(root);

        // Auxiliary array for storing
        // the inorder traversal of BST
        let inOrder = new Array(numNode + 1);

        index = 0;

        storeInorder(root, inOrder);

        // Function call to count the pair
        return countPairUtil(inOrder, index - 1, k);
    }

    // create tree
    let root = null;
    root = insert(root, 5);
    insert(root, 3);
    insert(root, 2);
    insert(root, 4);
    insert(root, 7);
    insert(root, 6);
    insert(root, 8);

    let k = 11;

    // Print the number of pair
    document.write(countPair(root, k));

</script>
```

**Output:** 

```
6
```