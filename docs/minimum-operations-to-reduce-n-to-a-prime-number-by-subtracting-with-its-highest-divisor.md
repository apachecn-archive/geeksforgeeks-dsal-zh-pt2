# 用最大除数

进行减法运算，将 N 减为素数的最小运算

> 原文:[https://www . geeksforgeeks . org/用最大除数减法将 n 减为素数的最小运算/](https://www.geeksforgeeks.org/minimum-operations-to-reduce-n-to-a-prime-number-by-subtracting-with-its-highest-divisor/)

给定正整数 **N** 。在一次操作中，用除了 **N** 和 **1** 以外的最高除数减去 **N** 。任务是找到将 **N** 精确化为[素数](https://www.geeksforgeeks.org/prime-numbers/)所需的最小运算。

**示例:**

> **输入:** N = 38
> **输出:** 1
> **说明:**38 的最高除数是 19，所以减去它(38–19)= 19。19 是一个素数。
> 所以，需要的操作次数= 1。
> 
> **输入:**N = 69
> T3】输出: 2

**方法:**这个问题可以用简单的数学概念来解决。按照以下步骤解决给定的问题。

*   首先检查 **N** 是否已经是质数。
    *   如果 **N** 已经是质数，返回 **0** 。
    *   否则，初始化一个变量，比如**计数= 0** 来存储所需的操作数。
    *   初始化一个变量，比如说 i=2，运行一个 while 循环直到 N！=i
        *   边循环边运行，并在每次迭代中用其最大除数减去 N 的当前值。
        *   计算步数并通过 **1** 增加计数。
    *   返回**计数**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function check whether a number
// is prime or not
bool isPrime(int n)
{
    // Corner case
    if (n <= 1)
        return false;

    // Check from 2 to square root of n
    for (int i = 2; i <= sqrt(n); i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function to minimum operations required
// to reduce the number to a prime number
int minOperation(int N)
{
    // Because 1 cannot be converted to prime
    if (N == 1)
        return -1;

    // If given number is already prime
    // return 0
    if (isPrime(N) == true) {
        return 0;
    }

    // If number is not prime
    else {
        // Variable for total count
        int count = 0;
        int i = 2;

        // If number is not equal to i
        while (N != i) {
            // If N is completely divisible by i
            while (N % i == 0) {
                // Temporary variable to store
                // current number
                int temp = N;

                // Update the number by decrementing
                // with highest divisor
                N -= (temp / i);

                // Increment count by 1
                count++;
                if (isPrime(N))
                    return count;
            }
            i++;
        }

        // Return the count
        return count;
    }
}

// Driver Code
int main()
{
    int N = 38;

    cout << minOperation(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG {
    // Function check whether a number
    // is prime or not
    public static boolean isPrime(int n) {
        // Corner case
        if (n <= 1)
            return false;

        // Check from 2 to square root of n
        for (int i = 2; i <= Math.sqrt(n); i++)
            if (n % i == 0)
                return false;

        return true;
    }

    // Function to minimum operations required
    // to reduce the number to a prime number
    public static int minOperation(int N) {
        // Because 1 cannot be converted to prime
        if (N == 1)
            return -1;

        // If given number is already prime
        // return 0
        if (isPrime(N) == true) {
            return 0;
        }

        // If number is not prime
        else {
            // Variable for total count
            int count = 0;
            int i = 2;

            // If number is not equal to i
            while (N != i) {
                // If N is completely divisible by i
                while (N % i == 0) {
                    // Temporary variable to store
                    // current number
                    int temp = N;

                    // Update the number by decrementing
                    // with highest divisor
                    N -= (temp / i);

                    // Increment count by 1
                    count++;
                    if (isPrime(N))
                        return count;
                }
                i++;
            }

            // Return the count
            return count;
        }
    }

    // Driver Code
    public static void main(String args[]) {
        int N = 38;

        System.out.println(minOperation(N));
    }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# python program for the above approach
import math

# Function check whether a number
# is prime or not
def isPrime(n):

    # Corner case
    if (n <= 1):
        return False

    # Check from 2 to square root of n
    for i in range(2, int(math.sqrt(n)) + 1):
        if (n % i == 0):
            return False

    return True

# Function to minimum operations required
# to reduce the number to a prime number
def minOperation(N):

    # Because 1 cannot be converted to prime
    if (N == 1):
        return -1

    # If given number is already prime
    # return 0
    if (isPrime(N) == True):
        return 0

    # If number is not prime
    else:
        # Variable for total count
        count = 0
        i = 2

        # If number is not equal to i
        while (N != i):

            # If N is completely divisible by i
            while (N % i == 0):

                # Temporary variable to store
                # current number
                temp = N

                # Update the number by decrementing
                # with highest divisor
                N -= (temp // i)

                # Increment count by 1
                count += 1
                if (isPrime(N)):
                    return count
            i += 1

        # Return the count
        return count

# Driver Code
if __name__ == "__main__":
    N = 38
    print(minOperation(N))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Function check whether a number
    // is prime or not
    public static bool isPrime(int n)
    {

        // Corner case
        if (n <= 1)
            return false;

        // Check from 2 to square root of n
        for (int i = 2; i <= Math.Sqrt(n); i++)
            if (n % i == 0)
                return false;

        return true;
    }

    // Function to minimum operations required
    // to reduce the number to a prime number
    public static int minOperation(int N) {
        // Because 1 cannot be converted to prime
        if (N == 1)
            return -1;

        // If given number is already prime
        // return 0
        if (isPrime(N) == true) {
            return 0;
        }

        // If number is not prime
        else {
            // Variable for total count
            int count = 0;
            int i = 2;

            // If number is not equal to i
            while (N != i) {

                // If N is completely divisible by i
                while (N % i == 0) {

                    // Temporary variable to store
                    // current number
                    int temp = N;

                    // Update the number by decrementing
                    // with highest divisor
                    N -= (temp / i);

                    // Increment count by 1
                    count++;

                    if (isPrime(N))
                        return count;
                }
                i++;
            }

            // Return the count
            return count;
        }
    }

    // Driver Code
    public static void Main(string []args) {
        int N = 38;

        Console.WriteLine(minOperation(N));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function check whether a number
    // is prime or not
    const isPrime = (n) => {
        // Corner case
        if (n <= 1)
            return false;

        // Check from 2 to square root of n
        for (let i = 2; i <= parseInt(Math.sqrt(n)); i++)
            if (n % i == 0)
                return false;

        return true;
    }

    // Function to minimum operations required
    // to reduce the number to a prime number
    const minOperation = (N) => {

        // Because 1 cannot be converted to prime
        if (N == 1)
            return -1;

        // If given number is already prime
        // return 0
        if (isPrime(N) == true) {
            return 0;
        }

        // If number is not prime
        else
        {

            // Variable for total count
            let count = 0;
            let i = 2;

            // If number is not equal to i
            while (N != i)
            {

                // If N is completely divisible by i
                while (N % i == 0)
                {

                    // Temporary variable to store
                    // current number
                    let temp = N;

                    // Update the number by decrementing
                    // with highest divisor
                    N -= parseInt(temp / i);

                    // Increment count by 1
                    count++;
                    if (isPrime(N))
                        return count;
                }
                i++;
            }

            // Return the count
            return count;
        }
    }

    // Driver Code
    let N = 38;
    document.write(minOperation(N));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
1
```

**时间复杂度:** O(sqrtN)

**辅助空间:** O(1)