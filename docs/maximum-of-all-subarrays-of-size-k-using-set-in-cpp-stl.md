# 使用 C++ STL 中设置的 k 大小的所有子阵列的最大值

> 原文:[https://www . geeksforgeeks . org/最大尺寸 k 子阵列使用 cpp-stl 中的集合/](https://www.geeksforgeeks.org/maximum-of-all-subarrays-of-size-k-using-set-in-cpp-stl/)

给定一个大小为 **N** 的数组和一个整数 **K** ，任务是为每个大小为 **K** 的连续子数组找到最大值，并最终打印所有这些值的总和。

**示例:**

> **输入:** arr[] = {4，10，54，11，8，7，9}，K = 3
> **输出:** 182
> 
> **输入:** arr[] = {1，2，3，4，1，6，7，8，2，1}，K = 4
> **输出:** 45

**先决条件**:

*   [滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)
*   [在 C++ STL 中设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)

**方法:**
Set 在 **O(logK)** 时间执行插入和移除操作，并且总是以排序的顺序存储键。
想法是使用一组[对](https://www.geeksforgeeks.org/sets-of-pairs-in-c/)，其中对中的第一项是元素本身，对中的第二项包含元素的数组索引。

1.  选取前 k 个元素，用这些元素及其索引创建一组[对](https://www.geeksforgeeks.org/sets-of-pairs-in-c/)，如上所述。
2.  现在，设置 **sum = 0** 并使用[窗口滑动技术](https://www.geeksforgeeks.org/window-sliding-technique/)并从 **j = 0** 循环至**n–k**:
    *   获取当前窗口集合(最后一个元素)中的最大元素，更新 **sum = sum + currMax** 。
    *   在集合中搜索当前窗口最左边的元素并删除它。
    *   在集合中插入当前窗口的下一个元素，以移动到下一个窗口。

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of maximum of
// all k size sub-arrays using set in C++ STL
int maxOfSubarrays(int arr[], int n, int k)
{
    // Create a set of pairs
    set<pair<int, int> > q;

    // Create a reverse iterator to the set
    set<pair<int, int> >::reverse_iterator it;

    // Insert the first k elements along
    // with their indices into the set
    for (int i = 0; i < k; i++) {
        q.insert(pair<int, int>(arr[i], i));
    }

    // To store the sum
    int sum = 0;
    for (int j = 0; j < n - k + 1; j++) {

        // Iterator to the end of the
        // set since it has the maximum value
        it = q.rbegin();

        // Add the maximum element
        // of the current window
        sum += it->first;

        // Delete arr[j] (Leftmost element of
        // current window) from the set
        q.erase(pair<int, int>(arr[j], j));

        // Insert next element
        q.insert(pair<int, int>(arr[j + k], j + k));
    }

    // Return the required sum
    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 4, 10, 54, 11, 8, 7, 9 };

    int K = 3;

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxOfSubarrays(arr, n, K);

    return 0;
}
```

**Output:**

```
182

```

时间复杂度:O(n Log n)
辅助空间:O(k)

上述问题可以在 O(n)时间内解决。请参见以下基于出列的解决方案。
[滑动窗口最大值(k 大小所有子阵列的最大值)](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/)