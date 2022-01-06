# 等于所有剩余元素之和的元素

> 原文:[https://www . geesforgeks . org/element-等于所有剩余元素的总和/](https://www.geeksforgeeks.org/element-equal-to-the-sum-of-all-the-remaining-elements/)

给定 N 个正元素的数组。任务是找到一个元素，这个元素等于数组中除它自己以外的所有元素的和。
**例:**

```
Input: arr[] = {1, 2, 3, 6}
Output: 6
6 is the element which is equal to the sum of all 
remaining elements i.e. 1 + 2+ 3 = 6

Input: arr[] = {2, 2, 2, 2}
Output: -1
```

**逼近:**首先求一个数组所有元素的和。然后迭代每个元素，检查条件是如果 **(a[i] == sum-a[i] )** 。如果为真，则打印**a【I】**，否则打印“-1”，如果没有找到这样的元素。
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to find the element
int findEle(int arr[], int n)
{
    // sum is use to store
    // sum of all elements
    // of array
    ll sum = 0;

    for (int i = 0; i < n; i++)
        sum += arr[i];

    // iterate over all elements
    for (int i = 0; i < n; i++)
        if (arr[i] == sum - arr[i])
            return arr[i];

    return -1;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findEle(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.io.*;

class GFG {

// Function to find the element
static int findEle(int arr[], int n)
{
    // sum is use to store
    // sum of all elements
    // of array
    int sum = 0;

    for (int i = 0; i < n; i++)
        sum += arr[i];

    // iterate over all elements
    for (int i = 0; i < n; i++)
        if (arr[i] == sum - arr[i])
            return arr[i];

    return -1;
}

// Driver code

    public static void main (String[] args) {
        int arr[] = { 1, 2, 3, 6 };
    int n = arr.length;
    System.out.print(findEle(arr, n));
    }
}
// This code is contributed by shs..
```

## 蟒蛇 3

```
# Python 3 implementation of
# the above approach

# Function to find the element
def findEle(arr, n) :

    # sum is use to store
    # sum of all elements
    # of array
    sum = 0

    for i in range(n) :
        sum += arr[i]

    # iterate over all elements
    for i in range(n) :
        if arr[i] == sum - arr[i] :
            return arr[i]

    return -1

# Driver Code
if __name__ == "__main__" :

    arr = [1, 2, 3, 6 ]
    n = len(arr)
    print(findEle(arr, n))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG
{

// Function to find the element
static int findEle(int []arr, int n)
{
    // sum is use to store
    // sum of all elements
    // of array
    int sum = 0;

    for (int i = 0; i < n; i++)
        sum += arr[i];

    // iterate over all elements
    for (int i = 0; i < n; i++)
        if (arr[i] == sum - arr[i])
            return arr[i];

    return -1;
}

// Driver code
static public void Main (String []args)
{
    int []arr = { 1, 2, 3, 6 };
    int n = arr.Length;
    Console.WriteLine(findEle(arr, n));
}
}

// This code is contributed
// by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find the element
function findEle($arr, $n)
{
    // sum is use to store
    // sum of all elements
    // of array
    $sum = 0;

    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];

    // iterate over all elements
    for ($i = 0; $i < $n; $i++)
        if ($arr[$i] == $sum - $arr[$i])
            return $arr[$i];

    return -1;
}

// Driver code
$arr= array(1, 2, 3, 6 );
$n = sizeof($arr);
echo findEle($arr, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// javascript implementation of the above approach

// Function to find the element
function findEle(arr, n)
{
    // sum is use to store
    // sum of all elements
    // of array
    var sum = 0;

    for (var i = 0; i < n; i++)
        sum += arr[i];

    // iterate over all elements
    for (var i = 0; i < n; i++)
        if (arr[i] == sum - arr[i])
            return arr[i];

    return -1;
}

// Driver code
    var arr = [1, 2, 3, 6];
    var n = arr.length;
    document.write(findEle(arr, n));

// This code is contributed by ipg016107.
</script>
```

**Output:** 

```
6
```

**注:**上述问题可以用[中使用的概念来解决，检查数组中是否有一个元素等于所有剩余元素的和。](https://www.geeksforgeeks.org/check-if-the-array-has-an-element-which-is-equal-to-sum-of-all-the-remaining-elements/)