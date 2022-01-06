# 任意两个元素的绝对差不大于 X 的最长子阵

> 原文:[https://www . geesforgeks . org/最长子数组任意两个元素的绝对差值不大于 x/](https://www.geeksforgeeks.org/longest-subarray-in-which-absolute-difference-between-any-two-element-is-not-greater-than-x/)

给定一个大小为 **N** 的整数数组 **arr[]** 和一个整数 **X** ，任务是找到任意两个元素之间的绝对差不大于 **X** 的最长子数组。
**举例:**

> **输入:** arr = { 8，4，2，6，7 }，X = 4
> **输出:** 4 2 6
> **解释:**
> 由索引[1，3]描述的子数组，即{ 4，2，6 }不包含大于 4 的两个元素的差异。
> **输入:** arr = { 15，10，1，2，4，7，2}，X = 5
> **输出:** 2 4 7 2
> **解释:**
> 由索引[3，6]即{ 2，4，7，2 }描述的子数组不包含大于 5 的两个元素的这种差异。

**天真方法:**简单的解决方法是逐个考虑所有子阵列，找到该子阵列的最大和最小元素，检查它们的差值是否不大于 **X** 。在所有这样的子阵列中，打印最长的子阵列。
***时间复杂度:** O(N <sup>3</sup> )*
**高效方法:**思路是使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)考虑一个子数组，使用[映射数据结构](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)找到该子数组中的最大和最小元素。

*   首先窗口的**开始**和**结束**指向**第 0 个**指标。
*   在每次迭代中，如果在**结束**的元素还没有出现，则将其插入到地图中，否则其计数会增加。
*   如果最大和最小元素之差不大于 **X** ，则更新所需子数组的最大长度，并将该子数组的开头存储在变量中。
*   否则，增加窗口的**开始**，直到最大和最小元素之差不大于 **X** 。
*   当增加**开始**时，窗口的大小减小，当且仅当元素的计数变为零时，从地图中移除**开始**处的元素。

最后打印长度最长的子数组，任意两个元素的绝对差值不大于 **X** 。
以下是上述办法的实施情况:

## C++

