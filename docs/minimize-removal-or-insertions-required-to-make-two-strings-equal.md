# 尽量减少移除或插入，以使两个字符串相等

> 原文:[https://www . geesforgeks . org/minimum-remove-or-insertions-required-make-two-string-equal/](https://www.geeksforgeeks.org/minimize-removal-or-insertions-required-to-make-two-strings-equal/)

给定两个[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** 和 **T** ，长度 **N** 和 [**S** 都是字符串**T**T13】的字谜，任务是通过执行以下操作最少次数将字符串 **S** 转换为 **T** :](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)

*   从两端删除一个字符。
*   在任何位置插入一个字符。

打印所需最小操作数的计数。

**示例:**

> **输入:** S = "qpmon "，T = "mnopq"
> **输出:** 3
> **说明:**
> 操作 1:去掉末尾的‘n’，插在倒数第二个位置。字符串 S 修改为“qpmno”。
> 操作二:从开头去掉‘q’，插在最后一个位置。字符串 S 修改为“pmnoq”。
> 操作 3:从开头去掉‘p’，插在倒数第二个位置。字符串 S 修改为“mnopq”，与所需的字符串 t 相同。
> 
> **输入:** S = "abab "，T = " Baba "
> T3】输出: 1

**方法:**给定的问题可以通过以下观察来解决:

*   需要找到 **A** 的最长子串的长度，这是 **B** 中的一个子串。让子弦的长度为 **L** 。
*   然后，可以在不干扰现有顺序的情况下插入剩余的字符。
*   综上所述，最优答案将等于**N–L**。

因此，从以上观察，所需的最小操作数是字符串 **N** 和[之间的差，即字符串 **A** 的最长子串的长度，该子串是字符串 **B**](https://www.geeksforgeeks.org/find-length-longest-subsequence-one-string-substring-another-string/) 中的子串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the longest substring
// in string A which is a subsequence in B
int findLongestSubstring(
    int posA, int posB, string& A,
    string& B, bool canSkip, int n,
    vector<vector<vector<int> > >& dp)
{

    // If the indices are out of bounds
    if (posA >= n || posB >= n) {
        return 0;
    }

    // If an already computed subproblem occurred
    if (dp[posA][posB][canSkip] != -1) {
        return dp[posA][posB][canSkip];
    }

    // Required answer if the all the
    // characters of A and B are the same
    int op1 = 0;

    // Required answer if there is no
    // substring A which is a
    //  subsequence in B
    int op2 = 0;

    // Required answer if the current
    // character in B is skipped
    int op3 = 0;

    if (A[posA] == B[posB]) {
        op1 = 1 + findLongestSubstring(
                      posA + 1, posB + 1, A,
                      B, 0, n, dp);
    }
    if (canSkip) {
        op2 = findLongestSubstring(
            posA + 1, posB, A, B,
            canSkip, n, dp);
    }
    op3 = findLongestSubstring(
        posA, posB + 1, A, B,
        canSkip, n, dp);

    // The answer for the subproblem is
    // the maximum among the three
    return dp[posA][posB][canSkip]
           = max(op1, max(op2, op3));
}

// Function to return the minimum strings
// operations required to make two strings equal
void minOperations(string A, string B, int N)
{
    // Initialize the dp vector
    vector<vector<vector<int> > > dp(
        N, vector<vector<int> >(
               N, vector<int>(2, -1)));

    cout << N - findLongestSubstring(
                    0, 0, A, B, 1, N, dp);
}

// Driver Code
int main()
{
    string A = "abab";
    string B = "baba";

    int N = A.size();

    minOperations(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG {

  // Function to find the longest substring
  // in string A which is a subsequence in B
  static int
    findLongestSubstring(int posA, int posB, String A,
                         String B, int canSkip, int n,
                         int dp[][][])
  {

    // If the indices are out of bounds
    if (posA >= n || posB >= n)
    {
      return 0;
    }

    // If an already computed subproblem occurred
    if (dp[posA][posB][canSkip] != -1)
    {
      return dp[posA][posB][canSkip];
    }

    // Required answer if the all the
    // characters of A and B are the same
    int op1 = 0;

    // Required answer if there is no
    // substring A which is a
    //  subsequence in B
    int op2 = 0;

    // Required answer if the current
    // character in B is skipped
    int op3 = 0;
    if (A.charAt(posA) == B.charAt(posB))
    {
      op1 = 1
        + findLongestSubstring(posA + 1, posB + 1,
                               A, B, 0, n, dp);
    }
    if (canSkip == 1) {
      op2 = findLongestSubstring(posA + 1, posB, A, B,
                                 canSkip, n, dp);
    }
    op3 = findLongestSubstring(posA, posB + 1, A, B,
                               canSkip, n, dp);

    // The answer for the subproblem is
    // the maximum among the three
    return dp[posA][posB][canSkip]
      = Math.max(op1, Math.max(op2, op3));
  }

  // Function to return the minimum strings
  // operations required to make two strings equal
  static void minOperations(String A, String B, int N)
  {
    // Initialize the dp vector
    int[][][] dp = new int[N][N][2];

    for(int i = 0; i < N; i++)
    {
      for(int j = 0; j < N; j++)
      {        
        for(int k = 0; k < 2; k++)
        {    
          dp[i][j][k] = -1;
        }
      }
    }

    System.out.println(
      N - findLongestSubstring(0, 0, A, B, 1, N, dp));
  }

  // Driver Code
  public static void main(String[] args)
  {
    String A = "abab";
    String B = "baba";
    int N = A.length();
    minOperations(A, B, N);
  }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the longest substring
# in A which is a subsequence in B
def findLongestSubstring(posA, posB, A, B, canSkip, n):
    global dp
    if (posA >= n or posB >= n):
        return 0

    # If an already computed subproblem occurred
    if (dp[posA][posB][canSkip] != -1):
        return dp[posA][posB][canSkip]

    # Required answer if the all the
    # characters of A and B are the same
    op1 = 0

    # Required answer if there is no
    # subA which is a
    # subsequence in B
    op2 = 0

    # Required answer if the current
    # character in B is skipped
    op3 = 0

    if (A[posA] == B[posB]):
        op1 = 1 + findLongestSubstring(posA + 1, posB + 1, A, B, 0, n)
    if (canSkip):
        op2 = findLongestSubstring(posA + 1, posB, A, B, canSkip, n)

    op3 = findLongestSubstring(posA, posB + 1, A, B, canSkip, n)

    # The answer for the subproblem is
    # the maximum among the three
    dp[posA][posB][canSkip] = max(op1, max(op2, op3))
    return dp[posA][posB][canSkip]

# Function to return the minimum strings
# operations required to make two strings equal
def minOperations(A, B, N):
    print(N - findLongestSubstring(0, 0, A, B, 1, N))

# Driver Code
if __name__ == '__main__':
    A = "abab"
    B = "baba"
    dp = [[[-1, -1] for i in range(len(A))] for i in range(len(A))]
    N = len(A)
    minOperations(A, B, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

      // Function to find the longest substring
    // in string A which is a subsequence in B
    static int
    findLongestSubstring(int posA, int posB, String A,
                         String B, int canSkip, int n,
                         int[, , ] dp)
    {

        // If the indices are out of bounds
        if (posA >= n || posB >= n) {
            return 0;
        }

        // If an already computed subproblem occurred
        if (dp[posA, posB, canSkip] != -1) {
            return dp[posA, posB, canSkip];
        }

        // Required answer if the all the
        // characters of A and B are the same
        int op1 = 0;

        // Required answer if there is no
        // substring A which is a
        //  subsequence in B
        int op2 = 0;

        // Required answer if the current
        // character in B is skipped
        int op3 = 0;

        if (A[posA] == B[posB]) {
            op1 = 1
                  + findLongestSubstring(posA + 1, posB + 1,
                                         A, B, 0, n, dp);
        }
        if (canSkip == 1) {
            op2 = findLongestSubstring(posA + 1, posB, A, B,
                                       canSkip, n, dp);
        }
        op3 = findLongestSubstring(posA, posB + 1, A, B,
                                   canSkip, n, dp);

        // The answer for the subproblem is
        // the maximum among the three
        return dp[posA, posB, canSkip]
            = Math.Max(op1, Math.Max(op2, op3));
    }

    // Function to return the minimum strings
    // operations required to make two strings equal
    static void minOperations(String A, String B, int N)
    {
        // Initialize the dp vector
        int[, , ] dp = new int[N, N, 2];

          for(int i = 0; i < N; i++)
        {      
              for(int j = 0; j < N; j++)
            {               
                  for(int k = 0; k < 2; k++)
                {    
                      dp[i, j, k] = -1;
                }
            }
        }
        Console.WriteLine(
            N - findLongestSubstring(0, 0, A, B, 1, N, dp));
    }

    // Driver Code
    static public void Main ()
    {
        String A = "abab";
        String B = "baba";
        int N = A.Length;
        minOperations(A, B, N);
    }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the longest substring
// in string A which is a subsequence in B
function findLongestSubstring( posA, posB, A, B, canSkip, n, dp)
{

    // If the indices are out of bounds
    if (posA >= n || posB >= n) {
        return 0;
    }

    // If an already computed subproblem occurred
    if (dp[posA][posB][canSkip] != -1) {
        return dp[posA][posB][canSkip];
    }

    // Required answer if the all the
    // characters of A and B are the same
    var op1 = 0;

    // Required answer if there is no
    // substring A which is a
    //  subsequence in B
    var op2 = 0;

    // Required answer if the current
    // character in B is skipped
    var op3 = 0;

    if (A[posA] == B[posB]) {
        op1 = 1 + findLongestSubstring(
                      posA + 1, posB + 1, A,
                      B, 0, n, dp);
    }
    if (canSkip) {
        op2 = findLongestSubstring(
            posA + 1, posB, A, B,
            canSkip, n, dp);
    }
    op3 = findLongestSubstring(
        posA, posB + 1, A, B,
        canSkip, n, dp);

    // The answer for the subproblem is
    // the maximum among the three
    return dp[posA][posB][canSkip]
           = Math.max(op1, Math.max(op2, op3));
}

// Function to return the minimum strings
// operations required to make two strings equal
function minOperations(A, B, N)
{
    // Initialize the dp vector
    var dp = Array.from(Array(N), ()=> Array(N));

    for(var i =0; i<N; i++)
        for(var j =0; j<N; j++)
            dp[i][j] = new Array(2).fill(-1);

    document.write( N - findLongestSubstring(
                    0, 0, A, B, 1, N, dp));
}

// Driver Code
var A = "abab";
var B = "baba";
var N = A.length;
minOperations(A, B, N);

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>2</sup>)*
***空间复杂度:** O(N <sup>2</sup> )*