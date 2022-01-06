# 重复给定阵列 k 次形成的阵列中的最大子阵列和

> 原文:[https://www . geesforgeks . org/maximum-subarray-sum-in-array-formed-by-repeating-the-给定数组-k-times/](https://www.geeksforgeeks.org/maximum-subarray-sum-in-array-formed-by-repeating-the-given-array-k-times/)

给定一个整数 **k** 和一个由 **n** 个元素组成的整数数组**arr【】**，任务是在修改后的数组(通过重复给定的数组 k 次形成)中找到最大的子数组和。例如，如果 arr[] = {1，2}和 k = 3，则修改后的数组将是{1，2，1，2，1，2}。
**举例:**

> **输入:** arr[] = {1，2}，k = 3
> **输出:** 9
> 修改后的数组将为{1，2，1，2，1，2}
> ，最大子数组和将为 1 + 2 + 1 + 2 + 1 + 2 = 9
> **输入:** arr[] = {1，-2，1}，k = 5
> **输出:** 2

一个**简单的解决方案**是创建一个大小为 **n * k** 的数组，然后运行[卡丹的算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)来寻找最大的子数组和。时间复杂度为 **O(n * k)** 加上辅助空间 **O(n * k)** 。
一个**更好的解决方案**是计算数组**arr【】**的和，存储在 **sum** 中。

*   如果**求和< 0** ，则计算通过两次连接数组形成的数组的最大子数组和，而不考虑 **K** 。例如，取 arr[] = {1，-4，1}和 k = 5。数组的总和小于 0。因此，只要将数组连接两次，就可以找到数组的最大子数组和，而不考虑 **K** 的值，即 b[] = {1，-4，1，1，-4，1}，最大子数组和= 1 + 1 = 2
*   如果**求和> 0** ，那么最大子阵列将包括在前一步中计算的最大和(其中阵列被连接两次)+阵列的其余(k–2)次重复也可以包括在内，因为它们的和大于 0，这将有助于最大和。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

    // Function to concatenate array
    void arrayConcatenate(int *arr, int *b,
                                int k,int len)
    {
        // Array b will be formed by concatenation
        // array a exactly k times
        int j = 0;
        while (k > 0)
        {

            for (int i = 0; i < len; i++)
            {
                b[j++] = arr[i];
            }
            k--;
        }
    }

    // Function to return the maximum
    // subarray sum of arr[]
    long maxSubArrSum(int *a,int len)
    {
        int size = len;
        int max_so_far = INT_MIN;
        long max_ending_here = 0;

        for (int i = 0; i < size; i++)
        {
            max_ending_here = max_ending_here + a[i];
            if (max_so_far < max_ending_here)
                max_so_far = max_ending_here;
            if (max_ending_here < 0)
                max_ending_here = 0;
        }
        return max_so_far;
    }

    // Function to return the maximum sub-array
    // sum of the modified array
    long maxSubKSum(int *arr, int k,int len)
    {
        int arrSum = 0;
        long maxSubArrSum1 = 0;

        int b[(2 * len)]={0};

        // Concatenating the array 2 times
        arrayConcatenate(arr, b, 2,len);

        // Finding the sum of the array
        for (int i = 0; i < len; i++)
            arrSum += arr[i];

        // If sum is less than zero
        if (arrSum < 0)
            maxSubArrSum1 = maxSubArrSum(b,2*len);

        // If sum is greater than zero
        else
            maxSubArrSum1 = maxSubArrSum(b,2*len) +
                        (k - 2) * arrSum;

        return maxSubArrSum1;
    }

    // Driver code
    int main()
    {
        int arr[] = { 1, -2, 1 };
        int arrlen=sizeof(arr)/sizeof(arr[0]);
        int k = 5;
        cout << maxSubKSum(arr, k,arrlen) << endl;
        return 0;
    }

// This code is contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function to concatenate array
    static void arrayConcatenate(int arr[], int b[],
                                             int k)
    {
        // Array b will be formed by concatenation
        // array a exactly k times
        int j = 0;
        while (k > 0) {

            for (int i = 0; i < arr.length; i++) {
                b[j++] = arr[i];
            }
            k--;
        }
    }

    // Function to return the maximum
    // subarray sum of arr[]
    static int maxSubArrSum(int a[])
    {
        int size = a.length;
        int max_so_far = Integer.MIN_VALUE,
            max_ending_here = 0;

        for (int i = 0; i < size; i++) {
            max_ending_here = max_ending_here + a[i];
            if (max_so_far < max_ending_here)
                max_so_far = max_ending_here;
            if (max_ending_here < 0)
                max_ending_here = 0;
        }
        return max_so_far;
    }

    // Function to return the maximum sub-array
    // sum of the modified array
    static long maxSubKSum(int arr[], int k)
    {
        int arrSum = 0;
        long maxSubArrSum = 0;

        int b[] = new int[(2 * arr.length)];

        // Concatenating the array 2 times
        arrayConcatenate(arr, b, 2);

        // Finding the sum of the array
        for (int i = 0; i < arr.length; i++)
            arrSum += arr[i];

        // If sum is less than zero
        if (arrSum < 0)
            maxSubArrSum = maxSubArrSum(b);

        // If sum is greater than zero
        else
            maxSubArrSum = maxSubArrSum(b) +
                          (k - 2) * arrSum;

        return maxSubArrSum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, -2, 1 };
        int k = 5;
        System.out.println(maxSubKSum(arr, k));
    }
}
```

## 蟒蛇 3

```
# Python approach to this problem

