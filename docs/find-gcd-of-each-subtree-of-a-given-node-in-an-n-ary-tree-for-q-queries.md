# 为 Q 查询找到 N 元树中给定节点的每个子树的 GCD

> 原文:[https://www . geeksforgeeks . org/find-gcd-of-每个给定节点的子树-in-n-ary-tree-for-q-query/](https://www.geeksforgeeks.org/find-gcd-of-each-subtree-of-a-given-node-in-an-n-ary-tree-for-q-queries/)

给定包含 **N 个**节点的 [**N 元树**](https://www.geeksforgeeks.org/generic-treesn-array-trees/) ，与每个节点相关联的**值**和 **Q** 查询，其中每个查询包含单个节点。任务是找到子树中存在的所有节点(包括自身)的值的 [**GCD**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 。

**示例:**

> 树:
> 
> ```
>            1(2)
>          /     \ 
>        /        \
>      2(3)       3(4)
>               /     \
>              /       \
>           4(8)      5(16)
> ```
> 
> 查询[]: {2，3，1}
> **输出:** {3，4，1}
> **解释:**
> 对于**查询 1** : GCD(子树(node 2))= GCD(node 2)= GCD(3)=**3**
> 对于**查询 2** : GCD(子树(node3)) = GCD(node3，node4，node5) = GCD(4，8，16)

**天真方法:**

*   对于每个查询，[遍历给定节点的整个子树](https://www.geeksforgeeks.org/queries-for-DFS-of-a-subtree-in-a-tree/)。
*   [计算子树中每个节点的 GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 并返回。

***时间复杂度** : O(Q*N)*
***空间复杂度** : O(Q*N)*

**有效方法:**

*   首先使用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-DFS-for-a-graph/)预计算每个子树的 GCD。
*   如果节点是叶节点，这个节点的 GCD 就是编号本身。
*   对于非叶节点，子树的 GCD 是其子节点的所有子树值的 GCD。
*   现在，很容易在恒定时间内找到答案，因为答案已经存储了

下面是上述方法的实现:

## C++

```
// C++ program to find GCD
// of each subtree for
// a given node by Q queries

#include <bits/stdc++.h>
using namespace std;

// Maximum Number of nodes
const int N = 1e5 + 5;

// Tree represented
// as adjacency list
vector<vector<int> > v(N);

// for storing value
// associates with node
vector<int> val(N);

// for storing GCD
// of every subarray
vector<int> answer(N);

// number of nodes
int n;

// Function to find GCD of two numbers
// using Euclidean algo
int gcd(int a, int b)
{
    // if b == 0
    // then simply return a
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// DFS function to traverse the tree
void DFS(int node, int parent)
{
    // initializing answer
    // with GCD of this node.
    answer[node] = val[node];

    // iterate over each
    // child of current node
    for (int child : v[node])
    {
        // skipping the parent
        if (child == parent)
            continue;

        // call DFS for each child
        DFS(child, node);

        // taking GCD of the answer
        // of the child to
        // find node's GCD
        answer[node] = gcd(answer[node], answer[child]);
    }
}

// Calling DFS from the root (1)
// for precomputing answers
void preprocess() { DFS(1, -1); }

// Function to find and
// print GCD for Q queries
void findGCD(int queries[], int q)
{
    // doing preprocessing
    preprocess();

    // iterate over each given query
    for (int i = 0; i < q; i++) {

        int GCD = answer[queries[i]];

        cout << "For subtree of " << queries[i]
             << ", GCD = " << GCD << endl;
    }
}

// Driver code
int main()
{
    /*
    Tree:
            1 (2)
           /     \
        2 (3)    3 (4)
                 /    \
               4 (8)   5 (16)
    */
    n = 5;

    // making a undirected tree
    v[1].push_back(2);
    v[2].push_back(1);
    v[1].push_back(3);
    v[3].push_back(1);
    v[3].push_back(4);
    v[4].push_back(3);
    v[3].push_back(5);
    v[5].push_back(3);

    // values associated with nodes
    val[1] = 2;
    val[2] = 3;
    val[3] = 4;
    val[4] = 8;
    val[5] = 16;

    int queries[] = { 2, 3, 1 };
    int q = sizeof(queries) / sizeof(queries[0]);

    // Function call
    findGCD(queries, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find GCD
// of each subtree for
// a given node by Q queries
import java.util.*;
class GFG {

    // Maximum Number of nodes
    static int N = (int)(1e5 + 5);

    // Tree represented
    // as adjacency list
    static Vector<Integer>[] v = new Vector[N];

    // For storing value
    // associates with node
    static int[] val = new int[N];

    // For storing GCD
    // of every subarray
    static int[] answer = new int[N];

    // Number of nodes
    static int n;

    // Function to find GCD of
    // two numbers using
    // Euclidean algo
    static int gcd(int a, int b)
    {
        // If b == 0
        // then simply return a
        if (b == 0)
            return a;

        return gcd(b, a % b);
    }

    // DFS function to traverse
    // the tree
    static void DFS(int node, int parent)
    {
        // Initializing answer
        // with GCD of this node.
        answer[node] = val[node];

        // Iterate over each
        // child of current node
        for (int child : v[node]) {
            // Skipping the parent
            if (child == parent)
                continue;

            // Call DFS for each child
            DFS(child, node);

            // Taking GCD of the answer
            // of the child to
            // find node's GCD
            answer[node] = gcd(answer[node], answer[child]);
        }
    }

    // Calling DFS from the root (1)
    // for precomputing answers
    static void preprocess() { DFS(1, -1); }

    // Function to find and
    // print GCD for Q queries
    static void findGCD(int queries[], int q)
    {
        // Doing preprocessing
        preprocess();

        // iterate over each given query
        for (int i = 0; i < q; i++) {
            int GCD = answer[queries[i]];
            System.out.print("For subtree of " + queries[i]
                             + ", GCD = " + GCD + "\n");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        /*
          Tree:
                  1 (2)
                 /     \
              2 (3)    3 (4)
                       /    \
                     4 (8)   5 (16)
          */

        n = 5;

        for (int i = 0; i < v.length; i++)
            v[i] = new Vector<Integer>();

        // Making a undirected tree
        v[1].add(2);
        v[2].add(1);
        v[1].add(3);
        v[3].add(1);
        v[3].add(4);
        v[4].add(3);
        v[3].add(5);
        v[5].add(3);

        // Values associated with nodes
        val[1] = 2;
        val[2] = 3;
        val[3] = 4;
        val[4] = 8;
        val[5] = 16;

        int queries[] = { 2, 3, 1 };
        int q = queries.length;

         // Function call
        findGCD(queries, q);
    }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to find GCD
# of each subtree for a
# given node by Q queries

# Maximum number of nodes
N = 10**5 + 5

# Tree represented
# as adjacency list
v = [[] for i in range(N)]

# For storing value
# associates with node
val = [0] * (N)

# For storing GCD
# of every subarray
answer = [0] * (N)

# Number of nodes
n = 0

# Function to find GCD of two
# numbers. Using Euclidean algo

def gcd(a, b):

    # If b == 0 then
    # simply return a
    if (b == 0):
        return a

    return gcd(b, a % b)

# DFS function to traverse the tree

def DFS(node, parent):

    # Initializing answer
    # with GCD of this node.
    answer[node] = val[node]

    # Iterate over each
    # child of current node
    for child in v[node]:

        # Skipping the parent
        if (child == parent):
            continue

        # Call DFS for each child
        DFS(child, node)

        # Taking GCD of the answer
        # of the child to
        # find node's GCD
        answer[node] = gcd(answer[node],
                           answer[child])

# Calling DFS from the root (1)
# for precomputing answers

def preprocess():

    DFS(1, -1)

# Function to find and
# prGCD for Q queries

def findGCD(queries, q):

    # Doing preprocessing
    preprocess()

    # Iterate over each given query
    for i in range(q):
        GCD = answer[queries[i]]

        print("For subtree of ", queries[i],
              ", GCD = ", GCD)

# Driver code
if __name__ == '__main__':

    """
    Tree:
            1 (2)
          /         \
       2 (3)     3 (4)
                /     \
              4 (8)    5 (16)
    """

    n = 5

    # Making a undirected tree
    v[1].append(2)
    v[2].append(1)
    v[1].append(3)
    v[3].append(1)
    v[3].append(4)
    v[4].append(3)
    v[3].append(5)
    v[5].append(3)

    # Values associated with nodes
    val[1] = 2
    val[2] = 3
    val[3] = 4
    val[4] = 8
    val[5] = 16

    queries = [2, 3, 1]
    q = len(queries)

    # Function call
    findGCD(queries, q)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find GCD
// of each subtree for
// a given node by Q queries
using System;
using System.Collections.Generic;

public class GFG {

    // Maximum Number of nodes
    static int N = (int)(1e5 + 5);

    // Tree represented
    // as adjacency list
    static List<int>[] v = new List<int>[ N ];

    // For storing value
    // associates with node
    static int[] val = new int[N];

    // For storing GCD
    // of every subarray
    static int[] answer = new int[N];

    // Number of nodes
    static int n;

    // Function to find GCD of
    // two numbers using
    // Euclidean algo
    static int gcd(int a, int b)
    {
        // If b == 0
        // then simply return a
        if (b == 0)
            return a;

        return gcd(b, a % b);
    }

    // DFS function to traverse
    // the tree
    static void DFS(int node, int parent)
    {
        // Initializing answer
        // with GCD of this node.
        answer[node] = val[node];

        // Iterate over each
        // child of current node
        foreach(int child in v[node])
        {
            // Skipping the parent
            if (child == parent)
                continue;

            // Call DFS for each child
            DFS(child, node);

            // Taking GCD of the answer
            // of the child to
            // find node's GCD
            answer[node] = gcd(answer[node], answer[child]);
        }
    }

    // Calling DFS from the root (1)
    // for precomputing answers
    static void preprocess() { DFS(1, -1); }

    // Function to find and
    // print GCD for Q queries
    static void findGCD(int[] queries, int q)
    {
        // Doing preprocessing
        preprocess();

        // iterate over each given query
        for (int i = 0; i < q; i++) {
            int GCD = answer[queries[i]];
            Console.Write("For subtree of " + queries[i]
                          + ", GCD = " + GCD + "\n");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        /*
          Tree:
                  1 (2)
                 /     \
              2 (3)    3 (4)
                       /    \
                     4 (8)   5 (16)
          */

        n = 5;

        for (int i = 0; i < v.Length; i++)
            v[i] = new List<int>();

        // Making a undirected tree
        v[1].Add(2);
        v[2].Add(1);
        v[1].Add(3);
        v[3].Add(1);
        v[3].Add(4);
        v[4].Add(3);
        v[3].Add(5);
        v[5].Add(3);

        // Values associated with nodes
        val[1] = 2;
        val[2] = 3;
        val[3] = 4;
        val[4] = 8;
        val[5] = 16;

        int[] queries = { 2, 3, 1 };
        int q = queries.Length;
        findGCD(queries, q);
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to find GCD
// of each subtree for
// a given node by Q queries

// Maximum Number of nodes
var N = 100005;

// Tree represented
// as adjacency list
var v = Array.from(Array(N), ()=>Array());

// for storing value
// associates with node
var val = Array(N);

// for storing GCD
// of every subarray
var answer = Array(N);

// number of nodes
var n;

// Function to find GCD of two numbers
// using Euclidean algo
function gcd(a, b)
{

    // If b == 0
    // then simply return a
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// DFS function to traverse the tree
function DFS(node, parent)
{

    // Initializing answer
    // with GCD of this node.
    answer[node] = val[node];

    // Iterate over each
    // child of current node
    v[node].forEach(child => {

        // Skipping the parent
        if (child != parent)
        {

        // Call DFS for each child
        DFS(child, node);

        // Taking GCD of the answer
        // of the child to
        // find node's GCD
        answer[node] = gcd(answer[node], answer[child]);
        }
    });
}

// Calling DFS from the root (1)
// for precomputing answers
function preprocess()
{
    DFS(1, -1);
}

// Function to find and
// print GCD for Q queries
function findGCD(queries, q)
{

    // Doing preprocessing
    preprocess();

    // Iterate over each given query
    for(var i = 0; i < q; i++)
    {
        var GCD = answer[queries[i]];

        document.write("For subtree of " + queries[i] +
                       ", GCD = " + GCD + "<br>");
    }
}

// Driver code
/*
Tree:
        1 (2)
       /     \
    2 (3)    3 (4)
             /    \
           4 (8)   5 (16)
*/
n = 5;

// Making a undirected tree
v[1].push(2);
v[2].push(1);
v[1].push(3);
v[3].push(1);
v[3].push(4);
v[4].push(3);
v[3].push(5);
v[5].push(3);

// Values associated with nodes
val[1] = 2;
val[2] = 3;
val[3] = 4;
val[4] = 8;
val[5] = 16;
var queries = [ 2, 3, 1 ];
var q = queries.length;

// Function call
findGCD(queries, q);

// This code is contributed by itsok

</script>
```

**Output**

```
For subtree of 2, GCD = 3
For subtree of 3, GCD = 4
For subtree of 1, GCD = 1
```

***时间复杂度:** O(N + Q)*
***空间复杂度:** O(N)*