# 用大小为 k 的子串中元音和辅音数量的乘积加密字符串

> 原文:[https://www . geesforgeks . org/encrypt-string-product-number-元音-辅音-substring-size-k/](https://www.geeksforgeeks.org/encrypt-string-product-number-vowels-consonants-substring-size-k/)

给定一个字符串 **s** 和一个正整数 k，你需要对给定的字符串进行加密，这样大小为 k 的每个子串都用一个整数来表示，这个整数是由子串中元音数和辅音数的乘积得到的。
**例:**

```
Input : s = "hello", k = 2
Output : 1101
k = 2, so each substring should be of size 2,
he, consonants = 1, vowels = 1, product = 1
el, consonants = 1, vowels = 1, product = 1
ll, consonants = 1, vowels = 0, product = 0
lo, consonants = 1, vowels = 1, product = 1
So, encrypted string is 1101.

Input : s = "geeksforgeeks", k = 5
Output : 666446666
```

**方法一(蛮力):**
思路是找到大小为 k 的每个子串，计算出元音和辅音的个数，然后存储两个的乘积。

## C++

```
// CPP Program to Encrypt string with product
// of number of vowels and consonants in every
// substring of size k
#include <bits/stdc++.h>
using namespace std;

// isVowel() is a function that returns true
// for a vowel and false otherwise.
bool isVowel(char c)
{
    return (c == 'a' || c == 'e' || c == 'i' ||
            c == 'o' || c == 'u');
}

// function to Encrypt the string
string encryptString(string s, int n, int k)
{
    int countVowels = 0;
    int countConsonants = 0;
    string ans = "";

    // for each substring
    for (int l = 0; l <= n - k; l++) {
        countVowels = 0;
        countConsonants = 0;

        // substring of size k
        for (int r = l; r <= l + k - 1; r++) {

            // counting number of vowels and
            // consonants
            if (isVowel(s[r]) == true)
                countVowels++;
            else
                countConsonants++;
        }

        // append product to answer.
        ans += to_string(countVowels * countConsonants);
    }
    return ans;
}

// Driven Program
int main()
{
    string s = "hello";
    int n = s.length();
    int k = 2;
    cout << encryptString(s, n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Encrypt String with product
// of number of vowels and consonants in every
// substring of size k

class GFG {

// isVowel() is a function that returns true
// for a vowel and false otherwise.
    static boolean isVowel(char c) {
        return (c == 'a' || c == 'e' || c == 'i'
                || c == 'o' || c == 'u');
    }

// function to Encrypt the string
    static String encryptString(String s, int n, int k) {
        int countVowels = 0;
        int countConsonants = 0;
        String ans = "";

        // for each substring
        for (int l = 0; l <= n - k; l++) {
            countVowels = 0;
            countConsonants = 0;

            // substring of size k
            for (int r = l; r <= l + k - 1; r++) {

                // counting number of vowels and
                // consonants
                if (isVowel(s.charAt(r)) == true) {
                    countVowels++;
                } else {
                    countConsonants++;
                }
            }

            // append product to answer.
            ans += String.valueOf(countVowels * countConsonants);
        }
        return ans;
    }

// Driven Program
    static public void main(String[] args) {
        String s = "hello";
        int n = s.length();
        int k = 2;
        System.out.println(encryptString(s, n, k));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python Program to Encrypt string with
# product of number of vowels and
# consonants in every substring of size k

# isVowel() is a function that returns
# true for a vowel and false otherwise.
def isVowel(c):
    return (c == 'a' or c == 'e' or
            c == 'i' or c == 'o' or
            c == 'u')

# function to Encrypt the string
def encryptString(s, n, k):
    countVowels = 0
    countConsonants = 0
    ans = ""

    # for each substring
    for l in range(n - k + 1):
        countVowels = 0
        countConsonants = 0

        # substring of size k
        for r in range(l, l + k):

            # counting number of vowels
            # and consonants
            if (isVowel(s[r]) == True):
                countVowels += 1
            else:
                countConsonants += 1

        # append product to answer
        ans += (str)(countVowels *
                     countConsonants)
    return ans

# Driver Code
if __name__ == '__main__':
    s = "hello"
    n = len(s)
    k = 2
    print(encryptString(s, n, k))

# This code is contributed
# by PrinciRaj1992
```

## C#

```
// C# Program to Encrypt String with product
// of number of vowels and consonants in every
// substring of size k
using System;

public class GFG {

// isVowel() is a function that returns true
// for a vowel and false otherwise.
    static bool isVowel(char c) {
        return (c == 'a' || c == 'e' || c == 'i'
                || c == 'o' || c == 'u');
    }

// function to Encrypt the string
    static String encryptString(String s, int n, int k) {
        int countVowels = 0;
        int countConsonants = 0;
        String ans = "";

        // for each substring
        for (int l = 0; l <= n - k; l++) {
            countVowels = 0;
            countConsonants = 0;

            // substring of size k
            for (int r = l; r <= l + k - 1; r++) {

                // counting number of vowels and
                // consonants
                if (isVowel(s[r]) == true) {
                    countVowels++;
                } else {
                    countConsonants++;
                }
            }

            // append product to answer.
            ans += Convert.ToString(countVowels * countConsonants);
        }
        return ans;
    }

// Driven Program
    static public void Main() {
        String s = "hello";
        int n = s.Length;
        int k = 2;
        Console.Write(encryptString(s, n, k));
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to Encrypt string with
// product of number of vowels and
// consonants in every substring of size k

// isVowel() is a function that returns true
// for a vowel and false otherwise.
function isVowel($c)
{
    return ($c == 'a' || $c == 'e' || $c == 'i' ||
            $c == 'o' || $c == 'u');
}

// function to Encrypt the string
function encryptString($s, $n, $k)
{
    $countVowels = 0;
    $countConsonants = 0;
    $ans = "";

    // for each substring
    for ($l = 0; $l <= $n - $k; $l++)
    {
        $countVowels = 0;
        $countConsonants = 0;

        // substring of size k
        for ($r = $l; $r <= $l + $k - 1; $r++)
        {

            // counting number of vowels and
            // consonants
            if (isVowel($s[$r]) == true)
                $countVowels++;
            else
                $countConsonants++;
        }

        // append product to answer.
        $ans = $ans . (string)($countVowels *
                               $countConsonants);
    }
    return $ans;
}

// Driver Code
$s = "hello";
$n = strlen($s);
$k = 2;
echo encryptString($s, $n, $k) . "\n";

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// Javascript Program to Encrypt string with product
// of number of vowels and consonants in every
// substring of size k

// isVowel() is a function that returns true
// for a vowel and false otherwise.
function isVowel(c)
{
    return (c == 'a' || c == 'e' || c == 'i' ||
            c == 'o' || c == 'u');
}

// function to Encrypt the string
function encryptString(s, n, k)
{
    var countVowels = 0;
    var countConsonants = 0;
    var ans = "";

    // for each substring
    for (var l = 0; l <= n - k; l++) {
        countVowels = 0;
        countConsonants = 0;

        // substring of size k
        for (var r = l; r <= l + k - 1; r++) {

            // counting number of vowels and
            // consonants
            if (isVowel(s[r]) == true)
                countVowels++;
            else
                countConsonants++;
        }

        // append product to answer.
        ans += (countVowels * countConsonants).toString();
    }
    return ans;
}

// Driven Program
var s = "hello";
var n = s.length;
var k = 2;
document.write( encryptString(s, n, k));

</script>
```

**输出:**

```
1101
```

**方法 2(高效途径):**
上述途径可以优化。在上面的方法中，我们计算一个字符是元音还是辅音超过一次。现在，仔细看一下，我们可以看到，我们对相同的 k–1 字符计算了两次元音和辅音的数量。我们可以从[1]计算出这些字符的元音和辅音的数量。k–1]和[2……k-1]两次。
为了避免这种情况，我们可以预先计算元音和辅音的数量，直到每个索引 I，然后使用这些值来计算结果。
以下是本办法的实施情况:

