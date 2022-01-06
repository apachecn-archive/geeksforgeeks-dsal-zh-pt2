# 在 1 到 M 的范围内找到使数组的 LCM 最大化的元素

> 原文:[https://www . geesforgeks . org/find-element-the-max-LCM-of-of-a-array-in-1-m/](https://www.geeksforgeeks.org/find-element-that-maximizes-lcm-of-an-array-in-the-range-1-to-m/)

给定一个大小为 **N** 的数组 **arr** ，包含范围**【1，M】**内的数字，任务是在范围**【1，M】**内找到一个元素，使 LCM 最大化。
**举例:**

> **输入:** arr[]={3，4，2，7}，M = 8
> **输出:** 5
> **解释:**
> 现有数组的 LCM(3，4，2，7) = 84
> 将 1 到 8 中的剩余数字相加，检查得到的数组对应的 LCM。
> 1:(1，3，4，2，7)的 LCM 为 84
> 5:(5，3，4，2，7)的 LCM 为 420
> 6:(6，3，4，2，7)的 LCM 为 84
> 8:(5，3，4，2，7)的 LCM 为 168
> 很明显，加 5 最大化了 LCM。
> **输入:** arr[]={2，5，3，8，1}，M = 9
> **输出:** 7

**天真的方法:**

*   计算给定数组的 LCM。
*   将数组中不存在的**【1，M】**范围内的每个元素相加后计算 LCM，并返回其最大值的元素。

**高效方法:**

*   使用[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)预计算数字的[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)，直到 1000。
*   存储给定数组的 LCM 的每个质因数的频率。
*   从值[1，M]开始迭代，对于数组中不存在的每个值，计算该数的质因数频率与给定数组的 LCM 的质因数频率之差的**乘积。**
*   返回提供最大乘积的元素。

下面的代码是上述方法的实现:

## C++

```
// C++ program to find the element
// to be added to maximize the LCM

#include <bits/stdc++.h>
using namespace std;

// Vector which stores the prime factors
// of all the numbers upto 10000
vector<int> primeFactors[10001];
set<int> s;

// Function which finds prime
// factors using sieve method
void findPrimeFactors()
{

    // Boolean array which stores
    // true if the index is prime
    bool primes[10001];
    memset(primes, true, sizeof(primes));

    // Sieve of Eratosthenes
    for (int i = 2; i < 10001; i++) {

        if (primes[i]) {
            for (int j = i; j < 10001; j += i) {

                if (j != i) {
                    primes[j] = false;
                }
                primeFactors[j].push_back(i);
            }
        }
    }
}

// Function which stores frequency of every
// prime factor of LCM of the initial array
void primeFactorsofLCM(int* frequecyOfPrimes,
                       int* arr, int n)
{

    for (int i = 0; i < n; i++) {
        for (auto a : primeFactors[arr[i]]) {

            int k = 0;

            // While the prime factor
            // divides the number
            while ((arr[i] % a) == 0) {
                arr[i] /= a;
                k++;
            }

            frequecyOfPrimes[a]
                = max(frequecyOfPrimes[a], k);
        }
    }
}

// Function which returns the element
// which should be added to array
int elementToBeAdded(int* frequecyOfPrimes, int m)
{
    int product = 1;

    // To store the final answer
    int ans = 1;

    for (int i = 2; i <= m; i++) {

        if (s.find(i) != s.end())
            continue;

        int j = i;
        int current = 1;

        for (auto a : primeFactors[j]) {

            int k = 0;

            // While the prime factor
            // divides the number
            while ((j % a) == 0) {

                j /= a;
                k++;
                if (k > frequecyOfPrimes[a]) {
                    current *= a;
                }
            }
        }

        // Check element which provides
        // the maximum product
        if (current > product) {
            product = current;
            ans = i;
        }
    }
    return ans;
}

void findElement(int* arr, int n, int m)
{

    for (int i = 0; i < n; i++)
        s.insert(arr[i]);
    int frequencyOfPrimes[10001] = { 0 };
    primeFactorsofLCM(frequencyOfPrimes, arr, n);
    cout << elementToBeAdded(frequencyOfPrimes, m)
         << endl;
}

// Driver code
int main()
{
    // Precomputing the prime factors
    // of all numbers upto 10000
    findPrimeFactors();

    int N = 5;
    int M = 9;
    int arr[] = { 2, 5, 3, 8, 1 };

    findElement(arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the element
// to be added to maximize the LCM
import java.util.*;

class GFG{

// Vector which stores the prime factors
// of all the numbers upto 10000
static Vector<Integer> []primeFactors = new Vector[10001];
static HashSet<Integer> s = new HashSet<Integer>();

// Function which finds prime
// factors using sieve method
static void findPrimeFactors()
{

    // Boolean array which stores
    // true if the index is prime
    boolean []primes = new boolean[10001];
    Arrays.fill(primes, true);

    // Sieve of Eratosthenes
    for (int i = 2; i < 10001; i++) {

        if (primes[i]) {
            for (int j = i; j < 10001; j += i) {

                if (j != i) {
                    primes[j] = false;
                }
                primeFactors[j].add(i);
            }
        }
    }
}

// Function which stores frequency of every
// prime factor of LCM of the initial array
static void primeFactorsofLCM(int []frequecyOfPrimes,
                    int[] arr, int n)
{

    for (int i = 0; i < n; i++) {
        for (int a : primeFactors[arr[i]]) {

            int k = 0;

            // While the prime factor
            // divides the number
            while ((arr[i] % a) == 0) {
                arr[i] /= a;
                k++;
            }

            frequecyOfPrimes[a]
                = Math.max(frequecyOfPrimes[a], k);
        }
    }
}

// Function which returns the element
// which should be added to array
static int elementToBeAdded(int []frequecyOfPrimes, int m)
{
    int product = 1;

    // To store the final answer
    int ans = 1;

    for (int i = 2; i <= m; i++) {

        if (s.contains(i))
            continue;

        int j = i;
        int current = 1;

        for (int a : primeFactors[j]) {

            int k = 0;

            // While the prime factor
            // divides the number
            while ((j % a) == 0) {

                j /= a;
                k++;
                if (k > frequecyOfPrimes[a]) {
                    current *= a;
                }
            }
        }

        // Check element which provides
        // the maximum product
        if (current > product) {
            product = current;
            ans = i;
        }
    }
    return ans;
}

static void findElement(int[] arr, int n, int m)
{

    for (int i = 0; i < n; i++)
        s.add(arr[i]);
    int frequencyOfPrimes[] = new int[10001];
    primeFactorsofLCM(frequencyOfPrimes, arr, n);
    System.out.print(elementToBeAdded(frequencyOfPrimes, m)
        +"\n");
}

// Driver code
public static void main(String[] args)
{
    for (int i = 0; i < 10001; i++)
        primeFactors[i] = new Vector<Integer>();
    // Precomputing the prime factors
    // of all numbers upto 10000
    findPrimeFactors();

    int N = 5;
    int M = 9;
    int arr[] = { 2, 5, 3, 8, 1 };

    findElement(arr, N, M);
}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program to find the element
// to be added to maximize the LCM
using System;
using System.Collections.Generic;

class GFG{

// List which stores the prime factors
// of all the numbers upto 10000
static List<int> []primeFactors = new List<int>[10001];
static HashSet<int> s = new HashSet<int>();

// Function which finds prime
// factors using sieve method
static void findPrimeFactors()
{

    // Boolean array which stores
    // true if the index is prime
    bool []primes = new bool[10001];
    for (int i = 0; i < 10001; i++)
        primes[i] = true;

    // Sieve of Eratosthenes
    for (int i = 2; i < 10001; i++) {

        if (primes[i]) {
            for (int j = i; j < 10001; j += i) {

                if (j != i) {
                    primes[j] = false;
                }
                primeFactors[j].Add(i);
            }
        }
    }
}

// Function which stores frequency of every
// prime factor of LCM of the initial array
static void primeFactorsofLCM(int []frequecyOfPrimes,
                    int[] arr, int n)
{

    for (int i = 0; i < n; i++) {
        foreach (int a in primeFactors[arr[i]]) {

            int k = 0;

            // While the prime factor
            // divides the number
            while ((arr[i] % a) == 0) {
                arr[i] /= a;
                k++;
            }

            frequecyOfPrimes[a]
                = Math.Max(frequecyOfPrimes[a], k);
        }
    }
}

// Function which returns the element
// which should be added to array
static int elementToBeAdded(int []frequecyOfPrimes, int m)
{
    int product = 1;

    // To store the readonly answer
    int ans = 1;

    for (int i = 2; i <= m; i++) {

        if (s.Contains(i))
            continue;

        int j = i;
        int current = 1;

        foreach (int a in primeFactors[j]) {

            int k = 0;

            // While the prime factor
            // divides the number
            while ((j % a) == 0) {

                j /= a;
                k++;
                if (k > frequecyOfPrimes[a]) {
                    current *= a;
                }
            }
        }

        // Check element which provides
        // the maximum product
        if (current > product) {
            product = current;
            ans = i;
        }
    }
    return ans;
}

static void findElement(int[] arr, int n, int m)
{

    for (int i = 0; i < n; i++)
        s.Add(arr[i]);
    int []frequencyOfPrimes = new int[10001];
    primeFactorsofLCM(frequencyOfPrimes, arr, n);
    Console.Write(elementToBeAdded(frequencyOfPrimes, m)
        +"\n");
}

// Driver code
public static void Main(String[] args)
{
    for (int i = 0; i < 10001; i++)
        primeFactors[i] = new List<int>();

    // Precomputing the prime factors
    // of all numbers upto 10000
    findPrimeFactors();

    int N = 5;
    int M = 9;
    int []arr = { 2, 5, 3, 8, 1 };

    findElement(arr, N, M);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to find the element
// to be added to maximize the LCM

// Vector which stores the prime factors
// of all the numbers upto 10000
let primeFactors = new Array();

for(let i = 0;  i < 10001; i++){
    primeFactors.push([])
}

let s = new Set();

// Function which finds prime
// factors using sieve method
function findPrimeFactors()
{

    // Boolean array which stores
    // true if the index is prime
    let primes = new Array(10001);
    primes.fill(true)

    // Sieve of Eratosthenes
    for (let i = 2; i < 10001; i++) {

        if (primes[i]) {
            for (let j = i; j < 10001; j += i) {

                if (j != i) {
                    primes[j] = false;
                }
                primeFactors[j].push(i);
            }
        }
    }
}

// Function which stores frequency of every
// prime factor of LCM of the initial array
function primeFactorsofLCM(frequecyOfPrimes, arr, n)
{

    for (let i = 0; i < n; i++) {
        for (let a of primeFactors[arr[i]]) {

            let k = 0;

            // While the prime factor
            // divides the number
            while ((arr[i] % a) == 0) {
                arr[i] /= a;
                k++;
            }

            frequecyOfPrimes[a]
                = Math.max(frequecyOfPrimes[a], k);
        }
    }
}

// Function which returns the element
// which should be added to array
function elementToBeAdded(frequecyOfPrimes, m)
{
    let product = 1;

    // To store the final answer
    let ans = 1;

    for (let i = 2; i <= m; i++) {

        if (s.has(i))
            continue;

        let j = i;
        let current = 1;

        for (let a of primeFactors[j]) {

            let k = 0;

            // While the prime factor
            // divides the number
            while ((j % a) == 0) {

                j /= a;
                k++;
                if (k > frequecyOfPrimes[a]) {
                    current *= a;
                }
            }
        }

        // Check element which provides
        // the maximum product
        if (current > product) {
            product = current;
            ans = i;
        }
    }
    return ans;
}

function findElement(arr, n, m)
{

    for (let i = 0; i < n; i++)
        s.add(arr[i]);
    let frequencyOfPrimes = new Array(10001).fill(0);
    primeFactorsofLCM(frequencyOfPrimes, arr, n);
    document.write(elementToBeAdded(frequencyOfPrimes, m) + "<br>");
}

// Driver code

    // Precomputing the prime factors
    // of all numbers upto 10000
    findPrimeFactors();

    let N = 5;
    let M = 9;
    let arr = [ 2, 5, 3, 8, 1 ];

    findElement(arr, N, M);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
7
```

**时间复杂度:** O(N * log N + M * log M)