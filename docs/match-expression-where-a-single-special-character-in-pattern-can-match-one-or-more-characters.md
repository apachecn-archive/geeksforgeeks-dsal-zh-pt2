# 匹配表达式，其中模式中的单个特殊字符可以匹配一个或多个字符

> 原文:[https://www . geesforgeks . org/match-expression-其中单个特殊字符模式可以匹配一个或多个字符/](https://www.geeksforgeeks.org/match-expression-where-a-single-special-character-in-pattern-can-match-one-or-more-characters/)

给定两个字符串，其中一个是模式(pattern)，另一个是搜索表达式。搜索表达式包含“#”。
该#的工作方式如下:

1.  #与一个或多个字符匹配。
2.  在找到模式匹配之前，#匹配所有字符。例如，如果 pat =“A # B”，并且文本是“ACCBB”，那么#将只与“CC”匹配，并且模式被认为没有找到。

**示例:**

```
Input  : str = "ABABABA" 
         pat = "A#B#A" 
Output : yes

Input  : str = "ABCCB" 
         pat = "A#B"
Output : yes

Input  : str = "ABCABCCE" 
         pat = "A#C#"
Output : yes

Input  : str = "ABCABCCE" 
         pat = "A#C"
Output : no
```

我们可以观察到，每当我们遇到“#”时，我们必须考虑尽可能多的字符，直到模式的下一个字符不等于给定字符串的当前字符。首先，我们检查模式的当前字符是否等于' #'-
a)如果不等于，则检查字符串和模式的当前字符是否相同，如果相同，则递增两个计数器，否则仅从这里返回 false。不需要进一步检查。
b)如果是，那么我们要找到一个字符在文本中的位置，与模式的下一个字符相匹配。

## C++

```
// C++ program for pattern matching
// where a single special character
// can match one more characters
#include<bits/stdc++.h>

using namespace std;

// Returns true if pat matches with text
int regexMatch(string text, string pat)
{
    int lenText = text.length();
    int letPat = pat.length();

    // i is used as an index in pattern
    // and j as an index in text
    int i = 0, j = 0;

    // Traverse through pattern
    while (i < letPat)
    {
        // If current character of
        // pattern is not '#'
        if (pat[i] != '#')
        {
            // If does not match with text
            if (pat[i] != text[j])
            return false;

        // If matches, increment i and j
        i++;
        j++;
        }

        // Current character is '#'
        else
        {
            // At least one character
            // must match with #
            j++;

            // Match characters with # until
            // a matching character is found.
            while (text[j] != pat[i + 1])
            j++;

            // Matching with # is over,
            // move ahead in pattern
            i++;
        }
    }

    return (j == lenText);
}

// Driver code
int main()
{
    string str = "ABABABA";
    string pat = "A#B#A";
    if (regexMatch(str, pat))
        cout << "yes";
    else
        cout << "no";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for pattern matching
// where a single special character
// can match one more characters

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
    // Returns true if pat
    // matches with text.
    public static boolean regexMatch
                          (String text, String pat)
    {
        int lenText = text.length();
        int lenPat = pat.length();

        char[] Text = text.toCharArray();
        char[] Pat = pat.toCharArray();

        // i is used as an index in pattern
        // and j as an index in text.
        int i = 0, j = 0;

        // Traverse through pattern
        while (i < lenPat)
        {
            // If current character of
            // pattern is not '#'
            if (Pat[i] != '#')
            {
                // If does not match with text.
                if (Pat[i] != Text[j])
                return false;

            // If matches, increment i and j
            i++;
            j++;
            }

            // Current character is '#'
            else
            {
                // At least one character
                // must match with #
                j++;

                // Match characters with # until
                // a matching character is found.
                while (Text[j] != Pat[i + 1])
                j++;

                // Matching with # is over,
                // move ahead in pattern
                i++;
            }
        }

        return (j == lenText);
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "ABABABA";
        String pat = "A#B#A";
        if (regexMatch(str, pat))
            System.out.println("yes");
        else
            System.out.println("no");
    }
}

// This code is contributed by Mr. Somesh Awasthi
```

## 蟒蛇 3

