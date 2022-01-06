# 计算使用 N 个不相交弦划分圆的方式| Set-2

> 原文:[https://www . geesforgeks . org/count-way-divide-circle-using-n-non-interfering-chord-set-2/](https://www.geeksforgeeks.org/count-ways-to-divide-circle-using-n-non-intersecting-chord-set-2/)

给定一个数字 **N** 。任务是找到用 **2*N** 点在一个圆上画 **N** 弦的方法，这样就不会有两个弦相交。如果有一个和弦以一种方式出现而不是以另一种方式出现，那么这两种方式是不同的。因为答案可能是大号字体，它以 10^9+7.为模

**示例:**

> **输入:** N = 2
> **输出:** 2
> 如果点按顺时针方向编号为 1 到 4，
> 则不同的和弦绘制方式为:
> {(1-2)、(3-4)和{(1-4)、(2-3)}
> 
> **输入:**N = 1
> T3】输出: 1

**方法:**
如果我们在任两点之间画一个和弦，当前的点集合被分成两个更小的集合 S1 和 S2。如果我们从 S1 点到 S2 点画一个弦，它肯定会和我们刚才画的弦相交。所以，我们可以得出一个循环:

> 路(n) =和[i = 0 到 n-1] {路(I)*路(n-i-1) }。

上述递归关系类似于 n<sup>th</sup>T2 加泰罗尼亚数字的递归关系，等于**T5】2nC<sub>n</sub>/(n+1)**。不要用面额来除数字，而是用分子乘以分母的模逆，因为在模域中不允许除。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate x^y %mod efficiently
int power(long long x, int y, int mod)
{

    // Initialize the answer
    long long res = 1;
    while (y) {

        // If power is odd
        if (y & 1)

            // Update the answer
            res = (res * x) % mod;

        // Square the base and half the exponent
        x = (x * x) % mod;
        y = (y >> 1);
    }

    // Return the value
    return (int)(res % mod);
}

// Function to calculate ncr%mod efficiently
int ncr(int n, int r, int mod)
{

    // Initialize the answer
    long long res = 1;

    // Calculate ncr in O(r)
    for (int i = 1; i <= r; i += 1) {

        // Multiply with the numerator factor
        res = (res * (n - i + 1)) % mod;

        // Calculate the inverse of factor of denominator
        int inv = power(i, mod - 2, mod);

        // Multiply with inverse value
        res = (res * inv) % mod;
    }

    // Return answer value
    return (int)(res%mod);
}

// Function to return the number
// of non intersecting chords
int NoOfChords(int A)
{

    // define mod value
    int mod = 1e9 + 7;

    // Value of C(2n, n)
    long long ans = ncr(2 * A, A, mod);

    // Modulo inverse of (n+1)
    int inv = power(A + 1, mod - 2, mod);

    // Multiply with modulo inverse
    ans = (ans * inv) % mod;

    // Return the answer
    return (int)(ans%mod);
}

// Driver code
int main()
{

    int N = 2;

    // Function call
    cout << NoOfChords(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to calculate x^y %mod efficiently
    static int power(long x, int y, int mod)
    {

        // Initialize the answer
        long res = 1;
        while (y != 0)
        {

            // If power is odd
            if ((y & 1) == 1)

                // Update the answer
                res = (res * x) % mod;

            // Square the base and half the exponent
            x = (x * x) % mod;
            y = (y >> 1);
        }

        // Return the value
        return (int)(res % mod);
    }

    // Function to calculate ncr%mod efficiently
    static int ncr(int n, int r, int mod)
    {

        // Initialize the answer
        long res = 1;

        // Calculate ncr in O(r)
        for (int i = 1; i <= r; i += 1)
        {

            // Multiply with the numerator factor
            res = (res * (n - i + 1)) % mod;

            // Calculate the inverse of
            // factor of denominator
            int inv = power(i, mod - 2, mod);

            // Multiply with inverse value
            res = (res * inv) % mod;
        }

        // Return answer value
        return (int)(res % mod);
    }

    // Function to return the number
    // of non intersecting chords
    static int NoOfChords(int A)
    {

        // define mod value
        int mod = (int)(1e9 + 7);

        // Value of C(2n, n)
        long ans = ncr(2 * A, A, mod);

        // Modulo inverse of (n+1)
        int inv = power(A + 1, mod - 2, mod);

        // Multiply with modulo inverse
        ans = (ans * inv) % mod;

        // Return the answer
        return (int)(ans % mod);
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 2;

        // Function call
        System.out.println(NoOfChords(N));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to calculate x^y %mod efficiently
def power(x, y, mod):

    # Initialize the answer
    res = 1
    while (y):

        # If power is odd
        if (y & 1):

            # Update the answer
            res = (res * x) % mod

        # Square the base and half the exponent
        x = (x * x) % mod
        y = (y >> 1)

    # Return the value
    return (res % mod)

# Function to calculate ncr%mod efficiently
def ncr(n, r, mod):

    # Initialize the answer
    res = 1

    # Calculate ncr in O(r)
    for i in range(1,r+1):

        # Multiply with the numerator factor
        res = (res * (n - i + 1)) % mod

        # Calculate the inverse of factor of denominator
        inv = power(i, mod - 2, mod)

        # Multiply with inverse value
        res = (res * inv) % mod

    # Return answer value
    return (res%mod)

# Function to return the number
# of non intersecting chords
def NoOfChords(A):

    # define mod value
    mod = 10**9 + 7

    # Value of C(2n, n)
    ans = ncr(2 * A, A, mod)

    # Modulo inverse of (n+1)
    inv = power(A + 1, mod - 2, mod)

    # Multiply with modulo inverse
    ans = (ans * inv) % mod

    # Return the answer
    return (ans%mod)

# Driver code

N = 2

# Function call
print(NoOfChords(N))

# This code is contributed by mohit kumar 29
```

## C#

```
// Java implementation of the above approach
using System;

class GFG
{

    // Function to calculate x^y %mod efficiently
    static int power(long x, int y, int mod)
    {

        // Initialize the answer
        long res = 1;
        while (y != 0)
        {

            // If power is odd
            if ((y & 1) == 1)

                // Update the answer
                res = (res * x) % mod;

            // Square the base and half the exponent
            x = (x * x) % mod;
            y = (y >> 1);
        }

        // Return the value
        return (int)(res % mod);
    }

    // Function to calculate ncr%mod efficiently
    static int ncr(int n, int r, int mod)
    {

        // Initialize the answer
        long res = 1;

        // Calculate ncr in O(r)
        for (int i = 1; i <= r; i += 1)
        {

            // Multiply with the numerator factor
            res = (res * (n - i + 1)) % mod;

            // Calculate the inverse of factor of denominator
            int inv = power(i, mod - 2, mod);

            // Multiply with inverse value
            res = (res * inv) % mod;
        }

        // Return answer value
        return (int)(res % mod);
    }

    // Function to return the number
    // of non intersecting chords
    static int NoOfChords(int A)
    {

        // define mod value
        int mod = (int)(1e9 + 7);

        // Value of C(2n, n)
        long ans = ncr(2 * A, A, mod);

        // Modulo inverse of (n+1)
        int inv = power(A + 1, mod - 2, mod);

        // Multiply with modulo inverse
        ans = (ans * inv) % mod;

        // Return the answer
        return (int)(ans % mod);
    }

    // Driver code
    public static void Main ()
    {
        int N = 2;

        // Function call
        Console.WriteLine(NoOfChords(N));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach 

// Function to calculate x^y %mod efficiently
function power(x , y , mod)
{

    // Initialize the answer
    var res = 1;
    while (y != 0)
    {

        // If power is odd
        if ((y & 1) == 1)

            // Update the answer
            res = (res * x) % mod;

        // Square the base and half the exponent
        x = (x * x) % mod;
        y = (y >> 1);
    }

    // Return the value
    return parseInt(res % mod);
}

// Function to calculate ncr%mod efficiently
function ncr(n , r , mod)
{

    // Initialize the answer
    var res = 1;

    // Calculate ncr in O(r)
    for (var i = 1; i <= r; i += 1)
    {

        // Multiply with the numerator factor
        res = (res * (n - i + 1)) % mod;

        // Calculate the inverse of
        // factor of denominator
        var inv = power(i, mod - 2, mod);

        // Multiply with inverse value
        res = (res * inv) % mod;
    }

    // Return answer value
    return parseInt(res % mod);
}

// Function to return the number
// of non intersecting chords
function NoOfChords( A)
{

    // define mod value
    var mod = parseInt(7);

    // Value of C(2n, n)
    var ans = ncr(2 * A, A, mod);

    // Modulo inverse of (n+1)
    var inv = power(A + 1, mod - 2, mod);

    // Multiply with modulo inverse
    ans = (ans * inv) % mod;

    // Return the answer
    return parseInt(ans % mod);
}

// Driver code
var N = 2;

// Function call
document.write(NoOfChords(N));

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N*log(mod))