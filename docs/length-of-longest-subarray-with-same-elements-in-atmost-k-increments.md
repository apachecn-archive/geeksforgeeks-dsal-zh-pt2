# 在大气中具有相同元素的最长子阵列的长度以 K 为增量

> 原文:[https://www . geeksforgeeks . org/Atmos-k 增量中具有相同元素的最长子阵列长度/](https://www.geeksforgeeks.org/length-of-longest-subarray-with-same-elements-in-atmost-k-increments/)

给定一个整数数组 **arr** 和一个数字 **K** ，任务是找到[最长子阵列](https://www.geeksforgeeks.org/longest-increasing-subarray/)的长度，使得该子阵列中的所有元素可以以 K 为增量相同。

**示例:**

> **输入:** arr[] = {2，0，4，6，7}，K = 6
> **输出:** 3
> 最长的子阵是{2，0，4}，可以做成{4，4，4}，总增量= 6 ( ≤ K)
> 
> **输入:** arr[] = {12，10，16，20，7，11}，K = 25
> **输出:** 4
> 最长的子阵是{12，10，16，20}，可以做成{20，20，20}，总增量= 22 ( ≤ K)

**进场:**

*   变量 **i** 将用于存储所需最长子阵列的起点，变量 **j** 用于存储终点。因此，范围将是[i，j]
*   最初，假设有效范围为[0，N]。
*   实际范围[i，j]将使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)计算。对于执行的每个搜索:
    *   一个[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)可以用来寻找范围【I，j】中的最大元素
    *   使范围[i，j]中的所有元素等于找到的最大元素。
    *   然后，使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)数组来获得范围[i，j]中元素的和。
    *   然后，该范围内所需的增量数可以计算为:

```
Total number of increments
 = (j - i + 1) * (max_value) - Σ(i, j)

where i = index of the starting point of the subarray
      j = index of end point of subarray
      max_value = maximum value from index i to j
      Σ(i, j) = sum of all elements from index i to j
```

*   如果要求的增量数小于或等于 **K** ，则为有效子阵列，否则无效。
*   对于无效的子阵列，相应地更新下一个二分搜索法的起点和终点
*   返回最长子阵列范围的长度。

下面是上述方法的实现:

## C++

