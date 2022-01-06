# 最长子序列的长度，使得相邻元素的异或是非递减的

> 原文:[https://www . geeksforgeeks . org/最长子序列的长度使得相邻元素的异或不递减/](https://www.geeksforgeeks.org/length-of-the-longest-subsequence-such-that-xor-of-adjacent-elements-is-non-decreasing/)

给定一个正整数序列**arr****N**，任务是找到最长子序列的长度，使得子序列中相邻整数的异或必须为**非减**。

**示例:**

> **输入:** N = 8，arr = {1，100，3，64，0，5，2，15}
> **输出:** 6
> 最大长度的子序列为{1，3，0，5，2，15}
> ，相邻元素的 XOR 为{2，3，5，7，13}
> **输入:** N = 3，arr = {1，7，10}
> **输出**

**进场:**

*   这个问题可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来解决，其中**DP【I】**将存储在索引 **i** 处结束的最长有效子序列的长度。
*   首先，存储所有元素对，即 **arr[i] ^ arr[j]** 和对 **(i，j)** 的 xor，然后根据 xor 的值对它们进行排序，因为它们需要是非递减的。
*   现在，如果考虑对 **(i，j)** ，那么结束于 **j** 的最长子序列的长度将是 **max(dp[j]，1 + dp[i])** 。这样，计算每个位置的 **dp[]** 数组的最大可能值，然后取其中的最大值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the longest
// subsequence such that the XOR of adjacent
// elements in the subsequence must
// be non-decreasing
int LongestXorSubsequence(int arr[], int n)
{

    vector<pair<int, pair<int, int> > > v;

    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // Computing xor of all the pairs
            // of elements and store them
            // along with the pair (i, j)
            v.push_back(make_pair(arr[i] ^ arr[j],
                                  make_pair(i, j)));
        }
    }

    // Sort all possible xor values
    sort(v.begin(), v.end());

    int dp[n];

    // Initialize the dp array
    for (int i = 0; i < n; i++) {
        dp[i] = 1;
    }

    // Calculating the dp array
    // for each possible position
    // and calculating the max length
    // that ends at a particular index
    for (auto i : v) {
        dp[i.second.second]
            = max(dp[i.second.second],
                  1 + dp[i.second.first]);
    }

    int ans = 1;

    // Taking maximum of all position
    for (int i = 0; i < n; i++)
        ans = max(ans, dp[i]);

    return ans;
}

// Driver code
int main()
{

    int arr[] = { 2, 12, 6, 7, 13, 14, 8, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << LongestXorSubsequence(arr, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the length of the longest
# subsequence such that the XOR of adjacent
# elements in the subsequence must
# be non-decreasing
def LongestXorSubsequence(arr, n):

    v = []

    for i in range(0, n):
        for j in range(i + 1, n):

             # Computing xor of all the pairs
            # of elements and store them
            # along with the pair (i, j)
            v.append([(arr[i] ^ arr[j]), (i, j)])

        # v.push_back(make_pair(arr[i] ^ arr[j], make_pair(i, j)))

    # Sort all possible xor values
    v.sort()

    # Initialize the dp array
    dp = [1 for x in range(88)]

    # Calculating the dp array
    # for each possible position
    # and calculating the max length
    # that ends at a particular index
    for a, b in v:
        dp[b[1]] = max(dp[b[1]], 1 + dp[b[0]])

    ans = 1

    # Taking maximum of all position
    for i in range(0, n):
        ans = max(ans, dp[i])

    return ans

# Driver code
arr = [ 2, 12, 6, 7, 13, 14, 8, 6 ]
n = len(arr)
print(LongestXorSubsequence(arr, n))

# This code is contributed by Sanjit Prasad
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to find the length of the longest
// subsequence such that the XOR of adjacent
// elements in the subsequence must
// be non-decreasing
function LongestXorSubsequence(arr, n) {

    let v = [];

    for (let i = 0; i < n; i++) {
        for (let j = i + 1; j < n; j++) {

            // Computing xor of all the pairs
            // of elements and store them
            // along with the pair (i, j)
            v.push([arr[i] ^ arr[j], [i, j]]);
        }
    }

    // Sort all possible xor values
    v.sort((a, b) => a[0] - b[0]);

    let dp = new Array(n);

    // Initialize the dp array
    for (let i = 0; i < n; i++) {
        dp[i] = 1;
    }

    // Calculating the dp array
    // for each possible position
    // and calculating the max length
    // that ends at a particular index
    for (let i of v) {
        dp[i[1][1]]
            = Math.max(dp[i[1][1]],
                1 + dp[i[1][0]]);
    }

    let ans = 1;

    // Taking maximum of all position
    for (let i = 0; i < n; i++)
        ans = Math.max(ans, dp[i]);

    return ans;
}

// Driver code
let arr = [2, 12, 6, 7, 13, 14, 8, 6];
let n = arr.length;

document.write(LongestXorSubsequence(arr, n));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
5
```

**时间复杂度:**O(N * N)
T3】辅助空间: O(N)