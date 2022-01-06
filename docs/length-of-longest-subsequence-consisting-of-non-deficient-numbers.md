# 由非亏数组成的最长子序列的长度

> 原文:[https://www . geesforgeks . org/最长子序列长度-由非亏数组成/](https://www.geeksforgeeks.org/length-of-longest-subsequence-consisting-of-non-deficient-numbers/)

给定一个由 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是从不包含任何[亏数](https://www.geeksforgeeks.org/deficient-number/)的数组中找到最长的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度。

**示例:**

> **输入:** arr[] = {13，55，240，32，24，27，56，80，100，330，89}
> **输出:** 6
> **解释:**
> 不亏数的数组元素为{240，24，56，80，100，330 }
> 13 的除数为{1，13}。因此，除数之和= 14，小于 26(= 2 * 13)
> 55 的除数为{1，5，11，55}。因此，除数之和= 72，小于 110 ( = 2 * 55)。
> 32 的除数是{1，2，4，8，16，32}。因此，除数之和= 63，小于 64 ( = 2 * 32)。
> 27 的除数是{1，3，9，27}。因此，除数之和= 40，小于 54 ( = 2 * 27)。
> 89 的除数是{1，89}。因此，除数之和= 90，小于 178 ( = 2 * 89)。
> 因此，要求计数为 6。
> 
> **输入:** arr[] = {1，2，3，4，5，6}
> **输出:** 6
> **说明:**非亏数的数组元素为{1，2，3，4，5，6}

**方法:**解决问题的思路是简单地统计数组中存在的亏数。所有剩余数组元素的计数将是最长子序列所需的长度。按照以下步骤解决问题:

*   初始化一个变量，比如 **res** ，来存储非亏数组元素的计数。
*   [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】。对于每个数组元素，[检查是否为亏数](https://www.geeksforgeeks.org/deficient-number/)。
*   计算当前数组元素的所有因子的[和，如果**和**小于**2 * arr【I】**，则返回**真，**。否则，返回**假**。](https://www.geeksforgeeks.org/sum-of-all-proper-divisors-of-a-natural-number/)
*   如果发现某个数组元素为假，则增加 **res** 。
*   完成上述步骤后，打印 **res** 的值作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if n is
// a deficient number or not
bool isNonDeficient(int n)
{
    // Stores sum of divisors
    int sum = 0;

    // Iterate over the range [1, sqrt(N)]
    for (int i = 1; i <= sqrt(n); i++) {

        // If n is divisible by i
        if (n % i == 0) {

            // If divisors are equal,
            // add only one of them
            if (n / i == i) {
                sum = sum + i;
            }

            // Otherwise add both
            else {
                sum = sum + i;
                sum = sum + (n / i);
            }
        }
    }
    return sum >= 2 * n;
}

// Function to print the longest
// subsequence which does not
// contain any deficient numbers
int LongestNonDeficientSubsequence(int arr[], int n)
{
    // Stores the count of array
    // elements which are non-deficient
    int res = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If element is non-deficient
        if (isNonDeficient(arr[i])) {
            res += 1;
        }
    }

    // Return the answer
    return res;
}

// Driver Code
int main()
{
    int arr[]
        = { 13, 55, 240, 32, 24, 27,
            56, 80, 100, 330, 89 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << LongestNonDeficientSubsequence(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if n is
// a deficient number or not
static boolean isNonDeficient(int n)
{

    // Stores sum of divisors
    int sum = 0;

    // Iterate over the range [1, sqrt(N)]
    for(int i = 1; i <= Math.sqrt(n); i++)
    {

        // If n is divisible by i
        if (n % i == 0)
        {

            // If divisors are equal,
            // add only one of them
            if (n / i == i)
            {
                sum = sum + i;
            }

            // Otherwise add both
            else
            {
                sum = sum + i;
                sum = sum + (n / i);
            }
        }
    }
    return sum >= 2 * n;
}

// Function to print the longest
// subsequence which does not
// contain any deficient numbers
static int LongestNonDeficientSubsequence(int arr[],
                                          int n)
{

    // Stores the count of array
    // elements which are non-deficient
    int res = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // If element is non-deficient
        if (isNonDeficient(arr[i]))
        {
            res += 1;
        }
    }

    // Return the answer
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 13, 55, 240, 32, 24, 27,
                  56, 80, 100, 330, 89 };
    int N = arr.length;

    System.out.print(
        LongestNonDeficientSubsequence(arr, N));
}
}

// This code is contributed by splevel62
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check if n is
# a deficient number or not
def isNonDeficient(n):

    # Stores sum of divisors
    sum = 0

    # Iterate over the range [1, sqrt(N)]
    for i in range(1, int(math.sqrt(n)) + 1):

        # If n is divisible by i
        if (n % i == 0):

            # If divisors are equal,
            # add only one of them
            if (n // i == i):
                sum = sum + i

            # Otherwise add both
            else:
                sum = sum + i
                sum = sum + (n // i)

    return sum >= 2 * n

# Function to print the longest
# subsequence which does not
# contain any deficient numbers
def LongestNonDeficientSubsequence(arr, n):

    # Stores the count of array
    # elements which are non-deficient
    res = 0

    # Traverse the array
    for i in range(n):

        # If element is non-deficient
        if (isNonDeficient(arr[i])):
            res += 1

    # Return the answer
    return res

# Driver Code
if __name__ == "__main__":

    arr = [ 13, 55, 240, 32, 24, 27,
            56, 80, 100, 330, 89 ]
    N = len(arr)

    print(LongestNonDeficientSubsequence(arr, N))

# This code is contributed by chitranayal
```

## C#

```
// C# program for above approach
using System;

public class GFG
{

  // Function to check if n is
  // a deficient number or not
  static bool isNonDeficient(int n)
  {

    // Stores sum of divisors
    int sum = 0;

    // Iterate over the range [1, sqrt(N)]
    for(int i = 1; i <= Math.Sqrt(n); i++)
    {

      // If n is divisible by i
      if (n % i == 0)
      {

        // If divisors are equal,
        // add only one of them
        if (n / i == i)
        {
          sum = sum + i;
        }

        // Otherwise add both
        else
        {
          sum = sum + i;
          sum = sum + (n / i);
        }
      }
    }
    return sum >= 2 * n;
  }

  // Function to print the longest
  // subsequence which does not
  // contain any deficient numbers
  static int LongestNonDeficientSubsequence(int[] arr,
                                            int n)
  {

    // Stores the count of array
    // elements which are non-deficient
    int res = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

      // If element is non-deficient
      if (isNonDeficient(arr[i]))
      {
        res += 1;
      }
    }

    // Return the answer
    return res;
  }

  // Driver code
  public static void Main(String[] args)
  {
    int[] arr = { 13, 55, 240, 32, 24, 27,
                 56, 80, 100, 330, 89 };
    int N = arr.Length;

    Console.WriteLine(
      LongestNonDeficientSubsequence(arr, N));
  }
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>
// Js program for the above approach

// Function to check if n is
// a deficient number or not
function isNonDeficient( n)
{
    // Stores sum of divisors
    let sum = 0;

    // Iterate over the range [1, sqrt(N)]
    for (let i = 1; i <= Math.floor(Math.sqrt(n)); i++) {

        // If n is divisible by i
        if (n % i == 0) {

            // If divisors are equal,
            // add only one of them
            if (Math.floor(n / i) == i) {
                sum = sum + i;
            }

            // Otherwise add both
            else {
                sum = sum + i;
                sum = sum + Math.floor(n / i);
            }
        }
    }
    return sum >= 2 * n;
}

// Function to print the longest
// subsequence which does not
// contain any deficient numbers
function LongestNonDeficientSubsequence( arr, n)
{
    // Stores the count of array
    // elements which are non-deficient
    let res = 0;

    // Traverse the array
    for (let i = 0; i < n; i++) {

        // If element is non-deficient
        if (isNonDeficient(arr[i])) {
            res += 1;
        }
    }

    // Return the answer
    return res;
}
// Driver Code
    let arr
        = [ 13, 55, 240, 32, 24, 27,
            56, 80, 100, 330, 89 ];
    let N = arr.length;

   document.write( LongestNonDeficientSubsequence(arr, N));

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N<sup>3/2</sup>)*
***辅助空间:** O(N)*