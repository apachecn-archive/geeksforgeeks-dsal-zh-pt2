# 二叉树中的重复子树| SET 2

> 原文:[https://www . geeksforgeeks . org/duplicate-二叉树中的子树-set-2/](https://www.geeksforgeeks.org/duplicate-subtree-in-binary-tree-set-2/)

给定一棵二叉树，任务是检查二叉树是否包含大小为 2 或更大的重复子树。

```
Input:
               A
             /   \ 
           B       C
         /   \       \    
        D     E       B     
                     /  \    
                    D    E
Output: Yes
    B     
  /   \    
 D     E
is the duplicate sub-tree.

Input:
               A
             /   \ 
           B       C
         /   \
        D     E
Output: No
```

**方法:**已经讨论了基于 DFS 的方法[这里](https://www.geeksforgeeks.org/check-binary-tree-contains-duplicate-subtrees-size-2/)。可以使用[队列](https://www.geeksforgeeks.org/queue-data-structure/)以 [bfs](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 的方式遍历树。遍历节点时，将节点及其左、右子节点推送到地图中，如果地图中的任何一点包含重复，则该树包含重复的子树。例如，如果节点是 A，其子节点是 B 和 C，那么 ABC 将被推送到地图上。如果在任何时候，必须再次推送作业成本法，则该树包含重复的子树。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Structure for a binary tree node
struct Node {
    char key;
    Node *left, *right;
};

// A utility function to create a new node
Node* newNode(char key)
{
    Node* node = new Node;
    node->key = key;
    node->left = node->right = NULL;
    return node;
}

unordered_set<string> subtrees;

// Function that returns true if
// tree contains a duplicate subtree
// of size 2 or more
bool dupSubUtil(Node* root)
{

    // To store subtrees
    set<string> subtrees;

    // Used to traverse tree
    queue<Node*> bfs;
    bfs.push(root);

    while (!bfs.empty()) {
        Node* n = bfs.front();
        bfs.pop();

        // To store the left and the right
        // children of the current node
        char l = ' ', r = ' ';

        // If the node has a left child
        if (n->left != NULL) {
            l = n->left->key;

            // Push left node's data
            bfs.push(n->left);
        }

        // If the node has a right child
        if (n->right != NULL) {
            r = n->right->key;

            // Push right node's data
            bfs.push(n->right);
        }

        string subt;
        subt += n->key;
        subt += l;
        subt += r;

        if (l != ' ' || r != ' ') {

            // If this subtree count is greater than 0
            // that means duplicate exists
            if (!subtrees.insert(subt).second) {
                return true;
            }
        }
    }
    return false;
}

// Driver code
int main()
{
    Node* root = newNode('A');
    root->left = newNode('B');
    root->right = newNode('C');
    root->left->left = newNode('D');
    root->left->right = newNode('E');
    root->right->right = newNode('B');
    root->right->right->right = newNode('E');
    root->right->right->left = newNode('D');

    cout << (dupSubUtil(root) ? "Yes" : "No");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// Structure for a binary tree node
static class Node
{
    char key;
    Node left, right;
};

// A utility function to create a new node
static Node newNode(char key)
{
    Node node = new Node();
    node.key = key;
    node.left = node.right = null;
    return node;
}

static HashSet<String> subtrees = new HashSet<String>();

// Function that returns true if
// tree contains a duplicate subtree
// of size 2 or more
static boolean dupSubUtil(Node root)
{

    // To store subtrees
    // HashSet<String> subtrees;

    // Used to traverse tree
    Queue<Node> bfs = new LinkedList<>();
    bfs.add(root);

    while (!bfs.isEmpty())
    {
        Node n = bfs.peek();
        bfs.remove();

        // To store the left and the right
        // children of the current node
        char l = ' ', r = ' ';

        // If the node has a left child
        if (n.left != null)
        {
            l = n.left.key;

            // Push left node's data
            bfs.add(n.left);
        }

        // If the node has a right child
        if (n.right != null)
        {
            r = n.right.key;

            // Push right node's data
            bfs.add(n.right);
        }

        String subt = "";
        subt += n.key;
        subt += l;
        subt += r;

        if (l != ' ' || r != ' ')
        {

            // If this subtree count is greater than 0
            // that means duplicate exists
            if (!subtrees.contains(subt))
            {
                return true;
            }
        }
    }
    return false;
}

// Driver code
public static void main(String[] args)
{
    Node root = newNode('A');
    root.left = newNode('B');
    root.right = newNode('C');
    root.left.left = newNode('D');
    root.left.right = newNode('E');
    root.right.right = newNode('B');
    root.right.right.right = newNode('E');
    root.right.right.left = newNode('D');
    if (dupSubUtil(root))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Structure for a binary tree node
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.key = data
        self.left = None
        self.right = None

subtrees = set()

# Function that returns true if
# tree contains a duplicate subtree
# of size 2 or more
def dupSubUtil(root):

    # To store subtrees
    subtrees= set()

    # Used to traverse tree
    bfs = []
    bfs.append(root)
    while (len(bfs)):
        n = bfs[0]
        bfs.pop(0)

        # To store the left and the right
        # children of the current node
        l = ' '
        r = ' '

        # If the node has a left child
        if (n.left != None):
            x = n.left
            l = x.key

            # append left node's data
            bfs.append(n.left)

        # If the node has a right child
        if (n.right != None):
            x = n.right
            r = x.key

            # append right node's data
            bfs.append(n.right)

        subt=""
        subt += n.key
        subt += l
        subt += r

        if (l != ' ' or r != ' '):

            # If this subtree count is greater than 0
            # that means duplicate exists
            subtrees.add(subt)
            if (len(subtrees) > 1):
                return True

    return False

# Driver code

root = newNode('A')
root.left = newNode('B')
root.right = newNode('C')
root.left.left = newNode('D')
root.left.right = newNode('E')
root.right.right = newNode('B')
root.right.right.right = newNode('E')
root.right.right.left = newNode('D')

if dupSubUtil(root):
    print("Yes")
else:
    print("No")

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Structure for a binary tree node
public class Node
{
    public char key;
    public Node left, right;
};

// A utility function to create a new node
static Node newNode(char key)
{
    Node node = new Node();
    node.key = key;
    node.left = node.right = null;
    return node;
}

static HashSet<String> subtrees = new HashSet<String>();

// Function that returns true if
// tree contains a duplicate subtree
// of size 2 or more
static bool dupSubUtil(Node root)
{

    // To store subtrees
    // HashSet<String> subtrees;

    // Used to traverse tree
    Queue<Node> bfs = new Queue<Node>();
    bfs.Enqueue(root);

    while (bfs.Count != 0)
    {
        Node n = bfs.Peek();
        bfs.Dequeue();

        // To store the left and the right
        // children of the current node
        char l = ' ', r = ' ';

        // If the node has a left child
        if (n.left != null)
        {
            l = n.left.key;

            // Push left node's data
            bfs.Enqueue(n.left);
        }

        // If the node has a right child
        if (n.right != null)
        {
            r = n.right.key;

            // Push right node's data
            bfs.Enqueue(n.right);
        }

        String subt = "";
        subt += n.key;
        subt += l;
        subt += r;

        if (l != ' ' || r != ' ')
        {

            // If this subtree count is greater than 0
            // that means duplicate exists
            if (!subtrees.Contains(subt))
            {
                return true;
            }
        }
    }
    return false;
}

// Driver code
public static void Main(String[] args)
{
    Node root = newNode('A');
    root.left = newNode('B');
    root.right = newNode('C');
    root.left.left = newNode('D');
    root.left.right = newNode('E');
    root.right.right = newNode('B');
    root.right.right.right = newNode('E');
    root.right.right.left = newNode('D');
    if (dupSubUtil(root))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Structure for a binary tree node
class Node
{
    constructor()
    {
        this.key = '';
        this.left = null;
        this.right = null;
    }
};

// A utility function to create a new node
function newNode(key)
{
    var node = new Node();
    node.key = key;
    node.left = node.right = null;
    return node;
}

var subtrees = new Set();

// Function that returns true if
// tree contains a duplicate subtree
// of size 2 or more
function dupSubUtil(root)
{

    // To store subtrees
    // HashSet<String> subtrees;

    // Used to traverse tree
    var bfs = [];
    bfs.push(root);

    while (bfs.length != 0)
    {
        var n = bfs[0];
        bfs.pop();

        // To store the left and the right
        // children of the current node
        var l = ' ', r = ' ';

        // If the node has a left child
        if (n.left != null)
        {
            l = n.left.key;

            // Push left node's data
            bfs.push(n.left);
        }

        // If the node has a right child
        if (n.right != null)
        {
            r = n.right.key;

            // Push right node's data
            bfs.push(n.right);
        }

        var subt = "";
        subt += n.key;
        subt += l;
        subt += r;

        if (l != ' ' || r != ' ')
        {

            // If this subtree count is greater than 0
            // that means duplicate exists
            if (!subtrees.has(subt))
            {
                return true;
            }
        }
    }
    return false;
}

// Driver code
var root = newNode('A');
root.left = newNode('B');
root.right = newNode('C');
root.left.left = newNode('D');
root.left.right = newNode('E');
root.right.right = newNode('B');
root.right.right.right = newNode('E');
root.right.right.left = newNode('D');
if (dupSubUtil(root))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
Yes
```