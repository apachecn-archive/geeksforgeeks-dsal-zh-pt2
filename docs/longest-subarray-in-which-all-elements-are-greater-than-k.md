# 所有元素都大于 K 的最长子阵列

> 原文:[https://www . geesforgeks . org/最长子数组-其中所有元素都大于-k/](https://www.geeksforgeeks.org/longest-subarray-in-which-all-elements-are-greater-than-k/)

给定一个由 N 个整数和 K 个数字组成的数组，任务是找出所有元素都大于 K 的最长子数组的长度。
**示例:**

> **输入** : a[] = {3，4，5，6，7，2，10，11}，K = 5
> **输出** : 2
> 长度为 2 的最长子阵列有两种可能。
> 分别是{6，7}和{10，11}。
> **输入** : a[] = {8，25，10，19，19，18，20，11，18}，K = 13
> **输出** : 4
> 最长的子阵是{19，19，18，20}。

想法是开始使用计数器遍历数组。如果当前元素大于给定值 X，递增计数器，否则用前一长度和当前计数器的最大值替换前一长度，并重置计数器。
以下是上述办法的实施情况。

## C++

```
// C++ program to print the length of the longest
// subarray with all elements greater than X
#include <bits/stdc++.h>
using namespace std;

// Function to count number of segments
int longestSubarray(int a[], int n, int x)
{
    int count = 0;

    int length = 0;

    // Iterate in the array
    for (int i = 0; i < n; i++) {

        // check if array element
        // greater then X or not
        if (a[i] > x) {
            count += 1;
        }
        else {

            length = max(length, count);

            count = 0;
        }
    }

    // After iteration complete
    // check for the last segment
    if (count)
        length = max(length, count);

    return length;
}

// Driver Code
int main()
{
    int a[] = { 8, 25, 10, 19, 19, 18, 20, 11, 18 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 13;

    cout << longestSubarray(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the length of the longest
// subarray with all elements greater than X

import java.io.*;

class GFG {

// Function to count number of segments
static int longestSubarray(int a[], int n, int x)
{
    int count = 0;

    int length = 0;

    // Iterate in the array
    for (int i = 0; i < n; i++) {

        // check if array element
        // greater then X or not
        if (a[i] > x) {
            count += 1;
        }
        else {

            length = Math.max(length, count);

            count = 0;
        }
    }

    // After iteration complete
    // check for the last segment
    if (count>0)
        length = Math.max(length, count);

    return length;
}

// Driver Code
    public static void main (String[] args) {
            int []a = { 8, 25, 10, 19, 19, 18, 20, 11, 18 };
    int n = a.length;
    int k = 13;

  System.out.println(longestSubarray(a, n, k));
    }
}
// This Code is contributed
// by shs
```

## 蟒蛇 3

```
# Python3 program to print the length of
# the longest subarray with all elements
# greater than X

# Function to count number of segments
def longestSubarray(a, n, x):
    count = 0
    length = 0

    # Iterate in the array
    for i in range(n):

        # check if array element greater
        # then X or not
        if (a[i] > x):
            count += 1
        else:
            length = max(length, count)
            count = 0

    # After iteration complete
    # check for the last segment
    if (count > 0):
        length = max(length, count)
    return length

# Driver Code
if __name__ == '__main__':
    a = [ 8, 25, 10, 19, 19,
             18, 20, 11, 18 ]
    n = len(a)
    k = 13
    print(longestSubarray(a, n, k))

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to print the length of the longest
// subarray with all elements greater than X

using System;

class GFG {

// Function to count number of segments
static int longestSubarray(int []a, int n, int x)
{
    int count = 0;

    int length = 0;

    // Iterate in the array
    for (int i = 0; i < n; i++) {

        // check if array element
        // greater then X or not
        if (a[i] > x) {
            count += 1;
        }
        else {

            length = Math.Max(length, count);

            count = 0;
        }
    }

    // After iteration complete
    // check for the last segment
    if (count>0)
        length = Math.Max(length, count);

    return length;
}

// Driver Code
    public static void Main () {
            int []a = { 8, 25, 10, 19, 19, 18, 20, 11, 18 };
    int n = a.Length;
    int k = 13;

Console.WriteLine(longestSubarray(a, n, k));
    }
}
// This Code is contributed
// by shs
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the length
// of the longest subarray with all
// elements greater than X

// Function to count number of segments
function longestSubarray($a, $n, $x)
{
    $count = 0;

    $length = 0;

    // Iterate in the array
    for ($i = 0; $i < $n; $i++)
    {

        // check if array element
        // greater then X or not
        if ($a[$i] > $x)
        {
            $count += 1;
        }
        else
        {
            $length = max($length, $count);

            $count = 0;
        }
    }

    // After iteration complete
    // check for the last segment
    if ($count > 0)
        $length = max($length, $count);

    return $length;
}

// Driver Code
$a = array( 8, 25, 10, 19, 19,
            18, 20, 11, 18 );
$n = 9;
$k = 13;

echo longestSubarray($a, $n, $k);

// This code is contributed
// by Arnab Kundu
?>
```

## java 描述语言

```
<script>
// javascript program to print the length of the longest
// subarray with all elements greater than X   
// Function to count number of segments
    function longestSubarray(a , n , x) {
        var count = 0;

        var length = 0;

        // Iterate in the array
        for (i = 0; i < n; i++) {

            // check if array element
            // greater then X or not
            if (a[i] > x) {
                count += 1;
            } else {

                length = Math.max(length, count);

                count = 0;
            }
        }

        // After iteration complete
        // check for the last segment
        if (count > 0)
            length = Math.max(length, count);

        return length;
    }

    // Driver Code

        var a = [ 8, 25, 10, 19, 19, 18, 20, 11, 18 ];
        var n = a.length;
        var k = 13;

        document.write(longestSubarray(a, n, k));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
4
```

**时间复杂度**:O(N)
T3】辅助空间: O(1)