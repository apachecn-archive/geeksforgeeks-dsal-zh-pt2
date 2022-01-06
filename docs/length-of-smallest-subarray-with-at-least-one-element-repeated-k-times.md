# 至少有一个元素重复 K 次的最小子阵列长度

> 原文:[https://www . geeksforgeeks . org/至少有一个元素重复 k 次的最小子数组长度/](https://www.geeksforgeeks.org/length-of-smallest-subarray-with-at-least-one-element-repeated-k-times/)

给定长度为 **N** 和整数 **K** 的数组 **arr[]** 。任务是找到子阵列的最小长度，使得子阵列的至少一个元素在该子阵列中精确地重复****K**次。如果没有这样的子阵列，打印 **-1** 。**

****示例:****

> ****输入:** arr[] = {1，2，1，2，1}，K = 2
> **输出:** 3
> **解释:** Subarray [1，2，1]，有 K = 2 次出现 1**
> 
> ****输入:** arr[] = {2，2，2，3，4}，K = 3
> T3】输出: 3**

****方法:**在这个问题中，观察当我们在子阵列中正好有一个元素具有 **K** 频率时，将获得最小的长度，这意味着子阵列看起来像**【X】。。其中 **X** 是数组 arr 的一个元素。现在，按照以下步骤解决这个问题:****

1.  **创建一个对的数组，使得数字(即 **arr[i]** )是第一个元素，其索引(即 **i** )是第二个元素。**
2.  **对这个数组进行排序。**
3.  **现在，创建一个变量 **mn** 来存储答案，并用 **INT_MAX** 初始化。**
4.  **现在，遍历数组从 **i = 0** 到**I =(N–K)**，在每次迭代中:

    *   如果 **i** 和 **(i+K-1)** 处的元素相等，则使 **mn** 等于 **mn** 中的最小值和以下指标之间的差值。** 
5.  **返回 **mn** 作为最终答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum length of
// subarray having an element exactly K times
int minLengthKRepetitions(int* arr, int& N, 
                          int& K)
{
    pair<int, int> indices[N];
    int mn = INT_MAX, i;

    for (i = 0; i < N; i++) {
        indices[i].first = arr[i];
        indices[i].second = i;
    }

    sort(indices, indices + N);
    for (i = 0; i <= N - K; i++) {
        if (indices[i].first == indices[i + K - 1].first)
            mn = min(mn, indices[i + K - 1].second
                             - indices[i].second + 1);
    }

    return (mn == INT_MAX) ? -1 : mn;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 2, 2, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;

    cout << minLengthKRepetitions(arr, N, K);
    return 0;
}
```

****Output**

```
3
```** 

*****时间复杂度:*** O(N * log N)
***辅助空间:*** O(N)**