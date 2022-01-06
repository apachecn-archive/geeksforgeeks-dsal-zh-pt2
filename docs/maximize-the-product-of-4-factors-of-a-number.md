# 最大化一个数的四个因子的乘积

> 原文:[https://www . geeksforgeeks . org/最大化 4 因子产品数/](https://www.geeksforgeeks.org/maximize-the-product-of-4-factors-of-a-number/)

给定一个整数 N，任务是找到 A，B，C，D 的最大乘积，使得以下条件满足:

> *   **N % A = = 0**&&T2】N % B = = 0&&T4】N % C = = 0&&T6】N % D = = 0。
> *   Maximize product A*B*C*D where N = A+B+C+D

如果不存在解决方案，请打印“-1”(不带引号)。

**示例:**

```
Input: N = 8
Output: 16
The divisors of 8 are {1, 2, 4, 8}. 
The maximized product can be formed 
by multiplying 2*2*2*2 = 16 as 2+2+2+2 = 8.

Input: N = 4 
Output: 1
The divisors of 4 are {1, 2, 4}. 
The maximized product can be formed
by multiplying 1*1*1*1 = 1 as 1+1+1+1 =4.
```

**天真方法:**

1.  找出给定数字的因子，并将其存储在复杂度为 **O(sqrt(n))** 的名为*因子*的向量中。
2.  初始化乘积= -1，然后我们迭代因子向量，应用蛮力方法找到最大化乘积。

**以下是上述方法的实施:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Declare the vector of factors for storing the
vector<int> factors;

// function to find out the factors of a number
void findFactors(int n)
{
    // Loop until the i reaches the sqrt(n)
    for (int i = 1; i * i <= n; i++) {

        // Check if i is a factor of n
        if (n % i == 0) {

            // if both the factors are same
            // we only push one factor
            if ((n / i) == i)
                factors.push_back(i);

            else {

                // factor1 is pushed
                factors.push_back(n / i);

                // factor2 is pushed
                factors.push_back(i);
            }
        }
    }
}

// Function to find the maximum product
int findProduct(int n)
{
    // Initialize the product with -1
    int product = -1;
    int si = factors.size();
    for (int i = 0; i < si; i++)
        for (int j = 0; j < si; j++)
            for (int k = 0; k < si; k++)
                for (int l = 0; l < si; l++) {

                    // Find the sum of factors and store it in s
                    int s = factors[i] + factors[j]
                            + factors[k] + factors[l];

                    // Compare whether it is equal to the n
                    if (s == n) {

                        // product of factors
                        int p = factors[i] * factors[j] * factors[k] * factors[l];

                        // Check whether we have a better
                        // p now if yes update
                        if (p > product)
                            product = p;
                    }
                }

    return product;
}

// Driver code
int main()
{
    int n = 10;

    // initializes the vectors with the divisors of n
    findFactors(n);

    // prints out the maximised product.
    cout << findProduct(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.util.ArrayList;
import java.util.List;

public class GFG {

// Declare the ArrayList of factors for storing the
    static List< Integer> factors = new ArrayList<>(10);

// function to find out the factors of a number
    static void findFactors(int n) {
        // Loop until the i reaches the sqrt(n)
        for (int i = 1; i * i <= n; i++) {

            // Check if i is a factor of n
            if (n % i == 0) {
                // if both the factors are same
                // we only push one factor
                if ((n / i) == i) {
                    factors.add(factors.size(), i);
                } else {

                    // factor1 is pushed
                    factors.add(factors.size(), n / i);

                    // factor2 is pushed
                    factors.add(factors.size(), i);
                }
            }
        }
    }

// Function to find the maximum product
    static int findProduct(int n) {
        // Initialize the product with -1

        int product = -1;
        int si = factors.size();
        for (int i = 0; i < si; i++) {
            for (int j = 0; j < si; j++) {
                for (int k = 0; k < si; k++) {
                    for (int l = 0; l < si; l++) {

                        // Find the sum of factors and store it in s
                        int s = factors.get(i) + factors.get(j)
                                + factors.get(k) + factors.get(l);

                        // Compare whether it is equal to the n
                        if (s == n) {

                            // product of factors
                            int p = factors.get(i) * factors.get(j) * factors.get(k) *
                                               factors.get(l);

                            // Check whether we have a better
                            // p now if yes update
                            if (p > product) {
                                product = p;
                            }
                        }
                    }
                }
            }
        }

        return product;
    }

    // Driver Code
    public static void main(String[] args) {
        int n = 10;

        // initializes the List with the divisors of n
        findFactors(n);
        // prints out the maximised product.
        System.out.println(findProduct(n));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of above approach
from math import sqrt

# Declare the vector of factors
# for storing the
factors = []

# function to find out the factors
# of a number
def findFactors(n):

    # Loop until the i reaches the sqrt(n)
    for i in range(1, int(sqrt(n)) + 1, 1):

        # Check if i is a factor of n
        if (n % i == 0):

            # if both the factors are same
            # we only push one factor
            if ((n / i) == i):
                factors.append(i)

            else:

                # factor1 is pushed
                factors.append(n / i)

                # factor2 is pushed
                factors.append(i)

# Function to find the maximum product
def findProduct(n):

    # Initialize the product with -1
    product = -1
    si = len(factors)
    for i in range(si):
        for j in range(si):
            for k in range(si):
                for l in range(si):

                    # Find the sum of factors and store it in s
                    s = (factors[i] + factors[j] +
                         factors[k] + factors[l])

                    # Compare whether it is equal to the n
                    if (s == n):

                        # product of factors
                        p = (factors[i] * factors[j] *
                             factors[k] * factors[l])

                        # Check whether we have a better
                        # p now if yes update
                        if (p > product):
                            product = p

    return product

# Driver code
if __name__ == '__main__':
    n = 10

    # initializes the vectors with
    # the divisors of n
    findFactors(n)

    # prints out the maximised product.
    print(int(findProduct(n)))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG
{

// Declare the ArrayList of factors for storing the
static List<int> factors = new List<int>(10);

// function to find out the factors of a number
static void findFactors(int n)
{
    // Loop until the i reaches the sqrt(n)
    for (int i = 1; i * i <= n; i++)
    {

        // Check if i is a factor of n
        if (n % i == 0)
        {
            // if both the factors are same
            // we only push one factor
            if ((n / i) == i)
            {
                factors.Insert(factors.Count, i);
            }
            else
            {

                // factor1 is pushed
                factors.Insert(factors.Count, n / i);

                // factor2 is pushed
                factors.Insert(factors.Count, i);
            }
        }
    }
}

// Function to find the maximum product
static int findProduct(int n)
{

    // Initialize the product with -1
    int product = -1;
    int si = factors.Count;
    for (int i = 0; i < si; i++)
    {
        for (int j = 0; j < si; j++)
        {
            for (int k = 0; k < si; k++)
            {
                for (int l = 0; l < si; l++)
                {

                    // Find the sum of factors and store it in s
                    int s = factors[i] + factors[j] +
                            factors[k] + factors[l];

                    // Compare whether it is equal to the n
                    if (s == n)
                    {

                        // product of factors
                        int p = factors[i] * factors[j] *
                                factors[k] * factors[l];

                        // Check whether we have a better
                        // p now if yes update
                        if (p > product)
                        {
                            product = p;
                        }
                    }
                }
            }
        }
    }
    return product;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 10;

    // initializes the List with the divisors of n
    findFactors(n);

    // prints out the maximised product.
    Console.WriteLine(findProduct(n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

    // Declare the ArrayList of factors for storing the
    let factors = [];

    // function to find out the factors of a number
    function findFactors(n)
    {

        // Loop until the i reaches the sqrt(n)
        for (let i = 1; i * i <= n; i++)
        {

            // Check if i is a factor of n
            if (n % i == 0)
            {

                // if both the factors are same
                // we only push one factor
                if ((n / i) == i) {
                    factors.push(i);
                } else {

                    // factor1 is pushed
                    factors.push( n / i);

                    // factor2 is pushed
                    factors.push( i);
                }
            }
        }
    }

    // Function to find the maximum product
    function findProduct(n)
    {

           // Initialize the product with -1  
        let product = -1;
        let si = factors.length;
        for (let i = 0; i < si; i++) {
            for (let j = 0; j < si; j++) {
                for (let k = 0; k < si; k++) {
                    for (let l = 0; l < si; l++) {

                        // Find the sum of factors and store it in s
                        let s = factors[i] + factors[j]
                                + factors[k] + factors[l];

                        // Compare whether it is equal to the n
                        if (s == n) {

                            // product of factors
                            let p = factors[i] * factors[j] * factors[k] *
                                               factors[l];

                            // Check whether we have a better
                            // p now if yes update
                            if (p > product) {
                                product = p;
                            }
                        }
                    }
                }
            }
        }

        return product;
    }

    // Driver Code
    let n = 10;

    // initializes the List with the divisors of n
    findFactors(n);

    // prints out the maximised product.
    document.write(findProduct(n));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
20
```

**时间复杂度:**o((divisors)^4 的编号))

**更好的方法:**通过从上述代码中去除第四个循环，改为使用二分搜索法来寻找第四个因子，可以稍微降低复杂度。因为二分搜索法只在列表排序时工作。所以我们需要对因子向量进行排序，这样我们就可以把二分搜索法应用到这个问题上。

**以下是上述方法的实施:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// We declare the vector of factors for storing the
vector<int> factors;

// function to find out the factors of a number
void findFactors(int n)
{
    // we loop until the i reaches the sqrt(n)
    for (int i = 1; i * i <= n; i++) {

        // we check if i is a factor of n
        if (n % i == 0) {

            // if both the factors are same
            // only push one factor
            if ((n / i) == i) {
                factors.push_back(i);
            }
            else {

                // factor1 is pushed
                factors.push_back(n / i);

                // factor2 is pushed
                factors.push_back(i);
            }
        }
    }
}

int findProduct(int n)
{
    // initialise the product with -1
    int product = -1;
    int si = factors.size();

    for (int i = 0; i < si; i++)
        for (int j = 0; j < si; j++)
            for (int k = 0; k < si; k++) {

                // we find the sum of factors
                // and store it in s
                int s = factors[i] + factors[j] + factors[k];

                // we check whether the fourth
                // factor exists or not
                if (binary_search(factors.begin(), factors.end(), n - s)) {
                    // product of factors
                    int p = factors[i] * factors[j] * factors[k] * (n - s);

                    // we check whether we have a better
                    // p now if yes update
                    if (p > product)
                        product = p;
                }
            }

    return product;
}

// Driver code
int main()
{
    int n = 10;

    // initializes the vectors with the divisors of n
    findFactors(n);

    // sorts the factors vector
    sort(factors.begin(), factors.end());

    // prints out the maximised product.
    cout << findProduct(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class GFG {

// Declare the ArrayList of factors for storing the
    static List< Integer> factors = new ArrayList<>();

// function to find out the factors of a number
    static void findFactors(int n) {
        // we loop until the i reaches the sqrt(n)
        for (int i = 1; i * i <= n; i++) {

            // we check if i is a factor of n
            if (n % i == 0) {

                // if both the factors are same
                // only push one factor
                if ((n / i) == i) {
                    factors.add(factors.size(), i);
                } else {

                    // factor1 is pushed
                    factors.add(factors.size(), n/i);

                    // factor2 is pushed
                    factors.add(factors.size(), i);
                }
            }
        }
    }

// Function to find the maximum product
    static int findProduct(int n) {
// initialise the product with -1
        int product = -1;
        int si = factors.size();

        for (int i = 0; i < si; i++) {
            for (int j = 0; j < si; j++) {
                for (int k = 0; k < si; k++) {

                    // we find the sum of factors
                    // and store it in s
                    int s = factors.get(i) + factors.get(j) + factors.get(k);

                    // we check whether the fourth
                    // factor exists or not
                    if (Collections.binarySearch(factors, n - s) >= 0) {
                        // product of factors
                        int p = factors.get(i) * factors.get(j) * factors.get(k) * (n - s);

                        // we check whether we have a better
                        // p now if yes update
                        if (p > product) {
                            product = p;
                        }
                    }
                }
            }
        }

        return product;
    }

    // Driver Code
    public static void main(String[] args) {
        int n = 10;

        // initializes the vectors with the divisors of n
        findFactors(n);

        // sorts the factors vector
        Collections.sort(factors);

        // prints out the maximised product.
        System.out.println(findProduct(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# We declare the vector of factors for storing the
factors = []

# function to find out the factors of a number
def findFactors(n):

    # we loop until the i reaches the sqrt(n)
    for i in range(1, n + 1):
        if i * i > n:
            break

        # we check if i is a factor of n
        if (n % i == 0):

            # if both the factors are same
            # only push one factor
            if ((n / i) == i):
                factors.append(i)
            else:

                # factor1 is pushed
                factors.append(n // i)

                # factor2 is pushed
                factors.append(i)

def findProduct(n):

    # initialise the product with -1
    product = -1
    si = len(factors)

    for i in range(si):
        for j in range(si):
            for k in range(si):

                # we find the sum of factors
                # and store it in s
                s = factors[i] + factors[j] + factors[k]

                # we check whether the fourth
                # factor exists or not
                if ((n - s) in factors):

                    # product of factors
                    p = factors[i] * factors[j] * \
                        factors[k] * (n - s)

                    # we check whether we have a better
                    # p now if yes update
                    if (p > product):
                        product = p

    return product

# Driver code
n = 10

# initializes the vectors
# with the divisors of n
findFactors(n)

# sorts the factors vector
factors = sorted(factors)

# prints out the maximized product.
print(findProduct(n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG
{

// Declare the ArrayList of factors for storing the
static List< int> factors = new List<int>();

// function to find out the factors of a number
static void findFactors(int n)
{
    // we loop until the i reaches the sqrt(n)
    for (int i = 1; i * i <= n; i++)
    {

        // we check if i is a factor of n
        if (n % i == 0)
        {

            // if both the factors are same
            // only push one factor
            if ((n / i) == i)
            {
                factors.Insert(factors.Count, i);
            }
            else
            {

                // factor1 is pushed
                factors.Insert(factors.Count, n / i);

                // factor2 is pushed
                factors.Insert(factors.Count, i);
            }
        }
    }
}

// Function to find the maximum product
static int findProduct(int n)
{

    // initialise the product with -1
    int product = -1;
    int si = factors.Count;

    for (int i = 0; i < si; i++)
    {
        for (int j = 0; j < si; j++)
        {
            for (int k = 0; k < si; k++)
            {

                // we find the sum of factors
                // and store it in s
                int s = factors[i] + factors[j] + factors[k];

                // we check whether the fourth
                // factor exists or not
                if (factors.BinarySearch(n - s) >= 0)
                {
                    // product of factors
                    int p = factors[i] * factors[j] *
                            factors[k] * (n - s);

                    // we check whether we have a better
                    // p now if yes update
                    if (p > product)
                    {
                        product = p;
                    }
                }
            }
        }
    }
    return product;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 10;

    // initializes the vectors with the divisors of n
    findFactors(n);

    // sorts the factors vector
    factors.Sort();

    // prints out the maximised product.
    Console.WriteLine(findProduct(n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

    // Declare the ArrayList of factors for storing the
    let factors = [];

    // function to find out the factors of a number
    function findFactors(n)
    {
        // we loop until the i reaches the sqrt(n)
        for (let i = 1; i * i <= n; i++) {

            // we check if i is a factor of n
            if (n % i == 0) {

                // if both the factors are same
                // only push one factor
                if ((n / i) == i) {
                    factors.push( i);
                } else {

                    // factor1 is pushed
                    factors.push( n/i);

                    // factor2 is pushed
                    factors.push( i);
                }
            }
        }
    }

    // Function to find the maximum product
    function findProduct(n)
    {
        let product = -1;
        let si = factors.length;

        for (let i = 0; i < si; i++) {
            for (let j = 0; j < si; j++) {
                for (let k = 0; k < si; k++) {

                    // we find the sum of factors
                    // and store it in s
                    let s = factors[i] + factors[j] +
                    factors[k];

                    // we check whether the fourth
                    // factor exists or not
                    if ( factors.includes(n-s)) {
                        // product of factors
                        let p = factors[i] * factors[j] *
                        factors[k] * (n - s);

                        // we check whether we have a better
                        // p now if yes update
                        if (p > product) {
                            product = p;
                        }
                    }
                }
            }
        }

        return product;
    }

    // Driver Code

    let n = 10;
    // initializes the vectors with the divisors of n
    findFactors(n);

    // sorts the factors vector
    factors.sort(function(a,b){return a-b;});

    // prints out the maximised product.
    document.write(findProduct(n));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
20
```

**时间复杂度:**o((divisors)^3 数*对数(除数))

**有效方法:**这是返回的最大化乘积，最多为前 40 个自然数。

> 1-> -1, 2-> -1, 3-> -1, 4-> 1 , 5-> -1 , 6-> 4, 7-> -1, 8-> 16, 9-> -1, 10-> 20, 11-> -1 12-> 81, 13-> -1, 14-> -1 , 15-> -1, 16-> 256, 17-> -1 18-> 324, 19-> -1, 20-> 625, 21-> -1, 22-> -1, 23-> -1, 24-> 1296, 25-> -1, 26-> -1 27-> -1, 28-> 2401, 29-> -1, 30-> 2500, 31-> -1, 32-> 4096, 33-> -1, 34-> -1 35-> -1, 36-> 6561, 37-> -1, 38-> -1, 39-> -1, 40-> 10000, 41-> -1, 42-> 9604

如果我们仔细观察这种模式，我们会发现这种模式在某些情况下有些常见。

**例如:**

1.  对于每个奇数都没有解，因此返回-1。
2.  对于小于 4 的数字没有解决办法。
3.  对于每一个可被 4 整除的数，解总是以(n/4)^4.)的形式出现
    *   像 4 这样有因子{1，2，4}的数的解是 1 和(4/4)^4 = 1。
    *   像 8 这样有因子{1，2，4，8}解的数字是 16 ans (8/4)^4 = 16。
4.  对于每一个可被 6 整除的数，解总是以(n/3)^2 * (n/6)^2)的形式出现
    *   像 6 这样有因子{1，2，3，6}的数的解是 4 和(6/3)^2 * (6/6)^2 = 4。
    *   像 18 这样有因子{1，2，3，6，9，18}解的数字是 324 和(18/3)^2 * (18/6)^2 = 324。
5.  对于每一个能被 10 整除的数，解总是以(n/10) * (n/5)^2 * (n/2)的形式出现
    *   像 10 这样有因子{1，2，5，10}的数的解是 20 和(10/10)*(10/5)^2 * (10/2) = 20。
    *   像 20 这样有因子{1，2，5，10，25，50}解的数字是 12500 和(50/10)*(50/5)^2 *(50/2) = 12500。
6.  对于每隔一个偶数，像 14 和 22 这样的数字是没有解的。

**注:**我们首先考虑除以数的最低因子，为了计算最大乘积，我们忽略接下来的连续因子。例如，12 可以同时被 4 和 6 整除。但是我们考虑了最少的因子来计算，所以我们考虑 4 作为它的除数来计算乘积。

**以下是上述方法的实施:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// For calculation of a^b
int modExp(int a, int b)
{
    int result = 1;
    while (b > 0) {
        if (b & 1)
            result = result * a;
        a = a * a;
        b /= 2;
    }

    return result;
}

// Function to check
int check(int num)
{
    // every odd and number less than 3.
    if (num & 1 || num < 3)
        return -1;

    // every number divisible by 4.
    else if (num % 4 == 0)
        return modExp(num / 4, 4);

    // every number divisible by 6.
    else if (num % 6 == 0)
        return modExp(num / 3, 2) * modExp(num / 6, 2);

    // every number divisible by 10.
    else if (num % 10 == 0)
        return modExp(num / 5, 2) * (num / 10) * (num / 2);

    // for every even number which is not
    // divisible by above values.
    else
        return -1;
}

// Driver code
int main()
{
    int num = 10;
    cout << check(num);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG
{
// For calculation of a^b
static int modExp(int a, int b)
{
    int result = 1;
    while (b > 0)
    {
        if (b == 1)
            result = result * a;
        a = a * a;
        b /= 2;
    }

    return result;
}

// Function to check
static int check(int num)
{
    // every odd and number less than 3.
    if (num == 1 || num < 3)
        return -1;

    // every number divisible by 4.
    else if (num % 4 == 0)
        return modExp(num / 4, 4);

    // every number divisible by 6.
    else if (num % 6 == 0)
        return modExp(num / 3, 2) * modExp(num / 6, 2);

    // every number divisible by 10.
    else if (num % 10 == 0)
        return modExp(num / 5, 2) * (num / 10) * (num / 2);

    // for every even number which is not
    // divisible by above values.
    else
        return -1;
}

// Driver code
public static void main(String[] args)
{
    int num = 10;
    System.out.print(check(num));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# For calculation of a^b
def modExp( a, b):

    result = 1
    while (b > 0):
        if (int(b) & 1):
            result = result * a
        a = a * a
        b /= 2

    return result

# Function to check
def check( num):

    # every odd and number less than 3.
    if (num & 1 or num < 3):
        return -1

    # every number divisible by 4.
    elif (num % 4 == 0):
        return modExp(num / 4, 4)

    # every number divisible by 6.
    elif (num % 6 == 0):
        return modExp(num / 3, 2) * modExp(num / 6, 2)

    # every number divisible by 10.
    elif (num % 10 == 0):
        return modExp(num / 5, 2) * (num / 10) * (num / 2)

    # for every even number which is not
    # divisible by above values.
    else:
        return -1

# Driver code
if __name__=='__main__':
    num = 10
    print(int(check(num)))

# This code is contributed by ash264
```

## C#

```
// C#  implementation of above approach
using System;

public class GFG{
    // For calculation of a^b
static int modExp(int a, int b)
{
    int result = 1;
    while (b > 0)
    {
        if (b == 1)
            result = result * a;
        a = a * a;
        b /= 2;
    }

    return result;
}

// Function to check
static int check(int num)
{
    // every odd and number less than 3.
    if (num == 1 || num < 3)
        return -1;

    // every number divisible by 4.
    else if (num % 4 == 0)
        return modExp(num / 4, 4);

    // every number divisible by 6.
    else if (num % 6 == 0)
        return modExp(num / 3, 2) * modExp(num / 6, 2);

    // every number divisible by 10.
    else if (num % 10 == 0)
        return modExp(num / 5, 2) * (num / 10) * (num / 2);

    // for every even number which is not
    // divisible by above values.
    else
        return -1;
}

// Driver code
static public void Main (){

    int num = 10;
    Console.WriteLine(check(num));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of above approach

// For calculation of a^b
function modExp($a, $b)
{
    $result = 1;
    while ($b > 0)
    {
        if ($b & 1)
            $result = $result * $a;
        $a = $a * $a;
        $b /= 2;
    }

    return $result;
}

// Function to check
function check($num)
{
    // every odd and number less than 3.
    if ($num & 1 || $num < 3)
        return -1;

    // every number divisible by 4.
    else if ($num % 4 == 0)
        return modExp($num / 4, 4);

    // every number divisible by 6.
    else if ($num % 6 == 0)
        return modExp($num / 3, 2) *
               modExp($num / 6, 2);

    // every number divisible by 10.
    else if ($num % 10 == 0)
        return modExp($num / 5, 2) *
                     ($num / 10) * ($num / 2);

    // for every even number which is not
    // divisible by above values.
    else
        return -1;
}

// Driver code

$num = 10;
echo check($num);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// For calculation of a^b
function modExp(a, b)
{
    let result = 1;

    while (b > 0)
    {
        if (b == 1)
            result = result * a;

        a = a * a;
        b = Math.floor(b / 2);
    }
    return result;
}

// Function to check
function check(num)
{

    // every odd and number less than 3.
    if (num == 1 || num < 3)
        return -1;

    // Every number divisible by 4.
    else if (num % 4 == 0)
        return modExp(Math.floor(num / 4), 4);

    // Every number divisible by 6.
    else if (num % 6 == 0)
        return modExp(Math.floor(num / 3), 2) *
               modExp(Math.floor(num / 6), 2);

    // Every number divisible by 10.
    else if (num % 10 == 0)
        return modExp(Math.floor(num / 5), 2) *
                      Math.floor(num / 10) *
                      Math.floor(num / 2);

    // For every even number which is not
    // divisible by above values.
    else
        return -1;
}

// Driver code
let num = 10;

document.write(check(num));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
20
```

**时间复杂度:** O(log N)