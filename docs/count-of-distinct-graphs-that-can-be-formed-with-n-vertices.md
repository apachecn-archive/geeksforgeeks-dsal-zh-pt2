# 可以由 N 个顶点构成的不同图形的数量

> 原文:[https://www . geeksforgeeks . org/可由 n 个顶点构成的不同图形的数量/](https://www.geeksforgeeks.org/count-of-distinct-graphs-that-can-be-formed-with-n-vertices/)

给定一个整数 **N** ，这是顶点的数量。任务是找出可以形成的不同图形的数量。既然答案可以很大，打印**答案% 1000000007** 。
**例:**

> **输入:** N = 3
> **输出:** 8
> **输入:** N = 4
> **输出:** 64

**进场:**

*   具有 **N 个**顶点的图可以包含的最大边数是**X = N *(N–1)/2。**
*   包含 **0** 边和 **N** 顶点的图的总数将为 **<sup>X</sup> C <sub>0</sub>**
*   包含 **1** 边和 **N** 顶点的图的总数将为 **<sup>X</sup> C <sub>1</sub>**
*   以此类推，从多个边 1 到 **X** 加上 **N** 个顶点
*   因此，可以用 n 个顶点构成的图的总数将是:
    **<sup>X</sup>C<sub>0</sub>+<sup>X</sup>C<sub>1</sub>+<sup>X</sup>C<sub>2</sub>+…+<sup>X</sup>C<sub>X</sub>= 2<sup>X</sup>。**

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MOD = 1e9 + 7;

// Function to return (x^y) % MOD
// in O(log(y))
long long power(long long x,
                long long y,
                const int& MOD)
{
    long long res = 1;
    while (y > 0) {
        if (y & 1)
            res = (res * x) % MOD;
        x = (x * x) % MOD;
        y /= 2;
    }
    return res;
}

// Function to return the count of distinct
// graphs possible with n vertices
long long countGraphs(int n)
{

    // Maximum number of edges for a
    // graph with n vertices
    long long x = n * (n - 1) / 2;

    // Function to calculate
    // (2^x) % mod
    return power(2, x, MOD);
}

// Driver code
int main()
{
    int n = 5;

    cout << countGraphs(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static final int MOD = (int)1e9 + 7;

    // Function to return (x^y) % MOD
    // in O(log(y))
    static long power(long x,
                      long y)
    {
        long res = 1;
        while (y > 0)
        {
            if ((y & 1) != 0)
                res = (res * x) % MOD;
            x = (x * x) % MOD;
            y /= 2;
        }
        return res;
    }

    // Function to return the count of distinct
    // graphs possible with n vertices
    static long countGraphs(int n)
    {

        // Maximum number of edges for a
        // graph with n vertices
        long x = n * (n - 1) / 2;

        // Function to calculate
        // (2^x) % mod
        return power(2, x);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 5;

        System.out.println(countGraphs(n));
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
MOD = int(1e9 + 7)

# Function to return the count of distinct
# graphs possible with n vertices
def countGraphs(n):

    # Maximum number of edges for a
    # graph with n vertices
    x = (n *( n - 1 )) //2

    # Return 2 ^ x
    return (pow(2, x, MOD))

# Driver code
n = 5
print(countGraphs(n))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int MOD = (int)1e9 + 7;

    // Function to return (x^y) % MOD
    // in O(log(y))
    static long power(long x, long y)
    {
        long res = 1;
        while (y > 0)
        {
            if ((y & 1) != 0)
                res = (res * x) % MOD;
            x = (x * x) % MOD;
            y /= 2;
        }
        return res;
    }

    // Function to return the count of distinct
    // graphs possible with n vertices
    static long countGraphs(int n)
    {

        // Maximum number of edges for a
        // graph with n vertices
        long x = n * (n - 1) / 2;

        // Function to calculate
        // (2^x) % mod
        return power(2, x);
    }

    // Driver code
    static public void Main ()
    {
        int n = 5;

        Console.Write(countGraphs(n));
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

const MOD = 1000000000 + 7;

// Function to return (x^y) % MOD
// in O(log(y))
function power(x, y, MOD)
{
    let res = 1;
    while (y > 0) {
        if (y & 1)
            res = (res * x) % MOD;
        x = (x * x) % MOD;
        y = parseInt(y / 2);
    }
    return res;
}

// Function to return the count of distinct
// graphs possible with n vertices
function countGraphs(n)
{

    // Maximum number of edges for a
    // graph with n vertices
    let x = parseInt(n * (n - 1) / 2);

    // Function to calculate
    // (2^x) % mod
    return power(2, x, MOD);
}

// Driver code
    let n = 5;

    document.write(countGraphs(n));

</script>
```

**Output:** 

```
1024
```