# 所需的最小素数，其和等于 N

> 原文:[https://www . geeksforgeeks . org/需要最小素数，这样它们的和等于 n/](https://www.geeksforgeeks.org/minimum-number-of-primes-required-such-that-their-sum-is-equal-to-n/)

给定一个大于 1 的正整数 **N** ，任务是求和等于给定 **N** 的[素数](https://www.geeksforgeeks.org/prime-numbers/)的最小计数。
**举例:**

> **输入:** N = 100
> **输出:** 2
> **说明:**
> 100 可以写成 2 个质数 97 和 3 的和。
> **输入:** N = 25
> **输出:** 3
> **说明:**
> 25 可以写成 3 个质数 11、11、3 的和。

**逼近:**
对于和为给定数 **N** 的素数的最小值，[素数](https://www.geeksforgeeks.org/prime-numbers/)必须尽可能大。以下是对上述问题陈述的观察:

*   **情况 1:** 如果数是素数，那么求和 **N** 所需的最小素数为 **1** 。
*   **情况 2:** 如果数是偶数，那么根据[哥德巴赫猜想](https://www.geeksforgeeks.org/program-for-goldbachs-conjecture-two-primes-with-given-sum/)对于每一个大于 2 的偶数可以表示为两个素数之和。因此求和 **N** 所需的最小素数是 **2** 。
*   **情况 3:** 如果数字是奇数:
    1.  如果 **(N-2)** 是素数，那么构成给定和 **N** 所需的最小素数是 **2** 。
    2.  否则，得出给定和 **N** 所需的最小素数是 **3** ，因为:

        ```
        As N is odd, then (N - 3) is even.
        Hence As per case 2:
        The minimum prime number required to make the sum (N-3) is 2.
        Therefore,
        The minimum prime number required to make the sum N is 3(2+1).
        ```

以下是步骤:

1.  使用[这篇](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)文章中讨论的方法，检查给定的数字 **N** 是否是素数。如果是，则打印 **1** 。
2.  否则根据上述情况，打印给定总和 **N** 所需的最小数量[素数](https://www.geeksforgeeks.org/prime-numbers/)。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if n is prime
bool isPrime(int n)
{
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}

// Function to count the minimum
// prime required for given sum N
void printMinCountPrime(int N)
{

    int minCount;

    // Case 1:
    if (isPrime(N)) {
        minCount = 1;
    }

    // Case 2:
    else if (N % 2 == 0) {
        minCount = 2;
    }

    // Case 3:
    else {

        // Case 3a:
        if (isPrime(N - 2)) {
            minCount = 2;
        }

        // Case 3b:
        else {
            minCount = 3;
        }
    }

    cout << minCount << endl;
}

// Driver Code
int main()
{
    int N = 100;

    // Function Call
    printMinCountPrime(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if n is prime
static boolean isPrime(int n)
{
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}

// Function to count the minimum
// prime required for given sum N
static void printMinCountPrime(int N)
{

    int minCount;

    // Case 1:
    if (isPrime(N)) {
        minCount = 1;
    }

    // Case 2:
    else if (N % 2 == 0) {
        minCount = 2;
    }

    // Case 3:
    else {

        // Case 3a:
        if (isPrime(N - 2)) {
            minCount = 2;
        }

        // Case 3b:
        else {
            minCount = 3;
        }
    }

    System.out.print(minCount +"\n");
}

// Driver Code
public static void main(String[] args)
{
    int N = 100;

    // Function Call
    printMinCountPrime(N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach 

# Function to check if n is prime 
def isPrime(n) : 

    for i in range(2, int(n ** (1/2)) + 1) :
        if (n % i == 0) :
            return False; 

    return True; 

# Function to count the minimum 
# prime required for given sum N 
def printMinCountPrime(N) : 

    # Case 1: 
    if (isPrime(N)) :
        minCount = 1; 

    # Case 2: 
    elif (N % 2 == 0) :
        minCount = 2; 

    # Case 3: 
    else : 

        # Case 3a: 
        if (isPrime(N - 2)) :
            minCount = 2; 

        # Case 3b: 
        else :
            minCount = 3; 

    print(minCount) ; 

# Driver Code 
if __name__ == "__main__" : 
    N = 100; 

    # Function Call 
    printMinCountPrime(N); 

# This code is contributed by AnkitRai01
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if n is prime
static bool isPrime(int n)
{
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}

// Function to count the minimum
// prime required for given sum N
static void printMinCountPrime(int N)
{

    int minCount;

    // Case 1:
    if (isPrime(N)) {
        minCount = 1;
    }

    // Case 2:
    else if (N % 2 == 0) {
        minCount = 2;
    }

    // Case 3:
    else {

        // Case 3a:
        if (isPrime(N - 2)) {
            minCount = 2;
        }

        // Case 3b:
        else {
            minCount = 3;
        }
    }

    Console.WriteLine(minCount +"\n");
}

// Driver Code
public static void Main(string[] args)
{
    int N = 100;

    // Function Call
    printMinCountPrime(N);
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if n is prime
function isPrime(n)
{
    for (let i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}

// Function to count the minimum
// prime required for given sum N
function printMinCountPrime(N)
{

    let minCount;

    // Case 1:
    if (isPrime(N)) {
        minCount = 1;
    }

    // Case 2:
    else if (N % 2 == 0) {
        minCount = 2;
    }

    // Case 3:
    else {

        // Case 3a:
        if (isPrime(N - 2)) {
            minCount = 2;
        }

        // Case 3b:
        else {
            minCount = 3;
        }
    }

    document.write(minCount + "<br>");
}

// Driver Code

let N = 100;

// Function Call
printMinCountPrime(N);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(√N)，其中 N 为给定数。