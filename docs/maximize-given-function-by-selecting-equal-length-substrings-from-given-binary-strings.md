# 通过从给定的二进制字符串中选择相等长度的子字符串来最大化给定的函数

> 原文:[https://www . geesforgeks . org/通过从给定二进制字符串中选择等长子字符串来最大化给定函数/](https://www.geeksforgeeks.org/maximize-given-function-by-selecting-equal-length-substrings-from-given-binary-strings/)

给定两个[二进制字符串](https://www.geeksforgeeks.org/program-to-add-two-binary-strings/) **s1** 和 **s2** 。任务是从 **s1** 和 **s2** 中选择[子串](https://www.geeksforgeeks.org/substring-in-java/)表示 **sub1** 和 **sub2** 等长，使功能最大化:

> fun(s1，s2) = len(sub1) / (2 <sup>xor(sub1，sub2)</sup> )

**示例:**

> **输入:**s1 =“1101”，s2 =“1110”
> T3】输出: 3
> **说明:**下面是从 S1 和 S2 中选择的子串
> 子串从 S1->【110】
> 子串从 S2->【110】
> 子串因此，fun(s1，s2) = 3/ (2 <sup>xor(110，110)</sup> )
> 
> **输入:**S1 =“1111”，S2 =“1000”
> T3】输出: 1

**方法:**为了最大化给定的函数，需要用最小异或来选择大的[子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)。为了最小化分母，选择子字符串的方式应使 **sub1** 和 **sub2** 的[T5【异或】始终为 **0** ，这样分母项将始终为 **1** (2 <sup>0</sup> )。为此，从两个字符串 **s1** 和 **s2** 中找到](https://www.geeksforgeeks.org/find-the-maximum-subarray-xor-in-a-given-array/)[最长的公共子字符串](https://www.geeksforgeeks.org/longest-common-substring-dp-29/)，并打印其长度，这将是所需的答案。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

int dp[1000][1000];

// Function to find longest common substring.
int lcs(string s, string k, int n, int m)
{
    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= m; j++) {
            if (i == 0 or j == 0) {
                dp[i][j] = 0;
            }
            else if (s[i - 1] == k[j - 1]) {
                dp[i][j] = 1 + dp[i - 1][j - 1];
            }
            else {
                dp[i][j] = max(dp[i - 1][j],
                               dp[i][j - 1]);
            }
        }
    }

    // Return the result
    return dp[n][m];
}

// Driver Code
int main()
{
    string s1 = "1110";
    string s2 = "1101";

    cout << lcs(s1, s2,
                s1.size(), s2.size());

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

  static int dp[][] = new int[1000][1000];

  // Function to find longest common substring.
  static int lcs(String s, String k, int n, int m)
  {
      for (int i = 0; i <= n; i++) {
          for (int j = 0; j <= m; j++) {
              if (i == 0 || j == 0) {
                  dp[i][j] = 0;
              }
              else if (s.charAt(i - 1) == k.charAt(j - 1)) {
                  dp[i][j] = 1 + dp[i - 1][j - 1];
              }
              else {
                  dp[i][j] = Math.max(dp[i - 1][j],
                                 dp[i][j - 1]);
              }
          }
      }

      // Return the result
      return dp[n][m];
  }

  // Driver Code
  public static void main(String [] args)
  {
      String s1 = "1110";
      String s2 = "1101";

      System.out.print(lcs(s1, s2,
                  s1.length(), s2.length()));

  }
}

// This code is contributed by AR_Gaurav
```

## 蟒蛇 3

```
# Python3 program for above approach

import numpy as np;

dp = np.zeros((1000,1000));

# Function to find longest common substring.
def lcs( s,  k,  n,  m) :

    for i in range(n + 1) :
        for j in range(m + 1) :
            if (i == 0 or j == 0) :
                dp[i][j] = 0;

            elif (s[i - 1] == k[j - 1]) :
                dp[i][j] = 1 + dp[i - 1][j - 1];

            else :
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);

    # Return the result
    return dp[n][m];

# Driver Code
if __name__ == "__main__" :

    s1 = "1110";
    s2 = "1101";

    print(lcs(s1, s2,len(s1), len(s2)));

   # This code is contributed by AnkThon
```

## C#

```
// C# program for above approach
using System;
public class GFG{

  static int [,]dp = new int[1000,1000];

  // Function to find longest common substring.
  static int lcs(string s, string k, int n, int m)
  {
      for (int i = 0; i <= n; i++) {
          for (int j = 0; j <= m; j++) {
              if (i == 0 || j == 0) {
                  dp[i, j] = 0;
              }
              else if (s[i - 1] == k[j - 1]) {
                  dp[i, j] = 1 + dp[i - 1, j - 1];
              }
              else {
                  dp[i, j] = Math.Max(dp[i - 1, j],
                                 dp[i, j - 1]);
              }
          }
      }

      // Return the result
      return dp[n, m];
  }

  // Driver Code
  public static void Main(string [] args)
  {
      string s1 = "1110";
      string s2 = "1101";

      Console.Write(lcs(s1, s2, s1.Length, s2.Length));
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// JavaScript program for above approach
var dp = new Array(1000);
for (var i = 0; i < 1000; i++) {
  dp[i] = new Array(1000);
}

// Function to find longest common substring.
function lcs( s,  k,  n,  m)
{
    for (var i = 0; i <= n; i++) {
        for (var j = 0; j <= m; j++) {
            if (i == 0 || j == 0) {
                dp[i][j] = 0;
            }
            else if (s[i - 1] == k[j - 1]) {
                dp[i][j] = 1 + dp[i - 1][j - 1];
            }
            else {
                dp[i][j] = Math.max(dp[i - 1][j],
                               dp[i][j - 1]);
            }
        }
    }

    // Return the result
    return dp[n][m];
}

// Driver Code
var s1 = "1110";
var s2 = "1101";

document.write(lcs(s1, s2, s1.length, s2.length))

// This code is contributed by AnkThon
</script>
```

**Output**

```
3
```

**时间复杂度:** O(N*M)，其中 N 是 s1 的大小，M 是 s2 的大小。

**辅助空间:** O(N*M)，其中 N 为 s1 的大小，M 为 s2 的大小。