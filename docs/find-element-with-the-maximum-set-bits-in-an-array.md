# 查找数组中具有最大设置位的元素

> 原文:[https://www . geesforgeks . org/find-element-with-the-max-set-bits-in-array/](https://www.geeksforgeeks.org/find-element-with-the-maximum-set-bits-in-an-array/)

给定数组 **arr[]** 。任务是从**arr【】**中找到具有最大设置位数的元素。
**例:**

> **输入:** arr[] = {10，100，1000，10000}
> **输出:** 1000
> 二进制(10) = 1010 (2 组位)
> 二进制(100) = 1100100 (3 组位)
> 二进制(1000) = 1111101000 (6 组位)
> 二进制(10000)= 1000

**逼近:**遍历数组，找到当前元素中设置位的个数，找到设置位个数最多的元素。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std; ;

// Function to return the element from the array
// which has the maximum set bits
int maxBitElement(int arr[], int n)
{

    // To store the required element and
    // the maximum set bits so far
    int num = 0, max = -1;

    for (int i = 0; i < n; i++) {

        // Count of set bits in
        // the current element
        int cnt = __builtin_popcount(arr[i]);

        // Update the max
        if (cnt > max) {
            max = cnt;
            num = arr[i];
        }
    }
    return num;
}

// Driver code
int main()
{
    int arr[] = { 3, 2, 4, 7, 1, 10, 5, 8, 9, 6 };
    int n = sizeof(arr)/ sizeof(arr[0]) ;

    cout << maxBitElement(arr, n) << endl;

return 0 ;

// This code is contributed by AnkitRai01
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the element from the array
    // which has the maximum set bits
    static int maxBitElement(int arr[], int n)
    {

        // To store the required element and
        // the maximum set bits so far
        int num = 0, max = -1;

        for (int i = 0; i < n; i++) {

            // Count of set bits in
            // the current element
            int cnt = Integer.bitCount(arr[i]);

            // Update the max
            if (cnt > max) {
                max = cnt;
                num = arr[i];
            }
        }
        return num;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 3, 2, 4, 7, 1, 10, 5, 8, 9, 6 };
        int n = arr.length;
        System.out.print(maxBitElement(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the element from the array
# which has the maximum set bits
def maxBitElement(arr, n):

    # To store the required element and
    # the maximum set bits so far
    num = 0
    max = -1

    for i in range(n):

        # Count of set bits in
        # the current element
        cnt = bin(arr[i]).count('1')

        # Update the max
        if (cnt > max):
            max = cnt
            num = arr[i]
    return num

# Driver code
if __name__ == '__main__':
    arr = [3, 2, 4, 7, 1,
          10, 5, 8, 9, 6]
    n = len(arr)

    print(maxBitElement(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the element from the array
    // which has the maximum set bits
    static int maxBitElement(int []arr, int n)
    {

        // To store the required element and
        // the maximum set bits so far
        int num = 0, max = -1;

        for (int i = 0; i < n; i++)
        {

            // Count of set bits in
            // the current element
            int cnt = BitCount(arr[i]);

            // Update the max
            if (cnt > max)
            {
                max = cnt;
                num = arr[i];
            }
        }
        return num;
    }
    static int BitCount(int n)
    {
        int count = 0;
        while (n != 0)
        {
            count++;
            n &= (n - 1);
        }
        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 3, 2, 4, 7, 1, 10, 5, 8, 9, 6 };
        int n = arr.Length;
        Console.Write(maxBitElement(arr, n));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the element from
// the array which has the maximum set bits
function maxBitElement($arr, $n)
{

    // To store the required element and
    // the maximum set bits so far
    $num = 0; $max = -1;

    for ($i = 0; $i < $n; $i++)
    {

        // Count of set bits in
        // the current element
        $cnt = BitCount($arr[$i]);

        // Update the max
        if ($cnt > $max)
        {
            $max = $cnt;
            $num = $arr[$i];
        }
    }
    return $num;
}

function BitCount($n)
{
    $count = 0;
    while ($n != 0)
    {
        $count++;
        $n &= ($n - 1);
    }
    return $count;
}

// Driver code
$arr = array(3, 2, 4, 7, 1, 10, 5, 8, 9, 6 );
$n = count($arr);
echo(maxBitElement($arr, $n));

// This code contributed by PrinciRaj1992
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the element from the array
// which has the maximum set bits
function maxBitElement(arr, n)
{

    // To store the required element and
    // the maximum set bits so far
    let num = 0, max = -1;

    for (let i = 0; i < n; i++) {

        // Count of set bits in
        // the current element
        let cnt = BitCount(arr[i]);

        // Update the max
        if (cnt > max) {
            max = cnt;
            num = arr[i];
        }
    }
    return num;
}

function BitCount(n)
{
    let count = 0;
    while (n != 0)
    {
        count++;
        n &= (n - 1);
    }
    return count;
}

// Driver code
    let arr = [ 3, 2, 4, 7, 1, 10, 5, 8, 9, 6 ];
    let n = arr.length;

    document.write(maxBitElement(arr, n));

</script>
```

**Output:** 

```
7
```

时间复杂度:0(n)

辅助空间:0(1)