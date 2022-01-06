# 不使用乘法的数的阶乘

> 原文:[https://www . geeksforgeeks . org/不使用乘法的数的阶乘/](https://www.geeksforgeeks.org/factorial-of-a-number-without-using-multiplication/)

给定一个正数 **N** ，任务是在不使用乘法运算符的情况下计算 **N** 的[阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)。

**示例:**

> **输入** : N = 5
> **输出:**
> 120
> **说明:**
> 5*4*3*2*1=120
> 
> **输入:** N = 7
> **输出:**
> 5040

**观察:**

```
A*B=A+A+A+A...B times.

This observation can be used as follows:
5!=5*4*3*2*1
=(5+5+5+5)*3*2*1
=(20+20+20)*2*1
=60+60
=120
```

**方法:**这个问题可以使用[嵌套循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples-2/)的概念来解决。可以通过使用另一个循环来手动计算答案，而不是使用乘法运算符。按照以下步骤解决问题:

1.  将变量**和**初始化为 **N** 。
2.  使用变量 **i、**从 **N-1** 迭代到 **1** ，并执行以下操作:
    *   初始化一个变量**将**加到 **0** 。
    *   使用变量 **j** 从 **0** 迭代到 **i-1、**，并将 **ans** 添加到 **sum**
    *   将**和**加到**和**上。
3.  打印〔t0〕年〔t1〕年。

下面是上述方法的实现

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate factorial of the number
// without using multiplication operator
int factorialWithoutMul(int N)
{
    // variable to store the final factorial
    int ans = N;

    // Outer loop
    for (int i = N - 1; i > 0; i--) {
        int sum = 0;

        // Inner loop
        for (int j = 0; j < i; j++)
            sum += ans;
        ans = sum;
    }
    return ans;
}

// Driver code
int main()
{
    // Input
    int N = 5;

    // Function calling
    cout << factorialWithoutMul(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {
    // Function to calculate factorial of the number
    // without using multiplication operator
    public static int factorialWithoutMul(int N)
    {
        // variable to store the final factorial
        int ans = N;

        // Outer loop
        for (int i = N - 1; i > 0; i--) {
            int sum = 0;

            // Inner loop
            for (int j = 0; j < i; j++)
                sum += ans;
            ans = sum;
        }
        return ans;
    }
    // Driver code
    public static void main(String[] args)
    {
        int N = 5;

        // Function calling
        System.out.println(factorialWithoutMul(N));
        // This code is contributed by Potta Lokesh
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate factorial of the number
# without using multiplication operator
def factorialWithoutMul(N):

    # Variable to store the final factorial
    ans = N

    # Outer loop
    i = N - 1

    while (i > 0):
        sum = 0

        # Inner loop
        for j in range(i):
            sum += ans

        ans = sum
        i -= 1

    return ans

# Driver code
if __name__ == '__main__':

    # Input
    N = 5

    # Function calling
    print(factorialWithoutMul(N))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate factorial of the number
// without using multiplication operator
static int factorialWithoutMul(int N)
{

    // Variable to store the final factorial
    int ans = N;

    // Outer loop
    for(int i = N - 1; i > 0; i--)
    {
        int sum = 0;

        // Inner loop
        for(int j = 0; j < i; j++)
            sum += ans;

        ans = sum;
    }
    return ans;
}

// Driver code
public static void Main()
{

    // Input
    int N = 5;

    // Function calling
    Console.Write(factorialWithoutMul(N));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
   <script>
// JavaScript program for the above approach

// Function to calculate factorial of the number
// without using multiplication operator
function factorialWithoutMul(N)
{
    // variable to store the final factorial
    let ans = N;

    // Outer loop
    for (let i = N - 1; i > 0; i--) {
        let sum = 0;

        // Inner loop
        for (let j = 0; j < i; j++)
            sum += ans;
        ans = sum;
    }
    return ans;
}

// Driver code

    // Input
    let N = 5;

    // Function calling
    document.write(factorialWithoutMul(N));

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
120
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*