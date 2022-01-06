# 不包含任何元音的最长子串的长度

> 原文:[https://www . geesforgeks . org/不包含任何元音的最长子串长度/](https://www.geeksforgeeks.org/length-of-the-longest-substring-that-does-not-contain-any-vowel/)

给定一个由 **N** 个小写字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找出不包含任何元音的最长[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)的长度。

**示例:**

> **输入:** S = "geeksforgeeks"
> **输出:** 3
> 子串“ksf”是不包含任何元音的最长子串。这个子串的长度是 3。
> 
> **输入:**S = " ceebaceeffo "
> T3】输出: 2

**天真法:**解决给定问题最简单的方法是[生成给定字符串的所有子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/) **S** 并打印不包含任何元音的最大长度子串的长度。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)进行优化。
按照以下步骤解决问题:

*   初始化两个变量，说**计数**和 **res** 为 **0** ，存储无元音的[串](https://www.geeksforgeeks.org/string-data-structure/)的长度，以及分别找到的结果[子串](https://www.geeksforgeeks.org/substring-in-cpp/)的最大长度。
*   [使用变量 **i** 遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，并执行以下步骤:
    *   [如果当前字符 **S[i]** 是元音](https://www.geeksforgeeks.org/program-find-character-vowel-consonant/)，那么将**计数**的值更新为 **0** 。否则，将**计数**的值增加 **1** 。
    *   将 **res** 的值更新为 **res** 和 **count** 的[最大值](https://www.geeksforgeeks.org/stdmax-in-cpp/)。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the
// character is a vowel or not
bool vowel(char ch)
{
    if (ch == 'a' || ch == 'e'
        || ch == 'i' || ch == 'o'
        || ch == 'u' || ch == 'A'
        || ch == 'E' || ch == 'I'
        || ch == 'O' || ch == 'U') {
        return true;
    }
    return false;
}

// Function to find the length of
// the longest substring that
// doesn't contain any vowel
int maxLengthString(string s)
{
    // Stores the length of
    // the longest substring
    int maximum = 0;

    int count = 0;

    // Traverse the string, S
    for (int i = 0; i < s.length(); i++) {

        // If the current character
        // is vowel, set count as 0
        if (vowel(s[i])) {
            count = 0;
        }

        // If the current
        // character is a consonant
        else {

            // Increment count by 1
            count++;
        }

        // Update the maximum length
        maximum = max(maximum, count);
    }

    // Return the result
    return maximum;
}

// Driver Code
int main()
{
    string S = "geeksforgeeks";
    cout << maxLengthString(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {
    public static boolean vowel(char ch)
    {
        if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o'
            || ch == 'u' || ch == 'A' || ch == 'E'
            || ch == 'I' || ch == 'O' || ch == 'U') {
            return true;
        }
        return false;
    }

    // Function to find the length of
    // the longest substring that
    // doesn't contain any vowel
    public static int maxLengthString(String s)
    {
        // Stores the length of
        // the longest substring
        int maximum = 0;

        int count = 0;

        // Traverse the string, S
        for (int i = 0; i < s.length(); i++) {

            // If the current character
            // is vowel, set count as 0
            if (vowel(s.charAt(i))) {
                count = 0;
            }

            // If the current
            // character is a consonant
            else {

                // Increment count by 1
                count++;
            }

            // Update the maximum length
            maximum = Math.max(maximum, count);
        }

        // Return the result
        return maximum;
    }

    public static void main(String[] args)
    {
        String S = "geeksforgeeks";
        System.out.println(maxLengthString(S));
      // This code is contributed by Potta Lokesh
    }
```

## 计算机编程语言

```
# Python program for the above approach
# Function to check if the
# character is a vowel or not
def vowel(ch):

    if (ch == 'a' or ch == 'e'
        or ch == 'i' or ch == 'o'
        or ch == 'u' or ch == 'A'
        or ch == 'E' or ch == 'I'
        or ch == 'O' or ch == 'U'):
        return True

        return False

# Function to find the length of
# the longest substring that
# doesn't contain any vowel
def maxLengthString(s):

    # Stores the length of
    # the longest substring
    maximum = 0  
    count = 0;

    # Traverse the string, S
    for i in range(len(s)):

        # If the current character
        # is vowel, set count as 0
        if (vowel(s[i])):
            count = 0;

        # If the current
        # character is a consonant
        else:
            # Increment count by 1
            count += 1

        # Update the maximum length
        maximum = max(maximum, count)

    # Return the result
    return maximum

# Driver Code
S = 'geeksforgeeks'
print(maxLengthString(S))

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if the
// character is a vowel or not
static bool vowel(char ch)
{
    if (ch == 'a' || ch == 'e' ||
        ch == 'i' || ch == 'o' ||
        ch == 'u' || ch == 'A' ||
        ch == 'E' || ch == 'I' ||
        ch == 'O' || ch == 'U')
    {
        return true;
    }
    return false;
}

// Function to find the length of
// the longest substring that
// doesn't contain any vowel
static int maxLengthString(string s)
{

    // Stores the length of
    // the longest substring
    int maximum = 0;

    int count = 0;

    // Traverse the string, S
    for(int i = 0; i < s.Length; i++)
    {

        // If the current character
        // is vowel, set count as 0
        if (vowel(s[i]) == true)
        {
            count = 0;
        }

        // If the current
        // character is a consonant
        else
        {

            // Increment count by 1
            count++;
        }

        // Update the maximum length
        maximum = Math.Max(maximum, count);
    }

    // Return the result
    return maximum;
}

// Driver Code
public static void Main()
{
    string S = "geeksforgeeks";

    Console.Write(maxLengthString(S));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to check if the
        // character is a vowel or not
        function vowel(ch) {
            if (ch == 'a' || ch == 'e'
                || ch == 'i' || ch == 'o'
                || ch == 'u' || ch == 'A'
                || ch == 'E' || ch == 'I'
                || ch == 'O' || ch == 'U') {
                return true;
            }
            return false;
        }

        // Function to find the length of
        // the longest substring that
        // doesn't contain any vowel
        function maxLengthString(s) {
            // Stores the length of
            // the longest substring
            let maximum = 0;

            let count = 0;

            // Traverse the string, S
            for (let i = 0; i < s.length; i++) {

                // If the current character
                // is vowel, set count as 0
                if (vowel(s[i])) {
                    count = 0;
                }

                // If the current
                // character is a consonant
                else {

                    // Increment count by 1
                    count++;
                }

                // Update the maximum length
                maximum = Math.max(maximum, count);
            }

            // Return the result
            return maximum;
        }

        // Driver Code

        var S = "geeksforgeeks";
        document.write(maxLengthString(S));

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)