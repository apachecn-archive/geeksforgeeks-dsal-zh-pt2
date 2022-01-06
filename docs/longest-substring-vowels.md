# 元音最长子串

> 原文:[https://www.geeksforgeeks.org/longest-substring-vowels/](https://www.geeksforgeeks.org/longest-substring-vowels/)

给定一串小写字母 s，我们需要找到仅包含(a，e，I，o，u)的最长子串长度。

**示例:**

```
Input: s = "geeksforgeeks"
Output: 2
Longest substring is "ee"

Input: s = "theeare"
Output: 3
```

其思想是遍历字符串并跟踪字符串中元音的当前数量。如果我们看到不是元音的字符，我们会将计数重置为 0。但是在重置之前，我们更新最大计数值，这将是我们的结果。

## C++

```
// CPP program to find the
// longest substring of vowels.
#include <bits/stdc++.h>
using namespace std;

bool isVowel(char c)
{
    return (c == 'a' || c == 'e' || c == 'i'
            || c == 'o' || c == 'u');

}

int longestVowel(string s)
{
    int count = 0, res = 0;
    for (int i = 0; i < s.length(); i++)
    {

        // Increment current count
        // if s[i] is vowel
        if (isVowel(s[i]))
        count++;    

        else
        {

            // check previous value
            // is greater then or not
            res = max(res, count);

            count = 0;
        }
    }
    return max(res, count);
}

// Driver code
int main()
{
    string s = "theeare";
    cout << longestVowel(s) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// longest substring of vowels.
import java.util.*;

class GFG
{

    static boolean isVowel(char c)
    {
        return (c == 'a' || c == 'e' || c == 'i'
                 || c == 'o' || c == 'u');
    }

    static int longestVowel(String str)
    {
        int count = 0, res = 0;
        char[] s = str.toCharArray();

        for (int i = 0; i < s.length; i++)
        {

            // Increment current count
            // if s[i] is vowel
            if (isVowel(s[i]))
            count++;    

            else
            {
                // check previous value
                // is greater then or not
                res = Math.max(res, count);

                count = 0;
            }
        }

    return Math.max(res, count);
    }

// Driver code
public static void main (String[] args)
{
    String s = "theeare";
    System.out.println(longestVowel(s));
}
}
// This code is contributed by Mr. Somesh Awasthi
```

## 蟒蛇 3

```
# Python3 program to find the
# longest substring of vowels.
def isVowel(c):
    return (c == 'a' or c == 'e' or
            c == 'i' or c == 'o' or
            c == 'u')          

def longestVowel(s):
    count, res = 0, 0

    for i in range(len(s)):

        # Increment current count
        # if s[i] is vowel
        if (isVowel(s[i])):
            count += 1 

        else:

            # check previous value
            # is greater then or not
            res = max(res, count)

            count = 0
    return max(res, count)

# Driver code
if __name__ == "__main__":
    s = "theeare"
    print (longestVowel(s))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find the
// longest substring of vowels.
using System;

class GFG
{

    static bool isVowel(char c)
    {
        return (c == 'a' || c == 'e' || c == 'i' 
                || c == 'o' || c == 'u');
    }

    static int longestVowel(String str)
    {
        int count = 0, res = 0;
        char []s = str.ToCharArray();

        for (int i = 0; i < s.Length; i++)
        {

            // Increment current count
            // if s[i] is vowel
            if (isVowel(s[i]))
            count++;    

            else
            {
                // check previous value
                // is greater then or not
                res = Math.Max(res, count);

                count = 0;
            }
        }

    return Math.Max(res, count);
    }

// Driver code
public static void Main ()
    {
        String s = "theeare";
        Console.Write(longestVowel(s));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// longest substring of vowels.
function isVowel($c)
{
    return ($c == 'a' || $c == 'e' ||
            $c == 'i' || $c == 'o' ||
            $c == 'u');
}

function longestVowel($s)
{
    $count = 0; $res = 0;
    for ($i = 0; $i < strlen($s); $i++)
    {

        // Increment current count
        // if s[i] is vowel
        if (isVowel($s[$i]))
        $count++;    

        else
        {

            // check previous value
            // is greater then or not
            $res = max($res, $count);

            $count = 0;
        }
    }
    return max($res, $count);
}

// Driver code
$s = "theeare";
echo longestVowel($s) ;

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// longest substring of vowels.
function isVowel(c)
{
    return (c == 'a' || c == 'e' ||
            c == 'i' || c == 'o' ||
            c == 'u');
}

function longestVowel(str)
{
    let count = 0, res = 0;
    let s = str.split("");

    for(let i = 0; i < s.length; i++)
    {

        // Increment current count
        // if s[i] is vowel
        if (isVowel(s[i]))
            count++;   
        else
        {

            // Check previous value
            // is greater then or not
            res = Math.max(res, count);

            count = 0;
        }
    }
    return Math.max(res, count);
}

// Driver code
let s = "theeare";
document.write(longestVowel(s));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
3
```

本文由 [**Ajay Puri**](https://www.facebook.com/ajaygoswamiint) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。