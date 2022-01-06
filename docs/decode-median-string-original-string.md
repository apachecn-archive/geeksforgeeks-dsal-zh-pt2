# 将中间字符串解码为原始字符串

> 原文:[https://www . geesforgeks . org/decode-middle-string-original-string/](https://www.geeksforgeeks.org/decode-median-string-original-string/)

给定一个以中间形式书写的字符串，将其更改回原始字符串。字符串中的中间字母是位于字符串中间的字母。如果字符串的长度是偶数，中间的字母是中间两个字母的左边。给定的字符串是通过写下单词的中间字母，然后删除它，重复这个过程，直到没有剩下的字母。

**示例:**

```
Input: eekgs
Output: geeks 
Explanation: in the original string “geeks” 
can be written in median form by picking up 
e first then, again e, then k then g and at
the end s. As these are the median when the
median letter is picked and deleted. 

Input: abc 
Output: bac 
Explanation: median of bac is a, then median
of bc is b, then median of c is c.  
```

为了找到答案，我们可以从左到右遍历给定的编码字符串，并添加答案字符串中的每个字母，一个字母到开头，下一个字母到结尾，下一个字母到开头，依此类推。如果 n 是偶数，那么第一个字母必须加到开头，第二个字母必须加到结尾。在另一种情况下，第一个字母排在末尾，第二个排在开头。我们需要做它，直到我们没有添加来自给定字符串的所有字母。
**注**:对于偶数长度的字符串，当我们将第一个字符添加到开头，将第二个字符添加到结尾时，剩下的字符串将始终是偶数长度。长度为奇数的字符串也是如此。
*下面给出的是上述方法的实施*

## C++

```
// C++ program to decode a median string
// to the original string

#include <bits/stdc++.h>
using namespace std;

// function to calculate the median back string
string decodeMedianString(string s)
{
    // length of string
    int l = s.length();

    // initialize a blank string
    string s1 = "";

    // Flag to check if length is even or odd
    bool isEven = (l % 2 == 0)? true : false;

    // traverse from first to last
    for (int i = 0; i < l; i += 2) {

        // if len is even then add first character
        // to beginning of new string and second
        // character to end
        if (isEven) {  
            s1 = s[i] + s1;
            s1 += s[i + 1];
        } else {

            // if current length is odd and is
            // greater than 1
            if (l - i > 1) {

                // add first character to end and
                // second character to beginning
                s1 += s[i];
                s1 = s[i + 1] + s1;
            } else {

                // if length is 1, add character 
                // to end
                s1 += s[i];
            }
        }
    }

    return s1;
}

// driver program
int main()
{
    string s = "eekgs";
    cout << decodeMedianString(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to decode a median
// string to the original string

public class GFG {

    // function to calculate the
    // median back string
    static String decodeMedianString(String s)
    {

        // length of string
        int l = s.length();

        // initialize a blank string
        String s1 = "";

        // Flag to check if length is
        // even or odd
        boolean isEven = (l % 2 == 0) ?
                          true : false;

        // traverse from first to last
        for (int i = 0; i < l; i += 2)
        {

            // if len is even then add
            // first character to
            // beginning of new string
            // and second character to
            // end
            if (isEven) {
                s1 = s.charAt(i) + s1;
                s1 += s.charAt(i+1);
            }
            else {

                // if current length is
                // odd and is greater
                // than 1
                if (l - i > 1) {

                    // add first character
                    // to end and second
                    // character to
                    // beginning
                    s1 += s.charAt(i);
                    s1 = s.charAt(i+1) + s1;
                }
                else {

                    // if length is 1,
                    // add character
                    // to end
                    s1 += s.charAt(i);
                }
            }
        }

        return s1;
    }

    // Driver code
    public static void main(String args[])
    {
        String s = "eekgs";

        System.out.println(
                    decodeMedianString(s));
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# Python3 program to decode a median
# string to the original string

# function to calculate the median
# back string
def decodeMedianString(s):

    # length of string
    l = len(s)

    # initialize a blank string
    s1 = ""

    # Flag to check if length is
    # even or odd
    if(l % 2 == 0):
        isEven = True
    else:
        isEven = False

    # traverse from first to last
    for i in range(0, l, 2):

        # if len is even then add first
        # character to beginning of new
        # string and second character to end
        if (isEven):
            s1 = s[i] + s1
            s1 += s[i + 1]
        else :

            # if current length is odd and
            # is greater than 1
            if (l - i > 1):

                # add first character to end and
                # second character to beginning
                s1 += s[i]
                s1 = s[i + 1] + s1
            else:

                # if length is 1, add character
                # to end
                s1 += s[i]

    return s1

# Driver Code
if __name__ == '__main__':
    s = "eekgs"
    print(decodeMedianString(s))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to decode a median
// string to the original string
using System;

class GFG {

    // function to calculate the
    // median back string
    static string decodeMedianString(string s)
    {

        // length of string
        int l = s.Length;

        // initialize a blank string
        string s1 = "";

        // Flag to check if length is
        // even or odd
        bool isEven = (l % 2 == 0) ?
                         true : false;

        // traverse from first to last
        for (int i = 0; i < l; i += 2)
        {

            // if len is even then add
            // first character to
            // beginning of new string
            // and second character to
            // end
            if (isEven) {
                s1 = s[i] + s1;
                s1 += s[i + 1];
            }
            else {

                // if current length is
                // odd and is greater
                // than 1
                if (l - i > 1) {

                    // add first character
                    // to end and second
                    // character to
                    // beginning
                    s1 += s[i];
                    s1 = s[i + 1] + s1;
                }
                else {

                    // if length is 1,
                    // add character
                    // to end
                    s1 += s[i];
                }
            }
        }

        return s1;
    }

    // Driver code
    public static void Main ()
    {
        string s = "eekgs";
        Console.WriteLine(
               decodeMedianString(s));
    }
}

// This code is contributed by Sam007.
```

## java 描述语言

```
<script>
// javascript program to decode a median
// string to the original string

    // function to calculate the
    // median back string
    function decodeMedianString( s) {

        // length of string
        var l = s.length;

        // initialize a blank string
        var s1 = "";

        // Flag to check if length is
        // even or odd
        var isEven = (l % 2 == 0) ? true : false;

        // traverse from first to last
        for (i = 0; i < l; i += 2) {

            // if len is even then add
            // first character to
            // beginning of new string
            // and second character to
            // end
            if (isEven) {
                s1 = s.charAt(i) + s1;
                s1 += s.charAt(i + 1);
            } else {

                // if current length is
                // odd and is greater
                // than 1
                if (l - i > 1) {

                    // add first character
                    // to end and second
                    // character to
                    // beginning
                    s1 += s.charAt(i);
                    s1 = s.charAt(i + 1) + s1;
                } else {

                    // if length is 1,
                    // add character
                    // to end
                    s1 += s.charAt(i);
                }
            }
        }

        return s1;
    }

    // Driver code

        var s = "eekgs";

        document.write(decodeMedianString(s));

// This code contributed by Rajput-Ji
</script>
```

**输出:**

```
geeks
```

时间复杂度:O(n)
本文由 [**奋斗者**](https://www.facebook.com/raja.vikramaditya.7) 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。