# 第二个字符串可以由第一个字符串的字符构成的次数

> 原文:[https://www . geeksforgeeks . org/第一个字符串的字符可以构成第二个字符串的次数/](https://www.geeksforgeeks.org/count-of-times-second-string-can-be-formed-from-the-characters-of-first-string/)

给定两个字符串 **str** 和 **patt** ，任务是找出使用 **str** 的字符可以形成的 **patt** 的次数。
**举例:**

> **输入:** str = "geeksforgeeks "，patt = "geeks"
> **输出:**2
> “geeks”最多可以由
> 的“geeksforgeeks”的人物制作两次。
> **输入:**str = " abbca "，patt = "aabc"
> **输出:** 1

**方法:**统计 **str** 和 **patt** 所有字符的出现频率，并分别存储在数组 **strFreq[]** 和 **pattFreq[]** 中。现在出现在**模式**中的任何字符 **ch** 最多可以用**strFreq[ch]/pattFreq[ch]**个字，这个值在**模式**的所有字符中的最小值就是要求的答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 26;

// Function to update the freq[] array
// to store the frequencies of
// all the characters of str
void updateFreq(string str, int freq[])
{
    int len = str.length();

    // Update the frequency of the characters
    for (int i = 0; i < len; i++) {
        freq[str[i] - 'a']++;
    }
}

// Function to return the maximum count
// of times patt can be formed
// using the characters of str
int maxCount(string str, string patt)
{

    // To store the frequencies of
    // all the characters of str
    int strFreq[MAX] = { 0 };
    updateFreq(str, strFreq);

    // To store the frequencies of
    // all the characters of patt
    int pattFreq[MAX] = { 0 };
    updateFreq(patt, pattFreq);

    // To store the result
    int ans = INT_MAX;

    // For every character
    for (int i = 0; i < MAX; i++) {

        // If the current character
        // doesn't appear in patt
        if (pattFreq[i] == 0)
            continue;

        // Update the result
        ans = min(ans, strFreq[i] / pattFreq[i]);
    }

    return ans;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    string patt = "geeks";

    cout << maxCount(str, patt);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

static int MAX = 26;

// Function to update the freq[] array
// to store the frequencies of
// all the characters of str
static void updateFreq(String str, int freq[])
{
    int len = str.length();

    // Update the frequency of the characters
    for (int i = 0; i < len; i++)
    {
        freq[str.charAt(i) - 'a']++;
    }
}

// Function to return the maximum count
// of times patt can be formed
// using the characters of str
static int maxCount(String str, String patt)
{

    // To store the frequencies of
    // all the characters of str
    int []strFreq = new int[MAX];
    updateFreq(str, strFreq);

    // To store the frequencies of
    // all the characters of patt
    int []pattFreq = new int[MAX];
    updateFreq(patt, pattFreq);

    // To store the result
    int ans = Integer.MAX_VALUE;

    // For every character
    for (int i = 0; i < MAX; i++)
    {

        // If the current character
        // doesn't appear in patt
        if (pattFreq[i] == 0)
            continue;

        // Update the result
        ans = Math.min(ans, strFreq[i] / pattFreq[i]);
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    String patt = "geeks";

    System.out.print(maxCount(str, patt));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 26

# Function to update the freq[] array
# to store the frequencies of
# all the characters of strr
def updateFreq(strr, freq):
    lenn = len(strr)

    # Update the frequency of the characters
    for i in range(lenn):
        freq[ord(strr[i]) - ord('a')] += 1

# Function to return the maximum count
# of times patt can be formed
# using the characters of strr
def maxCount(strr, patt):

    # To store the frequencies of
    # all the characters of strr
    strrFreq = [0 for i in range(MAX)]
    updateFreq(strr, strrFreq)

    # To store the frequencies of
    # all the characters of patt
    pattFreq = [0 for i in range(MAX)]
    updateFreq(patt, pattFreq)

    # To store the result
    ans = 10**9

    # For every character
    for i in range(MAX):

        # If the current character
        # doesn't appear in patt
        if (pattFreq[i] == 0):
            continue

        # Update the result
        ans = min(ans, strrFreq[i] // pattFreq[i])

    return ans

# Driver code
strr = "geeksforgeeks"
patt = "geeks"

print(maxCount(strr, patt))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int MAX = 26;

// Function to update the []freq array
// to store the frequencies of
// all the characters of str
static void updateFreq(String str, int []freq)
{
    int len = str.Length;

    // Update the frequency of the characters
    for (int i = 0; i < len; i++)
    {
        freq[str[i] - 'a']++;
    }
}

// Function to return the maximum count
// of times patt can be formed
// using the characters of str
static int maxCount(String str, String patt)
{

    // To store the frequencies of
    // all the characters of str
    int []strFreq = new int[MAX];
    updateFreq(str, strFreq);

    // To store the frequencies of
    // all the characters of patt
    int []pattFreq = new int[MAX];
    updateFreq(patt, pattFreq);

    // To store the result
    int ans = int.MaxValue;

    // For every character
    for (int i = 0; i < MAX; i++)
    {

        // If the current character
        // doesn't appear in patt
        if (pattFreq[i] == 0)
            continue;

        // Update the result
        ans = Math.Min(ans, strFreq[i] / pattFreq[i]);
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    String patt = "geeks";

    Console.Write(maxCount(str, patt));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach

      const MAX = 26;

      // Function to update the freq[] array
      // to store the frequencies of
      // all the characters of str
      function updateFreq(str, freq) {
        var len = str.length;

        // Update the frequency of the characters
        for (var i = 0; i < len; i++) {
          freq[str[i].charCodeAt(0) - "a".charCodeAt(0)]++;
        }
      }

      // Function to return the maximum count
      // of times patt can be formed
      // using the characters of str
      function maxCount(str, patt) {
        // To store the frequencies of
        // all the characters of str
        var strFreq = new Array(MAX).fill(0);
        updateFreq(str, strFreq);

        // To store the frequencies of
        // all the characters of patt
        var pattFreq = new Array(MAX).fill(0);
        updateFreq(patt, pattFreq);

        // To store the result
        var ans = 21474836473;

        // For every character
        for (var i = 0; i < MAX; i++) {
          // If the current character
          // doesn't appear in patt
          if (pattFreq[i] == 0) continue;

          // Update the result
          ans = Math.min(ans, strFreq[i] / pattFreq[i]);
        }

        return ans;
      }

      // Driver code
      var str = "geeksforgeeks";
      var patt = "geeks";

      document.write(maxCount(str, patt));
    </script>
```

**Output:** 

```
2
```