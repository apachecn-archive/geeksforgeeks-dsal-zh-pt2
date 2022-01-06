# 使用段树的最长递增子序列的长度

> 原文:[https://www . geeksforgeeks . org/length-最长递增子序列-lis-use-segment-tree/](https://www.geeksforgeeks.org/length-of-longest-increasing-subsequences-lis-using-segment-tree/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算给定数组中存在的[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的数量。

**示例:**

> **输入:** arr[] = {2，2，2，2，2}
> **输出:** 5
> **说明:**最长递增子序列的长度为 1，即{2}。因此，长度为 1 的最长递增子序列的计数是 5。
> 
> **输入:** arr[] = {1，3，5，4，7}
> **输出:** 2
> **说明:**最长递增子序列的长度为 4，有 2 个长度为 4 的最长递增子序列，即{1，3，4，7}和{1，3，5，7}。

**方法:**在[这篇](https://www.geeksforgeeks.org/number-of-longest-increasing-subsequences/)文章中，已经使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)讨论了给定问题的方法。
本文建议使用[分段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)的不同方法。按照以下步骤解决给定的问题:

*   将[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)初始化为初始包含(0，0)对的[数组](https://www.geeksforgeeks.org/array-data-structure/)，其中 **1 <sup>st</sup>** 元素表示 [LIS](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/) 的长度，**2<sup>nd</sup>**<sup>元素表示当前长度 LIS 的计数。</sup>
*   线段树的第 1 <sup>st</sup> 元素的计算类似于[这篇](https://www.geeksforgeeks.org/lis-using-segment-tree/)文章中讨论的方法。
*   可以使用以下步骤计算线段树的第 2 <sup>和第</sup>元素:
    *   如果左子节点*的长度为* > *的长度为右子节点*的情况下，父节点将等于左子节点，因为 LIS 将是左子节点。
    *   如果左子节点*长度为* < *长度为右子节点*的情况下，父节点等于右子节点，因为 LIS 将是右子节点的。
    *   如果左子节点的*长度=右子节点的*长度，父节点等于左子节点和右子节点的 LIS 计数之和。**
*   需要的答案是段树根的 2 <sup>和</sup>元素。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

#define M 100000

// Stores the Segemnt tree
vector<pair<int, int> > tree(4 * M + 1);

// Function to update Segment tree, the root
// of which contains the length of the LIS
void update_tree(int start, int end,
                 int update_idx, int length_t,
                 int count_c, int idx)
{
    // If the intervals
    // are overlapping completely
    if (start == end
        && start == update_idx) {
        tree[idx].first
            = max(tree[idx].first, length_t);
        tree[idx].second = count_c;
        return;
    }

    // If intervals are not overlapping
    if (update_idx < start
        || end < update_idx) {
        return;
    }

    // If intervals are partially overlapping
    int mid = (start + end) / 2;

    update_tree(start, mid, update_idx,
                length_t, count_c,
                2 * idx);
    update_tree(mid + 1, end, update_idx,
                length_t, count_c,
                2 * idx + 1);

    // If length_t of left and
    // right child are equal
    if (tree[2 * idx].first
        == tree[2 * idx + 1].first) {
        tree[idx].first
            = tree[2 * idx].first;
        tree[idx].second
            = tree[2 * idx].second
              + tree[2 * idx + 1].second;
    }

    // If length_t of left > length_t right child
    else if (tree[2 * idx].first
             > tree[2 * idx + 1].first) {
        tree[idx] = tree[2 * idx];
    }

    // If length_t of left < length_t right child
    else {
        tree[idx] = tree[2 * idx + 1];
    }
}

// Function to find the LIS length
// and count in the given range
pair<int, int> query(int start, int end,
                     int query_start,
                     int query_end, int idx)
{
    // If the intervals
    // are overlapping completely
    if (query_start <= start
        && end <= query_end) {
        return tree[idx];
    }

    // If intervals are not overlapping
    pair<int, int> temp({ INT32_MIN, 0 });
    if (end < query_start
        || query_end < start) {
        return temp;
    }

    // If intervals are partially overlapping
    int mid = (start + end) / 2;
    auto left_child
        = query(start, mid, query_start,
                query_end, 2 * idx);
    auto right_child
        = query(mid + 1, end, query_start,
                query_end, 2 * idx + 1);

    // If length_t of left child is greater
    // than length_t of right child
    if (left_child.first > right_child.first) {
        return left_child;
    }

    // If length_t of right child is
    // greater than length_t of left child
    if (right_child.first > left_child.first) {
        return right_child;
    }

    // If length_t of left
    // and right child are equal
    // return there sum
    return make_pair(left_child.first,
                     left_child.second
                         + right_child.second);
}

// Comparator function to sort an array of pairs
// in increasing order of their 1st element and
// thereafter in decreasing order of the 2nd
bool comp(pair<int, int> a, pair<int, int> b)
{
    if (a.first == b.first) {
        return a.second > b.second;
    }
    return a.first < b.first;
}

// Function to find count
// of LIS in the given array
int countLIS(int arr[], int n)
{
    // Generating value-index pair array
    vector<pair<int, int> > pair_array(n);
    for (int i = 0; i < n; i++) {
        pair_array[i].first = arr[i];
        pair_array[i].second = i;
    }

    // Sort array of pairs with increasing order
    // of value and decreasing order of index
    sort(pair_array.begin(),
         pair_array.end(), comp);

    // Traverse the array
    // and perform query updates
    for (int i = 0; i < n; i++) {

        int update_idx = pair_array[i].second;

        // If update index is the 1st index
        if (update_idx == 0) {
            update_tree(0, n - 1, 0, 1, 1, 1);
            continue;
        }

        // Query over the interval [0, update_idx -1]
        pair<int, int> temp
            = query(0, n - 1, 0,
                    update_idx - 1, 1);

        // Update the segment tree
        update_tree(0, n - 1, update_idx,
                    temp.first + 1,
                    max(1, temp.second), 1);
    }

    // Stores the final answer
    pair<int, int> ans
        = query(0, n - 1, 0, n - 1, 1);

    // Return answer
    return ans.second;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 5, 4, 7 };
    int n = sizeof(arr) / sizeof(int);

    cout << countLIS(arr, n);

    return 0;
}
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

let M = 100000

// Stores the Segemnt tree
let tree = new Array(4 * M + 1).fill(0).map(() => []);

// Function to update Segment tree, the root
// of which contains the length of the LIS
function update_tree(start, end, update_idx, length_t, count_c, idx) {
  // If the intervals
  // are overlapping completely
  if (start == end
    && start == update_idx) {
    tree[idx][0]
      = Math.max(tree[idx][0], length_t);
    tree[idx][1] = count_c;
    return;
  }

  // If intervals are not overlapping
  if (update_idx < start
    || end < update_idx) {
    return;
  }

  // If intervals are partially overlapping
  let mid = Math.floor((start + end) / 2);

  update_tree(start, mid, update_idx,
    length_t, count_c,
    2 * idx);
  update_tree(mid + 1, end, update_idx,
    length_t, count_c,
    2 * idx + 1);

  // If length_t of left and
  // right child are equal
  if (tree[2 * idx][0]
    == tree[2 * idx + 1][0]) {
    tree[idx][0]
      = tree[2 * idx][0];
    tree[idx][1]
      = tree[2 * idx][1]
      + tree[2 * idx + 1][1];
  }

  // If length_t of left > length_t right child
  else if (tree[2 * idx][0]
    > tree[2 * idx + 1][0]) {
    tree[idx] = tree[2 * idx];
  }

  // If length_t of left < length_t right child
  else {
    tree[idx] = tree[2 * idx + 1];
  }
}

// Function to find the LIS length
// and count in the given range
function query(start, end, query_start, query_end, idx) {
  // If the intervals
  // are overlapping completely
  if (query_start <= start
    && end <= query_end) {
    return tree[idx];
  }

  // If intervals are not overlapping
  let temp = [Number.MIN_SAFE_INTEGER, 0];
  if (end < query_start
    || query_end < start) {
    return temp;
  }

  // If intervals are partially overlapping
  let mid = Math.floor((start + end) / 2);
  let left_child
    = query(start, mid, query_start,
      query_end, 2 * idx);
  let right_child
    = query(mid + 1, end, query_start,
      query_end, 2 * idx + 1);

  // If length_t of left child is greater
  // than length_t of right child
  if (left_child[0] > right_child[0]) {
    return left_child;
  }

  // If length_t of right child is
  // greater than length_t of left child
  if (right_child[0] > left_child[0]) {
    return right_child;
  }

  // If length_t of left
  // and right child are equal
  // return there sum
  return [left_child[0],
  left_child[1]
  + right_child[1]];
}

// Comparator function to sort an array of pairs
// in increasing order of their 1st element and
// thereafter in decreasing order of the 2nd
function comp(a, b) {
  if (a[0] == b[0]) {
    return a[1] > b[1];
  }
  return a[0] < b[0];
}

// Function to find count
// of LIS in the given array
function countLIS(arr, n) {
  // Generating value-index pair array
  let pair_array = new Array(n).fill(0).map(() => []);
  for (let i = 0; i < n; i++) {
    pair_array[i][0] = arr[i];
    pair_array[i][1] = i;
  }

  // Sort array of pairs with increasing order
  // of value and decreasing order of index
  pair_array.sort(comp);

  // Traverse the array
  // and perform query updates
  for (let i = 0; i < n; i++) {

    let update_idx = pair_array[i][1];

    // If update index is the 1st index
    if (update_idx == 0) {
      update_tree(0, n - 1, 0, 1, 1, 1);
      continue;
    }

    // Query over the interval [0, update_idx -1]
    let temp = query(0, n - 1, 0, update_idx - 1, 1);

    // Update the segment tree
    update_tree(0, n - 1, update_idx,
      temp[0] + 1,
      Math.max(1, temp[1]), 1);
  }

  // Stores the final answer
  let ans = query(0, n - 1, 0, n - 1, 1);

  // Return answer
  return ans[1];
}

// Driver Code

let arr = [1, 3, 5, 4, 7];
let n = arr.length;

document.write(countLIS(arr, n));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*