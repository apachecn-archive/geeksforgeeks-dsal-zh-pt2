# 计算一个数的所有完美除数

> 原文:[https://www . geesforgeks . org/count-perfect-dividers-number/](https://www.geeksforgeeks.org/count-perfect-divisors-number/)

给定一个数 n，计算 n 的完全除数。完全除数是某个整数的平方的除数。例如，8 的完美除数是 4。

**示例:**

```
Input  : n = 16 
Output : 3
Explanation : There are only 5 divisor of 16:
1, 2, 4, 8, 16\. Only three of them are perfect 
squares: 1, 4, 16\. Therefore the answer is 3

Input  : n = 7
Output : 1

```

**天真的做法**

蛮力就是[找出一个数的所有除数](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)。计算所有完美平方的除数。

## C++

```
// Below is C++ code to count total perfect Divisors
#include<bits/stdc++.h>
using namespace std;

// Utility function to check perfect square number
bool isPerfectSquare(int n)
{
    int sq = (int) sqrt(n);
    return (n == sq * sq);
}

// Returns count all perfect divisors of n
int countPerfectDivisors(int n)
{
    // Initialize result
    int count = 0;

    // Consider every number that can be a divisor
    // of n
    for (int i=1; i*i <= n; ++i)
    {
        // If i is a divisor
        if (n%i == 0)
        {
            if (isPerfectSquare(i))
                ++count;
            if (n/i != i && isPerfectSquare(n/i))
                ++count;
        }
    }
    return count;
}

// Driver code
int main()
{
    int n = 16;

    cout << "Total perfect divisors of "
         << n << " = " << countPerfectDivisors(n) << "\n";

    n = 12;
    cout << "Total perfect divisors of "
         << n << " = " << countPerfectDivisors(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count
// total perfect Divisors
import java.io.*;

class GFG
{

// Utility function to check
// perfect square number
static boolean isPerfectSquare(int n)
{
    int sq = (int) Math.sqrt(n);
    return (n == sq * sq);
}

// Returns count all
// perfect divisors of n
static int countPerfectDivisors(int n)
{
    // Initialize result
    int count = 0;

    // Consider every number
    // that can be a divisor of n
    for (int i = 1; i * i <= n; ++i)
    {
        // If i is a divisor
        if (n % i == 0)
        {
            if (isPerfectSquare(i))
                ++count;
            if (n / i != i &&
                isPerfectSquare(n / i))
                ++count;
        }
    }
    return count;
}

// Driver code
public static void main (String[] args)
{
    int n = 16;

    System.out.print("Total perfect " +
                   "divisors of " + n);
    System.out.println(" = " +
               countPerfectDivisors(n));

    n = 12;
    System.out.print("Total perfect " +
                   "divisors of " + n);
    System.out.println(" = " +
               countPerfectDivisors(n));
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python3 implementation of Naive method
# to count all perfect divisors

import math

def isPerfectSquare(x) :
    sq = (int)(math.sqrt(x))
    return (x == sq * sq)

# function to count all perfect divisors
def countPerfectDivisors(n) :

    # Initialize result
    cnt = 0

        # Consider every number that
        # can be a divisor of n
    for i in range(1, (int)(math.sqrt(n)) + 1) :

            # If i is a divisor
            if ( n % i == 0 ) :

                if isPerfectSquare(i):
                        cnt = cnt + 1
                if n/i != i and isPerfectSquare(n/i):
                        cnt = cnt + 1
    return cnt

# Driver program to test above function
print("Total perfect divisor of 16 = ",
    countPerfectDivisors(16))

print("Total perfect divisor of 12 = ",
    countPerfectDivisors(12))   

# This code is contributed by Saloni Gupta
```

## C#

```
// C# code to count
// total perfect Divisors
using System;

class GFG
{

// Utility function to check
// perfect square number
static bool isPerfectSquare(int n)
{
    int sq = (int) Math.Sqrt(n);
    return (n == sq * sq);
}

// Returns count all
// perfect divisors of n
static int countPerfectDivisors(int n)
{
    // Initialize result
    int count = 0;

    // Consider every number
    // that can be a divisor of n
    for (int i = 1;
             i * i <= n; ++i)
    {
        // If i is a divisor
        if (n % i == 0)
        {
            if (isPerfectSquare(i))
                ++count;
            if (n / i != i &&
                isPerfectSquare(n / i))
                ++count;
        }
    }
    return count;
}

// Driver code
static public void Main ()
{
    int n = 16;

    Console.Write("Total perfect " +
                "divisors of " + n);
    Console.WriteLine(" = " +
            countPerfectDivisors(n));

    n = 12;
    Console.Write("Total perfect " +
                "divisors of " + n);
    Console.WriteLine(" = " +
            countPerfectDivisors(n));
}
}

// This code is contributed
// by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to count
// total perfect Divisors

// function to check
// perfect square number
function isPerfectSquare($n)
{
    $sq = sqrt($n);
    return ($n == $sq * $sq);
}

// Returns count all
// perfect divisors of n
function countPerfectDivisors($n)
{

    // Initialize result
    $count = 0;

    // Consider every number
    // that can be a divisor
    // of n
    for ($i = 1; $i * $i <= $n; ++$i)
    {

        // If i is a divisor
        if ($n % $i == 0)
        {
            if (isPerfectSquare($i))
                ++$count;
            if ($n / $i != $i &&
                isPerfectSquare($n / $i))
                ++$count;
        }
    }
    return $count;
}

    // Driver Code
    $n = 16;
    echo "Total perfect divisors of ",
         $n, " = ", countPerfectDivisors($n), "\n";

    $n = 12;
    echo "Total perfect divisors of ",
         $n, " = ", countPerfectDivisors($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Utility function to check
// perfect square number
function isPerfectSquare(n)
{
    let sq = Math.sqrt(n);
    return (n == sq * sq);
}

// Returns count all
// perfect divisors of n
function countPerfectDivisors(n)
{

    // Initialize result
    let count = 0;

    // Consider every number
    // that can be a divisor of n
    for (let i = 1; i * i <= n; ++i)
    {

        // If i is a divisor
        if (n % i == 0)
        {
            if (isPerfectSquare(i))
                ++count;
            if (n / i != i &&
                isPerfectSquare(n / i))
                ++count;
        }
    }
    return count;
}

// Driver Code
    let n = 16;

    document.write("Total perfect " +
                   "divisors of " + n);
    document.write(" = " +
               countPerfectDivisors(n) + "<br/>");
    n = 12;
    document.write("Total perfect " +
                   "divisors of " + n);
    document.write(" = " +
               countPerfectDivisors(n));

// This code is contributed by chinmoy1997pal.
</script>
```

```
Output:
Total Perfect divisors of 16 = 3
Total Perfect divisors of 12 = 2
```

**时间复杂度:** O(sqrt(n))
**辅助空间:** O(1)

**高效方法(用于大量查询)**

这个想法是基于厄拉多塞的[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)。如果有大量查询，这种方法是有益的。以下是找到 n 个数以内所有完美除数的算法。

1.  创建从 1 到 n 的 n 个连续整数的列表:(1，2，3，…，n)
2.  最初，假设 d 是 2，第一个除数
3.  从 4(2 的平方)开始，将 perfectDiv[]数组中所有 4 的倍数增加 1，因为所有这些倍数都包含 4 作为完美除数。这些数字将是 4d、8d、12d 等
4.  对所有其他号码重复第 3 步<sup>和第 3 步</sup>。perfectDiv[]的最终数组将包含从 1 到 n 的所有完美除数

下面是上述步骤的实现。

## C++

```
// Below is C++ code to count total perfect
// divisors
#include<bits/stdc++.h>
using namespace std;
#define MAX 100001

int perfectDiv[MAX];

// Pre-compute counts of all perfect divisors
// of all numbers upto MAX.
void precomputeCounts()
{
    for (int i=1; i*i < MAX; ++i)
    {
        // Iterate through all the multiples of i*i
        for (int j=i*i; j < MAX; j += i*i)

            // Increment all such multiples by 1
            ++perfectDiv[j];
    }
}

// Returns count of perfect divisors of n.
int countPerfectDivisors(int n)
{
    return perfectDiv[n];
}

// Driver code
int main()
{
    precomputeCounts();

    int n = 16;
    cout << "Total perfect divisors of "
         << n << " = " << countPerfectDivisors(n) << "\n";

    n = 12;
    cout << "Total perfect divisors of "
         << n << " = " << countPerfectDivisors(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count total perfect
// divisors
class GFG
{

static int MAX = 100001;

static int[] perfectDiv = new int[MAX];

// Pre-compute counts of all perfect divisors
// of all numbers upto MAX.
static void precomputeCounts()
{
    for (int i = 1; i * i < MAX; ++i)
    {
        // Iterate through all the multiples of i*i
        for (int j = i * i; j < MAX; j += i * i)

            // Increment all such multiples by 1
            ++perfectDiv[j];
    }
}

// Returns count of perfect divisors of n.
static int countPerfectDivisors(int n)
{
    return perfectDiv[n];
}

// Driver code
public static void main (String[] args)
{
    precomputeCounts();

    int n = 16;
    System.out.println("Total perfect divisors of " +
                    n + " = " + countPerfectDivisors(n));

    n = 12;
    System.out.println("Total perfect divisors of " +
                        n + " = " + countPerfectDivisors(n));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Below is Python3 code to count total perfect
# divisors
MAX = 100001

perfectDiv= [0]*MAX

# Pre-compute counts of all perfect divisors
# of all numbers upto MAX.
def precomputeCounts():

    i=1
    while i*i < MAX:

        # Iterate through all the multiples of i*i
        for j in range(i*i,MAX,i*i):

            # Increment all such multiples by 1
            perfectDiv[j] += 1
        i += 1

# Returns count of perfect divisors of n.
def countPerfectDivisors( n):

    return perfectDiv[n]

# Driver code
if __name__ == "__main__":

    precomputeCounts()

    n = 16
    print ("Total perfect divisors of "
         , n , " = " ,countPerfectDivisors(n))

    n = 12
    print ( "Total perfect divisors of "
         ,n ," = " ,countPerfectDivisors(n))
```

## C#

```
// C# code to count total perfect
// divisors
using System;
class GFG
{

static int MAX = 100001;

static int[] perfectDiv = new int[MAX];

// Pre-compute counts of all perfect
// divisors of all numbers upto MAX.
static void precomputeCounts()
{
    for (int i = 1; i * i < MAX; ++i)
    {
        // Iterate through all the multiples of i*i
        for (int j = i * i; j < MAX; j += i * i)

            // Increment all such multiples by 1
            ++perfectDiv[j];
    }
}

// Returns count of perfect divisors of n.
static int countPerfectDivisors(int n)
{
    return perfectDiv[n];
}

// Driver code
public static void Main()
{
    precomputeCounts();

    int n = 16;
    Console.WriteLine("Total perfect divisors of " + n +
                       " = " + countPerfectDivisors(n));

    n = 12;
    Console.WriteLine("Total perfect divisors of " + n +
                       " = " + countPerfectDivisors(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Below is PHP code to count total
// perfect divisors

$MAX = 10001;

$perfectDiv = array_fill(0, $MAX, 0);

// Pre-compute counts of all perfect
// divisors of all numbers upto MAX.
function precomputeCounts()
{
    global $MAX, $perfectDiv;
    for ($i = 1; $i * $i < $MAX; ++$i)
    {
        // Iterate through all the multiples
        // of i*i
        for ($j = $i * $i;
             $j < $MAX; $j += $i * $i)

            // Increment all such multiples by 1
            ++$perfectDiv[$j];
    }
}

// Returns count of perfect divisors of n.
function countPerfectDivisors($n)
{
    global $perfectDiv;
    return $perfectDiv[$n];
}

// Driver code
precomputeCounts();

$n = 16;
echo "Total perfect divisors of " . $n .
     " = " . countPerfectDivisors($n) . "\n";

$n = 12;
echo "Total perfect divisors of " . $n .
     " = " . countPerfectDivisors($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript code to count total perfect
// divisors
let MAX = 100001;;
let perfectDiv = new Array(MAX);
for(let i = 0; i < MAX; i++)
{
    perfectDiv[i] = 0;
}

// Pre-compute counts of all perfect divisors
// of all numbers upto MAX.
function precomputeCounts()
{
    for(let i = 1; i * i < MAX; ++i)
    {

        // Iterate through all the multiples of i*i
        for(let j = i * i; j < MAX; j += i * i)

            // Increment all such multiples by 1
            ++perfectDiv[j];
    }
}

// Returns count of perfect divisors of n.
function countPerfectDivisors(n)
{
    return perfectDiv[n];
}

// Driver code
precomputeCounts();

let n = 16;
document.write("Total perfect divisors of " +
               n + " = " +
               countPerfectDivisors(n) + "<br>");

n = 12;
document.write("Total perfect divisors of " +
               n + " = " +
               countPerfectDivisors(n));

// This code is contributed by rag2127

</script>
```

**输出:**

```
Total Perfect divisors of 16 = 3
Total Perfect divisors of 12 = 2
```

**时间复杂度:** O(MAX * log(log (MAX)))
**辅助空间:** O(MAX)

本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。