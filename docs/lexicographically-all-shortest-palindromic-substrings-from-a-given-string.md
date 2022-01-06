# 从给定字符串中按词典顺序排列的所有最短回文子串

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最短回文子串-来自给定字符串/](https://www.geeksforgeeks.org/lexicographically-all-shortest-palindromic-substrings-from-a-given-string/)

给定一个大小为 n 的**字符串 s** ，任务是从给定的字符串中按字典顺序找到所有最短的回文子字符串。

**示例:**

> **输入:** s= "programming"
> **输出:** a g i m n o p r
> **解释:**
> 单词“programming”的字典式最短回文子串将是给定字符串中的单个字符。因此，输出是:一个通用输入输出设备。
> 
> **输入:** s=【极客暴发户】
> T3】输出: e f g k o r s

**方法:**
为了解决上面提到的问题，首先观察到最短的回文子串大小为 1。因此，根据问题陈述，我们必须按字典顺序找到大小为 1 的所有不同的子字符串，这意味着给定字符串中的所有字符。

下面是上述方法的实现:

## C++

```
// C++ program to find Lexicographically all
// Shortest Palindromic Substrings from a given string

#include <bits/stdc++.h>
using namespace std;

// Function to find all lexicographically
// shortest palindromic substring
void shortestPalindrome(string s)
{

    // Array to keep track of alphabetic characters
    int abcd[26] = { 0 };

    for (int i = 0; i < s.length(); i++)
        abcd[s[i] - 97] = 1;

    // Iterate to print all lexicographically shortest substring
    for (int i = 0; i < 26; i++) {
        if (abcd[i] == 1)
            cout << char(i + 97) << " ";
    }
}

// Driver code
int main()
{
    string s = "geeksforgeeks";

    shortestPalindrome(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Lexicographically all
// Shortest Palindromic Substrings from a given string
class Main
{
    // Function to find all lexicographically
    // shortest palindromic substring
    static void shortestPalindrome(String s)
    {

        // Array to keep track of
        // alphabetic characters
        int[] abcd = new int[26];

        for (int i = 0; i < s.length(); i++)
            abcd[s.charAt(i) - 97] = 1;

        // Iterate to print all lexicographically
        // shortest substring
        for (int i = 0; i < 26; i++)
        {
            if (abcd[i] == 1)
            {
                System.out.print((char)(i + 97) + " ");
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "geeksforgeeks";
        shortestPalindrome(s);
    }
}
```

## 蟒蛇 3

```
# C++ program to find Lexicographically all
# Shortest Palindromic Substrings from a given string

# Function to find all lexicographically
# shortest palindromic substring
def shortestPalindrome (s) :

    # Array to keep track of alphabetic characters
    abcd = [0]*26

    for i in range(len(s)):
        abcd[ord(s[i])-97] = 1

    # Iterate to print all lexicographically shortest substring
    for i in range(26):
        if abcd[i]== 1 :
            print( chr(i + 97), end =' ' )

# Driver code
s = "geeksforgeeks"

shortestPalindrome (s)
```

## C#

```
// C# program to find Lexicographically
// all shortest palindromic substrings
// from a given string
using System;

class GFG{

// Function to find all lexicographically
// shortest palindromic substring
static void shortestPalindrome(string s)
{

    // Array to keep track of
    // alphabetic characters
    int[] abcd = new int[26];

    for(int i = 0; i < s.Length; i++)
       abcd[s[i] - 97] = 1;

    // Iterate to print all lexicographically
    // shortest substring
    for(int i = 0; i < 26; i++)
    {
       if (abcd[i] == 1)
       {
           Console.Write((char)(i + 97) + " ");
       }
    }
}

// Driver code
static public void Main(string[] args)
{
    string s = "geeksforgeeks";
    shortestPalindrome(s);
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to find Lexicographically all
// Shortest Palindromic Substrings from a given string

    // Function to find all lexicographically
    // shortest palindromic substring
    function shortestPalindrome(s)
    {

        // Array to keep track of
        // alphabetic characters
        let abcd = Array.from({length: 26}, (_, i) => 0);

        for (let i = 0; i < s.length; i++)
            abcd[s[i].charCodeAt()  - 97] = 1;

        // Iterate to prlet all lexicographically
        // shortest substring
        for (let i = 0; i < 26; i++)
        {
            if (abcd[i] == 1)
            {
                document.write(String.fromCharCode(i + 97)  + " ");
            }
        }
    }

// Driver Code

    let s = "geeksforgeeks";
    shortestPalindrome(s.split(''));

</script>
```

**Output:** 

```
e f g k o r s
```

**时间复杂度:** O(N)，其中 N 是字符串的大小。
**空间复杂度:** O(1)