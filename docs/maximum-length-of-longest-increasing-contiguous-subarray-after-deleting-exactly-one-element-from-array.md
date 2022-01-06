# 从数组中精确删除一个元素后最长递增连续子数组的最大长度

> 原文:[https://www . geeksforgeeks . org/从数组中删除恰好一个元素后最大长度最长递增连续子数组/](https://www.geeksforgeeks.org/maximum-length-of-longest-increasing-contiguous-subarray-after-deleting-exactly-one-element-from-array/)

给定一个由 **N** 个整数组成的数组 **arr[ ]** 。任务是从给定的数组中精确地移除一个元素后，找到最长的递增连续子数组的最大长度。
**例:**

> **输入:** N = 5，arr[] = { 2，4，1，5，7 }
> **输出** **:** 4
> **说明:**从数组中移除第三个元素后，数组 arr[]变为[2，4，5，7]。因此，最长递增连续子阵列的长度为 4，这是最大值。
> **输入:** N = 4，arr[] = { 2，1，3，1}
> **输出:** 2
> **解释:**我们可以从数组中去掉第二个或第一个元素，数组中，arr[]变成{1，3，1 }或{ 2，3，1 }，最长递增的连续子数组长度为 2，最大。

**方法:**该任务可以通过跟踪从索引“I”开始并在索引“I”结束的[最长递增子序列](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)来解决。

*   创建两个大小为 **N** 的阵列**正面[ ]** 和**背面[ ]** ，并用 **1** 初始化这两个阵列。
*   计算从 **1** 到 **N** 的每个 **i** 的**前【I】**和**后**，其中**前【I】**代表从位置 **i** 开始的[最长递增子序列](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)的最大长度，而**后【I】**代表结束于位置 **i 的最长递增子序列的最大长度**
*   数组 **front[ ]** 可以从左到右依次计算，条件如下: **if(a[i] > a[i-1])** 更新 **front[i] = front[i-1] + 1，**否则继续**。**同样，数组**back【】**可以按照从右到左的顺序计算，条件如下:**如果(a[I]<****a[I+1】)**更新 **back[i] = back[i+1] + 1** ，否则继续
*   现在用这两个数组计算 **ans，**初始化为 1。
*   更新 **ans** 如果 **(a[i] < a[i+2])，**表示 **(i+1)** 第**个**元素被删除，与**回[**数组相同。

下面是上述方法的实现:

## C++

```
// c++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum length of longest
// increasing contiguous subarray after removing
// exactly one element from array
int maxLenSubarr(int arr[], int n)
{
    // Creating front[] and back[] arrays
    int front[n], back[n];
    for (int i = 0; i < n; i++) {
        front[i] = 1;
        back[i] = 1;
    }

    // Calculating the front[]
    for (int i = 1; i < n; i++) {
        if (arr[i] > arr[i - 1]) {

            // Update front[i]
            front[i] = front[i - 1] + 1;
        }
    }

    // Calculating the back[]
    for (int i = n - 2; i >= 0; i--) {
        if (arr[i] < arr[i + 1]) {

            // update back[i]
            back[i] = back[i + 1] + 1;
        }
    }

    // Store the length of longest increasing
    // contiguous subarray
    int ans = 1;

    // Check whether first element is
    // contributing in subarray or not
    bool check_first = true;

    // Keep track of longest subarray when
    // first element is removed
    int ans_first = 1;

    for (int i = 1; i < n; i++) {

        // front[i] == 1 means contribution of
        // first element in max
        // length subarray has ended
        if (front[i] == 1) {
            check_first = true;
        }

        ans_first = max(ans_first, front[i]);
    }

    // First element contributes in the subarray
    if (check_first == false) {
        ans_first -= 1;
    }

    // Check whether last element is
    // contributing in subarray or not
    bool check_last = true;

    // Keep track of longest subarray when
    // last element is removed
    int ans_last = 1;

    for (int i = n - 2; i >= 0; i--) {

        // back[i] == 1 means contribution of
        // last element in max
        // length subarray has ended
        if (back[i] == 1) {
            check_last = true;
        }
        ans_last = max(ans_last, back[i]);
    }

    // Last element contributes in the subarray
    if (check_last == false) {
        ans_last -= 1;
    }

    // Update ans
    ans = max(ans_first, ans_last);

    // Calculating max length when
    // (i+1)th element is deleted
    for (int i = 0; i < n - 2; i++) {
        if (arr[i] < arr[i + 2]) {
            ans = max(ans,
                      front[i] + back[i + 2]);
        }
    }

    return ans;
}

// Driver code
int main()
{

    int arr[] = { 2, 1, 3, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxLenSubarr(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

public class GFG {

// Function to find the maximum length of longest
// increasing contiguous subarray after removing
// exactly one element from array
static int maxLenSubarr(int arr[], int n)
{
    // Creating front[] and back[] arrays
    int front[] = new int[n];
    int back[] = new int[n];
    for (int i = 0; i < n; i++) {
        front[i] = 1;
        back[i] = 1;
    }

    // Calculating the front[]
    for (int i = 1; i < n; i++) {
        if (arr[i] > arr[i - 1]) {

            // Update front[i]
            front[i] = front[i - 1] + 1;
        }
    }

    // Calculating the back[]
    for (int i = n - 2; i >= 0; i--) {
        if (arr[i] < arr[i + 1]) {

            // update back[i]
            back[i] = back[i + 1] + 1;
        }
    }

    // Store the length of longest increasing
    // contiguous subarray
    int ans = 1;

    // Check whether first element is
    // contributing in subarray or not
    boolean check_first = true;

    // Keep track of longest subarray when
    // first element is removed
    int ans_first = 1;

    for (int i = 1; i < n; i++) {

        // front[i] == 1 means contribution of
        // first element in max
        // length subarray has ended
        if (front[i] == 1) {
            check_first = true;
        }

        ans_first = Math.max(ans_first, front[i]);
    }

    // First element contributes in the subarray
    if (check_first == false) {
        ans_first -= 1;
    }

    // Check whether last element is
    // contributing in subarray or not
    boolean check_last = true;

    // Keep track of longest subarray when
    // last element is removed
    int ans_last = 1;

    for (int i = n - 2; i >= 0; i--) {

        // back[i] == 1 means contribution of
        // last element in max
        // length subarray has ended
        if (back[i] == 1) {
            check_last = true;
        }
        ans_last = Math.max(ans_last, back[i]);
    }

    // Last element contributes in the subarray
    if (check_last == false) {
        ans_last -= 1;
    }

    // Update ans
    ans = Math.max(ans_first, ans_last);

    // Calculating max length when
    // (i+1)th element is deleted
    for (int i = 0; i < n - 2; i++) {
        if (arr[i] < arr[i + 2]) {
            ans = Math.max(ans,
                      front[i] + back[i + 2]);
        }
    }

    return ans;
}

    // Driver code
    public static void main (String[] args) {

        int arr[] = { 2, 1, 3, 1 };
        int n = arr.length;
        System.out.println(maxLenSubarr(arr, n));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum length of longest
# increasing contiguous subarray after removing
# exactly one element from array
def maxLenSubarr(arr, n) :

    # Creating front[] and back[] arrays
    front = [0] * n;  back = [0] * n;
    for i in range(n) :
        front[i] = 1;
        back[i] = 1;

    # Calculating the front[]
    for i in range(1, n) :
        if (arr[i] > arr[i - 1]) :

            # Update front[i]
            front[i] = front[i - 1] + 1;

    # Calculating the back[]
    for i in range(n - 2, -1, -1) :
        if (arr[i] < arr[i + 1]) :

            # update back[i]
            back[i] = back[i + 1] + 1;

    # Store the length of longest increasing
    # contiguous subarray
    ans = 1;

    # Check whether first element is
    # contributing in subarray or not
    check_first = True;

    # Keep track of longest subarray when
    # first element is removed
    ans_first = 1;

    for i in range(1, n) :

        # front[i] == 1 means contribution of
        # first element in max
        # length subarray has ended
        if (front[i] == 1) :
            check_first = True;

        ans_first = max(ans_first, front[i]);

    # First element contributes in the subarray
    if (check_first == False) :
        ans_first -= 1;

    # Check whether last element is
    # contributing in subarray or not
    check_last = True;

    # Keep track of longest subarray when
    # last element is removed
    ans_last = 1;

    for i in range(n - 2, -1, -1) :

        # back[i] == 1 means contribution of
        # last element in max
        # length subarray has ended
        if (back[i] == 1) :
            check_last = True;

        ans_last = max(ans_last, back[i]);

    # Last element contributes in the subarray
    if (check_last == False) :
        ans_last -= 1;

    # Update ans
    ans = max(ans_first, ans_last);

    # Calculating max length when
    # (i+1)th element is deleted
    for i in range( n - 2) :
        if (arr[i] < arr[i + 2]) :
            ans = max(ans, front[i] + back[i + 2]);

    return ans;

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 1, 3, 1 ];
    n = len(arr);
    print(maxLenSubarr(arr, n));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach

using System;

public class GFG {

// Function to find the maximum length of longest
// increasing contiguous subarray after removing
// exactly one element from array
static int maxLenSubarr(int []arr, int n)
{
    // Creating front[] and back[] arrays
    int []front = new int[n];
    int []back = new int[n];
    for (int i = 0; i < n; i++) {
        front[i] = 1;
        back[i] = 1;
    }

    // Calculating the front[]
    for (int i = 1; i < n; i++) {
        if (arr[i] > arr[i - 1]) {

            // Update front[i]
            front[i] = front[i - 1] + 1;
        }
    }

    // Calculating the back[]
    for (int i = n - 2; i >= 0; i--) {
        if (arr[i] < arr[i + 1]) {

            // update back[i]
            back[i] = back[i + 1] + 1;
        }
    }

    // Store the length of longest increasing
    // contiguous subarray
    int ans = 1;

    // Check whether first element is
    // contributing in subarray or not
    bool check_first = true;

    // Keep track of longest subarray when
    // first element is removed
    int ans_first = 1;

    for (int i = 1; i < n; i++) {

        // front[i] == 1 means contribution of
        // first element in max
        // length subarray has ended
        if (front[i] == 1) {
            check_first = true;
        }

        ans_first = Math.Max(ans_first, front[i]);
    }

    // First element contributes in the subarray
    if (check_first == false) {
        ans_first -= 1;
    }

    // Check whether last element is
    // contributing in subarray or not
    bool check_last = true;

    // Keep track of longest subarray when
    // last element is removed
    int ans_last = 1;

    for (int i = n - 2; i >= 0; i--) {

        // back[i] == 1 means contribution of
        // last element in max
        // length subarray has ended
        if (back[i] == 1) {
            check_last = true;
        }
        ans_last = Math.Max(ans_last, back[i]);
    }

    // Last element contributes in the subarray
    if (check_last == false) {
        ans_last -= 1;
    }

    // Update ans
    ans = Math.Max(ans_first, ans_last);

    // Calculating max length when
    // (i+1)th element is deleted
    for (int i = 0; i < n - 2; i++) {
        if (arr[i] < arr[i + 2]) {
            ans = Math.Max(ans,
                      front[i] + back[i + 2]);
        }
    }

    return ans;
}

    // Driver code
    public static void Main(string[] args) {

        int []arr = { 2, 1, 3, 1 };
        int n = arr.Length;
        Console.WriteLine(maxLenSubarr(arr, n));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the maximum length of longest
        // increasing contiguous subarray after removing
        // exactly one element from array
        function maxLenSubarr(arr, n)
        {

            // Creating front[] and back[] arrays
            let front = new Array(n), back = new Array(n);
            for (let i = 0; i < n; i++) {
                front[i] = 1;
                back[i] = 1;
            }

            // Calculating the front[]
            for (let i = 1; i < n; i++) {
                if (arr[i] > arr[i - 1]) {

                    // Update front[i]
                    front[i] = front[i - 1] + 1;
                }
            }

            // Calculating the back[]
            for (let i = n - 2; i >= 0; i--) {
                if (arr[i] < arr[i + 1]) {

                    // update back[i]
                    back[i] = back[i + 1] + 1;
                }
            }

            // Store the length of longest increasing
            // contiguous subarray
            let ans = 1;

            // Check whether first element is
            // contributing in subarray or not
            let check_first = true;

            // Keep track of longest subarray when
            // first element is removed
            let ans_first = 1;

            for (let i = 1; i < n; i++) {

                // front[i] == 1 means contribution of
                // first element in max
                // length subarray has ended
                if (front[i] == 1) {
                    check_first = true;
                }

                ans_first = Math.max(ans_first, front[i]);
            }

            // First element contributes in the subarray
            if (check_first == false) {
                ans_first -= 1;
            }

            // Check whether last element is
            // contributing in subarray or not
            let check_last = true;

            // Keep track of longest subarray when
            // last element is removed
            let ans_last = 1;

            for (let i = n - 2; i >= 0; i--) {

                // back[i] == 1 means contribution of
                // last element in max
                // length subarray has ended
                if (back[i] == 1) {
                    check_last = true;
                }
                ans_last = Math.max(ans_last, back[i]);
            }

            // Last element contributes in the subarray
            if (check_last == false) {
                ans_last -= 1;
            }

            // Update ans
            ans = Math.max(ans_first, ans_last);

            // Calculating max length when
            // (i+1)th element is deleted
            for (let i = 0; i < n - 2; i++) {
                if (arr[i] < arr[i + 2]) {
                    ans = Math.max(ans,
                        front[i] + back[i + 2]);
                }
            }

            return ans;
        }

        // Driver code
        let arr = [2, 1, 3, 1];
        let n = arr.length
        document.write(maxLenSubarr(arr, n));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
2
```

***时间复杂度*****:**O(N)
***辅助空间*** **:** O(N)