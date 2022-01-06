# 钻石树

> 原文:[https://www.geeksforgeeks.org/diamond-tree/](https://www.geeksforgeeks.org/diamond-tree/)

给定一个数字 **K** ，任务是创建符合这两个条件的类钻石树结构:

1.  树的前 K 级应该是一个平衡的二叉树，节点的值应该从 1 开始，从左到右增加。
2.  接下来的 K-1 级应该通过合并每一对节点并将其总和存储为其子节点来形成类似钻石的结构。

**例:**

```
Input: K = 2
Output:
1 
2 3 
5
Explanation: 
Structure will look like
          1                            
        /   \    
       2     3     
        \   /
          5

For the given value k = 2
First, create a balanced
binary tree of level 2 
with a value starting from 1.
Then on level 3 merge both
the node with a node 
having value 2 + 3 = 5\.  

Input: K = 3
Output:
1 
2 3 
4 5 6 7 
9 13 
22
Explanation: 
Structure will look like
          1                            
        /   \    
      2       3     
     /  \    /  \               
    4    5  6    7
     \   /   \  /   
       9      13
        \    /
          22

Input: K = 4 
Output:
1 
2 3 
4 5 6 7 
8 9 10 11 12 13 14 15 
17 21 25 29 
38 54 
92
Explanation: 
Structure will look like
             1                            
        /        \    
      2            3     
     /  \        /    \               
    4    5       6      7
  /  \  /  \    / \    / \
  8   9 10  11 12  13 14  15
  \  /  \  /   \  /    \  / 
   17    21     25      29
     \  /         \    /
      38            54
        \          /
             92
```

**进场:**

1.  首先使用[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)创建 [K 级平衡二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)，并给出从 1 开始从左到右递增的值。

2.  现在，通过使用级别顺序一次对两个节点求和，开始合并级别
3.  最后，打印二叉树的每一级

以下是上述方法的实现:

## C++

```
// C++ program to create the diamond
// like structure of Binary Tree
// for a given value of K

#include <bits/stdc++.h>
using namespace std;

// A Tree node
struct Node {
    int data;
    Node* left;
    Node* right;
};

// Utility function to create a new node
Node* createNewNode(int value)
{
    Node* temp = NULL;
    temp = new Node();
    temp->data = value;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

// Utility function to create the diamond
// like structure of Binary tree
void createStructureUtil(queue<Node*>& qu,
                        int k)
{
    int num = 1;
    int level = k - 1;

    // Run the outer while loop
    // and create structure up to
    // the k levels
    while (level--) {

        int qsize = qu.size();

        // Run inner while loop to
        // create current level
        while (qsize--) {

            Node* temp = qu.front();
            qu.pop();
            num += 1;

            // Create left child
            temp->left = createNewNode(num);
            num += 1;

            // Create right child
            temp->right = createNewNode(num);

            // Push the left child into
            // the queue
            qu.push(temp->left);

            // Push the right child into
            // the queue
            qu.push(temp->right);
        }
    }
    num += 1;

    // Run the while loop
    while (qu.size() > 1) {

        // Pop first element from the queue
        Node* first = qu.front();
        qu.pop();

        // Pop second element from the queue
        Node* second = qu.front();
        qu.pop();

        // Create diamond structure
        first->right
            = createNewNode(first->data
                            + second->data);
        second->left = first->right;

        // Push the node into the queue
        qu.push(first->right);
    }
}

// Function to print the Diamond
// Structure of Binary Tree
void printLevelOrder(Node* root, int k)
{
    // Base Case
    if (root == NULL)
        return;

    // Create an empty queue
    queue<Node*> qu;

    // Enqueue Root and initialize height
    qu.push(root);
    int level = k - 1;

    // while loop to print the element
    // up to the (k - 1) levels
    while (level--) {

        int qsize = qu.size();
        while (qsize--) {

            Node* temp = qu.front();
            qu.pop();
            cout << temp->data << " ";

            // Enqueue left child
            if (temp->left != NULL)
                qu.push(temp->left);

            // Enqueue right child
            if (temp->right != NULL)
                qu.push(temp->right);
        }
        cout << endl;
    }

    // Loop to print the element
    // rest all level except last
    // level
    while (qu.size() > 1) {

        int qsize = qu.size();
        while (qsize) {

            Node* first = qu.front();
            qu.pop();
            Node* second = qu.front();
            qu.pop();
            cout << first->data << " "
                 << second->data << " ";
            qu.push(first->right);
            qsize = qsize - 2;
        }
        cout << endl;
    }

    // Print the last element
    Node* first = qu.front();
    qu.pop();
    cout << first->data << endl;
}

// Function to create the
// structure
void createStructure(int k)
{
    queue<Node*> qu;
    Node* root = createNewNode(1);
    qu.push(root);

    // Utility Function call to
    // create structure
    createStructureUtil(qu, k);
    printLevelOrder(root, k);
}

// Driver code
int main()
{
    int k = 4;

    // Print Structure
    createStructure(k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to create the diamond
// like structure of Binary Tree
// for a given value of K
import java.util.*;

class GFG{

// A Tree node
static class Node {
    int data;
    Node left;
    Node right;
};

// Utility function to create a new node
static Node createNewNode(int value)
{
    Node temp = null;
    temp = new Node();
    temp.data = value;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Utility function to create the diamond
// like structure of Binary tree
static void createStructureUtil(Queue<Node> qu,
                        int k)
{
    int num = 1;
    int level = k - 1;

    // Run the outer while loop
    // and create structure up to
    // the k levels
    while (level-- >0) {

        int qsize = qu.size();

        // Run inner while loop to
        // create current level
        while (qsize-- > 0) {

            Node temp = qu.peek();
            qu.remove();
            num += 1;

            // Create left child
            temp.left = createNewNode(num);
            num += 1;

            // Create right child
            temp.right = createNewNode(num);

            // Push the left child into
            // the queue
            qu.add(temp.left);

            // Push the right child into
            // the queue
            qu.add(temp.right);
        }
    }
    num += 1;

    // Run the while loop
    while (qu.size() > 1) {

        // Pop first element from the queue
        Node first = qu.peek();
        qu.remove();

        // Pop second element from the queue
        Node second = qu.peek();
        qu.remove();

        // Create diamond structure
        first.right
            = createNewNode(first.data
                            + second.data);
        second.left = first.right;

        // Push the node into the queue
        qu.add(first.right);
    }
}

// Function to print the Diamond
// Structure of Binary Tree
static void printLevelOrder(Node root, int k)
{
    // Base Case
    if (root == null)
        return;

    // Create an empty queue
    Queue<Node> qu = new LinkedList<>();

    // Enqueue Root and initialize height
    qu.add(root);
    int level = k - 1;

    // while loop to print the element
    // up to the (k - 1) levels
    while (level-- > 0) {

        int qsize = qu.size();
        while (qsize-- > 0) {

            Node temp = qu.peek();
            qu.remove();
            System.out.print(temp.data+ " ");

            // Enqueue left child
            if (temp.left != null)
                qu.add(temp.left);

            // Enqueue right child
            if (temp.right != null)
                qu.add(temp.right);
        }
        System.out.println();
    }

    // Loop to print the element
    // rest all level except last
    // level
    while (qu.size() > 1) {

        int qsize = qu.size();
        while (qsize > 0) {

            Node first = qu.peek();
            qu.remove();
            Node second = qu.peek();
            qu.remove();
            System.out.print(first.data+ " "
                 + second.data+ " ");
            qu.add(first.right);
            qsize = qsize - 2;
        }
        System.out.println();
    }

    // Print the last element
    Node first = qu.peek();
    qu.remove();
    System.out.print(first.data +"\n");
}

// Function to create the
// structure
static void createStructure(int k)
{
    Queue<Node> qu = new LinkedList<>();
    Node root = createNewNode(1);
    qu.add(root);

    // Utility Function call to
    // create structure
    createStructureUtil(qu, k);
    printLevelOrder(root, k);
}

// Driver code
public static void main(String[] args)
{
    int k = 4;

    // Print Structure
    createStructure(k);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to create the diamond
# like structure of Binary Tree
# for a given value of K

# A Tree node
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Utility function to create a new node
def createNewNode(value):

    temp = Node(value)
    return temp

# Utility function to create the diamond
# like structure of Binary tree
def createStructureUtil(qu, k):

    num = 1;
    level = k - 1;

    # Run the outer while loop
    # and create structure up to
    # the k levels
    while (level != 0):

        level -= 1

        qsize = len(qu)

        # Run inner while loop to
        # create current level
        while (qsize != 0):

            qsize -= 1    
            temp = qu[0];
            qu.pop(0);
            num += 1;

            # Create left child
            temp.left = createNewNode(num);
            num += 1;

            # Create right child
            temp.right = createNewNode(num);

            # Push the left child into
            # the queue
            qu.append(temp.left);

            # Push the right child into
            # the queue
            qu.append(temp.right);

    num += 1;

    # Run the while loop
    while (len(qu) > 1):

        # Pop first element from the queue
        first = qu[0];
        qu.pop(0);

        # Pop second element from the queue
        second = qu[0];
        qu.pop(0);

        # Create diamond structure
        first.right = createNewNode(first.data + second.data);
        second.left = first.right;

        # Push the node into the queue
        qu.append(first.right);

# Function to print the Diamond
# Structure of Binary Tree
def printLevelOrder(root, k):

    # Base Case
    if (root == None):
        return;

    # Create an empty queue
    qu = []

    # Enqueue Root and initialize height
    qu.append(root);
    level = k - 1;

    # while loop to print the element
    # up to the (k - 1) levels
    while (level != 0):

        level -= 1

        qsize = len(qu)

        while (qsize != 0):

            qsize -= 1

            temp = qu[0];
            qu.pop(0);
            print(temp.data, end = ' ')

            # Enqueue left child
            if (temp.left != None):
                qu.append(temp.left);

            # Enqueue right child
            if (temp.right != None):
                qu.append(temp.right);
        print()

    # Loop to print the element
    # rest all level except last
    # level
    while (len(qu) > 1):

        qsize = len(qu)

        while (qsize != 0):

            first = qu[0];
            qu.pop(0);
            second = qu[0];
            qu.pop(0);
            print(str(first.data)+' '+str(second.data), end = ' ')
            qu.append(first.right);
            qsize = qsize - 2;
        print()

    # Print the last element
    first = qu[0];
    qu.pop(0);
    print(first.data)

# Function to create the
# structure
def createStructure(k):

    qu = []
    root = createNewNode(1);
    qu.append(root);

    # Utility Function call to
    # create structure
    createStructureUtil(qu, k);
    printLevelOrder(root, k);

# Driver code
if __name__=='__main__':

    k = 4;

    # Print Structure
    createStructure(k);

    # This code is contributed by rutvik_56
```

## C#

```
// C# program to create the diamond
// like structure of Binary Tree
// for a given value of K
using System;
using System.Collections.Generic;

class GFG{

// A Tree node
class Node {
    public int data;
    public Node left;
    public Node right;
};

// Utility function to create a new node
static Node createNewNode(int value)
{
    Node temp = null;
    temp = new Node();
    temp.data = value;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Utility function to create the diamond
// like structure of Binary tree
static void createStructureUtil(Queue<Node> qu,
                        int k)
{
    int num = 1;
    int level = k - 1;

    // Run the outer while loop
    // and create structure up to
    // the k levels
    while (level-- >0) {

        int qsize = qu.Count;

        // Run inner while loop to
        // create current level
        while (qsize-- > 0) {

            Node temp = qu.Peek();
            qu.Dequeue();
            num += 1;

            // Create left child
            temp.left = createNewNode(num);
            num += 1;

            // Create right child
            temp.right = createNewNode(num);

            // Push the left child into
            // the queue
            qu.Enqueue(temp.left);

            // Push the right child into
            // the queue
            qu.Enqueue(temp.right);
        }
    }
    num += 1;

    // Run the while loop
    while (qu.Count > 1) {

        // Pop first element from the queue
        Node first = qu.Peek();
        qu.Dequeue();

        // Pop second element from the queue
        Node second = qu.Peek();
        qu.Dequeue();

        // Create diamond structure
        first.right
            = createNewNode(first.data
                            + second.data);
        second.left = first.right;

        // Push the node into the queue
        qu.Enqueue(first.right);
    }
}

// Function to print the Diamond
// Structure of Binary Tree
static void printLevelOrder(Node root, int k)
{
    // Base Case
    if (root == null)
        return;

    // Create an empty queue
    Queue<Node> qu = new Queue<Node>();

    // Enqueue Root and initialize height
    qu.Enqueue(root);
    int level = k - 1;

    // while loop to print the element
    // up to the (k - 1) levels
    while (level-- > 0) {

        int qsize = qu.Count;
        while (qsize-- > 0) {

            Node temp = qu.Peek();
            qu.Dequeue();
            Console.Write(temp.data+ " ");

            // Enqueue left child
            if (temp.left != null)
                qu.Enqueue(temp.left);

            // Enqueue right child
            if (temp.right != null)
                qu.Enqueue(temp.right);
        }
        Console.WriteLine();
    }

    // Loop to print the element
    // rest all level except last
    // level
    Node first;
    while (qu.Count > 1) {

        int qsize = qu.Count;
        while (qsize > 0) {

            first = qu.Peek();
            qu.Dequeue();
            Node second = qu.Peek();
            qu.Dequeue();
            Console.Write(first.data+ " "
                 + second.data+ " ");
            qu.Enqueue(first.right);
            qsize = qsize - 2;
        }
        Console.WriteLine();
    }

    // Print the last element
    first = qu.Peek();
    qu.Dequeue();
    Console.Write(first.data +"\n");
}

// Function to create the
// structure
static void createStructure(int k)
{
    Queue<Node> qu = new Queue<Node>();
    Node root = createNewNode(1);
    qu.Enqueue(root);

    // Utility Function call to
    // create structure
    createStructureUtil(qu, k);
    printLevelOrder(root, k);
}

// Driver code
public static void Main(String[] args)
{
    int k = 4;

    // Print Structure
    createStructure(k);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

    // JavaScript program to create the diamond
    // like structure of Binary Tree
    // for a given value of K

    // A Tree node
    class Node {
        constructor(value) {
           this.left = null;
           this.right = null;
           this.data = value;
        }
    }

    // Utility function to create a new node
    function createNewNode(value)
    {
        let temp = null;
        temp = new Node(value);
        return temp;
    }

    // Utility function to create the diamond
    // like structure of Binary tree
    function createStructureUtil(qu, k)
    {
        let num = 1;
        let level = k - 1;

        // Run the outer while loop
        // and create structure up to
        // the k levels
        while (level-- >0) {

            let qsize = qu.length;

            // Run inner while loop to
            // create current level
            while (qsize-- > 0) {

                let temp = qu[0];
                qu.shift();
                num += 1;

                // Create left child
                temp.left = createNewNode(num);
                num += 1;

                // Create right child
                temp.right = createNewNode(num);

                // Push the left child into
                // the queue
                qu.push(temp.left);

                // Push the right child into
                // the queue
                qu.push(temp.right);
            }
        }
        num += 1;

        // Run the while loop
        while (qu.length > 1) {

            // Pop first element from the queue
            let first = qu[0];
            qu.shift();

            // Pop second element from the queue
            let second = qu[0];
            qu.shift();

            // Create diamond structure
            first.right
                = createNewNode(first.data
                                + second.data);
            second.left = first.right;

            // Push the node into the queue
            qu.push(first.right);
        }
    }

    // Function to print the Diamond
    // Structure of Binary Tree
    function printLevelOrder(root, k)
    {
        // Base Case
        if (root == null)
            return;

        // Create an empty queue
        let qu = [];

        // Enqueue Root and initialize height
        qu.push(root);
        let level = k - 1;

        // while loop to print the element
        // up to the (k - 1) levels
        while (level-- > 0) {

            let qsize = qu.length;
            while (qsize-- > 0) {

                let temp = qu[0];
                qu.shift();
                document.write(temp.data+ " ");

                // Enqueue left child
                if (temp.left != null)
                    qu.push(temp.left);

                // Enqueue right child
                if (temp.right != null)
                    qu.push(temp.right);
            }
            document.write("</br>");
        }

        // Loop to print the element
        // rest all level except last
        // level
        while (qu.length > 1) {

            let qsize = qu.length;
            while (qsize > 0) {

                let first = qu[0];
                qu.shift();
                let second = qu[0];
                qu.shift();
                document.write(first.data + " " + second.data+ " ");
                qu.push(first.right);
                qsize = qsize - 2;
            }
            document.write("</br>");
        }

        // Print the last element
        let first = qu[0];
        qu.shift();
        document.write(first.data +"</br>");
    }

    // Function to create the
    // structure
    function createStructure(k)
    {
        let qu = [];
        let root = createNewNode(1);
        qu.push(root);

        // Utility Function call to
        // create structure
        createStructureUtil(qu, k);
        printLevelOrder(root, k);
    }

    let k = 4;

    // Print Structure
    createStructure(k);

</script>
```

**Output:** 

```
1 
2 3 
4 5 6 7 
8 9 10 11 12 13 14 15 
17 21 25 29 
38 54 
92
```