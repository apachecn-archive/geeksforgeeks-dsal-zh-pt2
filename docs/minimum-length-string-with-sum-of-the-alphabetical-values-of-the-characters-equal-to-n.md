# 字符字母值之和等于 N 的最小长度字符串

> 原文:[https://www . geesforgeks . org/最小长度字符串加上字母值总和等于 n/](https://www.geeksforgeeks.org/minimum-length-string-with-sum-of-the-alphabetical-values-of-the-characters-equal-to-n/)

给定一个整数 N，任务是找到每个字符(As a = 1，b = 2，… z = 26)之和等于 N 的最小长度字符串。
**示例:**

```
Input: N = 5
Output: e
5 can be represented as "aac" or "ad" or "e" etc
But we will take e as it is the minimum length

Input: N = 34
Output: zj
```

**进场:**

*   为了最小化字符串的长度，将使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)。
*   通过贪婪方法，解决方案将非常简单。
*   绳子的最小长度为

```
N/26 + 1 => if N % 26 != 0
N/26     => if N % 26 == 0
```

*   而最小的字符串可以找到

```
(N/26 times z) + (N%26) => if N % 26 != 0
(N/26 times z)          => if N % 26 == 0
```

以下是上述方法的实现:

## C++

```
// C++ program to find the Minimum length String
// with Sum of the alphabetical values
// of the characters equal to N

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum length
int minLength(int n)
{
    int ans = n / 26;
    if (n % 26 != 0)
        ans++;

    return ans;
}

// Function to find the minimum length String
string minString(int n)
{
    int ans = n / 26;
    string res = "";

    while (ans--) {
        res = res + "z";
    }

    if (n % 26 != 0) {
        res = res
              + (char)((n % 26) + 96);
    }

    return res;
}

// Driver code
int main()
{
    int n = 50;

    cout << minLength(n)
         << endl
         << minString(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Minimum length String
// with Sum of the alphabetical values
// of the characters equal to N
class GFG
{

    // Function to find the minimum length
    static int minLength(int n)
    {
        int ans = n / 26;
        if (n % 26 != 0)
            ans++;

        return ans;
    }

    // Function to find the minimum length String
    static String minString(int n)
    {
        int ans = n / 26;
        String res = "";

        while (ans-- != 0)
        {
            res = res + "z";
        }

        if (n % 26 != 0)
        {
            res = res + (char)((n % 26) + 96);
        }

        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 50;

        System.out.println(minLength(n));
        System.out.println(minString(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find the Minimum length String
# with Sum of the alphabetical values
# of the characters equal to N

# Function to find the minimum length
def minLength(n):
    ans = n // 26
    if (n % 26 != 0):
        ans += 1

    return ans

# Function to find the minimum length String
def minString(n):
    ans = n // 26
    res = ""

    while (ans):
        res = res + "z"
        ans-=1

    if (n % 26 != 0):
        res = res + chr((n % 26) + 96)

    return res

# Driver code
n = 50;

print(minLength(n))
print(minString(n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# iprogram to find the Minimum length String
// with Sum of the alphabetical values
// of the characters equal to N
using System;

class GFG
{

    // Function to find the minimum length
    static int minLength(int n)
    {
        int ans = n / 26;
        if (n % 26 != 0)
            ans++;

        return ans;
    }

    // Function to find the minimum length String
    static String minString(int n)
    {
        int ans = n / 26;
        String res = "";

        while (ans-- != 0)
        {
            res = res + "z";
        }

        if (n % 26 != 0)
        {
            res = res + (char)((n % 26) + 96);
        }
        return res;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 50;

        Console.WriteLine(minLength(n));
        Console.WriteLine(minString(n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find the Minimum length String
// with Sum of the alphabetical values
// of the characters equal to N

// Function to find the minimum length
function minLength(n)
{
    var ans = parseInt(n / 26);
    if (n % 26 != 0)
        ans++;

    return ans;
}

// Function to find the minimum length String
function minString(n)
{
    var ans = parseInt(n / 26);
    var res = "";

    while (ans--) {
        res = res + "z";
    }

    if (n % 26 != 0) {
        res = res
              + String.fromCharCode((n % 26) + 96);
    }

    return res;
}

// Driver code
var n = 50;
document.write(minLength(n)+"<br>" + minString(n));

</script>
```

**Output:** 

```
2
zx
```