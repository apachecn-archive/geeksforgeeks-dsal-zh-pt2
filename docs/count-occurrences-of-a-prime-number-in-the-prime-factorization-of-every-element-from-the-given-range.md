# 计算给定范围内每个元素的素数因式分解中出现的素数

> 原文:[https://www . geesforgeks . org/count-给定范围内每个元素的素数因子分解出现次数/](https://www.geeksforgeeks.org/count-occurrences-of-a-prime-number-in-the-prime-factorization-of-every-element-from-the-given-range/)

给定三个整数 **L** 、 **R** 和 **P** ，其中 **P** 为素数，任务是统计 **P** 在**【L，R】**范围内所有数的素数因式分解中出现的次数。
**示例:**

> **输入:** L = 2，R = 8，P = 2
> **输出:** 7
> 
> <figure class="table">
> 
> | 元素 | 主要因素 | 时间 2 出现 |
> | --- | --- | --- |
> | Two | Two | one |
> | three | three | Zero |
> | four | 2 * 2 | Two |
> | five | five | Zero |
> | six | 2 * 3 | one |
> | seven | seven | Zero |
> | eight | 2 * 2 * 2 | three |
> 
> 1 + 0 + 2 + 0 + 1 + 0 + 3 = 7
> **输入:** L = 5，R = 25，P = 7
> **输出:** 3
> 
> </figure>

**天真的方法:**简单地迭代该范围，并为每个值计算 **P** 将该值除以多少次，并将它们相加得到结果。时间复杂度**O(R–L)**。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the highest
// power of p that divides n
int countFactors(int n, int p)
{
    int pwr = 0;
    while (n > 0 && n % p == 0) {
        n /= p;
        pwr++;
    }
    return pwr;
}

// Function to return the count of times p
// appears in the prime factors of the
// elements from the range [l, r]
int getCount(int l, int r, int p)
{

    // To store the required count
    int cnt = 0;

    // For every element of the range
    for (int i = l; i <= r; i++) {

        // Add the highest power of
        // p that divides i
        cnt += countFactors(i, p);
    }

    return cnt;
}

// Driver code
int main()
{
    int l = 2, r = 8, p = 2;

    cout << getCount(l, r, p);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the highest
// power of p that divides n
static int countFactors(int n, int p)
{
    int pwr = 0;
    while (n > 0 && n % p == 0)
    {
        n /= p;
        pwr++;
    }
    return pwr;
}

// Function to return the count of times p
// appears in the prime factors of the
// elements from the range [l, r]
static int getCount(int l, int r, int p)
{

    // To store the required count
    int cnt = 0;

    // For every element of the range
    for (int i = l; i <= r; i++)
    {

        // Add the highest power of
        // p that divides i
        cnt += countFactors(i, p);
    }
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int l = 2, r = 8, p = 2;

    System.out.println(getCount(l, r, p));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the highest
# power of p that divides n
def countFactors(n, p) :

    pwr = 0;

    while (n > 0 and n % p == 0) :
        n //= p;
        pwr += 1;

    return pwr;

# Function to return the count of times p
# appears in the prime factors of the
# elements from the range [l, r]
def getCount(l, r, p) :

    # To store the required count
    cnt = 0;

    # For every element of the range
    for i in range(l, r + 1) :

        # Add the highest power of
        # p that divides i
        cnt += countFactors(i, p);

    return cnt;

# Driver code
if __name__ == "__main__" :

    l = 2; r = 8; p = 2;

    print(getCount(l, r, p));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the highest
// power of p that divides n
static int countFactors(int n, int p)
{
    int pwr = 0;
    while (n > 0 && n % p == 0)
    {
        n /= p;
        pwr++;
    }
    return pwr;
}

// Function to return the count of times p
// appears in the prime factors of the
// elements from the range [l, r]
static int getCount(int l, int r, int p)
{

    // To store the required count
    int cnt = 0;

    // For every element of the range
    for (int i = l; i <= r; i++)
    {

        // Add the highest power of
        // p that divides i
        cnt += countFactors(i, p);
    }
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    int l = 2, r = 8, p = 2;

    Console.WriteLine(getCount(l, r, p));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the highest
// power of p that divides n
function countFactors(n, p)
{
    let pwr = 0;
    while (n > 0 && n % p == 0) {
        n /= p;
        pwr++;
    }
    return pwr;
}

// Function to return the count of times p
// appears in the prime factors of the
// elements from the range [l, r]
function getCount(l, r, p)
{

    // To store the required count
    let cnt = 0;

    // For every element of the range
    for (let i = l; i <= r; i++) {

        // Add the highest power of
        // p that divides i
        cnt += countFactors(i, p);
    }

    return cnt;
}

// Driver code
    let l = 2, r = 8, p = 2;

    document.write(getCount(l, r, p));

</script>
```

**Output:** 

```
7
```

**有效方法:**计算在**【L，R】**范围内可被 **P、P <sup>2</sup> 、P <sup>3</sup> 、…、P<sup>x</sup>T9】整除的值，其中 **x** 是 **P** 的最大幂，使得**P<sup>x</sup>T19】位于上限( **P <sup>每次迭代耗费 **O(1)** 时间因此时间复杂度变成 **O(x)** 其中 **x = (log(R) / log(P))** 。
以下是上述方法的实施:</sup>******

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the count of times p
// appears in the prime factors of the
// elements from the range [l, r]
int getCount(int l, int r, int p)
{

    // To store the required count
    int cnt = 0;
    int val = p;
    while (1) {

        // Number of values in the range [0, r]
        // that are divisible by val
        int a = r / val;

        // Number of values in the range [0, l - 1]
        // that are divisible by val
        int b = (l - 1) / val;

        // Increment the power of the val
        val *= p;

        // (a - b) is the count of numbers in the
        // range [l, r] that are divisible by val
        if (a - b) {
            cnt += (a - b);
        }

        // No values that are divisible by val
        // thus exiting from the loop
        else
            break;
    }

    return cnt;
}

// Driver code
int main()
{
    int l = 2, r = 8, p = 2;

    cout << getCount(l, r, p);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count of times p
// appears in the prime factors of the
// elements from the range [l, r]
static int getCount(int l, int r, int p)
{

    // To store the required count
    int cnt = 0;
    int val = p;
    while (true)
    {

        // Number of values in the range [0, r]
        // that are divisible by val
        int a = r / val;

        // Number of values in the range [0, l - 1]
        // that are divisible by val
        int b = (l - 1) / val;

        // Increment the power of the val
        val *= p;

        // (a - b) is the count of numbers in the
        // range [l, r] that are divisible by val
        if ((a - b) > 0)
        {
            cnt += (a - b);
        }

        // No values that are divisible by val
        // thus exiting from the loop
        else
            break;
    }
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int l = 2, r = 8, p = 2;

    System.out.println(getCount(l, r, p));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of times p
# appears in the prime factors of the
# elements from the range [l, r]
def getCount(l, r, p):

    # To store the required count
    cnt = 0;
    val = p;
    while (True):

        # Number of values in the range [0, r]
        # that are divisible by val
        a = r // val;

        # Number of values in the range [0, l - 1]
        # that are divisible by val
        b = (l - 1) // val;

        # Increment the power of the val
        val *= p;

        # (a - b) is the count of numbers in the
        # range [l, r] that are divisible by val
        if (a - b):
            cnt += (a - b);

        # No values that are divisible by val
        # thus exiting from the loop
        else:
            break;

    return int(cnt);

# Driver Code
l = 2;
r = 8;
p = 2;

print(getCount(l, r, p));

# This code is contributed by princiraj
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of times p
// appears in the prime factors of the
// elements from the range [l, r]
static int getCount(int l, int r, int p)
{

    // To store the required count
    int cnt = 0;
    int val = p;
    while (true)
    {

        // Number of values in the range [0, r]
        // that are divisible by val
        int a = r / val;

        // Number of values in the range [0, l - 1]
        // that are divisible by val
        int b = (l - 1) / val;

        // Increment the power of the val
        val *= p;

        // (a - b) is the count of numbers in the
        // range [l, r] that are divisible by val
        if ((a - b) > 0)
        {
            cnt += (a - b);
        }

        // No values that are divisible by val
        // thus exiting from the loop
        else
            break;
    }
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    int l = 2, r = 8, p = 2;

    Console.WriteLine(getCount(l, r, p));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the count of times p
// appears in the prime factors of the
// elements from the range [l, r]
function getCount(l, r, p)
{

    // To store the required count
    let cnt = 0;
    let val = p;
    while (1) {

        // Number of values in the range [0, r]
        // that are divisible by val
        let a = parseInt(r / val);

        // Number of values in the range [0, l - 1]
        // that are divisible by val
        let b = parseInt((l - 1) / val);

        // Increment the power of the val
        val *= p;

        // (a - b) is the count of numbers in the
        // range [l, r] that are divisible by val
        if (a - b) {
            cnt += (a - b);
        }

        // No values that are divisible by val
        // thus exiting from the loop
        else
            break;
    }

    return cnt;
}

// Driver code
    let l = 2, r = 8, p = 2;

    document.write(getCount(l, r, p));

</script>
```

**Output:** 

```
7
```