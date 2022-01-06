# 给定二叉树中子树值的最大平均值

> 原文:[https://www . geesforgeks . org/给定二叉树中子树值的最大平均值/](https://www.geeksforgeeks.org/maximum-average-of-subtree-values-in-a-given-binary-tree/)

给定一个由 **N** 个节点组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是找出任意子树节点值的最大平均值。

**示例:**

> **输入:**5
> /\
> 3 8
> T5】输出: 8
> **解释:**
> 节点 5 的子树的值的平均值= (5 + 3 + 8) / 3 = 5.33
> 节点 3 的子树的值的平均值= 3 / 1 = 3
> 节点 8 的子树的值的平均值= 8 / 1 = 8。
> 
> **输入:**20
> /\
> 12 18
> /\/\
> 11 3 15 8
> **输出:** 15
> **说明:**节点 15 的子树取值平均值最大。

**方法:**给定的问题类似于[求一棵树](https://www.geeksforgeeks.org/find-largest-subtree-sum-tree/)中最大子树和的问题。想法是使用 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)技术。按照以下步骤解决问题:

*   初始化一个变量，**和**用 **0** 来存储结果。
*   为 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)定义一个函数 **maxAverage()** 。
    *   初始化两个变量，**求和**存储其子树的和，**计数**存储其子树的节点数， **0** 。
    *   遍历当前节点的子节点，调用其子节点的 **maxAverage()** ，用子节点子树的和增加 **sum** ，用子节点的总节点数增加 **count**
    *   用当前节点的值增加**和**，用 **1** 计数。
    *   取 **ans** 和 **sum/count** 的最大值存储在 **ans** 中。
    *   最后，返回一对 **{sum，count}** 。
*   将获得的最大平均值打印为**和**。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

struct TreeNode
{
    int val;

    vector<TreeNode*> children;

    TreeNode(int v)
    {
        val = v;
    }
};

// Stores the result
double ans = 0.0;

// Function for finding maximum
// subtree average
vector<int> MaxAverage(TreeNode* root)
{

    // Checks if current node is not
    // NULL and doesn't have any children
    if (root != NULL && root->children.size() == 0)
    {
        ans = max(ans, (root->val) * (1.0));
        return {root->val, 1};
    }

    // Stores sum of its subtree in index 0
    // and count number of nodes in index 1
    vector<int> childResult (2);

    // Traverse all children of the current node
    for(TreeNode *child : root->children)
    {

        // Recursively calculate max average
        // of subtrees among its children
        vector<int> childTotal = MaxAverage(child);

        // Increment sum by sum
        // of its child's subtree
        childResult[0]     = childResult[0] + childTotal[0];

        // Increment number of nodes
        // by its child's node
        childResult[1] = childResult[1] + childTotal[1];
    }

    // Increment sum by current node's value
    int sum = childResult[0] + root->val;

    // Increment number of
    // nodes by one
    int count = childResult[1] + 1;

    // Take maximum of ans and
    // current node's average
    ans = max(ans, sum / count * 1.0);

    // Finally return pair of {sum, count}
    return{sum, count};
}

// Driver Code
int main()
{

    // Given tree
    TreeNode *root = new TreeNode(20);
    TreeNode *left = new TreeNode(12);
    TreeNode *right = new TreeNode(18);

    root->children.push_back(left);
    root->children.push_back(right);

    left->children.push_back(new TreeNode(11));
    left->children.push_back(new TreeNode(3));
    right->children.push_back(new TreeNode(15));
    right->children.push_back(new TreeNode(8));

    // Function call
    MaxAverage(root);

    // Print answer
    printf("%0.1f\n", ans);
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

// Structure of the Tree node
class TreeNode {
    public int val;
    public List<TreeNode> children;

    public TreeNode(int v)
    {
        val = v;
        children = new ArrayList<TreeNode>();
    }
}

class GFG {

    // Stores the result
    static double ans = 0.0;

    // Function for finding maximum
    // subtree average
    public static double[] MaxAverage(
        TreeNode root)
    {

        // Checks if current node is not
        // null and doesn't have any children
        if (root.children != null
            && root.children.size() == 0) {
            ans = Math.max(ans, root.val);
            return new double[] { root.val, 1 };
        }

        // Stores sum of its subtree in index 0
        // and count number of nodes in index 1
        double[] childResult = new double[2];

        // Traverse all children of the current node
        for (TreeNode child : root.children) {

            // Recursively calculate max average
            // of subtrees among its children
            double[] childTotal
                = MaxAverage(child);

            // Increment sum by sum
            // of its child's subtree
            childResult[0]
                = childResult[0] + childTotal[0];

            // Increment number of nodes
            // by its child's node
            childResult[1]
                = childResult[1] + childTotal[1];
        }

        // Increment sum by current node's value
        double sum = childResult[0] + root.val;

        // Increment number of
        // nodes by one
        double count = childResult[1] + 1;

        // Take maximum of ans and
        // current node's average
        ans = Math.max(ans, sum / count);

        // Finally return pair of {sum, count}
        return new double[] { sum, count };
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given tree
        TreeNode root = new TreeNode(20);
        TreeNode left = new TreeNode(12);
        TreeNode right = new TreeNode(18);
        root.children.add(left);
        root.children.add(right);
        left.children.add(new TreeNode(11));
        left.children.add(new TreeNode(3));
        right.children.add(new TreeNode(15));
        right.children.add(new TreeNode(8));

        // Function call
        MaxAverage(root);

        // Print answer
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores the result
ans = 0.0

class TreeNode:

    def __init__ (self, val):

        self.val = val
        self.children = []

# Function for finding maximum
# subtree average
def MaxAverage(root):

    global ans

    # Checks if current node is not
    # None and doesn't have any children
    if (root != None and len(root.children) == 0):
        ans = max(ans, (root.val))
        return [root.val, 1]

    # Stores sum of its subtree in index 0
    # and count number of nodes in index 1
    childResult = [0 for i in range(2)]

    # Traverse all children of the current node
    for child in root.children:

        # Recursively calculate max average
        # of subtrees among its children
        childTotal = MaxAverage(child)

        # Increment sum by sum
        # of its child's subtree
        childResult[0] = childResult[0] + childTotal[0]

        # Increment number of nodes
        # by its child's node
        childResult[1] = childResult[1] + childTotal[1]

    # Increment sum by current node's value
    sum = childResult[0] + root.val

    # Increment number of
    # nodes by one
    count = childResult[1] + 1

    # Take maximum of ans and
    # current node's average
    ans = max(ans, sum / count)

    # Finally return pair of {sum, count}
    return [sum, count]

# Driver Code
if __name__ == '__main__':

    # Given tree
    root =  TreeNode(20)
    left =  TreeNode(12)
    right =  TreeNode(18)

    root.children.append(left)
    root.children.append(right)

    left.children.append(TreeNode(11))
    left.children.append(TreeNode(3))
    right.children.append(TreeNode(15))
    right.children.append(TreeNode(8))

    # Function call
    MaxAverage(root)

    # Print answer
    print(ans * 1.0)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Globalization;
public class TreeNode
{
  public int val;
  public List<TreeNode> children;

  public TreeNode(int v)
  {
    val = v;
    children = new List<TreeNode>();
  }
}

public class GFG
{

  // Stores the result
  static double ans = 0.0;

  // Function for finding maximum
  // subtree average
  public static double[] MaxAverage( TreeNode root)
  {

    // Checks if current node is not
    // null and doesn't have any children
    if (root.children != null
        && root.children.Count == 0)
    {
      ans = Math.Max(ans, root.val);
      return new double[] { root.val, 1 };
    }

    // Stores sum of its subtree in index 0
    // and count number of nodes in index 1
    double[] childResult = new double[2];

    // Traverse all children of the current node
    foreach (TreeNode child in root.children)
    {

      // Recursively calculate max average
      // of subtrees among its children
      double[] childTotal
        = MaxAverage(child);

      // Increment sum by sum
      // of its child's subtree
      childResult[0]
        = childResult[0] + childTotal[0];

      // Increment number of nodes
      // by its child's node
      childResult[1]
        = childResult[1] + childTotal[1];
    }

    // Increment sum by current node's value
    double sum = childResult[0] + root.val;

    // Increment number of
    // nodes by one
    double count = childResult[1] + 1;

    // Take maximum of ans and
    // current node's average
    ans = Math.Max(ans, sum / count);

    // Finally return pair of {sum, count}
    return new double[] { sum, count };
  }

  // Driver code
  static public void Main ()
  {
    // Given tree
    TreeNode root = new TreeNode(20);
    TreeNode left = new TreeNode(12);
    TreeNode right = new TreeNode(18);
    root.children.Add(left);
    root.children.Add(right);
    left.children.Add(new TreeNode(11));
    left.children.Add(new TreeNode(3));
    right.children.Add(new TreeNode(15));
    right.children.Add(new TreeNode(8));

    // Function call
    MaxAverage(root);

    // Print answer
    NumberFormatInfo setPrecision = new NumberFormatInfo();

    setPrecision.NumberDecimalDigits = 1;

    Console.WriteLine(ans.ToString("N", setPrecision));
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Structure of the Tree node
class TreeNode
{
    constructor(v)
    {
        this.val = v;
        this.children = [];
    }
}

    // Stores the result
    let ans = 0.0;

    // Function for finding maximum
    // subtree average
    function MaxAverage(root)
    {
        // Checks if current node is not
        // null and doesn't have any children
        if (root.children != null
            && root.children.length == 0)
        {
            ans = Math.max(ans, root.val);
            return  [ root.val, 1 ];
        }

        // Stores sum of its subtree in index 0
        // and count number of nodes in index 1
        let childResult = new Array(2);
        for(let i=0;i<childResult.length;i++)
        {
            childResult[i] = 0;
        }

        // Traverse all children of the current node
        for (let child = 0; child < root.children.length; child++)
        {

            // Recursively calculate max average
            // of subtrees among its children
            let childTotal
                = MaxAverage(root.children[child]);

            // Increment sum by sum
            // of its child's subtree
            childResult[0]
                = childResult[0] + childTotal[0];

            // Increment number of nodes
            // by its child's node
            childResult[1]
                = childResult[1] + childTotal[1];
        }

        // Increment sum by current node's value
        let sum = childResult[0] + root.val;

        // Increment number of
        // nodes by one
        let count = childResult[1] + 1;

        // Take maximum of ans and
        // current node's average       
        ans = Math.max(ans, sum / count);

        // Finally return pair of {sum, count}
        return [ sum, count ];
    }

    // Driver Code

    // Given tree
        let root = new TreeNode(20);
        let left = new TreeNode(12);
        let right = new TreeNode(18);
        root.children.push(left);
        root.children.push(right);
        left.children.push(new TreeNode(11));
        left.children.push(new TreeNode(3));
        right.children.push(new TreeNode(15));
        right.children.push(new TreeNode(8));

        // Function call
        MaxAverage(root);

        // Print answer
        document.write(ans.toFixed(1));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
15.0
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)