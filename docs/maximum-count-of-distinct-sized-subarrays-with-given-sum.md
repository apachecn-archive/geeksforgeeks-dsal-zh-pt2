# 给定和的不同大小子阵列的最大计数

> 原文:[https://www . geeksforgeeks . org/具有给定总和的不同大小子阵列的最大计数/](https://www.geeksforgeeks.org/maximum-count-of-distinct-sized-subarrays-with-given-sum/)

给定二进制[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**的 **N** 整数，任务是找到不同大小的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最大计数，使得每个子阵列的和为 **K** 。

**示例:**

> **输入:** arr[] = {0，1，1，0}，K = 2
> **输出:** 3
> **解释:**子集{{0，1，1，0}，{0，1，1}，{1，1}}是 3 个子阵列的子集，使得每个子阵列的和为 2，并且每个子阵列的大小不同。子阵列{1，1，0}也有 sum 2，但已经包括了大小为 3 的子阵列。
> 
> **输入:** arr[] = {0，1，0，0，0，1，0}，K = 1
> **输出:** 5

**方法:**给定的问题可以借助[滑动窗口算法](https://www.geeksforgeeks.org/window-sliding-technique/)来解决。可以观察到一个[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的和等于子阵中 **1 的**个数。以下是要遵循的步骤:

*   维护一个跟踪当前窗口中 **1 的**的计数的变量。
*   如果当前窗口中 **1 的**计数小于 **K** ，则增大窗口大小，同样如果 **1 的**计数大于 **K** ，则减小窗口大小。
*   对于 **K** 相加的窗口，将其大小插入[设置数据结构](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。
*   遍历整个数组后，集合中元素的数量就是所需的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find size of the largest
// subset of subarrays having given sum
// and size of each subarray is distinct
int maxSubsetSize(int arr[], int N, int K)
{
    // Stores starting index
    // of the current window
    int ptr = 0;

    // Stores distinct subarray
    // sizes of the subset
    unordered_set<int> s;

    // Stores the sum of
    // current window
    int curSum = 0;

    // Loop to traverse over array
    for (int i = 0; i < N; i++) {

        // Update current window sum
        curSum += arr[i];

        // If sum is less that K
        if (curSum < K) {
            continue;
        }

        // If sum is more than K
        if (curSum > K) {

            // Decrease window size
            while (curSum > K) {
                curSum -= arr[ptr++];
            }
        }

        if (curSum == K) {

            // Insert size of the
            // current window
            s.insert(i - ptr + 1);
            int t = ptr;

            // Iterate over all windows
            // with same sum
            while (arr[t] == 0) {
                s.insert(i - t);
                t++;
            }
        }
    }

    // Return Answer
    return s.size();
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 1, 0 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    cout << maxSubsetSize(arr, N, K);

    return 0;
}
```

**Output**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)