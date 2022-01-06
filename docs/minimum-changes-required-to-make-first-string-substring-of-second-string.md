# 使第一个字符串成为第二个字符串的子字符串所需的最小更改数

> 原文:[https://www . geesforgeks . org/minimum-changes-required-make-first-string-substring-of-second-string/](https://www.geeksforgeeks.org/minimum-changes-required-to-make-first-string-substring-of-second-string/)

给定两条弦 S1 和 S2(大小 S1 <= Size of S2 ). The task is to find the minimum number of characters to be replaced in the string S2, such that the string S1 is a substring of S2.
**例** :

```
Input : S1 = cdef, S2 = abbdef
Output : 1

Input : S1 = gfg, S2 = fgg
Output : 2 
```

**进场:**

1.  穿越弦 S2
    *   从 S2 的每个索引中，检查 S1 长度的子串中不匹配字符的数量
    *   在*和*中存储和更新上一次和当前最少的误匹配
2.  返回到。

以下是上述方法的实现:

## C++

```
// CPP program to find the minimum number of
// characters to be replaced in string S2, such
// that S1 is a substring of S2

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of
// characters to be replaced in string S2, such
// that S1 is a substring of S2
int minimumChar(string S1, string S2)
{
    // Get the sizes of both strings
    int n = S1.size(), m = S2.size();

    int ans = INT_MAX;

    // Traverse the string S2
    for (int i = 0; i < m - n + 1; i++) {
        int minRemovedChar = 0;

        // From every index in S2, check the number of
        // mis-matching characters in substring of
        // length of S1
        for (int j = 0; j < n; j++) {
            if (S1[j] != S2[i + j]) {
                minRemovedChar++;
            }
        }

        // Take minimum of prev and current mis-match
        ans = min(minRemovedChar, ans);
    }

    // return answer
    return ans;
}

// Driver Code
int main()
{
    string S1 = "abc";
    string S2 = "paxzk";

    cout << minimumChar(S1, S2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// number of characters to be
// replaced in string S2, such
// that S1 is a substring of S2
import java.io.*;

class GFG
{

// Function to find the minimum
// number of characters to be
// replaced in string S2, such
// that S1 is a substring of S2
static int minimumChar(String S1,
                       String S2)
{
    // Get the sizes of both strings
    int n = S1.length();
    int m = S2.length();

    int ans = Integer.MAX_VALUE ;

    // Traverse the string S2
    for (int i = 0; i < m - n + 1; i++)
    {
        int minRemovedChar = 0;

        // From every index in S2, check
        // the number of mis-matching
        // characters in substring of
        // length of S1
        for (int j = 0; j < n; j++)
        {
            if (S1.charAt(j) != S2.charAt(i + j))
            {
                minRemovedChar++;
            }
        }

        // Take minimum of prev and
        // current mis-match
        ans = Math.min(minRemovedChar, ans);
    }

    // return answer
    return ans;
}

// Driver Code
public static void main (String[] args)
{
    String S1 = "abc";
    String S2 = "paxzk";

    System.out.println(minimumChar(S1, S2));
}
}

// This code is contributed by Shashank
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# number of characters to be replaced
# in string S2, such that S1 is a
# substring of S2
import sys

# Function to find the minimum number of
# characters to be replaced in string S2,
# such that S1 is a substring of S2
def minimumChar(S1, S2):

    # Get the sizes of both strings
    n, m = len(S1), len(S2)

    ans = sys.maxsize

    # Traverse the string S2
    for i in range(m - n + 1):
        minRemovedChar = 0

        # From every index in S2, check the
        # number of mis-matching characters
        # in substring of length of S1
        for j in range(n):
            if (S1[j] != S2[i + j]):
                minRemovedChar += 1

        # Take minimum of prev and
        # current mis-match
        ans = min(minRemovedChar, ans)

    # return answer
    return ans

# Driver Code
if __name__ == '__main__':
    S1 = "abc"
    S2 = "paxzk"
    print(minimumChar(S1, S2))

# This code is contributed
# by PrinciRaj1992
```

## C#

```
// C# program to find the minimum
// number of characters to be
// replaced in string S2, such
// that S1 is a substring of S2
using System;

class GFG
{

// Function to find the minimum
// number of characters to be
// replaced in string S2, such
// that S1 is a substring of S2
static int minimumChar(String S1,
                       String S2)
{
    // Get the sizes of both strings
    int n = S1.Length;
    int m = S2.Length;

    int ans = Int32.MaxValue ;

    // Traverse the string S2
    for (int i = 0; i < m - n + 1; i++)
    {
        int minRemovedChar = 0;

        // From every index in S2, check
        // the number of mis-matching
        // characters in substring of
        // length of S1
        for (int j = 0; j < n; j++)
        {
            if (S1[j] != S2[i + j])
            {
                minRemovedChar++;
            }
        }

        // Take minimum of prev and
        // current mis-match
        ans = Math.Min(minRemovedChar, ans);
    }

    // return answer
    return ans;
}

// Driver Code
public static void Main()
{
    String S1 = "abc";
    String S2 = "paxzk";

    Console.WriteLine(minimumChar(S1, S2));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the minimum
// number of characters to be replaced
// in string S2, such that S1 is a
// substring of S2

// Function to find the minimum number
// of characters to be replaced in
// string S2, such that S1 is a
// substring of S2
function minimumChar($S1, $S2)
{
    // Get the sizes of both strings
    $n = strlen($S1);
    $m = strlen($S2);

    $ans = PHP_INT_MAX;

    // Traverse the string S2
    for ($i = 0; $i < $m - $n + 1; $i++)
    {
        $minRemovedChar = 0;

        // From every index in S2, check
        // the number of mis-matching
        // characters in substring of
        // length of S1
        for ($j = 0; $j < $n; $j++)
        {
            if ($S1[$j] != $S2[$i + $j])
            {
                $minRemovedChar++;
            }
        }

        // Take minimum of prev and
        // current mis-match
        $ans = min($minRemovedChar, $ans);
    }

    // return answer
    return $ans;
}

// Driver Code
$S1 = "abc";
$S2 = "paxzk";

echo minimumChar($S1, $S2);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find the minimum
    // number of characters to be
    // replaced in string S2, such
    // that S1 is a substring of S2

    // Function to find the minimum
    // number of characters to be
    // replaced in string S2, such
    // that S1 is a substring of S2
    function minimumChar(S1, S2)
    {
        // Get the sizes of both strings
        let n = S1.length;
        let m = S2.length;

        let ans = Number.MAX_VALUE;

        // Traverse the string S2
        for (let i = 0; i < m - n + 1; i++)
        {
            let minRemovedChar = 0;

            // From every index in S2, check
            // the number of mis-matching
            // characters in substring of
            // length of S1
            for (let j = 0; j < n; j++)
            {
                if (S1[j] != S2[i + j])
                {
                    minRemovedChar++;
                }
            }

            // Take minimum of prev and
            // current mis-match
            ans = Math.min(minRemovedChar, ans);
        }

        // return answer
        return ans;
    }

    let S1 = "abc";
    let S2 = "paxzk";

    document.write(minimumChar(S1, S2));

</script>
```

**Output:** 

```
2
```

**时间复杂度** : O(N * M)。