# 二叉树中的最大子树和，使得该子树也是 BST

> 原文:[https://www . geesforgeks . org/maximum-sub-tree-sum-in-a-a-binary-tree-so-sub-tree-也是-a-bst/](https://www.geeksforgeeks.org/maximum-sub-tree-sum-in-a-binary-tree-such-that-the-sub-tree-is-also-a-bst/)

给定一个二叉树，任务是打印一个子树的节点的最大和，这个子树也是一个[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)。
**例:**

```
Input : 
       7
      /  \
     12    2
    /  \    \
   11  13    5
  /         / \
 2         1   38  

Output:44
BST rooted under node 5 has the maximum sum
       5
      / \
     1   38

Input:
      5
     /  \
    9    2
   /      \
  6        3
 / \
8   7   

Output: 8
Here each leaf node represents a binary search tree 
also a BST with sum 5 exists
     2
      \
       3
But the leaf node 8 has the maximum sum.
```

**方法:**我们以自下而上的方式遍历树。对于每个遍历的节点，我们存储该子树的最大值和最小值的信息，如果是 BST，则存储一个变量 isBST，存储到目前为止找到的 BST 的最大和的变量 **currmax** ，以及存储当前节点下的左右子树(也是 BST)的和的变量 **sum** 。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
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

    // Max Value in the subtree
    int max;

    // Min value in the subtree
    int min;

    // If subtree is BST
    bool isBST;

    // Sum of the nodes of the sub-tree
    // rooted under the current node
    int sum;

    // Max sum of BST found till now
    int currmax;
};

// Returns information about subtree such as
// subtree with maximum sum which is also a BST
Info MaxSumBSTUtil(struct Node* root, int& maxsum)
{
    // Base case
    if (root == NULL)
        return { INT_MIN, INT_MAX, true, 0, 0 };

    // If current node is a leaf node then
    // return from the function and store
    // information about the leaf node
    if (root->left == NULL && root->right == NULL) {
        maxsum = max(maxsum, root->data);
        return { root->data, root->data, true, root->data, maxsum };
    }

    // Store information about the left subtree
    Info L = MaxSumBSTUtil(root->left, maxsum);

    // Store information about the right subtree
    Info R = MaxSumBSTUtil(root->right, maxsum);

    Info BST;

    // If the subtree rooted under the current node
    // is a BST
    if (L.isBST && R.isBST && L.max < root->data && R.min > root->data) {

        BST.max = max(root->data, max(L.max, R.max));
        BST.min = min(root->data, min(L.min, R.min));

        maxsum = max(maxsum, R.sum + root->data + L.sum);
        BST.sum = R.sum + root->data + L.sum;

        // Update the current maximum sum
        BST.currmax = maxsum;

        BST.isBST = true;
        return BST;
    }

    // If the whole tree is not a BST then
    // update the current maximum sum
    BST.isBST = false;
    BST.currmax = maxsum;
    BST.sum = R.sum + root->data + L.sum;

    return BST;
}

// Function to return the maximum
// sum subtree which is also a BST
int MaxSumBST(struct Node* root)
{
    int maxsum = INT_MIN;
    return MaxSumBSTUtil(root, maxsum).currmax;
}

