# 将字符串转换为回文的最小成本

> 原文:[https://www . geesforgeks . org/mini-cost-convert-string-回文/](https://www.geeksforgeeks.org/minimum-cost-convert-string-palindrome/)

将字符串 S 转换为回文字符串。您只能用任何其他字符替换一个字符。当你用任何其他字符替换字符“a”时，它的成本是 1 个单位，同样，对于“b”它是 2 个单位…..而对于‘z’，它是 26 个单位。找到将字符串 S 转换为回文字符串所需的最小成本。
**例:**

```
Input : abcdef
Output : 6
Explanation: replace 'a', 'b' and 
'c' => cost= 1 + 2 + 3 = 6 

Input : aba
Output : 0
```

这个想法是从字符串的两端开始比较。让 **i** 初始化为 0 索引， **j** 初始化为长度–1。如果两个索引处的字符不相同，则需要支付费用。为了使成本最小，请替换较小的字符。然后将 **i** 增加 1，将 **j** 减少 1。重复直到 **i** 小于 **j** 。

## C++

```
// CPP program to find minimum cost to make
// a palindrome.
#include <bits/stdc++.h>
using namespace std;

// Function to return cost
int cost(string str)
{
    // length of string
    int len = str.length();     

    // Iterate from  both sides of string.
    // If not equal, a cost will be there
    int res = 0;
    for (int i=0, j=len-1; i < j; i++, j--)        
        if (str[i] != str[j])
            res += min(str[i], str[j]) - 'a' + 1;       

    return res;
}

// Driver code
int main()
{
    string str = "abcdef";
    cout << cost(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum cost to make
// a palindrome.
import java.io.*;

class GFG
{
    // Function to return cost
    static int cost(String str)
    {
        // length of string
        int len = str.length();

        // Iterate from both sides of string.
        // If not equal, a cost will be there
        int res = 0;
        for (int i = 0, j = len - 1; i < j; i++, j--)    
            if (str.charAt(i) != str.charAt(j))
                res += Math.min(str.charAt(i), str.charAt(j))
                                - 'a' + 1;    

        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "abcdef";
        System.out.println(cost(str));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# python program to find minimum
# cost to make a palindrome.

# Function to return cost
def cost(st):

    # length of string
    l = len(st)    

    # Iterate from both sides
    # of string. If not equal,
    # a cost will be there
    res = 0
    j = l - 1
    i = 0
    while(i < j):        
        if (st[i] != st[j]):
            res += (min(ord(st[i]),
                    ord(st[j])) -
                     ord('a') + 1)

        i = i + 1
        j = j - 1

    return res

# Driver code
st = "abcdef";
print(cost(st))

# This code is contributed by
# Sam007
```

## C#

```
// C# program to find minimum cost
// to make a palindrome.
using System;

class GFG
{

    // Function to return cost
    static int cost(String str)
    {
        // length of string
        int len = str.Length;

        // Iterate from both sides of string.
        // If not equal, a cost will be there
        int res = 0;
        for (int i = 0, j = len - 1; i < j; i++, j--)    
            if (str[i] != str[j])
                res += Math.Min(str[i], str[j])
                                - 'a' + 1;

        return res;
    }

    // Driver code
    public static void Main ()
    {
        string str = "abcdef";
        Console.WriteLine(cost(str));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// cost to make a palindrome.

// Function to return cost
function cost($str)
{
    // length of string
    $len = strlen($str);    

    // Iterate from both sides
    // of string. If not equal,
    // a cost will be there
    $res = 0;
    for ($i = 0, $j = $len - 1;
                $i < $j; $i++, $j--)        
        if ($str[$i] != $str[$j])
            $res += (min(ord($str[$i]),
                       ord($str[$j])) -
                       ord('a') + 1 );    

    return $res;
}

// Driver code
$str = "abcdef";
echo cost($str);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript program to find minimum cost
    // to make a palindrome.

    // Function to return cost
    function cost(str)
    {
        // length of string
        let len = str.length;

        // Iterate from both sides of string.
        // If not equal, a cost will be there
        let res = 0;
        for (let i = 0, j = len - 1; i < j; i++, j--)  
        {
            if (str[i] != str[j])
            {
                res += Math.min(str[i].charCodeAt(), str[j].charCodeAt()) - 'a'.charCodeAt() + 1;
            }
        }    

        return res;
    }

    let str = "abcdef";
      document.write(cost(str));

</script>
```

**输出:**

```
6
```