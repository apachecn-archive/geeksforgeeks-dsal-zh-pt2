# 使用合并排序树对在线查询范围内的数组中的不同数字进行计数

> 原文:[https://www . geeksforgeeks . org/count-of-distinct-numbers-in-in-a-range-for-online-query-use-merge-sort-tree/](https://www.geeksforgeeks.org/count-of-distinct-numbers-in-an-array-in-a-range-for-online-queries-using-merge-sort-tree/)

给定一个大小为**N**和**Q**的数组**arr[]**，查询形式为[L，R]，任务是在给定的范围内找到该数组中不同值的数量。

**示例:**

> **输入:** arr[] = {4，1，9，1，3，3}，Q = {{1，3}，{1，5}}
> **输出:**
> 3
> 4
> **说明:**
> 对于查询{1，3}，元素为{4，1，9}。因此，不同元素的计数= 3
> 对于查询{1，5}，元素是{4，1，9，1，3}。因此，不同元素的计数= 4
> 
> **输入:** arr[] = {4，2，1，1，4}，Q = {{2，4}，{3，5 } }
> T3】输出:T5】3
> 2

**天真方法:**一个简单的解决方案是，对于每个查询，从 L 到 R 迭代数组，并在集合中插入元素。最后，集合的大小给出了从 L 到 r 的不同元素的数量

***时间复杂度:** O(Q * N)*

**高效方法:**思路是用[合并排序树](https://www.geeksforgeeks.org/merge-sort-tree-smaller-or-equal-elements-in-given-row-range/)来解决这个问题。

1.  我们将把元素的下一次出现存储在临时数组中。
2.  然后对于从 L 到 R 的每一个查询，我们都会在 L 到 R 的范围内找到临时数组中值大于 R 的元素个数。

**步骤 1:** 取一个 next_right 数组，其中 next_right[i]保存数组 a 中数字 I 的下一个右索引，将这个数组初始化为 N(数组的长度)。
**步骤 2:** 从 next_right 数组中创建合并排序树并进行查询。计算从左到右的不同元素数目的查询相当于找到从左到右的大于右的元素数目

**从给定数组构建合并排序树**

*   我们从片段 arr[0]开始。。。n-1]。
*   每当我们将当前段分成两半时，如果它还没有变成长度为 1 的段。然后在两个部分调用相同的过程，对于每个这样的段，我们将排序后的数组存储在每个段中，就像在合并排序中一样。
*   此外，树将是一个完整的二叉树，因为我们总是在每一个级别将片段分成两半。
*   由于构造的树总是一棵有 N 片叶子的完全二叉树，因此将有 N-1 个内部节点。因此，节点总数将为 2 * N–1。

这里有一个例子。假设 1 5 2 6 9 4 7 1 是一个数组。

```
|1 1 2 4 5 6 7 9|
|1 2 5 6|1 4 7 9|
|1 5|2 6|4 9|1 7|
|1|5|2|6|9|4|7|1|

```

**下一个 _ 右数组的构造**

*   我们存储每个元素的下一个正确出现。
*   如果元素最后一次出现，那么我们存储‘N’(数组长度)
    **示例:**

    ```
    arr = [2, 3, 2, 3, 5, 6];
    next_right = [2, 3, 6, 6, 6, 6]

    ```

下面是上述方法的实现:

## C++

```
// C++ implementation to find
// count of distinct elements 
// in a range L to R for Q queries

#include <bits/stdc++.h>
using namespace std;

// Function to merge the right
// and the left tree
void merge(vector<int> tree[], 
                 int treeNode)
{
    int len1 = 
      tree[2 * treeNode].size();
    int len2 = 
      tree[2 * treeNode + 1].size();
    int index1 = 0, index2 = 0;

    // Fill this array in such a 
    // way such that values
    // remain sorted similar to mergesort
    while (index1 < len1 && index2 < len2) {

        // If the element on the left part
        // is greater than the right part
        if (tree[2 * treeNode][index1] > 
              tree[2 * treeNode + 1][index2]) {

            tree[treeNode].push_back(
                tree[2 * treeNode + 1][index2]
                );
            index2++;
        }
        else {
            tree[treeNode].push_back(
                tree[2 * treeNode][index1]
                );
            index1++;
        }
    }

    // Insert the leftover elements
    // from the left part
    while (index1 < len1) {
        tree[treeNode].push_back(
            tree[2 * treeNode][index1]
            );
        index1++;
    }

    // Insert the leftover elements
    // from the right part
    while (index2 < len2) {
        tree[treeNode].push_back(
            tree[2 * treeNode + 1][index2]
            );
        index2++;
    }
    return;
}

// Recursive function to build 
// segment tree by merging the 
// sorted segments in sorted way
void build(vector<int> tree[], 
    int* arr, int start, int end, 
                  int treeNode)
{
    // Base case
    if (start == end) {
        tree[treeNode].push_back(
            arr[start]);
        return;
    }
    int mid = (start + end) / 2;

    // Building the left tree
    build(tree, arr, start, 
          mid, 2 * treeNode);

    // Building the right tree
    build(tree, arr, mid + 1, end, 
                 2 * treeNode + 1);

    // Merges the right tree
    // and left tree
    merge(tree, treeNode);
    return;
}

// Function similar to query() method
// as in segment tree
int query(vector<int> tree[], 
     int treeNode, int start, int end, 
            int left, int right)
{

    // Current segment is out of the range
    if (start > right || end < left) {
        return 0;
    }
    // Current segment completely 
    // lies inside the range
    if (start >= left && end <= right) {

        // as the elements are in sorted order
        // so number of elements greater than R
        // can be find using binary 
        // search or upper_bound
        return tree[treeNode].end() - 
          upper_bound(tree[treeNode].begin(), 
            tree[treeNode].end(), right);
    }

    int mid = (start + end) / 2;

    // Query on the left tree
    int op1 = query(tree, 2 * treeNode, 
              start, mid, left, right);
    // Query on the Right tree
    int op2 = query(tree, 2 * treeNode + 1, 
            mid + 1, end, left, right);
    return op1 + op2;
}

// Driver Code
int main()
{

    int n = 5;
    int arr[] = { 1, 2, 1, 4, 2 };

    int next_right[n];
    // Initialising the tree
    vector<int> tree[4 * n];

    unordered_map<int, int> ump;

    // Construction of next_right 
    // array to store the
    // next index of occurence 
    // of elements
    for (int i = n - 1; i >= 0; i--) {
        if (ump[arr[i]] == 0) {
            next_right[i] = n;
            ump[arr[i]] = i;
        }
        else {
            next_right[i] = ump[arr[i]];
            ump[arr[i]] = i;
        }
    }
    // building the mergesort tree
    // by using next_right array
    build(tree, next_right, 0, n - 1, 1);

    int ans;
    // Queries one based indexing
    // Time complexity of each 
    // query is log(N)

    // first query
    int left1 = 0;
    int right1 = 2;
    ans = query(tree, 1, 0, n - 1, 
                  left1, right1);
    cout << ans << endl;

    // Second Query
    int left2 = 1;
    int right2 = 4;
    ans = query(tree, 1, 0, n - 1, 
                  left2, right2);
    cout << ans << endl;
}
```

**Output:**

```
2
3

```

***时间复杂度:** O(Q*log N)*