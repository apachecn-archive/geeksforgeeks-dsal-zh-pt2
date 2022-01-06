# 找到字母顺序，这样单词就可以被认为是排序的

> 原文:[https://www . geesforgeks . org/find-按字母顺序-这样-单词-可以被认为-排序/](https://www.geeksforgeeks.org/find-alphabetical-order-such-that-words-can-be-considered-sorted/)

给定一个单词数组，在英语字母表中找到任何字母顺序，这样给定的单词可以被认为是排序的(递增的)，如果存在这样的顺序，否则输出是不可能的。

示例:

```
Input :  words[] = {"zy", "ab"}
Output : zabcdefghijklmnopqrstuvwxy
Basically we need to make sure that 'z' comes
before 'a'.

Input :  words[] = {"geeks", "gamers", "coders", 
                    "everyoneelse"}
Output : zyxwvutsrqponmlkjihgceafdb

Input : words[] = {"marvel", "superman", "spiderman", 
                                           "batman"
Output : zyxwvuptrqonmsbdlkjihgfeca

```

**天真的方法:**蛮力的方法是检查所有可能的顺序，并检查它们是否满足给定的单词顺序。考虑到英语中有 **26** 字母，还有 **26！**可以是有效顺序的排列数量。考虑到我们检查每一对来验证订单，这种方法的复杂性达到了 **O(26！*N^2)** ，这远远超出了实际优选的时间复杂度。

**使用拓扑排序:**该解决方案需要了解[图及其作为邻接表](https://www.geeksforgeeks.org/graph-and-its-representations/)、 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 和[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)的表示。

按照我们要求的顺序，要求打印字母，以便每个字母后面必须跟有优先级比它们低的字母。这似乎有点类似于[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)的定义——在拓扑排序中，我们需要在相邻顶点之前打印一个顶点。让我们将字母表中的每个字母定义为标准有向图中的节点。如果 **A** 在顺序上位于 **B** 之前，则 **A** 被称为连接到 **B** (A— > B)。算法可以表述如下:

1.  If **n** is **1** , any order is valid.
2.  Take the first two words. Find the first different letter in the word (at the same index of the word). The letter of the first word will precede the letter of the second word.
3.  If there is no such letter, the length of the first string must be less than that of the second string.
4.  Assign the second word to the first word and enter the third word into the second word. Repeat **2** , **3** and **4** **(n-1)** times.
5.  Run a [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) traversal in topological order.
6.  Check whether all nodes are accessed. According to the topological order, if there is a loop in the graph, the nodes in the loop are still not accessed, because it is impossible to access these nodes after accessing every adjacent node. In this case, order does not exist. In this case, this means that the order in our list is contradictory.

```
/* CPP program to find an order of alphabets
so that given set of words are considered
sorted */
#include <bits/stdc++.h>
using namespace std;
#define MAX_CHAR 26

void findOrder(vector<string> v)
{
    int n = v.size();

    /* If n is 1, then any order works */
    if (n == 1) {
        cout << "abcdefghijklmnopqrstuvwxyz";
        return;
    }

    /* Adjacency list of 26 characters*/
    vector<int> adj[MAX_CHAR];

    /* Array tracking the number of edges that are 
    inward to each node*/
    vector<int> in(MAX_CHAR, 0);

    // Traverse through all words in given array
    string prev = v[0];

    /* (n-1) loops because we already acquired the 
    first word in the list*/
    for (int i = 1; i < n; ++i) {
        string s = v[i];

        /* Find first such letter in the present string that is different 
        from the letter in the previous string at the same index*/
        int j;
        for (j = 0; j < min(prev.length(), s.length()); ++j)
            if (s[j] != prev[j])
                break;

        if (j < min(prev.length(), s.length())) {

            /* The letter in the previous string precedes the one
            in the present string, hence add the letter in the present
            string as the child of the letter in the previous string*/
            adj[prev[j] - 'a'].push_back(s[j] - 'a');

            /* The number of inward pointing edges to the node representing 
            the letter in the present string increases by one*/
            in[s[j] - 'a']++;

            /* Assign present string to previous string for the next 
            iteration. */
            prev = s;
            continue;
        }

        /* If there exists no such letter then the string length of 
        the previous string must be less than or equal to the 
        present string, otherwise no such order exists*/
        if (prev.length() > s.length()) {
            cout << "Impossible";
            return;
        }

        /* Assign present string to previous string for the next
        iteration */
        prev = s;
    }

    /* Topological ordering requires the source nodes 
    that have no parent nodes*/
    stack<int> stk;
    for (int i = 0; i < MAX_CHAR; ++i)
        if (in[i] == 0)
            stk.push(i);

    /* Vector storing required order (anyone that satisfies) */
    vector<char> out;

    /* Array to keep track of visited nodes */
    bool vis[26];
    memset(vis, false, sizeof(vis));

    /* Standard DFS */
    while (!stk.empty()) {

        /* Acquire present character */
        char x = stk.top();
        stk.pop();

        /* Mark as visited */
        vis[x] = true;

        /* Insert character to output vector */
        out.push_back(x + 'a');

        for (int i = 0; i < adj[x].size(); ++i) {
            if (vis[adj[x][i]])
                continue;

            /* Since we have already included the present 
            character in the order, the number edges inward 
            to this child node can be reduced*/
            in[adj[x][i]]--;

            /* If the number of inward edges have been removed, 
            we can include this node as a source node*/
            if (in[adj[x][i]] == 0)
                stk.push(adj[x][i]);
        }
    }

    /* Check if all nodes(alphabets) have been visited.
    Order impossible if any one is unvisited*/
    for (int i = 0; i < MAX_CHAR; ++i)
        if (!vis[i]) {
            cout << "Impossible";
            return;
        }

    for (int i = 0; i < out.size(); ++i)
        cout << out[i];
}

// Driver code
int main()
{
    vector<string> v{ "efgh", "abcd" };
    findOrder(v);
    return 0;
}
```

输出:

```
zyxwvutsrqponmlkjihgfeadcb
```

这种方法的复杂性是 **O(N*|S|) + O(V+E)** ，其中 **|V|** =26(节点数与字母数相同)和 **|E|** < **N** (因为每个单词最多创建 1 条边作为输入)。因此整体复杂度为 **O(N*|S|+N)** 。 **|S|** 代表每个单词的长度。