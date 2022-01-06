# 所有数字

> 原文:[https://www.geeksforgeeks.org/droll-numbers/](https://www.geeksforgeeks.org/droll-numbers/)

给定一个数字 **N** ，任务是检查 **N** 是否是一个**德罗尔数字**。如果 **N** 是 **Droll 编号**，则打印**“是”**否则打印**“否”**。

> 大数是这样一个数，即 **N** 的偶数质因数之和等于 **N** 的奇数质因数之和。

**示例:**

> **输入:**N = 6272
> T3】输出:是
> T6】说明:T8】6272 = 2 * 2 * 2 * 2 * 2 * 2 * 7 * 7 是 droll
> 因为 2+2+2+2+2+2+2 = 14 = 7+7。
> 
> **输入:**N = 10
> T3】输出:否

**方法:**思路是求偶素因子和奇素因子的和，检查它们是否相等。如果它们相等，那么 **N** 是一个**德洛尔编号**并为其打印**“是”**，否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check droll numbers
bool isDroll(int n)
{
    if (n == 1)
        return false;

    // To store sum of even prime factors
    int sum_even = 0;

    // To store sum of odd prime factors
    int sum_odd = 0;

    // Add the number of 2s
    // that divide n in sum_even
    while (n % 2 == 0) {
        sum_even += 2;
        n = n / 2;
    }

    // N must be odd at this point.
    // So we can skip
    // one element (Note i = i +2)
    for (int i = 3; i <= sqrt(n); i = i + 2) {

        // While i divides n,
        // print i and divide n
        while (n % i == 0) {
            sum_odd += i;
            n = n / i;
        }
    }

    // This condition is to handle
    // the case when n is a prime
    // number greater than 2
    if (n > 2)
        sum_odd += n;

    // Condition to check droll number
    return sum_even == sum_odd;
}

Driver Code int main()
{
    // Given Number N
    int N = 72;

    // Function Call
    if (isDroll(N))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check droll numbers
static boolean isDroll(int n)
{
    if (n == 1)
        return false;

    // To store sum of even prime factors
    int sum_even = 0;

    // To store sum of odd prime factors
    int sum_odd = 0;

    // Add the number of 2s
    // that divide n in sum_even
    while (n % 2 == 0)
    {
        sum_even += 2;
        n = n / 2;
    }

    // N must be odd at this point.
    // So we can skip
    // one element (Note i = i +2)
    for(int i = 3; i <= Math.sqrt(n);
                   i = i + 2)
    {

       // While i divides n,
       // print i and divide n
       while (n % i == 0)
       {
           sum_odd += i;
           n = n / i;
       }
    }

    // This condition is to handle
    // the case when n is a prime
    // number greater than 2
    if (n > 2)
        sum_odd += n;

    // Condition to check droll number
    return sum_even == sum_odd;
}

// Driver code
public static void main(String[] args)
{

    // Given Number N
    int n = 72;

    // Function Call
    if (isDroll(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math;

# Function to check droll numbers
def isDroll(n):

    if (n == 1):
        return False;

    # To store sum of even prime factors
    sum_even = 0;

    # To store sum of odd prime factors
    sum_odd = 0;

    # Add the number of 2s
    # that divide n in sum_even
    while (n % 2 == 0):
        sum_even += 2;
        n = n // 2;

    # N must be odd at this point.
    # So we can skip
    # one element (Note i = i +2)
    for i in range(3, int(math.sqrt(n)) + 1, 2):

        # While i divides n,
        # print i and divide n
        while (n % i == 0):
            sum_odd += i;
            n = n // i;

    # This condition is to handle
    # the case when n is a prime
    # number greater than 2
    if (n > 2):
        sum_odd += n;

    # Condition to check droll number
    return sum_even == sum_odd;

# Driver Code

# Given Number N
N = 72;

# Function Call
if (isDroll(N)):
    print("Yes");
else:
    print("No");

# This code is contributed by Code_Mech
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check droll numbers
static bool isDroll(int n)
{
    if (n == 1)
        return false;

    // To store sum of even prime factors
    int sum_even = 0;

    // To store sum of odd prime factors
    int sum_odd = 0;

    // Add the number of 2s
    // that divide n in sum_even
    while (n % 2 == 0)
    {
        sum_even += 2;
        n = n / 2;
    }

    // N must be odd at this point.
    // So we can skip
    // one element (Note i = i +2)
    for(int i = 3; i <= Math.Sqrt(n);
                   i = i + 2)
    {

       // While i divides n,
       // print i and divide n
       while (n % i == 0)
       {
           sum_odd += i;
           n = n / i;
       }
    }

    // This condition is to handle
    // the case when n is a prime
    // number greater than 2
    if (n > 2)
        sum_odd += n;

    // Condition to check droll number
    return sum_even == sum_odd;
}

// Driver code
public static void Main()
{

    // Given Number N
    int n = 72;

    // Function Call
    if (isDroll(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check droll numbers
function isDroll(n)
{
    if (n == 1)
        return false;

    // To store sum of even prime factors
    let sum_even = 0;

    // To store sum of odd prime factors
    let sum_odd = 0;

    // Add the number of 2s
    // that divide n in sum_even
    while (n % 2 == 0)
    {
        sum_even += 2;
        n = n / 2;
    }

    // N must be odd at this point.
    // So we can skip
    // one element (Note i = i +2)
    for(let i = 3;
            i <= Math.sqrt(n);
            i = i + 2)
    {

       // While i divides n,
       // print i and divide n
       while (n % i == 0)
       {
           sum_odd += i;
           n = n / i;
       }
    }

    // This condition is to handle
    // the case when n is a prime
    // number greater than 2
    if (n > 2)
        sum_odd += n;

    // Condition to check droll number
    return sum_even == sum_odd;
}

// Driver Code

// Given Number N
let n = 72;

// Function Call
if (isDroll(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by susmitakundugoaldanga

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** *O(sqrt(N))*