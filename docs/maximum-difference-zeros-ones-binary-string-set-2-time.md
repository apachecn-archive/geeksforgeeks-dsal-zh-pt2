# 二进制字符串中 0 和 1 的最大差值|集合 2 (O(n)时间)

> 原文:[https://www . geesforgeks . org/最大差值-0-1-二进制-字符串-set-2-time/](https://www.geeksforgeeks.org/maximum-difference-zeros-ones-binary-string-set-2-time/)

给定 0 和 1 的二进制字符串。任务是找出给定二进制字符串的任何子字符串中 0 和 1 的最大差值。也就是说，对于给定二进制字符串中的任何子字符串，最大化(0 的数量–1 的数量)。

**示例:**

```
Input : S = "11000010001"
Output : 6
From index 2 to index 9, there are 7
0s and 1 1s, so number of 0s - number
of 1s is 6.

Input : S = "1111"
Output : -1
```

我们在下面的文章中讨论了动态编程方法:

[二进制字符串中 0 和 1 的最大差值|设置 1](https://www.geeksforgeeks.org/maximum-difference-zeros-ones-binary-string/) 。
在这篇文章中，我们看到了一种在 O(n)个时间和 O(1)个额外空间内有效的方法。如果我们把所有的 0 转换成 1，把所有的 1 转换成-1，现在我们的问题简化为使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)找出最大和子数组。

```
Input : S = "11000010001"
     After converting '0' into 1 and
     '1' into -1 our S Look Like
      S  = -1 -1 1 1 1 1 -1 1 1 1 -1
 Now we have to find out Maximum Sum sub_array 
 that is  : 6 is that case 

Output : 6
```

以下是上述想法的实现。

## C++

```
// CPP Program to find the length of
// substring with maximum difference of
// zeros and ones in binary string.
#include <iostream>
using namespace std;

// Returns the length of substring with
// maximum difference of zeroes and ones
// in binary string
int findLength(string str, int n)
{
    int current_sum = 0;
    int max_sum = 0;

    // traverse a binary string from left
    // to right
    for (int i = 0; i < n; i++) {

        // add current value to the current_sum
        // according to the Character
        // if it's '0' add 1 else -1
        current_sum += (str[i] == '0' ? 1 : -1);

        if (current_sum < 0)
            current_sum = 0;

        // update maximum sum
        max_sum = max(current_sum, max_sum);
    }

    // return -1 if string does not contain
    // any zero that means all ones
    // otherwise max_sum
    return max_sum == 0 ? -1 : max_sum;
}

// Driven Program
int main()
{
    string s = "11000010001";
    int n = 11;
    cout << findLength(s, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the length of
// substring with maximum difference of
// zeroes and ones in binary string.
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {

    // Find the length of substring with maximum
    // difference of zeros and ones in binary
    // string
    public static int findLength(String str, int n)
    {

        int current_sum = 0;
        int max_sum = 0;

        // traverse a binary string from left to right
        for (int i = 0; i < n; i++) {

            // add current value to the current_sum
            // according to the Character
            // if it's '0' add 1 else -1
            current_sum += (str.charAt(i) == '0' ? 1 : -1);

            if (current_sum < 0)
                current_sum = 0;

            // update maximum sum
            max_sum = Math.max(current_sum, max_sum);
        }
        // return -1 if string does not contain any zero
        // that means string contains all ones otherwise max_sum
        return max_sum == 0 ? -1 : max_sum;
    }

    public static void main(String[] args)
    {
        String str = "11000010001";
        int n = str.length();

        System.out.println(findLength(str, n));
    }
}
```

## 蟒蛇 3

```
# Python Program to find the length of
# substring with maximum difference of
# zeros and ones in binary string.

# Returns the length of substring with
# maximum difference of zeroes and ones
# in binary string
def findLength(string, n):
    current_sum = 0
    max_sum = 0

    # traverse a binary string from left
    # to right
    for i in range(n):

        # add current value to the current_sum
        # according to the Character
        # if it's '0' add 1 else -1
        current_sum += (1 if string[i] == '0' else -1)

        if current_sum < 0:
            current_sum = 0

        # update maximum sum
        max_sum = max(current_sum, max_sum)

    # return -1 if string does not contain
    # any zero that means all ones
    # otherwise max_sum
    return max_sum if max_sum else 0

# Driven Program
s = "11000010001"
n = 11
print(findLength(s, n))

# This code is contributed by Ansu Kumari.
```

## C#

```
// C# Program to find the length of
// substring with maximum difference of
// zeroes and ones in binary string.
using System;

class GFG
{

// Find the length of substring with
// maximum difference of zeros and
// ones in binary string
public static int findLength(string str,
                             int n)
{

    int current_sum = 0;
    int max_sum = 0;

    // traverse a binary string
    // from left to right
    for (int i = 0; i < n; i++)
    {

        // add current value to the current_sum
        // according to the Character
        // if it's '0' add 1 else -1
        current_sum += (str[i] == '0' ? 1 : -1);

        if (current_sum < 0)
        {
            current_sum = 0;
        }

        // update maximum sum
        max_sum = Math.Max(current_sum, max_sum);
    }
    // return -1 if string does not contain
    // any zero that means string contains
    // all ones otherwise max_sum
    return max_sum == 0 ? -1 : max_sum;
}

// Driver Code
public static void Main(string[] args)
{
    string str = "11000010001";
    int n = str.Length;

    Console.WriteLine(findLength(str, n));
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the length of
// substring with maximum difference of
// zeros and ones in binary string.

// Returns the length of substring with
// maximum difference of zeroes and ones
// in binary string
function findLength($str, $n)
{
    $current_sum = 0;
    $max_sum = 0;

    // traverse a binary string
    // from left to right
    for ($i = 0; $i < $n; $i++)
    {

        // add current value to the current_sum
        // according to the Character
        // if it's '0' add 1 else -1
        $current_sum += ($str[$i] == '0' ? 1 : -1);

        if ($current_sum < 0)
            $current_sum = 0;

        // update maximum sum
        $max_sum = max($current_sum, $max_sum);
    }

    // return -1 if string does not contain
    // any zero that means all ones
    // otherwise max_sum
    return $max_sum == 0 ? -1 : $max_sum;
}

    // Driver Code
    $s = "11000010001";
    $n = 11;
    echo findLength($s, $n),"\n";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the length of
// substring with maximum difference of
// zeroes and ones in binary string.

// Find the length of substring with
// maximum difference of zeros and
// ones in binary string
function findLength(str, n)
{

    let current_sum = 0;
    let max_sum = 0;

    // traverse a binary string
    // from left to right
    for (let i = 0; i < n; i++)
    {

        // add current value to the current_sum
        // according to the Character
        // if it's '0' add 1 else -1
        current_sum += (str[i] == '0' ? 1 : -1);

        if (current_sum < 0)
        {
            current_sum = 0;
        }

        // update maximum sum
        max_sum = Math.max(current_sum, max_sum);
    }
    // return -1 if string does not contain
    // any zero that means string contains
    // all ones otherwise max_sum
    return max_sum == 0 ? -1 : max_sum;
}

// Driver Code

    let str = "11000010001";
    let n = str.length;

    document.write(findLength(str, n));

      // This code is contributed by chinmoy1997pal.
</script>
```

**输出:**

```
6 
```

**时间复杂度:**O(n)
T3】空间复杂度: O(1)