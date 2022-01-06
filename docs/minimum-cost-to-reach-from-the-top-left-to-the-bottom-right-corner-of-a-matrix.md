# 从矩阵左上角到右下角的最小花费

> 原文:[https://www . geeksforgeeks . org/从矩阵左上角到右下角的最小到达成本/](https://www.geeksforgeeks.org/minimum-cost-to-reach-from-the-top-left-to-the-bottom-right-corner-of-a-matrix/)

给定一个由小写字符组成的 **N * M** 矩阵 **mat[][]** ，任务是找到从单元格 **mat[0][0]** 到单元格 **mat[N-1][M-1]** 的最小开销。如果你在一个单元格 **mat[i][j]** ，你可以跳至单元格 **mat[i+1][j]** ， **mat[i][j+1]** ， **mat[i-1][j]** ， **mat[i][j-1]** (不出界)，费用为 **1** 。此外，您可以跳转到任何单元格 **mat[m][n]** ，这样 **mat[n][m] = mat[i][j]** ，代价为 **0** 。
**举例:**

> **输入:**mat[][]= {“ABC”、“efg”、“hij”}
> **输出:** 4
> 最短路径之一将为:
> {0，0} - > {0，1} - > {0，2} - > {1，2} - > {2，2}
> 所有边的权重为 1，因此答案为 4。
> **输入:**mat[][]= {“ABC”、“efg”、“hbj”}
> **输出:** 2
> {0，0} - > {0，1} - > {2，1} - > {2，2}
> 1 + 0 + 1 = 2

**天真的做法:**解决这个问题的一种做法是 [0-1 BFS](https://www.geeksforgeeks.org/0-1-bfs-shortest-path-binary-graph/) 。将设置可视化为带有 **N * M** 节点的图形。所有节点都将连接到相邻节点，边长为 **1** 的节点和相同字符的边长为 **0** 的节点。现在，BFS 可以用来寻找从单元**垫【0】【0】**到单元垫【N-1】【M-1】的最短路径。其时间复杂度为 **O((N * M) <sup>2</sup> )** ，因为边数为 O((N * M) <sup>2</sup> 的数量级。
**高效方法:**对于每个字符 **X** ，找到与其相邻的所有字符。现在，创建一个图表，其中多个节点是字符串中不同字符的数量，每个字符代表一个字符。
每个节点 **X** 将有一个权重边缘 **1** ，所有节点都表示实图中与字符 **X** 相邻的字符。那么在这个新图中，BFS 可以从表示 **mat[0][0]** 的节点运行到表示 **mat[N-1][M-1]** 的节点。这种方法的时间复杂度为 **O(N * M)** 用于预处理图形，运行 BFS 的时间复杂度可以认为是恒定的。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 26;

// Function to return
// the value (x - 97)
int f(int x)
{
    return x - 'a';
}

// Function to return the minimum cost
int findMinCost(vector<string> arr)
{
    int n = arr.size();
    int m = arr[0].size();

    // Graph
    vector<vector<int> > gr(MAX);

    // Adjacency matrix
    bool edge[MAX][MAX];

    // Initialising the adjacency matrix
    for (int k = 0; k < MAX; k++)
        for (int l = 0; l < MAX; l++)
            edge[k][l] = 0;

    // Creating the adjacency matrix
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++) {
            if (i + 1 < n and !edge[f(arr[i][j])][f(arr[i + 1][j])]) {
                gr[f(arr[i][j])].push_back(f(arr[i + 1][j]));
                edge[f(arr[i][j])][f(arr[i + 1][j])] = 1;
            }
            if (j - 1 >= 0 and !edge[f(arr[i][j])][f(arr[i][j - 1])]) {
                gr[f(arr[i][j])].push_back(f(arr[i][j - 1]));
                edge[f(arr[i][j])][f(arr[i][j - 1])] = 1;
            }
            if (j + 1 < m and !edge[f(arr[i][j])][f(arr[i][j + 1])]) {
                gr[f(arr[i][j])].push_back(f(arr[i][j + 1]));
                edge[f(arr[i][j])][f(arr[i][j + 1])] = 1;
            }
            if (i - 1 >= 0 and !edge[f(arr[i][j])][f(arr[i - 1][j])]) {
                gr[f(arr[i][j])].push_back(f(arr[i - 1][j]));
                edge[f(arr[i][j])][f(arr[i - 1][j])] = 1;
            }
        }

    // Queue to perform BFS
    queue<int> q;
    q.push(arr[0][0] - 'a');

    // Visited array
    bool v[MAX] = { 0 };

    // To store the depth of BFS
    int d = 0;

    // BFS
    while (q.size()) {

        // Number of elements in
        // the current level
        int cnt = q.size();

        // Inner loop
        while (cnt--) {

            // Current element
            int curr = q.front();

            // Popping queue
            q.pop();

            // If the current node has
            // already been visited
            if (v[curr])
                continue;
            v[curr] = 1;

            // Checking if the current
            // node is the required node
            if (curr == arr[n - 1][m - 1] - 'a')
                return d;

            // Iterating through the current node
            for (auto it : gr[curr])
                q.push(it);
        }

        // Updating the depth
        d++;
    }

    return -1;
}

// Driver code
int main()
{
    vector<string> arr = { "abc",
                           "def",
                           "gbi" };

    cout << findMinCost(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    static int MAX = 26;

    // Function to return
    // the value (x - 97)
    static int f(int x)
    {
        return x - 'a';
    }

    // Function to return the minimum cost
    static int findMinCost(String[] arr)
    {
        int n = arr.length;
        int m = arr[0].length();

        // Graph
        Vector<Integer>[] gr = new Vector[MAX];
        for (int i = 0; i < MAX; i++)
            gr[i] = new Vector<Integer>();

        // Adjacency matrix
        boolean[][] edge = new boolean[MAX][MAX];

        // Initialising the adjacency matrix
        for (int k = 0; k < MAX; k++)
            for (int l = 0; l < MAX; l++)
                edge[k][l] = false;

        // Creating the adjacency matrix
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
            {
                if (i + 1 < n && !edge[f(arr[i].charAt(j))][f(arr[i + 1].charAt(j))])
                {
                    gr[f(arr[i].charAt(j))].add(f(arr[i + 1].charAt(j)));
                    edge[f(arr[i].charAt(j))][f(arr[i + 1].charAt(j))] = true;
                }
                if (j - 1 >= 0 && !edge[f(arr[i].charAt(j))][f(arr[i].charAt(j - 1))])
                {
                    gr[f(arr[i].charAt(j))].add(f(arr[i].charAt(j - 1)));
                    edge[f(arr[i].charAt(j))][f(arr[i].charAt(j - 1))] = true;
                }
                if (j + 1 < m && !edge[f(arr[i].charAt(j))][f(arr[i].charAt(j + 1))])
                {
                    gr[f(arr[i].charAt(j))].add(f(arr[i].charAt(j + 1)));
                    edge[f(arr[i].charAt(j))][f(arr[i].charAt(j + 1))] = true;
                }
                if (i - 1 >= 0 && !edge[f(arr[i].charAt(j))][f(arr[i - 1].charAt(j))])
                {
                    gr[f(arr[i].charAt(j))].add(f(arr[i - 1].charAt(j)));
                    edge[f(arr[i].charAt(j))][f(arr[i - 1].charAt(j))] = true;
                }
            }

        // Queue to perform BFS
        Queue<Integer> q = new LinkedList<Integer>();
        q.add(arr[0].charAt(0) - 'a');

        // Visited array
        boolean[] v = new boolean[MAX];

        // To store the depth of BFS
        int d = 0;

        // BFS
        while (q.size() > 0)
        {

            // Number of elements in
            // the current level
            int cnt = q.size();

            // Inner loop
            while (cnt-- > 0)
            {

                // Current element
                int curr = q.peek();

                // Popping queue
                q.remove();

                // If the current node has
                // already been visited
                if (v[curr])
                    continue;
                v[curr] = true;

                // Checking if the current
                // node is the required node
                if (curr == arr[n - 1].charAt(m - 1) - 'a')
                    return d;

                // Iterating through the current node
                for (Integer it : gr[curr])
                    q.add(it);
            }

            // Updating the depth
            d++;
        }

        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        String[] arr = { "abc", "def", "gbi" };

        System.out.print(findMinCost(arr));

    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 26

# Function to return
# the value (x - 97)
def f(x):
    return ord(x) - ord('a')

# Function to return the minimum cost
def findMinCost( arr):
    global MAX
    n = len(arr)
    m = len(arr[0])

    # Graph
    gr = []

    for x in range(MAX):
        gr.append([])

    # Adjacency matrix
    edge = []

    # Initialising the adjacency matrix
    for k in range(MAX):
        edge.append([])
        for l in range(MAX):
            edge[k].append(0)

    # Creating the adjacency matrix
    for i in range(n):
        for j in range(m):
            if (i + 1 < n and edge[f(arr[i][j])][f(arr[i + 1][j])] == 0):
                gr[f(arr[i][j])].append(f(arr[i + 1][j]))
                edge[f(arr[i][j])][f(arr[i + 1][j])] = 1

            if (j - 1 >= 0 and edge[f(arr[i][j])][f(arr[i][j - 1])] == 0):
                gr[f(arr[i][j])].append(f(arr[i][j - 1]))
                edge[f(arr[i][j])][f(arr[i][j - 1])] = 1

            if (j + 1 < m and edge[f(arr[i][j])][f(arr[i][j + 1])] == 0):
                gr[f(arr[i][j])].append(f(arr[i][j + 1]))
                edge[f(arr[i][j])][f(arr[i][j + 1])] = 1

            if (i - 1 >= 0 and edge[f(arr[i][j])][f(arr[i - 1][j])] == 0):
                gr[f(arr[i][j])].append(f(arr[i - 1][j]))
                edge[f(arr[i][j])][f(arr[i - 1][j])] = 1

    # Queue to perform BFS
    q = []
    q.append(ord(arr[0][0]) - ord('a'))

    # Visited array
    v = []
    for i in range(MAX):
        v.append(0)

    # To store the depth of BFS
    d = 0

    # BFS
    while (len(q) > 0):

        # Number of elements in
        # the current level
        cnt = len(q)

        # Inner loop
        while (cnt > 0):
            cnt = cnt - 1

            # Current element
            curr = q[0]

            # Popping queue
            q.pop(0)

            # If the current node has
            # already been visited
            if (v[curr] != 0):
                continue
            v[curr] = 1

            # Checking if the current
            # node is the required node
            if (curr == (ord(arr[n - 1][m - 1]) - ord('a'))):
                return d

            # Iterating through the current node
            for it in gr[curr]:
                q.append(it)

        # Updating the depth
        d = d + 1

    return -1

# Driver code
arr =[ "abc","def","gbi" ]
print( findMinCost(arr))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    static int MAX = 26;

    // Function to return
    // the value (x - 97)
    static int f(int x)
    {
        return x - 'a';
    }

    // Function to return the minimum cost
    static int findMinCost(String[] arr)
    {
        int n = arr.Length;
        int m = arr[0].Length;

        // Graph
        List<int>[] gr = new List<int>[MAX];
        for (int i = 0; i < MAX; i++)
            gr[i] = new List<int>();

        // Adjacency matrix
        bool[,] edge = new bool[MAX, MAX];

        // Initialising the adjacency matrix
        for (int k = 0; k < MAX; k++)
            for (int l = 0; l < MAX; l++)
                edge[k,l] = false;

        // Creating the adjacency matrix
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
            {
                if (i + 1 < n && !edge[f(arr[i][j]),f(arr[i + 1][j])])
                {
                    gr[f(arr[i][j])].Add(f(arr[i + 1][j]));
                    edge[f(arr[i][j]), f(arr[i + 1][j])] = true;
                }
                if (j - 1 >= 0 && !edge[f(arr[i][j]),f(arr[i][j - 1])])
                {
                    gr[f(arr[i][j])].Add(f(arr[i][j - 1]));
                    edge[f(arr[i][j]), f(arr[i][j - 1])] = true;
                }
                if (j + 1 < m && !edge[f(arr[i][j]),f(arr[i][j + 1])])
                {
                    gr[f(arr[i][j])].Add(f(arr[i][j + 1]));
                    edge[f(arr[i][j]), f(arr[i][j + 1])] = true;
                }
                if (i - 1 >= 0 && !edge[f(arr[i][j]),f(arr[i - 1][j])])
                {
                    gr[f(arr[i][j])].Add(f(arr[i - 1][j]));
                    edge[f(arr[i][j]), f(arr[i - 1][j])] = true;
                }
            }

        // Queue to perform BFS
        Queue<int> q = new Queue<int>();
        q.Enqueue(arr[0][0] - 'a');

        // Visited array
        bool[] v = new bool[MAX];

        // To store the depth of BFS
        int d = 0;

        // BFS
        while (q.Count > 0)
        {

            // Number of elements in
            // the current level
            int cnt = q.Count;

            // Inner loop
            while (cnt-- > 0)
            {

                // Current element
                int curr = q.Peek();

                // Popping queue
                q.Dequeue();

                // If the current node has
                // already been visited
                if (v[curr])
                    continue;
                v[curr] = true;

                // Checking if the current
                // node is the required node
                if (curr == arr[n - 1][m - 1] - 'a')
                    return d;

                // Iterating through the current node
                foreach (int it in gr[curr])
                    q.Enqueue(it);
            }

            // Updating the depth
            d++;
        }

        return -1;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String[] arr = { "abc", "def", "gbi" };

        Console.Write(findMinCost(arr));
    }
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
2
```

**时间复杂度** : O(N * M)。
**辅助空间** : O(N * M)。