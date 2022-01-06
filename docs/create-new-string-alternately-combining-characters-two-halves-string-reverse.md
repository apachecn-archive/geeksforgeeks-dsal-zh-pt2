# 通过反向交替组合字符串两半的字符来创建新字符串

> 原文:[https://www . geesforgeks . org/create-new-string-交替组合-字符-两半-string-reverse/](https://www.geeksforgeeks.org/create-new-string-alternately-combining-characters-two-halves-string-reverse/)

给定一个字符串 s，创建一个新的字符串，使其包含以相反顺序交替组合的字符串 s 的两部分的字符。
**例:**

```
Input : s = carbohydrates
Output : hsoebtraarcdy

Input : s = sunshine
Output : sennuish
```

**说明:**
**例 1:** 绳子的两半**碳水化合物**是**碳水化合物**和**水化物**。由于需要交替反向添加，先从前半部分的 **h** 开始，然后从后半部分的 **s** 开始，接着从前半部分的 **o** 开始，从后半部分的 **e** 开始，以此类推。弦 **p** 出来就是 **hsoebtraarcdy** 。如果其中一个字符串完全结束，那么只需以相反的顺序添加另一个字符串的剩余字符。
**例 2:** 弦的两半分别是**太阳**和**海星**。弦 **sennuish** 是想要的弦 **p** 。

## C++

```
// C++ program for creating a string
// by alternately combining the
// characters of two halves
// in reverse
#include <bits/stdc++.h>
using namespace std;

// Function performing calculations
void solve(string s)
{
    int l = s.length();
    int x = l / 2;
    int y = l;

    // Calculating the two halves
    // of string s as first and
    // second. The final string p
    string p = "";
    while (x > 0 && y > l / 2) {

        // It joins the characters to
        // final string in reverse order
        p += s[x - 1];
        x--;

        // It joins the characters to
        // final string in reverse order
        p += s[y - 1];
        y--;
    }

    if (y > l / 2) {
        p += s[y - 1];
        y--;
    }

    cout << p;
}

// Driver code
int main()
{
    string s = "sunshine";

    // Calling function
    solve(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for creating a string
// by alternately combining the
// characters of two halves
// in reverse
import java.io.*;

class GFG {

    // Function performing calculations
    public static void solve(String s)
    {
        int l = s.length();
        int x = l / 2;
        int y = l;

        // Calculating the two halves of
        // string s as first and second
        // The final string p
        String p = "";
        while (x > 0 && y > l / 2) {

            // It joins the characters to
            // final string in reverse order
            char ch = s.charAt(x - 1);
            p += ch;
            x--;

            // It joins the characters to
            // final string in reverse order
            ch = s.charAt(y - 1);
            p += ch;
            y--;
        }

        if (y > l / 2) {
            char ch = s.charAt(x - 1);
            p += ch;
            y--;
        }
        System.out.println(p);
    }

    // Driver method
    public static void main(String args[])
    {
        String s = "sunshine";

        // Calling function
        solve(s);
    }
}
```

## 蟒蛇 3

```
# Python 3 program for creating a string
# by alternately combining the
# characters of two halves
# in reverse

# Function performing calculations
def solve(s) :
    l = len(s)
    x = l // 2
    y = l

    # Calculating the two halves
    # of string s as first and
    # second. The final string p
    p = ""
    while (x > 0 and y > l / 2) :

        # It joins the characters to
        # final string in reverse order
        p =  p + s[x - 1]
        x = x - 1

        # It joins the characters to
        # final string in reverse order
        p = p + s[y - 1]
        y = y - 1

    if (y > l // 2) :
        p = p + s[y - 1]
        y = y - 1

    print (p)

# Driver code
s = "sunshine"

# Calling function
solve(s)

# This code is contributed by Nikita Tiwari
```

## C#

```
// C# program for creating a string
// by alternately combining the
// characters of two halves
// in reverse
using System;

class GFG {

    // Function performing calculations
    public static void solve(string s)
    {
        int l = s.Length;
        int x = l / 2;
        int y = l;

        // Calculating the two halves of
        // string s as first and second
        // The final string p
        string p = "";
        while (x > 0 && y > l / 2) {

            // It joins the characters to
            // final string in reverse order
            char ch = s[x - 1];
            p += ch;
            x--;

            // It joins the characters to
            // final string in reverse order
            ch = s[y - 1];
            p += ch;
            y--;
        }

        if (y > l / 2)
        {
            char ch = s[x - 1];
            p += ch;
            y--;
        }
        Console.WriteLine(p);
    }

    // Driver method
    public static void Main()
    {
        string s = "sunshine";

        // Calling function
        solve(s);
    }
}
// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Python 3 program for creating a string
// by alternately combining the
// characters of two halves in reverse

// Function performing calculations
function solve($s)
{
    $l = strlen($s);
    $x = $l / 2;
    $y = $l;

    // Calculating the two halves
    // of string s as first and
    // second. The final string p
    $p = "";
    while ($x > 0 && $y > $l / 2)
    {

        // It joins the characters to
        // final string in reverse order
        $p = $p.$s[$x - 1];
        $x--;

        // It joins the characters to
        // final string in reverse order
        $p = $p.$s[$y - 1];
        $y--;
    }

    if ($y > $l / 2)
    {
        $p = $p.$s[$y - 1];
        $y--;
    }

    echo $p;
}

// Driver code
$s = "sunshine";

// Calling function
solve($s);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript program for creating a string
// by alternately combining the
// characters of two halves
// in reverse

    // Function performing calculations
    function solve( s) {
        var l = s.length;
        var x = l / 2;
        var y = l;

        // Calculating the two halves of
        // string s as first and second
        // The final string p
        var p = "";
        while (x > 0 && y > l / 2) {

            // It joins the characters to
            // final string in reverse order
            var ch = s.charAt(x - 1);
            p += ch;
            x--;

            // It joins the characters to
            // final string in reverse order
            ch = s.charAt(y - 1);
            p += ch;
            y--;
        }

        if (y > l / 2) {
            var ch = s.charAt(x - 1);
            p += ch;
            y--;
        }
        document.write(p);
    }

    // Driver method

        var s = "sunshine";

        // Calling function
        solve(s);

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
sennuish
```