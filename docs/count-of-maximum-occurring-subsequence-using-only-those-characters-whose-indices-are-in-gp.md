# 仅使用那些索引在 GP

中的字符计算最大出现子序列

> 原文:[https://www . geesforgeks . org/最大出现子序列计数-仅使用那些索引在 gp 中的字符/](https://www.geeksforgeeks.org/count-of-maximum-occurring-subsequence-using-only-those-characters-whose-indices-are-in-gp/)

给定一个字符串 **S** ，任务是仅使用那些索引在[几何级数](https://www.geeksforgeeks.org/geometric-progression/)中的字符，从 **S** 中找到最大出现子序列 **P** 的计数。
**注:**考虑 s 中基于 1 的索引。

**示例:**

> **输入:**S =“ddee”
> T3】输出: 4
> **解释:**
> 如果我们取 P =“de”，那么 P 在 S 中出现 4 次。{ {1，3}、{1，4}、{2，3}、{2，4} }
> 
> **输入:**S =“geeks forgeeks”
> T3】输出: 6
> **解释:**
> 如果我们取 P =“ek”，那么 P 在 S 中出现 6 次。{ {2，4}，{3，4}，{2，12} {3，12}，{10，12}，{11，12}

**天真方法:**想法是[生成给定字符串的所有可能的子序列](https://www.geeksforgeeks.org/print-subsequences-string/)，使得字符串的索引必须处于**几何级数**中。现在对于生成的每个子序列，找到每个子序列的出现次数[，并打印这些出现次数中的最大值。](https://www.geeksforgeeks.org/count-distinct-occurrences-as-a-subsequence/)

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效方法:**想法是观察任何子序列 **P** 可以是**任何长度**。假设 P =“abc”并且它在 S 中出现 10 次(其中“ABC”在 S 中的 GP 中有它们的索引)，那么我们可以看到子序列“ab”(在 GP 中有索引)也将在 S 中出现 10 次。因此，为了简化解决方案，P 的可能长度将是**小于等于**等于 2。以下是步骤:

1.  有必要选择长度**大于 1** 的子序列 **P** ，因为如果 S 不仅仅包含唯一字符，长度大于 1 的 **P** 将比长度为 1 的子序列出现更多的时间。
2.  对于长度 1，计算字符串中每个字母的[频率。](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)
3.  对于长度 2，形成一个 2D 数组 **dp[26][26]** ，其中 **dp[i][j]** 表示**字符(' a' + i) +字符(' a' + j)** 的字符串频率。
4.  步骤 2 中使用的递归关系由下式给出:

> dp[i][j] = dp[i][j] + freq[i]
> 其中，
> freq[i] =字符 char 的频率(' a '+I)
> DP[I][j]= current _ char+char(' a '+I)形成的字符串的频率。

1.  频率数组和数组 **dp[][]** 的[最大值给出给定字符串中任何子序列](https://www.geeksforgeeks.org/frequent-element-array/)的[最大计数。](https://www.geeksforgeeks.org/frequency-of-maximum-occurring-subsequence-in-given-string/)

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count maximum occurring
// subsequence using only those characters
// whose indexes are in GP
int findMaxTimes(string S)
{
    long long int arr[26];
    long long int dp[26][26];

    // Initialize 1-D array and 2-D
    // dp array to 0
    memset(arr, 0, sizeof(arr));
    memset(dp, 0, sizeof(dp));

    // Iterate till the length of
    // the given string
    for (int i = 0; i < S.size(); i++) {
        int now = S[i] - 'a';
        for (int j = 0; j < 26; j++) {
            dp[j][now] += arr[j];
        }
        arr[now]++;
    }

    long long int ans = 0;

    // Update ans for 1-length subsequence
    for (int i = 0; i < 26; i++)
        ans = max(ans, arr[i]);

    // Update ans for 2-length subsequence
    for (int i = 0; i < 26; i++) {
        for (int j = 0; j < 26; j++) {
            ans = max(ans, dp[i][j]);
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    // Given string s
    string S = "ddee";

    // Function Call
    cout << findMaxTimes(S);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count maximum occurring
// subsequence using only those characters
// whose indexes are in GP
static int findMaxTimes(String S)
{
    int []arr = new int[26];
    int [][]dp = new int[26][26];

    // Iterate till the length of
    // the given String
    for(int i = 0; i < S.length(); i++)
    {
        int now = S.charAt(i) - 'a';
        for(int j = 0; j < 26; j++)
        {
            dp[j][now] += arr[j];
        }
        arr[now]++;
    }

    int ans = 0;

    // Update ans for 1-length subsequence
    for(int i = 0; i < 26; i++)
        ans = Math.max(ans, arr[i]);

    // Update ans for 2-length subsequence
    for(int i = 0; i < 26; i++)
    {
        for(int j = 0; j < 26; j++)
        {
            ans = Math.max(ans, dp[i][j]);
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given String s
    String S = "ddee";

    // Function call
    System.out.print(findMaxTimes(S));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count maximum occurring
# subsequence using only those characters
# whose indexes are in GP
def findMaxTimes(S):

    # Initialize 1-D array and 2-D
    # dp array to 0
    arr = [0] * 26
    dp = [[0 for x in range(26)]
             for y in range(26)]

    # Iterate till the length of
    # the given string
    for i in range(len(S)):
        now = ord(S[i]) - ord('a')

        for j in range(26):
            dp[j][now] += arr[j]

        arr[now] += 1

    ans = 0

    # Update ans for 1-length subsequence
    for i in range(26):
        ans = max(ans, arr[i])

    # Update ans for 2-length subsequence
    for i in range(26):
        for j in range(26):
            ans = max(ans, dp[i][j])

    # Return the answer
    return ans

# Driver Code

# Given string s
S = "ddee"

# Function call
print(findMaxTimes(S))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to count maximum occurring
// subsequence using only those characters
// whose indexes are in GP
static int findMaxTimes(String S)
{
    int []arr = new int[26];
    int [,]dp = new int[26, 26];

    // Iterate till the length of
    // the given String
    for(int i = 0; i < S.Length; i++)
    {
        int now = S[i] - 'a';
        for(int j = 0; j < 26; j++)
        {
            dp[j, now] += arr[j];
        }
        arr[now]++;
    }

    int ans = 0;

    // Update ans for 1-length subsequence
    for(int i = 0; i < 26; i++)
        ans = Math.Max(ans, arr[i]);

    // Update ans for 2-length subsequence
    for(int i = 0; i < 26; i++)
    {
        for(int j = 0; j < 26; j++)
        {
            ans = Math.Max(ans, dp[i, j]);
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Given String s
    String S = "ddee";

    // Function call
    Console.Write(findMaxTimes(S));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count maximum occurring
// subsequence using only those characters
// whose indexes are in GP
function findMaxTimes(S)
{
    var arr = Array(26).fill(0);
    var dp = Array.from(Array(26), ()=>Array(26).fill(0));

    // Iterate till the length of
    // the given string
    for (var i = 0; i < S.length; i++)
    {
        var now = S[i].charCodeAt(0) - 'a'.charCodeAt(0);
        for (var j = 0; j < 26; j++)
        {
            dp[j][now] += arr[j];
        }
        arr[now]++;
    }

    var ans = 0;

    // Update ans for 1-length subsequence
    for (var i = 0; i < 26; i++)
        ans = Math.max(ans, arr[i]);

    // Update ans for 2-length subsequence
    for (var i = 0; i < 26; i++)
    {
        for (var j = 0; j < 26; j++)
        {
            ans = Math.max(ans, dp[i][j]);
        }
    }

    // Return the answer
    return ans;
}

// Driver Code
// Given string s
var S = "ddee";

// Function Call
document.write( findMaxTimes(S));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(最大值(N*26，26 * 26))*
***辅助空间:** O(26 * 26)*