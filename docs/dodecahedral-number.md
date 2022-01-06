# 十二面体数

> 原文:[https://www.geeksforgeeks.org/dodecahedral-number/](https://www.geeksforgeeks.org/dodecahedral-number/)

给定一个数 n，任务是求**第 n 个**十二面体数。
一个[十二面体数](https://en.wikipedia.org/wiki/Dodecahedral_number)属于一个数字，代表它是十二面体。
前几个十二面体数(其中 n = 0，1，2，3……)。)分别是:0、1、20、84 等等。

**示例:**

```
Input : 2
Output : 20

Input :8
Output :2024
```

**第 n 个**十二面体数的数学公式:

## C++

```
// C++ program to find nth
// dodecahedral number
#include <bits/stdc++.h>
using namespace std;

// Function to find
// dodecahedral number
int dodecahedral_num(int n)
{
    // Formula to calculate nth
    // dodecahedral number
    // and return it into main function.
    return n * (3 * n - 1) * (3 * n - 2) / 2;
}

// Driver Code
int main()
{
    int n = 5;
    // print result
    cout << n << "th Dodecahedral number: ";
    cout << dodecahedral_num(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find nth dodecahedral
// number
import java.io.*;

class GFG {

    // Function to find dodecahedral number
    static int dodecahedral_num(int n)
    {

        // Formula to calculate nth
        // dodecahedral number
        // and return it into main function.
        return n * (3 * n - 1) *
                           (3 * n - 2) / 2;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 5;
        // print result
        System.out.print( n + "the Dodecahedral"
                                  + " number:");
        System.out.println( dodecahedral_num(n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to find
# nth dodecahedral number

# Function to calculate
# dodecahedral number

def dodecahedral_num(n):

    # Formula to calculate nth
    # dodecahedral number

    return n * (3 * n - 1) * (3 * n - 2) // 2

# Driver Code
n = 5
print("%sth Dodecahedral number :" %n,
                    dodecahedral_num(n))

# This code is contributed by ajit.                
```

## C#

```
// C# program to find nth dodecahedral
// number
using System;

class GFG {

    // Function to find dodecahedral number
    static int dodecahedral_num(int n)
    {

        // Formula to calculate nth
        // dodecahedral number
        // and return it into main function.
        return n * (3 * n - 1) *
                        (3 * n - 2) / 2;
    }

    // Driver Code
    public static void Main ()
    {
        int n = 5;

        // print result
        Console.Write( n + "the Dodecahedral"
                                + " number:");
        Console.WriteLine( dodecahedral_num(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find nth
// dodecahedral number

// Function to find
// dodecahedral number
function dodecahedral_num( $n)
{
    // Formula to calculate nth
    // dodecahedral number
    // and return it into main function.
    return $n * (3 * $n - 1) *
                (3 * $n - 2) / 2;
}

// Drivers Code
$n = 5;

// print result
echo $n, "th Dodecahedral number: ";
echo dodecahedral_num($n);

// This code is contributed by vt_m
?>
```

## java 描述语言

```
<script>

// Javascript program to find nth dodecahedral
// number

// Function to find dodecahedral number
function dodecahedral_num(n)
{

    // Formula to calculate nth
    // dodecahedral number and
    // return it into main function.
    return n * (3 * n - 1) *
               (3 * n - 2) / 2;
}

// Driver code
var n = 5;

// print result
document.write(n + "th Dodecahedral" +
               " number:");
document.write(dodecahedral_num(n));

// This code is contributed by Khushboogoyal499

</script>
```

**Output :** 

```
5th Dodecahedral number: 455
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)

参考:[https://en.wikipedia.org/wiki/Dodecahedral_number](https://en.wikipedia.org/wiki/Dodecahedral_number)T2】