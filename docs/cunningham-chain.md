# 坎宁安链

> 原文:[https://www.geeksforgeeks.org/cunningham-chain/](https://www.geeksforgeeks.org/cunningham-chain/)

一个[坎宁安链](https://en.wikipedia.org/wiki/Cunningham_chain)是一个素数序列。它有两种类型:

*   **第一类坎宁安链:**它是长度为 n 的素数序列，描述如下:

> 设 p1，p2，p3，…，p <sub>n</sub> 是长度 n 比
> p<sub>2</sub>= 2 * p<sub>1</sub>+1
> p<sub>3</sub>= 4 * p<sub>1</sub>+3
> p<sub>4</sub>= 8 * p<sub>1</sub>+7
> 。。。
> 。。。
> **p<sub>n</sub>= 2<sup>n-1</sup>* P1+(2<sup>n-1</sup>–1)**

*   这里 p1，p2，p3，…，pn 都是质数。如果 p 的任何值变成非质数，那么链在它之前的数处结束。
    对于 p0 = 2，顺序将是 2 5 11 23 47
    下面是上面的实现:

## C++

```
// C++ program for cunningham chain
// Function to print the series
// of first kind
#include <bits/stdc++.h>

using namespace std;

// Function to print
// Cunningham chain of the first kind
void print(int p0)
{
    int p1, i = 0, x, flag, k;

    // Iterate till all elements
    // are printed
    while (1) {
        flag = 1;
        x = (int)(pow(2, i));
        p1 = x * p0 + (x - 1);

        // check prime or not
        for (k = 2; k < p1; k++) {
            if (p1 % k == 0) {
                flag = 0;
                break;
            }
        }
        if (flag == 0)
            break;
        printf("%d ", p1);
        i++;
    }
}

// Driver Code
int main()
{
    int p0 = 2;
    print(p0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print the
// series of first kind
class GFG
{

// Function to print
// Cunningham chain
// of the first kind
static void print(int p0)
{
    int p1, i = 0, x, flag, k;

    // Iterate till all
    // elements are printed
    while (true)
    {
        flag = 1;
        x = (int)(Math.pow(2, i));
        p1 = x * p0 + (x - 1);

        // check prime or not
        for (k = 2; k < p1; k++)
        {
            if (p1 % k == 0)
            {
                flag = 0;
                break;
            }
        }
        if (flag == 0)
            break;
        System.out.print(" " + p1);
        i++;
    }
}

// Driver Code
public static void main(String args[])
{
    int p0 = 2;
    print(p0);
}
}

// This code is contributed
// by Kirti_Mangal
```

## 蟒蛇 3

```
# Python3 program for cunningham chain

# Function to print Cunningham chain
# of the first kind
def print_C(p0):

    i = 0;

    # Iterate till all elements
    # are printed
    while(True):
        flag = 1;
        x = pow(2, i);
        p1 = x * p0 + (x - 1);

        # check prime or not
        for k in range(2, p1):
            if (p1 % k == 0):
                flag = 0;
                break;

        if (flag == 0):
            break;

        print(p1, end = " ");
        i += 1;

# Driver Code
p0 = 2;
print_C(p0);

# This code is contributed by mits
```

## C#

```
// C# Program to print the
// series of first kind
using System;
class GFG
{

// Function to print
// Cunningham chain
// of the first kind
static void print(int p0)
{
    int p1, i = 0, x, flag, k;

    // Iterate till all
    // elements are printed
    while (true)
    {
        flag = 1;
        x = (int)(Math.Pow(2, i));
        p1 = x * p0 + (x - 1);

        // check prime or not
        for (k = 2; k < p1; k++)
        {
            if (p1 % k == 0)
            {
                flag = 0;
                break;
            }
        }
        if (flag == 0)
            break;
        Console.Write(" " + p1);
        i++;
    }
}

// Driver Code
public static void Main()
{
    int p0 = 2;
    print(p0);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for cunningham chain
// Function to print
// Cunningham chain of the first kind
function print_C($p0)
{
    $p1 = 0; $i = 0; $x; $flag; $k;

    // Iterate till all elements
    // are printed
    while (1)
    {
        $flag = 1;
        $x = pow(2, $i);
        $p1 = $x * $p0 + ($x - 1);

        // check prime or not
        for ($k = 2; $k < $p1; $k++)
        {
            if ($p1 % $k == 0) {
                $flag = 0;
                break;
            }
        }
        if ($flag == 0)
            break;
        echo $p1 . " ";
        $i++;
    }
}

// Driver Code
$p0 = 2;
print_C($p0);

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>
// Javascript program for cunningham chain
// Function to print
// Cunningham chain of the first kind
function print_C(p0)
{
    let p1 = 0;
    let i = 0;
    let x;
    let flag;
    let k;

    // Iterate till all elements
    // are printed
    while (1)
    {
        flag = 1;
        x = Math.pow(2, i);
        p1 = x * p0 + (x - 1);

        // check prime or not
        for (let k = 2; k < p1; k++)
        {
            if (p1 % k == 0) {
                flag = 0;
                break;
            }
        }
        if (flag == 0)
            break;
        document.write(p1 + " ");
        i++;
    }
}

// Driver Code
let p0 = 2;
print_C(p0);

// This code is contributed
// by gfgking

</script>
```

**Output:** 

```
2 5 11 23 47
```

*   **第二类坎宁安链:**它是长度为 n 的素数序列，描述如下:

> 设 p1，p2，p3，…，p <sub>n</sub> 为长度 n 比
> p<sub>2</sub>= 2 * p<sub>1</sub>–1
> p<sub>3</sub>= 4 * p<sub>1</sub>–3
> p<sub>4</sub>= 8 * p<sub>1</sub>–7
> 。。。
> 。。。
> **p<sub>n</sub>= 2<sup>n-1</sup>* P1 –( 2<sup>n-1</sup>–1)**

*   对于 p0 = 19，序列将是 19，37，73。
    下面是上面的实现:

## C++

```
// C++ program for cunningham chain
// Function to print the series
// of second kind
#include <bits/stdc++.h>

using namespace std;

// Function to print
// Cunningham chain of the second kind
void print(int p0)
{
    int p1, i = 0, x, flag, k;

    // Iterate till all elements
    // are printed
    while (1) {
        flag = 1;
        x = (int)(pow(2, i));
        p1 = x * p0 - (x - 1);

        // check prime or not
        for (k = 2; k < p1; k++) {
            if (p1 % k == 0) {
                flag = 0;
                break;
            }
        }
        if (flag == 0)
            break;
        printf("%d ", p1);
        i++;
    }
}

// Driver Code
int main()
{
    int p0 = 19;
    print(p0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for cunningham chain
// Function to print the series
// of second kind

class GFG{

// Function to print Cunningham chain
//  of the second kind
static void print(int p0)
{
    int p1, i = 0, x, flag, k;

    // Iterate till all elements
    // are printed
    while (true)
    {
        flag = 1;
        x = (int)(Math.pow(2, i));
        p1 = x * p0 - (x - 1);

        // check prime or not
        for (k = 2; k < p1; k++)
        {
            if (p1 % k == 0)
            {
                flag = 0;
                break;
            }
        }
        if (flag == 0)
            break;
        System.out.print(p1+" ");
        i++;
    }
}

// Driver Code
public static void main(String[] args)
{
    int p0 = 19;
    print(p0);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program for cunningham chain

# Function to print Cunningham chain
# of the second kind
def print_t(p0):

    i = 0;

    # Iterate till all elements
    # are printed
    while (True):
        flag = 1;
        x = pow(2, i);
        p1 = x * p0 - (x - 1);

        # check prime or not
        for k in range(2, p1):
            if (p1 % k == 0):
                flag = 0;
                break;

        if (flag == 0):
            break;
        print(p1,end=" ");
        i+=1;

# Driver Code
p0 = 19;
print_t(p0);

# This code is contributed by mits
```

## C#

```
// C# program for cunningham chain
// Function to print the series
// of second kind
using System;
class GFG
{

// Function to print
// Cunningham chain of the second kind
static void print(int p0)
{
    int p1, i = 0, x, flag, k;

    // Iterate till all elements
    // are printed
    while (true)
    {
        flag = 1;
        x = (int)(Math.Pow(2, i));
        p1 = x * p0 - (x - 1);

        // check prime or not
        for (k = 2; k < p1; k++)
        {
            if (p1 % k == 0)
            {
                flag = 0;
                break;
            }
        }
        if (flag == 0)
            break;
        Console.Write(p1 + " ");
        i++;
    }
}

// Driver Code
static void Main()
{
    int p0 = 19;
    print(p0);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for cunningham chain

// Function to print
// Cunningham chain of the second kind
function print_t($p0)
{
    $p1; $i = 0; $x; $flag; $k;

    // Iterate till all elements
    // are printed
    while (1)
    {
        $flag = 1;
        $x = pow(2, $i);
        $p1 = $x * $p0 - ($x - 1);

        // check prime or not
        for ($k = 2; $k < $p1; $k++) {
            if ($p1 % $k == 0) {
                $flag = 0;
                break;
            }
        }
        if ($flag == 0)
            break;
        echo $p1 . " ";
        $i++;
    }
}

// Driver Code
$p0 = 19;
print_t($p0);

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>

// JavaScript program for cunningham chain

// Function to print
// Cunningham chain of the second kind
function print(p0)
{
    var p1, i = 0, x, flag = 1, k, m = 4;

    // Iterate till all elements
    // are printed
    while (flag) {
        flag = 1;
        x = Math.pow(2, i);
        p1 = x * p0 - (x - 1);

        // check prime or not
        for (k = 2; k < p1; k++) {
            if (p1 % k == 0) {
                flag = 0;
                break;
            }
        }
        if (flag == 0)
            break;
        document.write(p1 + " ");
        i++;
    }
}

// Driver Code
var p0 = 19;
print(p0);

//This code is contributed by Shivani

</script>
```

**Output:** 

```
19 37 73
```