# 最长子阵列，相邻元素至少有一个公共数字|集合 1

> 原文:[https://www . geeksforgeeks . org/最长子数组这样相邻元素至少有一个公共数字/](https://www.geeksforgeeks.org/longest-subarray-such-that-adjacent-elements-have-at-least-one-common-digit/)

给定一个 N 个整数的数组，编写一个打印最长子阵列长度的程序，使得子阵列的相邻元素至少有一个数字是相同的。

**示例:**

```
Input : 12 23 45 43 36 97 
Output : 3 
Explanation: The subarray is 45 43 36 which has 
4 common in 45, 43 and 3 common in 43, 36\. 

Input : 11 22 33 44 54 56 63
Output : 4
Explanation: Subarray is 44, 54, 56, 63 
```

一个正常的方法是检查所有可能的子阵列。但是时间复杂度会是 O(n <sup>2</sup> )。
一种**有效的方法**是创建一个散列[n][10]数组，该数组标记第 I 个索引号中出现的数字。我们对每个元素进行迭代，检查相邻元素之间是否有共同的数字。如果它们有一个共同的数字，我们就记录长度。如果相邻的元素没有共同的数字，我们将计数初始化为零，并为子阵列再次开始计数。打印迭代时获得的最大计数。我们使用一个散列数组来最小化时间复杂度，因为这个数字可能在 10^18 范围内，在最坏的情况下需要 18 次迭代。
以下是上述方法的说明:

## C++

```
// CPP program to print the length of the
// longest subarray such that adjacent elements
// of the subarray have at least one digit in
// common.
#include <bits/stdc++.h>
using namespace std;

// function to print the longest subarray
// such that adjacent elements have at least
// one digit in common
int longestSubarray(int a[], int n)
{
    // remembers the occurrence of digits in
    // i-th index number
    int hash[n][10];
    memset(hash, 0, sizeof(hash));

    // marks the presence of digit in i-th
    // index number
    for (int i = 0; i < n; i++) {
        int num = a[i];
        while (num) {
            // marks the digit
            hash[i][num % 10] = 1;
            num /= 10;
        }
    }

    // counts the longest Subarray
    int longest = INT_MIN;
    // counts the subarray
    int count = 0;

    // check for all adjacent elements
    for (int i = 0; i < n - 1; i++) {
        int j;
        for (j = 0; j < 10; j++) {

            // if adjacent elements have digit j
            // in them count and break as we have
            // got at-least one digit
            if (hash[i][j] and hash[i + 1][j]) {
                count++;
                break;
            }
        }
        // if no digits are common
        if (j == 10) {
            longest = max(longest, count + 1);
            count = 0;
        }
    }

    longest = max(longest, count + 1);

    // returns the length of the longest subarray
    return longest;
}
// Driver Code
int main()
{
    int a[] = { 11, 22, 33, 44, 54, 56, 63 };

    int n = sizeof(a) / sizeof(a[0]);
    // function call
    cout << longestSubarray(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the length of the
// longest subarray such that adjacent elements
// of the subarray have at least one digit in
// common.

class GFG {

// function to print the longest subarray
// such that adjacent elements have at least
// one digit in common
    static int longestSubarray(int a[], int n) {
        // remembers the occurrence of digits in
        // i-th index number
        int hash[][] = new int[n][10];

        // marks the presence of digit in i-th
        // index number
        for (int i = 0; i < n; i++) {
            int num = a[i];
            while (num != 0) {
                // marks the digit
                hash[i][num % 10] = 1;
                num /= 10;
            }
        }

        // counts the longest Subarray
        int longest = Integer.MIN_VALUE;
        // counts the subarray
        int count = 0;

        // check for all adjacent elements
        for (int i = 0; i < n - 1; i++) {
            int j;
            for (j = 0; j < 10; j++) {

                // if adjacent elements have digit j
                // in them count and break as we have
                // got at-least one digit
                if (hash[i][j] == 1 & hash[i + 1][j] == 1) {
                    count++;
                    break;
                }
            }
            // if no digits are common
            if (j == 10) {
                longest = Math.max(longest, count + 1);
                count = 0;
            }
        }

        longest = Math.max(longest, count + 1);

        // returns the length of the longest subarray
        return longest;
    }
// Driver Code

    public static void main(String[] args) {
        int a[] = {11, 22, 33, 44, 54, 56, 63};

        int n = a.length;
        // function call
        System.out.println(longestSubarray(a, n));

    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to print the length of the
# longest subarray such that adjacent elements
# of the subarray have at least one digit in
# common.
import sys

# function to print the longest subarray
# such that adjacent elements have at least
# one digit in common
def longestSubarray(a, n):

    # remembers the occurrence of digits
    # in i-th index number
    hash = [[0 for i in range(10)]
               for j in range(n)]

    # marks the presence of digit in
    # i-th index number
    for i in range(n):
        num = a[i]
        while (num):

            # marks the digit
            hash[i][num % 10] = 1
            num = int(num / 10)

    # counts the longest Subarray
    longest = -sys.maxsize-1

    # counts the subarray
    count = 0

    # check for all adjacent elements
    for i in range(n - 1):
        for j in range(10):

            # if adjacent elements have digit j
            # in them count and break as we have
            # got at-least one digit
            if (hash[i][j] and hash[i + 1][j]):
                count += 1
                break

        # if no digits are common
        if (j == 10):
            longest = max(longest, count + 1)
            count = 0

    longest = max(longest, count + 1)

    # returns the length of the longest
    # subarray
    return longest

# Driver Code
if __name__ == '__main__':
    a = [11, 22, 33, 44, 54, 56, 63]

    n = len(a)

    # function call
    print(longestSubarray(a, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```

// C# program to print the length of the
// longest subarray such that adjacent elements
// of the subarray have at least one digit in
// common.
using System;
public class GFG {

// function to print the longest subarray
// such that adjacent elements have at least
// one digit in common
    static int longestSubarray(int []a, int n) {
        // remembers the occurrence of digits in
        // i-th index number
        int [,]hash = new int[n,10];

        // marks the presence of digit in i-th
        // index number
        for (int i = 0; i < n; i++) {
            int num = a[i];
            while (num != 0) {
                // marks the digit
                hash[i,num % 10] = 1;
                num /= 10;
            }
        }

        // counts the longest Subarray
        int longest = int.MinValue;
        // counts the subarray
        int count = 0;

        // check for all adjacent elements
        for (int i = 0; i < n - 1; i++) {
            int j;
            for (j = 0; j < 10; j++) {

                // if adjacent elements have digit j
                // in them count and break as we have
                // got at-least one digit
                if (hash[i,j] == 1 & hash[i + 1,j] == 1) {
                    count++;
                    break;
                }
            }
            // if no digits are common
            if (j == 10) {
                longest = Math.Max(longest, count + 1);
                count = 0;
            }
        }

        longest = Math.Max(longest, count + 1);

        // returns the length of the longest subarray
        return longest;
    }
// Driver Code

    public static void Main() {
        int []a = {11, 22, 33, 44, 54, 56, 63};

        int n = a.Length;
        // function call
        Console.Write(longestSubarray(a, n));

    }
}
// This code is contributed by Rajput-Ji//
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the length of the
// longest subarray such that adjacent
// elements of the subarray have at least
// one digit in common.

// function to print the longest subarray
// such that adjacent elements have at
// least one digit in common
function longestSubarray(&$a, $n)
{
    // remembers the occurrence of
    // digits in i-th index number
    $hash = array_fill(0, $n,
            array_fill(0, 10, NULL));

    // marks the presence of digit in
    // i-th index number
    for ($i = 0; $i < $n; $i++)
    {
        $num = $a[$i];
        while ($num)
        {
            // marks the digit
            $hash[$i][$num % 10] = 1;
            $num = intval($num / 10);
        }
    }

    // counts the longest Subarray
    $longest = PHP_INT_MIN;

    // counts the subarray
    $count = 0;

    // check for all adjacent elements
    for ($i = 0; $i < $n - 1; $i++)
    {
        for ($j = 0; $j < 10; $j++)
        {

            // if adjacent elements have digit j
            // in them count and break as we have
            // got at-least one digit
            if ($hash[$i][$j] and $hash[$i + 1][$j])
            {
                $count++;
                break;
            }
        }

        // if no digits are common
        if ($j == 10)
        {
            $longest = max($longest, $count + 1);
            $count = 0;
        }
    }

    $longest = max($longest, $count + 1);

    // returns the length of the
    // longest subarray
    return $longest;
}

// Driver Code
$a = array(11, 22, 33, 44, 54, 56, 63 );

$n = sizeof($a);

// function call
echo longestSubarray($a, $n);

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to print the length of the
// longest subarray such that adjacent elements
// of the subarray have at least one digit in
// common.

    // function to print the longest subarray
// such that adjacent elements have at least
// one digit in common
    function longestSubarray(a,n)
    {
        // remembers the occurrence of digits in
        // i-th index number
        let hash = new Array(n);
        for(let i=0;i<n;i++)
        {
            hash[i]=new Array(10);
            for(let j=0;j<10;j++)
            {
                hash[i][j]=0;
            }
        }

        // marks the presence of digit in i-th
        // index number
        for (let i = 0; i < n; i++) {
            let num = a[i];
            while (num != 0) {
                // marks the digit
                hash[i][num % 10] = 1;
                num = Math.floor(num/ 10);
            }
        }

        // counts the longest Subarray
        let longest = Number.MIN_VALUE;
        // counts the subarray
        let count = 0;

        // check for all adjacent elements
        for (let i = 0; i < n - 1; i++) {
            let j;
            for (j = 0; j < 10; j++) {

                // if adjacent elements have digit j
                // in them count and break as we have
                // got at-least one digit
                if (hash[i][j] == 1 & hash[i + 1][j] == 1) {
                    count++;
                    break;
                }
            }
            // if no digits are common
            if (j == 10) {
                longest = Math.max(longest, count + 1);
                count = 0;
            }
        }

        longest = Math.max(longest, count + 1);

        // returns the length of the longest subarray
        return longest;
    }

    // Driver Code
    let a=[11, 22, 33, 44, 54, 56, 63];
    let n = a.length;
    // function call
    document.write(longestSubarray(a, n));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
4
```

**时间复杂度:** O(n*10)
[最长子阵列，相邻元素至少有一个公共数字| Set–2](https://www.geeksforgeeks.org/longest-subarray-such-that-adjacent-elements-have-at-least-one-common-digit-set-2/)