```
// C++ program to find the length of
// Longest Subarray with same elements
// in atmost K increments

#include <bits/stdc++.h>
using namespace std;

// Initialize array for segment tree
int segment_tree[4 * 1000000];

// Function that builds the segment
// tree to return the max element
// in a range
int build(int* A, int start, int end,
          int node)
{
    if (start == end)
        // update the value in segment
        // tree from given array
        segment_tree[node] = A[start];

    else {
        // find the middle index
        int mid = (start + end) / 2;

        // If there are more than one
        // elements, then recur for left
        // and right subtrees and
        // store the max of values in this node
        segment_tree[node]
            = max(
                build(A, start, mid, 2 * node + 1),
                build(A, mid + 1, end, 2 * node + 2));
    }
    return segment_tree[node];
}

// Function to return the max
// element in the given range
int query(int start, int end, int l, int r,
          int node)
{
    // If the range is out of bounds,
    // return -1

    if (start > r || end < l)
        return -1;
    if (start >= l && end <= r)
        return segment_tree[node];
    int mid = (start + end) / 2;

    return max(query(start, mid, l,
                     r, 2 * node + 1),
               query(mid + 1, end, l,
                     r, 2 * node + 2));
}

// Function that returns length of longest
// subarray with same elements in atmost
// K increments.
int longestSubArray(int* A, int N, int K)
{

    // Initialize the result variable
    // Even though the K is 0,
    // the required longest subarray,
    // in that case, will also be of length 1
    int res = 1;

    // Initialize the prefix sum array
    int preSum[N + 1];

    // Build the prefix sum array
    preSum[0] = A[0];
    for (int i = 0; i < N; i++)
        preSum[i + 1] = preSum[i] + A[i];

    // Build the segment tree
    // for range max query
    build(A, 0, N - 1, 0);

    // Loop through the array
    // with a starting point as i
    // for the required subarray till
    // the longest subarray is found
    for (int i = 0; i < N; i++) {

        int start = i, end = N - 1,
            mid, max_index = i;

        // Performing the binary search
        // to find the endpoint
        // for the selected range
        while (start <= end) {

            // Find the mid for binary search
            mid = (start + end) / 2;

            // Find the max element
            // in the range [i, mid]
            // using Segment Tree
            int max_element
                = query(0, N - 1,
                        i, mid, 0);

            // Total sum of subarray after increments
            int expected_sum = (mid - i + 1)
                               * max_element;

            // Actual sum of elements
            // before increments
            int actual_sum = preSum[mid + 1]
                             - preSum[i];

            // Check if such increment is possible
            // If true, then current i
            // is the actual starting point
            // of the required longest subarray
            if (expected_sum - actual_sum <= K) {

                // Now for finding the endpoint
                // for this range
                // Perform the Binary search again
                // with the updated start
                start = mid + 1;

                // Store max end point for the range
                // to give longest subarray
                max_index = max(max_index, mid);
            }

            // If false, it means that
            // the selected range is invalid
            else {

                // Perform the Binary Search again
                // with the updated end
                end = mid - 1;
            }
        }

        // Store the length of longest subarray
        res = max(res, max_index - i + 1);
    }

    // Return result
    return res;
}

// Driver code
int main()
{
    int arr[] = { 2, 0, 4, 6, 7 }, K = 6;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << longestSubArray(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of
// Longest Subarray with same elements
// in atmost K increments
class GFG
{

    // Initialize array for segment tree
    static int segment_tree[] = new int[4 * 1000000];

    // Function that builds the segment
    // tree to return the max element
    // in a range
    static int build(int A[], int start, int end,
                     int node)
    {
        if (start == end)

            // update the value in segment
            // tree from given array
            segment_tree[node] = A[start];

        else
        {

            // find the middle index
            int mid = (start + end) / 2;

            // If there are more than one
            // elements, then recur for left
            // and right subtrees and
            // store the max of values in this node
            segment_tree[node] = Math.max(
                    build(A, start, mid, 2 * node + 1),
                    build(A, mid + 1, end, 2 * node + 2));
        }
        return segment_tree[node];
    }

    // Function to return the max
    // element in the given range
    static int query(int start, int end, int l, int r,
                     int node)
    {
        // If the range is out of bounds,
        // return -1
        if (start > r || end < l)
            return -1;
        if (start >= l && end <= r)
            return segment_tree[node];
        int mid = (start + end) / 2;

        return Math.max(query(start, mid, l,
                        r, 2 * node + 1),
                        query(mid + 1, end, l,
                        r, 2 * node + 2));
    }

    // Function that returns length of longest
    // subarray with same elements in atmost
    // K increments.
    static int longestSubArray(int A[], int N, int K)
    {

        // Initialize the result variable
        // Even though the K is 0,
        // the required longest subarray,
        // in that case, will also be of length 1
        int res = 1;

        // Initialize the prefix sum array
        int preSum[] = new int[N + 1];

        // Build the prefix sum array
        preSum[0] = A[0];
        for (int i = 0; i < N; i++)
            preSum[i + 1] = preSum[i] + A[i];

        // Build the segment tree
        // for range max query
        build(A, 0, N - 1, 0);

        // Loop through the array
        // with a starting point as i
        // for the required subarray till
        // the longest subarray is found
        for (int i = 0; i < N; i++)
        {

            int start = i, end = N - 1,
                mid, max_index = i;

            // Performing the binary search
            // to find the endpoint
            // for the selected range
            while (start <= end)
            {

                // Find the mid for binary search
                mid = (start + end) / 2;

                // Find the max element
                // in the range [i, mid]
                // using Segment Tree
                int max_element = query(0, N - 1,
                                        i, mid, 0);

                // Total sum of subarray after increments
                int expected_sum = (mid - i + 1)
                                * max_element;

                // Actual sum of elements
                // before increments
                int actual_sum = preSum[mid + 1]
                                - preSum[i];

                // Check if such increment is possible
                // If true, then current i
                // is the actual starting point
                // of the required longest subarray
                if (expected_sum - actual_sum <= K)
                {

                    // Now for finding the endpoint
                    // for this range
                    // Perform the Binary search again
                    // with the updated start
                    start = mid + 1;

                    // Store max end point for the range
                    // to give longest subarray
                    max_index = Math.max(max_index, mid);
                }

                // If false, it means that
                // the selected range is invalid
                else
                {

                    // Perform the Binary Search again
                    // with the updated end
                    end = mid - 1;
                }
            }

            // Store the length of longest subarray
            res = Math.max(res, max_index - i + 1);
        }

        // Return result
        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 2, 0, 4, 6, 7 }, K = 6;
        int N = arr.length;

        System.out.println(longestSubArray(arr, N, K));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find the length of
# Longest Subarray with same elements
# in atmost K increments

# Initialize array for segment tree
segment_tree = [0]*(4 * 1000000);

# Function that builds the segment
# tree to return the max element
# in a range
def build(A, start, end, node) :

    if (start == end) :

        # update the value in segment
        # tree from given array
        segment_tree[node] = A[start];

    else :

        # find the middle index
        mid = (start + end) // 2;

        # If there are more than one
        # elements, then recur for left
        # and right subtrees and
        # store the max of values in this node
        segment_tree[node] = max(
                build(A, start, mid, 2 * node + 1),
                build(A, mid + 1, end, 2 * node + 2));

    return segment_tree[node];

# Function to return the max
# element in the given range
def query(start, end, l, r, node) :

    # If the range is out of bounds,
    # return -1
    if (start > r or end < l) :
        return -1;

    if (start >= l and end <= r) :
        return segment_tree[node];

    mid = (start + end) // 2;

    return max(query(start, mid, l,
                    r, 2 * node + 1),
            query(mid + 1, end, l,
                    r, 2 * node + 2));

# Function that returns length of longest
# subarray with same elements in atmost
# K increments.
def longestSubArray(A, N, K) :

    # Initialize the result variable
    # Even though the K is 0,
    # the required longest subarray,
    # in that case, will also be of length 1
    res = 1;

    # Initialize the prefix sum array
    preSum = [0] * (N + 1);

    # Build the prefix sum array
    preSum[0] = A[0];
    for i in range(N) :
        preSum[i + 1] = preSum[i] + A[i];

    # Build the segment tree
    # for range max query
    build(A, 0, N - 1, 0);

    # Loop through the array
    # with a starting point as i
    # for the required subarray till
    # the longest subarray is found
    for i in range(N) :

        start = i;
        end = N - 1;
        max_index = i;

        # Performing the binary search
        # to find the endpoint
        # for the selected range
        while (start <= end) :

            # Find the mid for binary search
            mid = (start + end) // 2;

            # Find the max element
            # in the range [i, mid]
            # using Segment Tree
            max_element = query(0, N - 1, i, mid, 0);

            # Total sum of subarray after increments
            expected_sum = (mid - i + 1) * max_element;

            # Actual sum of elements
            # before increments
            actual_sum = preSum[mid + 1] - preSum[i];

            # Check if such increment is possible
            # If true, then current i
            # is the actual starting point
            # of the required longest subarray
            if (expected_sum - actual_sum <= K) :

                # Now for finding the endpoint
                # for this range
                # Perform the Binary search again
                # with the updated start
                start = mid + 1;

                # Store max end point for the range
                # to give longest subarray
                max_index = max(max_index, mid);

            # If false, it means that
            # the selected range is invalid
            else :

                # Perform the Binary Search again
                # with the updated end
                end = mid - 1;

        # Store the length of longest subarray
        res = max(res, max_index - i + 1);

    # Return result
    return res;

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 0, 4, 6, 7 ]; K = 6;
    N = len(arr);

    print(longestSubArray(arr, N, K));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the length of
// longest Subarray with same elements
// in atmost K increments
using System;

class GFG
{

    // Initialize array for segment tree
    static int []segment_tree = new int[4 * 1000000];

    // Function that builds the segment
    // tree to return the max element
    // in a range
    static int build(int []A, int start, int end,
                    int node)
    {
        if (start == end)

            // update the value in segment
            // tree from given array
            segment_tree[node] = A[start];

        else
        {

            // find the middle index
            int mid = (start + end) / 2;

            // If there are more than one
            // elements, then recur for left
            // and right subtrees and
            // store the max of values in this node
            segment_tree[node] = Math.Max(
                    build(A, start, mid, 2 * node + 1),
                    build(A, mid + 1, end, 2 * node + 2));
        }
        return segment_tree[node];
    }

    // Function to return the max
    // element in the given range
    static int query(int start, int end, int l, int r,
                    int node)
    {
        // If the range is out of bounds,
        // return -1
        if (start > r || end < l)
            return -1;
        if (start >= l && end <= r)
            return segment_tree[node];
        int mid = (start + end) / 2;

        return Math.Max(query(start, mid, l,
                        r, 2 * node + 1),
                        query(mid + 1, end, l,
                        r, 2 * node + 2));
    }

    // Function that returns length of longest
    // subarray with same elements in atmost
    // K increments.
    static int longestSubArray(int []A, int N, int K)
    {

        // Initialize the result variable
        // Even though the K is 0,
        // the required longest subarray,
        // in that case, will also be of length 1
        int res = 1;

        // Initialize the prefix sum array
        int []preSum = new int[N + 1];

        // Build the prefix sum array
        preSum[0] = A[0];
        for (int i = 0; i < N; i++)
            preSum[i + 1] = preSum[i] + A[i];

        // Build the segment tree
        // for range max query
        build(A, 0, N - 1, 0);

        // Loop through the array
        // with a starting point as i
        // for the required subarray till
        // the longest subarray is found
        for (int i = 0; i < N; i++)
        {

            int start = i, end = N - 1,
                mid, max_index = i;

            // Performing the binary search
            // to find the endpoint
            // for the selected range
            while (start <= end)
            {

                // Find the mid for binary search
                mid = (start + end) / 2;

                // Find the max element
                // in the range [i, mid]
                // using Segment Tree
                int max_element = query(0, N - 1,
                                        i, mid, 0);

                // Total sum of subarray after increments
                int expected_sum = (mid - i + 1)
                                * max_element;

                // Actual sum of elements
                // before increments
                int actual_sum = preSum[mid + 1]
                                - preSum[i];

                // Check if such increment is possible
                // If true, then current i
                // is the actual starting point
                // of the required longest subarray
                if (expected_sum - actual_sum <= K)
                {

                    // Now for finding the endpoint
                    // for this range
                    // Perform the Binary search again
                    // with the updated start
                    start = mid + 1;

                    // Store max end point for the range
                    // to give longest subarray
                    max_index = Math.Max(max_index, mid);
                }

                // If false, it means that
                // the selected range is invalid
                else
                {

                    // Perform the Binary Search again
                    // with the updated end
                    end = mid - 1;
                }
            }

            // Store the length of longest subarray
            res = Math.Max(res, max_index - i + 1);
        }

        // Return result
        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 2, 0, 4, 6, 7 };
        int K = 6;
        int N = arr.Length;

        Console.WriteLine(longestSubArray(arr, N, K));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript program to find the length of
    // Longest Subarray with same elements
    // in atmost K increments

    // Initialize array for segment tree
    let segment_tree = new Array(4 * 1000000);

    // Function that builds the segment
    // tree to return the max element
    // in a range
    function build(A, start, end, node)
    {
        if (start == end)

            // update the value in segment
            // tree from given array
            segment_tree[node] = A[start];

        else
        {

            // find the middle index
            let mid = parseInt((start + end) / 2, 10);

            // If there are more than one
            // elements, then recur for left
            // and right subtrees and
            // store the max of values in this node
            segment_tree[node] = Math.max(
                    build(A, start, mid, 2 * node + 1),
                    build(A, mid + 1, end, 2 * node + 2));
        }
        return segment_tree[node];
    }

    // Function to return the max
    // element in the given range
    function query(start, end, l, r, node)
    {
        // If the range is out of bounds,
        // return -1
        if (start > r || end < l)
            return -1;
        if (start >= l && end <= r)
            return segment_tree[node];
        let mid = parseInt((start + end) / 2, 10);

        return Math.max(query(start, mid, l,
                        r, 2 * node + 1),
                        query(mid + 1, end, l,
                        r, 2 * node + 2));
    }

    // Function that returns length of longest
    // subarray with same elements in atmost
    // K increments.
    function longestSubArray(A, N, K)
    {

        // Initialize the result variable
        // Even though the K is 0,
        // the required longest subarray,
        // in that case, will also be of length 1
        let res = 1;

        // Initialize the prefix sum array
        let preSum = new Array(N + 1);

        // Build the prefix sum array
        preSum[0] = A[0];
        for (let i = 0; i < N; i++)
            preSum[i + 1] = preSum[i] + A[i];

        // Build the segment tree
        // for range max query
        build(A, 0, N - 1, 0);

        // Loop through the array
        // with a starting point as i
        // for the required subarray till
        // the longest subarray is found
        for (let i = 0; i < N; i++)
        {

            let start = i, end = N - 1, mid, max_index = i;

            // Performing the binary search
            // to find the endpoint
            // for the selected range
            while (start <= end)
            {

                // Find the mid for binary search
                mid = parseInt((start + end) / 2, 10);

                // Find the max element
                // in the range [i, mid]
                // using Segment Tree
                let max_element = query(0, N - 1, i, mid, 0);

                // Total sum of subarray after increments
                let expected_sum = (mid - i + 1) * max_element;

                // Actual sum of elements
                // before increments
                let actual_sum = preSum[mid + 1] - preSum[i];

                // Check if such increment is possible
                // If true, then current i
                // is the actual starting point
                // of the required longest subarray
                if (expected_sum - actual_sum <= K)
                {

                    // Now for finding the endpoint
                    // for this range
                    // Perform the Binary search again
                    // with the updated start
                    start = mid + 1;

                    // Store max end point for the range
                    // to give longest subarray
                    max_index = Math.max(max_index, mid);
                }

                // If false, it means that
                // the selected range is invalid
                else
                {

                    // Perform the Binary Search again
                    // with the updated end
                    end = mid - 1;
                }
            }

            // Store the length of longest subarray
            res = Math.max(res, max_index - i + 1);
        }

        // Return result
        return res;
    }

    let arr = [ 2, 0, 4, 6, 7 ], K = 6;
    let N = arr.length;

    document.write(longestSubArray(arr, N, K));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N*(log(N)) <sup>2</sup> )