# A python module where element
# are added to list k times
def MaxsumArrKtimes(c, ktimes):

    # Store element in list d k times
    d = c * ktimes

    # two variable which can keep
    # track of maximum sum seen
    # so far and maximum sum ended.
    maxsofar = -99999
    maxending = 0

    for i in d:
        maxending = maxending + i
        if maxsofar < maxending:
            maxsofar = maxending
        if maxending < 0:
            maxending = 0
    return maxsofar

# Get the Maximum sum of element
print(MaxsumArrKtimes([1, -2, 1], 5))

# This code is contributed by AnupGaurav.

```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to concatenate array
static void arrayConcatenate(int []arr,
                             int []b, int k)
{
    // Array b will be formed by concatenation
    // array a exactly k times
    int j = 0;
    while (k > 0)
    {
        for (int i = 0; i < arr.Length; i++)
        {
            b[j++] = arr[i];
        }
        k--;
    }
}

// Function to return the maximum
// subarray sum of arr[]
static int maxSubArrSum(int []a)
{
    int size = a.Length;
    int max_so_far = int.MinValue,
        max_ending_here = 0;

    for (int i = 0; i < size; i++)
    {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;
        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to return the maximum sub-array
// sum of the modified array
static long maxSubKSum(int []arr, int k)
{
    int arrSum = 0;
    long maxSubArrsum = 0;

    int []b = new int[(2 * arr.Length)];

    // Concatenating the array 2 times
    arrayConcatenate(arr, b, 2);

    // Finding the sum of the array
    for (int i = 0; i < arr.Length; i++)
        arrSum += arr[i];

    // If sum is less than zero
    if (arrSum < 0)
        maxSubArrsum = maxSubArrSum(b);

    // If sum is greater than zero
    else
        maxSubArrsum = maxSubArrSum(b) +
                       (k - 2) * arrSum;

    return maxSubArrsum;
}

// Driver code
public static void Main()
{
    int []arr = { 1, -2, 1 };
    int k = 5;
    Console.WriteLine(maxSubKSum(arr, k));
}
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP implementation of the approach

// Function to concatenate array
function arrayConcatenate(&$arr, &$b, $k)
{
    // Array b will be formed by concatenation
    // array a exactly k times
    $j = 0;
    while ($k > 0)
    {

        for ($i = 0; $i < sizeof($arr); $i++)
        {
            $b[$j++] = $arr[$i];
        }
        $k--;
    }
}

// Function to return the maximum
// subarray sum of arr[]
function maxSubArrSum(&$a)
{
    $size = sizeof($a);
    $max_so_far = 0;
    $max_ending_here = 0;

    for ($i = 0; $i < $size; $i++)
    {
        $max_ending_here = $max_ending_here + $a[$i];
        if ($max_so_far < $max_ending_here)
            $max_so_far = $max_ending_here;
        if ($max_ending_here < 0)
            $max_ending_here = 0;
    }
    return $max_so_far;
}

// Function to return the maximum sub-array
// sum of the modified array
function maxSubKSum(&$arr,$k)
{
    $arrSum = 0;
    $maxSubArrSum = 0;

    $b = array_fill(0,(2 * sizeof($arr)),NULL);

    // Concatenating the array 2 times
    arrayConcatenate($arr, $b, 2);

    // Finding the sum of the array
    for ($i = 0; $i < sizeof($arr); $i++)
        $arrSum += $arr[$i];

    // If sum is less than zero
    if ($arrSum < 0)
        $maxSubArrSum = maxSubArrSum($b);

    // If sum is greater than zero
    else
        $maxSubArrSum = maxSubArrSum($b) +
                    ($k - 2) * $arrSum;

    return $maxSubArrSum;
}

    // Driver code
    $arr = array(1, -2, 1 );
    $k = 5;
    echo maxSubKSum($arr, $k);

// This code is contributed by Ita_c.   
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to concatenate array
function arrayConcatenate(arr,b,k)
{
    // Array b will be formed by concatenation
        // array a exactly k times
        let j = 0;
        while (k > 0) {

            for (let i = 0; i < arr.length; i++) {
                b[j++] = arr[i];
            }
            k--;
        }
}

// Function to return the maximum
    // subarray sum of arr[]
function maxSubArrSum(a)
{
    let size = a.length;
        let max_so_far = Number.MIN_VALUE,
            max_ending_here = 0;

        for (let i = 0; i < size; i++) {
            max_ending_here = max_ending_here + a[i];
            if (max_so_far < max_ending_here)
                max_so_far = max_ending_here;
            if (max_ending_here < 0)
                max_ending_here = 0;
        }
        return max_so_far;
}

// Function to return the maximum sub-array
    // sum of the modified array
function maxSubKSum(arr,k)
{
    let arrSum = 0;
        let maxsubArrSum = 0;

        let b = new Array(2 * arr.length);

        // Concatenating the array 2 times
        arrayConcatenate(arr, b, 2);

        // Finding the sum of the array
        for (let i = 0; i < arr.length; i++)
            arrSum += arr[i];

        // If sum is less than zero
        if (arrSum < 0)
            maxsubArrSum = maxSubArrSum(b);

        // If sum is greater than zero
        else
            maxsubArrSum = maxSubArrSum(b) +
                          (k - 2) * arrSum;

        return maxsubArrSum;
}

 // Driver code
let arr=[ 1, -2, 1 ];
let k = 5;
document.write(maxSubKSum(arr, k));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)