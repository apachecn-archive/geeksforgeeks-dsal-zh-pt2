# 乘积为 0 的最长子阵列

> 原文:[https://www . geeksforgeeks . org/最长子阵列-其产品为-0/](https://www.geeksforgeeks.org/longest-sub-array-whose-product-is-0/)

给定一个整数元素的数组 **arr[]** ，任务是找出乘积为 **0** 的最长子数组的长度。
**例:**

> **输入:** arr[] = {1，2，3，0，1，2，0}
> **输出:** 7
> {1，2，3，0，1，2，0}是乘积为 0 的最长子阵列。
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 0
> 不存在乘积为 0 的可能子阵列。

**进场:**

*   如果数组中没有等于 0 的元素，那么就没有乘积为 0 的子数组。
*   如果数组中至少有一个元素等于 0，那么乘积为 0 的最长子数组就是完整的数组。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the length of the
// longest sub-array whose product
// of elements is 0
int longestSubArray(int arr[], int n)
{
    bool isZeroPresent = false;
    for (int i = 0; i < n; i++) {
        if (arr[i] == 0) {
            isZeroPresent = true;
            break;
        }
    }

    if (isZeroPresent)
        return n;

    return 0;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 0, 1, 2, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << longestSubArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the length of the
    // longest sub-array whose product
    // of elements is 0
    static int longestSubArray(int arr[], int n)
    {
        boolean isZeroPresent = false;
        for (int i = 0; i < n; i++) {
            if (arr[i] == 0) {
                isZeroPresent = true;
                break;
            }
        }

        if (isZeroPresent)
            return n;

        return 0;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 1, 2, 3, 0, 1, 2, 0 };
        int n = arr.length;
        System.out.print(longestSubArray(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the length of
# the longest sub-array whose product
# of elements is 0
def longestSubArray(arr, n) :

    isZeroPresent = False
    for i in range (0 , n) :
        if (arr[i] == 0) :
            isZeroPresent = True
            break

    if (isZeroPresent) :
        return n

    return 0

# Driver code
arr = [ 1, 2, 3, 0, 1, 2, 0 ]
n = len(arr)
print(longestSubArray(arr, n))

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to return the length of the
    // longest sub-array whose product
    // of elements is 0
    static int longestSubArray(int[] arr, int n)
    {
        bool isZeroPresent = false;
        for (int i = 0; i < n; i++) {
            if (arr[i] == 0) {
                isZeroPresent = true;
                break;
            }
        }

        if (isZeroPresent)
            return n;

        return 0;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, 2, 3, 0, 1, 2, 0 };
        int n = arr.Length;
        Console.Write(longestSubArray(arr, n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the length of the
// longest sub-array whose product
// of elements is 0
function longestSubArray($arr, $n)
{

    $isZeroPresent = false;
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] == 0)
        {
            $isZeroPresent = true;
            break;
        }

    }
    if ($isZeroPresent)
        return $n;

    return 0;
}

// Driver code
$arr = array( 1, 2, 3, 0, 1, 2, 0 );
$n = sizeof($arr);
echo longestSubArray($arr, $n);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the length of the
// longest sub-array whose product
// of elements is 0
function longestSubArray(arr, n)
{
    var isZeroPresent = false;
    for (var i = 0; i < n; i++) {
        if (arr[i] == 0) {
            isZeroPresent = true;
            break;
        }
    }

    if (isZeroPresent)
        return n;

    return 0;
}

// Driver code
var arr = [ 1, 2, 3, 0, 1, 2, 0 ];
var n = arr.length;
document.write(longestSubArray(arr, n));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
7
```

**时间复杂度:** O(n)