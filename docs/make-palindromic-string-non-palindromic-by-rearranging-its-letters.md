# 通过重新排列回文串的字母

使回文串成为非回文串

> 原文:[https://www . geesforgeks . org/make-回文-字符串-非回文-通过重新排列其字母/](https://www.geeksforgeeks.org/make-palindromic-string-non-palindromic-by-rearranging-its-letters/)

给定字符串**包含小写字母(a–z)的字符串**。任务是在重新排列一些字符后打印字符串，使字符串成为非回文字符串。如果无法使字符串成为非回文，则打印 **-1** 。
**例:**

> **输入:** str = "abba"
> **输出:** aabb
> **输入:** str = "zzz"
> **输出:** -1

**方法:**如果字符串中的所有字符都相同，那么无论您如何重新排列字符，字符串都将保持不变，并将被回文。现在，如果存在非回文排列，重新排列字符的最佳方式是对字符串进行排序，该字符串将形成相同字符的连续段，并且永远不会被回文。为了减少对字符串排序所需的时间，我们可以存储所有 26 个字符的频率，并以排序的方式打印它们。
以下是上述办法的实施情况:

## C++

```
// CPP Program to rearrange letters of string
// to find a non-palindromic string if it exists
#include <bits/stdc++.h>
using namespace std;

// Function to print the non-palindromic string
// if it exists, otherwise prints -1
void findNonPalinString(string s)
{
    int freq[26] = { 0 }, flag = 0;

    for (int i = 0; i < s.size(); i++) {

        // If all characters are not
        // same, set flag to 1
        if (s[i] != s[0])
            flag = 1;

        // Update frequency of the current character
        freq[s[i] - 'a']++;
    }

    // If all characters are same
    if (!flag)
        cout << "-1";
    else {

        // Print characters in sorted manner
        for (int i = 0; i < 26; i++)
            for (int j = 0; j < freq[i]; j++)
                cout << char('a' + i);
    }
}

// Driver Code
int main()
{
    string s = "abba";

    findNonPalinString(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to rearrange letters of string
// to find a non-palindromic string if it exists
class GfG
{

// Function to print the non-palindromic string
// if it exists, otherwise prints -1
static void findNonPalinString(char s[])
{
    int freq[] = new int[26];
    int flag = 0;

    for (int i = 0; i < s.length; i++)
    {

        // If all characters are not
        // same, set flag to 1
        if (s[i] != s[0])
            flag = 1;

        // Update frequency of
        // the current character
        freq[s[i] - 'a']++;
    }

    // If all characters are same
    if (flag == 0)
        System.out.println("-1");
    else
    {

        // Print characters in sorted manner
        for (int i = 0; i < 26; i++)
            for (int j = 0; j < freq[i]; j++)
                System.out.print((char)('a' + i));
    }
}

// Driver Code
public static void main(String[] args)
{
    String s = "abba";

    findNonPalinString(s.toCharArray());
}
}

// This code is contributed by
// Prerna Saini.
```

## 蟒蛇 3

```
# Python3 Program to rearrange letters of string
# to find a non-palindromic string if it exists

# Function to print the non-palindromic string
# if it exists, otherwise prints -1
def findNonPalinString(s):

    freq = [0] * (26)
    flag = 0

    for i in range(0, len(s)):

        # If all characters are not same,
        # set flag to 1
        if s[i] != s[0]:
            flag = 1

        # Update frequency of the current
        # character
        freq[ord(s[i]) - ord('a')] += 1

    # If all characters are same
    if not flag:
        print("-1")

    else:

        # Print characters in sorted manner
        for i in range(0, 26):
            for j in range(0, freq[i]):
                print(chr(ord('a') + i),
                               end = "")

# Driver Code
if __name__ == "__main__":

    s = "abba"
    findNonPalinString(s)

# This code is contributed by
# Rituraj Jain
```

## C#

```
// C# Program to rearrange letters
// of string to find a non-palindromic
// string if it exists
using System;

class GfG
{

    // Function to print the
    // non-palindromic string
    // if it exists, otherwise
    // prints -1
    static void findNonPalinString(char []s)
    {
        int []freq = new int[26];
        int flag = 0;

        for (int i = 0; i < s.Length; i++)
        {

            // If all characters are not
            // same, set flag to 1
            if (s[i] != s[0])
                flag = 1;

            // Update frequency of
            // the current character
            freq[s[i] - 'a']++;
        }

        // If all characters are same
        if (flag == 0)
            Console.WriteLine("-1");
        else
        {

            // Print characters in sorted manner
            for (int i = 0; i < 26; i++)
                for (int j = 0; j < freq[i]; j++)
                        Console.Write((char)('a' + i));
        }
    }

    // Driver Code
    public static void Main()
    {
        string s = "abba";

        findNonPalinString(s.ToCharArray());
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>

// JavaScript Program to rearrange letters of string
// to find a non-palindromic string if it exists

// Function to print the non-palindromic string
// if it exists, otherwise prints -1
function findNonPalinString(s)
{
    var freq = Array.from({length: 26}, (_, i) => 0);
    var flag = 0;

    for (var i = 0; i < s.length; i++)
    {

        // If all characters are not
        // same, set flag to 1
        if (s[i] != s[0])
            flag = 1;

        // Update frequency of
        // the current character
        freq[s[i].charCodeAt(0) -
        'a'.charCodeAt(0)]++;
    }

    // If all characters are same
    if (flag == 0)
        document.write("-1");
    else
    {

        // Print characters in sorted manner
        for (var i = 0; i < 26; i++)
            for (var j = 0; j < freq[i]; j++)
                document.write(String.fromCharCode
                ('a'.charCodeAt(0) + i));
    }
}

// Driver Code
var s = "abba";

findNonPalinString(s.split(''));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
aabb
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)