## C++

```
// CPP Program to Encrypt string with product of
// number of vowels and consonants in substring
// of size k
#include <bits/stdc++.h>
using namespace std;

// isVowel() is a function that returns true
// for a vowel and false otherwise.
bool isVowel(char c)
{
    return (c == 'a' || c == 'e' || c == 'i' ||
            c == 'o' || c == 'u');
}

// function to Encrypt the string
string encryptString(string s, int n, int k)
{
    // cv to count vowel
    // cc to count consonants
    int cv[n], cc[n];

    if (isVowel(s[0]))
        cv[0] = 1;
    else
        cc[0] = 1;

    // Counting prefix count of vowel
    // and prefix count of consonants
    for (int i = 1; i < n; i++) {
        cv[i] = cv[i - 1] + isVowel(s[i]);
        cc[i] = cc[i - 1] + !isVowel(s[i]);
    }

    string ans = "";
    int prod = 0;

    prod = cc[k - 1] * cv[k - 1];
    ans += to_string(prod);

    // generating the encrypted string.
    for (int i = k; i < s.length(); i++) {
        prod = (cc[i] - cc[i - k]) * (cv[i] - cv[i - k]);
        ans += to_string(prod);
    }

    return ans;
}
// Driven Program
int main()
{
    string s = "hello";
    int n = s.length();
    int k = 2;

    cout << encryptString(s, n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Program to Encrypt String with product of
// number of vowels and consonants in subString
// of size k
class GFG
{

    // isVowel() is a function that returns true
    // for a vowel and false otherwise.
    static boolean isVowel(char c)
    {
        return (c == 'a' || c == 'e' ||
                c == 'i' || c == 'o' ||
                c == 'u');
    }

    // function to Encrypt the String
    static String encryptString(char[] s, int n, int k)
    {
        // cv to count vowel
        // cc to count consonants
        int[] cv = new int[n];
        int[] cc = new int[n];

        if (isVowel(s[0]))
            cv[0] = 1;
        else
            cc[0] = 1;

        // Counting prefix count of vowel
        // and prefix count of consonants
        for (int i = 1; i < n; i++)
        {
            cv[i] = cv[i - 1] + (isVowel(s[i]) == true ? 1 : 0);
            cc[i] = cc[i - 1] + (isVowel(s[i]) == true ? 0 : 1);
        }

        String ans = "";
        int prod = 0;

        prod = cc[k - 1] * cv[k - 1];
        ans += String.valueOf(prod);

        // generating the encrypted String.
        for (int i = k; i < s.length; i++)
        {
            prod = (cc[i] - cc[i - k]) *
                   (cv[i] - cv[i - k]);
            ans += String.valueOf(prod);
        }
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "hello";
        int n = s.length();
        int k = 2;

        System.out.print(encryptString(s.toCharArray(), n, k) + "\n");
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 Program to Encrypt string with
# product of number of vowels and consonants
# in substring of size k

# isVowel() is a function that returns true
# for a vowel and false otherwise.
def isVowel(c):
    return (c == 'a' or c == 'e' or
            c == 'i' or c == 'o' or c == 'u')

# function to Encrypt the string
def encryptString(s, n, k):

    # cv to count vowel
    # cc to count consonants
    cv = [0 for i in range(n)]
    cc = [0 for i in range(n)]

    if (isVowel(s[0])):
        cv[0] = 1
    else:
        cc[0] = 1

    # Counting prefix count of vowel
    # and prefix count of consonants
    for i in range(1,n):
        cv[i] = cv[i - 1] + isVowel(s[i])
        cc[i] = cc[i - 1] + (isVowel(s[i]) == False)

    ans = ""
    prod = 0

    prod = cc[k - 1] * cv[k - 1]
    ans += str(prod)

    # generating the encrypted string.
    for i in range(k, len(s)):
        prod = ((cc[i] - cc[i - k]) *
                (cv[i] - cv[i - k]))
        ans += str(prod)

    return ans

# Driver Code
if __name__ == '__main__':
    s = "hello"
    n = len(s)
    k = 2

    print(encryptString(s, n, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# Program to Encrypt String with
// product of number of vowels and
// consonants in subString of size k
using System;

class GFG
{

    // isVowel() is a function that
    // returns true for a vowel and
    // false otherwise.
    static bool isVowel(char c)
    {
        return (c == 'a' || c == 'e' ||
                c == 'i' || c == 'o' ||
                c == 'u');
    }

    // function to Encrypt the String
    static String encryptString(char[] s,
                         int n, int k)
    {
        // cv to count vowel
        // cc to count consonants
        int[] cv = new int[n];
        int[] cc = new int[n];

        if (isVowel(s[0]))
            cv[0] = 1;
        else
            cc[0] = 1;

        // Counting prefix count of vowel
        // and prefix count of consonants
        for (int i = 1; i < n; i++)
        {
            cv[i] = cv[i - 1] +
                   (isVowel(s[i]) == true ? 1 : 0);
            cc[i] = cc[i - 1] +
                   (isVowel(s[i]) == true ? 0 : 1);
        }

        String ans = "";
        int prod = 0;

        prod = cc[k - 1] * cv[k - 1];
        ans += String.Join("", prod);

        // generating the encrypted String.
        for (int i = k; i < s.Length; i++)
        {
            prod = (cc[i] - cc[i - k]) *
                   (cv[i] - cv[i - k]);
            ans += String.Join("", prod);
        }
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String s = "hello";
        int n = s.Length;
        int k = 2;

        Console.Write(encryptString(
                      s.ToCharArray(), n, k) + "\n");
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

      // JavaScript Program to Encrypt String with
      // product of number of vowels and
      // consonants in subString of size k

      // isVowel() is a function that
      // returns true for a vowel and
      // false otherwise.
      function isVowel(c) {
        return c === "a" || c === "e" || c === "i" ||
        c === "o" || c === "u";
      }

      // function to Encrypt the String
      function encryptString(s, n, k) {
        // cv to count vowel
        // cc to count consonants
        var cv = new Array(n).fill(0);
        var cc = new Array(n).fill(0);

        if (isVowel(s[0])) cv[0] = 1;
        else cc[0] = 1;

        // Counting prefix count of vowel
        // and prefix count of consonants
        for (var i = 1; i < n; i++) {
          cv[i] = cv[i - 1] + (isVowel(s[i]) === true ? 1 : 0);
          cc[i] = cc[i - 1] + (isVowel(s[i]) === true ? 0 : 1);
        }

        var ans = "";
        var prod = 0;

        prod = cc[k - 1] * cv[k - 1];
        ans += prod;

        // generating the encrypted String.
        for (var i = k; i < s.length; i++) {
          prod = (cc[i] - cc[i - k]) * (cv[i] - cv[i - k]);
          ans += prod;
        }
        return ans;
      }

      // Driver Code
      var s = "hello";
      var n = s.length;
      var k = 2;

      document.write(encryptString(s.split(""), n, k) + "<br>");

</script>
```

**输出:**

```
1101
```