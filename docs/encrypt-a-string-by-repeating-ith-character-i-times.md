# 通过重复第 I 个字符 I 次来加密字符串

> 原文:[https://www . geesforgeks . org/encrypt-a-string-by-repeating-with-character-I-times/](https://www.geeksforgeeks.org/encrypt-a-string-by-repeating-ith-character-i-times/)

给定字符串 **str** ，任务是用给定的加密算法对字符串进行加密。
该字符串的 **1 <sup>st</sup>** 字符将在加密字符串中重复**一次**，该**2<sup>nd</sup>T12】字符将重复两次，…、**n<sup>th</sup>T16】字符将重复 **n** 次。****

**示例:**

> **输入:** str = "极客"
> T3】输出:geeeekkkksss
> 
> **输入:**str = " ABCD "
> T3】输出:abbccdddd

**方法:**初始化 **cnt = 1** 并开始逐字符遍历字符串。重复当前角色 **cnt** 的次数，然后更新 **cnt = cnt + 1** 到达下一个角色。对字符串的每个字符重复这些步骤。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the encrypted string
string encryptString(string str, int n)
{
    int i = 0, cnt = 0;
    string encryptedStr = "";

    while (i < n) {

        // Number of times the current
        // character will be repeated
        cnt = i + 1;

        // Repeat the current character
        // in the encrypted string
        while (cnt--)
            encryptedStr += str[i];
        i++;
    }

    return encryptedStr;
}

// Driver code
int main()
{
    string str = "geeks";
    int n = str.length();
    cout << encryptString(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the encrypted String
static String encryptString(String str, int n)
{
    int i = 0, cnt = 0;
    String encryptedStr = "";

    while (i < n)
    {

        // Number of times the current
        // character will be repeated
        cnt = i + 1;

        // Repeat the current character
        // in the encrypted String
        while (cnt-- >0)
            encryptedStr += str.charAt(i);
        i++;
    }

    return encryptedStr;
}

// Driver code
public static void main(String[] args)
{
    String str = "geeks";
    int n = str.length();
    System.out.println(encryptString(str, n));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the encrypted string
def encryptString(string, n):

    i, cnt = 0, 0
    encryptedStr = ""

    while i < n:

        # Number of times the current
        # character will be repeated
        cnt = i + 1

        # Repeat the current character
        # in the encrypted string
        while cnt > 0:
            encryptedStr += string[i]
            cnt -= 1

        i += 1

    return encryptedStr

# Driver code
if __name__ == "__main__":

    string = "geeks"
    n = len(string)
    print(encryptString(string, n))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the encrypted String
static String encryptString(String str, int n)
{
    int i = 0, cnt = 0;
    String encryptedStr = "";

    while (i < n)
    {

        // Number of times the current
        // character will be repeated
        cnt = i + 1;

        // Repeat the current character
        // in the encrypted String
        while (cnt-- >0)
            encryptedStr += str[i];
        i++;
    }

    return encryptedStr;
}

// Driver code
static public void Main ()
{
    String str = "geeks";
    int n = str.Length;
    Console.WriteLine(encryptString(str, n));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the encrypted string
function encryptString($str, $n)
{
    $i = 0 ;
    $cnt = 0;
    $encryptedStr = "";

    while ($i < $n)
    {

        // Number of times the current
        // character will be repeated
        $cnt = $i + 1;

        // Repeat the current character
        // in the encrypted string
        while ($cnt--)
            $encryptedStr .= $str[$i];
        $i++;
    }

    return $encryptedStr;
}

// Driver code
$str = "geeks";
$n = strlen($str);

echo encryptString($str, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the encrypted String
    function encryptString(str, n)
    {
        let i = 0, cnt = 0;
        let encryptedStr = "";

        while (i < n)
        {

            // Number of times the current
            // character will be repeated
            cnt = i + 1;

            // Repeat the current character
            // in the encrypted String
            while (cnt-- >0)
                encryptedStr += str[i];
            i++;
        }

        return encryptedStr;
    }

    let str = "geeks";
    let n = str.length;
    document.write(encryptString(str, n));

</script>
```

**Output:** 

```
geeeeekkkksssss
```