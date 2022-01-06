# 最长的偶数长度回文子序列的长度，没有两个相邻字符相同

> 原文:[https://www . geesforgeks . org/最长回文长度-偶数长度子序列-没有两个相邻字符-相同/](https://www.geeksforgeeks.org/length-of-longest-palindromic-subsequence-of-even-length-with-no-two-adjacent-characters-same/)

给定一个字符串 **str** ，任务是找出最长的偶数长度回文子序列的长度，除中间字符外，没有两个相邻字符相同。

**示例:**

> **输入:**str = " abarcdba "
> **输出:** 6
> **说明:**
> abcba 是必输字符串，除中间字符外，没有两个连续字符相同。因此长度是 6
> 
> **输入:**str = " ABCD "
> T3】输出: 0

**方法:**思路是利用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)形成递归解并存储子问题的值。可以按照以下步骤计算结果:

*   形成一个递归函数，该函数将采用一个字符串和一个字符作为子序列的起始字符。
*   如果字符串的第一个和最后一个字符与给定的字符匹配，则移除第一个和最后一个字符，并使用除给定字符之外的从“a”到“z”的所有字符值调用函数，因为相邻的字符不能相同并找到最大长度。
*   如果字符串的第一个和最后一个字符与给定字符不匹配，那么找到字符串中给定字符的第一个和最后一个索引，分别说 **i** 、 **j** 。从 **i** 到 **j** 取子串，用子串和给定的字符调用函数。
*   最后，在一个[无序映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)中记忆这些值，如果用相同的参数再次调用该函数，则使用它。

以下是上述方法的实施:

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

#define lli long long int

// To store the values of subproblems
unordered_map<string, lli> dp;

// Function to find the
// Longest Palindromic subsequence of even
// length with no two adjacent characters same
lli solve(string s, char c)
{
    // Base cases
    // If the string length is 1 return 0
    if (s.length() == 1)
        return 0;

    // If the string length is 2
    if (s.length() == 2) {

        // Check if the characters match
        if (s[0] == s[1] && s[0] == c)
            return 1;
        else
            return 0;
    }

    // If the value with given parameters is
    // previously calculated
    if (dp[s + " " + c])
        return dp[s + " " + c];

    lli ans = 0;

    // If the first and last character of the
    // string matches with the given character
    if (s[0] == s[s.length() - 1] && s[0] == c) 
    {
        // Remove the first and last character
        // and call the function for all characters
        for (char c1 = 'a'; c1 <= 'z'; c1++)
            if (c1 != c)
                ans = max(
                    ans,
                    1 + solve(s.substr(1, 
                                       s.length() - 2),
                                       c1));
    }

    // If it does not match
    else {

        // Then find the first and last index of
        // given character in the given string
        for (lli i = 0; i < s.length(); i++) 
        {
            if (s[i] == c) 
            {
                for (lli j = s.length() - 1; j > i; j--)
                    if (s[j] == c) 
                    {
                        if (j == i)
                            break;

                        // Take the substring from i
                        // to j and call the function
                        // with substring
                        // and the given character
                        ans = solve(s.substr(i, j - i + 1),
                                    c);
                        break;
                    }

                break;
            }
        }
    }

    // Store the answer for future use
    dp[s + " " + c] = ans;
    return dp[s + " " + c];
}