```
# Python3 program for pattern matching
# where a single special character
# can match one more characters

# Returns true if pat matches with
# text
def regexMatch(text, pat):

    lenText = len(text)
    letPat = len(pat)

    # i is used as an index in
    # pattern and j as an index
    # in text
    i = 0
    j = 0

    # Traverse through pattern
    while (i < letPat):

        # If current character of
        # pattern is not '#'
        if (pat[i] != '#'):

            # If does not match with
            # text
            if (pat[i] != text[j]):
                return False

            # If matches, increment
            # i and j
            i += 1
            j += 1

        # Current character is '#'
        else:

            # At least one character
            # must match with #
            j += 1

            # Match characters with # until
            # a matching character is found.
            while (text[j] != pat[i + 1]):
                j += 1

            # Matching with # is over,
            # move ahead in pattern
            i += 1

    return (j == lenText)

# Driver code
if __name__ == "__main__":

    st = "ABABABA"
    pat = "A#B#A"
    if (regexMatch(st, pat)):
        print("yes")
    else:
        print("no")

# This code is contributed by Chitranayal
```

## C#

```
// C# program for pattern matching
// where a single special character
// can match one more characters
using System;

class GFG
{
    // Returns true if pat
    // matches with text.
    public static bool regexMatch
                       (String text, String pat)
    {
        int lenText = text.Length;
        int lenPat = pat.Length;

        char []Text = text.ToCharArray();
        char []Pat = pat.ToCharArray();

        // i is used as an index in pattern
        // and j as an index in text.
        int i = 0, j = 0;

        // Traverse through pattern
        while (i < lenPat)
        {
            // If current character
            // of pattern is not '#'
            if (Pat[i] != '#')
            {
                // If does not match with text.
                if (Pat[i] != Text[j])
                return false;

            // If matches, increment i and j
            i++;
            j++;
            }

            // Current character is '#'
            else
            {
                // At least one character
                // must match with #
                j++;

                // Match characters with # until
                // a matching character is found.
                while (Text[j] != Pat[i + 1])
                j++;

                // Matching with # is over,
                // move ahead in pattern
                i++;
            }
        }

        return (j == lenText);
    }

    // Driver code
    public static void Main ()
    {
        String str = "ABABABA";
        String pat = "A#B#A";
        if (regexMatch(str, pat))
            Console.Write("yes");
        else
            Console.Write("no");
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for pattern matching
// where a single special character
// can match one more characters

// Returns true if pat
// matches with text
function regexMatch($text, $pat)
{
    $lenText = strlen($text);
    $letPat = strlen($pat);

    // i is used as an index in pattern
    // and j as an index in text
    $i = 0; $j = 0;

    // Traverse through pattern
    while ($i < $letPat)
    {

        // If current character of
        // pattern is not '#'
        if ($pat[$i] != '#')
        {

            // If does not match with text
            if ($pat[$i] != $text[$j])
            return false;

        // If matches, increment i and j
        $i++;
        $j++;
        }

        // Current character is '#'
        else
        {

            // At least one character
            // must match with #
            $j++;

            // Match characters with # until
            // a matching character is found.
            while ($text[$j] != $pat[$i + 1])
            $j++;

            // Matching with # is over,
            // move ahead in pattern
            $i++;
        }
    }

    return ($j == $lenText);
}

// Driver code
$str = "ABABABA";
$pat = "A#B#A";
if (regexMatch($str, $pat))
    echo "yes";
else
    echo "no";

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// Javascript program for pattern matching
// where a single special character
// can match one more characters

    // Returns true if pat
    // matches with text.
    function regexMatch(text,pat)
    {
        let lenText = text.length;
        let lenPat = pat.length;

        let Text = text.split("");
        let Pat = pat.split("");

        let i = 0, j = 0;
        // Traverse through pattern
        while (i < lenPat)
        {
            // If current character of
            // pattern is not '#'
            if (Pat[i] != '#')
            {
                // If does not match with text.
                if (Pat[i] != Text[j])
                return false;

            // If matches, increment i and j
            i++;
            j++;
            }

            // Current character is '#'
            else
            {
                // At least one character
                // must match with #
                j++;

                // Match characters with # until
                // a matching character is found.
                while (Text[j] != Pat[i + 1])
                j++;

                // Matching with # is over,
                // move ahead in pattern
                i++;
            }
        }

        return (j == lenText);
    }

    // Driver code
    let str = "ABABABA";
    let pat = "A#B#A";
    if (regexMatch(str, pat))
        document.write("yes");
    else
        document.write("no");

    // This code is contributed by rag2127
</script>
```

**输出:**

```
yes
```

本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。