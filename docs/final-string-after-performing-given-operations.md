# 执行给定操作后的最终字符串

> 原文:[https://www . geeksforgeeks . org/final-执行给定操作后的字符串/](https://www.geeksforgeeks.org/final-string-after-performing-given-operations/)

给定仅包含字符 **x** 和 **y** 的字符串 **str** ，任务是尽可能执行以下操作:
找到一个索引，使得 **s[i] = 'x'** 和 **s[i+1] = 'y'** 并删除字符 **s[i]** 和 **s[i+1]** ，如果没有找到这样的索引，则找到这样的索引
执行给定操作后，打印最终字符串。
**举例:**

> **输入:** str = "xyyxx"
> **输出:** x
> 第一步:yxx (xy 被删除)
> 第二步:xyx (yx 被交换)
> 第三步:x (xy 被删除)
> **输入:**str = " xxyyyyyyy "
> **输出:** y

**方法:**在最后一个字符串中，要么只有 **x** 要么只有 **y** ，因为如果我们在字符串中同时有 **x** 和 **y** ，那么就会有一个点，我们有 **xy** 或 **yx** 作为子字符串。

*   如果是 **xy** ，我们直接删除。
*   如果是 **yx** ，我们反过来得到 **xy** ，然后删除。

因为在每个删除步骤中，一个 **x** 和一个 **y** 被删除，所以最后的字符串将删除 **min(x，y)** 数量的 **x** 和 **y** 字符。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the modified string
string printFinalString(string s)
{
    int i, n;
    n = s.length();
    int x = 0, y = 0;
    for (i = 0; i < n; i++) {

        // Count number of 'x'
        if (s[i] == 'x')
            x++;

        // Count number of 'y'
        else
            y++;
    }

    string finalString = "";

    // min(x, y) number of 'x' and 'y' will be deleted
    if (x > y)
        for (i = 0; i < x - y; i++)
            finalString += "x";
    else
        for (i = 0; i < y - x; i++)
            finalString += "y";

    return finalString;
}

// Driver Program to test above function
int main()
{
    string s = "xxyyxyy";
    cout << printFinalString(s);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
// Function to return the modified String
static String printFinalString(String s)
{
    int i, n;
    n = s.length();
    int x = 0, y = 0;
    for (i = 0; i < n; i++)
    {

        // Count number of 'x'
        if (s.charAt(i) == 'x')
        {
            x++;
        } // Count number of 'y'
        else
        {
            y++;
        }
    }

    String finalString = "";

    // min(x, y) number of 'x' and
    // 'y' will be deleted
    if (x > y)
    {
        for (i = 0; i < x - y; i++)
        {
            finalString += "x";
        }
    }
    else
    {
        for (i = 0; i < y - x; i++)
        {
            finalString += "y";
        }
    }

    return finalString;
}

// Driver Code
public static void main(String args[])
{
    String s = "xxyyxyy";
    System.out.println(printFinalString(s));
}
}

// This code is contributed
// by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the modified string
def prFinalString(s):
    i, n = 0, 0
    n = len(s)
    x, y = 0, 0
    for i in range(0, n):

        # Count number of 'x'
        if (s[i] == 'x'):
            x += 1

        # Count number of 'y'
        else:
            y += 1

    finalString = ""

    # min(x, y) number of 'x' and
    # 'y' will be deleted
    if (x > y):
        for i in range(0, x - y):
            finalString += "x"
    else:
        for i in range(0, y - x):
            finalString += "y"

    return finalString

# Driver Code
if __name__ == '__main__':
    s = "xxyyxyy"
    print(prFinalString(s))

# This code contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
// Function to return the modified String
static string printFinalString(string s)
{
    int i, n;
    n = s.Length;
    int x = 0, y = 0;
    for (i = 0; i < n; i++)
    {

        // Count number of 'x'
        if (s[i] == 'x')
        {
            x++;
        } // Count number of 'y'
        else
        {
            y++;
        }
    }

    string finalString = "";

    // min(x, y) number of 'x' and
    // 'y' will be deleted
    if (x > y)
    {
        for (i = 0; i < x - y; i++)
        {
            finalString += "x";
        }
    }
    else
    {
        for (i = 0; i < y - x; i++)
        {
            finalString += "y";
        }
    }

    return finalString;
}

// Driver Code
public static void Main()
{
    string s = "xxyyxyy";
    Console.WriteLine(printFinalString(s));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the modified string
function printFinalString($s)
{
    $n = strlen($s);
    $x = 0;
    $y = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // Count number of 'x'
        if ($s[$i] == 'x')
            $x++;

        // Count number of 'y'
        else
            $y++;
    }

    $finalString = (string)null;

    // min(x, y) number of 'x' and 'y' will be deleted
    if ($x > $y)
        for ($i = 0; $i < $x - $y; $i++)
            $finalString .= "x";
    else
        for ($i = 0; $i < $y - $x; $i++)
            $finalString .= "y";

    return $finalString;
}

// Driver Code
$s = "xxyyxyy";
echo printFinalString($s);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the modified string
function printFinalString(s)
{
    var i, n;
    n = s.length;
    var x = 0, y = 0;
    for (i = 0; i < n; i++) {

        // Count number of 'x'
        if (s[i] == 'x')
            x++;

        // Count number of 'y'
        else
            y++;
    }

    var finalString = "";

    // min(x, y) number of 'x' and 'y' will be deleted
    if (x > y)
        for (i = 0; i < x - y; i++)
            finalString += "x";
    else
        for (i = 0; i < y - x; i++)
            finalString += "y";

    return finalString;
}

// Driver Program to test above function
var s = "xxyyxyy";
document.write( printFinalString(s));

// This code is contributed by famously.
</script>
```

**Output:** 

```
y
```