# 最长回文子串长度:递归

> 原文:[https://www . geesforgeks . org/length-最长回文-子串-递归/](https://www.geeksforgeeks.org/length-of-longest-palindromic-sub-string-recursion/)

给定一个字符串 **S** ，任务是找到长度最长的子字符串，这是一个[回文](https://www.inf.unibz.it/~calvanese/teaching/06-07-ip/lecture-notes/uni11/node21.html)
T5【例:

> **输入:**S = " aaabaa "
> T3】输出: 6
> **说明:**
> 子串“aabbaa”是最长的回文子串。
> **输入:** S = "香蕉"
> **输出:** 5
> **解释:**
> 子串“anana”是回文最长的子串。

**方法:**思路是用[递归](https://www.geeksforgeeks.org/recursion/)把问题分解成更小的子问题。为了将问题分解成两个较小的子问题，比较字符串的开始和结束字符，并递归调用中间子字符串的函数。下面是递归的例子:

*   **基本情况:**这个问题的基本情况是字符串的起始索引大于等于结束索引。

```
if (start > end)
    return count
if (start == end)
    return count + 1
```

*   **递归情况:**比较字符串开始和结束索引处的字符:
    *   当开始和结束字符相等时，通过排除开始和结束字符递归调用子字符串

```
recursive_func(string, start+1, end-1)
```

*   当开始和结束字符不相等时，通过一次排除一个开始和结束字符来递归调用子字符串。

```
recursive_func(string, start+1, end)
recursive_func(string, start, end-1)
```

*   **Return 语句:**在每次递归调用时，通过包含和排除开始和结束字符来返回可能的最大计数。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// length of longest palindromic
// sub-string using Recursion

#include <iostream>
using namespace std;

// Function to find maximum
// of the two variables
int max(int x, int y)
{
    return (x > y) ? x : y;
}

// Function to find the longest
// palindromic substring : Recursion
int longestPalindromic(string str,
             int i, int j, int count)
{

    // Base condition when the start
    // index is greater than end index
    if (i > j)
        return count;

    // Base condition when both the
    // start and end index are equal
    if (i == j)
        return (count + 1);

    // Condition when corner characters
    // are equal in the string
    if (str[i] == str[j]) {

        // Recursive call to find the
        // longest Palindromic string
        // by excluding the corner characters
        count = longestPalindromic(str, i + 1,
                  j - 1, count + 2);
        return max(count,
        max(longestPalindromic(str, i + 1, j, 0),
         longestPalindromic(str, i, j - 1, 0)));
    }

    // Recursive call to find the
    // longest Palindromic string
    // by including one corner
    // character at a time
    return max(
       longestPalindromic(str, i + 1, j, 0),
       longestPalindromic(str, i, j - 1, 0));
}

// Function to find the longest
// palindromic sub-string
int longest_palindromic_substr(string str)
{
    // Utility function call
    return longestPalindromic(str, 0,
                 str.length() - 1, 0);
}

// Driver Code
int main()
{
    string str = "aaaabbaa";

    // Function Call
    cout << longest_palindromic_substr(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// length of longest palindromic
// sub-String using Recursion
class GFG{

// Function to find maximum
// of the two variables
static int max(int x, int y)
{
    return (x > y) ? x : y;
}

// Function to find the longest
// palindromic subString : Recursion
static int longestPalindromic(String str,
             int i, int j, int count)
{

    // Base condition when the start
    // index is greater than end index
    if (i > j)
        return count;

    // Base condition when both the
    // start and end index are equal
    if (i == j)
        return (count + 1);

    // Condition when corner characters
    // are equal in the String
    if (str.charAt(i) == str.charAt(j)) {

        // Recursive call to find the
        // longest Palindromic String
        // by excluding the corner characters
        count = longestPalindromic(str, i + 1,
                  j - 1, count + 2);
        return max(count,
        max(longestPalindromic(str, i + 1, j, 0),
         longestPalindromic(str, i, j - 1, 0)));
    }

    // Recursive call to find the
    // longest Palindromic String
    // by including one corner
    // character at a time
    return Math.max(
       longestPalindromic(str, i + 1, j, 0),
       longestPalindromic(str, i, j - 1, 0));
}

// Function to find the longest
// palindromic sub-String
static int longest_palindromic_substr(String str)
{
    // Utility function call
    return longestPalindromic(str, 0,
                 str.length() - 1, 0);
}

// Driver Code
public static void main(String[] args)
{
    String str = "aaaabbaa";

    // Function Call
    System.out.print(longest_palindromic_substr(str));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to find the
# length of longest palindromic
# sub-string using Recursion

# Function to find maximum
# of the two variables
def maxi(x, y) :
    if x > y :
        return x
    else :
        return y

# Function to find the longest
# palindromic substring : Recursion
def longestPalindromic(strn, i, j, count):

    # Base condition when the start
    # index is greater than end index
    if i > j :
        return count

    # Base condition when both the
    # start and end index are equal
    if i == j :
        return (count + 1)

    # Condition when corner characters
    # are equal in the string
    if strn[i] == strn[j] :

        # Recursive call to find the
        # longest Palindromic string
        # by excluding the corner characters
        count = longestPalindromic(strn, i + 1, j - 1, count + 2)
        return maxi(count, maxi(longestPalindromic(strn, i + 1, j, 0),
                    longestPalindromic(strn, i, j - 1, 0)))

    # Recursive call to find the
    # longest Palindromic string
    # by including one corner
    # character at a time
    return maxi( longestPalindromic(strn, i + 1, j, 0),
                longestPalindromic(strn, i, j - 1, 0))

# Function to find the longest
# palindromic sub-string
def longest_palindromic_substr(strn):

    # Utility function call
    k = len(strn) - 1
    return longestPalindromic(strn, 0, k, 0)

strn = "aaaabbaa"

# Function Call
print( longest_palindromic_substr(strn) )

# This code is contributed by chsadik99   

```

## C#

```
// C# implementation to find the
// length of longest palindromic
// sub-String using Recursion
using System;

class GFG{

// Function to find maximum
// of the two variables
static int max(int x, int y)
{
    return (x > y) ? x : y;
}

// Function to find the longest
// palindromic subString : Recursion
static int longestPalindromic(String str,
             int i, int j, int count)
{

    // Base condition when the start
    // index is greater than end index
    if (i > j)
        return count;

    // Base condition when both the
    // start and end index are equal
    if (i == j)
        return (count + 1);

    // Condition when corner characters
    // are equal in the String
    if (str[i] == str[j]) {

        // Recursive call to find the
        // longest Palindromic String
        // by excluding the corner characters
        count = longestPalindromic(str, i + 1,
                  j - 1, count + 2);
        return max(count,
        max(longestPalindromic(str, i + 1, j, 0),
         longestPalindromic(str, i, j - 1, 0)));
    }

    // Recursive call to find the
    // longest Palindromic String
    // by including one corner
    // character at a time
    return Math.Max(
       longestPalindromic(str, i + 1, j, 0),
       longestPalindromic(str, i, j - 1, 0));
}

// Function to find the longest
// palindromic sub-String
static int longest_palindromic_substr(String str)
{
    // Utility function call
    return longestPalindromic(str, 0,
                 str.Length - 1, 0);
}

// Driver Code
public static void Main(String[] args)
{
    String str = "aaaabbaa";

    // Function Call
    Console.Write(longest_palindromic_substr(str));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript implementation to find the
    // length of longest palindromic
    // sub-String using Recursion

    // Function to find maximum
    // of the two variables
    function max(x, y)
    {
        return (x > y) ? x : y;
    }

    // Function to find the longest
    // palindromic subString : Recursion
    function longestPalindromic(str, i, j, count)
    {

        // Base condition when the start
        // index is greater than end index
        if (i > j)
            return count;

        // Base condition when both the
        // start and end index are equal
        if (i == j)
            return (count + 1);

        // Condition when corner characters
        // are equal in the String
        if (str[i] == str[j]) {

            // Recursive call to find the
            // longest Palindromic String
            // by excluding the corner characters
            count = longestPalindromic(str, i + 1,
                      j - 1, count + 2);
            return max(count,
            max(longestPalindromic(str, i + 1, j, 0),
             longestPalindromic(str, i, j - 1, 0)));
        }

        // Recursive call to find the
        // longest Palindromic String
        // by including one corner
        // character at a time
        return Math.max(
           longestPalindromic(str, i + 1, j, 0),
           longestPalindromic(str, i, j - 1, 0));
    }

    // Function to find the longest
    // palindromic sub-String
    function longest_palindromic_substr(str)
    {
        // Utility function call
        return longestPalindromic(str, 0, str.length - 1, 0);
    }

    let str = "aaaabbaa";

    // Function Call
    document.write(longest_palindromic_substr(str));

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
6
```