# 计数到 N 的有趣素数

> 原文:[https://www . geesforgeks . org/count-of-interest-primes-upto-n/](https://www.geeksforgeeks.org/count-of-interesting-primes-upto-n/)

给定一个数字 **N** ，任务是找到小于等于 **N** 的有趣素数。
一个**有趣的素数**是任意的[素数](https://www.geeksforgeeks.org/prime-numbers/)，可以写成**a<sup>2</sup>+b<sup>4</sup>**，其中 **a** 和 **b** 都是正整数。例如，最小的有趣素数是**2 = 1<sup>2</sup>+1<sup>4</sup>**。

**示例:**

> **输入:** N = 10
> **输出:**2
> 2 = 1<sup>2</sup>+1<sup>4</sup>
> 5 = 2<sup>2</sup>+1<sup>4</sup>
> 两者都是小于等于 10 的有趣素数
> 
> **输入:**N = 1000
> T3】输出: 28

**天真方法:**

1.  遍历从 **1** 到 **N** 的所有数字。
2.  对于每个数字，检查它是否是质数。
3.  如果是质数，则通过以下方式检查是否可以表示为**a<sup>2</sup>+b<sup>4</sup>T5:**
    *   从 1 到 N 迭代 **b** 的所有可能值 <sup>1/4</sup> 。
    *   对于 **b** 的每个值，检查**N–b<sup>4</sup>**是否为完美正方形(即可以是 **a <sup>2</sup>** 也可以不是)。

下面是上述方法的实现:

## C++

```
// C++ program to find the number
// of interesting primes up to N

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// is prime or not
bool isPrime(int n)
{

    int flag = 1;

    // If n is divisible by any
    // number between 2 and sqrt(n),
    // it is not prime
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            flag = 0;
            break;
        }
    }

    return (flag == 1 ? true : false);
}

// Function to check if a number
// is perfect square or not
bool isPerfectSquare(int x)
{
    // Find floating point value of
    // square root of x.
    long double sr = sqrt(x);

    // If square root is an integer
    return ((sr - floor(sr)) == 0);
}

// Function to find the number of interesting
// primes less than equal to N.
int countInterestingPrimes(int n)
{

    int answer = 0;
    for (int i = 2; i <= n; i++) {

        // Check whether the number
        // is prime or not
        if (isPrime(i)) {

            // Iterate for values of b
            for (int j = 1;
                 j * j * j * j <= i;
                 j++) {

                // Check condition for a
                if (
                    isPerfectSquare(
                        i - j * j * j * j)) {
                    answer++;
                    break;
                }
            }
        }
    }

    // Return the required answer
    return answer;
}

// Driver code
int main()
{
    int N = 10;

    cout << countInterestingPrimes(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number
// of interesting primes up to N
class GFG{

// Function to check if a number
// is prime or not
static boolean isPrime(int n)
{

    int flag = 1;

    // If n is divisible by any
    // number between 2 and Math.sqrt(n),
    // it is not prime
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            flag = 0;
            break;
        }
    }

    return (flag == 1 ? true : false);
}

// Function to check if a number
// is perfect square or not
static boolean isPerfectSquare(int x)
{
    // Find floating point value of
    // square root of x.
    double sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0);
}

// Function to find the number of interesting
// primes less than equal to N.
static int countInterestingPrimes(int n)
{

    int answer = 0;
    for (int i = 2; i <= n; i++) {

        // Check whether the number
        // is prime or not
        if (isPrime(i)) {

            // Iterate for values of b
            for (int j = 1;
                 j * j * j * j <= i;
                 j++) {

                // Check condition for a
                if (
                    isPerfectSquare(
                        i - j * j * j * j)) {
                    answer++;
                    break;
                }
            }
        }
    }

    // Return the required answer
    return answer;
}

// Driver code
public static void main(String[] args)
{
    int N = 10;

    System.out.print(countInterestingPrimes(N));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find the number
# of interesting primes up to N
import math

# Function to check if a number
# is prime or not
def isPrime(n):

    flag = 1

    # If n is divisible by any
    # number between 2 and sqrt(n),
    # it is not prime
    i = 2
    while(i * i <= n):
        if (n % i == 0):
            flag = 0
            break
        i += 1

    return (True if flag == 1 else False)

# Function to check if a number
# is perfect square or not
def isPerfectSquare(x):

    # Find floating povalue of
    # square root of x.
    sr = math.sqrt(x)

    # If square root is an integer
    return ((sr - math.floor(sr)) == 0)

# Function to find the number of interesting
# primes less than equal to N.
def countInterestingPrimes(n):

    answer = 0
    for i in range(2, n):

        # Check whether the number
        # is prime or not
        if (isPrime(i)):

            # Iterate for values of b
            j = 1
            while(j * j * j * j <= i):

                # Check condition for a
                if (isPerfectSquare(i - j * j *
                                        j * j)):
                    answer += 1
                    break
                j += 1

    # Return the required answer
    return answer

# Driver code
if __name__=='__main__':

    N = 10

    print(countInterestingPrimes(N))

# This code is contributed by AbhiThakur
```

## C#

```
// C# program to find the number
// of interesting primes up to N
using System;
using System.Collections.Generic;

class GFG{

// Function to check if a number
// is prime or not
static bool isPrime(int n)
{

    int flag = 1;

    // If n is divisible by any
    // number between 2 and Math.Sqrt(n),
    // it is not prime
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            flag = 0;
            break;
        }
    }

    return (flag == 1 ? true : false);
}

// Function to check if a number
// is perfect square or not
static bool isPerfectSquare(int x)
{
    // Find floating point value of
    // square root of x.
    double sr = Math.Sqrt(x);

    // If square root is an integer
    return ((sr - Math.Floor(sr)) == 0);
}

// Function to find the number of interesting
// primes less than equal to N.
static int countInterestingPrimes(int n)
{

    int answer = 0;
    for (int i = 2; i <= n; i++) {

        // Check whether the number
        // is prime or not
        if (isPrime(i)) {

            // Iterate for values of b
            for (int j = 1;
                 j * j * j * j <= i;
                 j++) {

                // Check condition for a
                if (
                    isPerfectSquare(
                        i - j * j * j * j)) {
                    answer++;
                    break;
                }
            }
        }
    }

    // Return the required answer
    return answer;
}

// Driver code
public static void Main(String[] args)
{
    int N = 10;

    Console.Write(countInterestingPrimes(N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Java  script program to find the number
// of interesting primes up to N

// Function to check if a number
// is prime or not
function isPrime( n)
{

    let flag = 1;

    // If n is divisible by any
    // number between 2 and Math.sqrt(n),
    // it is not prime
    for (let i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            flag = 0;
            break;
        }
    }

    return (flag == 1 ? true : false);
}

// Function to check if a number
// is perfect square or not
function isPerfectSquare( x)
{
    // Find floating point value of
    // square root of x.
    let sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0);
}

// Function to find the number of interesting
// primes less than equal to N.
function countInterestingPrimes( n)
{

    let answer = 0;
    for (let i = 2; i <= n; i++) {

        // Check whether the number
        // is prime or not
        if (isPrime(i)) {

            // Iterate for values of b
            for (let j = 1;
                j * j * j * j <= i;
                j++) {

                // Check condition for a
                if (
                    isPerfectSquare(
                        i - j * j * j * j)) {
                    answer++;
                    break;
                }
            }
        }
    }

    // Return the required answer
    return answer;
}

// Driver code

    let N = 10;

    document.write(countInterestingPrimes(N));

// This code is contributed by Bobby
</script>
```

**Output:** 

```
2
```

***时间复杂度** : O(N)*

***辅助空间:** O(1)*

**有效方法:**

1.  如果我们存储所有 [**完美正方形**](https://www.geeksforgeeks.org/print-all-perfect-squares-from-the-given-range/) 和**完美四倍体**到 **N** ，那么我们可以遍历所有对，检查结果是否为素数。
2.  为了进一步优化，我们可以使用埃拉托斯特尼的[筛将所有素数存储到 **N** ，并在 **O(1)** 中进行素数检查。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
// C++ program to find the number
// of interesting primes up to N.

#include <bits/stdc++.h>
using namespace std;

// Function to find all prime numbers
void SieveOfEratosthenes(
    int n,
    unordered_set<int>& allPrimes)
{
    // Create a boolean array "prime[0..n]"
    // and initialize all entries as true.
    // A value in prime[i] will finally
    // be false if i is Not a prime.
    bool prime[n + 1];
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            // greater than or equal to
            // the square of it
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Store all prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            allPrimes.insert(p);
}

// Function to check if a number
// is perfect square or not
int countInterestingPrimes(int n)
{
    // To store all primes
    unordered_set<int> allPrimes;

    SieveOfEratosthenes(n, allPrimes);

    // To store all interseting primes
    unordered_set<int> intersetingPrimes;

    vector<int> squares, quadruples;

    // Store all perfect squares
    for (int i = 1; i * i <= n; i++) {
        squares.push_back(i * i);
    }

    // Store all perfect quadruples
    for (int i = 1; i * i * i * i <= n; i++) {
        quadruples.push_back(i * i * i * i);
    }

    // Store all interseting primes
    for (auto a : squares) {
        for (auto b : quadruples) {
            if (allPrimes.count(a + b))
                intersetingPrimes.insert(a + b);
        }
    }

    // Return count of interseting primes
    return intersetingPrimes.size();
}

// Driver code
int main()
{
    int N = 10;

    cout << countInterestingPrimes(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number
// of interesting primes up to N.
import java.util.*;

class GFG{

// Function to find all prime numbers
static void SieveOfEratosthenes(
    int n, HashSet<Integer> allPrimes)
{
    // Create a boolean array "prime[0..n]"
    // and initialize all entries as true.
    // A value in prime[i] will finally
    // be false if i is Not a prime.
    boolean []prime = new boolean[n + 1];
    Arrays.fill(prime, true);

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            // greater than or equal to
            // the square of it
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Store all prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            allPrimes.add(p);
}

// Function to check if a number
// is perfect square or not
static int countInterestingPrimes(int n)
{
    // To store all primes
    HashSet<Integer> allPrimes = new HashSet<Integer>();

    SieveOfEratosthenes(n, allPrimes);

    // To store all interseting primes
    HashSet<Integer> intersetingPrimes = new HashSet<Integer>();

    Vector<Integer> squares = new Vector<Integer>()
            , quadruples = new Vector<Integer>();

    // Store all perfect squares
    for (int i = 1; i * i <= n; i++) {
        squares.add(i * i);
    }

    // Store all perfect quadruples
    for (int i = 1; i * i * i * i <= n; i++) {
        quadruples.add(i * i * i * i);
    }

    // Store all interseting primes
    for (int a : squares) {
        for (int b : quadruples) {
            if (allPrimes.contains(a + b))
                intersetingPrimes.add(a + b);
        }
    }

    // Return count of interseting primes
    return intersetingPrimes.size();
}

// Driver code
public static void main(String[] args)
{
    int N = 10;

    System.out.print(countInterestingPrimes(N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the number
# of interesting primes up to N.

# Function to find all prime numbers
def SieveOfEratosthenes(n, allPrimes):

    # Create a boolean array "prime[0..n]"
    # and initialize all entries as true.
    # A value in prime[i] will finally
    # be false if i is Not a prime.
    prime = [True] * (n + 1)

    p = 2
    while p * p <= n:

        # If prime[p] is not changed,
        # then it is a prime
        if prime[p] == True:

            # Update all multiples of p
            # greater than or equal to
            # the square of it
            for i in range(p * p, n + 1, p):
                prime[i] = False
        p += 1

    # Store all prime numbers
    for p in range(2, n + 1):
        if prime[p]:
            allPrimes.add(p)

# Function to check if a number
# is perfect square or not
def countInterestingPrimes(n):

    # To store all primes
    allPrimes = set()

    # To store all interseting primes
    SieveOfEratosthenes(n, allPrimes)

    # To store all interseting primes
    interestingPrimes = set()

    squares, quadruples = [], []

    # Store all perfect squares
    i = 1
    while i * i <= n:
        squares.append(i * i)
        i += 1

    # Store all perfect quadruples
    i = 1
    while i * i * i * i <= n:
        quadruples.append(i * i * i * i)
        i += 1

    # Store all interseting primes
    for a in squares:
        for b in quadruples:
            if a + b in allPrimes:
                interestingPrimes.add(a + b)

    # Return count of interseting primes
    return len(interestingPrimes)

# Driver code
N = 10
print(countInterestingPrimes(N))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to find the number
// of interesting primes up to N.
using System;
using System.Collections.Generic;

class GFG{

// Function to find all prime numbers
static void SieveOfEratosthenes(
    int n, HashSet<int> allPrimes)
{
    // Create a bool array "prime[0..n]"
    // and initialize all entries as true.
    // A value in prime[i] will finally
    // be false if i is Not a prime.
    bool []prime = new bool[n + 1];
    for(int i = 0; i < n + 1; i++)
        prime[i] =  true;

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            // greater than or equal to
            // the square of it
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Store all prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            allPrimes.Add(p);
}

// Function to check if a number
// is perfect square or not
static int countInterestingPrimes(int n)
{
    // To store all primes
    HashSet<int> allPrimes = new HashSet<int>();

    SieveOfEratosthenes(n, allPrimes);

    // To store all interseting primes
    HashSet<int> intersetingPrimes = new HashSet<int>();

    List<int> squares = new List<int>()
            , quadruples = new List<int>();

    // Store all perfect squares
    for (int i = 1; i * i <= n; i++) {
        squares.Add(i * i);
    }

    // Store all perfect quadruples
    for (int i = 1; i * i * i * i <= n; i++) {
        quadruples.Add(i * i * i * i);
    }

    // Store all interseting primes
    foreach (int a in squares) {
        foreach (int b in quadruples) {
            if (allPrimes.Contains(a + b))
                intersetingPrimes.Add(a + b);
        }
    }

    // Return count of interseting primes
    return intersetingPrimes.Count;
}

// Driver code
public static void Main(String[] args)
{
    int N = 10;

    Console.Write(countInterestingPrimes(N));
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
2
```

时间复杂度:0(N)

辅助空间:O(N)