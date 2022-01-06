# 由所有最大出现元素的所有出现组成的最小子阵列的长度

> 原文:[https://www . geesforgeks . org/最小子数组长度-由所有最大出现元素的所有出现次数组成/](https://www.geeksforgeeks.org/length-of-smallest-subarray-consisting-of-all-occurrences-of-all-maximum-occurring-elements/)

给定一个大小为 **N** 的数组**arr【】**，任务是找出由**最大**出现元素
**的所有**出现**组成的**最小**T6】子数组的长度示例:**

> **输入:** arr[] = {1，2，1，3，2}
> **输出:** 5
> **说明:**最大频率(=2)的元素为 1 & 2。
> 因此，由 1 和 2 的所有出现组成的最小子阵列的长度是 5，即{1，2，1，3，2}
> 
> **输入:** arr[] = {1，2，5，1，5，5}
> **输出:** 4

**方法:**可以通过跟踪**第一个**&**最后一个**出现的**最大**出现元素来解决任务。**最小**子阵列的长度将是最后一个**事件的**最大**和第一个**事件的**最小**之间的**差。
按照以下步骤解决问题:******

*   创建一个**图**，存储元素的**频率**
*   找到**最大**频率的元素，存储它们的**第一个**和**最后一个**事件。
*   最后，返回最后一次出现的**的**最大值**和第一次出现的**的**最小值**之间的**差值******

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of smallest
// subarray consisting of all the occurrences
// of maximum occurring elements
int get(int arr[], int n)
{
    // Stores the frequencies
    unordered_map<int, int> occ;

    // Stores the maximum frequency
    int mx = -1;

    for (int i = 0; i < n; i++) {
        occ[arr[i]]++;
        mx = max(mx, occ[arr[i]]);
    }

    // Stores the maximum occurring elements
    unordered_map<int, int> chk;

    for (auto x : occ) {
        if (x.second == mx)
            chk[x.first]++;
    }

    // Stores the minimum of first occurrences
    // and maximum of last occurrences
    // of all the maximum occcurring elements
    int fr = INT_MAX, sc = INT_MIN;

    for (int i = 0; i < n; i++) {

        // Maximum occcurring element
        if (chk.find(arr[i]) != chk.end()) {
            fr = min(fr, i);
            sc = max(sc, i);
        }
    }

    return sc - fr + 1;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 5, 1, 5, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << get(arr, n);
    return 0;
}
```

**Output**

```
4
```

***时间复杂度*** : O(N)
***辅助空间*** **:** O(N)