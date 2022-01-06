# 一次移除后等于两个字符串之一的字符串计数

> 原文:[https://www . geeksforgeeks . org/移除一个字符串后变成等于两个字符串之一的字符串计数/](https://www.geeksforgeeks.org/count-of-strings-that-become-equal-to-one-of-the-two-strings-after-one-removal/)

给定两个字符串 **str1** 和 **str2** ，任务是统计所有有效的字符串。下面给出了一个有效字符串的示例:
If**str 1 =“toy”**和**str 2 =“try”**。那么 **S = "tory"** 是一个有效的字符串，因为当从其中删除一个字符时，即 S = "t **o** ry" = "try "它就等于 **str1** 。该属性也必须在 **str2** 中有效，即 S =“to**r**y”=“toy”= str 2。
任务是打印所有可能有效字符串的计数。
**例:**

> **输入:** str = "toy "，str2 = "try"
> **输出:** 2
> 给定的两个单词可以从单词“t **或** y 或单词“t **ro** y”中获得。所以输出是 2。
> **输入:**str 1 =“sweet”，str 2 =“sheep”
> **输出:** 0
> 两个给定的单词不能通过去掉一个字母从同一个单词中获得。

**方式:**计算 **A** 作为 **str1** 和 **str2** 的最长公共前缀， **C** 作为 **str1** 和 **str2** 的最长公共后缀。如果两个字符串相等，则 **26 * (n + 1)** 字符串是可能的。否则，将 **count = 0** 和 **l** 设置为不属于公共前缀的第一个索引， **r** 是不属于公共后缀的最右边的索引。
现在，如果**ST R1[l+1…r]= str 2[l…r-1]**则更新**计数=计数+ 1** 。
如果**str 1[l…r-1]= str 2[l+1…r]**则更新**计数=计数+ 1** 。
打印最后的**计数**。
以下是实施办法:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of the
// required strings
int findAnswer(string str1, string str2, int n)
{
    int l, r;
    int ans = 2;

    // Searching index after longest common
    // prefix ends
    for (int i = 0; i < n; ++i) {
        if (str1[i] != str2[i]) {
            l = i;
            break;
        }
    }

    // Searching index before longest common
    // suffix ends
    for (int i = n - 1; i >= 0; i--) {
        if (str1[i] != str2[i]) {
            r = i;
            break;
        }
    }

    // If str1 = str2
    if (r < l)
        return 26 * (n + 1);

    // If only 1 character is different
    // in both the strings
    else if (l == r)
        return ans;
    else {

        // Checking remaining part of string
        // for equality
        for (int i = l + 1; i <= r; i++) {
            if (str1[i] != str2[i - 1]) {
                ans--;
                break;
            }
        }

        // Searching in right of string h
        // (g to h)
        for (int i = l + 1; i <= r; i++) {
            if (str1[i - 1] != str2[i]) {
                ans--;
                break;
            }
        }

        return ans;
    }
}

// Driver code
int main()
{
    string str1 = "toy", str2 = "try";
    int n = str1.length();
    cout << findAnswer(str1, str2, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count of the
// required strings
static int findAnswer(String str1, String str2, int n)
{
    int l = 0, r = 0;
    int ans = 2;

    // Searching index after longest common
    // prefix ends
    for (int i = 0; i < n; ++i)
    {
        if (str1.charAt(i) != str2.charAt(i))
        {
            l = i;
            break;
        }
    }

    // Searching index before longest common
    // suffix ends
    for (int i = n - 1; i >= 0; i--)
    {
        if (str1.charAt(i) != str2.charAt(i))
        {
            r = i;
            break;
        }
    }

    // If str1 = str2
    if (r < l)
        return 26 * (n + 1);

    // If only 1 character is different
    // in both the strings
    else if (l == r)
        return ans;
    else {

        // Checking remaining part of string
        // for equality
        for (int i = l + 1; i <= r; i++)
        {
            if (str1.charAt(i) != str2.charAt(i - 1))
            {
                ans--;
                break;
            }
        }

        // Searching in right of string h
        // (g to h)
        for (int i = l + 1; i <= r; i++)
        {
            if (str1.charAt(i-1) != str2.charAt(i))
            {
                ans--;
                break;
            }
        }

        return ans;
    }
}

// Driver code
public static void main(String args[])
{
    String str1 = "toy", str2 = "try";
    int n = str1.length();
    System.out.println(findAnswer(str1, str2, n));

}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math as mt

# Function to return the count of
# the required strings
def findAnswer(str1, str2, n):

    l, r = 0, 0
    ans = 2

    # Searching index after longest
    # common prefix ends
    for i in range(n):
        if (str1[i] != str2[i]):
            l = i
            break

    # Searching index before longest
    # common suffix ends
    for i in range(n - 1, -1, -1):
        if (str1[i] != str2[i]):
            r = i
            break

    if (r < l):
        return 26 * (n + 1)

    # If only 1 character is different
    # in both the strings
    elif (l == r):
        return ans
    else:

        # Checking remaining part of
        # string for equality
        for i in range(l + 1, r + 1):
            if (str1[i] != str2[i - 1]):
                ans -= 1
                break

        # Searching in right of string h
        # (g to h)
        for i in range(l + 1, r + 1):
            if (str1[i - 1] != str2[i]):
                ans -= 1
                break

        return ans

# Driver code
str1 = "toy"
str2 = "try"
n = len(str1)
print(findAnswer(str1, str2, n))

# This code is contributed
# by Mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of the
// required strings
static int findAnswer(string str1, string str2, int n)
{
    int l = 0, r = 0;
    int ans = 2;

    // Searching index after longest common
    // prefix ends
    for (int i = 0; i < n; ++i)
    {
        if (str1[i] != str2[i])
        {
            l = i;
            break;
        }
    }

    // Searching index before longest common
    // suffix ends
    for (int i = n - 1; i >= 0; i--)
    {
        if (str1[i] != str2[i])
        {
            r = i;
            break;
        }
    }

    // If str1 = str2
    if (r < l)
        return 26 * (n + 1);

    // If only 1 character is different
    // in both the strings
    else if (l == r)
        return ans;
    else
    {

        // Checking remaining part of string
        // for equality
        for (int i = l + 1; i <= r; i++)
        {
            if (str1[i] != str2[i - 1])
            {
                ans--;
                break;
            }
        }

        // Searching in right of string h
        // (g to h)
        for (int i = l + 1; i <= r; i++)
        {
            if (str1[i-1] != str2[i])
            {
                ans--;
                break;
            }
        }
        return ans;
    }
}

// Driver code
public static void Main()
{
    String str1 = "toy", str2 = "try";
    int n = str1.Length;
    Console.WriteLine(findAnswer(str1, str2, n));
}
}

// This code is contributed by
// shs
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to return the count of 
// the required strings
function findAnswer($str1, $str2, $n)
{
    $ans = 2;

    // Searching index after longest 
    // common prefix ends
    for ($i = 0; $i < $n; ++$i)
    {
        if ($str1[$i] != $str2[$i])
        {
            $l = $i;
            break;
        }
    }

    // Searching index before longest
    // common suffix ends
    for ($i = $n - 1; $i >= 0; $i--)
    {
        if ($str1[$i] != $str2[$i])
        {
            $r = $i;
            break;
        }
    }

    // If str1 = str2
    if ($r < $l)
        return 26 * ($n + 1);

    // If only 1 character is different
    // in both the strings
    else if ($l == $r)
        return $ans;
    else
    {

        // Checking remaining part of string
        // for equality
        for ($i = $l + 1; $i <= $r; $i++)
        {
            if ($str1[$i] != $str2[$i - 1])
            {
                $ans--;
                break;
            }
        }

        // Searching in right of string h
        // (g to h)
        for ($i = $l + 1; $i <= $r; $i++)
        {
            if ($str1[$i - 1] != $str2[$i])
            {
                $ans--;
                break;
            }
        }

        return $ans;
    }
}

// Driver code
$str1 = "toy";
$str2 = "try";
$n = strlen($str1);

echo findAnswer($str1, $str2, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

    // Function to return the count of the
    // required strings
    function findAnswer( str1,  str2 , n)
    {
        var l = 0, r = 0;
        var ans = 2;

        // Searching index after longest common
        // prefix ends
        for (i = 0; i < n; ++i) {
            if (str1.charAt(i) != str2.charAt(i))
            {
                l = i;
                break;
            }
        }

        // Searching index before longest common
        // suffix ends
        for (i = n - 1; i >= 0; i--) {
            if (str1.charAt(i) != str2.charAt(i))
            {
                r = i;
                break;
            }
        }

        // If str1 = str2
        if (r < l)
            return 26 * (n + 1);

        // If only 1 character is different
        // in both the strings
        else if (l == r)
            return ans;
        else {

            // Checking remaining part of string
            // for equality
            for (i = l + 1; i <= r; i++) {
                if (str1.charAt(i) != str2.charAt(i - 1))
                {
                    ans--;
                    break;
                }
            }

            // Searching in right of string h
            // (g to h)
            for (i = l + 1; i <= r; i++) {
                if (str1.charAt(i - 1) != str2.charAt(i))
                {
                    ans--;
                    break;
                }
            }

            return ans;
        }
    }

    // Driver code

        var str1 = "toy", str2 = "try";
        var n = str1.length;
        document.write(findAnswer(str1, str2, n));

// This code contributed by gauravrajput1

</script>
```

**Output**

```
2
```

**时间复杂度:** O(N)

**辅助空间:** O(1)