# 查找字符串是否为 K 回文|设置 2

> 原文:[https://www . geesforgeks . org/find-if-string-is-k-回文-or-not-set-2/](https://www.geeksforgeeks.org/find-if-string-is-k-palindrome-or-not-set-2/)

给定一个字符串，找出这个字符串是否是 K-回文。一个 K-回文串最多去掉 K 个字符就变成了回文。

示例:

```
Input : String - abcdecba, k = 1
Output : Yes
String can become palindrome by removing
1 character i.e. either d or e

Input  : String - abcdeca, K = 2
Output : Yes
Can become palindrome by removing
2 characters b and e (or b and d).

Input : String - acdcb, K = 1
Output : No
String can not become palindrome by
removing only one character.

```

我们在[之前的](https://www.geeksforgeeks.org/find-if-string-is-k-palindrome-or-not/)帖子中讨论了一个 DP 解决方案，我们看到这个问题基本上是[编辑距离](https://www.geeksforgeeks.org/dynamic-programming-set-5-edit-distance/)问题的变体。在这篇文章中，讨论了另一个有趣的 DP 解决方案。

其思想是找到给定字符串的最长回文子序列。如果最长回文子序列与原始字符串的差值小于或等于 k，则该字符串为 k 回文，否则不是 k 回文。

例如，字符串 **abcdeca** 的最长回文子序列是 **acdca** (或 aceca)。不构成字符串最长回文子序列的字符应被删除，以使字符串回文。所以从 abcdeca 中去掉 b 和 d(或 e)，字符串会变成回文。

使用 [LCS](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/) 可以很容易地找到字符串中最长的回文子序列。下面是使用 LCS 寻找最长回文子序列的两步解。

1.  反转给定的序列，并将反转存储在另一个数组中，比如 rev[0..n-1]
2.  给定序列的 LCS 和 rev[]将是最长的回文序列。

以下是上述想法的实施–

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find if given string is K-Palindrome
// or not
#include <bits/stdc++.h>
using namespace std;

/* Returns length of LCS for X[0..m-1], Y[0..n-1] */
int lcs( string X, string Y, int m, int n )
{
    int L[m + 1][n + 1];

    /* Following steps build L[m+1][n+1] in bottom up
        fashion. Note that L[i][j] contains length of
        LCS of X[0..i-1] and Y[0..j-1] */
    for (int i = 0; i <= m; i++)
    {
        for (int j = 0; j <= n; j++)
        {
            if (i == 0 || j == 0)
                L[i][j] = 0;
            else if (X[i - 1] == Y[j - 1])
                L[i][j] = L[i - 1][j - 1] + 1;
            else
                L[i][j] = max(L[i - 1][j], L[i][j - 1]);
        }
    }
    // L[m][n] contains length of LCS for X and Y
    return L[m][n];
}

// find if given string is K-Palindrome or not
bool isKPal(string str, int k)
{
    int n = str.length();

    // Find reverse of string
    string revStr = str;
    reverse(revStr.begin(), revStr.end());

    // find longest palindromic subsequence of
    // given string
    int lps = lcs(str, revStr, n, n);

    // If the difference between longest palindromic
    // subsequence and the original string is less
    // than equal to k, then the string is k-palindrome
    return (n - lps <= k);
}

// Driver program
int main()
{
    string str = "abcdeca";
    int k = 2;
    isKPal(str, k) ? cout << "Yes" : cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if given  
// String is K-Palindrome or not
class GFG 
{

    /* Returns length of LCS for
    X[0..m-1], Y[0..n-1] */
    static int lcs(String X, String Y,
                        int m, int n) 
    {
        int L[][] = new int[m + 1][n + 1];

        /* Following steps build L[m+1][n+1]
        in bottom up fashion. Note that L[i][j] 
        contains length of LCS of X[0..i-1]
        and Y[0..j-1] */
        for (int i = 0; i <= m; i++)
        {
            for (int j = 0; j <= n; j++) 
            {
                if (i == 0 || j == 0) 
                {
                    L[i][j] = 0;
                } 
                else if (X.charAt(i - 1) == Y.charAt(j - 1))
                {
                    L[i][j] = L[i - 1][j - 1] + 1;
                } 
                else
                {
                    L[i][j] = Math.max(L[i - 1][j], L[i][j - 1]);
                }
            }
        }
        // L[m][n] contains length 
        // of LCS for X and Y 
        return L[m][n];
    }

    // find if given String is
    // K-Palindrome or not 
    static boolean isKPal(String str, int k) 
    {
        int n = str.length();

        // Find reverse of String 
        StringBuilder revStr = new StringBuilder(str);
        revStr = revStr.reverse();

        // find longest palindromic 
        // subsequence of given String 
        int lps = lcs(str, revStr.toString(), n, n);

        // If the difference between longest  
        // palindromic subsequence and the  
        // original String is less than equal 
        // to k, then the String is k-palindrome 
        return (n - lps <= k);
    }

    // Driver code 
    public static void main(String[] args) 
    {
        String str = "abcdeca";
        int k = 2;
        if (isKPal(str, k))
        {
            System.out.println("Yes");
        }
        else
            System.out.println("No");
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python program to find
# if given string is K-Palindrome
# or not

# Returns length of LCS
# for X[0..m-1], Y[0..n-1] 
def lcs(X, Y, m, n ):

    L = [[0]*(n+1) for _ in range(m+1)]

    # Following steps build
        # L[m+1][n+1] in bottom up
        # fashion. Note that L[i][j]
        # contains length of
    # LCS of X[0..i-1] and Y[0..j-1] 
    for i in range(m+1):
        for j in range(n+1):
            if not i or not j:
                L[i][j] = 0
            elif X[i - 1] == Y[j - 1]:
                L[i][j] = L[i - 1][j - 1] + 1
            else:
                L[i][j] = max(L[i - 1][j], L[i][j - 1])

    # L[m][n] contains length
        # of LCS for X and Y
    return L[m][n]

# find if given string is
# K-Palindrome or not
def isKPal(string, k):

    n = len(string)

    # Find reverse of string
    revStr = string[::-1]

    # find longest palindromic
        # subsequence of
    # given string
    lps = lcs(string, revStr, n, n)

    # If the difference between
        # longest palindromic
    # subsequence and the original
        # string is less
    # than equal to k, then
        # the string is k-palindrome
    return (n - lps <= k)

# Driver program
string = "abcdeca"
k = 2

print("Yes" if isKPal(string, k) else "No")

# This code is contributed
# by Ansu Kumari.
```

## C#

```
// C# program to find if given 
// String is K-Palindrome or not 
using System;

class GFG 
{ 

    /* Returns length of LCS for 
    X[0..m-1], Y[0..n-1] */
    static int lcs(String X, String Y, 
                        int m, int n) 
    { 
        int [,]L = new int[m + 1,n + 1]; 

        /* Following steps build L[m+1,n+1] 
        in bottom up fashion. Note that L[i,j] 
        contains length of LCS of X[0..i-1] 
        and Y[0..j-1] */
        for (int i = 0; i <= m; i++) 
        { 
            for (int j = 0; j <= n; j++) 
            { 
                if (i == 0 || j == 0) 
                { 
                    L[i, j] = 0; 
                } 
                else if (X[i - 1] == Y[j - 1]) 
                { 
                    L[i, j] = L[i - 1, j - 1] + 1; 
                } 
                else
                { 
                    L[i, j] = Math.Max(L[i - 1, j],
                                        L[i, j - 1]); 
                } 
            } 
        } 

        // L[m,n] contains length 
        // of LCS for X and Y 
        return L[m, n]; 
    } 

    // find if given String is 
    // K-Palindrome or not 
    static bool isKPal(String str, int k) 
    { 
        int n = str.Length; 

        // Find reverse of String 
        str = reverse(str); 

        // find longest palindromic 
        // subsequence of given String 
        int lps = lcs(str, str, n, n); 

        // If the difference between longest 
        // palindromic subsequence and the 
        // original String is less than equal 
        // to k, then the String is k-palindrome 
        return (n - lps <= k); 
    } 
    static String reverse(String input)
    {
        char[] temparray = input.ToCharArray();
        int left, right = 0;
        right = temparray.Length - 1;

        for (left = 0; left < right; left++, right--) 
        {

            // Swap values of left and right 
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.Join("",temparray);
    }

    // Driver code 
    public static void Main(String[] args) 
    { 
        String str = "abcdeca"; 
        int k = 2; 
        if (isKPal(str, k)) 
        { 
            Console.WriteLine("Yes"); 
        } 
        else
            Console.WriteLine("No"); 
    } 
} 

// This code is contributed by PrinciRaj1992
```

**Output:**

```
Yes

```

**上述解的时间复杂度**为 O(n <sup>2</sup> )。
**程序使用的辅助空间**为 O(n <sup>2</sup> )。使用 LCS 的[空间优化解可以进一步简化为 O(n)。](https://www.geeksforgeeks.org/space-optimized-solution-lcs/)

感谢**拉维·泰贾·卡韦蒂**提出上述解决方案。

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。