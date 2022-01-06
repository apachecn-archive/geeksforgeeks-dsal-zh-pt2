# 欧拉全能值比自身小一的元素计数

> 原文:[https://www . geesforgeks . org/count-of-elements-having-Euler-total-value-one-behind/](https://www.geeksforgeeks.org/count-of-elements-having-eulers-totient-value-one-less-than-itself/)

给定一个由 **N** 个整数组成的数组**arr【】**，以及一个范围 **L** 到 **R** ，任务是找出数组中从索引 **L 到 R** 的元素总数，满足以下条件:

> ![F(arr[i]) = arr[i] - 1  ](img/7699fa5d9baab46bb7fff5aacff032c8.png "Rendered by QuickLaTeX.com")
> 
> 其中 **F(x)** 为[欧拉全能性函数](https://www.geeksforgeeks.org/eulers-totient-function/)。

**示例:**

> **输入:** arr[] = {2，4，5，8}，L = 1，R = 3
> **输出:** 2
> **说明:**
> 这里在给定的范围内，F(2) = 1 和(2–1)= 1。类似地，F(5) = 4 和(5–1)= 4。
> 因此满足条件的指标总数为 2。
> **输入:** arr[] = {9，3，4，6，8}，L = 3，R = 5
> **输出:** 0
> **说明:**
> 给定范围内没有满足给定条件的元素。
> 所以总计数为 0。

**天真方法:**解决这个问题的天真方法是迭代数组的所有元素，检查当前元素的欧拉全能值是否比自身小一。如果是，则增加计数。
***时间复杂度:** O(N * sqrt(N))*
***辅助空间:** O(1)*
**高效进场:**

> [输入 n 的欧拉全能性函数](https://www.geeksforgeeks.org/eulers-totient-function/) F(n)是{1，2，3，…，n}中与 n 相对素数的数的计数，即[与 n 的最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)为 1 的数。

1.  如果我们观察，我们可以注意到上述给定条件仅由[素数](https://www.geeksforgeeks.org/prime-numbers/)满足。
2.  所以，我们需要做的就是计算给定范围内素数的总数。
3.  我们将使用厄拉多塞的[筛来有效地计算素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
4.  此外，我们将预先计算计数数组中素数的数量。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

long long prime[1000001] = { 0 };

// Seiev of Erotosthenes method to
// compute all primes
void seiveOfEratosthenes()
{

    for (int i = 2; i < 1000001;
         i++) {
        prime[i] = 1;
    }

    for (int i = 2; i * i < 1000001;
         i++) {

        // If current number is
        // marked prime then mark
        // its multiple as non-prime
        if (prime[i] == 1) {
            for (int j = i * i;
                 j < 1000001; j += i) {
                prime[j] = 0;
            }
        }
    }
}

// Function to count the number
// of element satisfying the condition
void CountElements(int arr[],
                   int n, int L,
                   int R)
{
    seiveOfEratosthenes();

    long long countPrime[n + 1]
        = { 0 };

    // Compute the number of primes
    // in count prime array
    for (int i = 1; i <= n; i++) {
        countPrime[i] = countPrime[i - 1]
                        + prime[arr[i - 1]];
    }

    // Print the number of elements
    // satisfying the condition
    cout << countPrime[R]
                - countPrime[L - 1]
         << endl;

    return;
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 2, 4, 5, 8 };

    // Size of the array
    int N = sizeof(arr) / sizeof(int);
    int L = 1, R = 3;

    // Function Call
    CountElements(arr, N, L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int prime[] = new int[1000001];

// Seiev of Erotosthenes method to
// compute all primes
static void seiveOfEratosthenes()
{
    for(int i = 2; i < 1000001; i++)
    {
       prime[i] = 1;
    }

    for(int i = 2; i * i < 1000001; i++)
    {

       // If current number is
       // marked prime then mark
       // its multiple as non-prime
       if (prime[i] == 1)
       {
           for(int j = i * i;
                   j < 1000001; j += i)
           {
              prime[j] = 0;
           }
       }
    }
}

// Function to count the number
// of element satisfying the condition
static void CountElements(int arr[], int n,
                          int L, int R)
{
    seiveOfEratosthenes();

    int countPrime[] = new int[n + 1];

    // Compute the number of primes
    // in count prime array
    for(int i = 1; i <= n; i++)
    {
       countPrime[i] = countPrime[i - 1] +
                        prime[arr[i - 1]];
    }

    // Print the number of elements
    // satisfying the condition
    System.out.print(countPrime[R] -
                     countPrime[L - 1] + "\n");

    return;
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 2, 4, 5, 8 };

    // Size of the array
    int N = arr.length;
    int L = 1, R = 3;

    // Function Call
    CountElements(arr, N, L, R);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach
prime = [0] * (1000001)

# Seiev of Erotosthenes method to
# compute all primes
def seiveOfEratosthenes():

    for i in range(2, 1000001):
        prime[i] = 1

    i = 2
    while(i * i < 1000001):

        # If current number is
        # marked prime then mark
        # its multiple as non-prime
        if (prime[i] == 1):
            for j in range(i * i, 1000001, i):
                prime[j] = 0

        i += 1

# Function to count the number
# of element satisfying the condition
def CountElements(arr, n, L, R):

    seiveOfEratosthenes()

    countPrime = [0] * (n + 1)

    # Compute the number of primes
    # in count prime array
    for i in range(1, n + 1):
        countPrime[i] = (countPrime[i - 1] +
                          prime[arr[i - 1]])

    # Print the number of elements
    # satisfying the condition
    print(countPrime[R] -
          countPrime[L - 1])

    return

# Driver Code

# Given array
arr = [ 2, 4, 5, 8 ]

# Size of the array
N = len(arr)
L = 1
R = 3

# Function call
CountElements(arr, N, L, R)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
class GFG{

static int []prime = new int[1000001];

// Seiev of Erotosthenes method to
// compute all primes
static void seiveOfEratosthenes()
{
    for(int i = 2; i < 1000001; i++)
    {
        prime[i] = 1;
    }

    for(int i = 2; i * i < 1000001; i++)
    {

        // If current number is
        // marked prime then mark
        // its multiple as non-prime
        if (prime[i] == 1)
        {
            for(int j = i * i;
                    j < 1000001; j += i)
            {
                prime[j] = 0;
            }
        }
    }
}

// Function to count the number
// of element satisfying the condition
static void CountElements(int []arr, int n,
                          int L, int R)
{
    seiveOfEratosthenes();

    int []countPrime = new int[n + 1];

    // Compute the number of primes
    // in count prime array
    for(int i = 1; i <= n; i++)
    {
        countPrime[i] = countPrime[i - 1] +
                         prime[arr[i - 1]];
    }

    // Print the number of elements
    // satisfying the condition
    Console.Write(countPrime[R] -
                  countPrime[L - 1] + "\n");

    return;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 2, 4, 5, 8 };

    // Size of the array
    int N = arr.Length;
    int L = 1, R = 3;

    // Function Call
    CountElements(arr, N, L, R);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

let prime = new Uint8Array(1000001);

// Seiev of Erotosthenes method to
// compute all primes
function seiveOfEratosthenes()
{

    for (let i = 2; i < 1000001;
        i++) {
        prime[i] = 1;
    }

    for (let i = 2; i * i < 1000001;
        i++) {

        // If current number is
        // marked prime then mark
        // its multiple as non-prime
        if (prime[i] == 1) {
            for (let j = i * i;
                j < 1000001; j += i) {
                prime[j] = 0;
            }
        }
    }
}

// Function to count the number
// of element satisfying the condition
function CountElements(arr, n, L, R)
{
    seiveOfEratosthenes();

    countPrime = new Uint8Array(n + 1);

    // Compute the number of primes
    // in count prime array
    for (let i = 1; i <= n; i++) {
        countPrime[i] = countPrime[i - 1]
                        + prime[arr[i - 1]];
    }

    // Print the number of elements
    // satisfying the condition
    document.write((countPrime[R]
                - countPrime[L - 1])
        + "<br>");

    return;
}

// Driver Code

    // Given array
    let arr = [ 2, 4, 5, 8 ];

    // Size of the array
    let N = arr.length;
    let L = 1, R = 3;

    // Function Call
    CountElements(arr, N, L, R);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
2
```

**时间复杂度:***O(N * log(logN))*
T5】辅助空间: *O(N)*