# 计数三个不重叠的子串，它们在连接时形成回文

> 原文:[https://www . geeksforgeeks . org/三个不重叠的子字符串的计数串联形成回文/](https://www.geeksforgeeks.org/count-of-three-non-overlapping-sub-strings-which-on-concatenation-forms-a-palindrome/)

给定一个字符串 **str** ，任务是计算一个回文子字符串由字符串 **str** 的三个子字符串 **x** 、 **y** 和 **z** 串联而成的方式数，使得它们都不重叠，即子字符串 **y** 出现在子字符串 **x** 之后，子字符串 **z** 出现在子字符串**之后
**例:**** 

> **输入:** str = "abca"
> **输出:** 2
> 两个有效对为(“a”、“b”、“a”)和(“a”、“c”、“a”)
> T7】输入: str = "abba"
> **输出:** 5

**方法:**找出三个不重叠的子串的所有可能的对，并且对于每一对，检查由它们的连接生成的串是否是回文。如果是，则增加计数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// s[i...j] + s[k...l] + s[p...q]
// is a palindrome
bool isPalin(int i, int j, int k, int l,
             int p, int q, string s)
{
    int start = i, end = q;
    while (start < end) {
        if (s[start] != s[end])
            return false;

        start++;
        if (start == j + 1)
            start = k;
        end--;
        if (end == p - 1)
            end = l;
    }
    return true;
}

// Function to return the count
// of valid sub-strings
int countSubStr(string s)
{
    // To store the count of
    // required sub-strings
    int count = 0;
    int n = s.size();

    // For choosing the first sub-string
    for (int i = 0; i < n - 2; i++) {
        for (int j = i; j < n - 2; j++) {

            // For choosing the second sub-string
            for (int k = j + 1; k < n - 1; k++) {
                for (int l = k; l < n - 1; l++) {

                    // For choosing the third sub-string
                    for (int p = l + 1; p < n; p++) {
                        for (int q = p; q < n; q++) {

                            // Check if the concatenation
                            // is a palindrome
                            if (isPalin(i, j, k, l, p, q, s)) {
                                count++;
                            }
                        }
                    }
                }
            }
        }
    }

    return count;
}

// Driver code
int main()
{
    string s = "abca";

    cout << countSubStr(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns true if
    // s[i...j] + s[k...l] + s[p...q]
    // is a palindrome
    static boolean isPalin(int i, int j, int k, int l,
                            int p, int q, String s)
    {
        int start = i, end = q;
        while (start < end) {
            if (s.charAt(start) != s.charAt(end))
            {
                return false;
            }

            start++;
            if (start == j + 1)
            {
                start = k;
            }
            end--;
            if (end == p - 1)
            {
                end = l;
            }
        }
        return true;
    }

    // Function to return the count
    // of valid sub-strings
    static int countSubStr(String s)
    {
        // To store the count of
        // required sub-strings
        int count = 0;
        int n = s.length();

        // For choosing the first sub-string
        for (int i = 0; i < n - 2; i++)
        {
            for (int j = i; j < n - 2; j++)
            {

                // For choosing the second sub-string
                for (int k = j + 1; k < n - 1; k++)
                {
                    for (int l = k; l < n - 1; l++)
                    {

                        // For choosing the third sub-string
                        for (int p = l + 1; p < n; p++)
                        {
                            for (int q = p; q < n; q++)
                            {

                                // Check if the concatenation
                                // is a palindrome
                                if (isPalin(i, j, k, l, p, q, s))
                                {
                                    count++;
                                }
                            }
                        }
                    }
                }
            }
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "abca";

        System.out.println(countSubStr(s));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if
# s[i...j] + s[k...l] + s[p...q]
# is a palindrome
def isPalin(i, j, k, l, p, q, s) :

    start = i; end = q;
    while (start < end) :

        if (s[start] != s[end]) :
            return False;

        start += 1;
        if (start == j + 1) :
            start = k;

        end -= 1;
        if (end == p - 1) :
            end = l;

    return True;

# Function to return the count
# of valid sub-strings
def countSubStr(s) :

    # To store the count of
    # required sub-strings
    count = 0;
    n = len(s);

    # For choosing the first sub-string
    for i in range(n-2) :

        for j in range(i, n-2) :

            # For choosing the second sub-string
            for k in range(j + 1, n-1) :
                for l in range(k, n-1) :

                    # For choosing the third sub-string
                    for p in range(l + 1, n) :
                        for q in range(p, n) :

                            # Check if the concatenation
                            # is a palindrome
                            if (isPalin(i, j, k, l, p, q, s)) :
                                count += 1;

    return count;

# Driver code
if __name__ == "__main__" :

    s = "abca";

    print(countSubStr(s));

# This course is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

    // Function that returns true if
    // s[i...j] + s[k...l] + s[p...q]
    // is a palindrome
    static bool isPalin(int i, int j, int k, int l,
                        int p, int q, String s)
    {
        int start = i, end = q;
        while (start < end)
        {
            if (s[start] != s[end])
            {
                return false;
            }

            start++;
            if (start == j + 1)
            {
                start = k;
            }
            end--;
            if (end == p - 1)
            {
                end = l;
            }
        }
        return true;
    }

    // Function to return the count
    // of valid sub-strings
    static int countSubStr(String s)
    {
        // To store the count of
        // required sub-strings
        int count = 0;
        int n = s.Length;

        // For choosing the first sub-string
        for (int i = 0; i < n - 2; i++)
        {
            for (int j = i; j < n - 2; j++)
            {

                // For choosing the second sub-string
                for (int k = j + 1; k < n - 1; k++)
                {
                    for (int l = k; l < n - 1; l++)
                    {

                        // For choosing the third sub-string
                        for (int p = l + 1; p < n; p++)
                        {
                            for (int q = p; q < n; q++)
                            {

                                // Check if the concatenation
                                // is a palindrome
                                if (isPalin(i, j, k, l, p, q, s))
                                {
                                    count++;
                                }
                            }
                        }
                    }
                }
            }
        }

        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "abca";

        Console.WriteLine(countSubStr(s));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if
// s[i...j] + s[k...l] + s[p...q]
// is a palindrome
function isPalin(i, j, k, l, p, q, s)
{
    var start = i, end = q;
    while (start < end) {
        if (s[start] != s[end])
            return false;

        start++;
        if (start == j + 1)
            start = k;
        end--;
        if (end == p - 1)
            end = l;
    }
    return true;
}

// Function to return the count
// of valid sub-strings
function countSubStr(s)
{
    // To store the count of
    // required sub-strings
    var count = 0;
    var n = s.length;

    // For choosing the first sub-string
    for (var i = 0; i < n - 2; i++) {
        for (var j = i; j < n - 2; j++) {

            // For choosing the second sub-string
            for (var k = j + 1; k < n - 1; k++) {
                for (var l = k; l < n - 1; l++) {

                    // For choosing the third sub-string
                    for (var p = l + 1; p < n; p++) {
                        for (var q = p; q < n; q++) {

                            // Check if the concatenation
                            // is a palindrome
                            if (isPalin(i, j, k, l, p, q, s)) {
                                count++;
                            }
                        }
                    }
                }
            }
        }
    }

    return count;
}

// Driver code
var s = "abca";
document.write( countSubStr(s));

// This code is contributed by famously.
</script>
```

**Output:** 

```
2
```