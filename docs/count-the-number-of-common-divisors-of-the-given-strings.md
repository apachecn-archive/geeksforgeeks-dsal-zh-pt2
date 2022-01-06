# 统计给定字符串的公约数

> 原文:[https://www . geeksforgeeks . org/count-给定字符串的公约数/](https://www.geeksforgeeks.org/count-the-number-of-common-divisors-of-the-given-strings/)

给定两个字符串 **a** 和 **b** ，任务是计算两个字符串的公约数。一个字符串 **s** 是字符串 **t** 的除数，如果 **t** 可以通过多次重复 **s** 来生成。
**示例:**

> **输入:** a = "xaxa "，b = " xaxa "
> **输出:** 2
> 公约数为“xa”和“xa”
> **输入:** a = "bbbb "，b = "bbb"
> **输出:** 1
> 唯一公约数为“b”

**方法:**一个字符串 **s** 要成为字符串 **t** 的候选除数，必须满足以下条件:

1.  **s** 必须是 **t** 的前缀。
2.  **len(t) % len(s) = 0**

初始化**计数= 0** 并从第一个字符开始作为前缀的结束字符，检查前缀的长度是否除以两个字符串的长度，以及两个字符串中的前缀是否相同。如果**是**，则更新**计数=计数+ 1** 。对所有可能的前缀重复这些步骤。最后打印**计数**的值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if sub-string
// s[0...k] is repeated a number of times
// to generate string s
int check(string s, int k)
{
    for (int i = 0; i < s.length(); i++)
        if (s[i] != s[i % k])
            return false;

    return true;
}

// Function to return the count of common divisors
int countCommonDivisors(string a, string b)
{
    int ct = 0;
    int n = a.size(), m = b.size();
    for (int i = 1; i <= min(n, m); i++) {

        // If the length of the sub-string
        // divides length of both the strings
        if (n % i == 0 && m % i == 0)

            // If prefixes match in both the strings
            if (a.substr(0, i) == b.substr(0, i))

                // If both the strings can be generated
                // by repeating the current prefix
                if (check(a, i) && check(b, i))
                    ct++;
    }
    return ct;
}

// Driver code
int main()
{
    string a = "xaxa", b = "xaxaxaxa";

    cout << countCommonDivisors(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns true if sub-string
    // s[0...k] is repeated a number of times
    // to generate String s
    static boolean check(String s, int k)
    {
        for (int i = 0; i < s.length(); i++)
        {
            if (s.charAt(i) != s.charAt(i % k))
            {
                return false;
            }
        }
        return true;
    }

    // Function to return the
    // count of common divisors
    static int countCommonDivisors(String a, String b)
    {
        int ct = 0;
        int n = a.length(), m = b.length();
        for (int i = 1; i <= Math.min(n, m); i++)
        {

            // If the length of the sub-string
            // divides length of both the strings
            if (n % i == 0 && m % i == 0) 
            {
                // If prefixes match in both the strings
                if (a.substring(0, i).equals(b.substring(0, i)))
                // by repeating the current prefix
                {
                    // If both the strings can be generated
                    if (check(a, i) && check(b, i))
                    {
                        ct++;
                    }
                }
            }
        }
        return ct;
    }

    // Driver code
    public static void main(String[] args)
    {
        String a = "xaxa", b = "xaxaxaxa";
        System.out.println(countCommonDivisors(a, b));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function that returns true if sub-string
# s[0...k] is repeated a number of times
# to generate String s
def check(s, k):

    for i in range (0, len(s)):

        if (s[i] != s[i % k]):

            return False

    return True

# Function to return the
# count of common divisors
def countCommonDivisors(a, b):

    ct = 0
    n = len(a)
    m = len(b)
    for i in range(1, min(n, m) + 1):

        # If the length of the sub-string
        # divides length of both the strings
        if (n % i == 0 and m % i == 0):

            # If prefixes match in both the strings
            if (a[0 : i] == b[0 : i]) :

                # by repeating the current prefix

                # If both the strings can be generated
                if (check(a, i) and check(b, i)) :

                    ct = ct + 1

    return ct

# Driver code
a = "xaxa"
b = "xaxaxaxa"
print(countCommonDivisors(a, b))

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function that returns true if sub-string
// s[0...k] is repeated a number of times
// to generate String s
static bool check(string s, int k)
{
    for (int i = 0; i < s.Length; i++)
    {
        if (s[i] != s[i % k])
        {
            return false;
        }
    }
    return true;
}

// Function to return the count of
// common divisors
static int countCommonDivisors(string a,
                               string b)
{
    int ct = 0;
    int n = a.Length, m = b.Length;
    for (int i = 1;
             i <= Math.Min(n, m); i++)
    {

        // If the length of the sub-string
        // divides length of both the strings
        if (n % i == 0 && m % i == 0)
        {
            // If prefixes match in both the strings
            if (a.Substring(0, i) == (b.Substring(0, i)))

            // by repeating the current prefix
            {
                // If both the strings can be generated
                if (check(a, i) && check(b, i))
                {
                    ct++;
                }
            }
        }
    }
    return ct;
}

// Driver code
public static void Main()
{
    string a = "xaxa", b = "xaxaxaxa";
    Console.WriteLine(countCommonDivisors(a, b));
}
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if sub-string
// s[0...k] is repeated a number of times
// to generate string s
function check(s, k)
{
    for (var i = 0; i < s.length; i++)
        if (s[i] != s[i % k])
            return false;

    return true;
}

// Function to return the count of common divisors
function countCommonDivisors(a, b)
{
    var ct = 0;
    var n = a.length, m = b.length;
    for (var i = 1; i <= Math.min(n, m); i++) {

        // If the length of the sub-string
        // divides length of both the strings
        if (n % i == 0 && m % i == 0)

            // If prefixes match in both the strings
            if (a.substring(0, i) == b.substring(0, i))

                // If both the strings can be generated
                // by repeating the current prefix
                if (check(a, i) && check(b, i))
                    ct++;
    }
    return ct;
}

// Driver code
var a = "xaxa", b = "xaxaxaxa";
document.write( countCommonDivisors(a, b));

// This code is contributed by famously.
</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N * M)
T3】辅助空间: O(1)