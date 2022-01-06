# 计算可以由另一个给定字符串构造的字符串的出现次数

> 原文:[https://www . geeksforgeeks . org/count-一个可以从另一个给定字符串构造的字符串出现次数/](https://www.geeksforgeeks.org/count-occurrences-of-a-string-that-can-be-constructed-from-another-given-string/)

给定两个字符串 **str1** 和 **str2** ，其中 **str1** 为父字符串。任务是找出可以用 **str1** 的字母构成的字符串编号 **str2** 。
**注意:**所有字母均为小写，每个字符只能使用一次。
**举例:**

```
Input: str1 = "geeksforgeeks", str2 = "geeks"
Output: 2

Input: str1 = "geekgoinggeeky", str2 = "geeks"
Output: 0
```

**方法:**在 hash2 中存储 str2 的字符频率，在 hash1 中对 str1 也是如此。现在，找出所有 I 的 hash1[i]/hash2[i]的最小值，其中 hash2[i] > 0。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count
int findCount(string str1, string str2)
{
    int len = str1.size();
    int len2 = str2.size();
    int ans = INT_MAX;

    // Initialize hash for both strings
    int hash1[26] = { 0 }, hash2[26] = { 0 };

    // hash the frequency of letters of str1
    for (int i = 0; i < len; i++)
        hash1[str1[i] - 'a']++;

    // hash the frequency of letters of str2
    for (int i = 0; i < len2; i++)
        hash2[str2[i] - 'a']++;

    // Find the count of str2 constructed from str1
    for (int i = 0; i < 26; i++)
        if (hash2[i])
            ans = min(ans, hash1[i] / hash2[i]);

    // Return answer
    return ans;
}

// Driver code
int main()
{
    string str1 = "geeksclassesatnoida";
    string str2 = "sea";
    cout << findCount(str1, str2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{
    // Function to find the count
    static int findCount(String str1, String str2)
    {
        int len = str1.length();
        int len2 = str2.length();
        int ans = Integer.MAX_VALUE;

        // Initialize hash for both strings
        int [] hash1 = new int[26];
        int [] hash2 = new int[26];

        // hash the frequency of letters of str1
        for (int i = 0; i < len; i++)
            hash1[(int)(str1.charAt(i) - 'a')]++;

        // hash the frequency of letters of str2
        for (int i = 0; i < len2; i++)
            hash2[(int)(str2.charAt(i) - 'a')]++;

        // Find the count of str2 constructed from str1
        for (int i = 0; i < 26; i++)
            if (hash2[i] != 0)
                ans = Math.min(ans, hash1[i] / hash2[i]);

        // Return answer
        return ans;
    }

    // Driver code
    public static void main(String []args)
    {
        String str1 = "geeksclassesatnoida";
        String str2 = "sea";
        System.out.println(findCount(str1, str2));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

import sys

# Function to find the count
def findCount(str1, str2):

    len1 = len(str1)
    len2 = len(str2)
    ans = sys.maxsize

    # Initialize hash for both strings
    hash1 = [0] * 26
    hash2 = [0] * 26

    # hash the frequency of letters of str1
    for i in range(0, len1):
        hash1[ord(str1[i]) - 97] = hash1[ord(str1[i]) - 97] + 1

    # hash the frequency of letters of str2
    for i in range(0, len2):
        hash2[ord(str2[i]) - 97] = hash2[ord(str2[i]) - 97] + 1

    # Find the count of str2 constructed from str1
    for i in range (0, 26):
        if (hash2[i] != 0):
            ans = min(ans, hash1[i] // hash2[i])

    # Return answer
    return ans

# Driver code
str1 = "geeksclassesatnoida"
str2 = "sea"
print(findCount(str1, str2))

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    // Function to find the count
    static int findCount(string str1, string str2)
    {
        int len = str1.Length;
        int len2 = str2.Length;
        int ans = Int32.MaxValue;

        // Initialize hash for both strings
        int [] hash1 = new int[26];
        int [] hash2 = new int[26];

        // hash the frequency of letters of str1
        for (int i = 0; i < len; i++)
            hash1[str1[i] - 'a']++;

        // hash the frequency of letters of str2
        for (int i = 0; i < len2; i++)
            hash2[str2[i] - 'a']++;

        // Find the count of str2 constructed from str1
        for (int i = 0; i < 26; i++)
            if (hash2[i] != 0)
                ans = Math.Min(ans, hash1[i] / hash2[i]);

        // Return answer
        return ans;
    }

    // Driver code
    public static void Main()
    {
        string str1 = "geeksclassesatnoida";
        string str2 = "sea";
        Console.WriteLine(findCount(str1, str2));
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find the count
function findCount($str1, $str2)
{
    $len = strlen($str1) ;
    $len2 = strlen($str1);
    $ans = PHP_INT_MAX;

    // Initialize hash for both strings
    $hash1 = array_fill(0, 26, 0) ;
    $hash2 = array_fill(0, 26, 0);

    // hash the frequency of letters of str1
    for ($i = 0; $i < $len; $i++)
        $hash1[ord($str1[$i]) - ord('a')]++;

    // hash the frequency of letters of str2
    for ($i = 0; $i < $len2; $i++)
        $hash2[ord($str2[$i]) - ord('a')]++;

    // Find the count of str2 constructed from str1
    for ($i = 0; $i < 26; $i++)
        if ($hash2[$i])
            $ans = min($ans, $hash1[$i] / $hash2[$i]);

    // Return answer
    return $ans;
}

    // Driver code
    $str1 = "geeksclassesatnoida";
    $str2 = "sea";
    echo findCount($str1, $str2);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
      // JavaScript implementation of the above approach

      // Function to find the count
      function findCount(str1, str2) {
        var len = str1.length;
        var len2 = str2.length;
        //MAX Integer Value
        var ans = 21474836473;

        // Initialize hash for both strings
        var hash1 = new Array(26).fill(0);
        var hash2 = new Array(26).fill(0);

        // hash the frequency of letters of str1
        for (var i = 0; i < len; i++)
          hash1[str1[i].charCodeAt(0) - "a".charCodeAt(0)]++;

        // hash the frequency of letters of str2
        for (var i = 0; i < len2; i++)
          hash2[str2[i].charCodeAt(0) - "a".charCodeAt(0)]++;

        // Find the count of str2 constructed from str1
        for (var i = 0; i < 26; i++)
          if (hash2[i]) ans = Math.min(ans, hash1[i] / hash2[i]);

        // Return answer
        return ans;
      }

      // Driver code
      var str1 = "geeksclassesatnoida";
      var str2 = "sea";
      document.write(findCount(str1, str2));
    </script>
```

**Output:** 

```
3
```