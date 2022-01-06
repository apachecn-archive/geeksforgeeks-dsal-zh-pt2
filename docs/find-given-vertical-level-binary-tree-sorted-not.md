# 查找给定的二叉树垂直层次是否排序

> 原文:[https://www . geesforgeks . org/find-给定-垂直-级别-二叉树-排序-非/](https://www.geeksforgeeks.org/find-given-vertical-level-binary-tree-sorted-not/)

给定一棵二叉树。查找二叉树的给定垂直层次是否排序。
(对于两个节点重叠的情况，检查它们是否在其所在的级别形成排序序列。)
**先决条件:** [垂直顺序遍历](https://www.geeksforgeeks.org/print-a-binary-tree-in-vertical-order-set-3-using-level-order-traversal/)

示例:

```
Input : 1
       / \
      2   5
     / \
    7   4
       /
      6
   Level l = -1   
Output : Yes
Nodes in level -1 are 2 -> 6 which
forms a sorted sequence.

Input: 1
        / \
       2   6
        \ /
        3 4
   Level l = 0
Output : Yes
Note that nodes with value 3 and 4
are overlapping in the binary tree.
So we check if this form a sorted
sequence level wise. The sequence formed
at level 0 is 1 -> 3 -> 4 which is sorted.  
```

[Recommended : Please try your approach first on IDE and then look at the solution.](https://ide.geeksforgeeks.org)

一个**简单的**解决方案是先做二叉树的层级顺序遍历，将每个垂直层级存储在不同的数组中。检查之后，对应于 l 级的数组是否排序。这种解决方案对内存的需求很大，可以减少。

一种**高效的**解决方案是对二叉树进行垂直层次顺序遍历，并跟踪二叉树垂直层次 l 中的节点值。如果前一个元素小于或等于当前元素，则会对序列进行排序。执行垂直级别顺序遍历时，存储上一个值，并将垂直级别 l 中的当前节点与级别 l 的该上一个值进行比较。如果当前节点值大于或等于上一个值，则重复相同的过程，直到级别 l 结束。如果在任何阶段当前节点值小于上一个值，则级别 l 不排序。如果我们到达 l 层的末端，那么该层被排序。

**实施:**

## C++

```
// CPP program to determine whether
// vertical level l of binary tree
// is sorted or not.
#include <bits/stdc++.h>
using namespace std;

// Structure of a tree node.
struct Node {
    int key;
    Node *left, *right;
};

// Function to create new tree node.
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return temp;
}

// Helper function to determine if
// vertical level l of given binary
// tree is sorted or not.
bool isSorted(Node* root, int level)
{
    // If root is null, then the answer is an
    // empty subset and an empty subset is
    // always considered to be sorted.
    if (root == NULL)
        return true;

    // Variable to store previous
    // value in vertical level l.
    int prevVal = INT_MIN;

    // Variable to store current level
    // while traversing tree vertically.
    int currLevel;

    // Variable to store current node
    // while traversing tree vertically.
    Node* currNode;

    // Declare queue to do vertical order
    // traversal. A pair is used as element
    // of queue. The first element in pair
    // represents the node and the second
    // element represents vertical level
    // of that node.
    queue<pair<Node*, int> > q;

    // Insert root in queue. Vertical level
    // of root is 0.
    q.push(make_pair(root, 0));

    // Do vertical order traversal until
    // all the nodes are not visited.
    while (!q.empty()) {
        currNode = q.front().first;
        currLevel = q.front().second;
        q.pop();

        // Check if level of node extracted from
        // queue is required level or not. If it
        // is the required level then check if
        // previous value in that level is less
        // than or equal to value of node.
        if (currLevel == level) {
            if (prevVal <= currNode->key)
                prevVal = currNode->key;           
            else
                return false;           
        }

        // If left child is not NULL then push it
        // in queue with level reduced by 1.
        if (currNode->left)
            q.push(make_pair(currNode->left, currLevel - 1));

        // If right child is not NULL then push it
        // in queue with level increased by 1.
        if (currNode->right)
            q.push(make_pair(currNode->right, currLevel + 1));
    }

    // If the level asked is not present in the
    // given binary tree, that means that level
    // will contain an empty subset. Therefore answer
    // will be true.
    return true;
}

// Driver program
int main()
{
    /*
             1
            / \
           2   5
          / \
         7   4
            /
           6
    */

    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(5);
    root->left->left = newNode(7);
    root->left->right = newNode(4);
    root->left->right->left = newNode(6);

    int level = -1;
    if (isSorted(root, level) == true)
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## 蟒蛇 3

```
# Python program to determine whether
# vertical level l of binary tree
# is sorted or not.
from collections import deque
from sys import maxsize

INT_MIN = -maxsize

# Structure of a tree node.
class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# Helper function to determine if
# vertical level l of given binary
# tree is sorted or not.
def isSorted(root: Node, level: int) -> bool:

    # If root is null, then the answer is an
    # empty subset and an empty subset is
    # always considered to be sorted.
    if root is None:
        return True

    # Variable to store previous
    # value in vertical level l.
    prevVal = INT_MIN

    # Variable to store current level
    # while traversing tree vertically.
    currLevel = 0

    # Variable to store current node
    # while traversing tree vertically.
    currNode = Node(0)

    # Declare queue to do vertical order
    # traversal. A pair is used as element
    # of queue. The first element in pair
    # represents the node and the second
    # element represents vertical level
    # of that node.
    q = deque()

    # Insert root in queue. Vertical level
    # of root is 0.
    q.append((root, 0))

    # Do vertical order traversal until
    # all the nodes are not visited.
    while q:
        currNode = q[0][0]
        currLevel = q[0][1]
        q.popleft()

        # Check if level of node extracted from
        # queue is required level or not. If it
        # is the required level then check if
        # previous value in that level is less
        # than or equal to value of node.
        if currLevel == level:
            if prevVal <= currNode.key:
                prevVal = currNode.key
            else:
                return False

        # If left child is not NULL then push it
        # in queue with level reduced by 1.
        if currNode.left:
            q.append((currNode.left, currLevel - 1))

        # If right child is not NULL then push it
        # in queue with level increased by 1.
        if currNode.right:
            q.append((currNode.right, currLevel + 1))

    # If the level asked is not present in the
    # given binary tree, that means that level
    # will contain an empty subset. Therefore answer
    # will be true.
    return True

# Driver Code
if __name__ == "__main__":

    # /*
    #         1
    #         / \
    #     2 5
    #     / \
    #     7 4
    #         /
    #     6
    # */

    root = Node(1)
    root.left = Node(2)
    root.right = Node(5)
    root.left.left = Node(7)
    root.left.right = Node(4)
    root.left.right.left = Node(6)

    level = -1
    if isSorted(root, level):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# sanjeev2552
```

## java 描述语言

```
<script>

// Javascript program to determine whether
// vertical level l of binary tree
// is sorted or not.
class Node
{
    constructor(key)
    {
        this.left = null;
        this.right = null;
        this.key = key;
    }
}

// Function to create new tree node.
function newNode(key)
{
    let temp = new Node(key);
    return temp;
}

// Helper function to determine if
// vertical level l of given binary
// tree is sorted or not.
function isSorted(root, level)
{

    // If root is null, then the answer is an
    // empty subset and an empty subset is
    // always considered to be sorted.
    if (root == null)
        return true;

    // Variable to store previous
    // value in vertical level l.
    let prevVal = Number.MIN_VALUE;

    // Variable to store current level
    // while traversing tree vertically.
    let currLevel;

    // Variable to store current node
    // while traversing tree vertically.
    let currNode;

    // Declare queue to do vertical order
    // traversal. A pair is used as element
    // of queue. The first element in pair
    // represents the node and the second
    // element represents vertical level
    // of that node.
    let q = [];

    // Insert root in queue. Vertical level
    // of root is 0.
    q.push([root, 0]);

    // Do vertical order traversal until
    // all the nodes are not visited.
    while (q.length > 0)
    {
        currNode = q[0][0];
        currLevel = q[0][1];
        q.shift();

        // Check if level of node extracted from
        // queue is required level or not. If it
        // is the required level then check if
        // previous value in that level is less
        // than or equal to value of node.
        if (currLevel == level)
        {
            if (prevVal <= currNode.key)
                prevVal = currNode.key;           
            else
                return false;           
        }

        // If left child is not NULL then push it
        // in queue with level reduced by 1.
        if (currNode.left)
            q.push([currNode.left, currLevel - 1]);

        // If right child is not NULL then push it
        // in queue with level increased by 1.
        if (currNode.right)
            q.push([currNode.right, currLevel + 1]);
    }

    // If the level asked is not present in the
    // given binary tree, that means that level
    // will contain an empty subset. Therefore answer
    // will be true.
    return true;
}

// Driver code
/*
         1
        / \
       2   5
      / \
     7   4
        /
       6
*/
let root = newNode(1);
root.left = newNode(2);
root.right = newNode(5);
root.left.left = newNode(7);
root.left.right = newNode(4);
root.left.right.left = newNode(6);

let level = -1;
if (isSorted(root, level) == true)
    document.write("Yes");
else
    document.write("No");

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)