# 数量小于 Y 的最小集数

> 原文:[https://www . geesforgeks . org/最小集数小于 y/](https://www.geeksforgeeks.org/minimum-number-of-sets-with-numbers-less-than-y/)

给定一串连续的数字和一个数字 Y，任务是找到最小集合的数目，使得每个集合遵循下面的规则:

1.  集合应该包含连续的数字
2.  任何数字都不能多次使用。
3.  集合中的数字不应超过 y。

**示例:**

```
Input: s = "1234", Y = 30  
Output: 3
Three sets of {12, 3, 4}  

Input: s = "1234", Y = 4 
Output: 4
Four sets of {1}, {2}, {3}, {4} 
```

**方法:**使用贪婪方法可以解决以下问题，其步骤如下:

*   迭代字符串，并使用 num*10 + (s[i]-'0 ')将数字连接到变量(比如 num)
*   如果数字不大于 Y，则标记 f = 1。
*   如果数字超过 Y，那么如果 f = 1，则增加计数，并将 f 重新初始化为 0，并将 num 初始化为 s[i]-'0 '或 num 为 0。
*   在字符串完全迭代后，如果 f 为 1，则增加计数。

下面是上述方法的实现:

## C++

```
// C++ program to find the minimum number
// sets with consecutive numbers and less than Y
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of shets
int minimumSets(string s, int y)
{

    // Variable to count
    // the number of sets
    int cnt = 0;
    int num = 0;

    int l = s.length();
    int f = 0;

    // Iterate in the string
    for (int i = 0; i < l; i++) {

        // Add the number to string
        num = num * 10 + (s[i] - '0');

        // Mark that we got a number
        if (num <= y)
            f = 1;
        else // Every time it exceeds
        {

            // Check if previous was
            // anytime  less than Y
            if (f)
                cnt += 1;

            // Current number
            num = s[i] - '0';
            f = 0;

            // Check for current number
            if (num <= y)
                f = 1;
            else
                num = 0;
        }
    }

    // Check for last added number
    if (f)
        cnt += 1;

    return cnt;
}

// Driver Code
int main()
{
    string s = "1234";
    int y = 30;
    cout << minimumSets(s, y);

 return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum number
// sets with consecutive numbers and less than Y
import java.util.*;

class solution
{

// Function to find the minimum number of shets
static int minimumSets(String s, int y)
{

    // Variable to count
    // the number of sets
    int cnt = 0;
    int num = 0;

    int l = s.length();
    boolean f = false;

    // Iterate in the string
    for (int i = 0; i < l; i++) {

        // Add the number to string
        num = num * 10 + (s.charAt(i) - '0');

        // Mark that we got a number
        if (num <= y)
            f = true;
        else // Every time it exceeds
        {

            // Check if previous was
            // anytime less than Y
            if (f)
                cnt += 1;

            // Current number
            num = s.charAt(i) - '0';
            f = false;

            // Check for current number
            if (num <= y)
                f = true;
            else
                num = 0;
        }
    }

    // Check for last added number
    if (f == true)
        cnt += 1;

    return cnt;
}

// Driver Code
public static void main(String args[])
{
    String s = "1234";
    int y = 30;
    System.out.println(minimumSets(s, y));
}
}
// This code is contributed by
// Shashank_Sharma
```

## 蟒蛇 3

```
# Python3 program to find the minimum number
# sets with consecutive numbers and less than Y
import math as mt

# Function to find the minimum number of shets
def minimumSets(s, y):

    # Variable to count the number of sets
    cnt = 0
    num = 0

    l = len(s)
    f = 0

    # Iterate in the string
    for i in range(l):

        # Add the number to string
        num = num * 10 + (ord(s[i]) - ord('0'))

        # Mark that we got a number
        if (num <= y):
            f = 1
        else: # Every time it exceeds

            # Check if previous was anytime
            # less than Y
            if (f):
                cnt += 1

            # Current number
            num = ord(s[i]) - ord('0')
            f = 0

            # Check for current number
            if (num <= y):
                f = 1
            else:
                num = 0

    # Check for last added number
    if (f):
        cnt += 1

    return cnt

# Driver Code
s = "1234"
y = 30
print(minimumSets(s, y))

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# program to find the minimum number
// sets with consecutive numbers and less than Y

using System;

class solution
{

// Function to find the minimum number of shets
static int minimumSets(string s, int y)
{

    // Variable to count
    // the number of sets
    int cnt = 0;
    int num = 0;

    int l = s.Length ;
    bool f = false;

    // Iterate in the string
    for (int i = 0; i < l; i++) {

        // Add the number to string
        num = num * 10 + (s[i] - '0');

        // Mark that we got a number
        if (num <= y)
            f = true;
        else // Every time it exceeds
        {

            // Check if previous was
            // anytime less than Y
            if (f)
                cnt += 1;

            // Current number
            num = s[i] - '0';
            f = false;

            // Check for current number
            if (num <= y)
                f = true;
            else
                num = 0;
        }
    }

    // Check for last added number
    if (f == true)
        cnt += 1;

    return cnt;
}

// Driver Code
public static void Main()
{
    string s = "1234";
    int y = 30;

    Console.WriteLine(minimumSets(s, y));
}
// This code is contributed by Ryuga

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the minimum number
// sets with consecutive numbers and less than Y

// Function to find the minimum number of shets
function minimumSets($s, $y)
{

    // Variable to count
    // the number of sets
    $cnt = 0;
    $num = 0;

    $l = strlen($s);
    $f = 0;

    // Iterate in the string
    for ($i = 0; $i < $l; $i++)
    {

        // Add the number to string
        $num = $num * 10 + ($s[$i] - '0');

        // Mark that we got a number
        if ($num <= $y)
            $f = 1;
        else // Every time it exceeds
        {

            // Check if previous was
            // anytime less than Y
            if ($f)
                $cnt += 1;

            // Current number
            $num = $s[$i] - '0';
            $f = 0;

            // Check for current number
            if ($num <= $y)
                $f = 1;
            else
                $num = 0;
        }
    }

    // Check for last added number
    if ($f)
        $cnt += 1;

    return $cnt;
}

// Driver Code
$s = "1234";
$y = 30;
echo(minimumSets($s, $y));

//This code is contributed by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to find the minimum number
// sets with consecutive numbers and less than Y

// Function to find the minimum number of shets
function minimumSets(s, y)
{

    // Variable to count
    // the number of sets
    let cnt = 0;
    let num = 0;

    let l = s.length;
    let f = false;

    // Iterate in the string
    for (let i = 0; i < l; i++) {

        // Add the number to string
        num = num * 10 + (s[i] - '0');

        // Mark that we got a number
        if (num <= y)
            f = true;
        else // Every time it exceeds
        {

            // Check if previous was
            // anytime less than Y
            if (f)
                cnt += 1;

            // Current number
            num = s[i] - '0';
            f = false;

            // Check for current number
            if (num <= y)
                f = true;
            else
                num = 0;
        }
    }

    // Check for last added number
    if (f == true)
        cnt += 1;

    return cnt;
}

// Driver code

    let s = "1234";
    let y = 30;
     document.write(minimumSets(s, y));

</script>
```

**Output:** 

```
3
```