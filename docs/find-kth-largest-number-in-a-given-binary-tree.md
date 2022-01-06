# 在给定的二叉树中找到第 k 个最大的数

> 原文:[https://www . geesforgeks . org/find-kth-给定二叉树中的最大数/](https://www.geeksforgeeks.org/find-kth-largest-number-in-a-given-binary-tree/)

给定一个由 **N** 节点和正整数 **K** 组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是在给定的树上找到 **K <sup>第</sup>** **个最大的**数。
**示例:**

> **输入:**K = 3
> **1
> /\
> 2 3
> /\/\
> 4 5 6 7
> **输出:** 5
> **说明:**给定二叉树中第三大元素为 5。**
> 
> ****输入:**K = 1
> **1
> /\
> 2 3
> **输出:1**
> **说明:**给定二叉树中第一大元素为 1。****

******天真方法:**展平给定的二叉树，然后对数组进行排序。现在打印这个排序数组中第 Kt 个最大的数字。**** 

******高效方法:**上述方法可以通过将树的所有元素存储在[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)中而变得高效，因为元素是基于优先级顺序存储的，默认情况下优先级顺序是升序。尽管复杂性与上述方法相同，但在这里我们可以避免额外的排序步骤。
只需[打印优先队列](https://www.geeksforgeeks.org/k-largestor-smallest-elements-in-an-array/)中最大的 **K <sup>th</sup>** 元素。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Struct binary tree node
struct Node {
    int data;
    Node *left, *right;
};

// Function to create a new node of
// the tree
Node* newNode(int data)
{
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Utility function to find the Kth
// largest element in the given tree
int findKthLargest(priority_queue<int,
                                  vector<int> >& pq,
                   int k)
{
    // Loop until priority queue is not
    // empty and K greater than 0
    while (--k && !pq.empty()) {
        pq.pop();
    }

    // If PQ is not empty then return
    // the top element
    if (!pq.empty()) {
        return pq.top();
    }

    // Otherwise, return -1
    return -1;
}

// Function to traverse the given
// binary tree
void traverse(
    Node* root, priority_queue<int,
                               vector<int> >& pq)
{

    if (!root) {
        return;
    }

    // Pushing values in binary tree
    pq.push(root->data);

    // Left and Right Recursive Call
    traverse(root->left, pq);
    traverse(root->right, pq);
}

// Function to find the Kth largest
// element in the given tree
void findKthLargestTree(Node* root, int K)
{

    // Stores all elements tree in PQ
    priority_queue<int, vector<int> > pq;

    // Function Call
    traverse(root, pq);

    // Function Call
    cout << findKthLargest(pq, K);
}

// Driver Code
int main()
{
    // Given Input
    Node* root = newNode(1);
    root->left = newNode(2);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right = newNode(3);
    root->right->right = newNode(7);
    root->right->left = newNode(6);
    int K = 3;

    findKthLargestTree(root, K);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.*;
public class Main
{

    // Struct binary tree node
    static class Node
    {
        int data;
        Node left;
        Node right;
    }

    // Function to create new node of the tree
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    // Stores all elements tree in PQ
    static Vector<Integer> pq = new Vector<Integer>();

    // Utility function to find the Kth
    // largest element in the given tree
    static int findKthLargest(int k)
    {
        // Loop until priority queue is not
        // empty and K greater than 0
        --k;
        while (k > 0 && pq.size() > 0) {
            pq.remove(0);
            --k;
        }

        // If PQ is not empty then return
        // the top element
        if (pq.size() > 0) {
            return pq.get(0);
        }

        // Otherwise, return -1
        return -1;
    }

    // Function to traverse the given
    // binary tree
    static void traverse(Node root)
    {

        if (root == null) {
            return;
        }

        // Pushing values in binary tree
        pq.add(root.data);
        Collections.sort(pq);
        Collections.reverse(pq);

        // Left and Right Recursive Call
        traverse(root.left);
        traverse(root.right);
    }

    // Function to find the Kth largest
    // element in the given tree
    static void findKthLargestTree(Node root, int K)
    {
        // Function Call
        traverse(root);

        // Function Call
        System.out.print(findKthLargest(K));
    }

  // Driver code
    public static void main(String[] args)
    {

        // Given Input
        Node root = newNode(1);
        root.left = newNode(2);
        root.left.left = newNode(4);
        root.left.right = newNode(5);
        root.right = newNode(3);
        root.right.right = newNode(7);
        root.right.left = newNode(6);
        int K = 3;

        findKthLargestTree(root, K);
    }
}

// This code is contributed by divyesh07.**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach
class Node:
    # Struct binary tree node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Stores all elements tree in PQ
pq = []

# Utility function to find the Kth
# largest element in the given tree
def findKthLargest(k):
    # Loop until priority queue is not
    # empty and K greater than 0
    k-=1
    while (k > 0 and len(pq) > 0):
        pq.pop(0)
        k-=1

    # If PQ is not empty then return
    # the top element
    if len(pq) > 0:
        return pq[0]

    # Otherwise, return -1
    return -1

# Function to traverse the given
# binary tree
def traverse(root):
    if (root == None):
        return

    # Pushing values in binary tree
    pq.append(root.data)
    pq.sort()
    pq.reverse()

    # Left and Right Recursive Call
    traverse(root.left)
    traverse(root.right)

# Function to find the Kth largest
# element in the given tree
def findKthLargestTree(root, K):
    # Function Call
    traverse(root);

    # Function Call
    print(findKthLargest(K))

# Given Input
root = Node(1)
root.left = Node(2)
root.left.left = Node(4)
root.left.right = Node(5)
root.right = Node(3)
root.right.right = Node(7)
root.right.left = Node(6)
K = 3

findKthLargestTree(root, K)

# This code is contributed by mukesh07.**
```

## ****C#****

```
**// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Struct binary tree node
    class Node
    {
        public int data;
        public Node left, right;
    };

    // Function to create a new node of the tree
    static Node newNode(int data)
    {
      Node temp = new Node();
      temp.data = data;
      temp.left = null;
      temp.right = null;
      return temp;
    }

    // Stores all elements tree in PQ
    static List<int> pq = new List<int>();

    // Utility function to find the Kth
    // largest element in the given tree
    static int findKthLargest(int k)
    {
        // Loop until priority queue is not
        // empty and K greater than 0
        --k;
        while (k > 0 && pq.Count > 0) {
            pq.RemoveAt(0);
            --k;
        }

        // If PQ is not empty then return
        // the top element
        if (pq.Count > 0) {
            return pq[0];
        }

        // Otherwise, return -1
        return -1;
    }

    // Function to traverse the given
    // binary tree
    static void traverse(Node root)
    {

        if (root == null) {
            return;
        }

        // Pushing values in binary tree
        pq.Add(root.data);
        pq.Sort();
        pq.Reverse();

        // Left and Right Recursive Call
        traverse(root.left);
        traverse(root.right);
    }

    // Function to find the Kth largest
    // element in the given tree
    static void findKthLargestTree(Node root, int K)
    {
        // Function Call
        traverse(root);

        // Function Call
        Console.Write(findKthLargest(K));
    }

  static void Main() {
    // Given Input
    Node root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right = newNode(3);
    root.right.right = newNode(7);
    root.right.left = newNode(6);
    int K = 3;

    findKthLargestTree(root, K);
  }
}

// This code is contributed by divyeshrabadiya07.**
```

## ****java 描述语言****

```
**<script>
    // Javascript program for the above approach

    // Struct binary tree node
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

      // Function to create a new node of the tree
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    // Stores all elements tree in PQ
    let pq = [];

    // Utility function to find the Kth
    // largest element in the given tree
    function findKthLargest(k)
    {
        // Loop until priority queue is not
        // empty and K greater than 0
        --k;
        while (k > 0 && pq.length > 0) {
            pq.shift();
            --k;
        }

        // If PQ is not empty then return
        // the top element
        if (pq.length > 0) {
            return pq[0];
        }

        // Otherwise, return -1
        return -1;
    }

    // Function to traverse the given
    // binary tree
    function traverse(root)
    {

        if (root == null) {
            return;
        }

        // Pushing values in binary tree
        pq.push(root.data);
        pq.sort(function(a, b){return a - b});
        pq.reverse();

        // Left and Right Recursive Call
        traverse(root.left);
        traverse(root.right);
    }

    // Function to find the Kth largest
    // element in the given tree
    function findKthLargestTree(root, K)
    {
        // Function Call
        traverse(root);

        // Function Call
        document.write(findKthLargest(K));
    }

    // Given Input
    let root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right = newNode(3);
    root.right.right = newNode(7);
    root.right.left = newNode(6);
    let K = 3;

    findKthLargestTree(root, K);

    // This code is contributed by decode2207.
</script>**
```

******Output:** 

```
5
```**** 

*******时间复杂度:** O((N + K)log N)*
***辅助空间:** O(N)*****