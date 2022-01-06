# 一个数字中质数的计数

> 原文:[https://www . geeksforgeeks . org/素数位数/](https://www.geeksforgeeks.org/count-of-prime-digits-in-a-number/)

给定一个整数 **N** ，任务是统计 **N** 中[素数](https://www.geeksforgeeks.org/prime-numbers/)位数。
**举例:**

> **输入:** N = 12
> **输出:** 1
> **说明:**
> 数字的位数–{ 1，2}
> 但是，只有 2 是质数。
> **输入:** N = 1032
> **输出:** 2
> **解释:**
> 数字的位数–{ 1，0，3，2}
> 3 和 2 是质数

**方法:**思路是遍历数字的所有数字，检查该数字是否为[素数](https://www.geeksforgeeks.org/prime-numbers/)。由于在**【0，9】**范围内只有四个可能的质数，并且每个数字肯定都在这个范围内，我们只需要检查与集合 **{2，3，5，7}** 中的任一元素相等的数字个数。
以下是本办法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to count the number of
// prime digits in a number

#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// prime digits in a number
int countDigit(int n)
{
    int temp = n, count = 0;

    // Loop to compute all the digits
    // of the number
    while (temp != 0) {

        // Finding every digit of the
        // given number
        int d = temp % 10;

        temp /= 10;

        // Checking if digit is prime or not
        // Only 2, 3, 5 and 7 are prime
        // one-digit number
        if (d == 2 || d == 3
            || d == 5 || d == 7)
            count++;
    }

    return count;
}

// Driver code
int main()
{
    int n = 1234567890;

    cout << countDigit(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number of
// prime digits in a number
class GFG {

    // Function to find the count of
    // prime digits in a number
    static int countDigit(int n)
    {
        int temp = n, count = 0;

        // Loop to compute all the digits
        // of the number
        while (temp != 0) {

            // Finding every digit of the
            // given number
            int d = temp % 10;

            temp /= 10;

            // Checking if digit is prime or not
            // Only 2, 3, 5 and 7 are prime
            // one-digit number
            if (d == 2 || d == 3
                || d == 5 || d == 7)
                count++;
        }

        return count;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 1234567890;

        System.out.println(countDigit(n)) ;

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to count the number of
# prime digits in a number

# Function to find the count of
# prime digits in a number
def countDigit(n):
    temp = n
    count = 0

    # Loop to compute all the digits
    # of the number
    while (temp != 0):

        # Finding every digit of the
        # given number
        d = temp % 10

        temp //= 10

        # Checking if digit is prime or not
        # Only 2, 3, 5 and 7 are prime
        # one-digit number
        if (d == 2 or d == 3 or d == 5 or d == 7):
            count += 1

    return count

# Driver code
if __name__ == '__main__':
    n = 1234567890

    print(countDigit(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to count the number of
// prime digits in a number
using System;

class GFG {

    // Function to find the count of
    // prime digits in a number
    static int countDigit(int n)
    {
        int temp = n, count = 0;

        // Loop to compute all the digits
        // of the number
        while (temp != 0) {

            // Finding every digit of the
            // given number
            int d = temp % 10;

            temp /= 10;

            // Checking if digit is prime or not
            // Only 2, 3, 5 and 7 are prime
            // one-digit number
            if (d == 2 || d == 3
                || d == 5 || d == 7)
                count++;
        }

        return count;
    }

    // Driver code
    public static void Main (string[] args)
    {
        int n = 1234567890;

        Console.WriteLine(countDigit(n)) ;
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript program to count the number of
// prime digits in a number

// Function to find the count of
// prime digits in a number
function countDigit(n)
{
    let temp = n, count = 0;

    // Loop to compute all the digits
    // of the number
    while (temp != 0) {

        // Finding every digit of the
        // given number
        let d = temp % 10;

        temp = Math.floor(temp / 10);

        // Checking if digit is prime or not
        // Only 2, 3, 5 and 7 are prime
        // one-digit number
        if (d == 2 || d == 3
            || d == 5 || d == 7)
            count++;
    }

    return count;
}

// Driver code

let n = 1234567890;

document.write(countDigit(n) + "<br>");

// This code is contributed by gfgking

</script>
```

**Output:** 

```
4
```

**时间复杂度:** *O(log <sub>10</sub> N)* ，其中 N 为数字的长度。

**辅助空间:** O(1)