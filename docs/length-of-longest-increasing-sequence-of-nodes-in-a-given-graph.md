# 给定图中节点最长递增序列的长度

> 原文:[https://www . geesforgeks . org/给定图中最长递增节点序列的长度/](https://www.geeksforgeeks.org/length-of-longest-increasing-sequence-of-nodes-in-a-given-graph/)

给定一个[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/) **根，**的任务是找出图中最长递增序列的长度。

**示例:**

> **输入:**根=**7—-17
> /\
> 1—-2—-5 4
> /\ \
> 11 6—-8
> /
> 12
> T11】输出: 6
> **说明:**图中最长的递增序列由节点 1、2、5、6、8、12 组成**
> 
> ****输入:**2
> /\
> 3 1
> /\
> 5 6
> T7】输出: 4**

****方法:**给定的问题可以通过在图中的每个节点上使用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)来解决。其思想是使用[递归](http://www.geeksforgeeks.org/recursion/)访问值小于当前节点的邻居节点，并在计算到达当前节点的最长路径之前计算到达邻居的最长路径。可以遵循以下步骤来解决问题:**

*   **在根节点上应用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，访问并存储列表中的所有节点**
*   **使用[递归](http://www.geeksforgeeks.org/recursion/)在图的每个未访问节点上应用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，并使用[散列表](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)存储图的已访问节点，该节点映射到到达该节点的最长路径

    *   在每个节点[迭代邻居的数组列表](https://www.geeksforgeeks.org/iterating-arraylists-java/)，并对值小于当前节点值的邻居节点使用递归，并计算终止于它们的最长路径
    *   找出到达邻居的最长路径的最大值，并加 1 计算到达当前节点的最长路径** 
*   **返回所有最长路径的最大值**

**下面是上述方法的实现:**

## **C++**

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

class Node
{
public:
    vector<Node *> neighbors;
    int val;

    // constructor
    Node(int v)
    {

        val = v;
        neighbors = {};
    }
};

// Depth first search function to add
// every node of the graph in a list
void dfs(
    Node *root,
    unordered_map<Node *, int> &visited,
    vector<Node *> &nodes)
{

    // If the current node is
    // already visited then return
    if (visited.find(root) != visited.end())
        return;

    // Mark the current node as visited
    visited[root] = 0;

    // Add the current node in the list
    nodes.push_back(root);

    // Iterate through all neighbors
    for (Node *n : root->neighbors)
    {

        // Visit the neighbors
        dfs(n, visited, nodes);
    }
}
// Depth first search function
// to calculate the longest path
// ending at every node
int findLongestPath(
    Node *root, unordered_map<Node *, int> &visited)
{

    // If the current node is visited
    // then return its value
    if (visited[root] > 0)
        return visited[root];

    // Initialize a variable max to
    // calculate longest increasing path
    int maxi = 0;

    // Iterate through all neighbors
    for (Node *n : root->neighbors)
    {

        // If neighbor's value is less
        // than current node's value then
        // find longest path ending up to
        // the neighbor
        if (n->val < root->val)
        {

            // Update max
            maxi = max(
                maxi,
                findLongestPath(n, visited));
        }
    }

    // Store the value in the hashmap
    visited[root] = maxi + 1;

    // Return the longest increasing
    // path ending on root
    return maxi + 1;
}
// Function to find the longest
// increasing path in a graph
int longestIncPath(Node *root)
{

    // Base case
    if (root == NULL)
        return 0;

    // Initialize a variable max
    // to calculate longest path
    int maxi = 1;

    // Initialize a HashMap to
    // store the visited nodes
    unordered_map<Node *, int> visited;

    // List to store all the
    // nodes in a graph
    vector<Node *> nodes;

    // Apply DFS on the graph
    // add all the nodes in a list
    dfs(root, visited, nodes);

    // Iterate through the list of nodes
    for (int i = 0; i < nodes.size(); i++)
    {

        Node *curr = nodes[i];

        // Current node is not already visited
        if (visited[curr] == 0)
        {

            // Apply DFS to find the
            // longest path ending on
            // the current node
            findLongestPath(curr, visited);
        }

        // Update max by comparing it
        // with the longest path ending
        // on the current node
        maxi = max(
            maxi, visited[curr]);
    }

    // Return the answer
    return maxi;
}

// Driver code
int main()
{

    // Initialize the graph
    Node *seven = new Node(7);
    Node *five = new Node(5);
    Node *four = new Node(4);
    Node *sevTeen = new Node(17);
    Node *one = new Node(1);
    Node *two = new Node(2);
    Node *six = new Node(6);
    Node *eight = new Node(8);
    Node *eleven = new Node(11);
    Node *twelve = new Node(12);
    one->neighbors.push_back(two);
    eleven->neighbors.push_back(two);
    two->neighbors.push_back(one);
    two->neighbors.push_back(eleven);
    two->neighbors.push_back(five);
    eight->neighbors.push_back(twelve);
    eight->neighbors.push_back(six);
    eight->neighbors.push_back(four);
    four->neighbors.push_back(eight);
    four->neighbors.push_back(seven);
    twelve->neighbors.push_back(eight);
    six->neighbors.push_back(five);
    six->neighbors.push_back(eight);
    five->neighbors.push_back(two);
    five->neighbors.push_back(seven);
    five->neighbors.push_back(six);
    seven->neighbors.push_back(five);
    seven->neighbors.push_back(four);
    seven->neighbors.push_back(sevTeen);
    sevTeen->neighbors.push_back(seven);

    // Call the function
    // and print the result
    cout << (longestIncPath(seven));
    return 0;
}

// This code is contributed by Potta Lokesh
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

class GFG {

    static class Node {

        List<Node> neighbors;
        int val;

        // constructor
        public Node(int val)
        {

            this.val = val;
            neighbors = new ArrayList<>();
        }
    }

    // Function to find the longest
    // increasing path in a graph
    public static int longestIncPath(Node root)
    {

        // Base case
        if (root == null)
            return 0;

        // Initialize a variable max
        // to calculate longest path
        int max = 1;

        // Initialize a HashMap to
        // store the visited nodes
        Map<Node, Integer> visited
            = new HashMap<>();

        // List to store all the
        // nodes in a graph
        List<Node> nodes = new ArrayList<>();

        // Apply DFS on the graph
        // add all the nodes in a list
        dfs(root, visited, nodes);

        // Iterate through the list of nodes
        for (int i = 0; i < nodes.size(); i++) {

            Node curr = nodes.get(i);

            // Current node is not already visited
            if (visited.get(curr) == 0) {

                // Apply DFS to find the
                // longest path ending on
                // the current node
                findLongestPath(curr, visited);
            }

            // Update max by comparing it
            // with the longest path ending
            // on the current node
            max = Math.max(
                max, visited.get(curr));
        }

        // Return the answer
        return max;
    }

    // Depth first search function
    // to calculate the longest path
    // ending at every node
    public static int findLongestPath(
        Node root, Map<Node, Integer> visited)
    {

        // If the current node is visited
        // then return its value
        if (visited.get(root) > 0)
            return visited.get(root);

        // Initialize a variable max to
        // calculate longest increasing path
        int max = 0;

        // Iterate through all neighbors
        for (Node n : root.neighbors) {

            // If neighbor's value is less
            // than current node's value then
            // find longest path ending up to
            // the neighbor
            if (n.val < root.val) {

                // Update max
                max = Math.max(
                    max,
                    findLongestPath(n, visited));
            }
        }

        // Store the value in the hashmap
        visited.put(root, max + 1);

        // Return the longest increasing
        // path ending on root
        return max + 1;
    }

    // Depth first search function to add
    // every node of the graph in a list
    public static void dfs(
        Node root,
        Map<Node, Integer> visited,
        List<Node> nodes)
    {

        // If the current node is
        // already visited then return
        if (visited.containsKey(root))
            return;

        // Mark the current node as visited
        visited.put(root, 0);

        // Add the current node in the list
        nodes.add(root);

        // Iterate through all neighbors
        for (Node n : root.neighbors) {

            // Visit the neighbors
            dfs(n, visited, nodes);
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        // Initialize the graph
        Node seven = new Node(7);
        Node five = new Node(5);
        Node four = new Node(4);
        Node sevTeen = new Node(17);
        Node one = new Node(1);
        Node two = new Node(2);
        Node six = new Node(6);
        Node eight = new Node(8);
        Node eleven = new Node(11);
        Node twelve = new Node(12);
        one.neighbors.add(two);
        eleven.neighbors.add(two);
        two.neighbors.add(one);
        two.neighbors.add(eleven);
        two.neighbors.add(five);
        eight.neighbors.add(twelve);
        eight.neighbors.add(six);
        eight.neighbors.add(four);
        four.neighbors.add(eight);
        four.neighbors.add(seven);
        twelve.neighbors.add(eight);
        six.neighbors.add(five);
        six.neighbors.add(eight);
        five.neighbors.add(two);
        five.neighbors.add(seven);
        five.neighbors.add(six);
        seven.neighbors.add(five);
        seven.neighbors.add(four);
        seven.neighbors.add(sevTeen);
        sevTeen.neighbors.add(seven);

        // Call the function
        // and print the result
        System.out.println(
            longestIncPath(seven));
    }
}
```

## **C#**

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    class Node {

        public List<Node> neighbors;
        public int val;

        // constructor
        public Node(int val)
        {

            this.val = val;
            neighbors = new List<Node>();
        }
    }

    // Function to find the longest
    // increasing path in a graph
    static int longestIncPath(Node root)
    {

        // Base case
        if (root == null)
            return 0;

        // Initialize a variable max
        // to calculate longest path
        int max = 1;

        // Initialize a Dictionary to
        // store the visited nodes
        Dictionary<Node, int> visited
            = new Dictionary<Node, int>();

        // List to store all the
        // nodes in a graph
        List<Node> nodes = new List<Node>();

        // Apply DFS on the graph
        // add all the nodes in a list
        dfs(root, visited, nodes);

        // Iterate through the list of nodes
        for (int i = 0; i < nodes.Count; i++) {

            Node curr = nodes[i];

            // Current node is not already visited
            if (visited[curr] == 0) {

                // Apply DFS to find the
                // longest path ending on
                // the current node
                findlongestPath(curr, visited);
            }

            // Update max by comparing it
            // with the longest path ending
            // on the current node
            max = Math.Max(
                max, visited[curr]);
        }

        // Return the answer
        return max;
    }

    // Depth first search function
    // to calculate the longest path
    // ending at every node
    static int findlongestPath(
        Node root, Dictionary<Node, int> visited)
    {

        // If the current node is visited
        // then return its value
        if (visited[root] > 0)
            return visited[root];

        // Initialize a variable max to
        // calculate longest increasing path
        int max = 0;

        // Iterate through all neighbors
        foreach (Node n in root.neighbors) {

            // If neighbor's value is less
            // than current node's value then
            // find longest path ending up to
            // the neighbor
            if (n.val < root.val) {

                // Update max
                max = Math.Max(
                    max,
                    findlongestPath(n, visited));
            }
        }

        // Store the value in the hashmap
        if(visited.ContainsKey(root))
            visited[root] = max + 1;
        else
            visited.Add(root, max + 1);

        // Return the longest increasing
        // path ending on root
        return max + 1;
    }

    // Depth first search function to add
    // every node of the graph in a list
    static void dfs(
        Node root,
        Dictionary<Node, int> visited,
        List<Node> nodes)
    {

        // If the current node is
        // already visited then return
        if (visited.ContainsKey(root))
            return;

        // Mark the current node as visited
        visited.Add(root, 0);

        // Add the current node in the list
        nodes.Add(root);

        // Iterate through all neighbors
        foreach (Node n in root.neighbors) {

            // Visit the neighbors
            dfs(n, visited, nodes);
        }
    }

    // Driver code
    public static void Main(String[] args)
    {

        // Initialize the graph
        Node seven = new Node(7);
        Node five = new Node(5);
        Node four = new Node(4);
        Node sevTeen = new Node(17);
        Node one = new Node(1);
        Node two = new Node(2);
        Node six = new Node(6);
        Node eight = new Node(8);
        Node eleven = new Node(11);
        Node twelve = new Node(12);
        one.neighbors.Add(two);
        eleven.neighbors.Add(two);
        two.neighbors.Add(one);
        two.neighbors.Add(eleven);
        two.neighbors.Add(five);
        eight.neighbors.Add(twelve);
        eight.neighbors.Add(six);
        eight.neighbors.Add(four);
        four.neighbors.Add(eight);
        four.neighbors.Add(seven);
        twelve.neighbors.Add(eight);
        six.neighbors.Add(five);
        six.neighbors.Add(eight);
        five.neighbors.Add(two);
        five.neighbors.Add(seven);
        five.neighbors.Add(six);
        seven.neighbors.Add(five);
        seven.neighbors.Add(four);
        seven.neighbors.Add(sevTeen);
        sevTeen.neighbors.Add(seven);

        // Call the function
        // and print the result
        Console.WriteLine(
            longestIncPath(seven));
    }
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>
// Javascript code for the above approach

class Node {
  // constructor
  constructor(v) {

    this.val = v;
    this.neighbors = [];
  }
};

// Depth first search function to add
// every node of the graph in a list
function dfs(root, visited, nodes) {

  // If the current node is
  // already visited then return
  if (visited.has(root))
    return;

  // Mark the current node as visited
  visited.set(root, 0);

  // Add the current node in the list
  nodes.push(root);

  // Iterate through all neighbors
  for (n of root.neighbors) {

    // Visit the neighbors
    dfs(n, visited, nodes);
  }
}
// Depth first search function
// to calculate the longest path
// ending at every node
function findLongestPath(root, visited) {

  // If the current node is visited
  // then return its value
  if (visited.get(root) > 0)
    return visited.get(root);

  // Initialize a variable max to
  // calculate longest increasing path
  let maxi = 0;

  // Iterate through all neighbors
  for (n of root.neighbors) {

    // If neighbor's value is less
    // than current node's value then
    // find longest path ending up to
    // the neighbor
    if (n.val < root.val) {

      // Update max
      maxi = Math.max(
        maxi,
        findLongestPath(n, visited));
    }
  }

  // Store the value in the hashmap
  visited.set(root, maxi + 1);

  // Return the longest increasing
  // path ending on root
  return maxi + 1;
}
// Function to find the longest
// increasing path in a graph
function longestIncPath(root) {

  // Base case
  if (root == null)
    return 0;

  // Initialize a variable max
  // to calculate longest path
  let maxi = 1;

  // Initialize a HashMap to
  // store the visited nodes
  let visited = new Map();

  // List to store all the
  // nodes in a graph
  let nodes = [];

  // Apply DFS on the graph
  // add all the nodes in a list
  dfs(root, visited, nodes);

  // Iterate through the list of nodes
  for (let i = 0; i < nodes.length; i++) {

    let curr = nodes[i];

    // Current node is not already visited
    if (visited.get(curr) == 0) {

      // Apply DFS to find the
      // longest path ending on
      // the current node
      findLongestPath(curr, visited);
    }

    // Update max by comparing it
    // with the longest path ending
    // on the current node
    maxi = Math.max(
      maxi, visited.get(curr));
  }

  // Return the answer
  return maxi;
}

// Driver code

// Initialize the graph
let seven = new Node(7);
let five = new Node(5);
let four = new Node(4);
let sevTeen = new Node(17);
let one = new Node(1);
let two = new Node(2);
let six = new Node(6);
let eight = new Node(8);
let eleven = new Node(11);
let twelve = new Node(12);
one.neighbors.push(two);
eleven.neighbors.push(two);
two.neighbors.push(one);
two.neighbors.push(eleven);
two.neighbors.push(five);
eight.neighbors.push(twelve);
eight.neighbors.push(six);
eight.neighbors.push(four);
four.neighbors.push(eight);
four.neighbors.push(seven);
twelve.neighbors.push(eight);
six.neighbors.push(five);
six.neighbors.push(eight);
five.neighbors.push(two);
five.neighbors.push(seven);
five.neighbors.push(six);
seven.neighbors.push(five);
seven.neighbors.push(four);
seven.neighbors.push(sevTeen);
sevTeen.neighbors.push(seven);

// Call the function
// and print the result
document.write((longestIncPath(seven)));

// This code is contributed by saurabh_jaiswal.
</script>
```

****Output**

```
6
```** 

****时间复杂度:** O(V + E)，其中 V 为顶点数，E 为边数
T3】辅助空间: O(V)**