# 在字符串中从一个索引遍历到另一个索引的最小成本

> 原文:[https://www . geeksforgeeks . org/字符串中从一个索引遍历到另一个索引的最小成本/](https://www.geeksforgeeks.org/minimum-cost-to-traverse-from-one-index-to-another-in-the-string/)

给定由小写字符组成的长度为 **N** 的字符串 **S** ，任务是找到从索引 **i** 到索引 **j** 的最小成本。
在任一指标 **k** 处，跳转到指标 **k+1** 、 **k-1** (不出界)的成本为 1。
此外，跳转到任何指标 **m** 使得 **S[m] = S[k]** 的成本为 0。

**示例:**

> **输入:** S = "abcde "，i = 0，j = 4
> **输出:** 4
> **解释:**
> 最短路径将是:
> 0->1->2->3->4
> 这样，答案将是 4。
> 
> **输入:** S = "abcdefb "，i = 0，j = 5
> **输出:** 2
> **解释:**
> 0->1->6->5
> 0->1 边权重为 1，1- > 6 边权重为 0，6- > 5 边权重为 1。
> 因此，答案将是 2

**进场:**

1.  解决这个问题的一种方法是 [0-1 BFS](https://www.geeksforgeeks.org/0-1-bfs-shortest-path-binary-graph/) 。
2.  该设置可以被可视化为具有 **N 个**节点的图形。
3.  所有节点都将连接到权重为“1”的相邻节点和权重为“0”的具有相同字符的节点。
4.  在此设置中， [0-1 BFS](https://www.geeksforgeeks.org/0-1-bfs-shortest-path-binary-graph/) 可以运行以找到从索引“I”到索引“j”的最短路径。

**时间复杂度:**O(N^2–因为顶点数是 o(n^2)

**高效方法:**

1.  对于每个字符 **X** ，找到与其相邻的所有字符。
2.  创建一个图形，其中节点的数量等于字符串中不同字符的数量，每个字符代表一个字符。
3.  每个节点 **X** 将具有权重 1 的边，所有节点代表与字符 **X** 相邻的字符。
4.  然后 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 可以在这个新图中从代表 S[i]的节点运行到代表 S[j]的节点

**时间复杂度:** O(N)

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach.
#include <bits/stdc++.h>
using namespace std;

// function to find the minimum cost
int findMinCost(string s, int i, int j)
{
    // graph
    vector<vector<int> > gr(26);

    // adjacency matrix
    bool edge[26][26];

    // initialising adjacency matrix
    for (int k = 0; k < 26; k++)
        for (int l = 0; l < 26; l++)
            edge[k][l] = 0;

    // creating adjacency list
    for (int k = 0; k < s.size(); k++) {
        // pushing left adjacent elelemt for index 'k'
        if (k - 1 >= 0
            and !edge[s[k] - 97][s[k - 1] - 97])
            gr[s[k] - 97].push_back(s[k - 1] - 97),
                edge[s[k] - 97][s[k - 1] - 97] = 1;
        // pushing right adjacent element for index 'k'
        if (k + 1 <= s.size() - 1
            and !edge[s[k] - 97][s[k + 1] - 97])
            gr[s[k] - 97].push_back(s[k + 1] - 97),
                edge[s[k] - 97][s[k + 1] - 97] = 1;
    }

    // queue to perform BFS
    queue<int> q;
    q.push(s[i] - 97);

    // visited array
    bool v[26] = { 0 };

    // variable to store depth of BFS
    int d = 0;

    // BFS
    while (q.size()) {

        // number of elements in the current level
        int cnt = q.size();

        // inner loop
        while (cnt--) {

            // current element
            int curr = q.front();

            // popping queue
            q.pop();

            // base case
            if (v[curr])
                continue;
            v[curr] = 1;

            // checking if the current node is required node
            if (curr == s[j] - 97)
                return d;

            // iterating through the current node
            for (auto it : gr[curr])
                q.push(it);
        }

        // updating depth
        d++;
    }

    return -1;
}

// Driver Code
int main()
{
    // input variables
    string s = "abcde";
    int i = 0;
    int j = 4;

    // function to find the minimum cost
    cout << findMinCost(s, i, j);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
import java.util.*;

class GFG
{

    // function to find the minimum cost
    static int findMinCost(char[] s, int i, int j)
    {
        // graph
        Vector<Integer>[] gr = new Vector[26];
        for (int iN = 0; iN < 26; iN++)
            gr[iN] = new Vector<Integer>();

        // adjacency matrix
        boolean[][] edge = new boolean[26][26];

        // initialising adjacency matrix
        for (int k = 0; k < 26; k++)
            for (int l = 0; l < 26; l++)
                edge[k][l] = false;

        // creating adjacency list
        for (int k = 0; k < s.length; k++)
        {
            // pushing left adjacent elelemt for index 'k'
            if (k - 1 >= 0 && !edge[s[k] - 97][s[k - 1] - 97])
            {
                gr[s[k] - 97].add(s[k - 1] - 97);
                edge[s[k] - 97][s[k - 1] - 97] = true;
            }
            // pushing right adjacent element for index 'k'
            if (k + 1 <= s.length - 1 && !edge[s[k] - 97][s[k + 1] - 97])
            {
                gr[s[k] - 97].add(s[k + 1] - 97);
                edge[s[k] - 97][s[k + 1] - 97] = true;
            }
        }

        // queue to perform BFS
        Queue<Integer> q = new LinkedList<Integer>();
        q.add(s[i] - 97);

        // visited array
        boolean[] v = new boolean[26];

        // variable to store depth of BFS
        int d = 0;

        // BFS
        while (q.size() > 0)
        {

            // number of elements in the current level
            int cnt = q.size();

            // inner loop
            while (cnt-- > 0)
            {

                // current element
                int curr = q.peek();

                // popping queue
                q.remove();

                // base case
                if (v[curr])
                    continue;
                v[curr] = true;

                // checking if the current node is required node
                if (curr == s[j] - 97)
                    return d;

                // iterating through the current node
                for (Integer it : gr[curr])
                    q.add(it);
            }

            // updating depth
            d++;
        }

        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // input variables
        String s = "abcde";
        int i = 0;
        int j = 4;

        // function to find the minimum cost
        System.out.print(findMinCost(s.toCharArray(), i, j));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach.
from collections import deque as a queue

# function to find minimum cost
def findMinCost(s, i, j):

    # graph
    gr = [[] for i in range(26)]

    # adjacency matrix
    edge = [[ 0 for i in range(26)] for i in range(26)]

    # initialising adjacency matrix
    for k in range(26):
        for l in range(26):
            edge[k][l] = 0

    # creating adjacency list
    for k in range(len(s)):

        # pushing left adjacent elelemt for index 'k'
        if (k - 1 >= 0 and edge[ord(s[k]) - 97][ord(s[k - 1]) - 97] == 0):
            gr[ord(s[k]) - 97].append(ord(s[k - 1]) - 97)
            edge[ord(s[k]) - 97][ord(s[k - 1]) - 97] = 1

        # pushing right adjacent element for index 'k'
        if (k + 1 <= len(s) - 1 and edge[ord(s[k]) - 97][ord(s[k + 1]) - 97] == 0):
            gr[ord(s[k]) - 97].append(ord(s[k + 1]) - 97)
            edge[ord(s[k]) - 97][ord(s[k + 1]) - 97] = 1

    # queue to perform BFS
    q = queue()
    q.append(ord(s[i]) - 97)

    # visited array
    v = [0] * (26)

    # variable to store depth of BFS
    d = 0

    # BFS
    while (len(q)):

        # number of elements in the current level
        cnt = len(q)

        # inner loop
        while (cnt > 0):

            # current element
            curr = q.popleft()

            # base case
            if (v[curr] == 1):
                continue
            v[curr] = 1

            # checking if the current node is required node
            if (curr == ord(s[j]) - 97):
                return curr

            # iterating through the current node
            for it in gr[curr]:
                q.append(it)
            print()
            cnt -= 1

        # updating depth
        d = d + 1

    return -1

# Driver Code

# input variables
s = "abcde"
i = 0
j = 4

# function to find the minimum cost
print(findMinCost(s, i, j))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach.
using System;
using System.Collections.Generic;

class GFG
{

    // function to find the minimum cost
    static int findMinCost(char[] s, int i, int j)
    {
        // graph
        List<int>[] gr = new List<int>[26];
        for (int iN = 0; iN < 26; iN++)
            gr[iN] = new List<int>();

        // adjacency matrix
        bool[,] edge = new bool[26, 26];

        // initialising adjacency matrix
        for (int k = 0; k < 26; k++)
            for (int l = 0; l < 26; l++)
                edge[k, l] = false;

        // creating adjacency list
        for (int k = 0; k < s.Length; k++)
        {
            // pushing left adjacent elelemt for index 'k'
            if (k - 1 >= 0 && !edge[s[k] - 97, s[k - 1] - 97])
            {
                gr[s[k] - 97].Add(s[k - 1] - 97);
                edge[s[k] - 97, s[k - 1] - 97] = true;
            }

            // pushing right adjacent element for index 'k'
            if (k + 1 <= s.Length - 1 &&
                !edge[s[k] - 97, s[k + 1] - 97])
            {
                gr[s[k] - 97].Add(s[k + 1] - 97);
                edge[s[k] - 97, s[k + 1] - 97] = true;
            }
        }

        // queue to perform BFS
        Queue<int> q = new Queue<int>();
        q.Enqueue(s[i] - 97);

        // visited array
        bool[] v = new bool[26];

        // variable to store depth of BFS
        int d = 0;

        // BFS
        while (q.Count > 0)
        {

            // number of elements in the current level
            int cnt = q.Count;

            // inner loop
            while (cnt-- > 0)
            {

                // current element
                int curr = q.Peek();

                // popping queue
                q.Dequeue();

                // base case
                if (v[curr])
                    continue;
                v[curr] = true;

                // checking if the current node is required node
                if (curr == s[j] - 97)
                    return d;

                // iterating through the current node
                foreach (int it in gr[curr])
                    q.Enqueue(it);
            }

            // updating depth
            d++;
        }

        return -1;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // input variables
        String s = "abcde";
        int i = 0;
        int j = 4;

        // function to find the minimum cost
        Console.Write(findMinCost(s.ToCharArray(), i, j));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach.

// function to find the minimum cost
function findMinCost(s,i, j)
{
    // graph
    var gr = Array.from(Array(26), ()=> new Array());

    // adjacency matrix
    var edge = Array.from(Array(26), ()=> Array(26));

    // initialising adjacency matrix
    for (var k = 0; k < 26; k++)
        for (var l = 0; l < 26; l++)
            edge[k][l] = 0;

    // creating adjacency list
    for (var k = 0; k < s.length; k++) {
        // pushing left adjacent elelemt for index 'k'
        if (k - 1 >= 0
            && !edge[s[k].charCodeAt(0) - 97][s[k - 1].charCodeAt(0) - 97])
            gr[s[k].charCodeAt(0) - 97].push(s[k - 1].charCodeAt(0) - 97),
                edge[s[k].charCodeAt(0) - 97][s[k - 1].charCodeAt(0) - 97] = 1;
        // pushing right adjacent element for index 'k'
        if (k + 1 <= s.length - 1
            && !edge[s[k].charCodeAt(0) - 97][s[k + 1].charCodeAt(0) - 97])
            gr[s[k].charCodeAt(0) - 97].push(s[k + 1].charCodeAt(0) - 97),
                edge[s[k].charCodeAt(0) - 97][s[k + 1].charCodeAt(0) - 97] = 1;
    }

    // queue to perform BFS
    var q = [];
    q.push(s[i].charCodeAt(0) - 97);

    // visited array
    var v = Array(26).fill(0);

    // variable to store depth of BFS
    var d = 0;

    // BFS
    while (q.length>0) {

        // number of elements in the current level
        var cnt = q.length;

        // inner loop
        while (cnt-->0) {

            // current element
            var curr = q[0];

            // popping queue
            q.shift();

            // base case
            if (v[curr])
                continue;
            v[curr] = 1;

            // checking if the current node is required node
            if (curr == s[j].charCodeAt(0) - 97)
                return d;

            // iterating through the current node
            for(var it =0 ;it< gr[curr].length; it++)
            {
                q.push(gr[curr][it]);
            }   
        }

        // updating depth
        d++;
    }

    return -1;
}

// Driver Code
// input variables
var s = "abcde";
var i = 0;
var j = 4;
// function to find the minimum cost
document.write( findMinCost(s, i, j));

</script>
```

**输出:**

```
4
```