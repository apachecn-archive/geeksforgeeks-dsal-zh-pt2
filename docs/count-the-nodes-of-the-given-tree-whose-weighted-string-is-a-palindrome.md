# 计算给定树的节点，该树的加权字符串是回文

> 原文:[https://www . geeksforgeeks . org/count-给定树的节点，其加权字符串是回文/](https://www.geeksforgeeks.org/count-the-nodes-of-the-given-tree-whose-weighted-string-is-a-palindrome/)

给定一棵树和所有节点的权重(以字符串的形式)，任务是计算权重为回文的节点。

**示例:**

```
Input: 
```

![](img/1072d87c927642435bb7140f38e12567.png)

```
Output: 3
Only the weights of the nodes 2, 3 and 5 are palindromes.
```

**方法:**对树执行 [dfs](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，对于每个节点，检查它的字符串是否是回文。如果是，则增加计数。

**实施:**

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

// Function to perform dfs
void dfs(int node, int parent)
{

    // Weight of the current node
    string x = weight[node];

    // If the weight is a palindrome
    if (isPalindrome(x))
        cnt += 1;

    for (int to : graph[node]) {
        if (to == parent)
            continue;
        dfs(to, node);
    }
}

// Driver code
int main()
{

    // Weights of the node
    weight[1] = "abc";
    weight[2] = "aba";
    weight[3] = "bcb";
    weight[4] = "moh";
    weight[5] = "aa";

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

class GFG
{

static int cnt = 0;

static Vector<Vector<Integer>> graph = new Vector<Vector<Integer>>();
static Vector<String> weight = new Vector<String>();

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

// Function to perform dfs
static void dfs(int node, int parent)
{

    // Weight of the current node
    String x = weight.get(node);

    // If the weight is a palindrome
    if (isPalindrome(x))
        cnt += 1;

    for (int i=0;i<graph.get(node).size();i++)
    {

        if ( graph.get(node).get(i)== parent)
            continue;
        dfs(graph.get(node).get(i), node);
    }
}

// Driver code
public static void main(String args[])
{

    // Weights of the node
    weight.add( "");
    weight.add( "abc");
    weight.add( "aba");
    weight.add( "bcb");
    weight.add( "moh");
    weight.add( "aa");

    for(int i = 0; i < 100; i++)
    graph.add(new Vector<Integer>());

    // Edges of the tree
    graph.get(1).add(2);
    graph.get(2).add(3);
    graph.get(2).add(4);
    graph.get(1).add(5);
    dfs(1, 1);

    System.out.println( cnt);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
cnt = 0

graph = [0] * 100
for i in range(100):
    graph[i] = []

weight = ["0"] * 100

# Function that returns true
# if x is a palindrome
def isPalindrome(x):
    n = len(x)

    for i in range(0, n // 2):
        if x[i] != x[n - 1 - i]:
            return False

    return True

# Function to perform dfs
def dfs(node, parent):
    global cnt

    # Weight of the current node
    x = weight[node]

    # If the weight is a palindrome
    if (isPalindrome(x)):
        cnt += 1

    for to in graph[node]:
        if to == parent:
            continue
        dfs(to, node)

# Driver Code
if __name__ == "__main__":

    # Weights of the node
    weight[0] = ""
    weight[1] = "abc"
    weight[2] = "aba"
    weight[3] = "bcb"
    weight[4] = "moh"
    weight[5] = "aa"

    # Edges of the tree
    graph[1].append(2)
    graph[2].append(3)
    graph[2].append(4)
    graph[1].append(5)

    dfs(1, 1)

    print(cnt)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    static int cnt = 0;

    static List<List<int>> graph = new List<List<int>>();
    static List<String> weight = new List<String>();

    // Function that returns true
    // if x is a palindrome
    static bool isPalindrome(string x)
    {
        int n = x.Length;
        for (int i = 0; i < n / 2; i++)
        {
            if (x[i] != x[n - 1 - i])
                return false;
        }
        return true;
    }

    // Function to perform dfs
    static void dfs(int node, int parent)
    {

        // Weight of the current node
        String x = weight[node];

        // If the weight is a palindrome
        if (isPalindrome(x))
            cnt += 1;

        for (int i = 0; i < graph[node].Count; i++)
        {
            if (graph[node][i] == parent)
                continue;
            dfs(graph[node][i], node);
        }
    }

    // Driver code
    public static void Main(String []args)
    {

        // Weights of the node
        weight.Add( "");
        weight.Add( "abc");
        weight.Add( "aba");
        weight.Add( "bcb");
        weight.Add( "moh");
        weight.Add( "aa");

        for(int i = 0; i < 100; i++)
        graph.Add(new List<int>());

        // Edges of the tree
        graph[1].Add(2);
        graph[2].Add(3);
        graph[2].Add(4);
        graph[1].Add(5);

        dfs(1, 1);

        Console.WriteLine( cnt);

    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
let cnt = 0;

let graph = new Array(100);
let weight = new Array(100);
for(let i = 0; i < 100; i++)
{
    graph[i] = [];
    weight[i] = 0;
}

// Function that returns true
// if x is a palindrome
function isPalindrome(x)
{
    let n = x.length;
    for(let i = 0; i < n / 2; i++)
    {
        if (x[i] != x[n - 1 - i])
            return false;
    }
    return true;
}

// Function to perform dfs
function dfs(node, parent)
{

    // Weight of the current node
    let x = weight[node];

    // If the weight is a palindrome
    if (isPalindrome(x))
        cnt += 1;

    for(let to = 0; to < graph[node].length; to++)
    {
        if (graph[node][to] == parent)
            continue

        dfs(graph[node][to], node); 
    }
}

// Driver code

// Weights of the node
weight[1] = "abc";
weight[2] = "aba";
weight[3] = "bcb";
weight[4] = "moh";
weight[5] = "aa";

// Edges of the tree
graph[1].push(2);
graph[2].push(3);
graph[2].push(4);
graph[1].push(5);

dfs(1, 1);

document.write(cnt);

// This code is contributed by Dharanendra L V.

</script>
```

**Output:** 

```
3
```

**复杂度分析:**

*   **时间复杂度:** O(N*Len)，其中 Len 是给定树中节点的加权串的最大长度。
    在 DFS 中，树的每个节点都被处理一次，因此对于树中的 N 个节点，由于 DFS 而导致的复杂性是 O(N)。此外，每个节点的处理都涉及遍历该节点的加权字符串一次，因此增加了 O(Len)的复杂性，其中 Len 是加权字符串的长度。因此，总时间复杂度为 O(N*Len)。
*   **辅助空间:** O(1)。
    不需要任何额外的空间，所以空间复杂度不变。