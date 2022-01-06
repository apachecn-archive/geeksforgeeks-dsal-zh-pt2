# 由 k 个串联形成的字符串中最长的 0 子串

> 原文:[https://www . geesforgeks . org/k-concations 形成的字符串中最长的 0 子字符串/](https://www.geeksforgeeks.org/longest-substring-of-0s-in-a-string-formed-by-k-concatenations/)

给定一个长度为 **n** 的二进制字符串和一个整数 **k** 。考虑另一个由给定的二进制字符串 k 次串联而成的字符串 T。任务是打印只包含零的 T 的子串的最大大小。
**例:**

> 输入:str = 110010，k = 3
> 输出:2
> str = 110010 T = 110010110010(经过 3 次
> 串联形成的字符串)。因此，仅包含
> 零的 T(110010110010110010)的
> 子串的最大大小是 2。
> 输入:str = 00100110，k = 5
> 输出:3
> 这里，str = 00100110，T = 0010001000100100110
> 00100110001001001000110。所以，只包含零的 T 的子串
> 的最大大小是 3。

一种**简单的方法**是连接 K 个字符串副本，遍历所有元素，计算仅包含零的子字符串的最大大小。
T3【高效途径】T4:

> 不需要连接 K 个副本。
> 
> 1.  如果字符串只包含零，那么答案是字符串的长度。
> 2.  如果字符串由 0 和 1 组成，那么答案要么是只包含 0 的字符串的子字符串的最大长度，要么是只包含 0 的 A 的前缀长度和只包含 0 的字符串的后缀长度之和。
> 3.  需要注意的一点是，如果 K=1，则不需要前缀和后缀检查。

## C++

```
// C++ code to find maximum length
// of substring that contains only 0's
#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum length
// of substring containing only zero
int subzero(string str, int k)
{
    int ans = 0, curr = 0;
    int len = str.length();

    // loop to first calculate longest substring
    // in string
    for (int i = 0; i < len; ++i) {
        if (str[i] == '0')
            curr++;
        else
            curr = 0;

        ans = max(ans, curr);
    }

    // if all elements in string  are '0'
    if (ans == len)
        return len * k;

    // Else, find size of prefix and
    // suffix containing only zeroes
    else {
        int pre = 0, suff = 0;

        // Calculate prefix containing only zeroes
        for (int i = 0; i < len; i++) {
            if (str[i] == '0')
                pre++;
            else
                break;
        }

        // Calculate suffix containing only zeroes
        for (int i = len - 1; i >= 0; i--) {
            if (str[i] == '0')
                suff++;
            else
                break;
        }

        // if k<=1 then there is no need to take
        // prefix + suffix into account
        if (k > 1)
            ans = max(ans, pre + suff);
        return ans;
    }
}

// Drivers code
int main()
{
    string str = "00100110";
    int k = 5;
    cout << subzero(str, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find maximum length
// of substring that contains only 0's
import java.io.*;
import java.util.*;
import java.lang.*;

class GfG {

    // Function to calculate maximum length
    // of substring containing only zero
    public static int subzero(String s, int k)
    {
        int ans = 0, curr = 0;
        int len = s.length();
        char[] str = s.toCharArray();

        // loop to first calculate longest
        // substring in string
        for (int i = 0; i < len; ++i) {
            if (str[i] == '0')
                curr++;
            else
                curr = 0;

            ans = Math.max(ans, curr);
        }

        // if all elements in string are '0'
        if (ans == len)
            return len * k;

        // Else, find size of prefix and
        // suffix containing only zeroes
        else {
            int pre = 0, suff = 0;

            // Calculate prefix containing
            // only zeroes
            for (int i = 0; i < len; i++) {
                if (str[i] == '0')
                    pre++;
                else
                    break;
            }

            // Calculate suffix containing
            // only zeroes
            for (int i = len - 1; i >= 0; i--)
            {
                if (str[i] == '0')
                    suff++;
                else
                    break;
            }

            // if k<=1 then there is no need to
            // take prefix + suffix into account
            if (k > 1)
                ans = Math.max(ans, pre + suff);
            return ans;
        }
    }

    // Drivers code
    public static void main(String[] args)
    {
        String str = "00100110";
        int k = 5;
        System.out.println(subzero(str, k));
    }
}

// This code is contributed by Sagar Shukla
```

## 计算机编程语言

```
# Python code calculate maximum length of substring
# containing only zero
def subzero(str, k):
    ans = 0
    curr = 0
    n = len(str)

    # loop to calculate longest substring in string
    # containing 0's
    for i in str:
        if (i =='0'):
            curr+= 1

        else:
            curr = 0
        ans = max(ans, curr)
    # if all elements in string a are '0'
    if (ans == n):
        print(n * k)
        return

    # Else, find prefix and suffix containing
    # only zeroes
    else:
        pre = suff = 0

        # Calculate length of the  prefix containing
        # only zeroes
        for i in str:
            if(i =='0'):
                pre+= 1
            else:
                break

        # Calculate length of the suffix containing
        # only zeroes
        for i in range(n-1, -1, -1):
            if(str[i]=='0'):
                suff+= 1
            else:
                break

    # if k<= 1, no need to take suffix + prefix
    # into account
    if (k > 1):
        ans = max(ans, pre + suff)
    print(ans)
    return

# Driver program to test above function
k = 5
str ='00100110'
subzero(str, k)
```

## C#

```
// C# code to find maximum length
// of substring that contains only 0's
using System;

class GFG
{

// Function to calculate maximum length
// of substring containing only zero
public static int subzero(String s, int k)
{
    int ans = 0, curr = 0;
    int len = s.Length;
    char[] str = s.ToCharArray();

    // loop to first calculate longest
    // substring in string
    for (int i = 0; i < len; ++i)
    {
        if (str[i] == '0')
            curr++;
        else
            curr = 0;

        ans = Math.Max(ans, curr);
    }

    // if all elements in string are '0'
    if (ans == len)
        return len * k;

    // Else, find size of prefix and
    // suffix containing only zeroes
    else
    {
        int pre = 0, suff = 0;

        // Calculate prefix containing
        // only zeroes
        for (int i = 0; i < len; i++)
        {
            if (str[i] == '0')
                pre++;
            else
                break;
        }

        // Calculate suffix containing
        // only zeroes
        for (int i = len - 1; i >= 0; i--)
        {
            if (str[i] == '0')
                suff++;
            else
                break;
        }

        // if k<=1 then there is no need to
        // take prefix + suffix into account
        if (k > 1)
            ans = Math.Max(ans, pre + suff);
        return ans;
    }
}

// Driver code
public static void Main()
{
    String str = "00100110";
    int k = 5;
    Console.Write(subzero(str, k));
}
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find maximum length
// of substring that contains only 0's

// Function to calculate maximum length
// of substring containing only zero
function subzero($str, $k)
{
    $ans = 0;
    $curr = 0;
    $len = strlen($str);

    // loop to first calculate longest substring
    // in string
    for ($i = 0; $i < $len; ++$i)
    {
        if ($str[$i] == '0')
            $curr++;
        else
            $curr = 0;

        $ans = max($ans, $curr);
    }

    // if all elements in string are '0'
    if ($ans == $len)
        return $len * $k;

    // Else, find size of prefix and
    // suffix containing only zeroes
    else
    {
        $pre = 0;
        $suff = 0;

        // Calculate prefix containing only zeroes
        for ($i = 0; $i < $len; $i++)
        {
            if ($str[$i] == '0')
                $pre++;
            else
                break;
        }

        // Calculate suffix containing only zeroes
        for ($i = $len - 1; $i >= 0; $i--)
        {
            if ($str[$i] == '0')
                $suff++;
            else
                break;
        }

        // if k<=1 then there is no need to take
        // prefix + suffix into account
        if ($k > 1)
            $ans = max($ans, $pre + $suff);
        return $ans;
    }
}

// Driver code
$str = "00100110";
$k = 5;
echo subzero($str, $k);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript code to find maximum length
// of substring that contains only 0's

    // Function to calculate maximum length
    // of substring containing only zero
    function subzero(s,k)
    {
        let ans = 0, curr = 0;
        let len = s.length;
        let str = s.split("");

        // loop to first calculate longest
        // substring in string
        for (let i = 0; i < len; ++i) {
            if (str[i] == '0')
                curr++;
            else
                curr = 0;

            ans = Math.max(ans, curr);
        }

        // if all elements in string are '0'
        if (ans == len)
            return len * k;

        // Else, find size of prefix and
        // suffix containing only zeroes
        else {
            let pre = 0, suff = 0;

            // Calculate prefix containing
            // only zeroes
            for (let i = 0; i < len; i++) {
                if (str[i] == '0')
                    pre++;
                else
                    break;
            }

            // Calculate suffix containing
            // only zeroes
            for (let i = len - 1; i >= 0; i--)
            {
                if (str[i] == '0')
                    suff++;
                else
                    break;
            }

            // if k<=1 then there is no need to
            // take prefix + suffix into account
            if (k > 1)
                ans = Math.max(ans, pre + suff);
            return ans;
        }
    }

    // Drivers code
    let str = "00100110";
    let k = 5;
    document.write(subzero(str, k));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(n)