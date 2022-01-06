# 最长子阵列，最大值和最小值之差最大为-K

> 原文:[https://www . geesforgeks . org/最长子阵列最大和最小差值最多为 k/](https://www.geeksforgeeks.org/longest-subarray-such-that-difference-of-max-and-min-is-at-most-k/)

给定一个长度为 **N** 的**数组 arr[]** ，任务是找到最长子序列的长度，使其最大元素和最小元素之差不超过一个整数 **K.**

一个序列 *a* 是一个序列 *b* 的子序列如果？？？？通过删除几个(可能是零个)元素，可以从 *b* 中获得 a。例如，[3，1][3，1]是[3，2，1][3，2，1]和[4，3，1][4，3，1]的子序列，但不是[1，3，3，7][1，3，3，7]和[3，10，4][3，10，4]的子序列。

**示例:**

> **输入:** K = 3，arr[]= {1，4，5，6，9}
> **输出:** 3
> **说明:**
> 最大的斯巴瑞是{4，5，6}
> 
> **输入:** K = 4，arr[]= {1，2，3，4，5}
> **输出:** 5
> **说明:**
> 最大的斯巴瑞是{1，2，3，4，5}

**天真的方法:**

*   [生成所有子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)[找到子阵中的最小值和最大值](https://www.geeksforgeeks.org/maximum-and-minimum-in-an-array/)。
*   计算最小值和最大值之间的差值，如果它小于或等于 K，则更新答案。

***时间复杂度:** O(N <sup>3</sup> )*

**高效进场:**思路是先[整理阵](https://www.geeksforgeeks.org/sorting-algorithms/)，然后用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)优化进场。

*   [给定数组排序](https://www.geeksforgeeks.org/array-data-structure/array-sorting/)
*   对于数组中的每个不同元素 **A[i]** ，找到第一个元素 **A[j]** ，这样 **(A[j]-A[i]) > K** 。
*   对于它的实现，我们使用 [**【二分搜索法】**](https://www.geeksforgeeks.org/binary-search/) 或 [**下界**](https://www.geeksforgeeks.org/upper_bound-and-lower_bound-for-vector-in-cpp-stl/) 并且每次更新 ans 作为先前 ans 的最大值和 indixes 的差值。

下面是上述方法的实现:

## C++

```
// C++ program to find longest
// subarray such that difference
// of max and min is at-most K

#include <bits/stdc++.h>
using namespace std;

// Function to calculate longest
// subarray with above condition
int findLargestSubarray(
    vector<int>& arr,
    int N, int K)
{

    // Sort the array
    sort(arr.begin(), arr.end());

    int value1 = arr[0], value2 = 0;
    int index1, index2, i, MAX;
    index1 = index2 = 0;
    i = 0, MAX = 0;

    // Loop which will terminate
    // when no further elements
    // can be included in the subarray

    while (index2 != N) {

        // first value such that
        // arr[index2] - arr[index1] > K
        value2 = value1 + (K + 1);

        // calculate its index using lower_bound
        index2 = lower_bound(arr.begin(),
                             arr.end(), value2)
                 - arr.begin();

        // index2- index1 will give
        // the accurate length
        // of subarray then compare
        // for MAX length and store
        // in MAX variable
        MAX = max(MAX, (index2 - index1));

        // change the index1
        // to next greater element
        // than previous one
        // and recalculate the value1
        index1
            = lower_bound(
                  arr.begin(),
                  arr.end(), arr[index1] + 1)
              - arr.begin();
        value1 = arr[index1];
    }

    // finally return answer MAX
    return MAX;
}
// Driver Code
int main()
{
    int N, K;
    N = 18;
    K = 5;
    vector<int> arr{ 1, 1, 1, 2, 2,
                     2, 2, 2, 3,
                     3, 3, 6, 6, 7,
                     7, 7, 7, 7 };
    cout << findLargestSubarray(arr, N, K);
    return 0;
}
```

**Output:** 

```
15
```

**时间复杂度:** O(N*log(N))