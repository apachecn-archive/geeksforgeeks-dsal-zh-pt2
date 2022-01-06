# 使两个数字串相同的最小成本

> 原文:[https://www . geesforgeks . org/两个数字字符串相同的最小制作成本/](https://www.geeksforgeeks.org/minimum-cost-to-make-two-numeric-strings-identical/)

给定两个数字字符串，A 和 b。数字字符串是只包含数字['0'-'9']的字符串。
任务是使两个字符串在最小成本上相等。您被允许做的唯一操作是从任何字符串(A 或 B)中删除一个字符(即数字)。删除一个数字 D 的成本是 D 个单位。
**示例** :

> **输入**:A =【7135】，B =【135】
> **输出** : 7
> 要使两个字符串完全相同，我们必须从字符串 A 中删除‘7’。
> **输入**:A =【9142】，B =【1429】
> **输出** : 14
> 有两种方法可以使字符串“9142”与“1429”完全相同，即通过删除从两个字符串中删除 142 将花费 2*(1+4+2)=14，这比删除“9”更理想。

这个问题是一个流行的动态规划问题的变种-[最长公共子序列](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)。想法是找到**最大权重公共子序列**，这将是我们需要的最佳相同字符串。要计算删除成本，从字符串 A 和 b 的总和中减去最大权重公共子序列的总和

> **使字符串相同的最小重量= Costa+costB–2 *(LCS 成本)**

以下是上述思路的实现:

## C++

```
// CPP program to find minimum cost to make
// two numeric strings identical

#include <bits/stdc++.h>

using namespace std;

typedef long long int ll;

// Function to find weight of LCS
int lcs(int dp[101][101], string a, string b,
        int m, int n)
{
    for (int i = 0; i < 100; i++)
        for (int j = 0; j < 100; j++)
            dp[i][j] = -1;

    if (m < 0 || n < 0) {
        return 0;
    }

    // if this state is already
    // calculated then return
    if (dp[m][n] != -1)
        return dp[m][n];

    int ans = 0;
    if (a[m] == b[n]) {
        // adding required weight for
        // particular match
        ans = int(a[m] - 48) + lcs(dp, a, b,
                                   m - 1, n - 1);
    }
    else
        // recurse for left and right child
        // and store the max
        ans = max(lcs(dp, a, b, m - 1, n),
                  lcs(dp, a, b, m, n - 1));

    dp[m][n] = ans;
    return ans;
}

// Function to calculate cost of string
int costOfString(string str)
{
    int cost = 0;

    for (int i = 0; i < str.length(); i++)
        cost += int(str[i] - 48);

    return cost;
}

// Driver code
int main()
{
    string a, b;

    a = "9142";
    b = "1429";

    int dp[101][101];

    // Minimum cost needed to make two strings identical
    cout << (costOfString(a) + costOfString(b) -
                       2 * lcs(dp, a, b, a.length() - 1,
                                       b.length() - 1));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum cost to make
// two numeric strings identical

import java.io.*;

class GFG {

// Function to find weight of LCS
 static int lcs(int dp[][], String a, String b,
        int m, int n)
{
    for (int i = 0; i < 100; i++)
        for (int j = 0; j < 100; j++)
            dp[i][j] = -1;

    if (m < 0 || n < 0) {
        return 0;
    }

    // if this state is already
    // calculated then return
    if (dp[m][n] != -1)
        return dp[m][n];

    int ans = 0;
    if (a.charAt(m) == b.charAt(n)) {
        // adding required weight for
        // particular match
        ans = (a.charAt(m) - 48) + lcs(dp, a, b,
                                m - 1, n - 1);
    }
    else
        // recurse for left and right child
        // and store the max
        ans = Math.max(lcs(dp, a, b, m - 1, n),
                lcs(dp, a, b, m, n - 1));

    dp[m][n] = ans;
    return ans;
}

// Function to calculate cost of string
 static int costOfString(String str)
{
    int cost = 0;

    for (int i = 0; i < str.length(); i++)
        cost += (str.charAt(i) - 48);

    return cost;
}

// Driver code
    public static void main (String[] args) {
            String a, b;

    a = "9142";
    b = "1429";

    int dp[][] = new int[101][101];

    // Minimum cost needed to make two strings identical
    System.out.print( (costOfString(a) + costOfString(b) -
                    2 * lcs(dp, a, b, a.length() - 1,
                                    b.length() - 1)));

    }
}
// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to find minimum cost
# to make two numeric strings identical

# Function to find weight of LCS
def lcs(dp, a, b, m, n):

    for i in range(100):
        for j in range(100):
            dp[i][j] = -1

    if (m < 0 or n < 0) :
        return 0

    # if this state is already calculated
    # then return
    if (dp[m][n] != -1):
        return dp[m][n]

    ans = 0
    if (a[m] == b[n]):

        # adding required weight for
        # particular match
        ans = (ord(a[m]) - 48) + lcs(dp, a, b,
                                     m - 1, n - 1)

    else:

        # recurse for left and right child
        # and store the max
        ans = max(lcs(dp, a, b, m - 1, n),
                  lcs(dp, a, b, m, n - 1))

    dp[m][n] = ans
    return ans

# Function to calculate cost of string
def costOfString(s):

    cost = 0

    for i in range(len(s)):
        cost += (ord(s[i]) - 48)

    return cost

# Driver code
if __name__ == "__main__":

    a = "9142"
    b = "1429"

    dp = [[0 for x in range(101)]
             for y in range(101)]

    # Minimum cost needed to make two
    # strings identical
    print(costOfString(a) + costOfString(b) - 2 *
           lcs(dp, a, b, len(a) - 1, len(b) - 1))

# This code is contributed by ita_c
```

## C#

```
// C# program to find minimum cost to make
// two numeric strings identical
using System;
public class GFG {

// Function to find weight of LCS
static int lcs(int [,]dp, String a, String b,
        int m, int n)
{
    for (int i = 0; i < 100; i++)
        for (int j = 0; j < 100; j++)
            dp[i,j] = -1;

    if (m < 0 || n < 0) {
        return 0;
    }

    // if this state is already
    // calculated then return
    if (dp[m,n] != -1)
        return dp[m,n];

    int ans = 0;
    if (a[m] == b[n]) {
        // adding required weight for
        // particular match
        ans = (a[m] - 48) + lcs(dp, a, b, m - 1, n - 1);
    }
    else
        // recurse for left and right child
        // and store the max
        ans = Math.Max(lcs(dp, a, b, m - 1, n),
                lcs(dp, a, b, m, n - 1));

    dp[m,n] = ans;
    return ans;
}

// Function to calculate cost of string
static int costOfString(String str)
{
    int cost = 0;

    for (int i = 0; i < str.Length; i++)
        cost += (str[i] - 48);

    return cost;
}

// Driver code
    public static void Main () {
            String a, b;

    a = "9142";
    b = "1429";

    int [,]dp = new int[101,101];

    // Minimum cost needed to make two strings identical
    Console.Write( (costOfString(a) + costOfString(b) -
                2 * lcs(dp, a, b, a.Length- 1,
                b.Length - 1)));

    }
}
// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to find minimum cost to make
// two numeric strings identical

    // Function to find weight of LCS
    function lcs(dp,a,b,m,n)
    {

    if (m < 0 || n < 0) {
        return 0;
    }

    // if this state is already
    // calculated then return
    if (dp[m][n] != -1)
        return dp[m][n];

    let ans = 0;
    if (a[m] == b[n]) {
        // adding required weight for
        // particular match
        ans = (a[m].charCodeAt(0) - 48) + lcs(dp, a, b,
                                m - 1, n - 1);
    }
    else
        // recurse for left and right child
        // and store the max
        ans = Math.max(lcs(dp, a, b, m - 1, n),
                lcs(dp, a, b, m, n - 1));

    dp[m][n] = ans;
    return ans;
    }

    // Function to calculate cost of string
    function costOfString(str)
    {
        let cost = 0;

    for (let i = 0; i < str.length; i++)
        cost += (str[i].charCodeAt(0) - 48);

    return cost;
    }

    // Driver code
    let a = "9142";
    let b = "1429";
    let dp=new Array(101);
    for(let i=0;i<dp.length;i++)
    {
        dp[i]=new Array(101);
        for(let j=0;j<101;j++)
        {
            dp[i][j]=-1;
        }
    }
    // Minimum cost needed to make two strings identical
    document.write( (costOfString(a) + costOfString(b) -
                    2 * lcs(dp, a, b, a.length - 1,
                                    b.length - 1)));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
14
```