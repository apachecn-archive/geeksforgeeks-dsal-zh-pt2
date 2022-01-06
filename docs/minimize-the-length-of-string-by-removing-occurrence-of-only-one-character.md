# 通过删除仅出现的一个字符来最小化字符串的长度

> 原文:[https://www . geesforgeks . org/通过删除仅出现一个字符来最小化字符串长度/](https://www.geeksforgeeks.org/minimize-the-length-of-string-by-removing-occurrence-of-only-one-character/)

给定一个只包含小写字母的字符串 *str* ，任务是在执行以下操作后最小化字符串的长度:

*   删除该字符串中任何一个字符的所有出现。

示例:

```
Input: str = "abccderccwq"
Output: 7
character 'c' will be deleted since it has maximum occurrence.

Input: str = "dddded"
Output: 1
character 'd' will be deleted
```

**进场:**

1.  保持数组中每个字符的频率。
2.  找到频率最高的字符。
3.  最后，用该字符的频率减去原始字符串的长度，得到所需的答案。

以下是上述方法的实现:

## C++

```
// C++ program to minimize the length of string by
// removing occurrence of only one character
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum length
int minimumLength(string s)
{
    int maxOcc = 0, n = s.length();
    int arr[26] = {0};

    // Count the frequency of each alphabet
    for (int i = 0; i < n; i++)
        arr[s[i] - 'a']++;

    // Find the alphabets with maximum frequency
    for (int i = 0; i < 26; i++)
        if (arr[i] > maxOcc)
            maxOcc = arr[i];

    // Subtract the frequency of character
    // from length of string
    return (n - maxOcc);
}

// Driver Code
int main()
{
    string str = "afddewqd";
    cout << minimumLength(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to minimize the length of string
// by removing occurrence of only one character
import java.io.*;

class GFG {

// Function to find the minimum length
static int minimumLength(String s)
{
    int maxOcc = 0, n = s.length();
    int arr[] = new int[26];

    // Count the frequency of each alphabet
    for (int i = 0; i < n; i++)
        arr[s.charAt(i) - 'a']++;

    // Find the alphabets with maximum frequency
    for (int i = 0; i < 26; i++)
        if (arr[i] > maxOcc)
            maxOcc = arr[i];

    // Subtract the frequency of character
    // from length of string
    return (n - maxOcc);
}

// Driver Code

    public static void main (String[] args) {
    String str = "afddewqd";
    System.out.println( minimumLength(str));
    }
}

//This code is contributed by chandan_jnu...
```

## 蟒蛇 3

```
# Python 3 program to minimize the length of string
# by removing occurrence of only one character

# Function to find the minimum length
def minimumLength(s) :

    maxOcc = 0
    n = len(s)
    arr = [0]*26

    # Count the frequency of each alphabet
    for i in range(n) :
        arr[ord(s[i]) -ord('a')] += 1

    # Find the alphabets with maximum frequency
    for i in range(26) :
        if arr[i] > maxOcc :
            maxOcc = arr[i]

    # Subtract the frequency of character
    # from length of string
    return n - maxOcc

# Driver Code
if __name__ == "__main__" :

    str = "afddewqd"
    print(minimumLength(str))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to minimize the
// length of string by removing
// occurrence of only one character
using System;

class GFG
{
    // Function to find the minimum length
    static int minimumLength(String s)
    {
        int maxOcc = 0, n = s.Length;
        int []arr = new int[26];

        // Count the frequency of each alphabet
        for (int i = 0; i < n; i++)
            arr[s[i] - 'a']++;

        // Find the alphabets with
        // maximum frequency
        for (int i = 0; i < 26; i++)
            if (arr[i] > maxOcc)
                maxOcc = arr[i];

        // Subtract the frequency of character
        // from length of string
        return (n - maxOcc);
    }

    // Driver Code
    public static void Main (String[] args)
    {
        String str = "afddewqd";
        Console.WriteLine( minimumLength(str));
    }
}

// This code is contributed by
// PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to minimize the length of string by
// removing occurrence of only one character

// Function to find the minimum length
function minimumLength(s)
{
    var maxOcc = 0, n = s.length;
    var arr = Array(26).fill(0);

    // Count the frequency of each alphabet
    for (var i = 0; i < n; i++)
        arr[s[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

    // Find the alphabets with maximum frequency
    for (var i = 0; i < 26; i++)
        if (arr[i] > maxOcc)
            maxOcc = arr[i];

    // Subtract the frequency of character
    // from length of string
    return (n - maxOcc);
}

// Driver Code
var str = "afddewqd";
document.write( minimumLength(str));

</script>
```

**Output:** 

```
5
```