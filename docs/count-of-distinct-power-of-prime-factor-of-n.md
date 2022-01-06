# N 的质因数的不同幂的计数

> 原文:[https://www . geeksforgeeks . org/count-of-distinct-power-of-n-prime-factor/](https://www.geeksforgeeks.org/count-of-distinct-power-of-prime-factor-of-n/)

给定一个正整数 **N** ，任务是求给定数 N 的[质因数的不同幂的总数。
**例:**](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/) 

> **输入:** N = 216
> **输出:** 4
> **说明:**
> 216 可以表示为 2 * 2<sup>2</sup>* 3<sup>2</sup>。
> 满足条件的因子是 2，2 <sup>2</sup> ，3 和 3 <sup>2</sup> ，因为它们都被写成质因数的不同正幂。
> **输入:** N = 24
> **输出:** 3
> **说明:**
> 24 可以表示为 2 * 2 <sup>2</sup> * 3

**方法:**思路是找出 N 的所有[素因子，以及每个](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)[素因子](https://www.geeksforgeeks.org/prime-factor/)除以 **N** 的次数。
假设质因数**‘p’**除以 N**‘z’**次，则所需的不同质因数为 **p，p <sup>2</sup> ，…，p <sup>i</sup>** 。
求素数 p 的相异素数因子的个数求 I 的最小值使得 **(1 + 2 + …)。+ i) ≤ z** 。
因此，对于每一个[素数](https://www.geeksforgeeks.org/prime-numbers/)除以 **N** **K** 的次数，求 I 的最小值使得 **(1 + 2 + …。+ i) ≤ K** 。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number
// of distinct positive power of
// prime factor of integer N
int countFac(int n)
{
    int m = n;
    int count = 0;

    // Iterate for all prime factor
    for (int i = 2; (i * i) <= m; ++i) {

        int total = 0;

        // If it is a prime factor,
        // count the total number
        // of times it divides n.
        while (n % i == 0) {
            n /= i;
            ++total;
        }

        int temp = 0;

        // Find the Number of distinct
        // possible positive numbers
        for (int j = 1;
             (temp + j) <= total;
             ++j) {
            temp += j;
            ++count;
        }
    }
    if (n != 1)
        ++count;

    // Return the final count
    return count;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 24;

    // Function Call
    cout << countFac(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count the number
// of distinct positive power of
// prime factor of integer N
static int countFac(int n)
{
    int m = n;
    int count = 0;

    // Iterate for all prime factor
    for(int i = 2; (i * i) <= m; ++i)
    {
       int total = 0;

       // If it is a prime factor,
       // count the total number
       // of times it divides n.
       while (n % i == 0)
       {
           n /= i;
           ++total;
       }
       int temp = 0;

       // Find the Number of distinct
       // possible positive numbers
       for(int j = 1; (temp + j) <= total; ++j)
       {
          temp += j;
          ++count;
       }
    }
    if (n != 1)
        ++count;

    // Return the final count
    return count;
}

// Driver code
public static void main(String[] args)
{

    // Given Number N
    int N = 24;

    // Function Call
    System.out.println(countFac(N));
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number
# of distinct positive power of
# prime factor of integer N
def countFac(n):

    m = n
    count = 0

    # Iterate for all prime factor
    i = 2
    while((i * i) <= m):
        total = 0

        # If it is a prime factor,
        # count the total number
        # of times it divides n.
        while (n % i == 0):
            n /= i
            total += 1

        temp = 0

        # Find the Number of distinct
        # possible positive numbers
        j = 1
        while((temp + j) <= total):
            temp += j
            count += 1
            j += 1

        i += 1

    if (n != 1):
        count += 1

    # Return the final count
    return count

# Driver Code

# Given number N
N = 24

# Function call
print(countFac(N))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to count the number
// of distinct positive power of
// prime factor of integer N
static int countFac(int n)
{
    int m = n;
    int count = 0;

    // Iterate for all prime factor
    for(int i = 2; (i * i) <= m; ++i)
    {
       int total = 0;

       // If it is a prime factor,
       // count the total number
       // of times it divides n.
       while (n % i == 0)
       {
           n /= i;
           ++total;
       }
       int temp = 0;

       // Find the Number of distinct
       // possible positive numbers
       for(int j = 1; (temp + j) <= total; ++j)
       {
          temp += j;
          ++count;
       }
    }
    if (n != 1)
        ++count;

    // Return the final count
    return count;
}

// Driver code
public static void Main()
{

    // Given Number N
    int N = 24;

    // Function Call
    Console.Write(countFac(N));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the number
// of distinct positive power of
// prime factor of integer N
function countFac(n)
{
    var m = n;
    var count = 0;

    // Iterate for all prime factor
    for(var i = 2; (i * i) <= m; ++i)
    {
       var total = 0;

       // If it is a prime factor,
       // count the total number
       // of times it divides n.
       while (n % i == 0)
       {
           n /= i;
           ++total;
       }
       var temp = 0;

       // Find the Number of distinct
       // possible positive numbers
       for(var j = 1; (temp + j) <= total; ++j)
       {
          temp += j;
          ++count;
       }
    }
    if (n != 1)
        ++count;

    // Return the final count
    return count;
}

// Driver code

// Given Number N
var N = 24;

// Function Call
document.write(countFac(N));

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
3
```

**时间复杂度:**T2【O(sqrt(N))T4】