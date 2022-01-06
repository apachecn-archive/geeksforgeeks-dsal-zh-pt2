# 第一个和最后一个元素大于所有其他元素的最长子序列

> 原文:[https://www . geesforgeks . org/第一个和最后一个元素大于所有其他元素的最长子序列/](https://www.geeksforgeeks.org/longest-subsequence-with-first-and-last-element-greater-than-all-other-elements/)

给定一个从 1 到 N 的大小为 N 的置换，求最长子序列的长度，它具有第一个和最后一个元素大于所有其他子序列元素的性质。
**例:**

> **输入:** N = 6
> 4 2 6 5 3 1
> **输出:** 3
> 大小最长的子序列是[4，2，3]或[4，2，6]或[4，2，5]。没有其他子序列拥有上述属性，第一个和最后一个元素大于所有剩余的子序列元素。
> **输入:** N = 5
> 5 4 1 2 3
> **输出:** 4
> 最长的子序列是[5，1，2，3]或[4，1，2，3]。其中 5 和 3 大于所有其他子序列元素，即 1 和 2。

**方法:**
思路是使用[分威克树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)数据结构。开始从排列中的最高值迭代到最低值。对于每次迭代，只有当左指针可以移动到更左，右指针可以移动到更右时，才向左或向右移动指针到当前元素。
如果左索引是 L，右索引是 R，那么中间有来自[L+1，R-1]的元素。对于这个特定的迭代 I，使用芬威克树计算小于 min(arr[L]，arr[R])的元素数量。
存储每一个{left+1，right-1，val，index}类型的查询，其中 left 和 right 是当前的 left 和 right 指针，val 是 arr[L]和 arr[R]的最小值，idx 是该特定查询的索引。

1.  按升序对数组进行排序。
2.  按照 val，即 min(arr[L]，arr[R])对查询进行升序排序，将 Fenwick 数组初始化为 0。
3.  从第一个查询开始，遍历数组，直到数组中的值小于或等于 val。对于每个这样的元素，用等于 1 的值更新芬威克树。
4.  查询 l 到 r 范围内的 Fenwick 数组。
5.  打印所有查询结果的最大值。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

struct Query {

    int l, r, x, index;
};

struct Arrays {

    int val, index;
};

// Comparison functions
bool cmp1(Query q1, Query q2)
{
    return q1.x < q2.x;
}

bool cmp2(Arrays x, Arrays y)
{
    return x.val < y.val;
}

// Function to update the value in Fenwick tree
void update(int* Fenwick, int index, int val, int n)
{
    while (index <= n) {

        Fenwick[index] += val;
        index += index & (-index);
    }
}

// Function to return the query result
int query(int* Fenwick, int index, int n)
{
    int sum = 0;

    while (index > 0) {

        sum = sum + Fenwick[index];
        index -= index & (-index);
    }

    return sum;
}

// Function to return the length of subsequence
int maxLength(int n, vector<int>& v)
{
    int where[n + 2];

    memset(where, 0, sizeof where);

    Arrays arr[n];

    // Store the value in struct Array
    for (int i = 1; i <= n; ++i) {

        v[i - 1] = v[i - 1] - 1;

        int x = v[i - 1];

        where[x] = i - 1;
        arr[i - 1].val = x;
        arr[i - 1].index = i - 1;
    }

    // If less than 2 elements are
    // present return that element.
    if (n <= 2) {

        cout << n << endl;

        return 0;
    }

    // Set the left and right pointers to extreme
    int left = n, right = 0, mx = 0;

    Query queries[4 * n];

    int j = 0;
    for (int i = n - 1; i >= 0; --i) {

        // Calculate left and right pointer index.
        left = min(left, where[i]);
        right = max(right, where[i]);

        int diff = right - left;

        if (diff == 0 || diff == 1) {
            continue;
        }

        int val1 = v[left];
        int val2 = v[right];
        int minn = min(val1, val2);

        // Store the queries from [L+1, R-1].
        queries[j].l = left + 1;
        queries[j].r = right - 1;
        queries[j].x = minn;
        queries[j].index = j;

        ++j;
    }

    int Fenwick[n + 1];

    memset(Fenwick, 0, sizeof Fenwick);

    int q = j - 1;

    // Sort array and queries for fenwick updates
    sort(arr, arr + n + 1, cmp2);
    sort(queries, queries + q + 1, cmp1);

    int curr = 0;
    int ans[q];
    memset(ans, 0, sizeof ans);

    // For each query calculate maxx for
    // the answer and store it in ans array.
    for (int i = 0; i <= q; ++i) {

        while (arr[curr].val <= queries[i].x and curr < n) {

            update(Fenwick, arr[curr].index + 1, 1, n);
            curr++;
        }

        ans[queries[i].index] =
                query(Fenwick, queries[i].r + 1, n)
                - query(Fenwick, queries[i].l, n);
    }

    for (int i = 0; i <= q; ++i) {
        mx = max(mx, ans[i]);
    }

    // Mx will be mx + 2 as while calculating
    // mx, we excluded element
    // at index left and right
    mx = mx + 2;
    return mx;
}

// Driver Code
int main()
{
    int n = 6;
    vector<int> v = { 4, 2, 6, 5, 3, 1 };

    cout << maxLength(n, v) << endl;

    return 0;
}
```

## 蟒蛇 3

```
# Python implementation of the above approach
from typing import List
class Query:
    def __init__(self) -> None:
        self.l = 0
        self.r = 0
        self.x = 0
        self.index = 0

class Arrays:
    def __init__(self) -> None:
        self.val = 0
        self.index = 0

# Function to update the value in Fenwick tree
def update(Fenwick: List[int], index: int, val: int, n: int) -> None:
    while (index <= n):
        Fenwick[index] += val
        index += index & (-index)

# Function to return the query result
def query(Fenwick: List[int], index: int, n: int) -> int:
    summ = 0
    while (index > 0):
        summ = summ + Fenwick[index]
        index -= index & (-index)
    return summ

# Function to return the length of subsequence
def maxLength(n: int, v: List[int]) -> int:
    where = [0 for _ in range(n + 2)]
    arr = [Arrays() for _ in range(n)]

    # Store the value in struct Array
    for i in range(1, n + 1):
        v[i - 1] = v[i - 1] - 1
        x = v[i - 1]
        where[x] = i - 1
        arr[i - 1].val = x
        arr[i - 1].index = i - 1

    # If less than 2 elements are
    # present return that element.
    if (n <= 2):
        print(n)
        return 0

    # Set the left and right pointers to extreme
    left = n
    right = 0
    mx = 0
    queries = [Query() for _ in range(4 * n)]
    j = 0
    for i in range(n - 1, -1, -1):

        # Calculate left and right pointer index.
        left = min(left, where[i])
        right = max(right, where[i])
        diff = right - left
        if (diff == 0 or diff == 1):
            continue
        val1 = v[left]
        val2 = v[right]
        minn = min(val1, val2)

        # Store the queries from [L+1, R-1].
        queries[j].l = left + 1
        queries[j].r = right - 1
        queries[j].x = minn
        queries[j].index = j
        j += 1
    Fenwick = [0 for _ in range(n + 1)]
    q = j - 1

    # Sort array and queries for fenwick updates
    arr[:n + 1].sort(key=lambda x: x.val)
    queries[:q + 1].sort(key=lambda val: val.x)
    curr = 0
    ans = [0 for _ in range(q + 1)]

    # For each query calculate maxx for
    # the answer and store it in ans array.
    for i in range(q + 1):
        while (arr[curr].val <= queries[i].x and curr < n):
            update(Fenwick, arr[curr].index + 1, 1, n)
            curr += 1

        # if queries[i].index < q:
        ans[queries[i].index] = query(Fenwick, queries[i].r + 1, n) - query(
            Fenwick, queries[i].l, n)
    for i in range(q + 1):
        mx = max(mx, ans[i])

    # Mx will be mx + 2 as while calculating
    # mx, we excluded element
    # at index left and right
    mx = mx + 2
    return mx

# Driver Code
if __name__ == "__main__":

    n = 6
    v = [4, 2, 6, 5, 3, 1]

    print(maxLength(n, v))

# This code is contributed by sanjeev2552
```

**Output:** 

```
3
```