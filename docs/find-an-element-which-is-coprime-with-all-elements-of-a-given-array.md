# 找到与给定数组的所有元素互质的元素

> 原文:[https://www . geeksforgeeks . org/find-一个与给定数组的所有元素互素的元素/](https://www.geeksforgeeks.org/find-an-element-which-is-coprime-with-all-elements-of-a-given-array/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找到一个大于 **1** 的整数，它是所有给定数组元素的[互素](https://www.geeksforgeeks.org/coprime-divisors-of-a-number/)。

**示例:**

> **输入:** arr[ ] = {10，13，17，19}
> **输出:** 23
> **解释:**
> 23 每一个数组元素的 GCD 为 1。因此，23 是所有给定数组元素的互素。
> 
> **输入:** arr[] = {13，17，23，24，50}
> **输出:** 53
> **说明:**
> 每阵 elem 53 的 GCD*ent*为 1。因此，53 与所有给定的数组元素是互质的。

**方法:**想法是利用大于[最大数组元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)的[素数](https://www.geeksforgeeks.org/prime-numbers/)将与所有给定数组元素互质的事实。因此，只需找到大于数组中最大元素[的质数。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find an element which
// is coprime with all array elements
int find_X(int arr[], int N)
{

    // Stores maximum array element
    int R = INT_MIN;
    for (int i = 0; i < N; i++)
        R = max(R, arr[i]);

    // Stores if index of an array is prime or not
    bool prime[1000001];
    for (int i = 0; i < 1000001; i++)
        prime[i] = true;

    int p = 2;
    while (p * p <= 1000002)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2; i < 1000001; i += p)
            {
                prime[i] = false;
            }
        }

        // Increment p by 1
        p = p + 1;
    }

    prime[0] = false;
    prime[1] = false;

    // Traverse the range [R, 10000000 + 1]
    for (int i = R; i < 1000001; i++) {

        // If i is greater than R and prime
        if (i > R and prime[i] == true) {

            // Return i
            return i;
        }
    }

    // Dummy value to omit return error
    return -1;
}

// Driven Program
int main()
{
    // Given array
    int arr[] = { 10, 13, 17, 19 };

    // stores the length of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << find_X(arr, N);

    return 0;
}

// This code is contributed by Kingash.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to find an element which
  // is coprime with all array elements
  static int find_X(int arr[])
  {

    // Stores maximum array element
    int R = Integer.MIN_VALUE;
    for (int i = 0; i < arr.length; i++)
      R = Math.max(R, arr[i]);

    // Stores if index of an array is prime or not
    boolean prime[] = new boolean[1000001];
    Arrays.fill(prime, true);

    int p = 2;
    while (p * p <= 1000002) {

      // If prime[p] is not changed,
      // then it is a prime
      if (prime[p] == true) {

        // Update all multiples of p
        for (int i = p * 2; i < 1000001; i += p) {
          prime[i] = false;
        }
      }
      // Increment p by 1
      p = p + 1;
    }

    prime[0] = false;
    prime[1] = false;

    // Traverse the range [R, 10000000 + 1]
    for (int i = R; i < 1000001; i++) {

      // If i is greater than R and prime
      if (i > R && prime[i] == true) {

        // Return i
        return i;
      }
    }

    // Dummy value to omit return error
    return -1;
  }

  // Driver Code
  public static void main(String[] args)
  {
    // Given array
    int arr[] = { 10, 13, 17, 19 };

    // Function call
    System.out.println(find_X(arr));
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

import math

# Function to find an element which
# is coprime with all array elements
def find_X(arr):

    # Stores maximum array element
    R = max(arr)

    # Stores if index of an array is prime or not
    prime = [True for i in range(0, 1000001)]

    p = 2
    while (p * p <= 1000002):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, 1000001, p):
                prime[i] = False

        # Increment p by 1
        p = p + 1

    prime[0] = False
    prime[1] = False

    # Traverse the range [R, 10000000 + 1]
    for i in range(R, 1000001):

        # If i is greater than R and prime
        if i > R and prime[i] == True:

           # Return i
            return i

# Driver Code
arr = [10, 13, 17, 19]
print(find_X(arr))
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find an element which
// is coprime with all array elements
static int find_X(int[] arr)
{

    // Stores maximum array element
    int R = Int32.MinValue;

    for(int i = 0; i < arr.Length; i++)
        R = Math.Max(R, arr[i]);

    // Stores if index of an array is prime or not
    bool[] prime = new bool[1000001];

    for(int i = 0; i < 1000001; i++)
    {
        prime[i] = true;
    }

    int p = 2;

    while (p * p <= 1000002)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2; i < 1000001; i += p)
            {
                prime[i] = false;
            }
        }

        // Increment p by 1
        p = p + 1;
    }

    prime[0] = false;
    prime[1] = false;

    // Traverse the range [R, 10000000 + 1]
    for(int i = R; i < 1000001; i++)
    {

        // If i is greater than R and prime
        if (i > R && prime[i] == true)
        {

            // Return i
            return i;
        }
    }

    // Dummy value to omit return error
    return -1;
}

// Driver Code
public static void Main(String []args)
{

    // Given array
    int[] arr = { 10, 13, 17, 19 };

    // Function call
    Console.WriteLine(find_X(arr));
}
}

// This code is contributed by souravghosh0416
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find an element which
// is coprime with all array elements
function find_X(arr)
{

    // Stores maximum array element
    let R = Number.MIN_VALUE;
    for(let i = 0; i < arr.length; i++)
        R = Math.max(R, arr[i]);

    // Stores if index of an array is prime or not
    let prime = Array(1000001).fill(true);

    let p = 2;
    while (p * p <= 1000002)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for(let i = p * 2; i < 1000001; i += p)
            {
                prime[i] = false;
            }
        }

        // Increment p by 1
        p = p + 1;
    }
    prime[0] = false;
    prime[1] = false;

    // Traverse the range [R, 10000000 + 1]
    for(let i = R; i < 1000001; i++)
    {

        // If i is greater than R and prime
        if (i > R && prime[i] == true)
        {

            // Return i
            return i;
        }
    }

    // Dummy value to omit return error
    return -1;
}

// Driver code

// Given array
let arr = [ 10, 13, 17, 19 ];

// Function call
document.write(find_X(arr));

// This code is contributed by target_2   

</script>
```

**Output:** 

```
23
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*