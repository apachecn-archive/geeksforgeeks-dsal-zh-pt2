# 统计二叉树中相距最多 K 个距离的叶节点对

> 原文:[https://www . geesforgeks . org/count-二叉树中最多相隔 k 个叶节点对/](https://www.geeksforgeeks.org/count-pairs-of-leaf-nodes-in-a-binary-tree-which-are-at-most-k-distance-apart/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)和一个整数 **K** ，任务是从给定的二叉树中计算可能的[叶节点对](https://www.geeksforgeeks.org/write-a-c-program-to-get-count-of-leaf-nodes-in-a-binary-tree/)，使得它们之间的距离最多为 **K** 。

**示例:**

> **输入:** K = 3
> 
> ```
>       1
>      / \
>     2   3
>    /
>   4
> ```
> 
> **输出:** 1
> **说明:**
> 树的叶节点为 3 和 4
> ，它们之间的最短距离为 3。
> 这是唯一有效的配对。
> 
> **输入:** K = 3
> 
> ```
>        1
>       / \
>      2   3
>     / \ / \
>    4  5 6  7
> ```
> 
> **输出:** 2

**方法:**想法是使用[后序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)和大小为 **K + 1** 的数组来跟踪特定距离的节点数量。以下是步骤:

*   初始化一个大小为 **K + 1** 的数组 **arr[]** ，其中 **arr[i]** 表示距离当前节点 **i** 的[叶节点](https://www.geeksforgeeks.org/write-a-c-program-to-get-count-of-leaf-nodes-in-a-binary-tree/)的数量。
*   然后，针对数组中每个节点的左、右子树分别递归更新上述数组**左[]** 和**右[]** 。
*   在上述步骤之后，对于每个节点，相应索引处左[]和右[]之间的距离将给出最左边和最右边叶节点之间的距离。在数组 **res[]** 中更新为:

> res[i + 1] =左[i] *右[i]

*   现在，对于阵列**左[]** 和**右[]** 中所有可能的对 **(l，r)** ，如果它们之间的距离之和最多为**K**，则对的计数递增如下:

> 计数+=左[l] *右[r]

下面是上述方法的实现:

## C++

```
// C++14 implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a Node
struct Node
{
    int data;
    Node* left, *right;

    // Constructor of the class
    Node(int item)
    {
        data = item;
        left = right = NULL;
    }
};

// Stores the count of required pairs
int result = 0;

// Function to perform dfs to find pair of
// leaf nodes at most K distance apart
vector<int> dfs(Node* root, int distance)
{

    // Return empty array if node is NULL
    if (root == NULL)
    {
        vector<int> res(distance + 1, 0);
        return res;
    }

    // If node is a leaf node and return res
    if (root->left == NULL &&
       root->right == NULL)
    {
        vector<int> res(distance + 1, 0);
        res[1]++;
        return res;
    }

    // Traverse to the left
    vector<int> left = dfs(root->left,
                           distance);

    // Traverse to the right
    vector<int> right = dfs(root->right,
                            distance);

    vector<int> res(distance + 1, 0);

    // Update the distance between left
    // and right leaf node
    for(int i = res.size() - 2;
            i >= 1; i--)
        res[i + 1] = left[i]+ right[i];

    // Count all pair of leaf nodes
    // which are at most K distance apart
    for(int l = 1;l < left.size(); l++)
    {
        for(int r = 0;r < right.size(); r++)
        {
            if (l + r <= distance)
            {
                result += left[l] * right[r];
            }
        }
    }

    // Return res to parent node
    return res;
}

// Driver Code
int main()
{

    /*
         1
        / \
       2   3
      /
    4
    */

    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);

    // Given distance K
    int K = 3;

    // Function call
    dfs(root, K);

    cout << result;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach

// Structure of a Node
class Node {
    int data;
    Node left, right;

    // Constructor of the class
    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

public class GFG {
    Node root;

    // Stores the count of required pairs
    static int result;

    // Function to perform dfs to find pair of
    // leaf nodes at most K distance apart
    static int[] dfs(Node root, int distance)
    {
        // Return empty array if node is null
        if (root == null)
            return new int[distance + 1];

        // If node is a leaf node and return res
        if (root.left == null
            && root.right == null) {
            int res[] = new int[distance + 1];
            res[1]++;
            return res;
        }

        // Traverse to the left
        int[] left = dfs(root.left,
                         distance);

        // Traverse to the right
        int[] right = dfs(root.right,
                          distance);

        int res[] = new int[distance + 1];

        // Update the distance between left
        // and right leaf node
        for (int i = res.length - 2;
             i >= 1; i--) {
            res[i + 1] = left[i]
                         + right[i];
        }

        // Count all pair of leaf nodes
        // which are at most K distance apart
        for (int l = 1;
             l < left.length; l++) {

            for (int r = 0;
                 r < right.length; r++) {

                if (l + r <= distance) {
                    result += left[l]
                              * right[r];
                }
            }
        }

        // Return res to parent node
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        GFG tree = new GFG();

        /*
                1
               /  \
             2     3
            / 
           4   
       */

        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);

        tree.root.left.left = new Node(4);
        result = 0;

        // Given distance K
        int K = 3;

        // Function Call
        dfs(tree.root, K);

        System.out.println(result);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Structure of a Node
class newNode:

    def __init__(self, item):

        self.data =  item
        self.left = None
        self.right = None

# Stores the count of required pairs
result = 0

# Function to perform dfs to find pair of
# leaf nodes at most K distance apart
def dfs(root, distance):

    global result

    # Return empty array if node is None
    if (root == None):
        res = [0 for i in range(distance + 1)]
        return res

    # If node is a leaf node and return res
    if (root.left == None and root.right == None):
        res = [0 for i in range(distance + 1)]
        res[1] += 1
        return res

    # Traverse to the left
    left = dfs(root.left, distance)

    # Traverse to the right
    right = dfs(root.right, distance)

    res = [0 for i in range(distance + 1)]

    # Update the distance between left
    # and right leaf node
    i = len(res) - 2

    while(i >= 1):
        res[i + 1] = left[i] + right[i]
        i -= 1

    # Count all pair of leaf nodes
    # which are at most K distance apart
    for l in range(1, len(left)):
        for r in range(len(right)):
            if (l + r <= distance):
                result += left[l] * right[r]

    # Return res to parent node
    return res

# Driver Code
if __name__ == '__main__':

    '''
         1
        / \
       2   3
      /
    4
    '''
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)

    # Given distance K
    K = 3

    # Function call
    dfs(root, K)

    print(result)

# This code is contributed by ipg2016107
```

## C#

```
// C# implementation of the
// above approach
using System;

// Structure of a Node
class Node{

  public int data;
  public Node left, right;

  // Constructor of the class
  public Node(int item)
  {
    data = item;
    left = right = null;
  }
}

class GFG{

Node root;

// Stores the count of
// required pairs
static int result;

// Function to perform
// dfs to find pair of
// leaf nodes at most K
// distance apart
static int[] dfs(Node root,
                 int distance)
{
  int []res;
  // Return empty array if
  //  node is null
  if (root == null)
    return new int[distance + 1];

  // If node is a leaf node
  //and return res
  if (root.left == null &&
      root.right == null)
  {
    res = new int[distance + 1];
    res[1]++;
    return res;
  }

  // Traverse to the left
  int[] left = dfs(root.left,
                   distance);

  // Traverse to the right
  int[] right = dfs(root.right,
                    distance);

  res = new int[distance + 1];

  // Update the distance between left
  // and right leaf node
  for (int i = res.Length - 2;
           i >= 1; i--)
  {
    res[i + 1] = left[i] + right[i];
  }

  // Count all pair of leaf nodes
  // which are at most K distance apart
  for (int l = 1; l < left.Length; l++)
  {
    for (int r = 0; r < right.Length; r++)
    {
      if (l + r <= distance)
      {
        result += left[l] * right[r];
      }
    }
  }

  // Return res to parent node
  return res;
}

    // Driver Code
public static void Main(String[] args)
{
  GFG tree = new GFG();

  /*
                1
               /  \
             2     3
            / 
           4   
       */

  tree.root = new Node(1);
  tree.root.left = new Node(2);
  tree.root.right = new Node(3);

  tree.root.left.left = new Node(4);
  result = 0;

  // Given distance K
  int K = 3;

  // Function Call
  dfs(tree.root, K);

  Console.WriteLine(result);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    // Structure of a Node
    class Node
    {
        constructor(item) {
           this.left = null;
           this.right = null;
           this.data = item;
        }
    }

    let root;

    class GFG{
    }

    // Stores the count of required pairs
    let result;

    // Function to perform dfs to find pair of
    // leaf nodes at most K distance apart
    function dfs(root, distance)
    {
        // Return empty array if node is null
        if (root == null)
        {
            let arr = new Array(distance + 1);
            arr.fill(0);
            return arr;
        }

        // If node is a leaf node and return res
        if (root.left == null
            && root.right == null) {
            let res = new Array(distance + 1);
            res.fill(0);
            res[1]++;
            return res;
        }

        // Traverse to the left
        let left = dfs(root.left, distance);

        // Traverse to the right
        let right = dfs(root.right, distance);

        let res = new Array(distance + 1);
        res.fill(0);

        // Update the distance between left
        // and right leaf node
        for (let i = res.length - 2; i >= 1; i--) {
            res[i + 1] = left[i] + right[i];
        }

        // Count all pair of leaf nodes
        // which are at most K distance apart
        for (let l = 1; l < left.length; l++) {

            for (let r = 0; r < right.length; r++) {

                if (l + r <= distance) {
                    result += left[l] * right[r];
                }
            }
        }

        // Return res to parent node
        return res;
    }

    let tree = new GFG();

    /*
                  1
                 /  \
               2     3
              /
             4  
         */

    tree.root = new Node(1);
    tree.root.left = new Node(2);
    tree.root.right = new Node(3);

    tree.root.left.left = new Node(4);
    result = 0;

    // Given distance K
    let K = 3;

    // Function Call
    dfs(tree.root, K);

    document.write(result);

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N + E)，其中 N 为*二叉树*、*中*的节点数，E 为边数。**辅助空间:** O(H)，其中 H 为**二叉树的高度。*