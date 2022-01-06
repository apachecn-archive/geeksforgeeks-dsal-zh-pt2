# 统计第一串中的子序列，它们是第二串的字谜

> 原文:[https://www . geesforgeks . org/count-subseries-first-string-anagrams-second-string/](https://www.geeksforgeeks.org/count-subsequences-first-string-anagrams-second-string/)

分别给定长度为 **n1** 和 **n2** 的两根弦 **str1** 和 **str2** 。问题是统计 **str1** 的所有子序列，它们是 **str2** 的字谜。
**示例:**

```
Input : str1 = "abacd", str2 = "abc"
Output : 2
Index of characters in the 2 subsequences are:
{0, 1, 3} = {a, b, c} = abc and
{1, 2, 3} = {b, a, c} = bac
The above two subsequences of str1 
are anagrams of str2.

Input : str1 = "geeksforgeeks", str2 = "geeks" 
Output : 48
```

**方法:**创建两个数组**freq 1【】**和**freq 2【】**,每个数组大小为‘26 ’,实现为散列表，分别存储 **str1** 和 **str2** 每个字符的频率。让 **n1** 和 **n2** 分别为 **str1** 和 **str2** 的长度。现在实现以下算法:

```
countSubsequences(str1, str2)
        for i = 0 to n1-1
        freq1[str1[i] - 'a']++
    for i = 0 n2-1    
        freq2[str2[i] - 'a']++

    Initialize count = 1    
    for i = 0 to 25
        if freq2[i] != 0 then
            if freq2[i] <= freq1[i] then
            count = count * binomialCoeff(freq1[i], freq2[i])
        else
            return 0    
        return count
```

让频率 q1[i]表示为 **n** ，频率 q2[i]表示为 **r** 。现在，上面算法中提到的**binomialcoffef(n，r)** 无非是二项式系数 **<sup>n</sup> C <sub>r</sub>** 。具体实施参见[本](https://www.geeksforgeeks.org/space-and-time-efficient-binomial-coefficient/)岗。
**解释:**
让某个字符的频率说出 **ch** 在‘str 2’中是‘x’，在‘str 1’中是‘y’。如果 y < x，则不存在“str1”的子序列，它可能是“str2”的字谜。否则，**<sup>y</sup>C<sub>x</sub>**给出所选 **ch** 的出现次数，这将有助于所需子序列的总计数。

## C++

```
// C++ implementation to
// count subsequences in
// first string which are 
// anagrams of the second
// string
#include <bits/stdc++.h>
using namespace std;

#define SIZE 26

// Returns value of Binomial
// Coefficient C(n, k)
int binomialCoeff(int n, int k)
{
    int res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate value of
    // [n * (n-1) *---* (n-k+1)] /
    // [k * (k-1) *----* 1]
    for (int i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// function to count subsequences
// in first string which are
// anagrams of the second string
int countSubsequences(string str1, string str2)
{
    // hash tables to store frequencies
    // of each character
    int freq1[SIZE], freq2[SIZE];

    int n1 = str1.size();
    int n2 = str2.size();

    // Initialize
    memset(freq1, 0, sizeof(freq1));
    memset(freq2, 0, sizeof(freq2));

    // store frequency of each
    // character of 'str1'
    for (int i = 0; i < n1; i++)
        freq1[str1[i] - 'a']++;

    // store frequency of each
    // character of 'str2'
    for (int i = 0; i < n2; i++)
        freq2[str2[i] - 'a']++;

    // to store the total count
    // of subsequences
    int count = 1;

    for (int i = 0; i < SIZE; i++)

        // if character (i + 'a')
        // exists in 'str2'
        if (freq2[i] != 0) {

                // if this character's frequency
                // in 'str2' in less than or
                // equal to its frequency in
                // 'str1' then accumulate its
                // contribution to the count
                // of subsequences. If its
                // frequency in 'str1' is 'n'
                // and in 'str2' is 'r', then
                // its contribution will be nCr,
                //  where C is the binomial
                // coefficient.
            if (freq2[i] <= freq1[i])
                count = count * binomialCoeff(freq1[i], freq2[i]);

            // else return 0 as there could
            // be no subsequence which is an
            // anagram of 'str2'
            else
                return 0;
        }

    // required count of subsequences
    return count;
}

// Driver program to test above
int main()
{
    string str1 = "abacd";
    string str2 = "abc";
    cout << "Count = "
        << countSubsequences(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// count subsequences in
// first string which are
// anagrams of the second
// string
import java.util.*;
import java.lang.*;

public class GfG{

    public final static int SIZE = 26;

    // Returns value of Binomial
    // Coefficient C(n, k)
    public static int binomialCoeff(int n,
                                    int k)
    {
        int res = 1;

        // Since C(n, k) = C(n, n-k)
        if (k > n - k)
            k = n - k;

        // Calculate value of
        // [n * (n-1) *---* (n-k+1)] /
        // [k * (k-1) *----* 1]
        for (int i = 0; i < k; ++i)
        {
            res *= (n - i);
            res /= (i + 1);
        }

        return res;
    }

    // function to count subsequences
    // in first string which are
    // anagrams of the second string
    public static int countSubsequences(String str,
                                        String str3)
    {
        // hash tables to store frequencies
        // of each character
        int[] freq1 = new int [SIZE];
        int[] freq2 = new int [SIZE];

        char[] str1 = str.toCharArray();
        char[] str2 = str3.toCharArray();

        int n1 = str.length();
        int n2 = str3.length();

        // store frequency of each
        // character of 'str1'
        for (int i = 0; i < n1; i++)
            freq1[str1[i] - 'a']++;

        // store frequency of each
        // character of 'str2'
        for (int i = 0; i < n2; i++)
            freq2[str2[i] - 'a']++;

        // to store the total count
        // of subsequences
        int count = 1;

        for (int i = 0; i < SIZE; i++)

            // if character (i + 'a')
            // exists in 'str2'
            if (freq2[i] != 0) {

                // if this character's frequency
                // in 'str2' in less than or
                // equal to its frequency in
                // 'str1' then accumulate its
                // contribution to the count
                // of subsequences. If its
                // frequency in 'str1' is 'n'
                // and in 'str2' is 'r', then
                // its contribution will be nCr,
                // where C is the binomial
                // coefficient.
                if (freq2[i] <= freq1[i])
                    count = count * binomialCoeff(freq1[i], freq2[i]);

                // else return 0 as there could
                // be no subsequence which is an
                // anagram of 'str2'
                else
                    return 0;
            }

        // required count of subsequences
        return count;
    }

    // Driver function
    public static void main(String argc[])
    {
        String str1 = "abacd";
        String str2 = "abc";

        System.out.println("Count = " +
        countSubsequences(str1, str2));
    }
}

/* This code is contributed by Sagar Shukla */
```

## 计算机编程语言

```
# Python3 implementation to count
# subsequences in first which are
# anagrams of the second

# import library
import numpy as np

SIZE = 26

# Returns value of Binomial
# Coefficient C(n, k)
def binomialCoeff(n, k):

    res = 1

    # Since C(n, k) = C(n, n-k)
    if (k > n - k):
        k = n - k

    # Calculate value of
    # [n * (n-1) *---* (n-k+1)] /
    # [k * (k-1) *----* 1]
    for i in range(0, k):
        res = res * (n - i)
        res = int(res / (i + 1))

    return res

# Function to count subsequences
# in first which are anagrams
# of the second
def countSubsequences(str1, str2):

    # Hash tables to store frequencies
    # of each character
    freq1 = np.zeros(26, dtype = np.int)
    freq2 = np.zeros(26, dtype = np.int)

    n1 = len(str1)
    n2 = len(str2)

    # Store frequency of each
    # character of 'str1'
    for i in range(0, n1):
        freq1[ord(str1[i]) - ord('a') ] += 1

    # Store frequency of each
    # character of 'str2'
    for i in range(0, n2):

        freq2[ord(str2[i]) - ord('a')] += 1

    # To store the total count
    # of subsequences
    count = 1

    for i in range(0, SIZE):

        # if character (i + 'a')
        # exists in 'str2'
        if (freq2[i] != 0):
            # if this character's frequency
            # in 'str2' in less than or
            # equal to its frequency in
            # 'str1' then accumulate its
            # contribution to the count
            # of subsequences. If its
            # frequency in 'str1' is 'n'
            # and in 'str2' is 'r', then
            # its contribution will be nCr,
            # where C is the binomial
            # coefficient.
            if (freq2[i] <= freq1[i]):
                count = count * binomialCoeff(freq1[i], freq2[i])

            # else return 0 as there could
            # be no subsequence which is an
            # anagram of 'str2'
            else:
                return 0

    # required count of subsequences
    return count

# Driver code
str1 = "abacd"
str2 = "abc"
ans = countSubsequences(str1, str2)
print ("Count = ", ans)

# This code contributed by saloni1297
```

## C#

```
// C# implementation to
// count subsequences in
// first string which are
// anagrams of the second
// string
using System;

class GfG {

    public static int SIZE = 26;

    // Returns value of Binomial
    // Coefficient C(n, k)
    public static int binomialCoeff(int n,
                                    int k)
    {
        int res = 1;

        // Since C(n, k) = C(n, n-k)
        if (k > n - k)
            k = n - k;

        // Calculate value of
        // [n * (n-1) *---* (n-k+1)] /
        // [k * (k-1) *----* 1]
        for (int i = 0; i < k; ++i)
        {
            res *= (n - i);
            res /= (i + 1);
        }

        return res;
    }

    // function to count subsequences
    // in first string which are
    // anagrams of the second string
    public static int countSubsequences(String str,
                                        String str3)
    {
        // hash tables to store frequencies
        // of each character
        int[] freq1 = new int [SIZE];
        int[] freq2 = new int [SIZE];

        char[] str1 = str.ToCharArray();
        char[] str2 = str3.ToCharArray();

        int n1 = str.Length;
        int n2 = str3.Length;

        // store frequency of each
        // character of 'str1'
        for (int i = 0; i < n1; i++)
            freq1[str1[i] - 'a']++;

        // store frequency of each
        // character of 'str2'
        for (int i = 0; i < n2; i++)
            freq2[str2[i] - 'a']++;

        // to store the total count
        // of subsequences
        int count = 1;

        for (int i = 0; i < SIZE; i++)

            // if character (i + 'a')
            // exists in 'str2'
            if (freq2[i] != 0) {

                // if this character's frequency
                // in 'str2' in less than or
                // equal to its frequency in
                // 'str1' then accumulate its
                // contribution to the count
                // of subsequences. If its
                // frequency in 'str1' is 'n'
                // and in 'str2' is 'r', then
                // its contribution will be nCr,
                // where C is the binomial
                // coefficient.
                if (freq2[i] <= freq1[i])
                    count = count * binomialCoeff(freq1[i],
                                                  freq2[i]);

                // else return 0 as there could
                // be no subsequence which is an
                // anagram of 'str2'
                else
                    return 0;
            }

        // required count of subsequences
        return count;
    }

    // Driver code
    public static void Main(String[] argc)
    {
        String str1 = "abacd";
        String str2 = "abc";

        Console.Write("Count = " +
        countSubsequences(str1, str2));
    }
}

// This code is contributed by parashar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// count subsequences in
// first $which are
// anagrams of the second
// string
$SIZE = 26;

// Returns value of Binomial
// Coefficient C(n, k)
function binomialCoeff($n, $k)
{
    $res = 1;

    // Since C(n, k) = C(n, n-k)
    if ($k > $n - $k)
        $k = $n - $k;

    // Calculate value of
    // [n * (n-1) *---* (n-k+1)] /
    // [k * (k-1) *----* 1]
    for ($i = 0; $i < $k; ++$i)
    {
        $res *= ($n - $i);
        $res /= ($i + 1);
    }

    return $res;
}

// function to count
// subsequences in
// first string which
// are anagrams of the
// second string
function countSubsequences($str1,
                           $str2)
{
    global $SIZE;

    // hash tables to
    // store frequencies
    // of each character
    $freq1 = array();
    $freq2 = array();

    // Initialize
    for ($i = 0;
         $i < $SIZE; $i++)
    {
        $freq1[$i] = 0;
        $freq2[$i] = 0;
    }
    $n1 = strlen($str1);
    $n2 = strlen($str2);

    // store frequency of each
    // character of 'str1'
    for ($i = 0; $i < $n1; $i++)
        $freq1[ord($str1[$i]) -
               ord('a')]++;

    // store frequency of each
    // character of 'str2'
    for ($i = 0; $i < $n2; $i++)
        $freq2[ord($str2[$i]) -
               ord('a')]++;

    // to store the total count
    // of subsequences
    $count = 1;

    for ($i = 0; $i < $SIZE; $i++)

        // if character (i + 'a')
        // exists in 'str2'
        if ($freq2[$i] != 0)
        {

            // if this character's frequency
            // in 'str2' in less than or
            // equal to its frequency in
            // 'str1' then accumulate its
            // contribution to the count
            // of subsequences. If its
            // frequency in 'str1' is 'n'
            // and in 'str2' is 'r', then
            // its contribution will be nCr,
            // where C is the binomial
            // coefficient.
            if ($freq2[$i] <= $freq1[$i])
                $count = $count *
                         binomialCoeff($freq1[$i],
                                       $freq2[$i]);

            // else return 0 as there
            // could be no subsequence
            // which is an anagram of
            // 'str2'
            else
                return 0;
        }

    // required count
    // of subsequences
    return $count;
}

// Driver Code
$str1 = "abacd";
$str2 = "abc";
echo ("Count = ".
       countSubsequences($str1,
                         $str2));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// JavaScript implementation to
// count subsequences in
// first string which are 
// anagrams of the second
// string

var SIZE = 26

// Returns value of Binomial
// Coefficient C(n, k)
function binomialCoeff(n, k)
{
    var res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate value of
    // [n * (n-1) *---* (n-k+1)] /
    // [k * (k-1) *----* 1]
    for (var i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// function to count subsequences
// in first string which are
// anagrams of the second string
function countSubsequences(str1, str2)
{
    // hash tables to store frequencies
    // of each character
    var freq1 = Array(SIZE).fill(0),
        freq2 = Array(SIZE).fill(0);

    var n1 = str1.length;
    var n2 = str2.length;

    // store frequency of each
    // character of 'str1'
    for (var i = 0; i < n1; i++)
        freq1[str1[i].charCodeAt(0) -
        'a'.charCodeAt(0)]++;

    // store frequency of each
    // character of 'str2'
    for (var i = 0; i < n2; i++)
        freq2[str2[i].charCodeAt(0) -
        'a'.charCodeAt(0)]++;

    // to store the total count
    // of subsequences
    var count = 1;

    for (var i = 0; i < SIZE; i++)

        // if character (i + 'a')
        // exists in 'str2'
        if (freq2[i] != 0) {

                // if this character's frequency
                // in 'str2' in less than or
                // equal to its frequency in
                // 'str1' then accumulate its
                // contribution to the count
                // of subsequences. If its
                // frequency in 'str1' is 'n'
                // and in 'str2' is 'r', then
                // its contribution will be nCr,
                //  where C is the binomial
                // coefficient.
            if (freq2[i] <= freq1[i])
                count =
                count * binomialCoeff(freq1[i], freq2[i]);

            // else return 0 as there could
            // be no subsequence which is an
            // anagram of 'str2'
            else
                return 0;
        }

    // required count of subsequences
    return count;
}

// Driver program to test above
var str1 = "abacd";
var str2 = "abc";
document.write( "Count = "
     + countSubsequences(str1, str2));

</script>
```

**输出:**

```
Count = 2
```

**时间复杂度:** O(n1 + n2) + O(max)，其中 **max** 为最大频率。