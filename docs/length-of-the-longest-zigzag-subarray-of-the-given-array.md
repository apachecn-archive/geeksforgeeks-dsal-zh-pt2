# 给定阵列的最长锯齿形子阵列的长度

> 原文:[https://www . geeksforgeeks . org/给定阵列的最长之字形子阵列长度/](https://www.geeksforgeeks.org/length-of-the-longest-zigzag-subarray-of-the-given-array/)

给定一个包含 **n** 个数字的**数组 arr[]** ，任务是找到最长的[之字形](https://www.geeksforgeeks.org/converting-an-array-of-integers-into-zig-zag-fashion/)子阵列的长度，这样子阵列中的每个元素都应该是形式的

```
a < b > c < d > e < f
```

**示例:**

> **输入:** arr[] = {12，13，1，5，4，7，8，10，10，11}
> **输出:** 6
> **解释:**
> 子阵是长度为 6 的{12，13，1，5，4，7}，呈之字形。
> 
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 2
> **解释:**
> 子阵是长度为 2 的{1，2}或{2，3}或{4，5}。

**接近**:解决上述问题，按照以下步骤进行:

*   初始初始化 *cnt* ，一个计数器为 1。
*   迭代数组元素，检查元素是否符合形式

```
a < b > c < d > e < f
```

*   如果为真，则将碳纳米管增加 1。如果它不是形式上的

```
a < b > c < d > e < f
```

*   然后将 cnt 重新初始化 1。

下面是上述方法的实现:

## C++

```
// C++ implementation to find
// the length of longest zigzag
// subarray of the given array

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// longest zigZag contiguous subarray
int lenOfLongZigZagArr(int a[], int n)
{

    // 'max' to store the length
    // of longest zigZag subarray
    int max = 1,

        // 'len' to store the lengths
        // of longest zigZag subarray
        // at different instants of time
        len = 1;

    // Traverse the array from the beginning
    for (int i = 0; i < n - 1; i++) {

        if (i % 2 == 0
            && (a[i] < a[i + 1]))
            len++;

        else if (i % 2 == 1
                 && (a[i] > a[i + 1]))
            len++;

        else {
            // Check if 'max' length
            // is less than the length
            // of the current zigzag subarray.
            // If true, then update 'max'
            if (max < len)
                max = len;

            // Reset 'len' to 1
            // as from this element,
            // again the length of the
            // new zigzag subarray
            // is being calculated
            len = 1;
        }
    }

    // comparing the length of the last
    // zigzag subarray with 'max'
    if (max < len)
        max = len;

    // Return required maximum length
    return max;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << lenOfLongZigZagArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// the length of longest zigzag
// subarray of the given array
import java.io.*;
import java.util.*;
class GFG {

// Function to find the length of
// longest zigZag contiguous subarray
static int lenOfLongZigZagArr(int a[], int n)
{
    // 'max' to store the length
    // of longest zigZag subarray
    int max = 1,

    // 'len' to store the lengths
    // of longest zigZag subarray
    // at different instants of time
    len = 1;

    // Traverse the array from the beginning
    for (int i = 0; i < n - 1; i++)
    {
        if (i % 2 == 0 && (a[i] < a[i + 1]))
            len++;

        else if (i % 2 == 1 && (a[i] > a[i + 1]))
            len++;

        else
        {
            // Check if 'max' length
            // is less than the length
            // of the current zigzag subarray.
            // If true, then update 'max'
            if (max < len)
                max = len;

            // Reset 'len' to 1
            // as from this element,
            // again the length of the
            // new zigzag subarray
            // is being calculated
            len = 1;
        }
    }

    // comparing the length of the last
    // zigzag subarray with 'max'
    if (max < len)
        max = len;

    // Return required maximum length
    return max;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = arr.length;

    System.out.println(lenOfLongZigZagArr(arr, n));
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 implementation to find the
# length of longest zigzag subarray
# of the given array

# Function to find the length of
# longest zigZag contiguous subarray
def lenOfLongZigZagArr(a, n):

    # '_max' to store the length
    # of longest zigZag subarray
    _max = 1

    # '_len' to store the lengths
    # of longest zigZag subarray
    # at different instants of time
    _len = 1

    # Traverse the array from the beginning
    for i in range(n - 1):

        if i % 2 == 0 and a[i] < a[i + 1]:
            _len += 1

        elif i % 2 == 1 and a[i] > a[i + 1]:
            _len += 1

        else:

            # Check if '_max' length is less than
            # the length of the current zigzag
            # subarray. If true, then update '_max'
            if _max < _len:
                _max = _len

            # Reset '_len' to 1 as from this element,
            # again the length of the new zigzag
            # subarray is being calculated
            _len = 1

    # Comparing the length of the last
    # zigzag subarray with '_max'
    if _max < _len:
        _max = _len

    # Return required maximum length
    return _max

# Driver code
arr = [ 1, 2, 3, 4, 5 ]
n = len(arr)

print(lenOfLongZigZagArr(arr, n))

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation to find
// the length of longest zigzag
// subarray of the given array
using System;

class GFG{

// Function to find the length of
// longest zigZag contiguous subarray
static int lenOflongZigZagArr(int []a, int n)
{

    // 'max' to store the length
    // of longest zigZag subarray
    int max = 1,

    // 'len' to store the lengths
    // of longest zigZag subarray
    // at different instants of time
    len = 1;

    // Traverse the array from the beginning
    for(int i = 0; i < n - 1; i++)
    {
       if (i % 2 == 0 && (a[i] < a[i + 1]))
           len++;

       else if (i % 2 == 1 && (a[i] > a[i + 1]))
           len++;

       else
       {

           // Check if 'max' length
           // is less than the length
           // of the current zigzag subarray.
           // If true, then update 'max'
           if (max < len)
               max = len;

           // Reset 'len' to 1
           // as from this element,
           // again the length of the
           // new zigzag subarray
           // is being calculated
           len = 1;
       }
    }

    // Comparing the length of the last
    // zigzag subarray with 'max'
    if (max < len)
        max = len;

    // Return required maximum length
    return max;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5 };
    int n = arr.Length;

    Console.WriteLine(lenOflongZigZagArr(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to find
// the length of longest zigzag
// subarray of the given array

// Function to find the length of
// longest zigZag contiguous subarray
function lenOfLongZigZagArr( a, n)
{

    // 'max' to store the length
    // of longest zigZag subarray
    var max = 1,

    // 'len' to store the lengths
    // of longest zigZag subarray
    // at different instants of time
    len = 1;

    // Traverse the array from the beginning
    for (var i = 0; i < n - 1; i++) {

        if (i % 2 == 0
            && (a[i] < a[i + 1]))
            len++;

        else if (i % 2 == 1
                 && (a[i] > a[i + 1]))
            len++;

        else {
            // Check if 'max' length
            // is less than the length
            // of the current zigzag subarray.
            // If true, then update 'max'
            if (max < len)
                max = len;

            // Reset 'len' to 1
            // as from this element,
            // again the length of the
            // new zigzag subarray
            // is being calculated
            len = 1;
        }
    }

    // comparing the length of the last
    // zigzag subarray with 'max'
    if (max < len)
        max = len;

    // Return required maximum length
    return max;
}

// Driver code
var arr = [ 1, 2, 3, 4, 5 ];
var n = arr.length;
document.write( lenOfLongZigZagArr(arr, n));

</script>
```

**Output:** 

```
2
```