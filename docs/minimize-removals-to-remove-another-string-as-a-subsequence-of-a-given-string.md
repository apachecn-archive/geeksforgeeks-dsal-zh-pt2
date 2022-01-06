# 最小化移除以移除另一个字符串作为给定字符串的子序列

> 原文:[https://www . geesforgeks . org/minimum-removes-to-remove-另一个字符串作为给定字符串的子序列/](https://www.geeksforgeeks.org/minimize-removals-to-remove-another-string-as-a-subsequence-of-a-given-string/)

给定两个长度分别为 **N** 和 **M** 的**字符串**和 **X** ，任务是找到需要从字符串**字符串**中删除的最少字符，使得字符串**字符串**不包含字符串 **X** 作为[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。

**示例:**

> ***输入:*** str = "btagd "，X = "bad"
> ***输出:*** 1
> **说明:**
> 字符串“btag”已经不包含“bad”作为子序列。因此，只需要移除一次。
> 
> ***输入:*** str = "bbaaddd "，X = "bad"
> ***输出:** 2*

**方式:**这个问题可以通过[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。按照以下步骤解决问题:

*   [穿越弦](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。
*   初始化一个 [2D 阵](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)**DP【N】【M】**，其中 **N** 为弦的[长度**弦****M**为弦 **X** 的长度。](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)
*   **dp[i][j]** 表示在 [**子串**](https://www.geeksforgeeks.org/substring-in-java/) **串【0，I】**中要求的最小字符删除次数，使得不出现[子串](https://www.geeksforgeeks.org/substring-in-java/)**X【0，j】**作为[子序列。](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)
*   两种过渡状态是:
    *   如果 **str[i]等于 X[j]** ，
        *   情况 1:删除字符**字符串【I】**
        *   情况 2:通过确保在**字符串【0，I】**中不出现**X【0，j-1】**作为**子序列**，来维护字符**字符串【I】，**
        *   更新**DP[I][j]= min(DP[I 1][j 1]，DP[I 1][j]+1)**
    *   如果 **str[i]不等于 X[j]，** str[i]可以保持原样。
        *   更新**DP[I][j]= DP[I–1][j]【T3]**
*   打印最小清除量，即**DP[N–1][M–1]**

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to print the minimum number of
// character removals required to remove X
// as a subsequence from the string str
void printMinimumRemovals(string str, string X)
{

    // Length of the string str
    int N = str.size();

    // Length of the string X
    int M = X.size();

    // Stores the dp states
    int dp[N][M] = {};

    // Fill first row of dp[][]
    for (int j = 0; j < M; j++) {

        // If X[j] matches with str[0]
        if (str[0] == X[j]) {

            dp[0][j] = 1;
        }
    }

    for (int i = 1; i < N; i++) {

        for (int j = 0; j < M; j++) {

            // If str[i] is equal to X[j]
            if (str[i] == X[j]) {

                // Update state after removing str[i[
                dp[i][j] = dp[i - 1][j] + 1;

                // Update state after keeping str[i]
                if (j != 0)
                    dp[i][j]
                        = min(dp[i][j], dp[i - 1][j - 1]);
            }

            // If str[i] is not equal to X[j]
            else {

                dp[i][j] = dp[i - 1][j];
            }
        }
    }

    // Print the minimum number
    // of characters removals
    cout << dp[N - 1][M - 1];
}

// Driver Code
int main()
{
    // Input
    string str = "btagd";
    string X = "bad";

    // Function call to get minimum
    // number of character removals
    printMinimumRemovals(str, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;
class GFG {

  // Function to print the minimum number of
  // character removals required to remove X
  // as a subsequence from the string str
  static void printMinimumRemovals(String str, String X)
  {

    // Length of the string str
    int N = str.length();

    // Length of the string X
    int M = X.length();

    // Stores the dp states
    int dp[][] = new int[N][M];

    // Fill first row of dp[][]
    for (int j = 0; j < M; j++) {

      // If X[j] matches with str[0]
      if (str.charAt(0) == X.charAt(j)) {

        dp[0][j] = 1;
      }
    }

    for (int i = 1; i < N; i++) {

      for (int j = 0; j < M; j++) {

        // If str[i] is equal to X[j]
        if (str.charAt(i) == X.charAt(j)) {

          // Update state after removing str[i[
          dp[i][j] = dp[i - 1][j] + 1;

          // Update state after keeping str[i]
          if (j != 0)
            dp[i][j] = Math.min(
            dp[i][j], dp[i - 1][j - 1]);
        }

        // If str[i] is not equal to X[j]
        else {

          dp[i][j] = dp[i - 1][j];
        }
      }
    }

    // Print the minimum number
    // of characters removals
    System.out.println(dp[N - 1][M - 1]);
  }

  // Driver code
  public static void main(String[] args)
  {
    // Input
    String str = "btagd";
    String X = "bad";

    // Function call to get minimum
    // number of character removals
    printMinimumRemovals(str, X);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python 3 implementation of
# the above approach

# Function to print the minimum number of
# character removals required to remove X
# as a subsequence from the string str
def printMinimumRemovals(s, X):

    # Length of the string str
    N = len(s)

    # Length of the string X
    M = len(X)

    # Stores the dp states
    dp = [[0 for x in range(M)] for y in range(N)]

    # Fill first row of dp[][]
    for j in range(M):

        # If X[j] matches with str[0]
        if (s[0] == X[j]):
            dp[0][j] = 1

    for i in range(1, N):
        for j in range(M):

            # If s[i] is equal to X[j]
            if (s[i] == X[j]):

                # Update state after removing str[i[
                dp[i][j] = dp[i - 1][j] + 1

                # Update state after keeping str[i]
                if (j != 0):
                    dp[i][j] = min(dp[i][j], dp[i - 1][j - 1])

            # If str[i] is not equal to X[j]
            else:
                dp[i][j] = dp[i - 1][j]

    # Print the minimum number
    # of characters removals
    print(dp[N - 1][M - 1])

# Driver Code
if __name__ == "__main__":

    # Input
    s = "btagd"
    X = "bad"

    # Function call to get minimum
    # number of character removals
    printMinimumRemovals(s, X)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for above approach
using System;
public class GFG
{

  // Function to print the minimum number of
  // character removals required to remove X
  // as a subsequence from the string str
  static void printMinimumRemovals(string str, string X)
  {

    // Length of the string str
    int N = str.Length;

    // Length of the string X
    int M = X.Length;

    // Stores the dp states
    int[,] dp = new int[N, M];

    // Fill first row of dp[][]
    for (int j = 0; j < M; j++) {

      // If X[j] matches with str[0]
      if (str[0] == X[j]) {

        dp[0, j] = 1;
      }
    }

    for (int i = 1; i < N; i++) {

      for (int j = 0; j < M; j++) {

        // If str[i] is equal to X[j]
        if (str[i] == X[j]) {

          // Update state after removing str[i[
          dp[i, j] = dp[i - 1, j] + 1;

          // Update state after keeping str[i]
          if (j != 0)
            dp[i, j] = Math.Min(
            dp[i, j], dp[i - 1, j - 1]);
        }

        // If str[i] is not equal to X[j]
        else {

          dp[i, j] = dp[i - 1, j];
        }
      }
    }

    // Print the minimum number
    // of characters removals
    Console.WriteLine(dp[N - 1, M - 1]);
  }

// Driver code
public static void Main(String[] args)
{

    // Input
    string str = "btagd";
    string X = "bad";

    // Function call to get minimum
    // number of character removals
    printMinimumRemovals(str, X);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print the minimum number of
// character removals required to remove X
// as a subsequence from the string str
function printMinimumRemovals(str,X)
{
    // Length of the string str
    let N = str.length;

    // Length of the string X
    let M = X.length;

    // Stores the dp states
    let dp = new Array(N);
    for(let i=0;i<N;i++)
    {
        dp[i]=new Array(M);
        for(let j=0;j<M;j++)
        {
            dp[i][j]=0;
        }

    }

    // Fill first row of dp[][]
    for (let j = 0; j < M; j++) {

      // If X[j] matches with str[0]
      if (str[0] == X[j]) {

        dp[0][j] = 1;
      }
    }

    for (let i = 1; i < N; i++) {

      for (let j = 0; j < M; j++) {

        // If str[i] is equal to X[j]
        if (str[i] == X[j]) {

          // Update state after removing str[i[
          dp[i][j] = dp[i - 1][j] + 1;

          // Update state after keeping str[i]
          if (j != 0)
            dp[i][j] = Math.min(
            dp[i][j], dp[i - 1][j - 1]);
        }

        // If str[i] is not equal to X[j]
        else {

          dp[i][j] = dp[i - 1][j];
        }
      }
    }

    // Print the minimum number
    // of characters removals
    document.write(dp[N - 1][M - 1]);
}

 // Driver code
let str = "btagd";
let X = "bad";
// Function call to get minimum
// number of character removals
printMinimumRemovals(str, X);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*