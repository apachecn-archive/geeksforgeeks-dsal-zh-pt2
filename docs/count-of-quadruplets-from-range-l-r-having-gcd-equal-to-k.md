# GCD 等于 K 的范围【L，R】内的四胞胎计数

> 原文:[https://www . geeksforgeeks . org/from-range-l-r-having-gcd-equal-k 四胎的计数/](https://www.geeksforgeeks.org/count-of-quadruplets-from-range-l-r-having-gcd-equal-to-k/)

给定一个整数 **K** 和一个范围**【L，R】**，任务是从给定的范围中计数四胞胎对，该范围的 [gcd](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 等于 **K** 。
**举例:**

> **输入:** L = 1，R = 5，K = 3
> **输出:** 1
> (3，3，3，3)是 gcd = 3
> **唯一有效的四胞胎输入:** L = 2，R = 24，K = 5
> **输出:** 239

**天真的方法:**我们可以用四个循环迭代所有的数字，对于每四个小对，检查它的 gcd 是否等于 **K** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of quadruplets having gcd = k
int countQuadruplets(int l, int r, int k)
{

    // To store the required count
    int count = 0;

    // Check every quadruplet pair
    // whether its gcd is k
    for (int u = l; u <= r; u++) {
        for (int v = l; v <= r; v++) {
            for (int w = l; w <= r; w++) {
                for (int x = l; x <= r; x++) {
                    if (__gcd(__gcd(u, v), __gcd(w, x)) == k)
                        count++;
                }
            }
        }
    }

    // Return the required count
    return count;
}

// Driver code
int main()
{
    int l = 1, r = 10, k = 2;

    cout << countQuadruplets(l, r, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG {

    // Function to return
    // the gcd of a and b
    static int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function to return the count
    // of quadruplets having gcd = k
    static int countQuadruplets(int l, int r, int k)
    {

        // To store the required count
        int count = 0;

        // Check every quadruplet pair
        // whether its gcd is k
        for (int u = l; u <= r; u++) {
            for (int v = l; v <= r; v++) {
                for (int w = l; w <= r; w++) {
                    for (int x = l; x <= r; x++) {
                        if (gcd(gcd(u, v), gcd(w, x)) == k)
                            count++;
                    }
                }
            }
        }

        // Return the required count
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {

        int l = 1, r = 10, k = 2;

        System.out.println(countQuadruplets(l, r, k));
    }
}

// This code is contributed by jit_t.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import gcd

# Function to return the count
# of quadruplets having gcd = k
def countQuadruplets(l, r, k):

    # To store the required count
    count = 0

    # Check every quadruplet pair
    # whether its gcd is k
    for u in range(l, r + 1 ,1):
        for v in range(l, r + 1, 1):
            for w in range(l, r + 1, 1):
                for x in range(l, r + 1, 1):
                    if (gcd(gcd(u, v), gcd(w, x)) == k):
                        count += 1

    # Return the required count
    return count

# Driver code
if __name__ == '__main__':
    l = 1
    r = 10
    k = 2

    print(countQuadruplets(l, r, k))

# This code is contributed
# by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return
    // the gcd of a and b
    static int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function to return the count
    // of quadruplets having gcd = k
    static int countQuadruplets(int l, int r, int k)
    {

        // To store the required count
        int count = 0;

        // Check every quadruplet pair
        // whether its gcd is k
        for (int u = l; u <= r; u++) {
            for (int v = l; v <= r; v++) {
                for (int w = l; w <= r; w++) {
                    for (int x = l; x <= r; x++) {
                        if (gcd(gcd(u, v), gcd(w, x)) == k)
                            count++;
                    }
                }
            }
        }

        // Return the required count
        return count;
    }

    // Driver code
    static public void Main()
    {
        int l = 1, r = 10, k = 2;
        Console.WriteLine(countQuadruplets(l, r, k));
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// javascript implementation of the approach

    // Function to return
    // the gcd of a and b
    function gcd(a , b) {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function to return the count
    // of quadruplets having gcd = k
    function countQuadruplets(l , r , k) {

        // To store the required count
        var count = 0;

        // Check every quadruplet pair
        // whether its gcd is k
        for (u = l; u <= r; u++) {
            for (v = l; v <= r; v++) {
                for (w = l; w <= r; w++) {
                    for (x = l; x <= r; x++) {
                        if (gcd(gcd(u, v), gcd(w, x)) == k)
                            count++;
                    }
                }
            }
        }

        // Return the required count
        return count;
    }

    // Driver code

        var l = 1, r = 10, k = 2;

        document.write(countQuadruplets(l, r, k));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
607
```

**时间复杂度:**O((r–l)<sup>4</sup>)
T5】高效进场:T7】

1.  求给定范围内每一个可能对(x，y)的 GCD。
2.  计算每个可能的 GCD 值的频率。
3.  此后，如果两个数的 GCD 值为 k，则按频率[i] *频率[j]递增计数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return
// the gcd of a and b
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to return the count
// of quadruplets having gcd = k
int countQuadruplets(int l, int r, int k)
{

    int frequency[r + 1] = { 0 };

    // Count the frequency of every possible gcd
    // value in the range
    for (int i = l; i <= r; i++) {
        for (int j = l; j <= r; j++) {
            frequency[gcd(i, j)]++;
        }
    }

    // To store the required count
    long long answer = 0;

    // Calculate the answer using frequency values
    for (int i = 1; i <= r; i++) {
        for (int j = 1; j <= r; j++) {
            if (gcd(i, j) == k) {
                answer += (frequency[i] * frequency[j]);
            }
        }
    }

    // Return the required count
    return answer;
}

// Driver code
int main()
{
    int l = 1, r = 10, k = 2;

    cout << countQuadruplets(l, r, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return
// the gcd of a and b
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to return the count
// of quadruplets having gcd = k
static int countQuadruplets(int l, int r, int k)
{

    int frequency[]= new int[r + 1] ;

    // Count the frequency of every possible gcd
    // value in the range
    for (int i = l; i <= r; i++)
    {
        for (int j = l; j <= r; j++)
        {
            frequency[gcd(i, j)]++;
        }
    }

    // To store the required count
    long answer = 0;

    // Calculate the answer using frequency values
    for (int i = 1; i <= r; i++)
    {
        for (int j = 1; j <= r; j++)
        {
            if (gcd(i, j) == k)
            {
                answer += (frequency[i] * frequency[j]);
            }
        }
    }

    // Return the required count
    return (int)answer;
}

// Driver code
public static void main(String args[])
{
    int l = 1, r = 10, k = 2;

    System.out.println(countQuadruplets(l, r, k));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return
# the gcd of a and b
def gcd(a, b):
    if (b == 0):
        return a;
    return gcd(b, a % b);

# Function to return the count
# of quadruplets having gcd = k
def countQuadruplets(l, r, k):
    frequency = [0] * (r + 1);

    # Count the frequency of every possible gcd
    # value in the range
    for i in range(l, r + 1):
        for j in range(l, r + 1):
            frequency[gcd(i, j)] += 1;

    # To store the required count
    answer = 0;

    # Calculate the answer using frequency values
    for i in range(l, r + 1):
        for j in range(l, r + 1):
            if (gcd(i, j) == k):
                answer += (frequency[i] * frequency[j]);

    # Return the required count
    return answer;

# Driver code
if __name__ == '__main__':
    l, r, k = 1, 10, 2;

    print(countQuadruplets(l, r, k));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return
// the gcd of a and b
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to return the count
// of quadruplets having gcd = k
static int countQuadruplets(int l, int r, int k)
{

    int []frequency= new int[r + 1] ;

    // Count the frequency of every possible gcd
    // value in the range
    for (int i = l; i <= r; i++)
    {
        for (int j = l; j <= r; j++)
        {
            frequency[gcd(i, j)]++;
        }
    }

    // To store the required count
    long answer = 0;

    // Calculate the answer using frequency values
    for (int i = 1; i <= r; i++)
    {
        for (int j = 1; j <= r; j++)
        {
            if (gcd(i, j) == k)
            {
                answer += (frequency[i] * frequency[j]);
            }
        }
    }

    // Return the required count
    return (int)answer;
}

// Driver code
static public void Main ()
{
    int l = 1, r = 10, k = 2;
    Console.WriteLine(countQuadruplets(l, r, k));
}
}

// This code is contributed by @ajit_00023
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return
    // the gcd of a and b
    function gcd(a, b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Function to return the count
    // of quadruplets having gcd = k
    function countQuadruplets(l, r, k)
    {

        let frequency= new Array(r + 1);
        frequency.fill(0);

        // Count the frequency of every possible gcd
        // value in the range
        for (let i = l; i <= r; i++)
        {
            for (let j = l; j <= r; j++)
            {
                frequency[gcd(i, j)]++;
            }
        }

        // To store the required count
        let answer = 0;

        // Calculate the answer using frequency values
        for (let i = 1; i <= r; i++)
        {
            for (let j = 1; j <= r; j++)
            {
                if (gcd(i, j) == k)
                {
                    answer += (frequency[i] * frequency[j]);
                }
            }
        }

        // Return the required count
        return answer;
    }

    let l = 1, r = 10, k = 2;
    document.write(countQuadruplets(l, r, k));

</script>
```

**Output:** 

```
607
```

**时间复杂度:**O((r–l)<sup>2</sup>)