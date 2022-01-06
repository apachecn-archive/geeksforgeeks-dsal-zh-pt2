# 最小化使数组元素的和与积非零所需的增量或减量

> 原文:[https://www . geeksforgeeks . org/最小化-增量或减量-数组元素的和与积-非零/](https://www.geeksforgeeks.org/minimize-increments-or-decrements-required-to-make-sum-and-product-of-array-elements-non-zero/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算该数组所需的最小增量或减量操作数，使得该数组所有元素的和与[乘积](https://www.geeksforgeeks.org/program-for-product-of-array/) **arr[]** 都不为零。

**示例:**

> **输入:** arr[] = {-1，-1，0，0}
> **输出:** 2
> **解释:**执行以下操作将数组更新为:
> **操作 1:** 递增 arr[2]将数组修改为{-1，-1，1，0}。
> **操作 2:** 递减 arr[3]将数组修改为{-1，-1，1，-1}。
> 因此，上述数组的和与积为-2 和-1，即非零。
> 
> **输入:** arr[] = {-2，1，0 }
> T3】输出: 1

**方法:**给定的问题可以基于以下观察来解决:

*   使数组乘积非零所需的最小步骤，并且要使乘积非零，所有元素都必须非零。
*   如果和为负，则使数组的和为非零所需的最小步数，然后将所有 **0s** 元素递减 **1** ，如果和为正，则将所有零元素递增 **1** ，如果和为非零，则简单地递增或递减数组的任何元素。

请按照以下步骤解决此问题:

1.  [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并统计数组中的零个数。
2.  [求给定数组的和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)。
3.  如果零的计数**大于 0** ，那么结果就是该计数。
4.  否则如果和等于 0，那么结果就是 **1** 。
5.  否则结果将是 **0** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of array
int array_sum(int arr[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Return the sum
    return sum;
}

// Function that counts the minimum
// operations required to make the
// sum and product of array non-zero
int countOperations(int arr[], int N)
{
    // Stores count of zero elements
    int count_zeros = 0;

    // Iterate over the array to
    // count zero elements
    for (int i = 0; i < N; i++) {
        if (arr[i] == 0)
            count_zeros++;
    }

    // Sum of elements of the array
    int sum = array_sum(arr, N);

    // Print the result
    if (count_zeros)
        return count_zeros;

    if (sum == 0)
        return 1;

    return 0;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { -1, -1, 0, 0 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countOperations(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find the
// sum of array
static int array_sum(int arr[],
                     int n)
{
  int sum = 0;

  for (int i = 0; i < n; i++)
    sum += arr[i];

  // Return the sum
  return sum;
}

// Function that counts the minimum
// operations required to make the
// sum and product of array non-zero
static int countOperations(int arr[],
                           int N)
{
  // Stores count of zero
  // elements
  int count_zeros = 0;

  // Iterate over the array to
  // count zero elements
  for (int i = 0; i < N; i++)
  {
    if (arr[i] == 0)
      count_zeros++;
  }

  // Sum of elements of the
  // array
  int sum = array_sum(arr, N);

  // Print the result
  if (count_zeros != 0)
    return count_zeros;

  if (sum == 0)
    return 1;

  return 0;
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {-1, -1, 0, 0};

  // Size of array
  int N = arr.length;

  // Function Call
  System.out.print(countOperations(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to find the
# sum of array
def array_sum(arr, n):

    sum = 0

    for i in range(n):
        sum += arr[i]

    # Return the sum
    return sum

# Function that counts the minimum
# operations required to make the
# sum and product of array non-zero
def countOperations(arr, N):

    # Stores count of zero
    # elements
    count_zeros = 0

    # Iterate over the array to
    # count zero elements
    for i in range(N):
        if (arr[i] == 0):
            count_zeros+=1

    # Sum of elements of the
    # array
    sum = array_sum(arr, N)

    # Print result
    if (count_zeros):
        return count_zeros

    if (sum == 0):
        return 1

    return 0

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [-1, -1, 0, 0]

    # Size of array
    N = len(arr)

    # Function Call
    print(countOperations(arr, N))

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the
// sum of array
static int array_sum(int[] arr,
                     int n)
{
  int sum = 0;

  for(int i = 0; i < n; i++)
    sum += arr[i];

  // Return the sum
  return sum;
}

// Function that counts the minimum
// operations required to make the
// sum and product of array non-zero
static int countOperations(int[] arr,
                           int N)
{

  // Stores count of zero
  // elements
  int count_zeros = 0;

  // Iterate over the array to
  // count zero elements
  for(int i = 0; i < N; i++)
  {
    if (arr[i] == 0)
      count_zeros++;
  }

  // Sum of elements of the
  // array
  int sum = array_sum(arr, N);

  // Print the result
  if (count_zeros != 0)
    return count_zeros;

  if (sum == 0)
    return 1;

  return 0;
}

// Driver Code
public static void Main()
{

  // Given array arr[]
  int[] arr = { -1, -1, 0, 0 };

  // Size of array
  int N = arr.Length;

  // Function call
  Console.Write(countOperations(arr, N));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to find the
    // sum of array
    function array_sum(arr , n) {
        var sum = 0;

        for (i = 0; i < n; i++)
            sum += arr[i];

        // Return the sum
        return sum;
    }

    // Function that counts the minimum
    // operations required to make the
    // sum and product of array non-zero
    function countOperations(arr , N) {
        // Stores count of zero
        // elements
        var count_zeros = 0;

        // Iterate over the array to
        // count zero elements
        for (i = 0; i < N; i++) {
            if (arr[i] == 0)
                count_zeros++;
        }

        // Sum of elements of the
        // array
        var sum = array_sum(arr, N);

        // Prvar the result
        if (count_zeros != 0)
            return count_zeros;

        if (sum == 0)
            return 1;

        return 0;
    }

    // Driver Code

        // Given array arr
        var arr = [ -1, -1, 0, 0 ];

        // Size of array
        var N = arr.length;

        // Function Call
        document.write(countOperations(arr, N));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)