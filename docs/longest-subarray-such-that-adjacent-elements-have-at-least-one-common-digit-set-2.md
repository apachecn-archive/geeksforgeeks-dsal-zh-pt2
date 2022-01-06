# 最长子阵列，相邻元素至少有一个公共数字| Set–2

> 原文:[https://www . geeksforgeeks . org/最长子数组这样相邻元素至少有一个公共数字集-2/](https://www.geeksforgeeks.org/longest-subarray-such-that-adjacent-elements-have-at-least-one-common-digit-set-2/)

给定一个 N 个整数的数组，任务是找到最长子阵列的长度，使得子阵列的相邻元素至少有一个相同的数字。
**例:**

```
Input : arr[] = {12, 23, 45, 43, 36, 97}
Output : 3
Explanation: The subarray is 45 43 36 which has 
4 common in 45, 43 and 3 common in 43, 36.

Input : arr[] = {11, 22, 33, 44, 54, 56, 63}
Output : 4
Explanation: Subarray is 44, 54, 56, 63
```

在[之前的帖子](https://www.geeksforgeeks.org/longest-subarray-such-that-adjacent-elements-have-at-least-one-common-digit/)中讨论的解决方案使用了 O(N)个额外空间。这个问题可以用常数空间来解决。恒定大小的散列表用于存储给定数组元素中是否存在数字。要检查相邻元素是否有共同的数字，只需要计算两个相邻元素的数字。因此 hashmap 中所需的行数可以减少到 2。变量 *currRow* 代表当前行，*1–currRow*代表散列表中的前一行。如果相邻元素有共同的数字，则将当前长度增加 1，并与最大长度进行比较。否则将当前长度设置为 1。
以下是上述方法的实施:

## C++

```
// CPP program to print the length of the
// longest subarray such that adjacent elements
// of the subarray have at least one digit in
// common

#include <bits/stdc++.h>
using namespace std;

// Function to print the longest subarray
// such that adjacent elements have at least
// one digit in common
int longestSubarray(int arr[], int n)
{
    int i, d;

    // To mark presence of digit in current
    // element.
    int hash[2][10];
    memset(hash, 0, sizeof(hash));

    // To store current row.
    int currRow;

    // To store maximum length subarray length.
    int maxLen = 1;

    // To store current subarray length.
    int len = 0;

    // To store current array element.
    int tmp;

    // Mark the presence of digits of first element.
    tmp = arr[0];
    while (tmp > 0) {
        hash[0][tmp % 10] = 1;
        tmp /= 10;
    }

    currRow = 1;

    // Find digits of each element and check if adjacent
    // elements have common digit and update len.
    for (i = 1; i < n; i++) {
        tmp = arr[i];

        for (d = 0; d <= 9; d++)
            hash[currRow][d] = 0;

        // Find all digits in element.
        while (tmp > 0) {
            hash[currRow][tmp % 10] = 1;
            tmp /= 10;
        }

        // Find common digit in adjacent element.
        for (d = 0; d <= 9; d++) {
            if (hash[currRow][d] && hash[1 - currRow][d]) {
                len++;
                break;
            }
        }

        // If no common digit is found a new subarray
        // has to start from current element.
        if (d == 10) {
            len = 1;
        }

        maxLen = max(maxLen, len);

        currRow = 1 - currRow;
    }

    return maxLen;
}

// Driver Code
int main()
{
    int arr[] = { 11, 22, 33, 44, 54, 56, 63 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << longestSubarray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the length of the
// longest subarray such that adjacent elements
// of the subarray have at least one digit in
// common
class GFG
{

// Function to print the longest subarray
// such that adjacent elements have at least
// one digit in common
static int longestSubarray(int arr[], int n)
{
    int i, d;

    // To mark presence of digit in current
    // element.
    int hash[][] = new int[2][10];

    for( i = 0; i < 2; i++)
        for(int j = 0; j < 10; j++)
            hash[i][j] = 0;

    // To store current row.
    int currRow;

    // To store maximum length subarray length.
    int maxLen = 1;

    // To store current subarray length.
    int len = 0;

    // To store current array element.
    int tmp;

    // Mark the presence of digits of first element.
    tmp = arr[0];
    while (tmp > 0)
    {
        hash[0][tmp % 10] = 1;
        tmp /= 10;
    }

    currRow = 1;

    // Find digits of each element and check if adjacent
    // elements have common digit and update len.
    for (i = 1; i < n; i++)
    {
        tmp = arr[i];

        for (d = 0; d <= 9; d++)
            hash[currRow][d] = 0;

        // Find all digits in element.
        while (tmp > 0)
        {
            hash[currRow][tmp % 10] = 1;
            tmp /= 10;
        }

        // Find common digit in adjacent element.
        for (d = 0; d <= 9; d++)
        {
            if (hash[currRow][d] != 0 && hash[1 - currRow][d] != 0)
            {
                len++;
                break;
            }
        }

        // If no common digit is found a new subarray
        // has to start from current element.
        if (d == 10)
        {
            len = 1;
        }

        maxLen = Math.max(maxLen, len);

        currRow = 1 - currRow;
    }

    return maxLen;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 11, 22, 33, 44, 54, 56, 63 };
    int n = arr.length;

    System.out.println( longestSubarray(arr, n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to print the length of the
# longest subarray such that adjacent elements
# of the subarray have at least one digit in
# common
import math

# Function to print the longest subarray
# such that adjacent elements have at least
# one digit in common
def longestSubarray(arr, n):

    i = d = 0;

    # To mark presence of digit in current
    # element.
    HASH1 = [[0 for x in range(10)]
                for y in range(2)];

    # To store current row.
    currRow = 0;

    # To store maximum length subarray length.
    maxLen = 1;

    # To store current subarray length.
    len1 = 0;

    # To store current array element.
    tmp = 0;

    # Mark the presence of digits
    # of first element.
    tmp = arr[0];
    while (tmp > 0):
        HASH1[0][tmp % 10] = 1;
        tmp = tmp // 10;

    currRow = 1;

    # Find digits of each element and check
    # if adjacent elements have common digit
    # and update len.
    for i in range(0, n):
        tmp = arr[i];

        for d in range(0, 10):
            HASH1[currRow][d] = 0;

        # Find all digits in element.
        while (tmp > 0):
            HASH1[currRow][tmp % 10] = 1;
            tmp = tmp // 10;

        # Find common digit in adjacent element.
        for d in range(0, 10):
            if (HASH1[currRow][d] and
                HASH1[1 - currRow][d]):
                len1 += 1;
                break;

        # If no common digit is found a new subarray
        # has to start from current element.
        if (d == 10):
            len1 = 1;

        maxLen = max(maxLen, len1);

        currRow = 1 - currRow;

    return maxLen;

# Driver Code
arr = [ 11, 22, 33, 44, 54, 56, 63 ];
n = len(arr);

print(longestSubarray(arr, n));

# This code is contributed by chandan_jnu
```

## C#

```
// C# program to print the length of the
// longest subarray such that adjacent elements
// of the subarray have at least one digit in
// common
using System;

class GFG
{

// Function to print the longest subarray
// such that adjacent elements have at least
// one digit in common
static int longestSubarray(int []arr, int n)
{
    int i, d;

    // To mark presence of digit in current
    // element.
    int[,] hash = new int[2,10];

    for( i = 0; i < 2; i++)
        for(int j = 0; j < 10; j++)
            hash[i,j] = 0;

    // To store current row.
    int currRow;

    // To store maximum length subarray length.
    int maxLen = 1;

    // To store current subarray length.
    int len = 0;

    // To store current array element.
    int tmp;

    // Mark the presence of digits of first element.
    tmp = arr[0];
    while (tmp > 0)
    {
        hash[0,tmp % 10] = 1;
        tmp /= 10;
    }

    currRow = 1;

    // Find digits of each element and check if adjacent
    // elements have common digit and update len.
    for (i = 1; i < n; i++)
    {
        tmp = arr[i];

        for (d = 0; d <= 9; d++)
            hash[currRow,d] = 0;

        // Find all digits in element.
        while (tmp > 0)
        {
            hash[currRow,tmp % 10] = 1;
            tmp /= 10;
        }

        // Find common digit in adjacent element.
        for (d = 0; d <= 9; d++)
        {
            if (hash[currRow,d] != 0 &&
                hash[1 - currRow,d] != 0)
            {
                len++;
                break;
            }
        }

        // If no common digit is found a new subarray
        // has to start from current element.
        if (d == 10)
        {
            len = 1;
        }

        maxLen = Math.Max(maxLen, len);

        currRow = 1 - currRow;
    }

    return maxLen;
}

// Driver Code
static void Main()
{
    int []arr = { 11, 22, 33, 44, 54, 56, 63 };
    int n = arr.Length;

    Console.WriteLine( longestSubarray(arr, n));
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the length of the
// longest subarray such that adjacent elements
// of the subarray have at least one digit in
// common

// Function to print the longest subarray
// such that adjacent elements have at least
// one digit in common
function longestSubarray($arr, $n)
{
    $i = $d = 0;

    // To mark presence of digit in current
    // element.
    $hash = array_fill(0, 2, array_fill(0, 10, 0));

    // To store current row.
    $currRow = 0;

    // To store maximum length subarray length.
    $maxLen = 1;

    // To store current subarray length.
    $len = 0;

    // To store current array element.
    $tmp = 0;

    // Mark the presence of digits
    // of first element.
    $tmp = $arr[0];
    while ($tmp > 0)
    {
        $hash[0][$tmp % 10] = 1;
        $tmp = (int)($tmp / 10);
    }

    $currRow = 1;

    // Find digits of each element and check
    // if adjacent elements have common digit
    // and update len.
    for ($i = 1; $i < $n; $i++)
    {
        $tmp = $arr[$i];

        for ($d = 0; $d <= 9; $d++)
            $hash[$currRow][$d] = 0;

        // Find all digits in element.
        while ($tmp > 0)
        {
            $hash[$currRow][$tmp % 10] = 1;
            $tmp =(int)($tmp/10);
        }

        // Find common digit in adjacent element.
        for ($d = 0; $d <= 9; $d++)
        {
            if ($hash[$currRow][$d] &&
                $hash[1 - $currRow][$d])
            {
                $len++;
                break;
            }
        }

        // If no common digit is found a new subarray
        // has to start from current element.
        if ($d == 10)
        {
            $len = 1;
        }

        $maxLen = max($maxLen, $len);

        $currRow = 1 - $currRow;
    }

    return $maxLen;
}

// Driver Code
$arr = array( 11, 22, 33, 44, 54, 56, 63 );
$n = count($arr);

echo longestSubarray($arr, $n);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript program to print the length of the
// longest subarray such that adjacent elements
// of the subarray have at least one digit in
// common

// Function to print the longest subarray
// such that adjacent elements have at least
// one digit in common
function longestSubarray(arr, n)
{
    var i, d;

    // To mark presence of digit in current
    // element.
    var hash = Array.from(Array(2), () => Array(10));

    // To store current row.
    var currRow;

    // To store maximum length subarray length.
    var maxLen = 1;

    // To store current subarray length.
    var len = 0;

    // To store current array element.
    var tmp;

    // Mark the presence of digits of first element.
    tmp = arr[0];
    while (tmp > 0) {
        hash[0][tmp % 10] = 1;
        tmp = parseInt(tmp/10);
    }

    currRow = 1;

    // Find digits of each element and check if adjacent
    // elements have common digit and update len.
    for (i = 1; i < n; i++) {
        tmp = arr[i];

        for (d = 0; d <= 9; d++)
            hash[currRow][d] = 0;

        // Find all digits in element.
        while (tmp > 0) {
            hash[currRow][tmp % 10] = 1;
            tmp = parseInt(tmp/10);
        }

        // Find common digit in adjacent element.
        for (d = 0; d <= 9; d++) {
            if (hash[currRow][d] && hash[1 - currRow][d]) {
                len++;
                break;
            }
        }

        // If no common digit is found a new subarray
        // has to start from current element.
        if (d == 10) {
            len = 1;
        }

        maxLen = Math.max(maxLen, len);

        currRow = 1 - currRow;
    }

    return maxLen;
}

// Driver Code
var arr = [ 11, 22, 33, 44, 54, 56, 63 ];
var n = arr.length;
document.write( longestSubarray(arr, n));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)