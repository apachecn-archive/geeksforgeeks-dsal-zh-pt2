# 在另一个

中作为子序列出现的一个字符串的最大长度前缀

> 原文:[https://www . geesforgeks . org/最大长度-前缀-一个字符串-出现-子序列-另一个/](https://www.geeksforgeeks.org/maximum-length-prefix-one-string-occurs-subsequence-another/)

给定两根弦 **s** 和 **t** 。任务是找出出现在字符串 t 中作为子序列的字符串 S 的某些前缀的最大长度。
**例:**

```
Input : s = "digger"
        t = "biggerdiagram"
Output : 3
digger
biggerdiagram
Prefix "dig" of s is longest subsequence in t.

Input : s = "geeksforgeeks"
        t = "agbcedfeitk"
Output : 4
```

一个**简单的解决方案**是将所有前缀都加 1，检查当前前缀 s[]是否是 t[]的子序列。最后返回长度最大的前缀。
一个**高效的解决方案**是基于这样一个事实:要找到长度为 n 的前缀，我们必须先找到长度为 n–1 的前缀，然后在 t 中寻找 s[n-1]，同样，要找到长度为 n–1 的前缀，我们必须先找到长度为 n–2 的前缀，然后寻找 s[n–2]等等。
因此，我们保留一个计数器，它存储找到的前缀的当前长度。我们用 0 初始化它，从 s 的第一个字母开始，并不断迭代 t 来寻找第一个字母的出现。一遇到 s 的第一个字母，我们就更新计数器，寻找第二个字母。我们不断更新计数器并寻找下一个字母，直到找到字符串 s 或 t 中不再有字母为止。
下面是这种方法的实现:

## C++

```
// C++ program to find maximum
// length prefix of one string
// occur as subsequence in another
// string.
#include<bits/stdc++.h>
using namespace std;

// Return the maximum length
// prefix which is subsequence.
int maxPrefix(char s[], char t[])
{
    int count = 0;

    // Iterating string T.
    for (int i = 0; i < strlen(t); i++)
    {
        // If end of string S.
        if (count == strlen(s))
            break;

        // If character match,
        // increment counter.
        if (t[i] == s[count])
            count++;
    }

    return count;
}

// Driven Code
int main()
{
    char S[] = "digger";
    char T[] = "biggerdiagram";

    cout << maxPrefix(S, T)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// length prefix of one string
// occur as subsequence in another
// string.
public class GFG {    

    // Return the maximum length
    // prefix which is subsequence.
    static int maxPrefix(String s,
                         String t)
    {
        int count = 0;

        // Iterating string T.
        for (int i = 0; i < t.length(); i++)
        {
            // If end of string S.
            if (count == s.length())
                break;

            // If character match, 
            // increment counter.
            if (t.charAt(i) == s.charAt(count))
                count++;
        }

        return count;
    }

    // Driver Code
    public static void main(String args[])
    {
        String S = "digger";
        String T = "biggerdiagram";

        System.out.println(maxPrefix(S, T));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 program to find maximum
# length prefix of one string occur
# as subsequence in another string.

# Return the maximum length
# prefix which is subsequence.
def maxPrefix(s, t) :
    count = 0

    # Iterating string T.
    for i in range(0,len(t)) :

        # If end of string S.
        if (count == len(s)) :
            break

        # If character match,
        # increment counter.
        if (t[i] == s[count]) :
            count = count + 1

    return count

# Driver Code
S = "digger"
T = "biggerdiagram"

print(maxPrefix(S, T))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program to find maximum
// length prefix of one string
// occur as subsequence in
// another string.
using System;

class GFG
{    

    // Return the maximum length prefix
    // which is subsequence.
    static int maxPrefix(String s,
                         String t)
    {
        int count = 0;

        // Iterating string T.
        for (int i = 0; i < t.Length; i++)
        {
            // If end of string S.
            if (count == s.Length)
                break;

            // If character match,
            // increment counter.
            if (t[i] == s[count])
                count++;
        }

        return count;
    }

    // Driver Code
    public static void Main()
    {
        String S = "digger";
        String T = "biggerdiagram";

        Console.Write(maxPrefix(S, T));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// length prefix of one string
// occur as subsequence in another
// string.

// Return the maximum length
// prefix which is subsequence.
function maxPrefix($s, $t)
{
    $count = 0;

    // Iterating string T.
    for ($i = 0; $i < strlen($t); $i++)
    {
        // If end of string S.
        if ($count == strlen($s))
            break;

        // If character match,
        // increment counter.
        if ($t[$i] == $s[$count])
            $count++;
    }

    return $count;
}

// Driver Code
{
    $S = "digger";
    $T = "biggerdiagram";

    echo maxPrefix($S, $T) ;

    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find maximum
// length prefix of one string
// occur as subsequence in another
// string.

    // Return the maximum length
    // prefix which is subsequence.
    function maxPrefix(s,t)
    {
        let count = 0;

        // Iterating string T.
        for (let i = 0; i < t.length; i++)
        {
            // If end of string S.
            if (count == s.length)
                break;

            // If character match, 
            // increment counter.
            if (t[i] == s[count])
                count++;
        }

        return count;
    }

// Driver Code

    let S = "digger";
    let T = "biggerdiagram";

    document.write(maxPrefix(S, T));

</script>
```

**输出:**

```
3
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。