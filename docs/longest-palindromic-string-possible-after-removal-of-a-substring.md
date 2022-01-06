# 去除子串后可能的最长回文串

> 原文:[https://www . geeksforgeeks . org/最长回文字符串-删除子字符串后可能出现的情况/](https://www.geeksforgeeks.org/longest-palindromic-string-possible-after-removal-of-a-substring/)

给定一个字符串 **str** ，任务是在去掉一个子串后，从中找出能得到的最长回文串。

**示例:**

> **输入:**str = " abcdefghiedba "
> **输出:**【abcdefedcba "
> **解释:**去除子串“fgh”会留下剩余的字符串回文
> 
> **输入:** str = "abba"
> **输出:**【ABBA "
> **解释:**去除子串""，因为给定的字符串已经是回文了。

**进场:**

*   从给定字符串的两端找到可能最长的子字符串对 **A** 和 **B** ，它们是彼此相反的。
*   从原始字符串中删除它们。
*   使用 KMP 从剩余字符串的两端找到最长的回文子字符串，并考虑较长的子字符串。
*   将字符串 **A** 和 **B** 分别添加到该回文子串的开头和结尾，以获得所需的输出。

下面的代码是上述方法的实现:

## C++

```
// C++ Implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;
// Function to find the longest palindrome
// from the start of the string using KMP match
string findPalindrome(string C)
{
    string S = C;
    reverse(S.begin(), S.end());
    // Append S(reverse of C)  to C
    C = C + "&" + S;
    int n = C.length();
    int longestPalindrome[n];
    longestPalindrome[0] = 0;
    int len = 0;
    int i = 1;
    // Use KMP algorithm
    while (i < n) {
        if (C[i] == C[len]) {
            len++;
            longestPalindrome[i] = len;
            i++;
        }
        else {
            if (len != 0) {
                len = longestPalindrome[len - 1];
            }
            else {
                longestPalindrome[i] = 0;
                i++;
            }
        }
    }
    string ans = C.substr(0, longestPalindrome[n - 1]);
    return ans;
}

// Function to return longest palindromic
// string possible from the given string
// after removal of any substring
string findAns(string s)
{
    // Initialize three strings A, B AND F
    string A = "";
    string B = "";
    string F = "";

    int i = 0;
    int j = s.length() - 1;
    int len = s.length();

    // Loop to find longest substrings
    // from both ends which are
    // reverse of each other
    while (i < j && s[i] == s[j]) {
        i = i + 1;
        j = j - 1;
    }

    if (i > 0)
    {
        A = s.substr(0, i);
        B = s.substr(len - i, i);
    }

    // Proceed to third step of our approach
    if (len > 2 * i)
    {
        // Remove the substrings A and B
        string C = s.substr(i, s.length() - 2 * i);
        // Find the longest palindromic
        // substring from beginning of C
        string D = findPalindrome(C);

        // Find the longest palindromic
        // substring from end of C
        reverse(C.begin(), C.end());
        string E = findPalindrome(C);

        // Store the maximum of D and E in F
        if (D.length() > E.length()) {
            F = D;
        }
        else {
            F = E;
        }
    }

    // Find the final answer
    string answer = A + F + B;

    return answer;
}
// Driver Code
int main()
{
    string str = "abcdefghiedcba";
    cout << findAns(str) << endl;

}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of the
// above approach
import java.util.*;

class GFG{

// Function to find the longest palindrome
// from the start of the String using KMP match
static String findPalindrome(String C)
{
    String S = C;
    S = reverse(S);

    // Append S(reverse of C) to C
    C = C + "&" + S;
    int n = C.length();
    int []longestPalindrome = new int[n];
    longestPalindrome[0] = 0;
    int len = 0;
    int i = 1;

    // Use KMP algorithm
    while (i < n) {
        if (C.charAt(i) == C.charAt(len)) {
            len++;
            longestPalindrome[i] = len;
            i++;
        }
        else {
            if (len != 0) {
                len = longestPalindrome[len - 1];
            }
            else {
                longestPalindrome[i] = 0;
                i++;
            }
        }
    }
    String ans = C.substring(0, longestPalindrome[n - 1]);
    return ans;
}

// Function to return longest palindromic
// String possible from the given String
// after removal of any subString
static String findAns(String s)
{
    // Initialize three Strings A, B AND F
    String A = "";
    String B = "";
    String F = "";

    int i = 0;
    int j = s.length() - 1;
    int len = s.length();

    // Loop to find longest subStrings
    // from both ends which are
    // reverse of each other
    while (i < j && s.charAt(i) == s.charAt(j)) {
        i = i + 1;
        j = j - 1;
    }

    if (i > 0)
    {
        A = s.substring(0, i);
        B = s.substring(len - i, len);
    }

    // Proceed to third step of our approach
    if (len > 2 * i)
    {
        // Remove the subStrings A and B
        String C = s.substring(i, (s.length() - 2 * i) + i);

        // Find the longest palindromic
        // subString from beginning of C
        String D = findPalindrome(C);

        // Find the longest palindromic
        // subString from end of C
        C = reverse(C);
        String E = findPalindrome(C);

        // Store the maximum of D and E in F
        if (D.length() > E.length()) {
            F = D;
        }
        else {
            F = E;
        }
    }

    // Find the final answer
    String answer = A + F + B;

    return answer;
}
static String reverse(String input) {
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.valueOf(a);
}

// Driver Code
public static void main(String[] args)
{
    String str = "abcdefghiedcba";
    System.out.print(findAns(str) +"\n");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to find the longest
# palindrome from the start of
# the string using KMP match
def findPalindrome(C):

    S = C[::-1]

    # Append S(reverse of C)  to C
    C = C[:] + '&' + S

    n = len(C)
    longestPalindrome = [0 for i in range(n)]
    longestPalindrome[0] = 0

    ll = 0
    i = 1

    # Use KMP algorithm
    while (i < n):
        if (C[i] == C[ll]):
            ll += 1
            longestPalindrome[i] = ll
            i += 1

        else:

            if (ll != 0):
                ll = longestPalindrome[ll - 1]
            else:
                longestPalindrome[i] = 0
                i += 1

    ans = C[0:longestPalindrome[n - 1]]

    return ans

# Function to return longest palindromic
# string possible from the given string
# after removal of any substring
def findAns(s):

    # Initialize three strings
    # A, B AND F
    A = ""
    B = ""
    F = ""

    i = 0
    j = len(s) - 1
    ll = len(s)

    # Loop to find longest substrings
    # from both ends which are 
    # reverse of each other
    while (i < j and s[i] == s[j]):
        i = i + 1
        j = j - 1

    if (i > 0):
        A = s[0 : i]
        B = s[ll - i : ll]

    # Proceed to third step of our approach
    if (ll > 2 * i): 

        # Remove the substrings A and B
        C = s[i : i + (len(s) - 2 * i)]

        # Find the longest palindromic
        # substring from beginning of C
        D = findPalindrome(C)

        # Find the longest palindromic
        # substring from end of C
        C = C[::-1]

        E = findPalindrome(C)

        # Store the maximum of D and E in F
        if (len(D) > len(E)):
            F = D
        else:
            F = E

    # Find the final answer
    answer = A + F + B

    return answer

# Driver code
if __name__=="__main__":

    str = "abcdefghiedcba"

    print(findAns(str))

# This code is contributed by rutvik_56
```

## C#

```
// C# Implementation of the
// above approach
using System;

class GFG{

// Function to find the longest palindrome
// from the start of the String using KMP match
static String findPalindrome(String C)
{
    String S = C;
    S = reverse(S);

    // Append S(reverse of C) to C
    C = C + "&" + S;
    int n = C.Length;
    int []longestPalindrome = new int[n];
    longestPalindrome[0] = 0;
    int len = 0;
    int i = 1;

    // Use KMP algorithm
    while (i < n) {
        if (C[i] == C[len]) {
            len++;
            longestPalindrome[i] = len;
            i++;
        }
        else {
            if (len != 0) {
                len = longestPalindrome[len - 1];
            }
            else {
                longestPalindrome[i] = 0;
                i++;
            }
        }
    }
    String ans = C.Substring(0, longestPalindrome[n - 1]);
    return ans;
}

// Function to return longest palindromic
// String possible from the given String
// after removal of any subString
static String findAns(String s)
{
    // Initialize three Strings A, B AND F
    String A = "";
    String B = "";
    String F = "";

    int i = 0;
    int j = s.Length - 1;
    int len = s.Length;

    // Loop to find longest subStrings
    // from both ends which are
    // reverse of each other
    while (i < j && s[i] == s[j]) {
        i = i + 1;
        j = j - 1;
    }

    if (i > 0)
    {
        A = s.Substring(0, i);
        B = s.Substring(len - i, i);
    }

    // Proceed to third step of our approach
    if (len > 2 * i)
    {
        // Remove the subStrings A and B
        String C = s.Substring(i, (s.Length - 2 * i));

        // Find the longest palindromic
        // subString from beginning of C
        String D = findPalindrome(C);

        // Find the longest palindromic
        // subString from end of C
        C = reverse(C);
        String E = findPalindrome(C);

        // Store the maximum of D and E in F
        if (D.Length > E.Length) {
            F = D;
        }
        else {
            F = E;
        }
    }

    // Find the readonly answer
    String answer = A + F + B;

    return answer;
}
static String reverse(String input) {
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("",a);
}

// Driver Code
public static void Main(String[] args)
{
    String str = "abcdefghiedcba";
    Console.Write(findAns(str) +"\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
      // JavaScript Implementation of the
      // above approach
      // Function to find the longest palindrome
      // from the start of the String using KMP match
      function findPalindrome(C) {
        var S = C;
        S = reverse(S);

        // Append S(reverse of C) to C
        C = C + "&" + S;
        var n = C.length;
        var longestPalindrome = new Array(n).fill(0);
        longestPalindrome[0] = 0;
        var len = 0;
        var i = 1;

        // Use KMP algorithm
        while (i < n) {
          if (C[i] === C[len]) {
            len++;
            longestPalindrome[i] = len;
            i++;
          } else {
            if (len !== 0) {
              len = longestPalindrome[len - 1];
            } else {
              longestPalindrome[i] = 0;
              i++;
            }
          }
        }
        var ans = C.substring(0, longestPalindrome[n - 1]);
        return ans;
      }

      // Function to return longest palindromic
      // String possible from the given String
      // after removal of any subString
      function findAns(s) {
        // Initialize three Strings A, B AND F
        var A = "";
        var B = "";
        var F = "";

        var i = 0;
        var j = s.length - 1;
        var len = s.length;

        // Loop to find longest subStrings
        // from both ends which are
        // reverse of each other
        while (i < j && s[i] === s[j]) {
          i = i + 1;
          j = j - 1;
        }

        if (i > 0) {
          A = s.substring(0, i);
          B = s.substring(len - i, len);
        }

        // Proceed to third step of our approach
        if (len > 2 * i) {
          // Remove the subStrings A and B
          var C = s.substring(i, i + (s.length - 2 * i));

          // Find the longest palindromic
          // subString from beginning of C
          var D = findPalindrome(C);

          // Find the longest palindromic
          // subString from end of C
          C = reverse(C);
          var E = findPalindrome(C);

          // Store the maximum of D and E in F
          if (D.length > E.length) {
            F = D;
          } else {
            F = E;
          }
        }

        // Find the readonly answer
        var answer = A + F + B;

        return answer;
      }

      function reverse(input) {
        var a = input.split("");
        var r = a.length - 1;
        for (var l = 0; l < r; l++, r--) {
          var temp = a[l];
          a[l] = a[r];
          a[r] = temp;
        }
        return a.join("");
      }

      // Driver Code
      var str = "abcdefghiedcba";
      document.write(findAns(str));

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
abcdeiedcba
```

**时间复杂度:**O(N)
T3】辅助空间 : O(N)