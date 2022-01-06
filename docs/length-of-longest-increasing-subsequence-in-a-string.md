# 字符串中最长递增子序列的长度

> 原文:[https://www . geeksforgeeks . org/最长递增字符串子序列长度/](https://www.geeksforgeeks.org/length-of-longest-increasing-subsequence-in-a-string/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到给定字符串中[最长递增子序列](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)的长度。

> 按照其 [ASCII 值](https://en.wikipedia.org/wiki/ASCII)的递增顺序排列的字符序列称为递增序列。

**示例:**

> **输入:**S = " abcfg FFS "
> T3】输出: 6
> **说明:**子序列“**abcfg**”是字符串中存在的最长递增子序列。因此，最长递增子序列的长度为 **6** 。
> 
> **输入:**S = " aabac "
> T3】输出: 3

**方法:**思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。按照下面给出的步骤解决问题:

*   初始化一个数组，比如说大小为 **26** 的 **dp[]** ，在每个 **i** <sup>第</sup>个索引处存储最长递增子序列的长度，该最长递增子序列的最后一个字符是**(' a '+I)**<sup>。</sup>
*   初始化变量，比如**列表**，存储所需子序列的长度。
*   [迭代字符串的每个字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 。
    *   对于遇到的每个字符，即**S[I]–‘a’**，检查所有字符，如 **j** ，ASCII 值小于当前字符的值。
    *   初始化一个变量，比如 **curr** ，存储以当前字符结束的 LIS 长度。
    *   用**最大值更新**curr**(curr，dp[j])。**
    *   更新 LIS 的长度，用 **max(lis，curr + 1)表示 **lis、**。**
    *   更新**DP[S[I]–‘a’]**最大值为**d[S[I]–‘a’]**和 **curr。**
*   最后，打印 **lis** 的值作为 lis 的所需长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find length of longest
// increasing subsequence in a string
int lisOtimised(string s)
{
    // Stores at every i-th index, the
    // length of the longest increasing
    // subsequence ending with character i
    int dp[30] = { 0 };

    // Size of string
    int N = s.size();

    // Stores the length of LIS
    int lis = INT_MIN;

    // Iterate over each
    // character of the string
    for (int i = 0; i < N; i++) {

        // Store position of the
        // current character
        int val = s[i] - 'a';

        // Stores the length of LIS
        // ending with current character
        int curr = 0;

        // Check for all characters
        // less then current character
        for (int j = 0; j < val; j++) {
            curr = max(curr, dp[j]);
        }

        // Include current character
        curr++;

        // Update length of longest
        // increasing subsequence
        lis = max(lis, curr);

        // Updating LIS for current character
        dp[val] = max(dp[val], curr);
    }

    // Return the length of LIS
    return lis;
}

// Driver Code
int main()
{
    string s = "fdryutiaghfse";
    cout << lisOtimised(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int mn = -2147483648;

// Function to find length of longest
// increasing subsequence in a string
static int lisOtimised(String s)
{

    // Stores at every i-th index, the
    // length of the longest increasing
    // subsequence ending with character i
    int []dp = new int[30];
    Arrays.fill(dp, 0);

    // Size of string
    int N = s.length();

    // Stores the length of LIS
    int lis = mn;

    // Iterate over each
    // character of the string
    for(int i = 0; i < N; i++)
    {

        // Store position of the
        // current character
        int val =  (int)s.charAt(i) - 97;

        // Stores the length of LIS
        // ending with current character
        int curr = 0;

        // Check for all characters
        // less then current character
        for(int j = 0; j < val; j++)
        {
            curr = Math.max(curr, dp[j]);
        }

        // Include current character
        curr++;

        // Update length of longest
        // increasing subsequence
        lis = Math.max(lis, curr);

        // Updating LIS for current character
        dp[val] = Math.max(dp[val], curr);
    }

    // Return the length of LIS
    return lis;
}

// Driver Code
public static void main(String[] args)
{
    String s = "fdryutiaghfse";

    System.out.print(lisOtimised(s));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find length of longest
# increasing subsequence in a string
def lisOtimised(s):

    # Stores at every i-th index, the
    # length of the longest increasing
    # subsequence ending with character i
    dp = [0]*30

    # Size of string
    N = len(s)

    # Stores the length of LIS
    lis = -10**9

    # Iterate over each
    # character of the string
    for i in range(N):

        # Store position of the
        # current character
        val = ord(s[i]) - ord('a')

        # Stores the length of LIS
        # ending with current character
        curr = 0

        # Check for all characters
        # less then current character
        for j in range(val):
            curr = max(curr, dp[j])

        # Include current character
        curr += 1

        # Update length of longest
        # increasing subsequence
        lis = max(lis, curr)

        # Updating LIS for current character
        dp[val] = max(dp[val], curr)

    # Return the length of LIS
    return lis

# Driver Code
if __name__ == '__main__':
    s = "fdryutiaghfse"
    print (lisOtimised(s))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{
 static int mn = -2147483648;

 // Function to find length of longest
// increasing subsequence in a string
static int lisOtimised(string s)
{

    // Stores at every i-th index, the
    // length of the longest increasing
    // subsequence ending with character i
    int []dp = new int[30];
    Array.Clear(dp, 0, 30);

    // Size of string
    int N = s.Length;

    // Stores the length of LIS
    int lis = mn;

    // Iterate over each
    // character of the string
    for (int i = 0; i < N; i++) {

        // Store position of the
        // current character
        int val =  (int)s[i] - 97;

        // Stores the length of LIS
        // ending with current character
        int curr = 0;

        // Check for all characters
        // less then current character
        for (int j = 0; j < val; j++) {
            curr = Math.Max(curr, dp[j]);
        }

        // Include current character
        curr++;

        // Update length of longest
        // increasing subsequence
        lis = Math.Max(lis, curr);

        // Updating LIS for current character
        dp[val] = Math.Max(dp[val], curr);
    }

    // Return the length of LIS
    return lis;
}

// Driver Code
public static void Main()
{
    string s = "fdryutiaghfse";
    Console.Write(lisOtimised(s));
}
}

// This code is contributed by SURENDRA_GAANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find length of longest
// increasing subsequence in a string
function lisOtimised( s)
{
    // Stores at every i-th index, the
    // length of the longest increasing
    // subsequence ending with character i
    let dp = new Array(30).fill(0);

    // Size of string
    let N = s.length;

    // Stores the length of LIS
    let lis = Number.MIN_VALUE;

    // Iterate over each
    // character of the string
    for (let i = 0; i < N; i++) {

        // Store position of the
        // current character
        let val = s.charCodeAt(i) - 'a'.charCodeAt(0);

        // Stores the length of LIS
        // ending with current character
        let curr = 0;

        // Check for all characters
        // less then current character
        for (let j = 0; j < val; j++) {
            curr = Math.max(curr, dp[j]);
        }

        // Include current character
        curr++;

        // Update length of longest
        // increasing subsequence
        lis = Math.max(lis, curr);

        // Updating LIS for current character
        dp[val] = Math.max(dp[val], curr);
    }

    // Return the length of LIS
    return lis;
}

// Driver Code

 let s = "fdryutiaghfse";
 document.write(lisOtimised(s));

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)