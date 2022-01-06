# 通过将字符移动到前面或末尾将给定字符串转换为另一个字符串的最小操作

> 原文:[https://www . geesforgeks . org/通过将字符移动到前端或后端将给定字符串转换为另一个字符串的最小操作数/](https://www.geeksforgeeks.org/minimum-operations-to-transform-given-string-to-another-by-moving-characters-to-front-or-end/)

给定两个长度为 **N** 的字符串 **S** 和 **T** ，由小写字母组成，它们是相互排列的，任务是打印将 **S** 转换为 **T** 的最小操作数。在一个操作中，选择字符串 **S** 的任意字符，并将其移动到字符串 **S** 的开始或结束。

**示例:**

> **输入:**S =“abcde”，T =“edacb”
> T3】输出: 3
> **说明:**
> 我们可以通过 3 招将 S 转换为 T:
> 1。移动“d”开始:“dab ce”
> 2。移动“e”开始:“edabac”
> 3。将“b”移至末尾:“edacb”
> 
> **输入:** S = "dcdb "，T = "ddbc"
> **输出:** 1
> **说明:**
> 移动' c '结束

**天真方法:**天真方法是尝试所有交换角色的可能性。一个人可以把一些角色放在前面，放在最后，也可以把它放在同样的位置。以上三个操作可以使用[递归](https://www.geeksforgeeks.org/recursion/) 解决，并打印所有步骤后所需的最小步骤数。
***时间复杂度:** O(3 <sup>N</sup> ，其中 N 为给定字符串的长度。*
***辅助空间:** O(1)*

**高效方法:**对上述方法进行优化，其思路是观察移动字符串 **S** 的字符后，未变化的字符聚集在一起形成 **T** 中的连续子串。所以，如果我们能最大化这个子序列的长度，那么将字符串 **S** 转换为 **T** 的运算次数为:

> n–T 的最长连续子串的长度，它是 S 的子串

因此，要找到 **T** 的最长连续子串的长度，即字符串 **S** 的子序列，就要找到[最长公共子序列](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)的 **S** 和 **T** 。让 **dp[][]** 存储 **T** 的最长连续子串的长度，即字符串 **S** 的子序列。现在 **dp[i][j]** 将存储 **T[0，…，j]** 最长后缀的长度，这也是 **S[0，…，i]** 的子序列。递归关系由下式给出:

*   如果 I 大于 0， **dp[i][j] = max(dp[i-1][j]，dp[i][j])。**
*   如果 S[i]等于 T[i]，那么， **dp[i][j] = 1 + dp[i-1][j-1]。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int dp[1010][1010];

// Function that finds the minimum number
// of steps to find the minimum characters
// must be moved to convert string s to t
int solve(string s, string t)
{

    int n = s.size();

    // r = maximum value over all
    // dp[i][j] computed so far
    int r = 0;

    // dp[i][j] stores the longest
    // contiguous suffix of T[0..j]
    // that is subsequence of S[0..i]
    for (int i = 0; i < n; i++) {

        for (int j = 0; j < n; j++) {

            dp[i][j] = 0;
            if (i > 0) {

                dp[i][j] = max(dp[i - 1][j],
                               dp[i][j]);
            }
            if (s[i] == t[j]) {

                int ans = 1;
                if (i > 0 && j > 0) {

                    ans = 1 + dp[i - 1][j - 1];
                }

                // Update the maximum length
                dp[i][j] = max(dp[i][j], ans);
                r = max(r, dp[i][j]);
            }
        }
    }

    // Return the resulting length
    return (n - r);
}

// Driver Code
int main()
{
    // Given string s, t
    string s = "abcde";
    string t = "edacb";

    // Function Call
    cout << solve(s, t);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{
    static int[][] dp = new int[1010][1010];

    // Function that finds the minimum number
    // of steps to find the minimum characters
    // must be moved to convert String s to t
    static int solve(String s, String t)
    {
        int n = s.length();

        // r = maximum value over all
        // dp[i][j] computed so far
        int r = 0;

        // dp[i][j] stores the longest
        // contiguous suffix of T[0..j]
        // that is subsequence of S[0..i]
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                dp[i][j] = 0;
                if (i > 0)
                {
                    dp[i][j] = Math.max(dp[i - 1][j],
                                        dp[i][j]);
                }
                if (s.charAt(i) == t.charAt(j))
                {
                    int ans = 1;
                    if (i > 0 && j > 0)
                    {
                        ans = 1 + dp[i - 1][j - 1];
                    }

                    // Update the maximum length
                    dp[i][j] = Math.max(dp[i][j], ans);
                    r = Math.max(r, dp[i][j]);
                }
            }
        }

        // Return the resulting length
        return (n - r);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given String s, t
        String s = "abcde";
        String t = "edacb";

        // Function Call
        System.out.print(solve(s, t));
    }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach
dp = [[0] * 1010] * 1010

# Function that finds the minimum number
# of steps to find the minimum characters
# must be moved to convert string s to t
def solve(s, t):

    n = len(s)

    # r = maximum value over all
    # dp[i][j] computed so far
    r = 0

    # dp[i][j] stores the longest
    # contiguous suffix of T[0..j]
    # that is subsequence of S[0..i]
    for j in range(0, n):
        for i in range(0, n):
            dp[i][j] = 0

            if (i > 0):
                dp[i][j] = max(dp[i - 1][j],
                               dp[i][j])

            if (s[i] == t[j]):
                ans = 1
                if (i > 0 and j > 0):
                    ans = 1 + dp[i - 1][j - 1]

                # Update the maximum length
                dp[i][j] = max(dp[i][j], ans)
                r = max(r, dp[i][j])

    # Return the resulting length
    return (n - r)

# Driver Code

# Given string s, t
s = "abcde"
t = "edacb"

# Function call
print(solve(s, t))

# This code is contributed by code_hunt
```

## C#

```
// C# program for the above approach
using System;
class GFG{
static int[, ] dp = new int[1010, 1010];

// Function that finds the minimum number
// of steps to find the minimum characters
// must be moved to convert String s to t
static int solve(String s, String t)
{
    int n = s.Length;

    // r = maximum value over all
    // dp[i, j] computed so far
    int r = 0;

    // dp[i, j] stores the longest
    // contiguous suffix of T[0..j]
    // that is subsequence of S[0..i]
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            dp[i, j] = 0;
            if (i > 0)
            {
                dp[i, j] = Math.Max(dp[i - 1, j],
                                    dp[i, j]);
            }
            if (s[i] == t[j])
            {
                int ans = 1;
                if (i > 0 && j > 0)
                {
                    ans = 1 + dp[i - 1, j - 1];
                }

                // Update the maximum length
                dp[i, j] = Math.Max(dp[i, j], ans);
                r = Math.Max(r, dp[i, j]);
            }
        }
    }

    // Return the resulting length
    return (n - r);
}

// Driver Code
public static void Main(String[] args)
{

    // Given String s, t
    String s = "abcde";
    String t = "edacb";

    // Function Call
    Console.Write(solve(s, t));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

var dp = Array.from(Array(1010), ()=> Array(1010));

// Function that finds the minimum number
// of steps to find the minimum characters
// must be moved to convert string s to t
function solve(s, t)
{

    var n = s.length;

    // r = maximum value over all
    // dp[i][j] computed so far
    var r = 0;

    // dp[i][j] stores the longest
    // contiguous suffix of T[0..j]
    // that is subsequence of S[0..i]
    for (var i = 0; i < n; i++) {

        for (var j = 0; j < n; j++) {

            dp[i][j] = 0;
            if (i > 0) {

                dp[i][j] = Math.max(dp[i - 1][j],
                               dp[i][j]);
            }
            if (s[i] == t[j]) {

                var ans = 1;
                if (i > 0 && j > 0) {

                    ans = 1 + dp[i - 1][j - 1];
                }

                // Update the maximum length
                dp[i][j] = Math.max(dp[i][j], ans);
                r = Math.max(r, dp[i][j]);
            }
        }
    }

    // Return the resulting length
    return (n - r);
}

// Driver Code
// Given string s, t
var s = "abcde";
var t = "edacb";
// Function Call
document.write( solve(s, t));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N <sup>2</sup> ，其中 N 为给定字符串的长度*
***辅助空间:** O(N <sup>2</sup> )*

**注意:**上面的简单方法对于较小的字符串是有效的，而上面的有效方法对于较大的字符串是有效的。