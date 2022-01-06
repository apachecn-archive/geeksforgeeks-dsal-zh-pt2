# 最大化严格递增或递减子阵列的乘积

> 原文:[https://www . geeksforgeeks . org/最大化严格递增或递减子阵列的乘积/](https://www.geeksforgeeks.org/maximize-product-of-a-strictly-increasing-or-decreasing-subarray/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是从由严格递增或递减顺序的元素组成的任何子数组中找到[最大乘积](https://www.geeksforgeeks.org/maximum-product-subarray/)。

**示例:**

> **输入:** arr[] = { 1，2，10，8，1，100，101 }
> **输出:** 10100
> **说明:**
> 最大乘积递增子阵为{ 1，100，101 }。
> 因此，所需输出为 1 * 100 * 101。
> 
> **输入:** arr[] = { 1，5，7，2，10，12 }
> T3】输出: 240

**天真方法:**解决这个问题最简单的方法是[从给定的阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)中生成所有可能的子阵列。对于每个子阵列，检查子阵列中的元素是否严格按照递增或递减的顺序排列。如果发现是真的，那么计算子阵元素的乘积。最后，打印获得的最大产品。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法**上述方法可以通过[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)进行优化，对于给定数组中每增加或减少一个子数组，使用[卡丹算法](https://www.geeksforgeeks.org/maximum-product-subarray/)找到最大乘积。最后，打印增加或减少子阵列的所有产品的最大值。按照以下步骤解决问题:

*   初始化一个变量，比如 **maxProd** ，以存储给定数组中递增或递减子数组的最大可能乘积。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)计算[最长递增或递减子阵](https://www.geeksforgeeks.org/longest-increasing-subarray/)，比如**子阵【】**，其起始索引为 **i** 。
*   使用[卡丹算法对产品](https://www.geeksforgeeks.org/maximum-product-subarray/)计算**子阵**的最大乘积，比如 **ProdSub** ，更新 **maxProd = max(maxProd，ProdSub)** 。
*   最后，打印数值 **maxProd** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum product of
// subarray in the array, arr[]
int maxSubarrayProduct(vector<int> arr, int n)
{

    // Maximum positive product
    // ending at the i-th index
    int max_ending_here = 1;

    // Minimum negative product ending
    // at the current index
    int min_ending_here = 1;

    // Maximum product up to
    // i-th index
    int max_so_far = 0;

    // Check if an array element
    // is positive or not
    int flag = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If current element
        // is positive
        if (arr[i] > 0) {

            // Update max_ending_here
            max_ending_here
                = max_ending_here * arr[i];

            // Update min_ending_here
            min_ending_here
                = min(min_ending_here * arr[i], 1);

            // Update flag
            flag = 1;
        }

        // If current element is 0, reset
        // the start index of subarray
        else if (arr[i] == 0) {

            // Update max_ending_here
            max_ending_here = 1;

            // Update min_ending_here
            min_ending_here = 1;
        }

        // If current element is negative
        else {

            // Stores max_ending_here
            int temp = max_ending_here;

            // Update max_ending_here
            max_ending_here
                = max(min_ending_here * arr[i], 1);

            // Update min_ending_here
            min_ending_here = temp * arr[i];
        }

        // Update max_so_far, if needed
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;
    }

    // If no array elements is positive
    // and max_so_far is 0
    if (flag == 0 && max_so_far == 0)
        return 0;
    return max_so_far;
}

// Function to find the maximum product of either
// increasing subarray or the decreasing subarray
int findMaxProduct(int* a, int n)
{

    // Stores start index of either increasing
    // subarray or the decreasing subarray
    int i = 0;

    // Initially assume maxProd to be 1
    int maxProd = -1e9;

    // Traverse the array
    while (i < n) {

        // Store the longest either increasing
        // subarray or the decreasing subarray
        // whose start index is i
        vector<int> v;

        v.push_back(a[i]);

        // Check for increasing subarray
        if (i < n - 1 && a[i] < a[i + 1]) {

            // Insert elements of
            // increasing subarray
            while (i < n - 1 && a[i] < a[i + 1]) {
                v.push_back(a[i + 1]);
                i += 1;
            }
        }

        // Check for decreasing subarray
        else if (i < n - 1 && a[i] > a[i + 1]) {

            // Insert elements of
            // decreasing subarray
            while (i < n - 1 && a[i] > a[i + 1]) {
                v.push_back(a[i + 1]);
                i += 1;
            }
        }

        // Stores maximum subarray product of
        // current increasing or decreasing
        // subarray
        int prod = maxSubarrayProduct(v, v.size());

        // Update maxProd
        maxProd = max(maxProd, prod);

        // Update i
        i++;
    }

    // Finally print maxProd
    return maxProd;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 10, 8, 1, 100, 101 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << findMaxProduct(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

  // Function to find the maximum product of
  // subarray in the array, arr[]
  static int maxSubarrayProduct(Vector<Integer> arr, int n)
  {

    // Maximum positive product
    // ending at the i-th index
    int max_ending_here = 1;

    // Minimum negative product ending
    // at the current index
    int min_ending_here = 1;

    // Maximum product up to
    // i-th index
    int max_so_far = 0;

    // Check if an array element
    // is positive or not
    int flag = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

      // If current element
      // is positive
      if (arr.get(i) > 0)
      {

        // Update max_ending_here
        max_ending_here
          = max_ending_here * arr.get(i);

        // Update min_ending_here
        min_ending_here
          = Math.min(min_ending_here * arr.get(i), 1);

        // Update flag
        flag = 1;
      }

      // If current element is 0, reset
      // the start index of subarray
      else if (arr.get(i) == 0)
      {

        // Update max_ending_here
        max_ending_here = 1;

        // Update min_ending_here
        min_ending_here = 1;
      }

      // If current element is negative
      else
      {

        // Stores max_ending_here
        int temp = max_ending_here;

        // Update max_ending_here
        max_ending_here
          = Math.max(min_ending_here * arr.get(i), 1);

        // Update min_ending_here
        min_ending_here = temp * arr.get(i);
      }

      // Update max_so_far, if needed
      if (max_so_far < max_ending_here)
        max_so_far = max_ending_here;
    }

    // If no array elements is positive
    // and max_so_far is 0
    if (flag == 0 && max_so_far == 0)
      return 0;
    return max_so_far;
  }

  // Function to find the maximum product of either
  // increasing subarray or the decreasing subarray
  static int findMaxProduct(int[] a, int n)
  {

    // Stores start index of either increasing
    // subarray or the decreasing subarray
    int i = 0;

    // Initially assume maxProd to be 1
    int maxProd = 1;

    // Traverse the array
    while (i < n) {

      // Store the longest either increasing
      // subarray or the decreasing subarray
      // whose start index is i
      Vector<Integer> v = new Vector<>();

      v.add(a[i]);

      // Check for increasing subarray
      if (i < n - 1 && a[i] < a[i + 1]) {

        // Insert elements of
        // increasing subarray
        while (i < n - 1 && a[i] < a[i + 1]) {
          v.add(a[i + 1]);
          i += 1;
        }
      }

      // Check for decreasing subarray
      else if (i < n - 1 && a[i] > a[i + 1]) {

        // Insert elements of
        // decreasing subarray
        while (i < n - 1 && a[i] > a[i + 1]) {
          v.add(a[i + 1]);
          i += 1;
        }
      }

      // Stores maximum subarray product of
      // current increasing or decreasing
      // subarray
      int prod = maxSubarrayProduct(v, v.size());

      // Update maxProd
      maxProd = Math.max(maxProd, prod);

      // Update i
      i++;
    }

    // Finally print maxProd
    return maxProd;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 1, 2, 10, 8, 1, 100, 101 };
    int N = arr.length;

    System.out.print(findMaxProduct(arr, N));
  }
}

// This code contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum product
# of subarray in the array, arr[]
def maxSubarrayProduct(arr, n):

    # Maximum positive product
    # ending at the i-th index
    max_ending_here = 1

    # Minimum negative product ending
    # at the current index
    min_ending_here = 1

    # Maximum product up to
    # i-th index
    max_so_far = 0

    # Check if an array element
    # is positive or not
    flag = 0

    # Traverse the array
    for i in range(n):

        # If current element
        # is positive
        if (arr[i] > 0):

            # Update max_ending_here
            max_ending_here = max_ending_here * arr[i]

            # Update min_ending_here
            min_ending_here = min(
                min_ending_here * arr[i], 1)

            # Update flag
            flag = 1

        # If current element is 0, reset
        # the start index of subarray
        elif (arr[i] == 0):

            # Update max_ending_here
            max_ending_here = 1

            # Update min_ending_here
            min_ending_here = 1

        # If current element is negative
        else:

            # Stores max_ending_here
            temp = max_ending_here

            # Update max_ending_here
            max_ending_here = max(
                min_ending_here * arr[i], 1)

            # Update min_ending_here
            min_ending_here = temp * arr[i]

        # Update max_so_far, if needed
        if (max_so_far < max_ending_here):
            max_so_far = max_ending_here

    # If no array elements is positive
    # and max_so_far is 0
    if (flag == 0 and max_so_far == 0):
        return 0

    return max_so_far

# Function to find the maximum product
# of either increasing subarray or the
# decreasing subarray
def findMaxProduct(a, n):

    # Stores start index of either
    # increasing subarray or the
    # decreasing subarray
    i = 0

    # Initially assume maxProd to be 1
    maxProd = -10**9

    # Traverse the array
    while (i < n):

        # Store the longest either increasing
        # subarray or the decreasing subarray
        # whose start index is i
        v = []

        v.append(a[i])

        # Check for increasing subarray
        if i < n - 1 and a[i] < a[i + 1]:

            # Insert elements of
            # increasing subarray
            while (i < n - 1 and a[i] < a[i + 1]):
                v.append(a[i + 1])
                i += 1

        # Check for decreasing subarray
        elif (i < n - 1 and a[i] > a[i + 1]):

            # Insert elements of
            # decreasing subarray
            while (i < n - 1 and a[i] > a[i + 1]):
                v.append(a[i + 1])
                i += 1

        # Stores maximum subarray product of
        # current increasing or decreasing
        # subarray
        prod = maxSubarrayProduct(v, len(v))

        # Update maxProd
        maxProd = max(maxProd, prod)

        # Update i
        i += 1

    # Finally prmaxProd
    return maxProd

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 10, 8, 1, 100, 101 ]
    N = len(arr)

    print (findMaxProduct(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

public class GFG
{

  // Function to find the maximum product of
  // subarray in the array, []arr
  static int maxSubarrayProduct(List<int> arr, int n)
  {

    // Maximum positive product
    // ending at the i-th index
    int max_ending_here = 1;

    // Minimum negative product ending
    // at the current index
    int min_ending_here = 1;

    // Maximum product up to
    // i-th index
    int max_so_far = 0;

    // Check if an array element
    // is positive or not
    int flag = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

      // If current element
      // is positive
      if (arr[i] > 0)
      {

        // Update max_ending_here
        max_ending_here
          = max_ending_here * arr[i];

        // Update min_ending_here
        min_ending_here
          = Math.Min(min_ending_here * arr[i], 1);

        // Update flag
        flag = 1;
      }

      // If current element is 0, reset
      // the start index of subarray
      else if (arr[i] == 0)
      {

        // Update max_ending_here
        max_ending_here = 1;

        // Update min_ending_here
        min_ending_here = 1;
      }

      // If current element is negative
      else
      {

        // Stores max_ending_here
        int temp = max_ending_here;

        // Update max_ending_here
        max_ending_here
          = Math.Max(min_ending_here * arr[i], 1);

        // Update min_ending_here
        min_ending_here = temp * arr[i];
      }

      // Update max_so_far, if needed
      if (max_so_far < max_ending_here)
        max_so_far = max_ending_here;
    }

    // If no array elements is positive
    // and max_so_far is 0
    if (flag == 0 && max_so_far == 0)
      return 0;
    return max_so_far;
  }

  // Function to find the maximum product of either
  // increasing subarray or the decreasing subarray
  static int findMaxProduct(int[] a, int n)
  {

    // Stores start index of either increasing
    // subarray or the decreasing subarray
    int i = 0;

    // Initially assume maxProd to be 1
    int maxProd = 1;

    // Traverse the array
    while (i < n) {

      // Store the longest either increasing
      // subarray or the decreasing subarray
      // whose start index is i
      List<int> v = new List<int>();

      v.Add(a[i]);

      // Check for increasing subarray
      if (i < n - 1 && a[i] < a[i + 1]) {

        // Insert elements of
        // increasing subarray
        while (i < n - 1 && a[i] < a[i + 1]) {
          v.Add(a[i + 1]);
          i += 1;
        }
      }

      // Check for decreasing subarray
      else if (i < n - 1 && a[i] > a[i + 1]) {

        // Insert elements of
        // decreasing subarray
        while (i < n - 1 && a[i] > a[i + 1]) {
          v.Add(a[i + 1]);
          i += 1;
        }
      }

      // Stores maximum subarray product of
      // current increasing or decreasing
      // subarray
      int prod = maxSubarrayProduct(v, v.Count);

      // Update maxProd
      maxProd = Math.Max(maxProd, prod);

      // Update i
      i++;
    }

    // Finally print maxProd
    return maxProd;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 1, 2, 10, 8, 1, 100, 101 };
    int N = arr.Length;

    Console.Write(findMaxProduct(arr, N));
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
//Javascript program for the above approach

// Function to find the maximum product of
// subarray in the array, arr[]
function maxSubarrayProduct(arr, n)
{

    // Maximum positive product
    // ending at the i-th index
    var max_ending_here = 1;

    // Minimum negative product ending
    // at the current index
    var min_ending_here = 1;

    // Maximum product up to
    // i-th index
    var max_so_far = 0;

    // Check if an array element
    // is positive or not
    var flag = 0;

    // Traverse the array
    for (var i = 0; i < n; i++) {

        // If current element
        // is positive
        if (arr[i] > 0) {

            // Update max_ending_here
            max_ending_here
                = max_ending_here * arr[i];

            // Update min_ending_here
            min_ending_here
                = Math.min(min_ending_here * arr[i], 1);

            // Update flag
            flag = 1;
        }

        // If current element is 0, reset
        // the start index of subarray
        else if (arr[i] == 0) {

            // Update max_ending_here
            max_ending_here = 1;

            // Update min_ending_here
            min_ending_here = 1;
        }

        // If current element is negative
        else {

            // Stores max_ending_here
            var temp = max_ending_here;

            // Update max_ending_here
            max_ending_here
                = Math.max(min_ending_here * arr[i], 1);

            // Update min_ending_here
            min_ending_here = temp * arr[i];
        }

        // Update max_so_far, if needed
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;
    }

    // If no array elements is positive
    // and max_so_far is 0
    if (flag == 0 && max_so_far == 0)
        return 0;
    return max_so_far;
}

// Function to find the maximum product of either
// increasing subarray or the decreasing subarray
function findMaxProduct(a, n)
{

    // Stores start index of either increasing
    // subarray or the decreasing subarray
    var i = 0;

    // Initially assume maxProd to be 1
    var maxProd = -1e9;

    // Traverse the array
    while (i < n) {

        // Store the longest either increasing
        // subarray or the decreasing subarray
        // whose start index is i
        var v=[];

        v.push(a[i]);

        // Check for increasing subarray
        if (i < n - 1 && a[i] < a[i + 1]) {

            // Insert elements of
            // increasing subarray
            while (i < n - 1 && a[i] < a[i + 1]) {
                v.push(a[i + 1]);
                i += 1;
            }
        }

        // Check for decreasing subarray
        else if (i < n - 1 && a[i] > a[i + 1]) {

            // Insert elements of
            // decreasing subarray
            while (i < n - 1 && a[i] > a[i + 1]) {
                v.push(a[i + 1]);
                i += 1;
            }
        }

        // Stores maximum subarray product of
        // current increasing or decreasing
        // subarray
        var prod = maxSubarrayProduct(v, v.length);

        // Update maxProd
        maxProd = Math.max(maxProd, prod);

        // Update i
        i++;
    }

    // Finally print maxProd
    return maxProd;
}

    var arr = [ 1, 2, 10, 8, 1, 100, 101 ];
    var N = arr.length;
    document.write(findMaxProduct(arr, N));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
10100
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)