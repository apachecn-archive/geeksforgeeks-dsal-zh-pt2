# 最小化增量操作，使数组不递减

> 原文:[https://www . geesforgeks . org/minimum-increment-operations-to-make-array-non-reducing/](https://www.geeksforgeeks.org/minimize-increment-operations-to-make-array-non-decreasing/)

给定一个由 **n 个**整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 。修改数组，使每个元素至少与前一个元素一样大。这可以通过 **1** 增加任何元素的值来实现。任务是找到使数组不递减所需的最小移动次数。

**示例:**

> **输入:** n = 5，arr[] = {8，9，2，7，7}
> **输出:** 11
> **说明:**数组应该修改为 8 9 9 9 9，这个可以通过 11 招(7 + 2 + 2)完成。
> 
> **输入:** n = 10，arr[] = {1，1，1，1，1，1，1，1，1}
> **输出:** 0
> **说明:**数组已经不减了。

**逼近:**思路是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，在当前元素小于前一个元素的任意一点，然后将当前元素作为前一个元素，增加计数。按照以下步骤解决问题:

*   将变量**计数**初始化为 **0** 存储结果。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，n)** ，并执行以下任务:
    *   如果 **arr[i]** 小于 **arr[i-1]** ，则将 **arr[i]** 的值设置为 **arr[i-1]** ，并将**计数**的值增加 **arr[i]-arr[i-1]。**
*   执行上述步骤后，打印**计数**的值作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// value of count
long long countMoves(long int arr[], int n)
{

    // Variable to store the answer
    long int count = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {
        if (i > 0) {

            // Make the changes
            if (arr[i] < arr[i - 1]) {
                count += (arr[i - 1] - arr[i]);
                arr[i] = arr[i - 1];
            }
        }
    }

    // Return the answer
    return count;
}

// Driver Code
int main()
{

    int n = 5;

    long int arr[] = { 8, 9, 2, 7, 7 };

    cout << countMoves(arr, n);
    return 0;
}
```

**Output**

```
11
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)