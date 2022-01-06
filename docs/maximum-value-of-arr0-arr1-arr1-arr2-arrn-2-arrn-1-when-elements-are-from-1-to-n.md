# 当元素从 1 到 n 时| arr[0]–arr[1]|+| arr[1]–arr[2]|+…| arr[n–2]–arr[n–1]|的最大值

> 原文:[https://www . geeksforgeeks . org/arr 0-arr 1-arr 1-arr 2-arrn-2-arrn-1-当-elements-from-1-n/](https://www.geeksforgeeks.org/maximum-value-of-arr0-arr1-arr1-arr2-arrn-2-arrn-1-when-elements-are-from-1-to-n/)

给定一个大小为 **n** 的数组 **arr[]** ，其元素来自范围**【1，n】**。任务是找到**| arr[0]–arr[1]|+| arr[1]–arr[2]|+…+| arr[n–2]–arr[n–1]|**的最大值。您可以按任何顺序排列数组中的数字。
**举例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 7
> 按此方式排列数组求最大值，arr[] = {3，1，4，2 }
> | 3–1 |+| 1–4 |+| 4–2 | = 2+3+2 = 7
> **输入:** arr[] = {1，2，3}
> **输出:** 3
> 我们排列

一个简单的方法是[生成所有可能的排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)。计算每个排列的值，找出最大值。
**有效方法:**
一个元素的最大和为 0。
两个元素的最大和为 1
三个元素的最大和为 3(如上所述)
四个元素的最大和为 7(如上所述)
可以观察到，对于 **n** 的不同值，绝对差的最大和的模式为 **0、1、3、7、11、17、23、31、39、49、…..**其 **n <sup>第</sup>** 项为**((n * n/2)–1)**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// required value
int maxValue(int n)
{
    if (n == 1)
        return 0;

    return ((n * n / 2) - 1);
}

// Driver code
int main()
{
    int n = 4;
    cout << maxValue(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the maximum
    // required value
    static int maxValue(int n)
    {
        if (n == 1)
            return 0;

        return ((n * n / 2) - 1);
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 4;
        System.out.print(maxValue(n));
    }
}
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the maximum
# required value
def maxValue(n):
    if (n == 1):
        return 0

    return (( n * n // 2 ) - 1 )

# Driver code
n = 4
print(maxValue(n))
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to return the maximum
    // required value
    static int maxValue(int n)
    {
        if (n == 1)
            return 0;

        return ((n * n / 2) - 1);
    }

    // Driver code
    public static void Main()
    {
        int n = 4;
        Console.WriteLine(maxValue(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function to return the maximum
// required value
function maxValue($n)
{
    if ($n == 1)
        return 0;

    return (($n * $n / 2) - 1);
}

// Driver code
$n = 4;
echo maxValue($n);
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the maximum
// required value
function maxValue(n)
{
    if (n == 1)
        return 0;
    return (parseInt(n * n / 2) - 1);
}

// Driver code
var n = 4;
document.write(maxValue(n));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
7
```

**时间复杂度:** O(1)