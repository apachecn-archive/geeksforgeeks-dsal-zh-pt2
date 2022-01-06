# 仅由元音组成的子串计数

> 原文:[https://www . geesforgeks . org/count-of-substrings-仅由元音组成/](https://www.geeksforgeeks.org/count-of-substrings-consisting-only-of-vowels/)

给定一个字符串 **S** ，任务是统计所有只包含元音的子字符串。

**示例:**

> **输入:** S = "geeksforgeeks"
> **输出:** 7
> **解释:**
> 子串{“e”、“ee”、“e”、“o”、“e”、“ee”、“e”}仅由元音组成。
> 
> **输入:**S = " aeui "
> **输出:** 6
> **解释:**
> 子串{“a”、“ae”、“e”、“u”、“ui”、“I”}仅由元音组成。

**天真方法:**
最简单的方法是生成所有子串，并检查它们是否只包含元音。

下面是上述方法的实现:

## C++

```
// C++ program to Count all substrings
// in a string which contains only vowels
#include <iostream>
using namespace std;

// Function to check if a
// character is vowel or not
bool isvowel(char ch)
{
    return (ch == 'a' or ch == 'e'
            or ch == 'i' or ch == 'o'
            or ch == 'u');
}

// Function to check whether
// string contains only vowel
bool isvalid(string& s)
{
    int n = s.length();

    for (int i = 0; i < n; i++) {
        // Check if the character is
        // not vowel then invalid
        if (!isvowel(s[i]))
            return false;
    }

    return true;
}

// Function to Count all substrings
// in a string which contains
// only vowels
int CountTotal(string& s)
{
    int ans = 0;

    int n = s.length();

    // Generate all substring of s
    for (int i = 0; i < n; i++) {
        string temp = "";
        for (int j = i; j < n; j++) {
            temp += s[j];

            // If temp contains only vowels
            if (isvalid(temp))
                // Increment the count
                ans += 1;
        }
    }

    return ans;
}

// Driver Program
int main()
{
    string s = "aeoibsddaaeiouudb";

    cout << (CountTotal(s)) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all subStrings
// in a String which contains only vowels
import java.util.*;

class GFG{

// Function to check if a
// character is vowel or not
static boolean isvowel(char ch)
{
    return (ch == 'a' || ch == 'e' ||
            ch == 'i' || ch == 'o' ||
            ch == 'u');
}

// Function to check whether
// String contains only vowel
static boolean isvalid(String s)
{
    int n = s.length();

    for(int i = 0; i < n; i++)
    {

       // Check if the character is
       // not vowel then invalid
       if (!isvowel(s.charAt(i)))
           return false;
    }
    return true;
}

// Function to Count all subStrings
// in a String which contains
// only vowels
static int CountTotal(String s)
{
    int ans = 0;
    int n = s.length();

    // Generate all subString of s
    for(int i = 0; i < n; i++)
    {
       String temp = "";
       for(int j = i; j < n; j++)
       {
          temp += s.charAt(j);

          // If temp contains only vowels
          if (isvalid(temp))

              // Increment the count
              ans += 1;
       }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    String s = "aeoibsddaaeiouudb";

    System.out.print((CountTotal(s)) + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to count all substrings
# in a string which contains only vowels

# Function to check if a
# character is vowel or not
def isvowel(ch):
    return (ch == 'a' or ch == 'e' or
            ch == 'i' or ch == 'o' or
            ch == 'u')

# Function to check whether
# string contains only vowel
def isvalid(s):

    n = len(s)
    for i in range(n):

        # Check if the character is
        # not vowel then invalid
        if (not isvowel(s[i])):
            return False

    return True

# Function to Count all substrings
# in a string which contains
# only vowels
def CountTotal(s):

    ans = 0
    n = len(s)

    # Generate all substring of s
    for i in range(n):
        temp = ""

        for j in range(i, n):
            temp += s[j]

            # If temp contains only vowels
            if (isvalid(temp)):

                # Increment the count
                ans += 1

    return ans

# Driver code
if __name__ == '__main__':

    s = "aeoibsddaaeiouudb"

    print(CountTotal(s))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to count all subStrings
// in a String which contains only vowels
using System;
class GFG{

// Function to check if a
// character is vowel or not
static Boolean isvowel(char ch)
{
    return (ch == 'a' || ch == 'e' ||
            ch == 'i' || ch == 'o' ||
            ch == 'u');
}

// Function to check whether
// String contains only vowel
static Boolean isvalid(string s)
{
    int n = s.Length;

    for(int i = 0; i < n; i++)
    {

        // Check if the character is
        // not vowel then invalid
        if (!isvowel(s[i]))
            return false;
    }
    return true;
}

// Function to Count all subStrings
// in a String which contains
// only vowels
static int CountTotal(string s)
{
    int ans = 0;
    int n = s.Length;

    // Generate all subString of s
    for(int i = 0; i < n; i++)
    {
        string temp = "";
        for(int j = i; j < n; j++)
        {
            temp += s[j];

            // If temp contains only vowels
            if (isvalid(temp))

                // Increment the count
                ans += 1;
        }
    }
    return ans;
}

// Driver code
public static void Main()
{
    string s = "aeoibsddaaeiouudb";

    Console.Write((CountTotal(s)) + "\n");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to count all subStrings
// in a String which contains only vowels

// Function to check if a
// character is vowel or not
function isvowel(ch)
{
    return (ch == 'a' || ch == 'e' ||
            ch == 'i' || ch == 'o' ||
            ch == 'u');
}

// Function to check whether
// String contains only vowel
function isvalid(s)
{
    let n = s.length;

    for(let i = 0; i < n; i++)
    {

        // Check if the character is
        // not vowel then invalid
        if (!isvowel(s[i]))
            return false;
    }
    return true;
}

// Function to Count all subStrings
// in a String which contains
// only vowels
function CountTotal(s)
{
    let ans = 0;
    let n = s.length;

    // Generate all subString of s
    for(let i = 0; i < n; i++)
    {
        let temp = "";
        for(let j = i; j < n; j++)
        {
            temp += s[j];

            // If temp contains only vowels
            if (isvalid(temp))

                // Increment the count
                ans += 1;
        }
    }
    return ans;
}

// Driver code
let s = "aeoibsddaaeiouudb";

document.write((CountTotal(s)));

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
38
```

***时间复杂度:** O(N <sup>3</sup> )*

**高效方法:**
对上述方法进行优化，主要思想是**统计只包含元音的子串的长度**，比如 x，那么每 **x** 可能的子串个数为 **x * (x + 1) / 2** 只包含元音。对每个这样的子串重复这个过程，并返回最终计数。

下面是上述方法的实现:

## C++

```
// C++ program to Count all substrings
// in a string which contains only vowels
#include <iostream>
using namespace std;

// Function to check vowel or not
bool isvowel(char ch)
{
    return (ch == 'a' or ch == 'e'
            or ch == 'i' or ch == 'o'
            or ch == 'u');
}

// Function to Count all substrings
// in a string which contains
// only vowels
int CountTotal(string& s)
{
    int ans = 0;
    int n = s.length();
    int cnt = 0;

    for (int i = 0; i < n; i++) {
        // Check if current character
        // is vowel
        if (isvowel(s[i]))
            // Increment length of substring
            cnt += 1;

        else {
            // Calculate possible
            // substrings of calculated
            // length
            ans += (cnt * (cnt + 1) / 2);

            // Reset the length
            cnt = 0;
        }
    }

    // Add remaining possible
    // substrings consisting
    // of vowels occupying
    // last indices of the string
    if (cnt != 0) {
        ans += (cnt * (cnt + 1) / 2);
    }

    return ans;
}

// Driver Program
int main()
{
    string s = "geeksforgeeks";

    cout << (CountTotal(s)) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count all substrings
// in a string which contains only vowels
import java.io.*;

public class GFG {

    // Function to check vowel or not
    static boolean isvowel(char x)
    {
        return (x == 'a' || x == 'e'
                || x == 'i' || x == 'o'
                || x == 'u');
    }

    // Function to find largest
    // string which satisfy condition
    static int CountTotal(String str)
    {
        int ans = 0;

        int n = str.length();

        char[] s = str.toCharArray();

        int cnt = 0;

        for (int i = 0; i < n; i++) {
            // Check if current character
            // is vowel
            if (isvowel(s[i]))
                // Increment count
                cnt += 1;

            else {
                // Count all possible
                // substrings of calculated
                // length
                ans += (cnt * (cnt + 1) / 2);

                // Reset the length
                cnt = 0;
            }
        }

        // Add remaining possible
        // substrings consisting
        // of vowels occupying
        // last indices of the string
        if (cnt != 0)

            ans += (cnt * (cnt + 1) / 2);

        return ans;
    }

    // Driver Program
    static public void main(String[] args)
    {
        String s = "geeksforgeeks";

        System.out.println(CountTotal(s));
    }
}
```

## 蟒蛇 3

```
# Python3 program to Count all substrings
# in a string which contains only vowels

# function to check vowel or not
def isvowel(ch):
    return(ch in "aeiou")

# Function to Count all substrings
# in a string which contains
# only vowels
def CountTotal(s):

    ans = 0
    n = len(s)
    cnt = 0

    for i in range(0, n):

        # if current character is
        # vowel
        if(isvowel(s[i])):
            # increment
            cnt += 1

        else:

            # Count all possible
            # substring of calculated
            # length
            ans += (cnt*(cnt + 1) // 2)

            # Reset the length
            cnt = 0

    # Add remaining possible
    # substrings consisting
    # of vowels occupying
    # last indices of the string
    if(cnt != 0):
        ans += (cnt*(cnt + 1) // 2)

    return ans

# Driver Program
s = "geeksforgeeks"

print(CountTotal(s))
```

## C#

```
// C# program to count all substrings
// in a string which contains only vowels
using System;

class GFG{

// Function to check vowel or not
static bool isvowel(char x)
{
    return (x == 'a' || x == 'e' ||
            x == 'i' || x == 'o' ||
            x == 'u');
}

// Function to find largest
// string which satisfy condition
static int CountTotal(string str)
{
    int ans = 0;
    int n = str.Length;
    char[] s = str.ToCharArray();
    int cnt = 0;

    for(int i = 0; i < n; i++)
    {

       // Check if current character
       // is vowel
       if (isvowel(s[i]))

           // Increment count
           cnt += 1;
       else
       {

           // Count all possible
           // substrings of calculated
           // length
           ans += (cnt * (cnt + 1) / 2);

           // Reset the length
           cnt = 0;
       }
    }

    // Add remaining possible
    // substrings consisting
    // of vowels occupying
    // last indices of the string
    if (cnt != 0)
        ans += (cnt * (cnt + 1) / 2);

    return ans;
}

// Driver code
static public void Main(string[] args)
{
    string s = "geeksforgeeks";

    Console.Write(CountTotal(s));
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

    // Javascript program to count all substrings
    // in a string which contains only vowels

    // Function to check vowel or not
    function isvowel(x)
    {
        return (x == 'a' || x == 'e' ||
                x == 'i' || x == 'o' ||
                x == 'u');
    }

    // Function to find largest
    // string which satisfy condition
    function CountTotal(str)
    {
        let ans = 0;
        let n = str.length;
        let s = str.split('');
        let cnt = 0;

        for(let i = 0; i < n; i++)
        {

           // Check if current character
           // is vowel
           if (isvowel(s[i]))

               // Increment count
               cnt += 1;
           else
           {

               // Count all possible
               // substrings of calculated
               // length
               ans += (cnt * (cnt + 1) / 2);

               // Reset the length
               cnt = 0;
           }
        }

        // Add remaining possible
        // substrings consisting
        // of vowels occupying
        // last indices of the string
        if (cnt != 0)
            ans += (cnt * (cnt + 1) / 2);

        return ans;
    }

    let s = "geeksforgeeks";

    document.write(CountTotal(s));

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*T4】