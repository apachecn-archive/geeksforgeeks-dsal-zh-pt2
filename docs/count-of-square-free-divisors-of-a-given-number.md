# 给定数目的平方自由约数的计数

> 原文:[https://www . geesforgeks . org/给定数字的平方自由约数/](https://www.geeksforgeeks.org/count-of-square-free-divisors-of-a-given-number/)

给定一个整数 **N** ，任务是统计给定数的[无平方因子](https://www.geeksforgeeks.org/square-free-number/)的个数。

> 一个数被称为**无平方**，如果没有质因数对其进行多次除，即一个质因数除 **N** 的最大幂是 1。

**示例:**

> **输入:** N = 72
> **输出:** 3
> **说明:** 2、3、6 是除 72 的三个可能的平方自由数。
> 
> **输入:**N = 62290800
> T3】输出: 31

**天真方法:**
对于每一个整数 **N** ，找到它的因子，检查它是否是一个无平方数。如果是无平方数，则增加计数，否则继续下一个数。最后，打印给我们所需的 **N** 的无平方因子数的计数。
***时间复杂度:** O(N <sup>3/2</sup> )*

**高效方法:**
按照以下步骤解决问题:

*   从无平方数的定义可以理解为，找出给定数 **N** 的所有素因子，就可以找出所有可能的可以除 **N** 的无平方数。
*   让 **N** 的质因数个数为 **X** 。因此，**2<sup>X</sup>–1**无平方数可以用这些 **X** 质因数形成。
*   由于这些 **X** 素因子中的每一个都是 N 的因子，因此这些 **X** 素因子的任何乘积组合也是 N 的因子，因此将有**2<sup>X</sup>–1**N 的平方自由因子

> 插图:
> 
> *   N = 72
> *   N 的素因子是 2，3。
> *   因此，从这两个素数生成的三个可能的平方自由数是 2，3 和 6。
> *   因此，72 的总无平方因子是 3(= 2<sup>2</sup>–1)。

下面是上述方法的实现:

## C++

```
// C++ Program to find the square
// free divisors of a given number
#include <bits/stdc++.h>
using namespace std;

// The function to check
// if a number is prime or not
bool IsPrime(int i)
{
    // If the number is even
    // then its not prime
    if (i % 2 == 0 && i != 2)
        return false;

    else {
        for (int j = 3;
             j <= sqrt(i); j += 2) {
            if (i % j == 0)
                return false;
        }
        return true;
    }
}

// Driver Code
int main()
{
    // Stores the count of
    // distinct prime factors
    int c = 0;
    int N = 72;

    for (int i = 2;
         i <= sqrt(N); i++) {

        if (IsPrime(i)) {
            if (N % i == 0) {
                c++;
                if (IsPrime(N / i)
                    && i != (N / i)) {
                    c++;
                }
            }
        }
    }

    // Print the number of
    // square-free divisors
    cout << pow(2, c) - 1
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the square
// free divisors of a given number
import java.util.*;

class GFG{

// The function to check
// if a number is prime or not
static boolean IsPrime(int i)
{

    // If the number is even
    // then its not prime
    if (i % 2 == 0 && i != 2)
        return false;
    else
    {
        for(int j = 3;
                j <= Math.sqrt(i);
                j += 2)
        {
           if (i % j == 0)
               return false;
        }
        return true;
    }
}

// Driver code
public static void main(String[] args)
{

    // Stores the count of
    // distinct prime factors
    int c = 0;
    int N = 72;

    for(int i = 2;
            i <= Math.sqrt(N); i++)
    {
       if (IsPrime(i))
       {
           if (N % i == 0)
           {
               c++;
               if (IsPrime(N / i) &&
                     i != (N / i))
                   c++;
           }
       }
    }

    // Print the number of
    // square-free divisors
    System.out.print(Math.pow(2, c) - 1);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to find the square
# free divisors of a given number
import math

# The function to check
# if a number is prime or not
def IsPrime(i):

    # If the number is even
    # then its not prime
    if (i % 2 == 0 and i != 2):
        return 0;

    else:
        for j in range(3, int(math.sqrt(i) + 1), 2):
            if (i % j == 0):
                return 0;

        return 1;

# Driver code

# Stores the count of
# distinct prime factors
c = 0;
N = 72;

for i in range(2, int(math.sqrt(N)) + 1):
    if (IsPrime(i)):
        if (N % i == 0):
            c = c + 1

            if (IsPrime(N / i) and
                 i != (N / i)):
                c = c + 1

# Print the number of
# square-free divisors    
print (pow(2, c) - 1)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to find the square
// free divisors of a given number
using System;
class GFG{

// The function to check
// if a number is prime or not
static Boolean IsPrime(int i)
{

    // If the number is even
    // then its not prime
    if (i % 2 == 0 && i != 2)
        return false;
    else
    {
        for(int j = 3;
                j <= Math.Sqrt(i);
                j += 2)
        {
        if (i % j == 0)
            return false;
        }
        return true;
    }
}

// Driver code
public static void Main(String[] args)
{

    // Stores the count of
    // distinct prime factors
    int c = 0;
    int N = 72;

    for(int i = 2;
            i <= Math.Sqrt(N); i++)
    {
        if (IsPrime(i))
        {
            if (N % i == 0)
            {
                c++;
                if (IsPrime(N / i) &&
                        i != (N / i))
                    c++;
            }
        }
    }

    // Print the number of
    // square-free divisors
    Console.Write(Math.Pow(2, c) - 1);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program to find the square
// free divisors of a given number

// The function to check
// if a number is prime or not
function IsPrime(i)
{

    // If the number is even
    // then its not prime
    if (i % 2 == 0 && i != 2)
        return false;
    else
    {
        for(j = 3; j <= Math.sqrt(i); j += 2)
        {
            if (i % j == 0)
                return false;
        }
        return true;
    }
}

// Driver code

// Stores the count of
// distinct prime factors
var c = 0;
var N = 72;

for(i = 2; i <= Math.sqrt(N); i++)
{
    if (IsPrime(i))
    {
        if (N % i == 0)
        {
            c++;

            if (IsPrime(N / i) &&
                  i != (N / i))
                c++;
        }
    }
}

// Print the number of
// square-free divisors
document.write(Math.pow(2, c) - 1);

// This code is contributed by aashish1995

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*