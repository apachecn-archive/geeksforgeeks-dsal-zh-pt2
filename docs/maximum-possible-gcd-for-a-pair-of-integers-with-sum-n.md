# 和为 N 的一对整数的最大可能 GCD

> 原文:[https://www . geeksforgeeks . org/最大可能 gcd-for-a-对-整数-sum-n/](https://www.geeksforgeeks.org/maximum-possible-gcd-for-a-pair-of-integers-with-sum-n/)

给定一个整数 **N** ，任务是找到一对整数的最大可能 [**GCD**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) ，使得它们的和为 **N** 。

**示例:**

> **输入:** N = 30
> **输出:** 15
> **说明:**的(15，15)GCD 为 15，这是最大可能 GCD
> 
> **输入:** N = 33
> **输出:** 11
> **说明:(11，22)的** GCD 为 11，是最大可能 GCD

**天真法:**
解决这个问题最简单的方法就是用和 **N** 计算所有整数对的 GCD，找出其中最大可能的 **GCD** 。
***时间复杂度:**O(N<sup>2</sup>logN)*
***辅助空间:** O(1)*

**高效方法:**
按照下面给出的步骤优化上述方法:

*   向上迭代到 **√N** ，找到 **N** 的最大适当因子。
*   如果 **N** 是素数，即不能获得因子，打印 **1** ，因为所有对都是同素数。
*   否则，打印最大可能因子作为答案。

下面是上述方法的实现:

## C++

```
// C++ Program to find the maximum
// possible GCD of any pair with
// sum N
#include <bits/stdc++.h>
using namespace std;

// Function to find the required
// GCD value
int maxGCD(int N)
{
    for (int i = 2; i * i <= N; i++) {

        // If i is a factor of N
        if (N % i == 0) {

            // Return the largest
            // factor possible
            return N / i;
        }
    }

    // If N is a prime number
    return 1;
}

// Driver Code
int main()
{
    int N = 33;
    cout << "Maximum Possible GCD value is : "
        << maxGCD(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// possible GCD of any pair with
// sum N
class GFG{

// Function to find the required
// GCD value
static int maxGCD(int N)
{
    for(int i = 2; i * i <= N; i++)
    {

        // If i is a factor of N
        if (N % i == 0)
        {

            // Return the largest
            // factor possible
            return N / i;
        }
    }

    // If N is a prime number
    return 1;
}

// Driver Code
public static void main(String[] args)
{
    int N = 33;
    System.out.println("Maximum Possible GCD " +
                       "value is : " + maxGCD(N));
}
}

// This code is conhtributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# possible GCD of any pair with
# sum N

# Function to find the required
# GCD value
def maxGCD(N):

    i = 2
    while(i * i <= N):

        # If i is a factor of N
        if (N % i == 0):

            # Return the largest
            # factor possible
            return N // i

        i += 1

    # If N is a prime number
    return 1

# Driver Code
N = 33

print("Maximum Possible GCD value is : ",
       maxGCD(N))

# This code is contributed by code_hunt
```

## C#

```
// C# program to find the maximum
// possible GCD of any pair with
// sum N
using System;

class GFG{

// Function to find the required
// GCD value
static int maxGCD(int N)
{
    for(int i = 2; i * i <= N; i++)
    {

        // If i is a factor of N
        if (N % i == 0)
        {

            // Return the largest
            // factor possible
            return N / i;
        }
    }

    // If N is a prime number
    return 1;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 33;
    Console.WriteLine("Maximum Possible GCD " +
                      "value is : " + maxGCD(N));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to find the maximum
// possible GCD of any pair with
// sum N

// Function to find the required
// GCD value
function maxGCD(N)
{
    for(var i = 2; i * i <= N; i++)
    {

        // If i is a factor of N
        if (N % i == 0)
        {

            // Return the largest
            // factor possible
            return N / i;
        }
    }

    // If N is a prime number
    return 1;
}

// Driver code
var N = 33;
document.write("Maximum Possible GCD " +
               "value is :" + maxGCD(N));

// This code is contributed by Ankita saini.

</script>
```

**Output:** 

```
Maximum Possible GCD value is : 11
```

***时间复杂度:** O(√N)*
***辅助空间:** O(1)*