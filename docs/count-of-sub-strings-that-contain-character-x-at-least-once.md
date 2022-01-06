# 包含字符 X 至少一次的子串计数

> 原文:[https://www . geeksforgeeks . org/包含至少一次字符 x 的子字符串计数/](https://www.geeksforgeeks.org/count-of-sub-strings-that-contain-character-x-at-least-once/)

给定一个字符串**字符串**和一个字符 **X** 。任务是至少找到一次包含字符 **X** 的子字符串总数。
**举例:**

> **输入:** str = "abcd "，X = 'b'
> **输出:**6
> “ab”“ABC”“ABCD”“b”“BC”“BCD”为必输子串。
> **输入:** str = "geeksforgeeks "，X = 'e'
> **输出:** 66

**方式:**子串总数为 **n * (n + 1) / 2** ，其中只需统计包含字符 **X** 的子串。字符 **X** 出现在从 **X** 位置到字符串长度的子字符串中。对于 **X** 之前的每个字符，必须对该子串进行计数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// required sub-strings
int countSubStr(string str, int n, char x)
{
    int res = 0, count = 0;
    for (int i = 0; i < n; i++) {
        if (str[i] == x) {

            // Number of sub-strings from position
            // of current x to the end of str
            res += ((count + 1) * (n - i));

            // To store the number of characters
            // before x
            count = 0;
        }
        else
            count++;
    }

    return res;
}

// Driver code
int main()
{
    string str = "abcabc";
    int n = str.length();
    char x = 'c';

    cout << countSubStr(str, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of
// required sub-strings
static int countSubStr(String str, int n, char x)
{
    int res = 0, count = 0;
    for (int i = 0; i < n; i++)
    {
        if (str.charAt(i) == x)
        {

            // Number of sub-strings from position
            // of current x to the end of str
            res += ((count + 1) * (n - i));

            // To store the number of characters
            // before x
            count = 0;
        }
        else
            count++;
    }

    return res;
}

// Driver code
public static void main(String[] args)
{
    String str = "abcabc";
    int n = str.length();
    char x = 'c';

    System.out.println(countSubStr(str, n, x));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the count of
# required sub-strings
def countSubStr(str, n, x):
    res = 0; count = 0;
    for i in range(n):
        if (str[i] == x):

            # Number of sub-strings from position
            # of current x to the end of str
            res += ((count + 1) * (n - i));

            # To store the number of characters
            # before x
            count = 0;
        else:
            count+=1;

    return res;

# Driver code
str = "abcabc";
n = len(str);
x = 'c';

print(countSubStr(str, n, x));

# This code contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// required sub-strings
static int countSubStr(String str, int n, char x)
{
    int res = 0, count = 0;
    for (int i = 0; i < n; i++)
    {
        if (str[i] == x)
        {

            // Number of sub-strings from position
            // of current x to the end of str
            res += ((count + 1) * (n - i));

            // To store the number of characters
            // before x
            count = 0;
        }
        else
            count++;
    }

    return res;
}

// Driver code
public static void Main(String[] args)
{
    String str = "abcabc";
    int n = str.Length;
    char x = 'c';

    Console.WriteLine(countSubStr(str, n, x));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of
// required sub-strings
function countSubStr($str, $n, $x)
{
    $res = 0; $count = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($str[$i] == $x)
        {

            // Number of sub-strings from position
            // of current x to the end of str
            $res += (($count + 1) * ($n - $i));

            // To store the number of characters
            // before x
            $count = 0;
        }
        else
            $count++;
    }

    return $res;
}

// Driver code
$str = "abcabc";
$n = strlen($str);
$x = 'c';

echo countSubStr($str, $n, $x);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the count of
    // required sub-strings
    function countSubStr(str, n, x)
    {
        let res = 0, count = 0;
        for (let i = 0; i < n; i++)
        {
            if (str[i] == x)
            {

                // Number of sub-strings from position
                // of current x to the end of str
                res += ((count + 1) * (n - i));

                // To store the number of characters
                // before x
                count = 0;
            }
            else
                count++;
        }

        return res;
    }

    let str = "abcabc";
    let n = str.length;
    let x = 'c';

    document.write(countSubStr(str, n, x));

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
15
```