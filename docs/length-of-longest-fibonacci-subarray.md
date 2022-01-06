# 最长斐波那契子阵列的长度

> 原文:[https://www . geeksforgeeks . org/length-of-long-Fibonacci-subarray/](https://www.geeksforgeeks.org/length-of-longest-fibonacci-subarray/)

给定整数元素的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到 **arr[]** 的最大[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度，使得[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的所有元素都是[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。

**示例:**

> **输入:** arr[] = {11，8，21，5，3，28，4}
> **输出:** 4
> **解释:**
> 以所有元素为斐波那契数的最大长度子数组为{8，21，5，3}。
> 
> **输入:** arr[] = {25，100，36 }
> T3】输出: 0

**进场:**这个问题可以通过[穿越阵](https://www.geeksforgeeks.org/iterating-arrays-java/)**arr【】**来解决。按照下面的步骤来解决这个问题。

*   初始化变量，将 **max_length** 和 **current_length** 设为 **0** ，存储[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最大长度和[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的当前长度，使得[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中的每个元素都是[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代:
    *   如果当前数字是[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，那么将**当前 _ 长度**增加 **1** ，否则将**当前 _ 长度**设置为 **0。**
    *   现在，将**最大长度**指定为**当前长度**和**最大长度的最大值。**
*   完成以上步骤后，打印 **max_length** 作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// A utility function that returns
// true if x is perfect square
bool isPerfectSquare(int x)
{
    int s = sqrt(x);
    return (s * s == x);
}

// Returns true if n is a
// Fibinacci Number, else false
bool isFibonacci(int n)
{
    // Here n is Fibinac ci if one of 5*n*n + 4
    // or 5*n*n - 4 or both is a perferct square
    return isPerfectSquare(5 * n * n + 4)
           || isPerfectSquare(5 * n * n - 4);
}

// Function to find the length of the
// largest sub-array of an array every
// element of whose is a Fibonacci number
int contiguousFibonacciNumber(int arr[], int n)
{

    int current_length = 0;
    int max_length = 0;

    // Traverse the array arr[]
    for (int i = 0; i < n; i++) {

        // Check if arr[i] is a Fibonacci number
        if(isFibonacci(arr[i])) {
            current_length++;
        }
        else{
           current_length = 0;
        }

        // Stores the maximum length of the
        // Fibonacci number subarray
        max_length = max(max_length, current_length);
    }

    // Finally, return the maximum length
    return max_length;
}

// Driver code
int main()
{

    // Given Input
    int arr[] = { 11, 8, 21, 5, 3, 28, 4};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << contiguousFibonacciNumber(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;

class GFG
{

  // A utility function that returns
  // true if x is perfect square
  public static boolean isPerfectSquare(int x)
  {
    int s =(int) Math.sqrt(x);
    return (s * s == x);
  }

  // Returns true if n is a
  // Fibinacci Number, else false
  public static boolean isFibonacci(int n)
  {

    // Here n is Fibinacci if one of 5*n*n + 4
    // or 5*n*n - 4 or both is a perferct square
    return isPerfectSquare(5 * n * n + 4)
      || isPerfectSquare(5 * n * n - 4);
  }

  // Function to find the length of the
  // largest sub-array of an array every
  // element of whose is a Fibonacci number
  public static int contiguousFibonacciNumber(int arr[], int n)
  {

    int current_length = 0;
    int max_length = 0;

    // Traverse the array arr[]
    for (int i = 0; i < n; i++) {

      // Check if arr[i] is a Fibonacci number
      if (isFibonacci(arr[i])) {
        current_length++;
      }
      else {
        current_length = 0;
      }

      // Stores the maximum length of the
      // Fibonacci number subarray
      max_length = Math.max(max_length, current_length);
    }

    // Finally, return the maximum length
    return max_length;
  }

  // Driver code
  public static void main (String[] args)
  {

    // Given Input
    int arr[] = { 11, 8, 21, 5, 3, 28, 4 };
    int n = arr.length;

    // Function Cal
    System.out.println( contiguousFibonacciNumber(arr, n));
  }
}

 // This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# A utility function that returns
# true if x is perfect square
def isPerfectSquare(x):

    s = int(math.sqrt(x))

    if s * s == x:
        return True
    else:
        return False

# Returns true if n is a
# Fibonacci Number, else false
def isFibonacci(n):

    # Here n is fibonacci if one of 5*n*n+4
    # or 5*n*n-4 or both is a perfect square
    return (isPerfectSquare(5 * n * n + 4) or
            isPerfectSquare(5 * n * n - 4))

# Function to find the length of the
# largest sub-array of an array every
# element of whose is a Fibonacci number
def contiguousFibonacciNumber(arr, n):

    current_length = 0
    max_length = 0

    # Traverse the array arr
    for i in range(0, n):

        # Check if arr[i] is a Fibonacci number
        if isFibonacci(arr[i]):
            current_length += 1
        else:
            current_length = 0

        # stores the maximum length of the
        # Fibonacci number subarray
        max_length = max(max_length, current_length)

    # Finally, return the maximum length
    return max_length

# Driver code
if __name__ == '__main__':

    # Given Input
    arr = [ 11, 8, 21, 5, 3, 28, 4 ]
    n = len(arr)

    # Function Call
    print(contiguousFibonacciNumber(arr, n))

# This code is contributed by MuskanKalra1
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// A utility function that returns
// true if x is perfect square
static bool isPerfectSquare(int x)
{
    int s = (int)Math.Sqrt(x);
    return(s * s == x);
}

// Returns true if n is a
// Fibinacci Number, else false
static bool isFibonacci(int n)
{

    // Here n is Fibinacci if one of 5*n*n + 4
    // or 5*n*n - 4 or both is a perferct square
    return isPerfectSquare(5 * n * n + 4) ||
           isPerfectSquare(5 * n * n - 4);
}

// Function to find the length of the
// largest sub-array of an array every
// element of whose is a Fibonacci number
static int contiguousFibonacciNumber(int []arr, int n)
{
    int current_length = 0;
    int max_length = 0;

    // Traverse the array arr[]
    for(int i = 0; i < n; i++)
    {

        // Check if arr[i] is a Fibonacci number
        if (isFibonacci(arr[i]))
        {
            current_length++;
        }
        else
        {
            current_length = 0;
        }

        // Stores the maximum length of the
        // Fibonacci number subarray
        max_length = Math.Max(max_length,
                              current_length);
    }

    // Finally, return the maximum length
    return max_length;
}

// Driver code
public static void Main()
{

    // Given Input
    int []arr = { 11, 8, 21, 5, 3, 28, 4 };
    int n = arr.Length;

    // Function Call
    Console.Write(contiguousFibonacciNumber(arr, n));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach

      // A utility function that returns
      // true if x is perfect square
      function isPerfectSquare(x) {
          let s = parseInt(Math.sqrt(x));
          return (s * s == x);
      }

      // Returns true if n is a
      // Fibinacci Number, else false
      function isFibonacci(n)
      {

          // Here n is Fibinacci if one of 5*n*n + 4
          // or 5*n*n - 4 or both is a perferct square
          return isPerfectSquare(5 * n * n + 4)
              || isPerfectSquare(5 * n * n - 4);
      }

      // Function to find the length of the
      // largest sub-array of an array every
      // element of whose is a Fibonacci number
      function contiguousFibonacciNumber(arr, n) {

          let current_length = 0;
          let max_length = 0;

          // Traverse the array arr[]
          for (let i = 0; i < n; i++) {

              // Check if arr[i] is a Fibonacci number
              if (isFibonacci(arr[i])) {
                  current_length++;
              }
              else {
                  current_length = 0;
              }

              // Stores the maximum length of the
              // Fibonacci number subarray
              max_length = Math.max(max_length, current_length);
          }

          // Finally, return the maximum length
          return max_length;
      }

      // Driver code

      // Given Input
      let arr = [11, 8, 21, 5, 3, 28, 4];
      let n = arr.length;

      // Function Call
      document.write(contiguousFibonacciNumber(arr, n));

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)