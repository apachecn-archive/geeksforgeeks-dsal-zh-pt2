# 组成一个长度为 K 的回文字符串的字符串连接所需替换的最少字符数

> 原文:[https://www . geesforgeks . org/最少要替换的字符-字符串-k 长度的串联-回文字符串/](https://www.geeksforgeeks.org/minimum-characters-to-be-replaced-to-make-a-string-concatenation-of-a-k-length-palindromic-string/)

给定一个大小为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和一个正整数 **K** (其中 **N % K = 0)** ，任务是找到需要替换的最小字符数，使得该字符串为**K**-周期，并且 **K** 长度的周期字符串必须为[回文](https://www.geeksforgeeks.org/tag/palindrome/)。

**示例:**

> **输入:**S =“abaaba”，K = 3
> **输出:** 0
> **说明:**给定的字符串已经是 K 周期的，周期字符串“aba”是回文。
> 
> **输入:**S = " abaababa "，K = 2
> **输出:** 2
> **解释:**通过将索引 1 和 4 处的字符改为' a '，更新后的 sting“AAA”为 K 周期，周期字符串“aa”为回文。因此，所需的最小更改为 2。

**方法:**想法是根据给定的字符串索引创建一个[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)，并执行 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)来找到所需的更改数量。按照下面的步骤来解决这个问题:

*   将变量**总计**初始化为 **0** ，以存储所需更改的计数。
*   根据给定的条件，从字符串创建一个图形，在最后的字符串中，所有位置 **i，K I+1，K + i，2K I+1，2K + i，3K I+1，…** 的所有字符 **1 ≤ i ≤ K** 应该相等。
*   迭代范围**【0，N】**，并在索引 **i** 和**(N–I–1)**之间添加一条无向边。
*   迭代范围**【0，N–M】**，并在索引 **i** 和 **(i + K)** 之间添加一条无向边。
*   为了最小化所需的操作次数，使所有的字母与出现在这些位置最多的字母相等，这可以通过在字符串上执行 [DFS 遍历](https://www.geeksforgeeks.org/iterative-depth-first-traversal/)很容易地找到。
*   对于所有未访问的节点，在创建的图上执行 [**DFS 遍历**](https://www.geeksforgeeks.org/print-the-dfs-traversal-step-wise-backtracking-also/) :
    *   在该遍历中找到被访问字符中出现频率最高的最大元素(比如**最大频率**)。
    *   通过 **DFS 遍历**中所有访问字符的计数与上一步最大频率的差值，更新字符变化的总数。
*   完成以上步骤后，打印**合计**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function to add an edge to graph
void addEdge(vector<int> adj[], int u,
             int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// Function to perform DFS traversal on the
// graph recursively from a given vertex u
void DFS(int u, vector<int> adj[],
         int& cnt, vector<bool>& visited,
         int fre[], string S)
{
    // Visit the current vertex
    visited[u] = true;

    // Total number of nodes
    // in this component
    cnt++;

    // Increment the frequency of u
    fre[S[u] - 'a']++;

    for (int i = 0;
         i < adj[u].size(); i++) {
        if (!visited[adj[u][i]]) {
            DFS(adj[u][i], adj, cnt,
                visited, fre, S);
        }
    }
}

// Function for finding the minimum
// number changes required in given string
int minimumOperations(string& S, int m)
{
    int V = 100;
    vector<int> adj[V];
    int total = 0, N = S.length();

    // Form the edges according to the
    // given conditions
    for (int i = 0; i < N; i++) {
        addEdge(adj, i, N - i - 1);
        addEdge(adj, N - i - 1, i);
    }

    for (int i = 0; i < N - m; i++) {
        addEdge(adj, i, i + m);
        addEdge(adj, i + m, i);
    }

    // Find minimum number of operations
    vector<bool> visited(V, 0);

    for (int i = 0; i < N; i++) {

        // Frequency array for finding
        // the most frequent character
        if (!visited[i]) {

            // Frequency array for finding
            // the most frequent character
            int fre[26] = { 0 };
            int cnt = 0, maxx = -1;

            DFS(i, adj, cnt, visited, fre, S);

            // Finding most frequent character
            for (int j = 0; j < 26; j++)
                maxx = max(maxx, fre[j]);

            // Change rest of the characters
            // to most frequent one
            total += cnt - maxx;
        }
    }

    // Print total number of changes
    cout << total;
}

// Driver Code
int main()
{
    string S = "abaaba";
    int K = 2;

    // Function Call
    minimumOperations(S, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to add an edge to graph
static void addEdge(Vector<Integer> adj[], int u,
                                           int v)
{
    adj[u].add(v);
    adj[v].add(u);
}

static int cnt = 0;
static boolean[] visited;

// Function to perform DFS traversal on the
// graph recursively from a given vertex u
static void DFS(int u, Vector<Integer> adj[],
                int fre[], String S)
{

    // Visit the current vertex
    visited[u] = true;

    // Total number of nodes
    // in this component
    cnt++;

    // Increment the frequency of u
    fre[S.charAt(u) - 'a']++;

    for(int i = 0; i < adj[u].size(); i++)
    {
        if (!visited[adj[u].get(i)])
        {
            DFS(adj[u].get(i), adj, fre, S);
        }
    }
}

// Function for finding the minimum
// number changes required in given String
static void minimumOperations(String S, int m)
{
    int V = 100;
    @SuppressWarnings("unchecked")
    Vector<Integer> []adj = new Vector[V];

    int total = 0, N = S.length();

    for(int i = 0; i < adj.length; i++)
        adj[i] = new Vector<Integer>();

    // Form the edges according to the
    // given conditions
    for(int i = 0; i < N; i++)
    {
        addEdge(adj, i, N - i - 1);
        addEdge(adj, N - i - 1, i);
    }

    for(int i = 0; i < N - m; i++)
    {
        addEdge(adj, i, i + m);
        addEdge(adj, i + m, i);
    }

    // Find minimum number of operations
    visited =  new boolean[V];
    for(int i = 0; i < N; i++)
    {

        // Frequency array for finding
        // the most frequent character
        if (!visited[i])
        {

            // Frequency array for finding
            // the most frequent character
            int fre[] = new int[26];
            cnt = 0;
            int maxx = -1;

            DFS(i, adj, fre, S);

            // Finding most frequent character
            for(int j = 0; j < 26; j++)
                maxx = Math.max(maxx, fre[j]);

            // Change rest of the characters
            // to most frequent one
            total += cnt - maxx;
        }
    }

    // Print total number of changes
    System.out.print(total);
}

// Driver Code
public static void main(String[] args)
{
    String S = "abaaba";
    int K = 2;

    // Function Call
    minimumOperations(S, K);
}
}

// This code is contributed by aashish1995
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys
sys.setrecursionlimit(1500)

# Function to add an edge to graph
def addEdge(u, v):

    global adj
    adj[u].append(v)
    adj[v].append(u)

# Function to perform DFS traversal on the
# graph recursively from a given vertex u
def DFS(u, fre, S):

    global visited, adj, cnt

    # Visit the current vertex
    visited[u] = 1

    # Total number of nodes
    # in this component
    cnt += 1

    # Increment the frequency of u
    fre[ord(S[u]) - ord('a')] += 1

    for i in adj[u]:
        if (visited[i] == 0):
            DFS(i, fre, S)

# Function for finding the minimum
# number changes required in given string
def minimumOperations(S, m):

    global adj, visited, cnt

    total, N = 0, len(S)

    # Form the edges according to the
    # given conditions
    for i in range(N):
        addEdge(i, N - i - 1)
        addEdge(N - i - 1, i)

    for i in range(N-m):
        addEdge(i, i + m)
        addEdge(i + m, i)

    for i in range(N):

        # Frequency array for finding
        # the most frequent character
        if (not visited[i]):

            # Frequency array for finding
            # the most frequent character
            fre = [0] * 26
            cnt, maxx = 0, -1

            DFS(i, fre, S)

            # Finding most frequent character
            for j in range(26):
                maxx = max(maxx, fre[j])

            # Change rest of the characters
            # to most frequent one
            total += cnt - maxx

    # Print total number of changes
    print (total)

# Driver Code
if __name__ == '__main__':

    adj = [[] for i in range(101)]
    visited, cnt = [0 for i in range(101)], 0

    S = "abaaba"
    K = 2

    # Function Call
    minimumOperations(S, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to add an edge to graph
static void addEdge(List<int> []adj, int u,
                                     int v)
{
    adj[u].Add(v);
    adj[v].Add(u);
}

static int cnt = 0;
static bool[] visited;

// Function to perform DFS traversal on the
// graph recursively from a given vertex u
static void DFS(int u, List<int> []adj,
                int []fre, String S)
{

    // Visit the current vertex
    visited[u] = true;

    // Total number of nodes
    // in this component
    cnt++;

    // Increment the frequency of u
    fre[S[u] - 'a']++;

    for(int i = 0; i < adj[u].Count; i++)
    {
        if (!visited[adj[u][i]])
        {
            DFS(adj[u][i], adj, fre, S);
        }
    }
}

// Function for finding the minimum
// number changes required in given String
static void minimumOperations(String S, int m)
{
    int V = 100;

    List<int> []adj = new List<int>[V];

    int total = 0, N = S.Length;

    for(int i = 0; i < adj.Length; i++)
        adj[i] = new List<int>();

    // Form the edges according to the
    // given conditions
    for(int i = 0; i < N; i++)
    {
        addEdge(adj, i, N - i - 1);
        addEdge(adj, N - i - 1, i);
    }

    for(int i = 0; i < N - m; i++)
    {
        addEdge(adj, i, i + m);
        addEdge(adj, i + m, i);
    }

    // Find minimum number of operations
    visited =  new bool[V];
    for(int i = 0; i < N; i++)
    {

        // Frequency array for finding
        // the most frequent character
        if (!visited[i])
        {

            // Frequency array for finding
            // the most frequent character
            int []fre = new int[26];
            cnt = 0;
            int maxx = -1;

            DFS(i, adj, fre, S);

            // Finding most frequent character
            for(int j = 0; j < 26; j++)
                maxx = Math.Max(maxx, fre[j]);

            // Change rest of the characters
            // to most frequent one
            total += cnt - maxx;
        }
    }

    // Print total number of changes
    Console.Write(total);
}

// Driver Code
public static void Main(String[] args)
{
    String S = "abaaba";
    int K = 2;

    // Function Call
    minimumOperations(S, K);
}
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to add an edge to graph
    function addEdge(adj, u, v)
    {
        adj[u].push(v);
        adj[v].push(u);
    }

    let cnt = 0;
    let visited;

    // Function to perform DFS traversal on the
    // graph recursively from a given vertex u
    function DFS(u, adj, fre, S)
    {

        // Visit the current vertex
        visited[u] = true;

        // Total number of nodes
        // in this component
        cnt++;

        // Increment the frequency of u
        fre[S[u].charCodeAt() - 'a'.charCodeAt()]++;

        for(let i = 0; i < adj[u].length; i++)
        {
            if (!visited[adj[u][i]])
            {
                DFS(adj[u][i], adj, fre, S);
            }
        }
    }

    // Function for finding the minimum
    // number changes required in given String
    function minimumOperations(S, m)
    {
        let V = 100;

        let adj = [];
        for(let i = 0; i < V; i++)
        {
            adj.push([]);
        }

        let total = 0, N = S.length;

        for(let i = 0; i < adj.length; i++)
            adj[i] = [];

        // Form the edges according to the
        // given conditions
        for(let i = 0; i < N; i++)
        {
            addEdge(adj, i, N - i - 1);
            addEdge(adj, N - i - 1, i);
        }

        for(let i = 0; i < N - m; i++)
        {
            addEdge(adj, i, i + m);
            addEdge(adj, i + m, i);
        }

        // Find minimum number of operations
        visited =  new Array(V);
        visited.fill(false);
        for(let i = 0; i < N; i++)
        {

            // Frequency array for finding
            // the most frequent character
            if (!visited[i])
            {

                // Frequency array for finding
                // the most frequent character
                let fre = new Array(26);
                fre.fill(0);
                cnt = 0;
                let maxx = -1;

                DFS(i, adj, fre, S);

                // Finding most frequent character
                for(let j = 0; j < 26; j++)
                    maxx = Math.max(maxx, fre[j]);

                // Change rest of the characters
                // to most frequent one
                total += cnt - maxx;
            }
        }

        // Print total number of changes
        document.write(total);
    }

    // Driver code
    let S = "abaaba";
    let K = 2;

    // Function Call
    minimumOperations(S, K);

    // This code is contributed by decode2207.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)