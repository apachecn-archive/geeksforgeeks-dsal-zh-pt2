# 使用 BFS

计算二叉树的每个节点到根节点的距离

> 原文:[https://www . geeksforgeeks . org/使用-bfs/从根节点到二叉树每个节点的距离/](https://www.geeksforgeeks.org/distance-of-each-node-of-a-binary-tree-from-the-root-node-using-bfs/)

给定一个由值在**【1，N】**范围内的 **N** 个节点组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是找到从根节点到树的每个节点的距离。

**示例:**

> **输入:**
> 
> ```
>                   1
>                  /  \
>                 2   3 
>                / \   \
>              4   5   6
> ```
> 
> **输出:**0 1 2 2 2
> T3】说明:T5】根到节点 1 的距离为 0。
> 根到节点 2 的距离为 1。
> 根到节点 3 的距离为 1。
> 根到节点 4 的距离为 2。
> 根到节点 5 的距离为 2。
> 根到节点 6 的距离为 2。
> 
> **输入:**
> 
> ```
>                   5
>                  / \
>                4    6
>              /  \     
>             3    7
>           / \     
>         1    2
> ```
> 
> **输出:**3 3 1 0 1 2

**方法:**使用 [BFS 手法](https://www.geeksforgeeks.org/level-order-tree-traversal/)可以解决问题。这个想法是利用从根到一个节点的距离等于二叉树中该节点的[级别的事实。按照以下步骤解决问题:](https://www.geeksforgeeks.org/get-level-of-a-node-in-a-binary-tree/)

*   初始化一个队列，比如说 **Q** ，来存储树中每一层的节点。
*   初始化一个数组，比如 **dist[]** ，其中 **dist[i]** 存储从根节点到树的 **i <sup>th</sup>** 的距离。
*   [使用 BFS](https://www.geeksforgeeks.org/level-order-tree-traversal/) 遍历树。对于遇到的每个**I<sup>th</sup>T5】节点，更新**dist【I】**到二叉树中该节点的级别。**
*   最后，打印 **dist[]** 数组。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;
struct Node {

    // Stores data value
    // of the node
    int data;

    // Stores left subtree
    // of a node
    Node* left;

    // Stores right subtree
    // of a node
    Node* right;

    Node(int x)
    {

        data = x;
        left = right = NULL;
    }
};

void findDistance(Node* root, int N)
{

    // Store nodes at each level
    // of the binary tree
    queue<Node*> Q;

    // Insert root into Q
    Q.push(root);

    // Stores level of a node
    int level = 0;

    // dist[i]: Stores the distance
    // from root node to node i
    int dist[N + 1];

    // Traverse tree using BFS
    while (!Q.empty()) {

        // Stores count of nodes
        // at current level
        int M = Q.size();

        // Traverse the nodes at
        // current level
        for (int i = 0; i < M; i++) {

            // Stores front element
            // of the queue
            root = Q.front();

            // Pop front element
            // of the queue
            Q.pop();

            // Stores the distance from
            // root node to current node
            dist[root->data] = level;

            if (root->left) {

                // Push left subtree
                Q.push(root->left);
            }

            if (root->right) {

                // Push right subtree
                Q.push(root->right);
            }
        }

        // Update level
        level += 1;
    }

    for (int i = 1; i <= N; i++) {

        cout << dist[i] << " ";
    }
}

// Driver Code
int main()
{

    int N = 7;
    Node* root = new Node(5);
    root->left = new Node(4);
    root->right = new Node(6);
    root->left->left = new Node(3);
    root->left->right = new Node(7);
    root->left->left->left = new Node(1);
    root->left->left->right = new Node(2);
    findDistance(root, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG
{
static class Node
{

    // Stores data value
    // of the node
    int data;

    // Stores left subtree
    // of a node
    Node left;

    // Stores right subtree
    // of a node
    Node right;
    Node(int x)
    {
        data = x;
        left = right = null;
    }
};

static void findDistance(Node root, int N)
{

    // Store nodes at each level
    // of the binary tree
    Queue<Node> Q = new LinkedList<>();

    // Insert root into Q
    Q.add(root);

    // Stores level of a node
    int level = 0;

    // dist[i]: Stores the distance
    // from root node to node i
    int []dist = new int[N + 1];

    // Traverse tree using BFS
    while (!Q.isEmpty())
    {

        // Stores count of nodes
        // at current level
        int M = Q.size();

        // Traverse the nodes at
        // current level
        for (int i = 0; i < M; i++)
        {

            // Stores front element
            // of the queue
            root = Q.peek();

            // Pop front element
            // of the queue
            Q.remove();

            // Stores the distance from
            // root node to current node
            dist[root.data] = level;

            if (root.left != null)
            {

                // Push left subtree
                Q.add(root.left);
            }

            if (root.right != null)
            {

                // Push right subtree
                Q.add(root.right);
            }
        }

        // Update level
        level += 1;
    }

    for (int i = 1; i <= N; i++)
    {
        System.out.print(dist[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    int N = 7;
    Node root = new Node(5);
    root.left = new Node(4);
    root.right = new Node(6);
    root.left.left = new Node(3);
    root.left.right = new Node(7);
    root.left.left.left = new Node(1);
    root.left.left.right = new Node(2);
    findDistance(root, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
class Node:

    def __init__(self, data):

        # Stores data value
        # of the node
        self.data = data

        # Stores left subtree
        # of a node
        self.left = None

        # Stores right subtree
        # of a node
        self.right = None

def findDistance(root, N):

    # Store nodes at each level
    # of the binary tree
    Q = []

    # Insert root into Q
    Q.append(root)

    # Stores level of a node
    level = 0

    # dist[i]: Stores the distance
    # from root node to node i
    dist = [0 for i in range(N + 1)]

    # Traverse tree using BFS
    while Q:

        # Stores count of nodes
        # at current level
        M = len(Q)

        # Traverse the nodes at
        # current level
        for i in range(0, M):

            # Stores front element
            # of the queue
            root = Q[0]

            # Pop front element
            # of the queue
            Q.pop(0)

            #  Stores the distance from
            # root node to current node
            dist[root.data] = level

            if root.left:

                # Push left subtree
                Q.append(root.left)
            if root.right:

                # Push right subtree
                Q.append(root.right)

        # Update level
        level += 1

    for i in range(1, N + 1):
        print(dist[i], end = " ")

# Driver code
if __name__ == '__main__':

    N = 7
    root = Node(5)
    root.left = Node(4)
    root.right = Node(6)
    root.left.left = Node(3)
    root.left.right = Node(7)
    root.left.left.left = Node(1)
    root.left.left.right = Node(2)

    findDistance(root, N)

# This code is contributed by MuskanKalra1
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG
{
  class Node
  {

    // Stores data value
    // of the node
    public int data;

    // Stores left subtree
    // of a node
    public Node left;

    // Stores right subtree
    // of a node
    public Node right;
    public Node(int x)
    {
      data = x;
      left = right = null;
    }
  };

  static void findDistance(Node root, int N)
  {

    // Store nodes at each level
    // of the binary tree
    Queue<Node> Q = new Queue<Node>();

    // Insert root into Q
    Q.Enqueue(root);

    // Stores level of a node
    int level = 0;

    // dist[i]: Stores the distance
    // from root node to node i
    int []dist = new int[N + 1];

    // Traverse tree using BFS
    while (Q.Count != 0)
    {

      // Stores count of nodes
      // at current level
      int M = Q.Count;

      // Traverse the nodes at
      // current level
      for (int i = 0; i < M; i++)
      {

        // Stores front element
        // of the queue
        root = Q.Peek();

        // Pop front element
        // of the queue
        Q.Dequeue();

        // Stores the distance from
        // root node to current node
        dist[root.data] = level;

        if (root.left != null)
        {

          // Push left subtree
          Q.Enqueue(root.left);
        }

        if (root.right != null)
        {

          // Push right subtree
          Q.Enqueue(root.right);
        }
      }

      // Update level
      level += 1;
    }

    for (int i = 1; i <= N; i++)
    {
      Console.Write(dist[i] + " ");
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {

    int N = 7;
    Node root = new Node(5);
    root.left = new Node(4);
    root.right = new Node(6);
    root.left.left = new Node(3);
    root.left.right = new Node(7);
    root.left.left.left = new Node(1);
    root.left.left.right = new Node(2);
    findDistance(root, N);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

    // JavaScript program to implement the above approach

    // Structure of a tree node
    class Node
    {
        constructor(x) {
           this.left = null;
           this.right = null;
           this.data = x;
        }
    }

    function findDistance(root, N)
    {

        // Store nodes at each level
        // of the binary tree
        let Q = [];

        // Insert root into Q
        Q.push(root);

        // Stores level of a node
        let level = 0;

        // dist[i]: Stores the distance
        // from root node to node i
        let dist = new Array(N + 1);

        // Traverse tree using BFS
        while (Q.length > 0)
        {

            // Stores count of nodes
            // at current level
            let M = Q.length;

            // Traverse the nodes at
            // current level
            for (let i = 0; i < M; i++)
            {

                // Stores front element
                // of the queue
                root = Q[0];

                // Pop front element
                // of the queue
                Q.shift();

                // Stores the distance from
                // root node to current node
                dist[root.data] = level;

                if (root.left != null)
                {

                    // Push left subtree
                    Q.push(root.left);
                }

                if (root.right != null)
                {

                    // Push right subtree
                    Q.push(root.right);
                }
            }

            // Update level
            level += 1;
        }

        for (let i = 1; i <= N; i++)
        {
            document.write(dist[i] + " ");
        }
    }

    let N = 7;
    let root = new Node(5);
    root.left = new Node(4);
    root.right = new Node(6);
    root.left.left = new Node(3);
    root.left.right = new Node(7);
    root.left.left.left = new Node(1);
    root.left.left.right = new Node(2);
    findDistance(root, N);

</script>
```

**Output:** 

```
3 3 2 1 0 1 2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)