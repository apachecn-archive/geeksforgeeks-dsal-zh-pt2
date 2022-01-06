# 给定乘积的 N 个整数的最大 GCD

> 原文:[https://www . geesforgeks . org/maximum-gcd-of-n-integers-with-given-product/](https://www.geeksforgeeks.org/maximum-gcd-of-n-integers-with-given-product/)

给定 N 个具有未知值的整数(a <sub>i</sub> > 0)，其乘积为 p。任务是找到这 N 个整数的最大可能最大公约数。
**例:**

```
Input : N = 3, P = 24
Output : 2
The integers will have maximum GCD of 2 when a1 = 2, a2 = 2, a3 = 6.

Input : N = 2, P = 1
Output : 1
Only possibility is a1 = 1 and a2 = 1.
```

**进场:**

*   首先找到产品 **P** 的所有质因数，并存储在一个 Hashmap 中。
*   当一个质因数在所有整数中通用时， **N** 整数将具有最大 GCD。
*   所以如果**P = P1<sup>k1</sup>* p2<sup>k2</sup>* P3<sup>k3</sup>…。**其中 p1、p2 …为素数，则可得到的最大 GCD 为**ans = P1<sup>k1/N</sup>* p2<sup>k2/N</sup>* P3<sup>k3/N</sup>…。**

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum GCD
// of N integers with product P
int maxGCD(int N, int P)
{

    int ans = 1;

    // map to store prime factors of P
    unordered_map<int, int> prime_factors;

    // prime factorization of P
    for (int i = 2; i * i <= P; i++) {

        while (P % i == 0) {

            prime_factors[i]++;

            P /= i;
        }
    }

    if (P != 1)
        prime_factors[P]++;

    // traverse all prime factors and
    // multiply its 1/N power to the result
    for (auto v : prime_factors)
        ans *= pow(v.first, v.second / N);   

    return ans;
}

// Driver code
int main()
{
    int N = 3, P = 24;

    cout << maxGCD(N, P);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
class Solution
{
// Function to find maximum GCD
// of N integers with product P
static int maxGCD(int N, int P)
{

    int ans = 1;

    // map to store prime factors of P
    Map<Integer, Integer> prime_factors = 
                        new HashMap< Integer,Integer>();

    // prime factorization of P
    for (int i = 2; i * i <= P; i++) {

        while (P % i == 0) {

            if(prime_factors.get(i)==null)
            prime_factors.put(i,1);
            else
            prime_factors.put(i,(prime_factors.get(i)+1));

            P /= i;
        }
    }

    if (P != 1)
            if(prime_factors.get(P)==null)
            prime_factors.put(P,1);
            else
            prime_factors.put(P,(prime_factors.get(P)+1));

    // traverse all prime factors and
    // multiply its 1/N power to the result
        Set< Map.Entry< Integer,Integer> > st = prime_factors.entrySet();   

       for (Map.Entry< Integer,Integer> me:st)
       {

        ans *= Math.pow(me.getKey(),me.getValue() / N);   
        }

    return ans;
}

// Driver code
public static void main(String args[])
{
    int N = 3, P = 24;

    System.out.println( maxGCD(N, P));

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach
from math import sqrt

# Function to find maximum GCD
# of N integers with product P
def maxGCD(N, P):

    ans = 1

    # map to store prime factors of P
    prime_factors = {}

    # prime factorization of P
    for i in range(2, int(sqrt(P) + 1)) :

        while (P % i == 0) :

            if i not in prime_factors :
                prime_factors[i] = 0

            prime_factors[i] += 1
            P //= i

    if (P != 1) :
        prime_factors[P] += 1

    # traverse all prime factors and
    # multiply its 1/N power to the result
    for key, value in prime_factors.items() :
        ans *= pow(key, value // N)

    return ans

# Driver code
if __name__ == "__main__" :

    N, P = 3, 24

    print(maxGCD(N, P))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find maximum GCD
// of N integers with product P
static int maxGCD(int N, int P)
{

    int ans = 1;

    // map to store prime factors of P
    Dictionary<int, int> prime_factors =
                        new Dictionary< int,int>();

    // prime factorization of P
    for (int i = 2; i * i <= P; i++)
    {

        while (P % i == 0)
        {

            if(!prime_factors.ContainsKey(i))
                prime_factors.Add(i, 1);
            else
            prime_factors[i] = prime_factors[i] + 1;

            P /= i;
        }
    }

    if (P != 1)
            if(!prime_factors.ContainsKey(P))
                prime_factors.Add(P, 1);
            else
            prime_factors[P] = prime_factors[P] + 1;

    // traverse all prime factors and
    // multiply its 1/N power to the result
    foreach(KeyValuePair<int, int> me in prime_factors)
    {

        ans *= (int)Math.Pow(me.Key,me.Value / N);
    }

    return ans;
}

// Driver code
public static void Main(String []args)
{
    int N = 3, P = 24;

    Console.WriteLine( maxGCD(N, P));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to find maximum GCD
// of N integers with product P
function maxGCD(N, P) {

    let ans = 1;

    // map to store prime factors of P
    let prime_factors = new Map();

    // prime factorization of P
    for (let i = 2; i * i <= P; i++) {

        while (P % i == 0) {

            if (prime_factors.get(i) == null)
                prime_factors.set(i, 1);
            else
                prime_factors.set(i, (prime_factors.get(i) + 1));
            P = Math.floor(P / i);
        }
    }

    if (P != 1)
        prime_factors[P]++;

    // traverse all prime factors and
    // multiply its 1/N power to the result
    console.log(prime_factors)
    for (let v of prime_factors) {
        console.log(v)
        ans *= Math.pow(v[0], Math.floor(v[1] / N));
    }

    return ans;
}

// Driver code

let N = 3, P = 24;

document.write(maxGCD(N, P));

// This code is contributed by gfgking
</script>
```

**Output:** 

```
2
```