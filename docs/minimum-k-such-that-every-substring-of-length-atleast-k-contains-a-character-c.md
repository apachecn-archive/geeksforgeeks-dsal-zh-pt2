# 最小 K，使得长度至少为 K 的每个子串包含一个字符 c

> 原文:[https://www . geesforgeks . org/minimum-k-so-每一个长度至少为-k-的子串都包含一个字符-c/](https://www.geeksforgeeks.org/minimum-k-such-that-every-substring-of-length-atleast-k-contains-a-character-c/)

给定一个包含小写拉丁字母的字符串。如果长度至少为 K 的 S 的每个子串都包含这个字符 c，那么这个字符 c 被称为 K-惊奇。找到最小可能的 K，使得至少存在一个 K-惊奇字符。
**例:**

> **输入:**S =“abcde”
> **输出:** 3
> **解释:**长度至少为 3 的每个子串都包含字符‘c’，即
> {“ABC”、“bcd”、“cde”、“abcd”、“bcde”、“abcde”}
> **输入:**S =“AAAA”
> **输出:** 1

**先决条件:** [【二分搜索法】](https://www.geeksforgeeks.org/binary-search/)
**天真解决方案:**一种简单的方法是迭代所有可能的子串长度，即从 1 到 N(字符串的大小)，并针对每个当前长度的子串检查某些字符是否出现在所有这些子串中。
**高效解决方案:**关键思想是对答案 **K** 执行二分搜索法运算，因为如果某个字符 c 出现在所有长度为 **X** 的子串中，它将始终出现在所有长度为 **(X + 1)** 的子串中。因此，我们可以检查当前长度，并尝试使用分治算法将其最小化。为了检查某个字符是否出现在长度为 X 的所有子串中，迭代从“a”到“z”的所有字符，并在另一个循环中迭代存储最后一个字符的最后一次出现。
设当前位置为 j，那么长度 X 的最后一个子串将从(j–X)到 X，检查当前 K-惊奇字符最后出现的位置是否大于(j–X)。如果大于该值，则该子字符串是有效的字符串。
以下是上述办法的实施情况。

## C++

```
// CPP Program to find minimum K such that
// every substring of length atleast K
// contains some character c
#include <bits/stdc++.h>
using namespace std;

// This function checks if there exists some
// character which appears in all K length
// substrings
int check(string s, int K)
{
    // Iterate over all possible characters
    for (int ch = 0; ch < 26; ch++) {
        char c = 'a' + ch;

        // stores the last occurrence
        int last = -1;

        // set answer as true;
        bool found = true;
        for (int i = 0; i < K; i++)
            if (s[i] == c)
                last = i;

        // No occurrence found of current
        // character in first substring
        // of length K
        if (last == -1)
            continue;

        // Check for every last substring
        // of length K where last occurr-
        // ence exists in substring
        for (int i = K; i < s.size(); i++) {
            if (s[i] == c)
                last = i;

            // If last occ is not
            // present in substring
            if (last <= (i - K)) {
                found = false;
                break;
            }
        }
        // current character is K amazing
        if (found)
            return 1;
    }
    return 0;
}

// This function performs binary search over the
// answer to minimise it
int binarySearch(string s)
{
    int low = 1, high = (int)s.size();
    int ans;
    while (low <= high) {
        int mid = (high + low) >> 1;

        // Check if answer is found try
        // to minimise it
        if (check(s, mid)) {
            ans = mid;
            high = mid - 1;
        }
        else
            low = mid + 1;
    }
    return ans;
}

// Driver Code to test above functions
int32_t main()
{
    string s = "abcde";
    cout << binarySearch(s) << endl;

    s = "aaaa";
    cout << binarySearch(s) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find minimum K such that
// every substring of length atleast K
// contains some character c

class GFG
{

        // This function checks if there exists some
        // character which appears in all K length
        // substrings
        static int check(String s, int K)
        {
            // Iterate over all possible characters
            for (int ch = 0; ch < 26; ch++) {
                char c = (char)( 'a' + ch);

                // stores the last occurrence
                int last = -1;

                // set answer as true;
                boolean found = true;
                for (int i = 0; i < K; i++)
                    if (s.charAt(i) == c)
                        last = i;

                // No occurrence found of current
                // character in first substring
                // of length K
                if (last == -1)
                    continue;

                // Check for every last substring
                // of length K where last occurr-
                // ence exists in substring
                for (int i = K; i < s.length(); i++) {
                    if (s.charAt(i) == c)
                        last = i;

                    // If last occ is not
                    // present in substring
                    if (last <= (i - K)) {
                        found = false;
                        break;
                    }
                }
                // current character is K amazing
                if (found)
                    return 1;
            }
            return 0;
        }

        // This function performs binary search over the
        // answer to minimise it
        static int binarySearch(String s)
        {
            int low = 1, high = s.length();
            int ans=0;
            while (low <= high) {
                int mid = (high + low) >> 1;

                // Check if answer is found try
                // to minimise it
                if (check(s, mid)==1) {
                    ans = mid;
                    high = mid - 1;
                }
                else
                    low = mid + 1;
            }
            return ans;
        }

        // Driver Code to test above functions
        public static void main(String args[])
        {
            String s = "abcde";
            System.out.println(binarySearch(s));

            s = "aaaa";
            System.out.println(binarySearch(s));

        }

}

// This article is contributed
// by ihritik
```

## 蟒蛇 3

```
# Python3 Program to find minimum K such
# that every substring of length atleast
# K contains some character c

# This function checks if there exists
# some character which appears in all
# K length substrings
def check(s, K):

    # Iterate over all possible characters
    for ch in range(0, 26):
        c = chr(97 + ch) # Ascii value of 'a' => 97

        # stores the last occurrence
        last = -1

        # set answer as true
        found = True
        for i in range(0, K):
            if s[i] == c:
                last = i

        # No occurrence found of current character
        # in first substring of length K
        if last == -1:
            continue

        # Check for every last substring
        # of length K where last occurr-
        # ence exists in substring
        for i in range(K, len(s)):
            if s[i] == c:
                last = i

            # If last occ is not
            # present in substring
            if last <= (i - K):
                found = False
                break

        # current character is K amazing
        if found:
            return 1

    return 0

# This function performs binary search
# over the answer to minimise it
def binarySearch(s):

    low, high, ans = 1, len(s), None

    while low <= high:
        mid = (high + low) >> 1

        # Check if answer is found
        # try to minimise it
        if check(s, mid):
            ans, high = mid, mid - 1

        else:
            low = mid + 1

    return ans

# Driver Code
if __name__ == "__main__":

    s = "abcde"
    print(binarySearch(s))

    s = "aaaa"
    print(binarySearch(s))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# Program to find minimum K such that
// every substring of length atleast K
// contains some character c

using System;
class GFG
{

        // This function checks if there exists some
        // character which appears in all K length
        // substrings
        static int check(String s, int K)
        {
            // Iterate over all possible characters
            for (int ch = 0; ch < 26; ch++) {
                char c = (char)( 'a' + ch);

                // stores the last occurrence
                int last = -1;

                // set answer as true;
                bool found = true;
                for (int i = 0; i < K; i++)
                    if (s[i] == c)
                        last = i;

                // No occurrence found of current
                // character in first substring
                // of length K
                if (last == -1)
                    continue;

                // Check for every last substring
                // of length K where last occurr-
                // ence exists in substring
                for (int i = K; i < s.Length; i++) {
                    if (s[i] == c)
                        last = i;

                    // If last occ is not
                    // present in substring
                    if (last <= (i - K)) {
                        found = false;
                        break;
                    }
                }
                // current character is K amazing
                if (found)
                    return 1;
            }
            return 0;
        }

        // This function performs binary search over the
        // answer to minimise it
        static int binarySearch(String s)
        {
            int low = 1, high = s.Length;
            int ans=0;
            while (low <= high) {
                int mid = (high + low) >> 1;

                // Check if answer is found try
                // to minimise it
                if (check(s, mid)==1) {
                    ans = mid;
                    high = mid - 1;
                }
                else
                    low = mid + 1;
            }
            return ans;
        }

        // Driver Code to test above functions
        public static void Main()
        {
            String s = "abcde";
            Console.WriteLine(binarySearch(s));

            s = "aaaa";
            Console.WriteLine(binarySearch(s));

        }

}

// This article is contributed
// by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php Program to find minimum K such that
// every substring of length atleast K
// contains some character c

// This function checks if there exists some
// character which appears in all K length
// substrings
function check($s, $K)
{
    // Iterate over all possible characters
    for ($ch = 0; $ch < 26; $ch++)
    {
        $c = chr(ord('a') + $ch) ;

        // stores the last occurrence
        $last = -1;

        // set answer as true;
        $found = true;
        for ($i = 0; $i < $K; $i++)
            if ($s[$i] == $c)
                $last = $i;

        // No occurrence found of current
        // character in first substring
        // of length K
        if ($last == -1)
            continue;

        // Check for every last substring
        // of length K where last occurr-
        // ence exists in substring
        for ($i = $K; $i < strlen($s); $i++)
        {
            if ($s[$i] == $c)
                $last = $i;

            // If last occ is not
            // present in substring
            if ($last <= ($i - $K))
            {
                $found = false;
                break;
            }
        }

        // current character is K amazing
        if ($found)
            return 1;
    }
    return 0;
}

// This function performs binary search
// over the answer to minimise it
function binarySearch($s)
{
    $low = 1 ;
    $high = strlen($s) ;
    while ($low <= $high)
    {
        $mid = ($high + $low) >> 1;

        // Check if answer is found try
        // to minimise it
        if (check($s, $mid))
        {
            $ans = $mid;
            $high = $mid - 1;
        }
        else
            $low = $mid + 1;
    }
    return $ans;
}

// Driver Code
$s = "abcde";
echo binarySearch($s) . "\n";

$s = "aaaa";
echo binarySearch($s) . "\n";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript Program to find minimum K such that
// every substring of length atleast K
// contains some character c

// This function checks if there exists some
// character which appears in all K length
// substrings
function check(s, K)
{
    // Iterate over all possible characters
    for (var ch = 0; ch < 26; ch++) {
        var c = String.fromCharCode('a'.charCodeAt(0) + ch);

        // stores the last occurrence
        var last = -1;

        // set answer as true;
        var found = true;
        for (var i = 0; i < K; i++)
            if (s[i] == c)
                last = i;

        // No occurrence found of current
        // character in first substring
        // of length K
        if (last == -1)
            continue;

        // Check for every last substring
        // of length K where last occurr-
        // ence exists in substring
        for (var i = K; i < s.length; i++) {
            if (s[i] == c)
                last = i;

            // If last occ is not
            // present in substring
            if (last <= (i - K)) {
                found = false;
                break;
            }
        }
        // current character is K amazing
        if (found)
            return 1;
    }
    return 0;
}

// This function performs binary search over the
// answer to minimise it
function binarySearch(s)
{
    var low = 1, high = s.length;
    var ans;
    while (low <= high) {
        var mid = (high + low) >> 1;

        // Check if answer is found try
        // to minimise it
        if (check(s, mid)) {
            ans = mid;
            high = mid - 1;
        }
        else
            low = mid + 1;
    }
    return ans;
}

// Driver Code to test above functions
var s = "abcde";
document.write( binarySearch(s) + "<br>");
s = "aaaa";
document.write( binarySearch(s) );

</script>
```

**Output:** 

```
3
1
```

**时间复杂度:** O(N * logN * 26)，其中 N 是给定字符串的大小。