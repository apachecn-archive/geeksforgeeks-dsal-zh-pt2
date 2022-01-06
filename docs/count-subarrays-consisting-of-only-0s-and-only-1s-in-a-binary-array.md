# 计数二进制数组中仅由 0 和 1 组成的子数组

> 原文:[https://www . geesforgeks . org/count-subarrays-由二进制数组中只有 0 和只有 1 组成/](https://www.geeksforgeeks.org/count-subarrays-consisting-of-only-0s-and-only-1s-in-a-binary-array/)

给定一个只包含 0 和 1 的二进制数组。任务是找到:

*   只有 1 的子阵的数目。
*   只有 0 的子阵的数目。

**例:**

> **输入:** arr[] = {0，0，1，0，1，0，1，0，1，0，1，1}
> **输出:**
> 仅由 0 组成的子阵数量:7
> 仅由 1 组成的子阵数量:7
> **输入:** arr[] = {1，1，0，0，1，0，1，0，1，1}
> **输出:**

**方法:**要计数 1，想法是开始使用计数器遍历数组。如果当前元素为 1，则递增计数器，否则将计数器*(计数器+1)/2 添加到子阵列的数量中，并将计数器重新初始化为 0。同样，找出只有 0 的子阵的数量。
以下是上述办法的实施情况:

## C++

```
// C++ program to count the number of subarrays
// that having only 0's and only 1's
#include <bits/stdc++.h>
using namespace std;

// Function to count number of subarrays
void countSubarraysof1and0(int a[], int n)
{
    int count1 = 0, count0 = 0;

    int number1 = 0, number0 = 0;

    // Iterate in the array to find count
    // of subarrays with only 1 in it
    for (int i = 0; i < n; i++) {
        // check if array element
        // is 1 or not
        if (a[i] == 1) {
            count1 += 1;
        }
        else {
            number1 += (count1) * (count1 + 1) / 2;
            count1 = 0;
        }
    }

    // Iterate in the array to find count
    // of subarrays with only 0 in it
    for (int i = 0; i < n; i++) {
        // check if array element
        // is 0 or not
        if (a[i] == 0) {
            count0 += 1;
        }
        else {
            number0 += (count0) * (count0 + 1) / 2;
            count0 = 0;
        }
    }

    // After iteration completes,
    // check for the last set of subarrays
    if (count1)
        number1 += (count1) * (count1 + 1) / 2;

    if (count0)
        number0 += (count0) * (count0 + 1) / 2;

    cout << "Count of subarrays of 0 only: " << number0;
    cout << "\nCount of subarrays of 1 only: " << number1;
}

// Driver Code
int main()
{
    int a[] = { 1, 1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 1 };
    int n = sizeof(a) / sizeof(a[0]);

    countSubarraysof1and0(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number of subarrays
// that having only 0's and only 1's

import java.io.*;

class GFG {

// Function to count number of subarrays
static void countSubarraysof1and0(int a[], int n)
{
    int count1 = 0, count0 = 0;

    int number1 = 0, number0 = 0;

    // Iterate in the array to find count
    // of subarrays with only 1 in it
    for (int i = 0; i < n; i++) {
        // check if array element
        // is 1 or not
        if (a[i] == 1) {
            count1 += 1;
        }
        else {
            number1 += (count1) * (count1 + 1) / 2;
            count1 = 0;
        }
    }

    // Iterate in the array to find count
    // of subarrays with only 0 in it
    for (int i = 0; i < n; i++) {
        // check if array element
        // is 0 or not
        if (a[i] == 0) {
            count0 += 1;
        }
        else {
            number0 += (count0) * (count0 + 1) / 2;
            count0 = 0;
        }
    }

    // After iteration completes,
    // check for the last set of subarrays
    if (count1>0)
        number1 += (count1) * (count1 + 1) / 2;

    if (count0>0)
        number0 += (count0) * (count0 + 1) / 2;

    System.out.println("Count of subarrays of 0 only: " + number0);
    System.out.println( "\nCount of subarrays of 1 only: " + number1);
}

// Driver Code

    public static void main (String[] args) {
        int a[] = { 1, 1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 1 };
    int n = a.length;

    countSubarraysof1and0(a, n);;
    }
}
// This code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python 3 program to count the number of
# subarrays that having only 0's and only 1's

# Function to count number of subarrays
def countSubarraysof1and0(a, n):
    count1 = 0
    count0 = 0

    number1 = 0
    number0 = 0

    # Iterate in the array to find count
    # of subarrays with only 1 in it
    for i in range(0, n, 1):

        # check if array element is 1 or not
        if (a[i] == 1):
            count1 += 1
        else:
            number1 += ((count1) *
                        (count1 + 1) / 2)
            count1 = 0

    # Iterate in the array to find count
    # of subarrays with only 0 in it
    for i in range(0, n, 1):

        # check if array element
        # is 0 or not
        if (a[i] == 0):
            count0 += 1
        else:
            number0 += (count0) * (count0 + 1) / 2
            count0 = 0

    # After iteration completes,
    # check for the last set of subarrays
    if (count1):
        number1 += (count1) * (count1 + 1) / 2

    if (count0):
        number0 += (count0) * (count0 + 1) / 2

    print("Count of subarrays of 0 only:",
                             int(number0))
    print("Count of subarrays of 1 only:",
                             int(number1))

# Driver Code
if __name__ == '__main__':
    a = [1, 1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 1]
    n = len(a)

    countSubarraysof1and0(a, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to count the number of subarrays
// that having only 0's and only 1's

using System;

class GFG {

// Function to count number of subarrays
static void countSubarraysof1and0(int []a, int n)
{
    int count1 = 0, count0 = 0;

    int number1 = 0, number0 = 0;

    // Iterate in the array to find count
    // of subarrays with only 1 in it
    for (int i = 0; i < n; i++) {
        // check if array element
        // is 1 or not
        if (a[i] == 1) {
            count1 += 1;
        }
        else {
            number1 += (count1) * (count1 + 1) / 2;
            count1 = 0;
        }
    }

    // Iterate in the array to find count
    // of subarrays with only 0 in it
    for (int i = 0; i < n; i++) {
        // check if array element
        // is 0 or not
        if (a[i] == 0) {
            count0 += 1;
        }
        else {
            number0 += (count0) * (count0 + 1) / 2;
            count0 = 0;
        }
    }

    // After iteration completes,
    // check for the last set of subarrays
    if (count1>0)
        number1 += (count1) * (count1 + 1) / 2;

    if (count0>0)
        number0 += (count0) * (count0 + 1) / 2;

    Console.WriteLine("Count of subarrays of 0 only: " + number0);
    Console.WriteLine( "\nCount of subarrays of 1 only: " + number1);
}

// Driver Code

    public static void Main () {
        int []a = { 1, 1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 1 };
    int n = a.Length;

    countSubarraysof1and0(a, n);;
    }
}
// This code is contributed by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count the number
// of subarrays that having only
// 0's and only 1's

// Function to count number of subarrays
function countSubarraysof1and0($a, $n)
{
    $count1 = 0; $count0 = 0;

    $number1 = 0; $number0 = 0;

    // Iterate in the array to find count
    // of subarrays with only 1 in it
    for ($i = 0; $i <$n; $i++)
    {
        // check if array element
        // is 1 or not
        if ($a[$i] == 1)
        {
            $count1 += 1;
        }
        else
        {
            $number1 += ($count1) *
                        ($count1 + 1) / 2;
            $count1 = 0;
        }
    }

    // Iterate in the array to find count
    // of subarrays with only 0 in it
    for ($i = 0; $i <$n; $i++)
    {
        // check if array element
        // is 0 or not
        if ($a[$i] == 0)
        {
            $count0 += 1;
        }
        else
        {
            $number0 += ($count0) *
                        ($count0 + 1) / 2;
            $count0 = 0;
        }
    }

    // After iteration completes,
    // check for the last set of subarrays
    if ($count1)
        $number1 += ($count1) *
                    ($count1 + 1) / 2;

    if ($count0)
        $number0 += ($count0) *
                    ($count0 + 1) / 2;

    echo "Count of subarrays of 0 only: " , $number0;
    echo "\nCount of subarrays of 1 only: " , $number1;
}

// Driver Code
$a = array( 1, 1, 0, 0, 1, 0,
            1, 0, 1, 1, 1, 1 );
$n = count($a);

countSubarraysof1and0($a, $n);

// This code is contributed by inder_verma
?>
```

## java 描述语言

```
<script>

// Javascript program to count the number of subarrays
// that having only 0's and only 1's

// Function to count number of subarrays
function countSubarraysof1and0(a, n)
{
    let count1 = 0, count0 = 0;

    let number1 = 0, number0 = 0;

    // Iterate in the array to find count
    // of subarrays with only 1 in it
    for (let i = 0; i < n; i++) {
        // check if array element
        // is 1 or not
        if (a[i] == 1) {
            count1 += 1;
        }
        else {
            number1 += (count1) * (count1 + 1) / 2;
            count1 = 0;
        }
    }

    // Iterate in the array to find count
    // of subarrays with only 0 in it
    for (let i = 0; i < n; i++) {
        // check if array element
        // is 0 or not
        if (a[i] == 0) {
            count0 += 1;
        }
        else {
            number0 += (count0) * (count0 + 1) / 2;
            count0 = 0;
        }
    }

    // After iteration completes,
    // check for the last set of subarrays
    if (count1>0)
        number1 += (count1) * (count1 + 1) / 2;

    if (count0>0)
        number0 += (count0) * (count0 + 1) / 2;

    document.write("Count of subarrays of 0 only: " + number0 + "<br/>");
    document.write( "\nCount of subarrays of 1 only: " + number1);
}

// driver program

    let a = [ 1, 1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 1 ];
    let n = a.length;

    countSubarraysof1and0(a, n);

</script>
```

**Output:** 

```
Count of subarrays of 0 only: 5
Count of subarrays of 1 only: 15
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)