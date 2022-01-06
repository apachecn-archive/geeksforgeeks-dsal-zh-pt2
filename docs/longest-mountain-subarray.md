# 最长的山地子阵

> 原文:[https://www.geeksforgeeks.org/longest-mountain-subarray/](https://www.geeksforgeeks.org/longest-mountain-subarray/)

给定一个具有 **N** 元素的数组 **arr[]** ，任务是找出最长的子数组，它具有山的形状。

> 一个**山子阵列**由最初按升序排列的元素组成，直到到达一个峰值元素，在峰值元素之外，子阵列的所有其他元素都按降序排列。

**示例:**

> **输入:**arr =【2，2，2】
> **输出:** 0
> **说明:**
> 不存在显示山子阵行为的子阵。
> 
> **输入:**arr =【1，3，1，4，5，6，7，8，9，8，7，6，5】
> **输出:** 11
> **说明:**
> 有两个子阵可以认为是山地子阵。第一个来自索引 0–2(3 个元素)，下一个来自索引 2–12(11 个元素)。作为 11 > 2，我们的答案是 11。

**天真的做法:**
仔细检查每一个可能的子阵，看看是不是山地子阵。这可能需要很长时间来找到解决方案，并且上述方法的时间复杂度可以估计为 **O(N*N)** 遍历每个可能的子阵列，以及 **O(N)** 检查它是否是山子阵列。因此，程序的整体时间复杂度是 **O(N <sup>3</sup> )** ，这是非常高的。

**有效方法:**

1.  如果给定数组的长度小于 3，则打印 0，因为在这种情况下不可能有山地子数组。
2.  最初将最大长度设置为 0。
3.  使用双指针技术(“开始”指针和“结束”指针)找出给定数组中最长的山子数组。
4.  当遇到增加的子数组时，在“开始”指针中标记该增加的子数组的开始索引。
5.  如果在“结束”指针中找到一个索引值，则重置两个指针中的值，因为它标志着一个新的山体子阵列的开始。
6.  当遇到递减的子阵列时，在“结束”指针中标记山子阵列的结束索引。
7.  计算当前山体子阵列的长度，与目前为止遍历的所有山体子阵列的当前最大长度进行比较，并不断更新当前最大长度。

下面是上述有效方法的实现:

## C++

```
// C++ code for Longest Mountain Subarray

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// longest mountain subarray
int LongestMountain(vector<int>& a)
{
    int i = 0, j = -1,
        k = -1, p = 0,
        d = 0, n = 0;

    // If the size of array is less
    // than 3, the array won't show
    // mountain like behaviour
    if (a.size() < 3) {
        return 0;
    }

    for (i = 0; i < a.size() - 1; i++) {

        if (a[i + 1] > a[i]) {

            // When a new mountain sub-array
            // is found, there is a need to
            // set the variables k, j to -1
            // in order to help calculate the
            // length of new mountain sub-array
            if (k != -1) {
                k = -1;
                j = -1;
            }

            // j marks the starting index of a
            // new mountain sub-array. So set the
            // value of j to current index i.
            if (j == -1) {
                j = i;
            }
        }
        else {

            // Checks if next element is
            // less than current element
            if (a[i + 1] < a[i]) {

                // Checks if starting element exists
                // or not, if the starting element
                // of the mountain sub-array exists
                // then the index of ending element
                // is stored in k
                if (j != -1) {
                    k = i + 1;
                }

                // This condition checks if both
                // starting index and ending index
                // exists or not, if yes, the
                // length is calculated.
                if (k != -1 && j != -1) {

                    // d holds the length of the
                    // longest mountain sub-array.
                    // If the current length is
                    // greater than the
                    // calculated length, then
                    // value of d is updated.
                    if (d < k - j + 1) {
                        d = k - j + 1;
                    }
                }
            }

            // ignore if there is no
            // increase or decrease in
            // the value of the next element
            else {
                k = -1;
                j = -1;
            }
        }
    }

    // Checks and calculates
    // the length if last element
    // of the array is the last
    // element of a mountain sub-array
    if (k != -1 && j != -1) {
        if (d < k - j + 1) {
            d = k - j + 1;
        }
    }
    return d;
}

// Driver code
int main()
{
    vector<int> d = { 1, 3, 1, 4,
                      5, 6, 7, 8,
                      9, 8, 7, 6, 5 };

    cout << LongestMountain(d)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for Longest Mountain Subarray
import java.io.*;

class GFG{

// Function to find the
// longest mountain subarray
public static int LongestMountain(int a[])
{
    int i = 0, j = -1, k = -1, d = 0;

    // If the size of array is less than 3,
    // the array won't show mountain like
    // behaviour
    if (a.length < 3)
        return 0;

    for(i = 0; i < a.length - 1; i++)
    {
        if (a[i + 1] > a[i])
        {

            // When a new mountain sub-array is
            // found, there is a need to set the
            // variables k, j to -1 in order to
            // help calculate the length of new
            // mountain sub-array
            if (k != -1)
            {
                k = -1;
                j = -1;
            }

            // j marks the starting index of a
            // new mountain sub-array. So set the
            // value of j to current index i.
            if (j == -1)
                j = i;
        }
        else
        {

            // Checks if next element is
            // less than current element
            if (a[i + 1] < a[i])
            {

                // Checks if starting element exists
                // or not, if the starting element of
                // the mountain sub-array exists then
                // the index of ending element is
                // stored in k
                if (j != -1)
                    k = i + 1;

                // This condition checks if both
                // starting index and ending index
                // exists or not, if yes,the length
                // is calculated.
                if (k != -1 && j != -1)
                {

                    // d holds the length of the
                    // longest mountain sub-array.
                    // If the current length is
                    // greater than the calculated
                    // length, then value of d is
                    // updated.
                    if (d < k - j + 1)
                        d = k - j + 1;
                }
            }

            // Ignore if there is no increase
            // or decrease in the value of the
            // next element
            else
            {
                k = -1;
                j = -1;
            }
        }
    }

    // Checks and calculates the length
    // if last element of the array is
    // the last element of a mountain sub-array
    if (k != -1 && j != -1)
    {
        if (d < k - j + 1)
            d = k - j + 1;
    }
    return d;
}

// Driver code
public static void main (String[] args)
{
    int a[] = { 1, 3, 1, 4, 5, 6, 7,
                8, 9, 8, 7, 6, 5 };

    System.out.println(LongestMountain(a));
}
}

// This code is contributed by piyush3010
```

## 蟒蛇 3

```
# Python3 code for longest mountain subarray

# Function to find the
# longest mountain subarray
def LongestMountain(a):

    i = 0
    j = -1
    k = -1
    p = 0
    d = 0
    n = 0

    # If the size of the array is less
    # than 3, the array won't show
    # mountain like behaviour
    if (len(a) < 3):
        return 0

    for i in range(len(a) - 1):
        if (a[i + 1] > a[i]):

            # When a new mountain sub-array
            # is found, there is a need to
            # set the variables k, j to -1
            # in order to help calculate the
            # length of new mountain sub-array
            if (k != -1):
                k = -1
                j = -1

            # j marks the starting index of a
            # new mountain sub-array. So set the
            # value of j to current index i.
            if (j == -1):
                j = i
        else:

            # Checks if next element is
            # less than current element
            if (a[i + 1] < a[i]):

                # Checks if starting element exists
                # or not, if the starting element
                # of the mountain sub-array exists
                # then the index of ending element
                # is stored in k
                if (j != -1):
                    k = i + 1

                # This condition checks if both
                # starting index and ending index
                # exists or not, if yes, the
                # length is calculated.
                if (k != -1 and j != -1):

                    # d holds the length of the
                    # longest mountain sub-array.
                    # If the current length is
                    # greater than the
                    # calculated length, then
                    # value of d is updated.
                    if (d < k - j + 1):
                        d = k - j + 1

            # Ignore if there is no
            # increase or decrease in
            # the value of the next element
            else:
                k = -1
                j = -1

    # Checks and calculates
    # the length if last element
    # of the array is the last
    # element of a mountain sub-array
    if (k != -1 and j != -1):
        if (d < k - j + 1):
            d = k - j + 1

    return d

# Driver code
d = [ 1, 3, 1, 4, 5, 6,
      7, 8, 9, 8, 7, 6, 5 ]

print(LongestMountain(d))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# code for the
// longest Mountain Subarray
using System;
class GFG{

// Function to find the
// longest mountain subarray
public static int longestMountain(int []a)
{
  int i = 0, j = -1, k = -1,
  p = 0, d = 0;

  // If the size of array is less than 3,
  // the array won't show mountain like
  // behaviour
  if (a.Length < 3)
    return 0;

  for(i = 0; i < a.Length - 1; i++)
  {
    if (a[i + 1] > a[i])
    {
      // When a new mountain sub-array is
      // found, there is a need to set the
      // variables k, j to -1 in order to
      // help calculate the length of new
      // mountain sub-array
      if (k != -1)
      {
        k = -1;
        j = -1;
      }

      // j marks the starting index of a
      // new mountain sub-array. So set the
      // value of j to current index i.
      if (j == -1)
        j = i;
    }
    else
    {
      // Checks if next element is
      // less than current element
      if (a[i + 1] < a[i])
      {
        // Checks if starting element exists
        // or not, if the starting element of
        // the mountain sub-array exists then
        // the index of ending element is
        // stored in k
        if (j != -1)
          k = i + 1;

        // This condition checks if both
        // starting index and ending index
        // exists or not, if yes,the length
        // is calculated.
        if (k != -1 && j != -1)
        {
          // d holds the length of the
          // longest mountain sub-array.
          // If the current length is
          // greater than the calculated
          // length, then value of d is
          // updated.
          if (d < k - j + 1)
            d = k - j + 1;
        }
      }

      // Ignore if there is no increase
      // or decrease in the value of the
      // next element
      else
      {
        k = -1;
        j = -1;
      }
    }
  }

  // Checks and calculates the length
  // if last element of the array is
  // the last element of a mountain sub-array
  if (k != -1 && j != -1)
  {
    if (d < k - j + 1)
      d = k - j + 1;
  }
  return d;
}

// Driver code
public static void Main(String[] args)
{
  int []a = {1, 3, 1, 4, 5, 6, 7,
             8, 9, 8, 7, 6, 5};
  Console.WriteLine(longestMountain(a));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript code for Longest Mountain Subarray

// Function to find the
// longest mountain subarray
function LongestMountain(a)
{
    let i = 0, j = -1, k = -1,
        p = 0, d = 0, n = 0;

    // If the size of array is less than 3,
    // the array won't show mountain like
    // behaviour
    if (a.length < 3)
        return 0;

    for(i = 0; i < a.length - 1; i++)
    {
        if (a[i + 1] > a[i])
        {

            // When a new mountain sub-array is
            // found, there is a need to set the
            // variables k, j to -1 in order to
            // help calculate the length of new
            // mountain sub-array
            if (k != -1)
            {
                k = -1;
                j = -1;
            }

            // j marks the starting index of a
            // new mountain sub-array. So set the
            // value of j to current index i.
            if (j == -1)
                j = i;
        }
        else
        {

            // Checks if next element is
            // less than current element
            if (a[i + 1] < a[i])
            {

                // Checks if starting element exists
                // or not, if the starting element of
                // the mountain sub-array exists then
                // the index of ending element is
                // stored in k
                if (j != -1)
                    k = i + 1;

                // This condition checks if both
                // starting index and ending index
                // exists or not, if yes,the length
                // is calculated.
                if (k != -1 && j != -1)
                {

                    // d holds the length of the
                    // longest mountain sub-array.
                    // If the current length is
                    // greater than the calculated
                    // length, then value of d is
                    // updated.
                    if (d < k - j + 1)
                        d = k - j + 1;
                }
            }

            // Ignore if there is no increase
            // or decrease in the value of the
            // next element
            else
            {
                k = -1;
                j = -1;
            }
        }
    }

    // Checks and calculates the length
    // if last element of the array is
    // the last element of a mountain sub-array
    if (k != -1 && j != -1)
    {
        if (d < k - j + 1)
            d = k - j + 1;
    }
    return d;
}

// Driver Code

    let a = [ 1, 3, 1, 4, 5, 6, 7,
                8, 9, 8, 7, 6, 5 ];

    document.write(LongestMountain(a));

</script>
```

**Output:** 

```
11
```

***时间复杂度:** O(N)*
***辅助空间复杂度:** O(1)*