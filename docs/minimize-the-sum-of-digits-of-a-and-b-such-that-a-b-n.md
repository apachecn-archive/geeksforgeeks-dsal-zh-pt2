# 最小化 A 和 B 的位数之和，使得 A + B = N

> 原文:[https://www . geeksforgeeks . org/最小化 a 和 b 的数字总和，以便 a-b-n/](https://www.geeksforgeeks.org/minimize-the-sum-of-digits-of-a-and-b-such-that-a-b-n/)

给定一个整数 **N** ，任务是求两个正整数 **A** 和 **B** ，使得 **A + B = N** 且 **A** 和 **B** 的位数之和最小。打印 **A** 和 **B** 的位数之和。
**举例:**

> **输入:** N = 16
> **输出:** 7
> (10 + 6) = 16 和(1 + 0 + 6) = 7
> 是最小可能。
> **输入:** N = 1000
> **输出:** 10
> (900 + 100) = 1000

**趋近:**如果 **N** 是 **10** 的幂，则答案为 **10** ，否则答案为 **N** 的位数之和。很明显，答案不能小于 **N** 的位数总和，因为每当产生进位时，位数总和就会减少。而且当 **N** 是 **10** 的幂时，显然答案不可能是 **1** ，所以答案会是 **10** 。因为 **A** 或 **B** 不能是 **0** ，因为两者都必须是正数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// possible sum of digits of A
// and B such that A + B = n
int minSum(int n)
{
    // Find the sum of digits of n
    int sum = 0;
    while (n > 0) {
        sum += (n % 10);
        n /= 10;
    }

    // If num is a power of 10
    if (sum == 1)
        return 10;

    return sum;
}

// Driver code
int main()
{
    int n = 1884;

    cout << minSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

// Function to return the minimum
// possible sum of digits of A
// and B such that A + B = n
static int minSum(int n)
{
    // Find the sum of digits of n
    int sum = 0;
    while (n > 0)
    {
        sum += (n % 10);
        n /= 10;
    }

    // If num is a power of 10
    if (sum == 1)
        return 10;

    return sum;
}

// Driver code
public static void main(String[] args)
{
    int n = 1884;

    System.out.print(minSum(n));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the minimum
# possible sum of digits of A
# and B such that A + B = n
def minSum(n) :

    # Find the sum of digits of n
    sum = 0;
    while (n > 0) :
        sum += (n % 10);
        n //= 10;

    # If num is a power of 10
    if (sum == 1) :
        return 10;

    return sum;

# Driver code
if __name__ == "__main__" :
    n = 1884;

    print(minSum(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum
// possible sum of digits of A
// and B such that A + B = n
static int minSum(int n)
{
    // Find the sum of digits of n
    int sum = 0;
    while (n > 0)
    {
        sum += (n % 10);
        n /= 10;
    }

    // If num is a power of 10
    if (sum == 1)
        return 10;

    return sum;
}

// Driver code
public static void Main(String[] args)
{
    int n = 1884;

    Console.Write(minSum(n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum
// possible sum of digits of A
// and B such that A + B = n
function minSum(n)
{

    // Find the sum of digits of n
    var sum = 0;
    while (n > 0) {
        sum += (n % 10);
        n = parseInt(n/10);
    }

    // If num is a power of 10
    if (sum == 1)
        return 10;

    return sum;
}

// Driver code
var n = 1884;
document.write( minSum(n));

// This code is contributed by famously.
</script>
```

**Output:** 

```
21
```