# 最大圆子阵和的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-program-for-maximum-circular-subarray-sum/](https://www.geeksforgeeks.org/cpp-program-for-maximum-circular-subarray-sum/)

给定 n 个数字(都是+ve 和-ve)，排列成一个圆，求连续数字的最大和。

**示例:**

```
Input: a[] = {8, -8, 9, -9, 10, -11, 12}
Output: 22 (12 + 8 - 8 + 9 - 9 + 10)

Input: a[] = {10, -3, -4, 7, 6, 5, -4, -1} 
Output:  23 (7 + 6 + 5 - 4 -1 + 10) 

Input: a[] = {-1, 40, -14, 7, 6, 5, -4, -1}
Output: 52 (7 + 6 + 5 - 4 - 1 - 1 + 40)
```

**方法 1** 最大和可以有两种情况:

*   **情况 1:** 对最大和有贡献的元素被排列成没有缠绕。示例:{-10，2，-1，5}，{-2，4，-1，4，-1}。在这种情况下，[卡丹的算法](https://www.geeksforgeeks.org/archives/576)会产生结果。
*   **情况 2:** 对最大和有贡献的元素被布置成使得包裹在那里。示例:{10，-12，11}，{12，-5，4，-8，11}。在这种情况下，我们将包装改为非包装。让我们看看如何。贡献元素的包装意味着非贡献元素的不包装，所以找出非贡献元素的总和，并从总和中减去这个总和。为了找出非贡献的总和，反转每个元素的符号，然后运行卡丹的算法。
    我们的数组就像一个环，我们必须消除最大连续负数，这意味着在倒排数组中最大连续正数。最后，我们比较两种情况下得到的和，并返回两个和的最大值。

以下是上述方法的实现。

## C++

```
// C++ program for maximum contiguous circular sum problem
#include <bits/stdc++.h>
using namespace std;

// Standard Kadane's algorithm to
// find maximum subarray sum
int kadane(int a[], int n);

// The function returns maximum
// circular contiguous sum in a[]
int maxCircularSum(int a[], int n)
{
    // Case 1: get the maximum sum using standard kadane'
    // s algorithm
    int max_kadane = kadane(a, n);
     // if maximum sum using standard kadane' is less than 0
    if(max_kadane < 0)
      return max_kadane;

    // Case 2: Now find the maximum sum that includes
    // corner elements.
    int max_wrap = 0, i;
    for (i = 0; i < n; i++) {
        max_wrap += a[i]; // Calculate array-sum
        a[i] = -a[i]; // invert the array (change sign)
    }

    // max sum with corner elements will be:
    // array-sum - (-max subarray sum of inverted array)
    max_wrap = max_wrap + kadane(a, n);

    // The maximum circular sum will be maximum of two sums
    return (max_wrap > max_kadane) ? max_wrap : max_kadane;
}

// Standard Kadane's algorithm to find maximum subarray sum
// See https:// www.geeksforgeeks.org/archives/576 for details
int kadane(int a[], int n)
{
    int max_so_far = 0, max_ending_here = 0;
    int i;
    for (i = 0; i < n; i++) {
        max_ending_here = max_ending_here + a[i];

        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;
          if (max_ending_here < 0)
              max_ending_here = 0;
    }
    return max_so_far;
}

/* Driver program to test maxCircularSum() */
int main()
{
    int a[] = { 11, 10, -20, 5, -3, -5, 8, -13, 10 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << "Maximum circular sum is " << maxCircularSum(a, n) << endl;
    return 0;
}

// This is code is contributed by rathbhupendra
```

**输出:**

```
Maximum circular sum is 31
```

**复杂度分析:**

*   **时间复杂度:** O(n)，其中 n 为输入数组中的元素个数。
    因为只需要数组的线性遍历。
*   **辅助空间:** O(1)。
    因为不需要额外的空间。

**注意**如果所有数字都是负数，例如{-1，-2，-3}，上述算法就不起作用了。在这种情况下，它返回 0。这种情况可以通过在运行上述算法之前添加一个预检查来查看是否所有数字都是负数来处理。

**<u>方法 2</u>**
**方法:**在该方法中，修改 Kadane 的算法，找出最小连续子阵和与最大连续子阵和，然后检查 max_value 与从总和中减去 min_value 后剩下的值之间的最大值。
**算法**

1.  我们将计算给定数组的总和。
2.  我们将变量 curr_max，max_so_far，curr_min，min_so_far 声明为数组的第一个值。
3.  现在我们将使用卡丹算法来寻找最大子阵和和最小子阵和。
4.  检查数组中的所有值:-
    1.  如果 min_so_far 等于 sum，即所有值都是负的，那么我们返回 max_so_far。
    2.  否则，我们将计算 max_so_far 和(sum–min _ so _ far)的最大值并返回。

下面给出了上述方法的实现。

## C++

```
// C++ program for maximum contiguous circular sum problem
#include <bits/stdc++.h>
using namespace std;

// The function returns maximum
// circular contiguous sum in a[]
int maxCircularSum(int a[], int n)
{
    // Corner Case
    if (n == 1)
        return a[0];

    // Initialize sum variable which store total sum of the array.
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += a[i];
    }

    // Initialize every variable with first value of array.
    int curr_max = a[0], max_so_far = a[0], curr_min = a[0], min_so_far = a[0];

    // Concept of Kadane's Algorithm
    for (int i = 1; i < n; i++) {
        // Kadane's Algorithm to find Maximum subarray sum.
        curr_max = max(curr_max + a[i], a[i]);
        max_so_far = max(max_so_far, curr_max);

        // Kadane's Algorithm to find Minimum subarray sum.
        curr_min = min(curr_min + a[i], a[i]);
        min_so_far = min(min_so_far, curr_min);
    }

    if (min_so_far == sum)
        return max_so_far;

    // returning the maximum value
    return max(max_so_far, sum - min_so_far);
}

/* Driver program to test maxCircularSum() */
int main()
{
    int a[] = { 11, 10, -20, 5, -3, -5, 8, -13, 10 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << "Maximum circular sum is " << maxCircularSum(a, n) << endl;
    return 0;
}
```

**输出:**

```
Maximum circular sum is 31
```

**复杂度分析:**

*   **时间复杂度:** O(n)，其中 n 为输入数组中的元素个数。
    因为只需要数组的线性遍历。
*   **辅助空间:** O(1)。
    因为不需要额外的空间。

详见[最大圆子阵和](https://www.geeksforgeeks.org/maximum-contiguous-circular-sum/)整篇文章！