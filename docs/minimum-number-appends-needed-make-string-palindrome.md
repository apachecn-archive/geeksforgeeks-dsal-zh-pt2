# 组成字符串回文所需的最少追加次数

> 原文:[https://www . geesforgeks . org/minimum-number-attachments-required-make-string-回文/](https://www.geeksforgeeks.org/minimum-number-appends-needed-make-string-palindrome/)

给定一个字符串 s，我们需要告诉要追加的最少字符(在末尾插入)来组成一个字符串回文。

**示例:**

```
Input : s = "abede"
Output : 2
We can make string palindrome as "abedeba"
by adding ba at the end of the string.

Input : s = "aabb"
Output : 2
We can make string palindrome as"aabbaa"
by adding aa at the end of the string.
```

解决方法可以通过从字符串的开头一个接一个地删除字符，并检查字符串是否是回文来实现。
例如，考虑上面的字符串，s =**“abede”**。
我们检查字符串是否回文。
结果为假，那么我们从字符串的开头去掉字符，现在字符串变成**“Bede”**。
我们检查字符串是否回文。结果还是假的，然后我们把字符串开头的字符去掉，现在字符串变成**“ede”**。
我们检查字符串是否回文。结果为真，因此输出变为 2，这是从字符串中删除的字符数。

## C++

```
// C program to find minimum number of appends
// needed to make a string Palindrome
#include<stdio.h>
#include<string.h>
#include<stdbool.h>

// Checking if the string is palindrome or not
bool isPalindrome(char *str)
{
    int len = strlen(str);

    // single character is always palindrome
    if (len == 1)
        return true;

    // pointing to first character
    char *ptr1 = str;

    // pointing to last character
    char *ptr2 = str+len-1;

    while (ptr2 > ptr1)
    {
        if (*ptr1 != *ptr2)
            return false;
        ptr1++;
        ptr2--;
    }

    return true;
}

// Recursive function to count number of appends
int noOfAppends(char s[])
{
    if (isPalindrome(s))
        return 0;

    // Removing first character of string by
    // incrementing base address pointer.
    s++;

    return 1 + noOfAppends(s);
}

// Driver program to test above functions
int main()
{
    char s[] = "abede";
    printf("%d\n", noOfAppends(s));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number of appends
// needed to make a string Palindrome
class GFG
{

// Checking if the string is palindrome or not
static boolean isPalindrome(char []str)
{
    int len = str.length;

    // single character is always palindrome
    if (len == 1)
        return true;

    // pointing to first character
    int ptr1 = 0;

    // pointing to last character
    int  ptr2 = len-1;

    while (ptr2 >= ptr1)
    {
        if (str[ptr1] != str[ptr2])
            return false;
        ptr1++;
        ptr2--;
    }

    return true;
}

// Recursive function to count number of appends
static int noOfAppends(String s)
{
    if (isPalindrome(s.toCharArray()))
        return 0;

    // Removing first character of string by
    // incrementing base address pointer.
    s=s.substring(1);

    return 1 + noOfAppends(s);
}

// Driver code
public static void main(String arr[])
{
    String s = "abede";
    System.out.printf("%d\n", noOfAppends(s));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find minimum number of appends
# needed to make a String Palindrome

# Checking if the String is palindrome or not
def isPalindrome(Str):

    Len = len(Str)

    # single character is always palindrome
    if (Len == 1):
        return True

    # pointing to first character
    ptr1 = 0

    # pointing to last character
    ptr2 = Len - 1

    while (ptr2 > ptr1):

        if (Str[ptr1] != Str[ptr2]):
            return False
        ptr1 += 1
        ptr2 -= 1

    return True

# Recursive function to count number of appends
def noOfAppends(s):

    if (isPalindrome(s)):
        return 0

    # Removing first character of String by
    # incrementing base address pointer.
    del s[0]

    return 1 + noOfAppends(s)

# Driver Code
se = "abede"
s = [i for i in se]
print(noOfAppends(s))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find minimum number of appends
// needed to make a string Palindrome
using System;

class GFG
{

// Checking if the string is palindrome or not
static Boolean isPalindrome(char []str)
{
    int len = str.Length;

    // single character is always palindrome
    if (len == 1)
        return true;

    // pointing to first character
    char ptr1 = str[0];

    // pointing to last character
    char ptr2 = str[len-1];

    while (ptr2 > ptr1)
    {
        if (ptr1 != ptr2)
            return false;
        ptr1++;
        ptr2--;
    }

    return true;
}

// Recursive function to count number of appends
static int noOfAppends(String s)
{
    if (isPalindrome(s.ToCharArray()))
        return 0;

    // Removing first character of string by
    // incrementing base address pointer.
    s=s.Substring(1);

    return 1 + noOfAppends(s);
}

// Driver code
public static void Main(String []arr)
{
    String s = "abede";
    Console.Write("{0}\n", noOfAppends(s));
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find minimum number of appends
// needed to make a string Palindrome

    // Checking if the string is palindrome or not
    function isPalindrome(str)
    {
        let len = str.length;

    // single character is always palindrome
    if (len == 1)
        return true;

    // pointing to first character
    let ptr1 = 0;

    // pointing to last character
    let  ptr2 = len-1;

    while (ptr2 >= ptr1)
    {
        if (str[ptr1] != str[ptr2])
            return false;
        ptr1++;
        ptr2--;
    }

    return true;
    }

    // Recursive function to count number of appends
    function noOfAppends(s)
    {
        if (isPalindrome(s.split("")))
            return 0;

    // Removing first character of string by
    // incrementing base address pointer.
    s=s.substring(1);

    return 1 + noOfAppends(s);
    }

    // Driver code
    let s = "abede";
    document.write(noOfAppends(s));

// This code is contributed by unknown2108
</script>
```

**Output**

```
2
```