# 没有两个相邻字母相同的元音最长子串

> 原文:[https://www . geesforgeks . org/最长元音子串不带两个相邻字母-相同/](https://www.geeksforgeeks.org/longest-substring-of-vowels-with-no-two-adjacent-alphabets-same/)

给定由小写字母组成的字符串 **str** ，任务是找到最长子字符串的长度，使得它的所有字符都是元音字母，并且没有两个相邻的字母相同。

**示例:**

> **输入:**str = " aeoibsdaeioudb "
> **输出:** 5
> **解释:**
> 相邻字母不相同的元音最长子串是“aeiou”
> 子串长度= 5
> 
> **输入:** str = "geeksforgeeks"
> **输出:** 1
> **解释:**
> 相邻字母不相同的元音最长子串是“e”或“o”。
> 子串长度= 1

**天真方法:**
从给定的字符串生成所有可能的子字符串。对于每个子串，检查它的所有字符是否都是元音，并且没有两个相邻的字符是相同的，然后比较所有这样的子串的长度，并打印最大长度。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check a
// character is vowel or not
bool isVowel(char c)
{
    return (c == 'a' || c == 'e'
            || c == 'i' || c == 'o'
            || c == 'u');
}

// Function to check a
// substring is valid or not
bool isValid(string& s)
{

    int n = s.size();

    // If size is 1 then
    // check only first character
    if (n == 1)
        return (isVowel(s[0]));

    // If 0'th character is
    // not vowel then invalid
    if (isVowel(s[0]) == false)
        return false;

    for (int i = 1; i < n; i++) {

        // If two adjacent characters
        // are same or i'th char is
        // not vowel then invalid
        if (s[i] == s[i - 1]
            || !isVowel(s[i]))
            return false;
    }

    return true;
}

// Function to find length
// of longest substring
// consisting only of
// vowels and no similar
// adjacent alphabets
int findMaxLen(string& s)
{
    // Stores max length
    // of valid substring
    int maxLen = 0;
    int n = s.length();

    for (int i = 0; i < n; i++) {

        // For current substring
        string temp = "";

        for (int j = i; j < n; j++) {

            temp = temp + s[j];

            // Check if substring
            // is valid
            if (isValid(temp))

                // Size of substring
                // is (j-i+1)
                maxLen = max(
                    maxLen, (j - i + 1));
        }
    }

    return maxLen;
}

// Driver code
int main()
{
    string Str = "aeoibsddaeiouudb";

    cout << findMaxLen(Str) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.io.*;
class GFG{

// Function to check a
// character is vowel or not
static boolean isVowel(char c)
{
    return (c == 'a' || c == 'e' ||
            c == 'i' || c == 'o' ||
            c == 'u');
}

// Function to check a
// subString is valid or not
static boolean isValid(String s)
{
    int n = s.length();

    // If size is 1 then
    // check only first character
    if (n == 1)
        return (isVowel(s.charAt(0)));

    // If 0'th character is
    // not vowel then invalidlen
    if (isVowel(s.charAt(0)) == false)
        return false;

    for (int i = 1; i < n; i++)
    {

        // If two adjacent characters
        // are same or i'th char is
        // not vowel then invalid
        if (s.charAt(i) == s.charAt(i - 1) ||
                  !isVowel(s.charAt(i)))
            return false;
    }
    return true;
}

// Function to find length
// of longest subString
// consisting only of
// vowels and no similar
// adjacent alphabets
static int findMaxLen(String s)
{

    // Stores max length
    // of valid subString
    int maxLen = 0;
    int n = s.length();

    for (int i = 0; i < n; i++)
    {

        // For current subString
        String temp = "";

        for (int j = i; j < n; j++)
        {

            temp = temp + s.charAt(j);

            // Check if subString
            // is valid
            if (isValid(temp))

                // Size of subString
                // is (j-i+1)
                maxLen = Math.max(maxLen,
                                 (j - i + 1));
        }
    }
    return maxLen;
}

// Driver code
public static void main (String[] args)
{
    String Str = "aeoibsddaeiouudb";

    System.out.println(findMaxLen(Str));
}
}

// This code is contributed by shubhamcoder
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to check a
# character is vowel or not
def isVowel(c):
    return (c == 'a' or c == 'e' or
            c == 'i' or c == 'o' or
            c == 'u')

# Function to check a
# substring is valid or not
def isValid(s):
    n = len(s)

    # If size is 1 then
    # check only first character
    if (n == 1):
        return (isVowel(s[0]))

    # If 0'th character is
    # not vowel then invalid
    if (isVowel(s[0]) == False):
        return False

    for i in range (1, n):

        # If two adjacent characters
        # are same or i'th char is
        # not vowel then invalid
        if (s[i] == s[i - 1] or not
            isVowel(s[i])):
            return False

    return True

# Function to find length
# of longest substring
# consisting only of
# vowels and no similar
# adjacent alphabets
def findMaxLen(s):

    # Stores max length
    # of valid substring
    maxLen = 0
    n = len(s)

    for i in range (n):

        # For current substring
        temp = ""

        for j in range (i, n):
            temp = temp + s[j]

            # Check if substring
            # is valid
            if (isValid(temp)):

                # Size of substring
                # is (j-i+1)
                maxLen = (max(maxLen, (j - i + 1)))

    return maxLen

# Driver code
if __name__ == "__main__":

    Str = "aeoibsddaeiouudb"
    print (findMaxLen(Str))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of the above approach
using System;
class GFG{

// Function to check a
// character is vowel or not
static bool isVowel(char c)
{
    return (c == 'a' || c == 'e' ||
            c == 'i' || c == 'o' ||
            c == 'u');
}

// Function to check a
// substring is valid or not
static bool isValid(string s)
{

    int n = s.Length;

    // If size is 1 then
    // check only first character
    if (n == 1)
        return (isVowel(s[0]));

    // If 0'th character is
    // not vowel then invalid
    if (isVowel(s[0]) == false)
        return false;

    for(int i = 1; i < n; i++)
    {

       // If two adjacent characters
       // are same or i'th char is
       // not vowel then invalid
       if (s[i] == s[i - 1] ||
          !isVowel(s[i]))
           return false;
    }
    return true;
}

// Function to find length
// of longest substring
// consisting only of
// vowels and no similar
// adjacent alphabets
static int findMaxLen(string s)
{
    // Stores max length
    // of valid substring
    int maxLen = 0;
    int n = s.Length;

    for(int i = 0; i < n; i++)
    {

       // For current substring
       string temp = "";

       for(int j = i; j < n; j++)
       {
           temp = temp + s[j];

           // Check if substring
           // is valid
           if (isValid(temp))

               // Size of substring
               // is (j-i+1)
               maxLen = Math.Max(maxLen,
                                (j - i + 1));
       }
    }
    return maxLen;
}

// Driver code
public static void Main()
{
    string Str = "aeoibsddaeiouudb";

    Console.WriteLine(findMaxLen(Str));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript implementation of the
// above approach

// Function to check a
// character is vowel or not
function isVowel(c)
{
    return (c == 'a' || c == 'e' ||
            c == 'i' || c == 'o' ||
            c == 'u');
}

// Function to check a
// subString is valid or not
function isValid(s)
{
    let n = s.length;

    // If size is 1 then
    // check only first character
    if (n == 1)
        return (isVowel(s[0]));

    // If 0'th character is
    // not vowel then invalidlen
    if (isVowel(s[0]) == false)
        return false;

    for(let i = 1; i < n; i++)
    {

        // If two adjacent characters
        // are same or i'th char is
        // not vowel then invalid
        if (s[i] == s[i - 1] ||
           !isVowel(s[i]))
            return false;
    }
    return true;
}

// Function to find length
// of longest subString
// consisting only of
// vowels and no similar
// adjacent alphabets
function findMaxLen(s)
{

    // Stores max length
    // of valid subString
    let maxLen = 0;
    let n = s.length;

    for(let i = 0; i < n; i++)
    {

        // For current subString
        let temp = "";

        for(let j = i; j < n; j++)
        {
            temp = temp + s[j];

            // Check if subString
            // is valid
            if (isValid(temp))

                // Size of subString
                // is (j-i+1)
                maxLen = Math.max(maxLen,
                                 (j - i + 1));
        }
    }
    return maxLen;
}

// Driver Code
let Str = "aeoibsddaeiouudb";

document.write(findMaxLen(Str));

// This code is contributed by sanjoy_62

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N <sup>3</sup> )*

**有效方法:**
这个问题的线性时间解决方案是可能的。如果一个子串的所有字符都是元音，并且没有两个相邻的字符是相同的，那么这个子串将被认为是有效的。其思想是遍历字符串并跟踪最长的有效子字符串。
详细步骤如下:

1.  创建一个变量 **cur** 来存储当前有效子串的长度，另一个变量 **maxVal** 来跟踪到目前为止找到的最大值 **cur** ，最初两者都设置为 0。
2.  如果索引 0 处的字符是元音，则它是长度为 1 的有效子串，因此 maxVal = 1
3.  从索引 1 开始遍历**字符串**。如果当前字符不是元音，则不存在有效的子串，cur = 0
4.  如果当前字符是元音并且
    *   不同于前一个字符，则将其包含在当前有效子串中，并将 **cur** 增加 1。更新 **maxVal** 。
    *   与前一个字符相同，则新的有效子字符串从此字符开始，并且 **cur** 重置为 1。
5.  **maxVal** 的最终值给出了答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check a
// character is vowel or not
bool isvowel(char c)
{
    return c == 'a' || c == 'e'
           || c == 'i' || c == 'o'
           || c == 'u';
}
// Function to find length
// of longest substring
// consisting only of
// vowels and no similar
// adjacent alphabets
int findMaxLen(string& s)
{
    // Stores max length
    // of valid subString
    int maxLen = 0;

    // Stores length of
    // current valid subString
    int cur = 0;

    if (isvowel(s[0]))
        cur = maxLen = 1;

    for (int i = 1; i < s.length(); i++) {
        if (isvowel(s[i])) {
            // If curr and prev character
            // are not same, include it
            if (s[i] != s[i - 1])
                cur += 1;

            // If same as prev one, start
            // new subString from here
            else
                cur = 1;
        }

        else {
            cur = 0;
        }

        // Store max in maxLen
        maxLen = max(cur, maxLen);
    }

    return maxLen;
}

// Driver code
int main()
{
    string Str = "aeoibsddaeiouudb";
    cout << findMaxLen(Str) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach

public class GFG {

    // Function to check a
    // character is vowel or not
    static boolean isVowel(char x)
    {
        return (x == 'a' || x == 'e'
                || x == 'i' || x == 'o'
                || x == 'u');
    }

    // Function to find length
    // of longest substring
    // consisting only of
    // vowels and no similar
    // adjacent alphabets
    static int findMaxLen(String s)
    {
        // Stores max length
        // of valid subString
        int maxLen = 0;

        // Stores length of
        // current valid subString
        int cur;

        if (isVowel(s.charAt(0)))
            maxLen = 1;

        cur = maxLen;

        for (int i = 1; i < s.length(); i++) {
            if (isVowel(s.charAt(i))) {
                // If curr and prev character
                // are not same, include it
                if (s.charAt(i)
                    != s.charAt(i - 1))
                    cur += 1;

                // If same as prev one, start
                // new subString from here
                else
                    cur = 1;
            }

            else {
                cur = 0;
            }

            // Store max in maxLen
            maxLen = Math.max(cur, maxLen);
        }

        return maxLen;
    }

    // Driver code
    public static void main(String[] args)
    {
        String Str = "aeoibsddaeiouudb";

        System.out.println(findMaxLen(Str));
    }
}
```

## 蟒蛇 3

```
# Python implementation of
# the above approach

# Function to check a
# character is vowel or not
def isVowel(x):

    return (x == 'a' or x == 'e' or
            x == 'i' or x == 'o' or
            x == 'u');

# Function to find length
# of longest substring
# consisting only of
# vowels and no similar
# adjacent alphabets
def findMaxLen(s):

    # Stores max length
    # of valid subString
    maxLen = 0

    # Stores length of
    # current valid subString
    cur = 0

    if(isVowel(s[0])):
        maxLen = 1;

    cur = maxLen

    for i in range(1, len(s)):

        if(isVowel(s[i])):
            # If curr and prev character
            # are not same, include it
            if(s[i] != s[i-1]):
                cur += 1

            # If same as prev one, start
            # new subString from here   
            else:
                cur = 1

        else:
            cur = 0;

        # Store max in maxLen
        maxLen = max(cur, maxLen);

    return maxLen

# Driver code

Str = "aeoibsddaeiouudb"

print(findMaxLen(Str))
```

## C#

```
// C# implementation of
// the above approach

using System;

public class GFG {

    // Function to check a
    // character is vowel or not
    public static bool isVowel(char x)
    {
        return (x == 'a' || x == 'e'
                || x == 'i' || x == 'o'
                || x == 'u');
    }

    // Function to find length
    // of longest substring
    // consisting only of
    // vowels and no similar
    // adjacent alphabets
    public static int findMaxLen(string s)
    {
        // Stores max length
        // of valid subString
        int maxLen = 0;

        // Stores length of
        // current valid subString
        int cur;

        if (isVowel(s[0]))
            maxLen = 1;

        cur = maxLen;

        for (int i = 1; i < s.Length; i++) {
            if (isVowel(s[i])) {
                // If curr and prev character
                // are not same, include it
                if (s[i] != s[i - 1])
                    cur += 1;

                // If same as prev one, start
                // new subString from here
                else
                    cur = 1;
            }

            else {
                cur = 0;
            }

            // Store max in maxLen
            maxLen = Math.Max(cur, maxLen);
        }

        return maxLen;
    }

    // Driver code
    public static void Main(string[] args)
    {
        string Str = "aeoibsddaeiouudb";

        Console.WriteLine(findMaxLen(Str));
    }
}
```

## java 描述语言

```
<script>
      // JavaScript implementation of
      // the above approach
      // Function to check a
      // character is vowel or not
      function isVowel(x) {
        return x === "a" || x === "e" || x === "i" || x === "o" || x === "u";
      }

      // Function to find length
      // of longest substring
      // consisting only of
      // vowels and no similar
      // adjacent alphabets
      function findMaxLen(s)
      {

        // Stores max length
        // of valid subString
        var maxLen = 0;

        // Stores length of
        // current valid subString
        var cur;

        if (isVowel(s[0])) maxLen = 1;

        cur = maxLen;

        for (var i = 1; i < s.length; i++) {
          if (isVowel(s[i])) {
            // If curr and prev character
            // are not same, include it
            if (s[i] !== s[i - 1]) cur += 1;
            // If same as prev one, start
            // new subString from here
            else cur = 1;
          } else {
            cur = 0;
          }

          // Store max in maxLen
          maxLen = Math.max(cur, maxLen);
        }

        return maxLen;
      }

      // Driver code
      var Str = "aeoibsddaeiouudb";
      document.write(findMaxLen(Str));

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N)*