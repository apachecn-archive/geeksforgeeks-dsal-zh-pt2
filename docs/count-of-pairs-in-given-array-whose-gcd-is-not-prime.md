# 给定数组中 GCD 不是素数的对的计数

> 原文:[https://www . geesforgeks . org/给定数组中的对计数-谁的 gcd 不是质数/](https://www.geeksforgeeks.org/count-of-pairs-in-given-array-whose-gcd-is-not-prime/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到对的数量，使得对的[最大公约数(GCD)](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 不是[素数](https://www.geeksforgeeks.org/tag/prime-number/)。对 **(i，j)** 和 **(j，i)** 被认为是相同的。

**示例:**

> **输入:** arr[] ={ 2，3，9}
> **输出:** 10
> **解释:**
> 以下是 GCD 不是素数的可能对:
> 
> 1.  (0，1):arr[0](= 2)和 arr[1](= 3)的 GCD 为 1。
> 2.  (0，2):arr[0](= 2)和 arr[2](= 9)的 GCD 为 1。
> 
> 因此，对的总数是 2。
> 
> **输入:** arr[] = {3，5，2，10}
> **输出:** 4

**方法:**给定的问题可以通过找到所有质数直到 **10 <sup>5</sup>** 并将其存储在[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中，然后对于每一对 **(i，j)** 来解决。如果它们的 GCD 不在集合中，则计算这一对。按照以下步骤解决问题:

*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/)**prime screen()**，使用厄拉多塞的[筛查找到**10<sup>5</sup>T7】以内的素数，并存储在**](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)**[无序集合](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/)中，比如 **S** 。**
*   初始化变量，说**计数**为 **0** ，存储对的总计数。
*   [从给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，如果它们的 GCD 不在集合中，那么将**计数**的值增加 **1** 。
*   执行上述步骤后，打印**计数**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the prime numbers
void primeSieve(bool* p)
{
    for (int i = 2; i * i <= 1000000; i++) {

        // If p[i] is not changed,
        // then it is a prime
        if (p[i] == true) {

            // Update all multiples of i
            // as non prime
            for (int j = i * 2;
                 j <= 1000000; j += i) {
                p[j] = false;
            }
        }
    }
}

// Function to find GCD of two integers
// a and b
int gcd(int a, int b)
{
    // Base Case
    if (b == 0)
        return a;

    // Find GCD Recursively
    return gcd(b, a % b);
}

// Function to count the number of
// pairs whose GCD is non prime
int countPairs(int arr[], int n,
               unordered_set<int> s)
{
    // Stores the count of valid pairs
    int count = 0;

    // Traverse over the array arr[]
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            // Calculate the GCD
            int x = gcd(arr[i], arr[j]);

            // Update the count
            if (s.find(x) == s.end())
                count++;
        }
    }

    // Return count
    return count;
}

// Utility Function to find all the prime
// numbers and find all the pairs
void countPairsUtil(int arr[], int n)
{
    // Stores all the prime numbers
    unordered_set<int> s;
    bool p[1000005];
    memset(p, true, sizeof(p));

    // Find all the prime numbers
    primeSieve(p);

    s.insert(2);

    // Insert prime numbers in the
    // unordered set
    for (int i = 3; i <= 1000000; i += 2)
        if (p[i])
            s.insert(i);

    // Find the count of valid pairs
    cout << countPairs(arr, n, s);
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);
    countPairsUtil(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the prime numbers
static void primeSieve(boolean[] p)
{
    for (int i = 2; i * i <= 1000000; i++) {

        // If p[i] is not changed,
        // then it is a prime
        if (p[i] == true) {

            // Update all multiples of i
            // as non prime
            for (int j = i * 2;
                 j <= 1000000; j += i) {
                p[j] = false;
            }
        }
    }
}

// Function to find GCD of two integers
// a and b
static int gcd(int a, int b)
{
    // Base Case
    if (b == 0)
        return a;

    // Find GCD Recursively
    return gcd(b, a % b);
}

// Function to count the number of
// pairs whose GCD is non prime
static int countPairs(int arr[], int n,
               HashSet<Integer> s)
{
    // Stores the count of valid pairs
    int count = 0;

    // Traverse over the array arr[]
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            // Calculate the GCD
            int x = gcd(arr[i], arr[j]);

            // Update the count
            if (!s.contains(x))
                count++;
        }
    }

    // Return count
    return count;
}

// Utility Function to find all the prime
// numbers and find all the pairs
static void countPairsUtil(int arr[], int n)
{
    // Stores all the prime numbers
    HashSet<Integer> s = new HashSet<Integer>();
    boolean []p = new boolean[1000005];
    for(int i=0;i<p.length;i++)
        p[i] = true;

    // Find all the prime numbers
    primeSieve(p);

    s.add(2);

    // Insert prime numbers in the
    // unordered set
    for (int i = 3; i <= 1000000; i += 2)
        if (p[i])
            s.add(i);

    // Find the count of valid pairs
    System.out.print(countPairs(arr, n, s));
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 9 };
    int N = arr.length;
    countPairsUtil(arr, N);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach

