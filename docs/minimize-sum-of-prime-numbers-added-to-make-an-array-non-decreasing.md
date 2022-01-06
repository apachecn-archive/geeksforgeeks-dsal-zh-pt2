# 最小化相加的素数之和，使数组不递减

> 原文:[https://www . geeksforgeeks . org/minimum-质数之和-相加形成数组-非递减/](https://www.geeksforgeeks.org/minimize-sum-of-prime-numbers-added-to-make-an-array-non-decreasing/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过向数组元素添加素数来将其转换为非递减数组，使得所添加的素数之和尽可能最小。

**示例:**

> **输入:** arr[] = {2，1，5，4，3}
> **输出:** 7
> **解释:**
> {2， **1** ，5， **4，3** } - > {2， **3** ，5， **6，6** }
> 通过将数组的 2 <sup>nd</sup> 元素改为
> 所以，总成本是 2 + 2 + 3 = 7
> 
> **输入:** arr[] = {3，3，3，3 }
> T3】输出: 10

**方法:**想法是给数组元素添加尽可能少的[素数](https://www.geeksforgeeks.org/prime-numbers/)，使数组不递减。以下是步骤:

1.  初始化一个变量来存储最小成本，比如 **res** 。
2.  使用厄拉多塞的[筛生成并存储 10 <sup>7</sup> 以内的所有质数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
3.  现在，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下步骤:
    *   如果当前元素小于前一个元素，那么找到最小的质数(比如**最接近的 _ 质数**)，这个质数可以相加使数组不减。
    *   更新当前元素 **arr[i] = arr[i] +最接近 _prime** 。
    *   将**最接近的 _prime** 添加到 **res** 。
4.  打印获得的 **res** 的最终值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

#define MAX 10000000

// Stores if an index is a
// prime / non-prime value
bool isPrime[MAX];

// Stores the prime
vector<int> primes;

// Function to generate all
// prime numbers
void SieveOfEratosthenes()
{
    memset(isPrime, true, sizeof(isPrime));

    for (int p = 2; p * p <= MAX; p++) {

        // If current element is prime
        if (isPrime[p] == true) {

            // Set all its multiples non-prime
            for (int i = p * p; i <= MAX; i += p)
                isPrime[i] = false;
        }
    }

    // Store all prime numbers
    for (int p = 2; p <= MAX; p++)
        if (isPrime[p])
            primes.push_back(p);
}

// Function to find the closest
// prime to a particular number
int prime_search(vector<int> primes,
                 int diff)
{

    // Applying binary search
    // on primes vector
    int low = 0;
    int high = primes.size() - 1;

    int res;

    while (low <= high) {
        int mid = (low + high) / 2;

        // If the prime added makes
        // the elements equal
        if (primes[mid] == diff) {

            // Return this as the
            // closest prime
            return primes[mid];
        }

        // If the array remains
        // non-decreasing
        else if (primes[mid] < diff) {

            // Search for a bigger
            // prime number
            low = mid + 1;
        }

        // Otherwise
        else {

            res = primes[mid];

            // Check if a smaller prime  can
            // make array non-decreasing or not
            high = mid - 1;
        }
    }

    // Return closest number
    return res;
}

// Function to find the minimum cost
int minCost(int arr[], int n)
{

    // Find all primes
    SieveOfEratosthenes();

    // Store the result
    int res = 0;

    // Iterate over the array
    for (int i = 1; i < n; i++) {

        // Current element is less
        // than the previous element
        if (arr[i] < arr[i - 1]) {
            int diff = arr[i - 1] - arr[i];

            // Find the closest prime which
            // makes the array non decreasing
            int closest_prime
                = prime_search(primes, diff);

            // Add to overall cost
            res += closest_prime;

            // Update current element
            arr[i] += closest_prime;
        }
    }

    // Return the minimum cost
    return res;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 1, 5, 4, 3 };
    int n = 5;

    // Function Call
    cout << minCost(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static final int MAX = 10000000;

// Stores if an index is a
// prime / non-prime value
static boolean []isPrime = new boolean[MAX + 1];

// Stores the prime
static Vector<Integer> primes = new Vector<Integer>();

// Function to generate all
// prime numbers
static void SieveOfEratosthenes()
{
    Arrays.fill(isPrime, true);

    for(int p = 2; p * p <= MAX; p++)
    {

        // If current element is prime
        if (isPrime[p] == true)
        {

            // Set all its multiples non-prime
            for(int i = p * p; i <= MAX; i += p)
                isPrime[i] = false;
        }
    }

    // Store all prime numbers
    for(int p = 2; p <= MAX; p++)
        if (isPrime[p])
            primes.add(p);
}

// Function to find the closest
// prime to a particular number
static int prime_search(Vector<Integer> primes,
                        int diff)
{

    // Applying binary search
    // on primes vector
    int low = 0;
    int high = primes.size() - 1;

    int res = -1;

    while (low <= high)
    {
        int mid = (low + high) / 2;

        // If the prime added makes
        // the elements equal
        if (primes.get(mid) == diff)
        {

            // Return this as the
            // closest prime
            return primes.get(mid);
        }

        // If the array remains
        // non-decreasing
        else if (primes.get(mid) < diff)
        {

            // Search for a bigger
            // prime number
            low = mid + 1;
        }

        // Otherwise
        else
        {
            res = primes.get(mid);

            // Check if a smaller prime can
            // make array non-decreasing or not
            high = mid - 1;
        }
    }

    // Return closest number
    return res;
}

// Function to find the minimum cost
static int minCost(int arr[], int n)
{

    // Find all primes
    SieveOfEratosthenes();

    // Store the result
    int res = 0;

    // Iterate over the array
    for(int i = 1; i < n; i++)
    {

        // Current element is less
        // than the previous element
        if (arr[i] < arr[i - 1])
        {
            int diff = arr[i - 1] - arr[i];

            // Find the closest prime which
            // makes the array non decreasing
            int closest_prime = prime_search(primes,
                                             diff);

            // Add to overall cost
            res += closest_prime;

            // Update current element
            arr[i] += closest_prime;
        }
    }

    // Return the minimum cost
    return res;
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 2, 1, 5, 4, 3 };
    int n = 5;

    // Function call
    System.out.print(minCost(arr, n));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Pthon3 Program to implement
# the above approach
MAX = 10000000

# Stores if an index is a
# prime / non-prime value
isPrime = [True] * (MAX + 1)

# Stores the prime
primes = []

# Function to generate all
# prime numbers
def SieveOfEratosthenes():

    global isPrime

    p = 2
    while p * p <= MAX:

        # If current element is prime
        if (isPrime[p] == True):

            # Set all its multiples non-prime
            for i in range (p * p, MAX + 1, p):
                isPrime[i] = False

        p += 1

    # Store all prime numbers
    for p in range (2, MAX + 1):
        if (isPrime[p]):
            primes.append(p)

# Function to find the closest
# prime to a particular number
def prime_search(primes, diff):

    # Applying binary search
    # on primes vector
    low = 0
    high = len(primes) - 1

    while (low <= high):
        mid = (low + high) // 2

        # If the prime added makes
        # the elements equal
        if (primes[mid] == diff):

            # Return this as the
            # closest prime
            return primes[mid]

        # If the array remains
        # non-decreasing
        elif (primes[mid] < diff):

            # Search for a bigger
            # prime number
            low = mid + 1

        # Otherwise
        else:
            res = primes[mid]

            # Check if a smaller prime  can
            # make array non-decreasing or not
            high = mid - 1

    # Return closest number
    return res

# Function to find the minimum cost
def minCost(arr, n):

    # Find all primes
    SieveOfEratosthenes()

    # Store the result
    res = 0

    # Iterate over the array
    for i in range (1, n):

        # Current element is less
        # than the previous element
        if (arr[i] < arr[i - 1]):
            diff = arr[i - 1] - arr[i]

            # Find the closest prime which
            # makes the array non decreasing
            closest_prime = prime_search(primes, diff)

            # Add to overall cost
            res += closest_prime

            # Update current element
            arr[i] += closest_prime

    # Return the minimum cost
    return res

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [2, 1, 5, 4, 3]
    n = 5

    #Function Call
    print (minCost(arr, n))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement 
// the above approach 
using System;
using System.Collections;
using System.Collections.Generic; 

class GFG{

static int MAX = 10000000;

// Stores if an index is a
// prime / non-prime value
static bool []isPrime = new bool[MAX + 1];

// Stores the prime
static ArrayList primes = new ArrayList();

// Function to generate all
// prime numbers
static void SieveOfEratosthenes()
{
    Array.Fill(isPrime, true);

    for(int p = 2; p * p <= MAX; p++)
    {

        // If current element is prime
        if (isPrime[p] == true)
        {

            // Set all its multiples non-prime
            for(int i = p * p; i <= MAX; i += p)
                isPrime[i] = false;
        }
    }

    // Store all prime numbers
    for(int p = 2; p <= MAX; p++)
        if (isPrime[p])
            primes.Add(p);
}

// Function to find the closest
// prime to a particular number
static int prime_search(ArrayList primes,
                        int diff)
{

    // Applying binary search
    // on primes vector
    int low = 0;
    int high = primes.Count - 1;

    int res = -1;

    while (low <= high)
    {
        int mid = (low + high) / 2;

        // If the prime added makes
        // the elements equal
        if ((int)primes[mid] == diff)
        {

            // Return this as the
            // closest prime
            return (int)primes[mid];
        }

        // If the array remains
        // non-decreasing
        else if ((int)primes[mid] < diff)
        {

            // Search for a bigger
            // prime number
            low = mid + 1;
        }

        // Otherwise
        else
        {
            res = (int)primes[mid];

            // Check if a smaller prime can
            // make array non-decreasing or not
            high = mid - 1;
        }
    }

    // Return closest number
    return res;
}

// Function to find the minimum cost
static int minCost(int []arr, int n)
{

    // Find all primes
    SieveOfEratosthenes();

    // Store the result
    int res = 0;

    // Iterate over the array
    for(int i = 1; i < n; i++)
    {

        // Current element is less
        // than the previous element
        if (arr[i] < arr[i - 1])
        {
            int diff = arr[i - 1] - arr[i];

            // Find the closest prime which
            // makes the array non decreasing
            int closest_prime = prime_search(primes,
                                             diff);

            // Add to overall cost
            res += closest_prime;

            // Update current element
            arr[i] += closest_prime;
        }
    }

    // Return the minimum cost
    return res;
}

// Driver Code
public static void Main(string[] args)
{

    // Given array
    int []arr = { 2, 1, 5, 4, 3 };
    int n = 5;

    // Function call
    Console.Write(minCost(arr, n));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

let MAX = 10000000;

// Stores if an index is a
// prime / non-prime value
let isPrime = new Array(MAX);

// Stores the prime
let primes = new Array();

// Function to generate all
// prime numbers
function SieveOfEratosthenes()
{
   isPrime.fill(true);

    for (let p = 2; p * p <= MAX; p++) {

        // If current element is prime
        if (isPrime[p] == true) {

            // Set all its multiples non-prime
            for (let i = p * p; i <= MAX; i += p)
                isPrime[i] = false;
        }
    }

    // Store all prime numbers
    for (let p = 2; p <= MAX; p++)
        if (isPrime[p])
            primes.push(p);
}

// Function to find the closest
// prime to a particular number
function prime_search(primes, diff)
{

    // Applying binary search
    // on primes vector
    let low = 0;
    let high = primes.length - 1;

    let res = 0;

    while (low <= high) {
        let mid = Math.floor((low + high) / 2);

        // If the prime added makes
        // the elements equal
        if (primes[mid] == diff) {

            // Return this as the
            // closest prime

            return primes[mid];
        }

        // If the array remains
        // non-decreasing
        else if (primes[mid] < diff) {

            // Search for a bigger
            // prime number
            low = mid + 1;
        }

        // Otherwise
        else {

            res = primes[mid];

            // Check if a smaller prime  can
            // make array non-decreasing or not
            high = mid - 1;
        }
    }

    // Return closest number
    return res;
}

// Function to find the minimum cost
function minCost(arr, n)
{

    // Find all primes
    SieveOfEratosthenes();

    // Store the result
    let res = 0;

    // Iterate over the array
    for (let i = 1; i < n; i++) {

        // Current element is less
        // than the previous element
        if (arr[i] < arr[i - 1]) {
            let diff = arr[i - 1] - arr[i];

            // Find the closest prime which
            // makes the array non decreasing
            let closest_prime
                = prime_search(primes, diff);

            // Add to overall cost
            res += closest_prime;

            // Update current element
            arr[i] += closest_prime;
        }
    }

    // Return the minimum cost
    return res;
}

// Driver Code
    // Given array
    let arr = [ 2, 1, 5, 4, 3 ];
    let n = 5;

    // Function Call
    document.write(minCost(arr, n))

// This code is contributed by gfgking

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N * log(logN))*
***辅助空间:** O(N)*