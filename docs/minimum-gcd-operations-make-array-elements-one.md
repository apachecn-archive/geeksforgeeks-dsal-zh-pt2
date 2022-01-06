# 使所有数组元素成为一个的最小 gcd 操作

> 原文:[https://www . geesforgeks . org/minimum-gcd-operations-make-array-elements-one/](https://www.geeksforgeeks.org/minimum-gcd-operations-make-array-elements-one/)

给定一个大小为 n 的数组 A[]。可以用该元素的 [gcd](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 替换数组中的任何数字，也可以用它的任何相邻元素替换。求这种运算的最小次数，使整个数组的元素等于 1。如果不可能打印-1。
**例:**

```
Input : A[] = {4, 8, 9}
Output : 3
Explanation:
In the first move we choose (8, 9) 
gcd(8, 9) = 1\. Now the array becomes {4, 1, 9}.
After second move, the array becomes {1, 1, 9}. 
After third move the array becomes {1, 1, 1}.

Input : A[] = { 5, 10, 2, 6 }
Output : 5
Explanation:
There is no pair with GCD equal one. We first
consider (5, 10) and replace 10 with 5\. Now array
becomes { 5, 5, 2, 6 }. Now we consider pair (5, 2)
and replace 5 with 1, array becomes { 5, 1, 2, 6 }.
We have a 1, so further steps are simple.

Input : A[] = {8, 10, 12}
Output : -1
Explanation:
Its not possible to make all the element equal to 1.

Input : A[] = { 8, 10, 12, 6, 3 }
Output : 7 
```

*   如果最初数组包含 1，我们的答案是数组的大小和数组中 1 的数量之差。
*   如果数组中没有等于 1 的元素。我们需要找到 GCD 等于 1 的最小子阵列。我们的结果是 N+(GCD 为 1 的最小子阵列的长度)–1。示例案例有{ 5，10，2，6 }和{ 8，10，12，6，3 }。

我们可以找到 O(N^2 的所有子阵列)并且 GCD 可以使用[欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)以 O(Log N)计算。
整体复杂度为 O(N^2 对数 n)。
下面是上述思路的实现。

## C++

```
// CPP program to find minimum GCD operations
// to make all array elements one.
#include <bits/stdc++.h>
using namespace std;

// Function to count number of moves.
int minimumMoves(int A[], int N)
{
   // Counting Number of ones.
    int one = 0;
    for (int i = 0; i < N; i++)
        if (A[i] == 1)
            one++;

    // If there is a one
    if (one != 0)
        return N - one;

    // Find smallest subarray with GCD equals
    // to one.
    int minimum = INT_MAX;
    for (int i = 0; i < N; i++) {
        int g = A[i]; // to calculate GCD
        for (int j = i + 1; j < N; j++) {
            g = __gcd(A[j], g);
            if (g == 1) {
                minimum = min(minimum, j - i);
                break;
            }
        }
    }

    if (minimum == INT_MAX) // Not Possible
        return -1;
    else
        return N + minimum - 1; // Final answer
}

// Driver code
int main()
{
    int A[] = { 2, 4, 3, 9 };
    int N = sizeof(A) / sizeof(A[0]);
    cout << minimumMoves(A, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum GCD operations
// to make all array elements one.
import java.util.*;

class GFG {

//__gcd function
static int __gcd(int a, int b)
{
    if (a == 0)
    return b;
    return __gcd(b % a, a);
}

// Function to count number of moves.
static int minimumMoves(int A[], int N)
{
    // Counting Number of ones.
    int one = 0;
    for (int i = 0; i < N; i++)
    if (A[i] == 1)
        one++;

    // If there is a one
    if (one != 0)
    return N - one;

    // Find smallest subarray with
    // GCD equals to one.
    int minimum = Integer.MAX_VALUE;
    for (int i = 0; i < N; i++) {

    // to calculate GCD
    int g = A[i];
    for (int j = i + 1; j < N; j++) {
        g = __gcd(A[j], g);
        if (g == 1) {
        minimum = Math.min(minimum, j - i);
        break;
        }
    }
    }

    if (minimum == Integer.MAX_VALUE) // Not Possible
    return -1;
    else
    return N + minimum - 1; // Final answer
}

// Driver code
public static void main(String[] args)
{
    int A[] = {2, 4, 3, 9};
    int N = A.length;
    System.out.print(minimumMoves(A, N));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# minimum GCD operations
# to make all array elements one.

#__gcd function
def __gcd(a,b):

    if (a == 0):
        return b
    return __gcd(b % a, a)

# Function to count number of moves.
def minimumMoves(A,N):

    # Counting Number of ones.
    one = 0
    for i in range(N):
        if (A[i] == 1):
            one+=1

    # If there is a one
    if (one != 0):
        return N - one

    # Find smallest subarray with GCD equals
    # to one.
    minimum = +2147483647
    for i in range(N):
        g = A[i] # to calculate GCD
        for j in range(i + 1,N):
            g = __gcd(A[j], g)
            if (g == 1):
                minimum = min(minimum, j - i)
                break

    if (minimum == +2147483647): # Not Possible
        return -1
    else:
        return N + minimum - 1; # Final answer

# Driver program
A = [ 2, 4, 3, 9 ]
N = len(A)
print(minimumMoves(A, N))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find minimum GCD operations
// to make all array elements one.
using System;

class GFG {

//__gcd function
static int __gcd(int a, int b)
{
    if (a == 0)
    return b;
    return __gcd(b % a, a);
}

// Function to count number of moves.
static int minimumMoves(int []A, int N)
{
    // Counting Number of ones.
    int one = 0;
    for (int i = 0; i < N; i++)
    if (A[i] == 1)
        one++;

    // If there is a one
    if (one != 0)
    return N - one;

    // Find smallest subarray with
    // GCD equals to one.
    int minimum = int.MaxValue;
    for (int i = 0; i < N; i++) {

    // to calculate GCD
    int g = A[i];
    for (int j = i + 1; j < N; j++) {
        g = __gcd(A[j], g);
        if (g == 1) {
        minimum = Math.Min(minimum, j - i);
        break;
        }
    }
    }

    if (minimum == int.MaxValue) // Not Possible
    return -1;
    else
    return N + minimum - 1; // Final answer
}

// Driver code
public static void Main()
{
    int []A = {2, 4, 3, 9};
    int N = A.Length;
    Console.WriteLine(minimumMoves(A, N));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// GCD operations to make all
// array elements one.

// __gcd function
function __gcd($a, $b)
{
    if ($a == 0)
    return $b;
    return __gcd($b % $a, $a);
}

// Function to count
// number of moves.
function minimumMoves($A, $N)
{
    // Counting Number of ones.
    $one = 0;
    for ($i = 0; $i < $N; $i++)
    if ($A[$i] == 1)
        $one++;

    // If there is a one
    if ($one != 0)
    return $N - $one;

    // Find smallest subarray 
    // with GCD equals to one.
    $minimum = PHP_INT_MAX;
    for ($i = 0; $i < $N; $i++)
    {

    // to calculate GCD
    $g = $A[$i];
    for ($j = $i + 1;
         $j < $N; $j++)
    {
        $g = __gcd($A[$j], $g);
        if ($g == 1)
        {
            $minimum = min($minimum,
                           $j - $i);
            break;
        }
    }
    }

    if ($minimum == PHP_INT_MAX) // Not Possible
    return -1;
    else
    return $N + $minimum - 1; // Final answer
}

// Driver code
$A = array(2, 4, 3, 9);
$N = sizeof($A);
echo (minimumMoves($A, $N));

// This code is contributed
// by akt_mit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find minimum
// GCD operations to make all
// array elements one.

// __gcd function
function __gcd(a, b)
{
    if (a == 0)
    return b;
    return __gcd(b % a, a);
}

// Function to count
// number of moves.
function minimumMoves(A, N)
{
    // Counting Number of ones.
    let one = 0;
    for (let i = 0; i < N; i++)
    if (A[i] == 1)
        one++;

    // If there is a one
    if (one != 0)
    return N - one;

    // Find smallest subarray 
    // with GCD equals to one.
    let minimum = Number.MAX_SAFE_INTEGER;
    for (let i = 0; i < N; i++)
    {

    // to calculate GCD
    let g = A[i];
    for (let j = i + 1;
         j < N; j++)
    {
        g = __gcd(A[j], g);
        if (g == 1)
        {
            minimum = Math.min(minimum,
                           j - i);
            break;
        }
    }
    }

    if (minimum == Number.MAX_SAFE_INTEGER) // Not Possible
    return -1;
    else
    return N + minimum - 1; // Final answer
}

// Driver code
let A = [2, 4, 3, 9];
let N = A.length;
document.write(minimumMoves(A, N));

// This code is contributed by _saurabh_jaiswal.

</script>
```

**输出:**

```
4
```