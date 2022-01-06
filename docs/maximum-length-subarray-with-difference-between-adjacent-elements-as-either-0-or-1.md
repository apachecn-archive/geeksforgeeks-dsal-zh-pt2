# 相邻元素之差为 0 或 1 的最大长度子阵列

> 原文:[https://www . geesforgeks . org/最大长度-相邻元素之间有差异的子数组-非 0 即 1/](https://www.geeksforgeeks.org/maximum-length-subarray-with-difference-between-adjacent-elements-as-either-0-or-1/)

给定一组 **n 个**整数。任务是找到子阵列的最大长度，使得子阵列的所有连续元素之间的绝对差为 **0** 或 **1** 。
**举例:**

> **输入:** arr[] = {2，5，6，3，7，6，5，8}
> **输出:** 3
> {5，6}和{7，6，5}是唯一有效的子数组。
> **输入:** arr[] = {-2，-1，5，-1，4，0，3}
> **输出:** 2

**方法:**从数组的第一个元素开始，找到第一个有效的子数组并存储它的长度，然后从下一个元素(第一个子数组中没有包含的第一个元素)开始，找到另一个有效的子数组。重复该过程，直到找到所有有效的子阵列，然后打印最大子阵列的长度。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the maximum length
// of the sub-array such that the
// absolute difference between every two
// consecutive elements is either 1 or 0
int getMaxLength(int arr[],int n)
{
    int l = n;
    int i = 0, maxlen = 0;
    while (i < l)
    {
        int j = i;
        while (i+1 < l &&
             (abs(arr[i] - arr[i + 1]) == 1 ||
             abs(arr[i] - arr[i + 1]) == 0))
        {
            i++;
        }

            // Length of the valid sub-array currently
            // under consideration
            int currLen = i - j + 1;

            // Update the maximum length
            if (maxlen < currLen)
                maxlen = currLen;

            if (j == i)
                i++;
    }

    // Any valid sub-array cannot be of length 1
    //maxlen = (maxlen == 1) ? 0 : maxlen;

    // Return the maximum possible length
    return maxlen;
}

// Driver code
int main()
{
    int arr[] = { 2, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << getMaxLength(arr, n);
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function to return the maximum length
    // of the sub-array such that the
    // absolute difference between every two
    // consecutive elements is either 1 or 0
    public static int getMaxLength(int arr[])
    {

        int l = arr.length;
        int i = 0, maxlen = 0;
        while (i < l) {
            int j = i;
            while (i + 1 < l
                   && (Math.abs(arr[i] - arr[i + 1]) == 1
                       || Math.abs(arr[i] - arr[i + 1]) == 0)) {
                i++;
            }

            // Length of the valid sub-array currently
            // under cosideration
            int currLen = i - j + 1;

            // Update the maximum length
            if (maxlen < currLen)
                maxlen = currLen;

            if (j == i)
                i++;
        }

        // Any valid sub-array cannot be of length 1
        maxlen = (maxlen == 1) ? 0 : maxlen;

        // Return the maximum possible length
        return maxlen;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 4 };
        System.out.print(getMaxLength(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum length
# of the sub-array such that the
# absolute difference between every two
# consecutive elements is either 1 or 0
def getMaxLength(arr, n) :

    l = n;
    i = 0; maxlen = 0;

    while (i < l) :
        j = i;
        while (i + 1 < l and
              (abs(arr[i] - arr[i + 1]) == 1 or
               abs(arr[i] - arr[i + 1]) == 0)) :

            i += 1;

        # Length of the valid sub-array
        # currently under cosideration
        currLen = i - j + 1;

        # Update the maximum length
        if (maxlen < currLen) :
            maxlen = currLen;

        if (j == i) :
            i += 1;

    # Any valid sub-array cannot be of length 1
    # maxlen = (maxlen == 1) ? 0 : maxlen;

    # Return the maximum possible length
    return maxlen;

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 4 ];
    n = len(arr)
    print(getMaxLength(arr, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the maximum length
    // of the sub-array such that the
    // Absolute difference between every two
    // consecutive elements is either 1 or 0
    public static int getMaxLength(int []arr)
    {

        int l = arr.Length;
        int i = 0, maxlen = 0;
        while (i < l)
        {
            int j = i;
            while (i + 1 < l &&
                    (Math.Abs(arr[i] - arr[i + 1]) == 1 ||
                    Math.Abs(arr[i] - arr[i + 1]) == 0))
            {
                i++;
            }

            // Length of the valid sub-array currently
            // under consideration
            int currLen = i - j + 1;

            // Update the maximum length
            if (maxlen < currLen)
                maxlen = currLen;

            if (j == i)
                i++;
        }

        // Any valid sub-array cannot be of length 1
        maxlen = (maxlen == 1) ? 0 : maxlen;

        // Return the maximum possible length
        return maxlen;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = { 2, 4 };
        Console.Write(getMaxLength(arr));
    }
}

// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximum length
// of the sub-array such that the
// absolute difference between every two
// consecutive elements is either 1 or 0
function getMaxLength($arr, $n)
{
    $l = $n;
    $i = 0;
    $maxlen = 0;
    while ($i < $l)
    {
        $j = $i;
        while ($i + 1 < $l &&
              (abs($arr[$i] - $arr[$i + 1]) == 1 ||
                abs($arr[$i] - $arr[$i + 1]) == 0))
        {
            $i++;
        }

        // Length of the valid sub-array
        // currently under consideration
        $currLen = $i - $j + 1;

        // Update the maximum length
        if ($maxlen < $currLen)
            $maxlen = $currLen;

        if ($j == $i)
            $i++;
    }

    // Any valid sub-array cannot be of length 1
    //maxlen = (maxlen == 1) ? 0 : maxlen;

    // Return the maximum possible length
    return $maxlen;
}

// Driver code
$arr = array(2, 4 );
$n = sizeof($arr);
echo getMaxLength($arr, $n)

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum length
    // of the sub-array such that the
    // absolute difference between every two
    // consecutive elements is either 1 or 0
function getMaxLength(arr)
{
    let l = arr.length;
        let i = 0, maxlen = 0;
        while (i < l) {
            let j = i;
            while (i + 1 < l
                   && (Math.abs(arr[i] - arr[i + 1]) == 1
                       || Math.abs(arr[i] - arr[i + 1]) == 0)) {
                i++;
            }

            // Length of the valid sub-array currently
            // under cosideration
            let currLen = i - j + 1;

            // Update the maximum length
            if (maxlen < currLen)
                maxlen = currLen;

            if (j == i)
                i++;
        }

        // Any valid sub-array cannot be of length 1
        //maxlen = (maxlen == 1) ? 0 : maxlen;

        // Return the maximum possible length
        return maxlen;
}

// Driver code
let arr = [2, 4 ];
document.write(getMaxLength(arr));

// This code is contributed by rag2127.
</script>
```

**Output:** 

```
1
```