// Driver code
int main()
{
    string s = "abscrcdba";

    lli ma = 0;

    // Check for all starting characters
    for (char c1 = 'a'; c1 <= 'z'; c1++)
        ma = max(ma, solve(s, c1) * 2);
    cout << ma << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG {

    // To store the values of subproblems
    static Map<String, Integer> dp = new HashMap<>();

    // Function to find the
    // Longest Palindromic subsequence of even
    // length with no two adjacent characters same
    static Integer solve(char[] s, char c)
    {

        // Base cases
        // If the String length is 1 return 0
        if (s.length == 1)
            return 0;

        // If the String length is 2
        if (s.length == 2) {

            // Check if the characters match
            if (s[0] == s[1] && s[0] == c)
                return 1;
            else
                return 0;
        }

        // If the value with given parameters is
        // previously calculated
        if (dp.containsKey(String.valueOf(s) + " " + c))
            return dp.get(String.valueOf(s) + " " + c);
        Integer ans = 0;

        // If the first and last character of the
        // String matches with the given character
        if (s[0] == s[s.length - 1] && s[0] == c)
        {
            // Remove the first and last character
            // and call the function for all characters
            for (char c1 = 'a'; c1 <= 'z'; c1++)

                if (c1 != c)
                    ans = Math.max(
                        ans,
                        1 + solve(Arrays.copyOfRange(
                                        s, 1, 
                                        s.length - 1),
                                        c1));
        }

        // If it does not match
        else {

            // Then find the first and last index of
            // given character in the given String
            for (Integer i = 0; i < s.length; i++) 
            {
                if (s[i] == c) 
                {
                    for (Integer j = s.length - 1; 
                         j > i;
                         j--)
                        if (s[j] == c) 
                        {
                            if (j == i)
                                break;

                            // Take the subString from i
                            // to j and call the function
                            // with subString
                            // and the given character
                            ans = solve(Arrays.copyOfRange(
                                            s, i, 
                                            j + 1),
                                            c);
                            break;
                        }

                    break;
                }
            }
        }

        // Store the answer for future use
        dp.put(String.valueOf(s) + " " + c, ans);
        return dp.get(String.valueOf(s) + " " + c);
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "abscrcdba";

        Integer ma = 0;

        // Check for all starting characters
        for (char c1 = 'a'; c1 <= 'z'; c1++)
            ma = Math.max(ma,
                          solve(s.toCharArray(), c1) * 2);
        System.out.print(ma + "\n");
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# To store the values of subproblems
dp = {}

# Function to find the
# Longest Palindromic subsequence of even
# length with no two adjacent characters same

def solve(s, c):

    # Base cases
    # If the string length is 1 return 0
    if (len(s) == 1):
        return 0

    # If the string length is 2
    if (len(s) == 2):

        # Check if the characters match
        if (s[0] == s[1] and s[0] == c):
            return 1
        else:
            return 0

    # If the value with given parameters is
    # previously calculated
    if (s + " " + c) in dp:
        return dp[s + " " + c]

    ans = 0

    # If the first and last character of the
    # string matches with the given character
    if (s[0] == s[len(s) - 1] and s[0] == c):

        # Remove the first and last character
        # and call the function for all characters
        for c1 in range(97, 123):

            if (chr(c1) != c):
                ans = max(ans, 1 + solve(
                    s[1: len(s) - 1], chr(c1)))

    # If it does not match
    else:

        # Then find the first and last index of
        # given character in the given string
        for i in range(len(s)):

            if (s[i] == c):
                for j in range(len(s) - 1, i, -1):
                    if (s[j] == c):
                        if (j == i):
                            break

                        # Take the substring from i
                        # to j and call the function
                        # with substring
                        # and the given character
                        ans = solve(s[i: j - i + 2], c)
                        break

                break

    # Store the answer for future use
    dp[s + " " + c] = ans

    return dp[s + " " + c]

# Driver code
if __name__ == "__main__":

    s = "abscrcdba"

    ma = 0

    # Check for all starting characters
    for c1 in range(97, 123):
        ma = max(ma, solve(s, chr(c1)) * 2)

    print(ma)

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG {

    // To store the values of subproblems
    static Dictionary<string, int> dp
        = new Dictionary<string, int>();

    // Function to find the
    // Longest Palindromic subsequence of even
    // length with no two adjacent characters same
    static int solve(char[] s, char c)
    {

        // Base cases
        // If the String length is 1 return 0
        if (s.Length == 1)
            return 0;

        // If the String length is 2
        if (s.Length == 2) {

            // Check if the characters match
            if (s[0] == s[1] && s[0] == c)
                return 1;
            else
                return 0;
        }

        // If the value with given parameters is
        // previously calculated
        if (dp.ContainsKey(new string(s) + " " + c))
            return dp[new string(s) + " " + c];

        int ans = 0;

        // If the first and last character of the
        // String matches with the given character
        if (s[0] == s[s.Length - 1] && s[0] == c) 
        {

            // Remove the first and last character
            // and call the function for all characters
            for (char c1 = 'a'; c1 <= 'z'; c1++)

                if (c1 != c) {
                    int len = s.Length - 2;
                    char[] tmp = new char[len];

                    Array.Copy(s, 1, tmp, 0, len);
                    ans = Math.Max(ans, 1 + solve(tmp, c1));
                }
        }

        // If it does not match
        else {

            // Then find the first and last index of
            // given character in the given String
            for (int i = 0; i < s.Length; i++) 
            {
                if (s[i] == c) 
                {
                    for (int j = s.Length - 1; j > i; j--)
                        if (s[j] == c) 
                        {
                            if (j == i)
                                break;

                            // Take the subString from i
                            // to j and call the function
                            // with subString and the
                            // given character
                            int len = j + 1 - i;
                            char[] tmp = new char[len];
                            Array.Copy(s, i, tmp, 0, len);
                            ans = solve(tmp, c);
                            break;
                        }
                    break;
                }
            }
        }

        // Store the answer for future use
        dp[new string(s) + " " + c] = ans;
        return dp[new string(s) + " " + c];
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string s = "abscrcdba";

        int ma = 0;

        // Check for all starting characters
        for (char c1 = 'a'; c1 <= 'z'; c1++)
            ma = Math.Max(ma,
                          solve(s.ToCharArray(), c1) * 2);

        Console.Write(ma + "\n");
    }
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// To store the values of subproblems
var dp = new Map();

// Function to find the
// Longest Palindromic subsequence of even
// length with no two adjacent characters same
function solve(s, c)
{
    // Base cases
    // If the string length is 1 return 0
    if (s.length == 1)
        return 0;

    // If the string length is 2
    if (s.length == 2) {

        // Check if the characters match
        if (s[0] == s[1] && s[0] == c)
            return 1;
        else
            return 0;
    }

    // If the value with given parameters is
    // previously calculated
    if (dp.has(s + " " + c))
        return dp.get(s + " " + c);

    var ans = 0;

    // If the first and last character of the
    // string matches with the given character
    if (s[0] == s[s.length - 1] && s[0] == c) 
    {
        // Remove the first and last character
        // and call the function for all characters
        for (var c1 = 'a'.charCodeAt(0); c1 <= 'z'.charCodeAt(0); c1++)
            if (String.fromCharCode(c1) != c)
                ans = Math.max(
                    ans,
                    1 + solve(s.substring(1, 
                                       s.length - 1),
                                       String.fromCharCode(c1)));
    }

    // If it does not match
    else {

        // Then find the first and last index of
        // given character in the given string
        for (var i = 0; i < s.length; i++) 
        {
            if (s[i] == c) 
            {
                for (var j = s.length - 1; j > i; j--)
                    if (s[j] == c) 
                    {
                        if (j == i)
                            break;

                        // Take the substring from i
                        // to j and call the function
                        // with substring
                        // and the given character
                        ans = solve(s.substring(i, j + 1),
                                    c);
                        break;
                    }

                break;
            }
        }
    }

    // Store the answer for future use
    dp.set(s + " " + c, ans);
    return ans;
}

// Driver code
var s = "abscrcdba";
var ma = 0;
// Check for all starting characters
for (var c1 = 'a'.charCodeAt(0); c1 <= 'z'.charCodeAt(0); c1++)
    ma = Math.max(ma, solve(s, String.fromCharCode(c1)) * 2);
document.write(ma);

</script>
```

**Output**

```
6
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N)

**相关文章:** [最长回文子序列](https://www.geeksforgeeks.org/longest-palindromic-subsequence-dp-12/)