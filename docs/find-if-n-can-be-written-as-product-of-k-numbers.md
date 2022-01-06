# 判断 n 是否可以写成 k 个数字的乘积

> 原文:[https://www . geesforgeks . org/find-if-n-can-write-as-product-of-k-numbers/](https://www.geeksforgeeks.org/find-if-n-can-be-written-as-product-of-k-numbers/)

给定一个正数 n，我们需要精确地打印 k 个正数(都大于 1)，这样 k 个数字的乘积就是 n。如果不存在这样的 k 个数字，打印-1。如果有很多可能答案，你必须打印其中一个答案，其中 k 个数字被排序。
**例:**

```
Input : n = 54, k = 3
Output : 2, 3, 9
Note that 2, 3 and 9 are k numbers
with product equals to n.

Input : n = 54, k = 8
Output : -1
```

这个问题使用的思路非常类似于[打印给定数字](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)的所有质因数。
想法很简单。首先，我们计算 n 的所有素因子，并将它们存储在一个向量中。注意，我们存储每个质数的次数和它在质因数分解中出现的次数一样多。现在为了找到大于 1 的 k 个数，我们检查向量的大小是否大于或等于 k。

1.  如果尺寸小于 k，我们打印-1。
2.  否则我们打印第一个 k-1 因子，因为它来自向量，最后一个因子是向量所有剩余元素的乘积。

注意，我们以排序的方式插入了所有质因数，因此向量中的所有数字都是排序的。这也满足了我们对 k 数的排序条件。

## C++

```
// C++ program to find if it is possible to
// write a number n as product of exactly k
// positive numbers greater than 1.
#include <bits/stdc++.h>
using namespace std;

// Prints k factors of n if n can be written
// as multiple of k numbers.  Else prints -1.
void kFactors(int n, int k)
{
    // A vector to store all prime factors of n
    vector<int> P;

    // Insert all 2's in vector
    while (n%2 == 0)
    {
        P.push_back(2);
        n /= 2;
    }

    // n must be odd at this point
    // So we skip one element (i = i + 2)
    for (int i=3; i*i<=n; i=i+2)
    {
        while (n%i == 0)
        {
            n = n/i;
            P.push_back(i);
        }
    }

    // This is to handle when n > 2 and
    // n is prime
    if (n > 2)
        P.push_back(n);

    // If size(P) < k, k factors are not possible
    if (P.size() < k)
    {
        cout << "-1" << endl;
        return;
    }

    // printing first k-1 factors
    for (int i=0; i<k-1; i++)
        cout << P[i] << ", ";

    // calculating and printing product of rest
    // of numbers
    int product = 1;
    for (int i=k-1; i<P.size(); i++)
        product = product*P[i];
    cout << product << endl;
}

// Driver program to test above function
int main()
{
    int n = 54, k = 3;
    kFactors(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if it is possible to
// write a number n as product of exactly k
// positive numbers greater than 1.
import java.util.*;

class GFG
{

// Prints k factors of n if n can be written
// as multiple of k numbers. Else prints -1.
static void kFactors(int n, int k)
{
    // A vector to store all prime factors of n
    ArrayList<Integer> P = new ArrayList<Integer>();

    // Insert all 2's in list
    while (n % 2 == 0)
    {
        P.add(2);
        n /= 2;
    }

    // n must be odd at this point
    // So we skip one element (i = i + 2)
    for (int i = 3; i * i <= n; i = i + 2)
    {
        while (n % i == 0)
        {
            n = n / i;
            P.add(i);
        }
    }

    // This is to handle when n > 2 and
    // n is prime
    if (n > 2)
        P.add(n);

    // If size(P) < k, k factors are
    // not possible
    if (P.size() < k)
    {
        System.out.println("-1");
        return;
    }

    // printing first k-1 factors
    for (int i = 0; i < k - 1; i++)
        System.out.print(P.get(i) + ", ");

    // calculating and printing product
    // of rest of numbers
    int product = 1;
    for (int i = k - 1; i < P.size(); i++)
        product = product * P.get(i);
    System.out.println(product);
}

// Driver code
public static void main(String[] args)
{
    int n = 54, k = 3;
    kFactors(n, k);
}
}

// This code is contributed
// by chandan_jnu
```

## 蟒蛇 3

```
# Python3 program to find if it is possible
# to write a number n as product of exactly k
# positive numbers greater than 1.
import math as mt

# Prints k factors of n if n can be written
# as multiple of k numbers. Else prints -1
def kFactors(n, k):

    # list to store all prime factors of n
    a = list()

    #insert all 2's in list
    while n % 2 == 0:
        a.append(2)
        n = n // 2

    # n must be odd at this point
    # so we skip one element(i=i+2)
    for i in range(3, mt.ceil(mt.sqrt(n)), 2):
        while n % i == 0:
            n = n / i;
            a.append(i)

    # This is to handle when n>2 and
    # n is prime
    if n > 2:
        a.append(n)

    # if size(a)<k,k factors are not possible
    if len(a) < k:
        print("-1")
        return

    # printing first k-1 factors
    for i in range(k - 1):
        print(a[i], end = ", ")

    # calculating and printing product
    # of rest of numbers
    product = 1

    for i in range(k - 1, len(a)):
        product *= a[i]
    print(product)

# Driver code
n, k = 54, 3
kFactors(n, k)

# This code is contributed
# by mohit kumar 29
```

## C#

```
// C# program to find if it is possible to
// write a number n as product of exactly k
// positive numbers greater than 1.
using System;
using System.Collections;

class GFG
{

// Prints k factors of n if n can be written
// as multiple of k numbers. Else prints -1.
static void kFactors(int n, int k)
{
    // A vector to store all prime factors of n
    ArrayList P = new ArrayList();

    // Insert all 2's in list
    while (n % 2 == 0)
    {
        P.Add(2);
        n /= 2;
    }

    // n must be odd at this point
    // So we skip one element (i = i + 2)
    for (int i = 3; i * i <= n; i = i + 2)
    {
        while (n % i == 0)
        {
            n = n / i;
            P.Add(i);
        }
    }

    // This is to handle when n > 2 and
    // n is prime
    if (n > 2)
        P.Add(n);

    // If size(P) < k, k factors are not possible
    if (P.Count < k)
    {
        Console.WriteLine("-1");
        return;
    }

    // printing first k-1 factors
    for (int i = 0; i < k - 1; i++)
        Console.Write(P[i]+", ");

    // calculating and printing product of rest
    // of numbers
    int product = 1;
    for (int i = k - 1; i < P.Count; i++)
        product = product*(int)P[i];
    Console.WriteLine(product);
}

// Driver code
static void Main()
{
    int n = 54, k = 3;
    kFactors(n, k);
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if it is possible to
// write a number n as product of exactly k
// positive numbers greater than 1.

// Prints k factors of n if n can be written
// as multiple of k numbers. Else prints -1.
function kFactors($n, $k)
{
    // A vector to store all prime
    // factors of n
    $P = array();

    // Insert all 2's in vector
    while ($n % 2 == 0)
    {
        array_push($P, 2);
        $n = (int)($n / 2);
    }

    // n must be odd at this point
    // So we skip one element (i = i + 2)
    for ($i = 3; $i * $i <= $n; $i = $i + 2)
    {
        while ($n % $i == 0)
        {
            $n = (int)($n / $i);
            array_push($P, $i);
        }
    }

    // This is to handle when n > 2 and
    // n is prime
    if ($n > 2)
        array_push($P, $n);

    // If size(P) < k, k factors are
    // not possible
    if (count($P) < $k)
    {
        echo "-1\n";
        return;
    }

    // printing first k-1 factors
    for ($i = 0; $i < $k - 1; $i++)
        echo $P[$i] . ", ";

    // calculating and printing product
    // of rest of numbers
    $product = 1;
    for ($i = $k - 1; $i < count($P); $i++)
        $product = $product * $P[$i];
    echo $product;
}

// Driver Code
$n = 54;
$k = 3;
kFactors($n, $k);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to find if it is possible to
// write a number n as product of exactly k
// positive numbers greater than 1.

    // Prints k factors of n if n can be written
    // as multiple of k numbers. Else prints -1.
    function kFactors(n , k) {
        // A vector to store all prime factors of n
        var P = Array();

        // Insert all 2's in list
        while (n % 2 == 0) {
            P.push(2);
            n = parseInt(n/2);
        }

        // n must be odd at this point
        // So we skip one element (i = i + 2)
        for (i = 3; i * i <= n; i = i + 2) {
            while (n % i == 0) {
                n = parseInt(n/i);
                P.push(i);
            }
        }

        // This is to handle when n > 2 and
        // n is prime
        if (n > 2)
            P.push(n);

        // If size(P) < k, k factors are
        // not possible
        if (P.length < k) {
            document.write("-1");
            return;
        }

        // printing first k-1 factors
        for (i = 0; i < k - 1; i++)
            document.write(P[i] + ", ");

        // calculating and printing product
        // of rest of numbers
        var product = 1;
        for (i = k - 1; i < P.length; i++)
            product = product * P[i];
        document.write(product);
    }

    // Driver code

        var n = 54, k = 3;
        kFactors(n, k);

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
2, 3, 9
```

本文由 [**普拉蒂克·查哈尔**](https://github.com/pratik-chhajer) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。