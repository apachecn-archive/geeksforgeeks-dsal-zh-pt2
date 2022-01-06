# 二叉树中连接两个节点的路径上的最小和最大节点

> 原文:[https://www . geeksforgeeks . org/位于连接二叉树中两个节点的路径中的最小和最大节点/](https://www.geeksforgeeks.org/minimum-and-maximum-node-that-lies-in-the-path-connecting-two-nodes-in-a-binary-tree/)

给定一棵二叉树和两个节点 **a** 和 **b** ，任务是打印位于连接给定节点 **a** 和 **b** 的路径中的最小和最大节点值。如果树中不存在这两个节点中的任何一个，则打印 **-1** 的最小值和最大值。

**示例:**

```
Input:
          1
         /  \
        2    3
       / \    \
      4   5    6
         /    / \
        7    8   9
a = 5, b = 6
Output:
Min = 1
Max = 6

Input:
           20
         /   \
        8     22
      /   \  /   \
     5     3 4    25
          / \
         10  14
a = 5, b = 14
Output:
Min = 3
Max = 14
```

**方法:**思路是找到两个节点的 [LCA](https://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/) 。然后开始在从 LCA 到第一个节点，然后从 LCA 到第二个节点的路径中搜索最小值和最大值节点，并打印这些值的最小值和最大值。如果任一节点不在树中，则打印 **-1** 的最小值和最大值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Structure of binary tree
struct Node {
    Node* left;
    Node* right;
    int data;
};

// Function to create a new node
Node* newNode(int key)
{
    Node* node = new Node();
    node->left = node->right = NULL;
    node->data = key;
    return node;
}

// Function to store the path from root node
// to given node of the tree in path vector and
// then returns true if the path exists
// otherwise false
bool FindPath(Node* root, vector<int>& path, int key)
{
    if (root == NULL)
        return false;

    path.push_back(root->data);

    if (root->data == key)
        return true;

    if (FindPath(root->left, path, key)
        || FindPath(root->right, path, key))
        return true;

    path.pop_back();
    return false;
}

// Function to print the minimum and the maximum
// value present in the path connecting the
// given two nodes of the given binary tree
int minMaxNodeInPath(Node* root, int a, int b)
{

    // To store the path from the root node to a
    vector<int> Path1;

    // To store the path from the root node to b
    vector<int> Path2;

    // To store the minimum and the maximum value
    // in the path from LCA to a
    int min1 = INT_MAX;
    int max1 = INT_MIN;

    // To store the minimum and the maximum value
    // in the path from LCA to b
    int min2 = INT_MAX;
    int max2 = INT_MIN;

    int i = 0;
    int j = 0;

    // If both a and b are present in the tree
    if (FindPath(root, Path1, a) && FindPath(root, Path2, b)) {

        // Compare the paths to get the first different value
        for (i = 0; i < Path1.size() && Path2.size(); i++)
            if (Path1[i] != Path2[i])
                break;

        i--;
        j = i;

        // Find minimum and maximum value
        // in the path from LCA to a
        for (; i < Path1.size(); i++) {
            if (min1 > Path1[i])
                min1 = Path1[i];
            if (max1 < Path1[i])
                max1 = Path1[i];
        }

        // Find minimum and maximum value
        // in the path from LCA to b
        for (; j < Path2.size(); j++) {
            if (min2 > Path2[j])
                min2 = Path2[j];
            if (max2 < Path2[j])
                max2 = Path2[j];
        }

        // Minimum of min values in first
        // path and second path
        cout << "Min = " << min(min1, min2) << endl;

        // Maximum of max values in first
        // path and second path
        cout << "Max = " << max(max1, max2);
    }

    // If no path exists
    else
        cout << "Min = -1\nMax = -1";
}

// Driver Code
int main()
{
    Node* root = newNode(20);
    root->left = newNode(8);
    root->right = newNode(22);
    root->left->left = newNode(5);
    root->left->right = newNode(3);
    root->right->left = newNode(4);
    root->right->right = newNode(25);
    root->left->right->left = newNode(10);
    root->left->right->right = newNode(14);

    int a = 5;
    int b = 1454;

    minMaxNodeInPath(root, a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Structure of binary tree
static class Node
{
    Node left;
    Node right;
    int data;
};

// Function to create a new node
static Node newNode(int key)
{
    Node node = new Node();
    node.left = node.right = null;
    node.data = key;
    return node;
}

static Vector<Integer> path;

// Function to store the path from root node
// to given node of the tree in path vector and
// then returns true if the path exists
// otherwise false
static boolean FindPath(Node root, int key)
{
    if (root == null)
        return false;

    path.add(root.data);

    if (root.data == key)
        return true;

    if (FindPath(root.left, key)
        || FindPath(root.right, key))
        return true;

    path.remove(path.size()-1);
    return false;
}

// Function to print the minimum and the maximum
// value present in the path connecting the
// given two nodes of the given binary tree
static int minMaxNodeInPath(Node root, int a, int b)
{

    // To store the path from the root node to a
    path = new Vector<Integer> ();
    boolean flag = true;

    // To store the path from the root node to b
    Vector<Integer> Path2 = new Vector<Integer>(),
                    Path1 = new Vector<Integer>();

    // To store the minimum and the maximum value
    // in the path from LCA to a
    int min1 = Integer.MAX_VALUE;
    int max1 = Integer.MIN_VALUE;

    // To store the minimum and the maximum value
    // in the path from LCA to b
    int min2 = Integer.MAX_VALUE;
    int max2 = Integer.MIN_VALUE;

    int i = 0;
    int j = 0;

    flag = FindPath(root, a);
    Path1 = path;

    path = new Vector<Integer>();

    flag&= FindPath(root, b);
    Path2 = path;

    // If both a and b are present in the tree
    if ( flag)
    {

        // Compare the paths to get the first different value
        for (i = 0; i < Path1.size() && i < Path2.size(); i++)
            if (Path1.get(i) != Path2.get(i))
                break;

        i--;
        j = i;

        // Find minimum and maximum value
        // in the path from LCA to a
        for (; i < Path1.size(); i++)
        {
            if (min1 > Path1.get(i))
                min1 = Path1.get(i);
            if (max1 < Path1.get(i))
                max1 = Path1.get(i);
        }

        // Find minimum and maximum value
        // in the path from LCA to b
        for (; j < Path2.size(); j++)
        {
            if (min2 > Path2.get(j))
                min2 = Path2.get(j);
            if (max2 < Path2.get(j))
                max2 = Path2.get(j);
        }

        // Minimum of min values in first
        // path and second path
        System.out.println( "Min = " + Math.min(min1, min2) );

        // Maximum of max values in first
        // path and second path
        System.out.println( "Max = " + Math.max(max1, max2));
    }

    // If no path exists
    else
        System.out.println("Min = -1\nMax = -1");
    return 0;
}

// Driver Code
public static void main(String args[])
{
    Node root = newNode(20);
    root.left = newNode(8);
    root.right = newNode(22);
    root.left.left = newNode(5);
    root.left.right = newNode(3);
    root.right.left = newNode(4);
    root.right.right = newNode(25);
    root.left.right.left = newNode(10);
    root.left.right.right = newNode(14);

    int a = 5;
    int b = 14;

    minMaxNodeInPath(root, a, b);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

class Node:

    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Function to store the path from root
# node to given node of the tree in
# path vector and then returns true if
# the path exists otherwise false
def FindPath(root, path, key):

    if root == None:
        return False

    path.append(root.data)

    if root.data == key:
        return True

    if (FindPath(root.left, path, key) or
        FindPath(root.right, path, key)):
        return True

    path.pop()
    return False

# Function to print the minimum and the
# maximum value present in the path
# connecting the given two nodes of the
# given binary tree
def minMaxNodeInPath(root, a, b):

    # To store the path from the
    # root node to a
    Path1 = []

    # To store the path from the
    # root node to b
    Path2 = []

    # To store the minimum and the maximum
    # value in the path from LCA to a
    min1, max1 = float('inf'), float('-inf')

    # To store the minimum and the maximum
    # value in the path from LCA to b
    min2, max2 = float('inf'), float('-inf')

    i, j = 0, 0

    # If both a and b are present in the tree
    if (FindPath(root, Path1, a) and
        FindPath(root, Path2, b)):

        # Compare the paths to get the
        # first different value
        while i < len(Path1) and i < len(Path2):
            if Path1[i] != Path2[i]:
                break
            i += 1

        i -= 1
        j = i

        # Find minimum and maximum value
        # in the path from LCA to a
        while i < len(Path1):
            if min1 > Path1[i]:
                min1 = Path1[i]
            if max1 < Path1[i]:
                max1 = Path1[i]
            i += 1

        # Find minimum and maximum value
        # in the path from LCA to b
        while j < len(Path2):
            if min2 > Path2[j]:
                min2 = Path2[j]
            if max2 < Path2[j]:
                max2 = Path2[j]
            j += 1

        # Minimum of min values in first
        # path and second path
        print("Min =", min(min1, min2))

        # Maximum of max values in first
        # path and second path
        print("Max =", max(max1, max2))

    # If no path exists
    else:
        print("Min = -1\nMax = -1")

# Driver Code
if __name__ == "__main__":

    root = Node(20)
    root.left = Node(8)
    root.right = Node(22)
    root.left.left = Node(5)
    root.left.right = Node(3)
    root.right.left = Node(4)
    root.right.right = Node(25)
    root.left.right.left = Node(10)
    root.left.right.right = Node(14)

    a, b = 5, 14

    minMaxNodeInPath(root, a, b)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;

class GFG{

// Structure of binary tree
class Node
{
    public Node left;
    public Node right;
    public int data;
};

// Function to create a new node
static Node newNode(int key)
{
    Node node = new Node();
    node.left = node.right = null;
    node.data = key;
    return node;
}

static ArrayList path;

// Function to store the path from root
// node to given node of the tree in path
// vector and then returns true if the
// path exists otherwise false
static bool FindPath(Node root, int key)
{
    if (root == null)
        return false;

    path.Add(root.data);

    if (root.data == key)
        return true;

    if (FindPath(root.left, key) ||
        FindPath(root.right, key))
        return true;

    path.Remove((int)path[path.Count - 1]);
    return false;
}

// Function to print the minimum and the maximum
// value present in the path connecting the
// given two nodes of the given binary tree
static int minMaxNodeInPath(Node root, int a,
                                       int b)
{

    // To store the path from the root node to a
    path = new ArrayList();
    bool flag = true;

    // To store the path from the root node to b
    ArrayList Path2 = new ArrayList();
    ArrayList Path1 = new ArrayList();

    // To store the minimum and the maximum value
    // in the path from LCA to a
    int min1 = Int32.MaxValue;
    int max1 = Int32.MinValue;

    // To store the minimum and the maximum value
    // in the path from LCA to b
    int min2 = Int32.MaxValue;
    int max2 = Int32.MinValue;

    int i = 0;
    int j = 0;

    flag = FindPath(root, a);
    Path1 = path;

    path = new ArrayList();

    flag &= FindPath(root, b);
    Path2 = path;

    // If both a and b are present in the tree
    if (flag)
    {

        // Compare the paths to get the
        // first different value
        for(i = 0; i < Path1.Count &&
                   i < Path2.Count; i++)
            if ((int)Path1[i] != (int)Path2[i])
                break;

        i--;
        j = i;

        // Find minimum and maximum value
        // in the path from LCA to a
        for(; i < Path1.Count; i++)
        {
            if (min1 > (int)Path1[i])
                min1 = (int)Path1[i];
            if (max1 < (int)Path1[i])
                max1 = (int)Path1[i];
        }

        // Find minimum and maximum value
        // in the path from LCA to b
        for(; j < Path2.Count; j++)
        {
            if (min2 > (int)Path2[j])
                min2 = (int)Path2[j];
            if (max2 < (int)Path2[j])
                max2 = (int)Path2[j];
        }

        // Minimum of min values in first
        // path and second path
        Console.Write("Min = " +
                      Math.Min(min1, min2) + "\n" );

        // Maximum of max values in first
        // path and second path
        Console.Write("Max = " +
                      Math.Max(max1, max2) + "\n");
    }

    // If no path exists
    else
        Console.Write("Min = -1\nMax = -1");
    return 0;
}

// Driver Code
public static void Main(string []arg)
{
    Node root = newNode(20);
    root.left = newNode(8);
    root.right = newNode(22);
    root.left.left = newNode(5);
    root.left.right = newNode(3);
    root.right.left = newNode(4);
    root.right.right = newNode(25);
    root.left.right.left = newNode(10);
    root.left.right.right = newNode(14);

    int a = 5;
    int b = 14;

    minMaxNodeInPath(root, a, b);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Structure of binary tree
    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.data = key;
        }
    }

    // Function to create a new node
    function newNode(key)
    {
        let node = new Node(key);
        return node;
    }

    let path = [];

    // Function to store the path from root node
    // to given node of the tree in path vector and
    // then returns true if the path exists
    // otherwise false
    function FindPath(root, key)
    {
        if (root == null)
            return false;

        path.push(root.data);

        if (root.data == key)
            return true;

        if (FindPath(root.left, key)
            || FindPath(root.right, key))
            return true;

        path.pop();
        return false;
    }

    // Function to print the minimum and the maximum
    // value present in the path connecting the
    // given two nodes of the given binary tree
    function minMaxNodeInPath(root, a, b)
    {

        // To store the path from the root node to a
        path = [];
        let flag = true;

        // To store the path from the root node to b
        let Path2 = [], Path1 = [];

        // To store the minimum and the maximum value
        // in the path from LCA to a
        let min1 = Number.MAX_VALUE;
        let max1 = Number.MIN_VALUE;

        // To store the minimum and the maximum value
        // in the path from LCA to b
        let min2 = Number.MAX_VALUE;
        let max2 = Number.MIN_VALUE;

        let i = 0;
        let j = 0;

        flag = FindPath(root, a);
        Path1 = path;

        path = [];

        flag&= FindPath(root, b);
        Path2 = path;

        // If both a and b are present in the tree
        if ( flag)
        {

            // Compare the paths to get the first different value
            for (i = 0; i < Path1.length && i < Path2.length; i++)
                if (Path1[i] != Path2[i])
                    break;

            i--;
            j = i;

            // Find minimum and maximum value
            // in the path from LCA to a
            for (; i < Path1.length; i++)
            {
                if (min1 > Path1[i])
                    min1 = Path1[i];
                if (max1 < Path1[i])
                    max1 = Path1[i];
            }

            // Find minimum and maximum value
            // in the path from LCA to b
            for (; j < Path2.length; j++)
            {
                if (min2 > Path2[j])
                    min2 = Path2[j];
                if (max2 < Path2[j])
                    max2 = Path2[j];
            }

            // Minimum of min values in first
            // path and second path
            document.write( "Min = " + Math.min(min1, min2) +
            "</br>");

            // Maximum of max values in first
            // path and second path
            document.write( "Max = " + Math.max(max1, max2) +
            "</br>");
        }

        // If no path exists
        else
            document.write("Min = -1\nMax = -1" + "</br>");
        return 0;
    }

    let root = newNode(20);
    root.left = newNode(8);
    root.right = newNode(22);
    root.left.left = newNode(5);
    root.left.right = newNode(3);
    root.right.left = newNode(4);
    root.right.right = newNode(25);
    root.left.right.left = newNode(10);
    root.left.right.right = newNode(14);

    let a = 5;
    let b = 14;

    minMaxNodeInPath(root, a, b);

</script>
```

**Output:** 

```
Min = 3
Max = 14
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)