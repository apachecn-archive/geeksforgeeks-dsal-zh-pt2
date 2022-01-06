# 合并两个平衡的二分搜索法树

> 原文:[https://www . geesforgeks . org/merge-two-balanced-binary-search-trees/](https://www.geeksforgeeks.org/merge-two-balanced-binary-search-trees/)

给你两个平衡的二分搜索法树，例如 AVL 树或红黑树。编写一个函数，将两个给定的平衡 BST 合并成一个平衡二叉查找树。假设第一棵树上有 m 个元素，另一棵树上有 n 个元素。您的合并函数需要 O(m+n)个时间。
在下面的解中，假设树的大小也被作为输入给出。如果没有给出尺寸，那么我们可以通过遍历树得到尺寸(见[这个](https://www.geeksforgeeks.org/write-a-c-program-to-calculate-size-of-a-tree/))。

**方法 1(将**第一棵树的**元素插入到第二棵树中)**
将第一个 BST 的所有元素逐一取出，插入到第二个 BST 中。将一个元素插入自平衡基站需要花费 Logn 时间(参见[本](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/))，其中 n 是基站的大小。所以这种方法的时间复杂度是 Log(n) + Log(n+1) … Log(m+n-1)。该表达式的值将介于 mLogn 和 mLog(m+n-1)之间。作为优化，我们可以选择较小的树作为第一棵树。
**方法 2(合并有序遍历)**
1)对第一棵树进行有序遍历，并将遍历存储在一个临时数组 arr1[]中。这一步需要 0(m)时间。
2)依次遍历第二棵树，并将遍历结果存储在另一个临时数组 arr2[]中。这一步需要 O(n)个时间。
3)步骤 1 和 2 中创建的数组是排序数组。将两个排序后的数组合并成一个大小为 m + n 的数组。这一步需要 O(m+n)个时间。
4)使用本文[中讨论的技术，从合并的数组中构建一个平衡树。这一步需要 O(m+n)个时间。
该方法的时间复杂度为 O(m+n)，优于方法 1。即使输入的 BST 不平衡，这种方法也需要 O(m+n)个时间。
以下是该方法的实施。](https://www.geeksforgeeks.org/sorted-array-to-balanced-bst/) 

## C++

```
// C++ program to Merge Two Balanced Binary Search Trees
#include<bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
class node
{
    public:
    int data;
    node* left;
    node* right;
};

// A utility function to merge two sorted arrays into one
int *merge(int arr1[], int arr2[], int m, int n);

// A helper function that stores inorder
// traversal of a tree in inorder array
void storeInorder(node* node, int inorder[],
                            int *index_ptr);

/* A function that constructs Balanced
Binary Search Tree from a sorted array
See https://www.geeksforgeeks.org/sorted-array-to-balanced-bst/ */
node* sortedArrayToBST(int arr[], int start, int end);

/* This function merges two balanced
BSTs with roots as root1 and root2.
m and n are the sizes of the trees respectively */
node* mergeTrees(node *root1, node *root2, int m, int n)
{
    // Store inorder traversal of
    // first tree in an array arr1[]
    int *arr1 = new int[m];
    int i = 0;
    storeInorder(root1, arr1, &i);

    // Store inorder traversal of second
    // tree in another array arr2[]
    int *arr2 = new int[n];
    int j = 0;
    storeInorder(root2, arr2, &j);

    // Merge the two sorted array into one
    int *mergedArr = merge(arr1, arr2, m, n);

    // Construct a tree from the merged
    // array and return root of the tree
    return sortedArrayToBST (mergedArr, 0, m + n - 1);
}

/* Helper function that allocates
a new node with the given data and
NULL left and right pointers. */
node* newNode(int data)
{
    node* Node = new node();
    Node->data = data;
    Node->left = NULL;
    Node->right = NULL;

    return(Node);
}

// A utility function to print inorder
// traversal of a given binary tree
void printInorder(node* node)
{
    if (node == NULL)
        return;

    /* first recur on left child */
    printInorder(node->left);

    cout << node->data << " ";

    /* now recur on right child */
    printInorder(node->right);
}

// A utility function to merge
// two sorted arrays into one
int *merge(int arr1[], int arr2[], int m, int n)
{
    // mergedArr[] is going to contain result
    int *mergedArr = new int[m + n];
    int i = 0, j = 0, k = 0;

    // Traverse through both arrays
    while (i < m && j < n)
    {
        // Pick the smaller element and put it in mergedArr
        if (arr1[i] < arr2[j])
        {
            mergedArr[k] = arr1[i];
            i++;
        }
        else
        {
            mergedArr[k] = arr2[j];
            j++;
        }
        k++;
    }

    // If there are more elements in first array
    while (i < m)
    {
        mergedArr[k] = arr1[i];
        i++; k++;
    }

    // If there are more elements in second array
    while (j < n)
    {
        mergedArr[k] = arr2[j];
        j++; k++;
    }

    return mergedArr;
}

// A helper function that stores inorder
// traversal of a tree rooted with node
void storeInorder(node* node, int inorder[], int *index_ptr)
{
    if (node == NULL)
        return;

    /* first recur on left child */
    storeInorder(node->left, inorder, index_ptr);

    inorder[*index_ptr] = node->data;
    (*index_ptr)++; // increase index for next entry

    /* now recur on right child */
    storeInorder(node->right, inorder, index_ptr);
}

/* A function that constructs Balanced
// Binary Search Tree from a sorted array
See https://www.geeksforgeeks.org/sorted-array-to-balanced-bst/ */
node* sortedArrayToBST(int arr[], int start, int end)
{
    /* Base Case */
    if (start > end)
    return NULL;

    /* Get the middle element and make it root */
    int mid = (start + end)/2;
    node *root = newNode(arr[mid]);

    /* Recursively construct the left subtree and make it
    left child of root */
    root->left = sortedArrayToBST(arr, start, mid-1);

    /* Recursively construct the right subtree and make it
    right child of root */
    root->right = sortedArrayToBST(arr, mid+1, end);

    return root;
}

/* Driver code*/
int main()
{
    /* Create following tree as first balanced BST
        100
        / \
        50 300
    / \
    20 70
    */
    node *root1 = newNode(100);
    root1->left     = newNode(50);
    root1->right = newNode(300);
    root1->left->left = newNode(20);
    root1->left->right = newNode(70);

    /* Create following tree as second balanced BST
            80
        / \
        40 120
    */
    node *root2 = newNode(80);
    root2->left     = newNode(40);
    root2->right = newNode(120);

    node *mergedTree = mergeTrees(root1, root2, 5, 3);

    cout << "Following is Inorder traversal of the merged tree \n";
    printInorder(mergedTree);

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to Merge Two Balanced Binary Search Trees
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node
{
    int data;
    struct node* left;
    struct node* right;
};

// A utility function to merge two sorted arrays into one
int *merge(int arr1[], int arr2[], int m, int n);

// A helper function that stores inorder traversal of a tree in inorder array
void storeInorder(struct node* node, int inorder[], int *index_ptr);

/* A function that constructs Balanced Binary Search Tree from a sorted array
   See https://www.geeksforgeeks.org/sorted-array-to-balanced-bst/ */
struct node* sortedArrayToBST(int arr[], int start, int end);

/* This function merges two balanced BSTs with roots as root1 and root2.
   m and n are the sizes of the trees respectively */
struct node* mergeTrees(struct node *root1, struct node *root2, int m, int n)
{
    // Store inorder traversal of first tree in an array arr1[]
    int *arr1 = new int[m];
    int i = 0;
    storeInorder(root1, arr1, &i);

    // Store inorder traversal of second tree in another array arr2[]
    int *arr2 = new int[n];
    int j = 0;
    storeInorder(root2, arr2, &j);

    // Merge the two sorted array into one
    int *mergedArr = merge(arr1, arr2, m, n);

    // Construct a tree from the merged array and return root of the tree
    return sortedArrayToBST (mergedArr, 0, m+n-1);
}

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct node* newNode(int data)
{
    struct node* node = (struct node*)
                        malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return(node);
}

// A utility function to print inorder traversal of a given binary tree
void printInorder(struct node* node)
{
    if (node == NULL)
        return;

    /* first recur on left child */
    printInorder(node->left);

    printf("%d ", node->data);

    /* now recur on right child */
    printInorder(node->right);
}

// A utility unction to merge two sorted arrays into one
int *merge(int arr1[], int arr2[], int m, int n)
{
    // mergedArr[] is going to contain result
    int *mergedArr = new int[m + n];
    int i = 0, j = 0, k = 0;

    // Traverse through both arrays
    while (i < m && j < n)
    {
        // Pick the smaller element and put it in mergedArr
        if (arr1[i] < arr2[j])
        {
            mergedArr[k] = arr1[i];
            i++;
        }
        else
        {
            mergedArr[k] = arr2[j];
            j++;
        }
        k++;
    }

    // If there are more elements in first array
    while (i < m)
    {
        mergedArr[k] = arr1[i];
        i++; k++;
    }

    // If there are more elements in second array
    while (j < n)
    {
        mergedArr[k] = arr2[j];
        j++; k++;
    }

    return mergedArr;
}

// A helper function that stores inorder traversal of a tree rooted with node
void storeInorder(struct node* node, int inorder[], int *index_ptr)
{
    if (node == NULL)
        return;

    /* first recur on left child */
    storeInorder(node->left, inorder, index_ptr);

    inorder[*index_ptr] = node->data;
    (*index_ptr)++;  // increase index for next entry

    /* now recur on right child */
    storeInorder(node->right, inorder, index_ptr);
}

/* A function that constructs Balanced Binary Search Tree from a sorted array
   See https://www.geeksforgeeks.org/sorted-array-to-balanced-bst/ */
struct node* sortedArrayToBST(int arr[], int start, int end)
{
    /* Base Case */
    if (start > end)
      return NULL;

    /* Get the middle element and make it root */
    int mid = (start + end)/2;
    struct node *root = newNode(arr[mid]);

    /* Recursively construct the left subtree and make it
       left child of root */
    root->left =  sortedArrayToBST(arr, start, mid-1);

    /* Recursively construct the right subtree and make it
       right child of root */
    root->right = sortedArrayToBST(arr, mid+1, end);

    return root;
}

/* Driver program to test above functions*/
int main()
{
    /* Create following tree as first balanced BST
           100
          /  \
        50    300
       / \
      20  70
    */
    struct node *root1  = newNode(100);
    root1->left         = newNode(50);
    root1->right        = newNode(300);
    root1->left->left   = newNode(20);
    root1->left->right  = newNode(70);

    /* Create following tree as second balanced BST
            80
           /  \
         40   120
    */
    struct node *root2  = newNode(80);
    root2->left         = newNode(40);
    root2->right        = newNode(120);

    struct node *mergedTree = mergeTrees(root1, root2, 5, 3);

    printf ("Following is Inorder traversal of the merged tree \n");
    printInorder(mergedTree);

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Merge Two Balanced Binary Search Trees
import java.io.*;
import java.util.ArrayList;

// A binary tree node
class Node {

    int data;
    Node left, right;

    Node(int d) {
        data = d;
        left = right = null;
    }
}

class BinarySearchTree
{

    // Root of BST
    Node root;

    // Constructor
    BinarySearchTree() {
        root = null;
    }

    // Inorder traversal of the tree
    void inorder()
    {
        inorderUtil(this.root);
    }

// Utility function for inorder traversal of the tree
void inorderUtil(Node node)
{
    if(node==null)
        return;

    inorderUtil(node.left);
    System.out.print(node.data + " ");
    inorderUtil(node.right);
}

    // A Utility Method that stores inorder traversal of a tree
    public ArrayList<Integer> storeInorderUtil(Node node, ArrayList<Integer> list)
    {
        if(node == null)
            return list;

        //recur on the left child
        storeInorderUtil(node.left, list);

        // Adds data to the list
        list.add(node.data);

        //recur on the right child
        storeInorderUtil(node.right, list);

        return list;
    }

    // Method that stores inorder traversal of a tree
    ArrayList<Integer> storeInorder(Node node)
    {
        ArrayList<Integer> list1 = new ArrayList<>();
        ArrayList<Integer> list2 = storeInorderUtil(node,list1);
        return list2;
    }

    // Method that merges two ArrayLists into one.
    ArrayList<Integer> merge(ArrayList<Integer>list1, ArrayList<Integer>list2, int m, int n)
    {
        // list3 will contain the merge of list1 and list2
        ArrayList<Integer> list3 = new ArrayList<>();
        int i=0;
        int j=0;

        //Traversing through both ArrayLists
        while( i<m && j<n)
        {
            // Smaller one goes into list3
            if(list1.get(i)<list2.get(j))
            {
                list3.add(list1.get(i));
                i++;
            }
            else
            {
                list3.add(list2.get(j));
                j++;
            }
        }

        // Adds the remaining elements of list1 into list3
        while(i<m)
        {
            list3.add(list1.get(i));
            i++;
        }

        // Adds the remaining elements of list2 into list3
        while(j<n)
        {
            list3.add(list2.get(j));
            j++;
        }
        return list3;
    }

    // Method that converts an ArrayList to a BST
    Node ALtoBST(ArrayList<Integer>list, int start, int end)
    {
        // Base case
        if(start > end)
            return null;

        // Get the middle element and make it root    
        int mid = (start+end)/2;
        Node node = new Node(list.get(mid));

        /* Recursively construct the left subtree and make it
        left child of root */
        node.left = ALtoBST(list, start, mid-1);

        /* Recursively construct the right subtree and make it
        right child of root */
        node.right = ALtoBST(list, mid+1, end);

    return node;
    }

    // Method that merges two trees into a single one.
    Node mergeTrees(Node node1, Node node2)
    {
        //Stores Inorder of tree1 to list1
        ArrayList<Integer>list1 = storeInorder(node1);

        //Stores Inorder of tree2 to list2
        ArrayList<Integer>list2 = storeInorder(node2);

        // Merges both list1 and list2 into list3
        ArrayList<Integer>list3 = merge(list1, list2, list1.size(), list2.size());

        //Eventually converts the merged list into resultant BST
        Node node = ALtoBST(list3, 0, list3.size()-1);
        return node;
    }

    // Driver function
    public static void main (String[] args)
    {

        /* Creating following tree as First balanced BST
                100
                / \
                50 300
                / \
               20 70
        */

        BinarySearchTree tree1 = new BinarySearchTree();
        tree1.root = new Node(100);
        tree1.root.left = new Node(50);
        tree1.root.right = new Node(300);
        tree1.root.left.left = new Node(20);
        tree1.root.left.right = new Node(70);

        /* Creating following tree as second balanced BST
                80
                / \
              40 120
        */

        BinarySearchTree tree2 = new BinarySearchTree();
        tree2.root = new Node(80);   
        tree2.root.left = new Node(40);
        tree2.root.right = new Node(120);

        BinarySearchTree tree = new BinarySearchTree();   
        tree.root = tree.mergeTrees(tree1.root, tree2.root);
        System.out.println("The Inorder traversal of the merged BST is: ");
        tree.inorder();
    }
}
// This code has been contributed by Kamal Rawal
```

## 蟒蛇 3

```
# A binary tree node has data, pointer to left child 
# and a pointer to right child
class Node:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

# A utility function to merge two sorted arrays into one
# Time Complexity of below function: O(m + n)
# Space Complexity of below function: O(m + n)
def merge_sorted_arr(arr1, arr2):
    arr = []
    i = j = 0
    while i < len(arr1) and j < len(arr2):
        if arr1[i] <= arr2[j]:
            arr.append(arr1[i])
            i += 1
        else:
            arr.append(arr2[j])
            j += 1
    while i < len(arr1):
        arr.append(arr1[i])
        i += 1
    while i < len(arr2):
        arr.append(arr2[j])
        j += 1
    return arr

# A helper function that stores inorder
# traversal of a tree in arr
def inorder(root, arr = []):
    if root:
        inorder(root.left, arr)
        arr.append(root.val)
        inorder(root.right, arr)

# A utility function to insert the values
# in the individual Tree
def insert(root, val):
    if not root:
        return Node(val)
    if root.val == val:
        return root
    elif root.val > val:
        root.left = insert(root.left, val)
    else:
        root.right = insert(root.right, val)
    return root

# Converts the merged array to a balanced BST
# Explanation of the below code:
# https://www.geeksforgeeks.org/sorted-array-to-balanced-bst/
def arr_to_bst(arr):
    if not arr:
        return None
    mid = len(arr) // 2
    root = Node(arr[mid])
    root.left = arr_to_bst(arr[:mid])
    root.right = arr_to_bst(arr[mid + 1:])
    return root

if __name__=='__main__':
    root1 = root2 = None

    # Inserting values in first tree
    root1 = insert(root1, 100)
    root1 = insert(root1, 50)
    root1 = insert(root1, 300)
    root1 = insert(root1, 20)
    root1 = insert(root1, 70)

    # Inserting values in second tree
    root2 = insert(root2, 80)
    root2 = insert(root2, 40)
    root2 = insert(root2, 120)
    arr1 = []
    inorder(root1, arr1)
    arr2 = []
    inorder(root2, arr2)
    arr = merge_sorted_arr(arr1, arr2)
    root = arr_to_bst(arr)
    res = []
    inorder(root, res)
    print('Following is Inorder traversal of the merged tree')
    for i in res:
      print(i, end = ' ')

# This code is contributed by Flarow4
```

## C#

```
// C# program to Merge Two Balanced Binary Search Trees
using System;
using System.Collections.Generic;

// A binary tree node
public class Node
{

    public int data;
    public Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

public class BinarySearchTree
{

    // Root of BST
    public Node root;

    // Constructor
    public BinarySearchTree()
    {
        root = null;
    }

    // Inorder traversal of the tree
    public virtual void inorder()
    {
        inorderUtil(this.root);
    }

// Utility function for inorder traversal of the tree
public virtual void inorderUtil(Node node)
{
    if (node == null)
    {
        return;
    }

    inorderUtil(node.left);
    Console.Write(node.data + " ");
    inorderUtil(node.right);
}

    // A Utility Method that stores inorder traversal of a tree
    public virtual List<int> storeInorderUtil(Node node, List<int> list)
    {
        if (node == null)
        {
            return list;
        }

        //recur on the left child
        storeInorderUtil(node.left, list);

        // Adds data to the list
        list.Add(node.data);

        //recur on the right child
        storeInorderUtil(node.right, list);

        return list;
    }

    // Method that stores inorder traversal of a tree
    public virtual List<int> storeInorder(Node node)
    {
        List<int> list1 = new List<int>();
        List<int> list2 = storeInorderUtil(node,list1);
        return list2;
    }

    // Method that merges two ArrayLists into one. 
    public virtual List<int> merge(List<int> list1, List<int> list2, int m, int n)
    {
        // list3 will contain the merge of list1 and list2
        List<int> list3 = new List<int>();
        int i = 0;
        int j = 0;

        //Traversing through both ArrayLists
        while (i < m && j < n)
        {
            // Smaller one goes into list3
            if (list1[i] < list2[j])
            {
                list3.Add(list1[i]);
                i++;
            }
            else
            {
                list3.Add(list2[j]);
                j++;
            }
        }

        // Adds the remaining elements of list1 into list3
        while (i < m)
        {
            list3.Add(list1[i]);
            i++;
        }

        // Adds the remaining elements of list2 into list3
        while (j < n)
        {
            list3.Add(list2[j]);
            j++;
        }
        return list3;
    }

    // Method that converts an ArrayList to a BST
    public virtual Node ALtoBST(List<int> list, int start, int end)
    {
        // Base case
        if (start > end)
        {
            return null;
        }

        // Get the middle element and make it root     
        int mid = (start + end) / 2;
        Node node = new Node(list[mid]);

        /* Recursively construct the left subtree and make it
        left child of root */
        node.left = ALtoBST(list, start, mid - 1);

        /* Recursively construct the right subtree and make it
        right child of root */
        node.right = ALtoBST(list, mid + 1, end);

    return node;
    }

    // Method that merges two trees into a single one. 
    public virtual Node mergeTrees(Node node1, Node node2)
    {
        //Stores Inorder of tree1 to list1
        List<int> list1 = storeInorder(node1);

        //Stores Inorder of tree2 to list2
        List<int> list2 = storeInorder(node2);

        // Merges both list1 and list2 into list3
        List<int> list3 = merge(list1, list2, list1.Count, list2.Count);

        //Eventually converts the merged list into resultant BST
        Node node = ALtoBST(list3, 0, list3.Count - 1);
        return node;
    }

    // Driver function
    public static void Main(string[] args)
    {

        /* Creating following tree as First balanced BST
                100
                / \
                50 300
                / \
               20 70
        */

        BinarySearchTree tree1 = new BinarySearchTree();
        tree1.root = new Node(100);
        tree1.root.left = new Node(50);
        tree1.root.right = new Node(300);
        tree1.root.left.left = new Node(20);
        tree1.root.left.right = new Node(70);

        /* Creating following tree as second balanced BST
                80
                / \
              40 120
        */

        BinarySearchTree tree2 = new BinarySearchTree();
        tree2.root = new Node(80);
        tree2.root.left = new Node(40);
        tree2.root.right = new Node(120);

        BinarySearchTree tree = new BinarySearchTree();
        tree.root = tree.mergeTrees(tree1.root, tree2.root);
        Console.WriteLine("The Inorder traversal of the merged BST is: ");
        tree.inorder();
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

      // JavaScript program to Merge Two
      // Balanced Binary Search Trees
      // A binary tree node
      class Node {
        constructor(d) {
          this.data = d;
          this.left = null;
          this.right = null;
        }
      }

      class BinarySearchTree {
        // Constructor
        constructor() {
          this.root = null;
        }

        // Inorder traversal of the tree
        inorder() {
          this.inorderUtil(this.root);
        }

        // Utility function for inorder traversal of the tree
        inorderUtil(node) {
          if (node == null) {
            return;
          }

          this.inorderUtil(node.left);
          document.write(node.data + " ");
          this.inorderUtil(node.right);
        }

        // A Utility Method that stores
        // inorder traversal of a tree
        storeInorderUtil(node, list) {
          if (node == null) {
            return list;
          }

          //recur on the left child
          this.storeInorderUtil(node.left, list);

          // Adds data to the list
          list.push(node.data);

          //recur on the right child
          this.storeInorderUtil(node.right, list);

          return list;
        }

        // Method that stores inorder traversal of a tree
        storeInorder(node) {
          var list1 = [];
          var list2 = this.storeInorderUtil(node, list1);
          return list2;
        }

        // Method that merges two ArrayLists into one.
        merge(list1, list2, m, n) {
          // list3 will contain the merge of list1 and list2
          var list3 = [];
          var i = 0;
          var j = 0;

          //Traversing through both ArrayLists
          while (i < m && j < n) {
            // Smaller one goes into list3
            if (list1[i] < list2[j]) {
              list3.push(list1[i]);
              i++;
            } else {
              list3.push(list2[j]);
              j++;
            }
          }

          // Adds the remaining elements of list1 into list3
          while (i < m) {
            list3.push(list1[i]);
            i++;
          }

          // Adds the remaining elements of list2 into list3
          while (j < n) {
            list3.push(list2[j]);
            j++;
          }
          return list3;
        }

        // Method that converts an ArrayList to a BST
        ALtoBST(list, start, end) {
          // Base case
          if (start > end) {
            return null;
          }

          // Get the middle element and make it root
          var mid = parseInt((start + end) / 2);
          var node = new Node(list[mid]);

          /* Recursively construct the left subtree and make it
        left child of root */
          node.left = this.ALtoBST(list, start, mid - 1);

          /* Recursively construct the right subtree and make it
        right child of root */
          node.right = this.ALtoBST(list, mid + 1, end);

          return node;
        }

        // Method that merges two trees into a single one.
        mergeTrees(node1, node2) {
          //Stores Inorder of tree1 to list1
          var list1 = this.storeInorder(node1);

          //Stores Inorder of tree2 to list2
          var list2 = this.storeInorder(node2);

          // Merges both list1 and list2 into list3
          var list3 =
          this.merge(list1, list2, list1.length, list2.length);

          //Eventually converts the merged list into resultant BST
          var node = this.ALtoBST(list3, 0, list3.length - 1);
          return node;
        }
      }
      // Driver function
      /* Creating following tree as First balanced BST
                100
                / \
                50 300
                / \
            20 70
        */

      var tree1 = new BinarySearchTree();
      tree1.root = new Node(100);
      tree1.root.left = new Node(50);
      tree1.root.right = new Node(300);
      tree1.root.left.left = new Node(20);
      tree1.root.left.right = new Node(70);

      /* Creating following tree as second balanced BST
                80
                / \
            40 120
        */

      var tree2 = new BinarySearchTree();
      tree2.root = new Node(80);
      tree2.root.left = new Node(40);
      tree2.root.right = new Node(120);

      var tree = new BinarySearchTree();
      tree.root = tree.mergeTrees(tree1.root, tree2.root);
      document.write(
      "Following is Inorder traversal of the merged tree <br>"
      );
      tree.inorder();

</script>
```

**输出:**

```
Following is Inorder traversal of the merged tree
20 40 50 70 80 100 120 300
```

**方法 3(使用 DLL 就地合并)**
我们可以使用双向链表就地合并树。以下是步骤。
1)将给定的两个二分搜索法树就地转换成双链表(这一步请参考[这篇文章](https://www.geeksforgeeks.org/the-great-tree-list-recursion-problem/))。
2)合并两个排序后的链表(这一步请参考[这篇文章](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists/))。
3)从步骤 2 中创建的合并列表中构建一个平衡的二叉查找树。(这一步参考[本帖](https://www.geeksforgeeks.org/in-place-conversion-of-sorted-dll-to-balanced-bst/))
这种方法的时间复杂度也是 O(m+n)，这种方法做转换到位。
感谢 Dheeraj 和 Ronzii 提出这个方法。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。