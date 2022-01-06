# 给定预算内可访问的最大叶节点数

> 原文:[https://www . geesforgeks . org/在给定预算内可访问的最大叶节点数/](https://www.geeksforgeeks.org/maximum-number-of-leaf-nodes-that-can-be-visited-within-the-given-budget/)

给定一个二叉树和一个代表预算的整数 **b** 。任务是，如果访问叶节点的**成本等于该叶节点**的**级别，则找出在给定预算下可访问的最大叶节点数。
**注:**树根在**一级**。
**举例:**** 

```
Input: b = 8
           10
         /    \
        8       15
       /      /   \
      3      11     18 
              \
               13
Output: 2
For the above binary tree, leaf nodes are 3, 
13 and 18 at levels 3, 4 and 3 respectively.
Cost for visiting leaf node 3 is 3
Cost for visiting leaf node 13 is 4
Cost for visiting leaf node 18 is 3
Thus with given budget = 8, we can at maximum
visit two leaf nodes.

Input: b = 1
           8
         /   \
        7     10
       /      
      3      

Output: 0 
For the above binary tree, leaf nodes are
3 and 10 at levels 3 and 2 respectively.
Cost for visiting leaf node 3 is 3
Cost for visiting leaf node 10 is 2
In given budget = 1, we can't visit
any leaf node.
```

**进场:**

*   使用级别顺序遍历遍历二叉树，将所有叶节点的级别存储在[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)中。
*   从优先级队列中逐个删除一个元素，检查该值是否在预算范围内。
*   如果**是**，则**从预算中减去**该值，并更新**计数=计数+ 1** 。
*   否则，打印给定预算内可访问的最大叶节点的**计数。**

以下是上述方法的实现:

## C++

```
// C++ program to calculate the maximum number of leaf
// nodes that can be visited within the given budget
#include <bits/stdc++.h>
using namespace std;

// struct that represents a node of the tree
struct Node {
    Node* left;
    Node* right;
    int data;

    Node(int key)
    {
        data = key;
        this->left = nullptr;
        this->right = nullptr;
    }
};

Node* newNode(int key)
{
    Node* temp = new Node(key);
    return temp;
}

// Priority queue to store the levels
// of all the leaf nodes
vector<int> pq;

// Level order traversal of the binary tree
void levelOrder(Node* root)
{
    vector<Node*> q;
    int len, level = 0;
    Node* temp;

    // If tree is empty
    if (root == nullptr)
        return;

    q.push_back(root);

    while (true) {

        len = q.size();
        if (len == 0)
            break;
        level++;
        while (len > 0) {

            temp = q[0];
            q.erase(q.begin());

            // If left child exists
            if (temp->left != nullptr)
                q.push_back(temp->left);

            // If right child exists
            if (temp->right != nullptr)
                q.push_back(temp->right);

            // If node is a leaf node
            if (temp->left == nullptr && temp->right == nullptr)
            {
                pq.push_back(level);
                sort(pq.begin(), pq.end());
                reverse(pq.begin(), pq.end());
            }
            len--;
        }
    }
}

// Function to calculate the maximum number of leaf nodes
// that can be visited within the given budget
int countLeafNodes(Node* root, int budget)
{
    levelOrder(root);
    int val;

    // Variable to store the count of
    // number of leaf nodes possible to visit
    // within the given budget
    int count = 0;

    while (pq.size() != 0) {

        // Removing element from
        // min priority queue one by one
        val = pq[0];
        pq.erase(pq.begin());

        // If current val is under budget, the
        // node can be visited
        // Update the budget afterwards
        if (val <= budget) {
            count++;
            budget -= val;
        }
        else
            break;
    }
    return count;
}

// Driver code
int main()
{
    Node* root = newNode(10);
    root->left = newNode(8);
    root->right = newNode(15);
    root->left->left = newNode(3);
    root->left->left->right = newNode(13);
    root->right->left = newNode(11);
    root->right->right = newNode(18);

    int budget = 8;

    cout << countLeafNodes(root, budget);

    return 0;
}

// This code is contributed by decode2207.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the maximum number of leaf
// nodes that can be visited within the given budget
import java.io.*;
import java.util.*;
import java.lang.*;

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

    // Priority queue to store the levels
    // of all the leaf nodes
    static PriorityQueue<Integer> pq;

    // Level order traversal of the binary tree
    static void levelOrder(Node root)
    {
        Queue<Node> q = new LinkedList<>();
        int len, level = 0;
        Node temp;

        // If tree is empty
        if (root == null)
            return;

        q.add(root);

        while (true) {

            len = q.size();
            if (len == 0)
                break;
            level++;
            while (len > 0) {

                temp = q.remove();

                // If left child exists
                if (temp.left != null)
                    q.add(temp.left);

                // If right child exists
                if (temp.right != null)
                    q.add(temp.right);

                // If node is a leaf node
                if (temp.left == null && temp.right == null)
                    pq.add(level);
                len--;
            }
        }
    }

    // Function to calculate the maximum number of leaf nodes
    // that can be visited within the given budget
    static int countLeafNodes(Node root, int budget)
    {
        pq = new PriorityQueue<>();
        levelOrder(root);
        int val;

        // Variable to store the count of
        // number of leaf nodes possible to visit
        // within the given budget
        int count = 0;

        while (pq.size() != 0) {

            // Removing element from
            // min priority queue one by one
            val = pq.poll();

            // If current val is under budget, the
            // node can be visited
            // Update the budget afterwards
            if (val <= budget) {
                count++;
                budget -= val;
            }
            else
                break;
        }
        return count;
    }

    // Driver code
    public static void main(String args[])
    {

        Node root = new Node(10);
        root.left = new Node(8);
        root.right = new Node(15);
        root.left.left = new Node(3);
        root.left.left.right = new Node(13);
        root.right.left = new Node(11);
        root.right.right = new Node(18);

        int budget = 8;

        System.out.println(countLeafNodes(root, budget));
    }
}
```

## 蟒蛇 3

```
# Python3 program to calculate the maximum number of leaf
# nodes that can be visited within the given budget

# struct that represents a node of the tree
class Node:
    # Constructor to set the data of
    # the newly created tree node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Priority queue to store the levels
# of all the leaf nodes
pq = []

# Level order traversal of the binary tree
def levelOrder(root):

    q = []
    level = 0

    # If tree is empty
    if (root == None):
        return

    q.append(root)

    while (True) :

        Len = len(q)
        if (Len == 0):
            break
        level+=1
        while (Len > 0) :

            temp = q[0]
            del q[0]

            # If left child exists
            if (temp.left != None):
                q.append(temp.left)

            # If right child exists
            if (temp.right != None):
                q.append(temp.right)

            # If node is a leaf node
            if (temp.left == None and temp.right == None):

                pq.append(level)
                pq.sort()
                pq.reverse()

            Len-=1

    return pq

# Function to calculate the maximum number of leaf nodes
# that can be visited within the given budget
def countLeafNodes(root, budget):

    pq = levelOrder(root)

    # Variable to store the count of
    # number of leaf nodes possible to visit
    # within the given budget
    count = 0

    while (len(pq) != 0) :

        # Removing element from
        # min priority queue one by one
        val = pq[0]
        del pq[0]

        # If current val is under budget, the
        # node can be visited
        # Update the budget afterwards
        if (val <= budget) :
            count+=1
            budget -= val

        else:
            break

    return count

root = Node(10)
root.left = Node(8)
root.right = Node(15);
root.left.left = Node(3)
root.left.left.right = Node(13)
root.right.left = Node(11)
root.right.right = Node(18)

budget = 8

print(countLeafNodes(root, budget))

# This code is contributed by suresh07.
```

## C#

```
// C# program to calculate the maximum number of leaf
// nodes that can be visited within the given budget
using System;
using System.Collections.Generic;
class GFG {

    // Class that represents a node of the tree
    class Node
    {
        public Node left, right;
        public int data;
    };

    static Node newNode(int key)
    {
        Node temp = new Node();
        temp.data = key;
        temp.left = temp.right = null;
        return temp;
    }

    // Priority queue to store the levels
    // of all the leaf nodes
    static List<int> pq;

    // Level order traversal of the binary tree
    static void levelOrder(Node root)
    {
        List<Node> q = new List<Node>();
        int len, level = 0;
        Node temp;

        // If tree is empty
        if (root == null)
            return;

        q.Add(root);

        while (true) {

            len = q.Count;
            if (len == 0)
                break;
            level++;
            while (len > 0) {

                temp = q[0];
                q.RemoveAt(0);

                // If left child exists
                if (temp.left != null)
                    q.Add(temp.left);

                // If right child exists
                if (temp.right != null)
                    q.Add(temp.right);

                // If node is a leaf node
                if (temp.left == null && temp.right == null)
                {
                    pq.Add(level);
                    pq.Sort();
                    pq.Reverse();
                }
                len--;
            }
        }
    }

    // Function to calculate the maximum number of leaf nodes
    // that can be visited within the given budget
    static int countLeafNodes(Node root, int budget)
    {
        pq = new List<int>();
        levelOrder(root);
        int val;

        // Variable to store the count of
        // number of leaf nodes possible to visit
        // within the given budget
        int count = 0;

        while (pq.Count != 0) {

            // Removing element from
            // min priority queue one by one
            val = pq[0];
            pq.RemoveAt(0);

            // If current val is under budget, the
            // node can be visited
            // Update the budget afterwards
            if (val <= budget) {
                count++;
                budget -= val;
            }
            else
                break;
        }
        return count;
    }

  static void Main() {
    Node root = newNode(10);
    root.left = newNode(8);
    root.right = newNode(15);
    root.left.left = newNode(3);
    root.left.left.right = newNode(13);
    root.right.left = newNode(11);
    root.right.right = newNode(18);

    int budget = 8;

    Console.Write(countLeafNodes(root, budget));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

    // JavaScript program to calculate
    // the maximum number of leaf
    // nodes that can be visited within the given budget

    // Class that represents a node of the tree
    class Node {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Priority queue to store the levels
    // of all the leaf nodes
    let pq = [];

    // Level order traversal of the binary tree
    function levelOrder(root)
    {
        let q = [];
        let len, level = 0;
        let temp;

        // If tree is empty
        if (root == null)
            return;

        q.push(root);

        while (true) {

            len = q.length;
            if (len == 0)
                break;
            level++;
            while (len > 0) {

                temp = q.shift();

                // If left child exists
                if (temp.left != null)
                    q.push(temp.left);

                // If right child exists
                if (temp.right != null)
                    q.push(temp.right);

                // If node is a leaf node
                if (temp.left == null && temp.right == null)
                {
                    pq.push(level);
                    pq.sort(function(a, b){return a - b});
                    pq.reverse();
                }
                len--;
            }
        }
    }

    // Function to calculate the maximum number of leaf nodes
    // that can be visited within the given budget
    function countLeafNodes(root, budget)
    {
        pq = [];
        levelOrder(root);
        let val;

        // Variable to store the count of
        // number of leaf nodes possible to visit
        // within the given budget
        let count = 0;

        while (pq.length != 0) {

            // Removing element from
            // min priority queue one by one
            val = pq[0];
            pq.shift();

            // If current val is under budget, the
            // node can be visited
            // Update the budget afterwards
            if (val <= budget) {
                count++;
                budget -= val;
            }
            else
                break;
        }
        return count;
    }

    let root = new Node(10);
    root.left = new Node(8);
    root.right = new Node(15);
    root.left.left = new Node(3);
    root.left.left.right = new Node(13);
    root.right.left = new Node(11);
    root.right.right = new Node(18);

    let budget = 8;

    document.write(countLeafNodes(root, budget));

</script>
```

**Output:** 

```
2
```