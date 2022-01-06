# 交换和删除字符后平衡字符串的最大长度

> 原文:[https://www . geesforgeks . org/字符交换和删除后最大平衡字符串长度/](https://www.geeksforgeeks.org/maximum-length-of-balanced-string-after-swapping-and-removal-of-characters/)

给定一个字符串**字符串**，仅由字符 **'('** ，**)'**， **'['** ， **']'** ， **'{'** ， **'}'** 组成。任务是在移除任何字符并交换任何两个相邻字符后，找到平衡字符串的最大长度。
**举例:**

> **输入:**str =)[]]("
> **输出:** 6
> 该字符串可转换为()[]()
> **输入:**str = " { { { { { } "
> **输出:** 2

**方法:**想法是从字符串中移除额外的不匹配括号，因为我们无法为其生成一个平衡的对，并交换剩余的字符来平衡字符串。因此，答案是所有平衡括号对的相等总和。请注意，我们可以通过相邻的交换将字符移动到任何其他位置。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the length of
// the longest balanced sub-string
int maxBalancedStr(string s)
{

    // To store the count of parentheses
    int open1 = 0, close1 = 0;
    int open2 = 0, close2 = 0;
    int open3 = 0, close3 = 0;

    // Traversing the string
    for (int i = 0; i < s.length(); i++) {

        // Check type of parentheses and
        // incrementing count for it
        switch (s[i]) {
        case '(':
            open1++;
            break;
        case ')':
            close1++;
            break;
        case '{':
            open2++;
            break;
        case '}':
            close2++;
            break;
        case '[':
            open3++;
            break;
        case ']':
            close3++;
            break;
        }
    }

    // Sum all pair of balanced parentheses
    int maxLen = 2 * min(open1, close1)
                 + 2 * min(open2, close2)
                 + 2 * min(open3, close3);

    return maxLen;
}

// Driven code
int main()
{
    string s = "))[]]((";
    cout << maxBalancedStr(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the length of
// the longest balanced sub-string
static int maxBalancedStr(String s)
{

    // To store the count of parentheses
    int open1 = 0, close1 = 0;
    int open2 = 0, close2 = 0;
    int open3 = 0, close3 = 0;

    // Traversing the string
    for (int i = 0; i < s.length(); i++)
    {

        // Check type of parentheses and
        // incrementing count for it
        switch (s.charAt(i))
        {
        case '(':
            open1++;
            break;
        case ')':
            close1++;
            break;
        case '{':
            open2++;
            break;
        case '}':
            close2++;
            break;
        case '[':
            open3++;
            break;
        case ']':
            close3++;
            break;
        }
    }

    // Sum all pair of balanced parentheses
    int maxLen = 2 * Math.min(open1, close1)
                + 2 * Math.min(open2, close2)
                + 2 * Math.min(open3, close3);

    return maxLen;
}

// Driven code
public static void main(String[] args)
{
    String s = "))[]]((";
    System.out.println(maxBalancedStr(s));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the length of
# the longest balanced sub-string
def maxBalancedStr(s):

    # To store the count of parentheses
    open1 = 0
    close1 = 0
    open2 = 0
    close2 = 0
    open3 = 0
    close3 = 0

    # Traversing the string
    for i in range(len(s)):

        # Check type of parentheses and
        # incrementing count for it
        if(s[i] == '('):
            open1 += 1
            continue
        if s[i] == ')':
            close1 += 1
            continue
        if s[i] == '{':
            open2 += 1
            continue
        if s[i] == '}':
            close2 += 1
            continue
        if s[i] == '[':
            open3 += 1
            continue
        if s[i] == ']':
            close3 += 1
            continue

    # Sum all pair of balanced parentheses
    maxLen = (2 * min(open1, close1) +
              2 * min(open2, close2) +
              2 * min(open3, close3))

    return maxLen

# Driven code
if __name__ == '__main__':
    s = "))[]](("
    print(maxBalancedStr(s))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the length of
// the longest balanced sub-string
static int maxBalancedStr(string s)
{

    // To store the count of parentheses
    int open1 = 0, close1 = 0;
    int open2 = 0, close2 = 0;
    int open3 = 0, close3 = 0;

    // Traversing the string
    for (int i = 0; i < s.Length; i++)
    {

        // Check type of parentheses and
        // incrementing count for it
        switch (s[i])
        {
        case '(':
            open1++;
            break;
        case ')':
            close1++;
            break;
        case '{':
            open2++;
            break;
        case '}':
            close2++;
            break;
        case '[':
            open3++;
            break;
        case ']':
            close3++;
            break;
        }
    }

    // Sum all pair of balanced parentheses
    int maxLen = 2 * Math.Min(open1, close1)
                + 2 * Math.Min(open2, close2)
                + 2 * Math.Min(open3, close3);

    return maxLen;
}

// Driver code
public static void Main()
{
    string s = "))[]]((";
    Console.WriteLine(maxBalancedStr(s));
}
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
// Function to return the length of
// the longest balanced sub-string
 function maxBalancedStr($s)
{

    // To store the count of parentheses
    $open1 = 0; $close1 = 0;
    $open2 = 0; $close2 = 0;
    $open3 = 0; $close3 = 0;

    // Traversing the string
    for ($i = 0; $i < strlen($s); $i++)
    {

        // Check type of parentheses and
        // incrementing count for it
        switch ($s[$i])
        {
        case '(':
            $open1++;
            break;
        case ')':
            $close1++;
            break;
        case '{':
            $open2++;
            break;
        case '}':
            $close2++;
            break;
        case '[':
            $open3++;
            break;
        case ']':
            $close3++;
            break;
        }
    }

    // Sum all pair of balanced parentheses
    $maxLen = 2 * min($open1, $close1)
                + 2 * min($open2, $close2)
                + 2 * min($open3, $close3);

    return $maxLen;
}

// Driven code
{
    $s = "))[]]((";
    echo(maxBalancedStr($s));
}

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach   
// Function to return the length of
    // the longest balanced sub-string
    function maxBalancedStr( s) {

        // To store the count of parentheses
        var open1 = 0, close1 = 0;
        var open2 = 0, close2 = 0;
        var open3 = 0, close3 = 0;

        // Traversing the string
        for (i = 0; i < s.length; i++) {

            // Check type of parentheses and
            // incrementing count for it
            switch (s.charAt(i)) {
            case '(':
                open1++;
                break;
            case ')':
                close1++;
                break;
            case '{':
                open2++;
                break;
            case '}':
                close2++;
                break;
            case '[':
                open3++;
                break;
            case ']':
                close3++;
                break;
            }
        }

        // Sum all pair of balanced parentheses
        var maxLen = 2 * Math.min(open1, close1)
        + 2 * Math.min(open2, close2)
        + 2 * Math.min(open3, close3);

        return maxLen;
    }

    // Driven code

        var s = "))[]]((";
        document.write(maxBalancedStr(s));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
6
```