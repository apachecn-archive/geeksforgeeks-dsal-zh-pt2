# 数组中最大素数和最小素数之差

> 原文:[https://www . geesforgeks . org/数组中最大和最小素数之差/](https://www.geeksforgeeks.org/difference-between-the-largest-and-the-smallest-primes-in-an-array/)

给定一个整数数组，其中所有元素都小于 10^6.
任务是找出数组中最大素数和最小素数的区别。
**例:**

```
Input : Array = 1, 2, 3, 5
Output : Difference is 3
Explanation :
The largest prime number in the array is 5 and the smallest is 2
So, the difference is 3

Input : Array = 3, 5, 11, 17
Output : Difference is 14
```

**一个简单的方法:**
在基本的方法中，我们将检查数组的每个元素是否是质数。
然后，选择最大和最小的素数，打印差。
**高效方法:**
高效方法与基本方法非常相似。
我们将通过创建一个厄拉多塞的[筛，在 O(1)时间内检查数字是否为质数，来减少检查数字是否为质数的时间。
然后，我们将选择最大和最小的素数，并打印差值。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000000
bool prime[MAX + 1];

void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and initialize
    // all the entries as true. A value in prime[i] will
    // finally be false if 'i' is Not a prime, else true.

    memset(prime, true, sizeof(prime));

    // 1 is not prime
    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

int findDiff(int arr[], int n)
{
    // initial min max value
    int min = MAX + 2, max = -1;
    for (int i = 0; i < n; i++) {

        // check if the number is prime or not
        if (prime[arr[i]] == true) {

            // set the max and min values
            if (arr[i] > max)
                max = arr[i];
            if (arr[i] < min)
                min = arr[i];
        }
    }

    return (max == -1) ? -1 : (max - min);
}

// Driver code
int main()
{
    // create the sieve
    SieveOfEratosthenes();
    int n = 4;
    int arr[n] = { 1, 2, 3, 5 };

    int res = findDiff(arr, n);

    if (res == -1)
        cout << "No prime numbers" << endl;
    else
        cout << "Difference is " << res << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java implementation of the approach

import java.io.*;
class GFG {
static int MAX = 1000000;

static boolean prime[] = new boolean[MAX + 1];

static void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and initialize
    // all the entries as true. A value in prime[i] will
    // finally be false if 'i' is Not a prime, else true.

    //memset(prime, true, sizeof(prime));
    for(int i=0;i<MAX+1;i++)
    prime[i] =true;

    // 1 is not prime
    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

static int findDiff(int arr[], int n)
{
    // initial min max value
    int min = MAX + 2, max = -1;
    for (int i = 0; i < n; i++) {

        // check if the number is prime or not
        if (prime[arr[i]] == true) {

            // set the max and min values
            if (arr[i] > max)
                max = arr[i];
            if (arr[i] < min)
                min = arr[i];
        }
    }

    return (max == -1)? -1 : (max - min);
}

// Driver code

    public static void main (String[] args) {
        // create the sieve
    SieveOfEratosthenes();
    int n = 4;
    int arr[] = { 1, 2, 3, 5 };

    int res = findDiff(arr, n);

    if (res == -1)
        System.out.print( "No prime numbers") ;
    else
        System.out.println( "Difference is " + res);
    }
}

// This code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
MAX = 1000000

# Create a boolean array "prime[0..n]" and initialize
# all the entries as true. A value in prime[i] will
# finally be false if 'i' is Not a prime, else true
prime = [True]*(MAX+1)

def SieveOfEratosthenes():

    # 1 is not prime
    prime[1] = False

    p = 2
    c=0
    while (p * p <= MAX) :
        c+= 1

        # If prime[p] is not changed, then it is a prime
        if (prime[p] == True) :

            # Update all multiples of p

            for i in range( p * 2, MAX+1 , p):
                prime[i] = False

        p += 1

def findDiff(arr, n):

    # initial min max value
    min = MAX + 2
    max = -1

    for i in range(n) :

        # check if the number is prime or not
        if (prime[arr[i]] == True) :

            # set the max and min values
            #print("arra ",arr[i])
            #print("MAX ",max)
            #print(" MIN ",min)
            if (arr[i] > max):
                max = arr[i]
            if (arr[i] < min):
                min = arr[i]

    #print(" max ",max)
    return -1 if (max == -1) else (max - min)

# Driver code
if __name__ == "__main__":

    # create the sieve
    SieveOfEratosthenes()
    n = 4
    arr = [ 1, 2, 3, 5 ]

    res = findDiff(arr, n)

    if (res == -1):
        print("No prime numbers")
    else:
        print("Difference is " ,res )

# this code is contributed by
# ChitraNayal
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MAX = 1000000;

static bool []prime = new bool[MAX + 1];

static void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]"
    // and initialize all the entries as
    // true. A value in prime[i] will
    // finally be false if 'i' is Not a
    // prime, else true.

    // memset(prime, true, sizeof(prime));
    for(int i = 0; i < MAX + 1; i++)
    prime[i] = true;

    // 1 is not prime
    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

static int findDiff(int []arr, int n)
{
    // initial min max value
    int min = MAX + 2, max = -1;
    for (int i = 0; i < n; i++)
    {

        // check if the number is prime or not
        if (prime[arr[i]] == true)
        {

            // set the max and min values
            if (arr[i] > max)
                max = arr[i];
            if (arr[i] < min)
                min = arr[i];
        }
    }

    return (max == -1) ? -1 : (max - min);
}

// Driver code
public static void Main ()
{
    // create the sieve
    SieveOfEratosthenes();
    int n = 4;
    int []arr = { 1, 2, 3, 5 };

    int res = findDiff(arr, n);

    if (res == -1)
        Console.WriteLine( "No prime numbers") ;
    else
        Console.WriteLine( "Difference is " + res);
}
}

// This code is contributed by inder_verma
```

## java 描述语言

```
<script>
// Javascript implementation of above approach
MAX = 1000000;
prime = new Array(MAX + 1);
function SieveOfEratosthenes()
{

    // Create a boolean array "prime[0..n]" and initialize
    // all the entries as true. A value in prime[i] will
    // finally be false if 'i' is Not a prime, else true.
    prime.fill(true);

    // 1 is not prime
    prime[1] = false;

    for (var p = 2; p * p <= MAX; p++)
    {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (var i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

function findDiff(arr, n)
{
    // initial min max value
    var min = MAX + 2, max = -1;
    for (var i = 0; i < n; i++) {

        // check if the number is prime or not
        if (prime[arr[i]] == true)
        {

            // set the max and min values
            if (arr[i] > max)
                max = arr[i];
            if (arr[i] < min)
                min = arr[i];
        }
    }

    return (max == -1)? -1 : (max - min);
}

SieveOfEratosthenes();
var n = 4;
var arr = [ 1, 2, 3, 5 ];

var res = findDiff(arr, n);

if (res == -1)
   document.write( "No prime numbers" + "<br>" );
else
   document.write( "Difference is " + res + "<br>" );

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
Difference is 3
```