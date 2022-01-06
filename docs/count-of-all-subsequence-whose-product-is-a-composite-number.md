# 乘积为复合数的所有子序列的计数

> 原文:[https://www . geeksforgeeks . org/所有子序列的计数-谁的产品是复合数字/](https://www.geeksforgeeks.org/count-of-all-subsequence-whose-product-is-a-composite-number/)

给定一个**数组 arr[]** ，任务是从给定数组中找到非空子序列的数目，使得子序列的乘积是一个[合成数](https://www.geeksforgeeks.org/composite-number/)。
**例:**

> **输入:** arr[] = {2，3，4}
> **输出:** 5
> **解释:**
> 有 5 个子序列，它们的乘积是复合数{4}、{2，3}、{2，4}、{3，4}、{2，3，4}。
> **输入:** arr[] = {2，1，2}
> **输出:** 2
> **解释:**
> 有 2 个子序列，它们的乘积是复合数{2，2}、{2，1，2}

**方法:**用于查找此类子序列计数的方法类似于本文[中使用的方法](https://www.geeksforgeeks.org/number-of-subsequences-with-positive-product/)。此外，该方法可以稍加调整，以获得乘积为素数的子序列的计数。
要解决上面提到的问题，我们必须找到非空子序列的总数，**减去乘积不是复合数的子序列**。产品不是复合编号的 3 种可能情况是:

*   任何非空的 1 组合，即

> 功率(2，计数“1”)–1

*   长度为 1 的任何子序列，由基本上为
    的素数组成

> 素数计数

*   非空 1 与质数
    的组合

> (幂(2，1 的个数)–1)*(素数的计数)

以下是上述方法的实现:

## C++

```
// C++ implementation to count all
// subsequence whose product
// is Composite number

#include <bits/stdc++.h>
using namespace std;

// Function to check whether a
// number is prime or not
bool isPrime(int n)
{
    if (n <= 1)
        return false;
    for (int i = 2; i < n; i++)
        if (n % i == 0)

            return false;

    return true;
}

// Function to find number of subsequences
// whose product is a composite number
int countSubsequences(int arr[], int n)
{
    // Find total non empty subsequence
    int totalSubsequence = pow(2, n) - 1;

    int countPrime = 0, countOnes = 0;

    // Find count of prime number and ones
    for (int i = 0; i < n; i++) {
        if (arr[i] == 1)
            countOnes++;
        else if (isPrime(arr[i]))
            countPrime++;
    }

    int compositeSubsequence;

    // Calculate the non empty one subsequence
    int onesSequence = pow(2, countOnes) - 1;

    // Find count of composite subsequence
    compositeSubsequence
        = totalSubsequence - countPrime
          - onesSequence
          - onesSequence * countPrime;

    return compositeSubsequence;
}

// Driver code
int main()
{

    int arr[] = { 2, 1, 2 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countSubsequences(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count all
// subsequence whose product
// is Composite number
import java.util.*;
class GFG{

// Function to check whether a
// number is prime or not
static boolean isPrime(int n)
{
    if (n <= 1)
        return false;
    for (int i = 2; i < n; i++)
        if (n % i == 0)

            return false;

    return true;
}

// Function to find number of subsequences
// whose product is a composite number
static int countSubsequences(int arr[], int n)
{
    // Find total non empty subsequence
    int totalSubsequence = (int)(Math.pow(2, n) - 1);

    int countPrime = 0, countOnes = 0;

    // Find count of prime number and ones
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == 1)
            countOnes++;
        else if (isPrime(arr[i]))
            countPrime++;
    }

    int compositeSubsequence;

    // Calculate the non empty one subsequence
    int onesSequence = (int)(Math.pow(2, countOnes) - 1);

    // Find count of composite subsequence
    compositeSubsequence = totalSubsequence -
                                 countPrime -
                               onesSequence -
                               onesSequence *
                               countPrime;

    return compositeSubsequence;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 1, 2 };

    int n = arr.length;

    System.out.print(countSubsequences(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to count
# all subsequence whose product
# is composite number

# Function to check whether
# a number is prime or not
def isPrime(n):

    if (n <= 1):
        return False;

    for i in range(2, n):
        if (n % i == 0):
            return False;

    return True;

# Function to find number of subsequences
# whose product is a composite number
def countSubsequences(arr, n):

    # Find total non empty subsequence
    totalSubsequence = (int)(pow(2, n) - 1);

    countPrime = 0;
    countOnes = 0;

    # Find count of prime number and ones
    for i in range(n):
        if (arr[i] == 1):
            countOnes += 1;

        elif (isPrime(arr[i])):
            countPrime += 1;

    compositeSubsequence = 0;

    # Calculate the non empty one subsequence
    onesSequence = (int)(pow(2, countOnes) - 1);

    # Find count of composite subsequence
    compositeSubsequence = (totalSubsequence -
                                  countPrime -
                                onesSequence -
                                onesSequence *
                                  countPrime);

    return compositeSubsequence;

# Driver code
if __name__ == '__main__':

    arr = [ 2, 1, 2 ];
    n = len(arr);

    print(countSubsequences(arr, n));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation to count all
// subsequence whose product
// is Composite number
using System;
class GFG{

// Function to check whether a
// number is prime or not
static bool isPrime(int n)
{
    if (n <= 1)
        return false;
    for (int i = 2; i < n; i++)
        if (n % i == 0)

            return false;

    return true;
}

// Function to find number of subsequences
// whose product is a composite number
static int countSubsequences(int []arr, int n)
{
    // Find total non empty subsequence
    int totalSubsequence = (int)(Math.Pow(2, n) - 1);

    int countPrime = 0, countOnes = 0;

    // Find count of prime number and ones
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == 1)
            countOnes++;
        else if (isPrime(arr[i]))
            countPrime++;
    }

    int compositeSubsequence;

    // Calculate the non empty one subsequence
    int onesSequence = (int)(Math.Pow(2, countOnes) - 1);

    // Find count of composite subsequence
    compositeSubsequence = totalSubsequence -
                                 countPrime -
                               onesSequence -
                               onesSequence *
                                 countPrime;

    return compositeSubsequence;
}

// Driver code
public static void Main()
{
    int []arr = { 2, 1, 2 };

    int n = arr.Length;

    Console.Write(countSubsequences(arr, n));
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>

// Javascript implementation to count all
// subsequence whose product
// is Composite number

// Function to check whether a
// number is prime or not
function isPrime(n)
{
    if (n <= 1)
        return false;
    for (var i = 2; i < n; i++)
        if (n % i == 0)

            return false;

    return true;
}

// Function to find number of subsequences
// whose product is a composite number
function countSubsequences( arr, n)
{
    // Find total non empty subsequence
    var totalSubsequence = Math.pow(2, n) - 1;

    var countPrime = 0, countOnes = 0;

    // Find count of prime number and ones
    for (var i = 0; i < n; i++) {
        if (arr[i] == 1)
            countOnes++;
        else if (isPrime(arr[i]))
            countPrime++;
    }

    var compositeSubsequence;

    // Calculate the non empty one subsequence
    var onesSequence = Math.pow(2, countOnes) - 1;

    // Find count of composite subsequence
    compositeSubsequence
        = totalSubsequence - countPrime
          - onesSequence
          - onesSequence * countPrime;

    return compositeSubsequence;
}

// Driver code
var arr = [ 2, 1, 2 ];
var n = arr.length;
document.write( countSubsequences(arr, n));

</script>
```

**Output:** 

```
2
```