```
// C++ program to find the longest sub-array
// where the absolute difference between any
// two elements is not greater than X

#include <bits/stdc++.h>
using namespace std;

// Function that prints the longest sub-array
// where the absolute difference between any
// two element is not greater than X
void longestSubarray(int* A, int N, int X)
{
    // Initialize a variable to store
    // length of longest sub-array
    int maxLen = 0;

    // Initialize a variable to store the
    // beginning of the longest sub-array
    int beginning = 0;

    // Initialize a map to store the maximum
    // and the minimum elements for a given window
    map<int, int> window;

    // Initialize the window
    int start = 0, end = 0;

    // Loop througth the array
    for (; end < N; end++) {
        // Increment the count of that
        // element in the window
        window[A[end]]++;

        // Find the maximum and minimum element
        // in the current window
        auto minimum = window.begin()->first;
        auto maximum = window.rbegin()->first;

        // If the difference is not
        // greater than X
        if (maximum - minimum <= X) {
            // Update the length of the longest
            // sub-array and store the beginning
            // of the sub-array
            if (maxLen < end - start + 1) {
                maxLen = end - start + 1;
                beginning = start;
            }
        }
        // Decrease the size of the window
        else {
            while (start < end) {
                // Remove the element at start
                window[A[start]]--;

                // Remove the element from the window
                // if its count is zero
                if (window[A[start]] == 0) {

                    window.erase(window.find(A[start]));
                }
                // Increment the start of the window
                start++;

                // Find the maximum and minimum element
                // in the current window
                auto minimum = window.begin()->first;
                auto maximum = window.rbegin()->first;

                // Stop decreasing the size of window
                // when difference is not greater
                if (maximum - minimum <= X)
                    break;
            }
        }
    }

    // Print the longest sub-array
    for (int i = beginning; i < beginning + maxLen; i++)
        cout << A[i] << " ";
}

// Driver Code
int main()
{
    int arr[] = { 15, 10, 1, 2, 4, 7, 2 }, X = 5;

    int n = sizeof(arr) / sizeof(arr[0]);

    longestSubarray(arr, n, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find the longest sub-array
// where the absolute difference between any
// two elements is not greater than X
import java.io.*;
import java.lang.*;
import java.util.*;
class GFG
{

  // Function that prints the longest sub-array
  // where the absolute difference between any
  // two element is not greater than X
  static void longestSubarray(int A[], int N, int X)
  {

    // Initialize a variable to store
    // length of longest sub-array
    int maxLen = 0;

    // Initialize a variable to store the
    // beginning of the longest sub-array
    int beginning = 0;

    // Initialize a map to store the maximum
    // and the minimum elements for a given window
    TreeMap<Integer, Integer> window = new TreeMap<>();

    // Initialize the window
    int start = 0, end = 0;

    // Loop througth the array
    for (; end < N; end++)
    {

      // Increment the count of that
      // element in the window
      window.put(A[end],
                 window.getOrDefault(A[end], 0) + 1);

      // Find the maximum and minimum element
      // in the current window
      int minimum = window.firstKey();
      int maximum = window.lastKey();

      // If the difference is not
      // greater than X
      if (maximum - minimum <= X)
      {

        // Update the length of the longest
        // sub-array and store the beginning
        // of the sub-array
        if (maxLen < end - start + 1) {
          maxLen = end - start + 1;
          beginning = start;
        }
      }

      // Decrease the size of the window
      else {
        while (start < end)
        {

          // Remove the element at start
          window.put(A[start],
                     window.get(A[start]) - 1);

          // Remove the element from the window
          // if its count is zero
          if (window.get(A[start]) == 0) {

            window.remove(A[start]);
          }

          // Increment the start of the window
          start++;

          // Find the maximum and minimum element
          // in the current window
          minimum = window.firstKey();
          maximum = window.lastKey();

          // Stop decreasing the size of window
          // when difference is not greater
          if (maximum - minimum <= X)
            break;
        }
      }
    }

    // Print the longest sub-array
    for (int i = beginning; i < beginning + maxLen; i++)
      System.out.print(A[i] + " ");
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given array
    int arr[] = { 15, 10, 1, 2, 4, 7, 2 }, X = 5;

    // store the size of the array
    int n = arr.length;

    // Function call
    longestSubarray(arr, n, X);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program to find the longest sub-array
# where the absolute difference between any
# two elements is not greater than X

# Function that prints the longest sub-array
# where the absolute difference between any
# two element is not greater than X
def longestSubarray(A, N, X):

    # Initialize a variable to store
    # length of longest sub-array
    maxLen = 0

    # Initialize a variable to store the
    # beginning of the longest sub-array
    beginning = 0

    # Initialize a map to store the maximum
    # and the minimum elements for a given window
    window = {}

    # Initialize the window
    start = 0

    # Loop througth the array
    for end in range(N):

        # Increment the count of that
        # element in the window
        if A[end] in window:
            window[A[end]] += 1
        else:
            window[A[end]] = 1

        # Find the maximum and minimum element
        # in the current window
        minimum = min(list(window.keys()))
        maximum = max(list(window.keys()))

        # If the difference is not
        # greater than X
        if maximum - minimum <= X:

            # Update the length of the longest
            # sub-array and store the beginning
            # of the sub-array
            if maxLen < end - start + 1:
                maxLen = end - start + 1
                beginning = start

        # Decrease the size of the window
        else:
            while start < end:

                # Remove the element at start
                window[A[start]] -= 1

                # Remove the element from the window
                # if its count is zero
                if window[A[start]] == 0:
                    window.pop(A[start])

                # Increment the start of the window
                start += 1

                # Find the maximum and minimum element
                # in the current window
                minimum = min(list(window.keys()))
                maximum = max(list(window.keys()))

                # Stop decreasing the size of window
                # when difference is not greater
                if maximum - minimum <= X:
                    break

    # Print the longest sub-array
    for i in range(beginning, beginning + maxLen):
        print(A[i], end = ' ')

# Driver Code
arr = [15, 10, 1, 2, 4, 7, 2]
X = 5
n = len(arr)
longestSubarray(arr, n, X)

# This code is contributed by Shivam Singh
```

**Output:** 

```
2 4 7 2
```

***时间复杂度:** O(N * log(N))*