# 每个字符的频率小于或等于 k 的最长子串

> 原文:[https://www . geesforgeks . org/最长-子串-频率-字符-减-等-k/](https://www.geeksforgeeks.org/longest-sub-string-frequency-character-less-equal-k/)

给定一根长度为 **n** 的绳子**绳子**。问题是找出每个字符的频率小于等于给定值 **k** 的**串**中最长子串的长度。
**举例:**

```
Input : str = "babcaag", k = 1
Output : 3
abc and bca are the two longest
sub-strings having frequency of each character 
in them less than equal to '1'.

Input : str = "geeksforgeeks", k = 2
Output : 10
```

**方法:**创建一个大小为 26 的数组 **freq[]** ，作为哈希表来存储**字符串**中每个字符的频率。用值“0”初始化其所有索引。弦长为 **n** 。现在实现下面的算法。

```
longSubstring(str, k)
    Initialize start = 0
    Initialize maxLen = 0
    Declare ch

    for i = 0 to n-1
        ch = str[i]
    freq[ch - 'a']++
    if k < freq[ch - 'a'] then
        if maxLen < (i - start) then
            maxLen = i - start
        while (k < freq[ch - 'a'])    
            freq[str[start] - 'a']--
        start++

    if maxLen < (n - start) then
        maxLen = n - start

    return maxLen
```

## C++

```
// C++ implementation to find
// the length of the longest
// substring having frequency
// of each character less
// than equal to k
#include <bits/stdc++.h>
using namespace std;

#define SIZE 26

// function to find the length
// of the longest substring
// having frequency of each
// character less than equal
// to k
int longSubstring(string str, int k)
{
    // hash table to store frequency
    // of each table
    int freq[SIZE];

    // Initialize
    memset(freq, 0, sizeof(freq));

    // 'start' index of the current
    // substring
    int start = 0;

    // to store the maximum length
    int maxLen = 0;
    char ch;

    int n = str.size();

    // traverse the string 'str'
    for (int i = 0; i < n; i++)
    {
        // get the current character
        // as 'ch'
        ch = str[i];

        // increase frequency of
        // 'ch' in 'freq[]'
        freq[ch - 'a']++;

        // if frequency of 'ch' becomes
        // more than 'k'
        if (freq[ch - 'a'] > k)
        {
            // update 'maxLen'
            if (maxLen < (i - start))
                maxLen = i - start;

            // decrease frequency of
            // each character as they
            // are encountered from
            // the 'start' index until
            // frequency of 'ch' is
            // greater than 'k'
            while (freq[ch - 'a'] > k)
            {

                // decrement frequency
                // by '1'
                freq[str[start] - 'a']--;

                // increment 'start'
                start++;
            }
        }
    }

    // update maxLen
    if (maxLen < (n - start))
        maxLen = n - start;

    // required length
    return maxLen;
}

// Driver program to test above
int main()
{
    string str = "babcaag";
    int k = 1;

    cout << "Length = "
        << longSubstring(str, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// the length of the longest
// substring having frequency
// of each character less
// than equal to k
import java.util.*;
import java.lang.*;

public class GfG{

    public final static int SIZE = 26;

    // function to find the length
    // of the longest substring
    // having frequency of each
    // character less than equal
    // to k
    public static int longSubstring(String str1,
                                           int k)
    {
        // hash table to store frequency
        // of each table
        int[] freq = new int [SIZE];

        char[] str = str1.toCharArray();

        // 'start' index of the current
        // substring
        int start = 0;

        // to store the maximum length
        int maxLen = 0;
        char ch;

        int n = str1.length();

        // traverse the string 'str'
        for (int i = 0; i < n; i++)
        {
            // get the current character
            // as 'ch'
            ch = str[i];

            // increase frequency of
            // 'ch' in 'freq[]'
            freq[ch - 'a']++;

            // if frequency of 'ch'
            // becomes more than 'k'
            if (freq[ch - 'a'] > k)
            {
                // update 'maxLen'
                if (maxLen < (i - start))
                    maxLen = i - start;

                // decrease frequency of
                // each character as they
                // are encountered from
                // the 'start' index until
                // frequency of 'ch' is
                // greater than 'k'
                while (freq[ch - 'a'] > k)
                {

                    // decrement frequency
                    // by '1'
                    freq[str[start] - 'a']--;

                    // increment 'start'
                    start++;
                }
            }
        }

        // update maxLen
        if (maxLen < (n - start))
            maxLen = n - start;

        // required length
        return maxLen;
    }

    // Driver function
    public static void main(String argc[])
    {
        String str = "babcaag";
        int k = 1;

        System.out.println("Length = " +
        longSubstring(str, k));
    }
}

/* This code is contributed by Sagar Shukla */
```

## 蟒蛇 3

```
# Python3 implementation to find
# the length of the longest
# substring having frequency
# of each character less than
# equal to k

# import library
import numpy as np

SIZE = 26

# Function to find the length
# of the longest sub having
# frequency of each character
# less than equal to k
def longSub(str, k):

    # Hash table to store frequency
    # of each table
    freq = np.zeros(26, dtype = np.int )

    # 'start' index of the
    # current substring
    start = 0

    # To store the maximum length
    maxLen = 0

    n = len(str)

    # Traverse the 'str'
    for i in range(0, n):

        # Get the current character
        # as 'ch'
        ch = str[i]

        # Increase frequency of
        # 'ch' in 'freq[]'
        freq[ord(ch) - ord('a') ] += 1

        # If frequency of 'ch'
        # becomes more than 'k'
        if (freq[ord(ch) - ord('a')] > k):
            # update 'maxLen'
            if (maxLen < (i - start)):
                maxLen = i - start

            # decrease frequency of
            # each character as they
            # are encountered from
            # the 'start' index until
            # frequency of 'ch' is
            # greater than 'k'
            while (freq[ord(ch) - ord('a')] > k):

                # decrement frequency
                # by '1'
                freq[ord(str[start]) - ord('a')] -= 1

                # increment 'start'
                start = start + 1

    # Update maxLen
    if (maxLen < (n - start)):
        maxLen = n - start

    # required length
    return maxLen;

# Driver Code
str = "babcaag"
k = 1

print ("Length =", longSub(str, k))

# This code is contributed by 'saloni1297'
```

## C#

```
// C# implementation to find
// the length of the longest
// substring having frequency
// of each character less
// than equal to k
using System;

class GfG{

    public static int SIZE = 26;

    // function to find the length
    // of the longest substring
    // having frequency of each
    // character less than equal
    // to k
    public static int longSubstring(String str1,
                                          int k)
    {
        // hash table to store
        // frequency of each table
        int []freq = new int [SIZE];

        char []str = str1.ToCharArray();

        // 'start' index of the
        // current substring
        int start = 0;

        // to store the maximum length
        int maxLen = 0;
        char ch;

        int n = str1.Length;

        // traverse the string 'str'
        for (int i = 0; i < n; i++)
        {
            // get the current character
            // as 'ch'
            ch = str[i];

            // increase frequency of
            // 'ch' in 'freq[]'
            freq[ch - 'a']++;

            // if frequency of 'ch'
            // becomes more than 'k'
            if (freq[ch - 'a'] > k)
            {
                // update 'maxLen'
                if (maxLen < (i - start))
                    maxLen = i - start;

                // decrease frequency of
                // each character as they
                // are encountered from
                // the 'start' index until
                // frequency of 'ch' is
                // greater than 'k'
                while (freq[ch - 'a'] > k)
                {
                    // decrement frequency
                    // by '1'
                    freq[str[start] - 'a']--;

                    // increment 'start'
                    start++;
                }
            }
        }

        // update maxLen
        if (maxLen < (n - start))
            maxLen = n - start;

        // required length
        return maxLen;
    }

    // Driver function
    public static void Main()
    {
        String str = "babcaag";
        int k = 1;

        Console.Write("Length = " +
                       longSubstring(str, k));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// the length of the longest
// sub$having frequency
// of each character less
// than equal to k
$SIZE = 26;

// function to find the length
// of the longest sub$
// having frequency of each
// character less than equal
// to k
function longSubstring($str, $k)
{
    global $SIZE;

    // hash table to
    // store frequency
    // of each table
    $freq = array();

    // Initialize
    for($i = 0; $i < $SIZE; $i++)
        $freq[$i] = 0;    

    // 'start' index of
    // the current substring
    $start = 0;

    // to store the
    // maximum length
    $maxLen = 0;
    $ch = '';

    $n = strlen($str);

    // traverse the {content}apos;str'
    for ($i = 0; $i < $n; $i++)
    {
        // get the current
        // character as 'ch'
        $ch = $str[$i];

        // increase frequency
        // of 'ch' in 'freq[]'
        $freq[ord($ch) -
              ord('a')]++;

        // if frequency of
        // 'ch' becomes
        // more than 'k'
        if ($freq[ord($ch) -
                  ord('a')] > $k)
        {
            // update 'maxLen'
            if ($maxLen < ($i - $start))
                $maxLen = $i - $start;

            // decrease frequency of
            // each character as they
            // are encountered from
            // the 'start' index until
            // frequency of 'ch' is
            // greater than 'k'
            while ($freq[ord($ch) -
                         ord('a')] > $k)
            {

                // decrement frequency
                // by '1'
                $freq[ord($str[$start]) -
                      ord('a')]--;

                // increment 'start'
                $start++;
            }
        }
    }

    // update maxLen
    if ($maxLen < ($n - $start))
        $maxLen = $n - $start;

    // required length
    return $maxLen;
}

// Driver Code
$str = "babcaag";
$k = 1;

echo ("Length = " .
       longSubstring($str, $k));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// JavaScript implementation to find
// the length of the longest
// substring having frequency
// of each character less
// than equal to k

var SIZE = 26;

// function to find the length
// of the longest substring
// having frequency of each
// character less than equal
// to k
function longSubstring(str, k)
{
    // hash table to store frequency
    // of each table
    var freq = Array(SIZE).fill(0);

    // 'start' index of the current
    // substring
    var start = 0;

    // to store the maximum length
    var maxLen = 0;
    var ch;

    var n = str.length;

    // traverse the string 'str'
    for (var i = 0; i < n; i++)
    {
        // get the current character
        // as 'ch'
        ch = str[i];

        // increase frequency of
        // 'ch' in 'freq[]'
        freq[ch.charCodeAt(0) -
        'a'.charCodeAt(0)]++;

        // if frequency of 'ch' becomes
        // more than 'k'
        if (freq[ch.charCodeAt(0) -
        'a'.charCodeAt(0)] > k)
        {
            // update 'maxLen'
            if (maxLen < (i - start))
                maxLen = i - start;

            // decrease frequency of
            // each character as they
            // are encountered from
            // the 'start' index until
            // frequency of 'ch' is
            // greater than 'k'
            while (freq[ch.charCodeAt(0) -
            'a'.charCodeAt(0)] > k)
            {

                // decrement frequency
                // by '1'
                freq[str[start].charCodeAt(0) -
                'a'.charCodeAt(0)]--;

                // increment 'start'
                start++;
            }
        }
    }

    // update maxLen
    if (maxLen < (n - start))
        maxLen = n - start;

    // required length
    return maxLen;
}

// Driver program to test above
var str = "babcaag";
var k = 1;
document.write( "Length = "
     + longSubstring(str, k));

</script>
```

**输出:**

```
Length = 3
```

**时间复杂度:** O(n)。
**辅助空间:** O(1)。
由于 while 循环，复杂性看起来可能是二次的，但是如果我们仔细观察内部 while 循环，它将只遍历字符串一次。”