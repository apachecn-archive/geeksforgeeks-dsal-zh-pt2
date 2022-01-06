# 最长常见字谜子序列

> 原文:[https://www . geesforgeks . org/long-common-anagram-subsequel/](https://www.geeksforgeeks.org/longest-common-anagram-subsequence/)

分别给定长度为 **n1** 和 **n2** 的两根弦 **str1** 和 **str2** 。问题是找到最长子序列的长度，它以字谜的形式出现在两个字符串中。
**注意:**字符串只包含小写字母。
**举例:**

```
Input : str1 = "abdacp", str2 = "ckamb"
Output : 3
Subsequence of str1 = abc
Subsequence of str2 = cab
          OR
Subsequence of str1 = bac
Subsequence of str2 = cab

These are longest common anagram subsequences.

Input : str1 = "abbcfke", str2 = "fbaafbly"
Output : 4
```

**方法:**创建两个哈希表，比如 **freq1** 和 **freq2** 。将 **str1** 每个字符的频率存储在 **freq1** 中。同样，将 **str2** 的每个字符的频率存储在 **freq2** 中。初始化**镜头** = 0。现在，对于每个小写字母，从两个哈希表中找到它的最低频率，并将其累积到 **len** 。

## C++

```
// C++ implementation to find the length of the
// longest common anagram subsequence
#include <bits/stdc++.h>

using namespace std;

#define SIZE 26

// function to find the length of the
// longest common anagram subsequence
int longCommomAnagramSubseq(char str1[], char str2[],
                                int n1, int n2)
{
    // hash tables for storing frequencies of
    // each character
    int freq1[SIZE], freq2[SIZE];
    memset(freq1, 0, sizeof(freq1));
    memset(freq2, 0, sizeof(freq2));

    int len = 0;

    // calculate frequency of each character
    // of 'str1[]'
    for (int i = 0; i < n1; i++)
        freq1[str1[i] - 'a']++;

    // calculate frequency of each character
    // of 'str2[]'
    for (int i = 0; i < n2; i++)   
        freq2[str2[i] - 'a']++;

    // for each character add its minimum frequency
    // out of the two strings in 'len'
    for (int i = 0; i < SIZE; i++)   
        len += min(freq1[i], freq2[i]);

    // required length
    return len;   
}                               

// Driver program to test above
int main()
{
    char str1[] = "abdacp";
    char str2[] = "ckamb";
    int n1 = strlen(str1);
    int n2 = strlen(str2);
    cout << "Length = "
         << longCommomAnagramSubseq(str1, str2, n1, n2);
    return 0;    
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// the length() of the longest
// common anagram subsequence
import java.io.*;

class GFG
{
    static int SIZE = 26;

    // function to find the
    // length() of the longest
    // common anagram subsequence
    static int longCommomAnagramSubseq(String str1,
                                       String str2,
                                       int n1, int n2)
    {
        // hash tables for
        // storing frequencies
        // of each character
        int []freq1 = new int[SIZE];
        int []freq2 = new int[SIZE];

        for(int i = 0; i < SIZE; i++)
        {
            freq1[i] = 0;
            freq2[i] = 0;
        }

        int len = 0;

        // calculate frequency
        // of each character of
        // 'str1[]'
        for (int i = 0; i < n1; i++)
            freq1[(int)str1.charAt(i) - (int)'a']++;

        // calculate frequency
        // of each character
        // of 'str2[]'
        for (int i = 0; i < n2; i++)
            freq2[(int)str2.charAt(i) - (int)'a']++;

        // for each character add
        // its minimum frequency
        // out of the two Strings
        // in 'len'
        for (int i = 0; i < SIZE; i++)
            len += Math.min(freq1[i],
                            freq2[i]);

        // required length()
        return len;
    }                            

    // Driver Code
    public static void main(String args[])
    {
        String str1 = "abdacp";
        String str2 = "ckamb";
        int n1 = str1.length();
        int n2 = str2.length();
        System.out.print("Length = " +
                longCommomAnagramSubseq(str1, str2,
                                          n1, n2));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python 3 implementation to find
# the length of the longest common
# anagram subsequence

SIZE = 26

# function to find the length of the
# longest common anagram subsequence
def longCommomAnagramSubseq(str1, str2,
                                n1, n2):

    # List for storing frequencies
    # of each character
    freq1 = [0] * SIZE
    freq2 = [0] * SIZE

    l = 0

    # calculate frequency of each
    # character of 'str1[]'
    for i in range(n1):
        freq1[ord(str1[i]) -
              ord('a')] += 1

    # calculate frequency of each
    # character of 'str2[]'
    for i in range(n2) :
        freq2[ord(str2[i]) -
              ord('a')] += 1

    # for each character add its
    # minimum frequency out of
    # the two strings in 'len'
    for i in range(SIZE):
        l += min(freq1[i], freq2[i])

    # required length
    return l                            

# Driver Code
if __name__ == "__main__":

    str1 = "abdacp"
    str2 = "ckamb"
    n1 = len(str1)
    n2 = len(str2)
    print("Length = ",
           longCommomAnagramSubseq(str1, str2,
                                       n1, n2))

# This code is contributed by ita_c
```

## C#

```
// C# implementation to find
// the length of the longest
// common anagram subsequence
using System;

class GFG
{
    static int SIZE = 26;

    // function to find the
    // length of the longest
    // common anagram subsequence
    static int longCommomAnagramSubseq(string str1,
                                       string str2,
                                       int n1, int n2)
    {
        // hash tables for
        // storing frequencies
        // of each character
        int []freq1 = new int[SIZE];
        int []freq2 = new int[SIZE];

        for(int i = 0; i < SIZE; i++)
        {
            freq1[i] = 0;
            freq2[i] = 0;
        }

        int len = 0;

        // calculate frequency
        // of each character of
        // 'str1[]'
        for (int i = 0; i < n1; i++)
            freq1[str1[i] - 'a']++;

        // calculate frequency
        // of each character
        // of 'str2[]'
        for (int i = 0; i < n2; i++)
            freq2[str2[i] - 'a']++;

        // for each character add
        // its minimum frequency
        // out of the two strings
        // in 'len'
        for (int i = 0; i < SIZE; i++)
            len += Math.Min(freq1[i],
                            freq2[i]);

        // required length
        return len;
    }                            

    // Driver Code
    static void Main()
    {
        string str1 = "abdacp";
        string str2 = "ckamb";
        int n1 = str1.Length;
        int n2 = str2.Length;
        Console.Write("Length = " +
                longCommomAnagramSubseq(str1, str2,
                                        n1, n2));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// the length of the longest
// common anagram subsequence
$SIZE = 26;

// function to find the
// length of the longest
// common anagram subsequence
function longCommomAnagramSubseq($str1, $str2,
                                 $n1, $n2)
{
    global $SIZE;

    // hash tables for storing
    // frequencies of each character
    $freq1 = array();
    $freq2 = array();
    for($i = 0;
        $i < $SIZE; $i++)    
    {
        $freq1[$i] = 0;
        $freq2[$i] = 0;
    }
    $len = 0;

    // calculate frequency of
    // each character of 'str1'
    for ($i = 0; $i < $n1; $i++)
        $freq1[ord($str1[$i]) -
               ord('a')]++;

    // calculate frequency of
    // each character of 'str2'
    for ($i = 0; $i < $n2; $i++)
        $freq2[ord($str2[$i]) -
               ord('a')]++;

    // for each character add
    // its minimum frequency
    // out of the two strings
    // in 'len'
    for ($i = 0; $i < $SIZE; $i++)
    {
        $len += min($freq1[$i],
                    $freq2[$i]);
    }

    // required length
    return $len;
}                            

// Driver Code
$str1 = "abdacp";
$str2 = "ckamb";
$n1 = strlen($str1);
$n2 = strlen($str2);
echo ("Length = " .
      longCommomAnagramSubseq($str1, $str2,
                              $n1, $n2));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>
// Javascript implementation to find
// the length() of the longest
// common anagram subsequence

    let SIZE = 26;
    // function to find the
    // length() of the longest
    // common anagram subsequence
    function longCommomAnagramSubseq(str1,str2,n1,n2)
    {
        // hash tables for
        // storing frequencies
        // of each character
        let freq1 = new Array(SIZE);
        let freq2 = new Array(SIZE);

        for(let i = 0; i < SIZE; i++)
        {
            freq1[i] = 0;
            freq2[i] = 0;
        }

        let len = 0;

        // calculate frequency
        // of each character of
        // 'str1[]'
        for (let i = 0; i < n1; i++)
            freq1[str1[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

        // calculate frequency
        // of each character
        // of 'str2[]'
        for (let i = 0; i < n2; i++)
            freq2[str2[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

        // for each character add
        // its minimum frequency
        // out of the two Strings
        // in 'len'
        for (let i = 0; i < SIZE; i++)
            len += Math.min(freq1[i],
                            freq2[i]);

        // required length()
        return len;
    }

    // Driver Code
    let str1 = "abdacp";
    let str2 = "ckamb";
    let n1 = str1.length;
    let n2 = str2.length;
    document.write("Length = " +
                longCommomAnagramSubseq(str1, str2,
                                          n1, n2));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
Length = 3
```

**时间复杂度:** O(n+m)。
**辅助空间:** O(1)。