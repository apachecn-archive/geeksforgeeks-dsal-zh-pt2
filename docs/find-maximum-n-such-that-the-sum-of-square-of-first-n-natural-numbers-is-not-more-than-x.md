# 求最大 N，使得前 N 个自然数的平方和不大于 X

> 原文:[https://www . geesforgeks . org/find-maximum-n-so-第一个 n 个自然数的平方和不大于-x/](https://www.geeksforgeeks.org/find-maximum-n-such-that-the-sum-of-square-of-first-n-natural-numbers-is-not-more-than-x/)

给定一个整数 **X** ，任务是求最大值 **N** ，使得第一个 **N** 自然数之和不大于 **X** 。

**示例:**

> **输入:** X = 5
> **输出:** 2
> 2 是 N 的最大可能值，因为对于 N = 3，级数之和将超过 X
> ，即 1<sup>2</sup>+2<sup>2</sup>+3<sup>2</sup>= 1+4+9 = 14
> 
> **输入:**X = 25
> T3】输出: 3

**简单解法**:简单解法是从 **1** 到最大 **N** 运行一个循环，使得 **S(N) ≤ X** ，其中 **S(N)** 为第一个 **N** 自然数的平方和。第一个 **N** 自然数的平方和由公式 **S(N) = N * (N + 1) * (2 * N + 1) / 6** 给出。该方法的时间复杂度为 **O(N)** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of the squares
// of first N natural numbers
int squareSum(int N)
{
    int sum = (int)(N * (N + 1) * (2 * N + 1)) / 6;

    return sum;
}
// Function to return the maximum N such that
// the sum of the squares of first N
// natural numbers is not more than X
int findMaxN(int X)
{

    int N = sqrt(X);
    // Iterate till maxvalue of N
    for (int i = 1; i <= N; i++)
    {
        // If the condition fails then return the i-1 i.e
        // sum of squares till i-1
        if (squareSum(i) > X)
            return i - 1;
    }
    return -1L;
}

// Driver code
int main()
{
    int X = 25;
    cout << findMaxN(X);

    return 0;
}
// This code is contributed by hemanth gadarla
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the sum of the squares
    // of first N natural numbers
    static long squareSum(long N)
    {
        long sum = (long)(N * (N + 1)
                          * (2 * N + 1)) / 6;

        return sum;
    }

    // Function to return the maximum N such that
    // the sum of the squares of first N
    // natural numbers is not more than X
    static long findMaxN(long X)
    {
        long N = (long)Math.sqrt(X);
        // Iterate through the maxvalue
        // of N and find the
        // ith position
        for (long i = 1; i <= N; i++)
        {
            if (squareSum(i) > X)
                return i - 1;
        }
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        long X = 25;
        System.out.println(findMaxN(X));
    }
}

// This code contributed by Hemanth gadarla
```

## 蟒蛇 3

```
# Python implementation of the approach
import math

# Function to return the sum of the squares
# of first N natural numbers
def squareSum(N):
    sum = (N * (N + 1) * (2 * N + 1)) // 6
    return sum

# Function to return the maximum N such that
# the sum of the squares of first N
# natural numbers is not more than X
def findMaxN(X):
    N = (int)(math.sqrt(X))

    # Iterate till maxvalue of N
    for i in range(1, N + 1):

        # If the condition fails then return the i-1 i.e
        # sum of squares till i-1
        if (squareSum(i) > X):
            return i - 1
    return -1

# Driver code
X = 25
print(findMaxN(X))

# This code is contributed by souravmahato348.
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to return the sum of the squares
// of first N natural numbers
static long squareSum(long N)
{
    long sum = (long)(N * (N + 1) *
                      (2 * N + 1)) / 6;

    return sum;
}

// Function to return the maximum N such that
// the sum of the squares of first N
// natural numbers is not more than X
static long findMaxN(long X)
{
    long N = (long)Math.Sqrt(X);

    // Iterate through the maxvalue
    // of N and find the
    // ith position
    for(long i = 1; i <= N; i++)
    {
        if (squareSum(i) > X)
            return i - 1;
    }
    return -1;
}

