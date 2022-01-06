# 最大化给定数组中所有四元组的第二最小值之和

> 原文:[https://www . geeksforgeeks . org/给定阵列的最大每秒最小四倍数/](https://www.geeksforgeeks.org/maximize-sum-of-second-minimums-in-all-quadruples-of-a-given-array/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是选择一个四元组 **(i，j，k，l)** ，并计算所有可能的四元组的第二最小值之和。

***注:**保证 **N** 是 **4** 的倍数，每个阵元可以是单个四联的一部分。*

**示例:**

> **输入:** arr[] = {7，4，5，2，3，1，5，9}
> **输出:** 8
> **解释:**
> 四重 1: {7，1，5，9} = > 2 <sup>nd</sup> 最小值= 5。
> 四重 2: {4，5，2，3} = > 2 <sup>nd</sup> 最小值= 3。
> 因此，最大可能和为 8。
> 
> **输入:** arr[] = {7，4，3，3 }
> T3】输出: 3

**进场:**思路是用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决这个问题。以下是步骤:

*   初始化一个变量，比如**和**，以存储阵列的最大增益。
*   [按升序排列数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [反向遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并添加遇到的每三个元素。
*   打印得出的总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum possible sum of
// second minimums in each quadruple
void maxPossibleSum(int arr[], int N)
{

    // Sort the array
    sort(arr, arr + N);

    int sum = 0;
    int j = N - 3;

    while (j >= 0)
    {

        // Add the second minimum
        sum += arr[j];
        j -= 3;
    }

    // Print maximum possible sum
    cout << sum;
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 7, 4, 5, 2, 3, 1, 5, 9 };

    // Size of the array
    int N = 8;

    maxPossibleSum(arr, N);

    return 0;
}

// This code is contributed by aditya7409
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find maximum possible sum of
    // second minimums in each quadruple
    public static void maxPossibleSum(int[] arr, int N)
    {
        // Sort the array
        Arrays.sort(arr);

        int sum = 0;
        int j = N - 3;

        while (j >= 0) {

            // Add the second minimum
            sum += arr[j];
            j -= 3;
        }

        // Print maximum possible sum
        System.out.println(sum);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array
        int[] arr = { 7, 4, 5, 2, 3, 1, 5, 9 };

        // Size of the array
        int N = arr.length;

        maxPossibleSum(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find maximum possible sum of
# second minimums in each quadruple
def maxPossibleSum(arr,  N):

    # Sort the array
    arr.sort()
    sum = 0
    j = N - 3
    while (j >= 0):

        # Add the second minimum
        sum += arr[j]
        j -= 3

    # Print maximum possible sum
    print(sum)

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [7, 4, 5, 2, 3, 1, 5, 9]

    # Size of the array
    N = 8
    maxPossibleSum(arr, N)

    # This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to find maximum possible sum of
  // second minimums in each quadruple
  public static void maxPossibleSum(int[] arr, int N)
  {

    // Sort the array
    Array.Sort(arr);
    int sum = 0;
    int j = N - 3;
    while (j >= 0)
    {

      // Add the second minimum
      sum += arr[j];
      j -= 3;
    }

    // Print maximum possible sum
    Console.WriteLine(sum);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    // Given array
    int[] arr = { 7, 4, 5, 2, 3, 1, 5, 9 };

    // Size of the array
    int N = arr.Length;
    maxPossibleSum(arr, N);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// javascript program of the above approach

    // Function to find maximum possible sum of
    // second minimums in each quadruple
    function maxPossibleSum(arr, N)
    {
        // Sort the array
        arr.sort();

        let sum = 0;
        let j = N - 3;

        while (j >= 0) {

            // Add the second minimum
            sum += arr[j];
            j -= 3;
        }

        // Prlet maximum possible sum
        document.write(sum);
    }

    // Driver Code

     // Given array
        let arr = [ 7, 4, 5, 2, 3, 1, 5, 9 ];

        // Size of the array
        let N = arr.length;

        maxPossibleSum(arr, N);

// Thiscode is contributed by target_2.
</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)