# 将一个字符串转换为另一个字符串所需的最小给定操作次数

> 原文:[https://www . geesforgeks . org/最小给定操作数-需要将一个字符串转换为另一个字符串/](https://www.geeksforgeeks.org/minimum-number-of-given-operations-required-to-convert-a-string-to-another-string/)

给定两条长度相等的弦 **S** 和 **T** 。两个字符串都只包含字符**“0”**和**“1”**。任务是找到将串 **S** 转换为 **T** 的最小操作次数。钻柱 **S** 上允许有两种操作:

*   交换字符串的任意两个字符。
*   用**“1”**代替**“0”**，反之亦然。

**示例:**

> **输入:** S = "011 "，T = "101"
> **输出:** 1
> 互换第一个和第二个字符。
> 
> **输入:**S =“010”，T =“101”
> **输出:** 2
> 互换第一个和第二个字符，将第三个字符替换为‘1’。

**方法:**为字符串 **S** 找到 2 个值，0 但应为 1 的索引数和 1 但应为 0 的索引数。结果将是这两个值中的最大值，因为我们可以对这两个值中的最小值使用互换，剩余的不匹配字符可以反转，即**“0”**可以更改为**“1”**和**“1”**可以更改为**“0”**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum operations
// of the given type required to convert
// string s to string t
int minOperations(string s, string t, int n)
{
    int ct0 = 0, ct1 = 0;
    for (int i = 0; i < n; i++) {

        // Characters are already equal
        if (s[i] == t[i])
            continue;

        // Increment count of 0s
        if (s[i] == '0')
            ct0++;

        // Increment count of 1s
        else
            ct1++;
    }

    return max(ct0, ct1);
}

// Driver code
int main()
{
    string s = "010", t = "101";
    int n = s.length();
    cout << minOperations(s, t, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the minimum
// operations of the given type required
// to convert string s to string t
static int minOperations(String s,
                        String t, int n)
{
    int ct0 = 0, ct1 = 0;
    for (int i = 0; i < n; i++)
    {

        // Characters are already equal
        if (s.charAt(i) == t.charAt(i))
            continue;

        // Increment count of 0s
        if (s.charAt(i) == '0')
            ct0++;

        // Increment count of 1s
        else
            ct1++;
    }

    return Math.max(ct0, ct1);
}

// Driver code
public static void main(String args[])
{
    String s = "010", t = "101";
    int n = s.length();
    System.out.println(minOperations(s, t, n));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the minimum operations
# of the given type required to convert
# string s to string t
def minOperations(s, t, n):

    ct0 = 0
    ct1 = 0
    for i in range(n):

        # Characters are already equal
        if (s[i] == t[i]):
            continue

        # Increment count of 0s
        if (s[i] == '0'):
            ct0 += 1

        # Increment count of 1s
        else:
            ct1 += 1

    return max(ct0, ct1)

# Driver code
if __name__ == "__main__":

    s = "010"
    t = "101"
    n = len(s)
    print(minOperations(s, t, n))

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to return the minimum operations
// of the given type required to convert
// string s to string t
static int minOperations(string s, 
                         string t, int n)
{
    int ct0 = 0, ct1 = 0;
    for (int i = 0; i < n; i++)
    {

        // Characters are already equal
        if (s[i] == t[i])
            continue;

        // Increment count of 0s
        if (s[i] == '0')
            ct0++;

        // Increment count of 1s
        else
            ct1++;
    }

    return Math.Max(ct0, ct1);
}

// Driver code
public static void Main()
{
    string s = "010", t = "101";
    int n = s.Length;
    Console.Write(minOperations(s, t, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum operations
// of the given type required to convert
// string s to string t
function minOperations($s, $t, $n)
{
    $ct0 = 0 ; $ct1 = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // Characters are already equal
        if ($s[$i] == $t[$i])
            continue;

        // Increment count of 0s
        if ($s[$i] == '0')
            $ct0++;

        // Increment count of 1s
        else
            $ct1++;
    }

    return max($ct0, $ct1);
}

// Driver code
$s = "010"; $t = "101";
$n = strlen($s);
echo minOperations($s, $t, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the minimum operations
// of the given type required to convert
// string s to string t
function minOperations(s, t, n)
{
    var ct0 = 0,
    ct1 = 0;
    for(var i = 0; i < n; i++)
    {
        // Characters are already equal
        if (s[i] === t[i])
            continue;

        // Increment count of 0s
        if (s[i] === "0")
            ct0++;

        // Increment count of 1s
        else
            ct1++;
    }
    return Math.max(ct0, ct1);
}

// Driver code
var s = "010",
t = "101";
var n = s.length;

document.write(minOperations(s, t, n));

// This code is contributed by rdtank

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)