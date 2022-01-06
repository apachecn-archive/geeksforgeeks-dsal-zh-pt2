# 由相同字符组成的长度为 K 的子串的最大数量

> 原文:[https://www . geesforgeks . org/由相同字符组成的长度为 k 的子字符串的最大计数/](https://www.geeksforgeeks.org/maximum-count-of-sub-strings-of-length-k-consisting-of-same-characters/)

给定一个字符串**字符串**和一个整数 **k** 。任务是统计由相同字符组成的长度为 **k** 的子串的出现次数。长度为 k 的子串可以有多个，选择出现次数最多的一个作为**串**的子串(不重叠)。
**举例:**

> **输入:**str = " aacaabaa "，k = 2
> **输出:**3
> “aa”和“bb”是长度为 2 的唯一由相同字符组成的子字符串。
> “bb”作为 str 的子串只出现一次，而“aa”出现三次(这就是答案)
> **输入:** str = "abab "，k = 2
> **输出:** 0

**方法:**迭代从**‘a’**到**‘z’**的所有字符，并计算仅由当前字符组成的长度为 **k** 的字符串作为**字符串**的子字符串出现的次数。最后打印这些计数的最大值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of the required sub-strings
int maxSubStrings(string s, int k)
{
    int maxSubStr = 0, n = s.size();

    // Iterate over all characters
    for (int c = 0; c < 26; c++) {
        char ch = 'a' + c;

        // Count with current character
        int curr = 0;
        for (int i = 0; i <= n - k; i++) {
            if (s[i] != ch)
                continue;
            int cnt = 0;
            while (i < n && s[i] == ch && cnt != k) {
                i++;
                cnt++;
            }
            i--;

            // If the substring has a length k
            // then increment count with current character
            if (cnt == k)
                curr++;
        }

        // Update max count
        maxSubStr = max(maxSubStr, curr);
    }
    return maxSubStr;
}

// Driver Code
int main()
{
    string s = "aaacaabbaa";
    int k = 2;
    cout << maxSubStrings(s, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

// Function to return the count
// of the required sub-strings
static int maxSubStrings(String s, int k)
{
    int maxSubStr = 0, n = s.length();

    // Iterate over all characters
    for (int c = 0; c < 26; c++)
    {
        char ch = (char)((int)'a' + c);

        // Count with current character
        int curr = 0;
        for (int i = 0; i <= n - k; i++)
        {
            if (s.charAt(i) != ch)
                continue;
            int cnt = 0;
            while (i < n && s.charAt(i) == ch &&
                                        cnt != k)
            {
                i++;
                cnt++;
            }
            i--;

            // If the substring has a length
            //  k then increment count with
            // current character
            if (cnt == k)
                curr++;
        }

        // Update max count
        maxSubStr = Math.max(maxSubStr, curr);
    }
    return maxSubStr;
}

// Driver Code
public static void main(String []args)
{
    String s = "aaacaabbaa";
    int k = 2;
    System.out.println(maxSubStrings(s, k));
}
}

// This code is contributed by
// tufan_gupta2000
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the count
# of the required sub-strings
def maxSubStrings(s, k):
    maxSubStr = 0
    n = len(s)

    # Iterate over all characters
    for c in range(27):
        ch = chr(ord('a') + c)

        # Count with current character
        curr = 0
        for i in range(n - k):
            if (s[i] != ch):
                continue
            cnt = 0
            while (i < n and s[i] == ch and
                                   cnt != k):
                i += 1
                cnt += 1

            i -= 1

            # If the substring has a length k then
            # increment count with current character
            if (cnt == k):
                curr += 1

        # Update max count
        maxSubStr = max(maxSubStr, curr)

    return maxSubStr

# Driver Code
if __name__ == '__main__':
    s = "aaacaabbaa"
    k = 2
    print(maxSubStrings(s, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count
    // of the required sub-strings
    static int maxSubStrings(String s, int k)
    {
        int maxSubStr = 0, n = s.Length;

        // Iterate over all characters
        for (int c = 0; c < 26; c++)
        {
            char ch = (char)((int)'a' + c);

            // Count with current character
            int curr = 0;
            for (int i = 0; i <= n - k; i++)
            {
                if (s[i] != ch)
                    continue;
                int cnt = 0;
                while (i < n && s[i] == ch &&
                                cnt != k)
                {
                    i++;
                    cnt++;
                }
                i--;

                // If the substring has a length
                // k then increment count with
                // current character
                if (cnt == k)
                    curr++;
            }

            // Update max count
            maxSubStr = Math.Max(maxSubStr, curr);
        }
        return maxSubStr;
    }

    // Driver Code
    public static void Main()
    {
        string s = "aaacaabbaa";
        int k = 2;
        Console.WriteLine(maxSubStrings(s, k));
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function to return the count
      // of the required sub-strings
      function maxSubStrings(s, k) {
        var maxSubStr = 0,
          n = s.length;

        // Iterate over all characters
        for (var c = 0; c < 26; c++) {
          var ch = String.fromCharCode("a".charCodeAt(0) + c);

          // Count with current character
          var curr = 0;
          for (var i = 0; i <= n - k; i++) {
            if (s[i] !== ch) continue;
            var cnt = 0;
            while (i < n && s[i] === ch && cnt !== k) {
              i++;
              cnt++;
            }
            i--;

            // If the substring has a length
            // k then increment count with
            // current character
            if (cnt === k) curr++;
          }

          // Update max count
          maxSubStr = Math.max(maxSubStr, curr);
        }
        return maxSubStr;
      }

      // Driver Code
      var s = "aaacaabbaa";
      var k = 2;
      document.write(maxSubStrings(s, k));
    </script>
```

**Output:** 

```
3
```

**时间复杂度:** O(n)，其中 n 为字符串的长度。