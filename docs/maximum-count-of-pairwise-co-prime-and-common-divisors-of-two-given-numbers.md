# 两个给定数的成对同素和公约数的最大计数

> 原文:[https://www . geeksforgeeks . org/两个给定数的最大成对同素和公约数/](https://www.geeksforgeeks.org/maximum-count-of-pairwise-co-prime-and-common-divisors-of-two-given-numbers/)

给定两个数 **{N，M}** 的对**arr【】**的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，任务是为每对 **N** 和 **M** 找到[公约数的最大计数，使得公约数之间的每对都是同素的。](https://www.geeksforgeeks.org/common-divisors-of-two-numbers/)

> 一个数 **x** 是 **N** 和 **M** if、 **N%x = 0** 和 **M%x = 0** 的公约数。
> 如果两个数的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)为 1，则这两个数是同素的。

**示例:**

> **输入:** arr[][] = {{12，18}，{420，660}}
> **输出:** 3 4
> **解释:**
> 对于对(12，18):
> {1，2，3}是 12 和 18 的公约数，并且是成对的同素数。
> 对于对(420，660):
> {1，2，3，5}是 12 和 18 的公约数，并且是成对的同素。
> **输入:** arr[][] = {{8，18}，{20，66}}
> **输出:** 2 2

**逼近:**T2 N 和 **M** 的最大公约数，使得它们之间所有对的 **GCD** 始终为 **1** 为 1， **N 和 M** 的所有公约数为 1。要计算所有常见的质因数，其思路是找出给定两个数的 GCD(比如 **G** )，然后计算该数的[质因数个数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/) **G** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the gcd of
// two numbers
int gcd(int x, int y)
{
    if (x % y == 0)
        return y;
    else
        return gcd(y, x % y);
}

// Function to of pairwise co-prime
// and common divisors of two numbers
int countPairwiseCoprime(int N, int M)
{
    // Initialize answer with 1,
    // to include 1 in the count
    int answer = 1;

    // Count of primes of gcd(N, M)
    int g = gcd(N, M);
    int temp = g;

    // Finding prime factors of gcd
    for (int i = 2; i * i <= g; i++) {

        // Increment count if it is
        // divisible by i
        if (temp % i == 0) {
            answer++;

            while (temp % i == 0)
                temp /= i;
        }
    }
    if (temp != 1)
        answer++;

    // Return the total count
    return answer;
}

void countCoprimePair(int arr[][2], int N)
{

    // Function Call for each pair
    // to calculate the count of
    // pairwise co-prime divisors
    for (int i = 0; i < N; i++) {
        cout << countPairwiseCoprime(arr[i][0],
                                     arr[i][1])
             << ' ';
    }
}

// Driver Code
int main()
{
    // Given array of pairs
    int arr[][2] = { { 12, 18 }, { 420, 660 } };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countCoprimePair(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the gcd of
// two numbers
static int gcd(int x, int y)
{
    if (x % y == 0)
        return y;
    else
        return gcd(y, x % y);
}

// Function to of pairwise co-prime
// and common divisors of two numbers
static int countPairwiseCoprime(int N, int M)
{
    // Initialize answer with 1,
    // to include 1 in the count
    int answer = 1;

    // Count of primes of gcd(N, M)
    int g = gcd(N, M);
    int temp = g;

    // Finding prime factors of gcd
    for (int i = 2; i * i <= g; i++)
    {

        // Increment count if it is
        // divisible by i
        if (temp % i == 0)
        {
            answer++;

            while (temp % i == 0)
                temp /= i;
        }
    }
    if (temp != 1)
        answer++;

    // Return the total count
    return answer;
}

static void countCoprimePair(int arr[][], int N)
{

    // Function Call for each pair
    // to calculate the count of
    // pairwise co-prime divisors
    for (int i = 0; i < N; i++)
    {
        System.out.print(countPairwiseCoprime(arr[i][0],
                                               arr[i][1]) + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    // Given array of pairs
    int arr[][] = { { 12, 18 }, { 420, 660 } };
    int N = arr.length;

    // Function Call
    countCoprimePair(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the gcd of
# two numbers
def gcd(x, y):
    if (x % y == 0):
        return y
    else:
        return gcd(y, x % y)

# Function to of pairwise co-prime
# and common divisors of two numbers
def countPairwiseCoprime(N, M):

    # Initialize answer with 1,
    # to include 1 in the count
    answer = 1

    # Count of primes of gcd(N, M)
    g = gcd(N, M)
    temp = g

    # Finding prime factors of gcd
    for i in range(2, g + 1):

        if i * i > g:
            break

        # Increment count if it is
        # divisible by i
        if (temp % i == 0) :
            answer += 1

            while (temp % i == 0):
                temp //= i

    if (temp != 1):
        answer += 1

    # Return the total count
    return answer

def countCoprimePair(arr, N):

    # Function Call for each pair
    # to calculate the count of
    # pairwise co-prime divisors
    for i in range(N):
        print(countPairwiseCoprime(arr[i][0],
                                   arr[i][1]),
                                     end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array of pairs
    arr= [ [ 12, 18 ], [ 420, 660 ] ]
    N = len(arr)

    # Function Call
    countCoprimePair(arr, N)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the gcd of
// two numbers
static int gcd(int x, int y)
{
    if (x % y == 0)
        return y;
    else
        return gcd(y, x % y);
}

// Function to of pairwise co-prime
// and common divisors of two numbers
static int countPairwiseCoprime(int N, int M)
{
    // Initialize answer with 1,
    // to include 1 in the count
    int answer = 1;

    // Count of primes of gcd(N, M)
    int g = gcd(N, M);
    int temp = g;

    // Finding prime factors of gcd
    for (int i = 2; i * i <= g; i++)
    {

        // Increment count if it is
        // divisible by i
        if (temp % i == 0)
        {
            answer++;

            while (temp % i == 0)
                temp /= i;
        }
    }
    if (temp != 1)
        answer++;

    // Return the total count
    return answer;
}

static void countCoprimePair(int [,]arr, int N)
{

    // Function Call for each pair
    // to calculate the count of
    // pairwise co-prime divisors
    for (int i = 0; i < N; i++)
    {
        Console.Write(countPairwiseCoprime(arr[i, 0],
                                           arr[i, 1]) + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    // Given array of pairs
    int [,]arr = { { 12, 18 }, { 420, 660 } };
    int N = arr.GetLength(0);

    // Function Call
    countCoprimePair(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find the gcd of
// two numbers
function gcd(x, y)
{
    if (x % y == 0)
        return y;
    else
        return gcd(y, x % y);
}

// Function to of pairwise co-prime
// and common divisors of two numbers
function countPairwiseCoprime(N, M)
{
    // Initialize answer with 1,
    // to include 1 in the count
    let answer = 1;

    // Count of primes of gcd(N, M)
    let g = gcd(N, M);
    let temp = g;

    // Finding prime factors of gcd
    for (let i = 2; i * i <= g; i++)
    {

        // Increment count if it is
        // divisible by i
        if (temp % i == 0)
        {
            answer++;

            while (temp % i == 0)
                temp /= i;
        }
    }
    if (temp != 1)
        answer++;

    // Return the total count
    return answer;
}

function countCoprimePair(arr, N)
{

    // Function Call for each pair
    // to calculate the count of
    // pairwise co-prime divisors
    for (let i = 0; i < N; i++)
    {
        document.write(countPairwiseCoprime(arr[i][0],
                                               arr[i][1]) + " ");
    }
}

// Driver Code

   // Given array of pairs
    let arr = [[ 12, 18 ], [ 420, 660 ]];
    let N = arr.length;

    // Function Call
    countCoprimePair(arr, N);

</script>
```

**Output:** 

```
3 4
```

**时间复杂度:** *O(X*(sqrt(N) + sqrt(M))，其中 X 是对的数量，N & M 是 arr[]中的两对。*
**辅助空间:** *O(1)*