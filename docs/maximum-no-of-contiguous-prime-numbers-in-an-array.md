# 数组中相邻素数的最大数量

> 原文:[https://www . geeksforgeeks . org/数组中相邻质数的最大数量/](https://www.geeksforgeeks.org/maximum-no-of-contiguous-prime-numbers-in-an-array/)

给定一个由 N 个元素组成的数组 arr[]。任务是找出给定数组中连续素数的最大数量。
**例:**

```
Input: arr[] = {3, 5, 2, 66, 7, 11, 8}
Output: 3
Maximum contiguous prime number sequence is {2, 3, 5}

Input: arr[] = {1, 0, 2, 11, 32, 8, 9}
Output: 2
Maximum contiguous prime number sequence is {2, 11}
```

**进场:**

*   创建一个筛子来检查一个元素在 O(1)中是否是质数。
*   使用两个名为 current_max 和 max_so_far 的变量遍历数组。
*   如果找到一个质数，则增加 current_max，并将其与 max_so_far 进行比较。
*   如果当前最大值大于当前最大值，则将当前最大值赋给当前最大值
*   每次发现非素元素时，将 current_max 复位为 0。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

void SieveOfEratosthenes(bool prime[], int p_size)
{
    // false here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= p_size; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * p; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function that finds
// maximum contiguous subarray of prime numbers
int maxPrimeSubarray(int arr[], int n)
{
    int max_ele = *max_element(arr, arr+n);
    bool prime[max_ele + 1];
    memset(prime, true, sizeof(prime));

    SieveOfEratosthenes(prime, max_ele);

    int current_max = 0, max_so_far = 0;

    for (int i = 0; i < n; i++) {

        // check if element is non-prime
        if (prime[arr[i]] == false)
            current_max = 0;

        // If element is prime, than update
        // current_max and max_so_far accordingly.
        else {
            current_max++;
            max_so_far = max(current_max, max_so_far);
        }
    }

    return max_so_far;
}

// Driver code
int main()
{

    int arr[] = { 1, 0, 2, 4, 3, 29, 11, 7, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxPrimeSubarray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static void SieveOfEratosthenes(boolean prime[],
                                int p_size)
{
    // false here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= p_size; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p])
        {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * p; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function that finds
// maximum contiguous subarray of prime numbers
static int maxPrimeSubarray(int arr[], int n)
{
    int max_ele = Arrays.stream(arr).max().getAsInt();
    boolean prime[] = new boolean[max_ele + 1];
    Arrays.fill(prime, true);

    SieveOfEratosthenes(prime, max_ele);

    int current_max = 0, max_so_far = 0;

    for (int i = 0; i < n; i++)
    {
        // check if element is non-prime
        if (prime[arr[i]] == false)
            current_max = 0;

        // If element is prime, than update
        // current_max and max_so_far accordingly.
        else
        {
            current_max++;
            max_so_far = Math.max(current_max, max_so_far);
        }
    }
    return max_so_far;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 0, 2, 4, 3, 29, 11, 7, 8, 9 };
    int n = arr.length;
    System.out.print(maxPrimeSubarray(arr, n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of
# the approach

def SieveOfEratosthenes( prime, p_size):

    # false here indicates
    # that it is not prime
    prime[0] = False
    prime[1] = False
    for p in range(2,p_size+1):
        if(p*p>p_size):
            break

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]):

            # Update all multiples of p,
            # set them to non-prime
            i=p*p
            while(i<=p_size):
                prime[i] = False
                i = i + p

# Function that finds
# maximum contiguous subarray of prime numbers
def maxPrimeSubarray( arr, n):

    max_ele = max(arr)
    prime=[True]*(max_ele + 1)

    SieveOfEratosthenes(prime, max_ele)

    current_max = 0
    max_so_far = 0
    for i in range(n):

        # check if element is non-prime
        if (prime[arr[i]] == False):
            current_max = 0

        # If element is prime, than update
        # current_max and max_so_far accordingly.
        else:
            current_max=current_max + 1
            max_so_far = max(current_max, max_so_far)

    return max_so_far

# Driver code
if __name__=='__main__':
    arr = [ 1, 0, 2, 4, 3, 29, 11, 7, 8, 9 ]
    n = len(arr)
    print(maxPrimeSubarray(arr, n))

# this code is contributed by
# ash264
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;

class GFG
{

static void SieveOfEratosthenes(bool []prime,
                                int p_size)
{
    // false here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= p_size; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p])
        {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * p; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function that finds maximum
// contiguous subarray of prime numbers
static int maxPrimeSubarray(int []arr, int n)
{
    int max_ele = arr.Max();
    bool []prime = new bool[max_ele + 1];
    for(int i = 0; i < max_ele + 1; i++)
        prime[i]=true;

    SieveOfEratosthenes(prime, max_ele);

    int current_max = 0, max_so_far = 0;

    for (int i = 0; i < n; i++)
    {
        // check if element is non-prime
        if (prime[arr[i]] == false)
            current_max = 0;

        // If element is prime, than update
        // current_max and max_so_far accordingly.
        else
        {
            current_max++;
            max_so_far = Math.Max(current_max, max_so_far);
        }
    }
    return max_so_far;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 0, 2, 4, 3, 29, 11, 7, 8, 9 };
    int n = arr.Length;
    Console.Write(maxPrimeSubarray(arr, n));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

function SieveOfEratosthenes(prime, p_size)
{
    // false here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (var p = 2; p * p <= p_size; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (var i = p * p; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function that finds
// maximum contiguous subarray of prime numbers
function maxPrimeSubarray(arr, n)
{
    var max_ele = arr.reduce((a,b) => Math.max(a,b));
    var prime = Array(max_ele+1).fill(true);

    SieveOfEratosthenes(prime, max_ele);

    var current_max = 0, max_so_far = 0;

    for (var i = 0; i < n; i++) {

        // check if element is non-prime
        if (prime[arr[i]] == false)
            current_max = 0;

        // If element is prime, than update
        // current_max and max_so_far accordingly.
        else {
            current_max++;
            max_so_far = Math.max(current_max, max_so_far);
        }
    }

    return max_so_far;
}

// Driver code
var arr = [ 1, 0, 2, 4, 3, 29, 11, 7, 8, 9 ];
var n = arr.length;
document.write( maxPrimeSubarray(arr, n));

</script>
```

**Output**

```
4
```