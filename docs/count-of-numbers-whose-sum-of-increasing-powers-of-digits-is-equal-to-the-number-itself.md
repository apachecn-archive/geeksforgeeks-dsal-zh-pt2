# 位数增加幂的和等于数本身的数的计数

> 原文:[https://www . geeksforgeeks . org/数字计数-其数字幂的和等于数字本身/](https://www.geeksforgeeks.org/count-of-numbers-whose-sum-of-increasing-powers-of-digits-is-equal-to-the-number-itself/)

给定一个整数 **N** ， 任务是对所有小于或等于 **N** 的整数进行计数，这些整数跟随其位数之和的幂次(从 1 开始，每次增加 1) 等于整数本身，即如果**D<sub>1</sub>D<sub>2</sub>D<sub>3</sub>…D<sub>N</sub>T13】是一个 **N** 数字，那么它就满足给定的属性**(D<sub>1</sub>T19】1+D<sub>2</sub>T23】2+D<sub>3【T25
**举例:**</sub>**** 

> **输入:** N = 100
> **输出:**11
> 0<sup>1</sup>= 0
> 1<sup>1</sup>= 1
> 2<sup>1</sup>= 2
> …
> 9<sup>1</sup>= 9
> 8<sup>1</sup>+9<sup>2</sup>= 8+81 = 89【T23

**方法:**初始化**计数= 0** 并且对于从 **0** 到 **N** 的每个数字，找到增加幂的数字的和，并且如果结果和等于数字本身，则增加**计数**。最后，打印**计数**。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// count of digits of n
int countDigits(int n)
{
    int cnt = 0;
    while (n > 0) {
        cnt++;
        n /= 10;
    }
    return cnt;
}

// Function to return the sum of
// increasing powers of N
int digitPowSum(int n)
{

    // To store the required answer
    int sum = 0;

    // Count of digits in n which will
    // be the power of the last digit
    int pw = countDigits(n);

    // While there are digits left
    while (n > 0) {

        // Get the last digit
        int d = n % 10;

        // Add the last digit after raising
        // it to the required power
        sum += pow(d, pw);

        // Decrement the power for
        // the previous digit
        pw--;

        // Remove the last digit
        n /= 10;
    }
    return sum;
}

// Function to return the count
// of integers which satisfy
// the given conditions
int countNum(int n)
{
    int count = 0;

    for (int i = 0; i <= n; i++) {

        // If current element satisfies
        // the given condition
        if (i == digitPowSum(i)) {
            count++;
        }
    }
    return count;
}

// Driver code
int main()
{
    int n = 200;

    cout << countNum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Function to return the
    // count of digits of n
    static int countDigits(int n)
    {
        int cnt = 0;
        while (n > 0)
        {
            cnt++;
            n /= 10;
        }
        return cnt;
    }

    // Function to return the sum of
    // increasing powers of N
    static int digitPowSum(int n)
    {

        // To store the required answer
        int sum = 0;

        // Count of digits in n which will
        // be the power of the last digit
        int pw = countDigits(n);

        // While there are digits left
        while (n > 0)
        {

            // Get the last digit
            int d = n % 10;

            // Add the last digit after raising
            // it to the required power
            sum += Math.pow(d, pw);

            // Decrement the power for
            // the previous digit
            pw--;

            // Remove the last digit
            n /= 10;
        }
        return sum;
    }

    // Function to return the count
    // of integers which satisfy
    // the given conditions
    static int countNum(int n)
    {
        int count = 0;

        for (int i = 0; i <= n; i++)
        {

            // If current element satisfies
            // the given condition
            if (i == digitPowSum(i))
            {
                count++;
            }
        }
        return count;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 200;

        System.out.println(countNum(n));

    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the
# count of digits of n
def countDigits(n):
    cnt = 0
    while (n > 0):
        cnt += 1
        n //= 10
    return cnt

# Function to return the sum of
# increasing powers of N
def digitPowSum(n):

    # To store the required answer
    sum = 0

    # Count of digits in n which will
    # be the power of the last digit
    pw = countDigits(n)

    # While there are digits left
    while (n > 0):

        # Get the last digit
        d = n % 10

        # Add the last digit after raising
        # it to the required power
        sum += pow(d, pw)

        # Decrement the power for
        # the previous digit
        pw -= 1

        # Remove the last digit
        n //= 10
    return sum

# Function to return the count
# of integers which satisfy
# the given conditions
def countNum(n):

    count = 0

    for i in range(n + 1):

        # If current element satisfies
        # the given condition
        if (i == digitPowSum(i)):
            count += 1

    return count

# Driver code
n = 200

print(countNum(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the
    // count of digits of n
    static int countDigits(int n)
    {
        int cnt = 0;
        while (n > 0)
        {
            cnt++;
            n /= 10;
        }
        return cnt;
    }

    // Function to return the sum of
    // increasing powers of N
    static int digitPowSum(int n)
    {

        // To store the required answer
        int sum = 0;

        // Count of digits in n which will
        // be the power of the last digit
        int pw = countDigits(n);

        // While there are digits left
        while (n > 0)
        {

            // Get the last digit
            int d = n % 10;

            // Add the last digit after raising
            // it to the required power
            sum += (int) Math.Pow(d, pw);

            // Decrement the power for
            // the previous digit
            pw--;

            // Remove the last digit
            n /= 10;
        }
        return sum;
    }

    // Function to return the count
    // of integers which satisfy
    // the given conditions
    static int countNum(int n)
    {
        int count = 0;

        for (int i = 0; i <= n; i++)
        {

            // If current element satisfies
            // the given condition
            if (i == digitPowSum(i))
                count++;
        }
        return count;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 200;

        Console.WriteLine(countNum(n));

    }
}

// This code is contributed by
// sanjeev2552
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the
// count of digits of n
function countDigits(n)
{
    let cnt = 0;
    while (n > 0) {
        cnt++;
        n = Math.floor(n / 10);
    }
    return cnt;
}

// Function to return the sum of
// increasing powers of N
function digitPowSum(n)
{

    // To store the required answer
    let sum = 0;

    // Count of digits in n which will
    // be the power of the last digit
    let pw = countDigits(n);

    // While there are digits left
    while (n > 0) {

        // Get the last digit
        let d = n % 10;

        // Add the last digit after raising
        // it to the required power
        sum += Math.pow(d, pw);

        // Decrement the power for
        // the previous digit
        pw--;

        // Remove the last digit
        n = Math.floor(n / 10);
    }
    return sum;
}

// Function to return the count
// of integers which satisfy
// the given conditions
function countNum(n)
{
    let count = 0;

    for (let i = 0; i <= n; i++) {

        // If current element satisfies
        // the given condition
        if (i == digitPowSum(i)) {
            count++;
        }
    }
    return count;
}

// Driver code

    let n = 200;

    document.write(countNum(n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
13
```