# 任一方向距离 arr[I]D 处元素的最小和最大计数

> 原文:[https://www . geeksforgeeks . org/双向到达距离 d 处元素的最小和最大计数/](https://www.geeksforgeeks.org/minimum-and-maximum-count-of-elements-at-d-distance-from-arri-in-either-direction/)

给定一个[排序数组](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/) **arr[]** 和一个正整数 **D** ，任务是从数组元素 **arr[i]** 在任一方向上，即在范围**【arr[I]–D，arr[I]】**或**【arr[I]，arr[I]+D】**内，找出位于距离 **D** 的数组元素的最小和最大数量。

**示例:**

> **输入** arr[] = {2，4，7，11，13，14}，D = 4
> **输出:** 1 3
> **解释:**
> 包含的最小数组元素数是从 arr[0](= 2)开始的 1，因为只有 1 个元素位于[-2，2]范围内。
> 数组元素的最小数量是 arr[3](= 11)的 3，因为只有 3 个元素位于范围[11，15]内。
> 因此，打印 1、3。
> 
> **输入:** arr[] = {1，3，5，9，14}，D = 5
> T3】输出: 1 3

**方法:**使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决给定的问题，方法是在每个点的左右使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)检查距离范围 **D** 可以包含多少点。按照以下步骤解决问题:

