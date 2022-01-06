# 最小乘积子序列，其中相邻元素之间的最大距离为 K

> 原文:[https://www . geeksforgeeks . org/最小乘积子序列-其中相邻元素被 k 的最大距离隔开/](https://www.geeksforgeeks.org/minimal-product-subsequence-where-adjacent-elements-are-separated-by-a-maximum-distance-of-k/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是找出子序列的最小乘积，其中子序列的相邻元素之间的最大距离为 K。
**注:**子序列应该包括数组的第一个和最后一个元素。

**示例:**

> **输入:** arr[] = { 1，2，3，4 }，K = 2
> **输出:** 8
> 子序列中的第一个元素是 1。从 1 开始，我们可以移到 2 或 3(因为 K = 2)。我们可以移到 3，然后移到 4，得到 12 的乘积。不过**我们也可以先移到 2 再移到 4** 才有 8 的乘积。最小乘积子序列= { 1，2，4 }
> **输入:** arr[] = { 2，3 }，K = 2
> **输出:** 6

**朴素方法:**朴素方法是生成数组的所有子序列，并保持相邻元素之间的索引差异，找到最小乘积子序列。
**高效方法:**高效方法是使用**动态编程**。让 **dp[i]** 表示元素**到包括 arr[i]** 在内的索引“I”的最小乘积，它们之间相隔最大距离 **K** 。那么 dp[i]可以表述如下:

```
dp[i] = arr[i] * min{dp[j]} where j < i and 1 <= i - j <= K.
```

为了计算 **dp[i]** ，可以保持并遍历大小为 **K** 的窗口，以找到 **dp[j]** 的最小值，然后可以将该最小值**乘以 arr[i]** 。然而，这将导致一个 **O(N*K)** 解决方案。
为了进一步优化解决方案，可以将产品的值存储在 STL 集中，然后在 **O(log n)** 时间内找出产品的最小值。由于存储产品可能是一项麻烦的任务，因为产品很容易超过 10 <sup>18</sup> ，因此我们将存储产品的日志值，因为日志是一个单调函数，日志值的最小化将自动意味着产品的最小化。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the above approach.
#include <bits/stdc++.h>

#define mp make_pair
#define ll long long
using namespace std;

const int mod = 1000000007;
const int MAX = 100005;

// Function to get the minimum product of subsequence such that
// adjacent elements are separated by a max distance of K
int minimumProductSubsequence(int* arr, int n, int k)
{
    multiset<pair<double, int> > s;

    ll dp[MAX];
    double p[MAX];

    dp[0] = arr[0];
    p[0] = log(arr[0]);

    // multiset will hold pairs
    // pair = (log value of product, dp[j] value)
    // dp[j] = minimum product % mod
    // multiset will be sorted according to log values
    // Therefore, corresponding to the minimum log value
    // dp[j] value can be obtained.
    s.insert(mp(p[0], dp[0]));

    // For the first k-sized window.
    for (int i = 1; i < k; i++) {

        double l = (s.begin())->first;
        ll min = (s.begin())->second;

        // Update log value by adding previous
        // minimum log value
        p[i] = log(arr[i]) + l;
        // Update dp[i]
        dp[i] = (arr[i] * min) % mod;

        // Insert it again into the multiset
        // since it is within the k-size window
        s.insert(mp(p[i], dp[i]));
    }

    for (int i = k; i < n; i++) {

        double l = (s.begin())->first;
        ll min = (s.begin())->second;

        p[i] = log(arr[i]) + l;
        dp[i] = (arr[i] * min) % mod;

        // Eliminate previous value which falls out
        // of the k-sized window
        multiset<pair<double, int> >::iterator it;
        it = s.find(mp(p[i - k], dp[i - k]));
        s.erase(it);

        // Insert newest value to enter in
        // the k-sized window.
        s.insert(mp(p[i], dp[i]));
    }

    // dp[n - 1] will have minimum product %
    // mod such that adjacent elements are
    // separated by a max distance K
    return dp[n - 1];
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;

    cout << minimumProductSubsequence(arr, n, k);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach.
import math

mod = 1000000007;
MAX = 100005;

# Function to get the minimum product of subsequence such that
# adjacent elements are separated by a max distance of K
def minimumProductSubsequence(arr, n, k):

    s = []

    dp = [0 for i in range(MAX)];
    p = [0.0 for i in range(MAX)];

    dp[0] = arr[0];
    p[0] = math.log(arr[0]);

    # multiset will hold pairs
    # pair = (log value of product, dp[j] value)
    # dp[j] = minimum product % mod
    # multiset will be sorted according to log values
    # Therefore, corresponding to the minimum log value
    # dp[j] value can be obtained.
    s.append([p[0], dp[0]]);
    s.sort()

    # For the first k-sized window.
    for i in range(1, k):

        l = s[0][0]
        min = s[0][1]

        # Update log value by adding previous
        # minimum log value
        p[i] = math.log(arr[i]) + l;

        # Update dp[i]
        dp[i] = (arr[i] * min) % mod;

        # Insert it again into the multiset
        # since it is within the k-size window
        s.append([p[i], dp[i]]);
        s.sort()

    for i in range(k, n):

        l = s[0][0]
        min = s[0][1]

        p[i] = math.log(arr[i]) + l;
        dp[i] = (arr[i] * min) % mod;

        # Eliminate previous value which falls out
        # of the k-sized window
        if [p[i - k], dp[i - k]] in s:
            s.pop(s.index([p[i - k], dp[i - k]]))

        # Insert newest value to enter in
        # the k-sized window.
        s.append([p[i], dp[i]]);
        s.sort()

    # dp[n - 1] will have minimum product %
    # mod such that adjacent elements are
    # separated by a max distance K
    return dp[n - 1];

# Driver Code
if __name__=='__main__':

    arr = [ 1, 2, 3, 4 ]
    n = len(arr)

    k = 2;

    print(minimumProductSubsequence(arr, n, k))

# This code is contributed by rutvik_56
```

**Output**

```
8
```

**时间复杂度:** O(N* log(N))
**辅助空间:** O(N)