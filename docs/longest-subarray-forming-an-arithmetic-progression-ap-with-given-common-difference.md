# 形成具有给定公共差的算术级数的最长子阵列

> 原文:[https://www . geeksforgeeks . org/最长子数组-形成算术级数-带给定公差的 AP/](https://www.geeksforgeeks.org/longest-subarray-forming-an-arithmetic-progression-ap-with-given-common-difference/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找出最长的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度，该子数组形成一个具有共同差异 **K** 的[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)。

**示例:**

> ***输入:** arr[] = {3，4，5}，K = 1*
> ***输出:** 3*
> ***解释:**形成具有共同差异 1 的 AP 的最长子阵列是{3，4，5}。*
> 
> ***输入:** arr[] = {10，7，4，6，8，10，11}，K = 2*
> ***输出:** 4*
> ***解释:**形成与 2 相同差异的 AP 的最长可能子阵列是{4，6，8，10}。*

**方法:**给定的问题是基于实现的问题，可以使用[滑动窗口技术](http://www.geeksforgeeks.org/window-sliding-technique/)来解决。按照下面提到的步骤解决问题:

*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并维护一个存储当前窗口中变量数量的变量。
*   如果当前元素与数组中前一个元素的差值为 **K** ，则增加当前窗口的大小，否则，将窗口大小重置为 **1** 。
*   将最大差异打印为答案。

下面是上述方法的实现:

## C++14

```
// C++ program of the above appraoch
#include <bits/stdc++.h>
using namespace std;

// Function to find longest subarray
// forming an Arithmetic Progression
// with the given common difference
int maxlenAP(int arr[], int& n, int& d)
{
    // Stores the length of
    // the current window
    int count = 1;

    // Stores final answer
    int maxLen = INT_MIN;

    // Loop to traverse array
    for (int i = 1; i < n; i++) {
        if (arr[i] - arr[i - 1] == d)

            // Increment window size
            count++;
        else

            // Reset window size
            count = 1;

        // Update answer
        maxLen = max(maxLen, count);
    }

    // Return Answer
    return maxLen;
}

// Driver Code
int main()
{
    int arr[] = { 10, 7, 4, 6, 8, 10, 11 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    cout << maxlenAP(arr, N, K);

    return 0;
}
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)