*   初始化两个变量，比如 **min** 和 **max** 来存储距离范围 **D** 内包含的最小和最大元素。
*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr[]** ，并对每个元素执行以下操作:
    1.  初始化一个变量**距离**来计算距离范围 **D** 内包含的点数。
    2.  执行 **arr[i]** 左侧的[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，并使用以下步骤在**【arr[I]–D，arr[I]】**范围内查找数组元素:
        *   初始化**左= 0，右= I–1**并且在每次迭代时:
            *   求 **mid =(左+右)/ 2** 的值。
            *   如果**arr[mid]<arr[I]–D，**则将**左**的值更新为 **mid + 1** 。否则，将 **dist** 的值更新为 **mid** ，将 **right** 的值更新为**mid–1**。
    3.  根据**距离**的值更新**最小值**和**最大值**的值。
    4.  执行**左面的[二分搜索法](https://www.geeksforgeeks.org/binary-search/)arr【I】**并使用以下步骤找到范围**【arr【I】、arr【I】+D】**内的数组元素数量:
        *   初始化**左= i + 1，右= N–I**，每次迭代:
            *   求 **mid =(左+右)/ 2** 的值。
            *   如果 **arr[mid] > arr[i] + D** ，则将**右侧**的值更新为**mid–1**。否则，将 **dist** 的值更新为 **mid** ，将 **left** 的值更新为 **mid + 1** 。
    5.  根据**距离**的值更新**最小值**和**最大值**的值。
*   完成上述步骤后，打印 **min** 和 **max** 的值，作为最终的最小和最大覆盖点数。

下面是上述方法的实现:

## C++

```
// c++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform the Binary
// Search to the left of arr[i]
// over the given range
int leftSearch(int arr[], int val, int i)
{

    // Base Case
    if (i == 0)
        return 1;

    int left = 0, right = i - 1;
    int ind = -1;

    // Binary Search for index to left
    while (left <= right) {

        int mid = (left + right) / 2;
        if (arr[mid] < val) {
            left = mid + 1;
        }
        else {
            right = mid - 1;

            // update index
            ind = mid;
        }
    }

    // Return the number of elements
    // by subtracting indices
    return ind != -1 ? i - ind + 1 : 1;
}

// Function to perform the Binary
// Search to the right of arr[i]
// over the given range
int rightSearch(int arr[], int val, int i, int N)
{

    // Base Case
    if (i == (N - 1))
        return 1;

    int left = i + 1;
    int right = N - 1;
    int ind = -1;

    // Binary Search for index to right
    while (left <= right) {

        int mid = (left + right) / 2;
        if (arr[mid] > val) {
            right = mid - 1;
        }
        else {
            left = mid + 1;

            // Update the index
            ind = mid;
        }
    }

    // Return the number of elements
    // by subtracting indices
    return ind != -1 ? ind - i + 1 : 1;
}
vector<int> minMaxRange(int arr[], int D, int N)
{

    // Stores the minimum and maximum
    // number of points that lies
    // over the distance of D
    int mx = 1, mn = N;

    // Iterate the array
    for (int i = 0; i < N; i++) {

        // Count of elements included
        // to left of point at index i
        int dist = leftSearch(arr, arr[i] - D, i);

        // Update the minimum number
        // of points
        mn = min(mn, dist);

        // Update the maximum number
        // of points
        mx = max(mx, dist);

        // Count of elements included
        // to right of point at index i
        dist = rightSearch(arr, arr[i] + D, i, N);

        // Update the minimum number
        // of points
        mn = min(mn, dist);

        // Update the maximum number
        // of points
        mx = max(mx, dist);
    }

    // Return the array
    vector<int> v;
    v.push_back(mn);
    v.push_back(mx);
    return v;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 5, 9, 14 };
    int N = 5;
    int D = 4;
    vector<int> minMax = minMaxRange(arr, D, N);
    cout << minMax[0] << " " << minMax[1] << endl;
    return 0;
}

// This code is contributed by dwivediyash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.lang.Math;
import java.util.*;

class GFG {

    // Function to find the minimum and
    // maximum number of points included
    // in a range of distance D
    public static int[] minMaxRange(
        int[] arr, int D, int N)
    {

        // Stores the minimum and maximum
        // number of points that lies
        // over the distance of D
        int max = 1, min = N;

        // Iterate the array
        for (int i = 0; i < N; i++) {

            // Count of elements included
            // to left of point at index i
            int dist = leftSearch(
                arr, arr[i] - D, i);

            // Update the minimum number
            // of points
            min = Math.min(min, dist);

            // Update the maximum number
            // of points
            max = Math.max(max, dist);

            // Count of elements included
            // to right of point at index i
            dist = rightSearch(
                arr, arr[i] + D, i);

            // Update the minimum number
            // of points
            min = Math.min(min, dist);

            // Update the maximum number
            // of points
            max = Math.max(max, dist);
        }

        // Return the array
        return new int[] { min, max };
    }

    // Function to perform the Binary
    // Search to the left of arr[i]
    // over the given range
    public static int leftSearch(
        int[] arr, int val, int i)
    {
        // Base Case
        if (i == 0)
            return 1;

        int left = 0, right = i - 1;
        int ind = -1;

        // Binary Search for index to left
        while (left <= right) {

            int mid = (left + right) / 2;
            if (arr[mid] < val) {
                left = mid + 1;
            }
            else {
                right = mid - 1;

                // update index
                ind = mid;
            }
        }

        // Return the number of elements
        // by subtracting indices
        return ind != -1 ? i - ind + 1 : 1;
    }

    // Function to perform the Binary
    // Search to the right of arr[i]
    // over the given range
    public static int rightSearch(
        int[] arr, int val, int i)
    {
        // Base Case
        if (i == arr.length - 1)
            return 1;

        int left = i + 1;
        int right = arr.length - 1;
        int ind = -1;

        // Binary Search for index to right
        while (left <= right) {

            int mid = (left + right) / 2;
            if (arr[mid] > val) {
                right = mid - 1;
            }
            else {
                left = mid + 1;

                // Update the index
                ind = mid;
            }
        }

        // Return the number of elements
        // by subtracting indices
        return ind != -1 ? ind - i + 1 : 1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 3, 5, 9, 14 };
        int N = arr.length;
        int D = 4;
        int[] minMax = minMaxRange(arr, D, N);

        // Function Call
        System.out.print(
            minMax[0] + " " + minMax[1]);
    }
}
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find the minimum and
# maximum number of points included
# in a range of distance D
def minMaxRange(arr, D, N):

    # Stores the minimum and maximum
    # number of points that lies
    # over the distance of D
    Max = 1
    Min = N

    # Iterate the array
    for i in range(N):

        # Count of elements included
        # to left of point at index i
        dist = leftSearch(arr, arr[i] - D, i)

        # Update the minimum number
        # of points
        Min = min(Min, dist)

        # Update the maximum number
        # of points
        Max = max(Max, dist)

        # Count of elements included
        # to right of point at index i
        dist = rightSearch(arr, arr[i] + D, i)

        # Update the minimum number
        # of points
        Min = min(Min, dist)

        # Update the maximum number
        # of points
        Max = max(Max, dist)

    # Return the array
    return [Min, Max]

# Function to perform the Binary
# Search to the left of arr[i]
# over the given range
def leftSearch(arr, val, i):
    # Base Case
    if (i == 0):
        return 1

    left = 0
    right = i - 1
    ind = -1

    # Binary Search for index to left
    while (left <= right):

        mid = (left + right) // 2
        if (arr[mid] < val):
            left = mid + 1

        else:
            right = mid - 1

            # update index
            ind = mid

    # Return the number of elements
    # by subtracting indices
    return i - ind + 1 if ind != -1 else 1

# Function to perform the Binary
# Search to the right of arr[i]
# over the given range
def rightSearch(arr, val, i):

    # Base Case
    if (i == len(arr) - 1):
        return 1

    left = i + 1
    right = len(arr) - 1
    ind = -1

    # Binary Search for index to right
    while (left <= right):

        mid = (left + right) // 2

        if (arr[mid] > val):
            right = mid - 1
        else:
            left = mid + 1

            # Update the index
            ind = mid

    # Return the number of elements
    # by subtracting indices
    return ind - i + 1 if ind != -1 else 1

# Driver Code
arr = [1, 3, 5, 9, 14]
N = len(arr)
D = 4
minMax = minMaxRange(arr, D, N)

# Function Call
print(f"{minMax[0]}  {minMax[1]}")

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function to find the minimum and
    // maximum number of points included
    // in a range of distance D
    public static int[] minMaxRange(int[] arr, int D, int N)
    {

        // Stores the minimum and maximum
        // number of points that lies
        // over the distance of D
        int max = 1, min = N;

        // Iterate the array
        for (int i = 0; i < N; i++)
        {

            // Count of elements included
            // to left of point at index i
            int dist = leftSearch(
                arr, arr[i] - D, i);

            // Update the minimum number
            // of points
            min = Math.Min(min, dist);

            // Update the maximum number
            // of points
            max = Math.Max(max, dist);

            // Count of elements included
            // to right of point at index i
            dist = rightSearch(
                arr, arr[i] + D, i);

            // Update the minimum number
            // of points
            min = Math.Min(min, dist);

            // Update the maximum number
            // of points
            max = Math.Max(max, dist);
        }

        // Return the array
        return new int[] { min, max };
    }

    // Function to perform the Binary
    // Search to the left of arr[i]
    // over the given range
    public static int leftSearch(
        int[] arr, int val, int i)
    {
        // Base Case
        if (i == 0)
            return 1;

        int left = 0, right = i - 1;
        int ind = -1;

        // Binary Search for index to left
        while (left <= right)
        {

            int mid = (left + right) / 2;
            if (arr[mid] < val)
            {
                left = mid + 1;
            }
            else
            {
                right = mid - 1;

                // update index
                ind = mid;
            }
        }

        // Return the number of elements
        // by subtracting indices
        return ind != -1 ? i - ind + 1 : 1;
    }

    // Function to perform the Binary
    // Search to the right of arr[i]
    // over the given range
    public static int rightSearch(
        int[] arr, int val, int i)
    {
        // Base Case
        if (i == arr.Length - 1)
            return 1;

        int left = i + 1;
        int right = arr.Length - 1;
        int ind = -1;

        // Binary Search for index to right
        while (left <= right)
        {

            int mid = (left + right) / 2;
            if (arr[mid] > val)
            {
                right = mid - 1;
            }
            else
            {
                left = mid + 1;

                // Update the index
                ind = mid;
            }
        }

        // Return the number of elements
        // by subtracting indices
        return ind != -1 ? ind - i + 1 : 1;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 3, 5, 9, 14 };
        int N = arr.Length;
        int D = 4;
        int[] minMax = minMaxRange(arr, D, N);

        // Function Call
        Console.Write(minMax[0] + " " + minMax[1]);
    }
}

// This code is contributed by gfgking.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum and
        // maximum number of points included
        // in a range of distance D
        function minMaxRange(
            arr, D, N) {

            // Stores the minimum and maximum
            // number of points that lies
            // over the distance of D
            let max = 1, min = N;

            // Iterate the array
            for (let i = 0; i < N; i++) {

                // Count of elements included
                // to left of point at index i
                let dist = leftSearch(
                    arr, arr[i] - D, i);

                // Update the minimum number
                // of points
                min = Math.min(min, dist);

                // Update the maximum number
                // of points
                max = Math.max(max, dist);

                // Count of elements included
                // to right of point at index i
                dist = rightSearch(
                    arr, arr[i] + D, i);

                // Update the minimum number
                // of points
                min = Math.min(min, dist);

                // Update the maximum number
                // of points
                max = Math.max(max, dist);
            }

            // Return the array
            return [min, max];
        }

        // Function to perform the Binary
        // Search to the left of arr[i]
        // over the given range
        function leftSearch(
            arr, val, i) {
            // Base Case
            if (i == 0)
                return 1;

            let left = 0, right = i - 1;
            let ind = -1;

            // Binary Search for index to left
            while (left <= right) {

                let mid = Math.floor((left + right) / 2);
                if (arr[mid] < val) {
                    left = mid + 1;
                }
                else {
                    right = mid - 1;

                    // update index
                    ind = mid;
                }
            }

            // Return the number of elements
            // by subtracting indices
            return ind != -1 ? i - ind + 1 : 1;
        }

        // Function to perform the Binary
        // Search to the right of arr[i]
        // over the given range
        function rightSearch(
            arr, val, i) {
            // Base Case
            if (i == arr.length - 1)
                return 1;

            let left = i + 1;
            let right = arr.length - 1;
            let ind = -1;

            // Binary Search for index to right
            while (left <= right) {

                let mid = Math.floor((left + right) / 2);
                if (arr[mid] > val) {
                    right = mid - 1;
                }
                else {
                    left = mid + 1;

                    // Update the index
                    ind = mid;
                }
            }

            // Return the number of elements
            // by subtracting indices
            return ind != -1 ? ind - i + 1 : 1;
        }

        // Driver Code

        let arr = [1, 3, 5, 9, 14];
        let N = arr.length;
        let D = 4;
        let minMax = minMaxRange(arr, D, N);

        // Function Call
        document.write(
            minMax[0] + " " + minMax[1]);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
1 3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*