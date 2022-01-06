# 树中从根到给定节点的路径中与给定值的最大异或

> 原文:[https://www . geeksforgeeks . org/从根到树中给定节点的路径中给定值最大异或/](https://www.geeksforgeeks.org/maximum-xor-with-given-value-in-the-path-from-root-to-given-node-in-the-tree/)

给定一棵树，该树具有来自范围**【1，N】**的不同节点和两个整数 **x** 和**值**。任务是在从**根**到**值**的路径上用 **x** 异或时，求任意节点的最大值。

**示例:**

```
Input: val = 6, x = 4
    1
   / \
  2   3
 /     \
4       5
       /
      6
Output: 7
the path is 1 -> 3 -> 5 -> 6
1 ^ 4 = 5
3 ^ 4 = 7
5 ^ 4 = 1
6 ^ 4 = 2
Maximum is 7

Input: val = 4, x = 1
    1
   / \
  2   3
 /     
4    
Output: 5
```

**进场:**

*   这个问题的优化解决方案是创建一个父数组来存储每个节点的父节点。
*   从给定的节点开始，继续使用父数组在树中向上(这在回答许多查询时会很有帮助，因为只有路径上的节点会被遍历)。对路径中的所有节点进行 x 的异或运算，直到根。
*   为路径计算的最大异或就是答案。

下面是上述方法的实现:

## C++14

```
// CPP implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Tree node
class Node
{
public:
    int data;
    Node *left, *right;

    Node(int data)
    {
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};

// Recursive function to update
// the parent array such that parent[i]
// stores the parent of i
void updateParent(int *parent, Node *node)
{
    // If node is null then return
    if (node == NULL)
        return;

    // If left child of the node is not
    // null then set node as the parent
    // of its left child
    if (node->left != NULL)
        parent[node->left->data] = node->data;

    // If right child of the node is not
    // null then set node as the parent
    // of its right child
    if (node->right != NULL)
        parent[node->right->data] = node->data;

    // Recursive call for the
    // children of current node
    updateParent(parent, node->left);
    updateParent(parent, node->right);
}

// Function to return the maximum value
// of a node on the path from root to val
// when Xored with x
int getMaxXor(Node *root, int n, int val, int x)
{
    // Create the parent array
    int *parent = new int[n + 1];
    updateParent(parent, root);

    // Initialize max with x XOR val
    int maximum = x ^ val;

    // Get to the parent of val
    val = parent[val];

    // 0 is the parent of the root
    while (val != 0)
    {
        // Update maximum
        maximum = max(maximum, x ^ val);

        // Get one level up the tree
        val = parent[val];
    }
    return maximum;
}

// Driver Code
int main()
{
    int n = 6;
    Node *root;
    root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->right->right = new Node(5);
    root->right->right->left = new Node(6);

    int val = 6, x = 4;
    cout << getMaxXor(root, n, val, x) << endl;

    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Tree node
    static class Node {
        int data;
        Node left, right;
        Node(int data)
        {
            this.data = data;
            left = null;
            right = null;
        }
    }

    // Recursive function to update
    // the parent array such that parent[i]
    // stores the parent of i
    static void updateParent(int parent[],
                             Node node)
    {

        // If node is null then return
        if (node == null)
            return;

        // If left child of the node is not
        // null then set node as the parent
        // of its left child
        if (node.left != null)
            parent[node.left.data] = node.data;

        // If right child of the node is not
        // null then set node as the parent
        // of its right child
        if (node.right != null)
            parent[node.right.data] = node.data;

        // Recursive call for the
        // children of current node
        updateParent(parent, node.left);
        updateParent(parent, node.right);
    }

    // Function to return the maximum value
    // of a node on the path from root to val
    // when Xored with x
    static int getMaxXor(Node root,
                         int n, int val, int x)
    {

        // Create the parent array
        int parent[] = new int[n + 1];
        updateParent(parent, root);

        // Initialize max with x XOR val
        int max = x ^ val;

        // Get to the parent of val
        val = parent[val];

        // 0 is the parent of the root
        while (val != 0) {

            // Update maximum
            max = Math.max(max, x ^ val);

            // Get one level up the tree
            val = parent[val];
        }
        return max;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 6;
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.right.right = new Node(5);
        root.right.right.left = new Node(6);

        int val = 6, x = 4;
        System.out.println(getMaxXor(root, n, val, x));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Tree node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Recursive function to update
# the parent array such that parent[i]
# stores the parent of i
def updateParent(parent, node):

    # If node is None then return
    if (node == None):
        return parent

    # If left child of the node is not
    # None then set node as the parent
    # of its left child
    if (node.left != None):
        parent[node.left.data] = node.data

    # If right child of the node is not
    # None then set node as the parent
    # of its right child
    if (node.right != None):
        parent[node.right.data] = node.data

    # Recursive call for the
    # children of current node
    parent = updateParent(parent, node.left)
    parent = updateParent(parent, node.right)
    return parent

# Function to return the maximum value
# of a node on the path from root to val
# when Xored with x
def getMaxXor(root, n, val, x):

    # Create the parent array
    parent = [0]*(n + 1)
    parent=updateParent(parent, root)

    # Initialize max with x XOR val
    maximum = x ^ val

    # Get to the parent of val
    val = parent[val]

    # 0 is the parent of the root
    while (val != 0):

        # Update maximum
        maximum = max(maximum, x ^ val)

        # Get one level up the tree
        val = parent[val]

    return maximum

# Driver Code
n = 6

root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.right.right = Node(5)
root.right.right.left = Node(6)

val = 6
x = 4
print( getMaxXor(root, n, val, x) )

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Tree node
    public class Node
    {
        public int data;
        public Node left, right;
        public Node(int data)
        {
            this.data = data;
            left = null;
            right = null;
        }
    }

    // Recursive function to update
    // the parent array such that parent[i]
    // stores the parent of i
    static void updateParent(int []parent,
                             Node node)
    {

        // If node is null then return
        if (node == null)
            return;

        // If left child of the node is not
        // null then set node as the parent
        // of its left child
        if (node.left != null)
            parent[node.left.data] = node.data;

        // If right child of the node is not
        // null then set node as the parent
        // of its right child
        if (node.right != null)
            parent[node.right.data] = node.data;

        // Recursive call for the
        // children of current node
        updateParent(parent, node.left);
        updateParent(parent, node.right);
    }

    // Function to return the maximum value
    // of a node on the path from root to val
    // when Xored with x
    static int getMaxXor(Node root, int n,
                         int val, int x)
    {

        // Create the parent array
        int []parent = new int[n + 1];
        updateParent(parent, root);

        // Initialize max with x XOR val
        int max = x ^ val;

        // Get to the parent of val
        val = parent[val];

        // 0 is the parent of the root
        while (val != 0)
        {

            // Update maximum
            max = Math.Max(max, x ^ val);

            // Get one level up the tree
            val = parent[val];
        }
        return max;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 6;
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.right.right = new Node(5);
        root.right.right.left = new Node(6);

        int val = 6, x = 4;
        Console.WriteLine(getMaxXor(root, n, val, x));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Tree node
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

// Recursive function to update
// the parent array such that parent[i]
// stores the parent of i
function updateParent(parent, node)
{

    // If node is null then return
    if (node == null)
        return;

    // If left child of the node is not
    // null then set node as the parent
    // of its left child
    if (node.left != null)
        parent[node.left.data] = node.data;

    // If right child of the node is not
    // null then set node as the parent
    // of its right child
    if (node.right != null)
        parent[node.right.data] = node.data;

    // Recursive call for the
    // children of current node
    updateParent(parent, node.left);
    updateParent(parent, node.right);
}

// Function to return the maximum value
// of a node on the path from root to val
// when Xored with x
function getMaxXor(root, n, val, x)
{

    // Create the parent array
    let parent = new Array(n + 1);
    parent.fill(0);
    updateParent(parent, root);

    // Initialize max with x XOR val
    let max = x ^ val;

    // Get to the parent of val
    val = parent[val];

    // 0 is the parent of the root
    while (val != 0)
    {

        // Update maximum
        max = Math.max(max, x ^ val);

        // Get one level up the tree
        val = parent[val];
    }
    return max;
}

// Driver code
let n = 6;
let root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.right.right = new Node(5);
root.right.right.left = new Node(6);

let val = 6, x = 4;
document.write(getMaxXor(root, n, val, x));

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
7
```

**时间复杂度:** O(N)