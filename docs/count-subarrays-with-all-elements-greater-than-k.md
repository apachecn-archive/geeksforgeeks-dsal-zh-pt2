# 计数所有元素大于 K 的子阵列

> 原文:[https://www . geesforgeks . org/count-subarray-带全元素-大于-k/](https://www.geeksforgeeks.org/count-subarrays-with-all-elements-greater-than-k/)

给定一个由 N 个整数和一个数 K 组成的数组，任务是找到子数组的个数，使其中的所有元素都大于 K。

**示例:**

> **输入** : a[] = {3，4，5，6，7，2，10，11}，K = 5
> **输出** : 6
> 可能的子阵有{6}、{7}、{6，7}、{10}、{11}和{10，11}。
> **输入** : a[] = {8，25，10，19，19，18，20，11，18}，K = 13
> **输出** : 12

**方法:**想法是开始使用计数器遍历数组。如果当前元素大于给定值 X，则递增计数器，否则将计数器*(计数器+1)/2 添加到子阵列的数量中，并将计数器重新初始化为 0。

下面是上述方法的实现:

## C++

```
// C++ program to print the number of subarrays such
// that all elements are greater than K
#include <bits/stdc++.h>
using namespace std;

// Function to count number of subarrays
int countSubarrays(int a[], int n, int x)
{
    int count = 0;

    int number = 0;

    // Iterate in the array
    for (int i = 0; i < n; i++) {

        // check if array element
        // greater then X or not
        if (a[i] > x) {
            count += 1;
        }
        else {

            number += (count) * (count + 1) / 2;
            count = 0;
        }
    }

    // After iteration complete
    // check for the last set of subarrays
    if (count)
        number += (count) * (count + 1) / 2;

    return number;
}

// Driver Code
int main()
{
    int a[] = { 3, 4, 5, 6, 7, 2, 10, 11 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 5;

    cout << countSubarrays(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the number of subarrays such
// that all elements are greater than K

import java.io.*;

class GFG {

// Function to count number of subarrays
static int countSubarrays(int a[], int n, int x)
{
    int count = 0;

    int number = 0;

    // Iterate in the array
    for (int i = 0; i < n; i++) {

        // check if array element
        // greater then X or not
        if (a[i] > x) {
            count += 1;
        }
        else {

            number += (count) * (count + 1) / 2;
            count = 0;
        }
    }

    // After iteration complete
    // check for the last set of subarrays
    if (count!=0)
        number += (count) * (count + 1) / 2;

    return number;
}

// Driver Code
    public static void main (String[] args) {
        int a[] = { 3, 4, 5, 6, 7, 2, 10, 11 };
        int n = a.length;
        int k = 5;

        System.out.println (countSubarrays(a, n, k));

    }
}
```

## 蟒蛇 3

```
# Python program to print the number of
# subarrays such that all elements are
# greater than K

# Function to count number of subarrays
def countSubarrays(a, n, x):
    count = 0
    number = 0

    # Iterate in the array
    for i in range(n):

        # check if array element greater
        # then X or not
        if (a[i] > x):
            count += 1
        else:
            number += (count) * (count + 1) / 2
            count = 0

    # After iteration complete check for
    # the last set of subarrays
    if (count):
        number += (count) * (count + 1) / 2
    return int(number)

# Driver Code
if __name__ == '__main__':
    a = [3, 4, 5, 6, 7, 2, 10, 11]
    n = len(a)
    k = 5
    print(countSubarrays(a, n, k))

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to print the number of subarrays such
// that all elements are greater than K

using System;

class GFG {

// Function to count number of subarrays
static int countSubarrays(int []a, int n, int x)
{
    int count = 0;

    int number = 0;

    // Iterate in the array
    for (int i = 0; i < n; i++) {

        // check if array element
        // greater then X or not
        if (a[i] > x) {
            count += 1;
        }
        else {

            number += (count) * (count + 1) / 2;
            count = 0;
        }
    }

    // After iteration complete
    // check for the last set of subarrays
    if (count!=0)
        number += (count) * (count + 1) / 2;

    return number;
}

// Driver Code
    public static void Main () {
        int []a = { 3, 4, 5, 6, 7, 2, 10, 11 };
        int n = a.Length;
        int k = 5;

        Console.WriteLine(countSubarrays(a, n, k));

    }
}
// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the number
// of subarrays such that all
// elements are greater than K

// Function to count number
// of subarrays
function countSubarrays($a, $n, $x)
{
    $count = 0; $number = 0;

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
            $number += ($count) *
                       ($count + 1) / 2;
            $count = 0;
        }
    }

    // After iteration complete
    // check for the last set
    // of subarrays
    if ($count)
        $number += ($count) *
                   ($count + 1) / 2;

    return $number;
}

// Driver Code
$a = array(3, 4, 5, 6, 7, 2, 10, 11);
$n = count($a);
$k = 5;

echo countSubarrays($a, $n, $k);

// This code is contributed by anuj_67
?>
```

## java 描述语言

```
<script>
// javascript program to print the number of subarrays such
// that all elements are greater than K    
// Function to count number of subarrays
    function countSubarrays(a , n , x) {
        var count = 0;

        var number = 0;

        // Iterate in the array
        for (i = 0; i < n; i++) {

            // check if array element
            // greater then X or not
            if (a[i] > x) {
                count += 1;
            } else {

                number += (count) * (count + 1) / 2;
                count = 0;
            }
        }

        // After iteration complete
        // check for the last set of subarrays
        if (count != 0)
            number += (count) * (count + 1) / 2;

        return number;
    }

    // Driver Code

        var a = [ 3, 4, 5, 6, 7, 2, 10, 11 ];
        var n = a.length;
        var k = 5;

        document.write(countSubarrays(a, n, k));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
6
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)