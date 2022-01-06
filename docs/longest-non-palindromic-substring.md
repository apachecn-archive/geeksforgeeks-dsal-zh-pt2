# 最长非回文子串

> 原文:[https://www . geesforgeks . org/long-非回文-substring/](https://www.geeksforgeeks.org/longest-non-palindromic-substring/)

给定一个大小为 n 的字符串，任务是找出最大的非回文子串的长度。
**例:**

```
Input : abba 
Output : 3
Here maximum length non-palindromic substring is
'abb' which is of length '3'. There could be other
non-palindromic sub-strings also of length three 
like 'bba' in this case.

Input : a
Output : 0
```

一个**简单的解决方案**是考虑每个子串[检查是否是回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。最后返回最长非回文子串的长度。
一个**高效的解决方案**是基于下面的方法。

```
Check for the case where all characters of
the string are same or not.
    If yes, then answer will be '0'.
Else check whether the given string of size 
'n' is palindrome or not. 
    If yes, then answer will be 'n-1'
Else answer will be 'n' 
```

## C++

```
// C++ implementation to find maximum length
// substring which is not palindrome
#include <bits/stdc++.h>
using namespace std;

// utility function to check whether
// a string is palindrome or not
bool isPalindrome(string str)
{
    // Check for palindrome.
    int n = str.size();
    for (int i=0; i < n/2; i++)
        if (str.at(i) != str.at(n-i-1))
            return false;

    // palindrome string
    return true;
}

// function to find maximum length
// substring which is not palindrome
int maxLengthNonPalinSubstring(string str)
{
    int n = str.size();
    char ch = str.at(0);

    // to check whether all characters
    // of the string are same or not
    int i = 1;
    for (i=1; i<n; i++)
        if (str.at(i) != ch)
            break;

    // All characters are same, we can't
    // make a non-palindromic string.
    if (i == n)
        return 0;

    // If string is palindrome, we can make
    // it non-palindrome by removing any
    // corner character
    if (isPalindrome(str))
        return n-1;

    // Complete string is not a palindrome.
    return n;
}

// Driver program to test above
int main()
{
    string str = "abba";
    cout << "Maximum length = "
         << maxLengthNonPalinSubstring(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation to find maximum length
//substring which is not palindrome
public class GFG
{
    // utility function to check whether
    // a string is palindrome or not
    static Boolean isPalindrome(String str)
    {
        int n = str.length();

        // Check for palindrome.
        for (int i = 0; i < n/2; i++)
            if (str.charAt(i) != str.charAt(n-i-1))
                return false;

        // palindrome string
        return true;
    }

    // function to find maximum length
    // substring which is not palindrome
    static int maxLengthNonPalinSubstring(String str)
    {
        int n = str.length();
        char ch = str.charAt(0);

        // to check whether all characters
        // of the string are same or not
        int i = 1;
        for (i = 1; i < n; i++)
            if(str.charAt(i) != ch)
                break;

        // All characters are same, we can't
        // make a non-palindromic string.
        if (i == n)
            return 0;

        // If string is palindrome, we can make
        // it non-palindrome by removing any
        // corner character
        if (isPalindrome(str))
            return n-1;

        // Complete string is not a palindrome.
        return n;
    }

    // Driver Program to test above function
    public static void main(String args[])
    {
        String str = "abba";
        System.out.println("Maximum Length = "
             + maxLengthNonPalinSubstring(str));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 implementation to find maximum
# length substring which is not palindrome

# utility function to check whether
# a string is palindrome or not
def isPalindrome(str):

    # Check for palindrome.
    n = len(str)
    for i in range(n // 2):
        if (str[i] != str[n - i - 1]):
            return False

    # palindrome string
    return True

# function to find maximum length
# substring which is not palindrome
def maxLengthNonPalinSubstring(str):
    n = len(str)
    ch = str[0]

    # to check whether all characters
    # of the string are same or not
    i = 1
    for i in range(1, n):
        if (str[i] != ch):
            break

    # All characters are same, we can't
    # make a non-palindromic string.
    if (i == n):
        return 0

    # If string is palindrome, we can make
    # it non-palindrome by removing any
    # corner character
    if (isPalindrome(str)):
        return n - 1

    # Complete string is not a palindrome.
    return n

# Driver Code
if __name__ == "__main__":

    str = "abba"
    print("Maximum length =",
           maxLengthNonPalinSubstring(str))

# This code is contributed by ita_c
```

## C#

```
// C# implementation to find maximum length
// substring which is not palindrome
using System;

class GFG {

    // utility function to check whether
    // a string is palindrome or not
    static bool isPalindrome(String str)
    {
        int n = str.Length;

        // Check for palindrome.
        for (int i = 0; i < n / 2; i++)
            if (str[i] != str[n - i - 1])
                return false;

        // palindrome string
        return true;
    }

    // function to find maximum length
    // substring which is not palindrome
    static int maxLengthNonPalinSubstring(String str)
    {
        int n = str.Length;
        char ch = str[0];

        // to check whether all characters
        // of the string are same or not
        int i = 1;
        for (i = 1; i < n; i++)
            if(str[i] != ch)
                break;

        // All characters are same, we can't
        // make a non-palindromic string.
        if (i == n)
            return 0;

        // If string is palindrome, we can
        // make it non-palindrome by removing
        // any corner character
        if (isPalindrome(str))
            return n-1;

        // Complete string is not a palindrome.
        return n;
    }

    // Driver code
    public static void Main()
    {
        String str = "abba";
        Console.Write("Maximum Length = "
                      + maxLengthNonPalinSubstring(str));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find maximum length
// substring which is not palindrome

// utility function to check whether
// a string is palindrome or not
function isPalindrome($str)
{
    $n = strlen($str);

    // Check for palindrome.
    for ($i = 0; $i < $n / 2; $i++)
        if ($str[$i] != $str[$n - $i - 1])
            return false;

    // palindrome string
    return true;
}

// function to find maximum length
// substring which is not palindrome
function maxLengthNonPalinSubstring($str)
{
    $n = strlen($str);
    $ch = $str[0];

    // to check whether all characters
    // of the string are same or not
    $i = 1;
    for ($i = 1; $i < $n; $i++)
        if($str[$i] != $ch)
            break;

    // All characters are same, we can't
    // make a non-palindromic string.
    if ($i == $n)
        return 0;

    // If string is palindrome, we can
    // make it non-palindrome by removing
    // any corner character
    if (isPalindrome($str))
        return ($n - 1);

    // Complete string is not a palindrome.
    return $n;
}

// Driver code
$str = "abba";
echo "Maximum Length = ",
      maxLengthNonPalinSubstring($str);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

//Javascript implementation to find maximum length
//substring which is not palindrome

    // utility function to check whether
    // a string is palindrome or not
    function isPalindrome(str)
    {
        let n=str.length;
        // Check for palindrome.
        for (let i = 0; i < n/2; i++)
        {
            if(str[i] != str[n-i-1])
                return false;
        }
        // palindrome string
        return true;
    }
    // function to find maximum length
    // substring which is not palindrome
    function maxLengthNonPalinSubstring(str)
    {
        let n = str.length;
        let ch=str[0];
        // to check whether all characters
        // of the string are same or not
        let i = 1;
        for (i = 1; i < n; i++)
        {
            if(str[i] != ch)
            {
                break;
            }
        }
        // All characters are same, we can't
        // make a non-palindromic string.
        if (i == n)
            return 0;

        // If string is palindrome, we can make
        // it non-palindrome by removing any
        // corner character
        if (isPalindrome(str))
            return n-1;

        // Complete string is not a palindrome.
        return n;
    }
    // Driver Program to test above function
    let str = "abba";
    document.write("Maximum Length = " + maxLengthNonPalinSubstring(str));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Maximum length = 3
```

**时间复杂度:** O(n)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。