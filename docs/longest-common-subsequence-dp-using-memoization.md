# 使用记忆的最长公共子序列| DP

> 原文:[https://www . geesforgeks . org/最长-公共-子序列-dp-using-memoization/](https://www.geeksforgeeks.org/longest-common-subsequence-dp-using-memoization/)

给定两个字符串 s1 和 s2，任务是找到两个字符串中最长的公共子序列的长度。

**示例:**

> **输入:**S1 =“ABCDGH”，S2 =“AEDFHR”
> T3】输出: 3
> LCS 对于输入序列“AGGTAB”和“GXTXAYB”是长度为 4 的“GTAB”。
> **输入:** s1 =“奋斗者”，S2 =“Raj”
> **输出:** 1

这个问题的**天真解决方案**是生成两个给定序列的所有子序列，并找到最长的匹配子序列。这个解决方案在时间复杂度方面是指数级的。该问题的一般递归解决方案是生成两个给定序列的所有子序列，并找到最长的匹配子序列。总的可能组合为 2 <sup>n</sup> 。因此，递归解将取 **O(2 <sup>n</sup> )** 。
**最优子结构:**

*   假设输入序列分别是长度为 m 和 n 的 X[0… m-1]和 Y[0…n-1]。并且设 L(X[0… m-1]，Y[0…n-1])是两个序列 X 和 Y 的 LCS 长度，下面是 L(X[0… m-1]，Y[0…n-1])的递归定义。
*   如果两个序列的最后一个字符匹配(或 X[m-1] == Y[n-1])，那么 L(X[0… m-1]，Y[0…n-1]) = 1 + L(X[0… m-2]，Y[0…n-2])
*   如果两个序列的最后一个字符不匹配(或 X[m-1]！= Y[n-1])然后 L(X[0… m-1]，Y[0…n-1]) = MAX (L(X[0… m-2]，Y[0…n-1])，L(X[0… m-1]，Y[0…n-2])

下面给出了 LCS 问题的递归解:

## C++

```
// A Naive C++ recursive implementation
// of LCS of two strings
#include <bits/stdc++.h>
using namespace std;

// Returns length of LCS for X[0..m-1], Y[0..n-1]
int lcs(string X, string Y, int m, int n)
{
    if (m == 0 || n == 0)
        return 0;

    if (X[m - 1] == Y[n - 1])
        return 1 + lcs(X, Y, m - 1, n - 1);
    else
        return max(lcs(X, Y, m, n - 1),
                   lcs(X, Y, m - 1, n));
}

// Driver Code
int main()
{
    string X = "AGGTAB";
    string Y = "GXTXAYB";

    // Find the length of string
    int m = X.length();
    int n = Y.length();

    cout << "Length of LCS: " << lcs(X, Y, m, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Naive Java recursive implementation
// of LCS of two strings

class GFG {

// Returns length of LCS for X[0..m-1], Y[0..n-1]
    static int lcs(String X, String Y, int m, int n) {
        if (m == 0 || n == 0) {
            return 0;
        }

        if (X.charAt(m - 1) == Y.charAt(n - 1)) {
            return 1 + lcs(X, Y, m - 1, n - 1);
        } else {
            return Math.max(lcs(X, Y, m, n - 1),
                    lcs(X, Y, m - 1, n));
        }
    }
// Driver Code

    public static void main(String[] args) {
        String X = "AGGTAB";
        String Y = "GXTXAYB";

        // Find the length of String
        int m = X.length();
        int n = Y.length();
        System.out.println("Length of LCS: " + lcs(X, Y, m, n));

    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# A Naive Python recursive implementation
# of LCS of two strings

# Returns length of LCS for X[0..m-1], Y[0..n-1]
def lcs(X, Y, m, n):
    if (m == 0 or n == 0):
        return 0

    if (X[m - 1] == Y[n - 1]):
        return 1 + lcs(X, Y, m - 1, n - 1)
    else:
        return max(lcs(X, Y, m, n - 1),
                   lcs(X, Y, m - 1, n))

# Driver Code
if __name__ == '__main__':
    X = "AGGTAB"
    Y = "GXTXAYB"

    # Find the length of string
    m = len(X)
    n = len(Y)

    print("Length of LCS:",
           lcs(X, Y, m, n))

# This code is contributed by 29AjayKumar
```

## C#

```
// A Naive recursive C#implementation of
// LCS of two strings
using System;

class GFG
{

// Returns length of LCS for
// X[0..m-1], Y[0..n-1]
static int lcs(String X, String Y,
               int m, int n)
{
    if (m == 0 || n == 0)
    {
        return 0;
    }

    if (X[m - 1] == Y[n - 1])
    {
        return 1 + lcs(X, Y, m - 1, n - 1);
    } else {
        return Math.Max(lcs(X, Y, m, n - 1),
                        lcs(X, Y, m - 1, n));
    }
}

// Driver Code
public static void Main()
{
    String X = "AGGTAB";
    String Y = "GXTXAYB";

    // Find the length of String
    int m = X.Length;
    int n = Y.Length;
    Console.Write("Length of LCS: " +
                    lcs(X, Y, m, n));
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Naive PHP recursive implementation
// of LCS of two strings

// Returns length of LCS for
// X[0..m-1], Y[0..n-1]
function lcs($X, $Y, $m, $n)
{
    if ($m == 0 || $n == 0)
        return 0;

    if ($X[$m - 1] == $Y[$n - 1])
        return 1 + lcs($X, $Y,
                       $m - 1, $n - 1);
    else
        return max(lcs($X, $Y, $m, $n - 1),
                   lcs($X, $Y, $m - 1, $n));
}

// Driver Code
$X = "AGGTAB";
$Y = "GXTXAYB";

// Find the length of string
$m = strlen($X);
$n = strlen($Y);

echo "Length of LCS: " . lcs($X, $Y, $m, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// A Naive Javascript recursive implementation
// of LCS of two strings

    // Returns length of LCS for X[0..m-1], Y[0..n-1]
    function lcs(X,Y,m,n)
    {
        if (m == 0 || n == 0) {
            return 0;
        }

        if (X[m-1] == Y[n-1]) {
            return 1 + lcs(X, Y, m - 1, n - 1);
        } else {
            return Math.max(lcs(X, Y, m, n - 1),
                    lcs(X, Y, m - 1, n));
        }
    }

    // Driver Code
    let X = "AGGTAB";
    let Y = "GXTXAYB";
    // Find the length of String
    let m = X.length;
    let n = Y.length;
    document.write("Length of LCS: " + lcs(X, Y, m, n));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Length of LCS: 4
```

**使用记忆的动态编程**

考虑到上面的实现，下面是输入字符串*【AXYT】**【AYZX】*的部分递归树

```
                       lcs("AXYT", "AYZX")
                       /                 \
         lcs("AXY", "AYZX")            lcs("AXYT", "AYZ")
         /           \                   /               \
lcs("AX", "AYZX") lcs("AXY", "AYZ")   lcs("AXY", "AYZ") lcs("AXYT", "AY")
```

在上面的部分递归树中，**LCS(“AXY”、“AYZ”)被求解了两次**。在绘制完整的递归树时，已经观察到有许多子问题被反复解决。所以这个问题具有**重叠子结构**的性质，通过使用[T5【记忆】T7 或](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)[T9【制表】T10](https://www.geeksforgeeks.org/longest-common-subsequence/)可以避免相同子问题的重新计算。这里已经讨论了制表方法[。](https://www.geeksforgeeks.org/longest-common-subsequence/)
在递归代码中使用**记忆**的一个常见观察点将是每次函数调用中的**两个非常数参数 M 和 N** 。该函数有 4 个参数，但有 2 个参数是常量，不影响记忆化。重复的调用发生在之前调用过的 N 和 M 上。遵循以下步骤将有助于我们使用记忆来编写动力定位解决方案。

*   当字符串索引从 0 开始时，使用二维数组将计算出的 **lcs(m，n)值存储在 arr[m-1][n-1]** 处。
*   每当再次调用具有相同参数 m 和 n 的函数时，不要执行任何进一步的递归调用并返回 *arr[m-1][n-1]* ，因为 lcs(m，n)的先前计算已经存储在 *arr[m-1][n-1]* 中，因此减少了多次发生的递归调用。

下面是上述方法的实现:

## C++

```
// C++ program to memoize
// recursive implementation of LCS problem
#include <bits/stdc++.h>
using namespace std;

const int maximum = 1000;

// Returns length of LCS for X[0..m-1], Y[0..n-1] */
// memoization applied in recursive solution
int lcs(string X, string Y, int m, int n, int dp[][maximum])
{
    // base case
    if (m == 0 || n == 0)
        return 0;

    // if the same state has already been
    // computed
    if (dp[m - 1][n - 1] != -1)
        return dp[m - 1][n - 1];

    // if equal, then we store the value of the
    // function call
    if (X[m - 1] == Y[n - 1]) {

        // store it in arr to avoid further repetitive
        // work in future function calls
        dp[m - 1][n - 1] = 1 + lcs(X, Y, m - 1, n - 1, dp);

        return dp[m - 1][n - 1];
    }
    else {

        // store it in arr to avoid further repetitive
        // work in future function calls
        dp[m - 1][n - 1] = max(lcs(X, Y, m, n - 1, dp),
                               lcs(X, Y, m - 1, n, dp));

        return dp[m - 1][n - 1];
    }
}

// Driver Code
int main()
{

    string X = "AGGTAB";
    string Y = "GXTXAYB";
    int m = X.length();
    int n = Y.length();

    int dp[m][maximum];

    // assign -1 to all positions
    memset(dp, -1, sizeof(dp));

    cout << "Length of LCS: " << lcs(X, Y, m, n, dp);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Java program to memoize
// recursive implementation of LCS problem
class GFG {

    static final int maximum = 1000;

// Returns length of LCS for X[0..m-1], Y[0..n-1] */
// memoization applied in recursive solution
    static int lcs(String X, String Y, int m, int n, int dp[][]) {
        // base case
        if (m == 0 || n == 0) {
            return 0;
        }

        // if the same state has already been
        // computed
        if (dp[m - 1][n - 1] != -1) {
            return dp[m - 1][n - 1];
        }

        // if equal, then we store the value of the
        // function call
        if (X.charAt(m - 1) == Y.charAt(n - 1)) {

            // store it in arr to avoid further repetitive
            // work in future function calls
            dp[m - 1][n - 1] = 1 + lcs(X, Y, m - 1, n - 1, dp);

            return dp[m - 1][n - 1];
        } else {

            // store it in arr to avoid further repetitive
            // work in future function calls
            dp[m - 1][n - 1] = Math.max(lcs(X, Y, m, n - 1, dp),
                    lcs(X, Y, m - 1, n, dp));

            return dp[m - 1][n - 1];
        }
    }

// Driver Code
    public static void main(String[] args) {
        String X = "AGGTAB";
        String Y = "GXTXAYB";
        int m = X.length();
        int n = Y.length();

        int dp[][] = new int[m][maximum];

        // assign -1 to all positions
        for (int[] row : dp) {
            Arrays.fill(row, -1);
        }

        System.out.println("Length of LCS: " + lcs(X, Y, m, n, dp));
    }
}
/* This Java code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python3 program to memoize
# recursive implementation of LCS problem
maximum = 1000

# Returns length of LCS for X[0..m-1], Y[0..n-1] */
# memoization applied in recursive solution
def lcs(X, Y, m, n, dp):

    # base case
    if (m == 0 or n == 0):
        return 0

    # if the same state has already been
    # computed
    if (dp[m - 1][n - 1] != -1):
        return dp[m - 1][n - 1]

    # if equal, then we store the value of the
    # function call
    if (X[m - 1] == Y[n - 1]):

        # store it in arr to avoid further repetitive
        # work in future function calls
        dp[m - 1][n - 1] = 1 + lcs(X, Y, m - 1, n - 1, dp)

        return dp[m - 1][n - 1]

    else :

        # store it in arr to avoid further repetitive
        # work in future function calls
        dp[m - 1][n - 1] = max(lcs(X, Y, m, n - 1, dp),
                               lcs(X, Y, m - 1, n, dp))

        return dp[m - 1][n - 1]

# Driver Code
X = "AGGTAB"
Y = "GXTXAYB"
m = len(X)
n = len(Y)

dp = [[-1 for i in range(maximum)]
          for i in range(m)]

print("Length of LCS:", lcs(X, Y, m, n, dp))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to memoize
// recursive implementation of LCS problem
using System;

class GFG
{
static readonly int maximum = 1000;

// Returns length of LCS for
// X[0..m-1], Y[0..n-1]
// memoization applied in
// recursive solution
static int lcs(String X, String Y,
               int m, int n, int [,]dp)
{
    // base case
    if (m == 0 || n == 0)
    {
        return 0;
    }

    // if the same state has already been
    // computed
    if (dp[m - 1, n - 1] != -1)
    {
        return dp[m - 1, n - 1];
    }

    // if equal, then we store the value
    // of the function call
    if (X[m - 1] == Y[n - 1])
    {

        // store it in arr to avoid
        // further repetitive work
        // in future function calls
        dp[m - 1,
           n - 1] = 1 + lcs(X, Y, m - 1,
                                  n - 1, dp);

        return dp[m - 1, n - 1];
    }
    else
    {

        // store it in arr to avoid
        // further repetitive work
        // in future function calls
        dp[m - 1,
           n - 1] = Math.Max(lcs(X, Y, m, n - 1, dp),
                             lcs(X, Y, m - 1, n, dp));

        return dp[m - 1, n - 1];
    }
}

// Driver Code
public static void Main(String[] args)
{
    String X = "AGGTAB";
    String Y = "GXTXAYB";
    int m = X.Length;
    int n = Y.Length;

    int [,]dp = new int[m, maximum];

    // assign -1 to all positions
    for(int i = 0; i < m; i++)
    {
        for(int j = 0; j < maximum; j++)
        {
            dp[i, j] = -1;
        }
    }
    Console.WriteLine("Length of LCS: " +
                    lcs(X, Y, m, n, dp));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to memoize
// recursive implementation of LCS problem

let maximum = 1000;

// Returns length of LCS for X[0..m-1], Y[0..n-1] */
// memoization applied in recursive solution
function lcs(X,Y,m,n,dp)
{
    // base case
        if (m == 0 || n == 0) {
            return 0;
        }

        // if the same state has already been
        // computed
        if (dp[m - 1][n - 1] != -1) {
            return dp[m - 1][n - 1];
        }

        // if equal, then we store the value of the
        // function call
        if (X[m-1] == Y[n-1]) {

            // store it in arr to avoid further repetitive
            // work in future function calls
            dp[m - 1][n - 1] = 1 + lcs(X, Y, m - 1, n - 1, dp);

            return dp[m - 1][n - 1];
        } else {

            // store it in arr to avoid further repetitive
            // work in future function calls
            dp[m - 1][n - 1] = Math.max(lcs(X, Y, m, n - 1, dp),
                    lcs(X, Y, m - 1, n, dp));

            return dp[m - 1][n - 1];
        }
}

// Driver Code
let X = "AGGTAB";
let Y = "GXTXAYB";
let m = X.length;
let n = Y.length;

let dp=new Array(m);
for(let i=0;i<dp.length;i++)
{
    dp[i]=new Array(maximum);
    for(let j=0;j<dp[i].length;j++)
    {
        dp[i][j]=-1;
    }
}

document.write("Length of LCS: " + lcs(X, Y, m, n, dp));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Length of LCS: 4
```

**时间复杂度:** O(N * M)，其中 N 和 M 分别是第一个和第二个字符串的长度。
**辅助空间:** (N * M)