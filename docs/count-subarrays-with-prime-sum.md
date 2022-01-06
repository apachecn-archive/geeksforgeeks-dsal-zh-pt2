# 用素数和计数子阵列

> 原文:[https://www . geesforgeks . org/count-subarray-with-prime-sum/](https://www.geeksforgeeks.org/count-subarrays-with-prime-sum/)

给定整数数组 A[]。任务是计算总和为质数(大小> 1)的子阵列总数。

**示例**:

```
Input : A[] = { 1, 2, 3, 4, 5 }
Output : 3
Subarrays are -> {1, 2}, {2, 3}, {3, 4}

Input : A = { 22, 33, 4, 1, 10 };
Output : 4
```

**逼近:** [生成所有可能的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并将它们的和存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中。迭代向量，检查和[是否为素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。它是增加计数。
您可以使用[筛除误差](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)来检查一个和是否是 O(1)中的素数。

下面是上述方法的实现:

## C++

```
// C++ program to count subarrays
// with Prime sum

#include <bits/stdc++.h>
using namespace std;

// Function to count subarrays
// with Prime sum
int primeSubarrays(int A[], int n)
{
    int max_val = int(pow(10, 7));

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    vector<bool> prime(max_val + 1, true);

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    int cnt = 0; // Initialize result

    // Traverse through the array
    for (int i = 0; i < n - 1; ++i) {
        int val = A[i];
        for (int j = i + 1; j < n; ++j) {
            val += A[j];

            if (prime[val])
                ++cnt;
        }
    }

    // return answer
    return cnt;
}

// Driver program
int main()
{
    int A[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(A) / sizeof(A[0]);

    cout << primeSubarrays(A, n);

    return 0;
}
```

Java 语言(一种计算机语言，尤用于创建网站)

```
 // Java program to count subarrays 
// with Prime sum 
import java.util.*;
class Solution
{

// Function to count subarrays 
// with Prime sum 
static int primeSubarrays(int A[], int n) 
{ 
    int max_val = (int)(Math.pow(10, 7)); 

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS 
    // THAN OR EQUAL TO max_val 
    // Create a boolean array "prime[0..n]". A 
    // value in prime[i] will finally be false 
    // if i is Not a prime, else true. 
    Vector<Boolean> prime=new Vector<Boolean>(max_val + 1); 

    //initialize initial value
    for (int p = 0; p <max_val + 1; p++)
    prime.add(p,true);

    // Remaining part of SIEVE 
    prime.set(0, false); 
    prime.set(1, false); 
    for (int p = 2; p * p <= max_val; p++) { 

        // If prime[p] is not changed, then 
        // it is a prime 
        if (prime.get(p) == true) { 

            // Update all multiples of p 
            for (int i = p * 2; i <= max_val; i += p) 
                prime.set(i, false); 
        } 
    } 

    int cnt = 0; // Initialize result 

    // Traverse through the array 
    for (int i = 0; i < n - 1; ++i) { 
        int val = A[i]; 
        for (int j = i + 1; j < n; ++j) { 
            val += A[j]; 

            if (prime.get(val)) 
                ++cnt; 
        } 
    } 

    // return answer 
    return cnt; 
} 

// Driver program 
public static void main(String args[])
{ 
    int A[] = { 1, 2, 3, 4, 5 }; 
    int n = A.length; 

    System.out.print( primeSubarrays(A, n)); 

} 
}
//contributed by Arnab Kundu 
```

## 蟒蛇 3

```
# Python3 program to count subarrays
# with Prime sum

# Function to count subarrays
# with Prime sum
def primeSubarrays(A, n):

    max_val = 10**7

    # USE SIEVE TO FIND ALL PRIME NUMBERS
    # LESS THAN OR EQUAL TO max_val
    # Create a boolean array "prime[0..n]". A
    # value in prime[i] will finally be false
    # if i is Not a prime, else true.
    prime = [True] * (max_val + 1)

    # Remaining part of SIEVE
    prime[0] = False
    prime[1] = False
    for p in range(2, int(max_val**(0.5)) + 1):

        # If prime[p] is not changed, then
        # it is a prime
        if prime[p] == True:

            # Update all multiples of p
            for i in range(2 * p, max_val + 1, p):
                prime[i] = False

    cnt = 0 # Initialize result

    # Traverse through the array
    for i in range(0, n - 1):
        val = A[i]
        for j in range(i + 1, n):
            val += A[j]

            if prime[val] == True:
                cnt += 1

    # return answer
    return cnt

# Driver Code
if __name__ == "__main__":

    A = [1, 2, 3, 4, 5]
    n = len(A)

    print(primeSubarrays(A, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to count subarrays
// with Prime sum

class Solution
{

// Function to count subarrays
// with Prime sum
static int primeSubarrays(int[] A, int n)
{
    int max_val = (int)(System.Math.Pow(10, 7));

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    bool[] prime=new bool[max_val + 1];

    //initialize initial value
    for (int p = 0; p <max_val + 1; p++)
    prime[p]=true;

    // Remaining part of SIEVE
    prime[0]=false;
    prime[1]=false;
    for (int p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime[i]=false;
        }
    }

    int cnt = 0; // Initialize result

    // Traverse through the array
    for (int i = 0; i < n - 1; ++i) {
        int val = A[i];
        for (int j = i + 1; j < n; ++j) {
            val += A[j];

            if (prime[val])
                ++cnt;
        }
    }

    // return answer
    return cnt;
}

// Driver program
static void Main()
{
    int[] A = { 1, 2, 3, 4, 5 };
    int n = A.Length;

    System.Console.WriteLine( primeSubarrays(A, n));

}
}
//contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count subarrays
// with Prime sum

// Function to count subarrays
// with Prime sum
function primeSubarrays($A, $n)
{
    $max_val = pow(10, 5);

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    $prime=array_fill(0,$max_val + 1,true);

    // Remaining part of SIEVE
    $prime[0] = false;
    $prime[1] = false;
    for ($p = 2; $p * $p <= $max_val; $p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if ($prime[$p] == true) {

            // Update all multiples of p
            for ($i = $p * 2; $i <= $max_val; $i += $p)
                $prime[$i] = false;
        }
    }

    $cnt = 0; // Initialize result

    // Traverse through the array
    for ($i = 0; $i < $n - 1; ++$i) {
        $val = $A[$i];
        for ($j = $i + 1; $j < $n; ++$j) {
            $val += $A[$j];

            if ($prime[$val])
                ++$cnt;
        }
    }

    // return answer
    return $cnt;
}

// Driver program

    $A = array( 1, 2, 3, 4, 5 );
    $n = count($A);

    echo primeSubarrays($A, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to count subarrays
// with Prime sum

// Function to count subarrays
// with Prime sum
function primeSubarrays(A, n)
{
    var max_val = parseInt(Math.pow(10, 7));

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    var prime = new Array(max_val + 1);
    prime.fill(true);
    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
    for (var p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (var i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    var cnt = 0; // Initialize result

    // Traverse through the array
    for (var i = 0; i < n - 1; ++i) {
        var val = A[i];
        for (var j = i + 1; j < n; ++j) {
            val += A[j];

            if (prime[val])
                ++cnt;
        }
    }

    // return answer
    return cnt;
}
    var A = [ 1, 2, 3, 4, 5 ];
    var n =A.length;

document.write( primeSubarrays(A, n));

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N <sup>2</sup> )