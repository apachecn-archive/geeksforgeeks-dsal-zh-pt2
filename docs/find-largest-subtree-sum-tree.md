# 求一棵树中最大的子树和

> 原文:[https://www . geesforgeks . org/find-最大-子树-总和-树/](https://www.geeksforgeeks.org/find-largest-subtree-sum-tree/)

给定一棵二叉树，任务是寻找树中最大和的子树。
**例:**

```
Input :       1
            /   \
           2      3
          / \    / \
         4   5  6   7
Output : 28
As all the tree elements are positive,
the largest subtree sum is equal to
sum of all tree elements.

Input :       1
            /    \
          -2      3
          / \    /  \
         4   5  -6   2
Output : 7
Subtree with largest sum is :  -2
                             /  \ 
                            4    5
Also, entire tree sum is also 7.
```

[Recommended : Please try your approach first on IDE and then look at the solution.](https://ide.geeksforgeeks.org)

**方法:**对二叉树进行后序遍历。在每个节点上，递归地找到左子树值和右子树值。以当前节点为根的子树的值等于当前节点值、左节点子树和、右节点子树和之和。将当前子树总和与目前为止的最大子树总和进行比较。
**实施:**

## C++

```
// C++ program to find largest subtree
// sum in a given binary tree.
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

// Helper function to find largest
// subtree sum recursively.
int findLargestSubtreeSumUtil(Node* root, int& ans)
{
    // If current node is null then
    // return 0 to parent node.
    if (root == NULL)    
        return 0;

    // Subtree sum rooted at current node.
    int currSum = root->key +
      findLargestSubtreeSumUtil(root->left, ans)
      + findLargestSubtreeSumUtil(root->right, ans);

    // Update answer if current subtree
    // sum is greater than answer so far.
    ans = max(ans, currSum);

    // Return current subtree sum to
    // its parent node.
    return currSum;
}

// Function to find largest subtree sum.
int findLargestSubtreeSum(Node* root)
{
    // If tree does not exist,
    // then answer is 0.
    if (root == NULL)    
        return 0;

    // Variable to store maximum subtree sum.
    int ans = INT_MIN;

    // Call to recursive function to
    // find maximum subtree sum.
    findLargestSubtreeSumUtil(root, ans);

    return ans;
}

// Driver function
int main()
{
    /*
               1
             /   \
            /     \
          -2       3
          / \     /  \
         /   \   /    \
        4     5 -6     2
    */

    Node* root = newNode(1);
    root->left = newNode(-2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(-6);
    root->right->right = newNode(2);

    cout << findLargestSubtreeSum(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest
// subtree sum in a given binary tree.
import java.util.*;
class GFG
{

// Structure of a tree node.
static class Node
{
    int key;
    Node left, right;
}

static class INT
{
    int v;
    INT(int a)
    {
        v = a;
    }
}

// Function to create new tree node.
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return temp;
}

// Helper function to find largest
// subtree sum recursively.
static int findLargestSubtreeSumUtil(Node root,
                                     INT ans)
{
    // If current node is null then
    // return 0 to parent node.
    if (root == null)    
        return 0;

    // Subtree sum rooted
    // at current node.
    int currSum = root.key +
    findLargestSubtreeSumUtil(root.left, ans) +
    findLargestSubtreeSumUtil(root.right, ans);

    // Update answer if current subtree
    // sum is greater than answer so far.
    ans.v = Math.max(ans.v, currSum);

    // Return current subtree
    // sum to its parent node.
    return currSum;
}

// Function to find
// largest subtree sum.
static int findLargestSubtreeSum(Node root)
{
    // If tree does not exist,
    // then answer is 0.
    if (root == null)    
        return 0;

    // Variable to store
    // maximum subtree sum.
    INT ans = new INT(-9999999);

    // Call to recursive function
    // to find maximum subtree sum.
    findLargestSubtreeSumUtil(root, ans);

    return ans.v;
}

// Driver Code
public static void main(String args[])
{
    /*
            1
            / \
            /     \
        -2     3
        / \     / \
        / \ / \
        4     5 -6     2
    */

    Node root = newNode(1);
    root.left = newNode(-2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(-6);
    root.right.right = newNode(2);

    System.out.println(findLargestSubtreeSum(root));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find largest subtree
# sum in a given binary tree.

# Function to create new tree node.
class newNode:
    def __init__(self, key):
        self.key = key
        self.left = self.right = None

# Helper function to find largest
# subtree sum recursively.
def findLargestSubtreeSumUtil(root, ans):

    # If current node is None then
    # return 0 to parent node.
    if (root == None):
        return 0

    # Subtree sum rooted at current node.
    currSum = (root.key +
               findLargestSubtreeSumUtil(root.left, ans) +
               findLargestSubtreeSumUtil(root.right, ans))

    # Update answer if current subtree
    # sum is greater than answer so far.
    ans[0] = max(ans[0], currSum)

    # Return current subtree sum to
    # its parent node.
    return currSum

# Function to find largest subtree sum.
def findLargestSubtreeSum(root):

    # If tree does not exist,
    # then answer is 0.
    if (root == None):    
        return 0

    # Variable to store maximum subtree sum.
    ans = [-999999999999]

    # Call to recursive function to
    # find maximum subtree sum.
    findLargestSubtreeSumUtil(root, ans)

    return ans[0]

# Driver Code
if __name__ == '__main__':

    #
    #         1
    #         / \
    #     /     \
    #     -2     3
    #     / \     / \
    #     / \ / \
    # 4     5 -6     2
    root = newNode(1)
    root.left = newNode(-2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.left = newNode(-6)
    root.right.right = newNode(2)

    print(findLargestSubtreeSum(root))

# This code is contributed by PranchalK
```

## C#

```
using System;

// C# program to find largest
// subtree sum in a given binary tree.

public class GFG
{

// Structure of a tree node.
public class Node
{
    public int key;
    public Node left, right;
}

public class INT
{
    public int v;
    public INT(int a)
    {
        v = a;
    }
}

// Function to create new tree node.
public static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return temp;
}

// Helper function to find largest
// subtree sum recursively.
public static int findLargestSubtreeSumUtil(Node root, INT ans)
{
    // If current node is null then
    // return 0 to parent node.
    if (root == null)
    {
        return 0;
    }

    // Subtree sum rooted
    // at current node.
    int currSum = root.key + findLargestSubtreeSumUtil(root.left, ans)
                        + findLargestSubtreeSumUtil(root.right, ans);

    // Update answer if current subtree
    // sum is greater than answer so far.
    ans.v = Math.Max(ans.v, currSum);

    // Return current subtree
    // sum to its parent node.
    return currSum;
}

// Function to find
// largest subtree sum.
public static int findLargestSubtreeSum(Node root)
{
    // If tree does not exist,
    // then answer is 0.
    if (root == null)
    {
        return 0;
    }

    // Variable to store
    // maximum subtree sum.
    INT ans = new INT(-9999999);

    // Call to recursive function
    // to find maximum subtree sum.
    findLargestSubtreeSumUtil(root, ans);

    return ans.v;
}

// Driver Code
public static void Main(string[] args)
{
    /*
            1
            / \
            /     \
        -2     3
        / \     / \
        / \ / \
        4     5 -6     2
    */

    Node root = newNode(1);
    root.left = newNode(-2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(-6);
    root.right.right = newNode(2);

    Console.WriteLine(findLargestSubtreeSum(root));
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // Javascript program to find largest
    // subtree sum in a given binary tree.

    // Structure of a tree node.
    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.key = key;
        }
    }

    let v;

    // Function to create new tree node.
    function newNode(key)
    {
        let temp = new Node(key);
        return temp;
    }

    // Helper function to find largest
    // subtree sum recursively.
    function findLargestSubtreeSumUtil(root)
    {
        // If current node is null then
        // return 0 to parent node.
        if (root == null)    
            return 0;

        // Subtree sum rooted
        // at current node.
        let currSum = root.key +
        findLargestSubtreeSumUtil(root.left) +
        findLargestSubtreeSumUtil(root.right);

        // Update answer if current subtree
        // sum is greater than answer so far.
        v = Math.max(v, currSum);

        // Return current subtree
        // sum to its parent node.
        return currSum;
    }

    // Function to find
    // largest subtree sum.
    function findLargestSubtreeSum(root)
    {
        // If tree does not exist,
        // then answer is 0.
        if (root == null)    
            return 0;

        // Variable to store
        // maximum subtree sum.
        v = -9999999;

        // Call to recursive function
        // to find maximum subtree sum.
        findLargestSubtreeSumUtil(root);

        return v;
    }

    /*
            1
            / \
            /     \
        -2     3
        / \     / \
        / \ / \
        4     5 -6     2
    */

    let root = newNode(1);
    root.left = newNode(-2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(-6);
    root.right.right = newNode(2);

    document.write(findLargestSubtreeSum(root));

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
7
```