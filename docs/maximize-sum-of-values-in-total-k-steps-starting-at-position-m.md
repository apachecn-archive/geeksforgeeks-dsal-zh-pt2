# 从位置 M

开始，最大化所有 K 步值的总和

> 原文:[https://www . geeksforgeeks . org/最大化总 k 步值总和-从位置 m 开始/](https://www.geeksforgeeks.org/maximize-sum-of-values-in-total-k-steps-starting-at-position-m/)

给定包含 **N** 对**【A，B】**的排序后的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，其中 **A** 是 **X 轴**上的位置， **B** 是该位置上的值。所有的位置都是不同的。数组按位置的递增顺序排序。
给定两个整数 **M** 和 **K** 。任务是从位置 **M** 开始，采取总 **K** 步骤，最大化可访问值的总和，其中:

*   走一步就可以向右或向左移动 **1** 位置(从 **x** 到 **x+1** 或 **x-1** )。
*   任何位置的值只能加到最终总和中一次。
*   沿着 **Y 轴**没有**运动。**

**示例:**

> **输入:** arr[][] = {{2，8}，{6，3}，{8，6}}，M = 5，K = 4
> **输出:** 9
> **说明:**最佳方式是:
> 向右移动到位置 6，加 3。机芯 1 位置。
> 向右移动到位置 8，添加 6。机芯 2 位置。
> 总运动 3 步，和= 3 + 6 = 9。
> 
> **输入:** arr[][] = {{1，7}，{3，6}，{4，5}，{6，5}}，M = 3，K = 4
> **输出:** 18
> **说明:**最佳移动方式为:
> 在位置 3 加值回答。
> 向右移动到位置 4，添加 5。
> 向左移动到位置 1，并添加 7。
> 总和= 6 + 5 + 7 = 18。
> 注意，位置 3 可以访问两次，但价值只增加一次。
> 
> **输入:** arr[][] = {{0，3}，{6，4}，{8，5}}，M = 3，K = 2
> **输出:** 0
> **说明:**移动最多可以 K = 2 个位置，不能到达任何有点的位置。

**进场:**进场基于 [**前缀和**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) 的概念。站在任何需要确定的位置上所能覆盖的范围，则可以从前缀和数组中计算出总点数。请遵循以下步骤:

*   找到最大可能位置的前缀和。之后，执行两个循环。
*   第一个循环是先向右，然后向左。
*   第二个循环将在首先向左移动，然后向右移动时发生。
*   所有可行范围内覆盖的最大种子数量是最终答案。

下面是上述方法的实现

## C++

```
// C++ code to implement above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum points 
// that can be collected
int maxTotalPoints(vector<vector<int> >& arr,
                   int M, int K)
{
    int MX = 2e5 + 2;
    int i, l, r, ans = 0;

    // Incremented positions by one
    // to make calculations easier.
    M++;
    vector<int> prefix_sum(MX);
    for (auto& it : arr)
        prefix_sum[it[0] + 1] = it[1];
    for (i = 1; i < MX; i++)
        prefix_sum[i] += prefix_sum[i - 1];

    for (r = M; r < MX && r <= M + K; r++) {
        l = min(M, M - (K - 2 * (r - M)));
        l = max(1, l);
        ans = max(ans, prefix_sum[r] - 
                  prefix_sum[l - 1]);
    }

    for (l = M; l > 0 && l >= M - K; l--) {
        r = max(M, M + (K - 2 * (M - l)));
        r = min(MX - 1, r);
        ans = max(ans, prefix_sum[r] - 
                  prefix_sum[l - 1]);
    }
    return ans;
}

// Driver code
int main()
{
    vector<vector<int>> arr{{2, 8}, {6, 3}, {8, 6}};
    int M = 5;
    int K = 4;
    cout<<maxTotalPoints(arr, M, K);
    return 0;
}
```

**Output**

```
9
```

***时间复杂度:*** O(X)，其中 X 为最大位置
***辅助空间:*** O(X)