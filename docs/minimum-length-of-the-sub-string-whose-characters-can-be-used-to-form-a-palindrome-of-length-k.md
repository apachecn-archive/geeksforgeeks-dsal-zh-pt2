# 子串的最小长度，其字符可用于形成长度为 K 的回文

> 原文:[https://www . geesforgeks . org/最小长度子串-其字符可用于形成长度为 k 的回文/](https://www.geeksforgeeks.org/minimum-length-of-the-sub-string-whose-characters-can-be-used-to-form-a-palindrome-of-length-k/)

给定一个由小写英文字母和整数 **K** 组成的字符串 **str** 。任务是找到子串的最小长度，子串的字符可以用来组成一个长度为 **K** 的回文。如果不存在这样的子字符串，则打印 **-1** 。
**举例:**

> **输入:** str = "abcda "，k = 2
> **输出:** 5
> 为了形成长度为 2 的回文，需要同时出现‘a’。
> 因此，所需子串的长度为 5。
> **输入:** str = "abcde "，k = 5
> **输出:** -1
> 给定字符串的字符不能组成长度为 5 的回文串。

**进场:**思路是用二分搜索法。形成长度为 **K** 的回文所需的最小字符是 **K** 。所以，我们的搜索范围缩小到**【K，长度(str)】**。在这个范围内应用二分搜索法，找到一个长度为 **X** (K ≤ X ≤长度(S))的子串，这样使用这个子串的部分或全部字符，就可以形成一个大小为 **K** 的回文串。满足给定条件的最小 **X** 将是所需答案。如果没有这样的子字符串，则打印 **-1** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// a palindrome can be formed using
// exactly k characters
bool isPalindrome(int freq[], int k)
{
    // Variable to check if characters
    // with odd frequency are present
    int flag = 0;

    // Variable to store maximum length
    // of the palindrome that can be formed
    int length = 0;

    for (int i = 0; i < 26; i++) {
        if (freq[i] == 0)
            continue;

        else if (freq[i] == 1)
            flag = 1;

        else {
            if (freq[i] & 1)
                flag = 1;
            length += freq[i] / 2;
        }
    }

    // If k is odd
    if (k & 1) {
        if (2 * length + flag >= k)
            return true;
    }

    // If k is even
    else {
        if (2 * length >= k)
            return true;
    }

    // If palindrome of length
    // k cant be formed
    return false;
}

// Function that returns true if a palindrome
// of length k can be formed from a
// sub-string of length m
bool check(string str, int m, int k)
{
    // Stores frequency of characters
    // of a substring of length m
    int freq[26] = { 0 };

    for (int i = 0; i < m; i++)
        freq[str[i] - 'a']++;

    // If a palindrome can be
    // formed from a substring of
    // length m
    if (isPalindrome(freq, k))
        return true;

    // Check for all the substrings of
    // length m, if a palindrome of
    // length k can be formed
    for (int i = m; i < str.length(); i++) {
        freq[str[i - m] - 'a']--;
        freq[str[i] - 'a']++;

        if (isPalindrome(freq, k))
            return true;
    }

    // If no palindrome of length
    // k can be formed
    return false;
}

// Function to return the minimum length
// of the sub-string whose characters can be
// used to form a palindrome of length k
int find(string str, int n, int k)
{
    int l = k;
    int h = n;

    // To store the minimum length of the
    // sub-string that can be used to form
    // a palindrome of length k
    int ans = -1;

    while (l <= h) {
        int m = (l + h) / 2;
        if (check(str, m, k)) {
            ans = m;
            h = m - 1;
        }
        else
            l = m + 1;
    }

    return ans;
}

// Driver code
int main()
{
    string str = "abcda";
    int n = str.length();
    int k = 2;
    cout << find(str, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if
// a palindrome can be formed using
// exactly k characters
static boolean isPalindrome(int freq[], int k)
{
    // Variable to check if characters
    // with odd frequency are present
    int flag = 0;

    // Variable to store maximum length
    // of the palindrome that can be formed
    int length = 0;

    for (int i = 0; i < 26; i++)
    {
        if (freq[i] == 0)
            continue;

        else if (freq[i] == 1)
            flag = 1;

        else
        {
            if (freq[i] % 2 == 1)
                flag = 1;
            length += freq[i] / 2;
        }
    }

    // If k is odd
    if (k % 2 == 1)
    {
        if (2 * length + flag >= k)
            return true;
    }

    // If k is even
    else
    {
        if (2 * length >= k)
            return true;
    }

    // If palindrome of length
    // k cant be formed
    return false;
}

// Function that returns true if a palindrome
// of length k can be formed from a
// sub-string of length m
static boolean check(String str, int m, int k)
{
    // Stores frequency of characters
    // of a substring of length m
    int []freq = new int[26];

    for (int i = 0; i < m; i++)
        freq[str.charAt(i) - 'a']++;

    // If a palindrome can be
    // formed from a substring of
    // length m
    if (isPalindrome(freq, k))
        return true;

    // Check for all the substrings of
    // length m, if a palindrome of
    // length k can be formed
    for (int i = m; i < str.length(); i++)
    {
        freq[str.charAt(i-m) - 'a']--;
        freq[str.charAt(i) - 'a']++;

        if (isPalindrome(freq, k))
            return true;
    }

    // If no palindrome of length
    // k can be formed
    return false;
}

// Function to return the minimum length
// of the sub-string whose characters can be
// used to form a palindrome of length k
static int find(String str, int n, int k)
{
    int l = k;
    int h = n;

    // To store the minimum length of the
    // sub-string that can be used to form
    // a palindrome of length k
    int ans = -1;

    while (l <= h)
    {
        int m = (l + h) / 2;
        if (check(str, m, k))
        {
            ans = m;
            h = m - 1;
        }
        else
            l = m + 1;
    }

    return ans;
}

// Driver code
public static void main(String[] args)
{
    String str = "abcda";
    int n = str.length();
    int k = 2;
    System.out.println(find(str, n, k));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns true if
# a palindrome can be formed using
# exactly k characters
def isPalindrome(freq, k):

    # Variable to check if characters
    # with odd frequency are present
    flag = 0

    # Variable to store maximum length
    # of the palindrome that can be formed
    length = 0

    for i in range(26):
        if (freq[i] == 0):
            continue

        elif (freq[i] == 1):
            flag = 1

        else:
            if (freq[i] & 1):
                flag = 1
            length += freq[i] // 2

    # If k is odd
    if (k & 1):
        if (2 * length + flag >= k):
            return True

    # If k is even
    else:
        if (2 * length >= k):
            return True

    # If palindrome of length
    # k cant be formed
    return False

# Function that returns true if a palindrome
# of length k can be formed from a
# sub-string of length m
def check(str, m, k):

    # Stores frequency of characters
    # of a substring of length m
    freq = [0 for i in range(26)]

    for i in range(m):
        freq[ord(str[i]) - ord('a')] += 1

    # If a palindrome can be
    # formed from a substring of
    # length m
    if (isPalindrome(freq, k)):
        return True

    # Check for all the substrings of
    # length m, if a palindrome of
    # length k can be formed
    for i in range(m, len(str), 1):
        freq[ord(str[i - m]) - ord('a')] -= 1
        freq[ord(str[i]) - ord('a')] += 1

        if (isPalindrome(freq, k)):
            return True

    # If no palindrome of length
    # k can be formed
    return False

# Function to return the minimum length
# of the sub-string whose characters can be
# used to form a palindrome of length k
def find(str, n, k):
    l = k
    h = n

    # To store the minimum length of the
    # sub-string that can be used to form
    # a palindrome of length k
    ans = -1

    while (l <= h):
        m = (l + h) // 2
        if (check(str, m, k)):
            ans = m
            h = m - 1

        else:
            l = m + 1

    return ans

# Driver code
if __name__ == '__main__':
    str = "abcda"
    n = len(str)
    k = 2
    print(find(str, n, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if
// a palindrome can be formed using
// exactly k characters
static Boolean isPalindrome(int []freq, int k)
{
    // Variable to check if characters
    // with odd frequency are present
    int flag = 0;

    // Variable to store maximum length
    // of the palindrome that can be formed
    int length = 0;

    for (int i = 0; i < 26; i++)
    {
        if (freq[i] == 0)
            continue;

        else if (freq[i] == 1)
            flag = 1;

        else
        {
            if (freq[i] % 2 == 1)
                flag = 1;
            length += freq[i] / 2;
        }
    }

    // If k is odd
    if (k % 2 == 1)
    {
        if (2 * length + flag >= k)
            return true;
    }

    // If k is even
    else
    {
        if (2 * length >= k)
            return true;
    }

    // If palindrome of length
    // k cant be formed
    return false;
}

// Function that returns true if a palindrome
// of length k can be formed from a
// sub-string of length m
static Boolean check(String str, int m, int k)
{
    // Stores frequency of characters
    // of a substring of length m
    int []freq = new int[26];

    for (int i = 0; i < m; i++)
        freq[str[i] - 'a']++;

    // If a palindrome can be
    // formed from a substring of
    // length m
    if (isPalindrome(freq, k))
        return true;

    // Check for all the substrings of
    // length m, if a palindrome of
    // length k can be formed
    for (int i = m; i < str.Length; i++)
    {
        freq[str[i - m] - 'a']--;
        freq[str[i] - 'a']++;

        if (isPalindrome(freq, k))
            return true;
    }

    // If no palindrome of length
    // k can be formed
    return false;
}

// Function to return the minimum length
// of the sub-string whose characters can be
// used to form a palindrome of length k
static int find(String str, int n, int k)
{
    int l = k;
    int h = n;

    // To store the minimum length of the
    // sub-string that can be used to form
    // a palindrome of length k
    int ans = -1;

    while (l <= h)
    {
        int m = (l + h) / 2;
        if (check(str, m, k))
        {
            ans = m;
            h = m - 1;
        }
        else
            l = m + 1;
    }

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    String str = "abcda";
    int n = str.Length;
    int k = 2;
    Console.WriteLine(find(str, n, k));
}
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if
// a palindrome can be formed using
// exactly k characters
function isPalindrome($freq, $k)
{
    // Variable to check if characters
    // with odd frequency are present
    $flag = 0;

    // Variable to store maximum length
    // of the palindrome that can be formed
    $length = 0;

    for ($i = 0; $i < 26; $i++)
    {
        if ($freq[$i] == 0)
            continue;

        else if ($freq[$i] == 1)
            $flag = 1;

        else
        {
            if ($freq[$i] & 1)
                $flag = 1;

            $length += floor($freq[$i] / 2);
        }
    }

    // If k is odd
    if ($k & 1)
    {
        if (2 * $length + $flag >= $k)
            return true;
    }

    // If k is even
    else
    {
        if (2 * $length >= $k)
            return true;
    }

    // If palindrome of length
    // k cant be formed
    return false;
}

// Function that returns true if a palindrome
// of length k can be formed from a
// sub-string of length m
function check($str, $m, $k)
{
    // Stores frequency of characters
    // of a substring of length m
    $freq = array_fill(0, 26, 0);

    for ($i = 0; $i < $m; $i++)
        $freq[ord($str[$i]) - ord('a')]++;

    // If a palindrome can be
    // formed from a substring of
    // length m
    if (isPalindrome($freq, $k))
        return true;

    // Check for all the substrings of
    // length m, if a palindrome of
    // length k can be formed
    for ($i = $m; $i < strlen($str); $i++)
    {
        $freq[ord($str[$i - $m]) - ord('a')] -= 1;
        $freq[ord($str[$i]) - ord('a')] += 1;

        if (isPalindrome($freq, $k))
            return true;
    }

    // If no palindrome of length
    // k can be formed
    return false;
}

// Function to return the minimum length
// of the sub-string whose characters can be
// used to form a palindrome of length k
function find($str, $n, $k)
{
    $l = $k;
    $h = $n;

    // To store the minimum length of the
    // sub-string that can be used to form
    // a palindrome of length k
    $ans = -1;

    while ($l <= $h)
    {
        $m = floor(($l + $h) / 2);
        if (check($str, $m, $k))
        {
            $ans = $m;
            $h = $m - 1;
        }
        else
            $l = $m + 1;
    }

    return $ans;
}

// Driver code
$str = "abcda";
$n = strlen($str);
$k = 2;

echo find($str, $n, $k);

// This code is improved by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function that returns true if
    // a palindrome can be formed using
    // exactly k characters
    function isPalindrome(freq, k)
    {

        // Variable to check if characters
        // with odd frequency are present
        let flag = 0;

        // Variable to store maximum length
        // of the palindrome that can be formed
        let length = 0;

        for (let i = 0; i < 26; i++)
        {
            if (freq[i] == 0)
                continue;

            else if (freq[i] == 1)
                flag = 1;

            else
            {
                if (freq[i] % 2 == 1)
                    flag = 1;
                length += parseInt(freq[i] / 2, 10);
            }
        }

        // If k is odd
        if (k % 2 == 1)
        {
            if (2 * length + flag >= k)
                return true;
        }

        // If k is even
        else
        {
            if (2 * length >= k)
                return true;
        }

        // If palindrome of length
        // k cant be formed
        return false;
    }

    // Function that returns true if a palindrome
    // of length k can be formed from a
    // sub-string of length m
    function check(str, m, k)
    {
        // Stores frequency of characters
        // of a substring of length m
        let freq = new Array(26);
        freq.fill(0);

        for (let i = 0; i < m; i++)
            freq[str[i].charCodeAt() - 'a'.charCodeAt()]++;

        // If a palindrome can be
        // formed from a substring of
        // length m
        if (isPalindrome(freq, k))
            return true;

        // Check for all the substrings of
        // length m, if a palindrome of
        // length k can be formed
        for (let i = m; i < str.length; i++)
        {
            freq[str[i - m].charCodeAt() - 'a'.charCodeAt()]--;
            freq[str[i].charCodeAt() - 'a'.charCodeAt()]++;

            if (isPalindrome(freq, k))
                return true;
        }

        // If no palindrome of length
        // k can be formed
        return false;
    }

    // Function to return the minimum length
    // of the sub-string whose characters can be
    // used to form a palindrome of length k
    function find(str, n, k)
    {
        let l = k;
        let h = n;

        // To store the minimum length of the
        // sub-string that can be used to form
        // a palindrome of length k
        let ans = -1;

        while (l <= h)
        {
            let m = parseInt((l + h) / 2, 10);
            if (check(str, m, k))
            {
                ans = m;
                h = m - 1;
            }
            else
                l = m + 1;
        }
        return ans;
    }

    let str = "abcda";
    let n = str.length;
    let k = 2;
    document.write(find(str, n, k));

    // This code is contributed by divyeshrbadiya07.
</script>
```

**Output:** 

```
5
```