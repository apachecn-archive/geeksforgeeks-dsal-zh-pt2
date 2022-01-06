# 通过重复除以任何小于 M 的质因数，使两个值相等所需的步骤最少

> 原文:[https://www . geeksforgeeks . org/最小化所需步骤通过重复除以小于 m 的任何质因数来使两个值相等/](https://www.geeksforgeeks.org/minimize-steps-required-to-make-two-values-equal-by-repeated-division-by-any-of-their-prime-factor-which-is-less-than-m/)

给定三个正整数 **M** 、 **X** 和 **Y** ，任务是找到使 **X** 和 **Y** 相等所需的最小操作数，使得在每个操作中，将 **X** 或 **Y** 除以其一个[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)小于 **M** 。如果无法使 **X** 和 **Y** 相等，则打印**-1”**。

**示例:**

> **输入:** X = 20，Y =16，M = 10
> **输出:** 3
> **解释:**
> 对 X 和 Y 执行如下所示的操作:
> X:20->4:20/5 = 4
> Y:16->8:16/2 = 8，8 - > 4 : 8/2 = 4
> 因此，需要的总步数
> 
> **输入:** X =160，Y = 180，M = 10
> T3】输出: 5

**方法:**解决给定问题的思路是基于这样的观察，即 **X** 和 **Y** 相等的值是 **X** 和 **Y** 的[**GCD**T9】。按照以下步骤解决问题:](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)

*   使用厄拉多塞的[筛预先计算数字的所有](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[质因数至 10<sup>6</sup>T3，并将其存储在数组中。](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/)
*   计算数字 **X** 和**Y**T5 的 [GCD，并将它们的值存储在一个变量中，比如 **GCD** 。](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)
*   现在[统计 **X / GCD** 和 **Y / GCD** 中质因数](https://www.geeksforgeeks.org/maximum-number-unique-prime-factors/)的个数。如果任何质因数的值大于 **M** ，则不可能使 **X** 和 **Y** 相等。因此，打印**-1”**。
*   否则，打印 **X / GCD** 和 **Y / GCD** 中素数之和作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the prime factor of numbers
int primes[1000006];

// Function to find GCD of a and b
int gcd(int a, int b)
{

    // Base Case
    if (b == 0)
        return a;

    // Otherwise, calculate GCD
    else
        return gcd(b, a % b);
}

// Function to precompute the
// prime numbers till 1000000
void preprocess()
{

    // Initialize all the positions
    // with their respective values
    for(int i = 1; i <= 1000000; i++)
        primes[i] = i;

    // Iterate over the range [2, sqrt(10^6)]
    for(int i = 2; i * i <= 1000000; i++)
    {

        // If i is prime number
        if (primes[i] == i)
        {

            // Mark it as the factor
            for(int j = 2 * i; j <= 1000000; j += i)
            {
                if (primes[j] == j)
                    primes[j] = i;
            }
        }
    }
}

// Utility function to count the number
// of steps to make X and Y equal
int Steps(int x, int m)
{

    // Initialise steps
    int steps = 0;

    bool flag = false;

    // Iterate x is at most 1
    while (x > 1)
    {
        if (primes[x] > m)
        {
            flag = true;
            break;
        }

        // Divide with the
        // smallest prime factor
        x /= primes[x];

        steps++;
    }

    // If X and Y can't be
    // made equal
    if (flag)
        return -1;

    // Return steps
    return steps;
}

// Function to find the minimum number of
// steps required to make X and Y equal
int minimumSteps(int x, int y, int m)
{

    // Generate all the prime factors
    preprocess();

    // Calculate GCD of x and y
    int g = gcd(x, y);

    // Divide the numbers by their gcd
    x = x / g;
    y = y / g;

    int x_steps = Steps(x, m);
    int y_steps = Steps(y, m);

    // If not possible, then return -1;
    if (x_steps == -1 || y_steps == -1)
        return -1;

    // Return the resultant number of steps
    return x_steps + y_steps;
}

// Driver Code
int main()
{
    int X = 160;
    int Y = 180;
    int M = 10;

    cout << (minimumSteps(X, Y, M));
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class GFG {

    // Stores the prime factor of numbers
    static int primes[] = new int[1000006];

    // Function to find GCD of a and b
    static int gcd(int a, int b)
    {
        // Base Case
        if (b == 0)
            return a;

        // Otherwise, calculate GCD
        else
            return gcd(b, a % b);
    }

    // Function to precompute the
    // prime numbers till 1000000
    static void preprocess()
    {
        // Initialize all the positions
        // with their respective values
        for (int i = 1; i <= 1000000; i++)
            primes[i] = i;

        // Iterate over the range [2, sqrt(10^6)]
        for (int i = 2; i * i <= 1000000; i++) {

            // If i is prime number
            if (primes[i] == i) {

                // Mark it as the factor
                for (int j = 2 * i;
                     j <= 1000000; j += i) {

                    if (primes[j] == j)
                        primes[j] = i;
                }
            }
        }
    }

    // Utility function to count the number
    // of steps to make X and Y equal
    static int Steps(int x, int m)
    {
        // Initialise steps
        int steps = 0;

        boolean flag = false;

        // Iterate x is at most 1
        while (x > 1) {
            if (primes[x] > m) {
                flag = true;
                break;
            }

            // Divide with the
            // smallest prime factor
            x /= primes[x];

            steps++;
        }

        // If X and Y can't be
        // made equal
        if (flag)
            return -1;

        // Return steps
        return steps;
    }

    // Function to find the minimum number of
    // steps required to make X and Y equal
    static int minimumSteps(int x, int y, int m)
    {
        // Generate all the prime factors
        preprocess();

        // Calculate GCD of x and y
        int g = gcd(x, y);

        // Divide the numbers by their gcd
        x = x / g;
        y = y / g;

        int x_steps = Steps(x, m);
        int y_steps = Steps(y, m);

        // If not possible, then return -1;
        if (x_steps == -1 || y_steps == -1)
            return -1;

        // Return the resultant number of steps
        return x_steps + y_steps;
    }

    // Driver Code
    public static void main(String args[])
    {
        int X = 160;
        int Y = 180;
        int M = 10;

        System.out.println(
            minimumSteps(X, Y, M));
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Stores the prime factor of numbers
primes = [0] * (1000006)

# Function to find GCD of a and b
def gcd(a, b) :

    # Base Case
    if (b == 0) :
        return a

    # Otherwise, calculate GCD
    else :
        return gcd(b, a % b)

# Function to precompute the
# prime numbers till 1000000
def preprocess() :

    # Initialize all the positions
    # with their respective values
    for i in range(1, 1000001):
        primes[i] = i

    # Iterate over the range [2, sqrt(10^6)]
    i = 2
    while(i * i <= 1000000)  :

        # If i is prime number
        if (primes[i] == i) :

            # Mark it as the factor
            for j in range(2 * i, 1000001, i):
                if (primes[j] == j) :
                    primes[j] = i     
        i += 1

# Utility function to count the number
# of steps to make X and Y equal
def Steps(x, m) :

    # Initialise steps
    steps = 0

    flag = False

    # Iterate x is at most 1
    while (x > 1) :

        if (primes[x] > m) :
            flag = True
            break

        # Divide with the
        # smallest prime factor
        x //= primes[x]

        steps += 1

    # If X and Y can't be
    # made equal
    if (flag != 0) :
        return -1

    # Return steps
    return steps

# Function to find the minimum number of
# steps required to make X and Y equal
def minimumSteps(x, y, m) :

    # Generate all the prime factors
    preprocess()

    # Calculate GCD of x and y
    g = gcd(x, y)

    # Divide the numbers by their gcd
    x = x // g
    y = y // g

    x_steps = Steps(x, m)
    y_steps = Steps(y, m)

    # If not possible, then return -1
    if (x_steps == -1 or y_steps == -1) :
        return -1

    # Return the resultant number of steps
    return x_steps + y_steps

# Driver Code
X = 160
Y = 180
M = 10

print(minimumSteps(X, Y, M))

# This code is contributed by souravghosh0416.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Stores the prime factor of numbers
static int[] primes = new int[1000006];

// Function to find GCD of a and b
static int gcd(int a, int b)
{

    // Base Case
    if (b == 0)
        return a;

    // Otherwise, calculate GCD
    else
        return gcd(b, a % b);
}

// Function to precompute the
// prime numbers till 1000000
static void preprocess()
{

    // Initialize all the positions
    // with their respective values
    for(int i = 1; i <= 1000000; i++)
        primes[i] = i;

    // Iterate over the range [2, sqrt(10^6)]
    for(int i = 2; i * i <= 1000000; i++)
    {

        // If i is prime number
        if (primes[i] == i)
        {

            // Mark it as the factor
            for(int j = 2 * i;
                    j <= 1000000; j += i)
            {
                if (primes[j] == j)
                    primes[j] = i;
            }
        }
    }
}

// Utility function to count the number
// of steps to make X and Y equal
static int Steps(int x, int m)
{

    // Initialise steps
    int steps = 0;

    bool flag = false;

    // Iterate x is at most 1
    while (x > 1)
    {
        if (primes[x] > m)
        {
            flag = true;
            break;
        }

        // Divide with the
        // smallest prime factor
        x /= primes[x];

        steps++;
    }

    // If X and Y can't be
    // made equal
    if (flag)
        return -1;

    // Return steps
    return steps;
}

// Function to find the minimum number of
// steps required to make X and Y equal
static int minimumSteps(int x, int y, int m)
{

    // Generate all the prime factors
    preprocess();

    // Calculate GCD of x and y
    int g = gcd(x, y);

    // Divide the numbers by their gcd
    x = x / g;
    y = y / g;

    int x_steps = Steps(x, m);
    int y_steps = Steps(y, m);

    // If not possible, then return -1;
    if (x_steps == -1 || y_steps == -1)
        return -1;

    // Return the resultant number of steps
    return x_steps + y_steps;
}

// Driver code
static void Main()
{
    int X = 160;
    int Y = 180;
    int M = 10;

    Console.Write(minimumSteps(X, Y, M));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Stores the prime factor of numbers
    var primes = Array(1000006).fill(0);

    // Function to find GCD of a and b
    function gcd(a , b) {
        // Base Case
        if (b == 0)
            return a;

        // Otherwise, calculate GCD
        else
            return gcd(b, a % b);
    }

    // Function to precompute the
    // prime numbers till 1000000
    function preprocess() {
        // Initialize all the positions
        // with their respective values
        for (i = 1; i <= 1000000; i++)
            primes[i] = i;

        // Iterate over the range [2, sqrt(10^6)]
        for (i = 2; i * i <= 1000000; i++) {

            // If i is prime number
            if (primes[i] == i) {

                // Mark it as the factor
                for (j = 2 * i; j <= 1000000; j += i) {

                    if (primes[j] == j)
                        primes[j] = i;
                }
            }
        }
    }

    // Utility function to count the number
    // of steps to make X and Y equal
    function Steps(x , m) {
        // Initialise steps
        var steps = 0;

        var flag = false;

        // Iterate x is at most 1
        while (x > 1) {
            if (primes[x] > m) {
                flag = true;
                break;
            }

            // Divide with the
            // smallest prime factor
            x /= primes[x];

            steps++;
        }

        // If X and Y can't be
        // made equal
        if (flag)
            return -1;

        // Return steps
        return steps;
    }

    // Function to find the minimum number of
    // steps required to make X and Y equal
    function minimumSteps(x , y , m) {
        // Generate all the prime factors
        preprocess();

        // Calculate GCD of x and y
        var g = gcd(x, y);

        // Divide the numbers by their gcd
        x = x / g;
        y = y / g;

        var x_steps = Steps(x, m);
        var y_steps = Steps(y, m);

        // If not possible, then return -1;
        if (x_steps == -1 || y_steps == -1)
            return -1;

        // Return the resultant number of steps
        return x_steps + y_steps;
    }

    // Driver Code

        var X = 160;
        var Y = 180;
        var M = 10;

        document.write(minimumSteps(X, Y, M));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(N)*