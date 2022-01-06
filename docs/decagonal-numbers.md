# 十边形数字

> 原文:[https://www.geeksforgeeks.org/decagonal-numbers/](https://www.geeksforgeeks.org/decagonal-numbers/)

给你一个数 n，任务是找到第 n 个十边形数。十边形数是一个将三角形和正方形的概念扩展到十边形(一个十边形)的图形数。第 n 个十边形数计算 n 个嵌套十边形图案中的点数，所有十边形共享一个公共角，其中图案中的第 I 个十边形具有由 I 个点组成的边，这些点相互间隔一个单位。

示例:

```
Input : n = 3
Output : 27

Input : n = 7
Output : 175

```

第 n 个十边形数由公式
**(4n<sup>2</sup>–3n)**给出。

## C++

```
// C++ program to find nth decagonal number
#include <bits/stdc++.h>
using namespace std;

// Function to calculate decagonal number
int decagonal(int n)
{
    // Formula for finding nth decagonal number
    return 4 * n * n - 3 * n;
}

// Driver function
int main()
{
    int n = 10;
    cout << n << "th decagonal number :" << decagonal(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Decagonal Numbers
import java.util.*;

class GFG {

    // Function to calculate
    // decagonal number
    static int decagonal(int n)
    {
        // Formula for finding nth
        // decagonal number
        return 4 * n * n - 3 * n;
    }

    /* Driver function */
    public static void main(String[] args)
    {   
        int n = 10;
        System.out.println(n + "th decagonal number :"
                            + decagonal(n));
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 计算机编程语言

```
# Python program to find nth decagonal number
def decagonal(n):
    return 4 * n * n - 3 * n

# Driver code
n = 10
print(n, "th decagonal number :", decagonal(n))
```

## C#

```
// C# Code for Decagonal Numbers
using System;

class GFG {

    // Function to calculate
    // decagonal number
    static int decagonal(int n)
    {
        // Formula for finding nth
        // decagonal number
        return 4 * n * n - 3 * n;
    }

    // Driver Code
    public static void Main()
    {
        int n = 10;
        Console.Write(n + "th decagonal number : "
                                   + decagonal(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find nth
// decagonal number

// Function to calculate
// decagonal number
function decagonal($n)
{

    // Formula for finding nth
    // decagonal number
    return 4 * $n * $n - 3 * $n;
}

// Driver function
$n = 10;
echo $n, "th decagonal number :",
                 decagonal($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program for Decagonal Numbers

// Function to calculate
// decagonal number
function decagonal(n)
{

    // Formula for finding nth
    // decagonal number
    return 4 * n * n - 3 * n;
}

// Driver code
let n = 10;
document.write(n + "th decagonal number : " +
               decagonal(n));

// This code is contributed by souravghosh0416

</script>
```

**输出:**

```
10th decagonal number : 370
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)