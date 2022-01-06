# 使用图

的大小为 K 的所有子阵列的最小值和最大值

> 原文:[https://www . geeksforgeeks . org/最小和最大 k 尺寸子阵列使用图/](https://www.geeksforgeeks.org/minimum-and-maximum-of-all-subarrays-of-size-k-using-map/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **K** ，任务是找到所有大小为 K 的子数组的最小值和最大值[。](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/)

**示例:**

> **输入:** arr[] = {2，-2，3，-9，-5，-8}，K = 4
> **输出:**
> -9 3
> -9 3
> -9 3
> **说明:**
> 下面是大小为 4 的子阵列以及每个子阵列的最小值和最大值:
> 1。{2，-2，3，-9}，minValue = -9，maxValue = 3
> 2。{-2，3，-9，-5}，minValue = -9，maxValue = 3
> 3。{3，-9，-5，-8}，minValue = -9，maxValue = 3
> 
> **输入:** arr[] = { 5，4，3，2，1，6，3，5，4，2，1 }，K = 3
> **输出:**
> 3 5
> 2 4
> 1 3
> 1 6
> 1 6
> 3 6
> 3 5
> 2 5
> 1 4

**进场:**

1.  [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)到 K 个元素，并将每个元素的[计数](https://www.geeksforgeeks.org/count-frequencies-elements-array-o1-extra-space-time/)存储到[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
2.  插入 K 个元素后，对剩余的每个元素执行以下操作:
    *   将电流元件**arr【I】**的频率增加 1。
    *   将**arr[I–K+1]**的频率降低 1，以存储大小为 **K** 的当前子阵列(**arr[I–K+1，i]** )的频率。
    *   因为 map 以排序顺序存储键值对。因此，在映射开始的迭代器存储最小元素，在映射结束的迭代器存储最大元素。打印当前子阵列的最小和最大元素。
3.  对形成的每个子阵列重复上述步骤。

下面是上述方法的实现:

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum and
// maximum element for each subarray
// of size K
int maxSubarray(int arr[], int n, int k)
{

    // To store the frequency of element
    // for every subarray
    map<int, int> Map;

    // To count the subarray array size
    // while traversing array
    int l = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Increment till we store the
        // frequency of first K element
        l++;

        // Update the count for current
        // element
        Map[arr[i]]++;

        // If subarray size is K, then
        // find the minimum and maximum
        // for each subarray
        if (l == k) {

            // Iterator points to end
            // of the Map
            auto itMax = Map.end();
            itMax--;

            // Iterator points to start of
            // the Map
            auto itMin = Map.begin();

            // Print the minimum and maximum
            // element of current sub-array
            cout << itMin->first << ' '
                 << itMax->first << endl;

            // Decrement the frequency of
            // arr[i - K + 1]
            Map[arr[i - k + 1]]--;

            // if arr[i - K + 1] is zero
            // remove from the map
            if (Map[arr[i - k + 1]] == 0) {
                Map.erase(arr[i - k + 1]);
            }

            l--;
        }
    }
    return 0;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 5, 4, 3, 2, 1, 6,
                  3, 5, 4, 2, 1 };

    // Subarray size
    int k = 3;

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maxSubarray(arr, n, k);
    return 0;
}
```

**Output:**

```
3 5
2 4
1 3
1 6
1 6
3 6
3 5
2 5
1 4

```

**时间复杂度:** *O(N*log K)* ，其中 N 为元素个数。
**辅助空间:** *O(K)* ，其中 K 为子阵大小。