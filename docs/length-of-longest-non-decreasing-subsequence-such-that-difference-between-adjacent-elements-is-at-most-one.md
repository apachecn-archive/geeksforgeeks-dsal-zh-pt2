# 最长非递减子序列的长度，使得相邻元素之间的差最多为一个

> 原文:[https://www . geeksforgeeks . org/最长非递减子序列长度，使得相邻元素之间的差值最多为 1/](https://www.geeksforgeeks.org/length-of-longest-non-decreasing-subsequence-such-that-difference-between-adjacent-elements-is-at-most-one/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到最长的非递减子序列的长度，使得相邻元素之间的差最多为 **1** 。

**示例:**

> **输入:** arr[] = {8，5，4，8，4}
> **输出:** 3
> **解释:** {4，4，5}，{8，8}分别是长度为 2 和 3 的两个这样的非递减子序列。因此，两个子序列中最长的长度是 3。
> 
> **输入:** arr[] = {4，13，2，3}
> **输出:** 3
> **解释:** {2，3，4}，{13}分别是长度为 3 和 1 的两个这样的非递减子序列。因此，两个子序列中最长的长度是 3。

**接近**:按照以下步骤解决问题:

*   [按递增顺序排列数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)[【arr】](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   初始化一个变量，比如 **maxLen = 1，**来存储一个子序列的最大可能长度。初始化另一个变量，比如说 **len = 1** 来存储每个子序列的当前长度。
*   [用指针 **i** 遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)**arr【】**，对于每个元素:
    *   检查**ABS(arr[I]–arr[I–1])是否≤ 1** 。如果发现为真，则将**镜头**增加 **1** 。更新 **maxLen = max(maxLen，len)** 。
    *   否则，设置 **len = 1** ，即开始一个新的子序列。
*   打印 **maxLen** 的值作为最终答案。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the longest non-decreasing
// subsequence with difference between
// adjacent elements exactly equal to 1
void longestSequence(int arr[], int N)
{
  // Base case
  if (N == 0) {
    cout << 0;
    return;
  }

  // Sort the array in ascending order
  sort(arr, arr+N);

  // Stores the maximum length
  int maxLen = 1;

  int len = 1;

  // Traverse the array
  for (int i = 1; i < N; i++) {

    // If difference between current
    // pair of adjacent elements is 1 or 0
    if (arr[i] == arr[i - 1]
        || arr[i] == arr[i - 1] + 1) {
      len++;

      // Extend the current sequence
      // Update len and max_len
      maxLen = max(maxLen, len);
    }
    else {

      // Otherwise, start a new subsequence
      len = 1;
    }
  }

  // Print the maximum length
  cout << maxLen;
}

// Driver Code
int main()
{

  // Given array
  int arr[] = { 8, 5, 4, 8, 4 };

  // Size of the array
  int N = sizeof(arr) / sizeof(arr[0]);

  // Function call to find the longest
  // subsequence
  longestSequence(arr, N);

  return 0;
}

// This code is contributed by code_hunt.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;
class GFG {

    // Function to find the longest non-decreasing
    // subsequence with difference between
    // adjacent elements exactly equal to 1
    static void longestSequence(int arr[], int N)
    {
        // Base case
        if (N == 0) {
            System.out.println(0);
            return;
        }

        // Sort the array in ascending order
        Arrays.sort(arr);

        // Stores the maximum length
        int maxLen = 1;

        int len = 1;

        // Traverse the array
        for (int i = 1; i < N; i++) {

            // If difference between current
            // pair of adjacent elements is 1 or 0
            if (arr[i] == arr[i - 1]
                || arr[i] == arr[i - 1] + 1) {
                len++;

                // Extend the current sequence
                // Update len and max_len
                maxLen = Math.max(maxLen, len);
            }
            else {

                // Otherwise, start a new subsequence
                len = 1;
            }
        }

        // Print the maximum length
        System.out.println(maxLen);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array
        int arr[] = { 8, 5, 4, 8, 4 };

        // Size of the array
        int N = arr.length;

        // Function call to find the longest
        // subsequence
        longestSequence(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the longest non-decreasing
# subsequence with difference between
# adjacent elements exactly equal to 1
def longestSequence(arr, N):

    # Base case
    if (N == 0):
        print(0);
        return;

    # Sort the array in ascending order
    arr.sort();

    # Stores the maximum length
    maxLen = 1;
    len = 1;

    # Traverse the array
    for i in range(1,N):

        # If difference between current
        # pair of adjacent elements is 1 or 0
        if (arr[i] == arr[i - 1] or arr[i] == arr[i - 1] + 1):
            len += 1;

            # Extend the current sequence
            # Update len and max_len
            maxLen = max(maxLen, len);
        else:

            # Otherwise, start a new subsequence
            len = 1;

    # Print the maximum length
    print(maxLen);

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [8, 5, 4, 8, 4];

    # Size of the array
    N = len(arr);

    # Function call to find the longest
    # subsequence
    longestSequence(arr, N);

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to find the longest non-decreasing
  // subsequence with difference between
  // adjacent elements exactly equal to 1
  static void longestSequence(int []arr, int N)
  {

    // Base case
    if (N == 0)
    {
      Console.WriteLine(0);
      return;
    }

    // Sort the array in ascending order
    Array.Sort(arr);

    // Stores the maximum length
    int maxLen = 1;
    int len = 1;

    // Traverse the array
    for (int i = 1; i < N; i++) {

      // If difference between current
      // pair of adjacent elements is 1 or 0
      if (arr[i] == arr[i - 1]
          || arr[i] == arr[i - 1] + 1) {
        len++;

        // Extend the current sequence
        // Update len and max_len
        maxLen = Math.Max(maxLen, len);
      }
      else {

        // Otherwise, start a new subsequence
        len = 1;
      }
    }

    // Print the maximum length
    Console.WriteLine(maxLen);
  }

  // Driver Code
  public static void Main(string[] args)
  {

    // Given array
    int []arr = { 8, 5, 4, 8, 4 };

    // Size of the array
    int N = arr.Length;

    // Function call to find the longest
    // subsequence
    longestSequence(arr, N);
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the longest non-decreasing
// subsequence with difference between
// adjacent elements exactly equal to 1
function longestSequence(arr, N)
{
  // Base case
  if (N == 0) {
    document.write(0);
    return;
  }

  // Sort the array in ascending order
  arr.sort();

  // Stores the maximum length
  var maxLen = 1;

  var len = 1;
   var i;
  // Traverse the array
  for (i = 1; i < N; i++) {

    // If difference between current
    // pair of adjacent elements is 1 or 0
    if (arr[i] == arr[i - 1]
        || arr[i] == arr[i - 1] + 1) {
      len++;

      // Extend the current sequence
      // Update len and max_len
      maxLen = Math.max(maxLen, len);
    }
    else {

      // Otherwise, start a new subsequence
      len = 1;
    }
  }

  // Print the maximum length
  document.write(maxLen);
}

// Driver Code
  // Given array
  var arr = [8, 5, 4, 8, 4];

  // Size of the array
  var N = arr.length;

  // Function call to find the longest
  // subsequence
  longestSequence(arr, N);

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N * logN)*
***辅助空间:** O(1)*