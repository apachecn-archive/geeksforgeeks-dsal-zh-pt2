# 统计字符串的回文特征

> 原文:[https://www . geesforgeks . org/count-回文-特征-字符串/](https://www.geeksforgeeks.org/count-palindromic-characteristics-string/)

给定长度为 n 的字符串 s，计算具有不同回文特征类型的子字符串的数量。
**回文特征**是一个字符串中 k 个回文的数量，其中 k 位于范围[0，n]内。
一个字符串是**1-回文**(或简称回文)当且仅当它向后读和向前读相同时。
一个字符串是**k-回文** (k > 1)当且仅当:
1。它的左半部分等于它的右半部分。
2。它的左半部分和右半部分应该是非空的(k–1)-回文。长度为“t”的字符串的左半部分是长度为⌊t/2⌋的前缀，右半部分是长度相同的后缀。
**注意:**每个子串在字符串中出现的次数都被计算在内。例如，在字符串“aaa”中，子字符串“a”出现 3 次。
**示例:**

```
Input : abba
Output : 6 1 0 0
Explanation : 
"6" 1-palindromes = "a", "b", "b", "a", "bb", "abba".
"1" 2-palindrome = "bb". Because "b" is 1-palindrome 
and "bb" has both left and right parts equal. 
"0" 3-palindrome and 4-palindrome.

Input : abacaba
Output : 12 4 1 0 0 0 0
Explanation : 
"12" 1-palindromes = "a", "b", "a", "c", "a", "b", 
"a", "aba", "aca", "aba", "bacab", "abacaba".
"4" 2-palindromes = "aba", "aca", "aba", "abacaba". 
Because "a" and "aba" are 1-palindromes.
NOTE :  "bacab" is not 2-palindrome as "ba" 
is not 1-palindrome. "1" 3-palindrome = "abacaba". 
Because is "aba" is 2-palindrome. "0" other 
k-pallindromes where 4 < = k < = 7.
```

**方法:**取一个字符串 s，说它是 1-回文，检查它的左半部分也是 1-回文，那么很明显，它的右半部分将总是等于左半部分(因为该字符串也是 1-回文)，使原始字符串成为 2-回文。现在，类似地，检查字符串的左半部分，它也变成了 1-回文，然后它将使左半部分成为 2-回文，因此，使原始字符串成为 3-回文，以此类推，直到只剩下 1 个字母或部分不是 1-回文。
我们走吧。众所周知“阿巴卡巴”是 1-回文。所以，当检查它的左半部分“aba”时，它也是一个 1-回文，它使“abacaba”成为一个 2-回文。然后，检查“aba”的左半部分“a”，这也是一个 1 回文。所以它使“aba”成为 2-回文，“aba”使“abacaba”成为 3-回文。换句话说，如果一个字符串是 k-回文，那么它也是(k-1)-回文，(k-2)-回文，以此类推，直到 1-回文。下面给出了相同的代码，首先检查每一个子串是否是回文，然后在对数时间内递归计算 k-回文子串的数量。
**以下是上述方法的实施:**

## C++

```
// A C++ program which counts different
// palindromic characteristics of a string.
#include <bits/stdc++.h>
using namespace std;

const int MAX_STR_LEN = 1000;

bool P[MAX_STR_LEN][MAX_STR_LEN];
int Kpal[MAX_STR_LEN];

// A C++ function which checks whether a
// substring str[i..j] of a given string
// is a palindrome or not.
void checkSubStrPal(string str, int n)
{

    // P[i][j] = true if substring str
    // [i..j] is palindrome, else false
    memset(P, false, sizeof(P));

    // palindrome of single length
    for (int i = 0; i < n; i++)
        P[i][i] = true;

    // palindrome of length 2
    for (int i = 0; i < n - 1; i++)
        if (str[i] == str[i + 1])
            P[i][i + 1] = true;

    // Palindromes of length more then 2.
    // This loop is similar to Matrix Chain
    // Multiplication. We start with a gap of
    // length 2 and fill P table in a way that
    // gap between starting and ending indexes
    // increases one by one by outer loop.
    for (int gap = 2; gap < n; gap++)
    {

        // Pick starting point for current gap
        for (int i = 0; i < n - gap; i++)
        {

            // Set ending point
            int j = gap + i;

            // If current string is palindrome
            if (str[i] == str[j] && P[i + 1][j - 1])
                P[i][j] = true;
        }
    }
}

// A C++ function which recursively
// counts if a string str [i..j] is
// a k-palindromic string or not.
void countKPalindromes(int i, int j, int k)
{
    // terminating condition for a
    // string which is a k-palindrome.
    if (i == j)
    {
        Kpal[k]++;
        return;
    }

    // terminating condition for a
    // string which is not a k-palindrome.
    if (P[i][j] == false)
        return;

    // increases the counter for the
    // string if it is a k-palindrome.
    Kpal[k]++;

    // mid is middle pointer of
    // the string str [i...j].
    int mid = (i + j) / 2;

    // if length of string which is
    // (j - i + 1) is odd than we have
    // to subtract one from mid.
    // else if even then no change.
    if ((j - i + 1) % 2 == 1)
        mid--;

    // if the string is k-palindrome
    // then we check if it is a
    // (k+1) - palindrome or not by
    // just sending any of one half of
    // the string to the Count_k_Palindrome
    // function.
    countKPalindromes(i, mid, k + 1);
}

void printKPalindromes(string s)
{

    // Count of k-palindromes is equal
    // to zero initially.
    memset(Kpal, 0, sizeof(Kpal));

    // Finding all palindromic
    // substrings of given string
    int n = s.length();
    checkSubStrPal(s, n);

    // counting k-palindromes for each and
    // every substring of given string. .
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n - i; j++)
            countKPalindromes(j, j + i, 1);

    // Output the number of K-palindromic
    // substrings of a given string.
    for (int i = 1; i <= n; i++)
        cout << Kpal[i] << " ";
    cout << "\n";
}

// Driver code
int main()
{
    string s = "abacaba";
    printKPalindromes(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program which counts
// different palindromic
// characteristics of a string.        
import java.io.*;

class GFG
{
    static int MAX_STR_LEN = 1000;

    static boolean P[][] =
           new boolean[MAX_STR_LEN][MAX_STR_LEN];
    static int []Kpal =
           new int[MAX_STR_LEN];

    // function which checks
    // whether a substring
    // str[i..j] of a given
    // string is a palindrome or not.
    static void checkSubStrPal(String str,
                               int n)
    {

        // P[i,j] = true if substring
        // str [i..j] is palindrome,
        // else false
        for (int i = 0; i < MAX_STR_LEN; i++)
        {
            for (int j = 0; j < MAX_STR_LEN; j++)
                P[i][j] = false;
            Kpal[i] = 0;
        }

        // palindrome of
        // single length
        for (int i = 0; i < n; i++)
            P[i][i] = true;

        // palindrome of
        // length 2
        for (int i = 0; i < n - 1; i++)
            if (str.charAt(i) == str.charAt(i + 1))
                P[i][i + 1] = true;

        // Palindromes of length
        // more then 2\. This loop
        // is similar to Matrix
        // Chain Multiplication.
        // We start with a gap of
        // length 2 and fill P table
        // in a way that gap between
        // starting and ending indexes
        // increases one by one by
        // outer loop.
        for (int gap = 2; gap < n; gap++)
        {

            // Pick starting point
            // for current gap
            for (int i = 0; i < n - gap; i++)
            {

                // Set ending point
                int j = gap + i;

                // If current string
                // is palindrome
                if (str.charAt(i) == str.charAt(j) &&
                                     P[i + 1][j - 1])
                    P[i][j] = true;
            }
        }
    }

    // A function which recursively
    // counts if a string str [i..j] is
    // a k-palindromic string or not.
    static void countKPalindromes(int i, int j,
                                  int k)
    {
        // terminating condition
        // for a string which is
        // a k-palindrome.
        if (i == j)
        {
            Kpal[k]++;
            return;
        }

        // terminating condition for
        // a string which is not a
        // k-palindrome.
        if (P[i][j] == false)
            return;

        // increases the counter
        // for the string if it
        // is a k-palindrome.
        Kpal[k]++;

        // mid is middle pointer of
        // the string str [i...j].
        int mid = (i + j) / 2;

        // if length of string which
        // is (j - i + 1) is odd than
        // we have to subtract one
        // from mid else if even then
        // no change.
        if ((j - i + 1) % 2 == 1)
            mid--;

        // if the string is k-palindrome
        // then we check if it is a
        // (k+1) - palindrome or not
        // by just sending any of one
        // half of the string to the
        // Count_k_Palindrome function.
        countKPalindromes(i, mid, k + 1);
    }

    static void printKPalindromes(String s)
    {
        // Finding all palindromic
        // substrings of given string
        int n = s.length();
        checkSubStrPal(s, n);

        // counting k-palindromes for
        // each and every substring
        // of given string. .
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n - i; j++)
                countKPalindromes(j, j + i, 1);

        // Output the number of
        // K-palindromic substrings
        // of a given string.
        for (int i = 1; i <= n; i++)
            System.out.print(Kpal[i] + " ");
        System.out.println();
    }

    // Driver code
    public static void main(String args[])
    {
        String s = "abacaba";
        printKPalindromes(s);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python program which counts
# different palindromic
# characteristics of a string.        
MAX_STR_LEN = 1000;

P = [[0 for x in range(MAX_STR_LEN)]
        for y in range(MAX_STR_LEN)] ;

for i in range(0, MAX_STR_LEN) :
    for j in range(0, MAX_STR_LEN) :
        P[i][j] = False;

Kpal = [0] * MAX_STR_LEN;

# def which checks
# whether a substr[i..j]
# of a given is a
# palindrome or not.
def checkSubStrPal(str, n) :

    global P, Kpal, MAX_STR_LEN;

    # P[i,j] = True if substr
    # [i..j] is palindrome,
    # else False
    for i in range(0, MAX_STR_LEN) :

        for j in range(0, MAX_STR_LEN) :
            P[i][j] = False;
        Kpal[i] = 0;

    # palindrome of
    # single length
    for i in range(0, n) :
        P[i][i] = True;

    # palindrome of
    # length 2
    for i in range(0, n - 1) :
        if (str[i] == str[i + 1]) :
            P[i][i + 1] = True;

    # Palindromes of length more
    # then 2\. This loop is similar
    # to Matrix Chain Multiplication.
    # We start with a gap of length
    # 2 and fill P table in a way
    # that gap between starting and
    # ending indexes increases one
    # by one by outer loop.
    for gap in range(2, n) :

        # Pick starting point
        # for current gap
        for i in range(0, n - gap) :

            # Set ending point
            j = gap + i;

            # If current string
            # is palindrome
            if (str[i] == str[j] and
                P[i + 1][j - 1]) :
                P[i][j] = True;

# A Python def which
# recursively counts if
# a str [i..j] is a
# k-palindromic or not.
def countKPalindromes(i, j, k) :

    global Kpal, P;

    # terminating condition
    # for a which is a
    # k-palindrome.
    if (i == j) :

        Kpal[k] = Kpal[k] + 1;
        return;

    # terminating condition
    # for a which is not a
    # k-palindrome.
    if (P[i][j] == False) :
        return;

    # increases the counter
    # for the if it is a
    # k-palindrome.
    Kpal[k] = Kpal[k] + 1;

    # mid is middle pointer
    # of the str [i...j].
    mid = int((i + j) / 2);

    # if length of which is
    # (j - i + 1) is odd than
    # we have to subtract one
    # from mid else if even
    # then no change.
    if ((j - i + 1) % 2 == 1) :
        mid = mid - 1;

    # if the is k-palindrome
    # then we check if it is a
    # (k+1) - palindrome or not
    # by just sending any of
    # one half of the to the
    # Count_k_Palindrome def.
    countKPalindromes(i, mid, k + 1);

def printKPalindromes(s) :

    global P, Kpal, MAX_STR_LEN;

    # Finding all palindromic
    # substrings of given string
    n = len(s);
    checkSubStrPal(s, n);

    # counting k-palindromes
    # for each and every sub
    # of given string. .
    for i in range(0, n) :
        for j in range(0, n - i) :
            countKPalindromes(j, j + i, 1);

    # Output the number of
    # K-palindromic substrings
    # of a given string.
    for i in range(1, n + 1) :
        print (Kpal[i], end=" ");
    print();

# Driver code
s = "abacaba";
printKPalindromes(s);

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program which counts
// different palindromic
// characteristics of a string.        
using System;

class GFG
{
    static int MAX_STR_LEN = 1000;

    static bool [,]P = new bool[MAX_STR_LEN,
                                MAX_STR_LEN];
    static int []Kpal = new int[MAX_STR_LEN];

    // function which checks whether
    // a substring str[i..j] of a
    // given string is a palindrome or not.
    static void checkSubStrPal(string str,
                               int n)
    {

        // P[i,j] = true if substring str
        // [i..j] is palindrome, else false
        for (int i = 0; i < MAX_STR_LEN; i++)
        {
            for (int j = 0; j < MAX_STR_LEN; j++)
                P[i, j] = false;
            Kpal[i] = 0;
        }

        // palindrome of single length
        for (int i = 0; i < n; i++)
            P[i, i] = true;

        // palindrome of length 2
        for (int i = 0; i < n - 1; i++)
            if (str[i] == str[i + 1])
                P[i, i + 1] = true;

        // Palindromes of length more
        // then 2\. This loop is similar
        // to Matrix Chain Multiplication.
        // We start with a gap of length 2
        // and fill P table in a way that
        // gap between starting and ending
        // indexes increases one by one by
        // outer loop.
        for (int gap = 2; gap < n; gap++)
        {

            // Pick starting point
            // for current gap
            for (int i = 0; i < n - gap; i++)
            {

                // Set ending point
                int j = gap + i;

                // If current string
                // is palindrome
                if (str[i] == str[j] &&
                        P[i + 1, j - 1])
                    P[i, j] = true;
            }
        }
    }

    // A C++ function which recursively
    // counts if a string str [i..j] is
    // a k-palindromic string or not.
    static void countKPalindromes(int i, int j,
                                  int k)
    {
        // terminating condition for a
        // string which is a k-palindrome.
        if (i == j)
        {
            Kpal[k]++;
            return;
        }

        // terminating condition for
        // a string which is not a
        // k-palindrome.
        if (P[i, j] == false)
            return;

        // increases the counter for the
        // string if it is a k-palindrome.
        Kpal[k]++;

        // mid is middle pointer of
        // the string str [i...j].
        int mid = (i + j) / 2;

        // if length of string which is
        // (j - i + 1) is odd than we have
        // to subtract one from mid.
        // else if even then no change.
        if ((j - i + 1) % 2 == 1)
            mid--;

        // if the string is k-palindrome
        // then we check if it is a
        // (k+1) - palindrome or not
        // by just sending any of one
        // half of the string to the
        // Count_k_Palindrome function.
        countKPalindromes(i, mid, k + 1);
    }

    static void printKPalindromes(string s)
    {
        // Finding all palindromic
        // substrings of given string
        int n = s.Length;
        checkSubStrPal(s, n);

        // counting k-palindromes for each and
        // every substring of given string. .
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n - i; j++)
                countKPalindromes(j, j + i, 1);

        // Output the number of K-palindromic
        // substrings of a given string.
        for (int i = 1; i <= n; i++)
            Console.Write(Kpal[i] + " ");
        Console.WriteLine();
    }

    // Driver code
    static void Main()
    {
        string s = "abacaba";
        printKPalindromes(s);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program which counts
// different palindromic
// characteristics of a string.        
$MAX_STR_LEN = 1000;

$P = array(array());
$Kpal = array_fill(0, $MAX_STR_LEN, 0);

for($i = 0; $i < $MAX_STR_LEN; $i++)
{
    for($j = 0; $j < $MAX_STR_LEN; $j++)
        $P[$i][$j] = false;
}

// function which checks
// whether a substr[i..j]
// of a given is a
// palindrome or not.
function checkSubStrPal($str,
                        $n)
{
    global $P, $Kpal,
           $MAX_STR_LEN;

    // P[i,j] = true if substr
    // [i..j] is palindrome, else false
    for ($i = 0;
         $i < $MAX_STR_LEN; $i++)
    {
        for ($j = 0;
             $j < $MAX_STR_LEN; $j++)
            $P[$i][$j] = false;
        $Kpal[$i] = 0;
    }

    // palindrome of
    // single length
    for ($i = 0; $i < $n; $i++)
        $P[$i][$i] = true;

    // palindrome of
    // length 2
    for ($i = 0; $i < $n - 1; $i++)
        if ($str[$i] == $str[$i + 1])
            $P[$i][$i + 1] = true;

    // Palindromes of length more
    // then 2\. This loop is similar
    // to Matrix Chain Multiplication.
    // We start with a gap of length
    // 2 and fill P table in a way
    // that gap between starting and
    // ending indexes increases one
    // by one by outer loop.
    for ($gap = 2; $gap < $n; $gap++)
    {
        // Pick starting point
        // for current gap
        for ($i = 0;
             $i < $n - $gap; $i++)
        {
            // Set ending point
            $j = $gap + $i;

            // If current string
            // is palindrome
            if ($str[$i] == $str[$j] &&
                    $P[$i + 1][$j - 1])
                $P[$i][$j] = true;
        }
    }
}

// A PHP function which
// recursively counts if
// a str [i..j] is a
// k-palindromic or not.
function countKPalindromes($i, $j, $k)
{
    global $Kpal, $P;

    // terminating condition for a
    // which is a k-palindrome.
    if ($i == $j)
    {
        $Kpal[$k]++;
        return;
    }

    // terminating condition
    // for a which is not a
    // k-palindrome.
    if ($P[$i][$j] == false)
        return;

    // increases the counter
    // for the if it is a
    // k-palindrome.
    $Kpal[$k]++;

    // mid is middle pointer
    // of the str [i...j].
    $mid = ($i + $j) / 2;

    // if length of which is
    // (j - i + 1) is odd than
    // we have to subtract one
    // from mid else if even
    // then no change.
    if (($j - $i + 1) % 2 == 1)
        $mid--;

    // if the is k-palindrome
    // then we check if it is a
    // (k+1) - palindrome or not
    // by just sending any of
    // one half of the to the
    // Count_k_Palindrome function.
    countKPalindromes($i, $mid,
                      $k + 1);
}

function printKPalindromes($s)
{
    global $P, $Kpal,
           $MAX_STR_LEN;

    // Finding all palindromic
    // substrings of given string
    $n = strlen($s);
    checkSubStrPal($s, $n);

    // counting k-palindromes
    // for each and every sub
    // of given string. .
    for ($i = 0; $i < $n; $i++)
        for ($j = 0; $j < $n - $i; $j++)
            countKPalindromes($j, $j +
                              $i, 1);

    // Output the number of
    // K-palindromic substrings
    // of a given string.
    for ($i = 1; $i <= $n; $i++)
        echo ($Kpal[$i] . " ");
    echo("\n");
}

// Driver code
$s = "abacaba";
printKPalindromes($s);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

**Output :** 

```
12 4 1 0 0 0 0
```

**时间复杂度:** O( ![n^2$\log{n}$  ](img/2bd4a9930f6ed914f78fc62bf42859e5.png "Rendered by QuickLaTeX.com") )
**辅助空间:** O( ![n^2  ](img/9bba27746ccacc30681cbd224540189b.png "Rendered by QuickLaTeX.com"))