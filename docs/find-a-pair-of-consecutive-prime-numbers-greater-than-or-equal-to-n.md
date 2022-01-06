# 大于等于给定数的连续素数。

> 原文:[https://www . geesforgeks . org/find-一对大于或等于 n 的连续素数/](https://www.geeksforgeeks.org/find-a-pair-of-consecutive-prime-numbers-greater-than-or-equal-to-n/)

### 问题:

给定一个数 n，任务是找到两个连续的素数，使得这两个素数的乘积大于或等于 n。

### **示例:**

> **输入:** 14
> **输出:** 3 5
> **说明:** 3 和 5 是乘积大于 14 的连续素数。

### 方法:

假设 n 在 10^8 到 10^10.的范围内我们不能用筛子找出素数，因为范围是 upto10^10.

我们可以通过以下方法找到所需的连续素数。

*   找到小于 sqrt(n)的最大素数，并将其存储在临时变量中(第一个)。
*   找到大于 sqrt(n)的最小素数，并将其存储在临时变量(第二个)中。
*   如果第一个和第二个的乘积大于或等于 n，则打印它。
*   否则找一个大于秒的质数，和秒一起打印出来。

### 代码:

## C++

```
//C++ program for the above approach
#include <bits/stdc++.h>
#define endl "\n"
#define ll long long
using namespace std;

//Function to check prime.
bool is_prime(ll n)
{
    if (n == 1)
    {
        return false;
    }
    for (ll i = 2; i <= sqrt(n); i++)
    {
        if (n % i == 0)
        {
          // It means it is not
          // a prime
            return false;
        }
    }
  // No factor other than 1
  // therefore prime number
    return true;
}

//Function to find out the required
//consecutive primes.
void consecutive_primes(int n)
{
    ll first = -1, second = -1;

    //Finding first prime just
    // less than sqrt(n).
    for (ll i = sqrt(n); i >= 2; i--)
    {
        if (is_prime(i))
        {
            first = i;
            break;
        }
    }
    // Finding prime just greater
    //than sqrt(n).
    for (ll i = sqrt(n) + 1;
         i <= n / 2; i++)
    {
        if (is_prime(i))
        {
            second = i;
            break;
        }
    }
    // Product of both prime is greater
    // than n then print it
    if (first * second >= n)
    {
        cout << first << " "
          <<second << endl;
    }
    // Finding prime greater than second
    else
    {
        for (ll i = second + 1;
             i <= n; i++)
        {
            if (is_prime(i))
            {
                cout << second << " "
                  << i << endl;
                return;
            }
        }
    }
}
//Driver Program
int main()
{
    ll n = 14;
    consecutive_primes(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check prime.
static boolean is_prime(long n)
{
    if (n == 1)
    {
        return false;
    }
    for(long i = 2; i <= (long)Math.sqrt(n); i++)
    {
        if (n % i == 0)
        {

            // It means it is not
            // a prime
            return false;
        }
    }

    // No factor other than 1
    // therefore prime number
    return true;
}

// Function to find out the required
// consecutive primes.
static void consecutive_primes(long n)
{
    long first = -1, second = -1;

    // Finding first prime just
    // less than sqrt(n).
    for(long i = (long)Math.sqrt(n); i >= 2; i--)
    {
        if (is_prime(i))
        {
            first = i;
            break;
        }
    }

    // Finding prime just greater
    // than sqrt(n).
    for(long i = (long)Math.sqrt(n) + 1;
             i <= n / 2; i++)
    {
        if (is_prime(i))
        {
            second = i;
            break;
        }
    }

    // Product of both prime is greater
    // than n then print it
    if (first * second >= n)
    {
        System.out.println(first + " " + second);
    }

    // Finding prime greater than second
    else
    {
        for(long i = second + 1; i <= n; i++)
        {
            if (is_prime(i))
            {
                System.out.println(second + " " + i);
                return;
            }
        }
    }
}

// Driver code
public static void main(String args[])
{
    long n = 14;
    consecutive_primes(n);
}
}

// This code is contributed by splevel62
```

## 蟒蛇 3

```
#python 3 program for the above approach
#Function to check prime.
from math import sqrt

def is_prime(n):
    if (n == 1):
        return False
    for i in range(2,int(sqrt(n))+1,1):
        if (n % i == 0):
            # It means it is not
            # a prime
            return False
  # No factor other than 1
  # therefore prime number
    return True

# Function to find out the required
# consecutive primes.
def consecutive_primes(n):
    first = -1
    second = -1

    # Finding first prime just
    # less than sqrt(n).
    i = int(sqrt(n))
    while(i >= 2):
        if (is_prime(i)):
            first = i
            break
        i -= 1

    # Finding prime just greater
    #than sqrt(n).
    for i in range(int(sqrt(n)) + 1,n//2 +1 ,1):
        if (is_prime(i)):
            second = i
            break

    # Product of both prime is greater
    # than n then print it
    if (first * second >= n):
        print(first,second)

    # Finding prime greater than second
    else:
        for i in range(second + 1,n+1,1):
            if (is_prime(i)):
                print(second,i)
                return

# Driver Program
if __name__ == '__main__':
    n = 14
    consecutive_primes(n)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to check prime.
    static bool is_prime(long n)
    {
        if (n == 1) {
            return false;
        }
        for (long i = 2; i <= (long)Math.Sqrt(n); i++) {
            if (n % i == 0)
            {

                // It means it is not
                // a prime
                return false;
            }
        }

        // No factor other than 1
        // therefore prime number
        return true;
    }

    // Function to find out the required
    // consecutive primes.
    static void consecutive_primes(long n)
    {
        long first = -1, second = -1;

        // Finding first prime just
        // less than sqrt(n).
        for (long i = (long)Math.Sqrt(n); i >= 2; i--) {
            if (is_prime(i)) {
                first = i;
                break;
            }
        }
        // Finding prime just greater
        // than sqrt(n).
        for (long i = (long)Math.Sqrt(n) + 1; i <= n / 2;
             i++) {
            if (is_prime(i)) {
                second = i;
                break;
            }
        }
        // Product of both prime is greater
        // than n then print it
        if (first * second >= n) {
            Console.WriteLine(first + " " + second);
        }

        // Finding prime greater than second
        else {
            for (long i = second + 1; i <= n; i++) {
                if (is_prime(i)) {
                    Console.WriteLine(second + " " + i);
                    return;
                }
            }
        }
    }

    // Driver Program
    public static void Main()
    {
        long n = 14;
        consecutive_primes(n);
    }
}

// This code is contributed  by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check prime.
function is_prime(n)
{
    if (n == 1)
    {
        return false;
    }
    for(var i = 2; i <= parseInt(Math.sqrt(n)); i++)
    {
        if (n % i == 0)
        {

            // It means it is not
            // a prime
            return false;
        }
    }

    // No factor other than 1
    // therefore prime number
    return true;
}

// Function to find out the required
// consecutive primes.
function consecutive_primes(n)
{
    var first = -1, second = -1;

    // Finding first prime just
    // less than sqrt(n).
    for(var i = parseInt(Math.sqrt(n)); i >= 2; i--)
    {
        if (is_prime(i))
        {
            first = i;
            break;
        }
    }

    // Finding prime just greater
    // than sqrt(n).
    for(var i = parseInt(Math.sqrt(n)) + 1;
             i <= parseInt(n / 2); i++)
    {
        if (is_prime(i))
        {
            second = i;
            break;
        }
    }

    // Product of both prime is greater
    // than n then print it
    if (first * second >= n)
    {
        document.write(first + " " + second);
    }

    // Finding prime greater than second
    else
    {
        for(var i = second + 1; i <= n; i++)
        {
            if (is_prime(i))
            {
                document.write(second + " " + i);
                return;
            }
        }
    }
}

// Driver code
var n = 14;
consecutive_primes(n);

// This code is contributed by 29AjayKumar

</script>
```

**Output**

```
3 5
```

**时间复杂度:O(sqrt(n))**