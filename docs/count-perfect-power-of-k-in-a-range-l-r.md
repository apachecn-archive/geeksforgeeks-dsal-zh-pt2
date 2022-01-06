# 计算范围【L，R】

内 K 的完美幂

> 原文:[https://www . geesforgeks . org/count-perfect-a-range-l-r 中的 k 次方/](https://www.geeksforgeeks.org/count-perfect-power-of-k-in-a-range-l-r/)

给定三个整数 L、R 和 K，任务是找出 L 到 R 之间整数个数的计数，它们是 K 的完美幂，也就是以 <sup>K</sup> 形式的整数个数，其中 **a** 可以是任意数。

**示例:**

> **输入:** L = 3，R = 16，K = 3
> **输出:** 1
> **解释:**
> 3 到 16 之间只有一个整数在 a <sup>K</sup> 中是 8。
> 
> **输入:** L = 7，R = 18，K = 2
> **输出:** 2
> **说明:**
> 有两个这样的数字是以 <sup>K</sup> 的形式出现的，在 7 到 18 的范围内，也就是 9 和 16。

**方法:**思路是分别求 L 和 R 的 K <sup>次</sup>根，其中数字 N 的 [K <sup>次</sup>次](https://www.geeksforgeeks.org/n-th-root-number/)根是给出 N 的实数，当我们把它升到整数 N 次方时，那么在 L 和 R 范围内 K 次方的整数个数可以定义为–

```
Count = ( floor(Kthroot(R)) - ceil(Kthroot(L)) + 1 )
```

可以使用[牛顿公式](https://www.geeksforgeeks.org/program-for-newton-raphson-method/)计算 N 的第 K <sup>次</sup>次根，其中可以使用以下公式计算第 i <sup>次</sup>次迭代–

> x(I+1)=(1/k)*((k–1)* x(I)+n/x(I)^(n–1))

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// count of numbers those are
// powers of K in range L to R

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// Nth root of the number
double nthRoot(int A, int N)
{
    // initially guessing a random
    // number between 0 to 9
    double xPre = rand() % 10;

    // Smaller eps,
    // denotes more accuracy
    double eps = 1e-3;

    // Initializing difference between two
    // roots by INT_MAX
    double delX = INT_MAX;

    // xK denotes
    // current value of x
    double xK;

    // loop until we reach desired accuracy
    while (delX > eps) {
        // calculating current value
        // from previous value
        xK = ((N - 1.0) * xPre +
        (double)A / pow(xPre, N - 1))
                        / (double)N;
        delX = abs(xK - xPre);
        xPre = xK;
    }
    return xK;
}

// Function to count the perfect
// powers of K in range L to R
int countPowers(int a, int b, int k)
{
    return (floor(nthRoot(b, k)) -
           ceil(nthRoot(a, k)) + 1);
}

// Driver code
int main()
{
    int a = 7, b = 28, k = 2;
    cout << "Count of Powers is "
        << countPowers(a, b, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// count of numbers those are
// powers of K in range L to R
class GFG{

// Function to find the
// Nth root of the number
static double nthRoot(int A, int N)
{
    // initially guessing a random
    // number between 0 to 9
    double xPre = Math.random()*10 % 10;

    // Smaller eps,
    // denotes more accuracy
    double eps = 1e-3;

    // Initializing difference between two
    // roots by Integer.MAX_VALUE
    double delX = Integer.MAX_VALUE;

    // xK denotes
    // current value of x
    double xK = 0;

    // loop until we reach desired accuracy
    while (delX > eps)
    {
        // calculating current value
        // from previous value
        xK = ((N - 1.0) * xPre +
        (double)A / Math.pow(xPre, N - 1))
                        / (double)N;
        delX = Math.abs(xK - xPre);
        xPre = xK;
    }
    return xK;
}

// Function to count the perfect
// powers of K in range L to R
static int countPowers(int a, int b, int k)
{
    return (int) (Math.floor(nthRoot(b, k)) -
           Math.ceil(nthRoot(a, k)) + 1);
}

// Driver code
public static void main(String[] args)
{
    int a = 7, b = 28, k = 2;
    System.out.print("Count of Powers is "
        + countPowers(a, b, k));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation to find the
# count of numbers those are
# powers of K in range L to R
import sys
from math import pow,ceil,floor
import random

# Function to find the
# Nth root of the number
def nthRoot(A,N):

    # initially guessing a random
    # number between 0 to 9
    xPre = (random.randint(0, 9))%10

    # Smaller eps,
    # denotes more accuracy
    eps = 1e-3

    # Initializing difference between two
    # roots by INT_MAX
    delX = sys.maxsize

    # xK denotes
    # current value of x

    # loo3p until we reach desired accuracy
    while (delX > eps):

        # calculating current value
        # from previous value
        xK = ((N - 1.0) * xPre + A / pow(xPre, N - 1))/ N
        delX = abs(xK - xPre)
        xPre = xK
    return xK

# Function to count the perfect
# powers of K in range L to R
def countPowers(a, b, k):
    return (floor(nthRoot(b, k)) - ceil(nthRoot(a, k)) + 1)

# Driver code
if __name__ == '__main__':
    a = 7
    b = 28
    k = 2
    print("Count of Powers is",countPowers(a, b, k))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation to find the
// count of numbers those are
// powers of K in range L to R
using System;
using System.Collections.Generic;
public class GFG{

// Function to find the
// Nth root of the number
static double nthRoot(int A, int N)
{

    // initially guessing a random
    // number between 0 to 9
    Random r = new Random();
    double xPre = r.Next(0,9);

    // Smaller eps,
    // denotes more accuracy
    double eps = 1e-3;

    // Initializing difference between two
    // roots by int.MaxValue
    double delX = int.MaxValue;

    // xK denotes
    // current value of x
    double xK = 0;

    // loop until we reach desired accuracy
    while (delX > eps)
    {
        // calculating current value
        // from previous value
        xK = ((N - 1.0) * xPre +
        (double)A / Math.Pow(xPre, N - 1))
                        / (double)N;
        delX = Math.Abs(xK - xPre);
        xPre = xK;
    }
    return xK;
}

// Function to count the perfect
// powers of K in range L to R
static int countPowers(int a, int b, int k)
{
    return (int) (Math.Floor(nthRoot(b, k)) -
           Math.Ceiling(nthRoot(a, k)) + 1);
}

// Driver code
public static void Main(String[] args)
{
    int a = 7, b = 28, k = 2;
    Console.Write("Count of Powers is "
        + countPowers(a, b, k));
}
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// count of numbers those are
// powers of K in range L to R

// Function to find the
// Nth root of the number
function nthRoot(A, N)
{
    // initially guessing a random
    // number between 0 to 9
    var xPre = Math.random() % 10;

    // Smaller eps,
    // denotes more accuracy
    var eps = 0.001;

    // Initializing difference between two
    // roots by INT_MAX
    var delX = 1000000000;

    // xK denotes
    // current value of x
    var xK;

    // loop until we reach desired accuracy
    while (delX > eps) {
        // calculating current value
        // from previous value
        xK = ((N - 1.0) * xPre +
         A / Math.pow(xPre, N - 1))
                        / N;
        delX = Math.abs(xK - xPre);
        xPre = xK;
    }
    return xK;
}

// Function to count the perfect
// powers of K in range L to R
function countPowers(a, b, k)
{
    return (Math.floor(nthRoot(b, k)) -
           Math.ceil(nthRoot(a, k)) + 1);
}

// Driver code
var a = 7, b = 28, k = 2;
document.write("Count of Powers is "
     + countPowers(a, b, k));

</script>
```

**Output**

```
Count of Powers is 3
```

**性能分析:**

*   **时间复杂度:**和上面的方法一样，有两个函数调用来寻找花费 O(logN)时间的数字的 N <sup>次</sup>根，因此时间复杂度将是 **O(logN)** 。
*   **空间复杂度:**和上面的方法一样，没有使用额外的空间，因此空间复杂度为 **O(1)** 。