# 由前缀和后缀串联而成的字符串中最长的回文

> 原文:[https://www . geesforgeks . org/通过串联其前缀和后缀形成的最长字符串回文/](https://www.geeksforgeeks.org/longest-palindrome-in-a-string-formed-by-concatenating-its-prefix-and-suffix/)

给定一个由小写英文字母组成的字符串 **str** ，任务是找到满足以下条件的最长回文字符串 T:

*   **T = p + m + s** 其中 **p** 和 **s** 分别是给定字符串的前缀和后缀，字符串 **m** 是去掉 p 和 s 后字符串的前缀或后缀。
*   由 p 和 s 连接而成的字符串本身就是回文。
*   字符串 p 和 s 都可以是空字符串。

**例:**

> **输入:**str = " abcdfdecba "
> **输出:**abcdfdba
> **解释:**
> 这里，p = " ABC "
> s = " CBA "
> m = "dfd "
> p+s = " abcba "是回文，m = " DFD "是从字符串中去掉前缀和后缀后的前缀。因此，T =“abcddcba”。
> **输入:**str = " geeks forgeeks "
> **输出:** g
> **解释:**
> 这里，p = "
> s = " g "
> m = "
> p+s = "，这是一个回文，m = "g "是从字符串中去掉前缀和后缀后的前缀。因此，T =“g”。

**做法:**这个问题的思路是把答案分成三个部分，这样就会有一部分给定串的后缀和前缀一起组成回文，这就形成了答案串的开头和结尾。现在，从给定的字符串中删除这些前缀和后缀后，我们可以找到最大长度的后缀或前缀字符串(我们可以称之为 midPalindrome)，它是回文。
因此，答案串由
给出

```
answer = prefix + midPalindrome + suffix
```

可以按照以下步骤计算问题的答案:

*   找出字符串的后缀和前缀一起组成回文的长度。
*   从**字符串**中删除已经形成回文的后缀和前缀子字符串，并将其存储在单独的字符串中。
*   检查剩余字符串中的所有前缀和后缀子字符串，找到最长的字符串。
*   最后，将答案的三个部分结合起来并返回。

以下是上述方法的实现:

## C++

```
// C++ program to find the longest
// palindrome in a string formed by
// concatenating its prefix and suffix

#include <bits/stdc++.h>
using namespace std;

// Function to check whether
// the string is a palindrome
bool isPalindrome(string r)
{
    string p = r;

    // Reverse the string to
    // compare with the
    // original string
    reverse(p.begin(), p.end());

    // Check if both are same
    return (r == p);
}

// Function to find the longest
// palindrome in a string formed by
// concatenating its prefix and suffix
string PrefixSuffixPalindrome(string str)
{
    // Length of the string
    int n = str.size(), len = 0;

    // Finding the length upto which
    // the suffix and prefix forms a
    // palindrome together
    for (int i = 0; i < n / 2; i++) {
        if (str[i] != str[n - i - 1]) {
            len = i;
            break;
        }
    }

    // Check whether the string
    // has prefix and suffix substrings
    // which are palindromes.
    string prefix = "", suffix = "";
    string midPal = "";

    // Removing the suffix and prefix
    // substrings which already forms
    // a palindrome and storing them
    // in separate strings
    prefix = str.substr(0, len);
    suffix = str.substr(n - len);
    str = str.substr(len, n - 2 * len);

    // Check all prefix substrings
    // in the remaining string str
    for (int i = 1; i <= str.size(); i++) {
        string y = str.substr(0, i);

        // Check if the prefix substring
        // is a palindrome
        if (isPalindrome(y)) {

            // If the prefix substring
            // is a palindrome then check
            // if it is of maximum length
            // so far
            if (midPal.size() < y.size()) {
                midPal = y;
            }
        }
    }

    // Check all the suffix substrings
    // in the remaining string str
    for (int i = 1; i <= str.size(); i++) {
        string y = str.substr(str.size() - i);

        // Check if the suffix substring
        // is a palindrome
        if (isPalindrome(y)) {

            // If the suffix substring
            // is a palindrome then check
            // if it is of maximum length
            // so far
            if (midPal.size() < y.size()) {
                midPal = y;
            }
        }
    }

    // Combining all the thee parts
    // of the answer
    string answer = prefix + midPal + suffix;

    return answer;
}

// Driver code
int main()
{
    string str = "abcdfdcecba";

    cout << PrefixSuffixPalindrome(str) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest
// palindrome in a String formed by
// concatenating its prefix and suffix
import java.util.*;

class GFG{

// Function to check whether
// the String is a palindrome
static boolean isPalindrome(String r)
{
    String p = r;

    // Reverse the String to
    // compare with the
    // original String
    p = reverse(p);

    // Check if both are same
    return (r.equals(p));
}

// Function to find the longest
// palindrome in a String formed by
// concatenating its prefix and suffix
static String PrefixSuffixPalindrome(String str)
{
    // Length of the String
    int n = str.length(), len = 0;

    // Finding the length upto which
    // the suffix and prefix forms a
    // palindrome together
    for (int i = 0; i < n / 2; i++) {
        if (str.charAt(i) != str.charAt(n - i - 1)) {
            len = i;
            break;
        }
    }

    // Check whether the String
    // has prefix and suffix subStrings
    // which are palindromes.
    String prefix = "", suffix = "";
    String midPal = "";

    // Removing the suffix and prefix
    // subStrings which already forms
    // a palindrome and storing them
    // in separate Strings
    prefix = str.substring(0, len);
    suffix = str.substring(n - len);
    str = str.substring(len, (n - 2 * len) + len);

    // Check all prefix subStrings
    // in the remaining String str
    for (int i = 1; i <= str.length(); i++) {
        String y = str.substring(0, i);

        // Check if the prefix subString
        // is a palindrome
        if (isPalindrome(y)) {

            // If the prefix subString
            // is a palindrome then check
            // if it is of maximum length
            // so far
            if (midPal.length() < y.length()) {
                midPal = y;
            }
        }
    }

    // Check all the suffix subStrings
    // in the remaining String str
    for (int i = 1; i <= str.length(); i++) {
        String y = str.substring(str.length() - i);

        // Check if the suffix subString
        // is a palindrome
        if (isPalindrome(y)) {

            // If the suffix subString
            // is a palindrome then check
            // if it is of maximum length
            // so far
            if (midPal.length() < y.length()) {
                midPal = y;
            }
        }
    }

    // Combining all the thee parts
    // of the answer
    String answer = prefix + midPal + suffix;

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

// Driver code
public static void main(String[] args)
{
    String str = "abcdfdcecba";

    System.out.print(PrefixSuffixPalindrome(str));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the longest
# palindrome in a string formed by
# concatenating its prefix and suffix

# Function to check whether
# the string is a palindrome
def isPalindrome(r):

    p = r

    # Reverse the string to
    # compare with the
    # original string
    p = "".join(reversed(p))

    # Check if both are same
    return (r == p)

# Function to find the longest
# palindrome in a string formed by
# concatenating its prefix and suffix
def PrefixSuffixPalindrome(st):

    # Length of the string
    n = len(st)
    length = 0

    # Finding the length upto which
    # the suffix and prefix forms a
    # palindrome together
    for i in range( n // 2):
        if (st[i] != st[n - i - 1]):
            length = i
            break

    # Check whether the string
    # has prefix and suffix substrings
    # which are palindromes.
    prefix = ""
    suffix = ""
    midPal = ""

    # Removing the suffix and prefix
    # substrings which already forms
    # a palindrome and storing them
    # in separate strings
    prefix = st[:length]
    suffix = st[n - length:]
    st = st[length: n - 2 * length+length]

    # Check all prefix substrings
    # in the remaining string str
    for i in range(1,len(st)+1):
        y = st[0: i]

        # Check if the prefix substring
        # is a palindrome
        if (isPalindrome(y)):

            # If the prefix substring
            # is a palindrome then check
            # if it is of maximum length
            # so far
            if (len(midPal) < len(y)):
                midPal = y

    # Check all the suffix substrings
    # in the remaining string str
    for i in range(1,len(st)+1):
        y = st[len(st)-i]

        # Check if the suffix substring
        # is a palindrome
        if (isPalindrome(y)):

            # If the suffix substring
            # is a palindrome then check
            # if it is of maximum length
            # so far
            if (len(midPal) < len(y)):
                midPal = y

    # Combining all the thee parts
    # of the answer
    answer = prefix + midPal + suffix

    return answer

# Driver code
if __name__ == "__main__":

    st = "abcdfdcecba";

    print(PrefixSuffixPalindrome(st))

# This code is contributed by chitranayal

```

## C#

```
// C# program to find the longest
// palindrome in a String formed by
// concatenating its prefix and suffix
using System;

class GFG{

// Function to check whether
// the String is a palindrome
static bool isPalindrome(String r)
{
    String p = r;

    // Reverse the String to
    // compare with the
    // original String
    p = reverse(p);

    // Check if both are same
    return (r.Equals(p));
}

// Function to find the longest
// palindrome in a String formed by
// concatenating its prefix and suffix
static String PrefixSuffixPalindrome(String str)
{
    // Length of the String
    int n = str.Length, len = 0;

    // Finding the length upto which
    // the suffix and prefix forms a
    // palindrome together
    for (int i = 0; i < n / 2; i++) {
        if (str[i] != str[n - i - 1]) {
            len = i;
            break;
        }
    }

    // Check whether the String
    // has prefix and suffix subStrings
    // which are palindromes.
    String prefix = "", suffix = "";
    String midPal = "";

    // Removing the suffix and prefix
    // subStrings which already forms
    // a palindrome and storing them
    // in separate Strings
    prefix = str.Substring(0, len);
    suffix = str.Substring(n - len);
    str = str.Substring(len, (n - 2 * len) + len);

    // Check all prefix subStrings
    // in the remaining String str
    for (int i = 1; i <= str.Length; i++) {
        String y = str.Substring(0, i);

        // Check if the prefix subString
        // is a palindrome
        if (isPalindrome(y)) {

            // If the prefix subString
            // is a palindrome then check
            // if it is of maximum length
            // so far
            if (midPal.Length < y.Length) {
                midPal = y;
            }
        }
    }

    // Check all the suffix subStrings
    // in the remaining String str
    for (int i = 1; i <= str.Length; i++) {
        String y = str.Substring(str.Length - i);

        // Check if the suffix subString
        // is a palindrome
        if (isPalindrome(y)) {

            // If the suffix subString
            // is a palindrome then check
            // if it is of maximum length
            // so far
            if (midPal.Length < y.Length) {
                midPal = y;
            }
        }
    }

    // Combining all the thee parts
    // of the answer
    String answer = prefix + midPal + suffix;

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

// Driver code
public static void Main(String[] args)
{
    String str = "abcdfdcecba";

    Console.Write(PrefixSuffixPalindrome(str));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find the longest
// palindrome in a String formed by
// concatenating its prefix and suffix

// Function to check whether
// the String is a palindrome
function isPalindrome(r)
{
    let p = r;

    // Reverse the String to
    // compare with the
    // original String
    p = reverse(p);

    // Check if both are same
    return (r == (p));
}

// Function to find the longest
// palindrome in a String formed by
// concatenating its prefix and suffix
function PrefixSuffixPalindrome(str)
{
    // Length of the String
    let n = str.length, len = 0;

    // Finding the length upto which
    // the suffix and prefix forms a
    // palindrome together
    for (let i = 0; i < n / 2; i++) {
        if (str[i] != str[n - i - 1]) {
            len = i;
            break;
        }
    }

    // Check whether the String
    // has prefix and suffix subStrings
    // which are palindromes.
    let prefix = "", suffix = "";
    let midPal = "";

    // Removing the suffix and prefix
    // subStrings which already forms
    // a palindrome and storing them
    // in separate Strings
    prefix = str.substring(0, len);
    suffix = str.substring(n - len);
    str = str.substring(len, (n - 2 * len) + len);

    // Check all prefix subStrings
    // in the remaining String str
    for (let i = 1; i <= str.length; i++) {
        let y = str.substring(0, i);

        // Check if the prefix subString
        // is a palindrome
        if (isPalindrome(y)) {

            // If the prefix subString
            // is a palindrome then check
            // if it is of maximum length
            // so far
            if (midPal.length < y.length) {
                midPal = y;
            }
        }
    }

    // Check all the suffix subStrings
    // in the remaining String str
    for (let i = 1; i <= str.length; i++) {
        let y = str.substring(str.length - i);

        // Check if the suffix subString
        // is a palindrome
        if (isPalindrome(y)) {

            // If the suffix subString
            // is a palindrome then check
            // if it is of maximum length
            // so far
            if (midPal.length < y.length) {
                midPal = y;
            }
        }
    }

    // Combining all the thee parts
    // of the answer
    let answer = prefix + midPal + suffix;

    return answer;
}

function reverse(input)
{
    let a = input.split("");
    let l, r = a.length - 1;
    for (l = 0; l < r; l++, r--) {
        let temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return (a).join("");
}

// Driver code
let str = "abcdfdcecba";
document.write(PrefixSuffixPalindrome(str));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
abcdfdcba
```