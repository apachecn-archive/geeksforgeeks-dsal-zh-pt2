# 解密通过重复第 I 个字符 I 次加密的字符串

> 原文:[https://www . geesforgeks . org/decrypt-a-string-repeating-I-th-character-I-times/](https://www.geeksforgeeks.org/decrypt-a-string-encrypted-by-repeating-i-th-character-i-times/)

给定一个加密的字符串 **str** 和加密算法，任务是解密该字符串。加密算法如下:
字符串的 **1 <sup>st</sup>** 字符在加密后的字符串中会重复**一次**，而**2<sup>nd</sup>T12】字符会重复两次，…、**n<sup>th</sup>T16】字符会重复 **n** 次。例如，字符串**“ABCD”**将被加密为**“abbccdddd”**。****

**示例:**

> **输入:**输出:极客
> 
> **输入:**输出: abcd

**方式:**初始化 **i = 0** 并打印**str【I】**。
更新 **i = i + 1** 并打印**str【I】**，然后更新 **i = i + 2** 并打印**str【I】**以此类推，同时 **i <长度(str)** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the decrypted string
string decryptString(string str, int n)
{

    // Initial jump will be 1
    int i = 0, jump = 1;
    string decryptedStr = "";

    while (i < n) {
        decryptedStr += str[i];
        i += jump;

        // Increment jump by 1 with every character
        jump++;
    }

    return decryptedStr;
}

// Driver code
int main()
{
    string str = "geeeeekkkksssss";
    int n = str.length();
    cout << decryptString(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the decrypted string
static String decryptString(String str, int n)
{

    // Initial jump will be 1
    int i = 0, jump = 1;
    String decryptedStr = "";

    while (i < n)
    {
        decryptedStr += str.charAt(i);
        i += jump;

        // Increment jump by 1 with every character
        jump++;
    }

    return decryptedStr;
}

// Driver code
public static void main(String[] args)
{
    String str = "geeeeekkkksssss";
    int n = str.length();
    System.out.println(decryptString(str, n));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the decrypted string
def decryptString(str, n):

    # Initial jump will be 1
    i = 0
    jump = 1
    decryptedStr = ""

    while (i < n):
        decryptedStr += str[i];
        i += jump

        # Increment jump by 1 with
        # every character
        jump += 1

    return decryptedStr

# Driver code
if __name__ == '__main__':
    str = "geeeeekkkksssss"
    n = len(str)
    print(decryptString(str, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the decrypted string
static string decryptString(string str, int n)
{

    // Initial jump will be 1
    int i = 0, jump = 1;
    string decryptedStr = "";

    while (i < n)
    {
        decryptedStr += str[i];
        i += jump;

        // Increment jump by 1 with every character
        jump++;
    }

    return decryptedStr;
}

// Driver code
public static void Main()
{
    string str = "geeeeekkkksssss";
    int n = str.Length;
    Console.Write(decryptString(str, n));
}
}

// This code is contributed by ita_c
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the decrypted string
function decryptString($str, $n)
{

    // Initial jump will be 1
    $i = 0 ;
    $jump = 1 ;
    $decryptedStr = "";

    while ($i < $n)
    {
        $decryptedStr .= $str[$i];
        $i += $jump;

        // Increment jump by 1 with
        // every character
        $jump++;
    }
    return $decryptedStr;
}

// Driver code
$str = "geeeeekkkksssss";
$n = strlen($str);
echo decryptString($str, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the decrypted string
function decryptString(str,n)
{
    // Initial jump will be 1
    let i = 0, jump = 1;
    let decryptedStr = "";

    while (i < n)
    {
        decryptedStr += str[i];
        i += jump;

        // Increment jump by 1 with every character
        jump++;
    }

    return decryptedStr;
}

// Driver code
let str = "geeeeekkkksssss";
let n = str.length;
document.write(decryptString(str, n));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
geeks
```