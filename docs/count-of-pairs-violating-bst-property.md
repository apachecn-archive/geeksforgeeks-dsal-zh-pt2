# 违反 BST 属性的配对数

> 原文:[https://www . geesforgeks . org/对计数-违反-bst-property/](https://www.geeksforgeeks.org/count-of-pairs-violating-bst-property/)

给定一棵二叉树和树中的节点数，任务是找出违反 BST 属性的**对的数量。[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)是一种基于节点的二叉树数据结构，具有以下特性:**

*   节点的左子树只包含键小于节点键的节点。
*   节点的右子树只包含键大于节点键的节点。
*   左右子树也必须是二叉查找树树。

**示例:**

```
Input: 
         4
       /   \
      5     6
Output: 1
For the above binary tree, pair (5, 4) 
violate the BST property. Thus, count
of pairs violating BST property is 1.

Input:
           50
        /     \
      30        60
     /  \     /    \
   20    25  10     40
Output: 7
For the above binary tree, pairs (20, 10),
(25, 10), (30, 25), (30, 10), (50, 10), 
(50, 40), (60, 40) violate the BST property. 
Thus, count of pairs violating BST property 
is 7.
```

**进场:**

*   将二叉树的有序遍历存储在数组中。
*   现在计算所有的对，使得**a【I】>a【j】为 i < j** ，这是数组中[反转](https://www.geeksforgeeks.org/counting-inversions/)的数目。
*   打印违反 BST 属性的对的**计数。**

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of pairs
// in a binary tree violating the BST property
import java.io.*;
import java.util.*;

// Class that represents a node of the tree
class Node {
    int data;
    Node left, right;

    // Constructor to create a new tree node
    Node(int key)
    {
        data = key;
        left = right = null;
    }
}

class GFG {

    // This method sorts the input array and returns the
    // number of inversions in the array
    static int mergeSort(int arr[], int array_size)
    {
        int temp[] = new int[array_size];
        return _mergeSort(arr, temp, 0, array_size - 1);
    }

    // An auxiliary recursive method that sorts
    // the input array and  returns the number of
    // inversions in the array
    static int _mergeSort(int arr[], int temp[],
                          int left, int right)
    {
        int mid, inv_count = 0;
        if (right > left) {

            // Divide the array into two parts and
            // call _mergeSortAndCountInv() for each
            // of the parts
            mid = (right + left) / 2;

            // Inversion count will be sum of inversions
            // in left-part, right-part and number of
            // inversions in merging
            inv_count = _mergeSort(arr, temp, left, mid);
            inv_count += _mergeSort(arr, temp, mid + 1, right);

            // Merge the two parts
            inv_count += merge(arr, temp, left, mid + 1, right);
        }
        return inv_count;
    }

    // This method merges two sorted arrays and returns
    // inversion count in the arrays
    static int merge(int arr[], int temp[], int left,
                     int mid, int right)
    {
        int i, j, k;
        int inv_count = 0;

        // i is index for left subarray
        i = left;

        // j is index for right subarray
        j = mid;

        // k is index for resultant merged subarray
        k = left;
        while ((i <= mid - 1) && (j <= right)) {
            if (arr[i] <= arr[j]) {
                temp[k++] = arr[i++];
            }
            else {
                temp[k++] = arr[j++];
                inv_count = inv_count + (mid - i);
            }
        }

        // Copy the remaining elements of left subarray
        // (if there are any) to temp
        while (i <= mid - 1)
            temp[k++] = arr[i++];

        // Copy the remaining elements of right subarray
        // if there are any) to temp
        while (j <= right)
            temp[k++] = arr[j++];

        // Copy back the merged elements to original array
        for (i = left; i <= right; i++)
            arr[i] = temp[i];

        return inv_count;
    }

    // Array to store
    // inorder traversal of the binary tree
    static int[] a;
    static int in;

    // Inorder traversal of the binary tree
    static void Inorder(Node node)
    {
        if (node == null)
            return;

        Inorder(node.left);
        a[in++] = node.data;
        Inorder(node.right);
    }

    // Function to count the pairs
    // in a binary tree violating BST property
    static int pairsViolatingBST(Node root, int N)
    {
        if (root == null)
            return 0;

        in = 0;
        a = new int[N];
        Inorder(root);

        // Total inversions in the array
        int inversionCount = mergeSort(a, N);

        return inversionCount;
    }

    // Driver code
    public static void main(String args[])
    {
        int N = 7;
        Node root = new Node(50);
        root.left = new Node(30);
        root.right = new Node(60);
        root.left.left = new Node(20);
        root.left.right = new Node(25);
        root.right.left = new Node(10);
        root.right.right = new Node(40);

        System.out.println(pairsViolatingBST(root, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program to count number of pairs
# in a binary tree violating the BST property

# Class that represents a node of the tree
class newNode:

    def __init__(self, key):

        self.data = key
        self.left = None
        self.right = None

# Array to store
# inorder traversal of the binary tree
a = []
id = 0

# This method sorts the input array
# and returns the number of inversions
# in the array
def mergeSort(array_size):

    temp = [0] * array_size
    return _mergeSort(temp, 0, array_size - 1)

# An auxiliary recursive method that sorts
# the input array and  returns the number of
# inversions in the array
def _mergeSort(temp, left, right):

    inv_count = 0

    if (right > left):

        # Divide the array into two parts and
        # call _mergeSortAndCountInv() for each
        # of the parts
        mid = (right + left) // 2

        # Inversion count will be sum of inversions
        # in left-part, right-part and number of
        # inversions in merging
        inv_count = _mergeSort(temp, left, mid)
        inv_count += _mergeSort(temp, mid + 1,
                                right)

        # Merge the two parts
        inv_count += merge(temp, left, mid + 1,
                           right)

    return inv_count

# This method merges two sorted arrays
# and returns inversion count in the arrays
def merge(temp, left, mid, right):

    global a
    inv_count = 0

    # i is index for left subarray
    i = left

    # j is index for right subarray
    j = mid

    # k is index for resultant merged subarray
    k = left

    while ((i <= mid - 1) and (j <= right)):
        if (a[i] <= a[j]):
            temp[k] = a[i]
            k += 1
            i += 1

        else:
            temp[k] = a[j]
            k += 1
            j += 1
            inv_count = inv_count + (mid - i)

    # Copy the remaining elements of left
    # subarray (if there are any) to temp
    while (i <= mid - 1):
        temp[k] = a[i]
        k += 1
        i += 1

    # Copy the remaining elements of right
    # subarray if there are any) to temp
    while (j <= right):
        temp[k] = a[j]
        k += 1
        j += 1

    # Copy back the merged elements
    # to original array
    for i in range(left, right + 1, 1):
        a[i] = temp[i]

    return inv_count

# Inorder traversal of the binary tree
def Inorder(node):

    global a
    global id

    if (node == None):
        return

    Inorder(node.left)
    a.append(node.data)
    id += 1
    Inorder(node.right)

# Function to count the pairs
# in a binary tree violating
# BST property
def pairsViolatingBST(root, N):

    if (root == None):
        return 0

    Inorder(root)

    # Total inversions in the array
    inversionCount = mergeSort(N)

    return inversionCount

# Driver code
if __name__ == '__main__':

    N = 7
    root = newNode(50)
    root.left = newNode(30)
    root.right = newNode(60)
    root.left.left = newNode(20)
    root.left.right = newNode(25)
    root.right.left = newNode(10)
    root.right.right = newNode(40)

    print(pairsViolatingBST(root, N))

# This code is contributed by bgangwar59
```

## C#

```
// C# program to count number of pairs
// in a binary tree violating the BST property
using System;

// Class that represents a node of the tree
public class Node {
    public int data;
    public Node left, right;

    // Constructor to create a new tree node
    public Node(int key)
    {
        data = key;
        left = right = null;
    }
}

class GFG {

    // This method sorts the input array and returns the
    // number of inversions in the array
    static int mergeSort(int[] arr, int array_size)
    {
        int[] temp = new int[array_size];
        return _mergeSort(arr, temp, 0, array_size - 1);
    }

    // An auxiliary recursive method that sorts
    // the input array and returns the number of
    // inversions in the array
    static int _mergeSort(int[] arr, int[] temp,
                          int left, int right)
    {
        int mid, inv_count = 0;
        if (right > left) {

            // Divide the array into two parts and
            // call _mergeSortAndCountInv() for each
            // of the parts
            mid = (right + left) / 2;

            // Inversion count will be sum of inversions
            // in left-part, right-part and number of
            // inversions in merging
            inv_count = _mergeSort(arr, temp, left, mid);
            inv_count += _mergeSort(arr, temp, mid + 1, right);

            // Merge the two parts
            inv_count += merge(arr, temp, left, mid + 1, right);
        }
        return inv_count;
    }

    // This method merges two sorted arrays and returns
    // inversion count in the arrays
    static int merge(int[] arr, int[] temp, int left,
                     int mid, int right)
    {
        int i, j, k;
        int inv_count = 0;

        // i is index for left subarray
        i = left;

        // j is index for right subarray
        j = mid;

        // k is index for resultant merged subarray
        k = left;
        while ((i <= mid - 1) && (j <= right)) {
            if (arr[i] <= arr[j]) {
                temp[k++] = arr[i++];
            }
            else {
                temp[k++] = arr[j++];
                inv_count = inv_count + (mid - i);
            }
        }

        // Copy the remaining elements of left subarray
        // (if there are any) to temp
        while (i <= mid - 1)
            temp[k++] = arr[i++];

        // Copy the remaining elements of right subarray
        // if there are any) to temp
        while (j <= right)
            temp[k++] = arr[j++];

        // Copy back the merged elements to original array
        for (i = left; i <= right; i++)
            arr[i] = temp[i];

        return inv_count;
    }

    // Array to store
    // inorder traversal of the binary tree
    static int[] a;
    static int i;

    // Inorder traversal of the binary tree
    static void Inorder(Node node)
    {
        if (node == null)
            return;

        Inorder(node.left);
        a[i++] = node.data;
        Inorder(node.right);
    }

    // Function to count the pairs
    // in a binary tree violating BST property
    static int pairsViolatingBST(Node root, int N)
    {
        if (root == null)
            return 0;

        i = 0;
        a = new int[N];
        Inorder(root);

        // Total inversions in the array
        int inversionCount = mergeSort(a, N);

        return inversionCount;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int N = 7;
        Node root = new Node(50);
        root.left = new Node(30);
        root.right = new Node(60);
        root.left.left = new Node(20);
        root.left.right = new Node(25);
        root.right.left = new Node(10);
        root.right.right = new Node(40);

        Console.WriteLine(pairsViolatingBST(root, N));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
      // JavaScript program to count number of pairs
      // in a binary tree violating the BST property
      // Class that represents a node of the tree
      class Node
      {

        // Constructor to create a new tree node
        constructor(key) {
          this.data = key;
          this.left = null;
          this.right = null;
        }
      }

      // This method sorts the input array and returns the
      // number of inversions in the array
      function mergeSort(arr, array_size) {
        var temp = new Array(array_size).fill(0);
        return _mergeSort(arr, temp, 0, array_size - 1);
      }

      // An auxiliary recursive method that sorts
      // the input array and returns the number of
      // inversions in the array
      function _mergeSort(arr, temp, left, right) {
        var mid,
          inv_count = 0;
        if (right > left)
        {

          // Divide the array into two parts and
          // call _mergeSortAndCountInv() for each
          // of the parts
          mid = parseInt((right + left) / 2);

          // Inversion count will be sum of inversions
          // in left-part, right-part and number of
          // inversions in merging
          inv_count = _mergeSort(arr, temp, left, mid);
          inv_count += _mergeSort(arr, temp, mid + 1, right);

          // Merge the two parts
          inv_count += merge(arr, temp, left, mid + 1, right);
        }
        return inv_count;
      }

      // This method merges two sorted arrays and returns
      // inversion count in the arrays
      function merge(arr, temp, left, mid, right) {
        var i, j, k;
        var inv_count = 0;

        // i is index for left subarray
        i = left;

        // j is index for right subarray
        j = mid;

        // k is index for resultant merged subarray
        k = left;
        while (i <= mid - 1 && j <= right) {
          if (arr[i] <= arr[j]) {
            temp[k++] = arr[i++];
          } else {
            temp[k++] = arr[j++];
            inv_count = inv_count + (mid - i);
          }
        }

        // Copy the remaining elements of left subarray
        // (if there are any) to temp
        while (i <= mid - 1) temp[k++] = arr[i++];

        // Copy the remaining elements of right subarray
        // if there are any) to temp
        while (j <= right) temp[k++] = arr[j++];

        // Copy back the merged elements to original array
        for (i = left; i <= right; i++) arr[i] = temp[i];

        return inv_count;
      }

      // Array to store
      // inorder traversal of the binary tree
      var a = [];
      var i;

      // Inorder traversal of the binary tree
      function Inorder(node) {
        if (node == null) return;

        Inorder(node.left);
        a[i++] = node.data;
        Inorder(node.right);
      }

      // Function to count the pairs
      // in a binary tree violating BST property
      function pairsViolatingBST(root, N) {
        if (root == null) return 0;

        i = 0;
        a = new Array(N).fill(0);
        Inorder(root);

        // Total inversions in the array
        var inversionCount = mergeSort(a, N);

        return inversionCount;
      }

      // Driver code
      var N = 7;
      var root = new Node(50);
      root.left = new Node(30);
      root.right = new Node(60);
      root.left.left = new Node(20);
      root.left.right = new Node(25);
      root.right.left = new Node(10);
      root.right.right = new Node(40);

      document.write(pairsViolatingBST(root, N) + "<br>");

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
7
```