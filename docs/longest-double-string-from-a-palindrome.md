# 回文中最长的双串

> 原文:[https://www . geeksforgeeks . org/最长双字符串从回文/](https://www.geeksforgeeks.org/longest-double-string-from-a-palindrome/)

给定一个回文字符串，任务是找到双字符串的最大长度以及从给定的回文字符串中可以获得的长度。双字符串是一个子字符串连续两次重复的字符串。
**例:**

```
Input: 
abba
Output:
abab 
4
Explanation: 
abab is double string 
which can be obtained 
by changing the order of letters

Input:
abcba
Output:
abab 4
Explanation: 
abab is double string 
which can be obtained 
by changing the order of letters
and deleting letter c
```

**进场:**双串可以考虑两种情况:

*   **情况 1:** 如果字符串的长度是偶数，那么双字符串的长度永远是字符串的长度。

*   **情况 2:** 如果字符串的长度是奇数，那么双字符串的长度将总是字符串的长度–1。

以下是上述方法的实施

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to return the required position
int lenDoubleString(string s)
{

    int l = s.length();
    string first_half = s.substr(0, l / 2);
    string second_half = "";

    if (l % 2 == 0)
        second_half = s.substr(l / 2);
    else
        second_half = s.substr(l / 2 + 1);

    reverse(second_half.begin(), second_half.end());

    // Print the double string
    cout << first_half << second_half << endl;

    // Print the length of the double string
    if (l % 2 == 0)
        cout << l << endl;
    else
        cout << l - 1 << endl;
}

int main()
{
    string n = "abba";
    lenDoubleString(n);

    n = "abcdedcba";
    lenDoubleString(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the required position
static int lenDoubleString(String s)
{

    int l = s.length();
    String first_half = s.substring(0, l / 2);
    String second_half = "";

    if (l % 2 == 0)
        second_half = s.substring(l / 2);
    else
        second_half = s.substring(l / 2 + 1);

    second_half = reverse(second_half);

    // Print the double String
    System.out.println(first_half + second_half);

    // Print the length of the double String
    if (l % 2 == 0)
        System.out.println(l);
    else
        System.out.println(l - 1);
        return Integer.MIN_VALUE;
}
static String reverse(String input)
{
    char[] temparray = input.toCharArray();
    int left, right = 0;
    right = temparray.length - 1;

    for (left = 0; left < right; left++, right--)
    {
        // Swap values of left and right
        char temp = temparray[left];
        temparray[left] = temparray[right];
        temparray[right] = temp;
    }
    return String.valueOf(temparray);
}

// Driver code
public static void main(String[] args)
{
    String n = "abba";
    lenDoubleString(n);

    n = "abcdedcba";
    lenDoubleString(n);
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach.

# Function to return the required position
def lenDoubleString(s):

    l = len(s)
    first_half = s[0 : l // 2]
    second_half = ""

    if l % 2 == 0:
        second_half = s[l // 2 : ]
    else:
        second_half = s[l // 2 + 1 : ]

    second_half = second_half[::-1]

    # Print the double string
    print(first_half + second_half)

    # Print the length of the double string
    if l % 2 == 0:
        print(l)
    else:
        print(l - 1)

# Driver Code
if __name__ == "__main__":

    n = "abba"
    lenDoubleString(n)

    n = "abcdedcba"
    lenDoubleString(n)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the required position
static int lenDoubleString(String s)
{

    int l = s.Length;
    String first_half = s.Substring(0, l / 2);
    String second_half = "";

    if (l % 2 == 0)
        second_half = s.Substring(l / 2);
    else
        second_half = s.Substring(l / 2 + 1);

    second_half = reverse(second_half);

    // Print the double String
    Console.WriteLine(first_half + second_half);

    // Print the length of the double String
    if (l % 2 == 0)
        Console.WriteLine(l);
    else
        Console.WriteLine(l - 1);
        return int.MinValue;
}

static String reverse(String input)
{
    char[] temparray = input.ToCharArray();
    int left, right = 0;
    right = temparray.Length - 1;

    for (left = 0; left < right; left++, right--)
    {
        // Swap values of left and right
        char temp = temparray[left];
        temparray[left] = temparray[right];
        temparray[right] = temp;
    }
    return String.Join("",temparray);
}

// Driver code
public static void Main(String[] args)
{
    String n = "abba";
    lenDoubleString(n);

    n = "abcdedcba";
    lenDoubleString(n);
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the required position
function lenDoubleString($s)
{
    $l = strlen($s);
    $first_half = substr($s, 0, (int)($l / 2));
    $second_half = "";

    if ($l % 2 == 0)
        $second_half = substr($s, (int)($l / 2));
    else
        $second_half = substr($s, (int)($l / 2 + 1));

    $second_half = strrev($second_half);

    // Print the double string
    echo $first_half . "" .
         $second_half . "\n";

    // Print the length of the double string
    if ($l % 2 == 0)
        echo $l . "\n";
    else
        echo ($l - 1) . "\n";
}

// Driver Code
$n = "abba";
lenDoubleString($n);

$n = "abcdedcba";
lenDoubleString($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the
// above approach

// Function to return the required position
function lenDoubleString(s)
{

    var l = s.length;
    var first_half = s.substr(0, l / 2);
    var second_half = "";

    if (l % 2 == 0)
        second_half = s.substr(l / 2);
    else
        second_half = s.substr(l / 2 + 1);

    second_half = second_half.split("").reverse().join("");

    // Print the double string
    document.write(first_half);
    document.write(second_half+"<br>");

    // Print the length of the double string
    if (l % 2 == 0)
        document.write(l+"<br>");
    else
        document.write(l - 1+"<br>");

}

  var n = "abba";
  lenDoubleString(n);

  n = "abcdedcba";
  lenDoubleString(n);

// This code is contributed by ShubhamSingh10
</script>
```

**Output:** 

```
abab
4
abcdabcd
8
```

**时间复杂度:** O(1)。