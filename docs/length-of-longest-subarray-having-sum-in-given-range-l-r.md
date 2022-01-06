# 给定范围内具有和的最长子阵列的长度[L，R]

> 原文:[https://www . geeksforgeeks . org/最长子阵列长度-给定范围内有总和-l-r/](https://www.geeksforgeeks.org/length-of-longest-subarray-having-sum-in-given-range-l-r/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，求最长子阵列的长度，其和在**【L，R】**的范围内。

**示例:**

> **输入:** arr[] = {1，4，6}，L = 3，R = 8
> **输出:** 2
> **说明:**范围[3，8]内有和的有效子阵为{1，4}、{4}、{6}。其中最长的子阵列是长度为 2 的{1，4}。
> 
> **输入:** arr[] = {15，2，4，8，9，5，10，23}，L = 10，R = 23
> **输出:** 4

**方法:**给定的问题可以使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)来解决。首先，从[数组](https://www.geeksforgeeks.org/array-data-structure/)的起始元素创建一个窗口，使其总和大于 **L** 。保持两个变量 **i** 和 **j** 代表当前窗口的开始和结束索引。如果当前窗口的和大于 **R** ，则增加 **i** 的值，如果和小于 **L** ，则增加 **j** 的值。对于总和在**【L，R】**范围内的车窗，将其最大长度保持在变量 **len** 中，这是必需的答案。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// the longest subarray having its
// sum in the given range [L, R]
int largestSubArraySum(int arr[], int N,
                       int L, int R)
{
    // Store sum of current window
    int sum = 0;

    // Stores indices of current window
    int i = 0, j = 0;

    // Stores the maximum length
    int len = 0;

    // Calculating initial window
    while (sum < L && j < N) {
        sum += arr[j];
        j++;
    }

    // Loop to iterate over all windows
    // of having sum in range [L, R]
    while (i < N && j < N) {

        // If sum of window is less than L
        if (sum < L) {
            sum += arr[j];
            j++;
        }

        // If sum of window is more than R
        else if (sum > R) {
            sum -= arr[i];
            i++;
        }

        // If sum is in the range [L, R]
        else {

            // Update length
            len = max(len, j - i);
            sum += arr[j];
            j++;
        }
    }

    // Return Answer
    return len;
}

// Driver Code
int main()
{
    int arr[] = { 15, 2, 4, 8, 9, 5, 10, 23 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int L = 10, R = 23;

    cout << largestSubArraySum(arr, N, L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
class GFG {

    // Function to find the length of
    // the longest subarray having its
    // sum in the given range [L, R]
    static int largestSubArraySum(int[] arr, int N, int L,
                                  int R)
    {
        // Store sum of current window
        int sum = 0;

        // Stores indices of current window
        int i = 0, j = 0;

        // Stores the maximum length
        int len = 0;

        // Calculating initial window
        while (sum < L && j < N) {
            sum += arr[j];
            j++;
        }

        // Loop to iterate over all windows
        // of having sum in range [L, R]
        while (i < N && j < N) {

            // If sum of window is less than L
            if (sum < L) {
                sum += arr[j];
                j++;
            }

            // If sum of window is more than R
            else if (sum > R) {
                sum -= arr[i];
                i++;
            }

            // If sum is in the range [L, R]
            else {

                // Update length
                len = Math.max(len, j - i);
                sum += arr[j];
                j++;
            }
        }

        // Return Answer
        return len;
    }

    // Driver Code
    public static void main(String args[])
    {
        int[] arr = { 15, 2, 4, 8, 9, 5, 10, 23 };
        int N = arr.length;
        int L = 10, R = 23;

        System.out.println(largestSubArraySum(arr, N, L, R));
    }
}

// This code is contributed by Saurabh Jaiswal
```

## 蟒蛇 3

```
# Python 3 program of the above approach

# Function to find the length of
# the longest subarray having its
# sum in the given range [L, R]
def largestSubArraySum(arr, N, L, R):

    # Store sum of current window
    sum = 0

    # Stores indices of current window
    i = 0
    j = 0

    # Stores the maximum length
    len = 0

    # Calculating initial window
    while (sum < L and j < N):
        sum += arr[j]
        j += 1

    # Loop to iterate over all windows
    # of having sum in range [L, R]
    while (i < N and j < N):

        # If sum of window is less than L
        if (sum < L):
            sum += arr[j]
            j += 1

        # If sum of window is more than R
        elif (sum > R):
            sum -= arr[i]
            i += 1

        # If sum is in the range [L, R]
        else:

            # Update length
            len = max(len, j - i)
            sum += arr[j]
            j += 1

    # Return Answer
    return len

# Driver Code
if __name__ == "__main__":

    arr = [15, 2, 4, 8, 9, 5, 10, 23]
    N = len(arr)
    L = 10
    R = 23

    print(largestSubArraySum(arr, N, L, R))

    # This code is contributed by gaurav01.
```

## C#

```
// C# program of the above approach
using System;
class GFG {

    // Function to find the length of
    // the longest subarray having its
    // sum in the given range [L, R]
    static int largestSubArraySum(int[] arr, int N, int L,
                                  int R)
    {
        // Store sum of current window
        int sum = 0;

        // Stores indices of current window
        int i = 0, j = 0;

        // Stores the maximum length
        int len = 0;

        // Calculating initial window
        while (sum < L && j < N) {
            sum += arr[j];
            j++;
        }

        // Loop to iterate over all windows
        // of having sum in range [L, R]
        while (i < N && j < N) {

            // If sum of window is less than L
            if (sum < L) {
                sum += arr[j];
                j++;
            }

            // If sum of window is more than R
            else if (sum > R) {
                sum -= arr[i];
                i++;
            }

            // If sum is in the range [L, R]
            else {

                // Update length
                len = Math.Max(len, j - i);
                sum += arr[j];
                j++;
            }
        }

        // Return Answer
        return len;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 15, 2, 4, 8, 9, 5, 10, 23 };
        int N = arr.Length;
        int L = 10, R = 23;

        Console.WriteLine(largestSubArraySum(arr, N, L, R));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
    // JavaScript program of the above approach

    // Function to find the length of
    // the longest subarray having its
    // sum in the given range [L, R]
    const largestSubArraySum = (arr, N, L, R) => {

        // Store sum of current window
        let sum = 0;

        // Stores indices of current window
        let i = 0, j = 0;

        // Stores the maximum length
        let len = 0;

        // Calculating initial window
        while (sum < L && j < N) {
            sum += arr[j];
            j++;
        }

        // Loop to iterate over all windows
        // of having sum in range [L, R]
        while (i < N && j < N) {

            // If sum of window is less than L
            if (sum < L) {
                sum += arr[j];
                j++;
            }

            // If sum of window is more than R
            else if (sum > R) {
                sum -= arr[i];
                i++;
            }

            // If sum is in the range [L, R]
            else {

                // Update length
                len = Math.max(len, j - i);
                sum += arr[j];
                j++;
            }
        }

        // Return Answer
        return len;
    }

    // Driver Code
    let arr = [15, 2, 4, 8, 9, 5, 10, 23];
    let N = arr.length;
    let L = 10, R = 23;

    document.write(largestSubArraySum(arr, N, L, R));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)