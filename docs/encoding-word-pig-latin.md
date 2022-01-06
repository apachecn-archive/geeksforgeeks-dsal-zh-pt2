# 将单词编码成猪拉丁文

> 原文:[https://www.geeksforgeeks.org/encoding-word-pig-latin/](https://www.geeksforgeeks.org/encoding-word-pig-latin/)

设计一个程序，把一个单词作为输入，然后编码成 Pig 拉丁语。猪拉丁语是英语中的一个加密单词，它是通过以下更改生成的:
输入单词中出现的第一个元音连同它的剩余字母表一起放在新单词的开头。字母表出现在第一个元音变位之前，在新单词的末尾跟着“ay”。

**示例:**

```
Input: s = "paris"
Output: arispay

Input: s = "amazon"
Output: amazonay 
```

```
1) Find index of first vowel.
2) Create pig latin by appending following three.
.....a) Substring after starting with the first vowel
........till end.
.....b) Substring before first vowel.
.....c) "ay".
```

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to encode a word to a Pig Latin.
#include <bits/stdc++.h>
using namespace std;

bool isVowel(char c)
{
    return (c == 'A' || c == 'E' || c == 'I' ||
            c == 'O' || c == 'U' || c == 'a' ||
            c == 'e' || c == 'i' || c == 'o' ||
            c == 'u');
}

string pigLatin(string s)
{
    // the index of the first vowel is stored.
    int len = s.length();
    int index = -1;
    for (int i = 0; i < len; i++) {
        if (isVowel(s[i])) {
            index = i;
            break;
        }
    }

    // Pig Latin is possible only if vowels
    // is present
    if (index == -1)
        return "-1";

    // Take all characters after index (including
    // index). Append all characters which are before
    // index. Finally append "ay"
    return s.substr(index) + s.substr(0, index) + "ay";
}

// Driver code
int main()
{
    string str = pigLatin("graphic");
    if (str == "-1")
        cout << "No vowels found. Pig Latin not possible";
    else
        cout << str;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to encode a word to a Pig Latin.
class GFG {
static boolean isVowel(char c) {
    return (c == 'A' || c == 'E' || c == 'I' || c == 'O' || c == 'U' ||
            c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u');
}

static String pigLatin(String s) {

    // the index of the first vowel is stored.
    int len = s.length();
    int index = -1;
    for (int i = 0; i < len; i++)
    {
        if (isVowel(s.charAt(i))) {
        index = i;
        break;
    }
    }

    // Pig Latin is possible only if vowels
    // is present
    if (index == -1)
        return "-1";

    // Take all characters after index (including
    // index). Append all characters which are before
    // index. Finally append "ay"
    return s.substring(index) +
           s.substring(0, index) + "ay";
}

// Driver code
public static void main(String[] args) {
    String str = pigLatin("graphic");
    if (str == "-1")
        System.out.print("No vowels found." +
                         "Pig Latin not possible");

    else
        System.out.print(str);
}
}
// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to encode a word to a Pig Latin.

def isVowel(c):
    return (c == 'A' or c == 'E' or c == 'I' or
            c == 'O' or c == 'U' or c == 'a' or
            c == 'e' or c == 'i' or c == 'o' or
            c == 'u');

def pigLatin(s):

    # the index of the first vowel is stored.
    length = len(s);
    index = -1;
    for i in range(length):
        if (isVowel(s[i])):
            index = i;
            break;

    # Pig Latin is possible only if vowels
    # is present
    if (index == -1):
        return "-1";

    # Take all characters after index (including
    # index). Append all characters which are before
    # index. Finally append "ay"
    return s[index:] + s[0:index] + "ay";

str = pigLatin("graphic");
if (str == "-1"):
    print("No vowels found. Pig Latin not possible");
else:
    print(str);

# This code contributed by Rajput-Ji
```

## C#

```
// C# program to encode a word to a
// Pig Latin.
using System;

class GFG {

    static bool isVowel(char c)
    {
        return (c == 'A' || c == 'E' ||
                c == 'I' || c == 'O' ||
                c == 'U' || c == 'a' ||
                c == 'e' || c == 'i' ||
                c == 'o' || c == 'u');
    }

    static string pigLatin(string s)
    {

        // the index of the first
        // vowel is stored.
        int len = s.Length;
        int index = -1;
        for (int i = 0; i < len; i++)
        {
            if (isVowel(s[i]))
            {
                index = i;
                break;
            }
        }

        // Pig Latin is possible only
        // if vowels is present
        if (index == -1)
            return "-1";

        // Take all characters after
        // index (including index).
        // Append all characters which
        // are before index. Finally
        // append "ay"
        return s.Substring(index) +
               s.Substring(0, index)
                              + "ay";
    }

    // Driver code
    public static void Main()
    {
        string str = pigLatin("graphic");

        if (str == "-1")
            Console.WriteLine("No vowels"
                     + "found. Pig Latin"
                      + " not possible");
        else
            Console.WriteLine(str);
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// js program to encode a word to a
// Pig Latin.

function isVowel(c)
{
    return (c == 'A' || c == 'E' ||
            c == 'I' || c == 'O' ||
            c == 'U' || c == 'a' ||
            c == 'e' || c == 'i' ||
            c == 'o' || c == 'u');
}

function pigLatin(s)
{

    // the index of the first
    // vowel is stored.
    let len = s.length;
    let index = -1;
    for (let i = 0; i < len; i++)
    {
        if (isVowel(s[i]))
        {
            index = i;
            break;
        }
    }

    // Pig Latin is possible only
    // if vowels is present
    if (index == -1)
        return "-1";

    // Take all characters after
    // index (including index).
    // Append all characters which
    // are before index. Finally
    // append "ay"
    return s.substring(index) +
           s.substring(0, index)
                          + "ay";
}

// Driver code

str = pigLatin("graphic");

if (str == "-1")
    document.write("No vowels"
             + "found. Pig Latin"
              + " not possible");
else
    document.write(str);

</script>
```

**输出:**

```
aphicgray
```

本文由 [**德王**T3 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用](https://auth.geeksforgeeks.org/profile.php?user=dewangNautiyal)[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。