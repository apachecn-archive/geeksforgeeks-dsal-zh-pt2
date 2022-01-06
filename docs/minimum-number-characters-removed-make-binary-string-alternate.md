# 使二进制字符串交替出现需要删除的最少字符数

> 原文:[https://www . geesforgeks . org/最小字符数-删除-生成-二进制-字符串-替代/](https://www.geeksforgeeks.org/minimum-number-characters-removed-make-binary-string-alternate/)

给定一个二进制字符串，任务是找到要从中删除的最少字符数，使其成为替代字符。如果没有两个连续的 0 或 1，则二进制字符串是可选的。
**例:**

```
Input  : s = "000111"
Output : 4  
We need to delete two 0s and
two 1s to make string alternate.

Input  : s = "0000"
Output : 3  
We need to delete three characters
to make it alternate.

Input  :  s = "11111"
Output :  4   

Input  : s = "01010101"
Output : 0   

Input  : s = "101010"
Output : 0  
```

这个问题有以下简单的解决方法。
我们从左到右遍历字符串，并将当前字符与下一个字符进行比较。

1.  如果当前和下一个不同，则不需要执行删除。
2.  如果当前和下一个相同，我们需要执行一个删除操作来使它们交替。

下面是上述算法的实现。

## C++

```
// C++ program to find minimum number
// of characters to be removed to make
// a string alternate.
#include <bits/stdc++.h>
using namespace std;

// Returns count of minimum characters to
// be removed to make s alternate.
void countToMake0lternate(const string& s)
{
    int result = 0;

    for (int i = 0; i < (s.length() - 1); i++)

        // if two alternating characters
        // of string are same
        if (s[i] == s[i + 1])
            result++; // then need to
    // delete a character

    return result;
}

// Driver code
int main()
{
    cout << countToMake0lternate("000111") << endl;
    cout << countToMake0lternate("11111") << endl;
    cout << countToMake0lternate("01010101") << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number
// of characters to be removed to make
// a string alternate.
import java.io.*;

public class GFG {

    // Returns count of minimum characters to
    // be removed to make s alternate.
    static int countToMake0lternate(String s)
    {
        int result = 0;

        for (int i = 0; i < (s.length() - 1); i++)

            // if two alternating characters
            // of string are same
            if (s.charAt(i) == s.charAt(i + 1))
                result++; // then need to
        // delete a character

        return result;
    }

    // Driver code
    static public void main(String[] args)
    {
        System.out.println(countToMake0lternate("000111"));
        System.out.println(countToMake0lternate("11111"));
        System.out.println(countToMake0lternate("01010101"));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to find minimum number
# of characters to be removed to make
# a string alternate.

# Returns count of minimum characters
# to be removed to make s alternate.
def countToMake0lternate(s):

    result = 0

    for i in range(len(s) - 1):

        # if two alternating characters
        # of string are same
        if (s[i] == s[i + 1]):
            result += 1 # then need to
                        # delete a character

    return result

# Driver code
if __name__ == "__main__":

    print(countToMake0lternate("000111"))
    print(countToMake0lternate("11111"))
    print(countToMake0lternate("01010101"))

# This code is contributed by ita_c
```

## C#

```
// C# program to find minimum number
// of characters to be removed to make
// a string alternate.
using System;

public class GFG {

    // Returns count of minimum characters to
    // be removed to make s alternate.
    static int countToMake0lternate(string s)
    {
        int result = 0;

        for (int i = 0; i < (s.Length - 1); i++)

            // if two alternating characters
            // of string are same
            if (s[i] == s[i + 1])
                result++; // then need to
        // delete a character

        return result;
    }

    // Driver code
    static public void Main()
    {
        Console.WriteLine(countToMake0lternate("000111"));
        Console.WriteLine(countToMake0lternate("11111"));
        Console.WriteLine(countToMake0lternate("01010101"));
    }
}

// This article is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum number
// of characters to be removed to make
// a string alternate.

// Returns count of minimum characters
// to be removed to make s alternate.
function countToMake0lternate($s)
{
    $result = 0;

    for ($i = 0; $i < (strlen($s) - 1); $i++)

        // if two alternating characters
        // of string are same
        if ($s[$i] == $s[$i + 1])

            // then need to
            // delete a character
            $result++;

    return $result;
}

    // Driver code
    echo countToMake0lternate("000111"),"\n" ;
    echo countToMake0lternate("11111"),"\n" ;
    echo countToMake0lternate("01010101") ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum number
// of characters to be removed to make
// a string alternate.

    // Returns count of minimum characters to
    // be removed to make s alternate.
    function countToMake0lternate(s)
    {
        let result = 0;

        for (let i = 0; i < (s.length - 1); i++)

            // if two alternating characters
            // of string are same
            if (s[i] == s[i+1])
                result++; // then need to
        // delete a character

        return result;
    }

    // Driver code
    document.write(countToMake0lternate("000111")+"<br>");
    document.write(countToMake0lternate("11111")+"<br>");
    document.write(countToMake0lternate("01010101")+"<br>");

    // This code is contributed by rag2127

</script>
```

**输出:**

```
4
4
0
```

时间复杂度:O(n)，其中 n 是输入字符串中的字符数。
本文由 [**拉维·毛里亚(特洛伊)**](https://www.facebook.com/dangeroustrojan) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。