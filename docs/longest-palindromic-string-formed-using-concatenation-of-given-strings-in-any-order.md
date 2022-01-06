# 由任意顺序的给定字符串串联而成的最长回文字符串

> 原文:[https://www . geesforgeks . org/最长回文字符串格式-使用任意顺序给定字符串的串联/](https://www.geeksforgeeks.org/longest-palindromic-string-formed-using-concatenation-of-given-strings-in-any-order/)

给定一个相同长度的字符串数组 **arr[]** ，任务是找到最长的回文字符串，该字符串可以使用任意顺序的字符串串联而成。

**示例:**

> **输入:** arr[] = {“阿坝”、“阿坝”}
> T3】输出:阿坝
> 
> **输入:**arr[]= {“ABC”、“dba”、“kop”、“cba”、“Abd”}
> **输出:**abcdabacba

**进场:**

*   找出彼此相反的所有字符串对，分别存储在两个不同的数组 **pair1[]** 和 **pair2** 中，并从原始数组中删除这些字符串对。
*   在数组中找到任意回文串 **s1** 。
*   将数组对 1[]的所有字符串连接在一起成为 **s2**
*   将数组对 2[]的所有字符串以相反的顺序连接到 **s3** 中
*   将字符串 s2 + s1 + s3 连接在一起，得到最长的回文字符串。

下面是上述方法的实现。

## C++

```
// C++ implementation to find the longest
// palindromic String formed using
// concatenation of given strings in any order

#include <bits/stdc++.h>
using namespace std;

// Function to find the longest palindromic
// from given array of strings
void longestPalindrome(string a[],
                       int n)
{
    string pair1[n];
    string pair2[n];
    int r = 0;

    // Loop to find the pair of strings
    // which are reverse of each other
    for (int i = 0; i < n; i++) {
        string s = a[i];
        reverse(s.begin(), s.end());
        for (int j = i + 1; j < n; j++) {
            if (a[i] != "" && a[j] != "") {
                if (s == a[j]) {
                    pair1[r] = a[i];
                    pair2[r++] = a[j];
                    a[i] = "";
                    a[j] = "";
                    break;
                }
            }
        }
    }
    string s1 = "";

    // Loop to find if any palindromic
    // string is still left in the array
    for (int i = 0; i < n; i++) {
        string s = a[i];
        reverse(a[i].begin(), a[i].end());
        if (a[i] != "") {
            if (a[i] == s) {
                s1 = a[i];
                break;
            }
        }
    }
    string ans = "";

    // Update the answer with
    // all strings of pair1
    for (int i = 0; i < r; i++) {
        ans = ans + pair1[i];
    }
    // Update the answer with
    // palindromic string s1
    if (s1 != "") {
        ans = ans + s1;
    }
    // Update the answer with
    // all strings of pair2
    for (int j = r - 1; j >= 0; j--) {
        ans = ans + pair2[j];
    }
    cout << ans << endl;
}

// Driver Code
int main()
{
    string a1[2] = { "aba", "aba" };
    int n1 = sizeof(a1) / sizeof(a1[0]);
    longestPalindrome(a1, n1);

    string a2[5] = { "abc", "dba", "kop",
                     "abd", "cba" };
    int n2 = sizeof(a2) / sizeof(a2[0]);
    longestPalindrome(a2, n2);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the longest
// palindromic String formed using
// concatenation of given Strings in any order
class GFG
{

// Function to find the longest palindromic
// from given array of Strings
static void longestPalindrome(String a[],
                            int n)
{
    String []pair1 = new String[n];
    String []pair2 = new String[n];
    int r = 0;

    // Loop to find the pair of Strings
    // which are reverse of each other
    for (int i = 0; i < n; i++)
    {
        String s = a[i];
        s = reverse(s);
        for (int j = i + 1; j < n; j++)
        {
            if (a[i] != "" && a[j] != "")
            {
                if (s.equals(a[j]))
                {
                    pair1[r] = a[i];
                    pair2[r++] = a[j];
                    a[i] = "";
                    a[j] = "";
                    break;
                }
            }
        }
    }
    String s1 = "";

    // Loop to find if any palindromic
    // String is still left in the array
    for (int i = 0; i < n; i++)
    {
        String s = a[i];
        a[i] = reverse(a[i]);
        if (a[i] != "")
        {
            if (a[i].equals(s))
            {
                s1 = a[i];
                break;
            }
        }
    }
    String ans = "";

    // Update the answer with
    // all Strings of pair1
    for (int i = 0; i < r; i++)
    {
        ans = ans + pair1[i];
    }

    // Update the answer with
    // palindromic String s1
    if (s1 != "")
    {
        ans = ans + s1;
    }
    // Update the answer with
    // all Strings of pair2
    for (int j = r - 1; j >= 0; j--)
    {
        ans = ans + pair2[j];
    }
    System.out.print(ans +"\n");
}
static String reverse(String input)
{
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for (l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.valueOf(a);
}

// Driver Code
public static void main(String[] args)
{
    String []a1 = { "aba", "aba" };
    int n1 = a1.length;
    longestPalindrome(a1, n1);

    String []a2 = { "abc", "dba", "kop",
                    "abd", "cba" };
    int n2 = a2.length;
    longestPalindrome(a2, n2);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to find the longest
# palindromic String formed using
# concatenation of given strings in any order

# Function to find the longest palindromic
# from given array of strings
def longestPalindrome(a, n):
    pair1 = [0]*n
    pair2 = [0]*n
    r = 0

    # Loop to find the pair of strings
    # which are reverse of each other
    for i in range(n):
        s = a[i]
        s = s[::-1]
        for j in range(i + 1, n):
            if (a[i] != "" and a[j] != ""):
                if (s == a[j]):
                    pair1[r] = a[i]
                    pair2[r] = a[j]
                    r += 1
                    a[i] = ""
                    a[j] = ""
                    break

    s1 = ""

    # Loop to find if any palindromic
    # is still left in the array
    for i in range(n):
        s = a[i]
        a[i] = a[i][::-1]
        if (a[i] != ""):
            if (a[i] == s):
                s1 = a[i]
                break

    ans = ""

    # Update the answer with
    # all strings of pair1
    for i in range(r):
        ans = ans + pair1[i]

    # Update the answer with
    # palindromic s1
    if (s1 != ""):
        ans = ans + s1

    # Update the answer with
    # all strings of pair2
    for j in range(r - 1, -1, -1):
        ans = ans + pair2[j]
    print(ans)

# Driver Code
a1 = ["aba", "aba"]
n1 = len(a1)
longestPalindrome(a1, n1)

a2 = ["abc", "dba", "kop","abd", "cba"]
n2 = len(a2)
longestPalindrome(a2, n2)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find the longest
// palindromic String formed using
// concatenation of given Strings in any order
using System;

class GFG
{

// Function to find the longest palindromic
// from given array of Strings
static void longestPalindrome(String []a,
                            int n)
{
    String []pair1 = new String[n];
    String []pair2 = new String[n];
    int r = 0;

    // Loop to find the pair of Strings
    // which are reverse of each other
    for (int i = 0; i < n; i++)
    {
        String s = a[i];
        s = reverse(s);
        for (int j = i + 1; j < n; j++)
        {
            if (a[i] != "" && a[j] != "")
            {
                if (s.Equals(a[j]))
                {
                    pair1[r] = a[i];
                    pair2[r++] = a[j];
                    a[i] = "";
                    a[j] = "";
                    break;
                }
            }
        }
    }
    String s1 = "";

    // Loop to find if any palindromic
    // String is still left in the array
    for (int i = 0; i < n; i++)
    {
        String s = a[i];
        a[i] = reverse(a[i]);
        if (a[i] != "")
        {
            if (a[i].Equals(s))
            {
                s1 = a[i];
                break;
            }
        }
    }
    String ans = "";

    // Update the answer with
    // all Strings of pair1
    for (int i = 0; i < r; i++)
    {
        ans = ans + pair1[i];
    }

    // Update the answer with
    // palindromic String s1
    if (s1 != "")
    {
        ans = ans + s1;
    }
    // Update the answer with
    // all Strings of pair2
    for (int j = r - 1; j >= 0; j--)
    {
        ans = ans + pair2[j];
    }
    Console.Write(ans +"\n");
}
static String reverse(String input)
{
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;
    for (l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("",a);
}

// Driver Code
public static void Main(String[] args)
{
    String []a1 = { "aba", "aba" };
    int n1 = a1.Length;
    longestPalindrome(a1, n1);

    String []a2 = { "abc", "dba", "kop",
                    "abd", "cba" };
    int n2 = a2.Length;
    longestPalindrome(a2, n2);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to find the longest
// palindromic String formed using
// concatenation of given strings in any order

// Function to find the longest palindromic
// from given array of strings
function longestPalindrome(a, n)
{
    var pair1 = Array(n);
    var pair2 = Array(n);
    var r = 0;

    // Loop to find the pair of strings
    // which are reverse of each other
    for(var i = 0; i < n; i++)
    {
        var s = a[i];
        s = s.split('').reverse().join('');

        for(var j = i + 1; j < n; j++)
        {
            if (a[i] != "" && a[j] != "")
            {
                if (s == a[j])
                {
                    pair1[r] = a[i];
                    pair2[r++] = a[j];
                    a[i] = "";
                    a[j] = "";
                    break;
                }
            }
        }
    }
    var s1 = "";

    // Loop to find if any palindromic
    // string is still left in the array
    for(var i = 0; i < n; i++)
    {
        var s = a[i];
        a[i] = a[i].split('').reverse().join('');

        if (a[i] != "")
        {
            if (a[i] == s)
            {
                s1 = a[i];
                break;
            }
        }
    }
    var ans = "";

    // Update the answer with
    // all strings of pair1
    for(var i = 0; i < r; i++)
    {
        ans = ans + pair1[i];
    }

    // Update the answer with
    // palindromic string s1
    if (s1 != "")
    {
        ans = ans + s1;
    }

    // Update the answer with
    // all strings of pair2
    for(var j = r - 1; j >= 0; j--)
    {
        ans = ans + pair2[j];
    }
    document.write(ans + "<br>");
}

// Driver Code
var a1 = [ "aba", "aba" ];
var n1 = a1.length;
longestPalindrome(a1, n1);

var a2 = [ "abc", "dba", "kop",
           "abd", "cba" ];
var n2 = a2.length;
longestPalindrome(a2, n2);

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
abaaba
abcdbaabdcba
```