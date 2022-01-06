# 通过最多一次替换来最小化两个给定数组的相同索引元素的绝对差之和

> 原文:[https://www . geeksforgeeks . org/通过最多一次替换来最小化两个给定数组的相同索引元素的绝对差之和/](https://www.geeksforgeeks.org/minimize-sum-of-absolute-differences-of-same-indexed-elements-of-two-given-arrays-by-at-most-one-replacement/)

给定两个大小分别为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**，任务是通过最多替换**A【】**中的一个元素，找到两个数组的相同索引元素的绝对差的最小可能和，即所有 **i** 的**| A[I]–B[I]|**的和，使得 **0 ≤ i < N**

**示例:**

> **输入:** A[] = {6，4，1，9，7，5}，B[] = {3，9，7，4，2，1}，N = 6
> **输出:** 22
> **说明:**将 A[2]替换为 A[4]。数组 A[]修改为[6，4，7，9，7，5]。这将产生| 6–3 |+| 4–9 |+| 7–7 |+| 9–4 |+| 7–2 |+| 5–1 | = 22 的绝对和差，这是最大可能值。
> 
> **输入:** A[] = {2，5，8}，B[] = {7，6，1}，N = 3
> T3】输出: 7

**方法:**解决问题的思路是利用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)对每个 **B[i] (0 ≤ i < N)** 计算 **A[]** 到 **B[i]** 中最接近的元素，选出最佳选择。
按照以下步骤解决问题。

1.  初始化两个大小为 **N** 的数组 **diff[]** 和 **BestDiff[]** 。
2.  初始化一个变量**将**加到 **0** 。
3.  从 **0** 到**N–1**遍历，对于每个 **i** 存储**diff[I]= ABS(A[I]–B[I])**，并将 **diff[i]** 添加到 **sum** 。
4.  [将数组 **A[]** 按升序排序。](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)
5.  迭代索引 **0** 到**N–1**，对于每个 **i** ，使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，在 **A[]** 中找到最接近 **B[i]** 的元素，说出 **X** 并将其存储在 **BestDiff[]** 中作为**best diff[I]= ABS(B[I]–X)**
6.  初始化一个变量**最佳选择**。
7.  迭代索引 **0** 到**N–1**并将**最佳选择**更新为**最佳选择=最大值(最佳选择，差异[I]-最佳差异[i])**
8.  现在，**Sum–best pick**给出答案。

下面是上述方法的一个实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return minimum sum of absolute
// difference of same-indexed elements of two arrays
int minAbsoluteSumDiff(vector<int> A,
                       vector<int> B, int N)
{
    // Stores initial sum
    int sum = 0;

    // Stores the differences between
    // same-indexed elements of A[] and B[]
    int diff[N];

    for (int i = 0; i < N; i++) {

        // Update absolute difference
        diff[i] = abs(A[i] - B[i]);

        // Update sum of differences
        sum += diff[i];
    }

    // Sort array A[] in ascending order
    sort(A.begin(), A.end());

    // Stores best possible
    // difference for each i
    int bestDiff[N];

    for (int i = 0; i < N; i++) {

        // Find the index in A[]
        // which >= B[i].
        int j = lower_bound(A.begin(), A.end(), B[i])
                - A.begin();

        // Store minimum of abs(A[j] - B[i])
        // and abs(A[j - 1] - B[i])
        if (j != 0 && j != N)
            bestDiff[i] = min(abs(A[j] - B[i]),
                              abs(A[j - 1] - B[i]));

        // If A[j] can be replaced
        else if (j == 0)
            bestDiff[i] = abs(A[j] - B[i]);

        // If A[j - 1] can be replaced
        else if (j == N)
            bestDiff[i] = abs(A[j - 1] - B[i]);
    }

    // Find best possible replacement
    int bestPick = 0;
    for (int i = 0; i < N; i++) {
        bestPick = max(bestPick,
                       diff[i] - bestDiff[i]);
    }

    // Return the result
    return sum - bestPick;
}

