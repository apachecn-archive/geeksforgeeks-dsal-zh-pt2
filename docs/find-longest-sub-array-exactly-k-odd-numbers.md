# 找出正好有 k 个奇数的最长子阵列

> 原文:[https://www . geesforgeks . org/find-最长-子数组-精确-k-奇数/](https://www.geeksforgeeks.org/find-longest-sub-array-exactly-k-odd-numbers/)

给定大小为 **n** 的数组。问题是找到最长的子阵列，该子阵列恰好具有 **k** 个奇数。
示例:

```
Input : arr[] = {2, 3, 4, 11, 4, 12, 7}, k = 1
Output : 4
The sub-array is {4, 11, 4, 12}.

Input : arr[] = {3, 4, 6, 1, 9, 8, 2, 10}, k = 2
Output : 7
The sub-array is {4, 6, 1, 9, 8, 2, 10}.
```

**天真法:**考虑所有子阵列，统计其中奇数个数。返回正好有“k”个奇数且长度最大的长度。时间的复杂性来自 O(n^2).
**高效途径:**思路是使用[推拉窗](https://www.geeksforgeeks.org/window-sliding-technique/)。

```
longSubarrWithKOddNum(arr, n, k)
    Initialize max = 0, count = 0, start = 0

    for i = 0 to n-1
        if arr[i] % 2 != 0, then
        count++
    while (count > k && start <= i)    
        if arr[start++] % 2 != 0, then
            count--
    if count == k, then
        if max < (i - start + 1), then
            max = i - start + 1    
    return max
```

## C++

```
// C++ implementation to find the longest
// sub-array having exactly k odd numbers
#include <bits/stdc++.h>
using namespace std;

// function to find the longest sub-array
// having exactly k odd numbers
int longSubarrWithKOddNum(int arr[], int n,
                                     int k)
{
    int max = 0, count = 0, start = 0;

    // traverse the given array
    for (int i = 0; i < n; i++) {
        // if number is odd increment count
        if (arr[i] % 2 != 0)
            count++;

        // remove elements from sub-array from
        // 'start' index when count > k
        while (count > k && start <= i)   
            if (arr[start++] % 2 != 0)
                count--;

        // if count == k, then compare max with
        // current sub-array length
        if (count == k)
            if (max < (i - start + 1))
                max = i - start + 1;
    }

    // required length
    return max;
}

// Driver program to test above
int main()
{
    int arr[] = {3, 4, 6, 1, 9, 8, 2, 10};
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;

    cout << "Length = "
         << longSubarrWithKOddNum(arr, n, k);

    return 0;    
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the longest
// sub-array having exactly k odd numbers
import java.io.*;

class GFG {

    // function to find the longest sub-array
    // having exactly k odd numbers
    static int longSubarrWithKOddNum(int arr[], int n,
                                        int k)
    {
        int max = 0, count = 0, start = 0;

        // traverse the given array
        for (int i = 0; i < n; i++)
        {
            // if number is odd increment count
            if (arr[i] % 2 != 0)
                count++;

            // remove elements from sub-array from
            // 'start' index when count > k
            while (count > k && start <= i)
                if (arr[start++] % 2 != 0)
                    count--;

            // if count == k, then compare max
            // with current sub-array length
            if (count == k)
                if (max < (i - start + 1))
                    max = i - start + 1;
        }

        // required length
        return max;
    }

    // Driver program
    public static void main(String args[])
    {
        int arr[] = {3, 4, 6, 1, 9, 8, 2, 10};
        int n = arr.length;
        int k = 2;

        System.out.println("Length = "
                          + longSubarrWithKOddNum(arr, n, k));
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 implementation to find the longest
# sub-array having exactly k odd numbers

# Function to find the longest sub-array
# having exactly k odd numbers
def longSubarrWithKOddNum(arr, n, k) :

    mx, count, start = 0, 0, 0

    # Traverse the given array
    for i in range(0, n) :

        # if number is odd increment count
        if (arr[i] % 2 != 0) :
            count = count + 1

        # remove elements from sub-array from
        # 'start' index when count > k
        while (count > k and start <= i) :

            if (arr[start] % 2 != 0) :
                count = count - 1

            start = start + 1

        # if count == k, then compare max 
        # with current sub-array length
        if (count == k) :
            if (mx < (i - start + 1)) :
                mx = i - start + 1

    # required length
    return mx

# Driver Code
arr = [3, 4, 6, 1, 9, 8, 2, 10]
n = len(arr)
k = 2

print("Length = ", longSubarrWithKOddNum(arr, n, k))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# implementation to find the longest
// sub-array having exactly k odd numbers
using System;

class GFG {

    // function to find the longest sub-array
    // having exactly k odd numbers
    static int longSubarrWithKOddNum(int []arr, int n,
                                                int k)
    {
        int max = 0, count = 0, start = 0;

        // traverse the given array
        for (int i = 0; i < n; i++)
        {
            // if number is odd increment count
            if (arr[i] % 2 != 0)
                count++;

            // remove elements from sub-array from
            // 'start' index when count > k
            while (count > k && start <= i)
                if (arr[start++] % 2 != 0)
                    count--;

            // if count == k, then compare max
            // with current sub-array length
            if (count == k)
                if (max < (i - start + 1))
                    max = i - start + 1;
        }

        // required length
        return max;
    }

    // Driver program
    public static void Main()
    {
        int []arr = {3, 4, 6, 1, 9, 8, 2, 10};
        int n = arr.Length;
        int k = 2;

        Console.WriteLine("Length = "
                        + longSubarrWithKOddNum(arr, n, k));
    }
}

// This code is contributed
// by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the longest
// sub-array having exactly k odd numbers

// function to find the longest sub-array
// having exactly k odd numbers
function longSubarrWithKOddNum($arr, $n,
                                    $k)
{
    $max = 0; $count = 0; $start = 0;

    // traverse the given array
    for ($i = 0; $i < $n; $i++)
    {

        // if number is odd increment count
        if ($arr[$i] % 2 != 0)
            $count++;

        // remove elements from sub-array from
        // 'start' index when count > k
        while ($count > $k && $start <= $i)
            if ($arr[$start++] % 2 != 0)
                $count--;

        // if count == k, then compare max with
        // current sub-array length
        if ($count == $k)
            if ($max < ($i - $start + 1))
                $max = $i - $start + 1;
    }

    // required length
    return $max;
}

// Driver Code
{
    $arr = array(3, 4, 6, 1, 9, 8, 2, 10);
    $n = sizeof($arr) / sizeof($arr[0]);
    $k = 2;

    echo "Length = ", longSubarrWithKOddNum($arr, $n, $k);
    return 0;    
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the longest
// sub-array having exactly k odd numbers

// function to find the longest sub-array
// having exactly k odd numbers
function longSubarrWithKOddNum(arr, n, k)
{
    var max = 0, count = 0, start = 0;

    // traverse the given array
    for (var i = 0; i < n; i++) {
        // if number is odd increment count
        if (arr[i] % 2 != 0)
            count++;

        // remove elements from sub-array from
        // 'start' index when count > k
        while (count > k && start <= i)   
            if (arr[start++] % 2 != 0)
                count--;

        // if count == k, then compare max with
        // current sub-array length
        if (count == k)
            if (max < (i - start + 1))
                max = i - start + 1;
    }

    // required length
    return max;
}

// Driver program to test above
var arr = [3, 4, 6, 1, 9, 8, 2, 10];
var n = arr.length;
var k = 2;

document.write( "Length = "
     +  longSubarrWithKOddNum(arr, n, k));

</script>
```

输出:

```
Length = 7
```

时间复杂度:O(n)。