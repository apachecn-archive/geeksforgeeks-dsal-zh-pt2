# 使两个字符串相同的最小成本

> 原文:[https://www . geeksforgeeks . org/最低成本-两串相同/](https://www.geeksforgeeks.org/minimum-cost-make-two-strings-identical/)

给定两个字符串 X 和 Y，以及两个值 costX 和 costY。我们需要找到使给定的两个字符串相同所需的最小成本。我们可以从两个字符串中删除字符。从字符串 X 中删除一个字符的成本是成本 X，从字符串 Y 中删除一个字符的成本是成本 Y。从字符串中删除所有字符的成本是相同的。

**示例:**

```
Input :  X = "abcd", Y = "acdb", costX = 10, costY = 20.
Output:  30
For Making both strings identical we have to delete 
character 'b' from both the string, hence cost will
be = 10 + 20 = 30.

Input :  X = "ef", Y = "gh", costX = 10, costY = 20.
Output:  60
For making both strings identical, we have to delete 2-2
characters from both the strings, hence cost will be =
 10 + 10 + 20 + 20 = 60.
```

这个问题是最长公共子序列 [( LCS )](https://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/) 的一个变种。想法很简单，我们首先找到字符串 X 和 y 的最长公共子序列的长度。现在用单个字符串的长度减去 len_LCS，得到要删除的字符数，使它们相同。

```
// Cost of making two strings identical is SUM of following two
//   1) Cost of removing extra characters (other than LCS) 
//      from X[]
//   2) Cost of removing extra characters (other than LCS) 
//      from Y[]
Minimum Cost to make strings identical = costX * (m - len_LCS) + 
                                         costY * (n - len_LCS).  

m ==> Length of string X
m ==> Length of string Y
len_LCS ==> Length of LCS Of X and Y.
costX ==> Cost of removing a character from X[]
costY ==> Cost of removing a character from Y[]

Note that cost of removing all characters from a string
is same.               
```

以下是上述想法的实现。

## C++

```
/* C++ code to find minimum cost to make two strings
   identical */
#include<bits/stdc++.h>
using namespace std;

/* Returns length of LCS for X[0..m-1], Y[0..n-1] */
int lcs(char *X, char *Y, int m, int n)
{
    int L[m+1][n+1];

    /* Following steps build L[m+1][n+1] in bottom
       up fashion. Note that L[i][j] contains length
       of LCS of X[0..i-1] and Y[0..j-1] */
    for (int i=0; i<=m; i++)
    {
        for (int j=0; j<=n; j++)
        {
            if (i == 0 || j == 0)
                L[i][j] = 0;

            else if (X[i-1] == Y[j-1])
                L[i][j] = L[i-1][j-1] + 1;

            else
                L[i][j] = max(L[i-1][j], L[i][j-1]);
        }
    }

    /* L[m][n] contains length of LCS for X[0..n-1] and
       Y[0..m-1] */
    return L[m][n];
}

// Returns cost of making X[] and Y[] identical.  costX is
// cost of removing a character from X[] and costY is cost
// of removing a character from Y[]/
int findMinCost(char X[], char Y[], int costX, int costY)
{
    // Find LCS of X[] and Y[]
    int m = strlen(X), n = strlen(Y);
    int len_LCS = lcs(X, Y, m, n);

    // Cost of making two strings identical is SUM of
    // following two
    //   1) Cost of removing extra characters
    //      from first string
    //   2) Cost of removing extra characters from
    //      second string
    return costX * (m - len_LCS) +
           costY * (n - len_LCS);
}

/* Driver program to test above function */
int main()
{
    char X[] = "ef";
    char Y[] = "gh";
    cout << "Minimum Cost to make two strings "
         << " identical is = " << findMinCost(X, Y, 10, 20);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find minimum cost to
// make two strings identical
import java.io.*;

class GFG {

    // Returns length of LCS for X[0..m-1], Y[0..n-1]
    static int lcs(String X, String Y, int m, int n)
    {
        int L[][]=new int[m + 1][n + 1];

        /* Following steps build L[m+1][n+1] in bottom
        up fashion. Note that L[i][j] contains length
        of LCS of X[0..i-1] and Y[0..j-1] */
        for (int i = 0; i <= m; i++)
        {
            for (int j = 0; j <= n; j++)
            {
                if (i == 0 || j == 0)
                    L[i][j] = 0;

                else if (X.charAt(i - 1) == Y.charAt(j - 1))
                    L[i][j] = L[i - 1][j - 1] + 1;

                else
                    L[i][j] = Math.max(L[i - 1][j], L[i][j - 1]);
            }
        }

        // L[m][n] contains length of LCS
        // for X[0..n-1] and Y[0..m-1]
        return L[m][n];
    }

    // Returns cost of making X[] and Y[] identical.
    // costX is cost of removing a character from X[]
    // and costY is cost of removing a character from Y[]/
    static int findMinCost(String X, String Y, int costX, int costY)
    {
        // Find LCS of X[] and Y[]
        int m = X.length();
        int n = Y.length();
        int len_LCS;
        len_LCS = lcs(X, Y, m, n);

        // Cost of making two strings identical
        //  is SUM of following two
        // 1) Cost of removing extra characters
        // from first string
        // 2) Cost of removing extra characters
        // from second string
        return costX * (m - len_LCS) +
               costY * (n - len_LCS);
    }

    // Driver code
    public static void main (String[] args)
    {
        String X = "ef";
        String Y = "gh";
        System.out.println( "Minimum Cost to make two strings "
                            + " identical is = "
                            + findMinCost(X, Y, 10, 20));

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python code to find minimum cost
# to make two strings identical

# Returns length of LCS for
# X[0..m-1], Y[0..n-1]
def lcs(X, Y, m, n):
    L = [[0 for i in range(n + 1)]
            for i in range(m + 1)]

    # Following steps build
    # L[m+1][n+1] in bottom
    # up fashion. Note that
    # L[i][j] contains length
    # of LCS of X[0..i-1] and Y[0..j-1]
    for i in range(m + 1):
        for j in range(n + 1):
            if i == 0 or j == 0:
                L[i][j] = 0
            elif X[i - 1] == Y[j - 1]:
                L[i][j] = L[i - 1][j - 1] + 1
            else:
                L[i][j] = max(L[i - 1][j],
                              L[i][j - 1])
        # L[m][n] contains length of
        # LCS for X[0..n-1] and Y[0..m-1]
    return L[m][n]

# Returns cost of making X[]
# and Y[] identical. costX is
# cost of removing a character
# from X[] and costY is cost
# of removing a character from Y[]
def findMinCost(X, Y, costX, costY):

    # Find LCS of X[] and Y[]
    m = len(X)
    n = len(Y)
    len_LCS =lcs(X, Y, m, n)

    # Cost of making two strings
    # identical is SUM of following two
    # 1) Cost of removing extra 
    # characters from first string
    # 2) Cost of removing extra
    # characters from second string
    return (costX * (m - len_LCS) +
            costY * (n - len_LCS))

# Driver Code
X = "ef"
Y = "gh"
print('Minimum Cost to make two strings ', end = '')
print('identical is = ', findMinCost(X, Y, 10, 20))

# This code is contributed
# by sahilshelangia
```

## C#

```
// C# code to find minimum cost to
// make two strings identical
using System;

class GFG {

    // Returns length of LCS for X[0..m-1], Y[0..n-1]
    static int lcs(String X, String Y, int m, int n)
    {
        int [,]L = new int[m + 1, n + 1];

        /* Following steps build L[m+1][n+1] in bottom
           up fashion. Note that L[i][j] contains length
           of LCS of X[0..i-1] and Y[0..j-1] */
        for (int i = 0; i <= m; i++)
        {
            for (int j = 0; j <= n; j++)
            {
                if (i == 0 || j == 0)
                    L[i,j] = 0;

                else if (X[i - 1] == Y[j - 1])
                    L[i,j] = L[i - 1,j - 1] + 1;

                else
                    L[i,j] = Math.Max(L[i - 1,j], L[i,j - 1]);
            }
        }

        // L[m][n] contains length of LCS
        // for X[0..n-1] and Y[0..m-1]
        return L[m,n];
    }

    // Returns cost of making X[] and Y[] identical.
    // costX is cost of removing a character from X[]
    // and costY is cost of removing a character from Y[]
    static int findMinCost(String X, String Y,
                           int costX, int costY)
    {
        // Find LCS of X[] and Y[]
        int m = X.Length;
        int n = Y.Length;
        int len_LCS;
        len_LCS = lcs(X, Y, m, n);

        // Cost of making two strings identical
        // is SUM of following two
        // 1) Cost of removing extra characters
        // from first string
        // 2) Cost of removing extra characters
        // from second string
        return costX * (m - len_LCS) +
               costY * (n - len_LCS);
    }

    // Driver code
    public static void Main ()
    {
        String X = "ef";
        String Y = "gh";
        Console.Write( "Minimum Cost to make two strings " +
                       " identical is = " +
                       findMinCost(X, Y, 10, 20));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
/* PHP code to find minimum cost to make two strings
   identical */

/* Returns length of LCS for X[0..m-1], Y[0..n-1] */
function lcs($X, $Y, $m, $n)
{
    $L = array_fill(0,($m+1),array_fill(0,($n+1),NULL));

    /* Following steps build L[m+1][n+1] in bottom
       up fashion. Note that L[i][j] contains length
       of LCS of X[0..i-1] and Y[0..j-1] */
    for ($i=0; $i<=$m; $i++)
    {
        for ($j=0; $j<=$n; $j++)
        {
            if ($i == 0 || $j == 0)
                $L[$i][$j] = 0;

            else if ($X[$i-1] == $Y[$j-1])
                $L[$i][$j] = $L[$i-1][$j-1] + 1;

            else
                $L[$i][$j] = max($L[$i-1][$j], $L[$i][$j-1]);
        }
    }

    /* L[m][n] contains length of LCS for X[0..n-1] and
       Y[0..m-1] */
    return $L[$m][$n];
}

// Returns cost of making X[] and Y[] identical.  costX is
// cost of removing a character from X[] and costY is cost
// of removing a character from Y[]/
function findMinCost(&$X, &$Y,$costX, $costY)
{
    // Find LCS of X[] and Y[]
    $m = strlen($X);
    $n = strlen($Y);
    $len_LCS = lcs($X, $Y, $m, $n);

    // Cost of making two strings identical is SUM of
    // following two
    //   1) Cost of removing extra characters
    //      from first string
    //   2) Cost of removing extra characters from
    //      second string
    return $costX * ($m - $len_LCS) +
           $costY * ($n - $len_LCS);
}

/* Driver program to test above function */
$X = "ef";
$Y = "gh";
echo "Minimum Cost to make two strings ".
          " identical is = " . findMinCost($X, $Y, 10, 20);
return 0;
?>
```

## java 描述语言

```
<script>
// Javascript code to find minimum cost to
// make two strings identical

    // Returns length of LCS for X[0..m-1], Y[0..n-1]
    function lcs(X, Y, m, n)
    {
        let L = new Array(m+1);

        for(let i = 0; i < m + 1; i++)
        {
            L[i] = new Array(n + 1);
        }

        for(let i = 0; i < m + 1; i++)
        {
            for(let j = 0; j < n + 1; j++)
            {
                L[i][j] = 0;
            }
        }

        /* Following steps build L[m+1][n+1] in bottom
        up fashion. Note that L[i][j] contains length
        of LCS of X[0..i-1] and Y[0..j-1] */
        for (let i = 0; i <= m; i++)
        {
            for (let j = 0; j <= n; j++)
            {
                if (i == 0 || j == 0)
                    L[i][j] = 0;

                else if (X[i-1] == Y[j-1])
                    L[i][j] = L[i - 1][j - 1] + 1;

                else
                    L[i][j] = Math.max(L[i - 1][j], L[i][j - 1]);
            }
        }

        // L[m][n] contains length of LCS
        // for X[0..n-1] and Y[0..m-1]
        return L[m][n];
    }

    // Returns cost of making X[] and Y[] identical.
    // costX is cost of removing a character from X[]
    // and costY is cost of removing a character from Y[]/

    function findMinCost(X,Y,costX,costY)
    {
         // Find LCS of X[] and Y[]
        let m = X.length;
        let n = Y.length;
        let len_LCS;
        len_LCS = lcs(X, Y, m, n);

        // Cost of making two strings identical
        //  is SUM of following two
        // 1) Cost of removing extra characters
        // from first string
        // 2) Cost of removing extra characters
        // from second string
        return costX * (m - len_LCS) +
               costY * (n - len_LCS);

    }

    // Driver code
    let  X = "ef";
    let Y = "gh";
    document.write( "Minimum Cost to make two strings "
                            + " identical is = "
                            + findMinCost(X, Y, 10, 20));

    // This code is contributed by avanitrachhadiya2155
</script>
```

输出:

```
  Minimum Cost to make two strings identical is = 60
```

本文由 [**沙莎克·米什拉(古卢)**](https://auth.geeksforgeeks.org/profile.php?user=Shashank%20Mishra&list=practice) 供稿。本文由 geeksforgeeks 团队审阅。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。