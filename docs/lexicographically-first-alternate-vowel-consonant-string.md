# 词典上第一个交替的元音和辅音串

> 原文:[https://www . geeksforgeeks . org/词典-第一-交替-元音-辅音-字符串/](https://www.geeksforgeeks.org/lexicographically-first-alternate-vowel-consonant-string/)

给定一根弦**弦**。问题是重新排列给定字符串的字符，使元音和辅音占据交替位置，这样形成的字符串在字典顺序上(按字母顺序)应该是最小的。如果字符串不能以所需的方式重新排列，请打印“没有这样的字符串”。
**例:**

```
Input : mango
Output : gamon
It could be arranged in other ways too, like
manog, etc., but gamon is lexicographically
smallest.

Input : aeroplane
Output : alanepero
```

**进场:**以下为步骤:

1.  将输入字符串的每个字符的频率存储在哈希表中。
2.  统计给定字符串中元音和辅音的数量。
3.  如果计数之间的差异大于 1，则返回“不可能”。
4.  否则，在哈希表的帮助下形成单独的元音和辅音串，该哈希表具有输入串的每个字符的频率。注意，在创建元音和辅音字符串时，各个字符串中的字符应该按字母顺序排列。
5.  如果元音多于辅音，先打印第一个元音，然后交替打印辅音和元音串中的剩余字符。
6.  如果辅音多于元音，先打印第一个辅音，然后交替打印元音和辅音串中的剩余字符。
7.  如果计数相同，比较第一个元音和第一个辅音，先打印较小的一个，然后继续交替打印。

## C++

```
// C++ implementation of lexicographically first
// alternate vowel and consonant string
#include <bits/stdc++.h>
using namespace std;

#define SIZE 26

// 'ch' is vowel or not
bool isVowel(char ch)
{
    if (ch == 'a' || ch == 'e' || ch == 'i' ||
                       ch == 'o' || ch == 'u')
        return true;
    return false;
}

// create alternate vowel and consonant string
// str1[0...l1-1] and str2[start...l2-1]
string createAltStr(string str1, string str2,
                    int start, int l)
{
    string finalStr = "";

    // first adding character of vowel/consonant
    // then adding character of consonant/vowel
    for (int i = 0, j = start; j < l; i++, j++)
        finalStr = (finalStr + str1.at(i)) +
                                 str2.at(j);
    return finalStr;
}

// function to find the required lexicographically
// first alternate vowel and consonant string
string findAltStr(string str)
{
    // hash table to store frequencies
    // of each character in 'str'
    int char_freq[SIZE];

    // initialize all elements of char_freq[]
    // to 0
    memset(char_freq, 0, sizeof(char_freq));

    int nv = 0, nc = 0;
    string vstr = "", cstr = "";
    int l = str.size();

    for (int i = 0; i < l; i++) {
        char ch = str.at(i);

        // count vowels
        if (isVowel(ch))
            nv++;

        // count consonants
        else
            nc++;

        // update frequency of 'ch' in
        // char_freq[]
        char_freq[ch - 97]++;
    }

    // no such string can be formed
    if (abs(nv - nc) >= 2)
        return "no such string";

    // form the vowel string 'vstr' and
    // consonant string 'cstr' which contains
    // characters in lexicographical order
    for (int i = 0; i < SIZE; i++) {
        char ch = (char)(i + 97);
        for (int j = 1; j <= char_freq[i]; j++) {
            if (isVowel(ch))
                vstr += ch;
            else
                cstr += ch;
        }
    }

    // remove first character of vowel string
    // then create alternate string with
    // cstr[0...nc-1] and vstr[1...nv-1]
    if (nv > nc)
        return (vstr.at(0) + createAltStr(cstr,
                                 vstr, 1, nv));

    // remove first character of consonant string
    // then create alternate string with
    // vstr[0...nv-1] and cstr[1...nc-1]
    if (nc > nv)
        return (cstr.at(0) + createAltStr(vstr,
                                  cstr, 1, nc));

    // if both vowel and consonant
    // strings are of equal length
    // start creating string with consonant
    if (cstr.at(0) < vstr.at(0))
        return createAltStr(cstr, vstr, 0, nv);

    // start creating string with vowel
    return createAltStr(vstr, cstr, 0, nc);
}

// Driver program to test above
int main()
{
    string str = "aeroplane";
    cout << findAltStr(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of lexicographically first
// alternate vowel and consonant String
import java.util.Arrays;
class GFG {

    static final int SIZE = 26;

    // 'ch' is vowel or not
    static boolean isVowel(char ch)
    {
        if (ch == 'a' || ch == 'e' || ch == 'i'
                || ch == 'o' || ch == 'u')
        {
            return true;
        }
        return false;
    }

    // create alternate vowel and consonant String
    // str1[0...l1-1] and str2[start...l2-1]
    static String createAltStr(String str1, String str2,
            int start, int l)
    {
        String finalStr = "";

        // first adding character of vowel/consonant
        // then adding character of consonant/vowel
        for (int i = 0, j = start; j < l; i++, j++)
        {
            finalStr = (finalStr + str1.charAt(i))
                    + str2.charAt(j);
        }
        return finalStr;
    }

    // function to find the required
    // lexicographically  first alternate
    // vowel and consonant String
    static String findAltStr(String str)
    {

        // hash table to store frequencies
        // of each character in 'str'
        int char_freq[] = new int[SIZE];

        // initialize all elements of char_freq[]
        // to 0
        Arrays.fill(char_freq, 0);

        int nv = 0, nc = 0;
        String vstr = "", cstr = "";
        int l = str.length();

        for (int i = 0; i < l; i++)
        {
            char ch = str.charAt(i);

            // count vowels
            if (isVowel(ch))
            {
                nv++;
            }

            // count consonants
            else
            {
                nc++;
            }

            // update frequency of 'ch' in
            // char_freq[]
            char_freq[ch - 97]++;
        }

        // no such String can be formed
        if (Math.abs(nv - nc) >= 2)
        {
            return "no such String";
        }

        // form the vowel String 'vstr' and
        // consonant String 'cstr' which contains
        // characters in lexicographical order
        for (int i = 0; i < SIZE; i++) {
            char ch = (char) (i + 97);
            for (int j = 1; j <= char_freq[i]; j++)
            {
                if (isVowel(ch))
                {
                    vstr += ch;
                }
                else
                {
                    cstr += ch;
                }
            }
        }

        // remove first character of vowel String
        // then create alternate String with
        // cstr[0...nc-1] and vstr[1...nv-1]
        if (nv > nc) {
            return (vstr.charAt(0) + createAltStr(cstr,
                    vstr, 1, nv));
        }

        // remove first character of consonant String
        // then create alternate String with
        // vstr[0...nv-1] and cstr[1...nc-1]
        if (nc > nv)
        {
            return (cstr.charAt(0) + createAltStr(vstr,
                    cstr, 1, nc));
        }

        // if both vowel and consonant
        // strings are of equal length
        // start creating String with consonant
        if (cstr.charAt(0) < vstr.charAt(0))
        {
            return createAltStr(cstr, vstr, 0, nv);
        }

        // start creating String with vowel
        return createAltStr(vstr, cstr, 0, nc);
    }

    // Driver code
    public static void main(String[] args) {
        String str = "aeroplane";
        System.out.println(findAltStr(str));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of lexicographically first
# alternate vowel and consonant string
SIZE = 26

# 'ch' is vowel or not
def isVowel(ch):
    if (ch == 'a' or ch == 'e' or
        ch == 'i' or ch == 'o' or
        ch == 'u'):
        return True
    return False

# create alternate vowel and consonant string
# str1[0...l1-1] and str2[start...l2-1]
def createAltStr(str1, str2, start, l):
    finalStr = ""
    i = 0
    j = start

    # first adding character of vowel/consonant
    # then adding character of consonant/vowel
    while j < l:
        finalStr += str1[i] + str2[j]
        i += 1
        j += 1
    return finalStr

# function to find the required lexicographically
# first alternate vowel and consonant string
def findAltStr(string):

    # hash table to store frequencies
    # of each character in 'str'
    char_freq = [0] * SIZE # initialize all elements
                           # of char_freq[] to 0
    nv = 0
    nc = 0
    vstr = ""
    cstr = ""
    l = len(string)

    for i in range(l):
        ch = string[i]

        # count vowels
        if isVowel(ch):
            nv += 1

        # count consonants
        else:
            nc += 1

        # update frequency of 'ch' in
        # char_freq[]
        char_freq[ord(ch) - 97] += 1

    # no such string can be formed
    if abs(nv - nc) >= 2:
        return "no such string"

    # form the vowel string 'vstr' and
    # consonant string 'cstr' which contains
    # characters in lexicographical order
    for i in range(SIZE):
        ch = chr(i + 97)
        for j in range(1, char_freq[i] + 1):
            if isVowel(ch):
                vstr += ch
            else:
                cstr += ch

    # remove first character of vowel string
    # then create alternate string with
    # cstr[0...nc-1] and vstr[1...nv-1]
    if nv > nc:
        return vstr[0] + createAltStr(cstr,
                                      vstr, 1, nv)

    # remove first character of consonant string
    # then create alternate string with
    # vstr[0...nv-1] and cstr[1...nc-1]
    if nc > nv:
        return cstr[0] + createAltStr(vstr,
                                      cstr, 1, nc)

    # if both vowel and consonant
    # strings are of equal length
    # start creating string with consonant
    if cstr[0] < vstr[0]:
        return createAltStr(cstr, vstr, 0, nv)

    # start creating string with vowel
    return createAltStr(vstr, cstr, 0, nc)

# Driver Code
if __name__ == "__main__":
    string = "aeroplane"
    print(findAltStr(string))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of lexicographically first
// alternate vowel and consonant String
using System;

class GFG
{
    static readonly int SIZE = 26;

    // 'ch' is vowel or not
    static bool isVowel(char ch)
    {
        if (ch == 'a' || ch == 'e' || ch == 'i'
                || ch == 'o' || ch == 'u')
        {
            return true;
        }
        return false;
    }

    // create alternate vowel and consonant String
    // str1[0...l1-1] and str2[start...l2-1]
    static String createAltStr(String str1, String str2,
            int start, int l)
    {
        String finalStr = "";

        // first adding character of vowel/consonant
        // then adding character of consonant/vowel
        for (int i = 0, j = start; j < l; i++, j++)
        {
            finalStr = (finalStr + str1[i]) +
                                    str2[j];
        }
        return finalStr;
    }

    // function to find the required
    // lexicographically first alternate
    // vowel and consonant String
    static String findAltStr(String str)
    {

        // hash table to store frequencies
        // of each character in 'str'
        int []char_freq = new int[SIZE];

        int nv = 0, nc = 0;
        String vstr = "", cstr = "";
        int l = str.Length;

        for (int i = 0; i < l; i++)
        {
            char ch = str[i];

            // count vowels
            if (isVowel(ch))
            {
                nv++;
            }

            // count consonants
            else
            {
                nc++;
            }

            // update frequency of 'ch' in
            // char_freq[]
            char_freq[ch - 97]++;
        }

        // no such String can be formed
        if (Math.Abs(nv - nc) >= 2)
        {
            return "no such String";
        }

        // form the vowel String 'vstr' and
        // consonant String 'cstr' which contains
        // characters in lexicographical order
        for (int i = 0; i < SIZE; i++)
        {
            char ch = (char) (i + 97);
            for (int j = 1; j <= char_freq[i]; j++)
            {
                if (isVowel(ch))
                {
                    vstr += ch;
                }
                else
                {
                    cstr += ch;
                }
            }
        }

        // remove first character of vowel String
        // then create alternate String with
        // cstr[0...nc-1] and vstr[1...nv-1]
        if (nv > nc)
        {
            return (vstr[0] + createAltStr(cstr,
                    vstr, 1, nv));
        }

        // remove first character of consonant String
        // then create alternate String with
        // vstr[0...nv-1] and cstr[1...nc-1]
        if (nc > nv)
        {
            return (cstr[0] + createAltStr(vstr,
                    cstr, 1, nc));
        }

        // if both vowel and consonant
        // strings are of equal length
        // start creating String with consonant
        if (cstr[0] < vstr[0])
        {
            return createAltStr(cstr, vstr, 0, nv);
        }

        // start creating String with vowel
        return createAltStr(vstr, cstr, 0, nc);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "aeroplane";
        Console.WriteLine(findAltStr(str));
    }
}

/* This code has been contributed
by PrinciRaj1992*/
```

## java 描述语言

```
<script>

// JavaScript implementation of lexicographically first
// alternate vowel and consonant String

let SIZE = 26;

// 'ch' is vowel or not
function isVowel(ch)
{
    if (ch == 'a' || ch == 'e' || ch == 'i'
                || ch == 'o' || ch == 'u')
        {
            return true;
        }
        return false;
}

// create alternate vowel and consonant String
    // str1[0...l1-1] and str2[start...l2-1]
function createAltStr(str1,str2,start,l)
{
    let finalStr = "";

        // first adding character of vowel/consonant
        // then adding character of consonant/vowel
        for (let i = 0, j = start; j < l; i++, j++)
        {
            finalStr = (finalStr + str1[i])
                    + str2[j];
        }
        return finalStr;
}

// function to find the required
    // lexicographically  first alternate
    // vowel and consonant String
function findAltStr(str)
{
    // hash table to store frequencies
        // of each character in 'str'
        let char_freq = new Array(SIZE);

        // initialize all elements of char_freq[]
        // to 0
        for(let i=0;i<SIZE;i++)
            char_freq[i]=0;

        let nv = 0, nc = 0;
        let vstr = "", cstr = "";
        let l = str.length;

        for (let i = 0; i < l; i++)
        {
            let ch = str[i];

            // count vowels
            if (isVowel(ch))
            {
                nv++;
            }

            // count consonants
            else
            {
                nc++;
            }

            // update frequency of 'ch' in
            // char_freq[]
            char_freq[ch.charCodeAt(0) - 97]++;
        }

        // no such String can be formed
        if (Math.abs(nv - nc) >= 2)
        {
            return "no such String";
        }

        // form the vowel String 'vstr' and
        // consonant String 'cstr' which contains
        // characters in lexicographical order
        for (let i = 0; i < SIZE; i++) {
            let ch = String.fromCharCode (i + 97);
            for (let j = 1; j <= char_freq[i]; j++)
            {
                if (isVowel(ch))
                {
                    vstr += ch;
                }
                else
                {
                    cstr += ch;
                }
            }
        }

        // remove first character of vowel String
        // then create alternate String with
        // cstr[0...nc-1] and vstr[1...nv-1]
        if (nv > nc) {
            return (vstr[0] + createAltStr(cstr,
                    vstr, 1, nv));
        }

        // remove first character of consonant String
        // then create alternate String with
        // vstr[0...nv-1] and cstr[1...nc-1]
        if (nc > nv)
        {
            return (cstr[0] + createAltStr(vstr,
                    cstr, 1, nc));
        }

        // if both vowel and consonant
        // strings are of equal length
        // start creating String with consonant
        if (cstr[0] < vstr[0])
        {
            return createAltStr(cstr, vstr, 0, nv);
        }

        // start creating String with vowel
        return createAltStr(vstr, cstr, 0, nc);
}

// Driver code
let str = "aeroplane";
document.write(findAltStr(str));

// This code is contributed by rag2127

</script>
```

**输出:**

```
alanepero
```

**时间复杂度:** O(n)，其中 **n** 为弦的长度。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。