// Driver code
public static void Main(string[] args)
{
    long X = 25;

    Console.WriteLine(findMaxN(X));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the sum of the squares
// of first N natural numbers
function squareSum(N)
{
    let sum = parseInt((N * (N + 1) *
                        (2 * N + 1)) / 6);

    return sum;
}

// Function to return the maximum N such that
// the sum of the squares of first N
// natural numbers is not more than X
function findMaxN(X)
{
    let N = Math.sqrt(X);

    // Iterate till maxvalue of N
    for(let i = 1; i <= N; i++)
    {

        // If the condition fails then
        // return the i-1 i.e sum of
        // squares till i-1
        if (squareSum(i) > X)
            return i - 1;
    }
    return -1;
}

// Driver code
let X = 25;

document.write(findMaxN(X));

// This code is contributed by rishavmahato348

</script>
```

**Output**

```
3
```

**高效方法** :
一个高效的解决方案是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到 **N** 的值。这种方法的时间复杂度是 **O(log N)** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of the squares
// of first N natural numbers
int squareSum(int N)
{
    int sum = (int)(N * (N + 1) * (2 * N + 1)) / 6;

    return sum;
}

// Function to return the maximum N such that
// the sum of the squares of first N
// natural numbers is not more than X
int findMaxN(int X)
{
    int low = 1, high = 100000;
    int N = 0;

    while (low <= high)
    {
        int mid = (high + low) / 2;

        if (squareSum(mid) <= X)
        {
            N = mid;
            low = mid + 1;
        }

        else
            high = mid - 1;
    }

    return N;
}

// Driver code
int main()
{
    int X = 25;
    cout << findMaxN(X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the sum of the squares
    // of first N natural numbers
    static long squareSum(long N)
    {
        long sum = (long)(N * (N + 1)
                          * (2 * N + 1)) / 6;

        return sum;
    }

    // Function to return the maximum N such that
    // the sum of the squares of first N
    // natural numbers is not more than X
    static long findMaxN(long X)
    {
        long low = 1, high = 100000;
        int N = 0;

        while (low <= high) {
            long mid = (high + low) / 2;

            if (squareSum(mid) <= X)
            {
                N = (int)mid;
                low = mid + 1;
            }

            else
                high = mid - 1;
        }

        return N;
    }

    // Driver code
    public static void main(String[] args)
    {
        long X = 25;
        System.out.println(findMaxN(X));
    }
}

// This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the sum of the squares
    // of first N natural numbers
    static long squareSum(long N)
    {
        long sum = (long)(N * (N + 1)
                          * (2 * N + 1)) / 6;

        return sum;
    }

    // Function to return the maximum N such that
    // the sum of the squares of first N
    // natural numbers is not more than X
    static long findMaxN(long X)
    {
        long low = 1, high = 100000;
        int N = 0;

        while (low <= high) {
            long mid = (high + low) / 2;

            if (squareSum(mid) <= X) {
                N = (int)mid;
                low = mid + 1;
            }

            else
                high = mid - 1;
        }

        return N;
    }

    // Driver code
    static public void Main()
    {

        long X = 25;
        Console.WriteLine(findMaxN(X));
    }
}

// This code contributed by ajit
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the sum of the
# squares of first N natural numbers
def squareSum(N):

    Sum = (N * (N + 1) * (2 * N + 1)) // 6
    return Sum

# Function to return the maximum N such
# that the sum of the squares of first N
# natural numbers is not more than X
def findMaxN(X):

    low, high, N = 1, 100000, 0

    while low <= high:
        mid = (high + low) // 2

        if squareSum(mid) <= X:
            N = mid
            low = mid + 1

        else:
            high = mid - 1

    return N

# Driver code
if __name__ == "__main__":

    X = 25
    print(findMaxN(X))

# This code is contributed
# by Rituraj Jain
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the sum of the
// squares of first N natural numbers
function squareSum($N)
{
    $sum = ($N * (int)($N + 1) *
                  (2 * $N + 1)) / 6;

    return $sum;
}

// Function to return the maximum N such
// that the sum of the squares of first N
// natural numbers is not more than X
function findMaxN($X)
{
    $low = 1;
    $high = 100000;
    $N = 0;

    while ($low <= $high)
    {
        $mid = (int)($high + $low) / 2;

        if (squareSum($mid) <= $X)
        {
            $N = $mid;
            $low = $mid + 1;
        }

        else
            $high = $mid - 1;
    }

    return $N;
}

// Driver code
$X = 25;
echo findMaxN($X);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the sum of the squares
// of first N natural numbers
function squareSum(N)
{
    var sum = parseInt((N * (N + 1) *
                        (2 * N + 1)) / 6);

    return sum;
}

// Function to return the maximum N such that
// the sum of the squares of first N
// natural numbers is not more than X
function findMaxN(X)
{
    var low = 1, high = 100000;
    var N = 0;

    while (low <= high)
    {
        var mid = (high + low) / 2;

        if (squareSum(mid) <= X)
        {
            N = parseInt(mid);
            low = mid + 1;
        }
        else
            high = mid - 1;
    }
    return N;
}

// Driver Code
var X = 25;

document.write(findMaxN(X));

// This code is contributed by Ankita saini

</script>
```

**Output**

```
3
```

**交替进场** :
思路是**从 N 减去连续方块**，而 **N > =(i*i)** 其中 **i** 从 1 开始，当 **N < (i*i)时循环结束。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long

// Function to return the maximum N such that
// the sum of the squares of first N
// natural numbers is not more than X
ll findMaxN(ll X)
{
    ll i = 1; // To keep track of all squares in the series
    ll count = 0; // to count the number of squares used to
                  // reach N
    ll N = X;
    while (N >= (i * i)) {
        // Subtract the square of current number
        N -= (i * i);
        // Increment count
        count += 1;
        // increment i for next square number
        i += 1;
    }
    return count;
}

// Driver code
int main()
{
    ll X = 25;
    cout << findMaxN(X);

    return 0;
}
// This code is contributed by hemanth gadarla
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the maximum N such that
    // the sum of the squares of first N
    // natural numbers is not more than X
    static long findMaxN(long X)
    {

        long N = X;
        // To keep track of the squares of consecutive
        // numbers
        int i = 1;
        while (N >= (i * i)) {
            N -= (i * i);
            i += 1;
        }

        return i - 1;
    }

    // Driver code
    public static void main(String[] args)
    {
        long X = 25;
        System.out.println(findMaxN(X));
    }
}

