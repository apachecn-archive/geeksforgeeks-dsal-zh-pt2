# 和不能被整数 K 整除的最长子阵列的长度

> 原文:[https://www . geesforgeks . org/最长子数组长度-其和不能被整数 k 整除/](https://www.geeksforgeeks.org/length-of-longest-subarray-whose-sum-is-not-divisible-by-integer-k/)

给定一个大小为 N 的**数组 arr[]** 和一个**整数 k** ，我们的任务是找到元素之和不能被 k 整除的最长子数组的长度。如果不存在这样的子数组，那么返回-1。
**例:**

> **输入:** arr[] = {8，4，3，1，5，9，2}，k = 2
> **输出:** 5
> **解释:**
> 子阵为{8，4，3，1，5}，和= 21，不能被 2 整除。
> **输入:** arr[] = {6，3，12，15}，k = 3
> **输出:** -1
> **说明:**
> 没有不能被 3 整除的子数组。

**天真方法:**想法是考虑所有子阵，返回最长子阵的长度，使得其元素之和不能被 **k** 整除。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*
**高效方法:**主要观察结果是移除一个可被 k 整除的元素不会有助于解决问题，但是如果我们移除一个不可被 k 整除的元素**，那么总和将不能被 k 整除**

*   因此，让 *k* 最左边的非倍数位于索引**左侧**，让 *k* 最右边的非倍数位于索引**右侧**。
*   删除直到索引**左侧**的前缀元素，或者直到索引**右侧**的后缀元素，并删除元素数量较少的元素。
*   这个问题有**两个角例**。首先，如果数组的每个元素都可以被 k 整除，那么就不存在这样的子数组，所以返回-1。其次，如果整个数组的某些部分不能被 k 整除，那么子数组将是数组本身，所以返回数组的大小。

以下是上述方法的实现:

## C++

```
// C++ Program to find the length of
// the longest subarray whose sum is
// not divisible by integer K

#include <bits/stdc++.h>
using namespace std;

// Function to find the longest subarray
// with sum is not divisible by k
int MaxSubarrayLength(int arr[], int n, int k)
{
    // left is the index of the
    // leftmost element that is
    // not divisible by k
    int left = -1;

    // right is the index of the
    // rightmost element that is
    // not divisible by k
    int right;

    // sum of the array
    int sum = 0;

    for (int i = 0; i < n; i++) {

        // Find the element that
        // is not multiple of k
        if ((arr[i] % k) != 0) {

            // left = -1 means we are
            // finding the leftmost
            // element that is not
            // divisible by k
            if (left == -1) {
                left = i;
            }

            // Updating the
            // rightmost element
            right = i;
        }

        // update the sum of the
        // array up to the index i
        sum += arr[i];
    }

    // Check if the sum of the
    // array is not divisible
    // by k, then return the
    // size of array
    if ((sum % k) != 0) {
        return n;
    }

    // All elements of array
    // are divisible by k,
    // then no such subarray
    // possible so return -1
    else if (left == -1) {
        return -1;
    }

    else {
        // length of prefix elements
        // that can be removed
        int prefix_length = left + 1;

        // length of suffix elements
        // that can be removed
        int suffix_length = n - right;

        // Return the length of
        // subarray after removing
        // the elements which have
        // lesser number of elements
        return n - min(prefix_length,
                       suffix_length);
    }
}

// Driver Code
int main()
{

    int arr[] = { 6, 3, 12, 15 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int K = 3;

    cout << MaxSubarrayLength(arr, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of
// the longest subarray whose sum is
// not divisible by integer K
import java.util.*;

class GFG{

// Function to find the longest subarray
// with sum is not divisible by k
static int MaxSubarrayLength(int arr[], int n,
                                        int k)
{

    // left is the index of the
    // leftmost element that is
    // not divisible by k
    int left = -1;

    // right is the index of the
    // rightmost element that is
    // not divisible by k
    int right = 0;

    // sum of the array
    int sum = 0;

    for(int i = 0; i < n; i++)
    {

        // Find the element that
        // is not multiple of k
        if ((arr[i] % k) != 0)
        {

            // left = -1 means we are
            // finding the leftmost
            // element that is not
            // divisible by k
            if (left == -1)
            {
                left = i;
            }

            // Updating the
            // rightmost element
            right = i;
        }

        // Update the sum of the
        // array up to the index i
        sum += arr[i];
    }

    // Check if the sum of the
    // array is not divisible
    // by k, then return the
    // size of array
    if ((sum % k) != 0)
    {
        return n;
    }

    // All elements of array
    // are divisible by k,
    // then no such subarray
    // possible so return -1
    else if (left == -1)
    {
        return -1;
    }
    else
    {

        // Length of prefix elements
        // that can be removed
        int prefix_length = left + 1;

        // Length of suffix elements
        // that can be removed
        int suffix_length = n - right;

        // Return the length of
        // subarray after removing
        // the elements which have
        // lesser number of elements
        return n - Math.min(prefix_length,
                            suffix_length);
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 6, 3, 12, 15 };
    int n = arr.length;
    int K = 3;

    System.out.println(MaxSubarrayLength(arr, n, K));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the length of
# the longest subarray whose sum is
# not divisible by integer

# Function to find the longest subarray
# with sum is not divisible by k
def MaxSubarrayLength(arr, n, k):

    # left is the index of the
    # leftmost element that is
    # not divisible by k
    left = -1

    # sum of the array
    sum = 0

    for i in range(n):

        # Find the element that
        # is not multiple of k
        if ((arr[i] % k) != 0):

            # left = -1 means we are
            # finding the leftmost
            # element that is not
            # divisible by k
            if (left == -1):
                left = i

            # Updating the
            # rightmost element
            right = i

        # Update the sum of the
        # array up to the index i
        sum += arr[i]

    # Check if the sum of the
    # array is not divisible
    # by k, then return the
    # size of array
    if ((sum % k) != 0):
        return n

    # All elements of array
    # are divisible by k,
    # then no such subarray
    # possible so return -1
    elif(left == -1):
        return -1

    else:

        # length of prefix elements
        # that can be removed
        prefix_length = left + 1

        # length of suffix elements
        # that can be removed
        suffix_length = n - right

        # Return the length of
        # subarray after removing
        # the elements which have
        # lesser number of elements
        return n - min(prefix_length,
                       suffix_length)

# Driver Code
if __name__ == "__main__":

    arr = [ 6, 3, 12, 15 ]
    n = len(arr)
    K = 3

    print(MaxSubarrayLength(arr, n, K))

# This code is contributed by chitranayal
```

## C#

```
// C# program to find the length of
// the longest subarray whose sum is
// not divisible by integer K
using System;

class GFG{

// Function to find the longest subarray
// with sum is not divisible by k
static int MaxSubarrayLength(int []arr, int n,
                                        int k)
{

    // left is the index of the
    // leftmost element that is
    // not divisible by k
    int left = -1;

    // right is the index of the
    // rightmost element that is
    // not divisible by k
    int right = 0;

    // sum of the array
    int sum = 0;

    for(int i = 0; i < n; i++)
    {

        // Find the element that
        // is not multiple of k
        if ((arr[i] % k) != 0)
        {

            // left = -1 means we are
            // finding the leftmost
            // element that is not
            // divisible by k
            if (left == -1)
            {
                left = i;
            }

            // Updating the
            // rightmost element
            right = i;
        }

        // Update the sum of the
        // array up to the index i
        sum += arr[i];
    }

    // Check if the sum of the
    // array is not divisible
    // by k, then return the
    // size of array
    if ((sum % k) != 0)
    {
        return n;
    }

    // All elements of array
    // are divisible by k,
    // then no such subarray
    // possible so return -1
    else if (left == -1)
    {
        return -1;
    }
    else
    {

        // Length of prefix elements
        // that can be removed
        int prefix_length = left + 1;

        // Length of suffix elements
        // that can be removed
        int suffix_length = n - right;

        // Return the length of
        // subarray after removing
        // the elements which have
        // lesser number of elements
        return n - Math.Min(prefix_length,
                            suffix_length);
    }
}

// Driver code
public static void Main(string[] args)
{
    int []arr = { 6, 3, 12, 15 };
    int n = arr.Length;
    int K = 3;

    Console.Write(MaxSubarrayLength(arr, n, K));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to find the length of
// the longest subarray whose sum is
// not divisible by integer K

// Function to find the longest subarray
// with sum is not divisible by k
function MaxSubarrayLength(arr, n, k)
{

    // left is the index of the
    // leftmost element that is
    // not divisible by k
    let left = -1;

    // right is the index of the
    // rightmost element that is
    // not divisible by k
    let right = 0;

    // sum of the array
    let sum = 0;

    for(let i = 0; i < n; i++)
    {

        // Find the element that
        // is not multiple of k
        if ((arr[i] % k) != 0)
        {

            // left = -1 means we are
            // finding the leftmost
            // element that is not
            // divisible by k
            if (left == -1)
            {
                left = i;
            }

            // Updating the
            // rightmost element
            right = i;
        }

        // Update the sum of the
        // array up to the index i
        sum += arr[i];
    }

    // Check if the sum of the
    // array is not divisible
    // by k, then return the
    // size of array
    if ((sum % k) != 0)
    {
        return n;
    }

    // All elements of array
    // are divisible by k,
    // then no such subarray
    // possible so return -1
    else if (left == -1)
    {
        return -1;
    }
    else
    {

        // Length of prefix elements
        // that can be removed
        let prefix_length = left + 1;

        // Length of suffix elements
        // that can be removed
        let suffix_length = n - right;

        // Return the length of
        // subarray after removing
        // the elements which have
        // lesser number of elements
        return n - Math.min(prefix_length,
                            suffix_length);
    }
}

// Driver Code
    let arr = [ 6, 3, 12, 15 ];
    let n = arr.length;
    let K = 3;

    document.write(MaxSubarrayLength(arr, n, K));

  // This code is contributed by target_2.
</script>
```

**Output:** 

```
-1
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*