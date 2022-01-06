# 将 A 的部分数字替换为 B 的数字

，使 A 的值最大化

> 原文:[https://www . geeksforgeeks . org/通过用 b 位数替换其部分位数来最大化 a 的价值/](https://www.geeksforgeeks.org/maximize-the-value-of-a-by-replacing-some-of-its-digits-with-digits-of-b/)

给定两个代表两个整数的字符串 **A** 和 **B** ，任务是将 **A** 的 0 位或 0 位以上替换为 **B** 的任意一位后，打印 **A** 的最大值。
**注**:B 中的一位数字只能使用一次。
**举例:**

> **输入:** A = "1234 "，B = " 4321 "
> T3】输出: 4334
> 1 可以换成 4，2 可以换成 3。
> **输入:**A =“1002”，B =“100”
> **输出:** 1102
> 前 0 可以换成 1。

**方法:**由于 **A** 的值必须最大化，任何数字都将被更大值的数字替换。左边的数字对数值的贡献更大，所以应该用尽可能大的数值来代替。排序 **B** 并在 **A** 中从左向右迭代，如果可能的话尝试用最大可用选项替换当前数字。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximized value of A
string maxValue(string a, string b)
{
    // Sort digits in ascending order
    sort(b.begin(), b.end());
    int n = a.length();
    int m = b.length();

    // j points to largest digit in B
    int j = m - 1;
    for (int i = 0; i < n; i++) {

        // If all the digits of b have been used
        if (j < 0)
            break;

        if (b[j] > a[i]) {
            a[i] = b[j];

            // Current digit has been used
            j--;
        }
    }

    // Return the maximized value
    return a;
}

// Driver code
int main()
{
    string a = "1234";
    string b = "4321";

    cout << maxValue(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.util.*;

class GFG{

// Function to return the maximized value of A
static String maxValue(char []a, char []b)
{
    // Sort digits in ascending order
    Arrays.sort(b);
    int n = a.length;
    int m = b.length;

    // j points to largest digit in B
    int j = m - 1;
    for (int i = 0; i < n; i++) {

        // If all the digits of b have been used
        if (j < 0)
            break;

        if (b[j] > a[i]) {
            a[i] = b[j];

            // Current digit has been used
            j--;
        }
    }

    // Return the maximized value
    return String.valueOf(a);
}

// Driver code
public static void main(String[] args)
{
    String a = "1234";
    String b = "4321";

    System.out.print(maxValue(a.toCharArray(), b.toCharArray()));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximized
# value of A
def maxValue(a, b):

    # Sort digits in ascending order
    b = sorted(b)
    bi = [i for i in b]
    ai = [i for i in a]

    n = len(a)
    m = len(b)

    # j points to largest digit in B
    j = m - 1
    for i in range(n):

        # If all the digits of b
        # have been used
        if (j < 0):
            break

        if (bi[j] > ai[i]):
            ai[i] = bi[j]

            # Current digit has been used
            j -= 1

    # Return the maximized value
    x = "" . join(ai)
    return x

# Driver code
a = "1234"
b = "4321"

print(maxValue(a, b))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximized value of A
static String maxValue(char []a, char []b)
{
    // Sort digits in ascending order
    Array.Sort(b);
    int n = a.Length;
    int m = b.Length;

    // j points to largest digit in B
    int j = m - 1;
    for (int i = 0; i < n; i++)
    {

        // If all the digits of b have been used
        if (j < 0)
            break;

        if (b[j] > a[i])
        {
            a[i] = b[j];

            // Current digit has been used
            j--;
        }
    }

    // Return the maximized value
    return String.Join("",a);
}

// Driver code
public static void Main(String[] args)
{
    String a = "1234";
    String b = "4321";

    Console.Write(maxValue(a.ToCharArray(), b.ToCharArray()));
}
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximized value of A
function maxValue($a, $b)
{
    // Sort digits in ascending order
    sort($b);
    $n = sizeof($a);
    $m = sizeof($b);

    // j points to largest digit in B
    $j = $m - 1;
    for ($i = 0; $i < $n; $i++)
    {

        // If all the digits of b have been used
        if ($j < 0)
            break;

        if ($b[$j] > $a[$i])
        {
            $a[$i] = $b[$j];

            // Current digit has been used
            $j--;
        }
    }

    // Convert array into string
    $a = implode("",$a);

    // Return the maximized value
    return $a ;
}

    // Driver code
    # convert string into array
    $a = str_split("1234");
    $b = str_split("4321");

    echo maxValue($a, $b);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the maximized value of A
function maxValue(a,b)
{
    // Sort digits in ascending order
    b.sort(function(x,y){return x-y;});
    let n = a.length;
    let m = b.length;

    // j points to largest digit in B
    let j = m - 1;
    for (let i = 0; i < n; i++) {

        // If all the digits of b have been used
        if (j < 0)
            break;

        if (b[j] > a[i]) {
            a[i] = b[j];

            // Current digit has been used
            j--;
        }
    }

    // Return the maximized value
    return (a).join("");
}

// Driver code
let a = "1234";
let b = "4321";

document.write(maxValue(a.split(""), b.split("")));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
4334
```