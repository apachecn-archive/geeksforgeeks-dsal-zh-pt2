# 给定范围内所有数字位数的累计乘积

> 原文:[https://www . geesforgeks . org/给定范围内所有数字的累计乘积/](https://www.geeksforgeeks.org/cumulative-product-of-digits-of-all-numbers-in-the-given-range/)

给定**两个整数 L 和 R** ，任务是求 L 到 R
**范围内所有自然数的位数累计乘积(即位数乘积的乘积)示例** :

> **输入:** L = 2，R = 5
> **输出:** 14
> **解释:**
> 2 * 3 * 4 * 5 = 120
> **输入:** L = 11，R = 15
> **输出:** 120
> **解释:**
> (1 * 1)*(1 * 2)*(1 * 3)*(1 * 4)*(1)

**方法:**
要解决上面提到的问题，我们必须观察如果:

*   如果 **L 和 R 之间的差值大于 9** ，则乘积为 0，因为在 9 的间隔后，每个数字都出现一个数字 0。
*   否则，我们可以在一个从 L 到 R 的循环中找到该产品，该循环最多将运行 9 次。

以下是上述方法的实现:

## C++

```
// C++ program to print the product
// of all numbers in range L and R

#include <bits/stdc++.h>
using namespace std;

// Function to get product of digits
int getProduct(int n)
{
    int product = 1;

    while (n != 0) {
        product = product * (n % 10);
        n = n / 10;
    }

    return product;
}

// Function to find the product of digits
// of all natural numbers in range L to R
int productinRange(int l, int r)
{
    if (r - l > 9)
        return 0;

    else {
        int p = 1;

        // Iterate between L to R
        for (int i = l; i <= r; i++)

            p *= getProduct(i);

        return p;
    }
}

// Driver Code
int main()
{
    int l = 11, r = 15;
    cout << productinRange(l, r)
         << endl;

    l = 1, r = 15;
    cout << productinRange(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the product
// of all numbers in range L and R
class GFG{

// Function to get product of digits
static int getProduct(int n)
{
    int product = 1;

    while (n != 0)
    {
        product = product * (n % 10);
        n = n / 10;
    }
    return product;
}

// Function to find the product of digits
// of all natural numbers in range L to R
static int productinRange(int l, int r)
{
    if (r - l > 9)
        return 0;

    else
    {
        int p = 1;

        // Iterate between L to R
        for (int i = l; i <= r; i++)

            p *= getProduct(i);

        return p;
    }
}

// Driver Code
public static void main(String[] args)
{
    int l = 11, r = 15;
    System.out.print(productinRange(l, r) + "\n");

    l = 1; r = 15;
    System.out.print(productinRange(l, r));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to print the product
# of all numbers in range L and R

# Function to get product of digits
def getProduct(n):

    product = 1

    while (n != 0):
        product = product * (n % 10)
        n = int(n / 10)

    return product

# Function to find the product of digits
# of all natural numbers in range L to R
def productinRange(l, r):

    if (r - l > 9):
        return 0

    else:
        p = 1

        # Iterate between L to R
        for i in range(l, r + 1):

            p = p * getProduct(i)

        return p

# Driver Code
l = 11
r = 15
print (productinRange(l, r), end='\n')

l = 1
r = 15
print (productinRange(l, r))

# This code is contributed by PratikBasu
```

## C#

```
// C# program to print the product
// of all numbers in range L and R
using System;

class GFG{

// Function to get product of digits
static int getProduct(int n)
{
    int product = 1;

    while (n != 0)
    {
        product = product * (n % 10);
        n = n / 10;
    }
    return product;
}

// Function to find the product of digits
// of all natural numbers in range L to R
static int productinRange(int l, int r)
{
    if (r - l > 9)
        return 0;

    else
    {
        int p = 1;

        // Iterate between L to R
        for(int i = l; i <= r; i++)
           p *= getProduct(i);

        return p;
    }
}

// Driver Code
public static void Main(String[] args)
{
    int l = 11, r = 15;
    Console.Write(productinRange(l, r) + "\n");

    l = 1; r = 15;
    Console.Write(productinRange(l, r));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program to print the product
// of all numbers in range L and R

// Function to get product of digits
function getProduct(n)
{
    var product = 1;

    while (n != 0) {
        product = product * (n % 10);
        n = parseInt(n / 10);
    }

    return product;
}

// Function to find the product of digits
// of all natural numbers in range L to R
function productinRange(l, r)
{
    if (r - l > 9)
        return 0;

    else {
        var p = 1;

        // Iterate between L to R
        for (var i = l; i <= r; i++)
            p *= getProduct(i);
        return p;
    }
}

// Driver Code
var l = 11, r = 15;
document.write( productinRange(l, r)+ "<br>");
l = 1, r = 15;
document.write( productinRange(l, r));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
120
0
```