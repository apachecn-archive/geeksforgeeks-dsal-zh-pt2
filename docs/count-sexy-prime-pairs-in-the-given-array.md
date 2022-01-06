# 统计给定数组中性感素数对

> 原文:[https://www . geesforgeks . org/count-sexy-prime-pairs-in-the-given-array/](https://www.geeksforgeeks.org/count-sexy-prime-pairs-in-the-given-array/)

给定一个包含自然数的大小为 **N** 的数组 **arr[]** ，任务是计算 **arr[]** 中所有可能的对，它们是[性感素对](https://www.geeksforgeeks.org/sexy-prime/)。

> A **SPP(性感质数对)**是那些质数并且质数之间相差 6 的数。换句话说，SPP(性感质数对)是质数差距为 6 的质数。

**例:**

> **输入:** arr[] = { 6，7，5，11，13 }
> **输出:** 2
> **解释:**
> 这 2 对是(5，11)和(7，13)。
> **输入:** arr[] = { 2，4，6，11 }
> **输出:** 0
> **说明:**
> 没有这样的对组成 SPP(性感素对)。

**天真方法:**解决上述问题的思路是找到给定数组中所有可能的对**arr【】**并检查两个元素对是否都是[质数](https://www.geeksforgeeks.org/prime-numbers/)且相差 **6** ，则当前对形成 [SPP(性感质数对)](https://www.geeksforgeeks.org/sexy-prime/)。
以下是上述方法的实施:

## C++

```
// C++ program to count Sexy
// Prime pairs in array

#include <bits/stdc++.h>
using namespace std;

// A utility function to check if
// the number n is prime or not
bool isPrime(int n)
{
    // Base Cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check to skip middle five
    // numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i += 6) {

        // If n is divisible by i and i+2
        // then it is not prime
        if (n % i == 0
            || n % (i + 6) == 0) {
            return false;
        }
    }

    return true;
}

// A utility function that check
// if n1 and n2 are SPP (Sexy Prime Pair)
// or not
bool SexyPrime(int n1, int n2)
{
    return (isPrime(n1)
            && isPrime(n2)
            && abs(n1 - n2) == 6);
}

// Function to find SPP (Sexy Prime Pair)
// pairs from the given array
int countSexyPairs(int arr[], int n)
{
    int count = 0;

    // Iterate through all pairs
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // Increment count if
            // SPP (Sexy Prime Pair) pair
            if (SexyPrime(arr[i], arr[j])) {
                count++;
            }
        }
    }

    return count;
}

// Driver code
int main()
{
    int arr[] = { 6, 7, 5, 11, 13 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call to find
    // SPP (Sexy Prime Pair) pair
    cout << countSexyPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count Sexy
// Prime pairs in array
import java.util.*;

class GFG {

    // A utility function to check if
    // the number n is prime or not
    static boolean isPrime(int n)
    {
        // Base Cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // Check to skip middle five
        // numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i += 6) {

            // If n is divisible by i and i+2
            // then it is not prime
            if (n % i == 0 || n % (i + 6) == 0) {
                return false;
            }
        }

        return true;
    }

    // A utility function that check
    // if n1 and n2 are SPP (Sexy Prime Pair)
    // or not
    static boolean SexyPrime(int n1, int n2)
    {
        return (isPrime(n1)
                && isPrime(n2)
                && Math.abs(n1 - n2) == 6);
    }

    // Function to find SPP (Sexy Prime Pair)
    // pairs from the given array
    static int countSexyPairs(int arr[], int n)
    {
        int count = 0;

        // Iterate through all pairs
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {

                // Increment count if
                // SPP (Sexy Prime Pair) pair
                if (SexyPrime(arr[i], arr[j])) {
                    count++;
                }
            }
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 6, 7, 5, 11, 13 };
        int n = arr.length;

        // Function call to find
        // SPP (Sexy Prime Pair) pair
        System.out.print(
            countSexyPairs(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to count Sexy
# Prime pairs in array
from math import sqrt

# A utility function to check if
# the number n is prime or not
def isPrime(n):

    # Base Cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # Check to skip middle five
    # numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False

    for i in range(5, int(sqrt(n))+1, 6):

        # If n is divisible by i and i + 2
        # then it is not prime
        if (n % i == 0 or n % (i + 6) == 0):
            return False

    return True

# A utility function that check
# if n1 and n2 are SPP (Sexy Prime Pair)
# or not
def SexyPrime(n1, n2):
    return (isPrime(n1)
           and isPrime(n2)
           and abs(n1 - n2) == 6)

# Function to find SPP (Sexy Prime Pair)
# pairs from the given array
def countSexyPairs(arr, n):
    count = 0

    # Iterate through all pairs
    for i in range(n):
        for j in range(i + 1, n):

            # Increment count if
            # SPP (Sexy Prime Pair) pair
            if (SexyPrime(arr[i], arr[j])):
                count += 1

    return count

# Driver code
if __name__ == '__main__':
    arr = [6, 7, 5, 11, 13]
    n = len(arr)

    # Function call to find
    # SPP (Sexy Prime Pair) pair
    print(countSexyPairs(arr, n))
```

## C#

```
// C# program to count Sexy
// Prime pairs in array
using System;

class GFG {

    // A utility function to check if
    // the number n is prime or not
    static bool isPrime(int n)
    {
        // Base Cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // Check to skip middle five
        // numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i += 6) {

            // If n is divisible by i and i+2
            // then it is not prime
            if (n % i == 0
                || n % (i + 6) == 0) {
                return false;
            }
        }

        return true;
    }

    // A utility function that check
    // if n1 and n2 are SPP (Sexy Prime Pair)
    // or not
    static bool SexyPrime(int n1, int n2)
    {
        return (isPrime(n1)
                && isPrime(n2)
                && Math.Abs(n1 - n2) == 6);
    }

    // Function to find SPP (Sexy Prime Pair)
    // pairs from the given array
    static int countSexyPairs(int[] arr, int n)
    {
        int count = 0;

        // Iterate through all pairs
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {

                // Increment count if
                // SPP (Sexy Prime Pair) pair
                if (SexyPrime(arr[i], arr[j])) {
                    count++;
                }
            }
        }

        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 6, 7, 5, 11, 13 };
        int n = arr.Length;

        // Function call to find
        // SPP (Sexy Prime Pair) pair
        Console.Write(countSexyPairs(arr, n));
    }
}
```

## java 描述语言

```
<script>

// javascript program to count Sexy
// Prime pairs in array

    // A utility function to check if
    // the number n is prime or not

    function isPrime( n)
    {
        // Base Cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // Check to skip middle five
        // numbers in below loop

        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (var i = 5; i * i <= n; i += 6) {

            // If n is divisible by i and i+2
            // then it is not prime
            if (n % i == 0
                || n % (i + 6) == 0) {
                return false;
            }
        }

        return true;
    }

    // A utility function that check
    // if n1 and n2 are SPP (Sexy Prime Pair)
    // or not

    function SexyPrime( n1,  n2)
    {
        return (isPrime(n1)
                && isPrime(n2)
                && Math.abs(n1 - n2) == 6);
    }

    // Function to find SPP (Sexy Prime Pair)
    // pairs from the given array
    function countSexyPairs( arr,  n)
    {
        var count = 0;

        // Iterate through all pairs
        for (var i = 0; i < n; i++) {
            for (var j = i + 1; j < n; j++) {

                // Increment count if
                // SPP (Sexy Prime Pair) pair
                if (SexyPrime(arr[i], arr[j])) {
                    count++;
                }
            }
        }

        return count;
    }

    // Driver code

        var arr = [ 6, 7, 5, 11, 13 ]
        var n = arr.length;

        // Function call to find
        // SPP (Sexy Prime Pair) pair
        document.write(countSexyPairs(arr, n));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(sqrt(M) * N <sup>2</sup> ，其中 N 为给定数组中的元素个数，M 为数组中的最大元素个数。*
**高效方法:**
上述方法可通过以下步骤进行优化:

1.  使用厄拉多塞的[筛，预计算所有](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[素数](https://www.geeksforgeeks.org/prime-numbers/)直到给定数组**arr【】**中的最大数。
2.  存储给定数组中所有元素的所有频率，并对数组进行排序。
3.  对于数组中的每个元素，检查该元素是否是质数。
4.  如果元素是质数，那么检查(元素+ 6)是否是质数并且是否存在于给定的数组中。
5.  如果(元素+ 6)存在，那么(元素+ 6)的频率将给出当前元素的对的计数。
6.  对数组中的所有元素重复上述步骤。

以下是上述方法的实现:

## C++

```
// C++ program to count Sexy
// Prime pairs in array

#include <bits/stdc++.h>
using namespace std;

// To store check the prime
// number
vector<bool> Prime;

// A utility function that find
// the Prime Numbers till N
void computePrime(int N)
{

    // Resize the Prime Number
    Prime.resize(N + 1, true);
    Prime[0] = Prime[1] = false;

    // Loop till sqrt(N) to find
    // prime numbers and make their
    // multiple false in the bool
    // array Prime
    for (int i = 2; i * i <= N; i++) {
        if (Prime[i]) {
            for (int j = i * i; j < N; j += i) {
                Prime[j] = false;
            }
        }
    }
}

// Function that returns the count
// of SPP (Sexy Prime Pair) Pairs
int countSexyPairs(int arr[], int n)
{

    // Find the maximum element in
    // the given array arr[]
    int maxE = *max_element(arr, arr + n);

    // Function to calculate the
    // prime numbers till N
    computePrime(maxE);

    // To store the count of pairs
    int count = 0;

    // To store the frequency of
    // element in the array arr[]
    int freq[maxE + 1] = { 0 };

    for (int i = 0; i < n; i++) {
        freq[arr[i]]++;
    }

    // Sort before traversing the array
    sort(arr, arr + n);

    // Traverse the array and find
    // the pairs with SPP (Sexy Prime Pair)
    for (int i = 0; i < n; i++) {

        // If current element is
        // Prime, then check for
        // (current element + 6)
        if (Prime[arr[i]]) {
            if (freq[arr[i] + 6] > 0
                && Prime[arr[i] + 6]) {
                count++;
            }
        }
    }

    // Return the count of pairs
    return count;
}

// Driver code
int main()
{
    int arr[] = { 6, 7, 5, 11, 13 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call to find
    // SPP (Sexy Prime Pair) pair
    cout << countSexyPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count Sexy
// Prime pairs in array

import java.util.*;

class GFG {

    // To store check the prime
    // number
    static boolean[] Prime;

    // A utility function that find
    // the Prime Numbers till N
    static void computePrime(int N)
    {

        // Resize the Prime Number
        Prime = new boolean[N + 1];
        Arrays.fill(Prime, true);
        Prime[0] = Prime[1] = false;

        // Loop till Math.sqrt(N) to find
        // prime numbers and make their
        // multiple false in the bool
        // array Prime
        for (int i = 2; i * i <= N; i++) {
            if (Prime[i]) {
                for (int j = i * i; j < N; j += i) {
                    Prime[j] = false;
                }
            }
        }
    }

    // Function that returns the count
    // of SPP (Sexy Prime Pair) Pairs
    static int countSexyPairs(int arr[], int n)
    {

        // Find the maximum element in
        // the given array arr[]
        int maxE = Arrays.stream(arr)
                       .max()
                       .getAsInt();

        // Function to calculate the
        // prime numbers till N
        computePrime(maxE);

        // To store the count of pairs
        int count = 0;

        // To store the frequency of
        // element in the array arr[]
        int freq[] = new int[maxE + 1];

        for (int i = 0; i < n; i++) {
            freq[arr[i]]++;
        }

        // Sort before traversing the array
        Arrays.sort(arr);

        // Traverse the array and find
        // the pairs with SPP (Sexy Prime Pair)
        for (int i = 0; i < n; i++) {

            // If current element is
            // Prime, then check for
            // (current element + 6)
            if (Prime[arr[i]]) {
                if (arr[i] + 6 < freq.length
                    && freq[arr[i] + 6] > 0
                    && Prime[arr[i] + 6]) {
                    count++;
                }
            }
        }

        // Return the count of pairs
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 6, 7, 5, 11, 13 };
        int n = arr.length;

        // Function call to find
        // SPP (Sexy Prime Pair) pair
        System.out.print(
            countSexyPairs(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to count Sexy
# Prime pairs in array

# A utility function that find
# the Prime Numbers till N
def computePrime( N):

    # Resize the Prime Number
    Prime = [True]*(N + 1)
    Prime[0] = False
    Prime[1] = False

    # Loop till sqrt(N) to find
    # prime numbers and make their
    # multiple false in the bool
    # array Prime
    i = 2
    while i * i <= N:
        if (Prime[i]):
            for j in range( i * i, N, i):
                Prime[j] = False
        i += 1

    return Prime

# Function that returns the count
# of SPP (Sexy Prime Pair) Pairs
def countSexyPairs(arr, n):

    # Find the maximum element in
    # the given array arr[]
    maxE = max(arr)

    # Function to calculate the
    # prime numbers till N
    Prime = computePrime(maxE)

    # To store the count of pairs
    count = 0

    # To store the frequency of
    # element in the array arr[]
    freq = [0]*(maxE + 6)

    for i in range( n):
        freq[arr[i]] += 1

    # Sort before traversing the array
    arr.sort()

    # Traverse the array and find
    # the pairs with SPP (Sexy Prime Pair)s
    for i in range(n):

        # If current element is
        # Prime, then check for
        # (current element + 6)
        if (Prime[arr[i]]):
            if ((arr[i] + 6) <= (maxE)
                and freq[arr[i] + 6] > 0
                and Prime[arr[i] + 6]):
                count += 1

    # Return the count of pairs
    return count

# Driver code
if __name__ == "__main__":

    arr = [ 6, 7, 5, 11, 13 ]
    n = len(arr)

    # Function call to find
    # SPP (Sexy Prime Pair)s pair
    print( countSexyPairs(arr, n))

```

## C#

```
// C# program to count Sexy
// Prime pairs in array

using System;
using System.Linq;

class GFG {

    // To store check the prime
    // number
    static bool[] Prime;

    // A utility function that find
    // the Prime Numbers till N
    static void computePrime(int N)
    {

        // Resize the Prime Number
        Prime = new bool[N + 1];
        for (int i = 0; i <= N; i++) {
            Prime[i] = true;
        }

        Prime[0] = Prime[1] = false;

        // Loop till Math.Sqrt(N) to find
        // prime numbers and make their
        // multiple false in the bool
        // array Prime
        for (int i = 2; i * i <= N; i++) {
            if (Prime[i]) {
                for (int j = i * i; j < N; j += i) {
                    Prime[j] = false;
                }
            }
        }
    }

    // Function that returns the count
    // of SPP (Sexy Prime Pair) Pairs
    static int countSexyPairs(int[] arr, int n)
    {

        // Find the maximum element in
        // the given array []arr
        int maxE = arr.Max();

        // Function to calculate the
        // prime numbers till N
        computePrime(maxE);

        // To store the count of pairs
        int count = 0;

        // To store the frequency of
        // element in the array []arr
        int[] freq = new int[maxE + 1];

        for (int i = 0; i < n; i++) {
            freq[arr[i]]++;
        }

        // Sort before traversing the array
        Array.Sort(arr);

        // Traverse the array and find
        // the pairs with SPP (Sexy Prime Pair)s
        for (int i = 0; i < n; i++) {

            // If current element is
            // Prime, then check for
            // (current element + 6)
            if (Prime[arr[i]]) {
                if (arr[i] + 6 < freq.Length
                    && freq[arr[i] + 6] > 0
                    && Prime[arr[i] + 6]) {
                    count++;
                }
            }
        }

        // Return the count of pairs
        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 6, 7, 5, 11, 13 };
        int n = arr.Length;

        // Function call to find
        // SPP (Sexy Prime Pair)s pair
        Console.Write(countSexyPairs(arr, n));
    }
}
```

## java 描述语言

```
<script>

// javascript program to count Sexy
// Prime pairs in array

// To store check the prime
// number
var Prime = Array(100).fill(true);

// A utility function that find
// the Prime Numbers till N
function computePrime(N)
{

     var i,j;
    // Resize the Prime Number]
    Prime[0] = Prime[1] = false;

    // Loop till sqrt(N) to find
    // prime numbers and make their
    // multiple false in the bool
    // array Prime
    for (i = 2; i * i <= N; i++) {
        if (Prime[i]) {
            for (j = i * i; j < N; j += i) {
                Prime[j] = false;
            }
        }
    }
}

// Function that returns the count
// of SPP (Sexy Prime Pair) Pairs
function countSexyPairs(arr, n)
{

    // Find the maximum element in
    // the given array arr[]
    var maxE = Math.max.apply(Math, arr);

    // Function to calculate the
    // prime numbers till N
    computePrime(maxE);

    // To store the count of pairs
    var count = 0;

    // To store the frequency of
    // element in the array arr[]
    var freq = Array(maxE + 1).fill(0);

    for (i = 0; i < n; i++) {
        freq[arr[i]]++;
    }

    // Sort before traversing the array
    arr.sort();

    // Traverse the array and find
    // the pairs with SPP (Sexy Prime Pair)
    for (i = 0; i < n; i++) {

        // If current element is
        // Prime, then check for
        // (current element + 6)
        if (Prime[arr[i]]) {
            if (freq[arr[i] + 6] > 0
                && Prime[arr[i] + 6]) {
                count++;
            }
        }
    }

    // Return the count of pairs
    return count;
}

// Driver code
    var arr = [6, 7, 5, 11, 13];
    var n = arr.length;

    // Function call to find
    // SPP (Sexy Prime Pair) pair
    document.write(countSexyPairs(arr, n));

// This code is contributed by ipg2016107.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * sqrt(M))，其中 N 是给定数组中的元素个数，M 是数组中的最大元素。*
***辅助空间复杂度:** O(N)*