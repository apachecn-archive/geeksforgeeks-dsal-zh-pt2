# 数组边界元素的最长递增序列

> 原文:[https://www . geeksforgeeks . org/按数组元素边界递增最长序列/](https://www.geeksforgeeks.org/longest-increasing-sequence-by-the-boundary-elements-of-an-array/)

给定一个具有唯一元素的长度为 **N** 的数组 **arr[]** ，任务是找出该数组两端的元素能够形成的最长递增子序列的长度。
**例:**

> **输入:** arr[] = {3，5，1，4，2}
> **输出:** 4
> **解释:**
> 最长序列为:{2，3，4，5}
> Pick 2，序列为{2}，数组为{3，5，1，4}
> Pick 3，序列为{2，3}，数组为{5，1，4}
> Pick 4，序列为{2，3，4}，数组为

**进场:**这个问题可以通过 [**双指针进场**](https://www.geeksforgeeks.org/two-pointers-technique/) 解决。在数组的第一个和最后一个索引处设置两个指针。选择当前指向的两个值中的最小值，并检查它是否大于先前选择的值。如果是，更新指针并增加 LIS 的长度，然后重复该过程。否则，打印获得的 LIS 长度。
以下是上述方法的实现:

## C++

```
// C++ Program to print the
// longest increasing
// subsequence from the
// boundary elements of an array

#include <bits/stdc++.h>
using namespace std;

// Function to return the length of
// Longest Increasing subsequence
int longestSequence(int n, int arr[])
{

    // Set pointers at
    // both ends
    int l = 0, r = n - 1;

    // Stores the recent
    // value added to the
    // subsequence
    int prev = INT_MIN;

    // Stores the length of
    // the subsequence
    int ans = 0;

    while (l <= r) {

        // Check if both elements
        // can be added to the
        // subsequence
        if (arr[l] > prev
            && arr[r] > prev) {

            if (arr[l] < arr[r]) {
                ans += 1;
                prev = arr[l];
                l += 1;
            }
            else {
                ans += 1;
                prev = arr[r];
                r -= 1;
            }
        }

        // Check if the element
        // on the left can be
        // added to the
        // subsequence only
        else if (arr[l] > prev) {
            ans += 1;
            prev = arr[l];
            l += 1;
        }

        // Check if the element
        // on the right can be
        // added to the
        // subsequence only
        else if (arr[r] > prev) {
            ans += 1;
            prev = arr[r];
            r -= 1;
        }

        // If none of the values
        // can be added to the
        // subsequence
        else {
            break;
        }
    }
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 3, 5, 1, 4, 2 };

    // Length of array
    int n = sizeof(arr)
            / sizeof(arr[0]);

    cout << longestSequence(n, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the longest
// increasing subsequence from the
// boundary elements of an array
import java.util.*;

class GFG{

// Function to return the length of
// Longest Increasing subsequence
static int longestSequence(int n, int arr[])
{

    // Set pointers at
    // both ends
    int l = 0, r = n - 1;

    // Stores the recent
    // value added to the
    // subsequence
    int prev = Integer.MIN_VALUE;

    // Stores the length of
    // the subsequence
    int ans = 0;

    while (l <= r)
    {

        // Check if both elements
        // can be added to the
        // subsequence
        if (arr[l] > prev &&
            arr[r] > prev)
        {
            if (arr[l] < arr[r])
            {
                ans += 1;
                prev = arr[l];
                l += 1;
            }
            else
            {
                ans += 1;
                prev = arr[r];
                r -= 1;
            }
        }

        // Check if the element on the
        // left can be added to the
        // subsequence only
        else if (arr[l] > prev)
        {
            ans += 1;
            prev = arr[l];
            l += 1;
        }

        // Check if the element on the
        // right can be added to the
        // subsequence only
        else if (arr[r] > prev)
        {
            ans += 1;
            prev = arr[r];
            r -= 1;
        }

        // If none of the values
        // can be added to the
        // subsequence
        else
        {
            break;
        }
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 5, 1, 4, 2 };

    // Length of array
    int n = arr.length;

    System.out.print(longestSequence(n, arr));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to print the
# longest increasing subsequence
# from the boundary elements
# of an array
import sys

# Function to return the length of
# Longest Increasing subsequence
def longestSequence(n, arr):

    # Set pointers at
    # both ends
    l = 0
    r = n - 1

    # Stores the recent value
    # added to the subsequence
    prev = -sys.maxsize - 1

    # Stores the length of
    # the subsequence
    ans = 0

    while (l <= r):

        # Check if both elements can be
        # added to the subsequence
        if (arr[l] > prev and
            arr[r] > prev):

            if (arr[l] < arr[r]):
                ans += 1
                prev = arr[l]
                l += 1

            else:
                ans += 1
                prev = arr[r]
                r -= 1

        # Check if the element
        # on the left can be
        # added to the
        # subsequence only
        elif (arr[l] > prev):
            ans += 1
            prev = arr[l]
            l += 1

        # Check if the element
        # on the right can be
        # added to the
        # subsequence only
        elif (arr[r] > prev):
            ans += 1
            prev = arr[r]
            r -= 1

        # If none of the values
        # can be added to the
        # subsequence
        else:
            break

    return ans

# Driver code
arr = [ 3, 5, 1, 4, 2 ]

# Length of array
n = len(arr)

print(longestSequence(n, arr))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to print the longest
// increasing subsequence from the
// boundary elements of an array
using System;

class GFG{

// Function to return the length of
// longest Increasing subsequence
static int longestSequence(int n, int []arr)
{

    // Set pointers at
    // both ends
    int l = 0, r = n - 1;

    // Stores the recent value
    // added to the subsequence
    int prev = int.MinValue;

    // Stores the length of
    // the subsequence
    int ans = 0;

    while (l <= r)
    {

        // Check if both elements
        // can be added to the
        // subsequence
        if (arr[l] > prev &&
            arr[r] > prev)
        {
            if (arr[l] < arr[r])
            {
                ans += 1;
                prev = arr[l];
                l += 1;
            }
            else
            {
                ans += 1;
                prev = arr[r];
                r -= 1;
            }
        }

        // Check if the element on the
        // left can be added to the
        // subsequence only
        else if (arr[l] > prev)
        {
            ans += 1;
            prev = arr[l];
            l += 1;
        }

        // Check if the element on the
        // right can be added to the
        // subsequence only
        else if (arr[r] > prev)
        {
            ans += 1;
            prev = arr[r];
            r -= 1;
        }

        // If none of the values
        // can be added to the
        // subsequence
        else
        {
            break;
        }
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 3, 5, 1, 4, 2 };

    // Length of array
    int n = arr.Length;

    Console.Write(longestSequence(n, arr));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript Program to print the
// longest increasing
// subsequence from the
// boundary elements of an array

// Function to return the length of
// Longest Increasing subsequence
function longestSequence(n, arr)
{

    // Set pointers at
    // both ends
    var l = 0, r = n - 1;

    // Stores the recent
    // value added to the
    // subsequence
    var prev = -1000000000;

    // Stores the length of
    // the subsequence
    var ans = 0;

    while (l <= r) {

        // Check if both elements
        // can be added to the
        // subsequence
        if (arr[l] > prev
            && arr[r] > prev) {

            if (arr[l] < arr[r]) {
                ans += 1;
                prev = arr[l];
                l += 1;
            }
            else {
                ans += 1;
                prev = arr[r];
                r -= 1;
            }
        }

        // Check if the element
        // on the left can be
        // added to the
        // subsequence only
        else if (arr[l] > prev) {
            ans += 1;
            prev = arr[l];
            l += 1;
        }

        // Check if the element
        // on the right can be
        // added to the
        // subsequence only
        else if (arr[r] > prev) {
            ans += 1;
            prev = arr[r];
            r -= 1;
        }

        // If none of the values
        // can be added to the
        // subsequence
        else {
            break;
        }
    }
    return ans;
}

// Driver Code
var arr = [ 3, 5, 1, 4, 2 ];

// Length of array
var n = arr.length;
document.write( longestSequence(n, arr));

// This code is contributed by itsok.
</script>   
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*T4】