# 为给定乘积的三元组找到不同的整数

> 原文:[https://www . geeksforgeeks . org/find-distinct-integer-for-a-triple-with-给定-product/](https://www.geeksforgeeks.org/find-distinct-integers-for-a-triplet-with-given-product/)

给定一个整数 **X** ，任务是找出大于 **1** 的三个不同的整数，即**A****B**和 **C** ，使得 **(A * B * C) = X** 。如果不存在这样的三元组，则打印 **-1** 。
**示例:**

> **输入:** X = 64
> **输出:** 2 4 8
> (2 * 4 * 8) = 64
> **输入:** X = 32
> **输出:** -1
> 不存在这样的三元组。

**逼近:**假设我们有一个三元组 **(A，B，C)** 。请注意，为了使它们的乘积等于 **X** ，每个整数都必须是 **X** 的因子。因此，使用本文中讨论的方法，将 **X** 的所有因素存储在 **O(sqrt(X))** 时间中。
现在最多会有 **sqrt(X)** 因素。接下来，通过运行两个循环来迭代每个因子，一个循环选择 **A** ，另一个循环选择 **B** 。现在如果这个三元组有效，即 **C = X / (A * B)** ，其中 **C** 也是 **X** 的因子。要检查这一点，请将所有因素存储在[无序 _ 集合](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)中。如果找到有效的三联体，则打印三联体，否则打印 **-1** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required triplets
void findTriplets(int x)
{
    // To store the factors
    vector<int> fact;
    unordered_set<int> factors;

    // Find factors in sqrt(x) time
    for (int i = 2; i <= sqrt(x); i++) {
        if (x % i == 0) {
            fact.push_back(i);
            if (x / i != i)
                fact.push_back(x / i);
            factors.insert(i);
            factors.insert(x / i);
        }
    }

    bool found = false;
    int k = fact.size();
    for (int i = 0; i < k; i++) {

        // Choose a factor
        int a = fact[i];
        for (int j = 0; j < k; j++) {

            // Choose another factor
            int b = fact[j];

            // These conditions need to be
            // met for a valid triplet
            if ((a != b) && (x % (a * b) == 0)
                && (x / (a * b) != a)
                && (x / (a * b) != b)
                && (x / (a * b) != 1)) {

                // Print the valid triplet
                cout << a << " " << b << " "
                     << (x / (a * b));
                found = true;
                break;
            }
        }

        // Triplet found
        if (found)
            break;
    }

    // Triplet not found
    if (!found)
        cout << "-1";
}

// Driver code
int main()
{
    int x = 105;

    findTriplets(x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to find the required triplets
static void findTriplets(int x)
{
    // To store the factors
    Vector<Integer> fact = new Vector<Integer>();
    HashSet<Integer> factors = new HashSet<Integer>();

    // Find factors in Math.sqrt(x) time
    for (int i = 2; i <= Math.sqrt(x); i++)
    {
        if (x % i == 0)
        {
            fact.add(i);
            if (x / i != i)
                fact.add(x / i);
            factors.add(i);
            factors.add(x / i);
        }
    }

    boolean found = false;
    int k = fact.size();
    for (int i = 0; i < k; i++)
    {

        // Choose a factor
        int a = fact.get(i);
        for (int j = 0; j < k; j++)
        {

            // Choose another factor
            int b = fact.get(j);

            // These conditions need to be
            // met for a valid triplet
            if ((a != b) && (x % (a * b) == 0)
                && (x / (a * b) != a)
                && (x / (a * b) != b)
                && (x / (a * b) != 1))
            {

                // Print the valid triplet
                System.out.print(a+ " " + b + " "
                    + (x / (a * b)));
                found = true;
                break;
            }
        }

        // Triplet found
        if (found)
            break;
    }

    // Triplet not found
    if (!found)
        System.out.print("-1");
}

// Driver code
public static void main(String[] args)
{
    int x = 105;

    findTriplets(x);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

# Function to find the required triplets
def findTriplets(x) :

    # To store the factors
    fact = [];
    factors = set();

    # Find factors in sqrt(x) time
    for i in range(2, int(sqrt(x))) :
        if (x % i == 0) :
            fact.append(i);

            if (x / i != i) :
                fact.append(x // i);

            factors.add(i);
            factors.add(x // i);

    found = False;
    k = len(fact);

    for i in range(k) :

        # Choose a factor
        a = fact[i];

        for j in range(k) :

            # Choose another factor
            b = fact[j];

            # These conditions need to be
            # met for a valid triplet
            if ((a != b) and (x % (a * b) == 0)
                and (x / (a * b) != a)
                and (x / (a * b) != b)
                and (x / (a * b) != 1)) :

                # Print the valid triplet
                print(a,b,x // (a * b));
                found = True;
                break;

        # Triplet found
        if (found) :
            break;

    # Triplet not found
    if (not found) :
        print("-1");

# Driver code
if __name__ == "__main__" :

    x = 105;

    findTriplets(x);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the required triplets
static void findTriplets(int x)
{
    // To store the factors
    List<int> fact = new List<int>();
    HashSet<int> factors = new HashSet<int>();

    // Find factors in Math.Sqrt(x) time
    for (int i = 2; i <= Math.Sqrt(x); i++)
    {
        if (x % i == 0)
        {
            fact.Add(i);
            if (x / i != i)
                fact.Add(x / i);
            factors.Add(i);
            factors.Add(x / i);
        }
    }

    bool found = false;
    int k = fact.Count;
    for (int i = 0; i < k; i++)
    {

        // Choose a factor
        int a = fact[i];
        for (int j = 0; j < k; j++)
        {

            // Choose another factor
            int b = fact[j];

            // These conditions need to be
            // met for a valid triplet
            if ((a != b) && (x % (a * b) == 0)
                && (x / (a * b) != a)
                && (x / (a * b) != b)
                && (x / (a * b) != 1))
            {

                // Print the valid triplet
                Console.Write(a+ " " + b + " "
                    + (x / (a * b)));
                found = true;
                break;
            }
        }

        // Triplet found
        if (found)
            break;
    }

    // Triplet not found
    if (!found)
        Console.Write("-1");
}

// Driver code
public static void Main(String[] args)
{
    int x = 105;

    findTriplets(x);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the required triplets
function findTriplets(x)
{
    // To store the factors
    let fact = [];
    let factors = new Set();

    // Find factors in Math.sqrt(x) time
    for (let i = 2; i <= Math.sqrt(x); i++)
    {
        if (x % i == 0)
        {
            fact.push(i);
            if (x / i != i)
                fact.push(x / i);
            factors.add(i);
            factors.add(x / i);
        }
    }

    let found = false;
    let k = fact.length;
    for (let i = 0; i < k; i++)
    {

        // Choose a factor
        let a = fact[i];
        for (let j = 0; j < k; j++)
        {

            // Choose another factor
            let b = fact[j];

            // These conditions need to be
            // met for a valid triplet
            if ((a != b) && (x % (a * b) == 0)
                && (x / (a * b) != a)
                && (x / (a * b) != b)
                && (x / (a * b) != 1))
            {

                // Prlet the valid triplet
                document.write(a+ " " + b + " "
                    + (x / (a * b)));
                found = true;
                break;
            }
        }

        // Triplet found
        if (found)
            break;
    }

    // Triplet not found
    if (!found)
        document.write("-1");
}

// Driver code

      let x = 105;

    findTriplets(x);

</script>
```

**Output:** 

```
3 5 7
```

**时间复杂度:** O(N)，N=X

**辅助空间:** O(N)