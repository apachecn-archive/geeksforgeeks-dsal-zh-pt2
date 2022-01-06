# 以给定的最小频率对 Q 查询进行着色树的子树中不同颜色的计数

> 原文:[https://www . geeksforgeeks . org/带有给定最小查询频率的彩色树子树中不同颜色的计数/](https://www.geeksforgeeks.org/count-of-distinct-colors-in-a-subtree-of-a-colored-tree-with-given-min-frequency-for-q-queries/)

给定一个带有与每个节点相关联的某种颜色的 [N 元](https://www.geeksforgeeks.org/generic-treesn-array-trees/)树和 **Q** 查询。每个查询包含两个整数 **A** 和 **X** 。任务是统计以 **A** 为根的子树中所有不同的颜色，这些颜色在该子树中出现的频率大于或等于 **X** 。
**示例:**

> **输入:**树:
> 
> ```
>  
>            1(1)
>          /       \ 
>        /          \
>      2(2)         5(3)
>     /   \       /  |   \
>    /     \     /   |    \
> 3(2)    4(3) 6(2) 7(3)  8(3)
> ```
> 
> query[] = {{1，2}、{1，3}、{1，4}、{2，3}、{5，3}}
> **输出:** {2，2，1，0，1}
> **解释:**
> 在以 1 为根的子树中，颜色 2 出现的频率为 3，颜色 3 出现的频率为 4。因此，1 个查询的答案是 2，第 2 个查询的答案是 2，第 3 个查询的答案是 1。
> 对于以 2 为根的子树，颜色 2 的频率为 2，颜色 3 的频率为 1。所以没有一种颜色的频率大于或等于 4。
> 对于以 5 为根的子树，颜色 2 的频率为 1，颜色 3 的频率为 3。所以颜色 3 的频率等于 3。

**天真的方法**T2】

*   对于每个查询，我们将遍历给定节点的整个子树。
*   我们将维护一个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，它存储给定节点的子树中每种颜色的频率。
*   然后，遍历地图，计算颜色的数量，使其频率大于给定的 x。

***时间复杂度:** O(Q * N)*
***空间复杂度:** O(Q * N)*
**方法:(使用莫氏算法)**

*   我们将首先使用欧拉巡回赛将树放平。

*   我们会给每个节点编号，什么时候进入 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 什么时候出来。让我们用每个节点的 **tin【节点】**和 **tout【节点】**来表示。
*   在我们将树展平成一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)后，的每一个子树都可以表示为某个数组，开始和结束索引分别为 **tin【节点】**和 **tout【节点】**。
*   现在问题变成了某个子阵中频率大于等于 **X** 的元素个数。
*   我们就用[莫的算法](https://www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/)来解决这个问题。
*   首先，我们将存储查询并按照 **tin【节点】/ SQ** 排序，其中 **SQ** 是 **N** 的[平方根。](https://www.geeksforgeeks.org/square-root-of-an-integer/)
*   当我们移动指针时，我们将在一个数组中存储带有颜色的频率，并且查询的答案存储在数组的第 **X** 个位置，因为它存储了频率大于等于 X 的颜色计数

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to count distinct colors
// in a subtree of a Colored Tree
// with given min frequency for Q queries

#include <bits/stdc++.h>
using namespace std;

const int N = 1e5 + 5;

// graph as adjacency list
vector<vector<int> > v(N);

// colour written on node.
vector<int> colour(N);

// order of node entering in DFS
vector<int> in(N);

// order of node exiting in DFS
vector<int> out(N);

// for counting the frequency of
// nodes with colour i
vector<int> cnt(N);

// for storing frequency of colours
vector<int> freq(N);

// tree in a flatten
// form (using Euler tour)
vector<int> flatTree(N);

// number of nodes
int n,

    // square root of n
    sq;

// indexes for in and
// out of node in DFS
int start = 0;

// DFS function to find
// order of euler tour
void DFSEuler(int a, int par)
{

    // storing the start index
    in[a] = ++start;

    // storing colour of node
    // in flatten array
    flatTree[start] = colour[a];

    for (int i : v[a]) {

        // doing DFS on its child
        // skipping parent
        if (i == par)
            continue;

        DFSEuler(i, a);
    }

    // out index of the node.
    out[a] = start;
}

// comparator for queries
bool comparator(pair<int, int>& a,
                pair<int, int>& b)
{
    // comparator for queries to be
    // sorted according to in[x] / sq
    if (in[a.first] / sq != in[b.first] / sq)
        return in[a.first] < in[b.first];

    return out[a.first] < out[b.first];
}

// Function to answer the queries
void solve(vector<pair<int, int> > arr,
           int q)
{
    sq = sqrt(n) + 1;

    // for storing answers
    vector<int> answer(q);

    // for storing indexes of queries
    // in the order of input.
    map<pair<int, int>, int> idx;

    for (int i = 0; i < q; i++) {

        // storing indexes of queries
        idx[arr[i]] = i;
    }

    // doing depth first search to
    // find indexes to flat the
    // tree using euler tour.
    DFSEuler(1, 0);

    // After doing Euler tour,
    // subtree of x can be
    // represented as a subarray
    // from in[x] to out[x];

    // we'll sort the queries
    // according to the in[i];
    sort(arr.begin(),
         arr.end(),
         comparator);

    // two pointers for
    // sliding the window
    int l = 1, r = 0;

    for (int i = 0; i < q; i++) {

        // finding answer to the query
        int node = arr[i].first,
            x = arr[i].second;
        int id = idx[arr[i]];

        while (l > in[node]) {

            // decrementing the pointer as
            // it is greater than start
            // and adding answer
            // to our freq array.
            l--;
            cnt[flatTree[l]]++;
            freq[cnt[flatTree[l]]]++;
        }

        while (r < out[node]) {

            // incrementing pointer as it is
            // less than the end value and
            // adding answer to our freq array.
            r++;
            cnt[flatTree[r]]++;
            freq[cnt[flatTree[r]]]++;
        }

        while (l < in[node]) {

            // removing the lth node from
            // freq array and incrementing
            // the pointer
            freq[cnt[flatTree[l]]]--;
            cnt[flatTree[l]]--;
            l++;
        }

        while (r > out[node]) {

            // removing the rth node from
            // freq array and decrementing
            // the pointer
            freq[cnt[flatTree[r]]]--;
            cnt[flatTree[r]]--;
            r--;
        }

        // answer to this query
        // is stored at freq[x]
        // freq[x] stores the frequency
        // of nodes greater equal to x
        answer[id] = freq[x];
    }

    // printing the queries
    for (int i = 0; i < q; i++)
        cout << answer[i] << " ";
}

int main()
{
    // Driver Code
    /*
               1(1)
             /       \
           /          \
         2(2)         5(3)
        /   \       /  |   \
       /     \     /   |    \
    3(2)    4(3) 6(2) 7(3)  8(3)
    */
    n = 8;
    v[1].push_back(2);
    v[2].push_back(1);
    v[2].push_back(3);
    v[3].push_back(2);
    v[2].push_back(4);
    v[4].push_back(2);
    v[1].push_back(5);
    v[5].push_back(1);
    v[5].push_back(6);
    v[6].push_back(5);
    v[5].push_back(7);
    v[7].push_back(5);
    v[5].push_back(8);
    v[8].push_back(5);

    colour[1] = 1;
    colour[2] = 2;
    colour[3] = 2;
    colour[4] = 3;
    colour[5] = 3;
    colour[6] = 2;
    colour[7] = 3;
    colour[8] = 3;

    vector<pair<int, int> > queries
        = { { 1, 2 },
            { 1, 3 },
            { 1, 4 },
            { 2, 3 },
            { 5, 3 } };
    int q = queries.size();

    solve(queries, q);
    return 0;
}
```

**Output:** 

```
2 2 1 0 1
```

**时间复杂度:** ![O(Q * \sqrt{N})  ](img/3bb17dc13728138b318c4e38b6e0e911.png "Rendered by QuickLaTeX.com")
**空间复杂度:** ![O(N)  ](img/49a9eabbb27564e25ba8e2b64e1e7e4b.png "Rendered by QuickLaTeX.com")