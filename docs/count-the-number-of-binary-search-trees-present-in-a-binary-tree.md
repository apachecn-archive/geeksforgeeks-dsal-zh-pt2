# 计算二叉树中二分搜索法树的数量

> 原文:[https://www . geeksforgeeks . org/count-二进制搜索树的数量-存在于二进制树中/](https://www.geeksforgeeks.org/count-the-number-of-binary-search-trees-present-in-a-binary-tree/)

给定一棵二叉树，任务是计算其中存在的二分搜索法树的数量。

**例:**

> **输入:**
> 
> ```
>     1
>    /  \
>   2    3
>  / \  / \
> 4   5 6  7
> ```
> 
> **输出:** 4
> 这里每个叶节点代表一个二叉查找树，总共有 4 个节点。
> **输入:**
> 
> ```
>       11
>      /  \
>     8    10
>    /    /  \
>   5    9    8
>  / \
> 4   6
> ```
> 
> **输出:** 6
> 根在节点 5 下的子树是一个 BST
> 
> ```
>    5
>   / \
>  4   6
> ```
> 
> 我们的另一个 BST 位于节点 8 下
> 
> ```
>         8    
>        /    
>       5    
>      / \
>     4   6
> ```
> 
> 因此，总共存在 6 个 BST(包括叶节点)。

**方法:**如果每个节点 x 都满足以下条件，则二叉树是二叉查找树树。

1.  (x 的)左子树中的最大值小于 x 的值。
2.  (x 的)右子树中的最小值大于 x 的值。

我们以自下而上的方式遍历树。对于每个遍历的节点，我们存储该子树的最大值和最小值的信息，如果是 BST，则存储变量 **isBST** ，如果是 BST，则存储变量 **num_BST** 以存储当前节点下的二叉查找树根数。
以下是上述方法的实施:

## C++

```
// C++ program to count number of Binary search trees
// in a given Binary Tree
#include <bits/stdc++.h>
using namespace std;

// Binary tree node
struct Node {
    struct Node* left;
    struct Node* right;
    int data;

    Node(int data)
    {
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};

// Information stored in every
// node during bottom up traversal
struct Info {

    // Stores the number of BSTs present
    int num_BST;

    // Max Value in the subtree
    int max;

    // Min value in the subtree
    int min;

    // If subtree is BST
    bool isBST;
};

// Returns information about subtree such as
// number of BST's it has
Info NumberOfBST(struct Node* root)
{
    // Base case
    if (root == NULL)
        return { 0, INT_MIN, INT_MAX, true };

    // If leaf node then return from function and store
    // information about the leaf node
    if (root->left == NULL && root->right == NULL)
        return { 1, root->data, root->data, true };

    // Store information about the left subtree
    Info L = NumberOfBST(root->left);

    // Store information about the right subtree
    Info R = NumberOfBST(root->right);

    // Create a node that has to be returned
    Info bst;
    bst.min = min(root->data, (min(L.min, R.min)));
    bst.max = max(root->data, (max(L.max, R.max)));

    // If whole tree rooted under the
    // current root is BST
    if (L.isBST && R.isBST && root->data > L.max && root->data < R.min) {

        // Update the number of BSTs
        bst.isBST = true;
        bst.num_BST = 1 + L.num_BST + R.num_BST;
    }

    // If the whole tree is not a BST,
    // update the number of BSTs
    else {
        bst.isBST = false;
        bst.num_BST = L.num_BST + R.num_BST;
    }

    return bst;
}

// Driver code
int main()
{
    struct Node* root = new Node(5);
    root->left = new Node(9);
    root->right = new Node(3);
    root->left->left = new Node(6);
    root->right->right = new Node(4);
    root->left->left->left = new Node(8);
    root->left->left->right = new Node(7);

    cout << NumberOfBST(root).num_BST;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// number of Binary search
// trees in a given Binary Tree
import java.util.*;

class GFG {

    // Binary tree node
    static class Node {
        Node left;
        Node right;
        int data;

        Node(int data)
        {
            this.data = data;
            this.left = null;
            this.right = null;
        }
    };

    // Information stored in every
    // node during bottom up traversal
    static class Info {

        // Stores the number of BSTs present
        int num_BST;

        // Max Value in the subtree
        int max;

        // Min value in the subtree
        int min;

        // If subtree is BST
        boolean isBST;

        Info(int a, int b, int c, boolean d)
        {
            num_BST = a;
            max = b;
            min = c;
            isBST = d;
        }
        Info()
        {
        }
    };

    // Returns information about subtree such as
    // number of BST's it has
    static Info NumberOfBST(Node root)
    {
        // Base case
        if (root == null)
            return new Info(0, Integer.MIN_VALUE,
                            Integer.MAX_VALUE, true);

        // If leaf node then return
        // from function and store
        // information about the leaf node
        if (root.left == null && root.right == null)
            return new Info(1, root.data, root.data, true);

        // Store information about the left subtree
        Info L = NumberOfBST(root.left);

        // Store information about the right subtree
        Info R = NumberOfBST(root.right);

        // Create a node that has to be returned
        Info bst = new Info();
        bst.min = Math.min(root.data, (Math.min(L.min, R.min)));
        bst.max = Math.max(root.data, (Math.max(L.max, R.max)));

        // If whole tree rooted under the
        // current root is BST
        if (L.isBST && R.isBST && root.data > L.max && root.data < R.min) {

            // Update the number of BSTs
            bst.isBST = true;
            bst.num_BST = 1 + L.num_BST + R.num_BST;
        }

        // If the whole tree is not a BST,
        // update the number of BSTs
        else {
            bst.isBST = false;
            bst.num_BST = L.num_BST + R.num_BST;
        }

        return bst;
    }

    // Driver code
    public static void main(String args[])
    {
        Node root = new Node(5);
        root.left = new Node(9);
        root.right = new Node(3);
        root.left.left = new Node(6);
        root.right.right = new Node(4);
        root.left.left.left = new Node(8);
        root.left.left.right = new Node(7);

        System.out.print(NumberOfBST(root).num_BST);
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python program to count number of Binary search
# trees in a given Binary Tree
INT_MIN = -2**31
INT_MAX = 2**31
class newNode():

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Returns information about subtree such as
# number of BST's it has
def NumberOfBST(root):

    # Base case
    if (root == None):
        return 0, INT_MIN, INT_MAX, True

    # If leaf node then return from function and store
    # information about the leaf node
    if (root.left == None and root.right == None):
        return 1, root.data, root.data, True

    # Store information about the left subtree
    L = NumberOfBST(root.left)

    # Store information about the right subtree
    R = NumberOfBST(root.right)

    # Create a node that has to be returned
    bst = [0]*4
    bst[2] = min(root.data, (min(L[2], R[2])))
    bst[1] = max(root.data, (max(L[1], R[1])))

    # If whole tree rooted under the
    # current root is BST
    if (L[3] and R[3] and root.data > L[1] and root.data < R[2]):

        # Update the number of BSTs
        bst[3] = True
        bst[0] = 1 + L[0] + R[0]

    # If the whole tree is not a BST,
    # update the number of BSTs
    else:
        bst[3] = False
        bst[0] = L[0] + R[0]

    return bst

# Driver code
if __name__ == '__main__':
    root = newNode(5)
    root.left = newNode(9)
    root.right = newNode(3)
    root.left.left = newNode(6)
    root.right.right = newNode(4)
    root.left.left.left = newNode(8)
    root.left.left.right = newNode(7)

    print(NumberOfBST(root)[0])

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
using System;

// C# program to count
// number of Binary search
// trees in a given Binary Tree

public class GFG {

    // Binary tree node
    public class Node {
        public Node left;
        public Node right;
        public int data;

        public Node(int data)
        {
            this.data = data;
            this.left = null;
            this.right = null;
        }
    }

    // Information stored in every
    // node during bottom up traversal
    public class Info {

        // Stores the number of BSTs present
        public int num_BST;

        // Max Value in the subtree
        public int max;

        // Min value in the subtree
        public int min;

        // If subtree is BST
        public bool isBST;

        public Info(int a, int b, int c, bool d)
        {
            num_BST = a;
            max = b;
            min = c;
            isBST = d;
        }
        public Info()
        {
        }
    }

    // Returns information about subtree such as
    // number of BST's it has
    static Info NumberOfBST(Node root)
    {
        // Base case
        if (root == null)
            return new Info(0, Int32.MinValue,
                            Int32.MaxValue, true);

        // If leaf node then return
        // from function and store
        // information about the leaf node
        if (root.left == null && root.right == null)
            return new Info(1, root.data, root.data, true);

        // Store information about the left subtree
        Info L = NumberOfBST(root.left);

        // Store information about the right subtree
        Info R = NumberOfBST(root.right);

        // Create a node that has to be returned
        Info bst = new Info();
        bst.min = Math.Min(root.data, (Math.Min(L.min, R.min)));
        bst.max = Math.Max(root.data, (Math.Max(L.max, R.max)));

        // If whole tree rooted under the
        // current root is BST
        if (L.isBST && R.isBST && root.data > L.max && root.data < R.min) {

            // Update the number of BSTs
            bst.isBST = true;
            bst.num_BST = 1 + L.num_BST + R.num_BST;
        }

        // If the whole tree is not a BST,
        // update the number of BSTs
        else {
            bst.isBST = false;
            bst.num_BST = L.num_BST + R.num_BST;
        }

        return bst;
    }

    // Driver code
    public static void Main(string[] args)
    {
        Node root = new Node(5);
        root.left = new Node(9);
        root.right = new Node(3);
        root.left.left = new Node(6);
        root.right.right = new Node(4);
        root.left.left.left = new Node(8);
        root.left.left.right = new Node(7);

        Console.Write(NumberOfBST(root).num_BST);
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
      // JavaScript program to count
      // number of Binary search
      // trees in a given Binary Tree

      // Binary tree node
      class Node {
        constructor(data) {
          this.data = data;
          this.left = null;
          this.right = null;
        }
      }

      // Information stored in every
      // node during bottom up traversal
      class Info
      {
        constructor(a, b, c, d)
        {

          // Stores the number of BSTs present
          this.num_BST = a;

          // Max Value in the subtree
          this.max = b;

          // Min value in the subtree
          this.min = c;

          // If subtree is BST
          this.isBST = d;
        }
      }

      // Returns information about subtree such as
      // number of BST's it has
      function NumberOfBST(root)
      {

        // Base case
        if (root == null) return new Info(0, -2147483648, 2147483647, true);

        // If leaf node then return
        // from function and store
        // information about the leaf node
        if (root.left == null && root.right == null)
          return new Info(1, root.data, root.data, true);

        // Store information about the left subtree
        var L = NumberOfBST(root.left);

        // Store information about the right subtree
        var R = NumberOfBST(root.right);

        // Create a node that has to be returned
        var bst = new Info();
        bst.min = Math.min(root.data, Math.min(L.min, R.min));
        bst.max = Math.max(root.data, Math.max(L.max, R.max));

        // If whole tree rooted under the
        // current root is BST
        if (L.isBST && R.isBST && root.data > L.max && root.data < R.min) {
          // Update the number of BSTs
          bst.isBST = true;
          bst.num_BST = 1 + L.num_BST + R.num_BST;
        }

        // If the whole tree is not a BST,
        // update the number of BSTs
        else {
          bst.isBST = false;
          bst.num_BST = L.num_BST + R.num_BST;
        }

        return bst;
      }

      // Driver code
      var root = new Node(5);
      root.left = new Node(9);
      root.right = new Node(3);
      root.left.left = new Node(6);
      root.right.right = new Node(4);
      root.left.left.left = new Node(8);
      root.left.left.right = new Node(7);

      document.write(NumberOfBST(root).num_BST);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
4
```