# 满足给定方程

的斐波那契对的计数

> 原文:[https://www . geeksforgeeks . org/满足给定等式的斐波那契对的计数/](https://www.geeksforgeeks.org/count-of-fibonacci-pairs-which-satisfy-the-given-equation/)

给定一个包含正整数 **Q** 和两个数字 **A** 和 **B** 的数组 **arr[]** ，任务是为数组 **arr** 中的每个数字 **N** 找到有序对 **(x，y)** 的数量，这样:

*   它们满足方程 **A*x + B*y = N** ，并且
*   x 和 y 是[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。

**例:**

> **输入:** arr[] = {15，25}，A = 1，B = 2
> **输出:** 2 1
> **解释:**
> 对于 15:有 2 个有序对(x，y) = (13，1) & (5，5)这样 1*x + 2*y = 15
> 对于 25:只有一个有序对(x，y) = (21，2)这样 1*x + 2*y

**天真方法:**这个问题的天真方法是:

*   对于数组中的每个查询 **N** ，计算[斐波那契数直到 N](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)
*   如果满足给定条件 **A*x + B*y = N** ，从这个斐波那契数中检查所有可能的对。

***时间复杂度:** O(N <sup>2</sup> )*
**高效进场:**

*   预计算所有斐波那契数，并将其存储在数组中。
*   现在，迭代斐波那契数和所有可能的组合，为范围[1，max(arr)]中的每个数更新有序对的数量，并将其存储在另一个数组中。
*   现在，对于每个查询 N，有序对的数量可以在恒定时间内得到回答。

以下是上述方法的实现:

## C++

```
// C++ program to find the count of
// Fibonacci pairs (x, y) which
// satisfy the equation Ax+By=N

#include <bits/stdc++.h>
#define size 10001
using namespace std;

// Array to store the Fibonacci numbers
long long fib[100010];

// Array to store the number of ordered pairs
int freq[100010];

// Function to find if a number
// is a perfect square
bool isPerfectSquare(int x)
{
    int s = sqrt(x);
    return (s * s == x);
}

// Function that returns 1
// if N is non-fibonacci number else 0
int isFibonacci(int n)
{
    // N is Fibinacci if one of
    // 5*n*n + 4 or 5*n*n - 4 or both
    // are perferct square
    if (isPerfectSquare(5 * n * n + 4)
        || isPerfectSquare(5 * n * n - 4))
        return 1;
    return 0;
}

// Function to store the fibonacci numbers
// and their frequency in form a * x + b * y
void compute(int a, int b)
{
    // Storing the Fibonacci numbers
    for (int i = 1; i < 100010; i++) {
        fib[i] = isFibonacci(i);
    }

    // For loop to find all the possible
    // combinations of the Fibonacci numbers
    for (int x = 1; x < 100010; x++) {
        for (int y = 1; y < size; y++) {

            // Finding the number of ordered pairs
            if (fib[x] == 1 && fib[y] == 1
                && a * x + b * y < 100010) {
                freq[a * x + b * y]++;
            }
        }
    }
}

// Driver code
int main()
{
    int Q = 2, A = 5, B = 10;
    compute(A, B);
    int arr[Q] = { 50, 150 };

    // Find the ordered pair for every query
    for (int i = 0; i < Q; i++) {
        cout << freq[arr[i]] << " ";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of
// Fibonacci pairs (x, y) which
// satisfy the equation Ax+By=N
class GFG{

static final int size = 10001;

// Array to store the Fibonacci numbers
static long []fib = new long[100010];

// Array to store the number of ordered pairs
static int []freq = new int[100010];

// Function to find if a number
// is a perfect square
static boolean isPerfectSquare(int x)
{
    int s = (int) Math.sqrt(x);
    return (s * s == x);
}

// Function that returns 1
// if N is non-fibonacci number else 0
static int isFibonacci(int n)
{
    // N is Fibinacci if one of
    // 5*n*n + 4 or 5*n*n - 4 or both
    // are perferct square
    if (isPerfectSquare(5 * n * n + 4)
        || isPerfectSquare(5 * n * n - 4))
        return 1;
    return 0;
}

// Function to store the fibonacci numbers
// and their frequency in form a * x + b * y
static void compute(int a, int b)
{
    // Storing the Fibonacci numbers
    for (int i = 1; i < 100010; i++) {
        fib[i] = isFibonacci(i);
    }

    // For loop to find all the possible
    // combinations of the Fibonacci numbers
    for (int x = 1; x < 100010; x++) {
        for (int y = 1; y < size; y++) {

            // Finding the number of ordered pairs
            if (fib[x] == 1 && fib[y] == 1
                && a * x + b * y < 100010) {
                freq[a * x + b * y]++;
            }
        }
    }
}

// Driver code
public static void main(String[] args)
{
    int Q = 2, A = 5, B = 10;
    compute(A, B);
    int arr[] = { 50, 150 };

    // Find the ordered pair for every query
    for (int i = 0; i < Q; i++) {
        System.out.print(freq[arr[i]]+ " ");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python program to find the count of
# Fibonacci pairs (x, y) which
# satisfy the equation Ax+By=N
import math
size = 101

# Array to store the Fibonacci numbers
fib = [0]*100010

# Array to store the number of ordered pairs
freq = [0]*(100010)

# Function to find if a number
# is a perfect square
def isPerfectSquare(x):
    s = int(math.sqrt(x))

    return (s * s) == x

# Function that returns 1
# if N is non-fibonacci number else 0
def isFibonacci(n):

    # N is Fibinacci if one of
    # 5*n*n + 4 or 5*n*n - 4 or both
    # are perferct square
    if (isPerfectSquare(5 * n * n + 4) or isPerfectSquare(5 * n * n - 4)):
        return 1;
    return 0;

# Function to store the fibonacci numbers
# and their frequency in form a * x + b * y
def compute( a, b):

    # Storing the Fibonacci numbers
    for i in range(1, 100010):
        fib[i] = isFibonacci(i)

    # For loop to find all the possible
    # combinations of the Fibonacci numbers
    for x in range(1, 100010):
        for y in range(1, size):

            # Finding the number of ordered pairs
            if (fib[x] == 1 and fib[y] == 1 and a * x + b * y < 100010):
                freq[a * x + b * y] += 1

# Driver code

Q = 2
A = 5
B = 10
compute(A, B);
arr = [ 50, 150 ]

# Find the ordered pair for every query
for i in range(Q):
        print(freq[arr[i]], end=" ")

# This code is contributed by ANKITKUMAR34
```

## C#

```
// C# program to find the count of
// Fibonacci pairs (x, y) which
// satisfy the equation Ax+By=N
using System;

class GFG{

static readonly int size = 10001;

// Array to store the Fibonacci numbers
static long []fib = new long[100010];

// Array to store the number of ordered pairs
static int []freq = new int[100010];

// Function to find if a number
// is a perfect square
static bool isPerfectSquare(int x)
{
    int s = (int) Math.Sqrt(x);
    return (s * s == x);
}

// Function that returns 1
// if N is non-fibonacci number else 0
static int isFibonacci(int n)
{
    // N is Fibinacci if one of
    // 5*n*n + 4 or 5*n*n - 4 or both
    // are perferct square
    if (isPerfectSquare(5 * n * n + 4)
        || isPerfectSquare(5 * n * n - 4))
        return 1;
    return 0;
}

// Function to store the fibonacci numbers
// and their frequency in form a * x + b * y
static void compute(int a, int b)
{
    // Storing the Fibonacci numbers
    for (int i = 1; i < 100010; i++) {
        fib[i] = isFibonacci(i);
    }

    // For loop to find all the possible
    // combinations of the Fibonacci numbers
    for (int x = 1; x < 100010; x++) {
        for (int y = 1; y < size; y++) {

            // Finding the number of ordered pairs
            if (fib[x] == 1 && fib[y] == 1
                && a * x + b * y < 100010) {
                freq[a * x + b * y]++;
            }
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    int Q = 2, A = 5, B = 10;
    compute(A, B);
    int []arr = { 50, 150 };

    // Find the ordered pair for every query
    for (int i = 0; i < Q; i++) {
        Console.Write(freq[arr[i]]+ " ");
    }
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find the count of
// Fibonacci pairs (x, y) which
// satisfy the equation Ax+By=N
var size = 10001

// Array to store the Fibonacci numbers
var fib = Array(100010).fill(0);

// Array to store the number of ordered pairs
var freq = Array(100010).fill(0);

// Function to find if a number
// is a perfect square
function isPerfectSquare(x)
{
    var s = parseInt(Math.sqrt(x));
    return (s * s == x);
}

// Function that returns 1
// if N is non-fibonacci number else 0
function isFibonacci(n)
{

    // N is Fibinacci if one of
    // 5*n*n + 4 or 5*n*n - 4 or both
    // are perferct square
    if (isPerfectSquare(5 * n * n + 4)
        || isPerfectSquare(5 * n * n - 4))
        return 1;
    return 0;
}

// Function to store the fibonacci numbers
// and their frequency in form a * x + b * y
function compute(a, b)
{

    // Storing the Fibonacci numbers
    for (var i = 1; i < 100010; i++)
    {
        fib[i] = isFibonacci(i);
    }

    // For loop to find all the possible
    // combinations of the Fibonacci numbers
    for (var x = 1; x < 100010; x++)
    {
        for (var y = 1; y < size; y++)
        {

            // Finding the number of ordered pairs
            if (fib[x] == 1 && fib[y] == 1
                && a * x + b * y < 100010)
            {
                freq[a * x + b * y]++;
            }
        }
    }
}

// Driver code
var Q = 2, A = 5, B = 10;
compute(A, B);
var arr = [ 50, 150 ];

// Find the ordered pair for every query
for (var i = 0; i < Q; i++)
{
    document.write(freq[arr[i]] + " ");
}

// This code is contributed by rutvik_56.

</script>
```

**Output:** 

```
1 0
```

时间复杂度:0(大小+ 100010)

辅助空间:0(尺寸+ 100010)