# 通过递归移除所有相邻重复项清空给定字符串的方式计数

> 原文:[https://www . geeksforgeeks . org/递归删除所有相邻重复项清空给定字符串的次数/](https://www.geeksforgeeks.org/count-of-ways-to-empty-given-string-by-recursively-removing-all-adjacent-duplicates/)

给定一个字符串 **S** ，在一次移动中允许**移除两个相邻的相等字符**。删除后，被删除字符的两个端点将连接在一起。计算**清空字符串的方法总数。**

**示例:**

> **输入:**S = aabccb
> T3】输出:3
> T6】说明:T8】1。aab**<u>cc</u>**B->aa**<u>bb</u>**->**<u>aa</u>**T21】2。aab**<u>cc</u>**B->**<u>aa</u>**bb->**T31】bb**
> 3。**<u>aa</u>**bccb->b**<u>cc</u>**B->**T44】bb**
> 因此，在一组有效的招式之后，总共有 3 种清空琴弦的方法。
> 
> **输入:** S = aabbc
> **输出:** 0
> **说明:**字符串长度为奇数，不可能清空整个字符串。

**途径:**以上问题可以借助[动态规划解决。](https://www.geeksforgeeks.org/dynamic-programming/)按照以下步骤解决问题:

*   让我们定义一个**二维 dp 表** **dp[i][j]，它将存储范围[i，j]的答案。**
*   定义一个[递归方法](https://www.geeksforgeeks.org/recursion/)来解决问题。
*   要计算 **dp[i][j]** ，循环查看 **i** 和 **j** 之间的所有指数 **k** ，其中 **S[i] = S[k]** 。
*   现在对于一个个体 **k** ，答案将是 **dp[i+1][k-1]*dp[k+1][j]*(安排范围移除的方式总数)。**
*   要计算等式的最后一项，请注意整个范围**【I+1，k-1】**的移除将在**S【I】和 S【k】的移除之前进行。**
*   因此该范围内的总移除量将为**(j–I+1)/2**(因为两个元素同时被移除)。从这些清除中必须选择**(j–k)/2 清除。**
*   所以最终的公式将是

> ![dp[i+1][k-1]*dp[k+1][j]*{}^{(j-i + 1)/2}C_{(j - k)/2} ](img/eccb3c2987c483dbfc5d4bb96454dc04.png "Rendered by QuickLaTeX.com")

*   使用 [<u>记忆</u>](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/) 不再重新计算状态。
*   检查**递归函数中的基本情况。**
*   最终答案将是 **dp[0][N-1]**

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Define the dp table globally
int dp[505][505], choose[502][502];

// Recursive function to calculate the dp
// values for range [L, R]
int calc(int l, int r, string& s)
{

    // The range is odd length
    if (abs(r - l) % 2 == 0) {
        return 0;
    }

    if (l > r) {
        return dp[l][r] = 1;
    }

    // The state is already calculated
    if (dp[l][r] != -1) {
        return dp[l][r];
    }

    // If the length is 2
    if ((r - l) == 1) {
        if (s[l] == s[r]) {
            dp[l][r] = 1;
        }
        else {
            dp[l][r] = 0;
        }
        return dp[l][r];
    }

    // Total answer for this state
    int ans = 0;
    for (int k = l + 1; k <= r; k += 2) {

        // Variable to store the current answer.
        int temp = 1;

        // Remove characters s[l] and s[i].
        if (s[l] == s[k]) {
            temp = calc(l + 1, k - 1, s)
                   * calc(k + 1, r, s)
                   * choose[(r - l + 1) / 2]
                           [(r - k) / 2];
            ans += temp;
        }
    }
    return dp[l][r] = ans;
}

int waysToClearString(string S)
{

    // Initialize all the states of dp to -1
    memset(dp, -1, sizeof(dp));

    // Calculate all Combinations
    int n = S.length();
    choose[0][0] = 1;
    for (int i = 1; i <= n / 2; ++i) {
        choose[i][0] = 1;
        for (int j = 1; j <= i; ++j) {
            choose[i][j]
                = (choose[i - 1][j]
                   + choose[i - 1][j - 1]);
        }
    }
    return calc(0, n - 1, S);
}

// Driver Code
int main()
{
    string S = "aabccb";

    cout << waysToClearString(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

// Define the dp table globally
static int [][]dp = new int[505][505];
static int [][]choose = new int[502][502];

// Recursive function to calculate the dp
// values for range [L, R]
static int calc(int l, int r, String s)
{

    // The range is odd length
            if (Math.abs(r - l) % 2 == 0) {
                return 0;
            }

            if (l > r) {
                return dp[l][r] = 1;
            }

            // The state is already calculated
            if (dp[l][r] != -1) {
                return dp[l][r];
            }

            // If the length is 2
            if ((r - l) == 1) {
                if (s.charAt(l) == s.charAt(r)) {
                    dp[l][r] = 1;
                }
                else {
                    dp[l][r] = 0;
                }
                return dp[l][r];
            }

            // Total answer for this state
            int ans = 0;
            for (int k = l + 1; k <= r; k += 2) {

                // Variable to store the current answer.
                int temp = 1;

                // Remove characters s[l] and s[i].
                if (s.charAt(l) == s.charAt(k)) {
                    temp = calc(l + 1, k - 1, s)
                        * calc(k + 1, r, s)
                        * choose[((r - l + 1) / 2)]
                        [((r - k) / 2)];
                    ans += temp;
                }
            }
            return dp[l][r] = ans;
}

static int waysToClearString(String S)
{

    // Initialize all the states of dp to -1
    // Initialize all the states of dp to -1
    for(int i=0;i<505;i++){
        for(int j=0;j<505;j++)
            dp[i][j] = -1;
    }

            // Calculate all Combinations
            int n = S.length();
            choose[0][0] = 1;
            for (int i = 1; i <= (n / 2); ++i) {
                choose[i][0] = 1;
                for (int j = 1; j <= i; ++j) {
                    choose[i][j]
                        = (choose[i - 1][j]
                            + choose[i - 1][j - 1]);
                }
            }
            return calc(0, n - 1, S);
}

// Driver Code
public static void main (String[] args)
{
    String S = "aabccb";

    System.out.println(waysToClearString(S));
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 implementation for the above approach
import numpy as np

# Define the dp table globally
dp = np.zeros((505,505));
choose = np.zeros((502,502));

# Recursive function to calculate the dp
# values for range [L, R]
def calc(l, r, s) :

    # The range is odd length
    if (abs(r - l) % 2 == 0) :
        return 0;

    if (l > r) :
        dp[l][r] = 1;
        return dp[l][r]

    # The state is already calculated
    if (dp[l][r] != -1) :
        return dp[l][r];

    # If the length is 2
    if ((r - l) == 1) :
        if (s[l] == s[r]) :
            dp[l][r] = 1;

        else :
            dp[l][r] = 0;

        return dp[l][r];

    # Total answer for this state
    ans = 0;

    for k in range(l + 1, r + 1, 2) :

        # Variable to store the current answer.
        temp = 1;

        # Remove characters s[l] and s[i].
        if (s[l] == s[k]) :
            temp = calc(l + 1, k - 1, s) * calc(k + 1, r, s) * choose[(r - l + 1) // 2][(r - k) // 2];
            ans += temp;

    dp[l][r] = ans;
    return dp[l][r]

def waysToClearString(S) :

    # Initialize all the states of dp to -1
    #memset(dp, -1, sizeof(dp));

    for i in range(505):
        for j in range(505) :
            dp[i][j] = -1

    # Calculate all Combinations
    n = len(S);
    choose[0][0] = 1;
    for i in range(1, (n // 2) + 1) :
        choose[i][0] = 1;
        for j in range(1, i + 1) :
            choose[i][j]= choose[i - 1][j] + choose[i - 1][j - 1];

    return calc(0, n - 1, S);

# Driver Code
if __name__ == "__main__" :

    S = "aabccb";

    print(waysToClearString(S));

    # This code is contributed by AnkThon
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;

class GFG{
// Define the dp table globally
static int [,]dp = new int[505,505];
static int [,]choose = new int[502,502];

// Recursive function to calculate the dp
// values for range [L, R]
static int calc(int l, int r, string s)
{

    // The range is odd length
    if (Math.Abs(r - l) % 2 == 0) {
        return 0;
    }

    if (l > r) {
        return dp[l,r] = 1;
    }

    // The state is already calculated
    if (dp[l,r] != -1) {
        return dp[l,r];
    }

    // If the length is 2
    if ((r - l) == 1) {
        if (s[l] == s[r]) {
            dp[l,r] = 1;
        }
        else {
            dp[l,r] = 0;
        }
        return dp[l,r];
    }

    // Total answer for this state
    int ans = 0;
    for (int k = l + 1; k <= r; k += 2) {

        // Variable to store the current answer.
        int temp = 1;

        // Remove characters s[l] and s[i].
        if (s[l] == s[k]) {
            temp = calc(l + 1, k - 1, s)
                   * calc(k + 1, r, s)
                   * choose[(r - l + 1) / 2,(r - k) / 2];
            ans += temp;
        }
    }
    return dp[l,r] = ans;
}

static int waysToClearString(string S)
{

    // Initialize all the states of dp to -1
    for(int i=0;i<505;i++){
        for(int j=0;j<505;j++)
            dp[i,j] = -1;
    }

    // Calculate all Combinations
    int n = S.Length;
    choose[0,0] = 1;
    for (int i = 1; i <= n / 2; ++i) {
        choose[i,0] = 1;
        for (int j = 1; j <= i; ++j) {
            choose[i,j]
                = (choose[i - 1,j]
                   + choose[i - 1,j - 1]);
        }
    }
    return calc(0, n - 1, S);
}

// Driver Code
public static void Main()
{
    string S = "aabccb";

    Console.Write(waysToClearString(S));
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Define the dp table globally
        var dp = new Array(505);

        for (var i = 0; i < dp.length; i++) {
            dp[i] = new Array(505).fill(-1);
        }
        var choose = new Array(505);

        for (var i = 0; i < choose.length; i++) {
            choose[i] = new Array(505).fill(0);
        }

        // Recursive function to calculate the dp
        // values for range [L, R]
        function calc(l, r, s) {

            // The range is odd length
            if (Math.abs(r - l) % 2 == 0) {
                return 0;
            }

            if (l > r) {
                return dp[l][r] = 1;
            }

            // The state is already calculated
            if (dp[l][r] != -1) {
                return dp[l][r];
            }

            // If the length is 2
            if ((r - l) == 1) {
                if (s[l] == s[r]) {
                    dp[l][r] = 1;
                }
                else {
                    dp[l][r] = 0;
                }
                return dp[l][r];
            }

            // Total answer for this state
            let ans = 0;
            for (let k = l + 1; k <= r; k += 2) {

                // Variable to store the current answer.
                let temp = 1;

                // Remove characters s[l] and s[i].
                if (s[l] == s[k]) {
                    temp = calc(l + 1, k - 1, s)
                        * calc(k + 1, r, s)
                        * choose[Math.floor((r - l + 1) / 2)]
                        [Math.floor((r - k) / 2)];
                    ans += temp;
                }
            }
            return dp[l][r] = ans;
        }

        function waysToClearString(S) {

            // Initialize all the states of dp to -1

            // Calculate all Combinations
            let n = S.length;
            choose[0][0] = 1;
            for (let i = 1; i <= Math.floor(n / 2); ++i) {
                choose[i][0] = 1;
                for (let j = 1; j <= i; ++j) {
                    choose[i][j]
                        = (choose[i - 1][j]
                            + choose[i - 1][j - 1]);
                }
            }
            return calc(0, n - 1, S);
        }

        // Driver Code

        let S = "aabccb";

        document.write(waysToClearString(S));

// This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
3
```

***时间复杂度:**o(n^3)*
*T6】辅助空间: O(N^2)*