# 索引范围内回文子串的计数

> 原文:[https://www . geeksforgeeks . org/回文数-索引范围内的子字符串/](https://www.geeksforgeeks.org/count-of-palindromic-substrings-in-an-index-range/)

给定一个由除此之外的小字母字符组成的字符串，我们将以索引元组的形式给定该字符串的许多子字符串。我们需要找出给定子串范围内回文子串的个数。
**例:**

```
Input : String str = "xyaabax"
           Range1 = (3, 5)   
           Range2 = (2, 3) 
Output : 4
         3
For Range1,  substring is "aba"
Count of palindromic substring in "aba" is 
four : "a", "b", "aba", "a"
For Range2,  substring is "aa"
Count of palindromic substring in "aa" is 
3 : "a", "a", "aa"
```

先决条件:[统计一个字符串中所有回文子串](https://www.geeksforgeeks.org/count-palindrome-sub-strings-string/)
我们可以用动态规划来解决这个问题。首先我们将制作一个 2D 阵列 isPalin，isPalin[i][j]将是 1 如果字符串(I..j)是回文，否则为 0。在构造 isPalin 之后，我们将构造另一个 2D 数组 dp，dp[i][j]将告诉串(I)中回文子串的计数..j)
现在我们可以写出 isPalin 和 dp 值之间的关系，如下所示，

```
// isPalin[i][j] will be 1 if ith and jth characters 
// are equal and mid substring str(i+1..j-1) is also
// a palindrome
isPalin[i][j] = (str[i] == str[j]) and 
                (isPalin[i + 1][j – 1])

// Similar to set theory we can write the relation among
// dp values as,
// dp[i][j] will be addition of number of palindromes from 
// i to j-1 and i+1 to j  subtracting palindromes from i+1
// to j-1 because they are counted twice once in dp[i][j-1] 
// and then in dp[i + 1][j] plus 1 if str(i..j) is also a
// palindrome
dp[i][j] = dp[i][j-1] + dp[i+1][j] - dp[i+1][j-1] + 
                                     isPalin[i][j];
```

对于构建 dp 数组，解决方案的总时间复杂度将是 o(长度^ 2 ),然后是每个查询的 O(1)。

## C++

```
// C++ program to query number of palindromic
// substrings of a string in a range
#include <bits/stdc++.h>
using namespace std;
#define M 50

// Utility method to construct the dp array
void constructDP(int dp[M][M], string str)
{
    int l = str.length();

    // declare 2D array isPalin, isPalin[i][j] will
    // be 1 if str(i..j) is palindrome
    int isPalin[l + 1][l + 1];

    // initialize dp and isPalin array by zeros
    for (int i = 0; i <= l; i++) {
        for (int j = 0; j <= l; j++) {
            isPalin[i][j] = dp[i][j] = 0;
        }
    }

    // loop for starting index of range
    for (int i = l - 1; i >= 0; i--) {

        // initialize value for one character strings as 1
        isPalin[i][i] = 1;
        dp[i][i] = 1;

        // loop for ending index of range
        for (int j = i + 1; j < l; j++) {

            /* isPalin[i][j] will be 1 if ith and
               jth characters are equal and mid
               substring str(i+1..j-1) is also a
               palindrome             */
            isPalin[i][j] = (str[i] == str[j] && (i + 1 > j - 1 || isPalin[i + 1][j - 1]));

            /* dp[i][j] will be addition of number
               of palindromes from i to j-1 and i+1
               to j subtracting palindromes from i+1
               to j-1 (as counted twice) plus 1 if
               str(i..j) is also a palindrome */
            dp[i][j] = dp[i][j - 1] + dp[i + 1][j] - dp[i + 1][j - 1] + isPalin[i][j];
        }
    }
}

// method returns count of palindromic substring in range (l, r)
int countOfPalindromeInRange(int dp[M][M], int l, int r)
{
    return dp[l][r];
}

// Driver code to test above methods
int main()
{
    string str = "xyaabax";

    int dp[M][M];
    constructDP(dp, str);

    int l = 3;
    int r = 5;

    cout << countOfPalindromeInRange(dp, l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program  to query number of palindromic
// substrings of a string in a range
import java.io.*;

class GFG {
    // Function to construct the dp array
    static void constructDp(int dp[][], String str)
    {
        int l = str.length();

        // declare 2D array isPalin, isPalin[i][j] will
        // be 1 if str(i..j) is palindrome
        int[][] isPalin = new int[l + 1][l + 1];

        // initialize dp and isPalin array by zeros
        for (int i = 0; i <= l; i++) {
            for (int j = 0; j <= l; j++) {
                isPalin[i][j] = dp[i][j] = 0;
            }
        }

        // loop for starting index of range
        for (int i = l - 1; i >= 0; i--) {
            // initialize value for one character strings as 1
            isPalin[i][i] = 1;
            dp[i][i] = 1;

            // loop for ending index of range
            for (int j = i + 1; j < l; j++) {
                /* isPalin[i][j] will be 1 if ith and
                jth characters are equal and mid
                substring str(i+1..j-1) is also a
                palindrome             */
                isPalin[i][j] = (str.charAt(i) == str.charAt(j) && (i + 1 > j - 1 || (isPalin[i + 1][j - 1]) != 0)) ? 1 : 0;

                /* dp[i][j] will be addition of number
                of palindromes from i to j-1 and i+1
                to j subtracting palindromes from i+1
                to j-1 (as counted twice) plus 1 if
                str(i..j) is also a palindrome */
                dp[i][j] = dp[i][j - 1] + dp[i + 1][j] - dp[i + 1][j - 1] + isPalin[i][j];
            }
        }
    }

    // method returns count of palindromic substring in range (l, r)
    static int countOfPalindromeInRange(int dp[][], int l, int r)
    {
        return dp[l][r];
    }

    // driver program
    public static void main(String args[])
    {
        int MAX = 50;
        String str = "xyaabax";
        int[][] dp = new int[MAX][MAX];
        constructDp(dp, str);

        int l = 3;
        int r = 5;
        System.out.println(countOfPalindromeInRange(dp, l, r));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 program to query the number of
# palindromic substrings of a string in a range
M = 50

# Utility method to construct the dp array
def constructDP(dp, string):

    l = len(string)

    # declare 2D array isPalin, isPalin[i][j]
    # will be 1 if str(i..j) is palindrome
    # and initialize it with zero
    isPalin = [[0 for i in range(l + 1)]
                  for j in range(l + 1)]

    # loop for starting index of range
    for i in range(l - 1, -1, -1):

        # initialize value for one
        # character strings as 1
        isPalin[i][i], dp[i][i] = 1, 1

        # loop for ending index of range
        for j in range(i + 1, l):

            # isPalin[i][j] will be 1 if ith and jth
            # characters are equal and mid substring
            # str(i+1..j-1) is also a palindrome
            isPalin[i][j] = (string[i] == string[j] and
                            (i + 1 > j - 1 or isPalin[i + 1][j - 1]))

            # dp[i][j] will be addition of number
            # of palindromes from i to j-1 and i+1
            # to j subtracting palindromes from i+1
            # to j-1 (as counted twice) plus 1 if
            # str(i..j) is also a palindrome
            dp[i][j] = (dp[i][j - 1] + dp[i + 1][j] -
                        dp[i + 1][j - 1] + isPalin[i][j])

# Method returns count of palindromic
# substring in range (l, r)
def countOfPalindromeInRange(dp, l, r):
    return dp[l][r]

# Driver code
if __name__ == "__main__":

    string = "xyaabax"
    dp = [[0 for i in range(M)]
             for j in range(M)]

    constructDP(dp, string)

    l, r = 3, 5
    print(countOfPalindromeInRange(dp, l, r))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to query number of palindromic
// substrings of a string in a range
using System;

class GFG {

    // Function to construct the dp array
    static void constructDp(int[, ] dp, string str)
    {
        int l = str.Length;

        // declare 2D array isPalin, isPalin[i][j]
        // will be 1 if str(i..j) is palindrome
        int[, ] isPalin = new int[l + 1, l + 1];

        // initialize dp and isPalin array by zeros
        for (int i = 0; i <= l; i++) {
            for (int j = 0; j <= l; j++) {
                isPalin[i, j] = dp[i, j] = 0;
            }
        }

        // loop for starting index of range
        for (int i = l - 1; i >= 0; i--) {

            // initialize value for one
            // character strings as 1
            isPalin[i, i] = 1;
            dp[i, i] = 1;

            // loop for ending index of range
            for (int j = i + 1; j < l; j++) {

                /* isPalin[i][j] will be 1 if ith and
                jth characters are equal and mid
                substring str(i+1..j-1) is also a
                palindrome*/
                isPalin[i, j] = (str[i] == str[j] && (i + 1 > j - 1 ||
                                (isPalin[i + 1, j - 1]) != 0)) ? 1 : 0;

                /* dp[i][j] will be addition of number
                of palindromes from i to j-1 and i+1
                to j subtracting palindromes from i+1
                to j-1 (as counted twice) plus 1 if
                str(i..j) is also a palindrome */
                dp[i, j] = dp[i, j - 1] + dp[i + 1, j] -
                           dp[i + 1, j - 1] + isPalin[i, j];
            }
        }
    }

    // method returns count of palindromic
    // substring in range (l, r)
    static int countOfPalindromeInRange(int[, ] dp,
                                      int l, int r)
    {
        return dp[l, r];
    }

    // driver program
    public static void Main()
    {
        int MAX = 50;
        string str = "xyaabax";
        int[, ] dp = new int[MAX, MAX];
        constructDp(dp, str);

        int l = 3;
        int r = 5;
        Console.WriteLine(countOfPalindromeInRange(dp, l, r));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to query number of palindromic
// substrings of a string in a range

$GLOBALS['M'] = 50;

// Utility method to construct the dp array
function constructDP($dp, $str)
{
    $l = strlen($str);

    // declare 2D array isPalin, isPalin[i][j]
    // will be 1 if str(i..j) is palindrome
    $isPalin = array(array());

    // initialize dp and isPalin array by zeros
    for ($i = 0; $i <= $l; $i++)
    {
        for ($j = 0; $j <= $l; $j++)
        {
            $isPalin[$i][$j] = $dp[$i][$j] = 0;
        }
    }

    // loop for starting index of range
    for ($i = $l - 1; $i >= 0; $i--)
    {

        // initialize value for one character
        // strings as 1
        $isPalin[$i][$i] = 1;
        $dp[$i][$i] = 1;

        // loop for ending index of range
        for ($j = $i + 1; $j < $l; $j++)
        {

            /* isPalin[i][j] will be 1 if ith and
            jth characters are equal and mid
            substring str(i+1..j-1) is also a
            palindrome         */
            $isPalin[$i][$j] = ($str[$i] == $str[$j] &&
                               ($i + 1 > $j - 1 ||
                                $isPalin[$i + 1][$j - 1]));

            /* dp[i][j] will be addition of number
            of palindromes from i to j-1 and i+1
            to j subtracting palindromes from i+1
            to j-1 (as counted twice) plus 1 if
            str(i..j) is also a palindrome */
            $dp[$i][$j] = $dp[$i][$j - 1] + $dp[$i + 1][$j] -
                          $dp[$i + 1][$j - 1] + $isPalin[$i][$j];
        }
    }
    return $dp ;
}

// method returns count of palindromic
// substring in range (l, r)
function countOfPalindromeInRange($dp, $l, $r)
{
    return $dp[$l][$r];
}

// Driver code
$str = "xyaabax";

$dp = array(array());

for($i = 0; $i < $GLOBALS['M']; $i++ )
    for($j = 0; $j < $GLOBALS['M']; $j++)
        $dp[$i][$j] = 0;

$dp = constructDP($dp, $str);

$l = 3;
$r = 5;

echo countOfPalindromeInRange($dp, $l, $r);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript program  to query number of palindromic
    // substrings of a string in a range

    // Function to construct the dp array
    function constructDp(dp, str)
    {
        let l = str.length;

        // declare 2D array isPalin, isPalin[i][j] will
        // be 1 if str(i..j) is palindrome
        let isPalin = new Array(l + 1);

        // initialize dp and isPalin array by zeros
        for (let i = 0; i <= l; i++) {
            isPalin[i] = new Array(l + 1);
            for (let j = 0; j <= l; j++) {
                isPalin[i][j] = dp[i][j] = 0;
            }
        }

        // loop for starting index of range
        for (let i = l - 1; i >= 0; i--) {
            // initialize value for one character strings as 1
            isPalin[i][i] = 1;
            dp[i][i] = 1;

            // loop for ending index of range
            for (let j = i + 1; j < l; j++) {
                /* isPalin[i][j] will be 1 if ith and
                jth characters are equal and mid
                substring str(i+1..j-1) is also a
                palindrome             */
                isPalin[i][j] = (str[i] == str[j] && (i + 1 > j - 1 || (isPalin[i + 1][j - 1]) != 0)) ? 1 : 0;

                /* dp[i][j] will be addition of number
                of palindromes from i to j-1 and i+1
                to j subtracting palindromes from i+1
                to j-1 (as counted twice) plus 1 if
                str(i..j) is also a palindrome */
                dp[i][j] = dp[i][j - 1] + dp[i + 1][j] - dp[i + 1][j - 1] + isPalin[i][j];
            }
        }
    }

    // method returns count of palindromic substring in range (l, r)
    function countOfPalindromeInRange(dp, l, r)
    {
        return dp[l][r];
    }

    let MAX = 50;
    let str = "xyaabax";
    let dp = new Array(MAX);
    for (let i = 0; i < MAX; i++) {
      dp[i] = new Array(MAX);
      for (let j = 0; j < MAX; j++) {
        dp[i][j] = 0;
      }
    }

    constructDp(dp, str);

    let l = 3;
    let r = 5;
    document.write(countOfPalindromeInRange(dp, l, r));

</script>
```

**输出:**

```
4
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。