# 计算一个图中邻居之和最多为 K 的节点数

> 原文:[https://www . geesforgeks . org/count-图中节点数-其邻居总和最多为-k/](https://www.geeksforgeeks.org/count-the-number-of-nodes-in-a-graph-whose-sum-of-neighbors-is-at-most-k/)

给定一个[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/) **根，**和一个值 **K，**任务是找出图中邻居之和小于 **K.** 的节点数

**示例:**

> **输入:**根= 8k = 14
> /\
> 2—3 7—3
> /\ \
> 5 6 0
> \ \/\
> 1 2 6 9
> **输出:** 10
> **说明:**邻居之和小于 14 的节点为值为 8、7、6、9、3(最右侧)、2、5、1、6、2 的节点
> 
> **输入:**根=**T3】2k = 5
> /\
> 3 1
> /\
> 5 6
> T9】输出:** 3

**方法:**给定的问题可以通过使用图中的[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)来解决。其思想是使用[递归](http://www.geeksforgeeks.org/recursion/)并访问每个节点，检查其邻居节点之和是否小于 **K.** 可以按照以下步骤解决问题:

*   使用[递归](http://www.geeksforgeeks.org/recursion/)对图应用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，并使用[哈希集](http://www.geeksforgeeks.org/hashset-in-java/)存储图的访问节点
*   在每个节点上，遍历该节点的邻居，并将它们的和相加
    *   如果总和大于 **K** ，则增加计数
*   将计数作为结果返回

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

class Node
{
public:
    vector<Node *> neighbors;
    int val;
    Node(int v)
    {
        val = v;
        neighbors = {};
    }
};
// Depth first search function to visit
// every node of the graph and check if
// sum of neighbor nodes is less than K
void dfs(
    Node *root,
    set<Node *> &visited,
    vector<int> &count, int K)
{

    // If the current node is
    // already visited then return
    if (visited.find(root) != visited.end())
        return;

    // Mark the current node as visited
    visited.insert(root);

    // Initialize a variable sum to
    // calculate sum of neighbors
    int sum = 0;

    // Iterate through all neighbors
    for (Node *n : root->neighbors)
    {
        sum += n->val;
    }

    // If sum is less than K then
    // increment count by 1
    if (sum < K)
        count[0] = count[0] + 1;

    for (Node *n : root->neighbors)
    {

        // Visit the neighbor nodes
        dfs(n, visited, count, K);
    }
}

// Function to find the number of nodes
// in the graph with sum less than K
int nodeSumLessThanK(
    Node *root, int K)
{

    // Initialize the variable count
    // to count the answer
    vector<int> count(1, 0);
    // Initialize a HashSet to
    // store the visited nodes
    set<Node *> visited;

    // Apply DFS on the graph
    dfs(root, visited, count, K);

    // Return the answer stored in count
    return count[0];
}

// Driver code
int main()
{

    // Initialize the graph
    Node *root = new Node(2);
    root->neighbors.push_back(new Node(3));
    root->neighbors.push_back(new Node(1));
    root->neighbors[0]->neighbors.push_back(new Node(5));
    root->neighbors[1]->neighbors.push_back(new Node(6));
    int K = 5;

    // Call the function
    // and print the result
    cout << (nodeSumLessThanK(root, K));
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

class GFG {

    static class Node {

        List<Node> neighbors;
        int val;
        public Node(int val)
        {
            this.val = val;
            neighbors = new ArrayList<>();
        }
    }

    // Function to find the number of nodes
    // in the graph with sum less than K
    public static int nodeSumLessThanK(
        Node root, int K)
    {

        // Initialize the variable count
        // to count the answer
        int[] count = new int[1];

        // Initialize a HashSet to
        // store the visited nodes
        Set<Node> visited = new HashSet<>();

        // Apply DFS on the graph
        dfs(root, visited, count, K);

        // Return the answer stored in count
        return count[0];
    }

    // Depth first search function to visit
    // every node of the graph and check if
    // sum of neighbor nodes is less than K
    public static void dfs(
        Node root,
        Set<Node> visited,
        int[] count, int K)
    {

        // If the current node is
        // already visited then return
        if (visited.contains(root))
            return;

        // Mark the current node as visited
        visited.add(root);

        // Initialize a variable sum to
        // calculate sum of neighbors
        int sum = 0;

        // Iterate through all neighbors
        for (Node n : root.neighbors) {
            sum += n.val;
        }

        // If sum is less than K then
        // increment count by 1
        if (sum < K)
            count[0]++;

        for (Node n : root.neighbors) {

            // Visit the neighbor nodes
            dfs(n, visited, count, K);
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        // Initialize the graph
        Node root = new Node(2);
        root.neighbors.add(new Node(3));
        root.neighbors.add(new Node(1));
        root.neighbors.get(0)
            .neighbors.add(new Node(5));
        root.neighbors.get(1)
            .neighbors.add(new Node(6));
        int K = 5;

        // Call the function
        // and print the result
        System.out.println(
            nodeSumLessThanK(root, K));
    }
}
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    class Node {

        public List<Node> neighbors;
        public int val;
        public Node(int val)
        {
            this.val = val;
            neighbors = new List<Node>();
        }
    }

    // Function to find the number of nodes
    // in the graph with sum less than K
    static int nodeSumLessThanK(
        Node root, int K)
    {

        // Initialize the variable count
        // to count the answer
        int[] count = new int[1];

        // Initialize a HashSet to
        // store the visited nodes
        HashSet<Node> visited = new HashSet<Node>();

        // Apply DFS on the graph
        dfs(root, visited, count, K);

        // Return the answer stored in count
        return count[0];
    }

    // Depth first search function to visit
    // every node of the graph and check if
    // sum of neighbor nodes is less than K
    static void dfs(
        Node root,
        HashSet<Node> visited,
        int[] count, int K)
    {

        // If the current node is
        // already visited then return
        if (visited.Contains(root))
            return;

        // Mark the current node as visited
        visited.Add(root);

        // Initialize a variable sum to
        // calculate sum of neighbors
        int sum = 0;

        // Iterate through all neighbors
        foreach (Node n in root.neighbors) {
            sum += n.val;
        }

        // If sum is less than K then
        // increment count by 1
        if (sum < K)
            count[0]++;

        foreach (Node n in root.neighbors) {

            // Visit the neighbor nodes
            dfs(n, visited, count, K);
        }
    }

    // Driver code
    public static void Main(String[] args)
    {

        // Initialize the graph
        Node root = new Node(2);
        root.neighbors.Add(new Node(3));
        root.neighbors.Add(new Node(1));
        root.neighbors[0]
            .neighbors.Add(new Node(5));
        root.neighbors[1]
            .neighbors.Add(new Node(6));
        int K = 5;

        // Call the function
        // and print the result
        Console.WriteLine(
            nodeSumLessThanK(root, K));
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript code for the above approach

class Node {
  constructor(v) {
    this.val = v;
    this.neighbors = [];
  }
};
// Depth first search function to visit
// every node of the graph and check if
// sum of neighbor nodes is less than K
function dfs(root, visited, count, K) {

  // If the current node is
  // already visited then return
  if (visited.has(root))
    return;

  // Mark the current node as visited
  visited.add(root);

  // Initialize a variable sum to
  // calculate sum of neighbors
  let sum = 0;

  // Iterate through all neighbors
  for (let n of root.neighbors) {
    sum += n.val;
  }

  // If sum is less than K then
  // increment count by 1
  if (sum < K)
    count[0] = count[0] + 1;

  for (let n of root.neighbors) {

    // Visit the neighbor nodes
    dfs(n, visited, count, K);
  }
}

// Function to find the number of nodes
// in the graph with sum less than K
function nodeSumLessThanK(root, K) {

  // Initialize the variable count
  // to count the answer
  let count = new Array(1).fill(0);
  // Initialize a HashSet to
  // store the visited nodes
  let visited = new Set();

  // Apply DFS on the graph
  dfs(root, visited, count, K);

  // Return the answer stored in count
  return count[0];
}

// Driver code

// Initialize the graph
let root = new Node(2);
root.neighbors.push(new Node(3));
root.neighbors.push(new Node(1));
root.neighbors[0].neighbors.push(new Node(5));
root.neighbors[1].neighbors.push(new Node(6));
let K = 5;

// Call the function
// and print the result
document.write(nodeSumLessThanK(root, K));

// This code is contributed by gfgking.
</script>
```

**Output**

```
3
```

**时间复杂度:** O(V + E)，其中 V 为顶点数，E 为图中边数
**辅助空间:** O(V)