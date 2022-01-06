# 求前 N 个自然数的平均值

> 原文:[https://www . geesforgeks . org/find-average-first-n-natural-numbers/](https://www.geeksforgeeks.org/find-average-first-n-natural-numbers/)

写一个程序，求前 N 个自然数的平均值。
示例:

```
Input  : 10
Output : 5.5
1+2+3+4+5+6+7+8+9+10 = 5.5

Input  : 7
Output : 4.0
1+2+3+4+5+6+7 = 4
```

前提条件:[前 n 个自然数之和](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)。
如前一帖所述，n 个自然数的和 n(n+1)/2，我们求出 n 个自然数的平均值，所以除以 n 就是 n(n+1)/2*n = (n+1)/2。这里 1 是第一项，n 是最后一项。

## C++

```
// CPP Program to find the Average of first
// n natural numbers
#include <bits/stdc++.h>
using namespace std;

// Return the average of first n natural numbers
float avgOfFirstN(int n)
{
    return (float)(1 + n)/2;
}

// Driven Program
int main()
{
    int n = 20;
    cout << avgOfFirstN(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the Average of first
// n natural numbers
import java.io.*;

class GFG {

    // Return the average of first n
    // natural numbers
    static float avgOfFirstN(int n)
    {
        return (float)(1 + n) / 2;
    }

    // Driven Program
    public static void main(String args[])
    {
        int n = 20;
        System.out.println(avgOfFirstN(n));
    }
}

/*This code is contributed by Nikita tiwari.*/
```

## 蟒蛇 3

```
# Python 3 Program to find the Average
# of first n natural numbers

# Return the average of first n
# natural numbers
def avgOfFirstN(n) :
    return (float)(1 + n) / 2;

# Driven Program
n = 20
print(avgOfFirstN(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C#Program to find the Average of first
// n natural numbers
using System;

class GFG {

    // Return the average of first n
    // natural numbers
    static float avgOfFirstN(int n)
    {
        return (float)(1 + n) / 2;
    }

    // Driven Program
    public static void Main()
    {
        int n = 20;
        Console.WriteLine(avgOfFirstN(n));
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find
// the Average of first
// n natural numbers

// Return the average
// of first n natural
// numbers
function avgOfFirstN($n)
{
    return (float)(1 + $n) / 2;
}

// Driver Code
$n = 20;
echo(avgOfFirstN($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// javascript Program to find the Average of first
// n natural numbers

// Return the average of first n natural numbers
function avgOfFirstN( n)
{
    return (1 + n)/2;
}

// Driven Program

    let n = 20;
    document.write(avgOfFirstN(n));

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
10.5
```

**时间复杂度:O(1)**