// Driver code
int main()
{
    struct Node* root = new Node(5);
    root->left = new Node(14);
    root->right = new Node(3);
    root->left->left = new Node(6);
    root->right->right = new Node(7);
    root->left->left->left = new Node(9);
    root->left->left->right = new Node(1);

    cout << MaxSumBST(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Binary tree node
static class Node
{
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
static class Info
{

    // Max Value in the subtree
    int max;

    // Min value in the subtree
    int min;

    // If subtree is BST
    boolean isBST;

    // Sum of the nodes of the sub-tree
    // rooted under the current node
    int sum;

    // Max sum of BST found till now
    int currmax;

    Info(int m,int mi,boolean is,int su,int cur)
    {
        max = m;
        min = mi;
        isBST = is;
        sum = su;
        currmax = cur;
    }
    Info(){}
};

static class INT
{
    int a;
}

// Returns information about subtree such as
// subtree with the maximum sum which is also a BST
static Info MaxSumBSTUtil( Node root, INT maxsum)
{
    // Base case
    if (root == null)
        return new Info( Integer.MIN_VALUE,
                        Integer.MAX_VALUE, true, 0, 0 );

    // If current node is a leaf node then
    // return from the function and store
    // information about the leaf node
    if (root.left == null && root.right == null)
    {
        maxsum.a = Math.max(maxsum.a, root.data);
        return new Info( root.data, root.data,
                        true, root.data, maxsum.a );
    }

    // Store information about the left subtree
    Info L = MaxSumBSTUtil(root.left, maxsum);

    // Store information about the right subtree
    Info R = MaxSumBSTUtil(root.right, maxsum);

    Info BST=new Info();

    // If the subtree rooted under the current node
    // is a BST
    if (L.isBST && R.isBST && L.max < root.data &&
                               R.min > root.data)
    {

        BST.max = Math.max(root.data, Math.max(L.max, R.max));
        BST.min = Math.min(root.data, Math.min(L.min, R.min));

        maxsum.a = Math.max(maxsum.a, R.sum + root.data + L.sum);
        BST.sum = R.sum + root.data + L.sum;

        // Update the current maximum sum
        BST.currmax = maxsum.a;

        BST.isBST = true;
        return BST;
    }

    // If the whole tree is not a BST then
    // update the current maximum sum
    BST.isBST = false;
    BST.currmax = maxsum.a;
    BST.sum = R.sum + root.data + L.sum;

    return BST;
}

// Function to return the maximum
// sum subtree which is also a BST
static int MaxSumBST( Node root)
{
    INT maxsum = new INT();
    maxsum.a = Integer.MIN_VALUE;
    return MaxSumBSTUtil(root, maxsum).currmax;
}

// Driver code
public static void main(String args[])
{
    Node root = new Node(5);
    root.left = new Node(14);
    root.right = new Node(3);
    root.left.left = new Node(6);
    root.right.right = new Node(7);
    root.left.left.left = new Node(9);
    root.left.left.right = new Node(1);

    System.out.println( MaxSumBST(root));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
from sys import maxsize as INT_MAX
INT_MIN = -INT_MAX

# Binary tree node
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Information stored in every
# node during bottom up traversal
class Info:

    def __init__(self, _max, _min,
                 isBST, _sum, currmax):

        # Max Value in the subtree
        self.max = _max

        # Min value in the subtree
        self.min = _min

        # If subtree is BST
        self.isBST = isBST

        # Sum of the nodes of the sub-tree
        # rooted under the current node
        self.sum = _sum

        # Max sum of BST found till now
        self.currmax = currmax

# Returns information about
# subtree such as subtree
# with maximum sum which
# is also a BST
def MaxSumBSTUtil(root: Node) -> Info:
    global maxsum

    # Base case
    if (root is None):
        return Info(INT_MIN, INT_MAX,
                    True, 0, 0)

    # If current node is a
    # leaf node then return
    # from the function and store
    # information about the leaf node
    if (root.left is None and
        root.right is None):
        maxsum = max(maxsum,
                     root.data)
        return Info(root.data, root.data,
                    True, root.data, maxsum)

    # Store information about
    # the left subtree
    L = MaxSumBSTUtil(root.left)

    # Store information about
    # the right subtree
    R = MaxSumBSTUtil(root.right)

    BST = Info

    # If the subtree rooted under
    # the current node is a BST
    if (L.isBST and R.isBST and
        L.max < root.data and
        R.min > root.data):

        BST.max = max(root.data,
                  max(L.max, R.max))
        BST.min = min(root.data,
                  min(L.min, R.min))

        maxsum = max(maxsum, R.sum +
                     root.data + L.sum)
        BST.sum = R.sum + root.data + L.sum

        # Update the current maximum sum
        BST.currmax = maxsum

        BST.isBST = True
        return BST

    # If the whole tree is not
    # a BST then update the
    # current maximum sum
    BST.isBST = False
    BST.currmax = maxsum
    BST.sum = R.sum + root.data + L.sum

    return BST

# Function to return the maximum
# sum subtree which is also a BST
def MaxSumBST(root: Node) -> int:
    global maxsum
    return MaxSumBSTUtil(root).currmax

# Driver code
if __name__ == "__main__":

    root = Node(5)
    root.left = Node(14)
    root.right = Node(3)
    root.left.left = Node(6)
    root.right.right = Node(7)
    root.left.left.left = Node(9)
    root.left.left.right = Node(1)

    maxsum = INT_MIN
    print(MaxSumBST(root))

# This code is contributed by sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Binary tree node
public class Node
{
    public Node left;
    public Node right;
    public int data;

    public Node(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};

// Information stored in every
// node during bottom up traversal
public class Info
{

    // Max Value in the subtree
    public int max;

    // Min value in the subtree
    public int min;

    // If subtree is BST
    public bool isBST;

    // Sum of the nodes of the sub-tree
    // rooted under the current node
    public int sum;

    // Max sum of BST found till now
    public int currmax;

    public Info(int m,int mi,bool s,int su,int cur)
    {
        max = m;
        min = mi;
        isBST = s;
        sum = su;
        currmax = cur;
    }
    public Info(){}
};

public class INT
{
    public int a;
}

// Returns information about subtree such as
// subtree with the maximum sum which is also a BST
static Info MaxSumBSTUtil( Node root, INT maxsum)
{
    // Base case
    if (root == null)
        return new Info( int.MinValue,
                        int.MaxValue, true, 0, 0 );

    // If current node is a leaf node then
    // return from the function and store
    // information about the leaf node
    if (root.left == null && root.right == null)
    {
        maxsum.a = Math.Max(maxsum.a, root.data);
        return new Info( root.data, root.data,
                        true, root.data, maxsum.a );
    }

    // Store information about the left subtree
    Info L = MaxSumBSTUtil(root.left, maxsum);

    // Store information about the right subtree
    Info R = MaxSumBSTUtil(root.right, maxsum);

    Info BST = new Info();

    // If the subtree rooted under the current node
    // is a BST
    if (L.isBST && R.isBST && L.max < root.data &&
                            R.min > root.data)
    {

        BST.max = Math.Max(root.data, Math.Max(L.max, R.max));
        BST.min = Math.Min(root.data, Math.Min(L.min, R.min));

        maxsum.a = Math.Max(maxsum.a, R.sum + root.data + L.sum);
        BST.sum = R.sum + root.data + L.sum;

        // Update the current maximum sum
        BST.currmax = maxsum.a;

        BST.isBST = true;
        return BST;
    }

    // If the whole tree is not a BST then
    // update the current maximum sum
    BST.isBST = false;
    BST.currmax = maxsum.a;
    BST.sum = R.sum + root.data + L.sum;

    return BST;
}

// Function to return the maximum
// sum subtree which is also a BST
static int MaxSumBST( Node root)
{
    INT maxsum = new INT();
    maxsum.a = int.MinValue;
    return MaxSumBSTUtil(root, maxsum).currmax;
}

// Driver code
public static void Main(String []args)
{
    Node root = new Node(5);
    root.left = new Node(14);
    root.right = new Node(3);
    root.left.left = new Node(6);
    root.right.right = new Node(7);
    root.left.left.left = new Node(9);
    root.left.left.right = new Node(1);

    Console.WriteLine( MaxSumBST(root));
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Binary tree node
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};

// Information stored in every
// node during bottom up traversal
class Info
{

    constructor(m,mi,s,su,cur)
    {
        // max Value in the subtree
        this.max = m;
        // min value in the subtree
        this.min = mi;
        // If subtree is BST
        this.isBST = s;
        // Sum of the nodes of the sub-tree
        // rooted under the current node
        this.sum = su;
        // max sum of BST found till now
        this.currmax = cur;
    }
};

class INT
{
    constructor()
    {
        this.a = 0;
    }
}

// Returns information about subtree such as
// subtree with the maximum sum which is also a BST
function MaxSumBSTUtil( root, maxsum)
{
    // Base case
    if (root == null)
        return new Info( -1000000000,
                        1000000000, true, 0, 0 );

    // If current node is a leaf node then
    // return from the function and store
    // information about the leaf node
    if (root.left == null && root.right == null)
    {
        maxsum.a = Math.max(maxsum.a, root.data);
        return new Info( root.data, root.data,
                        true, root.data, maxsum.a );
    }

    // Store information about the left subtree
    var L = MaxSumBSTUtil(root.left, maxsum);

    // Store information about the right subtree
    var R = MaxSumBSTUtil(root.right, maxsum);

    var BST = new Info();

    // If the subtree rooted under the current node
    // is a BST
    if (L.isBST && R.isBST && L.max < root.data &&
                            R.min > root.data)
    {

        BST.max = Math.max(root.data, Math.max(L.max, R.max));
        BST.min = Math.min(root.data, Math.min(L.min, R.min));

        maxsum.a = Math.max(maxsum.a, R.sum + root.data + L.sum);
        BST.sum = R.sum + root.data + L.sum;

        // Update the current maximum sum
        BST.currmax = maxsum.a;

        BST.isBST = true;
        return BST;
    }

    // If the whole tree is not a BST then
    // update the current maximum sum
    BST.isBST = false;
    BST.currmax = maxsum.a;
    BST.sum = R.sum + root.data + L.sum;

    return BST;
}

// Function to return the maximum
// sum subtree which is also a BST
function MaxSumBST( root)
{
    var maxsum = new INT();
    maxsum.a = -1000000000;
    return MaxSumBSTUtil(root, maxsum).currmax;
}

// Driver code
var root = new Node(5);
root.left = new Node(14);
root.right = new Node(3);
root.left.left = new Node(6);
root.right.right = new Node(7);
root.left.left.left = new Node(9);
root.left.left.right = new Node(1);
document.write( MaxSumBST(root));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
10
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)