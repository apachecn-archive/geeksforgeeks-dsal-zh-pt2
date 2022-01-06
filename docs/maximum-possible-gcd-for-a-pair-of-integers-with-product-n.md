# 乘积为 N 的一对整数的最大可能 GCD

> 原文:[https://www . geeksforgeeks . org/最大可能 gcd-for-a-pair-integer-with-product-n/](https://www.geeksforgeeks.org/maximum-possible-gcd-for-a-pair-of-integers-with-product-n/)

给定一个整数 **N** ，任务是用乘积 **N** 在所有整数对中找到最大可能的 GCD。
**例:**

> **输入:** N=12
> **输出:** 2
> **说明:**
> 与产品 12 的所有可能配对为{1，12}、{2，6}、{3，4}
> GCD(1，12) = 1
> GCD(2，6) = 2
> GCD(3，4) = 1
> 因此，最大可能 GCD =最大值(1，2，1) =

**天真方法:**
解决这个问题最简单的方法就是用乘积 **N** 生成所有可能的对，并计算所有这样的对的 GCD。最后，打印获得的最大 GCD。
***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*
**高效方法:**
上述方法可以通过[找到给定数的所有除数](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/) **N** 进行优化。对于获得的每对除数，计算它们的 GCD。最后，打印获得的最大 GCD。
按照以下步骤解决问题:

*   声明一个变量**最大 Gcd** 来跟踪最大 Gcd。
*   迭代到 **√N** ，对于每个整数，检查是否是 **N** 的因子。
*   如果 **N** 可被 **i** 整除，则计算该对因子 **(i，N / i)** 的 GCD。
*   对比 **GCD(i，N / i)** 更新 **maxGcd** 。
*   最后打印 **maxGcd** 。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return
/// the maximum GCD
int getMaxGcd(int N)
{
    int maxGcd = INT_MIN, A, B;

    // To find all divisors of N
    for (int i = 1; i <= sqrt(N); i++) {

        // If i is a factor
        if (N % i == 0) {
            // Store the pair of factors
            A = i, B = N / i;

            // Store the maximum GCD
            maxGcd = max(maxGcd, __gcd(A, B));
        }
    }

    // Return the maximum GCD
    return maxGcd;
}

// Driver Code
int main()
{

    int N = 18;
    cout << getMaxGcd(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to return
// the maximum GCD
static int getMaxGcd(int N)
{
    int maxGcd = Integer.MIN_VALUE, A, B;

    // To find all divisors of N
    for(int i = 1; i <= Math.sqrt(N); i++)
    {

        // If i is a factor
        if (N % i == 0)
        {

            // Store the pair of factors
            A = i;
            B = N / i;

            // Store the maximum GCD
            maxGcd = Math.max(maxGcd, gcd(A, B));
        }
    }

    // Return the maximum GCD
    return maxGcd;
}

// Driver Code
public static void main(String s[])
{
    int N = 18;

    System.out.println(getMaxGcd(N));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys
import math

# Function to return
# the maximum GCD
def getMaxGcd(N):

    maxGcd = -sys.maxsize - 1

    # To find all divisors of N
    for i in range(1, int(math.sqrt(N)) + 1):

        # If i is a factor
        if (N % i == 0):

            # Store the pair of factors
            A = i
            B = N // i

            # Store the maximum GCD
            maxGcd = max(maxGcd, math.gcd(A, B))

    # Return the maximum GCD
    return maxGcd

# Driver Code
N = 18

print(getMaxGcd(N))

# This code is contributed by code_hunt
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to return
// the maximum GCD
static int getMaxGcd(int N)
{
    int maxGcd = int.MinValue, A, B;

    // To find all divisors of N
    for(int i = 1; i <= Math.Sqrt(N); i++)
    {

        // If i is a factor
        if (N % i == 0)
        {

            // Store the pair of factors
            A = i;
            B = N / i;

            // Store the maximum GCD
            maxGcd = Math.Max(maxGcd, gcd(A, B));
        }
    }

    // Return the maximum GCD
    return maxGcd;
}

// Driver Code
public static void Main(String []s)
{
    int N = 18;

    Console.WriteLine(getMaxGcd(N));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

    function gcd(a , b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function to return
    // the maximum GCD
    function getMaxGcd(N)
    {
        var maxGcd = Number.MIN_VALUE, A, B;

        // To find all divisors of N
        for (i = 1; i <= Math.sqrt(N); i++)
        {

            // If i is a factor
            if (N % i == 0)
            {

                // Store the pair of factors
                A = i;
                B = N / i;

                // Store the maximum GCD
                maxGcd = Math.max(maxGcd, gcd(A, B));
            }
        }

        // Return the maximum GCD
        return maxGcd;
    }

    // Driver Code
        var N = 18;
        document.write(getMaxGcd(N));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(√N*log(N))*
***辅助空间:** O(1)*