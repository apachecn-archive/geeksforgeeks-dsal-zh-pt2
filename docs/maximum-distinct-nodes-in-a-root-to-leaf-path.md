# 根到叶路径中最大不同节点数

> 原文:[https://www . geeksforgeeks . org/maximum-distinct-nodes-in-a-root-to-leaf-path/](https://www.geeksforgeeks.org/maximum-distinct-nodes-in-a-root-to-leaf-path/)

给定一棵二叉树，找出所有根到叶路径中不同节点的数量，并打印最大值。
**例:**

```
Input :   1
        /    \
       2      3
      / \    / \
     4   5  6   3
             \   \
              8   9 
Output : 4 
The root to leaf path with maximum distinct
nodes is 1-3-6-8.
```

一个**简单的解决方案**是[探索所有根到叶的路径](https://www.geeksforgeeks.org/given-a-binary-tree-print-all-root-to-leaf-paths/)。在每个根到叶路径中，计算不同的节点，最后返回最大计数。
一个有效的解决方案**是使用哈希。我们递归遍历树，并保持从根到当前节点的路径上不同节点的计数。我们对左右子树进行递归，最终返回两个最大值。
以下是上述想法的实现** 

## C++

```
// C++ program to find count of distinct nodes
// on a path with maximum distinct nodes.
#include <bits/stdc++.h>
using namespace std;

// A node of binary tree
struct Node {
    int data;
    struct Node *left, *right;
};

// A utility function to create a new Binary
// Tree node
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

int largestUinquePathUtil(Node* node, unordered_map<int, int> m)
{
    if (!node)
        return m.size();

    // put this node into hash
    m[node->data]++;

    int max_path = max(largestUinquePathUtil(node->left, m),
                       largestUinquePathUtil(node->right, m));

    // remove current node from path "hash"
    m[node->data]--;

    // if we reached a condition where all duplicate value
    // of current node is deleted
    if (m[node->data] == 0)
        m.erase(node->data);

    return max_path;
}

// A utility function to find long unique value path
int largestUinquePath(Node* node)
{
    if (!node)
        return 0;

    // hash that store all node value
    unordered_map<int, int> hash;

    // return max length unique value path
    return largestUinquePathUtil(node, hash);
}

// Driver program to test above functions
int main()
{
    // Create binary tree shown in above figure
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->left->right = newNode(8);
    root->right->right->right = newNode(9);

    cout << largestUinquePath(root) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of distinct nodes
// on a path with maximum distinct nodes.
import java.util.*;
class GFG
{

// A node of binary tree
static class Node
{
    int data;
    Node left, right;
};

// A utility function to create a new Binary
// Tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

static int largestUinquePathUtil(Node node, HashMap<Integer,
                                                    Integer> m)
{
    if (node == null)
        return m.size();

    // put this node into hash
    if(m.containsKey(node.data))
    {
        m.put(node.data, m.get(node.data) + 1);
    }
    else
    {
        m.put(node.data, 1);
    }

    int max_path = Math.max(largestUinquePathUtil(node.left, m),
                            largestUinquePathUtil(node.right, m));

    // remove current node from path "hash"
    if(m.containsKey(node.data))
    {
        m.put(node.data, m.get(node.data) - 1);
    }

    // if we reached a condition where all duplicate value
    // of current node is deleted
    if (m.get(node.data) == 0)
        m.remove(node.data);

    return max_path;
}

// A utility function to find long unique value path
static int largestUinquePath(Node node)
{
    if (node == null)
        return 0;

    // hash that store all node value
    HashMap<Integer,
            Integer> hash = new HashMap<Integer,
                                        Integer>();

    // return max length unique value path
    return largestUinquePathUtil(node, hash);
}

// Driver Code
public static void main(String[] args)
{
    // Create binary tree shown in above figure
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.right.left.right = newNode(8);
    root.right.right.right = newNode(9);

    System.out.println(largestUinquePath(root));   
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find count of
# distinct nodes on a path with
# maximum distinct nodes.

# A utility class to create a
# new Binary Tree node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

def largestUinquePathUtil(node, m):
    if (not node):
        return len(m)

    # put this node into hash
    if node.data in m:
        m[node.data] += 1
    else:
        m[node.data] = 1

    max_path = max(largestUinquePathUtil(node.left, m),
                   largestUinquePathUtil(node.right, m))

    # remove current node from path "hash"
    m[node.data] -= 1

    # if we reached a condition
    # where all duplicate value
    # of current node is deleted
    if (m[node.data] == 0):
        del m[node.data]

    return max_path

# A utility function to find
# long unique value path
def largestUinquePath(node):
    if (not node):
        return 0

    # hash that store all node value
    Hash = {}

    # return max length unique value path
    return largestUinquePathUtil(node, Hash)

# Driver Code
if __name__ == '__main__':

    # Create binary tree shown
    # in above figure
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.left = newNode(6)
    root.right.right = newNode(7)
    root.right.left.right = newNode(8)
    root.right.right.right = newNode(9)

    print(largestUinquePath(root))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find count of distinct nodes
// on a path with maximum distinct nodes.
using System;
using System.Collections.Generic;

class GFG
{

// A node of binary tree
public class Node
{
    public int data;
    public Node left, right;
};

// A utility function to create a new Binary
// Tree node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

static int largestUinquePathUtil(Node node,
                                 Dictionary<int, int> m)
{
    if (node == null)
        return m.Count;

    // put this node into hash
    if(m.ContainsKey(node.data))
    {
        m[node.data] = m[node.data] + 1;
    }
    else
    {
        m.Add(node.data, 1);
    }

    int max_path = Math.Max(largestUinquePathUtil(node.left, m),
                            largestUinquePathUtil(node.right, m));

    // remove current node from path "hash"
    if(m.ContainsKey(node.data))
    {
        m[node.data] = m[node.data] - 1;
    }

    // if we reached a condition where all
    // duplicate value of current node is deleted
    if (m[node.data] == 0)
        m.Remove(node.data);

    return max_path;
}

// A utility function to find long unique value path
static int largestUinquePath(Node node)
{
    if (node == null)
        return 0;

    // hash that store all node value
    Dictionary<int,    
               int> hash = new Dictionary<int,
                                          int>();

    // return max length unique value path
    return largestUinquePathUtil(node, hash);
}

// Driver Code
public static void Main(String[] args)
{

    // Create binary tree shown in above figure
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.right.left.right = newNode(8);
    root.right.right.right = newNode(9);

    Console.WriteLine(largestUinquePath(root));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program to find count of distinct nodes
    // on a path with maximum distinct nodes.

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // A utility function to create a new Binary
    // Tree node
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    function largestUinquePathUtil(node, m)
    {
        if (node == null)
            return m.size;

        // put this node into hash
        if(m.has(node.data))
        {
            m.set(node.data, m.get(node.data) + 1);
        }
        else
        {
            m.set(node.data, 1);
        }

        let max_path = Math.max(largestUinquePathUtil(node.left, m),
                                largestUinquePathUtil(node.right, m));

        // remove current node from path "hash"
        if(m.has(node.data))
        {
            m.set(node.data, m.get(node.data) - 1);
        }

        // if we reached a condition where all duplicate value
        // of current node is deleted
        if (m.get(node.data) == 0)
            m.delete(node.data);

        return max_path;
    }

    // A utility function to find long unique value path
    function largestUinquePath(node)
    {
        if (node == null)
            return 0;

        // hash that store all node value
        let hash = new Map();

        // return max length unique value path
        return largestUinquePathUtil(node, hash);
    }

    // Create binary tree shown in above figure
    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.right.left.right = newNode(8);
    root.right.right.right = newNode(9);

    document.write(largestUinquePath(root));   

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(n)

本文由[尼尚辛格](https://www.facebook.com/nishant.chaudhary.7334)供稿。如果你喜欢极客博客并想投稿，你也可以用 write.geeksforgeeks.org 写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。