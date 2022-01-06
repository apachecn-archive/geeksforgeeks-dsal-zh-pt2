# 删除值为 x 的叶节点

> 原文:[https://www.geeksforgeeks.org/delete-leaf-nodes-value-x/](https://www.geeksforgeeks.org/delete-leaf-nodes-value-x/)

给定一棵二叉树和一个目标整数 x，删除所有值为 x 的叶节点。另外，删除新形成的目标值为 x 的叶。
**例:**

```
Input : x = 5  
            6
         /     \
        5       4
      /   \       \
     1     2       5 
Output : 
            6
         /     \
        5       4
      /   \  
     1     2 
Inorder Traversal is 1 5 2 6 4
```

来源:[微软访谈](https://www.geeksforgeeks.org/microsoft-interview-experience-set-122-off-campus/)
我们以后置的方式遍历树，递归删除节点。方法和[这个](https://www.geeksforgeeks.org/remove-all-nodes-which-lie-on-a-path-having-sum-less-than-k/)和[这个](https://www.geeksforgeeks.org/remove-nodes-root-leaf-paths-length-k/)问题很相似。

## C++

```
// CPP code to delete all leaves with given
// value.
#include <bits/stdc++.h>
using namespace std;

// A binary tree node
struct Node {
    int data;
    struct Node *left, *right;
};

// A utility function to allocate a new node
struct Node* newNode(int data)
{
    struct Node* newNode = new Node;
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return (newNode);
}

Node* deleteLeaves(Node* root, int x)
{
    if (root == NULL)
        return nullptr;
    root->left = deleteLeaves(root->left, x);
    root->right = deleteLeaves(root->right, x);

    if (root->data == x && root->left == NULL &&
                          root->right == NULL) {

        return nullptr;
    }
    return root;
}

void inorder(Node* root)
{
    if (root == NULL)
        return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

// Driver program
int main(void)
{
    struct Node* root = newNode(10);
    root->left = newNode(3);
    root->right = newNode(10);
    root->left->left = newNode(3);
    root->left->right = newNode(1);
    root->right->right = newNode(3);
    root->right->right->left = newNode(3);
    root->right->right->right = newNode(3);
    deleteLeaves(root, 3);
    cout << "Inorder traversal after deletion : ";
    inorder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to delete all leaves with given
// value.
class GfG {

// A binary tree node
static class Node {
    int data;
    Node left, right;
}

// A utility function to allocate a new node
static Node newNode(int data)
{
    Node newNode = new Node();
    newNode.data = data;
    newNode.left = null;
    newNode.right = null;
    return (newNode);
}

static Node deleteLeaves(Node root, int x)
{
    if (root == null)
        return null;
    root.left = deleteLeaves(root.left, x);
    root.right = deleteLeaves(root.right, x);

    if (root.data == x && root.left == null && root.right == null) {

        return null;
    }
    return root;
}

static void inorder(Node root)
{
    if (root == null)
        return;
    inorder(root.left);
    System.out.print(root.data + " ");
    inorder(root.right);
}

// Driver program
public static void main(String[] args)
{
    Node root = newNode(10);
    root.left = newNode(3);
    root.right = newNode(10);
    root.left.left = newNode(3);
    root.left.right = newNode(1);
    root.right.right = newNode(3);
    root.right.right.left = newNode(3);
    root.right.right.right = newNode(3);
    deleteLeaves(root, 3);
    System.out.print("Inorder traversal after deletion : ");
    inorder(root);
}
}
```

## 蟒蛇 3

```
# Python3 code to delete all leaves
# with given value.

# A utility class to allocate a new node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

def deleteLeaves(root, x):
    if (root == None):
        return None
    root.left = deleteLeaves(root.left, x)
    root.right = deleteLeaves(root.right, x)

    if (root.data == x and
        root.left == None and
        root.right == None):
        return None
    return root

def inorder(root):
    if (root == None):
        return
    inorder(root.left)
    print(root.data, end = " ")
    inorder(root.right)

# Driver Code
if __name__ == '__main__':
    root = newNode(10)
    root.left = newNode(3)
    root.right = newNode(10)
    root.left.left = newNode(3)
    root.left.right = newNode(1)
    root.right.right = newNode(3)
    root.right.right.left = newNode(3)
    root.right.right.right = newNode(3)
    deleteLeaves(root, 3)
    print("Inorder traversal after deletion : ")
    inorder(root)

# This code is contributed by PranchalK
```

## C#

```
// C# code to delete all leaves with given
// value.
using System;

class GfG
{

    // A binary tree node
    class Node
    {
        public int data;
        public Node left, right;
    }

    // A utility function to allocate a new node
    static Node newNode(int data)
    {
        Node newNode = new Node();
        newNode.data = data;
        newNode.left = null;
        newNode.right = null;
        return (newNode);
    }

    static Node deleteLeaves(Node root, int x)
    {
        if (root == null)
            return null;
        root.left = deleteLeaves(root.left, x);
        root.right = deleteLeaves(root.right, x);

        if (root.data == x &&
            root.left == null &&
            root.right == null)
        {

            return null;
        }
        return root;
    }

    static void inorder(Node root)
    {
        if (root == null)
            return;
        inorder(root.left);
        Console.Write(root.data + " ");
        inorder(root.right);
    }

    // Driver code
    public static void Main(String[] args)
    {
        Node root = newNode(10);
        root.left = newNode(3);
        root.right = newNode(10);
        root.left.left = newNode(3);
        root.left.right = newNode(1);
        root.right.right = newNode(3);
        root.right.right.left = newNode(3);
        root.right.right.right = newNode(3);
        deleteLeaves(root, 3);
        Console.Write("Inorder traversal after deletion : ");
        inorder(root);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

    // JavaScript code to delete all leaves with given value.

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // A utility function to allocate a new node
    function newNode(data)
    {
        let newNode = new Node(data);
        return (newNode);
    }

    function deleteLeaves(root, x)
    {
        if (root == null)
            return null;
        root.left = deleteLeaves(root.left, x);
        root.right = deleteLeaves(root.right, x);

        if (root.data == x && root.left == null && root.right == null)
        {

            return null;
        }
        return root;
    }

    function inorder(root)
    {
        if (root == null)
            return;
        inorder(root.left);
        document.write(root.data + " ");
        inorder(root.right);
    }

    let root = newNode(10);
    root.left = newNode(3);
    root.right = newNode(10);
    root.left.left = newNode(3);
    root.left.right = newNode(1);
    root.right.right = newNode(3);
    root.right.right.left = newNode(3);
    root.right.right.right = newNode(3);
    deleteLeaves(root, 3);
    document.write("Inorder traversal after deletion : ");
    inorder(root);

</script>
```

**输出:**

```
Inorder traversal after deletion : 3 1 10 10
```