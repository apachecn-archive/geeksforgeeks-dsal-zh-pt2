# 查找通过从字符串中移除或重排字符形成的最长回文

> 原文:[https://www . geesforgeks . org/find-最长回文-通过从字符串中移除或洗牌字符形成/](https://www.geeksforgeeks.org/find-longest-palindrome-formed-by-removing-or-shuffling-chars-from-string/)

给定一个字符串，找到最长的回文，可以通过从字符串中移除或重排字符来构建。如果有多个长度最长的回文字符串，只返回一个回文。
示例:

```
Input:  abc
Output: a OR b OR c

Input:  aabbcc
Output: abccba OR baccab OR cbaabc OR
any other palindromic string of length 6.

Input:  abbaccd
Output: abcdcba OR ...

Input:  aba
Output: aba
```

我们可以把任何回文串分成三部分——开头、中间和结尾。对于奇数长度的回文字符串，比如 2n + 1，“beg”由字符串的前 n 个字符组成，“mid”仅由 1 个字符组成，即第(n + 1)个字符，“end”由回文字符串的最后 n 个字符组成。对于偶数长度 2n 的回文字符串，“mid”将始终为空。需要注意的是，为了让字符串成为回文，“end”将与“beg”相反。
想法是在我们的解决方案中使用上面的观察。由于允许对字符进行洗牌，字符的顺序在输入字符串中并不重要。我们首先得到输入字符串中每个字符的频率。那么在输入字符串中出现偶数(比如 2n)的所有字符都将是输出字符串的一部分，因为我们可以很容易地将 n 个字符放在“beg”字符串中，将其他 n 个字符放在“end”字符串中(通过保持回文顺序)。对于出现奇数(比如 2n + 1)的字符，我们用所有这些字符中的一个来填充“中间”。剩余的 2n 个字符被分成两半，并在开头和结尾相加。
以下是上述想法的实现–

## C++

```
// C++ program to find the longest palindrome by removing
// or shuffling characters from the given string
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest palindrome by removing
// or shuffling characters from the given string
string findLongestPalindrome(string str)
{
    // to stores freq of characters in a string
    int count[256] = { 0 };

    // find freq of characters in the input string
    for (int i = 0; i < str.size(); i++)
        count[str[i]]++;

    // Any palindromic string consists of three parts
    // beg + mid + end
    string beg = "", mid = "", end = "";

    // solution assumes only lowercase characters are
    // present in string. We can easily extend this
    // to consider any set of characters
    for (char ch = 'a'; ch <= 'z'; ch++)
    {
        // if the current character freq is odd
        if (count[ch] & 1)
        {
            // mid will contain only 1 character. It
            // will be overridden with next character
            // with odd freq
            mid = ch;

            // decrement the character freq to make
            // it even and consider current character
            // again
            count[ch--]--;
        }

        // if the current character freq is even
        else
        {
            // If count is n(an even number), push
            // n/2 characters to beg string and rest
            // n/2 characters will form part of end
            // string
            for (int i = 0; i < count[ch]/2 ; i++)
                beg.push_back(ch);
        }
    }

    // end will be reverse of beg
    end = beg;
    reverse(end.begin(), end.end());

    // return palindrome string
    return beg + mid + end;
}

// Driver code
int main()
{
    string str = "abbaccd";

    cout << findLongestPalindrome(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest palindrome by removing
// or shuffling characters from the given string

class GFG {

// Function to find the longest palindrome by removing
// or shuffling characters from the given string
    static String findLongestPalindrome(String str) {
        // to stores freq of characters in a string
        int count[] = new int[256];

        // find freq of characters in the input string
        for (int i = 0; i < str.length(); i++) {
            count[str.charAt(i)]++;
        }

        // Any palindromic string consists of three parts
        // beg + mid + end
        String beg = "", mid = "", end = "";

        // solution assumes only lowercase characters are
        // present in string. We can easily extend this
        // to consider any set of characters
        for (char ch = 'a'; ch <= 'z'; ch++) {
            // if the current character freq is odd
            if (count[ch] % 2 == 1) {
                // mid will contain only 1 character. It
                // will be overridden with next character
                // with odd freq
                mid = String.valueOf(ch);

                // decrement the character freq to make
                // it even and consider current character
                // again
                count[ch--]--;
            } // if the current character freq is even
            else {
                // If count is n(an even number), push
                // n/2 characters to beg string and rest
                // n/2 characters will form part of end
                // string
                for (int i = 0; i < count[ch] / 2; i++) {
                    beg += ch;
                }
            }
        }

        // end will be reverse of beg
        end = beg;
        end = reverse(end);

        // return palindrome string
        return beg + mid + end;
    }

    static String reverse(String str) {
        // convert String to character array
        // by using toCharArray
        String ans = "";
        char[] try1 = str.toCharArray();

        for (int i = try1.length - 1; i >= 0; i--) {
            ans += try1[i];
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args) {
        String str = "abbaccd";
        System.out.println(findLongestPalindrome(str));
    }
}
// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find the longest palindrome by removing
# or shuffling characters from the given string

# Function to find the longest palindrome by removing
# or shuffling characters from the given string
def findLongestPalindrome(strr):

    # to stores freq of characters in a string
    count = [0]*256

    # find freq of characters in the input string
    for i in range(len(strr)):
        count[ord(strr[i])] += 1

    # Any palindromic consists of three parts
    # beg + mid + end
    beg = ""
    mid = ""
    end = ""

    # solution assumes only lowercase characters are
    # present in string. We can easily extend this
    # to consider any set of characters
    ch = ord('a')
    while ch <= ord('z'):

        # if the current character freq is odd
        if (count[ch] & 1):

            # mid will contain only 1 character. It
            # will be overridden with next character
            # with odd freq
            mid = ch

            # decrement the character freq to make
            # it even and consider current character
            # again
            count[ch] -= 1
            ch -= 1

        # if the current character freq is even
        else:

            # If count is n(an even number), push
            # n/2 characters to beg and rest
            # n/2 characters will form part of end
            # string
            for i in range(count[ch]//2):
                beg += chr(ch)
        ch += 1

    # end will be reverse of beg
    end = beg

    end = end[::-1]

    # return palindrome string
    return beg + chr(mid) + end

# Driver code
strr = "abbaccd"

print(findLongestPalindrome(strr))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the longest
// palindrome by removing or
// shuffling characters from
// the given string
using System;

class GFG
{

    // Function to find the longest
    // palindrome by removing or
    // shuffling characters from
    // the given string
    static String findLongestPalindrome(String str)
    {
        // to stores freq of characters in a string
        int []count = new int[256];

        // find freq of characters
        // in the input string
        for (int i = 0; i < str.Length; i++)
        {
            count[str[i]]++;
        }

        // Any palindromic string consists of
        // three parts beg + mid + end
        String beg = "", mid = "", end = "";

        // solution assumes only lowercase
        // characters are present in string.
        // We can easily extend this to
        // consider any set of characters
        for (char ch = 'a'; ch <= 'z'; ch++)

        {
            // if the current character freq is odd
            if (count[ch] % 2 == 1) 
            {

                // mid will contain only 1 character.
                // It will be overridden with next
                // character with odd freq
                mid = String.Join("",ch);

                // decrement the character freq to make
                // it even and consider current
                // character again
                count[ch--]--;
            }

            // if the current character freq is even
            else
            {

                // If count is n(an even number), push
                // n/2 characters to beg string and rest
                // n/2 characters will form part of end
                // string
                for (int i = 0; i < count[ch] / 2; i++)
                {
                    beg += ch;
                }
            }
        }

        // end will be reverse of beg
        end = beg;
        end = reverse(end);

        // return palindrome string
        return beg + mid + end;
    }

    static String reverse(String str)
    {
        // convert String to character array
        // by using toCharArray
        String ans = "";
        char[] try1 = str.ToCharArray();

        for (int i = try1.Length - 1; i >= 0; i--)
        {
            ans += try1[i];
        }
        return ans;
    }

    // Driver code
    public static void Main()
    {
        String str = "abbaccd";
        Console.WriteLine(findLongestPalindrome(str));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the
// longest palindrome by removing
// or shuffling characters from
// the given string

// Function to find the longest
// palindrome by removing
// or shuffling characters from
// the given string
    function findLongestPalindrome(str)
    {
        // to stores freq of characters
        // in a string
        let count = new Array(256);
        for(let i=0;i<256;i++)
        {
            count[i]=0;
        }

        // find freq of characters in
        // the input string
        for (let i = 0; i < str.length; i++) {
            count[str[i].charCodeAt(0)]++;
        }

        // Any palindromic string consists
        // of three parts
        // beg + mid + end
        let beg = "", mid = "", end = "";

        // solution assumes only
        // lowercase characters are
        // present in string.
        // We can easily extend this
        // to consider any set of characters
        for (let ch = 'a'.charCodeAt(0);
        ch <= 'z'.charCodeAt(0); ch++) {
            // if the current character freq is odd
            if (count[ch] % 2 == 1) {
                // mid will contain only 1 character. It
                // will be overridden with next character
                // with odd freq
                mid = String.fromCharCode(ch);

                // decrement the character freq to make
                // it even and consider current character
                // again
                count[ch--]--;
            } // if the current character freq is even
            else {
                // If count is n(an even number), push
                // n/2 characters to beg string and rest
                // n/2 characters will form part of end
                // string
                for (let i = 0; i < count[ch] / 2; i++)
                {
                    beg += String.fromCharCode(ch);
                }
            }
        }

        // end will be reverse of beg
        end = beg;
        end = reverse(end);

        // return palindrome string
        return beg + mid + end;
    }

    function reverse(str)
    {
        // convert String to character array
        // by using toCharArray
        let ans = "";
        let try1 = str.split("");

        for (let i = try1.length - 1; i >= 0; i--) {
            ans += try1[i];
        }
        return ans;
    }

    // Driver code
    let str = "abbaccd";
    document.write(findLongestPalindrome(str));

    // This code is contributed by unknown2108

</script>
```

**输出:**

```
abcdcba
```

**上述解的时间复杂度**为 O(n)，其中 n 为字符串的长度。因为字母表中的字符数是恒定的，所以它们无助于渐近分析。
**程序使用的辅助空格**为 M，其中 M 为 ASCII 字符数。
本文由 **Aditya Goel** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。