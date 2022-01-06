# 通过从数组中移除一个元素来最小化相邻差的和

> 原文:[https://www . geeksforgeeks . org/通过从数组中移除一个元素来最小化相邻元素的差之和/](https://www.geeksforgeeks.org/minimize-sum-of-adjacent-difference-with-removal-of-one-element-from-array/)

给定一个大于 2 的正整数数组。任务是求数组连续差模之和的最小值，即从数组中去掉一个元素后的**| A1-A0 |+| A2-A1 |+| A3-A2 |+……+| An-1-An-2 |+| An-A(n-1)|**的值，其中 **An** 代表数组元素值的第 n 个索引。

**示例:**

> **输入:** arr[] = [1，5，3，2，10]
> **输出:** 7
> 在移除 10 时，我们得到 B = {1，5，3，2}即|1-5|+|5-3|+|3-2| = 4+2+1 = 7
> 
> **输入:**arr[]=【6，12，7，8，10，15】
> **输出:** 9
> 在移除 12 时，我们得到 B = {6，12，7，8，10，15}即| 6-7 |+| 7-8 |+| 8-10 |+| 10-15 | = 1+1+2+5 = 9

这个想法是从头到尾遍历数组，找到数组中的元素，在这个元素上我们得到连续模的最大差值。从计算的总值中减去最大值。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the element
int findMinRemoval(int arr[], int n)
{
    // Value variable for storing the total value
    int temp, value = 0;

    // Declaring maximum value as zero
    int maximum = 0;

    // If array contains on element
    if (n == 1)
        return 0;

    for (int i = 0; i < n; i++) {

        // Storing the maximum value in temp variable
        if (i != 0 && i != n - 1) {
            value = value + abs(arr[i] - arr[i + 1]);

            // Adding the adjacent difference modulus
            // values of removed element. Removing adjacent
            // difference modulus value after removing element
            temp = abs(arr[i] - arr[i + 1]) +
                   abs(arr[i] - arr[i - 1]) -
                   abs(arr[i - 1] - arr[i + 1]);
        }
        else if (i == 0) {
            value = value + abs(arr[i] - arr[i + 1]);
            temp = abs(arr[i] - arr[i + 1]);
        }
        else
            temp = abs(arr[i] - arr[i - 1]);

        maximum = max(maximum, temp);
    }

    // Returning total value-maximum value
    return (value - maximum);
}

// Drivers code
int main()
{
    int arr[] = { 1, 5, 3, 2, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findMinRemoval(arr, n) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to find the element
static int findMinRemoval(int arr[], int n)
{
    // Value variable for storing the total value
    int temp, value = 0;

    // Declaring maximum value as zero
    int maximum = 0;

    // If array contains on element
    if (n == 1)
        return 0;

    for (int i = 0; i < n; i++)
    {

        // Storing the maximum value in temp variable
        if (i != 0 && i != n - 1)
        {
            value = value + Math.abs(arr[i] - arr[i + 1]);

            // Adding the adjacent difference modulus
            // values of removed element. Removing adjacent
            // difference modulus value after removing element
            temp = Math.abs(arr[i] - arr[i + 1]) +
                Math.abs(arr[i] - arr[i - 1]) -
                Math.abs(arr[i - 1] - arr[i + 1]);
        }
        else if (i == 0)
        {
            value = value + Math.abs(arr[i] - arr[i + 1]);
            temp = Math.abs(arr[i] - arr[i + 1]);
        }
        else
            temp = Math.abs(arr[i] - arr[i - 1]);

        maximum = Math.max(maximum, temp);
    }

    // Returning total value-maximum value
    return (value - maximum);
}

// Drivers code
public static void main(String[] args)
{
    int arr[] = { 1, 5, 3, 2, 10 };
    int n = arr.length;
    System.out.print(findMinRemoval(arr, n) + "\n");
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to find the element
def findMinRemoval(arr, n):

    # Value variable for storing the
    # total value
    value = 0

    # Declaring maximum value as zero
    maximum = 0

    # If array contains on element
    if (n == 1):
        return 0

    for i in range( n):

        # Storing the maximum value in
        # temp variable
        if (i != 0 and i != n - 1):
            value = value + abs(arr[i] - arr[i + 1])

            # Adding the adjacent difference modulus
            # values of removed element. Removing
            # adjacent difference modulus value after
            # removing element
            temp = (abs(arr[i] - arr[i + 1]) +
                    abs(arr[i] - arr[i - 1]) -
                    abs(arr[i - 1] - arr[i + 1]))

        elif (i == 0):
            value = value + abs(arr[i] - arr[i + 1])
            temp = abs(arr[i] - arr[i + 1])

        else:
            temp = abs(arr[i] - arr[i - 1])

        maximum = max(maximum, temp)

    # Returning total value-maximum value
    return (value - maximum)

# Drivers code
if __name__ == "__main__":

    arr = [ 1, 5, 3, 2, 10 ]
    n = len(arr)

    print(findMinRemoval(arr, n))

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to find the element
    static int findMinRemoval(int []arr, int n)
    {
        // Value variable for storing the total value
        int temp, value = 0;

        // Declaring maximum value as zero
        int maximum = 0;

        // If array contains on element
        if (n == 1)
            return 0;

        for (int i = 0; i < n; i++)
        {

            // Storing the maximum value in temp variable
            if (i != 0 && i != n - 1)
            {
                value = value + Math.Abs(arr[i] - arr[i + 1]);

                // Adding the adjacent difference modulus
                // values of removed element. Removing adjacent
                // difference modulus value after removing element
                temp = Math.Abs(arr[i] - arr[i + 1]) +
                    Math.Abs(arr[i] - arr[i - 1]) -
                    Math.Abs(arr[i - 1] - arr[i + 1]);
            }
            else if (i == 0)
            {
                value = value + Math.Abs(arr[i] - arr[i + 1]);
                temp = Math.Abs(arr[i] - arr[i + 1]);
            }
            else
                temp = Math.Abs(arr[i] - arr[i - 1]);

            maximum = Math.Max(maximum, temp);
        }

        // Returning total value-maximum value
        return (value - maximum);
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 5, 3, 2, 10 };
        int n = arr.Length;
        Console.WriteLine(findMinRemoval(arr, n));
    }
}

// This code contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the element
function findMinRemoval($arr, $n)
{
    // Value variable for storing the total value
    $value = 0;

    // Declaring maximum value as zero
    $maximum = 0;

    // If array contains on element
    if ($n == 1)
        return 0;
    $temp=0;
    for ($i = 0; $i < $n; $i++)
    {

        // Storing the maximum value in temp variable
        if ($i != 0 && $i != $n - 1)
        {
            $value = $value + abs($arr[$i] - $arr[$i + 1]);

            // Adding the adjacent difference modulus
            // values of removed element. Removing adjacent
            // difference modulus value after removing element
            $temp = abs($arr[$i] - $arr[$i + 1]) +
                abs($arr[$i] - $arr[$i - 1]) -
                abs($arr[$i - 1] - $arr[$i + 1]);
        }
        else if ($i == 0)
        {
            $value = $value + abs($arr[$i] - $arr[$i + 1]);
            $temp = abs($arr[$i] - $arr[$i + 1]);
        }
        else
            $temp = abs($arr[$i] - $arr[$i - 1]);

        $maximum = max($maximum, $temp);
    }

    // Returning total value-maximum value
    return ($value - $maximum);
}

    // Drivers code
    $arr = array( 1, 5, 3, 2, 10 );
    $n = count($arr);

    echo findMinRemoval($arr, $n);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to find the element
function findMinRemoval(arr, n)
{
    // Value variable for storing the total value
    var temp, value = 0;

    // Declaring maximum value as zero
    var maximum = 0;

    // If array contains on element
    if (n == 1)
        return 0;

    for (var i = 0; i < n; i++) {

        // Storing the maximum value in temp variable
        if (i != 0 && i != n - 1) {
            value = value + Math.abs(arr[i] - arr[i + 1]);

            // Adding the adjacent difference modulus
            // values of removed element. Removing adjacent
            // difference modulus value after removing element
            temp = Math.abs(arr[i] - arr[i + 1]) +
                   Math.abs(arr[i] - arr[i - 1]) -
                   Math.abs(arr[i - 1] - arr[i + 1]);
        }
        else if (i == 0) {
            value = value + Math.abs(arr[i] - arr[i + 1]);
            temp = Math.abs(arr[i] - arr[i + 1]);
        }
        else
            temp = Math.abs(arr[i] - arr[i - 1]);

        maximum = Math.max(maximum, temp);
    }

    // Returning total value-maximum value
    return (value - maximum);
}

// Drivers code
var arr = [1, 5, 3, 2, 10];
var n = arr.length;
document.write( findMinRemoval(arr, n) + "<br>");

</script>
```

**Output:** 

```
7
```