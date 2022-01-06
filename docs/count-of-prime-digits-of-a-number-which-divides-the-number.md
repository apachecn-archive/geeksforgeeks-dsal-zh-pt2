# 数除以数的素数个数

> 原文:[https://www . geeksforgeeks . org/数字除数的素数计数/](https://www.geeksforgeeks.org/count-of-prime-digits-of-a-number-which-divides-the-number/)

给定一个整数 **N** ，任务是统计 N 中的位数，N 是一个质数，也是除数。
**例:**

> **输入:** N = 12
> **输出:** 1
> **解释:**
> 数字的位数= {1，2}
> 但是，只有 2 是除以 N 的素数。
> **输入:** N = 1032
> **输出:** 2
> **解释:**
> 数字的位数= {1，0，3，2 }【T24】

**天真方法:**思路是找出数字的所有位数。对于每个数字，检查是否是质数。如果是，那么检查它是否除数。如果两种情况都为真，则计数增加 1。最终的计数是必需的答案。
**有效方法:**由于只有 2、3、5 和 7 是一位数，因此对于每个数字，检查是否除以该数，如果是 2、3、5 或 7。如果两种情况都为真，则计数增加 1。最终的计数是必需的答案。
以下是本办法的实施:

## C++

```
// C++ program to count number of digits
// which is prime and also divides number

#include <bits/stdc++.h>

using namespace std;

// Function to find the number of
// digits in number which divides the
// number and is also a prime number
int countDigit(int n)
{
    bool prime[10];
    memset(prime, false, sizeof(prime));

    // Only 2, 3, 5 and 7 are prime
    // one-digit number
    prime[2] = prime[3] = true;
    prime[5] = prime[7] = true;

    int temp = n, count = 0;

    // Loop to compute all the digits
    // of the number untill it
    // is not equal to the zero
    while (temp != 0) {

        // Fetching each digit
        // of the number
        int d = temp % 10;

        temp /= 10;

        // Checking if digit is greater than 0
        // and can divides n and is prime too
        if (d > 0 && n % d == 0 && prime[d])
            count++;
    }

    return count;
}

// Driven Code
int main()
{
    int n = 1032;

    cout << countDigit(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of digits
// which is prime and also divides number
class GFG {

    // Function to find the number of
    // digits in number which divides the
    // number and is also a prime number
    static int countDigit(int n)
    {
        boolean prime[]  = new boolean[10];

        for (int i = 0; i < 10; i++)
            prime[i] = false;

        // Only 2, 3, 5 and 7 are prime
        // one-digit number
        prime[2] = prime[3] = true;
        prime[5] = prime[7] = true;

        int temp = n, count = 0;

        // Loop to compute all the digits
        // of the number untill it
        // is not equal to the zero
        while (temp != 0) {

            // Fetching each digit
            // of the number
            int d = temp % 10;

            temp /= 10;

            // Checking if digit is greater than 0
            // and can divides n and is prime too
            if (d > 0 && n % d == 0 && prime[d] == true)
                count++;
        }

        return count;
    }

    // Driven Code
    public static void main (String[] args)
    {
        int n = 1032;

        System.out.println(countDigit(n)) ;
    }
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python program to count number of digits
# which is prime and also divides number

# Function to find the number of
# digits in number which divides the
# number and is also a prime number
def countDigit(n):
    prime = [False]*10

    # Only 2, 3, 5 and 7 are prime
    # one-digit number
    prime[2] = True
    prime[3] = True;
    prime[5] = True
    prime[7] = True;

    temp = n
    count = 0;

    # Loop to compute all the digits
    # of the number untill it
    # is not equal to the zero
    while (temp != 0):

        # Fetching each digit
        # of the number
        d = temp % 10;

        temp //= 10;

        # Checking if digit is greater than 0
        # and can divides n and is prime too
        if (d > 0 and n % d == 0 and prime[d]):
            count += 1

    return count

# Driver Code
n = 1032

print(countDigit(n))

# This code is contributed by ANKITKUMAR34
```

## C#

```
// C# program to count number of digits
// which is prime and also divides number
using System;

class GFG {

    // Function to find the number of
    // digits in number which divides the
    // number and is also a prime number
    static int countDigit(int n)
    {
        bool []prime  = new bool[10];

        for (int i = 0; i < 10; i++)
            prime[i] = false;

        // Only 2, 3, 5 and 7 are prime
        // one-digit number
        prime[2] = prime[3] = true;
        prime[5] = prime[7] = true;

        int temp = n, count = 0;

        // Loop to compute all the digits
        // of the number untill it
        // is not equal to the zero
        while (temp != 0) {

            // Fetching each digit
            // of the number
            int d = temp % 10;

            temp /= 10;

            // Checking if digit is greater than 0
            // and can divides n and is prime too
            if (d > 0 && n % d == 0 && prime[d] == true)
                count++;
        }

        return count;
    }

    // Driven Code
    public static void Main (string[] args)
    {
        int n = 1032;

        Console.WriteLine(countDigit(n)) ;
    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// Javascript program to count number of digits
// which is prime and also divides number

// Function to find the number of
// digits in number which divides the
// number and is also a prime number
function countDigit(n)
{
    var prime = Array(10).fill(false);

    // Only 2, 3, 5 and 7 are prime
    // one-digit number
    prime[2] = prime[3] = true;
    prime[5] = prime[7] = true;

    var temp = n, count = 0;

    // Loop to compute all the digits
    // of the number untill it
    // is not equal to the zero
    while (temp != 0) {

        // Fetching each digit
        // of the number
        var d = temp % 10;

        temp = parseInt(temp/10);

        // Checking if digit is greater than 0
        // and can divides n and is prime too
        if (d > 0 && n % d == 0 && prime[d])
            count++;
    }

    return count;
}

// Driven Code
    n = 1032;

    document.write(countDigit(n));

</script>
```

**Output:** 

```
2
```

时间复杂度:O(log <sub>10</sub> n)

辅助空间:0(质数)