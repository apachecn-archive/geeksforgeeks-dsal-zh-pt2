# 统计以给定模式结束的字符串

> 原文:[https://www . geesforgeks . org/count-strings-以给定模式结束/](https://www.geeksforgeeks.org/count-strings-that-end-with-the-given-pattern/)

给定一个模式 **pat** 和一个字符串数组**sArr【】**，任务是统计数组中以给定模式结束的字符串数量。
**例:**

> **输入:**pat =“ks”，sArr[] = {“极客”、“极客 forgeks”、“games”、“unit”}
> **输出:** 2
> 只有字符串“极客”和“极客 forgeks”以模式“ks”结尾。
> **输入:**pat =“ABC”，SarR[]= {“ABCD”、“abcc”、“aaa”、“BBB”}
> **输出:** 0

**进场:**

*   初始化**计数= 0** 并开始遍历给定的字符串数组。
*   对于每个字符串 **str** ，初始化 **strLen = len(str)** 和 **patLen = len(pattern)** 。
    *   如果 **patLen > strLen** 则跳到下一个字符串，因为当前字符串不能以给定的模式结束。
    *   否则，将字符串与从末尾开始的模式匹配。如果字符串与模式匹配，则更新**计数=计数+ 1** 。
*   最后打印**计数**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that return true if str
// ends with pat
bool endsWith(string str, string pat)
{
    int patLen = pat.length();
    int strLen = str.length();

    // Pattern is larger in length than
    // the string
    if (patLen > strLen)
        return false;

    // We match starting from the end while
    // patLen is greater than or equal to 0.
    patLen--;
    strLen--;
    while (patLen >= 0) {

        // If at any index str doesn't match
        // with pattern
        if (pat[patLen] != str[strLen])
            return false;
        patLen--;
        strLen--;
    }

    // If str ends with the given pattern
    return true;
}

// Function to return the count of required
// strings
int countOfStrings(string pat, int n,
                       string sArr[])
{
    int count = 0;

    for (int i = 0; i < n; i++)

        // If current string ends with
        // the given pattern
        if (endsWith(sArr[i], pat))
            count++;

    return count;
}

// Driver code
int main()
{

    string pat = "ks";
    int n = 4;
    string sArr[] = { "geeks", "geeksforgeeks", "games", "unit" };

    cout << countOfStrings(pat, n, sArr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

    // Function that return true
    // if str ends with pat
    static boolean endsWith(String str, String pat)
    {
        int patLen = pat.length();
        int strLen = str.length();

        // Pattern is larger in length
        // than the string
        if (patLen > strLen)
            return false;

        // We match starting from the end while
        // patLen is greater than or equal to 0.
        patLen--;
        strLen--;
        while (patLen >= 0)
        {

            // If at any index str doesn't match
            // with pattern
            if (pat.charAt(patLen) != str.charAt(strLen))
                return false;
            patLen--;
            strLen--;
        }

        // If str ends with the given pattern
        return true;
    }

    // Function to return the
    // count of required strings
    static int countOfStrings(String pat, int n,
                        String sArr[])
    {
        int count = 0;
        for (int i = 0; i < n; i++)
        {

            // If current string ends with
            // the given pattern
            if (endsWith(sArr[i], pat))
                count++;
        }
        return count;
    }

    // Driver code
    public static void main(String []args)
    {
        String pat = "ks";
        int n = 4;
        String sArr[] = { "geeks", "geeksforgeeks", "games", "unit" };
        System.out.println(countOfStrings(pat, n, sArr));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that return true if str1
# ends with pat
def endsWith(str1, pat):

    patLen = len(pat)
    str1Len = len(str1)

    # Pattern is larger in length
    # than the str1ing
    if (patLen > str1Len):
        return False

    # We match starting from the end while
    # patLen is greater than or equal to 0.
    patLen -= 1
    str1Len -= 1
    while (patLen >= 0):

        # If at any index str1 doesn't match
        # with pattern
        if (pat[patLen] != str1[str1Len]):
            return False
        patLen -= 1
        str1Len -= 1

    # If str1 ends with the given pattern
    return True

# Function to return the count of
# required str1ings
def countOfstr1ings(pat, n, sArr):

    count = 0

    for i in range(n):

        # If current str1ing ends with
        # the given pattern
        if (endsWith(sArr[i], pat) == True):
            count += 1
    return count

# Driver code
pat = "ks"
n = 4
sArr= [ "geeks", "geeksforgeeks",
                 "games", "unit"]

print(countOfstr1ings(pat, n, sArr))

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that return true if str
// ends with pat
static bool endsWith(string str, string pat)
{
    int patLen = pat.Length;
    int strLen = str.Length;

    // Pattern is larger in length than
    // the string
    if (patLen > strLen)
        return false;

    // We match starting from the end while
    // patLen is greater than or equal to 0.
    patLen--;
    strLen--;
    while (patLen >= 0)
    {

        // If at any index str doesn't match
        // with pattern
        if (pat[patLen] != str[strLen])
            return false;
        patLen--;
        strLen--;
    }

    // If str ends with the given pattern
    return true;
}

// Function to return the count of required
// strings
static int countOfStrings(string pat, int n,
                        string[] sArr)
{
    int count = 0;

    for (int i = 0; i < n; i++)

        // If current string ends with
        // the given pattern
        if (endsWith(sArr[i], pat))
            count++;

    return count;
}

// Driver code
public static void Main()
{

    string pat = "ks";
    int n = 4;
    string[] sArr = { "geeks", "geeksforgeeks",
                                "games", "unit" };
    Console.WriteLine(countOfStrings(pat, n, sArr));
}
}

// This code is contributed by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that return true if str
// ends with pat
function endsWith($str, $pat)
{
    $patLen = strlen($pat);
    $strLen = strlen($str);

    // Pattern is larger in length than
    // the string
    if ($patLen > $strLen)
        return false;

    // We match starting from the end while
    // patLen is greater than or equal to 0.
    $patLen--;
    $strLen--;
    while ($patLen >= 0)
    {

        // If at any index str doesn't match
        // with pattern
        if ($pat[$patLen] != $str[$strLen])
            return false;
        $patLen--;
        $strLen--;
    }

    // If str ends with the given pattern
    return true;
}

// Function to return the count of required
// strings
function countOfStrings($pat, $n, $sArr)
{
    $count = 0;

    for ($i = 0; $i < $n; $i++)

        // If current string ends with
        // the given pattern
        if (endsWith($sArr[$i], $pat))
            $count++;

    return $count;
}

// Driver code
$pat = "ks";
$n = 4;
$sArr = array("geeks", "geeksforgeeks",
              "games", "unit");

echo countOfStrings($pat, $n, $sArr);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // Function that return true
    // if str ends with pat
    function endsWith(str,pat)
    {
        let patLen = pat.length;
        let strLen = str.length;

        // Pattern is larger in length
        // than the string
        if (patLen > strLen)
            return false;

        // We match starting from the end while
        // patLen is greater than or equal to 0.
        patLen--;
        strLen--;
        while (patLen >= 0)
        {

            // If at any index str doesn't match
            // with pattern
            if (pat[patLen] != str[strLen])
                return false;
            patLen--;
            strLen--;
        }

        // If str ends with the given pattern
        return true;
    }

     // Function to return the
    // count of required strings
    function countOfStrings(pat,n,sArr)
    {
        let count = 0;
        for (let i = 0; i < n; i++)
        {

            // If current string ends with
            // the given pattern
            if (endsWith(sArr[i], pat))
                count++;
        }
        return count;
    }

    // Driver code
    let pat = "ks";
    let n = 4;
    let sArr=[ "geeks", "geeksforgeeks", "games", "unit"];
    document.write(countOfStrings(pat, n, sArr));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
2
```