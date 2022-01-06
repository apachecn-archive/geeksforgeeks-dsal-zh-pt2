# 计算将两根弦的 LCS 长度增加一的方法

> 原文:[https://www . geesforgeks . org/count-way-address-LCS-length-two-string-one/](https://www.geeksforgeeks.org/count-ways-increase-lcs-length-two-strings-one/)

给定两个低字母表字符的字符串，我们需要找到在第一个字符串中插入一个字符的方法的数量，使得两个字符串的 [LCS](https://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/) 的长度增加一。

**示例:**

```
Input : str1 = “abab”, str2 = “abc”
Output : 3
LCS length of given two strings is 2.
There are 3 ways of insertion in str1, 
to increase the LCS length by one which 
are enumerated below, 
str1 = “abcab”    str2 = “abc”  LCS length = 3
str1 = “abacb”    str2 = “abc”  LCS length = 3
str1 = “ababc”    str2 = “abc”  LCS length = 3

Input : str1 = “abcabc”, str2 = “abcd”
Output : 4

```

我们的想法是在第一个字符串的每个位置尝试所有 26 个可能的字符，如果 str1 的长度是 m，那么可以在(m + 1)个位置插入一个新的字符，现在假设在任何时候在 str1 的第 I 个位置插入字符 c，那么我们将把它与 str2 中具有字符 c 的所有位置进行匹配。假设一个这样的位置是 j，那么为了使总 LCS 长度比前一个多一个，下面的条件应该满足，

```
LCS(str1[1, m], str2[1, n]) = LCS(str1[1, i],  str2[1, j-1]) + 
                              LCS(str1[i+1, m], str2[j+1, n])  

```

上面的等式表明，在插入的字符处后缀和前缀子串的 LCS 之和必须与字符串的总 LCS 数相同，因此当在第一个字符串中插入相同的字符时，LCS 长度将增加 1。
在下面的代码中，两个 2D 数组 lcsl 和 lcsr 分别用于存储字符串的前缀和后缀的 LCS。填充这些 2D 阵列的方法可以在这里找到[。](https://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/)

请参见下面的代码，以便更好地理解，

## C++

```
// C++ program to get number of ways to increase
// LCS by 1
#include <bits/stdc++.h>
using namespace std;

#define M 26

// Utility method to get integer position of lower
// alphabet character
int toInt(char ch)
{
    return (ch - 'a');
}

// Method returns total ways to increase LCS length by 1
int waysToIncreaseLCSBy1(string str1, string str2)
{
    int m = str1.length(), n = str2.length();

    // Fill positions of each character in vector
    vector<int> position[M];
    for (int i = 1; i <= n; i++)
        position[toInt(str2[i-1])].push_back(i);

    int lcsl[m + 2][n + 2];
    int lcsr[m + 2][n + 2];

    // Initializing 2D array by 0 values
    for (int i = 0; i <= m+1; i++)
        for (int j = 0; j <= n + 1; j++)
            lcsl[i][j] = lcsr[i][j] = 0;

    // Filling LCS array for prefix substrings
    for (int i = 1; i <= m; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            if (str1[i-1] == str2[j-1])
                lcsl[i][j] = 1 + lcsl[i-1][j-1];
            else
                lcsl[i][j] = max(lcsl[i-1][j],
                                lcsl[i][j-1]);
        }
    }

    // Filling LCS array for suffix substrings
    for (int i = m; i >= 1; i--)
    {
        for (int j = n; j >= 1; j--)
        {
            if (str1[i-1] == str2[j-1])
                lcsr[i][j] = 1 + lcsr[i+1][j+1];
            else
                lcsr[i][j] = max(lcsr[i+1][j],
                                 lcsr[i][j+1]);
        }
    }

    // Looping for all possible insertion positions
    // in first string
    int ways = 0;
    for (int i=0; i<=m; i++)
    {
        // Trying all possible lower case characters
        for (char c='a'; c<='z'; c++)
        {
            // Now for each character, loop over same
            // character positions in second string
            for (int j=0; j<position[toInt(c)].size(); j++)
            {
                int p = position[toInt(c)][j];

                // If both, left and right substrings make
                // total LCS then increase result by 1
                if (lcsl[i][p-1] + lcsr[i+1][p+1] == lcsl[m][n])
                    ways++;
            }
        }
    }

    return ways;
}

//  Driver code to test above methods
int main()
{
    string str1 = "abcabc";
    string str2 = "abcd";
    cout << waysToIncreaseLCSBy1(str1, str2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get number of ways to increase
// LCS by 1
import java.util.*;

class GFG
{
    static int M = 26;

    // Method returns total ways to increase
    // LCS length by 1
    static int waysToIncreaseLCSBy1(String str1,
                                    String str2)
    {
        int m = str1.length(), n = str2.length();

        // Fill positions of each character in vector
        Vector<Integer>[] position = new Vector[M];
        for (int i = 0; i < M; i++)
            position[i] = new Vector<>();

        for (int i = 1; i <= n; i++)
            position[str2.charAt(i - 1) - 'a'].add(i);

        int[][] lcsl = new int[m + 2][n + 2];
        int[][] lcsr = new int[m + 2][n + 2];

        // Initializing 2D array by 0 values
        for (int i = 0; i <= m + 1; i++)
            for (int j = 0; j <= n + 1; j++)
                lcsl[i][j] = lcsr[i][j] = 0;

        // Filling LCS array for prefix substrings
        for (int i = 1; i <= m; i++)
        {
            for (int j = 1; j <= n; j++)
            {
                if (str1.charAt(i - 1) == str2.charAt(j - 1))
                    lcsl[i][j] = 1 + lcsl[i - 1][j - 1];
                else
                    lcsl[i][j] = Math.max(lcsl[i - 1][j],
                                          lcsl[i][j - 1]);
            }
        }

        // Filling LCS array for suffix substrings
        for (int i = m; i >= 1; i--)
        {
            for (int j = n; j >= 1; j--)
            {
                if (str1.charAt(i - 1) == str2.charAt(j - 1))
                    lcsr[i][j] = 1 + lcsr[i + 1][j + 1];
                else
                    lcsr[i][j] = Math.max(lcsr[i + 1][j],
                                          lcsr[i][j + 1]);
            }
        }

        // Looping for all possible insertion positions
        // in first string
        int ways = 0;
        for (int i = 0; i <= m; i++)
        {

            // Trying all possible lower case characters
            for (char d = 0; d < 26; d++)
            {

                // Now for each character, loop over same
                // character positions in second string
                for (int j = 0; j < position[d].size(); j++)
                {
                    int p = position[d].elementAt(j);

                    // If both, left and right substrings make
                    // total LCS then increase result by 1
                    if (lcsl[i][p - 1] +
                        lcsr[i + 1][p + 1] == lcsl[m][n])
                        ways++;
                }
            }
        }
        return ways;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str1 = "abcabc";
        String str2 = "abcd";
        System.out.println(waysToIncreaseLCSBy1(str1, str2));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to get number of ways to increase
# LCS by 1

M = 26

# Method returns total ways to increase LCS length by 1
def waysToIncreaseLCSBy1(str1, str2):
    m = len(str1)
    n = len(str2)

    # Fill positions of each character in vector
    # vector<int> position[M];
    position = [[] for i in range(M)]
    for i in range(1, n+1, 1):
        position[ord(str2[i-1])-97].append(i)

    # Initializing 2D array by 0 values
    lcsl = [[0 for i in range(n+2)] for j in range(m+2)]
    lcsr = [[0 for i in range(n+2)] for j in range(m+2)]

    # Filling LCS array for prefix substrings
    for i in range(1, m+1, 1):
        for j in range(1, n+1,1):
            if (str1[i-1] == str2[j-1]):
                lcsl[i][j] = 1 + lcsl[i-1][j-1]
            else:
                lcsl[i][j] = max(lcsl[i-1][j],
                                lcsl[i][j-1])

    # Filling LCS array for suffix substrings
    for i in range(m, 0, -1):
        for j in range(n, 0, -1):
            if (str1[i-1] == str2[j-1]):
                lcsr[i][j] = 1 + lcsr[i+1][j+1]
            else:
                lcsr[i][j] = max(lcsr[i+1][j],
                                lcsr[i][j+1])

        # Looping for all possible insertion positions
        # in first string
    ways = 0
    for i in range(0, m+1,1):
        # Trying all possible lower case characters
        for C in range(0, 26,1):
            # Now for each character, loop over same
            # character positions in second string
            for j in range(0, len(position[C]),1):
                p = position[C][j]

                # If both, left and right substrings make
                # total LCS then increase result by 1
                if (lcsl[i][p-1] + lcsr[i+1][p+1] == lcsl[m][n]):
                    ways += 1
    return ways

# Driver code to test above methods
str1 = "abcabc"
str2 = "abcd"
print(waysToIncreaseLCSBy1(str1, str2))

# This code is contributed by ankush_953
```

## C#

```
// C# program to get number of ways
// to increase LCS by 1
using System;
using System.Collections.Generic;

class GFG{

static int M = 26;

// Method returns total ways to increase
// LCS length by 1
static int waysToIncreaseLCSBy1(String str1,
                                String str2)
{
    int m = str1.Length, n = str2.Length;

    // Fill positions of each character in vector
    List<int>[] position = new List<int>[M];
    for(int i = 0; i < M; i++)
        position[i] = new List<int>();

    for(int i = 1; i <= n; i++)
        position[str2[i - 1] - 'a'].Add(i);

    int[,] lcsl = new int[m + 2, n + 2];
    int[,] lcsr = new int[m + 2, n + 2];

    // Initializing 2D array by 0 values
    for(int i = 0; i <= m + 1; i++)
        for(int j = 0; j <= n + 1; j++)
            lcsl[i, j] = lcsr[i, j] = 0;

    // Filling LCS array for prefix substrings
    for(int i = 1; i <= m; i++)
    {
        for(int j = 1; j <= n; j++)
        {
            if (str1[i - 1] == str2[j - 1])
                lcsl[i, j] = 1 + lcsl[i - 1, j - 1];
            else
                lcsl[i, j] = Math.Max(lcsl[i - 1, j],
                                      lcsl[i, j - 1]);
        }
    }

    // Filling LCS array for suffix substrings
    for(int i = m; i >= 1; i--)
    {
        for(int j = n; j >= 1; j--)
        {
            if (str1[i - 1] == str2[j - 1])
                lcsr[i, j] = 1 + lcsr[i + 1, j + 1];
            else
                lcsr[i, j] = Math.Max(lcsr[i + 1, j],
                                      lcsr[i, j + 1]);
        }
    }

    // Looping for all possible insertion
    // positions in first string
    int ways = 0;
    for(int i = 0; i <= m; i++)
    {

        // Trying all possible lower
        // case characters
        for(int d = 0; d < 26; d++)
        {

            // Now for each character, loop over same
            // character positions in second string
            for(int j = 0; j < position[d].Count; j++)
            {
                int p = position[d][j];

                // If both, left and right substrings make
                // total LCS then increase result by 1
                if (lcsl[i, p - 1] +
                    lcsr[i + 1, p + 1] == lcsl[m, n])
                    ways++;
            }
        }
    }
    return ways;
}

// Driver Code
public static void Main(String[] args)
{
    String str1 = "abcabc";
    String str2 = "abcd";

    Console.WriteLine(waysToIncreaseLCSBy1(str1, str2));
}
}

// This code is contributed by Princi Singh
```

**输出:**

```
4

```

**时间复杂度:**O(Mn)
T3】辅助空间: O(mn)

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。