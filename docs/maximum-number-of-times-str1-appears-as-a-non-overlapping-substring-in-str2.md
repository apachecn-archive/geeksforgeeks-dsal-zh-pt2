# 【str1 在 str2 中作为非重叠子串出现的最大次数

> 原文:[https://www . geesforgeks . org/最大次数-str 1-作为非重叠子串出现在-str2/](https://www.geeksforgeeks.org/maximum-number-of-times-str1-appears-as-a-non-overlapping-substring-in-str2/)

给定两个字符串 **str1** 和 **str2** ，任务是在重新排列 **str2**
**的字符后，将 **str1** 在 **str2** 中出现的最大次数作为不重叠的子串找到【示例:**

> **输入:** str1 =“极客”，str 2 =“gskeffekees”
> T3】输出:2
> str =**极客**为**极客**
> **输入:**str 1 =“aa”，str 2 =“AAAA”
> **输出:** 2

**方法:**想法是存储两个字符串的字符频率并进行比较。

*   如果有一个字符在第一个字符串中的频率大于它在第二个字符串中的频率，那么答案总是 0，因为字符串 **str1** 永远不会出现在 **str2** 中。
*   存储两个字符串的字符频率后，在 **str1** 和 **str2** 的非零字符频率之间执行整数除法。最小值就是答案。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 26;

// Function to return the maximum number
// of times str1 can appear as a
// non-overlapping substring in str2
int maxSubStr(string str1, int len1, string str2, int len2)
{

    // str1 cannot never be substring of str2
    if (len1 > len2)
        return 0;

    // Store the frequency of the characters of str1
    int freq1[MAX] = { 0 };
    for (int i = 0; i < len1; i++)
        freq1[str1[i] - 'a']++;

    // Store the frequency of the characters of str2
    int freq2[MAX] = { 0 };
    for (int i = 0; i < len2; i++)
        freq2[str2[i] - 'a']++;

    // To store the required count of substrings
    int minPoss = INT_MAX;

    for (int i = 0; i < MAX; i++) {

        // Current character doesn't appear in str1
        if (freq1[i] == 0)
            continue;

        // Frequency of the current character in str1
        // is greater than its frequency in str2
        if (freq1[i] > freq2[i])
            return 0;

        // Update the count of possible substrings
        minPoss = min(minPoss, freq2[i] / freq1[i]);
    }
    return minPoss;
}

// Driver code
int main()
{
    string str1 = "geeks", str2 = "gskefrgoekees";
    int len1 = str1.length();
    int len2 = str2.length();

    cout << maxSubStr(str1, len1, str2, len2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    final static int MAX = 26;

    // Function to return the maximum number
    // of times str1 can appear as a
    // non-overlapping substring in str2
    static int maxSubStr(char []str1, int len1,
                         char []str2, int len2)
    {

        // str1 cannot never be substring of str2
        if (len1 > len2)
            return 0;

        // Store the frequency of the characters of str1
        int freq1[] = new int[MAX];

        for (int i = 0; i < len1; i++)
            freq1[i] = 0;

        for (int i = 0; i < len1; i++)
            freq1[str1[i] - 'a']++;

        // Store the frequency of the characters of str2
        int freq2[] = new int[MAX];

        for (int i = 0; i < len2; i++)
            freq2[i] = 0;

        for (int i = 0; i < len2; i++)
            freq2[str2[i] - 'a']++;

        // To store the required count of substrings
        int minPoss = Integer.MAX_VALUE;

        for (int i = 0; i < MAX; i++)
        {

            // Current character doesn't appear in str1
            if (freq1[i] == 0)
                continue;

            // Frequency of the current character in str1
            // is greater than its frequency in str2
            if (freq1[i] > freq2[i])
                return 0;

            // Update the count of possible substrings
            minPoss = Math.min(minPoss, freq2[i] / freq1[i]);
        }
        return minPoss;
    }

    // Driver code
    public static void main (String[] args)
    {
        String str1 = "geeks", str2 = "gskefrgoekees";
        int len1 = str1.length();
        int len2 = str2.length();

        System.out.println(maxSubStr(str1.toCharArray(), len1,
                                     str2.toCharArray(), len2));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys
MAX = 26;

# Function to return the maximum number
# of times str1 can appear as a
# non-overlapping substring bin str2
def maxSubStr(str1, len1, str2, len2):

    # str1 cannot never be
    # substring of str2
    if (len1 > len2):
        return 0;

    # Store the frequency of
    # the characters of str1
    freq1 = [0] * MAX;
    for i in range(len1):
        freq1[ord(str1[i]) -
              ord('a')] += 1;

    # Store the frequency of
    # the characters of str2
    freq2 = [0] * MAX;
    for i in range(len2):
        freq2[ord(str2[i]) -
              ord('a')] += 1;

    # To store the required count
    # of substrings
    minPoss = sys.maxsize;

    for i in range(MAX):

        # Current character doesn't appear
        # in str1
        if (freq1[i] == 0):
            continue;

        # Frequency of the current character
        # in str1 is greater than its
        # frequency in str2
        if (freq1[i] > freq2[i]):
            return 0;

        # Update the count of possible substrings
        minPoss = min(minPoss, freq2[i] /
                               freq1[i]);
    return int(minPoss);

# Driver code
str1 = "geeks"; str2 = "gskefrgoekees";
len1 = len(str1);
len2 = len(str2);

print(maxSubStr(str1, len1, str2, len2));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    readonly static int MAX = 26;

    // Function to return the maximum number
    // of times str1 can appear as a
    // non-overlapping substring in str2
    static int maxSubStr(char []str1, int len1,
                         char []str2, int len2)
    {

        // str1 cannot never be substring of str2
        if (len1 > len2)
            return 0;

        // Store the frequency of the characters of str1
        int []freq1 = new int[MAX];

        for (int i = 0; i < len1; i++)
            freq1[i] = 0;

        for (int i = 0; i < len1; i++)
            freq1[str1[i] - 'a']++;

        // Store the frequency of the characters of str2
        int []freq2 = new int[MAX];

        for (int i = 0; i < len2; i++)
            freq2[i] = 0;

        for (int i = 0; i < len2; i++)
            freq2[str2[i] - 'a']++;

        // To store the required count of substrings
        int minPoss = int.MaxValue;

        for (int i = 0; i < MAX; i++)
        {

            // Current character doesn't appear in str1
            if (freq1[i] == 0)
                continue;

            // Frequency of the current character in str1
            // is greater than its frequency in str2
            if (freq1[i] > freq2[i])
                return 0;

            // Update the count of possible substrings
            minPoss = Math.Min(minPoss, freq2[i] / freq1[i]);
        }
        return minPoss;
    }

    // Driver code
    public static void Main (String[] args)
    {
        String str1 = "geeks", str2 = "gskefrgoekees";
        int len1 = str1.Length;
        int len2 = str2.Length;

        Console.WriteLine(maxSubStr(str1.ToCharArray(), len1,
                                    str2.ToCharArray(), len2));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
const MAX = 26;

// Function to return the maximum number
// of times str1 can appear as a
// non-overlapping substring in str2
function maxSubStr(str1, len1, str2, len2)
{

    // str1 cannot never be substring of str2
    if (len1 > len2)
        return 0;

    // Store the frequency of the characters of str1
    let freq1 = new Array(MAX).fill(0);
    for (let i = 0; i < len1; i++)
        freq1[str1.charCodeAt(i) - 'a'.charCodeAt(0)]++;

    // Store the frequency of the characters of str2
    let freq2 = new Array(MAX).fill(0);
    for (let i = 0; i < len2; i++)
        freq2[str2.charCodeAt(i) - 'a'.charCodeAt(0)]++;

    // To store the required count of substrings
    let minPoss = Number.MAX_SAFE_INTEGER;

    for (let i = 0; i < MAX; i++) {

        // Current character doesn't appear in str1
        if (freq1[i] == 0)
            continue;

        // Frequency of the current character in str1
        // is greater than its frequency in str2
        if (freq1[i] > freq2[i])
            return 0;

        // Update the count of possible substrings
        minPoss = Math.min(minPoss, Math.floor(freq2[i] / freq1[i]));
    }
    return minPoss;
}

// Driver code

let str1 = "geeks", str2 = "gskefrgoekees";
let len1 = str1.length;
let len2 = str2.length;

document.write(maxSubStr(str1, len1, str2, len2));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(max(M，N))，其中 M 和 N 分别是给定字符串 str1 和 str2 的长度。