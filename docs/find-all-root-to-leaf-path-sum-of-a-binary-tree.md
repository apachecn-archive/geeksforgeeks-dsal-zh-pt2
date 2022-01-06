# 求二叉树所有根到叶的路径和

> 原文:[https://www . geeksforgeeks . org/find-all-root-to-leaf-path-a-sum-a-二叉树/](https://www.geeksforgeeks.org/find-all-root-to-leaf-path-sum-of-a-binary-tree/)

给定一棵[二叉树，](https://www.geeksforgeeks.org/binary-tree-data-structure/)的任务是打印给定二叉树的所有根到叶路径的和。

**示例:**

```
Input:
                 30
              /      \
            10        50
           /  \      /  \
          3   16   40    60
Output: 43 56 120 140
Explanation:
In the above binary tree
there are 4 leaf nodes. 
Hence, total 4 path sum are
present from root node to the
leaf node. 
(i.e., 30-10-3, 30-10-16,
       30-50-40, 30-50-60) 
Therefore, the path sums from
left to right would be
(43, 56, 120, 140).

Input:
                 11
              /      \
            12        5
              \      /  
              16   40
Output: 39 56
Explanation:
In the above binary tree
there are 2 leaf nodes. 
Hence, total 2 path sum are
present from root node to
the leaf node.
(i.e 11-12-16, 11-5-40) 
Therefore, the path sums from
left to right would be (39 56).
```

**方法:**思路是利用 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)从二叉树的根到叶行进，计算每个根到叶路径的和。按照以下步骤解决问题:

1.  从二叉树的根节点开始，初始路径和为 0。
2.  将当前节点的值添加到路径总和中。
3.  用路径和的当前值移动到当前节点的左右子节点。
4.  对二叉树的所有后续节点重复步骤 2 和 3。
5.  到达叶节点后，将路径和添加到**路径和**的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中。
6.  打印矢量的所有元素**路径总和**作为输出。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// TreeNode structure
struct TreeNode {
    int val;
    TreeNode *left, *right;
};

// Function that returns a new TreeNode
// with given value
struct TreeNode* addNode(int data)
{
    // Allocate memory
    struct TreeNode* node
        = (struct TreeNode*)malloc(
            sizeof(struct TreeNode));

    // Assign data to val variable
    node->val = data;
    node->left = NULL;
    node->right = NULL;
    return node;
};

// Function that calculates the root to
// leaf path sum of the BT using DFS
void dfs(TreeNode* root, int sum,
         vector<int>& pathSum)
{
    // Return if the node is NULL
    if (root == NULL)
        return;

    // Add value of the node to
    // the path sum
    sum += root->val;

    // Store the path sum if node is leaf
    if (root->left == NULL
        and root->right == NULL) {

        pathSum.push_back(sum);
        return;
    }

    // Move to the left child
    dfs(root->left, sum, pathSum);

    // Move to the right child
    dfs(root->right, sum, pathSum);
}

// Function that finds the root to leaf
// path sum of the given binary tree
void findPathSum(TreeNode* root)
{
    // To store all the path sum
    vector<int> pathSum;

    // Calling dfs function
    dfs(root, 0, pathSum);

    // Printing all the path sum
    for (int num : pathSum) {
        cout << num << " ";
    }
    cout << endl;
}

// Driver Code
int main()
{
    // Given binary tree
    TreeNode* root = addNode(30);
    root->left = addNode(10);
    root->right = addNode(50);
    root->left->left = addNode(3);
    root->left->right = addNode(16);
    root->right->left = addNode(40);
    root->right->right = addNode(60);

    /*  The above code constructs this tree

                30
             /      \
           10        50
          /  \      /  \
         3   16   40    60
   */

    // Function Call
    findPathSum(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Structure of
// binary tree node
static class Node
{
    int val;
    Node left, right;
};

// Function to create new node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.val = data;
    temp.left = temp.right = null;
    return temp;
}

// Function that calculates the root to
// leaf path sum of the BT using DFS
static void dfs(Node root, int sum,
                ArrayList<Integer> pathSum)
{

    // Return if the node is NULL
    if (root == null)
        return;

    // Add value of the node to
    // the path sum
    sum += root.val;

    // Store the path sum if node is leaf
    if (root.left == null &&
       root.right == null)
    {
        pathSum.add(sum);
        return;
    }

    // Move to the left child
    dfs(root.left, sum, pathSum);

    // Move to the right child
    dfs(root.right, sum, pathSum);
}

// Function that finds the root to leaf
// path sum of the given binary tree
static void findPathSum(Node root)
{

    // To store all the path sum
    ArrayList<Integer> pathSum = new ArrayList<>();

    // Calling dfs function
    dfs(root, 0, pathSum);

    // Printing all the path sum
    for(int num : pathSum)
    {
        System.out.print(num + " ");
    }
}

// Driver code
public static void main(String[] args)
{

    // Construct binary tree
    Node root = newNode(30);
    root.left = newNode(10);
    root.right = newNode(50);
    root.left.left = newNode(3);
    root.left.right = newNode(16);
    root.right.left = newNode(40);
    root.right.right = newNode(60);

    /*  The above code constructs this tree

            30
         /      \
       10        50
      /  \      /  \
     3   16   40    60
*/

    // Function call
    findPathSum(root);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
from collections import deque

# A Tree node
class Node:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None

pathSum = []

# Function that calculates
# the root to leaf path
# sum of the BT using DFS
def dfs(root, sum):

    # Return if the node
    # is NULL
    if (root == None):
        return

    # Add value of the node to
    # the path sum
    sum += root.data

    # Store the path sum if
    # node is leaf
    if (root.left == None and
        root.right == None):
        pathSum.append(sum)
        return

    # Move to the left child
    dfs(root.left, sum)

    # Move to the right child
    dfs(root.right, sum)

# Function that finds the
# root to leaf path sum
# of the given binary tree
def findPathSum(root):

    # To store all the path sum
    # vector<int> pathSum

    # Calling dfs function
    dfs(root, 0)

    # Printing all the path sum
    for num in pathSum:
        print(num, end = " ")

# Driver Code
if __name__ == '__main__':

    # Given binary tree
    root = Node(30)
    root.left = Node(10)
    root.right = Node(50)
    root.left.left = Node(3)
    root.left.right = Node(16)
    root.right.left = Node(40)
    root.right.right = Node(60)

   #  /*  The above code constructs this tree
   #
   #              30
   #           /      \
   #         10        50
   #        /  \      /  \
   #       3   16   40    60
   # */

    # Function Call
    findPathSum(root)

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

// Structure of
// binary tree node
public class Node
{
    public int val;
    public Node left, right;  
    public Node(int item)
    {
        val = item;
        left = right = null;
    }
}
public class BinaryTree
{
    public static Node node;

    // Function that calculates the root to
    // leaf path sum of the BT using DFS
    static void dfs(Node root, int sum, List<int> pathSum)
    {

        // Return if the node is NULL
        if (root == null)
        {
            return;
        }

        // Add value of the node to
        // the path sum
        sum += root.val;

        // Store the path sum if node is leaf
        if(root.left == null && root.right == null)
        {
            pathSum.Add(sum);
            return;
        }

        // Move to the left child
        dfs(root.left, sum, pathSum);

        // Move to the right child
        dfs(root.right, sum, pathSum);
    }

    // Function that finds the root to leaf
    // path sum of the given binary tree
    static void findPathSum(Node root)
    {

        // To store all the path sum
        List<int> pathSum = new List<int>();

        // Calling dfs function
        dfs(root, 0, pathSum);

        // Printing all the path sum
        foreach(int num in pathSum)
        {
            Console.Write(num + " ");
        }
    }

    // Driver code
    static public void Main ()
    {

        // Construct binary tree
        BinaryTree.node = new Node(30);
        BinaryTree.node.left = new Node(10);
        BinaryTree.node.right = new Node(50);
        BinaryTree.node.left.left = new Node(3);
        BinaryTree.node.left.right = new Node(16);
        BinaryTree.node.right.left = new Node(40);
        BinaryTree.node.right.right = new Node(60);

      /*  The above code constructs this tree

            30
         /      \
       10        50
      /  \      /  \
     3   16   40    60
*/
        // Function call
        findPathSum(node);
    }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Structure of
// binary tree node
class Node
{
    constructor(data)
    {
        this.val=data;
        this.left=this.right=null;
    }
}

// Function that calculates the root to
// leaf path sum of the BT using DFS
function dfs(root,sum,pathSum)
{
    // Return if the node is NULL
    if (root == null)
        return;

    // Add value of the node to
    // the path sum
    sum += root.val;

    // Store the path sum if node is leaf
    if (root.left == null &&
       root.right == null)
    {
        pathSum.push(sum);
        return;
    }

    // Move to the left child
    dfs(root.left, sum, pathSum);

    // Move to the right child
    dfs(root.right, sum, pathSum);
}

// Function that finds the root to leaf
// path sum of the given binary tree
function findPathSum(root)
{
    // To store all the path sum
    let pathSum = [];

    // Calling dfs function
    dfs(root, 0, pathSum);

    // Printing all the path sum
    for(let num=0;num<pathSum.length;num++)
    {
        document.write(pathSum[num] + " ");
    }
}

// Driver code
// Construct binary tree
let root = new Node(30);
root.left = new Node(10);
root.right = new Node(50);
root.left.left = new Node(3);
root.left.right = new Node(16);
root.right.left = new Node(40);
root.right.right = new Node(60);

/*  The above code constructs this tree

            30
         /      \
       10        50
      /  \      /  \
     3   16   40    60
*/

// Function call
findPathSum(root);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
43 56 120 140
```

***时间复杂度*****:***O(N)*
***辅助空间:** O(N)*