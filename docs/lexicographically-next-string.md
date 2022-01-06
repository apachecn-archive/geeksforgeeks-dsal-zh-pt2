# 字典顺序下一个字符串

> 原文:[https://www . geeksforgeeks . org/词典-下一个字符串/](https://www.geeksforgeeks.org/lexicographically-next-string/)

给定一个字符串，按字典顺序查找下一个字符串。
**例:**

```
Input : geeks
Output : geekt
The last character 's' is changed to 't'.

Input : raavz
Output : raawz
Since we can't increase last character, 
we increment previous character.

Input :  zzz
Output : zzza
```

如果字符串为空，我们返回“a”。如果字符串包含所有字符作为' z '，我们在末尾追加' a '。否则，我们从末尾找到不是 z 的第一个字符，并将其递增。

## C++

```
// C++ program to find lexicographically next
// string
#include <bits/stdc++.h>
using namespace std;

string nextWord(string s)
{
    // If string is empty.
    if (s == "")
        return "a";

    // Find first character from right
    // which is not z.

    int i = s.length() - 1;
    while (s[i] == 'z' && i >= 0)
        i--;

    // If all characters are 'z', append
    // an 'a' at the end.
    if (i == -1)
        s = s + 'a';

    // If there are some non-z characters
    else
        s[i]++;

    return s;
}

// Driver code
int main()
{
    string str = "samez";
    cout << nextWord(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// lexicographically next string
import java.util.*;

class GFG
{
public static String nextWord(String str)
{

    // if string is empty
    if (str == "")
    return "a";

    // Find first character from
    // right which is not z.
    int i = str.length() - 1;
    while (str.charAt(i) == 'z' && i >= 0)
        i--;

    // If all characters are 'z',
    // append an 'a' at the end.
    if (i == -1)
        str = str + 'a';

// If there are some
// non-z characters
else
    str = str.substring(0, i) +
         (char)((int)(str.charAt(i)) + 1) +
                      str.substring(i + 1);
return str;
}

// Driver Code
public static void main (String[] args)
{
    String str = "samez";
    System.out.print(nextWord(str));
}
}

// This code is contributed
// by Kirti_Mangal
```

## 蟒蛇 3

```
# Python 3 program to find lexicographically
# next string

def nextWord(s):

    # If string is empty.
    if (s == " "):
        return "a"

    # Find first character from right
    # which is not z.
    i = len(s) - 1
    while (s[i] == 'z' and i >= 0):
        i -= 1

    # If all characters are 'z', append
    # an 'a' at the end.
    if (i == -1):
        s = s + 'a'

    # If there are some non-z characters
    else:
        s = s.replace(s[i], chr(ord(s[i]) + 1), 1)

    return s

# Driver code
if __name__ == '__main__':
    str = "samez"
    print(nextWord(str))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find
// lexicographically next string
using System;

class GFG
{
public static string nextWord(string str)
{

    // if string is empty
    if (str == "")
    {
    return "a";
    }

    // Find first character from
    // right which is not z.
    int i = str.Length - 1;
    while (str[i] == 'z' && i >= 0)
    {
        i--;
    }

    // If all characters are 'z',
    // append an 'a' at the end.
    if (i == -1)
    {
        str = str + 'a';
    }

    // If there are some
    // non-z characters
    else
    {
        str = str.Substring(0, i) +
             (char)((int)(str[i]) + 1) +
              str.Substring(i + 1);
    }
    return str;
}

// Driver Code
public static void Main(string[] args)
{
    string str = "samez";
    Console.Write(nextWord(str));
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to find lexicographically next
// string

function nextWord(s)
{
    // If string is empty.
    if (s == "")
        return "a";

    // Find first character from right
    // which is not z.

    var i = s.length - 1;
    while (s[i] == 'z' && i >= 0)
        i--;

    // If all characters are 'z', append
    // an 'a' at the end.
    if (i == -1)
        s = s + 'a';

    // If there are some non-z characters
    else
        s[i] = String.fromCharCode(s[i].charCodeAt(0)+1);

    return s.join('');
}

// Driver code
var str = "samez".split('');
document.write( nextWord(str));

// This code is contributed by noob2000.
</script>
```

**输出:**

```
samfz
```

本文由 [**帕万·阿西普**](https://auth.geeksforgeeks.org/profile.php?user=Pawan Asipu) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。