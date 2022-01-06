# 通过最多增加 K

来最大化具有相等元素的子阵列的长度

> 原文:[https://www . geeksforgeeks . org/通过最多添加 k 个元素来最大化子数组长度/](https://www.geeksforgeeks.org/maximize-length-of-subarray-having-equal-elements-by-adding-at-most-k/)

给定一个由 **N** 个正整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，该整数代表可以添加到数组元素中的最大数量。任务是通过最多增加 **K** 来最大化相等元素的最长可能子阵列的长度。

**示例:**

> **输入:** arr[] = {3，0，2，2，1}，k = 3
> **输出:** 4
> **解释:**
> 第一步:arr[1]加 2 将数组修改为{3，2，2，2，1}
> 第二步:arr[4]加 1 将数组修改为{3，2，2，2，2}
> 因此，答案将是 4 ({arr[1]，…，arr[4]})
> 
> **输入:** arr[] = {1，1，1}，k = 7
> **输出:** 3
> **说明:**
> 所有数组元素已经相等。因此，长度为 3。

**方法:**按照以下步骤解决问题:

*   [排序数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **arr[]** 。然后，使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)为具有相同元素的最大指数选择一个可能的值。
*   对于每个**pick _ value，**使用[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)技术检查是否可以使任何大小的子阵列**pick _ value**的所有元素相等。
*   最后，打印获得的最长可能长度的子阵列。

下面是上述方法的实现:

## C++14

```
// C++14 program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a subarray of
// length len consisting of equal elements
// can be obtained or not
bool check(vector<int> pSum, int len, int k,
           vector<int> a)
{

    // Sliding window
    int i = 0;
    int j = len;

    while (j <= a.size())
    {

        // Last element of the sliding window
        // will be having the max size in the
        // current window
        int maxSize = a[j - 1];

        int totalNumbers = maxSize * len;

        // The current number of element in all
        // indices of the current sliding window
        int currNumbers = pSum[j] - pSum[i];

        // If the current number of the window,
        // added to k exceeds totalNumbers
        if (currNumbers + k >= totalNumbers)
        {
            return true;
        }
        else
        {
            i++;
            j++;
        }
    }
    return false;
}

// Function to find the maximum number of
// indices having equal elements after
// adding at most k numbers
int maxEqualIdx(vector<int> arr, int k)
{

    // Sort the array in
    // ascending order
    sort(arr.begin(), arr.end());

    // Make prefix sum array
    vector<int> prefixSum(arr.size());
    prefixSum[1] = arr[0];

    for(int i = 1;
            i < prefixSum.size() - 1; ++i)
    {
        prefixSum[i + 1] = prefixSum[i] +
                                 arr[i];
    }

    // Initialize variables
    int max = arr.size();
    int min = 1;
    int ans = 1;

    while (min <= max)
    {

        // Update mid
        int mid = (max + min) / 2;

        // Check if any subarray
        // can be obtained of length
        // mid having equal elements
        if (check(prefixSum, mid, k, arr))
        {
            ans = mid;
            min = mid + 1;
        }
        else
        {

            // Decrease max to mid
            max = mid - 1;
        }
    }
    return ans;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 1, 1 };
    int k = 7;

    // Function call
    cout << (maxEqualIdx(arr, k));
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach

import java.util.*;

class GFG {

    // Function to find the maximum number of
    // indices having equal elements after
    // adding at most k numbers
    public static int maxEqualIdx(int[] arr,
                                  int k)
    {
        // Sort the array in
        // ascending order
        Arrays.sort(arr);

        // Make prefix sum array
        int[] prefixSum
            = new int[arr.length + 1];
        prefixSum[1] = arr[0];

        for (int i = 1; i < prefixSum.length - 1;
             ++i) {

            prefixSum[i + 1]
                = prefixSum[i] + arr[i];
        }

        // Initialize variables
        int max = arr.length;
        int min = 1;
        int ans = 1;

        while (min <= max) {

            // Update mid
            int mid = (max + min) / 2;

            // Check if any subarray
            // can be obtained of length
            // mid having equal elements
            if (check(prefixSum, mid, k, arr)) {

                ans = mid;
                min = mid + 1;
            }
            else {

                // Decrease max to mid
                max = mid - 1;
            }
        }

        return ans;
    }

    // Function to check if a subarray of
    // length len consisting of equal elements
    // can be obtained or not
    public static boolean check(int[] pSum,
                                int len, int k,
                                int[] a)
    {

        // Sliding window
        int i = 0;
        int j = len;
        while (j <= a.length) {

            // Last element of the sliding window
            // will be having the max size in the
            // current window
            int maxSize = a[j - 1];

            int totalNumbers = maxSize * len;

            // The current number of element in all
            // indices of the current sliding window
            int currNumbers = pSum[j] - pSum[i];

            // If the current number of the window,
            // added to k exceeds totalNumbers
            if (currNumbers + k >= totalNumbers) {

                return true;
            }
            else {
                i++;
                j++;
            }
        }
        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[] arr = { 1, 1, 1 };
        int k = 7;

        // Function call
        System.out.println(maxEqualIdx(arr, k));
    }
}
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to find the maximum number of
# indices having equal elements after
# adding at most k numbers
def maxEqualIdx(arr, k):

    # Sort the array in
    # ascending order
    arr.sort()

    # Make prefix sum array
    prefixSum = [0] * (len(arr) + 1)
    prefixSum[1] = arr[0]

    for i in range(1, len(prefixSum) - 1 ,1):
        prefixSum[i + 1] = prefixSum[i] + arr[i]

    # Initialize variables
    max = len(arr)
    min = 1
    ans = 1

    while (min <= max):

        # Update mid
        mid = (max + min) // 2

        # Check if any subarray
        # can be obtained of length
        # mid having equal elements
        if (check(prefixSum, mid, k, arr)):
            ans = mid
            min = mid + 1
        else:

            # Decrease max to mid
            max = mid - 1

    return ans

# Function to check if a subarray of
# length len consisting of equal elements
# can be obtained or not
def check(pSum, lenn, k, a):

    # Sliding window
    i = 0
    j = lenn

    while (j <= len(a)):

        # Last element of the sliding window
        # will be having the max size in the
        # current window
        maxSize = a[j - 1]

        totalNumbers = maxSize * lenn

        # The current number of element in all
        # indices of the current sliding window
        currNumbers = pSum[j] - pSum[i]

        # If the current number of the window,
        # added to k exceeds totalNumbers
        if (currNumbers + k >= totalNumbers):
            return True

        else:
            i += 1
            j += 1

    return False

# Driver Code

arr = [ 1, 1, 1 ]
k = 7

# Function call
print(maxEqualIdx(arr, k))

# This code is contributed by code_hunt
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to find the maximum number of
// indices having equal elements after
// adding at most k numbers
public static int maxEqualIdx(int[] arr,
                              int k)
{
  // Sort the array in
  // ascending order
  Array.Sort(arr);

  // Make prefix sum array
  int[] prefixSum = new int[arr.Length + 1];
  prefixSum[1] = arr[0];

  for (int i = 1;
           i < prefixSum.Length - 1; ++i)
  {
    prefixSum[i + 1] = prefixSum[i] + arr[i];
  }

  // Initialize variables
  int max = arr.Length;
  int min = 1;
  int ans = 1;

  while (min <= max)
  {
    // Update mid
    int mid = (max + min) / 2;

    // Check if any subarray
    // can be obtained of length
    // mid having equal elements
    if (check(prefixSum, mid, k, arr))
    {
      ans = mid;
      min = mid + 1;
    }
    else
    {
      // Decrease max to mid
      max = mid - 1;
    }
  }
  return ans;
}

// Function to check if a subarray of
// length len consisting of equal elements
// can be obtained or not
public static bool check(int[] pSum,
                         int len, int k,
                         int[] a)
{
  // Sliding window
  int i = 0;
  int j = len;
  while (j <= a.Length)
  {
    // Last element of the sliding window
    // will be having the max size in the
    // current window
    int maxSize = a[j - 1];

    int totalNumbers = maxSize * len;

    // The current number of element in all
    // indices of the current sliding window
    int currNumbers = pSum[j] - pSum[i];

    // If the current number of the window,
    // added to k exceeds totalNumbers
    if (currNumbers + k >= totalNumbers)
    {
      return true;
    }
    else
    {
      i++;
      j++;
    }
  }
  return false;
}

// Driver Code
public static void Main(String[] args)
{
  int[] arr = {1, 1, 1};
  int k = 7;

  // Function call
  Console.WriteLine(maxEqualIdx(arr, k));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to find the maximum number of
    // indices having equal elements after
    // adding at most k numbers
    function maxEqualIdx(arr, k)
    {
        // Sort the array in
        // ascending order
        arr.sort();

        // Make prefix sum array
        let prefixSum
            = new Array(arr.length + 1).fill(0);
        prefixSum[1] = arr[0];

        for (let i = 1; i < prefixSum.length - 1;
             ++i) {

            prefixSum[i + 1]
                = prefixSum[i] + arr[i];
        }

        // Initialize variables
        let max = arr.length;
        let min = 1;
        let ans = 1;

        while (min <= max) {

            // Update mid
            let mid = Math.floor((max + min) / 2);

            // Check if any subarray
            // can be obtained of length
            // mid having equal elements
            if (check(prefixSum, mid, k, arr)) {

                ans = mid;
                min = mid + 1;
            }
            else {

                // Decrease max to mid
                max = mid - 1;
            }
        }

        return ans;
    }

    // Function to check if a subarray of
    // length len consisting of equal elements
    // can be obtained or not
    function check(pSum, len, k, a)
    {

        // Sliding window
        let i = 0;
        let j = len;
        while (j <= a.length) {

            // Last element of the sliding window
            // will be having the max size in the
            // current window
            let maxSize = a[j - 1];

            let totalNumbers = maxSize * len;

            // The current number of element in all
            // indices of the current sliding window
            let currNumbers = pSum[j] - pSum[i];

            // If the current number of the window,
            // added to k exceeds totalNumbers
            if (currNumbers + k >= totalNumbers) {

                return true;
            }
            else {
                i++;
                j++;
            }
        }
        return false;
    }

// Driver Code

        let arr = [ 1, 1, 1 ];
        let k = 7;

        // Function call
        document.write(maxEqualIdx(arr, k));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*