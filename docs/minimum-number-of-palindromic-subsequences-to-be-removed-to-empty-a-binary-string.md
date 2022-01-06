# 清空二进制字符串需要移除的最小回文子序列数

> 原文:[https://www . geesforgeks . org/最小回文子序列数-要删除的空二进制字符串/](https://www.geeksforgeeks.org/minimum-number-of-palindromic-subsequences-to-be-removed-to-empty-a-binary-string/)

给定一个二进制字符串，计算要删除的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最小数量，使其成为一个空字符串。
**例:**

```
Input: str[] = "10001"
Output: 1
Since the whole string is palindrome, 
we need only one removal.

Input: str[] = "10001001"
Output: 2
We can remove the middle 1 as first 
removal, after first removal string
becomes 1000001 which is a palindrome.
```

预期时间复杂度:O(n)

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/palindromic-subsequences1335/1)

这个问题很简单，可以用下面两个事实轻松解决。
1)如果给定的字符串是回文，我们只需要删除一次。
2)否则我们需要两次清除。请注意，每个二进制字符串都有所有 1 作为子序列，所有 0 作为另一个子序列。我们可以移除两个子序列中的任何一个来获得一元字符串。一元字符串总是回文。

## C++

```
// C++ program to count minimum palindromic subsequences
// to be removed to make an string empty.
#include <bits/stdc++.h>
using namespace std;

// A function to check if a string str is palindrome
bool isPalindrome(const char *str)
{
    // Start from leftmost and rightmost corners of str
    int l = 0;
    int h = strlen(str) - 1;

    // Keep comparing characters while they are same
    while (h > l)
        if (str[l++] != str[h--])
            return false;

    return true;
}

// Returns count of minimum palindromic subseuqnces to
// be removed to make string empty
int minRemovals(const char *str)
{
   // If string is empty
   if (str[0] == '')
      return 0;

   // If string is palindrome
   if (isPalindrome(str))
      return 1;

   // If string is not palindrome
   return 2;
}

// Driver code to test above
int main()
{
   cout << minRemovals("010010") << endl;
   cout << minRemovals("0100101") << endl;
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count minimum palindromic
// subsequences to be removed to make
// an string empty.
import java.io.*;

class GFG {

// A function to check if a string
// str is palindrome
static boolean isPalindrome(String str)
{
    // Start from leftmost and rightmost
    // corners of str
    int l = 0;
    int h = str.length() - 1;

    // Keep comparing characters
    // while they are same
    while (h > l)
        if (str.charAt(l++) != str.charAt(h--))
            return false;

    return true;
}

// Returns count of minimum palindromic
// subseuqnces to be removed to
// make string empty
static int minRemovals(String str)
{
    // If string is empty
    if (str.charAt(0) == '')
        return 0;

    // If string is palindrome
    if (isPalindrome(str))
        return 1;

    // If string is not palindrome
    return 2;
}

// Driver code to test above
public static void main (String[] args)
{
    System.out.println (minRemovals("010010"));
    System.out.println (minRemovals("0100101"));

}
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python program to count minimum
# palindromic subsequences to
# be removed to make an string
# empty.

# A function to check if a
# string str is palindrome
def isPalindrome(str):

    # Start from leftmost and
    # rightmost corners of str
    l = 0
    h = len(str) - 1

    # Keep comparing characters
    # while they are same
    while (h > l):
        if (str[l] != str[h]):
            return 0
        l = l + 1
        h = h - 1

    return 1

# Returns count of minimum
# palindromic subseuqnces to
# be removed to make string
# empty
def minRemovals(str):

    #If string is empty
    if (str[0] == ''):
        return 0

    #If string is palindrome
    if (isPalindrome(str)):
        return 1

    # If string is not palindrome
    return 2

# Driver code
print(minRemovals("010010"))
print(minRemovals("0100101"))

# This code is contributed by Sam007.
```

## C#

```
// C# program to count minimum palindromic
// subsequences to be removed to make
// an string empty.
using System;

class GFG
{

    // A function to check if a
    // string str is palindrome
    static bool isPalindrome(String str)
    {
        // Start from leftmost and
        // rightmost corners of str
        int l = 0;
        int h = str.Length - 1;

        // Keep comparing characters
        // while they are same
        while (h > l)
            if (str[l++] != str[h--])
                return false;

        return true;
    }

    // Returns count of minimum palindromic
    // subseuqnces to be removed to
    // make string empty
    static int minRemovals(String str)
    {
        // If string is empty
        if (str[0] == '')
            return 0;

        // If string is palindrome
        if (isPalindrome(str))
            return 1;

        // If string is not palindrome
        return 2;
    }

    // Driver code to
    public static void Main ()
    {
        Console.WriteLine(minRemovals("010010"));
        Console.WriteLine(minRemovals("0100101"));

    }

}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count minimum
// palindromic subsequences to
// be removed to make an string empty.

// A function to check if a
// string str is palindrome
function isPalindrome($str)
{
    // Start from leftmost and
    // rightmost corners of str
    $l = 0;
    $h = strlen($str) - 1;

    // Keep comparing characters
    // while they are same
    while ($h > $l)
        if ($str[$l++] != $str[$h--])
            return false;

    return true;
}

// Returns count of minimum
// palindromic subsequences
// to be removed to make
// string empty
function minRemovals($str)
{
// If string is empty
if ($str[0] == '')
    return 0;

// If string is palindrome
if (isPalindrome($str))
    return 1;

// If string is not palindrome
return 2;
}

// Driver Code
echo minRemovals("010010"), "\n";
echo minRemovals("0100101") , "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to count
    // minimum palindromic
    // subsequences to be removed to make
    // an string empty.

    // A function to check if a
    // string str is palindrome
    function isPalindrome(str)
    {
        // Start from leftmost and
        // rightmost corners of str
        let l = 0;
        let h = str.length - 1;

        // Keep comparing characters
        // while they are same
        while (h > l)
            if (str[l++] != str[h--])
                return false;

        return true;
    }

    // Returns count of minimum palindromic
    // subseuqnces to be removed to
    // make string empty
    function minRemovals(str)
    {
        // If string is empty
        if (str[0] == '')
            return 0;

        // If string is palindrome
        if (isPalindrome(str))
            return 1;

        // If string is not palindrome
        return 2;
    }

 // Driver Code

    document.write(minRemovals("010010") + "</br>");
      document.write(minRemovals("0100101"));

</script>
```

**输出:**

```
1
2
```

**演习:**T2】

1.  扩展上述解决方案，计算要移除的子序列的最小数量，使其成为空字符串。
2.  三进制字符串的最大计数是多少

这个问题和解决方案是由 **Hardik Gulati** 贡献的。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息