# 使用动态编程给定字符串的不同回文子字符串

> 原文:[https://www . geesforgeks . org/distinct-回文-给定字符串的子字符串-使用动态编程/](https://www.geeksforgeeks.org/distinct-palindromic-sub-strings-of-the-given-string-using-dynamic-programming/)

给定一个由小写字母组成的字符串 **str** ，任务是找到给定字符串的所有不同的回文子字符串。

**示例:**

> **输入:**str = " abaaa "
> T3】输出: 5
> 回文子串为“a”、“aa”、“aaa”、“aba”和“b”
> 
> **输入:**str = " ABCD "
> T3】输出: 4

**方法:**这个问题的解决方案已经讨论过了[这里](https://www.geeksforgeeks.org/find-number-distinct-palindromic-sub-strings-given-string/)使用[的 Manacher 算法](https://www.geeksforgeeks.org/manachers-algorithm-linear-time-longest-palindromic-substring-part-1/)。不过我们也可以用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来解决。
创建一个数组 **dp[][]** 其中 **dp[i][j]** 设置为 **1** 如果 **str[i…j]** 是回文否则 **0** 。生成数组后，将所有回文子串存储在[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，以获得不同子串的计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of distinct palindromic sub-strings
// of the given string s
int palindromeSubStrs(string s)
{

    // To store the positions of
    // palindromic sub-strings
    int dp[s.size()][s.size()];
    int st, end, i, j, len;

    // Map to store the sub-strings
    map<string, bool> m;
    for (i = 0; i < s.size(); i++) {

        // Sub-strings of length 1 are palindromes
        dp[i][i] = 1;

        // Store continuous palindromic sub-strings
        m[string(s.begin() + i, s.begin() + i + 1)] = 1;
    }

    // Store palindromes of size 2
    for (i = 0; i < s.size() - 1; i++) {
        if (s[i] == s[i + 1]) {
            dp[i][i + 1] = 1;
            m[string(s.begin() + i, s.begin() + i + 2)] = 1;
        }

        // If str[i...(i+1)] is not a palindromic
        // then set dp[i][i + 1] = 0
        else {
            dp[i][i + 1] = 0;
        }
    }

    // Find palindromic sub-strings of length>=3
    for (len = 3; len <= s.size(); len++) {
        for (st = 0; st <= s.size() - len; st++) {

            // End of palindromic substring
            end = st + len - 1;

            // If s[start] == s[end] and
            // dp[start+1][end-1] is already palindrome
            // then s[start....end] is also a palindrome
            if (s[st] == s[end] && dp[st + 1][end - 1]) {

                // Set dp[start][end] = 1
                dp[st][end] = 1;
                m[string(s.begin() + st, s.begin() + end + 1)] = 1;
            }

            // Not a palindrome
            else
                dp[st][end] = 0;
        }
    }

    // Return the count of distinct palindromes
    return m.size();
}

// Driver code
int main()
{
    string s = "abaaa";
    cout << palindromeSubStrs(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashMap;

class GFG
{

    // Function to return the count
    // of distinct palindromic sub-strings
    // of the given string s
    static int palindromeSubStrs(String s)
    {

        // To store the positions of
        // palindromic sub-strings
        int[][] dp = new int[s.length()][s.length()];
        int st, end, i, len;

        // Map to store the sub-strings
        HashMap<String,
                Boolean> m = new HashMap<>();

        for (i = 0; i < s.length(); i++)
        {

            // Sub-strings of length 1 are palindromes
            dp[i][i] = 1;

            // Store continuous palindromic sub-strings
            m.put(s.substring(i, i + 1), true);
        }

        // Store palindromes of size 2
        for (i = 0; i < s.length() - 1; i++)
        {
            if (s.charAt(i) == s.charAt(i + 1))
            {
                dp[i][i + 1] = 1;
                m.put(s.substring(i, i + 2), true);
            }

            // If str[i...(i+1)] is not a palindromic
            // then set dp[i][i + 1] = 0
            else
                dp[i][i + 1] = 0;
        }

        // Find palindromic sub-strings of length>=3
        for (len = 3; len <= s.length(); len++)
        {
            for (st = 0; st <= s.length() - len; st++)
            {

                // End of palindromic substring
                end = st + len - 1;

                // If s[start] == s[end] and
                // dp[start+1][end-1] is already palindrome
                // then s[start....end] is also a palindrome
                if (s.charAt(st) == s.charAt(end) &&
                    dp[st + 1][end - 1] == 1)
                {

                    // Set dp[start][end] = 1
                    dp[st][end] = 1;
                    m.put(s.substring(st, end + 1), true);
                }

                // Not a palindrome
                else
                    dp[st][end] = 0;
            }
        }

        // Return the count of distinct palindromes
        return m.size();
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "abaaa";
        System.out.println(palindromeSubStrs(s));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# import numpy lib as np
import numpy as np;

# Function to return the count
# of distinct palindromic sub-strings
# of the given string s
def palindromeSubStrs(s) :

    # To store the positions of
    # palindromic sub-strings
    dp = np.zeros((len(s),len(s)));

    # Map to store the sub-strings
    m = {};

    for i in range(len(s)) :

        # Sub-strings of length 1 are palindromes
        dp[i][i] = 1;

        # Store continuous palindromic sub-strings
        m[s[i: i + 1]] = 1;

    # Store palindromes of size 2
    for i in range(len(s)- 1) :
        if (s[i] == s[i + 1]) :
            dp[i][i + 1] = 1;
            m[ s[i : i + 2]] = 1;

        # If str[i...(i+1)] is not a palindromic
        # then set dp[i][i + 1] = 0
        else :
            dp[i][i + 1] = 0;

    # Find palindromic sub-strings of length>=3
    for length in range(3,len(s) + 1) :
        for st in range(len(s) - length + 1) :

            # End of palindromic substring
            end = st + length - 1;

            # If s[start] == s[end] and
            # dp[start+1][end-1] is already palindrome
            # then s[start....end] is also a palindrome
            if (s[st] == s[end] and dp[st + 1][end - 1]) :

                # Set dp[start][end] = 1
                dp[st][end] = 1;
                m[s[st : end + 1]] = 1;

            # Not a palindrome
            else :
                dp[st][end] = 0;

    # Return the count of distinct palindromes
    return len(m);

# Driver code
if __name__ == "__main__" :

    s = "abaaa";
    print(palindromeSubStrs(s));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the count
    // of distinct palindromic sub-strings
    // of the given string s
    static int palindromeSubStrs(String s)
    {

        // To store the positions of
        // palindromic sub-strings
        int[,] dp = new int[s.Length, s.Length];
        int st, end, i, len;

        // Map to store the sub-strings
        Dictionary<String,
                Boolean> m = new Dictionary<String,
                Boolean>();

        for (i = 0; i < s.Length; i++)
        {

            // Sub-strings of length 1 are palindromes
            dp[i,i] = 1;

            // Store continuous palindromic sub-strings
            if(!m.ContainsKey(s.Substring(i, 1)))
                m.Add(s.Substring(i, 1), true);
        }

        // Store palindromes of size 2
        for (i = 0; i < s.Length - 1; i++)
        {
            if (s[i] == s[i + 1])
            {
                dp[i, i + 1] = 1;
                if(!m.ContainsKey(s.Substring(i, 2)))
                    m.Add(s.Substring(i, 2), true);
            }

            // If str[i...(i+1)] is not a palindromic
            // then set dp[i,i + 1] = 0
            else
                dp[i, i + 1] = 0;
        }

        // Find palindromic sub-strings of length>=3
        for (len = 3; len <= s.Length; len++)
        {
            for (st = 0; st <= s.Length - len; st++)
            {

                // End of palindromic substring
                end = st + len - 1;

                // If s[start] == s[end] and
                // dp[start+1,end-1] is already palindrome
                // then s[start....end] is also a palindrome
                if (s[st] == s[end] &&
                    dp[st + 1, end - 1] == 1)
                {

                    // Set dp[start,end] = 1
                    dp[st, end] = 1;
                    m.Add(s.Substring(st, end + 1-st), true);
                }

                // Not a palindrome
                else
                    dp[st, end] = 0;
            }
        }

        // Return the count of distinct palindromes
        return m.Count;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String s = "abaaa";
        Console.WriteLine(palindromeSubStrs(s));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of distinct palindromic sub-strings
// of the given string s
function palindromeSubStrs(s)
{

    // To store the positions of
    // palindromic sub-strings
    let dp = new Array(s.length);
    for(let i = 0; i < dp.length; i++)
    {
        dp[i] = new Array(2);
    }

    for(let i = 0; i < dp.length; i++)
    {
        for(let j = 0; j < dp.length; j++)
        {
            dp[i][j] = 0;
        }
    }
    let st, end, i, len;

    // Map to store the sub-strings
    let m = new Map();

    for(i = 0; i < s.length; i++)
    {

        // Sub-strings of length 1 are palindromes
        dp[i][i] = 1;

        // Store continuous palindromic sub-strings
        m.set(s.substr(i, i + 1), true);
    }

    // Store palindromes of size 2
    for(i = 0; i < s.length - 1; i++)
    {
        if (s[i] == s[i + 1])
        {
            dp[i][i + 1] = 1;
            m.set(s.substr(i, i + 2), true);
        }

        // If str[i...(i+1)] is not a palindromic
        // then set dp[i][i + 1] = 0
        else
            dp[i][i + 1] = 0;
    }

    // Find palindromic sub-strings of length>=3
    for(len = 3; len <= s.length; len++)
    {
        for(st = 0; st <= s.length - len; st++)
        {

            // End of palindromic substring
            end = st + len - 1;

            // If s[start] == s[end] and
            // dp[start+1][end-1] is already palindrome
            // then s[start....end] is also a palindrome
            if (s[st] == s[end] &&
                dp[st + 1][end - 1] == 1)
            {

                // Set dp[start][end] = 1
                dp[st][end] = 1;
                m.set(s.substr(st, end + 1), true);
            }

            // Not a palindrome
            else
                dp[st][end] = 0;
        }
    }

    // Return the count of distinct palindromes
    return m.size;
}

// Driver Code
let s = "abaaa";
document.write(palindromeSubStrs(s));

// This code is contributed by code_hunt

</script>
```

**Output:** 

```
5
```