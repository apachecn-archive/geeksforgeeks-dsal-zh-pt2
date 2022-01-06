# 相邻字符不同的最长子序列

> 原文:[https://www . geeksforgeeks . org/不同相邻字符的最长子序列/](https://www.geeksforgeeks.org/longest-subsequence-with-different-adjacent-characters/)

给定弦**弦**。任务是找到**字符串**中最长的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，使得子序列中所有相邻的字符都不同。

**示例:**

> **输入:** str =【亚贝巴】
> **输出:** 5
> **说明:**
> “亚贝巴”是满足条件的子序列
> 
> **输入:** str = "xxxxy"
> **输出:** 2
> **说明:**
> “xy”是满足条件的子序列

**方法 1:** [**【贪婪逼近】**](https://www.geeksforgeeks.org/greedy-algorithms/)
可以观察到，给定相邻字符不同的给定字符串的最长子序列，选择与之前选择的字符不相似的第一个字符。
思路是在遍历字符串的同时跟踪之前拾取的字符，如果当前字符与之前的字符不同，那么就对当前字符进行计数，找到最长的子序列。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest Subsequence
// with different adjacent character
int longestSubsequence(string s)
{
    // Length of the string s
    int n = s.length();
    int answer = 0;

    // Previously picked character
    char prev = '-';

    for (int i = 0; i < n; i++) {
        // If the current character is
        // different from the previous
        // then include this character
        // and update previous character
        if (prev != s[i]) {
            prev = s[i];
            answer++;
        }
    }

    return answer;
}

// Driver Code
int main()
{
    string str = "ababa";

    // Function call
    cout << longestSubsequence(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the longest subsequence
// with different adjacent character
static int longestSubsequence(String s)
{

    // Length of the String s
    int n = s.length();
    int answer = 0;

    // Previously picked character
    char prev = '-';

    for(int i = 0; i < n; i++)
    {

       // If the current character is
       // different from the previous
       // then include this character
       // and update previous character
       if (prev != s.charAt(i))
       {
           prev = s.charAt(i);
           answer++;
       }
    }

    return answer;
}

// Driver Code
public static void main(String[] args)
{
    String str = "ababa";

    // Function call
    System.out.print(longestSubsequence(str));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the longest Subsequence
# with different adjacent character
def longestSubsequence(s):

    # Length of the string s
    n = len(s);
    answer = 0;

    # Previously picked character
    prev = '-';

    for i in range(0, n):

        # If the current character is
        # different from the previous
        # then include this character
        # and update previous character
        if (prev != s[i]):
            prev = s[i];
            answer += 1;

    return answer;

# Driver Code
str = "ababa";

# Function call
print(longestSubsequence(str));

# This code is contributed by Code_Mech
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the longest subsequence
// with different adjacent character
static int longestSubsequence(String s)
{

    // Length of the String s
    int n = s.Length;
    int answer = 0;

    // Previously picked character
    char prev = '-';

    for(int i = 0; i < n; i++)
    {

       // If the current character is
       // different from the previous
       // then include this character
       // and update previous character
       if (prev != s[i])
       {
           prev = s[i];
           answer++;
       }
    }
    return answer;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "ababa";

    // Function call
    Console.Write(longestSubsequence(str));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the longest Subsequence
// with different adjacent character
function longestSubsequence(s)
{
    // Length of the string s
    var n = s.length;
    var answer = 0;

    // Previously picked character
    var prev = '-';

    for (var i = 0; i < n; i++) {
        // If the current character is
        // different from the previous
        // then include this character
        // and update previous character
        if (prev != s[i]) {
            prev = s[i];
            answer++;
        }
    }

    return answer;
}

// Driver Code
var str = "ababa";
// Function call
document.write( longestSubsequence(str));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N)，其中 N 为给定字符串的长度。

**方法二:** [**动态规划**](https://www.geeksforgeeks.org/dynamic-programming/)

1.  对于给定字符串中的每个字符，请执行以下操作:
    *   为结果子序列选择字符串中的当前字符，并对剩余的字符串进行循环，以便为结果子序列找到下一个可能的字符。
    *   省略当前字符，并对剩余的字符串重复，以便为结果子序列找到下一个可能的字符。
2.  上述递归调用中的最大值将是具有不同相邻元素的最长子序列。
3.  递归关系由下式给出:

```
Let dp[pos][prev] be the length of longest subsequence 
till index pos such that alphabet prev was picked previously.a dp[pos][prev] = max(1 + function(pos+1, s[pos] - 'a' + 1, s), 
                    function(pos+1, prev, s));
```

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// dp table
int dp[100005][27];

// A recursive function to find the
// update the dp[][] table
int calculate(int pos, int prev, string& s)
{

    // If we reach end of the string
    if (pos == s.length()) {
        return 0;
    }

    // If subproblem has been computed
    if (dp[pos][prev] != -1)
        return dp[pos][prev];

    // Initialise variable to find the
    // maximum length
    int val = 0;

    // Choose the current character
    if (s[pos] - 'a' + 1 != prev) {
        val = max(val,
                  1 + calculate(pos + 1,
                                s[pos] - 'a' + 1,
                                s));
    }

    // Omit the current character
    val = max(val, calculate(pos + 1, prev, s));

    // Return the store answer to the
    // current subproblem
    return dp[pos][prev] = val;
}

// Function to find the longest Subsequence
// with different adjacent character
int longestSubsequence(string s)
{

    // Length of the string s
    int n = s.length();

    // Initialise the memoisation table
    memset(dp, -1, sizeof(dp));

    // Return the final ans after every
    // recursive call
    return calculate(0, 0, s);
}

// Driver Code
int main()
{
    string str = "ababa";

    // Function call
    cout << longestSubsequence(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// dp table
static int dp[][] = new int[100005][27];

// A recursive function to find the
// update the dp[][] table
static int calculate(int pos, int prev, String s)
{

    // If we reach end of the String
    if (pos == s.length())
    {
        return 0;
    }

    // If subproblem has been computed
    if (dp[pos][prev] != -1)
        return dp[pos][prev];

    // Initialise variable to find the
    // maximum length
    int val = 0;

    // Choose the current character
    if (s.charAt(pos) - 'a' + 1 != prev)
    {
        val = Math.max(val, 1 + calculate(pos + 1,
                                s.charAt(pos) - 'a' + 1,
                                s));
    }

    // Omit the current character
    val = Math.max(val, calculate(pos + 1, prev, s));

    // Return the store answer to the
    // current subproblem
    return dp[pos][prev] = val;
}

// Function to find the longest Subsequence
// with different adjacent character
static int longestSubsequence(String s)
{

    // Length of the String s
    int n = s.length();

    // Initialise the memoisation table
    for(int i = 0; i < 100005; i++)
    {
        for (int j = 0; j < 27; j++)
        {
            dp[i][j] = -1;
        }
    }

    // Return the final ans after every
    // recursive call
    return calculate(0, 0, s);
}

// Driver Code
public static void main(String[] args)
{
    String str = "ababa";

    // Function call
    System.out.print(longestSubsequence(str));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for the above approach
# dp table
dp = [[-1 for i in range(27)] for j in range(100005)];

# A recursive function to find the
# update the dp table
def calculate(pos, prev, s):

    # If we reach end of the String
    if (pos == len(s)):
        return 0;

    # If subproblem has been computed
    if (dp[pos][prev] != -1):
        return dp[pos][prev];

    # Initialise variable to find the
    # maximum length
    val = 0;

    # Choose the current character
    if (ord(s[pos]) - ord('a') + 1 != prev):
        val = max(val, 1 + calculate(pos + 1,
                                     ord(s[pos]) -
                                     ord('a') + 1, s));

    # Omit the current character
    val = max(val, calculate(pos + 1, prev, s));

    # Return the store answer to
    # the current subproblem
    dp[pos][prev] = val;
    return dp[pos][prev];

# Function to find the longest Subsequence
# with different adjacent character
def longestSubsequence(s):

    # Length of the String s
    n = len(s);

    # Return the final ans after every
    # recursive call
    return calculate(0, 0, s);

# Driver Code
if __name__ == '__main__':
    str = "ababa";

    # Function call
    print(longestSubsequence(str));

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

// dp table
static int [,]dp = new int[100005,27];

// A recursive function to find the
// update the [,]dp table
static int calculate(int pos, int prev, String s)
{

    // If we reach end of the String
    if (pos == s.Length)
    {
        return 0;
    }

    // If subproblem has been computed
    if (dp[pos,prev] != -1)
        return dp[pos,prev];

    // Initialise variable to
    // find the maximum length
    int val = 0;

    // Choose the current character
    if (s[pos] - 'a' + 1 != prev)
    {
        val = Math.Max(val, 1 +
                       calculate(pos + 1,
                                 s[pos] - 'a' + 1,
                                 s));
    }

    // Omit the current character
    val = Math.Max(val, calculate(pos + 1, prev, s));

    // Return the store answer to the
    // current subproblem
    return dp[pos,prev] = val;
}

// Function to find the longest Subsequence
// with different adjacent character
static int longestSubsequence(String s)
{

    // Length of the String s
    int n = s.Length;

    // Initialise the memoisation table
    for(int i = 0; i < 100005; i++)
    {
        for (int j = 0; j < 27; j++)
        {
            dp[i,j] = -1;
        }
    }

    // Return the readonly ans after every
    // recursive call
    return calculate(0, 0, s);
}

// Driver Code
public static void Main(String[] args)
{
    String str = "ababa";

    // Function call
    Console.Write(longestSubsequence(str));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // dp table
    let dp = new Array(100005);

    // A recursive function to find the
    // update the dp[][] table
    function calculate(pos, prev, s)
    {

        // If we reach end of the String
        if (pos == s.length)
        {
            return 0;
        }

        // If subproblem has been computed
        if (dp[pos][prev] != -1)
            return dp[pos][prev];

        // Initialise variable to find the
        // maximum length
        let val = 0;

        // Choose the current character
        if (s[pos].charCodeAt() - 'a'.charCodeAt() + 1 != prev)
        {
            val = Math.max(val, 1 + calculate(pos + 1,
                  s[pos].charCodeAt() - 'a'.charCodeAt() + 1,
                                    s));
        }

        // Omit the current character
        val = Math.max(val, calculate(pos + 1, prev, s));

        // Return the store answer to the
        // current subproblem
        dp[pos][prev] = val;
        return dp[pos][prev];
    }

    // Function to find the longest Subsequence
    // with different adjacent character
    function longestSubsequence(s)
    {

        // Length of the String s
        let n = s.length;

        // Initialise the memoisation table
        for(let i = 0; i < 100005; i++)
        {
            dp[i] = new Array(27);
            for (let j = 0; j < 27; j++)
            {
                dp[i][j] = -1;
            }
        }

        // Return the final ans after every
        // recursive call
        return calculate(0, 0, s);
    }

    let str = "ababa";

    // Function call
    document.write(longestSubsequence(str));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N)，其中 N 为给定字符串的长度。
**辅助空间:** O(26*N)其中 N 是给定字符串的长度。