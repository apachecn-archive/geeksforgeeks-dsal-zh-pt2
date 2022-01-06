# 最长回文子串|集合 1

> 原文:[https://www . geesforgeks . org/long-回文-substring-set-1/](https://www.geeksforgeeks.org/longest-palindrome-substring-set-1/)

给定一个字符串，找出最长的子字符串，即回文。

**例如**

```
Input: Given string :"forgeeksskeegfor", 
Output: "geeksskeeg"

Input: Given string :"Geeks", 
Output: "ee"
```

**<u>法一</u> :** 蛮力。
**方法:**简单的方法是检查每个子串是否是回文。要做到这一点，首先运行三个嵌套循环，外部两个循环通过固定角字符逐个挑选所有子串，内部循环检查挑选的子串是否是回文。

## C++

```
// A C++ solution for longest palindrome
#include <bits/stdc++.h>
using namespace std;

// Function to print a substring str[low..high]
void printSubStr(string str, int low, int high)
{
    for (int i = low; i <= high; ++i)
        cout << str[i];
}

// This function prints the
// longest palindrome substring
// It also returns the length
// of the longest palindrome
int longestPalSubstr(string str)
{
    // get length of input string
    int n = str.size();

    // All substrings of length 1
    // are palindromes
    int maxLength = 1, start = 0;

    // Nested loop to mark start and end index
    for (int i = 0; i < str.length(); i++) {
        for (int j = i; j < str.length(); j++) {
            int flag = 1;

            // Check palindrome
            for (int k = 0; k < (j - i + 1) / 2; k++)
                if (str[i + k] != str[j - k])
                    flag = 0;

            // Palindrome
            if (flag && (j - i + 1) > maxLength) {
                start = i;
                maxLength = j - i + 1;
            }
        }
    }

    cout << "Longest palindrome substring is: ";
    printSubStr(str, start, start + maxLength - 1);

    // return length of LPS
    return maxLength;
}

// Driver Code
int main()
{
    string str = "forgeeksskeegfor";
    cout << "\nLength is: "
         << longestPalSubstr(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java solution for longest palindrome
import java.util.*;

class GFG{

// Function to print a subString str[low..high]
static void printSubStr(String str, int low, int high)
{
    for (int i = low; i <= high; ++i)
        System.out.print(str.charAt(i));
}

// This function prints the
// longest palindrome subString
// It also returns the length
// of the longest palindrome
static int longestPalSubstr(String str)
{
    // get length of input String
    int n = str.length();

    // All subStrings of length 1
    // are palindromes
    int maxLength = 1, start = 0;

    // Nested loop to mark start and end index
    for (int i = 0; i < str.length(); i++) {
        for (int j = i; j < str.length(); j++) {
            int flag = 1;

            // Check palindrome
            for (int k = 0; k < (j - i + 1) / 2; k++)
                if (str.charAt(i + k) != str.charAt(j - k))
                    flag = 0;

            // Palindrome
            if (flag!=0 && (j - i + 1) > maxLength) {
                start = i;
                maxLength = j - i + 1;
            }
        }
    }

    System.out.print("Longest palindrome subString is: ");
    printSubStr(str, start, start + maxLength - 1);

    // return length of LPS
    return maxLength;
}

// Driver Code
public static void main(String[] args)
{
    String str = "forgeeksskeegfor";
    System.out.print("\nLength is: "
         + longestPalSubstr(str));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# A Python3 solution for longest palindrome

# Function to pra subString str[low..high]
def printSubStr(str, low, high):

    for i in range(low, high + 1):
        print(str[i], end = "")

# This function prints the
# longest palindrome subString
# It also returns the length
# of the longest palindrome
def longestPalSubstr(str):

    # Get length of input String
    n = len(str)

    # All subStrings of length 1
    # are palindromes
    maxLength = 1
    start = 0

    # Nested loop to mark start
    # and end index
    for i in range(n):
        for j in range(i, n):
            flag = 1

            # Check palindrome
            for k in range(0, ((j - i) // 2) + 1):
                if (str[i + k] != str[j - k]):
                    flag = 0

            # Palindrome
            if (flag != 0 and (j - i + 1) > maxLength):
                start = i
                maxLength = j - i + 1

    print("Longest palindrome subString is: ", end = "")
    printSubStr(str, start, start + maxLength - 1)

    # Return length of LPS
    return maxLength

# Driver Code
if __name__ == '__main__':

    str = "forgeeksskeegfor"

    print("\nLength is: ", longestPalSubstr(str))

# This code is contributed by 29AjayKumar
```

## C#

```
// A C# solution for longest palindrome
using System;

class GFG{

// Function to print a subString str[low..high]
static void printSubStr(String str, int low, int high)
{
    for (int i = low; i <= high; ++i)
        Console.Write(str[i]);
}

// This function prints the
// longest palindrome subString
// It also returns the length
// of the longest palindrome
static int longestPalSubstr(String str)
{
    // get length of input String
    int n = str.Length;

    // All subStrings of length 1
    // are palindromes
    int maxLength = 1, start = 0;

    // Nested loop to mark start and end index
    for (int i = 0; i < str.Length; i++) {
        for (int j = i; j < str.Length; j++) {
            int flag = 1;

            // Check palindrome
            for (int k = 0; k < (j - i + 1) / 2; k++)
                if (str[i + k] != str[j - k])
                    flag = 0;

            // Palindrome
            if (flag!=0 && (j - i + 1) > maxLength) {
                start = i;
                maxLength = j - i + 1;
            }
        }
    }

    Console.Write("longest palindrome subString is: ");
    printSubStr(str, start, start + maxLength - 1);

    // return length of LPS
    return maxLength;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "forgeeksskeegfor";
    Console.Write("\nLength is: "
         + longestPalSubstr(str));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// A Javascript solution for longest palindrome

// Function to print a subString str[low..high]
function printSubStr(str,low,high)
{
    for (let i = low; i <= high; ++i)
        document.write(str[i]);
}

// This function prints the
// longest palindrome subString
// It also returns the length
// of the longest palindrome
function longestPalSubstr(str)
{
    // get length of input String
    let n = str.length;

    // All subStrings of length 1
    // are palindromes
    let maxLength = 1, start = 0;

    // Nested loop to mark start and end index
    for (let i = 0; i < str.length; i++) {
        for (let j = i; j < str.length; j++) {
            let flag = 1;

            // Check palindrome
            for (let k = 0; k < (j - i + 1) / 2; k++)
                if (str[i + k] != str[j - k])
                    flag = 0;

            // Palindrome
            if (flag!=0 && (j - i + 1) > maxLength) {
                start = i;
                maxLength = j - i + 1;
            }
        }
    }

    document.write("Longest palindrome subString is: ");
    printSubStr(str, start, start + maxLength - 1);

    // return length of LPS
    return maxLength;
}

// Driver Code
let str = "forgeeksskeegfor";
document.write("<br>Length is: "
         + longestPalSubstr(str));

// This code is contributed by rag2127
</script>
```

**输出:**

```
Longest palindrome subString is: geeksskeeg
Length is:  10
```

**复杂度分析:**

*   **时间复杂度:** O(n^3).
    该方法需要三个嵌套循环来寻找最长的回文子串，因此时间复杂度为 O(n^3).
*   **辅助复杂度** : O(1)。
    因为不需要额外的空间。

**<u>方法二</u> :** 动态规划。
**方法:**通过存储子问题的结果，可以降低时间复杂度。想法和[这个](https://www.geeksforgeeks.org/archives/19155)帖子差不多。

1.  维护一个自下而上填充的布尔表[n][n]。
2.  如果子串是回文，则表[i][j]的值为真，否则为假。
3.  要计算表[i][j]，请检查表[i+1][j-1]的值，如果该值为真，并且 str[i]与 str[j]相同，则我们使表[i][j]为真。
4.  否则，表[i][j]的值为假。
5.  我们之前必须为长度= 1 和长度=2 的子串填充表，因为
    正如我们正在发现的，如果表[i+1][j-1]是真或假，那么在
    的情况下(I)长度== 1，假设 i=2，j=2 和 i+1，j-1 不在[i，j]
    之间(ii)长度== 2，假设 i=2，j=3 和 i+1，j-1 也不在[i，j]之间。

![](img/4cb5e10872567c423c92b61512042791.png)

下面是上述方法的实现:

## C++

```
// A C++ dynamic programming
// solution for longest palindrome

#include <bits/stdc++.h>
using namespace std;

// Function to print a substring
// str[low..high]
void printSubStr(
    string str, int low, int high)
{
    for (int i = low; i <= high; ++i)
        cout << str[i];
}

// This function prints the
// longest palindrome substring
// It also returns the length of
// the longest palindrome
int longestPalSubstr(string str)
{
    // get length of input string
    int n = str.size();

    // table[i][j] will be false if substring
    // str[i..j] is not palindrome.
    // Else table[i][j] will be true
    bool table[n][n];

    memset(table, 0, sizeof(table));

    // All substrings of length 1
    // are palindromes
    int maxLength = 1;

    for (int i = 0; i < n; ++i)
        table[i][i] = true;

    // check for sub-string of length 2.
    int start = 0;
    for (int i = 0; i < n - 1; ++i) {
        if (str[i] == str[i + 1]) {
            table[i][i + 1] = true;
            start = i;
            maxLength = 2;
        }
    }

    // Check for lengths greater than 2.
    // k is length of substring
    for (int k = 3; k <= n; ++k) {
        // Fix the starting index
        for (int i = 0; i < n - k + 1; ++i) {
            // Get the ending index of substring from
            // starting index i and length k
            int j = i + k - 1;

            // checking for sub-string from ith index to
            // jth index iff str[i+1] to str[j-1] is a
            // palindrome
            if (table[i + 1][j - 1] && str[i] == str[j]) {
                table[i][j] = true;

                if (k > maxLength) {
                    start = i;
                    maxLength = k;
                }
            }
        }
    }

    cout << "Longest palindrome substring is: ";
    printSubStr(str, start, start + maxLength - 1);

    // return length of LPS
    return maxLength;
}

// Driver Code
int main()
{
    string str = "forgeeksskeegfor";
    cout << "\nLength is: "
         << longestPalSubstr(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Solution
public class LongestPalinSubstring {
    // A utility function to print
    // a substring str[low..high]
    static void printSubStr(
        String str, int low, int high)
    {
        System.out.println(
            str.substring(
                low, high + 1));
    }

    // This function prints the longest
    // palindrome substring of str[].
    // It also returns the length of the
    // longest palindrome
    static int longestPalSubstr(String str)
    {
        // get length of input string
        int n = str.length();

        // table[i][j] will be false if
        // substring str[i..j] is not palindrome.
        // Else table[i][j] will be true
        boolean table[][] = new boolean[n][n];

        // All substrings of length 1 are palindromes
        int maxLength = 1;
        for (int i = 0; i < n; ++i)
            table[i][i] = true;

        // check for sub-string of length 2.
        int start = 0;
        for (int i = 0; i < n - 1; ++i) {
            if (str.charAt(i) == str.charAt(i + 1)) {
                table[i][i + 1] = true;
                start = i;
                maxLength = 2;
            }
        }

        // Check for lengths greater than 2.
        // k is length of substring
        for (int k = 3; k <= n; ++k) {

            // Fix the starting index
            for (int i = 0; i < n - k + 1; ++i) {
                // Get the ending index of substring from
                // starting index i and length k
                int j = i + k - 1;

                // checking for sub-string from ith index to
                // jth index iff str.charAt(i+1) to
                // str.charAt(j-1) is a palindrome
                if (table[i + 1][j - 1]
                    && str.charAt(i) == str.charAt(j)) {
                    table[i][j] = true;

                    if (k > maxLength) {
                        start = i;
                        maxLength = k;
                    }
                }
            }
        }
        System.out.print("Longest palindrome substring is; ");
        printSubStr(str, start,
                    start + maxLength - 1);

        // return length of LPS
        return maxLength;
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {

        String str = "forgeeksskeegfor";
        System.out.println("Length is: " + longestPalSubstr(str));
    }
}

// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program

import sys

# A utility function to print a
# substring str[low..high]
def printSubStr(st, low, high) :
    sys.stdout.write(st[low : high + 1])
    sys.stdout.flush()
    return ''

# This function prints the longest palindrome
# substring of st[]. It also returns the length
# of the longest palindrome
def longestPalSubstr(st) :
    n = len(st) # get length of input string

    # table[i][j] will be false if substring
    # str[i..j] is not palindrome. Else
    # table[i][j] will be true
    table = [[0 for x in range(n)] for y
                          in range(n)]

    # All substrings of length 1 are
    # palindromes
    maxLength = 1
    i = 0
    while (i < n) :
        table[i][i] = True
        i = i + 1

    # check for sub-string of length 2.
    start = 0
    i = 0
    while i < n - 1 :
        if (st[i] == st[i + 1]) :
            table[i][i + 1] = True
            start = i
            maxLength = 2
        i = i + 1

    # Check for lengths greater than 2.
    # k is length of substring
    k = 3
    while k <= n :
        # Fix the starting index
        i = 0
        while i < (n - k + 1) :

            # Get the ending index of
            # substring from starting
            # index i and length k
            j = i + k - 1

            # checking for sub-string from
            # ith index to jth index iff
            # st[i + 1] to st[(j-1)] is a
            # palindrome
            if (table[i + 1][j - 1] and
                      st[i] == st[j]) :
                table[i][j] = True

                if (k > maxLength) :
                    start = i
                    maxLength = k
            i = i + 1
        k = k + 1
    print "Longest palindrome substring is: ", printSubStr(st, start,
                                               start + maxLength - 1)

    return maxLength # return length of LPS

# Driver program to test above functions
st = "forgeeksskeegfor"
l = longestPalSubstr(st)
print "Length is:", l

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Solution
using System;

class GFG {

    // A utility function to print a
    // substring str[low...( high - (low+1))]
    static void printSubStr(string str, int low,
                            int high)
    {
        Console.WriteLine(str.Substring(low,
                                        high - low + 1));
    }

    // This function prints the longest
    // palindrome substring of str[].
    // It also returns the length of the
    // longest palindrome
    static int longestPalSubstr(string str)
    {

        // Get length of input string
        int n = str.Length;

        // Table[i, j] will be false if substring
        // str[i..j] is not palindrome. Else
        // table[i, j] will be true
        bool[, ] table = new bool[n, n];

        // All substrings of length 1 are palindromes
        int maxLength = 1;
        for (int i = 0; i < n; ++i)
            table[i, i] = true;

        // Check for sub-string of length 2.
        int start = 0;

        for (int i = 0; i < n - 1; ++i) {
            if (str[i] == str[i + 1]) {
                table[i, i + 1] = true;
                start = i;
                maxLength = 2;
            }
        }

        // Check for lengths greater than 2.
        // k is length of substring
        for (int k = 3; k <= n; ++k) {

            // Fix the starting index
            for (int i = 0; i < n - k + 1; ++i) {

                // Get the ending index of substring from
                // starting index i and length k
                int j = i + k - 1;

                // Checking for sub-string from ith index
                // to jth index iff str.charAt(i+1) to
                // str.charAt(j-1) is a palindrome
                if (table[i + 1, j - 1] && str[i] == str[j]) {
                    table[i, j] = true;
                    if (k > maxLength) {
                        start = i;
                        maxLength = k;
                    }
                }
            }
        }
        Console.Write("Longest palindrome substring is: ");
        printSubStr(str, start, start + maxLength - 1);

        // Return length of LPS
        return maxLength;
    }

    // Driver code
    public static void Main(string[] args)
    {
        string str = "forgeeksskeegfor";

        Console.WriteLine("Length is: " + longestPalSubstr(str));
    }
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>
// Javascript Solution

    // A utility function to print
    // a substring str[low..high]
   function printSubStr(str,low,high)
   {
           document.write(
            str.substring(
                low, high + 1)+"<br>");
   }

   // This function prints the longest
    // palindrome substring of str[].
    // It also returns the length of the
    // longest palindrome
   function longestPalSubstr(str)
   {

           // get length of input string
        let n = str.length;

        // table[i][j] will be false if
        // substring str[i..j] is not palindrome.
        // Else table[i][j] will be true
        let table = new Array(n);
        for(let i = 0; i < n; i++)
        {
            table[i] = new Array(n);
        }

        // All substrings of length 1 are palindromes
        let maxLength = 1;
        for (let i = 0; i < n; ++i)
            table[i][i] = true;

        // check for sub-string of length 2.
        let start = 0;
        for (let i = 0; i < n - 1; ++i)
        {
            if (str[i] == str[i + 1])
            {
                table[i][i + 1] = true;
                start = i;
                maxLength = 2;
            }
        }

        // Check for lengths greater than 2.
        // k is length of substring
        for (let k = 3; k <= n; ++k) {

            // Fix the starting index
            for (let i = 0; i < n - k + 1; ++i)
            {

                // Get the ending index of substring from
                // starting index i and length k
                let j = i + k - 1;

                // checking for sub-string from ith index to
                // jth index iff str.charAt(i+1) to
                // str.charAt(j-1) is a palindrome
                if (table[i + 1][j - 1]
                    && str[i] == str[j]) {
                    table[i][j] = true;

                    if (k > maxLength) {
                        start = i;
                        maxLength = k;
                    }
                }
            }
        }
        document.write("Longest palindrome substring is; ");
        printSubStr(str, start,
                    start + maxLength - 1);

        // return length of LPS
        return maxLength;
   }

   // Driver program to test above functions
   let str = "forgeeksskeegfor";
   document.write("Length is: " + longestPalSubstr(str));

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Longest palindrome substring is: geeksskeeg
Length is: 10
```

**复杂度分析:**

*   **时间复杂度** : O(n^2).
    需要两个嵌套遍历。
*   **辅助空间** : O(n^2).
    需要 n*n 大小的矩阵来存储 dp 数组。

在 [Set-2](https://www.geeksforgeeks.org/longest-palindromic-substring-set-2/) 中可以找到更好的空间复杂度方法。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。