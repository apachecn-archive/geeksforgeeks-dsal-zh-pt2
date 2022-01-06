# 查找二叉查找树中重复节点的最大数量

> 原文:[https://www . geesforgeks . org/find-二进制搜索树中重复节点的最大数量/](https://www.geeksforgeeks.org/find-maximum-count-of-duplicate-nodes-in-a-binary-search-tree/)

给定一个有重复项的二叉查找树(BST)，在给定的 BST 中找到节点(最常出现的元素)。如果 BST 包含两个或更多这样的节点，请打印其中任何一个。
**注意:**我们不能使用任何额外的空间。(假设递归产生的隐式堆栈空间不计算在内)
假设 BST 定义如下:

*   节点的左子树仅包含键小于或等于节点键的节点。
*   节点的右子树仅包含键大于或等于节点键的节点。
*   左右子树都必须是二分搜索法树。

**例:**

```
Input :   Given BST is

                    6
                 /    \
                5       7
              /   \    /  \
             4     5  7    7
Output : 7 

Input :  Given BST is

                    10
                 /    \
                5       12
              /   \    /  \
             5     6  12    16
Output : 5 or 12 
We can print any of the two value 5 or 12.
```

**方法:**
要找到节点，我们需要找到 BST 的 order 遍历，因为它的 order 遍历将按排序顺序进行。
所以，想法是做递归的 Inorder 遍历，保持对前一个节点的跟踪。如果当前节点值等于前一个值，我们可以增加当前计数，如果当前计数大于最大计数，则替换元素。
以下是上述方法的实施:

## C++

```
/* C++ program to find the median of BST in O(n)
   time and O(1) space*/

#include <iostream>
using namespace std;

/* A binary search tree Node has data, pointer
   to left child and a pointer to right child */

struct Node {
    int val;
    struct Node *left, *right;
};

struct Node* newNode(int data)
{
    struct Node* temp = new Node;
    temp->val = data;
    temp->left = temp->right = NULL;
    return temp;
}

// cur for storing the current count of the value
// and mx for the maximum count of the element which is denoted by node

int cur = 1, mx = 0;
int node;
struct Node* previous = NULL;

// Find the inorder traversal of the BST
void inorder(struct Node* root)
{
    // If root is NULL then return
    if (root == NULL) {
        return;
    }
    inorder(root->left);
    if (previous != NULL) {
        // If the previous value is equal to the current value
        // then increase the count
        if (root->val == previous->val) {
            cur++;
        }
        // Else initialize the count by 1
        else {
            cur = 1;
        }
    }
    // If current count is greater than the max count
    // then update the mx value
    if (cur > mx) {
        mx = cur;
        node = root->val;
    }
    // Make the current Node as previous
    previous = root;
    inorder(root->right);
}

// Utility function
int findnode(struct Node* root)
{
    inorder(root);
    return node;
}
int main()
{
    /* Let us create following BST
                   6
                 /    \
                5       7
              /   \    /  \
             4     5  7    7
    */

    struct Node* root = newNode(6);
    root->left = newNode(5);
    root->right = newNode(7);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(7);
    root->right->right = newNode(7);

    cout << "Node of BST is " << findnode(root) << '\n';
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to find the median of BST
in O(n) time and O(1) space*/
class GFG
{

/* A binary search tree Node has data, pointer
to left child and a pointer to right child */
static class Node
{
    int val;
    Node left, right;
};

static Node newNode(int data)
{
    Node temp = new Node();
    temp.val = data;
    temp.left = temp.right = null;
    return temp;
}

// cur for storing the current count
// of the value and mx for the maximum count
// of the element which is denoted by node
static int cur = 1, mx = 0;
static int node;
static Node previous = null;

// Find the inorder traversal of the BST
static void inorder(Node root)
{
    // If root is null then return
    if (root == null)
    {
        return;
    }
    inorder(root.left);
    if (previous != null)
    {

        // If the previous value is equal to
        // the current value then increase the count
        if (root.val == previous.val)
        {
            cur++;
        }

        // Else initialize the count by 1
        else
        {
            cur = 1;
        }
    }

    // If current count is greater than the
    // max count then update the mx value
    if (cur > mx)
    {
        mx = cur;
        node = root.val;
    }

    // Make the current Node as previous
    previous = root;
    inorder(root.right);
}

// Utility function
static int findnode(Node root)
{
    inorder(root);
    return node;
}

// Java Code
public static void main(String args[])
{
    /* Let us create following BST
                6
                / \
                5     7
            / \ / \
            4     5 7 7
    */
    Node root = newNode(6);
    root.left = newNode(5);
    root.right = newNode(7);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(7);
    root.right.right = newNode(7);

    System.out.println("Node of BST is " +
                          findnode(root));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python program to find the median of BST
# in O(n) time and O(1) space

# A binary search tree Node has data, pointer
# to left child and a pointer to right child
class Node:
    def __init__(self):
        self.val = 0
        self.left = None
        self.right = None

def newNode(data: int) -> Node:
    temp = Node()
    temp.val = data
    temp.left = temp.right = None
    return temp

# cur for storing the current count
# of the value and mx for the maximum count
# of the element which is denoted by node
cur = 1
mx = 0
node = 0
previous = Node()

# Find the inorder traversal of the BST
def inorder(root: Node):
    global cur, mx, node, previous

    # If root is null then return
    if root is None:
        return

    inorder(root.left)

    if previous is not None:

        # If the previous value is equal to
        # the current value then increase the count
        if root.val == previous.val:
            cur += 1

        # Else initialize the count by 1
        else:
            cur = 1

    # If current count is greater than the
    # max count then update the mx value
    if cur > mx:
        mx = cur
        node = root.val

    # Make the current Node as previous
    previous = root
    inorder(root.right)

# Utility function
def findNode(root: Node) -> int:
    global node

    inorder(root)
    return node

# Driver Code
if __name__ == "__main__":
    # Let us create following BST
    #         6
    #         / \
    #     5     7
    #     / \ / \
    #     4 5 7 7
    root = newNode(6)
    root.left = newNode(5)
    root.right = newNode(7)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.left = newNode(7)
    root.right.right = newNode(7)

    print("Node of BST is", findNode(root))

# This code is contributed by
# sanjeev2552
```

## C#

```
/* C# program to find the median of BST
in O(n) time and O(1) space*/
using System;

class GFG
{

/* A binary search tree Node has data, pointer
to left child and a pointer to right child */
public class Node
{
    public int val;
    public Node left, right;
};

static Node newNode(int data)
{
    Node temp = new Node();
    temp.val = data;
    temp.left = temp.right = null;
    return temp;
}

// cur for storing the current count
// of the value and mx for the maximum count
// of the element which is denoted by node
static int cur = 1, mx = 0;
static int node;
static Node previous = null;

// Find the inorder traversal of the BST
static void inorder(Node root)
{
    // If root is null then return
    if (root == null)
    {
        return;
    }
    inorder(root.left);
    if (previous != null)
    {

        // If the previous value is equal to
        // the current value then increase the count
        if (root.val == previous.val)
        {
            cur++;
        }

        // Else initialize the count by 1
        else
        {
            cur = 1;
        }
    }

    // If current count is greater than the
    // max count then update the mx value
    if (cur > mx)
    {
        mx = cur;
        node = root.val;
    }

    // Make the current Node as previous
    previous = root;
    inorder(root.right);
}

// Utility function
static int findnode(Node root)
{
    inorder(root);
    return node;
}

// Driver Code
public static void Main(String []args)
{
    /* Let us create following BST
                6
                / \
                5     7
            / \ / \
            4     5 7 7
    */
    Node root = newNode(6);
    root.left = newNode(5);
    root.right = newNode(7);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(7);
    root.right.right = newNode(7);

    Console.WriteLine("Node of BST is " +
                         findnode(root));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

/* Javascript program to find the median of BST
in O(n) time and O(1) space*/

/* A binary search tree Node has data, pointer
to left child and a pointer to right child */
class Node
{
    constructor()
    {
        this.val = 0;
        this.left = null;
        this.right = null;
    }
};

function newNode(data)
{
    var temp = new Node();
    temp.val = data;
    temp.left = temp.right = null;
    return temp;
}

// cur for storing the current count
// of the value and mx for the maximum count
// of the element which is denoted by node
var cur = 1, mx = 0;
var node;
var previous = null;

// Find the inorder traversal of the BST
function inorder(root)
{
    // If root is null then return
    if (root == null)
    {
        return;
    }
    inorder(root.left);
    if (previous != null)
    {

        // If the previous value is equal to
        // the current value then increase the count
        if (root.val == previous.val)
        {
            cur++;
        }

        // Else initialize the count by 1
        else
        {
            cur = 1;
        }
    }

    // If current count is greater than the
    // max count then update the mx value
    if (cur > mx)
    {
        mx = cur;
        node = root.val;
    }

    // Make the current Node as previous
    previous = root;
    inorder(root.right);
}

// Utility function
function findnode(root)
{
    inorder(root);
    return node;
}

// Driver Code
/* Let us create following BST
            6
            / \
            5     7
        / \ / \
        4     5 7 7
*/
var root = newNode(6);
root.left = newNode(5);
root.right = newNode(7);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.right.left = newNode(7);
root.right.right = newNode(7);
document.write("Node of BST is " +
                     findnode(root));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
node of BST is 7
```

**时间复杂度:** ![O(N)    ](img/f60d48dc419b1d7a2754ba98e43e1b1a.png "Rendered by QuickLaTeX.com")
**辅助空间** : O(N)。