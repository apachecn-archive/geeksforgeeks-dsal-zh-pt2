# 统计一个字符串中的特殊回文

> 原文:[https://www . geesforgeks . org/count-special-回文串/](https://www.geeksforgeeks.org/count-special-palindromes-in-a-string/)

给定一个字符串，计算所有大小大于 1 的特殊回文子字符串。如果子串中的所有字符都相同，或者只有中间字符在奇数长度上不同，则子串被称为特殊回文子串。例“aabaa”和“aaa”是特殊回文子串，“abcba”不是特殊回文子串。
**例:**

```
Input :  str = " abab"
Output : 2
All Special Palindromic  substring are: "aba", "bab"

Input : str = "aabbb"
Output : 4
All Special substring are: "aa", "bb", "bbb", "bb"
```

**简单的解决方法**就是我们简单的逐个生成所有的子串，统计有多少子串是特殊回文子串。该解决方案需要 0(n<sup>3</sup>时间。
**高效解决方案**
有 2 种情况:
**情况 1:** 所有回文子串都具有相同的字符:
我们可以通过简单地计算相同的连续字符并使用公式 K*(K+1)/2(可能的子串总数:这里 K 是连续相同字符的计数)来处理这种情况。

```
 Lets Str = "aaabba"
 Traverse string from left to right and Count of same char
  "aaabba"  =  3, 2, 1
   for "aaa" : total substring possible are
   'aa' 'aa', 'aaa', 'a', 'a', 'a'  : 3(3+1)/2 = 6 
   "bb" : 'b', 'b', 'bb' : 2(2+1)/2 = 3
   'a'  : 'a' : 1(1+1)/2 = 1 
```

**情况 2:**
我们可以通过将相同字符的计数存储在另一个名为“sameChar[n]”的大小为 n 的临时数组中来处理这种情况。逐个挑选每个字符，并检查其前一个字符和前一个字符是否相等。如果相等，则 ( sameChar[previous]，sameChar[forward])子字符串之间可能存在**min _ in。** 

```
Let's Str = "aabaaab"
 Count of smiler char from left to right :
 that we will store in Temporary array "sameChar"
  Str         =    " a a b a a a b "
sameChar[]  =      2 2 1 3 3 3 1
According to the problem statement middle character is different:
so we have only left with char "b" at index :2 ( index from 0 to n-1)
substring : "aabaaa"
so only two substring are possible : "aabaa", "aba"
that is min (smilerChar[index-1], smilerChar[index+1] ) that is 2.
```

以下是以上想法的实现

## C++

```
// C++ program to count special Palindromic substring
#include <bits/stdc++.h>
using namespace std;

// Function to count special Palindromic susbstring
int CountSpecialPalindrome(string str)
{
    int n = str.length();

    // store count of special Palindromic substring
    int result = 0;

    // it will store the count of continues same char
    int sameChar[n] = { 0 };

    int i = 0;

    // traverse string character from left to right
    while (i < n) {

        // store same character count
        int sameCharCount = 1;

        int j = i + 1;

        // count smiler character
        while (str[i] == str[j] && j < n)
            sameCharCount++, j++;

        // Case : 1
        // so total number of substring that we can
        // generate are : K *( K + 1 ) / 2
        // here K is sameCharCount
        result += (sameCharCount * (sameCharCount + 1) / 2);

        // store current same char count in sameChar[]
        // array
        sameChar[i] = sameCharCount;

        // increment i
        i = j;
    }

    // Case 2: Count all odd length Special Palindromic
    // substring
    for (int j = 1; j < n; j++)
    {
        // if current character is equal to previous
        // one then we assign Previous same character
        // count to current one
        if (str[j] == str[j - 1])
            sameChar[j] = sameChar[j - 1];

        // case 2: odd length
        if (j > 0 && j < (n - 1) &&
            (str[j - 1] == str[j + 1] &&
             str[j] != str[j - 1]))
            result += min(sameChar[j - 1],
                          sameChar[j + 1]);
    }

    // subtract all single length substring
    return result - n;
}

// driver program to test above fun
int main()
{
    string str = "abccba";
    cout << CountSpecialPalindrome(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count special
// Palindromic substring
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG
{

// Function to count special
// Palindromic susbstring
public static int CountSpecialPalindrome(String str)
{
    int n = str.length();

    // store count of special
    // Palindromic substring
    int result = 0;

    // it will store the count
    // of continues same char
    int[] sameChar = new int[n];
    for(int v = 0; v < n; v++)
    sameChar[v] = 0;

    int i = 0;

    // traverse string character
    // from left to right
    while (i < n)
    {

        // store same character count
        int sameCharCount = 1;

        int j = i + 1;

        // count smiler character
        while (j < n &&
            str.charAt(i) == str.charAt(j))
        {
            sameCharCount++;
            j++;
        }

        // Case : 1
        // so total number of
        // substring that we can
        // generate are : K *( K + 1 ) / 2
        // here K is sameCharCount
        result += (sameCharCount *
                  (sameCharCount + 1) / 2);

        // store current same char
        // count in sameChar[] array
        sameChar[i] = sameCharCount;

        // increment i
        i = j;
    }

    // Case 2: Count all odd length
    //           Special Palindromic
    //           substring
    for (int j = 1; j < n; j++)
    {
        // if current character is
        // equal to previous one
        // then we assign Previous
        // same character count to
        // current one
        if (str.charAt(j) == str.charAt(j - 1))
            sameChar[j] = sameChar[j - 1];

        // case 2: odd length
        if (j > 0 && j < (n - 1) &&
        (str.charAt(j - 1) == str.charAt(j + 1) &&
             str.charAt(j) != str.charAt(j - 1)))
            result += Math.min(sameChar[j - 1],
                               sameChar[j + 1]);
    }

    // subtract all single
    // length substring
    return result - n;
}

// Driver code
public static void main(String args[])
{
    String str = "abccba";
    System.out.print(CountSpecialPalindrome(str));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python3 program to count special
# Palindromic substring

# Function to count special
# Palindromic susbstring
def CountSpecialPalindrome(str):
    n = len(str);

    # store count of special
    # Palindromic substring
    result = 0;

    # it will store the count
    # of continues same char
    sameChar=[0] * n;

    i = 0;

    # traverse string character
    # from left to right
    while (i < n):

        # store same character count
        sameCharCount = 1;

        j = i + 1;

        # count smiler character
        while (j < n):
            if(str[i] != str[j]):
                break;
            sameCharCount += 1;
            j += 1;

        # Case : 1
        # so total number of substring
        # that we can generate are :
        # K *( K + 1 ) / 2
        # here K is sameCharCount
        result += int(sameCharCount *
                     (sameCharCount + 1) / 2);

        # store current same char
        # count in sameChar[] array
        sameChar[i] = sameCharCount;

        # increment i
        i = j;

    # Case 2: Count all odd length
    # Special Palindromic substring
    for j in range(1, n):

        # if current character is equal
        # to previous one then we assign
        # Previous same character count
        # to current one
        if (str[j] == str[j - 1]):
            sameChar[j] = sameChar[j - 1];

        # case 2: odd length
        if (j > 0 and j < (n - 1) and
           (str[j - 1] == str[j + 1] and
            str[j] != str[j - 1])):
            result += (sameChar[j - 1]
                    if(sameChar[j - 1] < sameChar[j + 1])
                    else sameChar[j + 1]);

    # subtract all single
    # length substring
    return result-n;

# Driver Code
str = "abccba";
print(CountSpecialPalindrome(str));

# This code is contributed by mits.
```

## C#

```
// C# program to count special
// Palindromic substring
using System;

class GFG
{

// Function to count special
// Palindromic susbstring
public static int CountSpecialPalindrome(String str)
{
    int n = str.Length;

    // store count of special
    // Palindromic substring
    int result = 0;

    // it will store the count
    // of continues same char
    int[] sameChar = new int[n];
    for(int v = 0; v < n; v++)
    sameChar[v] = 0;

    int i = 0;

    // traverse string character
    // from left to right
    while (i < n)
    {

        // store same character count
        int sameCharCount = 1;

        int j = i + 1;

        // count smiler character
        while (j < n &&
               str[i] == str[j])
        {
            sameCharCount++;
            j++;
        }

        // Case : 1
        // so total number of
        // substring that we can
        // generate are : K *( K + 1 ) / 2
        // here K is sameCharCount
        result += (sameCharCount *
                  (sameCharCount + 1) / 2);

        // store current same char
        // count in sameChar[] array
        sameChar[i] = sameCharCount;

        // increment i
        i = j;
    }

    // Case 2: Count all odd length
    //         Special Palindromic
    //         substring
    for (int j = 1; j < n; j++)
    {
        // if current character is
        // equal to previous one
        // then we assign Previous
        // same character count to
        // current one
        if (str[j] == str[j - 1])
            sameChar[j] = sameChar[j - 1];

        // case 2: odd length
        if (j > 0 && j < (n - 1) &&
           (str[j - 1] == str[j + 1] &&
            str[j] != str[j - 1]))
            result += Math.Min(sameChar[j - 1],
                              sameChar[j + 1]);
    }

    // subtract all single
    // length substring
    return result - n;
}

// Driver code
public static void Main()
{
    String str = "abccba";
    Console.Write(CountSpecialPalindrome(str));
}
}

// This code is contributed by mits.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count special
// Palindromic substring

// Function to count special
// Palindromic susbstring
function CountSpecialPalindrome($str)
{
    $n = strlen($str);

    // store count of special
    // Palindromic substring
    $result = 0;

    // it will store the count
    // of continues same char
    $sameChar=array_fill(0, $n, 0);

    $i = 0;

    // traverse string character
    // from left to right
    while ($i < $n)
    {

        // store same character count
        $sameCharCount = 1;

        $j = $i + 1;

        // count smiler character
        while ($j < $n)
        {
            if($str[$i] != $str[$j])
            break;
            $sameCharCount++;
            $j++;
        }

        // Case : 1
        // so total number of substring
        // that we can generate are :
        // K *( K + 1 ) / 2
        // here K is sameCharCount
        $result += (int)($sameCharCount *
                        ($sameCharCount + 1) / 2);

        // store current same char
        // count in sameChar[] array
        $sameChar[$i] = $sameCharCount;

        // increment i
        $i = $j;
    }

    // Case 2: Count all odd length
    // Special Palindromic substring
    for ($j = 1; $j < $n; $j++)
    {
        // if current character is equal
        // to previous one then we assign
        // Previous same character count
        // to current one
        if ($str[$j] == $str[$j - 1])
            $sameChar[$j] = $sameChar[$j - 1];

        // case 2: odd length
        if ($j > 0 && $j < ($n - 1) &&
            ($str[$j - 1] == $str[$j + 1] &&
                $str[$j] != $str[$j - 1]))
            $result += $sameChar[$j - 1] <
                       $sameChar[$j + 1] ?
                       $sameChar[$j - 1] :
                       $sameChar[$j + 1];
    }

    // subtract all single
    // length substring
    return $result - $n;
}

// Driver Code
$str = "abccba";
echo CountSpecialPalindrome($str);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>
      // JavaScript program to count special Palindromic substring

      // Function to count special Palindromic susbstring
      function CountSpecialPalindrome(str) {
        var n = str.length;

        // store count of special Palindromic substring
        var result = 0;

        // it will store the count of continues same char
        var sameChar = [...Array(n)];

        var i = 0;

        // traverse string character from left to right
        while (i < n) {
          // store same character count
          var sameCharCount = 1;

          var j = i + 1;

          // count smiler character
          while (str[i] == str[j] && j < n) sameCharCount++, j++;

          // Case : 1
          // so total number of substring that we can
          // generate are : K *( K + 1 ) / 2
          // here K is sameCharCount
          result += (sameCharCount * (sameCharCount + 1)) / 2;

          // store current same char count in sameChar[]
          // array
          sameChar[i] = sameCharCount;

          // increment i
          i = j;
        }

        // Case 2: Count all odd length Special Palindromic
        // substring
        for (var j = 1; j < n; j++) {
          // if current character is equal to previous
          // one then we assign Previous same character
          // count to current one
          if (str[j] == str[j - 1]) sameChar[j] = sameChar[j - 1];

          // case 2: odd length
          if (
            j > 0 &&
            j < n - 1 &&
            str[j - 1] == str[j + 1] &&
            str[j] != str[j - 1]
          )
            result += Math.min(sameChar[j - 1], sameChar[j + 1]);
        }

        // subtract all single length substring
        return result - n;
      }

      // driver program to test above fun
      var str = "abccba";
      document.write(CountSpecialPalindrome(str) + "<br>");
    </script>
```

**输出:**

```
1
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)