// Driver code
int main()
{
    // Input
    vector<int> A = { 2, 5, 8 };
    vector<int> B = { 7, 6, 1 };

    int N = 3;

    cout << minAbsoluteSumDiff(A, B, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Recursive implementation of
    // lower_bound
    static int lower_bound(int arr[], int low, int high,
                           int X)
    {

        // Base Case
        if (low > high) {
            return low;
        }

        // Find the middle index
        int mid = low + (high - low) / 2;

        // If arr[mid] is greater than
        // or equal to X then search
        // in left subarray
        if (arr[mid] >= X) {
            return lower_bound(arr, low, mid - 1, X);
        }

        // If arr[mid] is less than X
        // then search in right subarray
        return lower_bound(arr, mid + 1, high, X);
    }

    // Function to return minimum sum of absolute
    // difference of same-indexed elements of two arrays
    static int minAbsoluteSumDiff(int A[], int B[], int N)
    {
        // Stores initial sum
        int sum = 0;

        // Stores the differences between
        // same-indexed elements of A[] and B[]
        int diff[] = new int[N];

        for (int i = 0; i < N; i++) {

            // Update absolute difference
            diff[i] = Math.abs(A[i] - B[i]);

            // Update sum of differences
            sum += diff[i];
        }

        // Sort array A[] in ascending order
        Arrays.sort(A);

        // Stores best possible
        // difference for each i
        int bestDiff[] = new int[N];

        for (int i = 0; i < N; i++) {

            // Find the index in A[]
            // which >= B[i].
            int j = lower_bound(A, 0, N - 1, B[i]);

            // Store minimum of abs(A[j] - B[i])
            // and abs(A[j - 1] - B[i])
            if (j != 0 && j != N)
                bestDiff[i]
                    = Math.min(Math.abs(A[j] - B[i]),
                               Math.abs(A[j - 1] - B[i]));

            // If A[j] can be replaced
            else if (j == 0)
                bestDiff[i] = Math.abs(A[j] - B[i]);

            // If A[j - 1] can be replaced
            else if (j == N)
                bestDiff[i] = Math.abs(A[j - 1] - B[i]);
        }

        // Find best possible replacement
        int bestPick = 0;
        for (int i = 0; i < N; i++) {
            bestPick
                = Math.max(bestPick, diff[i] - bestDiff[i]);
        }

        // Return the result
        return sum - bestPick;
    }

    // Driver code
    public static void main(String[] args)
    {
        // Input
        int A[] = { 2, 5, 8 };
        int B[] = { 7, 6, 1 };

        int N = 3;

        System.out.println(minAbsoluteSumDiff(A, B, N));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach
from bisect import bisect_left,bisect_right

# Function to return minimum sum of absolute
# difference of same-indexed elements of two arrays
def minAbsoluteSumDiff(A, B, N):

    # Stores initial sum
    sum = 0

    # Stores the differences between
    # same-indexed elements of A[] and B[]
    diff = [0] * N

    for i in range(N):

        # Update absolute difference
        diff[i] = abs(A[i] - B[i])

        # Update sum of differences
        sum += diff[i]

    # Sort array A[] in ascending order
    A.sort()

    # Stores best possible
    # difference for each i
    bestDiff = [0] * N

    for i in range(N):

        # Find the index in A[]
        # which >= B[i].
        j = bisect_left(A, B[i])

        # Store minimum of abs(A[j] - B[i])
        # and abs(A[j - 1] - B[i])
        if (j != 0 and j != N):
            bestDiff[i] = min(abs(A[j] - B[i]),
                              abs(A[j - 1] - B[i]))

        # If A[j] can be replaced
        elif (j == 0):
            bestDiff[i] = abs(A[j] - B[i])

        # If A[j - 1] can be replaced
        elif (j == N):
            bestDiff[i] = abs(A[j - 1] - B[i])

    # Find best possible replacement
    bestPick = 0

    for i in range(N):
        bestPick = max(bestPick,
                       diff[i] - bestDiff[i])

    # Return the result
    return sum - bestPick

# Driver code
if __name__ == "__main__":

    # Input
    A = [ 2, 5, 8 ]
    B = [ 7, 6, 1 ]

    N = 3

    print(minAbsoluteSumDiff(A, B, N))

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Recursive implementation of
    // lower_bound
static int lower_bound(int []arr, int low, int high, int X)
    {

        // Base Case
        if (low > high) {
            return low;
        }

        // Find the middle index
        int mid = low + (high - low) / 2;

        // If arr[mid] is greater than
        // or equal to X then search
        // in left subarray
        if (arr[mid] >= X) {
            return lower_bound(arr, low, mid - 1, X);
        }

        // If arr[mid] is less than X
        // then search in right subarray
        return lower_bound(arr, mid + 1, high, X);
    }

    // Function to return minimum sum of absolute
    // difference of same-indexed elements of two arrays
    static int minAbsoluteSumDiff(int []A, int []B, int N)
    {
        // Stores initial sum
        int sum = 0;

        // Stores the differences between
        // same-indexed elements of A[] and B[]
        int []diff = new int[N];

        for (int i = 0; i < N; i++) {

            // Update absolute difference
            diff[i] = Math.Abs(A[i] - B[i]);

            // Update sum of differences
            sum += diff[i];
        }

        // Sort array A[] in ascending order
        Array.Sort(A);

        // Stores best possible
        // difference for each i
        int []bestDiff = new int[N];

        for (int i = 0; i < N; i++) {

            // Find the index in A[]
            // which >= B[i].
            int j = lower_bound(A, 0, N - 1, B[i]);

            // Store minimum of abs(A[j] - B[i])
            // and abs(A[j - 1] - B[i])
            if (j != 0 && j != N)
                bestDiff[i]
                    = Math.Min(Math.Abs(A[j] - B[i]),
                               Math.Abs(A[j - 1] - B[i]));

            // If A[j] can be replaced
            else if (j == 0)
                bestDiff[i] = Math.Abs(A[j] - B[i]);

            // If A[j - 1] can be replaced
            else if (j == N)
                bestDiff[i] = Math.Abs(A[j - 1] - B[i]);
        }

        // Find best possible replacement
        int bestPick = 0;
        for (int i = 0; i < N; i++) {
            bestPick
                = Math.Max(bestPick, diff[i] - bestDiff[i]);
        }

        // Return the result
        return sum - bestPick;
    }

    // Driver code
    public static void Main()
    {
        // Input
        int []A = { 2, 5, 8 };
        int []B = { 7, 6, 1 };

        int N = 3;

        Console.Write(minAbsoluteSumDiff(A, B, N));
    }
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

  function lower_bound(arr, low, high,
                           X)
    {

        // Base Case
        if (low > high) {
            return low;
        }

        // Find the middle index
        var mid = low + (high - low) / 2;

        // If arr[mid] is greater than
        // or equal to X then search
        // in left subarray
        if (arr[mid] >= X) {
            return lower_bound(arr, low, mid - 1, X);
        }

        // If arr[mid] is less than X
        // then search in right subarray
        return lower_bound(arr, mid + 1, high, X);
    }

    // Function to return minimum sum of absolute
    // difference of same-indexed elements of two arrays
    function minAbsoluteSumDiff(A, B, N)
    {
        // Stores initial sum
        var sum = 0;

        // Stores the differences between
        // same-indexed elements of A[] and B[]
        var diff = new Array(N);

        for (i = 0; i < N; i++) {

            // Update absolute difference
            diff[i] = Math.abs(A[i] - B[i]);

            // Update sum of differences
            sum += diff[i];
        }

        // Sort array A[] in ascending order
        A.sort();

        // Stores best possible
        // difference for each i
        var bestDiff = new Array(N);
        var i;
        for (i = 0; i < N; i++) {

            // Find the index in A[]
            // which >= B[i].
            var j = lower_bound(A, 0, N - 1, B[i]);

            // Store minimum of abs(A[j] - B[i])
            // and abs(A[j - 1] - B[i])
            if (j != 0 && j != N)
                bestDiff[i]
                    = Math.min(Math.abs(A[j] - B[i]),
                               Math.abs(A[j - 1] - B[i]));

            // If A[j] can be replaced
            else if (j == 0)
                bestDiff[i] = Math.abs(A[j] - B[i]);

            // If A[j - 1] can be replaced
            else if (j == N)
                bestDiff[i] = Math.abs(A[j - 1] - B[i]);
        }

        // Find best possible replacement
        var bestPick = 0;
        for (i = 0; i < N; i++) {
            bestPick
                = Math.max(bestPick, diff[i] - bestDiff[i]);
        }

        // Return the result
        return sum - bestPick;
    }

         // Driver code
        // Input
        var A = [2, 5, 8];
        var B = [7, 6, 1];

        var N = 3;

        document.write(minAbsoluteSumDiff(A, B, N));

</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(NLogN)*
***辅助空间:** O(N)*