# 通过插入给定的字符

使字符串成为非回文字符串

> 原文:[https://www . geesforgeks . org/make-a-string-非回文-通过插入给定字符/](https://www.geeksforgeeks.org/make-a-string-non-palindromic-by-inserting-a-given-character/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和一个字符 **X** ，任务是通过在字符串 **S** 中插入字符 **X** 来生成一个非回文字符串。如果无法获得非回文字符串，则打印 **"-1"** 。

**示例:**

> **输入:**S =“ababab”，X =‘a’
> **输出:**“aababab”
> **解释:**在字符串 S 开头插入字符‘a’将字符串修饰为“aababab”，为非回文。
> 
> **输入:** S = "rrr "，X = 'r'
> **输出:** -1

**方法:**给定的问题可以基于以下观察来解决:如果字符串只包含字符 **X** ，那么不可能使字符串非回文。否则，字符串可以变成非回文。按照以下步骤解决问题:

1.  如果字符串 S 中字符 X 的[计数与字符串 S](https://www.geeksforgeeks.org/count-occurrences-of-a-character-in-a-repeated-string/) 的[长度相同，则打印**-1”**。](https://www.geeksforgeeks.org/c-program-to-find-the-length-of-a-string/)
2.  否则，检查[字符串 **S** 和字符 **X** 的连接是否为回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。如果发现**为真**，则打印字符串 **S + X** 。否则打印 **(X + S)** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// string is palindromic or not
bool Palindrome(string str)
{
    // Traverse the string str
    for (int i = 0, j = str.length() - 1;
         i < j; i++, j--) {

        // Check if i-th character from
        // both ends are the same or not
        if (str[i] != str[j])
            return false;
    }

    // Return true, as str is palindrome
    return true;
}

// Function to make the non-palindromic
// string by inserting the character X
void NonPalindrome(string str, char X)
{

    // If all the characters
    // in the string are X
    if (count(str.begin(), str.end(), X)
        == str.length()) {

        cout << "-1";
        return;
    }

    // Check if X + str is
    // palindromic or not
    if (Palindrome(X + str))
        cout << str + X << endl;
    else
        cout << X + str << endl;
}

// Driver Code
int main()
{
    string S = "geek";
    char X = 's';
    NonPalindrome(S, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to check if a
    // string is palindromic or not
    static boolean Palindrome(String str)
    {
        // Traverse the string str
        for (int i = 0, j = str.length() - 1; i < j;
             i++, j--) {

            // Check if i-th character from
            // both ends are the same or not
            if (str.charAt(i) != str.charAt(j))
                return false;
        }

        // Return true, as str is palindrome
        return true;
    }

    // Function to make the non-palindromic
    // string by inserting the character X
    static void NonPalindrome(String str, char X)
    {

        // stores the count of char X in str
        int count = 0;
        for (int i = 0; i < str.length(); i++)
            if (str.charAt(i) == X)
                count++;

        // If all the characters
        // in the string are X
        if (count == str.length()) {

            System.out.println("-1");
            return;
        }

        // Check if X + str is
        // palindromic or not
        if (Palindrome(X + str))
            System.out.println(str + X);
        else
            System.out.println(X + str);
    }

    // Driver Code
    public static void main(String[] args)
    {

        String S = "geek";
        char X = 's';
        NonPalindrome(S, X);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if a
# string is palindromic or not
def Palindrome(str):

    if str == str[::-1]:
        return True

    # Return true, as str is palindrome
    return False

# Function to make the non-palindromic
# string by inserting the character X
def NonPalindrome(str, X):

    # If all the characters
    # in the string are X
    if (str.count(X) == len(str)):
        print("-1")
        return

    # Check if X + str is
    # palindromic or not
    if (Palindrome(X + str)):
        print(str + X)
    else:
        print(X + str)

# Driver Code
if __name__ == '__main__':

    S = "geek"
    X = 's'

    NonPalindrome(S, X)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach

using System;
using System.Linq;
class GFG {
    // Function to check if a
    // string is palindromic or not
    static bool Palindrome(string str)
    {
        // Traverse the string str
        for (int i = 0, j = str.Length - 1; i < j;
             i++, j--) {

            // Check if i-th character from
            // both ends are the same or not
            if (str[i] != str[j])
                return false;
        }

        // Return true, as str is palindrome
        return true;
    }

    // Function to make the non-palindromic
    // string by inserting the character X
    static void NonPalindrome(string str, char X)
    {

        // If all the characters
        // in the string are X
        if (str.Count(p => p == X) == str.Length) {

            Console.Write("-1");
            return;
        }

        // Check if X + str is
        // palindromic or not
        if (Palindrome(X + str))
            Console.WriteLine(str + X);
        else
            Console.WriteLine(X + str);
    }

    // Driver Code
    public static void Main()
    {
        string S = "geek";
        char X = 's';
        NonPalindrome(S, X);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to check if a
// string is palindromic or not
function Palindrome( str)
{
    // Traverse the string str
    for (let i = 0, j = str.length - 1; i < j;
        i++, j--) {

        // Check if i-th character from
        // both ends are the same or not
        if (str.charAt(i) != str.charAt(j))
            return false;
    }

    // Return true, as str is palindrome
    return true;
}

// Function to make the non-palindromic
// string by inserting the character X
function NonPalindrome( str, X)
{

    // stores the count of char X in str
    var count = 0;
    for (let i = 0; i < str.length; i++)
        if (str.charAt(i) == X)
            count++;

    // If all the characters
    // in the string are X
    if (count == str.length) {

        document.write("-1");
        return;
    }

    // Check if X + str is
    // palindromic or not
    if (Palindrome(X + str))
        document.write(str + X);
    else
        document.write(X + str);
}

// Driver Code

var S = "geek";
var X = 's';
NonPalindrome(S, X);

</script>
```

**输出:**

```
sgeek
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)