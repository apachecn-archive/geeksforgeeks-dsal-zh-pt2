# 串联二进制字符串中最大连续零数

> 原文:[https://www . geeksforgeeks . org/最大连续零串联二进制字符串/](https://www.geeksforgeeks.org/maximum-consecutive-zeroes-in-concatenated-binary-string/)

给你一个长度为 **n** 的二进制字符串 **str** 。假设您通过将字符串的 **k** 个副本连接在一起，创建了另一个大小为 n * k 的字符串。仅由 0 组成的串联字符串的子字符串的最大大小是多少？给定 k > 1。

**示例:**

> 输入:str = "110010 "，k = 2
> 输出:2
> 字符串经过两次串接后变成 110010110010。这个字符串有两个零。
> 
> 输入:str = "00100110 "，k = 4
> 输出:3

如果给定的字符串包含全零，则答案为 n * k。如果 S 包含 1，则答案为仅包含零的字符串的子字符串的最大长度，或者仅包含零的字符串的最大前缀的长度与仅包含零的字符串的最大后缀的长度之和。只有当 k > 1 时，才能计算最后一个。

## C++

```
// C++ program to find maximum number 
// of consecutive zeroes after 
// concatenating a binary string
#include<bits/stdc++.h>
using namespace std;

// returns the maximum size of a 
// substring consisting only of 
// zeroes after k concatenation
int max_length_substring(string st, 
                         int n, int k)
{

    // stores the maximum length 
    // of the required substring
    int max_len = 0;

    int len = 0;
    for (int i = 0; i < n; ++i) 
    {

        // if the current character is 0
        if (st[i] == '0')
            len++;
        else
            len = 0;

        // stores maximum length of current
        // substrings with zeroes
        max_len = max(max_len, len);
    }

    // if the whole string is
    // filled with zero
    if (max_len == n)
        return n * k;

    int pref = 0, suff = 0;

    // computes the length of the maximal
    // prefix which contains only zeroes
    for (int i = 0; st[i] == '0';
                    ++i, ++pref);

    // computes the length of the maximal 
    // suffix which contains only zeroes
    for (int i = n - 1; st[i] == '0'; 
                        --i, ++suff);

    // if more than 1 concatenations
    // are to be made
    if (k > 1)
        max_len = max(max_len, 
                 pref + suff);

    return max_len;
}

// Driver code
int main()
{
    int n = 6;
    int k = 3;
    string st = "110010";
    int ans = max_length_substring(st, n, k);

    cout << ans;
}

// This code is contributed by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum number of
// consecutive zeroes after concatenating
// a binary string

class GFG {

    // returns the maximum size of a substring
    // consisting only of zeroes
    // after k concatenation
    static int max_length_substring(String st,
                                    int n, int k)
    {

        // stores the maximum length of the
        // required substring
        int max_len = 0;

        int len = 0;
        for (int i = 0; i < n; ++i) {

            // if the current character is 0
            if (st.charAt(i) == '0')
                len++;
            else
                len = 0;

            // stores maximum length of current
            // substrings with zeroes
            max_len = Math.max(max_len, len);
        }

        // if the whole string is filled with zero
        if (max_len == n)
            return n * k;

        int pref = 0, suff = 0;

        // computes the length of the maximal
        // prefix which contains only zeroes
        for (int i = 0; st.charAt(i) == '0'; ++i, ++pref)
            ;

        // computes the length of the maximal 
        // suffix which contains only zeroes
        for (int i = n - 1; st.charAt(i) == '0'; --i, ++suff)
            ;

        // if more than 1 concatenations are to be made
        if (k > 1)
            max_len = Math.max(max_len, pref + suff);

        return max_len;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 6;
        int k = 3;
        String st = "110010";
        int ans = max_length_substring(st, n, k);

        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find maximum 
# number of consecutive zeroes 
# after concatenating a binary string

# returns the maximum size of a 
# substring consisting only of 
# zeroes after k concatenation
def max_length_substring(st, n, k):

    # stores the maximum length 
    # of the required substring
    max_len = 0

    len = 0
    for i in range(0, n):

        # if the current character is 0
        if (st[i] == '0'):
            len = len + 1;
        else:
            len = 0

        # stores maximum length of 
        # current substrings with zeroes
        max_len = max(max_len, len)

    # if the whole is filled 
    # with zero
    if (max_len == n):
        return n * k

    pref = 0
    suff = 0

    # computes the length of the maximal
    # prefix which contains only zeroes
    i = 0
    while(st[i] == '0'):
        i = i + 1
        pref = pref + 1

    # computes the length of the maximal 
    # suffix which contains only zeroes
    i = n - 1
    while(st[i] == '0'):
        i = i - 1
        suff = suff + 1

    # if more than 1 concatenations 
    # are to be made
    if (k > 1):
        max_len = max(max_len, 
                      pref + suff)

    return max_len

# Driver code
n = 6
k = 3
st = "110010"
ans = max_length_substring(st, n, k)

print(ans)

# This code is contributed by ihritik
```

## C#

```
// C# program to find maximum number 
// of consecutive zeroes after 
// concatenating a binary string
using System;

class GFG 
{

// returns the maximum size of 
// a substring consisting only 
// of zeroes after k concatenation
static int max_length_substring(string st,
                                int n, int k)
{

    // stores the maximum length 
    // of the required substring
    int max_len = 0;

    int len = 0;
    for (int i = 0; i < n; ++i) 
    {

        // if the current character is 0
        if (st[i] == '0')
            len++;
        else
            len = 0;

        // stores maximum length of current
        // substrings with zeroes
        max_len = Math.Max(max_len, len);
    }

    // if the whole string is 
    // filled with zero
    if (max_len == n)
        return n * k;

    int pref = 0, suff = 0;

    // computes the length of the maximal
    // prefix which contains only zeroes
    for (int i = 0; st[i] == '0'; 
                    ++i, ++pref);

    // computes the length of the maximal 
    // suffix which contains only zeroes
    for (int i = n - 1; st[i] == '0';
                        --i, ++suff);

    // if more than 1 concatenations 
    // are to be made
    if (k > 1)
        max_len = Math.Max(max_len, 
                           pref + suff);

    return max_len;
}

// Driver code
public static void Main(string[] args)
{
    int n = 6;
    int k = 3;
    string st = "110010";
    int ans = max_length_substring(st, n, k);

    Console.WriteLine(ans);
}
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum number 
// of consecutive zeroes after 
// concatenating a binary string

// returns the maximum size of a 
// substring consisting only of 
// zeroes after k concatenation
function max_length_substring($st, $n, $k)
{

    // stores the maximum length 
    // of the required substring
    $max_len = 0;

    $len = 0;
    for ($i = 0; $i < $n; ++$i) 
    {

        // if the current character is 0
        if ($st[$i] == '0')
            $len++;
        else
            $len = 0;

        // stores maximum length of 
        // current substrings with zeroes
        $max_len = max($max_len, $len);
    }

    // if the whole $is filled
    // with zero
    if ($max_len == $n)
        return $n * $k;

    $pref = 0;
    $suff = 0;

    // computes the length of the maximal
    // prefix which contains only zeroes
    for ($i = 0; $st[$i] == '0'; 
                 ++$i, ++$pref);

    // computes the length of the maximal 
    // suffix which contains only zeroes
    for ($i = $n - 1; $st[$i] == '0'; 
                      --$i, ++$suff);

    // if more than 1 concatenations 
    // are to be made
    if ($k > 1)
        $max_len = max($max_len, 
                       $pref + $suff);

    return $max_len;
}

// Driver code
$n = 6;
$k = 3;
$st = "110010";
$ans = max_length_substring($st, $n, $k);

echo $ans;

// This code is contributed by ihritik
?>
```

**Output:**

```
2

```