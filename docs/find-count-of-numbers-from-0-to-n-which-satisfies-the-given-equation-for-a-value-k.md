# 求从 0 到 n 的数的计数，该计数满足给定的 K 值方程

> 原文:[https://www . geeksforgeeks . org/find-从 0 到 n 的数字计数-哪一个满足给定的值等式-k/](https://www.geeksforgeeks.org/find-count-of-numbers-from-0-to-n-which-satisfies-the-given-equation-for-a-value-k/)

给定三个**正整数 a、b 和 n** ，我们的任务是找出满足给定等式**((K % a)% b)=((K % b)% a)**
**的所有数字 K 的总数【例:**

> **输入:** a = 3，b = 4，n = 25
> **输出:** 10
> **说明:**
> 满足上式的值为 0 1 2 3 12 13 14 15 24 25。例如，对于 K = 13((13 % 3) % 4)给出 1，((13 % 4) % 3)也给出 1 作为输出。
> **输入:** a = 1，b = 13，n = 500
> **输出:** 501
> **说明:**
> 总共有 501 个 0 到 500 之间的数字满足给定的等式。

**方法:**
为了解决上面提到的问题，我们有一个给定的条件 **(( k % a ) % b) = (( k % b ) % a)** ，从 **0 到 max(a，b)–1**的数字总是满足这个条件。所以根据上面提供的陈述，如果我们有 **a < = b，那么检查从 0 到 b-1 的所有数字**，我们有以下两种情况:

*   我们计算(k % a) % b，在这种情况下答案总是(k % a)，因为(k % a)的值总是小于 b。
*   我们计算(k % b) % a，在这种情况下，答案也总是(k % a)，因为(k % b)将返回 k，因为 k 小于 b。

同样，我们可以检查 a > b 的情况。所以现在我们需要检查 0 到 n 范围内所有能被 a 和 b 整除的数字。这可以借助 a 和 b 的 **LCM** 找到。所以，现在我们可以很容易地通过用 LCM 潜水 n 来找到 0 到 n 范围内 LCM 的倍数。我们将在倍数中添加 1，以包括 0 作为倍数。然后我们必须将倍数的数量乘以 max(a，b)，这样我们就可以找到满足给定条件的所有数字。但是如果最后倍数和 max(a，b)的和超过了我们的 n 个数范围，那么我们需要排除多余的数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation to Find the total
// count of all the numbers from 0 to n which
// satisfies the given equation for a value K

#include <bits/stdc++.h>
using namespace std;

// Function to find the values
int findAns(int a, int b, int n)
{
    // Calculate the LCM
    int lcm = (a * b) / __gcd(a, b);

    // Calculate the multiples of lcm
    int multiples = (n / lcm) + 1;

    // Find the values which satisfies
    // the given condition
    int answer = max(a, b) * multiples;

    // Subtract the extra values
    int lastvalue = lcm * (n / lcm) + max(a, b);

    if (lastvalue > n)
        answer = answer - (lastvalue - n - 1);

    // Return the final result
    return answer;
}

// Driver code
int main()
{
    int a = 1, b = 13, n = 500;

    cout << findAns(a, b, n) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the total
// count of all the numbers from 0 to n which
// satisfies the given equation for a value K
class GFG{

// Function to find the values
static int findAns(int a, int b, int n)
{
    // Calculate the LCM
    int lcm = (a * b) / __gcd(a, b);

    // Calculate the multiples of lcm
    int multiples = (n / lcm) + 1;

    // Find the values which satisfies
    // the given condition
    int answer = Math.max(a, b) * multiples;

    // Subtract the extra values
    int lastvalue = lcm * (n / lcm) + Math.max(a, b);
    if (lastvalue > n)
        answer = answer - (lastvalue - n - 1);

    // Return the final result
    return answer;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void main(String[] args)
{
    int a = 1, b = 13, n = 500;
    System.out.print(findAns(a, b, n) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation to find the total
# count of all the numbers from 0 to n which
# satisfies the given equation for a value K

# Function to find the values
def findAns(a, b, n):

    # Calculate the LCM
    lcm = (a * b) // __gcd(a, b);

    # Calculate the multiples of lcm
    multiples = (n // lcm) + 1;

    # Find the values which satisfies
    # the given condition
    answer = max(a, b) * multiples;

    # Subtract the extra values
    lastvalue = lcm * (n // lcm) + max(a, b);

    if (lastvalue > n):
        answer = answer - (lastvalue - n - 1);

    # Return the final result
    return answer;

def __gcd(a, b):

    if(b == 0):
        return a;
    else:
        return __gcd(b, a % b);

# Driver code
if __name__ == '__main__':

    a = 1;
    b = 13;
    n = 500;

    print(findAns(a, b, n));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation to find the total
// count of all the numbers from 0 to n which
// satisfies the given equation for a value K
using System;

class GFG{

// Function to find the values
static int findAns(int a, int b, int n)
{
    // Calculate the LCM
    int lcm = (a * b) / __gcd(a, b);

    // Calculate the multiples of lcm
    int multiples = (n / lcm) + 1;

    // Find the values which satisfies
    // the given condition
    int answer = Math.Max(a, b) * multiples;

    // Subtract the extra values
    int lastvalue = lcm * (n / lcm) + Math.Max(a, b);
    if (lastvalue > n)
    {
        answer = answer - (lastvalue - n - 1);
    }

    // Return the readonly result
    return answer;
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver code
public static void Main(String[] args)
{
    int a = 1, b = 13, n = 500;
    Console.Write(findAns(a, b, n) + "\n");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// javascript implementation to find the total
// count of all the numbers from 0 to n which
// satisfies the given equation for a value K   
// Function to find the values
    function findAns(a , b , n) {
        // Calculate the LCM
        var lcm = (a * b) / __gcd(a, b);

        // Calculate the multiples of lcm
        var multiples = (n / lcm) + 1;

        // Find the values which satisfies
        // the given condition
        var answer = Math.max(a, b) * multiples;

        // Subtract the extra values
        var lastvalue = lcm * (n / lcm) + Math.max(a, b);
        if (lastvalue > n)
            answer = answer - (lastvalue - n - 1);

        // Return the final result
        return answer;
    }

    function __gcd(a , b) {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver code

        var a = 1, b = 13, n = 500;
        document.write(findAns(a, b, n) + "\n");

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
501
```