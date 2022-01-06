# 十二边形数字

> 原文:[https://www.geeksforgeeks.org/dodecagonal-number/](https://www.geeksforgeeks.org/dodecagonal-number/)

给定一个数 n，求第 n 个十二边形数。[十二边形数字](https://en.wikipedia.org/wiki/Dodecagonal_number)代表十二边形(一个有 12 条边的多边形)。
一些十二边形数字是:
1，12，33，64，105，156，217，288，369，460，561，672，793，924……..
**例:**

```
Input : n = 4
Output : 64

Input : n = 9
Output : 369
```

**十二边形数第 n 项公式:**

```
n-th Dodecagonal number = 5n2 - 4n
```

下面是第 n 个十二边形数的实现:

## C++

```
// CPP Program to find the
// nth Dodecagonal number
#include <bits/stdc++.h>
using namespace std;

// function for Dodecagonal
// number
int Dodecagonal_number(int n)
{
    // formula for find Dodecagonal
    // nth term
    return 5 * n * n - 4 * n;
}

// Driver Code
int main()
{

    int n = 7;
    cout << Dodecagonal_number(n) << endl;

    n = 12;
    cout << Dodecagonal_number(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// nth Dodecagonal number
import java.util.*;

class GFG
{

    // function for
    // Dodecagonal number
    static int Dodecagonal_number(int n)
    {
        // formula for find
        // Dodecagonal nth term
        return 5 * n * n - 4 * n;
    }

    // Driver Code
    public static void main(String[] args)
    {

    int n = 7;
    System.out.println(Dodecagonal_number(n));

    n = 12;
    System.out.println(Dodecagonal_number(n));

    }
}

// This code is contributed by Anuj_67
```

## 蟒蛇 3

```
# Python program to find
# nth Dodecagonal number

# Function to calculate
# Dodecagonal number
def Dodecagonal_number(n):

    # Formula to calculate nth
    # Dodecagonal number

    return  5 * n * n - 4 * n

# Driver Code
n = 7
print(Dodecagonal_number(n))

n = 12
print(Dodecagonal_number(n))

# This code is contributed by aj_36.
```

## C#

```
// C# program to find the nth Dodecagonal
// number
using System;

class GFG {

    // function for Dodecagonal
    // number
    static int Dodecagonal_number(int n)
    {
        // formula for find Dodecagonal
        // nth term
        return 5 * n * n - 4 * n;
    }

    // Driver Code
    static void Main()
    {

        int n = 7;
        Console.WriteLine(Dodecagonal_number(n));

        n = 12;
        Console.WriteLine(Dodecagonal_number(n));

    }
}

// This code is contributed by Anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// nth Dodecagonal number

// function for Dodecagonal
// number
function Dodecagonal_number($n)
{

    // formula for find Dodecagonal
    // nth term
    return 5 * $n * $n - 4 * $n;
}

// Driver code
    $n = 7;
    echo Dodecagonal_number($n), "\n";

    $n = 12;
    echo Dodecagonal_number($n), "\n";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
// Javascript Program to find the
// nth Dodecagonal number

// function for Dodecagonal
// number
function Dodecagonal_number(n)
{

    // formula for find Dodecagonal
    // nth term
    return 5 * n * n - 4 * n;
}

// Driver Code

let n = 7;
document.write(Dodecagonal_number(n) + "<br>");

n = 12;
document.write(Dodecagonal_number(n) + "<br>");

// This code is contributed by subham348.
</script>
```

**Output :** 

```
217
672
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)

**参考文献:**T2https://en.wikipedia.org/wiki/Dodecagonal_number