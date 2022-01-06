# 监控二叉树所有节点所需的最小摄像机数量

> 原文:[https://www . geesforgeks . org/监控二叉树所有节点所需的最小摄像机数量/](https://www.geeksforgeeks.org/minimum-number-of-cameras-required-to-monitor-all-nodes-of-a-binary-tree/)

给定一个由 **N** 个节点组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是找到监控整棵树所需的最少摄像机数量，使得放置在任何节点的每个摄像机都可以监控节点本身、其父节点及其直接子节点。

**示例:**

> **输入:**
> 0
> /
> 0
> /\
> 0 0
> **输出:** 1
> **说明:**
> 0
> /
> **0**<———摄像机
> /\
> 0
> 在上面的树中，加粗的节点就是有摄像机的节点。将摄像机放置在树的 1 级可以监控给定二叉树的所有节点。
> 因此，需要的摄像头最少数量为 1 个。
> 
> **输入:**
> 0
> /
> 0
> /
> 0
> \
> 0
> **输出:** 2

**方法:**给定的问题可以通过存储节点的状态来解决，无论摄像机是否已经放置，或者该节点是否被具有摄像机的任何其他节点监控。其思想是在给定的树上执行 [DFS 遍历，并返回每个](https://www.geeksforgeeks.org/dfs-traversal-of-a-tree-using-recursion/)[递归调用](https://www.geeksforgeeks.org/recursion/)中每个节点的状态。将以下转换视为函数返回的状态:

*   如果值为 **1** ，则监控该节点。
*   如果值为 **2** ，则不监控该节点。
*   如果值为 **3** ，则该节点有摄像机。

按照以下步骤解决问题:

*   初始化一个变量，比如**计数**来存储监控给定树的所有节点所需的最小摄像机数量。
*   创建一个[函数](https://www.geeksforgeeks.org/functions-in-c/)，比如 **dfs(root)** ，该函数获取给定树的根，并返回每个节点的状态，无论摄像机是否已经放置，或者该节点是否被任何其他具有摄像机的节点监控，并执行以下步骤:
    *   如果节点的值为**空**，则返回 **1** ，因为**空**节点始终被监控。
    *   [递归调用左右子树的](https://www.geeksforgeeks.org/recursion/)，并将它们返回的值存储在变量 **L** 和 **R** 中。
    *   如果 **L** 和 **R** 的值为 **1** ，则从当前递归调用返回 **2** ，因为当前根节点未被监控。
    *   如果 **L** 或 **R** 的值为 **2** ，则将**的值递增**计数 **1** 作为未监控的左右节点之一，并返回 **3** 。
    *   否则，返回 **1** 。
*   从根调用上面的递归函数，如果它返回的值是 **2** ，那么将**计数**的值增加 **1** 。
*   完成上述步骤后，打印**计数**的值作为相机的合成数量。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure for a Tree node
struct Node {
    int key;
    struct Node *left, *right;
};

// Function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;

    // Return the newly created node
    return (temp);
}

// Stores the minimum number of
// cameras required
int cnt = 0;

// Utility function to find minimum
// number of cameras required to
// monitor the entire tree
int minCameraSetupUtil(Node* root)
{
    // If root is NULL
    if (root == NULL)
        return 1;

    int L = minCameraSetupUtil(
        root->left);
    int R = minCameraSetupUtil(
        root->right);

    // Both the nodes are monitored
    if (L == 1 && R == 1)
        return 2;

    // If one of the left and the
    // right subtree is not monitored
    else if (L == 2 || R == 2) {
        cnt++;
        return 3;
    }

    // If the root node is monitored
    return 1;
}

// Function to find the minimum number
// of cameras required to monitor
// entire tree
void minCameraSetup(Node* root)
{
    int value = minCameraSetupUtil(root);

    // Print the count of cameras
    cout << cnt + (value == 2 ? 1 : 0);
}

// Driver Code
int main()
{
    // Given Binary Tree
    Node* root = newNode(0);
    root->left = newNode(0);
    root->left->left = newNode(0);
    root->left->left->left = newNode(0);
    root->left->left->left->right = newNode(0);

    minCameraSetup(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {
    // TreeNode class
    static class Node {
        public int key;
        public Node left, right;
    };

    static Node newNode(int key)
    {
        Node temp = new Node();
        temp.key = key;
        temp.left = temp.right = null;
        return temp;
    }

    // Stores the minimum number of
    // cameras required
    static int cnt = 0;

    // Utility function to find minimum
    // number of cameras required to
    // monitor the entire tree
    static int minCameraSetupUtil(Node root)
    {
        // If root is NULL
        if (root == null)
            return 1;

        int L = minCameraSetupUtil(root.left);
        int R = minCameraSetupUtil(root.right);

        // Both the nodes are monitored
        if (L == 1 && R == 1)
            return 2;

        // If one of the left and the
        // right subtree is not monitored
        else if (L == 2 || R == 2) {
            cnt++;
            return 3;
        }

        // If the root node is monitored
        return 1;
    }

    // Function to find the minimum number
    // of cameras required to monitor
    // entire tree
    static void minCameraSetup(Node root)
    {
        int value = minCameraSetupUtil(root);

        // Print the count of cameras
        System.out.println(cnt + (value == 2 ? 1 : 0));
    }

    // Driver code
    public static void main(String[] args)
    {
        // Given Binary Tree
        Node root = newNode(0);
        root.left = newNode(0);
        root.left.left = newNode(0);
        root.left.left.left = newNode(0);
        root.left.left.left.right = newNode(0);

        minCameraSetup(root);
    }
}
// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Structure for a Tree node
class Node:

    def __init__(self, k):

        self.key = k
        self.left = None
        self.right = None

# Stores the minimum number of
# cameras required
cnt = 0

# Utility function to find minimum
# number of cameras required to
# monitor the entire tree
def minCameraSetupUtil(root):

    global cnt

    # If root is None
    if (root == None):
        return 1

    L = minCameraSetupUtil(root.left)
    R = minCameraSetupUtil(root.right)

    # Both the nodes are monitored
    if (L == 1 and R == 1):
        return 2

    # If one of the left and the
    # right subtree is not monitored
    elif (L == 2 or R == 2):
        cnt += 1
        return 3

    # If the root node is monitored
    return 1

# Function to find the minimum number
# of cameras required to monitor
# entire tree
def minCameraSetup(root):

    value = minCameraSetupUtil(root)

    # Print the count of cameras
    print(cnt + (1 if value == 2 else 0))

# Driver Code
if __name__ == '__main__':

    # Given Binary Tree
    root = Node(0)
    root.left = Node(0)
    root.left.left = Node(0)
    root.left.left.left = Node(0)
    root.left.left.left.right = Node(0)

    minCameraSetup(root)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

    // TreeNode class
    class Node {
        public int key;
        public Node left, right;
    };

    static Node newNode(int key)
    {
        Node temp = new Node();
        temp.key = key;
        temp.left = temp.right = null;
        return temp;
    }

    // Stores the minimum number of
    // cameras required
    static int cnt = 0;

    // Utility function to find minimum
    // number of cameras required to
    // monitor the entire tree
    static int minCameraSetupUtil(Node root)
    {

        // If root is NULL
        if (root == null)
            return 1;

        int L = minCameraSetupUtil(root.left);
        int R = minCameraSetupUtil(root.right);

        // Both the nodes are monitored
        if (L == 1 && R == 1)
            return 2;

        // If one of the left and the
        // right subtree is not monitored
        else if (L == 2 || R == 2) {
            cnt++;
            return 3;
        }

        // If the root node is monitored
        return 1;
    }

    // Function to find the minimum number
    // of cameras required to monitor
    // entire tree
    static void minCameraSetup(Node root)
    {
        int value = minCameraSetupUtil(root);

        // Print the count of cameras
        Console.WriteLine(cnt + (value == 2 ? 1 : 0));
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Given Binary Tree
        Node root = newNode(0);
        root.left = newNode(0);
        root.left.left = newNode(0);
        root.left.left.left = newNode(0);
        root.left.left.left.right = newNode(0);

        minCameraSetup(root);
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // TreeNode class
    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.key = key;
        }
    }

    function newNode(key)
    {
        let temp = new Node(key);
        return temp;
    }

    // Stores the minimum number of
    // cameras required
    let cnt = 0;

    // Utility function to find minimum
    // number of cameras required to
    // monitor the entire tree
    function minCameraSetupUtil(root)
    {

        // If root is NULL
        if (root == null)
            return 1;

        let L = minCameraSetupUtil(root.left);
        let R = minCameraSetupUtil(root.right);

        // Both the nodes are monitored
        if (L == 1 && R == 1)
            return 2;

        // If one of the left and the
        // right subtree is not monitored
        else if (L == 2 || R == 2) {
            cnt++;
            return 3;
        }

        // If the root node is monitored
        return 1;
    }

    // Function to find the minimum number
    // of cameras required to monitor
    // entire tree
    function minCameraSetup(root)
    {
        let value = minCameraSetupUtil(root);

        // Print the count of cameras
        document.write(cnt + (value == 2 ? 1 : 0) + "</br>");
    }

    // Given Binary Tree
    let root = newNode(0);
    root.left = newNode(0);
    root.left.left = newNode(0);
    root.left.left.left = newNode(0);
    root.left.left.left.right = newNode(0);

    minCameraSetup(root);

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*
***辅助空间:** O(H)，其中 H 是给定树的* [*高度*](https://www.geeksforgeeks.org/write-a-c-program-to-find-the-maximum-depth-or-height-of-a-tree/) 。