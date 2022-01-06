# 重复 K 次的二进制串中 0 的最长子串

> 原文:[https://www . geesforgeks . org/二进制字符串中最长的 0 子字符串重复 k 次/](https://www.geeksforgeeks.org/longest-sub-string-of-0s-in-a-binary-string-which-is-repeated-k-times/)

给定大小为 **N** 的二进制字符串 **S** 和一个数字 **K** 。任务是在给定字符串重复 K 次形成的字符串中找到 0 的最长子字符串。
**举例:**

> **输入:** S = "100001 "，K = 3
> **输出:** 4
> 重复给定字符串 3 次后，字符串变为 1000011000011000001。
> 0 的最长子串为 4
> **输入:**S =“010001000”，K = 4
> **输出:** 4

**进场:**

1.  如果 **K 是一**，那么使用一个简单的循环找到一个字符串中最长的 0 的子串
2.  如果 **K 大于 1**，则在字符串末尾添加一个给定的字符串。然后字符串变成 S+S，长度为 2*N，使用简单的循环找到字符串中最长的子字符串 0
    *   如果最长的子串是 2*N，那么我们的答案将是 K*N
    *   否则这将是我们需要的答案

以下是上述方法的实现:

## C++

```
// C++ program to find the find the Longest continuous
// sequence of '0' after repeating Given string K time
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest substring of 0's
int longest_substring(string s, int k)
{
    // To store size of the string
    int n = s.size();

    if(k>1)
    {
        s += s;
        n *= 2;
    }   

    // To store the required answer
    int ans = 0;

    // Find the longest substring of 0's
    int i = 0;
    while (i < n)
    {
        int x = 0;

        // Run a loop upto s[i] is zero
        while (s[i] == '0' && i < n)
            x++, i++;
        ans = max(ans, x);
        i++;
    }

    // Check the conditions
    if(k==1 or ans!=n)
        return ans;

    else
        return (ans/2)*k;
}

// Driver code
int main()
{
    string s = "010001000";

    int k = 4;

    // Function call
    cout << longest_substring(s, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Longest continuous
// sequence of '0' after repeating Given string K time
class GFG
{

// Function to find the longest substring of 0's
static int longest_substring(String s, int k)
{
    // To store size of the string
    int n = s.length();

    if(k > 1)
    {
        s += s;
        n *= 2;
    }

    // To store the required answer
    int ans = 0;

    // Find the longest substring of 0's
    int i = 0;
    while (i < n)
    {
        int x = 0;

        // Run a loop upto s[i] is zero
        while (i < n && s.charAt(i) == '0')
        {
            x++; i++;
        }
        ans = Math.max(ans, x);
        i++;
    }

    // Check the conditions
    if(k == 1 || ans != n)
        return ans;

    else
        return (ans / 2) * k;
}

// Driver code
public static void main(String[] args)
{
    String s = "010001000";

    int k = 4;

    // Function call
    System.out.println(longest_substring(s, k));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the find the Longest continuous
# sequence of '0' after repeating Given K time

# Function to find the longest subof 0's
def longest_substring(s, k):
    # To store size of the string
    n = len(s)

    if(k>1):
        s += s
        n *= 2

    # To store the required answer
    ans = 0

    # Find the longest subof 0's
    i = 0
    while (i < n):
        x = 0

        # Run a loop upto s[i] is zero
        while (i < n and s[i] == '0'):
            x,i=x+1, i+1
        ans = max(ans, x)
        i+=1

    # Check the conditions
    if(k==1 or ans!=n):
        return ans

    else:
        return (ans//2)*k

# Driver code

s = "010001000"

k = 4

# Function call
print(longest_substring(s, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the Longest continuous
// sequence of '0' after repeating Given string K time
using System;

class GFG
{

// Function to find the longest substring of 0's
static int longest_substring(String s, int k)
{
    // To store size of the string
    int n = s.Length;

    if(k > 1)
    {
        s += s;
        n *= 2;
    }

    // To store the required answer
    int ans = 0;

    // Find the longest substring of 0's
    int i = 0;
    while (i < n)
    {
        int x = 0;

        // Run a loop upto s[i] is zero
        while (i < n && s[i] == '0')
        {
            x++; i++;
        }
        ans = Math.Max(ans, x);
        i++;
    }

    // Check the conditions
    if(k == 1 || ans != n)
        return ans;

    else
        return (ans / 2) * k;
}

// Driver code
public static void Main(String[] args)
{
    String s = "010001000";

    int k = 4;

    // Function call
    Console.WriteLine(longest_substring(s, k));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find the find the Longest continuous
// sequence of '0' after repeating Given string K time

// Function to find the longest substring of 0's
function longest_substring(s, k)
{
    // To store size of the string
    var n = s.length;

    if(k>1)
    {
        s += s;
        n *= 2;
    }   

    // To store the required answer
    var ans = 0;

    // Find the longest substring of 0's
    var i = 0;
    while (i < n)
    {
        var x = 0;

        // Run a loop upto s[i] is zero
        while (s[i] == '0' && i < n)
            x++, i++;
        ans = Math.max(ans, x);
        i++;
    }

    // Check the conditions
    if(k==1 || ans!=n)
        return ans;

    else
        return (ans/2)*k;
}

// Driver code
var s = "010001000";

var k = 4;

// Function call
document.write( longest_substring(s, k));

</script>
```

**输出:**

```
4
```