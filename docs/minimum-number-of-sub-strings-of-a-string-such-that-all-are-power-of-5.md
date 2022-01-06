# 一串子串的最小数目，使得所有子串都是 5 的幂

> 原文:[https://www . geeksforgeeks . org/字符串中的最小子字符串数，这样所有子字符串都是 5 的幂/](https://www.geeksforgeeks.org/minimum-number-of-sub-strings-of-a-string-such-that-all-are-power-of-5/)

给定一个二进制字符串 **str** 。任务是找到最小的正整数 **C** ，这样二进制串就可以被切割成 **C** 段(子串)，每个子串应该是 5 的幂，没有前导零。
**举例:**

> **输入:** str = "101101101"
> **输出:** 3
> 字符串“101101101”可以被切割成三个二进制字符串“101”、“101”、“101”
> ，每个二进制字符串都是 5 的幂。
> **输入:** str = "1111101"
> **输出:** 1
> 字符串“1111101”可以切割成一个二进制字符串“1111101”，即十进制的
> 125 和 5 的幂。
> **输入:** str = "00000"
> **输出:** -1
> 只有零的字符串相当于 0，不是 5 的幂。

**方法:**这个问题是[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的简单变异。
从 **i = 1** 开始迭代，对于每一个**str【j…I】**其中**j = 0**&**j<I**，我们检查该数是否由**str【j】构成..i]** 是 **5** 的幂，那么我们用最小可能切割尺寸值的值更新 **dp[]** 数组。在确认由**字符串[j..十进制中的**是 **5** 的幂，我们计算 **dp[i] = min(dp[i]，dp[j] + 1)** 。
这种技术非常类似于寻找最长的递增子序列。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll unsigned long long

// Function that returns true
// if n is a power of 5
bool ispower(ll n)
{
    if (n < 125)
        return (n == 1 || n == 5 || n == 25);
    if (n % 125 != 0)
        return false;
    else
        return ispower(n / 125);
}

// Function to return the decimal
// value of binary equivalent
ll number(string s, int i, int j)
{
    ll ans = 0;
    for (int x = i; x < j; x++) {
        ans = ans * 2 + (s[x] - '0');
    }
    return ans;
}

// Function to return the minimum cuts required
int minCuts(string s, int n)
{
    int dp[n + 1];

    // Allocating memory for dp[] array
    memset(dp, n + 1, sizeof(dp));
    dp[0] = 0;

    // From length 1 to n
    for (int i = 1; i <= n; i++) {

        // If previous character is '0' then ignore
        // to avoid number with leading 0s.
        if (s[i - 1] == '0')
            continue;
        for (int j = 0; j < i; j++) {

            // Ignore s[j] = '0' starting numbers
            if (s[j] == '0')
                continue;

            // Number formed from s[j....i]
            ll num = number(s, j, i);

            // Check for power of 5
            if (!ispower(num))
                continue;

            // Assigning min value to get min cut possible
            dp[i] = min(dp[i], dp[j] + 1);
        }
    }

    // (n + 1) to check if all the strings are traversed
    // and no divisible by 5 is obtained like 000000
    return ((dp[n] < n + 1) ? dp[n] : -1);
}

// Driver code
int main()
{
    string s = "101101101";
    int n = s.length();
    cout << minCuts(s, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function that returns true
    // if n is a power of 5
    static boolean ispower(long n)
    {
        if (n < 125)
        {
            return (n == 1 || n == 5 || n == 25);
        }
        if (n % 125 != 0)
        {
            return false;
        }
        else
        {
            return ispower(n / 125);
        }
    }

    // Function to return the decimal
    // value of binary equivalent
    static long number(String s, int i, int j)
    {
        long ans = 0;
        for (int x = i; x < j; x++)
        {
            ans = ans * 2 + (s.charAt(x) - '0');
        }
        return ans;
    }

    // Function to return the minimum cuts required
    static int minCuts(String s, int n)
    {
        int[] dp = new int[n + 1];

        // Alongocating memory for dp[] array
        Arrays.fill(dp, n+1);
        dp[0] = 0;

        // From length 1 to n
        for (int i = 1; i <= n; i++)
        {

            // If previous character is '0' then ignore
            // to avoid number with leading 0s.
            if (s.charAt(i - 1) == '0')
            {
                continue;
            }
            for (int j = 0; j < i; j++)
            {

                // Ignore s[j] = '0' starting numbers
                if (s.charAt(j) == '0')
                {
                    continue;
                }

                // Number formed from s[j....i]
                long num = number(s, j, i);

                // Check for power of 5
                if (!ispower(num))
                {
                    continue;
                }

                // Assigning min value to get min cut possible
                dp[i] = Math.min(dp[i], dp[j] + 1);
            }
        }

        // (n + 1) to check if all the Strings are traversed
        // and no divisible by 5 is obtained like 000000
        return ((dp[n] < n + 1) ? dp[n] : -1);
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "101101101";
        int n = s.length();
        System.out.println(minCuts(s, n));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns true
# if n is a power of 5
def ispower( n):
    if (n < 125):
        return (n == 1 or n == 5 or n == 25)
    if (n % 125 != 0):
        return 0
    else:
        return ispower(n // 125)

# Function to return the decimal
# value of binary equivalent
def number(s, i, j):
    ans = 0
    for x in range( i, j) :
        ans = ans * 2 + (ord(s[x]) - ord('0'))
    return ans

# Function to return the minimum cuts required
def minCuts(s, n):

    # Allocating memory for dp[] array
    dp=[n+1 for i in range(n+1)]
    dp[0] = 0;

    # From length 1 to n
    for i in range(1, n+1) :

        # If previous character is '0' then ignore
        # to avoid number with leading 0s.
        if (s[i - 1] == '0'):
            continue
        for j in range(i) :

            # Ignore s[j] = '0' starting numbers
            if (s[j] == '0'):
                continue

            # Number formed from s[j....i]
            num = number(s, j, i)

            # Check for power of 5
            if (not ispower(num)):
                continue

            # Assigning min value to get min cut possible
            dp[i] = min(dp[i], dp[j] + 1)

    # (n + 1) to check if all the strings are traversed
    # and no divisible by 5 is obtained like 000000
    if dp[n] < n + 1:
        return dp[n]
    else:
        return  -1

# Driver code
if __name__== "__main__":
    s = "101101101"
    n = len(s)
    print(minCuts(s, n))

# This code is contributed by ChitraNayal
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true
    // if n is a power of 5
    static Boolean ispower(long n)
    {
        if (n < 125)
        {
            return (n == 1 || n == 5 || n == 25);
        }
        if (n % 125 != 0)
        {
            return false;
        }
        else
        {
            return ispower(n / 125);
        }
    }

    // Function to return the decimal
    // value of binary equivalent
    static long number(String s, int i, int j)
    {
        long ans = 0;
        for (int x = i; x < j; x++)
        {
            ans = ans * 2 + (s[x] - '0');
        }
        return ans;
    }

    // Function to return the minimum cuts required
    static int minCuts(String s, int n)
    {
        int[] dp = new int[n + 1];

        // Alongocating memory for dp[] array
        for (int i = 0; i <= n; i++)
            dp[i]=n+1;
        dp[0] = 0;

        // From length 1 to n
        for (int i = 1; i <= n; i++)
        {

            // If previous character is '0' then ignore
            // to avoid number with leading 0s.
            if (s[i - 1] == '0')
            {
                continue;
            }
            for (int j = 0; j < i; j++)
            {

                // Ignore s[j] = '0' starting numbers
                if (s[j] == '0')
                {
                    continue;
                }

                // Number formed from s[j....i]
                long num = number(s, j, i);

                // Check for power of 5
                if (!ispower(num))
                {
                    continue;
                }

                // Assigning min value to get min cut possible
                dp[i] = Math.Min(dp[i], dp[j] + 1);
            }
        }

        // (n + 1) to check if all the Strings are traversed
        // and no divisible by 5 is obtained like 000000
        return ((dp[n] < n + 1) ? dp[n] : -1);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "101101101";
        int n = s.Length;
        Console.WriteLine(minCuts(s, n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true
// if n is a power of 5
function ispower($n)
{
    if ($n < 125)
        return ($n == 1 || $n == 5 || $n == 25);
    if ($n % 125 != 0)
        return false;
    else
        return ispower($n / 125);
}

// Function to return the decimal
// value of binary equivalent
function number($s, $i, $j)
{
    $ans = 0;
    for ($x = $i; $x < $j; $x++)
    {
        $ans = $ans * 2 + (ord($s[$x]) - ord('0'));
    }
    return $ans;
}

// Function to return the minimum cuts required
function minCuts($s, $n)
{
    // Allocating memory for dp[] array
    $dp = array_fill(0,$n + 1,$n + 1);

    $dp[0] = 0;

    // From length 1 to n
    for ($i = 1; $i <= $n; $i++)
    {

        // If previous character is '0' then ignore
        // to avoid number with leading 0s.
        if ($s[$i - 1] == '0')
            continue;
        for ($j = 0; $j < $i; $j++)
        {

            // Ignore s[j] = '0' starting numbers
            if ($s[$j] == '0')
                continue;

            // Number formed from s[j....i]
            $num = number($s, $j, $i);

            // Check for power of 5
            if (!ispower($num))
                continue;

            // Assigning min value to get min cut possible
            $dp[$i] = min($dp[$i], $dp[$j] + 1);
        }
    }

    // (n + 1) to check if all the strings are traversed
    // and no divisible by 5 is obtained like 000000
    return (($dp[$n] < $n + 1) ? $dp[$n] : -1);
}

    // Driver code
    $s = "101101101";
    $n = strlen($s);
    echo minCuts($s, $n);

    // This code is contributed by AnkitRai01

?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true
// if n is a power of 5
function ispower(n)
{
    if (n < 125)
        return (n == 1 || n == 5 || n == 25);
    if (n % 125 != 0)
        return false;
    else
        return ispower(parseInt(n / 125));
}

// Function to return the decimal
// value of binary equivalent
function number(s, i, j)
{
    var ans = 0;
    for (var x = i; x < j; x++) {
        ans = ans * 2 + (s[x] - '0');
    }
    return ans;
}

// Function to return the minimum cuts required
function minCuts(s, n)
{
    var dp = Array(n+1).fill(n+1);
    dp[0] = 0;

    // From length 1 to n
    for (var i = 1; i <= n; i++) {

        // If previous character is '0' then ignore
        // to avoid number with leading 0s.
        if (s[i - 1] == '0')
            continue;
        for (var j = 0; j < i; j++) {

            // Ignore s[j] = '0' starting numbers
            if (s[j] == '0')
                continue;

            // Number formed from s[j....i]
            var num = number(s, j, i);

            // Check for power of 5
            if (!ispower(num))
                continue;

            // Assigning min value to get min cut possible
            dp[i] = Math.min(dp[i], dp[j] + 1);
        }
    }

    // (n + 1) to check if all the strings are traversed
    // and no divisible by 5 is obtained like 000000
    return ((dp[n] < n + 1) ? dp[n] : -1);
}

// Driver code
var s = "101101101";
var n = s.length;
document.write( minCuts(s, n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(n)<sup>2</sup>)
T5】空间复杂度: O(n)