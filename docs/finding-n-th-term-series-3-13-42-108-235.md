# 求数列 3、13、42、108、235 的第 n 项……

> 原文:[https://www . geesforgeks . org/find-n-th-term-series-3-13-42-108-235/](https://www.geeksforgeeks.org/finding-n-th-term-series-3-13-42-108-235/)

给定一个数字 n，求数列 3、13、42、108、235 中的第 n 项……
**例:**

```
Input : 3
Output : 42

Input : 4
Output : 108
```

约束:
1<= T<= 100
1<= N<= 100
**天真法:**
级数基本上表示自然数立方和项数之和乘以 2。第一项是单个数的和。第二项是两个数的和，以此类推。
**举例:**

```
n = 2
2nd term equals to sum of 1st term and 8 i.e
A2 = A1 + 23 + n*2
   = 1 + 8 + 4
   = 13

Similarly,
A3 = A2 + 33 + n*2
   = 9 + 27 + 6
   = 42 and so on..
```

一个简单的解决方案是将前 n 个自然数的立方和项数乘以 2。

## C++

```
// C++ program to find n-th term of
// series 3, 13, 42, 108, 235…
#include <bits/stdc++.h>
using namespace std;

// Function to generate a fixed number
int magicOfSequence(int N)
{
    int sum = 0;
    for (int i = 1; i <= N; i++)
        sum += (i*i*i + i*2);
    return sum;   
}

// Driver Method
int main()
{
    int N = 4;
    cout << magicOfSequence(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Finding n-th term
// of series 3, 13, 42, 108, 235 ...

class GFG {

// Function to generate
// a fixed number
public static int magicOfSequence(int N)
{
    int sum = 0;
    for (int i = 1; i <= N; i++)
        sum += (i * i * i + i * 2);
    return sum;
}

// Driver Method
public static void main(String args[])
{
    int N = 4;
    System.out.println(magicOfSequence(N));
}
}

// This code is contributed by Jaideep Pyne
```

## 蟒蛇 3

```
# Python3 program to
# find n-th term of
# series 3, 13, 42, 108, 235…

# Function to generate
# a fixed number
def magicOfSequence(N) :

    sum = 0
    for i in range(1, N + 1) :
        sum += (i * i * i + i * 2)
    return sum;

# Driver Code
N = 4
print(magicOfSequence(N))

# This code is contributed by vij.
```

## C#

```
// C# Program to Finding
// n-th term of series
// 3, 13, 42, 108, 235 ...
using System;

class GFG
{

// Function to generate
// a fixed number
public static int magicOfSequence(int N)
{
    int sum = 0;
    for (int i = 1; i <= N; i++)
        sum += (i * i * i + i * 2);
    return sum;
}

// Driver Code
static public void Main ()
{
    int N = 4;
    Console.WriteLine(magicOfSequence(N));
}
}

// This code is contributed
// by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP  program to find n-th term of
// series 3, 13, 42, 108, 235…

// Function to generate a fixed number

function magicOfSequence($N)
{
    $sum = 0;
    for ($i = 1; $i <= $N; $i++)
        $sum += ($i*$i*$i + $i*2);
    return $sum;
}

// Driver Method

    $N = 4;
    echo  magicOfSequence($N);

// This code is contributed by m_kit   
?>
```

## java 描述语言

```
<script>
// JavaScript program to find n-th term of
// series 3, 13, 42, 108, 235…

// Function to generate a fixed number
function magicOfSequence( N)
{
    let sum = 0;
    for (let i = 1; i <= N; i++)
        sum += (i*i*i + i*2);
    return sum;   
}

// Driver Function

    let N = 4;
    document.write(magicOfSequence(N));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
120
```