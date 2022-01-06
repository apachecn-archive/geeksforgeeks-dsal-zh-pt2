# A 和 B 的最大公约数，使得它们都是同素的

> 原文:[https://www . geeksforgeeks . org/a 和 b 的最大公约数，这样所有的都是互易素数/](https://www.geeksforgeeks.org/maximum-count-of-common-divisors-of-a-and-b-such-that-all-are-co-primes-to-one-another/)

给定两个整数 **A** 和 **B** 。任务是从 **A** 和 **B** 的公约数中找出最大元素的个数，这样所有选中的元素都是同素的。
**举例:**

> **输入:** A = 12，B = 18
> T3】输出:3
> A 和 B 的公约数是 1，2，3 和 6。
> 选择 1、2 和 3。所有对都是彼此的同素
> ，即 gcd(1，2) = gcd(1，3) = gcd(2，3) = 1。
> **输入:** A = 1，B = 3
> **输出:** 1

**进场:**可以观察到 **A** 和 **B** 的所有共同因素一定是其 [gcd](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 的一个因素。并且，为了使该 gcd 的因子相互共质数，该对中的一个元素必须是 **1** 或者两个元素都必须是[质数](https://www.geeksforgeeks.org/prime-numbers/)。所以答案会比 **gcd(A，B)** 的质因数数多 1。**注意**增加 **1** 是因为 **1** 也可以是所选约数的一部分，因为它与其他对的 gcd 永远是 **1** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of common factors
// of a and b such that all the elements
// are co-prime to one another
int maxCommonFactors(int a, int b)
{
    // GCD of a and b
    int gcd = __gcd(a, b);

    // Include 1 initially
    int ans = 1;

    // Find all the prime factors of the gcd
    for (int i = 2; i * i <= gcd; i++) {
        if (gcd % i == 0) {
            ans++;
            while (gcd % i == 0)
                gcd /= i;
        }
    }

    // If gcd is prime
    if (gcd != 1)
        ans++;

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int a = 12, b = 18;

    cout << maxCommonFactors(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to return the count of common factors
// of a and b such that all the elements
// are co-prime to one another
static int maxCommonFactors(int a, int b)
{

    // GCD of a and b
    int __gcd = gcd(a, b);

    // Include 1 initially
    int ans = 1;

    // Find all the prime factors of the gcd
    for (int i = 2; i * i <= __gcd; i++)
    {
        if (__gcd % i == 0)
        {
            ans++;
            while (__gcd % i == 0)
                __gcd /= i;
        }
    }

    // If gcd is prime
    if (__gcd != 1)
        ans++;

    // Return the required answer
    return ans;
}

// Driver code
public static void main (String[] args)
{
    int a = 12, b = 18;

    System.out.println(maxCommonFactors(a, b));
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function to return the count of common factors
# of a and b such that all the elements
# are co-prime to one another
def maxCommonFactors(a, b):

    # GCD of a and b
    gcd = math.gcd(a, b)

    # Include 1 initially
    ans = 1;

    # Find all the prime factors of the gcd
    i = 2
    while (i * i <= gcd):
        if (gcd % i == 0):
            ans += 1
            while (gcd % i == 0):
                gcd = gcd // i
        i += 1   

    # If gcd is prime
    if (gcd != 1):
        ans += 1

    # Return the required answer
    return ans

# Driver code
a = 12
b = 18
print(maxCommonFactors(a, b))

# This code is contributed by
# divyamohan123
```

## C#

```
// C# implementation of the above approach
using System;        

class GFG
{

    static int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function to return the count of common factors
    // of a and b such that all the elements
    // are co-prime to one another
    static int maxCommonFactors(int a, int b)
    {

        // GCD of a and b
        int __gcd = gcd(a, b);

        // Include 1 initially
        int ans = 1;

        // Find all the prime factors of the gcd
        for (int i = 2; i * i <= __gcd; i++)
        {
            if (__gcd % i == 0)
            {
                ans++;
                while (__gcd % i == 0)
                    __gcd /= i;
            }
        }

        // If gcd is prime
        if (__gcd != 1)
            ans++;

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int a = 12, b = 18;

        Console.WriteLine(maxCommonFactors(a, b));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

function GCD(a, b)
{
  if (b == 0)
      return a;
  return GCD(b, a % b);
}

// Function to return the count of common factors
// of a and b such that all the elements
// are co-prime to one another
function maxCommonFactors(a, b)
{
    // GCD of a and b
    let gcd = GCD(a, b);

    // Include 1 initially
    let ans = 1;

    // Find all the prime factors of the gcd
    for (let i = 2; i * i <= gcd; i++) {
        if (gcd % i == 0) {
            ans++;
            while (gcd % i == 0)
                gcd = parseInt(gcd / i);
        }
    }

    // If gcd is prime
    if (gcd != 1)
        ans++;

    // Return the required answer
    return ans;
}

// Driver code
    let a = 12, b = 18;

    document.write(maxCommonFactors(a, b));

</script>
```

**Output:** 

```
3
```