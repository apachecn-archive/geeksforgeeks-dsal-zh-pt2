# 将由相同元素组成的最长子阵列的长度最大化最多 K 次递减

> 原文:[https://www . geeksforgeeks . org/最大化最长子阵列长度-由最多 k 个递减的相同元素组成/](https://www.geeksforgeeks.org/maximize-length-of-longest-subarray-consisting-of-same-elements-by-at-most-k-decrements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是找出由相同元素组成的最长子数组的长度，该长度可以通过将数组元素递减 **1** 最多 **K** 次来获得。

**示例:**

> **输入:** arr[] = { 1，2，3 }，K = 1
> **输出:** 2
> **解释:**
> arr[0]减 1 将 arr[]修改为{ 1，1，3 }
> 元素相等的最长子阵列为{ 1，1 }。
> 因此，要求输出为 2。
> 
> **输入:** arr[] = { 1，7，3，4，5，6 }，K = 6
> T3】输出: 4

**方法:**使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)和[二分搜索法手法](https://www.geeksforgeeks.org/binary-search/)可以解决问题。想法是使用以下观察结果:

> 使子阵列{ arr[start]，…，arr[end] }的所有阵列元素相等所需的递减操作总数
> =**(σ(start，end))–(end–start+1)*(min _ value)**
> 
> 其中， **start** =子阵列起点索引
> **end** =子阵列终点索引
> **min_value** =从索引 I 到 j 的最小值
> **σ(开始，结束)** =从索引 I 到 j 的所有元素之和

按照以下步骤解决上述问题:

1.  初始化[段树](https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)计算阵列子阵列中的最小元素，初始化[前缀和阵列](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)计算子阵列的和元素。
2.  [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**。对于每个**I<sup>th</sup>T7】元素，执行以下操作:**
    *   初始化两个变量，比如说， **start = i** ，**end = N–1**，在**【开始，结束】**范围内应用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，根据上述观察，通过最多递减 **K** 运算，检查子阵列 **{ arr【开始】，…，arr【结束】}** 的所有元素是否可以相等。
    *   如果子阵列 **{ arr[start]，…，arr[end] }** 的所有元素可以通过最多递减 **K** 操作而相等，则更新 **start = (start + end) / 2 + 1** 。
    *   否则，更新 **end =(开始+结束)/2–1**T2】
3.  最后，打印从上述操作中获得的最长子阵列的长度。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to construct Segment Tree
// to return the minimum element in a range
int build(int tree[], int* A, int start,
          int end, int node)
{
    // If leaf nodes of
    // the tree are found
    if (start == end) {

        // Update the value in segment
        // tree from given array
        tree[node] = A[start];

        return tree[node];
    }

    // Divide left and right subtree
    int mid = (start + end) / 2;

    // Stores smallest element in
    // subarray { arr[start], arr[mid] }
    int X = build(tree, A, start, mid,
                  2 * node + 1);

    // Stores smallest element in
    // subarray { arr[mid + 1], arr[end] }
    int Y = build(tree, A, mid + 1,
                  end, 2 * node + 2);

    // Stores smallest element in
    // subarray { arr[start], arr[end] }
    return tree[node] = min(X, Y);
}

// Function to find the smallest
// element present in a subarray
int query(int tree[], int start, int end,
          int l, int r, int node)
{
    // If elements of the subarray
    // are not in the range [l, r]
    if (start > r || end < l)
        return INT_MAX;

    // If all the elements of the
    // subarray are in the range [l, r]
    if (start >= l && end <= r)
        return tree[node];

    // Divide tree into left
    // and right subtree
    int mid = (start + end) / 2;

    // Stores smallest element
    // in left subtree
    int X = query(tree, start, mid, l,
                  r, 2 * node + 1);

    // Stores smallest element in
    // right subtree
    int Y = query(tree, mid + 1, end, l,
                  r, 2 * node + 2);

    return min(X, Y);
}

// Function that find length of longest
// subarray with all equal elements in
// atmost K decrements
int longestSubArray(int* A, int N, int K)
{
    // Stores length of longest subarray
    // with all equal elements in atmost
    // K decrements.
    int res = 1;

    // Store the prefix sum array
    int preSum[N + 1];

    // Calculate the prefix sum array
    preSum[0] = A[0];
    for (int i = 0; i < N; i++)
        preSum[i + 1] = preSum[i] + A[i];

    int tree[4 * N + 5];

    // Build the segment tree
    // for range min query
    build(tree, A, 0, N - 1, 0);

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Stores start index
        // of the subarray
        int start = i;

        // Stores end index
        // of the subarray
        int end = N - 1;

        int mid;

        // Stores end index of
        // the longest subarray
        int max_index = i;

        // Performing the binary search
        // to find the endpoint
        // for the selected range
        while (start <= end) {

            // Find the mid for binary search
            mid = (start + end) / 2;

            // Find the smallest element in
            // range [i, mid] using Segment Tree
            int min_element
                = query(tree, 0, N - 1, i, mid, 0);

            // Stores total sum of subarray
            // after K decrements
            int expected_sum
                = (mid - i + 1) * min_element;

            // Stores sum of elements of
            // subarray before K decrements
            int actual_sum
                = preSum[mid + 1] - preSum[i];

            // If subarray found with
            // all equal elements
            if (actual_sum - expected_sum <= K) {

                // Update start
                start = mid + 1;

                // Update max_index
                max_index = max(max_index, mid);
            }

            // If false, it means that
            // the selected range is invalid
            else {

                // Update end
                end = mid - 1;
            }
        }

        // Store the length of longest subarray
        res = max(res, max_index - i + 1);
    }

    // Return result
    return res;
}

// Driver Code
int main()
{
    int arr[] = { 1, 7, 3, 4, 5, 6 };
    int k = 6;
    int n = 6;
    cout << longestSubArray(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to construct Segment Tree
// to return the minimum element in a range
static int build(int tree[], int[] A, int start,
                 int end, int node)
{

    // If leaf nodes of
    // the tree are found
    if (start == end)
    {

        // Update the value in segment
        // tree from given array
        tree[node] = A[start];

        return tree[node];
    }

    // Divide left and right subtree
    int mid = (start + end) / 2;

    // Stores smallest element in
    // subarray { arr[start], arr[mid] }
    int X = build(tree, A, start, mid,
                  2 * node + 1);

    // Stores smallest element in
    // subarray { arr[mid + 1], arr[end] }
    int Y = build(tree, A, mid + 1,
                 end, 2 * node + 2);

    // Stores smallest element in
    // subarray { arr[start], arr[end] }
    return (tree[node] = Math.min(X, Y));
}

// Function to find the smallest
// element present in a subarray
static int query(int tree[], int start, int end,
                 int l, int r, int node)
{

    // If elements of the subarray
    // are not in the range [l, r]
    if (start > r || end < l)
        return Integer.MAX_VALUE;

    // If all the elements of the
    // subarray are in the range [l, r]
    if (start >= l && end <= r)
        return tree[node];

    // Divide tree into left
    // and right subtree
    int mid = (start + end) / 2;

    // Stores smallest element
    // in left subtree
    int X = query(tree, start, mid, l,
                  r, 2 * node + 1);

    // Stores smallest element in
    // right subtree
    int Y = query(tree, mid + 1, end, l,
                  r, 2 * node + 2);

    return Math.min(X, Y);
}

// Function that find length of longest
// subarray with all equal elements in
// atmost K decrements
static int longestSubArray(int[] A, int N, int K)
{

    // Stores length of longest subarray
    // with all equal elements in atmost
    // K decrements.
    int res = 1;

    // Store the prefix sum array
    int preSum[] = new int[N + 1];

    // Calculate the prefix sum array
    preSum[0] = A[0];
    for(int i = 0; i < N; i++)
        preSum[i + 1] = preSum[i] + A[i];

    int tree[] = new int[4 * N + 5];

    // Build the segment tree
    // for range min query
    build(tree, A, 0, N - 1, 0);

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Stores start index
        // of the subarray
        int start = i;

        // Stores end index
        // of the subarray
        int end = N - 1;

        int mid;

        // Stores end index of
        // the longest subarray
        int max_index = i;

        // Performing the binary search
        // to find the endpoint
        // for the selected range
        while (start <= end)
        {

            // Find the mid for binary search
            mid = (start + end) / 2;

            // Find the smallest element in
            // range [i, mid] using Segment Tree
            int min_element = query(tree, 0, N - 1,
                                    i, mid, 0);

            // Stores total sum of subarray
            // after K decrements
            int expected_sum = (mid - i + 1) *
                                min_element;

            // Stores sum of elements of
            // subarray before K decrements
            int actual_sum = preSum[mid + 1] -
                             preSum[i];

            // If subarray found with
            // all equal elements
            if (actual_sum - expected_sum <= K)
            {

                // Update start
                start = mid + 1;

                // Update max_index
                max_index = Math.max(max_index, mid);
            }

            // If false, it means that
            // the selected range is invalid
            else
            {

                // Update end
                end = mid - 1;
            }
        }

        // Store the length of longest subarray
        res = Math.max(res, max_index - i + 1);
    }

    // Return result
    return res;
}

// Driver Code
static public void main(String args[])
{
    int arr[] = { 1, 7, 3, 4, 5, 6 };
    int k = 6;
    int n = 6;

    System.out.print(longestSubArray(arr, n, k));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to construct Segment Tree
# to return the minimum element in a range
def build(tree, A, start, end, node):

    # If leaf nodes of
    # the tree are found
    if (start == end):

        # Update the value in segment
        # tree from given array
        tree[node] = A[start]

        return tree[node]

    # Divide left and right subtree
    mid = (int)((start + end) / 2)

    # Stores smallest element in
    # subarray : arr[start], arr[mid]
    X = build(tree, A, start, mid,
              2 * node + 1)

    # Stores smallest element in
    # subarray : arr[mid + 1], arr[end]
    Y = build(tree, A, mid + 1,
             end, 2 * node + 2)

    # Stores smallest element in
    # subarray : arr[start], arr[end]
    return (tree[node] == min(X, Y))

# Function to find the smallest
# element present in a subarray
def query(tree, start, end, l, r, node):

    # If elements of the subarray
    # are not in the range [l, r]
    if (start > r or end < l) :
        return sys.maxsize

    # If all the elements of the
    # subarray are in the range [l, r]
    if (start >= l and end <= r):
        return tree[node]

    # Divide tree into left
    # and right subtree
    mid = (int)((start + end) / 2)

    # Stores smallest element
    # in left subtree
    X = query(tree, start, mid, l,
              r, 2 * node + 1)

    # Stores smallest element in
    # right subtree
    Y = query(tree, mid + 1, end, l,
            r, 2 * node + 2)

    return min(X, Y)

# Function that find length of longest
# subarray with all equal elements in
# atmost K decrements
def longestSubArray(A, N, K):

    # Stores length of longest subarray
    # with all equal elements in atmost
    # K decrements.
    res = 1

    # Store the prefix sum array
    preSum = [0] * (N + 1)

    # Calculate the prefix sum array
    preSum[0] = A[0]
    for i in range(N):
        preSum[i + 1] = preSum[i] + A[i]

    tree = [0] * (4 * N + 5)

    # Build the segment tree
    # for range min query
    build(tree, A, 0, N - 1, 0)

    # Traverse the array
    for i in range(N):

        # Stores start index
        # of the subarray
        start = i

        # Stores end index
        # of the subarray
        end = N - 1

        # Stores end index of
        # the longest subarray
        max_index = i

        # Performing the binary search
        # to find the endpoint
        # for the selected range
        while (start <= end):

            # Find the mid for binary search
            mid = (int)((start + end) / 2)

            # Find the smallest element in
            # range [i, mid] using Segment Tree
            min_element = query(tree, 0, N - 1, i, mid, 0)

            # Stores total sum of subarray
            # after K decrements
            expected_sum = (mid - i + 1) * min_element

            # Stores sum of elements of
            # subarray before K decrements
            actual_sum = preSum[mid + 1] - preSum[i]

            # If subarray found with
            # all equal elements
            if (actual_sum - expected_sum <= K):

                # Update start
                start = mid + 1

                # Update max_index
                max_index = max(max_index, mid)

            # If false, it means that
            # the selected range is invalid
            else:

                # Update end
                end = mid - 1

        # Store the length of longest subarray
        res = max(res, max_index - i + 2)

    # Return result
    return res

# Driver Code
arr = [ 1, 7, 3, 4, 5, 6 ]
k = 6
n = 6

print(longestSubArray(arr, n, k))

# This code is contributed by splevel62
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to construct Segment Tree
// to return the minimum element in a range
static int build(int[] tree, int[] A, int start,
                 int end, int node)
{

    // If leaf nodes of
    // the tree are found
    if (start == end)
    {

        // Update the value in segment
        // tree from given array
        tree[node] = A[start];

        return tree[node];
    }

    // Divide left and right subtree
    int mid = (start + end) / 2;

    // Stores smallest element in
    // subarray { arr[start], arr[mid] }
    int X = build(tree, A, start, mid,
                  2 * node + 1);

    // Stores smallest element in
    // subarray { arr[mid + 1], arr[end] }
    int Y = build(tree, A, mid + 1,
                  end, 2 * node + 2);

    // Stores smallest element in
    // subarray { arr[start], arr[end] }
    return (tree[node] = Math.Min(X, Y));
}

// Function to find the smallest
// element present in a subarray
static int query(int[] tree, int start, int end,
                 int l, int r, int node)
{

    // If elements of the subarray
    // are not in the range [l, r]
    if (start > r || end < l)
        return Int32.MaxValue;

    // If all the elements of the
    // subarray are in the range [l, r]
    if (start >= l && end <= r)
        return tree[node];

    // Divide tree into left
    // and right subtree
    int mid = (start + end) / 2;

    // Stores smallest element
    // in left subtree
    int X = query(tree, start, mid, l,
                  r, 2 * node + 1);

    // Stores smallest element in
    // right subtree
    int Y = query(tree, mid + 1, end, l,
                  r, 2 * node + 2);

    return Math.Min(X, Y);
}

// Function that find length of longest
// subarray with all equal elements in
// atmost K decrements
static int longestSubArray(int[] A, int N, int K)
{

    // Stores length of longest subarray
    // with all equal elements in atmost
    // K decrements.
    int res = 1;

    // Store the prefix sum array
    int[] preSum = new int[N + 1];

    // Calculate the prefix sum array
    preSum[0] = A[0];
    for(int i = 0; i < N; i++)
        preSum[i + 1] = preSum[i] + A[i];

    int[] tree = new int[4 * N + 5];

    // Build the segment tree
    // for range min query
    build(tree, A, 0, N - 1, 0);

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Stores start index
        // of the subarray
        int start = i;

        // Stores end index
        // of the subarray
        int end = N - 1;

        int mid;

        // Stores end index of
        // the longest subarray
        int max_index = i;

        // Performing the binary search
        // to find the endpoint
        // for the selected range
        while (start <= end)
        {

            // Find the mid for binary search
            mid = (start + end) / 2;

            // Find the smallest element in
            // range [i, mid] using Segment Tree
            int min_element = query(tree, 0, N - 1,
                                    i, mid, 0);

            // Stores total sum of subarray
            // after K decrements
            int expected_sum = (mid - i + 1) *
                                min_element;

            // Stores sum of elements of
            // subarray before K decrements
            int actual_sum = preSum[mid + 1] -
                             preSum[i];

            // If subarray found with
            // all equal elements
            if (actual_sum - expected_sum <= K)
            {

                // Update start
                start = mid + 1;

                // Update max_index
                max_index = Math.Max(max_index, mid);
            }

            // If false, it means that
            // the selected range is invalid
            else
            {

                // Update end
                end = mid - 1;
            }
        }

        // Store the length of longest subarray
        res = Math.Max(res, max_index - i + 1);
    }

    // Return result
    return res;
}

// Driver Code
static void Main()
{
    int[] arr = { 1, 7, 3, 4, 5, 6 };
    int k = 6;
    int n = 6;

    Console.WriteLine(longestSubArray(arr, n, k));
}
}

// This code is contributed by susmitakundugoaldanga
```

**Output:**

```
4
```

***时间复杂度:**O(N *(log(N))<sup>2</sup>)*
***辅助空间:O(N)***