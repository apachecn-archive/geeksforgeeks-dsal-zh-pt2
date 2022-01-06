# 从给定字符串中最多删除 K 个字符的最小游程编码长度

> 原文:[https://www . geesforgeks . org/最小游程长度编码-通过从给定字符串中最多删除 k 个字符来实现/](https://www.geeksforgeeks.org/minimum-length-of-run-length-encoding-possible-by-removing-at-most-k-characters-from-a-given-string/)

给定一个长度为 **N** 的字符串 **S** ，仅由小写英文字母组成，任务是通过从字符串 **S** 中最多移除 **K** 个字符来找到最小可能长度的 [**游程编码**](https://www.geeksforgeeks.org/run-length-encoding/) 。

**示例:**

> **输入:**S =“abbcdcdd”，N = 9，K = 2
> **输出:** 5
> **解释:**一种可能的方法是从 S 中删除两个出现的‘c’。
> 生成的新字符串是“abbbddd”，其游程编码为“ab3d3”。
> 因此，编码字符串的长度为 5。
> 
> **输入:**S =“aabbca”，N = 6，K = 3
> **输出:** 2
> **解释:**一种可能的方法是同时删除‘b’的出现和‘c’的一个出现。
> 生成的新字符串为“aaa”，其游程编码为“a3”。
> 因此，编码字符串的长度为 2

**天真方法:**解决问题最简单的方法是从字符串中移除 **K** 字符的每个组合，并计算它们各自的[游程编码](https://www.geeksforgeeks.org/run-length-encoding/)。最后，打印获得的最小游程编码的长度。

***时间复杂度:** O(K * N！(N–K)！* K！)*
***辅助空间:** O(K)*

**高效方法:**要优化上述方法，请按照以下步骤解决问题:

*   维护一个辅助数组 **dp[n][k][26][n]** ，其中 **dp[idx][K][last][count]** 表示从索引 **idx** 开始获得的最小游程编码，其中， **K** 表示剩余的删除数， **last** 表示到目前为止出现频率为**计数**的最后一个字符。
*   对于每个角色，都有两种可能，要么删除角色，要么保留角色。
*   考虑删除索引 **idx** 处的当前字符，并递归计算通过传递参数 **(idx + 1，K–1，最后，计数)**获得的最小游程编码
*   现在，考虑保留索引 **idx** 处的当前字符，并递归计算以下两种情况的最小游程编码:
*   **如果 S[idx] = last:** 通过传递参数 **(idx + 1，K，S[idx]，count + 1)** 计算最小游程编码。
*   否则，通过传递参数 **(idx + 1，K，S[idx]，1)** ，计算最小游程编码。
*   返回上述计算值的最小值，并对字符串的所有索引重复上述步骤。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

#define maxN 20

int dp[maxN][maxN][27][maxN];

// Function which solves the desired problem
int solve(string& s, int n, int idx,
          int k, char last = 123,
          int count = 0)
{
    // idx: current index in s
    // k: Remaining number of deletions
    // last: Previous character
    // count: Number of occurrences
    // of the previous character

    // Base Case
    if (k < 0)
        return n + 1;

    // If the entire string has
    // been traversed
    if (idx == n)
        return 0;

    int& ans = dp[idx][k][last - 'a'][count];

    // If precomputed subproblem
    // occurred
    if (ans != -1)
        return ans;

    ans = n + 1;

    // Minimum run length encoding by
    // removing the current character
    ans = min(ans,
              solve(s, n, idx + 1, k - 1, last, count));

    // Minimum run length encoding by
    // retaining the current character
    int inc = 0;

    if (count == 1 || count == 9
        || count == 99)
        inc = 1;

    // If the current and the
    // previous characters match
    if (last == s[idx]) {

        ans = min(ans,
                  inc + solve(s, n, idx + 1, k, s[idx],
                              count + 1));
    }

    // Otherwise
    else {

        ans = min(ans,
                  1 + solve(s, n, idx + 1, k, s[idx], 1));
    }

    return ans;
}

// Function to return minimum run-length encoding
// for string s by removing atmost k characters
int MinRunLengthEncoding(string& s, int n, int k)
{
    memset(dp, -1, sizeof(dp));
    return solve(s, n, 0, k);
}

// Driver Code
int main()
{
    string S = "abbbcdcdd";
    int N = 9, K = 2;
    cout << MinRunLengthEncoding(S, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static int maxN = 20;

static int dp[][][][] = new int[maxN][maxN][27][maxN];

// Function which solves the desired problem
public static int solve(String s, int n,
                         int idx, int k,
                       char last, int count)
{

    // idx: current index in s
    // k: Remaining number of deletions
    // last: Previous character
    // count: Number of occurrences
    // of the previous character

    // Base Case
    if (k < 0)
        return n + 1;

    // If the entire string has
    // been traversed
    if (idx == n)
        return 0;

    int ans = dp[idx][k][last - 'a'][count];

    // If precomputed subproblem
    // occurred
    if (ans != -1)
        return ans;

    ans = n + 1;

    // Minimum run length encoding by
    // removing the current character
    ans = Math.min(ans, solve(s, n, idx + 1,
                              k - 1, last,
                              count));

    // Minimum run length encoding by
    // retaining the current character
    int inc = 0;

    if (count == 1 || count == 9 || count == 99)
        inc = 1;

    // If the current and the
    // previous characters match
    if (last == s.charAt(idx))
    {
        ans = Math.min(ans, inc + solve(s, n, idx + 1,
                                        k, s.charAt(idx),
                                        count + 1));
    }

    // Otherwise
    else
    {
        ans = Math.min(ans, 1 + solve(s, n, idx + 1, k,
                                      s.charAt(idx), 1));
    }
    return dp[idx][k][last - 'a'][count] = ans;
}

// Function to return minimum run-length encoding
// for string s by removing atmost k characters
public static int MinRunLengthEncoding(String s, int n,
                                                 int k)
{
    for(int i[][][] : dp)
        for(int j[][] : i)
            for(int p[] : j)
                Arrays.fill(p, -1);

    return solve(s, n, 0, k, (char)123, 0);
}

// Driver Code
public static void main(String args[])
{
    String S = "abbbcdcdd";
    int N = 9, K = 2;

    System.out.println(MinRunLengthEncoding(S, N, K));
}
}

// This code is contributed by hemanth gadarla
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
maxN = 20

dp = [[[[0 for i in range(maxN)]
           for j in range(27)]
           for k in range(27)]
           for l in range(maxN)]

# Function which solves the desired problem
def solve(s, n, idx, k, last, count):

    # idx: current index in s
    # k: Remaining number of deletions
    # last: Previous character
    # count: Number of occurrences
    # of the previous character

    # Base Case
    if (k < 0):
        return n + 1

    # If the entire string has
    # been traversed
    if (idx == n):
        return 0

    ans = dp[idx][k][ord(last) - ord('a')][count]

    # If precomputed subproblem
    # occurred
    if (ans != -1):
        return ans

    ans = n + 1

    # Minimum run length encoding by
    # removing the current character
    ans = min(ans, solve(s, n, idx + 1,
                         k - 1, last, count))

    # Minimum run length encoding by
    # retaining the current character
    inc = 0

    if (count == 1 or count == 9 or
        count == 99):
        inc = 1

    # If the current and the
    # previous characters match
    if (last == s[idx]):
        ans = min(ans, inc + solve(s, n, idx + 1, k,
                                   s[idx], count + 1))

    # Otherwise
    else:
        ans = max(ans, 1 + solve(s, n, idx + 1,
                                 k, s[idx], 1))

    dp[idx][k][ord(last) - ord('a')][count] = ans
    #print(ans)

    return dp[idx][k][ord(last) - ord('a')][count]

# Function to return minimum run-length encoding
# for string s by removing atmost k characters
def MinRunLengthEncoding(s, n, k):

    for i in range(maxN):
        for j in range(27):
            for k in range(27):
                for l in range(maxN):
                    dp[i][j][k][l] = -1

    return solve(s, n, 0, k, chr(123), 0) - 1

# Driver Code
if __name__ == '__main__':

    S = "abbbcdcdd"
    N = 9
    K = 2

    print(MinRunLengthEncoding(S, N, K))

# This code is contributed by gauravrajput1
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

static int maxN = 20;

static int [,,,]dp =
       new int[maxN, maxN,
               27, maxN];

// Function which solves
// the desired problem
public static int solve(String s, int n,
                        int idx, int k,
                        char last, int count)
{   
  // idx: current index in s
  // k: Remaining number of deletions
  // last: Previous character
  // count: Number of occurrences
  // of the previous character

  // Base Case
  if (k < 0)
    return n + 1;

  // If the entire string
  // has been traversed
  if (idx == n)
    return 0;

  int ans = dp[idx, k, last -
               'a', count];

  // If precomputed subproblem
  // occurred
  if (ans != -1)
    return ans;

  ans = n + 1;

  // Minimum run length encoding by
  // removing the current character
  ans = Math.Min(ans,
                 solve(s, n, idx + 1,
                       k - 1, last,
                       count));

  // Minimum run length encoding by
  // retaining the current character
  int inc = 0;

  if (count == 1 || count == 9 ||
      count == 99)
    inc = 1;

  // If the current and the
  // previous characters match
  if (last == s[idx])
  {
    ans = Math.Min(ans, inc +
                   solve(s, n, idx + 1,
                         k, s[idx],
                         count + 1));
  }

  // Otherwise
  else
  {
    ans = Math.Min(ans, 1 +
                   solve(s, n, idx + 1,
                         k, s[idx], 1));
  }
  return dp[idx, k, last -
            'a', count] = ans;
}

// Function to return minimum
// run-length encoding for string
// s by removing atmost k characters
public static int MinRunLengthEncoding(String s,
                                       int n, int k)
{
  for (int i = 0; i < maxN; i++)
    for (int j = 0; j < maxN; j++)
      for (int p = 0; p < 27; p++)
        for (int l = 0; l < maxN; l++)
          dp[i, j, p, l] = -1;

  return solve(s, n, 0,
               k, (char)123, 0);
}

// Driver Code
public static void Main(String []args)
{
  String S = "abbbcdcdd";
  int N = 9, K = 2;
  Console.WriteLine(
          MinRunLengthEncoding(S,
                               N, K));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program to implement the above approach

    let maxN = 20;

    let dp = new Array(maxN);

    // Function which solves the desired problem
    function solve(s, n, idx, k, last, count)
    {

        // idx: current index in s
        // k: Remaining number of deletions
        // last: Previous character
        // count: Number of occurrences
        // of the previous character

        // Base Case
        if (k < 0)
            return n + 1;

        // If the entire string has
        // been traversed
        if (idx == n)
            return 0;

        let ans = dp[idx][k][last - 'a'.charCodeAt()][count];

        // If precomputed subproblem
        // occurred
        if (ans != -1)
            return ans;

        ans = n + 1;

        // Minimum run length encoding by
        // removing the current character
        ans = Math.min(ans, solve(s, n, idx + 1,
                                  k - 1, last,
                                  count));

        // Minimum run length encoding by
        // retaining the current character
        let inc = 0;

        if (count == 1 || count == 9 || count == 99)
            inc = 1;

        // If the current and the
        // previous characters match
        if (last == s[idx].charCodeAt())
        {
            ans = Math.min(ans, inc + solve(s, n, idx + 1,
                                            k, s[idx].charCodeAt(),
                                            count + 1));
        }

        // Otherwise
        else
        {
            ans = Math.min(ans, 1 + solve(s, n, idx + 1, k,
                                          s[idx].charCodeAt(), 1));
        }
        dp[idx][k][last - 'a'.charCodeAt()][count] = ans;
        return dp[idx][k][last - 'a'.charCodeAt()][count];
    }

    // Function to return minimum run-length encoding
    // for string s by removing atmost k characters
    function MinRunLengthEncoding(s, n, k)
    {
        for(let i = 0; i < maxN; i++)
        {
            dp[i] = new Array(maxN);
            for(let j = 0; j < maxN; j++)
            {
                dp[i][j] = new Array(27);
                for(let k = 0; k < 27; k++)
                {
                    dp[i][j][k] = new Array(maxN);
                    for(let l = 0; l < maxN; l++)
                    {
                        dp[i][j][k][l] = -1;
                    }
                }
            }
        }

        return solve(s, n, 0, k, 123, 0);
    }

    let S = "abbbcdcdd";
    let N = 9, K = 2;

    document.write(MinRunLengthEncoding(S, N, K));

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(26 * N<sup>2</sup>* K)*
***辅助空间:** O(26 * N <sup>2</sup> * K)*