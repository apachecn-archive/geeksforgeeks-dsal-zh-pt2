# 回文子串最大长度，以给定字符开始和结束

> 原文:[https://www . geeksforgeeks . org/最大长度-回文-子串-以给定字符开头和结尾/](https://www.geeksforgeeks.org/maximum-length-palindromic-substring-such-that-it-starts-and-ends-with-given-char/)

给定一个字符串 **str** 和一个字符 **ch** ，任务是找到 **str** 的最长回文子字符串，使其以给定的字符 **ch** 开始和结束。
**举例:**

> **输入:**str = " lapqoqppl "，ch = ' p '
> T3】输出:6
> “pqoqp”是以' p '开头和结尾的最大长度回文
> 子串。
> **输入:** str = "geeksforgeeks "，ch = 'k'
> **输出:**1
> “k”为有效子串。

**方法:**对于每个可能的索引对 **(i，j)** ，使得 **str[i] = str[j] = ch** 检查子串 **str[i…j]** 是否是回文。对于所有找到的回文，存储到目前为止找到的最长回文的长度。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// str[i...j] is a palindrome
bool isPalindrome(string str, int i, int j)
{
    while (i < j) {
        if (str[i] != str[j])
            return false;
        i++;
        j--;
    }
    return true;
}

// Function to return the length of the
// longest palindromic sub-string such that
// it starts and ends with the character ch
int maxLenPalindrome(string str, int n, char ch)
{
    int maxLen = 0;

    for (int i = 0; i < n; i++) {

        // If current character is
        // a valid starting index
        if (str[i] == ch) {

            // Instead of finding the ending index from
            // the beginning, find the index from the end
            // This is because if the current sub-string
            // is a palindrome then there is no need to check
            // the sub-strings of smaller length and we can
            // skip to the next iteration of the outer loop
            for (int j = n - 1; j >= i; j--) {

                // If current character is
                // a valid ending index
                if (str[j] == ch) {

                    // If str[i...j] is a palindrome then update
                    // the length of the maximum palindrome so far
                    if (isPalindrome(str, i, j)) {
                        maxLen = max(maxLen, j - i + 1);
                        break;
                    }
                }
            }
        }
    }
    return maxLen;
}

// Driver code
int main()
{
    string str = "lapqooqpqpl";
    int n = str.length();
    char ch = 'p';

    cout << maxLenPalindrome(str, n, ch);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns true if
    // str[i...j] is a palindrome
    static boolean isPalindrome(String str,
                               int i, int j)
    {
        while (i < j)
        {
            if (str.charAt(i) != str.charAt(j))
            {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }

    // Function to return the length of the
    // longest palindromic sub-string such that
    // it starts and ends with the character ch
    static int maxLenPalindrome(String str, int n, char ch)
    {
        int maxLen = 0;

        for (int i = 0; i < n; i++)
        {

            // If current character is
            // a valid starting index
            if (str.charAt(i) == ch)
            {

                // Instead of finding the ending index from
                // the beginning, find the index from the end
                // This is because if the current sub-string
                // is a palindrome then there is no need to check
                // the sub-strings of smaller length and we can
                // skip to the next iteration of the outer loop
                for (int j = n - 1; j >= i; j--)
                {

                    // If current character is
                    // a valid ending index
                    if (str.charAt(j) == ch)
                    {

                        // If str[i...j] is a palindrome then update
                        // the length of the maximum palindrome so far
                        if (isPalindrome(str, i, j))
                        {
                            maxLen = Math.max(maxLen, j - i + 1);
                            break;
                        }
                    }
                }
            }
        }
        return maxLen;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "lapqooqpqpl";
        int n = str.length();
        char ch = 'p';

        System.out.println(maxLenPalindrome(str, n, ch));
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function that returns true if
# str[i...j] is a palindrome
def isPalindrome(str, i, j):
    while (i < j):
        if (str[i] != str[j]):
            return False;
        i+=1;
        j-=1;
    return True;

# Function to return the length of the
# longest palindromic sub-string such that
# it starts and ends with the character ch
def maxLenPalindrome(str, n, ch):
    maxLen = 0;

    for i in range(n):

        # If current character is
        # a valid starting index
        if (str[i] == ch):

            # Instead of finding the ending index from
            # the beginning, find the index from the end
            # This is because if the current sub-string
            # is a palindrome then there is no need to check
            # the sub-strings of smaller length and we can
            # skip to the next iteration of the outer loop
            for j in range(n-1,i+1,-1):
                # If current character is
                # a valid ending index
                if (str[j] == ch):

                    # If str[i...j] is a palindrome then update
                    # the length of the maximum palindrome so far
                    if (isPalindrome(str, i, j)):
                        maxLen = max(maxLen, j - i + 1);
                        break;

    return maxLen;

# Driver code
str = "lapqooqpqpl";
n = len(str);
ch = 'p';

print(maxLenPalindrome(str, n, ch));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if
    // str[i...j] is a palindrome
    static bool isPalindrome(string str,
                            int i, int j)
    {
        while (i < j)
        {
            if (str[i] != str[j])
            {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }

    // Function to return the length of the
    // longest palindromic sub-string such that
    // it starts and ends with the character ch
    static int maxLenPalindrome(string str, int n, char ch)
    {
        int maxLen = 0;

        for (int i = 0; i < n; i++)
        {

            // If current character is
            // a valid starting index
            if (str[i] == ch)
            {

                // Instead of finding the ending index from
                // the beginning, find the index from the end
                // This is because if the current sub-string
                // is a palindrome then there is no need to check
                // the sub-strings of smaller length and we can
                // skip to the next iteration of the outer loop
                for (int j = n - 1; j >= i; j--)
                {

                    // If current character is
                    // a valid ending index
                    if (str[j] == ch)
                    {

                        // If str[i...j] is a palindrome then update
                        // the length of the maximum palindrome so far
                        if (isPalindrome(str, i, j))
                        {
                            maxLen = Math.Max(maxLen, j - i + 1);
                            break;
                        }
                    }
                }
            }
        }
        return maxLen;
    }

    // Driver code
    public static void Main()
    {
        string str = "lapqooqpqpl";
        int n = str.Length;
        char ch = 'p';

        Console.WriteLine(maxLenPalindrome(str, n, ch));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function that returns true if
      // str[i...j] is a palindrome
      function isPalindrome(str, i, j) {
        while (i < j) {
          if (str[i] !== str[j]) {
            return false;
          }
          i++;
          j--;
        }
        return true;
      }

      // Function to return the length of the
      // longest palindromic sub-string such that
      // it starts and ends with the character ch
      function maxLenPalindrome(str, n, ch) {
        var maxLen = 0;

        for (var i = 0; i < n; i++) {
          // If current character is
          // a valid starting index
          if (str[i] === ch) {
            // Instead of finding the ending index from
            // the beginning, find the index from the end
            // This is because if the current sub-string
            // is a palindrome then there is no need to check
            // the sub-strings of smaller length and we can
            // skip to the next iteration of the outer loop
            for (var j = n - 1; j >= i; j--) {
              // If current character is
              // a valid ending index
              if (str[j] === ch) {
                // If str[i...j] is a palindrome then update
                // the length of the maximum palindrome so far
                if (isPalindrome(str, i, j)) {
                  maxLen = Math.max(maxLen, j - i + 1);
                  break;
                }
              }
            }
          }
        }
        return maxLen;
      }

      // Driver code
      var str = "lapqooqpqpl";
      var n = str.length;
      var ch = "p";

      document.write(maxLenPalindrome(str, n, ch));
    </script>
```

**Output:** 

```
6
```