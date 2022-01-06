# 需要添加到字符串中的最小字符数，以便所有小写字母以递增顺序作为子序列出现

> 原文:[https://www . geeksforgeeks . org/最小字符数-需要添加到字符串中，以便所有小写字母都以递增顺序出现/](https://www.geeksforgeeks.org/minimum-number-of-characters-required-to-be-added-to-a-string-such-that-all-lowercase-alphabets-occurs-as-a-subsequence-in-increasing-order/)

给定一个由 **N** 个字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到必须添加到 **S** 中的最小字符数，以便所有小写字母在 **S** 中以递增顺序作为[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)出现。

**示例:**

> **输入:** S = "axyabzaxd"
> **输出:** 22
> **解释:**
> 从 b 到 w (bcdefghijklmnopqrstuvw)的计数为 22 的字符在给定的字符串 S 中丢失了。
> 因此，为了使所有的小写英文字符成为其中的子序列，我们必须添加所有这 22 个字符。
> 因此，最少要添加 22 个字符。
> 
> **输入:**S = " abcdefghxyabzjklmnoappqrtd "
> T3】输出: 6

**天真方法:**解决给定问题的最简单方法是[生成给定字符串的所有可能的子序列 **S**](https://www.geeksforgeeks.org/print-subsequences-string/) 并检查在哪个子序列中追加字符串中最少数量的字符会以递增的顺序给出所有小写字母的子序列。检查所有子序列后，打印附加的最小字符数。
***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过以下观察进行优化:

*   因为附加字符后必须出现所有小写字符，即字符串 **S** 必须包含字符串 **T** 作为子序列**“abcdefghijklmnopqrstuvwxyz”**。
*   必须以任何顺序追加的最小字符数是首先找到字符串 **S** 和字符串 **T** 的[最长公共子序列](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)(比如说 **L** ，因为这给出了我们不需要添加的最大字符数
*   然后打印**(26–L)**的值作为所需的最小字符数。

从上面的观察中，找到字符串 S 和 T 的 [LCS 的值](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)，并打印**(26–LCS)**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to find the LCS
// of strings S and string T
int LCS(string& S, int N, string& T, int M,
        vector<vector<int> >& dp)
{

    // Base Case
    if (N == 0 or M == 0)
        return 0;

    // Already Calculated State
    if (dp[N][M] != -1)
        return dp[N][M];

    // If the characters are the same
    if (S[N - 1] == T[M - 1]) {
        return dp[N][M] = 1 + LCS(S, N - 1, T, M - 1, dp);
    }

    // Otherwise
    return dp[N][M] = max(LCS(S, N - 1, T, M, dp),
                          LCS(S, N, T, M - 1, dp));
}

// Function to find the minimum number of
// characters that needs to be appended
// in the string to get all lowercase
// alphabets as a subsequences
int minimumCharacter(string& S)
{

    // String containing all the characters
    string T = "abcdefghijklmnopqrstuvwxyz";

    int N = S.length(), M = T.length();

    // Stores the result of overlapping
    // subproblems
    vector<vector<int> > dp(N + 1, vector<int>(M + 1, -1));

    // Return the minimum characters
    // required
    return (26 - LCS(S, N, T, M, dp));
}

// Driver Code
int main()
{

    string S = "abcdadc";
    cout << minimumCharacter(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to find the LCS
  // of strings S and string T
  static int LCS(String S, int N, String T,
                 int M, int dp[][])
  {

    // Base Case
    if (N == 0 || M == 0)
      return 0;

    // Already Calculated State
    if (dp[N][M] != 0)
      return dp[N][M];

    // If the characters are the same
    if (S.charAt(N - 1)== T.charAt(M - 1)) {
      return dp[N][M] = 1 + LCS(S, N - 1,
                                T, M - 1, dp);
    }

    // Otherwise
    return dp[N][M] = Math.max(
      LCS(S, N - 1, T, M, dp),
      LCS(S, N, T, M - 1, dp));
  }

  // Function to find the minimum number of
  // characters that needs to be appended
  // in the string to get all lowercase
  // alphabets as a subsequences
  static int minimumCharacter(String S)
  {

    // String containing all the characters
    String T = "abcdefghijklmnopqrstuvwxyz";

    int N = S.length(), M = T.length();

    // Stores the result of overlapping
    // subproblems
    int dp[][]= new int[N+1][M+1];
    // Return the minimum characters
    // required
    return (26 - LCS(S, N, T, M, dp));
  }

  // Driver Code
  public static void main (String[] args) {
    String S = "abcdadc";

    System.out.println(minimumCharacter(S));
  }
}

// This code is contributed by Potta Lokesh
```

## 计算机编程语言

```
# Python3 program for the above approach
import numpy as np

# Function to find the LCS
# of strings S and string T
def LCS(S, N, T, M, dp) :

    # Base Case
    if (N == 0 or M == 0) :
        return 0;

    # Already Calculated State
    if (dp[N][M] != 0) :
        return dp[N][M];

    # If the characters are the same
    if (S[N - 1] == T[M - 1]) :
        dp[N][M] = 1 + LCS(S, N - 1, T, M - 1, dp);
        return dp[N][M]

    # Otherwise
    dp[N][M] = max( LCS(S, N - 1, T, M, dp), LCS(S, N, T, M - 1, dp));

    return dp[N][M]

# Function to find the minimum number of
# characters that needs to be appended
# in the string to get all lowercase
# alphabets as a subsequences
def minimumCharacter(S) :

    # String containing all the characters
    T = "abcdefghijklmnopqrstuvwxyz";

    N = len(S); M = len(T);

    # Stores the result of overlapping
    # subproblems
    dp = np.zeros((N + 1, M + 1));

    # Return the minimum characters
    # required
    return (26 - LCS(S, N, T, M, dp));

# Driver Code
if __name__ == "__main__" :

    S = "abcdadc";
    print(minimumCharacter(S));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach

using System;

public class GFG
{

  // Function to find the LCS
  // of strings S and string T
  static int LCS(String S, int N, String T,
                 int M, int [,]dp)
  {

    // Base Case
    if (N == 0 || M == 0)
      return 0;

    // Already Calculated State
    if (dp[N,M] != 0)
      return dp[N,M];

    // If the characters are the same
    if (S[N - 1]== T[M - 1]) {
      return dp[N,M] = 1 + LCS(S, N - 1,
                                T, M - 1, dp);
    }

    // Otherwise
    return dp[N,M] = Math.Max(
      LCS(S, N - 1, T, M, dp),
      LCS(S, N, T, M - 1, dp));
  }

  // Function to find the minimum number of
  // characters that needs to be appended
  // in the string to get all lowercase
  // alphabets as a subsequences
  static int minimumchar(String S)
  {

    // String containing all the characters
    String T = "abcdefghijklmnopqrstuvwxyz";

    int N = S.Length, M = T.Length;

    // Stores the result of overlapping
    // subproblems
    int [,]dp= new int[N+1,M+1];
    // Return the minimum characters
    // required
    return (26 - LCS(S, N, T, M, dp));
  }

  // Driver Code
  public static void Main(String[] args) {
    String S = "abcdadc";

    Console.WriteLine(minimumchar(S));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program for the above approach

 // Function to find the LCS
  // of strings S and string T
  function LCS(S , N, T,
                 M , dp)
  {

    // Base Case
    if (N == 0 || M == 0)
      return 0;

    // Already Calculated State
    if (dp[N][M] != 0)
      return dp[N][M];

    // If the characters are the same
    if (S.charAt(N - 1)== T.charAt(M - 1)) {
      return dp[N][M] = 1 + LCS(S, N - 1,
                                T, M - 1, dp);
    }

    // Otherwise
    return dp[N][M] = Math.max(
      LCS(S, N - 1, T, M, dp),
      LCS(S, N, T, M - 1, dp));
  }

  // Function to find the minimum number of
  // characters that needs to be appended
  // in the string to get all lowercase
  // alphabets as a subsequences
  function minimumCharacter(S)
  {

    // String containing all the characters
    var T = "abcdefghijklmnopqrstuvwxyz";

    var N = S.length, M = T.length;

    // Stores the result of overlapping
    // subproblems
    var dp= Array(N+1).fill(0).map(x => Array(M+1).fill(0));
    // Return the minimum characters
    // required
    return (26 - LCS(S, N, T, M, dp));
  }

  // Driver Code
  var S = "abcdadc";

  document.write(minimumCharacter(S));

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
22
```

***时间复杂度:** O(26*N)*
***辅助空间:** O(1)*