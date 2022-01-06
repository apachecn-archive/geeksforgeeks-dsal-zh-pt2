# 给定数组中所有元素的整数计数

> 原文:[https://www . geeksforgeeks . org/对给定数组的所有元素进行除法运算的整数计数/](https://www.geeksforgeeks.org/count-of-integers-that-divide-all-the-elements-of-the-given-array/)

给定一个由 **N** 元素组成的数组 **arr[]** 。任务是找出除以所有数组元素的正整数的个数。
**例:**

> **输入:** arr[] = {2，8，10，6}
> **输出:** 2
> 1 和 2 是给定数组中唯一除以
> 所有元素的整数。
> **输入:** arr[] = {6，12，18，12，6}
> **输出:** 4

**方法:**我们知道将划分所有数组元素的最大整数将是数组的 [gcd](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) ，而将划分数组所有元素的所有其他整数将必须是这个 gcd 的因子。因此，有效整数的计数将等于所有数组元素的 gcd 因子的计数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// the required integers
int getCount(int a[], int n)
{

    // To store the gcd of the array elements
    int gcd = 0;
    for (int i = 0; i < n; i++)
        gcd = __gcd(gcd, a[i]);

    // To store the count of factors
    // of the found gcd
    int cnt = 0;

    for (int i = 1; i * i <= gcd; i++) {
        if (gcd % i == 0) {

            // If g is a perfect square
            if (i * i == gcd)
                cnt++;

            // Factors appear in pairs
            else
                cnt += 2;
        }
    }

    return cnt;
}

// Driver code
int main()
{
    int a[] = { 4, 16, 1024, 48 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << getCount(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Recursive function to return gcd
    static int calgcd(int a, int b)
    {
        if (b == 0)
            return a;
        return calgcd(b, a % b);
    }

    // Function to return the count of
    // the required integers
    static int getCount(int [] a, int n)
    {

        // To store the gcd of the array elements
        int gcd = 0;
        for (int i = 0; i < n; i++)
            gcd = calgcd(gcd, a[i]);

        // To store the count of factors
        // of the found gcd
        int cnt = 0;

        for (int i = 1; i * i <= gcd; i++)
        {
            if (gcd % i == 0)
            {

                // If g is a perfect square
                if (i * i == gcd)
                    cnt++;

                // Factors appear in pairs
                else
                    cnt += 2;
            }
        }
        return cnt;
    }

    // Driver code
    public static void main (String[] args)
    {
        int [] a = { 4, 16, 1024, 48 };
        int n = a.length;

        System.out.println(getCount(a, n));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# the required integers
from math import gcd as __gcd
def getCount(a, n):

    # To store the gcd of the array elements
    gcd = 0
    for i in range(n):
        gcd = __gcd(gcd, a[i])

    # To store the count of factors
    # of the found gcd
    cnt = 0

    for i in range(1, gcd + 1):
        if i * i > gcd:
            break
        if (gcd % i == 0):

            # If g is a perfect square
            if (i * i == gcd):
                cnt += 1

            # Factors appear in pairs
            else:
                cnt += 2

    return cnt

# Driver code
a = [4, 16, 1024, 48]
n = len(a)

print(getCount(a, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Recursive function to return gcd
    static int calgcd(int a, int b)
    {
        if (b == 0)
            return a;
        return calgcd(b, a % b);
    }

    // Function to return the count of
    // the required integers
    static int getCount(int [] a, int n)
    {

        // To store the gcd of the array elements
        int gcd = 0;
        for (int i = 0; i < n; i++)
            gcd = calgcd(gcd, a[i]);

        // To store the count of factors
        // of the found gcd
        int cnt = 0;

        for (int i = 1; i * i <= gcd; i++)
        {
            if (gcd % i == 0)
            {

                // If g is a perfect square
                if (i * i == gcd)
                    cnt++;

                // Factors appear in pairs
                else
                    cnt += 2;
            }
        }
        return cnt;
    }

    // Driver code
    public static void Main ()
    {
        int [] a = { 4, 16, 1024, 48 };
        int n = a.Length;

        Console.WriteLine(getCount(a, n));
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

function calgcd(a, b)
{
    if (b == 0)
        return a;
    return calgcd(b, a % b);
}

// Function to return the count of
// the required integers
function getCount(a, n)
{

    // To store the gcd of the array elements
    let gcd = 0;
    for (let i = 0; i < n; i++)
        gcd = calgcd(gcd, a[i]);

    // To store the count of factors
    // of the found gcd
    let cnt = 0;

    for (let i = 1; i * i <= gcd; i++) {
        if (gcd % i == 0) {

            // If g is a perfect square
            if (i * i == gcd)
                cnt++;

            // Factors appear in pairs
            else
                cnt += 2;
        }
    }

    return cnt;
}

// Driver code
    let a = [ 4, 16, 1024, 48 ];
    let n = a.length;

    document.write(getCount(a, n));

</script>
```

**Output:** 

```
3
```