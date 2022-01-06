# 加权串为回文的树的叶节点数

> 原文:[https://www . geesforgeks . org/树的叶节点数-其加权字符串是回文/](https://www.geeksforgeeks.org/count-of-leaf-nodes-of-the-tree-whose-weighted-string-is-a-palindrome/)

给定一棵 [**N 元树**](https://www.geeksforgeeks.org/generic-treesn-array-trees/) ，以及所有节点的字符串形式的权重，任务是计算权重为回文的叶节点的数量。

**示例:**

```
Input: 
               1(ab)
              /  \
       (abca)2     5 (aba)
          /   \ 
   (axxa)3     4 (geeks)
Output: 2
Explanation: 
Only the weights of the leaf nodes
"axxa" and "aba" are palindromes.

Input: 
               1(abx)
              /  
            2(abaa) 
           /    
          3(amma)  
Output: 1
Explanation: 
Only the weight of the leaf
node "amma" is palindrome.
```

**方法:**要解决上述问题，请遵循以下步骤:

*   [深度优先搜索](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)可以用来遍历完整的树。
*   我们将在遍历时跟踪父节点，以避免访问节点数组。
*   最初，我们可以为每个节点设置一个标志，如果该节点至少有一个子节点(即非叶节点)，那么我们将重置该标志。
*   没有子节点的节点是叶节点。对于每个叶节点，我们将检查它的字符串是否是回文。如果是，则增加计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

int cnt = 0;

vector<int> graph[100];
vector<string> weight(100);

// Function that returns true
// if x is a palindrome
bool isPalindrome(string x)
{
    int n = x.size();
    for (int i = 0; i < n / 2; i++) {
        if (x[i] != x[n - 1 - i])
            return false;
    }
    return true;
}

// Function to perform DFS on the tree
void dfs(int node, int parent)
{
    int flag = 1;

    // Iterating the children of current node
    for (int to : graph[node]) {

        // There is at least a child
        // of the current node
        if (to == parent)
            continue;
        flag = 0;
        dfs(to, node);
    }

    // Current node is connected to only
    // its parent i.e. it is a leaf node
    if (flag == 1) {
        // Weight of the current node
        string x = weight[node];

        // If the weight is a palindrome
        if (isPalindrome(x))
            cnt += 1;
    }
}

// Driver code
int main()
{

    // Weights of the node
    weight[1] = "ab";
    weight[2] = "abca";
    weight[3] = "axxa";
    weight[4] = "geeks";
    weight[5] = "aba";

    // Edges of the tree
    graph[1].push_back(2);
    graph[2].push_back(3);
    graph[2].push_back(4);
    graph[1].push_back(5);

    dfs(1, 1);

    cout << cnt;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG{

static int cnt = 0;

static Vector<Integer> []graph = new Vector[100];
static String []weight = new String[100];

// Function that returns true
// if x is a palindrome
static boolean isPalindrome(String x)
{
    int n = x.length();
    for (int i = 0; i < n / 2; i++)
    {
        if (x.charAt(i) != x.charAt(n - 1 - i))
            return false;
    }
    return true;
}

// Function to perform DFS on the tree
static void dfs(int node, int parent)
{
    int flag = 1;

    // Iterating the children of current node
    for (int to : graph[node])
    {

        // There is at least a child
        // of the current node
        if (to == parent)
            continue;
        flag = 0;
        dfs(to, node);
    }

    // Current node is connected to only
    // its parent i.e. it is a leaf node
    if (flag == 1)
    {
        // Weight of the current node
        String x = weight[node];

        // If the weight is a palindrome
        if (isPalindrome(x))
            cnt += 1;
    }
}

// Driver code
public static void main(String[] args)
{
    for(int i = 0; i < graph.length;i++)
        graph[i] = new Vector<Integer>();

    // Weights of the node
    weight[1] = "ab";
    weight[2] = "abca";
    weight[3] = "axxa";
    weight[4] = "geeks";
    weight[5] = "aba";

    // Edges of the tree
    graph[1].add(2);
    graph[2].add(3);
    graph[2].add(4);
    graph[1].add(5);

    dfs(1, 1);

    System.out.print(cnt);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation of the approach
cnt = 0

graph = [0] * 100
for i in range(100):
    graph[i] = []

weight = [0] * 100

# Function that returns true
# if x is a palindrome
def isPalindrome(x: str) -> bool:

    n = len(x)

    for i in range(n // 2):
        if (x[i] != x[n - 1 - i]):
            return False

    return True

# Function to perform DFS on the tree
def dfs(node: int, parent: int) -> None:

    global cnt, graph, weight

    flag = 1

    # Iterating the children of current node
    for to in graph[node]:

        # There is at least a child
        # of the current node
        if (to == parent):
            continue

        flag = 0
        dfs(to, node)

    # Current node is connected to only
    # its parent i.e. it is a leaf node
    if (flag == 1):

        # Weight of the current node
        x = weight[node]

        # If the weight is a palindrome
        if (isPalindrome(x)):
            cnt += 1

# Driver code
if __name__ == "__main__":

    # Weights of the node
    weight[1] = "ab"
    weight[2] = "abca"
    weight[3] = "axxa"
    weight[4] = "geeks"
    weight[5] = "aba"

    # Edges of the tree
    graph[1].append(2)
    graph[2].append(3)
    graph[2].append(4)
    graph[1].append(5)

    dfs(1, 1)

    print(cnt)

# This code is contributed by sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG{

static int cnt = 0;

static List<int> []graph = new List<int>[100];
static String []weight = new String[100];

// Function that returns true
// if x is a palindrome
static bool isPalindrome(String x)
{
    int n = x.Length;
    for(int i = 0; i < n / 2; i++)
    {
       if (x[i] != x[n - 1 - i])
           return false;
    }
    return true;
}

// Function to perform DFS on the tree
static void dfs(int node, int parent)
{
    int flag = 1;

    // Iterating the children of
    // current node
    foreach (int to in graph[node])
    {

        // There is at least a child
        // of the current node
        if (to == parent)
            continue;
        flag = 0;
        dfs(to, node);
    }

    // Current node is connected to only
    // its parent i.e. it is a leaf node
    if (flag == 1)
    {

        // Weight of the current node
        String x = weight[node];

        // If the weight is a palindrome
        if (isPalindrome(x))
            cnt += 1;
    }
}

// Driver code
public static void Main(String[] args)
{
    for(int i = 0; i < graph.Length; i++)
       graph[i] = new List<int>();

    // Weights of the node
    weight[1] = "ab";
    weight[2] = "abca";
    weight[3] = "axxa";
    weight[4] = "geeks";
    weight[5] = "aba";

    // Edges of the tree
    graph[1].Add(2);
    graph[2].Add(3);
    graph[2].Add(4);
    graph[1].Add(5);

    dfs(1, 1);

    Console.Write(cnt);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    let cnt = 0;

    let graph = new Array(100);
    let weight = new Array(100);

    // Function that returns true
    // if x is a palindrome
    function isPalindrome(x)
    {
        let n = x.length;
        for (let i = 0; i < parseInt(n / 2, 10); i++)
        {
            if (x[i] != x[n - 1 - i])
                return false;
        }
        return true;
    }

    // Function to perform DFS on the tree
    function dfs(node, parent)
    {
        let flag = 1;

        // Iterating the children of current node
        for (let to = 0; to < graph[node].length; to++)
        {

            // There is at least a child
            // of the current node
            if (graph[node][to] == parent)
                continue;
            flag = 0;
            dfs(graph[node][to], node);
        }

        // Current node is connected to only
        // its parent i.e. it is a leaf node
        if (flag == 1)
        {
            // Weight of the current node
            let x = weight[node];

            // If the weight is a palindrome
            if (isPalindrome(x))
                cnt += 1;
        }
    }

    for(let i = 0; i < graph.length;i++)
        graph[i] = [];

    // Weights of the node
    weight[1] = "ab";
    weight[2] = "abca";
    weight[3] = "axxa";
    weight[4] = "geeks";
    weight[5] = "aba";

    // Edges of the tree
    graph[1].push(2);
    graph[2].push(3);
    graph[2].push(4);
    graph[1].push(5);

    dfs(1, 1);

    document.write(cnt);

</script>
```

**Output:** 

```
2
```