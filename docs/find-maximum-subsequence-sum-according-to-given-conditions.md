# 根据给定条件求最大子序列和

> 原文:[https://www . geesforgeks . org/find-最大-子序列-根据给定条件求和/](https://www.geeksforgeeks.org/find-maximum-subsequence-sum-according-to-given-conditions/)

给定一个整数数组 **nums** 和一个整数 **K** ，任务是找到数组的非空子序列的最大和，使得对于子序列中每两个连续的整数，nums[i]和 nums[j]，其中 **i < j** ，满足条件**j–I<= K**。

> 数组的**子序列**是通过从数组中删除一些元素(可以是零)而获得的，剩余的元素保持其原始顺序。

**例:**

```
Input: nums = [10, 2, -10, 5, 20], K = 2
Output: 37
Explanation: 
The subsequence is [10, 2, 5, 20].

Input: nums = [-1, -2, -3], K = 1
Output: -1

Input: nums = [10, -2, -10, -5, 20], K = 2
Output: 23
```

**进场:**

*   这个问题的最优解可以通过[滑动窗口最大化和动态规划](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/)来实现。
*   在计算 I 的最大和之后，在任何索引 I 处，nums[i]现在将存储从结束于 I 的子序列中可以获得的最大可能和。
*   要计算每个索引 I 的最大可能和，请检查从它之前的大小为 K 的窗口中可以获得的最大值。如果最大值为负值，请使用零。
*   为了最佳地使用计算出的和的值，我们使用一个 deque 来按照和的递增顺序存储和以及它们的索引。当元素的索引超出当前索引的窗口 k 时，我们也从后面弹出元素

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find the maximum sum
// subsequence under given constraint
#include <bits/stdc++.h>
using namespace std;

// Function return the maximum sum
int ConstrainedSubsetSum(vector<int>& nums,
                         int k)
{
    deque<pair<int, int> > d;

    // Iterating the given array
    for (int i = 0; i < nums.size(); i++)
    {
        // Check if deque is empty
        nums[i] += d.size()
            ? max(d.back().first, 0) : 0;

        while (d.size() &&
               d.front().first < nums[i])
            d.pop_front();

        d.push_front({ nums[i], i });

        if (d.back().second == i - k)
            d.pop_back();
    }

    int ans = nums[0];

    for (auto x : nums)
        ans = max(ans, x);

    return ans;
}

// Driver code
int main()
{
    vector<int> nums = { 10, -2, -10,
                        -5, 20 };
    int K = 2;

    // Function call
    cout << ConstrainedSubsetSum(nums, K)
        << endl;
    return 0;
}
```

**Output:** 

```
23
```

**时间复杂度:**O(N)
T3】空间复杂度: O(K)