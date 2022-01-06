# 为多个查询找到数组中的第 K 个最小元素

> 原文:[https://www . geeksforgeeks . org/find-k-th-多查询数组中的最小元素/](https://www.geeksforgeeks.org/find-k-th-smallest-element-in-an-array-for-multiple-queries/)

给定大小为 **N** 的数组 **arr[]** 和由需要在给定数组上处理的 **M** 个查询组成的数组 **Q[][]** 。众所周知，这些查询可以是以下两种类型:

*   **类型 1:** 如果 Q = 1，那么在数组{type，element_to_add}中添加一个元素。
*   **键入 2:** 如果 Q = 2，则打印数组中的第 K 个最小元素。{type，k}

任务是执行给定的查询，从而给出以下约束:

*   1 ≤查询数≤ 1000000。
*   1 ≤ N ≤ 1000000。
*   1 ≤ arr[i] ≤ 100000000。并且，数组可以包含重复的条目。

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6}，Q[][] = {{1，7}，{2，4}，{1，5}，{2，6}}
> **输出:** 4 5
> **解释:**
> 第一个查询用于在数组中添加 7。数组 arr[]变成:{1，2，3，4，5，6，7}
> 第二个查询是查找第 4 个<sup>最小元素。在这种情况下是 4。
> 第三个查询用于在数组中添加 5。数组 arr[]变成:{1，2，3，4，5，5，6，7}
> 第四个查询是查找第 6 个<sup>最小元素。在这种情况下是 5。</sup></sup>
> 
> **输入:** arr[] = {2，4，2，1，5，6，2，4}，Q[][] = {{1，3}，{2，2}，{1，10}，{2，7}}
> **输出:** 2 4

**朴素方法:**解决这个问题的朴素方法是在数组中添加元素，并为每个第一类查询对数组进行排序。并且，每当第二种类型的查询发生时，打印排序数组中的第 K 个元素。

**时间复杂度:** *O(M * (Nlog(N)))* 其中 M 为查询数，N 为数组大小。

**高效方法:**想法是使用[基于策略的数据结构](https://www.geeksforgeeks.org/policy-based-data-structures-g/)。对于这个问题，我们可以使用 [order_of_key](https://www.geeksforgeeks.org/order_of_key-in-c/) 数据结构来查找数组中的第 K 个最小元素。

*   [order_of_key()](https://www.geeksforgeeks.org/order_of_key-in-c/) 是有序集的内置函数，它是 C++中基于[策略的数据结构](https://www.geeksforgeeks.org/policy-based-data-structures-g/)。基于策略的数据结构不是 C++标准库的一部分，但是 g++编译器支持它们。这种数据结构找到了对数时间复杂度的第 K 个最小元素。
*   但是，这种数据结构不允许重复键。为了使用重复元素的数据结构，使用了[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)。
*   我们创建一对给定的元素和索引号，将其插入到基于策略的数据结构中。
*   首先通过比较第一个元素和第二个元素来对这些对进行排序。例如，(2，1)在(2，7)之前排序。

下面是上述方法的实现:

```
// C++ program to find K-th
// smallest element in an array
// for multiple queries

#include <bits/stdc++.h>
using namespace std;

#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace __gnu_pbds;

template <class T>

// Defining the policy-based data
// structure
using oset
    = tree<T, null_type,
           less<T>, rb_tree_tag,
           tree_order_statistics_node_update>;

// Function to find K-th
// smallest element in an array
// for multiple queries
void Operations(int arr[], int n,
                int query[][2], int k)
{

    // Declare the data structure that
    // stores the pairs
    oset<pair<int, int> > s;

    int j = 0;
    // Loop to insert the initial array
    // elements into the set
    for (j = 0; j < n; j++) {
        s.insert({ arr[j], j });
    }

    // Loop to process the queries
    for (int i = 0; i < k; i++) {
        if (query[i][0] == 1) {

            // Inserting the element if the
            // type of query is 1
            s.insert({ query[i][1], j });
            j++;
        }

        // Finding the K-th smallest element
        // if the type of the query is 2
        else if (query[i][0] == 2) {
            cout << (*s
                          .find_by_order(
                              query[i][1] - 1))
                        .first
                 << endl;
        }
    }
}

// Driver code
int main()
{
    int n = 8;
    int arr[] = { 2, 4, 2, 1, 5, 6, 2, 4 };

    int k = 4;
    // Queries. The first element denotes
    // the type of the query
    int query[4][2] = { { 1, 3 },
                        { 2, 2 },
                        { 1, 10 },
                        { 2, 7 } };

    Operations(arr, n, query, k);

    return 0;
}
```

**Output:**

```
2
4

```

**时间复杂度:** *O(M * log(N))* ，其中 M 为查询数，N 为数组大小。