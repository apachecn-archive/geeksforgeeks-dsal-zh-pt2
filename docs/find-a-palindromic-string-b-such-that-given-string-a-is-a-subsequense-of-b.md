# 找到一个回文串 B，这样给定的串 A 就是 B 的子集

> 原文:[https://www . geesforgeks . org/find-a-回文字符串-b-so-给定字符串-a-is-a-subsequense-of-b/](https://www.geeksforgeeks.org/find-a-palindromic-string-b-such-that-given-string-a-is-a-subsequense-of-b/)

给一根绳子![A  ](img/d87f1cb8a8e09ef6d976b963803548e2.png "Rendered by QuickLaTeX.com")。找一个字符串![B  ](img/af5280b6d00ec107c9fc36bb5fe47e67.png "Rendered by QuickLaTeX.com")，其中 **B** 是回文，A 是 B 的子序列

一个字符串的**子序列**是一个可以通过删除一些(不一定是连续的)字符而不改变其余字符的顺序来派生出来的字符串。例如，“cotst”是“竞赛”的子序列。

一个**回文**是一个向前或向后读相同的字符串。

**示例**:

```
Input : A = "aba"
Output : B = aba
Explanation : "aba" is a subsequence of "aba" 
which is a palindrome.

Input : A = "ab"
Output : B = abba
```

**方法:**让反转成为弦的反转![s  ](img/2f9e9564d9a0ab37fcfa0d3c7cda6a42.png "Rendered by QuickLaTeX.com")。现在， **s + reverse(s)** 将永远有![s  ](img/2f9e9564d9a0ab37fcfa0d3c7cda6a42.png "Rendered by QuickLaTeX.com")作为子序列(作为前半部分)，它是一个回文。
因此， **B = A +反向(A)** 。

下面是上述方法的实现:

## C++14

```
// C++ program to find a palindromic string B
// such that given String A is a subsequense of B
#include <bits/stdc++.h>
using namespace std;

// Function to check if a string is palindrome
bool checkPalindrome(string s)
{
    // Reversing a string
    string x = s;
    reverse(s.begin(), s.end());

    // check if reversed string is equal
    // to given string
    return s == x;
}

// Function to find a palindromic string B
// such that given String A is a subsequense of B
string findStringB(string A)
{
    // Reversing the string A
    string B = A;
    reverse(A.begin(), A.end());
    A = A + B;

    // If the string A is already a palindrome
    // return A
    if (checkPalindrome(B))
        return B;

    // else return B
    return A;
}

string reverse(string input)
{
    string temparray = input;
    int left, right = 0;
    right = temparray.length() - 1;

    for (left = 0; left < right; left++, right--)

        // Swap values of left and right
        swap(temparray[left], temparray[right]);

    return temparray;
}

// Driver Code
int main(int argc, char const *argv[])
{
    string A = "ab";
    cout << findStringB(A) << endl;
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a palindromic string B
// such that given String A is a subsequense of B

class GFG
{

    // Function to check if a string is palindrome
    static boolean checkPalindrome(String s)
    {
        // Reversing a string
        String x = reverse(s);

        // check if reversed string is equal
        // to given string
        return x.equals(s);
    }

    // Function to find a palindromic string B
    // such that given String A is a subsequense of B
    static String findStringB(String A)
    {

        // Reversing the string A
        String B = reverse(A);
        B = B + A;

        // If the string A is already a palindrome
        // return A
        if (checkPalindrome(A))
        {
            return A;
        }

        // else return B
        return B;
    }

    static String reverse(String input)
    {
        char[] temparray = input.toCharArray();
        int left, right = 0;
        right = temparray.length - 1;

        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.valueOf(temparray);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String A = "ab";
        System.out.println(findStringB(A));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to find a palindromic string B
# such that given String A is a subsequense of B

# Function to check if a string is palindrome
def checkPalindrome(s):
    # Reversing a string
    x = s[::-1]
    # check if reversed string is equal
    # to given string
    if(x == s):
        return True
    else:
        return False

# Function to find a palindromic string B
# such that given String A is a subsequense of B
def findStringB(A):

    # Reversing the string A
    B = A[::-1]

    B = B + A

    # If the string A is already a palindrome
    # return A
    if(checkPalindrome(A)):
        return A

    # else return B   
    return B

# Driver Code
A ="ab"
print(findStringB(A))
```

## C#

```
// C# program to find a palindromic string B
// such that given String A is a subsequense of B
using System;

class GFG
{

    // Function to check if a string is palindrome
    static bool checkPalindrome(String s)
    {
        // Reversing a string
        String x = reverse(s);

        // check if reversed string is equal
        // to given string
        return x.Equals(s);
    }

    // Function to find a palindromic string B
    // such that given String A is a subsequense of B
    static String findStringB(String A)
    {

        // Reversing the string A
        String B = reverse(A);
        B = B + A;

        // If the string A is already a palindrome
        // return A
        if (checkPalindrome(A))
        {
            return A;
        }

        // else return B
        return B;
    }

    static String reverse(String input)
    {
        char[] temparray = input.ToCharArray();
        int left, right = 0;
        right = temparray.Length - 1;

        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.Join("",temparray);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String A = "ab";
        Console.WriteLine(findStringB(A));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find a palindromic string B
// such that given String A is a subsequense of B

// Function to check if a string is palindrome
function checkPalindrome(s)
{

    // Reversing a string
    let x = reverse(s);

    // Check if reversed string is equal
    // to given string
    return x == (s);
}

// Function to find a palindromic string B
// such that given String A is a subsequense of B
function findStringB(A)
{

    // Reversing the string A
    let B = reverse(A);
    B = B + A;

    // If the string A is already a palindrome
    // return A
    if (checkPalindrome(A))
    {
        return A;
    }

    // Else return B
    return B;
}

function reverse(input)
{
    let temparray = input.split("");
    let left, right = 0;
    right = temparray.length - 1;

    for(left = 0; left < right; left++, right--)
    {

        // Swap values of left and right
        let temp = temparray[left];
        temparray[left] = temparray[right];
        temparray[right] = temp;
    }
    return (temparray).join("");
}

// Driver Code
let A = "ab";
document.write(findStringB(A));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
baab
```