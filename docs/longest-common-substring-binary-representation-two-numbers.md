# 两个数的二进制表示中最长的公共子串

> 原文:[https://www . geesforgeks . org/最长-公共-子串-二进制-表示-两个数字/](https://www.geeksforgeeks.org/longest-common-substring-binary-representation-two-numbers/)

给定两个整数 n 和 m，找出数字及其十进制值的二进制表示中最长的连续子集。
例 1:

```
Input : n = 10, m = 11
Output : 5
Explanation : Binary representation of 
10 -> 1010
11 -> 1011
longest common substring in both is 101
and decimal value of 101 is 5
```

示例 2:

```
Input : n = 8, m = 16
Output : 8
Explanation : Binary representation of 
8  -> 1000
16 -> 10000
longest common substring in both is 1000
and decimal value of 1000 is 8
```

示例 3:

```
Input : n = 0, m = 8
Output : 9
Explanation : Binary representation of 
0  -> 0
8 -> 1000
longest common substring in both is 0
and decimal value of 0 is 0
```

**问题来源:**[https://www . geeksforgeeks . org/Citrix-面试-体验-设置-5-校园/](https://www.geeksforgeeks.org/citrix-interview-experience-set-5-campus/)

**先决条件:**
1) [子串](https://www.geeksforgeeks.org/c-string-class-and-its-applications/) C++
2) [找到 C++](https://www.geeksforgeeks.org/stdfind-in-c/)
我们将给定的数字转换为它们的二进制表示，并将二进制表示存储在两个字符串中。一旦我们得到字符串，我们通过尝试从最大可能长度开始的所有长度子字符串来找到最长的公共子字符串。

## C++

```
// CPP program to find longest contiguous
// subset in binary representation of given
// two numbers n and m
#include <bits/stdc++.h>
using namespace std;

// utility function which returns
// decimal value of binary representation
int getDecimal(string s)
{
    int len = s.length();
    int ans = 0;
    int j = 0;
    for (int i = len - 1; i >= 0; i--)
    {
        if (s[i] == '1')
            ans += pow(2, j);
        j += 1;
    }
    return ans;
}

// Utility function which convert decimal
// number to its binary representation
string convertToBinary(int n)
{
    string temp;
    while (n > 0)
    {
        int rem = n % 2;
        temp.push_back(48 + rem);
        n = n / 2;
    }
    reverse(temp.begin(), temp.end());
    return temp;
}

// utility function to check all the
// substrings and get the longest substring.
int longestCommon(int n, int m)
{
    int mx = -INT_MAX; // maximum length
    string s1 = convertToBinary(n);
    string s2 = convertToBinary(m);

    string res; // final resultant string
    int len = s1.length();
    int l = len;

    // for every substring of s1,
    // check if its length is greater than
    // previously found string
    // and also it is present in string s2
    while (len > 0)
    {
        for (int i = 0; i < l - len + 1; i++)
        {
            string temp = s1.substr(i, len);

            int tlen = temp.length();
            if (tlen > mx && s2.find(temp) != string::npos)
            {
                res = temp;
                mx = tlen;
            }
        }
        len = len - 1;
    }

    // If there is no common string
    if (res == "")
        return -1;

    return getDecimal(res);
}

// driver program
int main()
{
    int n = 10, m = 11;
    cout << "longest common decimal value : "
         << longestCommon(m, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest contiguous
// subset in binary representation of given
// two numbers n and m
public class GFG
{   
    // utility function to check all the
    // substrings and get the longest substring.
    static int longestCommon(int n, int m)
    {
        int mx = -Integer.MAX_VALUE; // maximum length
        String s1 = Integer.toBinaryString(n);
        String s2 = Integer.toBinaryString(m);

        String res = null;  // final resultant string
        int len = s1.length();
        int l = len;

        // for every substring of s1,
        // check if its length is greater than
        // previously found string
        // and also it is present in string s2
        while (len > 0)
        {
            for (int i = 0; i < l - len + 1; i++)
            {
                String temp = s1.substring(i, i + len);

                int tlen = temp.length();
                if (tlen > mx && s2.contains(temp))
                {
                    res = temp;
                    mx = tlen;
                }
            }

            len = len - 1;
        }

        // If there is no common string
        if(res == "")
            return -1;

        return Integer.parseInt(res,2);
    }

    // driver program to test above function
    public static void main(String[] args)
    {
        int n = 10;
        int m = 11;
        System.out.println("Longest common decimal value : "
                            +longestCommon(m, n));
    }
}

// This code is Contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to find longest contiguous
# subset in binary representation of given
# two numbers n and m

# utility function which returns
# decimal value of binary representation
def getDecimal(s):
    lenn = len(s)
    ans = 0
    j = 0
    for i in range(lenn - 1, -1, -1):
        if (s[i] == '1'):
            ans += pow(2, j)
        j += 1
    return ans

# Utility function which convert decimal
# number to its binary representation
def convertToBinary(n):

    return bin(n)[2:]

# utility function to check all the
# substrings and get the longest substring.
def longestCommon(n, m):
    mx = -10**9 # maximum length
    s1 = convertToBinary(n)
    s2 = convertToBinary(m)
    #print(s1,s2)

    res="" # final resultant string
    lenn = len(s1)
    l = lenn

    # for every subof s1,
    # check if its length is greater than
    # previously found string
    # and also it is present in s2
    while (lenn > 0):

        for i in range(l - lenn + 1):

            temp = s1[i:lenn + 1]
            # print(temp)

            tlenn = len(temp)

            if (tlenn > mx and( s2.find(temp) != -1)):
                res = temp
                mx = tlenn

        lenn = lenn - 1

    # If there is no common string
    if (res == ""):
        return -1

    return getDecimal(res)

# Driver Code
n = 10
m = 11
print("longest common decimal value : ",
                    longestCommon(m, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find longest contiguous
// subset in binary representation of given
// two numbers n and m
using System;
using System.Collections.Generic;

class GFG
{
    // utility function to check all the
    // substrings and get the longest substring.
    static int longestCommon(int n, int m)
    {
        int mx = -int.MaxValue; // maximum length
        String s1 = Convert.ToString(n, 2);
        String s2 = Convert.ToString(m, 2);;

        String res = null; // final resultant string
        int len = s1.Length;
        int l = len;

        // for every substring of s1,
        // check if its length is greater than
        // previously found string
        // and also it is present in string s2
        while (len > 0)
        {
            for (int i = 0; i < l - len + 1; i++)
            {
                String temp = s1.Substring(i, len);

                int tlen = temp.Length;
                if (tlen > mx && s2.Contains(temp))
                {
                    res = temp;
                    mx = tlen;
                }
            }

            len = len - 1;
        }

        // If there is no common string
        if(res == "")
            return -1;

        return Convert.ToInt32(res, 2);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 10;
        int m = 11;
        Console.WriteLine("Longest common decimal value : "
                            +longestCommon(m, n));
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find longest contiguous
// subset in binary representation of given
// two numbers n and m

    // utility function to check all the
    // substrings and get the longest substring.
    function longestCommon(n,m)
    {
        let mx = -Number.MAX_VALUE; // maximum length
        let s1 = (n >>> 0).toString(2);
        let s2 = (m >>> 0).toString(2);

        let res = null;  // final resultant string
        let len = s1.length;
        let l = len;

        // for every substring of s1,
        // check if its length is greater than
        // previously found string
        // and also it is present in string s2
        while (len > 0)
        {
            for (let i = 0; i < l - len + 1; i++)
            {
                let temp = s1.substring(i, i + len);

                let tlen = temp.length;
                if (tlen > mx && s2.includes(temp))
                {
                    res = temp;
                    mx = tlen;
                }
            }

            len = len - 1;
        }

        // If there is no common string
        if(res == "")
            return -1;

        return parseInt(res, 2);
    }

    // driver program to test above function
    let n = 10;
    let m = 11;
    document.write("Longest common decimal value : "
                            +longestCommon(m, n));

// This code is contributed by unknown2108

</script>
```

**输出:**

```
longest common decimal value : 5
```

**对上述方法的优化:**
上述解决方案可以通过以下帖子中讨论的方法进行优化:
[动态规划|集合 29(最长公共子串)](https://www.geeksforgeeks.org/longest-common-substring/)
本文由 [**曼德普·辛格**](https://github.com/msdeep14) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。