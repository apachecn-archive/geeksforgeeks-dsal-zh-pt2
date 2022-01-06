# 统计 N 元树中给定 K 个节点的共同祖先数量

> 原文:[https://www . geeksforgeeks . org/count-n 元树中给定 k 个节点的公共祖先数量/](https://www.geeksforgeeks.org/count-the-number-of-common-ancestors-of-given-k-nodes-in-a-n-ary-tree/)

给定一个 [N 元树](https://www.geeksforgeeks.org/generic-treesn-array-trees/) **根**和一个 **K** 节点列表，任务是找到树中给定 **K** 节点的共同祖先的数量。

**示例:**

> **输入:**根= 3
> /\
> 2 1
> /\/| \
> 9 7 8 6 3
> K = { 7，2，9 }
> T8】输出: 2
> **说明:**节点 7，9 和 2 的共同祖先是 2 和 3
> 
> **输入:**根=**2
> \
> 1
> \
> 0—4
> /| \
> 9 3 8
> K = { 9，8，3，4，0}
> **输出:** 3**

****方法:**使用[后序遍历](https://www.geeksforgeeks.org/post-order-traversal-of-binary-tree-in-on-using-o1-space/)可以解决给定的问题。其思想是找到 **K** 节点的[最低共同祖先](https://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/)，然后增加它上面每个节点的祖先计数，直到到达根。可以遵循以下步骤来解决问题:**

*   **将所有列表节点添加到一个集合中**
*   **在树上应用[后序遍历](https://www.geeksforgeeks.org/post-order-traversal-of-binary-tree-in-on-using-o1-space/):

    *   找到[最低的共同祖先](https://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/)，然后在每次递归调用时开始增加节点数的值** 
*   **返回计算出的答案**

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

class GFG {

    static class Node {

        List<Node> children;
        int val;

        // constructor
        public Node(int val)
        {
            children = new ArrayList<>();
            this.val = val;
        }
    }

    // Function to find the number
    // of common ancestors in a tree
    public static int numberOfAncestors(
        Node root,
        List<Node> nodes)
    {

        // Initialize a set
        Set<Node> set = new HashSet<>();

        // Iterate the list of nodes
        // and add them in a set
        for (Node curr : nodes) {
            set.add(curr);
        }

        // Find LCA and return
        // number of ancestors
        return CAcount(root, set)[1].val;
    }

    // Function to find LCA and
    // count number of ancestors
    public static Node[] CAcount(
        Node root, Set<Node> set)
    {

        // If the current node
        // is a desired node
        if (set.contains(root)) {

            Node[] res = new Node[2];
            res[0] = root;
            res[1] = new Node(1);
            return res;
        }

        // If leaf node then return null
        if (root.children.size() == 0) {

            return new Node[2];
        }

        // To count number of desired nodes
        // in the children branches
        int childCount = 0;

        // Initialize a node to return
        Node[] ans = new Node[2];

        // Iterate through all children
        for (Node child : root.children) {

            Node[] res = CAcount(child, set);

            // Increment child count if
            // desired node is found
            if (res[0] != null)
                childCount++;

            // If first desired node is found
            if (childCount == 1
                && ans[0] == null) {

                ans = res;
            }
            else if (childCount > 1) {

                ans[0] = root;
                ans[1] = new Node(1);
                return ans;
            }
        }

        // If LCA found below then increment
        // number of common ancestors
        if (ans[0] != null)
            ans[1].val++;

        // Return the answer
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {

        // Initialize the tree
        Node zero = new Node(0);
        Node one = new Node(1);
        Node two = new Node(2);
        Node three = new Node(3);
        Node four = new Node(4);
        Node five = new Node(5);
        Node six = new Node(6);
        Node seven = new Node(7);
        zero.children.add(one);
        zero.children.add(two);
        zero.children.add(three);
        one.children.add(four);
        one.children.add(five);
        five.children.add(six);
        five.children.add(seven);

        // List of nodes whose
        // ancestors are to be found
        List<Node> nodes = new ArrayList<>();
        nodes.add(four);
        nodes.add(six);
        nodes.add(seven);

        // Call the function
        // and print the result
        System.out.println(
            numberOfAncestors(zero, nodes));
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

        public List<Node> children;
        public int val;

        // constructor
        public Node(int val)
        {
            children = new List<Node>();
            this.val = val;
        }
    }

    // Function to find the number
    // of common ancestors in a tree
    static int numberOfAncestors(
        Node root,
        List<Node> nodes)
    {

        // Initialize a set
        HashSet<Node> set = new HashSet<Node>();

        // Iterate the list of nodes
        // and add them in a set
        foreach (Node curr in nodes) {
            set.Add(curr);
        }

        // Find LCA and return
        // number of ancestors
        return CAcount(root, set)[1].val;
    }

    // Function to find LCA and
    // count number of ancestors
    static Node[] CAcount(
        Node root, HashSet<Node> set)
    {

        // If the current node
        // is a desired node
        if (set.Contains(root)) {

            Node[] res = new Node[2];
            res[0] = root;
            res[1] = new Node(1);
            return res;
        }

        // If leaf node then return null
        if (root.children.Count == 0) {

            return new Node[2];
        }

        // To count number of desired nodes
        // in the children branches
        int childCount = 0;

        // Initialize a node to return
        Node[] ans = new Node[2];

        // Iterate through all children
        foreach (Node child in root.children) {

            Node[] res = CAcount(child, set);

            // Increment child count if
            // desired node is found
            if (res[0] != null)
                childCount++;

            // If first desired node is found
            if (childCount == 1
                && ans[0] == null) {

                ans = res;
            }
            else if (childCount > 1) {

                ans[0] = root;
                ans[1] = new Node(1);
                return ans;
            }
        }

        // If LCA found below then increment
        // number of common ancestors
        if (ans[0] != null)
            ans[1].val++;

        // Return the answer
        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {

        // Initialize the tree
        Node zero = new Node(0);
        Node one = new Node(1);
        Node two = new Node(2);
        Node three = new Node(3);
        Node four = new Node(4);
        Node five = new Node(5);
        Node six = new Node(6);
        Node seven = new Node(7);
        zero.children.Add(one);
        zero.children.Add(two);
        zero.children.Add(three);
        one.children.Add(four);
        one.children.Add(five);
        five.children.Add(six);
        five.children.Add(seven);

        // List of nodes whose
        // ancestors are to be found
        List<Node> nodes = new List<Node>();
        nodes.Add(four);
        nodes.Add(six);
        nodes.Add(seven);

        // Call the function
        // and print the result
        Console.WriteLine(
            numberOfAncestors(zero, nodes));
    }
}

// This code is contributed by shikhasingrajput
```

## **java 描述语言**

```
<script>
// Javascript implementation for the above approach

class Node {
  // constructor
  constructor(val) {
    this.children = new Array();
    this.val = val;
  }
}

// Function to find the number
// of common ancestors in a tree
function numberOfAncestors(root, nodes) {

  // Initialize a set
  let set = new Set();

  // Iterate the list of nodes
  // and add them in a set
  for (curr of nodes) {
    set.add(curr);
  }

  // Find LCA and return
  // number of ancestors
  return CAcount(root, set)[1].val;
}

// Function to find LCA and
// count number of ancestors
function CAcount(root, set) {

  // If the current node
  // is a desired node
  if (set.has(root)) {

    let res = new Node(2);
    res[0] = root;
    res[1] = new Node(1);
    return res;
  }

  // If leaf node then return null
  if (root.children.length == 0) {

    return new Node(2);
  }

  // To count number of desired nodes
  // in the children branches
  let childCount = 0;

  // Initialize a node to return
  let ans = new Node(2);

  // Iterate through all children
  for (child of root.children) {

    let res = CAcount(child, set);

    // Increment child count if
    // desired node is found
    if (res[0] != null)
      childCount++;

    // If first desired node is found
    if (childCount == 1
      && ans[0] == null) {

      ans = res;
    }
    else if (childCount > 1) {

      ans[0] = root;
      ans[1] = new Node(1);
      return ans;
    }
  }

  // If LCA found below then increment
  // number of common ancestors
  if (ans[0] != null)
    ans[1].val++;

  // Return the answer
  return ans;
}

// Driver code

// Initialize the tree
let zero = new Node(0);
let one = new Node(1);
let two = new Node(2);
let three = new Node(3);
let four = new Node(4);
let five = new Node(5);
let six = new Node(6);
let seven = new Node(7);
zero.children.push(one);
zero.children.push(two);
zero.children.push(three);
one.children.push(four);
one.children.push(five);
five.children.push(six);
five.children.push(seven);

// List of nodes whose
// ancestors are to be found
let nodes = new Array();
nodes.push(four);
nodes.push(six);
nodes.push(seven);

// Call the function
// and print the result
document.write(numberOfAncestors(zero, nodes));

// This code is contributed by saurabh_jaiswal.
</script>
```

****Output**

```
2
```** 

****时间复杂度:** O(N)，其中 N 为树中节点数
T3】辅助空间: O(H)，H 为树高**