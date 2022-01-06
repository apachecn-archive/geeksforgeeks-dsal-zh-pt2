# 包含元音的最长公共子序列的长度

> 原文:[https://www . geeksforgeeks . org/含最长公共子序列元音的长度/](https://www.geeksforgeeks.org/length-of-longest-common-subsequence-containing-vowels/)

给定两根长度分别为**米**和 **n** 的弦 **X** 和 **Y** 。问题是找到包含所有元音字符的字符串 **X** 和 **Y** 的最长公共子序列的长度。

**示例:**

```
Input : X = "aieef" 
        Y = "klaief"
Output : aie

Input : X = "geeksforgeeks" 
        Y = "feroeeks"
Output : eoee
```

**来源:** [Paytm 面试体验(后端开发者)。](https://www.geeksforgeeks.org/paytm-interview-experience-backend-developer/)
**天真方法:**生成两个给定序列的所有子序列，找到包含所有元音字符的最长匹配子序列。这个解决方案在时间复杂度方面是指数级的。

**有效方法(动态规划):**该方法是[最长公共子序列| DP-4](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/) 问题的一种变体。

这篇文章的不同之处在于，普通的子序列字符必须都是元音。

## C++

```
// C++ implementation to find the length of longest common
// subsequence which contains all vowel characters
#include <bits/stdc++.h>

using namespace std;

// function to check whether 'ch'
// is a vowel or not
bool isVowel(char ch)
{
    if (ch == 'a' || ch == 'e' || ch == 'i'
        || ch == 'o' || ch == 'u')
        return true;
    return false;
}

// function to find the length of longest common subsequence
// which contains all vowel characters
int lcs(char* X, char* Y, int m, int n)
{
    int L[m + 1][n + 1];
    int i, j;

    // Following steps build L[m+1][n+1] in bottom up fashion. Note
    // that L[i][j] contains length of LCS of X[0..i-1] and Y[0..j-1]
    for (i = 0; i <= m; i++) {
        for (j = 0; j <= n; j++) {
            if (i == 0 || j == 0)
                L[i][j] = 0;

            else if ((X[i - 1] == Y[j - 1]) && isVowel(X[i - 1]))
                L[i][j] = L[i - 1][j - 1] + 1;

            else
                L[i][j] = max(L[i - 1][j], L[i][j - 1]);
        }
    }

    // L[m][n] contains length of LCS for X[0..n-1] and Y[0..m-1]
    // which contains all vowel characters
    return L[m][n];
}

// Driver program to test above
int main()
{
    char X[] = "aieef";
    char Y[] = "klaief";

    int m = strlen(X);
    int n = strlen(Y);

    cout << "Length of LCS = "
         << lcs(X, Y, m, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// length of longest common subsequence
// which contains all vowel characters
class GFG
{

// function to check whether 'ch'
// is a vowel or not
static boolean isVowel(char ch)
{
    if (ch == 'a' || ch == 'e' ||
        ch == 'i' || ch == 'o' ||
        ch == 'u')
        return true;
    return false;
}

// function to find the length of
// longest common subsequence which
// contains all vowel characters
static int lcs(String X, String Y,
               int m, int n)
{
    int L[][] = new int[m + 1][n + 1];
    int i, j;

    // Following steps build L[m+1][n+1]
    // in bottom up fashion. Note that
    // L[i][j] contains length of LCS of
    // X[0..i-1] and Y[0..j-1]
    for (i = 0; i <= m; i++)
    {
        for (j = 0; j <= n; j++)
        {
            if (i == 0 || j == 0)
                L[i][j] = 0;

            else if ((X.charAt(i - 1) == Y.charAt(j - 1)) &&
                                isVowel(X.charAt(i - 1)))
                L[i][j] = L[i - 1][j - 1] + 1;

            else
                L[i][j] = Math.max(L[i - 1][j],
                                   L[i][j - 1]);
        }
    }

    // L[m][n] contains length of LCS
    // for X[0..n-1] and Y[0..m-1]
    // which contains all vowel characters
    return L[m][n];
}

// Driver Code
public static void main(String[] args)
{
    String X = "aieef";
    String Y = "klaief";

    int m = X.length();
    int n = Y.length();

    System.out.println("Length of LCS = " +
                          lcs(X, Y, m, n));
}
}

// This code is contributed by Bilal
```

## 蟒蛇 3

```
# Python3 implementation to find the
# length of longest common subsequence
# which contains all vowel characters

# function to check whether 'ch'
# is a vowel or not
def isVowel(ch):
    if (ch == 'a' or ch == 'e' or
        ch == 'i'or ch == 'o' or
        ch == 'u'):
        return True
    return False

# function to find the length of longest
# common subsequence which contains all
# vowel characters
def lcs(X, Y, m, n):

    L = [[0 for i in range(n + 1)]
            for j in range(m + 1)]
    i, j = 0, 0

    # Following steps build L[m+1][n+1] in
    # bottom up fashion. Note that L[i][j]
    # contains length of LCS of X[0..i-1]
    # and Y[0..j-1]
    for i in range(m + 1):
        for j in range(n + 1):
            if (i == 0 or j == 0):
                L[i][j] = 0
            elif ((X[i - 1] == Y[j - 1]) and
                      isVowel(X[i - 1])):
                L[i][j] = L[i - 1][j - 1] + 1
            else:
                L[i][j] = max(L[i - 1][j],
                              L[i][j - 1])

    # L[m][n] contains length of LCS for
    # X[0..n-1] and Y[0..m-1] which
    # contains all vowel characters
    return L[m][n]

# Driver Code
X = "aieef"
Y = "klaief"

m = len(X)
n = len(Y)

print("Length of LCS =", lcs(X, Y, m, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation to find the
// length of longest common subsequence
// which contains all vowel characters
using System;

class GFG
{

// function to check whether
// 'ch' is a vowel or not
static int isVowel(char ch)
{
    if (ch == 'a' || ch == 'e' ||
        ch == 'i' || ch == 'o' ||
        ch == 'u')
        return 1;
    return 0;
}

// find max value
static int max(int a, int b)
{
    return (a > b) ? a : b;
}

// function to find the length of
// longest common subsequence which
// contains all vowel characters
static int lcs(String X, String Y,
               int m, int n)
{
    int [,]L = new int[m + 1, n + 1];
    int i, j;

    // Following steps build L[m+1,n+1]
    // in bottom up fashion. Note that
    // L[i,j] contains length of LCS of
    // X[0..i-1] and Y[0..j-1]
    for (i = 0; i <= m; i++)
    {
        for (j = 0; j <= n; j++)
        {
            if (i == 0 || j == 0)
                L[i, j] = 0;

            else if ((X[i - 1] == Y[j - 1]) &&
                    isVowel(X[i - 1]) == 1)
                L[i, j] = L[i - 1, j - 1] + 1;

            else
                L[i, j] = max(L[i - 1, j],
                              L[i, j - 1]);
        }
    }

    // L[m,n] contains length of LCS
    // for X[0..n-1] and Y[0..m-1]
    // which contains all vowel characters
    return L[m, n];
}

// Driver Code
static public void Main(String []args)
{
    String X = "aieef";
    String Y = "klaief";

    int m = X.Length;
    int n = Y.Length;

    Console.WriteLine("Length of LCS = " +
                         lcs(X, Y, m, n));
}
}

// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the length of
// longest common subsequence which contains
// all vowel characters

// function to check whether 'ch'
// is a vowel or not
function isVowel($ch)
{
    if ($ch == 'a' || $ch == 'e' ||
        $ch == 'i' || $ch == 'o' || $ch == 'u')
        return true;
    return false;
}

// function to find the length of longest common
// subsequence which contains all vowel characters
function lcs($X, $Y, $m, $n)
{
    $L = array_fill(0, $m + 1, array_fill(0, $n + 1, NULL));

    // Following steps build L[m+1][n+1] in bottom
    // up fashion. Note that L[i][j] contains length
    // of LCS of X[0..i-1] and Y[0..j-1]
    for ($i = 0; $i <= $m; $i++)
    {
        for ($j = 0; $j <= $n; $j++)
        {
            if ($i == 0 || $j == 0)
                $L[$i][$j] = 0;

            else if (($X[$i - 1] == $Y[$j - 1]) &&
                            isVowel($X[$i - 1]))
                $L[$i][$j] = $L[$i - 1][$j - 1] + 1;

            else
                $L[$i][$j] = max($L[$i - 1][$j],
                                 $L[$i][$j - 1]);
        }
    }

    // L[m][n] contains length of LCS for X[0..n-1]
    // and Y[0..m-1] which contains all vowel characters
    return $L[$m][$n];
}

// Driver Code
$X = "aieef";
$Y = "klaief";

$m = strlen($X);
$n = strlen($Y);

echo "Length of LCS = " . lcs($X, $Y, $m, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// length of longest common subsequence
// which contains all vowel characters

// Function to check whether 'ch'
// is a vowel or not
function isVowel(ch)
{
    if (ch == 'a' || ch == 'e' ||
        ch == 'i' || ch == 'o' ||
        ch == 'u')
        return true;

    return false;
}

// Function to find the length of
// longest common subsequence which
// contains all vowel characters
function lcs(X, Y, m, n)
{
    let L = new Array(m + 1);
    let i, j;

    // Following steps build L[m+1][n+1]
    // in bottom up fashion. Note that
    // L[i][j] contains length of LCS of
    // X[0..i-1] and Y[0..j-1]
    for(i = 0; i <= m; i++)
    {
        L[i] = new Array(n + 1);
        for(j = 0; j <= n; j++)
        {
            if (i == 0 || j == 0)
                L[i][j] = 0;

            else if ((X[i - 1] == Y[j - 1]) &&
                          isVowel(X[i - 1]))
                L[i][j] = L[i - 1][j - 1] + 1;

            else
                L[i][j] = Math.max(L[i - 1][j],
                                L[i][j - 1]);
        }
    }

    // L[m][n] contains length of LCS
    // for X[0..n-1] and Y[0..m-1]
    // which contains all vowel characters
    return L[m][n];
}

// Driver Code
let X = "aieef";
let Y = "klaief";
let m = X.length;
let n = Y.length;

document.write("Length of LCS = " + lcs(X, Y, m, n));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
Length of LCS = 3
```

**时间复杂度:** O(m*n)。
**辅助空间:** O(m*n)。