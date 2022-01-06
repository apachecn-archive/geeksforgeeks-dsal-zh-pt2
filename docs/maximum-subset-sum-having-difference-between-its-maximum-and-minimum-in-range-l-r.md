# 最大子集和，其最大值和最小值之差在[L，R]

范围内

> 原文:[https://www . geeksforgeeks . org/最大子集和与其最大和最小范围差-l-r/](https://www.geeksforgeeks.org/maximum-subset-sum-having-difference-between-its-maximum-and-minimum-in-range-l-r/)

给定正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和范围**【L，R】**，任务是找到最大子集和，使得子集的最大和最小元素之间的差位于给定的范围内。

**示例:**

> **输入:** arr[] = {6，5，0，9，1}，L = 0，R = 3
> **输出:** 15
> **解释:**给定数组的子集{6，9}的最大和最小元素之差为 3，位于给定范围[0，3]内，元素之和为 15，这是最大可能值。
> 
> **输入:** arr[] = {5，10，15，20，25}，L = 1，R = 2
> **输出:** 0
> **说明:**不存在有效子集。

**方法:**给定的问题可以在[整理给定的数组](https://www.geeksforgeeks.org/sorting-algorithms/)后，借助一个[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来解决。以下是要遵循的步骤:

*   [按非递减顺序对给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序。
*   使用这里[讨论的算法](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)创建前缀和数组**和[]** 。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，获取 **i** 在**【0，N)** 范围内的所有值。
*   对于每个 **i** ，找到最大整数的索引 **j** ，使得**arr【j】<= arr【I】+R**。这可以使用[上限函数](https://www.geeksforgeeks.org/upper_bound-in-cpp/)来完成。
*   维护一个变量**和**，它存储最大子集和。最初， **ans = 0** 。
*   如果子阵列**arr【I，j】**形成有效子集，将 **ans** 的值更新为 **ans** 和子阵列**arr【I，j】**之和的最大值。
*   存储在**和**中的值是必需的答案。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find Maximum Subset Sum such
// that the difference between maximum and
// minimum elements lies in the range [L, R]
int maxSubsetSum(vector<int> arr, int L, int R)
{
    int N = arr.size();

    // Sort the given array arr[] in
    // non-decreasing order
    sort(arr.begin(), arr.end());

    // Stores the sum of elements till
    // current index of the array arr[]
    int sum[N + 1] = {};

    // Stores the Maximum subset sum
    int ans = 0;

    // Create prefix sum array
    for (int i = 1; i <= N; i++) {
        sum[i] = sum[i - 1] + arr[i - 1];
    }

    // Iterate over all indices of array
    for (int i = 0; i < N; i++) {

        // Maximum possible value of
        // subset considering arr[i]
        // as the minimum element
        int val = arr[i] + R;

        // Calculate the position of the
        // largest element <= val
        auto ptr = upper_bound(
            arr.begin(), arr.end(), val);
        ptr--;
        int j = ptr - arr.begin();

        // If the difference between the
        // maximum and the minimum lies in
        // the range, update answer
        if ((arr[j] - arr[i] <= R)
            && (arr[j] - arr[i] >= L)) {
            ans = max(ans, sum[j + 1] - sum[i]);
        }
    }

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    vector<int> arr{ 6, 5, 0, 9, 1 };
    int L = 0;
    int R = 3;
    cout << maxSubsetSum(arr, L, R);

    return 0;
}
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach
        function InsertionIndex(nums, target, left)
        {
            let low = 0,
                high = nums.length

            while (low < high) {
                const mid = low + Math.floor((high - low) / 2)

                if (nums[mid] > target || (left && target === nums[mid]))
                    high = mid
                else
                    low = mid + 1
            }

            return low
        }
        function upper_bound(nums, target) {
            const targetRange = [-1, -1]

            const leftIdx = InsertionIndex(nums, target, true)

            if (leftIdx === nums.length || nums[leftIdx] != target)
                return targetRange

            targetRange[0] = leftIdx
            targetRange[1] = InsertionIndex(nums, target, false) - 1

            return targetRange

        }
        function maxSubsetSum(arr, L, R) {
            let N = arr.length;

            // Sort the given array arr[] in
            // non-decreasing order
            arr.sort(function (a, b) { return a - b })

            // Stores the sum of elements till
            // current index of the array arr[]
            let sum = new Array(N + 1).fill(0);

            // Stores the Maximum subset sum
            let ans = 0;

            // Create prefix sum array
            for (let i = 1; i <= N; i++) {
                sum[i] = sum[i - 1] + arr[i - 1];
            }

            // Iterate over all indices of array
            for (let i = 0; i < N; i++) {

                // Maximum possible value of
                // subset considering arr[i]
                // as the minimum element
                let val = arr[i] + R;

                // Calculate the position of the
                // largest element <= val
                let ptr = upper_bound(
                    arr, val);
                let j = ptr[1]

                // If the difference between the
                // maximum and the minimum lies in
                // the range, update answer
                if ((arr[j] - arr[i] <= R)
                    && (arr[j] - arr[i] >= L)) {
                    ans = Math.max(ans, sum[j + 1] - sum[i]);
                }
            }

            // Return Answer
            return ans;
        }

        // Driver Code
        let arr = [6, 5, 0, 9, 1];
        let L = 0;
        let R = 3;
        document.write(maxSubsetSum(arr, L, R));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
15
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*