# 最小化增量，使 N 的数字和至多为 S

> 原文:[https://www . geeksforgeeks . org/最小化增量到最多 n 位数的总和/](https://www.geeksforgeeks.org/minimize-increments-to-make-digit-sum-of-n-at-most-s/)

给定两个正整数 **N** 和 **S** 。任务是最小化 **N (N = N + 1)** 上使 **N** 的位数之和小于或等于 **S** 所需的增量数。
**注:** **N** 的范围可达一个 **18** 位数和 **1 < = S < = 162** 。

**示例:**

> ***输入:** N = 600，S = 5*
> ***输出:** 400*
> ***说明:**当 1000(600 + 400)的位数之和小于 5 时，需要最小 400 的增量。*
> 
> ***输入:** N = 345899211156769，S = 20*
> ***输出:**10078843231*
> ***说明:**最小要求增量为 10078843231。*

**方法:**这里的关键观察是，为了以最小增量最小化任何数字的位数总和，需要最小化从单位位置开始的位数。按照以下步骤解决给定的问题。

*   对于基本情况，如果 **N** 的位数之和已经小于或等于 **S** ，则输出为 **0** 。
*   初始化变量，比如说 **ans** =0 和 **p** = 1，其中 **ans** 将存储所需的最小增量， **p** 将从设备位置开始跟踪数字位置。
*   循环遍历 **N** 可以拥有的最大位数(即 18)，找到 **N** 的最后一位数字。用**数字**表示。然后找到将此**数字**转换为 **0** 所需的最小增量。用表示，说**加**。
    *   **数字=(不适用)10%**
    *   **相加= p * (10 位数)**
    *   通过**增加**来增加 **N** 和 **ans** 。
    *   现在检查 **N** 的位数之和是否小于等于 **S** 。
        *   如果条件为真，则脱离循环并输出答案。
        *   否则，将 **p** 乘以 10，从 **N** 的单位位置访问倒数第二位数字。
*   循环再次运行，并执行相同的步骤，直到找到所需的答案。
*   返回 **ans** 作为最终答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum
// of digits of N
int findSum(long long int N)
{
    // Stores the sum of digits of N
    int res = 0;

    // Loop to extract the digits of N
    // and find their sum
    while (N) {

        // Extracting the last digit of N
        // and adding it to res
        res += (N % 10);

        // Update N
        N /= 10;
    }

    return res;
}

// Function to find the minimum increments
// required to make the sum of digits of N
// less than or equal to S.
long long int minIncrements(long long int N, int S)
{
    // If the sum of digits of N is less than
    // or equal to S
    if (findSum(N) <= S) {

        // Output 0
        return 0;
    }

    // variable to access the digits of N
    long long int p = 1;

    // Stores the required answer
    long long int ans = 0;

    // Loop to access the digits of N
    for (int i = 0; i <= 18; ++i) {

        // Stores the digit of N starting
        // from unit's place
        int digit = (N / p) % 10;

        // Stores the increment required
        // to make the digit 0
        long long int add = p * (10 - digit);

        // Update N
        N += add;

        // Update ans
        ans += add;

        // If the sum of digits of N is less than
        // or equal to S
        if (findSum(N) <= S) {

            // Break from the loop
            break;
        }

        // Update p to access the next digit
        p = p * 10;
    }

    return ans;
}

// Driver Code
int main()
{

    // Given N and S
    long long int N = 345899211156769;
    int S = 20;

    // Function call
    cout << minIncrements(N, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

// Function to find the sum
// of digits of N
static int findSum(long N)
{

    // Stores the sum of digits of N
    int res = 0;

    // Loop to extract the digits of N
    // and find their sum
    while (N != 0) {

        // Extracting the last digit of N
        // and adding it to res
        res += (N % 10);

        // Update N
        N /= 10;
    }

    return res;
}

// Function to find the minimum increments
// required to make the sum of digits of N
// less than or equal to S.
static long minIncrements(long N, int S)
{

    // If the sum of digits of N is less than
    // or equal to S
    if (findSum(N) <= S) {

        // Output 0
        return 0;
    }

    // variable to access the digits of N
    long p = 1;

    // Stores the required answer
    long ans = 0;

    // Loop to access the digits of N
    for (int i = 0; i <= 18; ++i) {

        // Stores the digit of N starting
        // from unit's place
        long digit = (N / p) % 10;

        // Stores the increment required
        // to make the digit 0
        long add = p * (10 - digit);

        // Update N
        N += add;

        // Update ans
        ans += add;

        // If the sum of digits of N is less than
        // or equal to S
        if (findSum(N) <= S) {

            // Break from the loop
            break;
        }

        // Update p to access the next digit
        p = p * 10;
    }

    return ans;
}

// Driver Code
public static void main(String args[])
{
    // Given N and S
    long N = 345899211156769L;
    int S = 20;

    // Function call
    System.out.println(minIncrements(N, S));
}
}

// This code is contributed by Samim Hossain Mondal
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the sum
# of digits of N
def findSum(N):

  # Stores the sum of digits of N
  res = 0;

  # Loop to extract the digits of N
  # and find their sum
  while (N):

    # Extracting the last digit of N
    # and adding it to res
    res += (N % 10);

    # Update N
    N = N // 10;

  return res;

# Function to find the minimum increments
# required to make the sum of digits of N
# less than or equal to S.
def minIncrements(N, S):

  # If the sum of digits of N is less than
  # or equal to S
  if (findSum(N) <= S):

    # Output 0
    return 0;

  # variable to access the digits of N
  p = 1;

  # Stores the required answer
  ans = 0;

  # Loop to access the digits of N
  for i in range(0, 18):

    # Stores the digit of N starting
    # from unit's place
    digit = (N // p) % 10;

    # Stores the increment required
    # to make the digit 0
    add = p * (10 - digit);

    # Update N
    N += add;

    # Update ans
    ans += add;

    # If the sum of digits of N is less than
    # or equal to S
    if (findSum(N) <= S):

      # Break from the loop
      break;

    # Update p to access the next digit
    p = p * 10;

  return ans;

# Driver Code

# Given N and S
N = 345899211156769;
S = 20;

# Function call
print(minIncrements(N, S))

# This code is contributed by saurabh_jaiswal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;

class GFG
{

// Function to find the sum
// of digits of N
static long findSum(long N)
{

    // Stores the sum of digits of N
    long res = 0;

    // Loop to extract the digits of N
    // and find their sum
    while (N != 0) {

        // Extracting the last digit of N
        // and adding it to res
        res += (N % 10);

        // Update N
        N /= 10;
    }

    return res;
}

// Function to find the minimum increments
// required to make the sum of digits of N
// less than or equal to S.
static long minIncrements(long N, long S)
{

    // If the sum of digits of N is less than
    // or equal to S
    if (findSum(N) <= S) {

        // Output 0
        return 0;
    }

    // variable to access the digits of N
    long p = 1;

    // Stores the required answer
    long ans = 0;

    // Loop to access the digits of N
    for (int i = 0; i <= 18; ++i) {

        // Stores the digit of N starting
        // from unit's place
        long digit = (N / p) % 10;

        // Stores the increment required
        // to make the digit 0
        long add = p * (10 - digit);

        // Update N
        N += add;

        // Update ans
        ans += add;

        // If the sum of digits of N is less than
        // or equal to S
        if (findSum(N) <= S) {

            // Break from the loop
            break;
        }

        // Update p to access the next digit
        p = p * 10;
    }

    return ans;
}

// Driver Code
public static void Main()
{
    // Given N and S
    long N = 345899211156769;
    long S = 20;

    // Function call
    Console.Write(minIncrements(N, S));
}
}

// This code is contributed by Samim Hossain Mondal
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the sum
// of digits of N
function findSum(N)
{

  // Stores the sum of digits of N
  let res = 0;

  // Loop to extract the digits of N
  // and find their sum
  while (N) {

    // Extracting the last digit of N
    // and adding it to res
    res += (N % 10);

    // Update N
    N /= 10;
  }

  return res;
}

// Function to find the minimum increments
// required to make the sum of digits of N
// less than or equal to S.
function minIncrements(N, S) {
  // If the sum of digits of N is less than
  // or equal to S
  if (findSum(N) <= S) {

    // Output 0
    return 0;
  }

  // variable to access the digits of N
  let p = 1;

  // Stores the required answer
  let ans = 0;

  // Loop to access the digits of N
  for (let i = 0; i <= 18; ++i) {

    // Stores the digit of N starting
    // from unit's place
    let digit = (N / p) % 10;

    // Stores the increment required
    // to make the digit 0
    let add = p * (10 - digit);

    // Update N
    N += add;

    // Update ans
    ans += add;

    // If the sum of digits of N is less than
    // or equal to S
    if (findSum(N) <= S) {

      // Break from the loop
      break;
    }

    // Update p to access the next digit
    p = p * 10;
  }

  return ans;
}

// Driver Code

// Given N and S
let N = 345899211156769;
let S = 20;

// Function call
document.write(minIncrements(N, S))

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
100788843231
```

**时间复杂度:** O(18*logN)。

**辅助空间:** O(1)。