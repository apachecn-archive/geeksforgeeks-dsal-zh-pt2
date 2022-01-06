# 相邻数字间有绝对差的 N 位数计数为 K

> 原文:[https://www . geesforgeks . org/n 位数计数-相邻位数之间有绝对差值-as-k/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-having-absolute-difference-between-adjacent-digits-as-k/)

给定两个整数 **N** 和**K**，任务是对所有**正整数**进行计数，其中**长度 N** 相邻数字之间的绝对差值等于 **K** 。

**示例:**

> **输入:** N = 4，K = 8
> **输出:** 3
> **说明:**每个数字每连续一位数的绝对差为 8。三个可能的数字是 8080、1919 和 9191。
> 
> **输入:** N = 2，K = 0
> **输出:** 9
> **解释:** 11，22，33，44，55，66，77，88，99。每个数字的每个连续数字之间的绝对差值是 0。

**方法:**该方法基于[递归](http://www.geeksforgeeks.org/recursion/)。对数字[1，9]进行迭代，对于每个数字，使用递归将具有绝对数字差的 N 位数字计为 K。下列情况出现在递归函数调用中。

*   **基本情况:**对于所有一位数整数，即 N = 1，递增答案计数。
*   **递归调用:**如果在到目前为止形成的数字(num)的**的数字**上加上数字 **K** 不超过 9，则通过减少 **N** 并使 **num = (num*10 + num%10 + K)** 进行递归调用。

> if(num % 10 + K ≤ 9)
> 递归 _ 函数(10 * num + (num % 10 + K)，N–1)；

*   如果所有递归调用后 **K** 的值都不为零，并且如果 **num % 10 ≥ K** ，则通过减少 **N** 再次递归调用，并将 **num** 更新为**(10 * num+num % 10–K)。**

> if(num % 10 ≥ K)
> 递归 _ 函数(10 * num+num % 10–K，N–1)

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// To store the count of numbers
int countNums = 0;

// Function that recursively finds the
// possible numbers and append into ans
void checkUtil(int num, int K, int N)
{
    // Base Case
    if (N == 1) {
        countNums++;
        return;
    }

    // Check the sum of last digit and k
    // less than or equal to 9 or not
    if ((num % 10 + K) <= 9)
        checkUtil(10 * num +
                  (num % 10 + K), K, N - 1);

    // If K = 0, then subtraction and
    // addition does not make any
    // difference
    if (K) {

        // If unit's digit greater than K
        if ((num % 10 - K) >= 0)
            checkUtil(10 * num +
                      num % 10 - K, K, N - 1);
    }
}

// Function to call checkUtil function
// for every integer from 1 to 9
void check(int K, int N)
{
    // Loop to check for
    // all digits from 1 to 9
    for (int i = 1; i <= 9; i++) {
        checkUtil(i, K, N);
    }
}

// Driver Code
int main()
{
    // Given N and K
    int N = 4, K = 8;
    check(K, N);

    // Count total possible numbers
    cout << countNums << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// To store the count of numbers
static int countNums = 0;

// Function that recursively finds the
// possible numbers and append into ans
static void checkUtil(int num, int K, int N)
{

    // Base Case
    if (N == 1) {
        countNums++;
        return;
    }

    // Check the sum of last digit and k
    // less than or equal to 9 or not
    if ((num % 10 + K) <= 9)
        checkUtil(10 * num +
                  (num % 10 + K), K, N - 1);

    // If K = 0, then subtraction and
    // addition does not make any
    // difference
    if (K>0) {

        // If unit's digit greater than K
        if ((num % 10 - K) >= 0)
            checkUtil(10 * num +
                      num % 10 - K, K, N - 1);
    }
}

// Function to call checkUtil function
// for every integer from 1 to 9
static void check(int K, int N)
{

    // Loop to check for
    // all digits from 1 to 9
    for (int i = 1; i <= 9; i++) {
        checkUtil(i, K, N);
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given N and K
    int N = 4, K = 8;
    check(K, N);

    // Count total possible numbers
    System.out.print(countNums +"\n");
}
}

// This code contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program for the above approach

# To store the count of numbers
countNums = 0;

# Function that recursively finds the
# possible numbers and append into ans
def checkUtil(num, K, N):
    global countNums;

    # Base Case
    if (N == 1):
        countNums += 1;
        return;

    # Check the sum of last digit and k
    # less than or equal to 9 or not
    if ((num % 10 + K) <= 9):
        checkUtil(10 * num + (num % 10 + K), K, N - 1);

    # If K = 0, then subtraction and
    # addition does not make any
    # difference
    if (K > 0):

        # If unit's digit greater than K
        if ((num % 10 - K) >= 0):
            checkUtil(10 * num + num % 10 - K, K, N - 1);

# Function to call checkUtil function
# for every integer from 1 to 9
def check(K, N):

    # Loop to check for
    # all digits from 1 to 9
    for i in range(1,10):
        checkUtil(i, K, N);

# Driver Code
if __name__ == '__main__':
    # Given N and K
    N = 4;
    K = 8;
    check(K, N);

    # Count total possible numbers
    print(countNums);

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// To store the count of numbers
static int countNums = 0;

// Function that recursively finds the
// possible numbers and append into ans
static void checkUtil(int num, int K, int N)
{

    // Base Case
    if (N == 1)
    {
        countNums++;
        return;
    }

    // Check the sum of last digit and k
    // less than or equal to 9 or not
    if ((num % 10 + K) <= 9)
        checkUtil(10 * num +
                 (num % 10 + K), K, N - 1);

    // If K = 0, then subtraction and
    // addition does not make any
    // difference
    if (K > 0)
    {

        // If unit's digit greater than K
        if ((num % 10 - K) >= 0)
            checkUtil(10 * num +
                      num % 10 - K, K, N - 1);
    }
}

// Function to call checkUtil function
// for every integer from 1 to 9
static void check(int K, int N)
{

    // Loop to check for
    // all digits from 1 to 9
    for(int i = 1; i <= 9; i++)
    {
        checkUtil(i, K, N);
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given N and K
    int N = 4, K = 8;
    check(K, N);

    // Count total possible numbers
    Console.Write(countNums + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // To store the count of numbers
      let countNums = 0;

      // Function that recursively finds the
      // possible numbers and append into ans
      function checkUtil(num, K, N)
      {

          // Base Case
          if (N == 1) {
              countNums++;
              return;
          }

          // Check the sum of last digit and k
          // less than or equal to 9 or not
          if ((num % 10 + K) <= 9)
              checkUtil(10 * num +
                  (num % 10 + K), K, N - 1);

          // If K = 0, then subtraction and
          // addition does not make any
          // difference
          if (K) {

              // If unit's digit greater than K
              if ((num % 10 - K) >= 0)
                  checkUtil(10 * num +
                      num % 10 - K, K, N - 1);
          }
      }

      // Function to call checkUtil function
      // for every integer from 1 to 9
      function check(K, N)
      {

          // Loop to check for
          // all digits from 1 to 9
          for (let i = 1; i <= 9; i++) {
              checkUtil(i, K, N);
          }
      }

      // Driver Code

      // Given N and K
      let N = 4, K = 8;
      check(K, N);

      // Count total possible numbers
      document.write(countNums + '<br>');

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
3
```

**时间复杂度:**O(2<sup>N</sup>)
T5】辅助空间: O(1)