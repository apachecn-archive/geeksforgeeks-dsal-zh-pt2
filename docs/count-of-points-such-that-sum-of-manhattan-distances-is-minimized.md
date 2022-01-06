# 点的计数，使得曼哈顿距离的总和最小化

> 原文:[https://www . geeksforgeeks . org/点数如此之少，以至于曼哈顿距离之和被最小化/](https://www.geeksforgeeks.org/count-of-points-such-that-sum-of-manhattan-distances-is-minimized/)

给定 2D 数组中 **K** 维空间中的 **N** 点**点【】【】**，其中**1≤N≤10<sup>5</sup>T9】和 **1 ≤ K ≤ 5** 。任务是确定点的**数量**(具有整数坐标)，使得从这些点到 **N** 点的**曼哈顿距离**的**和**最小化**。

> **曼哈顿距离**是沿**直角**处的轴测量的两点之间的**距离**的总和。在 **p1** 在 **(x1，y1)** 而 **p2** 在 **(x2，y2)** 的平面上，是**| x1–x2 |+| y1–y2 |**。

**示例:**

> **输入:** N = 3，K = 3，
> 点数= { {1，1，1}，
> {2，2，2}，
> {3，3，3} }
> **输出:** 1
> **解释**:从{2，2，2}开始，曼哈顿到其他 2 个点的距离之和最小
> 
> **输入:** N = 4，K = 4，
> 点数= { {1，6，9，6}，
> {5，2，5，7}，
> {2，0，1，5}，
> {4，6，3，9} }
> **输出:** 90

**进场:**进场基于 [**排序**](http://www.geeksforgeeks.org/sorting-algorithms/) 。为了最小化曼哈顿距离，只需对所有**【K】**维度中的点进行排序，并按照给定的点数进行。按照以下步骤解决问题:

*   **情况-1** 当 **N** 为**奇数**时:可根据以下观察解决
    *   这种最佳点的数量将始终为 **1** ，因为在所有 **K** 维度中对它们进行排序后，将只有一个**中值点，在该点处曼哈顿距离之和将达到最小值。**

> 例如:考虑表达式|x-3| + |x-5| + |x-8|。这仅在单个点 x = 5 时达到最小值。

*   **案例-2** 当 **N** 为**甚至**时:以下观察有助于解决问题。
    *   根据一个维度对点进行排序。
    *   每个维度将有 **2** 个中间指数，即 **(N/2)-1** 和 **(N/2)** 。
        *   范围**【点[(N/2) -1]、点[N/2]】**中的所有数字将作为**中间值**，在此处曼哈顿距离之和将达到最小值。
        *   因此，该尺寸的中间坐标总数将为**点[(N/2)]–点[(N/2)-1]+1** 。
    *   同样，在该维度的基础上对数字进行排序后，找出所有维度中的中值坐标数，它们的乘积将形成 **K** 维空间中此类最优点的总数。

> 例如:考虑表达式|x-3| + |x-5| + |x-8| + |x-10|。对于[5，8]范围内的所有 x，这将达到最小值。所以会有(8-5)+1 = 4 个这样的 x。同样，对所有的 K 维求。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required number
// of points which minimizes the sum 
// of Manhattan distances
int NumberOfPointsWithMinDistance(
    int n, int k, vector<vector<int> >& point)
{
    // Sorting points in all k dimension
    for (int i = 0; i < k; ++i)
        sort(point[i].begin(), point[i].end());

    // When n is odd
    if (n % 2 == 1) {
        return 1;
    }

    // When n is even
    int ans = 1;
    for (int i = 0; i < k; ++i) {

        int possible_points
            = point[i][n / 2] - 
            point[i][(n / 2) - 1] + 1;
        ans = ans * possible_points;
    }
    return ans;
}

int main()
{
    int N = 4, K = 4;
    vector<vector<int> > 
        Points = { { 1, 5, 2, 4 },
                   { 6, 2, 0, 6 },
                   { 9, 5, 1, 3 },
                   { 6, 7, 5, 9 } };

    cout << NumberOfPointsWithMinDistance(N, K, Points);
    return 0;
}
```

**Output**

```
90
```

***时间复杂度*****:**O(K * N * log(N))
***辅助空间*** : O(1)