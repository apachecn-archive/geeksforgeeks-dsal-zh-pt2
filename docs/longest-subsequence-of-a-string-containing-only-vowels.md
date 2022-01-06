# 只包含元音的字符串的最长子序列

> 原文:[https://www . geeksforgeeks . org/仅包含元音的最长子序列字符串/](https://www.geeksforgeeks.org/longest-subsequence-of-a-string-containing-only-vowels/)

给定一个仅包含字母的字符串 **str** ，任务是打印仅包含元音的字符串 **str** 的最长子序列。
**例:**

> **输入:** str = "geeksforgeeks"
> **输出:** eeoee
> **解释:**
> “eeoee”是仅包含元音的字符串中最长的子序列。
> **输入:** str = "HelloWorld"
> **输出:** eoo
> **解释:**
> “EEO”是仅包含元音的字符串中最长的子序列。

**进场:**

*   逐个字符遍历给定的字符串。
*   如果字符是元音，将其附加到结果字符串中。
*   当遍历完成时，所需的仅包含元音的最长子序列存储在结果字符串中。

以下是上述方法的实现:

## C++

```
// C++ program to find the longest
// subsequence containing only vowels

#include <bits/stdc++.h>
using namespace std;

// Function to check whether
// a character is vowel or not
bool isVowel(char x)
{
    x = tolower(x);

    // Returns true if x is vowel
    return (x == 'a' || x == 'e'
            || x == 'i' || x == 'o'
            || x == 'u');
}

// Function to find the longest subsequence
// which contain all vowels
string longestVowelSubsequence(string str)
{
    string answer = "";

    // Length of the string
    int n = str.size();

    // Iterating through the string
    for (int i = 0; i < n; i++) {

        // Checking if the character is a
        // vowel or not
        if (isVowel(str[i])) {

            // If it is a vowel, then add it
            // to the final string
            answer += str[i];
        }
    }

    return answer;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    cout << longestVowelSubsequence(str)
 << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest
// subsequence containing only vowels
class GFG{

// Function to check whether
// a character is vowel or not
static boolean isVowel(char x)
{
    x = Character.toLowerCase(x);

    // Returns true if x is vowel
    return (x == 'a' || x == 'e'
            || x == 'i' || x == 'o'
            || x == 'u');
}

// Function to find the longest subsequence
// which contain all vowels
static String longestVowelSubsequence(String str)
{
    String answer = "";

    // Length of the String
    int n = str.length();

    // Iterating through the String
    for (int i = 0; i < n; i++) {

        // Checking if the character is a
        // vowel or not
        if (isVowel(str.charAt(i))) {

            // If it is a vowel, then add it
            // to the final String
            answer += str.charAt(i);
        }
    }
    return answer;
}

// Driver code
public static void main(String[] args)
{
    String str = "geeksforgeeks";
    System.out.print(longestVowelSubsequence(str)
 +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find the longest
# subsequence containing only vowels

# Function to check whether
# a character is vowel or not
def isVowel(x):

    # Returns true if x is vowel
    return (x == 'a' or x == 'e'or x == 'i' or x == 'o' or x == 'u')

# Function to find the longest subsequence
# which contain all vowels
def longestVowelSubsequence(str):

    answer = ""

    # Length of the string
    n = len(str)

    # Iterating through the string
    for i in range(n):

        # Checking if the character is a
        # vowel or not
        if (isVowel(str[i])):

            # If it is a vowel, then add it
            # to the final string
            answer += str[i]

    return answer

# Driver code
str = "geeksforgeeks"
print(longestVowelSubsequence(str))

# This code is contributed by apurva raj
```

## C#

```
// C# program to find the longest
// subsequence containing only vowels
using System;

class GFG{

// Function to check whether
// a character is vowel or not
static bool isVowel(char x)
{
    x = char.ToLower(x);

    // Returns true if x is vowel
    return (x == 'a' || x == 'e'
            || x == 'i' || x == 'o'
            || x == 'u');
}

// Function to find the longest subsequence
// which contain all vowels
static String longestVowelSubsequence(String str)
{
    String answer = "";

    // Length of the String
    int n = str.Length;

    // Iterating through the String
    for (int i = 0; i < n; i++) {

        // Checking if the character is a
        // vowel or not
        if (isVowel(str[i])) {

            // If it is a vowel, then add it
            // to the readonly String
            answer += str[i];
        }
    }
    return answer;
}

// Driver code
public static void Main(String[] args)
{
    String str = "geeksforgeeks";
    Console.Write(longestVowelSubsequence(str)+"\n");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to find the longest
// subsequence containing only vowels

// Function to check whether
// a character is vowel or not
function isVowel(x)
{
    x = (x.toLowerCase());

    // Returns true if x is vowel
    return (x == 'a' || x == 'e'
            || x == 'i' || x == 'o'
            || x == 'u');
}

// Function to find the longest subsequence
// which contain all vowels
function longestVowelSubsequence(str)
{
    var answer = "";

    // Length of the string
    var n = str.length;

    // Iterating through the string
    for (var i = 0; i < n; i++) {

        // Checking if the character is a
        // vowel or not
        if (isVowel(str[i])) {

            // If it is a vowel, then add it
            // to the final string
            answer += str[i];
        }
    }

    return answer;
}

// Driver code
var str = "geeksforgeeks";
document.write( longestVowelSubsequence(str));

// Thi code is contributed by importantly.
</script>
```

**Output:** 

```
eeoee
```

**时间复杂度:** O(N)