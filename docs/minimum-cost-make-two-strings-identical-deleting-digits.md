# 通过删除数字

使两个字符串相同的最小成本

> 原文:[https://www . geesforgeks . org/最低成本-制作两个字符串-相同-删除数字/](https://www.geeksforgeeks.org/minimum-cost-make-two-strings-identical-deleting-digits/)

给定两个仅由数字“0”到“9”组成的字符串 X 和 Y。找出使给定的两个字符串相同所需的最小成本。唯一允许的操作是从任何字符串中删除字符。删除数字“d”的操作成本是 d 个单位。

```
Input:  X = 3759, Y = 9350
Output: 23
Explanation
For making both string identical, delete
characters 3, 7, 5 from first string and
delete characters 3, 5, 0 from second 
string. Total cost of operation is
3 + 7 + 5 + 3 + 5 + 0 = 23

Input:  X = 3198, Y = 98
Output: 4
```

这个问题是最长公共子序列( [LCS](https://www.geeksforgeeks.org/longest-common-subsequence/) )和[这个](https://www.geeksforgeeks.org/minimum-cost-make-two-strings-identical/)的一个变种。这个想法很简单，不是寻找最长公共子序列的**长度**，而是通过从两个字符串中添加**相同的字符**来寻找最大成本。
现在要找到最小成本，从两个字符串的总成本中减去上述结果，即

```
costX = Cost of removing all characters
        from string 'X'
CostY = Cost of removing all characters 
        from string 'Y'
cost_Id = Cost of removing identical characters
          from both strings

Minimum cost to make both string identical = 
                      costX + costY - cost_Id
```

以下是上述方法的实现:

## C++

```
/* C++ code to find minimum cost to make two strings
   identical */
#include <bits/stdc++.h>
using namespace std;

/* Function to returns cost of removing the identical
   characters in LCS for X[0..m-1], Y[0..n-1] */
int lcs(char* X, char* Y, int m, int n)
{
    int L[m + 1][n + 1];

    /* Following steps build L[m+1][n+1] in bottom
       up fashion. Note that L[i][j] contains cost
       of removing identical characters in LCS of
       X[0..i-1] and Y[0..j-1] */
    for (int i = 0; i <= m; ++i) {
        for (int j = 0; j <= n; j++) {

            if (i == 0 || j == 0)
                L[i][j] = 0;

            // If both characters are same, add both
            // of them
            else if (X[i - 1] == Y[j - 1])
                L[i][j] = L[i - 1][j - 1] +
                          2 * (X[i - 1] - '0');

            // Otherwise find the maximum cost among them
            else
                L[i][j] = max(L[i - 1][j], L[i][j - 1]);
        }
    }

    return L[m][n];
}

// Returns cost of making X[] and Y[] identical
int findMinCost(char X[], char Y[])
{
    // Find LCS of X[] and Y[]
    int m = strlen(X), n = strlen(Y);

    // Initialize the cost variable
    int cost = 0;

    // Find cost of all characters in
    // both strings
    for (int i = 0; i < m; ++i)
        cost += X[i] - '0';

    for (int i = 0; i < n; ++i)
        cost += Y[i] - '0';

    return cost - lcs(X, Y, m, n);
}

/* Driver program to test above function */
int main()
{
    char X[] = "3759";
    char Y[] = "9350";
    cout << "Minimum Cost to make two strings "
         << "identical is = " << findMinCost(X, Y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find minimum cost to
// make two strings identical
import java.util.*;
import java.lang.*;

public class GfG{

/* Function to returns cost of removing the identical
characters in LCS for X[0..m-1], Y[0..n-1] */
static int lcs(char[] X, char[] Y, int m, int n)
{
    int[][] L=new int[m + 1][n + 1];

    /* Following steps build L[m+1][n+1] in
    bottom up fashion. Note that L[i][j] contains
    cost of removing identical characters in
    LCS of X[0..i-1] and Y[0..j-1] */
    for (int i = 0; i <= m; ++i) {
        for (int j = 0; j <= n; j++) {

            if (i == 0 || j == 0)
                L[i][j] = 0;

            // If both characters are same,
            // add both of them
            else if (X[i - 1] == Y[j - 1])
                L[i][j] = L[i - 1][j - 1] +
                        2 * (X[i - 1] - '0');

            // Otherwise find the maximum
            // cost among them
            else
                L[i][j] = L[i - 1][j] > L[i][j - 1] ?
                          L[i - 1][j] : L[i][j - 1];
        }
    }

    return L[m][n];
}

// Returns cost of making X[] and Y[] identical
static int findMinCost(char X[], char Y[])
{
    // Find LCS of X[] and Y[]
    int m = X.length, n = Y.length;

    // Initialize the cost variable
    int cost = 0;

    // Find cost of all characters in
    // both strings
    for (int i = 0; i < m; ++i)
        cost += X[i] - '0';

    for (int i = 0; i < n; ++i)
        cost += Y[i] - '0';

    return cost - lcs(X, Y, m, n);
}

// driver function
    public static void main(String argc[]){

    char X[] = ("3759").toCharArray();
    char Y[] = ("9350").toCharArray();

    System.out.println("Minimum Cost to make two strings"+
                 " identical is = " +findMinCost(X, Y));
    }
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 code to find minimum cost to make two strings
#   identical

# Function to returns cost of removing the identical
# characters in LCS for X[0..m-1], Y[0..n-1]
def lcs(X, Y,  m,  n):
    L=[[0 for i in range(n+1)]for i in range(m+1)]

    # Following steps build L[m+1][n+1] in bottom
    # up fashion. Note that L[i][j] contains cost
    # of removing identical characters in LCS of
    # X[0..i-1] and Y[0..j-1]
    for i in range(m+1):
        for j in range(n+1):
            if (i == 0 or j == 0):
                L[i][j] = 0

            # If both characters are same, add both
            # of them
            elif (X[i - 1] == Y[j - 1]):
                L[i][j] = L[i - 1][j - 1] + 2 * (ord(X[i - 1]) - 48)

            # Otherwise find the maximum cost among them
            else:
                L[i][j] = max(L[i - 1][j], L[i][j - 1])
    return L[m][n]

# Returns cost of making X[] and Y[] identical
def findMinCost( X,  Y):
    # Find LCS of X[] and Y[]
    m = len(X)
    n = len(Y)
    # Initialize the cost variable
    cost = 0

    # Find cost of all acters in
    # both strings
    for i in range(m):
        cost += ord(X[i]) - 48

    for i in range(n):
        cost += ord(Y[i]) - 48
    ans=cost - lcs(X, Y, m, n)
    return ans

# Driver program to test above function
X = "3759"
Y = "9350"
print("Minimum Cost to make two strings ",
     "identical is = " ,findMinCost(X, Y))

#this code is contributed by sahilshelangia
```

## C#

```
// C# code to find minimum cost to
// make two strings identical
using System;

public class GfG{

    /* Function to returns cost of removing the identical
    characters in LCS for X[0..m-1], Y[0..n-1] */
    static int lcs(string X, string Y, int m, int n)
    {
        int [,]L=new int[m + 1,n + 1];

        /* Following steps build L[m+1][n+1] in
        bottom up fashion. Note that L[i][j] contains
        cost of removing identical characters in
        LCS of X[0..i-1] and Y[0..j-1] */
        for (int i = 0; i <= m; ++i) {
            for (int j = 0; j <= n; j++) {

                if (i == 0 || j == 0)
                    L[i,j] = 0;

                // If both characters are same,
                // add both of them
                else if (X[i - 1] == Y[j - 1])
                    L[i,j] = L[i - 1,j - 1] +
                            2 * (X[i - 1] - '0');

                // Otherwise find the maximum
                // cost among them
                else
                    L[i,j] = L[i - 1,j] > L[i,j - 1] ?
                            L[i - 1,j] : L[i,j - 1];
            }
        }

        return L[m,n];
    }

    // Returns cost of making X[] and Y[] identical
    static int findMinCost( string X, string Y)
    {
        // Find LCS of X[] and Y[]
        int m = X.Length, n = Y.Length;

        // Initialize the cost variable
        int cost = 0;

        // Find cost of all characters in
        // both strings
        for (int i = 0; i < m; ++i)
            cost += X[i] - '0';

        for (int i = 0; i < n; ++i)
            cost += Y[i] - '0';

        return cost - lcs(X, Y, m, n);
    }

    // Driver function
    public static void Main()
    {
        string X = "3759";
        string Y= "9350";

        Console.WriteLine("Minimum Cost to make two strings"+
                    " identical is = " +findMinCost(X, Y));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find minimum cost to
// make two strings identical

/* Function to returns cost of removing the identical
characters in LCS for X[0..m-1], Y[0..n-1] */
function lcs( $X, $Y, $m, $n)
{
    $L = array($m + 1,$n+ 1);

    /* Following steps build L[m+1][n+1] in
    bottom up fashion. Note that L[i][j] contains
    cost of removing identical characters in
    LCS of X[0..i-1] and Y[0..j-1] */
    for ($i = 0; $i <= $m; ++$i)
    {
        for ($j = 0; $j <= $n; $j++)
        {

            if ($i == 0 || $j == 0)
                $L[$i][$j] = 0;

            // If both characters are same,
            // add both of them
            else if ($X[$i - 1] == $Y[$j - 1])
                $L[$i][$j] = $L[$i - 1][$j - 1] +
                        2 * ($X[$i - 1] - '0');

            // Otherwise find the maximum
            // cost among them
            else
                $L[$i][$j] = $L[$i - 1][$j] > $L[$i][$j - 1] ?
                        $L[$i - 1][$j] : $L[$i][$j - 1];
        }
    }

    return $L[$m][$n];
}

// Returns cost of making X[] and Y[] identical
function findMinCost($X, $Y)
{
    // Find LCS of X[] and Y[]
    $m = sizeof($X); $n = sizeof($Y);

    // Initialize the cost variable
    $cost = 0;

    // Find cost of all characters in
    // both strings
    for ($i = 0; $i < $m; ++$i)
        $cost += $X[$i] - '0';

    for ($i = 0; $i < $n; ++$i)
        $cost += $Y[$i] - '0';

    return $cost - lcs($X, $Y, $m, $n);
}

// Driver code

    $X = str_split("3759");
    $Y = str_split("9350");

    echo("Minimum Cost to make two strings".
                " identical is = " .findMinCost($X, $Y));

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>
    // Javascript code to find minimum cost to make two strings identical

    /* Function to returns cost of removing the identical
    characters in LCS for X[0..m-1], Y[0..n-1] */
    function lcs(X, Y, m, n)
    {
        let L=new Array(m + 1);

        for (let i = 0; i <= m; ++i)
        {
            L[i] = new Array(n + 1);
            for (let j = 0; j <= n; j++)
            {
                L[i][j] = 0;
            }
        }

        /* Following steps build L[m+1][n+1] in
        bottom up fashion. Note that L[i][j] contains
        cost of removing identical characters in
        LCS of X[0..i-1] and Y[0..j-1] */
        for (let i = 0; i <= m; ++i) {
            for (let j = 0; j <= n; j++) {

                if (i == 0 || j == 0)
                    L[i][j] = 0;

                // If both characters are same,
                // add both of them
                else if (X[i - 1] == Y[j - 1])
                    L[i][j] = L[i - 1][j - 1] +
                            2 * (X[i - 1] - '0');

                // Otherwise find the maximum
                // cost among them
                else
                    L[i][j] = L[i - 1][j] > L[i][j - 1] ?
                              L[i - 1][j] : L[i][j - 1];
            }
        }

        return L[m][n];
    }

    // Returns cost of making X[] and Y[] identical
    function findMinCost(X, Y)
    {
        // Find LCS of X[] and Y[]
        let m = X.length, n = Y.length;

        // Initialize the cost variable
        let cost = 0;

        // Find cost of all characters in
        // both strings
        for (let i = 0; i < m; ++i)
            cost += X[i].charCodeAt() - '0'.charCodeAt();

        for (let i = 0; i < n; ++i)
            cost += Y[i].charCodeAt() - '0'.charCodeAt();

        return cost - lcs(X, Y, m, n);
    }

    let X = ("3759").split('');
    let Y = ("9350").split('');

    document.write("Minimum Cost to make two strings"+
                 " identical is = " +findMinCost(X, Y));

</script>
```

**输出:**

```
Minimum Cost to make two strings  identical is = 23
```

**时间复杂度:**O(m * n)
T3】辅助空间: O(m*n)