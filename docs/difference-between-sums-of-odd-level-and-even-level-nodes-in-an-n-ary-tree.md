# N 元树中奇数层和偶数层节点的和之差

> 原文:[https://www . geesforgeks . org/奇数层和偶数层树中节点的和之差/](https://www.geeksforgeeks.org/difference-between-sums-of-odd-level-and-even-level-nodes-in-an-n-ary-tree/)

给定一个以 1 为根的 [N 元树](https://en.wikipedia.org/wiki/M-ary_tree)，任务是找出奇数层节点的和与偶数层节点的和之间的差。

**示例:**

> **输入:**
> 4
> /| \
> 2 3-5
> /\/\
> -1 3-2 6
> **输出:** 10
> **说明:**
> 偶数级节点之和= 2 + 3 + (-5) = 0
> 奇数级节点之和= 4 + (-1) + 3 + (-2) + 6 = 10
> 因此，所需的差值为
> 
> **输入:**
> 1
> /| \
> 2-1 3
> /\ \
> 4 5 8
> //| \
> 2 6 12 7
> 
> **输出:** -13

**方法:**解决问题的思路是利用[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)找到偶数级和奇数级节点各自的和，并计算它们之间的差。按照以下步骤解决问题:

*   初始化一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)来存储节点及其各自的级别。
*   初始化变量 **evenSum** 和 **oddSum** 分别存储偶数层和奇数层节点的和。
*   将 **N 元树**的**根**连同其对应的级别，即 1，推入**队列**。
*   现在，重复以下步骤，直到队列变空:
    *   从队列中弹出节点。将弹出节点的级别存储在一个变量中，比如 **currentLevel。**
    *   如果**当前级别**为**偶数**，则将该节点的值添加到**偶数**。否则，添加到 **oddSum** 。
    *   将其所有子对象推入队列，并将它们各自的级别设置为**当前级别+ 1** 。
*   完成以上步骤后，计算并打印 **oddSum** 和**event sum**的差值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a node
// of an n-ary tree
struct Node {
    int val;
    vector<Node*> children;
};

// Function to create a
// new tree node
Node* newNode(int val)
{
    Node* temp = new Node;
    temp->val = val;
    return temp;
}

// Function to find the difference
// between of sums node values of
// odd and even levels in an N-ary tree
int evenOddLevelDifference(Node* root)
{
    // Store the sums of nodes at
    // even and odd levels
    int evenSum = 0, oddSum = 0;

    // Initialize a queue to store
    // pair of node and level
    queue<pair<Node*, int> > q;

    // Push the root into the
    // queue with level 1
    q.push({ root, 1 });

    // Iterate all levels
    // of tree are traversed
    while (!q.empty()) {

        // Store the node at the
        // front of the queue
        pair<Node*, int> currNode
            = q.front();

        // Pop the front node
        q.pop();

        // Store the current level
        int currLevel
            = currNode.second;

        // Store the current node value
        int currVal
            = currNode.first->val;

        // If current node
        // level is odd
        if (currLevel % 2)

            // Add to odd sum
            oddSum += currVal;
        else

            // Add to even sum
            evenSum += currVal;

        // Push all the children of current node
        // with increasing current level by 1
        for (auto child : currNode.first->children) {
            q.push({ child, currLevel + 1 });
        }
    }

    // Return the difference
    return (oddSum - evenSum);
}

// Driver Code
int main()
{
    // Create the N-ary Tree
    Node* root = newNode(4);
    root->children.push_back(newNode(2));
    root->children.push_back(newNode(3));
    root->children.push_back(newNode(-5));
    root->children[0]->children.push_back(newNode(-1));
    root->children[0]->children.push_back(newNode(3));
    root->children[2]->children.push_back(newNode(-2));
    root->children[2]->children.push_back(newNode(6));

    cout << evenOddLevelDifference(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;

class GFG{

// Structure of a node
// of an n-ary tree
static class Node
{
    int val;
    ArrayList<Node> children;

    public Node(int val)
    {
        this.val = val;
        this.children = new ArrayList<Node>();
    }
};

static class Pair
{
    Node first;
    int second;

    public Pair(Node node, int val)
    {
        this.first = node;
        this.second = val;
    }
}

// Function to find the difference
// between of sums node values of
// odd and even levels in an N-ary tree
static int evenOddLevelDifference(Node root)
{

    // Store the sums of nodes at
    // even and odd levels
    int evenSum = 0, oddSum = 0;

    // Initialize a queue to store
    // pair of node and level
    Queue<Pair> q = new LinkedList<>();

    // Push the root into the
    // queue with level 1
    q.add(new Pair(root, 1));

    // Iterate all levels
    // of tree are traversed
    while (!q.isEmpty())
    {

        // Store the node at the
        // front of the queue
        Pair currNode = q.poll();

        // Store the current level
        int currLevel = currNode.second;

        // Store the current node value
        int currVal = currNode.first.val;

        // If current node
        // level is odd
        if (currLevel % 2 == 1)

            // Add to odd sum
            oddSum += currVal;
        else

            // Add to even sum
            evenSum += currVal;

        // Push all the children of current node
        // with increasing current level by 1
        for(Node child : currNode.first.children)
        {
            q.add(new Pair(child, currLevel + 1));
        }
    }

    // Return the difference
    return (oddSum - evenSum);
}

// Driver Code
public static void main(String[] args)
{

    // Create the N-ary Tree
    Node root = new Node(4);
    root.children.add(new Node(2));
    root.children.add(new Node(3));
    root.children.add(new Node(-5));
    root.children.get(0).children.add(new Node(-1));
    root.children.get(0).children.add(new Node(3));
    root.children.get(2).children.add(new Node(-2));
    root.children.get(2).children.add(new Node(6));

    System.out.println(evenOddLevelDifference(root));
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Structure of a node
# of an n-ary tree
class Node:

    def __init__(self, val):

        self.val = val
        self.children = []

# Function to create a
# new tree node
def newNode(val):

    temp = Node(val)

    return temp

# Function to find the difference
# between of sums node values of
# odd and even levels in an N-ary tree
def evenOddLevelDifference(root):

    # Store the sums of nodes at
    # even and odd levels
    evenSum = 0
    oddSum = 0

    # Initialize a queue to store
    # pair of node and level
    q = []

    # Push the root into the
    # queue with level 1
    q.append([root, 1])

    # Iterate all levels
    # of tree are traversed
    while (len(q) != 0):

        # Store the node at the
        # front of the queue
        currNode = q[0]

        # Pop the front node
        q.pop(0)

        # Store the current level
        currLevel = currNode[1]

        # Store the current node value
        currVal = currNode[0].val

        # If current node
        # level is odd
        if (currLevel % 2 != 0):

            # Add to odd sum
            oddSum += currVal
        else:

            # Add to even sum
            evenSum += currVal

        # Push all the children of current node
        # with increasing current level by 1
        for child in currNode[0].children:
            q.append([child, currLevel + 1])

    # Return the difference
    return (oddSum - evenSum)

# Driver code
if __name__=="__main__":

    # Create the N-ary Tree
    root = newNode(4)
    root.children.append(newNode(2))
    root.children.append(newNode(3))
    root.children.append(newNode(-5))
    root.children[0].children.append(newNode(-1))
    root.children[0].children.append(newNode(3))
    root.children[2].children.append(newNode(-2))
    root.children[2].children.append(newNode(6))

    print(evenOddLevelDifference(root))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Structure of a node
// of an n-ary tree
class Node
{
    public int val;
    public ArrayList children;

    public Node(int val)
    {
        this.val = val;
        this.children = new ArrayList();
    }
};

class Pair
{
    public Node first;
    public int second;

    public Pair(Node node, int val)
    {
        this.first = node;
        this.second = val;
    }
}

// Function to find the difference
// between of sums node values of
// odd and even levels in an N-ary tree
static int evenOddLevelDifference(Node root)
{

    // Store the sums of nodes at
    // even and odd levels
    int evenSum = 0, oddSum = 0;

    // Initialize a queue to store
    // pair of node and level
    Queue q = new Queue();

    // Push the root into the
    // queue with level 1
    q.Enqueue(new Pair(root, 1));

    // Iterate all levels
    // of tree are traversed
    while (q.Count != 0)
    {

        // Store the node at the
        // front of the queue
        Pair currNode = (Pair)q.Dequeue();

        // Store the current level
        int currLevel = currNode.second;

        // Store the current node value
        int currVal = currNode.first.val;

        // If current node
        // level is odd
        if (currLevel % 2 == 1)

            // Add to odd sum
            oddSum += currVal;
        else

            // Add to even sum
            evenSum += currVal;

        // Push all the children of current node
        // with increasing current level by 1
        foreach(Node child in currNode.first.children)
        {
            q.Enqueue(new Pair(child, currLevel + 1));
        }
    }

    // Return the difference
    return(oddSum - evenSum);
}

// Driver Code
public static void Main(string[] args)
{

    // Create the N-ary Tree
    Node root = new Node(4);
    root.children.Add(new Node(2));
    root.children.Add(new Node(3));
    root.children.Add(new Node(-5));

    ((Node)root.children[0]).children.Add(new Node(-1));
    ((Node)root.children[0]).children.Add(new Node(3));
    ((Node)root.children[2]).children.Add(new Node(-2));
    ((Node)root.children[2]).children.Add(new Node(6));

    Console.Write(evenOddLevelDifference(root));
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    // Structure of a node of an n-ary tree
    // Structure of a Tree Node
    class Node
    {
        constructor(val) {
           this.children = [];
           this.val = val;
        }
    }

    // Function to find the difference
    // between of sums node values of
    // odd and even levels in an N-ary tree
    function evenOddLevelDifference(root)
    {

        // Store the sums of nodes at
        // even and odd levels
        let evenSum = 0, oddSum = 0;

        // Initialize a queue to store
        // pair of node and level
        let q = [];

        // Push the root into the
        // queue with level 1
        q.push([root, 1]);

        // Iterate all levels
        // of tree are traversed
        while (q.length != 0)
        {

            // Store the node at the
            // front of the queue
            let currNode = q[0];
            q.shift();

            // Store the current level
            let currLevel = currNode[1];

            // Store the current node value
            let currVal = currNode[0].val;

            // If current node
            // level is odd
            if (currLevel % 2 == 1)

                // Add to odd sum
                oddSum += currVal;
            else

                // Add to even sum
                evenSum += currVal;

            // Push all the children of current node
            // with increasing current level by 1
            for(let child = 0; child < (currNode[0].children).length;
            child++)
            {
                q.push([currNode[0].children[child], currLevel + 1]);
            }
        }

        // Return the difference
        return(oddSum - evenSum);
    }

    // Create the N-ary Tree
    let root = new Node(4);
    root.children.push(new Node(2));
    root.children.push(new Node(3));
    root.children.push(new Node(-5));

    (root.children[0]).children.push(new Node(-1));
    (root.children[0]).children.push(new Node(3));
    (root.children[2]).children.push(new Node(-2));
    (root.children[2]).children.push(new Node(6));

    document.write(evenOddLevelDifference(root));

</script>
```

**Output:** 

```
10
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)