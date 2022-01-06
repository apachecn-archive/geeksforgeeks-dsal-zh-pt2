# N 元树中两个给定节点之间的最小距离

> 原文:[https://www . geesforgeks . org/n 元树中两个给定节点之间的最小距离/](https://www.geeksforgeeks.org/minimum-distance-between-two-given-nodes-in-an-n-ary-tree/)

给定一个由 **N** 个节点组成的 [N 元树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)，任务是找到从节点 **A** 到树的节点 **B** 的最小距离。

**示例**:

> **输入**:
> 1
> /\
> 2 3
> /\/\ \
> 4 5 6 7 8
> A = 4，B = 3
> **输出** : 3
> **说明**:路径 4- > 2- > 1- > 3 给出了 A 到 B 的最小距离。
> 
> **输入**:
> 1
> /\
> 2 3
> /\ \
> 6 7 8
> A = 6，B = 7
> /T9】输出 : 2

**方法:**这个问题可以用 [**LCA** (最低共同祖先)](https://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/)的概念来解决。两个给定节点 **A** 和 **B** 之间的最小距离可以通过公式–
**mindistance(A，B) = dist (LCA，A) + dist (LCA，B)**
按照以下步骤解决问题:

1.  分别找到从根节点到节点 **A** 和 **B** 的路径，同时将两条路径存储在两个数组中。
2.  现在迭代，直到两个数组的值相同，并且不匹配之前的值是 **LCA** 节点值。
3.  不匹配之前的值是 **LCA** 节点值。
4.  找到 **LCA** 节点到节点 **A** 和 **B** 的距离，可以通过给定的步骤找到:
    *   在第一个数组中，从 **LCA** 节点值开始迭代，增加计数，直到找到节点 **A** 的值，即**距离(LCA，A)。**
    *   在第二个数组中，从 **LCA** 节点值开始迭代，增加计数，直到找到节点 B 的值，即 **dist (LCA，B)**
5.  返回这些距离的总和，即**距离(LCA，A) +距离(LCA，B)** 。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of Node
struct Node {
    int val;
    vector<Node*> child;
};

// Utility function to create a
// new tree node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->val = key;
    return temp;
}

bool flag;

// Function to get the path
// from root to a node
void findPath(Node* root, int key,
              vector<int>& arr)
{
    if (!root)
        return;
    arr.push_back(root->val);
    // if key is found set flag and return
    if (root->val == key) {
        flag = 1;
        return;
    }
    // recur for all children
    for (int i = 0; i < root->child.size(); i++) {

        findPath(root->child[i], key, arr);

        // if key is found dont need to pop values
        if (flag == 1)
            return;
    }

    arr.pop_back();
    return;
}

void findMinDist(Node* root, int A, int B)
{
    if (root == NULL)
        return;
    int val = root->val;

    // vector to store both paths
    vector<int> arr1, arr2;

    // set flag as false;
    flag = false;

    // find path from root to node a
    findPath(root, A, arr1);

    // set flag again as false;
    flag = false;

    // find path from root to node b
    findPath(root, B, arr2);

    // to store index of LCA node
    int j;

    // if unequal values are found
    // return previous value
    for (int i = 1; i < min(arr1.size(), arr2.size()); i++) {
        if (arr1[i] != arr2[i]) {
            val = arr1[i - 1];
            j = i - 1;
            break;
        }
    }
    int d1 = 0, d2 = 0;

    // iterate for finding distance
    // between LCA(a, b) and a
    for (int i = j; i < arr1.size(); i++)
        if (arr1[i] == A)
            break;
        else
            d1 += 1;

    // iterate for finding distance
    // between LCA(a, b) and b
    for (int i = j; i < arr2.size(); i++)
        if (arr2[i] == B)
            break;
        else
            d2 += 1;
    // get distance
    val = d1 + d2;
    cout << val << '\n';
}

// Driver Code
int main()

{
    Node* root = newNode(1);
    (root->child).push_back(newNode(2));
    (root->child).push_back(newNode(3));
    (root->child[0]->child).push_back(newNode(4));
    (root->child[0]->child).push_back(newNode(5));
    (root->child[1]->child).push_back(newNode(6));
    (root->child[1])->child.push_back(newNode(7));
    (root->child[1]->child).push_back(newNode(8));
    int A = 4, B = 3;

    // get min distance
    findMinDist(root, A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    // Structure of Node
    static class Node {

        public int val;
        public Node left, right;
        public Vector<Node> child;

        public Node(int key)
        {
            val = key;
            left = right = null;
            child = new Vector<Node>();
        }
    }

    // Utility function to create a
    // new tree node
    static Node newNode(int key)
    {
        Node temp = new Node(key);
        return temp;
    }

    static int flag;

    // Function to get the path
    // from root to a node
    static void findPath(Node root, int key,
                  Vector<Integer> arr)
    {
        if (root==null)
            return;
        arr.add(root.val);
        // if key is found set flag and return
        if (root.val == key) {
            flag = 1;
            return;
        }
        // recur for all children
        for (int i = 0; i < root.child.size(); i++) {

            findPath(root.child.get(i), key, arr);

            // if key is found dont need to pop values
            if (flag == 1)
                return;
        }

        arr.remove(arr.size()-1);
        return;
    }

    static void findMinDist(Node root, int A, int B)
    {
        if (root == null)
            return;
        int val = root.val;

        // vector to store both paths
        Vector<Integer> arr1 = new Vector<Integer>();
        Vector<Integer> arr2 = new Vector<Integer>();

        // set flag as false;
        flag = 0;

        // find path from root to node a
        findPath(root, A, arr1);

        // set flag again as false;
        flag = 0;

        // find path from root to node b
        findPath(root, B, arr2);

        // to store index of LCA node
        int j=0;

        // if unequal values are found
        // return previous value
        for (int i = 1; i < Math.min(arr1.size(), arr2.size()); i++) {
            if (arr1.get(i) != arr2.get(i)) {
                val = arr1.get(i - 1);
                j = i - 1;
                break;
            }
        }
        int d1 = 0, d2 = 0;

        // iterate for finding distance
        // between LCA(a, b) and a
        for (int i = j; i < arr1.size(); i++)
            if (arr1.get(i) == A)
                break;
            else
                d1 += 1;

        // iterate for finding distance
        // between LCA(a, b) and b
        for (int i = j; i < arr2.size(); i++)
            if (arr2.get(i) == B)
                break;
            else
                d2 += 1;
        // get distance
        val = d1 + d2;
        System.out.println(val);
    }

    public static void main(String[] args) {
        Node root = newNode(1);
        (root.child).add(newNode(2));
        (root.child).add(newNode(3));
        (root.child.get(0).child).add(newNode(4));
        (root.child.get(0).child).add(newNode(5));
        (root.child.get(1).child).add(newNode(6));
        (root.child.get(1)).child.add(newNode(7));
        (root.child.get(1).child).add(newNode(8));
        int A = 4, B = 3;

        // get min distance
        findMinDist(root, A, B);
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Structure of Node
class Node:
    def __init__(self, key):
        self.val = key
        self.left = None
        self.right = None
        self.child = []

# Utility function to create a
# new tree node
def newNode(key):
    temp = Node(key)
    return temp

flag = 0

# Function to get the path
# from root to a node
def findPath(root, key, arr):
    global flag
    if (root==None):
        return
    arr.append(root.val)
    # if key is found set flag and return
    if (root.val == key):
        flag = 1
        return
    # recur for all children
    for i in range(len(root.child)):
        findPath(root.child[i], key, arr)

        # if key is found dont need to pop values
        if (flag == 1):
            return

    arr.pop()
    return

def findMinDist(root, A, B):
    global flag
    if (root == None):
        return
    val = root.val

    # vector to store both paths
    arr1 = []
    arr2 = []

    # set flag as false;
    flag = 0

    # find path from root to node a
    findPath(root, A, arr1)

    # set flag again as false;
    flag = 0

    # find path from root to node b
    findPath(root, B, arr2)

    # to store index of LCA node
    j=0

    # if unequal values are found
    # return previous value
    for i in range(min(len(arr1), len(arr2))):
        if (arr1[i] != arr2[i]):
            val = arr1[i - 1]
            j = i - 1
            break
    d1, d2 = 0, 0

    # iterate for finding distance
    # between LCA(a, b) and a
    for i in range(j, len(arr1)):
        if (arr1[i] == A):
            break
        else:
            d1 += 1

    # iterate for finding distance
    # between LCA(a, b) and b
    for i in range(j, len(arr2)):
        if (arr2[i] == B):
            break
        else:
            d2 += 1
    # get distance
    val = d1 + d2
    print(val)

root = newNode(1)
(root.child).append(newNode(2))
(root.child).append(newNode(3))
(root.child[0].child).append(newNode(4))
(root.child[0].child).append(newNode(5))
(root.child[1].child).append(newNode(6))
(root.child[1]).child.append(newNode(7))
(root.child[1].child).append(newNode(8))
A, B = 4, 3

# get min distance
findMinDist(root, A, B)

# This code is contributed by rameshtravel07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

// Structure of Node
class GFG{

    public class Node {
        public int val;
        public Node left=null, right=null;
        public List<Node> child = new List<Node>();
    }

// Utility function to create a
// new tree node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.val = key;
    return temp;
}

static int flag;

// Function to get the path
// from root to a node
static void findPath(Node root, int key,
              List<int> arr)
{
    if (root==null)
        return;
    arr.Add(root.val);
    // if key is found set flag and return
    if (root.val == key) {
        flag = 1;
        return;
    }
    // recur for all children
    for (int i = 0; i < root.child.Count; i++) {

        findPath(root.child[i], key, arr);

        // if key is found dont need to pop values
        if (flag == 1)
            return;
    }

    arr.RemoveAt(arr.Count-1);
    return;
}

static void findMinDist(Node root, int A, int B)
{
    if (root == null)
        return;
    int val = root.val;

    // vector to store both paths
    List<int> arr1 = new List<int>();
    List<int> arr2 = new List<int>();

    // set flag as false;
    flag = 0;

    // find path from root to node a
    findPath(root, A, arr1);

    // set flag again as false;
    flag = 0;

    // find path from root to node b
    findPath(root, B, arr2);

    // to store index of LCA node
    int j=0;

    // if unequal values are found
    // return previous value
    for (int i = 1; i < Math.Min(arr1.Count, arr2.Count); i++) {
        if (arr1[i] != arr2[i]) {
            val = arr1[i - 1];
            j = i - 1;
            break;
        }
    }
    int d1 = 0, d2 = 0;

    // iterate for finding distance
    // between LCA(a, b) and a
    for (int i = j; i < arr1.Count; i++)
        if (arr1[i] == A)
            break;
        else
            d1 += 1;

    // iterate for finding distance
    // between LCA(a, b) and b
    for (int i = j; i < arr2.Count; i++)
        if (arr2[i] == B)
            break;
        else
            d2 += 1;
    // get distance
    val = d1 + d2;
    Console.WriteLine(val);
}

// Driver Code
public static void Main()

{
    Node root = newNode(1);
    (root.child).Add(newNode(2));
    (root.child).Add(newNode(3));
    (root.child[0].child).Add(newNode(4));
    (root.child[0].child).Add(newNode(5));
    (root.child[1].child).Add(newNode(6));
    (root.child[1]).child.Add(newNode(7));
    (root.child[1].child).Add(newNode(8));
    int A = 4, B = 3;

    // get min distance
    findMinDist(root, A, B);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Structure of Node
    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.val = key;
           this.child = [];
        }
    }

    // Utility function to create a
    // new tree node
    function newNode(key)
    {
        let temp = new Node(key);
        return temp;
    }

    let flag;

    // Function to get the path
    // from root to a node
    function findPath(root, key, arr)
    {
        if (root==null)
            return;
        arr.push(root.val);
        // if key is found set flag and return
        if (root.val == key) {
            flag = 1;
            return;
        }
        // recur for all children
        for (let i = 0; i < root.child.length; i++) {

            findPath(root.child[i], key, arr);

            // if key is found dont need to pop values
            if (flag == 1)
                return;
        }

        arr.pop();
        return;
    }

    function findMinDist(root, A, B)
    {
        if (root == null)
            return;
        let val = root.val;

        // vector to store both paths
        let arr1 = [];
        let arr2 = [];

        // set flag as false;
        flag = 0;

        // find path from root to node a
        findPath(root, A, arr1);

        // set flag again as false;
        flag = 0;

        // find path from root to node b
        findPath(root, B, arr2);

        // to store index of LCA node
        let j=0;

        // if unequal values are found
        // return previous value
        for (let i = 1; i < Math.min(arr1.length, arr2.length); i++) {
            if (arr1[i] != arr2[i]) {
                val = arr1[i - 1];
                j = i - 1;
                break;
            }
        }
        let d1 = 0, d2 = 0;

        // iterate for finding distance
        // between LCA(a, b) and a
        for (let i = j; i < arr1.length; i++)
            if (arr1[i] == A)
                break;
            else
                d1 += 1;

        // iterate for finding distance
        // between LCA(a, b) and b
        for (let i = j; i < arr2.length; i++)
            if (arr2[i] == B)
                break;
            else
                d2 += 1;
        // get distance
        val = d1 + d2;
        document.write(val);
    }

    let root = newNode(1);
    (root.child).push(newNode(2));
    (root.child).push(newNode(3));
    (root.child[0].child).push(newNode(4));
    (root.child[0].child).push(newNode(5));
    (root.child[1].child).push(newNode(6));
    (root.child[1]).child.push(newNode(7));
    (root.child[1].child).push(newNode(8));
    let A = 4, B = 3;

    // get min distance
    findMinDist(root, A, B);

// This code is contributed by decode2207.
</script>
```

**Output**

```
3
```

**时间复杂度:** O(N)。
**辅助空间:** O(N)。