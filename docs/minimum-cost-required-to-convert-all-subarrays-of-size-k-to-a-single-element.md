# 将大小为 K 的所有子阵列转换为单个元素所需的最小成本

> 原文:[https://www . geeksforgeeks . org/将 k 尺寸的所有子阵列转换为单个元素所需的最小成本/](https://www.geeksforgeeks.org/minimum-cost-required-to-convert-all-subarrays-of-size-k-to-a-single-element/)

**先决条件:** [滑动窗口中值](https://www.geeksforgeeks.org/median-of-sliding-window-in-an-array/)
给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到使长度为 **K** 的每个子数组的每个元素相等所需的最小成本。用另一个元素替换任何数组元素的成本是两者之间的绝对差异。
**举例:**

> **输入:** A[] = {1，2，3，4，6}，K = 3
> **输出:** 7
> **解释:**
> 子阵 1:将子阵{1，2，3}转换为{2，2，2}的成本= |1-2| + |2-2| + |3-2| = 2
> 子阵 2:将子阵{2，3，4}转换为{3，3，3}的成本= |2-3 4} = |3-4| + |4-4| + |6-4| = 3
> 最小成本= 2 + 2 + 3 = 7/
> **输入:** A[] = {2，3，4，4，1，7，6}，K = 4
> **输出:** 21

**方法:**
要找到将子阵列的每个元素转换为单个元素的最小成本，请将子阵列的每个元素更改为该子阵列的[中间值](https://www.geeksforgeeks.org/median/)。按照以下步骤解决问题:

*   为了有效地找到每个运行子阵列的**中间值**，使用[多集](https://www.geeksforgeeks.org/multiset-in-cpp-stl/)来获得每个子阵列中元素的排序顺序。中间将是这个**多集**的**中间元素**。
*   对于下一个子阵列，从多集合中移除前一个子阵列最左边的元素，将当前元素添加到多集合中。
*   保持指针**居中**以有效地跟踪多集的中间元素。
*   如果新添加的元素比先前的中间元素小**，则将**中间的**移动到其紧邻的较小元素。否则，将**中间的**移到紧接的下一个元素。**
*   **通过公式**| A[I]–中位数<sub>计算更换子阵列每个元素的成本 _ 子阵列</sub> |** 。**
*   **最后打印总成本。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// cost to convert each element of
// every subarray of size K equal
int minimumCost(vector<int> arr, int n,
                int k)
{
    // Stores the minimum cost
    int totalcost = 0;
    int i, j;

    // Stores the first K elements
    multiset<int> mp(arr.begin(),
                     arr.begin() + k);

    if (k == n) {

        // Obtain the middle element of
        // the multiset
        auto mid = next(mp.begin(),
                        n / 2 - ((k + 1) % 2));

        int z = *mid;

        // Calculate cost for the subarray
        for (i = 0; i < n; i++)
            totalcost += abs(z - arr[i]);

        // Return the total cost
        return totalcost;
    }
    else {

        // Obtain the middle element
        // in multiset
        auto mid = next(mp.begin(),
                        k / 2 - ((k + 1) % 2));

        for (i = k; i < n; i++) {

            int zz = *mid;
            int cost = 0;
            for (j = i - k; j < i; j++) {

                // Cost for the previous
                // k length subarray
                cost += abs(arr[j] - zz);
            }
            totalcost += cost;

            // Insert current element
            // into multiset
            mp.insert(arr[i]);

            if (arr[i] < *mid) {

                // New element appears
                // to the left of mid
                mid--;
            }

            if (arr[i - k] <= *mid) {

                // New element appears
                // to the right of mid
                mid++;
            }

            // Remove leftmost element
            // from the window
            mp.erase(mp.lower_bound(arr[i - k]));

            // For last element
            if (i == n - 1) {
                zz = *mid;
                cost = 0;

                for (j = i - k + 1;
                     j <= i; j++) {

                    // Calculate cost for the subarray
                    cost += abs(zz - arr[j]);
                }

                totalcost += cost;
            }
        }

        // Return the total cost
        return totalcost;
    }
}

// Driver Code
int main()
{
    int N = 5, K = 3;

    vector<int> A({ 1, 2, 3, 4, 6 });

    cout << minimumCost(A, N, K);
}
```

****Output:** 

```
7
```** 

*****时间复杂度:** O(NlogN)*
***辅助空间:** O(1)***