# 将每个元素的绝对差之和与剩余数组的差最大化

> 原文:[https://www . geesforgeks . org/最大化每个元素与剩余数组的绝对差之和/](https://www.geeksforgeeks.org/maximize-difference-between-the-sum-of-absolute-differences-of-each-element-with-the-remaining-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是最大化一个元素的绝对差之和与数组中剩余元素的差。

**示例:**

> **输入:** arr[] = {1，2，4，7}
> **输出:** 6
> **解释:**
> 对于 i = 1，| 1–2 |+| 1–4 |+| 1–7 | = 1+3+6 = 10。
> 对于 i = 2，| 2–1 |+| 2–4 |+| 2–7 | = 1+2+5 = 8。
> 对于 i = 3，| 4–1 |+| 4–2 |+| 4–7 | = 3+2+3 = 8。
> 对于 i = 4，| 7–1 |+| 7–2 |+| 7–4 | = 6+5+3 = 14。
> 最大值=14，最小值=8。
> 因此，最大差值= 14–8 = 6。
> 
> **输入:** arr[] = {2，1，5，4，3}
> **输出:** 4

**天真方法:**最简单的想法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素，使用嵌套循环遍历数组，计算并存储其与剩余数组的绝对差之和。计算时，记录获得的最大值和最小值。最后，打印最大值和最小值之间的差值。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，这个想法是基于这样的观察:在一个[排序数组](https://www.geeksforgeeks.org/search-insert-and-delete-in-a-sorted-array/)中，对于任何索引 **i** ，它左边的元素会更小，而它右边的元素会更大。该排序数组中任何元素**arr【I】**的绝对差之和可以使用以下公式计算:

> (其左侧的元素数量)*(arr[i])–其左侧的元素总和+其右侧的元素总和–(其右侧的元素数量)*(arr[I])

按照以下步骤解决问题:

*   将 **totalSum** 初始化为 **0** 存储数组所有元素的和， **leftSum** 初始化为 **0** 存储任意索引左边元素的和。
*   初始化两个变量， **Max** 为[**INT _ MIN**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/)**MIN**为 [**INT_MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 。
*   [按升序排列数组**arr[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   使用变量 **i** 遍历数组、 **arr[]** ，并执行以下操作:
    *   使用**Sum =(I * arr[I])–left Sum+total Sum –((N–I–1)* arr[I])**中的公式存储 **arr[i]** 与其余元素的绝对差之和。
    *   将 **Max** 更新为 **Max** 和 **Sum** 的最大值。
    *   将 **Min** 更新为 **Min** 和 **Sum** 的最小值。
*   完成上述步骤后，打印**最大值**和**最小值**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to maximize difference of
// the sum of absolute difference of
// an element with the rest of the
// elements in the array
void findMaxDifference(int arr[], int n)
{
    // Sort the array in ascending order
    sort(arr, arr + n);

    // Stores prefix sum at any instant
    int Leftsum = 0;

    // Store the total array sum
    int Totalsum = 0;

    // Initialize minimum and maximum
    // absolute difference
    int Min = INT_MAX, Max = INT_MIN;

    // Traverse the array to find
    // the total array sum
    for (int i = 0; i < n; i++)
        Totalsum += arr[i];

    // Traverse the array arr[]
    for (int i = 0; i < n; i++) {

        // Store the number of
        // elements to its left
        int leftNumbers = i;

        // Store the number of
        // elements to its right
        int rightNumbers = n - i - 1;

        // Update the sum of elements
        // on its left
        Totalsum = Totalsum - arr[i];

        // Store the absolute difference sum
        int sum = (leftNumbers * arr[i])
                  - Leftsum
                  + Totalsum
                  - (rightNumbers * arr[i]);

        // Update the Minimum
        Min = min(Min, sum);

        // Update the Maximum
        Max = max(Max, sum);

        // Update sum of elements
        // on its left
        Leftsum += arr[i];
    }

    // Print the result
    cout << Max - Min;
}

// Driven Code
int main()
{
    int arr[] = { 1, 2, 4, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    findMaxDifference(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to maximize difference of
// the sum of absolute difference of
// an element with the rest of the
// elements in the array
static void findMaxDifference(int arr[], int n)
{

    // Sort the array in ascending order
    Arrays.sort(arr);

    // Stores prefix sum at any instant
    int Leftsum = 0;

    // Store the total array sum
    int Totalsum = 0;

    // Initialize minimum and maximum
    // absolute difference
    int Min = Integer.MAX_VALUE, Max = Integer.MIN_VALUE;

    // Traverse the array to find
    // the total array sum
    for (int i = 0; i < n; i++)
        Totalsum += arr[i];

    // Traverse the array arr[]
    for (int i = 0; i < n; i++)
    {

        // Store the number of
        // elements to its left
        int leftNumbers = i;

        // Store the number of
        // elements to its right
        int rightNumbers = n - i - 1;

        // Update the sum of elements
        // on its left
        Totalsum = Totalsum - arr[i];

        // Store the absolute difference sum
        int sum = (leftNumbers * arr[i])
                  - Leftsum
                  + Totalsum
                  - (rightNumbers * arr[i]);

        // Update the Minimum
        Min = Math.min(Min, sum);

        // Update the Maximum
        Max = Math.max(Max, sum);

        // Update sum of elements
        // on its left
        Leftsum += arr[i];
    }

    // Print the result
    System.out.print(Max - Min);
}

// Driven Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 4, 7 };
    int N = arr.length;
    findMaxDifference(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to maximize difference of
# the sum of absolute difference of
# an element with the rest of the
# elements in the array
def findMaxDifference(arr, n):

    # Sort the array in ascending order
    arr = sorted(arr)

    # Stores prefix sum at any instant
    Leftsum = 0

    # Store the total array sum
    Totalsum = 0

    # Initialize minimum and maximum
    # absolute difference
    Min, Max = 10**8, -10**8

    # Traverse the array to find
    # the total array sum
    for i in range(n):
        Totalsum += arr[i]

    # Traverse the array arr[]
    for i in range(n):

        # Store the number of
        # elements to its left
        leftNumbers = i

        # Store the number of
        # elements to its right
        rightNumbers = n - i - 1

        # Update the sum of elements
        # on its left
        Totalsum = Totalsum - arr[i]

        # Store the absolute difference sum
        sum = (leftNumbers * arr[i])- Leftsum + Totalsum - (rightNumbers * arr[i])

        # Update the Minimum
        Min = min(Min, sum)

        # Update the Maximum
        Max = max(Max, sum)

        # Update sum of elements
        # on its left
        Leftsum += arr[i]

    # Prthe result
    print (Max - Min)

# Driven Code
if __name__ == '__main__':
    arr = [1, 2, 4, 7]
    N = len(arr)
    findMaxDifference(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG
{

  // Function to maximize difference of
  // the sum of absolute difference of
  // an element with the rest of the
  // elements in the array
  static void findMaxDifference(int[] arr, int n)
  {

    // Sort the array in ascending order
    Array.Sort(arr);

    // Stores prefix sum at any instant
    int Leftsum = 0;

    // Store the total array sum
    int Totalsum = 0;

    // Initialize minimum and maximum
    // absolute difference
    int Minn = Int32.MaxValue, Maxx = Int32.MinValue;

    // Traverse the array to find
    // the total array sum
    for (int i = 0; i < n; i++)
      Totalsum += arr[i];

    // Traverse the array arr[]
    for (int i = 0; i < n; i++)
    {

      // Store the number of
      // elements to its left
      int leftNumbers = i;

      // Store the number of
      // elements to its right
      int rightNumbers = n - i - 1;

      // Update the sum of elements
      // on its left
      Totalsum = Totalsum - arr[i];

      // Store the absolute difference sum
      int sum = (leftNumbers * arr[i])
        - Leftsum
        + Totalsum
        - (rightNumbers * arr[i]);

      // Update the Minimum
      Minn = Math.Min(Minn, sum);

      // Update the Maximum
      Maxx = Math.Max(Maxx, sum);

      // Update sum of elements
      // on its left
      Leftsum += arr[i];
    }

    // Print the result
    Console.WriteLine(Maxx - Minn);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int[] arr = { 1, 2, 4, 7 };
    int N = arr.Length;
    findMaxDifference(arr, N);
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// javascript program of the above approach

// Function to maximize difference of
// the sum of absolute difference of
// an element with the rest of the
// elements in the array
function findMaxDifference(arr, n)
{

    // Sort the array in ascending order
    arr.sort();

    // Stores prefix sum at any instant
    let Leftsum = 0;

    // Store the total array sum
    let Totalsum = 0;

    // Initialize minimum and maximum
    // absolute difference
    let Min = Number.MAX_VALUE, Max = Number.MIN_VALUE;

    // Traverse the array to find
    // the total array sum
    for (let i = 0; i < n; i++)
        Totalsum += arr[i];

    // Traverse the array arr[]
    for (let i = 0; i < n; i++)
    {

        // Store the number of
        // elements to its left
        let leftNumbers = i;

        // Store the number of
        // elements to its right
        let rightNumbers = n - i - 1;

        // Update the sum of elements
        // on its left
        Totalsum = Totalsum - arr[i];

        // Store the absolute difference sum
        let sum = (leftNumbers * arr[i])
                  - Leftsum
                  + Totalsum
                  - (rightNumbers * arr[i]);

        // Update the Minimum
        Min = Math.min(Min, sum);

        // Update the Maximum
        Max = Math.max(Max, sum);

        // Update sum of elements
        // on its left
        Leftsum += arr[i];
    }

    // Prlet the result
    document.write(Max - Min);
}

    // Driver Code

     // Given array
        let arr = [ 1, 2, 4, 7 ];
    let N = arr.length;
    findMaxDifference(arr, N);

// This code is contributed by target_2.
</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*