# 将一个给定的二进制字符串转换为全 1 所需的最小给定运算

> 原文:[https://www . geesforgeks . org/最小给定操作-要求将给定二进制字符串转换为全 1/](https://www.geeksforgeeks.org/minimum-given-operations-required-to-convert-a-given-binary-string-to-all-1s/)

给定一个二进制数作为长度为 1 的字符串。任务是找到所需的最小操作数，使该数变为 **2 <sup>L</sup> -1** ，即仅由长度为 **L** 的**1**组成的字符串。
在每次操作中，数字 **N** 可以用 **N xor (N + 1)** 代替。
**举例:**

> **输入:**【str = " 10010111 "
> **输出:** 5
> N = 1001011，N + 1 = 10011000，因此 n xor(n+1)= 00001111
> n = 00001111，N + 1 = 00010000，所以 n xor(n+1)= 000111
> so n xorg(n+1)= 01111111
> 【n = 01111111，N + 1 = 10000000，so n xorg(n+1)= 11111**t11**输入:**str = " 101000101011111】**输出:** 17**

**进场:**执行给定的操作后，可以观察到为了得到需要的数量，最终操作的数量会是:

> **操作数** =字符串长度(去除前导 0 后)–从末尾开始的连续 1 的计数(从最低有效位开始)

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number
// of operations required
int changeToOnes(string str)
{

    // ctr will store the number of
    // consecutive ones at the end
    // of the given binary string
    int i, l, ctr = 0;
    l = str.length();

    // Loop to find number of 1s
    // at the end of the string
    for (i = l - 1; i >= 0; i--) {

        // If the current character is 1
        if (str[i] == '1')
            ctr++;

        // If we encounter the first 0
        // from the LSB position then
        // we'll break the loop
        else
            break;
    }

    // Number of operations
    // required is (l - ctr)
    return l - ctr;
}

// Function to remove leading
// zeroes from the string
string removeZeroesFromFront(string str)
{
    string s;

    int i = 0;

    // Loop until s[i] becomes
    // not equal to 1
    while (i < str.length() && str[i] == '0')
        i++;

    // If we reach the end of
    // the string, it means that
    // string contains only 0's
    if (i == str.length())
        s = "0";

    // Return the string without
    // leading zeros
    else
        s = str.substr(i, str.length() - i);
    return s;
}

// Driver code
int main()
{
    string str = "10010111";

    // Removing the leading zeroes
    str = removeZeroesFromFront(str);

    cout << changeToOnes(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the number
// of operations required
static int changeToOnes(String str)
{

    // ctr will store the number of
    // consecutive ones at the end
    // of the given binary string
    int i, l, ctr = 0;
    l = str.length();

    // Loop to find number of 1s
    // at the end of the string
    for (i = l - 1; i >= 0; i--)
    {

        // If the current character is 1
        if (str.charAt(i) == '1')
            ctr++;

        // If we encounter the first 0
        // from the LSB position then
        // we'll break the loop
        else
            break;
    }

    // Number of operations
    // required is (l - ctr)
    return l - ctr;
}

// Function to remove leading
// zeroes from the string
static String removeZeroesFromFront(String str)
{
    String s;

    int i = 0;

    // Loop until s[i] becomes
    // not equal to 1
    while (i < str.length() &&
               str.charAt(i) == '0')
        i++;

    // If we reach the end of
    // the string, it means that
    // string contains only 0's
    if (i == str.length())
        s = "0";

    // Return the string without
    // leading zeros
    else
        s = str.substring(i, str.length() - i);
    return s;
}

// Driver code
public static void main(String[] args)
{
    String str = "10010111";

    // Removing the leading zeroes
    str = removeZeroesFromFront(str);

    System.out.println(changeToOnes(str));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number
# of operations required
def changeToOnes(string) :

    # ctr will store the number of
    # consecutive ones at the end
    # of the given binary string
    ctr = 0;
    l = len(string);

    # Loop to find number of 1s
    # at the end of the string
    for i in range(l - 1, -1, -1) :

        # If the current character is 1
        if (string[i] == '1') :
            ctr += 1;

        # If we encounter the first 0
        # from the LSB position then
        # we'll break the loop
        else :
            break;

    # Number of operations
    # required is (l - ctr)
    return l - ctr;

# Function to remove leading
# zeroes from the string
def removeZeroesFromFront(string) :

    s = "";

    i = 0;

    # Loop until s[i] becomes
    # not equal to 1
    while (i < len(string) and
                   string[i] == '0') :
        i += 1;

    # If we reach the end of
    # the string, it means that
    # string contains only 0's
    if (i == len(string)) :
        s = "0";

    # Return the string without
    # leading zeros
    else :
        s = string[i: len(string) - i];

    return s;

# Driver code
if __name__ == "__main__" :

    string = "10010111";

    # Removing the leading zeroes
    string = removeZeroesFromFront(string);

    print(changeToOnes(string));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the number
// of operations required
static int changeToOnes(String str)
{

    // ctr will store the number of
    // consecutive ones at the end
    // of the given binary string
    int i, l, ctr = 0;
    l = str.Length;

    // Loop to find number of 1s
    // at the end of the string
    for (i = l - 1; i >= 0; i--)
    {

        // If the current character is 1
        if (str[i] == '1')
            ctr++;

        // If we encounter the first 0
        // from the LSB position then
        // we'll break the loop
        else
            break;
    }

    // Number of operations
    // required is (l - ctr)
    return l - ctr;
}

// Function to remove leading
// zeroes from the string
static String removeZeroesFromFront(String str)
{
    String s;

    int i = 0;

    // Loop until s[i] becomes
    // not equal to 1
    while (i < str.Length &&
               str[i] == '0')
        i++;

    // If we reach the end of
    // the string, it means that
    // string contains only 0's
    if (i == str.Length)
        s = "0";

    // Return the string without
    // leading zeros
    else
        s = str.Substring(i, str.Length - i);
    return s;
}

// Driver code
public static void Main(String[] args)
{
    String str = "10010111";

    // Removing the leading zeroes
    str = removeZeroesFromFront(str);

    Console.WriteLine(changeToOnes(str));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the number
// of operations required
function changeToOnes(str)
{

    // ctr will store the number of
    // consecutive ones at the end
    // of the given binary string
    var i, l, ctr = 0;
    l = str.length;

    // Loop to find number of 1s
    // at the end of the string
    for (i = l - 1; i >= 0; i--) {

        // If the current character is 1
        if (str[i] == '1')
            ctr++;

        // If we encounter the first 0
        // from the LSB position then
        // we'll break the loop
        else
            break;
    }

    // Number of operations
    // required is (l - ctr)
    return l - ctr;
}

// Function to remove leading
// zeroes from the string
function removeZeroesFromFront(str)
{
    var s;

    var i = 0;

    // Loop until s[i] becomes
    // not equal to 1
    while (i < str.length && str[i] == '0')
        i++;

    // If we reach the end of
    // the string, it means that
    // string contains only 0's
    if (i == str.length)
        s = "0";

    // Return the string without
    // leading zeros
    else
        s = str.substring(i, str.length - i);
    return s;
}

// Driver code
var str = "10010111";
// Removing the leading zeroes
str = removeZeroesFromFront(str);
document.write( changeToOnes(str));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(n)