from math import sqrt,gcd

# Function to find the prime numbers
def primeSieve(p):
    for i in range(2,int(sqrt(1000000)),1):

        # If p[i] is not changed,
        # then it is a prime
        if (p[i] == True):

            # Update all multiples of i
            # as non prime
            for j in range(i * 2,1000001,i):
                p[j] = False

# Function to count the number of
# pairs whose GCD is non prime
def countPairs(arr, n, s):

    # Stores the count of valid pairs
    count = 0

    # Traverse over the array arr[]
    for i in range(n - 1):
        for j in range(i + 1,n,1):

            # Calculate the GCD
            x = gcd(arr[i], arr[j])

            # Update the count
            if (x not in s):
                count += 1

    # Return count
    return count

# Utility Function to find all the prime
# numbers and find all the pairs
def countPairsUtil(arr, n):

    # Stores all the prime numbers
    s = set()
    p = [True for  i in range(1000005)]

    # Find all the prime numbers
    primeSieve(p)

    s.add(2)

    # Insert prime numbers in the
    # unordered set
    for i in range(3,1000001,2):
        if (p[i]):
            s.add(i)

    # Find the count of valid pairs
    print(countPairs(arr, n, s))

# Driver Code
if __name__ == '__main__':
    arr = [2, 3, 9]
    N = len(arr)
    countPairsUtil(arr, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

// Function to find the prime numbers
static void primeSieve(bool[] p)
{
    for (int i = 2; i * i <= 1000000; i++) {

        // If p[i] is not changed,
        // then it is a prime
        if (p[i] == true) {

            // Update all multiples of i
            // as non prime
            for (int j = i * 2;
                 j <= 1000000; j += i) {
                p[j] = false;
            }
        }
    }
}

// Function to find GCD of two integers
// a and b
static int gcd(int a, int b)
{
    // Base Case
    if (b == 0)
        return a;

    // Find GCD Recursively
    return gcd(b, a % b);
}

// Function to count the number of
// pairs whose GCD is non prime
static int countPairs(int []arr, int n,
               HashSet<int> s)
{
    // Stores the count of valid pairs
    int count = 0;

    // Traverse over the array []arr
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            // Calculate the GCD
            int x = gcd(arr[i], arr[j]);

            // Update the count
            if (!s.Contains(x))
                count++;
        }
    }

    // Return count
    return count;
}

// Utility Function to find all the prime
// numbers and find all the pairs
static void countPairsUtil(int []arr, int n)
{

    // Stores all the prime numbers
    HashSet<int> s = new HashSet<int>();
    bool []p = new bool[1000005];
    for(int i = 0; i < p.Length; i++)
        p[i] = true;

    // Find all the prime numbers
    primeSieve(p);

    s.Add(2);

    // Insert prime numbers in the
    // unordered set
    for (int i = 3; i <= 1000000; i += 2)
        if (p[i])
            s.Add(i);

    // Find the count of valid pairs
    Console.Write(countPairs(arr, n, s));
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 3, 9 };
    int N = arr.Length;
    countPairsUtil(arr, N);

}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find the prime numbers
    function primeSieve( p) {
        for (var i = 2; i * i <= 1000000; i++) {

            // If p[i] is not changed,
            // then it is a prime
            if (p[i] == true) {

                // Update all multiples of i
                // as non prime
                for (j = i * 2; j <= 1000000; j += i) {
                    p[j] = false;
                }
            }
        }
    }

    // Function to find GCD of two integers
    // a and b
    function gcd(a, b)
    {
        // Base Case
        if (b == 0)
            return a;

        // Find GCD Recursively
        return gcd(b, a % b);
    }

    // Function to count the number of
    // pairs whose GCD is non prime
    function countPairs(arr , n, s) {
        // Stores the count of valid pairs
        var count = 0;

        // Traverse over the array arr
        for (var i = 0; i < n - 1; i++) {
            for (var j = i + 1; j < n; j++) {

                // Calculate the GCD
                var x = gcd(arr[i], arr[j]);

                // Update the count
                if (!s.has(x))
                    count++;
            }
        }

        // Return count
        return count;
    }

    // Utility Function to find all the prime
    // numbers and find all the pairs
    function countPairsUtil(arr, n)
    {

        // Stores all the prime numbers
        var s = new Set();
        var p = Array(1000005).fill(false);
        for (var i = 0; i < p.length; i++)
            p[i] = true;

        // Find all the prime numbers
        primeSieve(p);

        s.add(2);

        // Insert prime numbers in the
        // unordered set
        for (i = 3; i <= 1000000; i += 2)
            if (p[i])
                s.add(i);

        // Find the count of valid pairs
        document.write(countPairs(arr, n, s));
    }

    // Driver Code
        var arr = [ 2, 3, 9 ];
        var N = arr.length;
        countPairsUtil(arr, N);

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O((N<sup>2</sup>)* log N)*
***辅助空间:** O(N)*