# 数组中滑动窗口的中间值|集合 2

> 原文:[https://www . geesforgeks . org/数组集滑动窗口中位数-2/](https://www.geeksforgeeks.org/median-of-sliding-window-in-an-array-set-2/)

**先决条件:** [基于策略的数据结构](https://www.geeksforgeeks.org/policy-based-data-structures-g/)[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)。
给定整数**arr【】**和整数 **K** 的数组，任务是从左边开始，每次向右移动一个位置，找到每个大小为 **K** 的窗口的中间值。
**举例:**

> **输入:** arr[] = {-1，5，13，8，2，3，1}，K = 3
> **输出:** 5 8 8 3 3 3
> **解释:**
> 第一窗口:{-1，5，13}中位数= 5
> 第二窗口:{5，13，8}中位数= 8
> 第三窗口:{13，8，2}中位数= 8
> 第四窗口:{8，2，3}中位数 1}中位数= 3
> **输入:** arr[] = {-1，5，13，8，2，3，3，1}，K = 4
> **输出:** 6.5 6.5 5.5 3.0 2.5

**天真方法:**
解决问题最简单的方法就是遍历每一个大小为 **K** 的窗口，对窗口的元素进行排序，找到中间的元素。打印每个窗口的中间元素作为中间值。
***时间复杂度:**O(N * KlogK)*
***辅助空间:** O(K)*
**排序集方法:**参考[数组中滑动窗口的中值](https://www.geeksforgeeks.org/median-of-sliding-window-in-an-array/)使用[排序集](https://www.geeksforgeeks.org/sortedset-java-examples/)解决问题。
**有序集方法:**
在本文中，一种使用基于策略的[有序集](https://www.geeksforgeeks.org/ordered-set-gnu-c-pbds/)数据结构来解决问题的方法。
按照以下步骤解决问题:

1.  在有序集合中插入第一个大小为 **K** 的窗口(保持排序顺序)。因此，这个有序集合的中间元素是相应窗口的所需中值。

2.  中间元素可以通过 **O(logN)** 计算复杂度中的 find_by_order()方法得到。
3.  通过移除前一个窗口的第一个元素并插入新元素，进入下一个窗口。要从集合中移除任何元素，使用 **order_by_key()** 找到元素在**order _ Set**中的顺序，这将导致 0(LogN)的计算复杂度，并且**通过使用 **find_by_order()** 方法在 order _ Set 中搜索其获得的顺序来擦除()**该元素。现在为新窗口添加新元素。

4.  对每个窗口重复上述步骤，并打印各自的中间值。

下面是上述方法的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ Program to implement the
// above approach
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>

using namespace std;
using namespace __gnu_pbds;

// Policy based data structure
typedef tree<int, null_type,
             less_equal<int>, rb_tree_tag,
             tree_order_statistics_node_update>
    Ordered_set;

// Function to find and return the
// median of every window of size k
void findMedian(int arr[], int n,
                int k)
{

    Ordered_set s;

    for (int i = 0; i < k; i++)
        s.insert(arr[i]);

    if (k & 1) {

        // Value at index k/2
        // in sorted list.
        int ans = *s.find_by_order(k / 2);

        cout << ans << " ";

        for (int i = 0; i < n - k; i++) {

            // Erasing Element out of window.
            s.erase(s.find_by_order(
                s.order_of_key(
                    arr[i])));

            // Inserting newer element
            // to the window
            s.insert(arr[i + k]);

            // Value at index k/2 in
            // sorted list.
            ans = *s.find_by_order(k / 2);

            cout << ans << " ";
        }
        cout << endl;
    }
    else {

        // Getting the two middle
        // median of sorted list.
        float ans = ((float)*s.find_by_order(
                         (k + 1) / 2 - 1)
                     + (float)*s.find_by_order(k
                                               / 2))
                    / 2;

        printf("%.2f ", ans);

        for (int i = 0; i < n - k; i++) {
            s.erase(s.find_by_order(
                s.order_of_key(arr[i])));

            s.insert(arr[i + k]);

            ans = ((float)*s.find_by_order(
                       (k + 1) / 2 - 1)
                   + (float)*s.find_by_order(k
                                             / 2))
                  / 2;

            printf("%.2f ", ans);
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    int arr[] = { -1, 5, 13, 8, 2,
                  3, 3, 1 };
    int k = 3;

    int n = sizeof(arr)
            / sizeof(arr[0]);
    findMedian(arr, n, k);

    return 0;
}
```

**Output:** 

```
5 8 8 3 3 3
```

***时间复杂度:** O(NlogK)*
***辅助空间:** O(K)*