// This code contributed by Hemanth gadarla
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum N such that
# the sum of the squares of first N
# natural numbers is not more than X
def findMaxN(X):

    # To keep track of all squares in the series
    i = 1 

    # To count the number of squares used to
    count = 0 

    # Reach N
    N = X

    while (N >= (i * i)):

        # Subtract the square of current number
        N -= (i * i)

        # Increment count
        count += 1

        # increment i for next square number
        i += 1

    return count

# Driver code
X = 25
print(findMaxN(X))

# This code is contributed by subhammahato348
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to return the maximum N such that
// the sum of the squares of first N
// natural numbers is not more than X
static long findMaxN(long X)
{
    long N = X;

    // To keep track of the squares
    // of consecutive numbers
    int i = 1;

    while (N >= (i * i))
    {
        N -= (i * i);
        i += 1;
    }
    return i - 1;
}

// Driver code
public static void Main()
{
    long X = 25;

    Console.Write(findMaxN(X));
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum N such that
// the sum of the squares of first N
// natural numbers is not more than X
function findMaxN(X)
{

    // To keep track of all squares
    // in the series
    var i = 1;

    // To count the number of squares
    // used to reach N
    var count = 0;
    var N = X;

    while (N >= (i * i))
    {

        // Subtract the square of current number
        N -= (i * i);

        // Increment count
        count += 1;

        // Increment i for next square number
        i += 1;
    }
    return count;
}

// Driver code
var X = 25;

document.write(findMaxN(X));

// This code is contributed by noob2000

</script>
```

**Output**

```
3
```