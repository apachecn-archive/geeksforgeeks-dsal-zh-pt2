# 长度为 N 的不同排列的计数，按位“与”为零

> 原文:[https://www . geesforgeks . org/count-of-distinct-置换-length-n-having-bitwise-and-as-zero/](https://www.geeksforgeeks.org/count-of-distinct-permutations-of-length-n-having-bitwise-and-as-zero/)

给定一个整数 **N** 。，任务是找到长度为 **N** 的**不同**排列的数量，使得每个排列的[位](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值为**零**。

**示例:**

> **输入:** N = 1
> **输出:** 0
> **说明:**长度 1 的排列只有一个:[1]，它的按位 and 是 1。
> 
> **输入:** N = 3
> **输出:** 6
> **解释:**长度 N 按位与为 0 的排列为:[1，2，3]，[1，3，2]，[2，1，3]，[3，1，2]，[2，3，1]，[3，2，1]。

**方法:**任务可以通过观察来解决。可以观察到，如果一个数是 2 的**次幂**，比如说“ **x** ，那么 **x & (x-1)** 的按位“与”总是**零。**长度**大于**的所有排列，都有**位“与”**作为**零**，对于 **N = 1** ，不同排列的计数为 **0** 。因此，所需的计数等于可能排列的数量，即 **N！**

以下是上述方法的实施–

## C++

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate factorial
// of a number
long long int fact(long long N)
{
    long long int ans = 1;
    for (int i = 2; i <= N; i++)
        ans *= i;

    return ans;
}

// Function to find distinct no of
// permutations having bitwise and (&)
// equals to 0
long long permutation_count(long long n)
{
    // corner case
    if (n == 1)
        return 0;

    return fact(n);
}

// Driver code
int main()
{

    long long N = 3;
    cout << permutation_count(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to calculate factorial
// of a number
static long fact( long N)
{
    long  ans = 1;
    for (int i = 2; i <= N; i++)
        ans *= i;

    return ans;
}

// Function to find distinct no of
// permutations having bitwise and (&)
// equals to 0
static long  permutation_count(long n)
{

    // corner case
    if (n == 1)
        return 0;

    return fact(n);
}

    public static void main (String[] args) {
       long N = 3;
     System.out.println(permutation_count(N));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the
# above approach

# Function to calculate factorial
# of a number
def fact(N):

    ans = 1
    for i in range(2,  N + 1):
        ans *= i

    return ans

# Function to find distinct no of
# permutations having bitwise and (&)
# equals to 0
def permutation_count(n):

    # corner case
    if (n == 1):
        return 0

    return fact(n)

# Driver code
if __name__ == "__main__":

    N = 3
    print(permutation_count(N))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the
// above approach
using System;

class GFG
{
// Function to calculate factorial
// of a number
static long fact(long N)
{
    long ans = 1;
    for (int i = 2; i <= N; i++)
        ans *= i;

    return ans;
}

// Function to find distinct no of
// permutations having bitwise and (&)
// equals to 0
static long permutation_count(long n)
{
    // corner case
    if (n == 1)
        return 0;

    return fact(n);
}

// Driver code
public static void Main()
{

    long N = 3;
    Console.Write(permutation_count(N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the
// above approach

// Function to calculate factorial
// of a number
function fact(N)
{
    let ans = 1;
    for (let i = 2; i <= N; i++)
        ans *= i;

    return ans;
}

// Function to find distinct no of
// permutations having bitwise and (&)
// equals to 0
function permutation_count(n)
{
    // corner case
    if (n == 1)
        return 0;

    return fact(n);
}

// Driver code
let N = 3;
document.write(permutation_count(N));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
6
```

***时间复杂度*** : O(N)
***辅助空间*** : O(1)