# 和为 S 的最小数(小于或等于 N)

> 原文:[https://www . geesforgeks . org/minimum-numbers-小于或等于 n-with-sum-s/](https://www.geeksforgeeks.org/minimum-numbers-smaller-than-or-equal-to-n-with-sum-s/)

给定 N 个数字(1，2，3，…)。n)和一个数字 s .任务是打印相加得出的最小数字数 S.
**示例** :

> 输入:N = 5，S = 11
> 输出:3
> 三个数字(小于或等于 N)可以是任意给定的组合。
> (3、4、4)
> (2、4、5)
> (1、5、5)
> (3、3、5)
> 输入:N = 1，S = 10
> 输出:10

**逼近**:贪婪的我们尽可能多的选择 N，然后如果剩下的少于 N，我们就选择那个加起来就是 S 的数，因此总数是 **(S/N) + 1(如果 S%N > 0)** 。
以下是上述办法的实施情况。

## C++

```
// C++ program to find the minimum numbers
// required to get to S
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// numbers required to get to S
int minimumNumbers(int n, int s)
{
    if (s % n)
        return s / n + 1;
    else
        return s / n;
}

// Driver Code
int main()
{
    int n = 5;
    int s = 11;
    cout << minimumNumbers(n, s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum numbers
// required to get to S
import java.io.*;

class GFG {

// Function to find the minimum
// numbers required to get to S
static int minimumNumbers(int n, int s)
{
    if ((s % n)>0)
        return s / n + 1;
    else
        return s / n;
}

// Driver Code

    public static void main (String[] args) {
        int n = 5;
    int s = 11;
    System.out.println(minimumNumbers(n, s));
    }
}
// This code is contributed by shs..
```

## 蟒蛇 3

```
# Python 3 program to find the
# minimum numbers required to get to S

# Function to find the minimum
# numbers required to get to S
def minimumNumbers(n, s):

    if (s % n):
        return s / n + 1;
    else:
        return s / n;

# Driver Code
n = 5;
s = 11;
print(int(minimumNumbers(n, s)));

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# program to find the minimum numbers
// required to get to S
using System;

class GFG {

// Function to find the minimum
// numbers required to get to S
static int minimumNumbers(int n, int s)
{
    if ((s % n)>0)
        return s / n + 1;
    else
        return s / n;
}

// Driver Code

    public static void Main () {
        int n = 5;
    int s = 11;
    Console.WriteLine(minimumNumbers(n, s));
    }
}
// This code is contributed by shs..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the minimum numbers
// required to get to S

// Function to find the minimum
// numbers required to get to S
function minimumNumbers($n, $s)
{
    if ($s % $n)
        return round($s / $n + 1);
    else
        return round($s /$n);
}

// Driver Code
$n = 5;
$s = 11;
echo minimumNumbers($n, $s);

// This code is contributed by shs..
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the minimum numbers
// required to get to S

// Function to find the minimum
// numbers required to get to S
function minimumNumbers(n, s)
{
    if (s % n)
        return parseInt(s / n) + 1;
    else
        return parseInt(s / n);
}

// Driver Code
    let n = 5;
    let s = 11;
    document.write(minimumNumbers(n, s));

</script>
```

**Output:** 

```
3
```