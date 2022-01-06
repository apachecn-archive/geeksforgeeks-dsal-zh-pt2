# 形成最短回文的最少插入数

> 原文:[https://www . geesforgeks . org/minimum-insertions-to-form-short-回文/](https://www.geeksforgeeks.org/minimum-insertions-to-form-shortest-palindrome/)

给定一个字符串 S，确定应该添加到 S 左侧的最少字符数，以便整个字符串成为回文。

**示例:**

```
Input: S = "LOL"
Output: 0
LOL is already a palindrome

Input: S = "JAVA"
Output: 3
We need to add 3 characters to form AVAJAVA.
```

其思想是找到给定字符串的最长回文前缀。前缀后的字符数就是我们的答案。最长的回文前缀可以通过从最后一个字符循环到第一个字符来找到。比如在“JAVA”中，最长的回文前缀是“J”，所以我们需要在开头加剩余的 3 个字符组成回文。

## C++

```
// C++ program to find minimum number of insertions
// on left side to form a palindrome.

#include <bits/stdc++.h>
using namespace std;

// Returns true if a string str[st..end] is palindrome
bool isPalin(char str[], int st, int end)
{
    while (st < end)
    {
        if (str[st] != str[end])
            return false;
        st++;
        end--;
    }
    return true;
}

// Returns count of insertions on left side to make
// str[] a palindrome
int findMinInsert(char str[], int n)
{
    // Find the largest prefix of given string
    // that is palindrome.
    for (int i=n-1; i>=0; i--)
    {        
        // Characters after the palindromic prefix
        // must be added at the beginning also to make
        // the complete string palindrome
        if (isPalin(str, 0, i))
            return (n-i-1);
    }
}

// Driver program
int main()
{
    char Input[] = "JAVA";
    printf("%d", findMinInsert(Input, strlen(Input)));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number
// of insertions on left side to form
// a palindrome.
import java.util.*;

class GFG{

// Returns true if a string
// str[st..end] is palindrome
static boolean isPalin(char []str, int st,
                                   int end)
{
    while (st < end)
    {
        if (str[st] != str[end])
            return false;

        st++;
        end--;
    }
    return true;
}

// Returns count of insertions on
// left side to make str[] a palindrome
static int findMinInsert(char []str, int n)
{

    // Find the largest prefix of given
    // string that is palindrome.
    for(int i = n - 1; i >= 0; i--)
    {

        // Characters after the palindromic
        // prefix must be added at the
        // beginning also to make the
        // complete string palindrome
        if (isPalin(str, 0, i))
            return (n - i - 1);
    }
    return 0;
}

// Driver Code
public static void main(String []args)
{
    char []Input = "JAVA".toCharArray();

    System.out.println(findMinInsert(Input,
                                     Input.length));
}
}

// This code is contributed by pratham76
```

## 蟒蛇 3

```
# Python3 program to find
# minimum number of insertions
# on left side to form a palindrome.

# Returns true if a string
# str[st..end] is palindrome
def isPalin(str, st, end):

    while (st < end):

        if (str[st] != str[end]):
            return False
        st += 1
        end--1

    return True

# Returns count of insertions
# on left side to make
# str[] a palindrome
def findMinInsert(str, n):

    # Find the largest
    # prefix of given string
    # that is palindrome.
    for i in range(n-1 ,-1, -1):

        # Characters after the
        # palindromic prefix must
        # be added at the beginning
        # also to make the complete
        # string palindrome
        if (isPalin(str, 0, i)):
            return (n - i - 1)

# Driver Code
Input = "JAVA"
print(findMinInsert(Input,
                    len(Input)))

# This code is contributed
# by Smitha
```

## C#

```
// C# program to find minimum number
// of insertions on left side to form
// a palindrome.
using System;
using System.Text;

class GFG{

// Returns true if a string
// str[st..end] is palindrome
static bool isPalin(char []str, int st,
                                int end)
{
    while (st < end)
    {
        if (str[st] != str[end])
            return false;

        st++;
        end--;
    }
    return true;
}

// Returns count of insertions on
// left side to make str[] a palindrome
static int findMinInsert(char []str, int n)
{

    // Find the largest prefix of given string
    // that is palindrome.
    for(int i = n - 1; i >= 0; i--)
    {

        // Characters after the palindromic
        // prefix must be added at the
        // beginning also to make the
        // complete string palindrome
        if (isPalin(str, 0, i))
            return (n - i - 1);
    }
    return 0;
}

// Driver Code
public static void Main(string []args)
{
    char []Input = "JAVA".ToCharArray();

    Console.Write(findMinInsert(Input,
                                Input.Length));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// javascript program to find minimum number of insertions
// on left side to form a palindrome.

// Returns true if a string str[st..end] is palindrome
function isPalin(str,st,end)
{
    while (st < end)
    {
        if (str[st] != str[end])
            return false;
        st++;
        end--;
    }
    return true;
}

// Returns count of insertions on left side to make
// str[] a palindrome
function findMinInsert(str,n)
{
    // Find the largest prefix of given string
    // that is palindrome.
    for (let i = n - 1; i >= 0; i--)
    {       
        // Characters after the palindromic prefix
        // must be added at the beginning also to make
        // the complete string palindrome
        if (isPalin(str, 0, i))
            return (n - i - 1);
    }
}

    let Input = "JAVA";
    document.write(findMinInsert(Input,Input.length));

 // This code is contributed by vaibhavrabadiya07.  
</script>
```

**输出:**

```
3
```

**时间复杂度:** O(n <sup>2</sup>

感谢乌卡什·特里维迪提出这个解决方案。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息