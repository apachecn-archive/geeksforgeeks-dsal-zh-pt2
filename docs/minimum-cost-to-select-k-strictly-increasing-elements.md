# 选择 K 个严格递增元素的最小成本

> 原文:[https://www . geesforgeks . org/最小选择成本-k-严格递增-元素/](https://www.geeksforgeeks.org/minimum-cost-to-select-k-strictly-increasing-elements/)

给定一个数组和一个整数 k，再给定一个数组，该数组存储从第一个数组中选择元素的成本。任务是计算从数组中选择 K 个严格递增元素的最小代价。
**例:**

```
Input: N = 4, K = 2
ele[] = {2, 6, 4, 8}
cost[] = {40, 20, 30, 10}
Output: 30
Explanation:
30 is the minimum cost by selecting elements 
6 and 8 from the array with cost 
10 + 20 respectively

Input: N = 11, K = 4
ele = {2, 6, 4, 8, 1, 3, 15, 9, 22, 16, 45}
cost = {40, 20, 30, 10, 50, 10, 20, 30, 40, 20, 10}
Output: 60
Explanation:
60 is the minimum cost by selecting elements 
3, 15, 16, 45 from the array with cost 
10 + 20 + 20 + 10 respectively
```

**方法:**
给定的问题可以使用动态规划方法轻松解决。由于问题要求增加元素，然后是最小成本，那么很明显，我们必须通过逐个选择或不选择元素来移动，并计算每个元素的最小成本。
现在，以存储我们的最小成本值的 3D DP 数组为例，其中缓存[i][prev][cnt]存储到目前为止考虑的第 I 个元素、prev 元素和数量计数的最小成本。
涉及 3 个基础条件:

*   如果计算了 k 个元素，返回 0。
*   如果遍历了数组的所有元素，返回 MAX_VALUE。
*   检查它是否已经在 dp 数组中计算过。

现在是选择第一个元素或不选择第一个元素的部分:

*   当不考虑 ith 元素时，ans = dp(i+1，prev，cnt，s，c)
*   当 ith 元素大于前一个元素时，检查添加其成本是否使总成本最小 ans = min(ans，c[i] + dp(i+1，I，cnt+1，s，c))

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

const int N = 1005;
const int K = 20;
int n, k;
int dp[N + 1][N + 1][K + 1];

// Function to calculate
// min cost to choose
// k increasing elements
int minCost(int i, int prev, int cnt,
                    int ele[], int cost[])
{
    // If k elements are
    // counted return 0
    if (cnt == k + 1) {
        return 0;
    }

    // If all elements
    // of array has been
    // traversed then
    // return MAX_VALUE
    if (i == n + 1) {
        return 1e5;
    }

    // To check if this is
    // already calculated
    int& ans = dp[i][prev][cnt];
    if (ans != -1) {
        return ans;
    }

    // When i'th elements
    // is not considered
    ans = minCost(i + 1, prev, cnt, ele, cost);

    // When the ith element
    // is greater than previous
    // element check if adding
    // its cost makes total cost minimum
    if (ele[i] > ele[prev]) {
        ans = min(ans, cost[i] + minCost(i + 1,
                           i, cnt + 1, ele, cost));
    }
    return ans;
}

// Driver code
int main()
{

    memset(dp, -1, sizeof(dp));
    n = 4;
    k = 2;

    int ele[n + 1] = { 0, 2, 6, 4, 8 };

    int cost[n + 1] = { 0, 40, 20, 30, 10 };

    int ans = minCost(1, 0, 1, ele, cost);

    if (ans == 1e5) {
        ans = -1;
    }

    cout << ans << endl;

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
N = 1005;
K = 20;

n = 0
k = 0

dp = [[[-1 for k in range(K + 1)] for j in range(N + 1)] for i in range(N + 1)]

# Function to calculate
# min cost to choose
# k increasing elements
def minCost(i, prev, cnt, ele, cost):

    # If k elements are
    # counted return 0
    if (cnt == k + 1):
        return 0;

    # If all elements
    # of array has been
    # traversed then
    # return MAX_VALUE
    if (i == n + 1):
        return 100000;

    # To check if this is
    # already calculated
    ans = dp[i][prev][cnt];

    if (ans != -1):
        return ans;

    # When i'th elements
    # is not considered
    ans = minCost(i + 1, prev, cnt, ele, cost);

    # When the ith element
    # is greater than previous
    # element check if adding
    # its cost makes total cost minimum
    if (ele[i] > ele[prev]):
        ans = min(ans, cost[i] + minCost(i + 1, i, cnt + 1, ele, cost));

    return ans;

# Driver code
if __name__=='__main__':

    n = 4;
    k = 2;

    ele = [ 0, 2, 6, 4, 8 ]

    cost = [ 0, 40, 20, 30, 10 ]

    ans = minCost(1, 0, 1, ele, cost);

    if (ans == 100000):
        ans = -1;

    print(ans)

# This code is contributed by rutvik_56
```

**Output:** 

```
30
```