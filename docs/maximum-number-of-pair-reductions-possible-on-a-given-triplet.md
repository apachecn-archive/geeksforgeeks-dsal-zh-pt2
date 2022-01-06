# 给定三元组上可能的最大配对减少数

> 原文:[https://www . geeksforgeeks . org/给定三元组上可能的最大成对减少数/](https://www.geeksforgeeks.org/maximum-number-of-pair-reductions-possible-on-a-given-triplet/)

给定一组整数 **(A，B，C)** ，任务是通过 **1** 计算给定三个整数的正对可以执行的最大递减次数。

**示例:**

> **输入:** A = 4，B = 3，C = 2
> **输出:** 4
> **说明:**
> 操作 1:减少对(4，3)。因此，三元组简化为{3，2，2}。
> 操作 2:减少对(3，2)。因此，三元组简化为{2，1，2}。
> 操作 3:减少对(2，2)。因此，三元组简化为{1，1，1}。
> 操作 3:减少对(1，1)。因此，三元组简化为{0，0，1}。
> 无法进行进一步操作。
> 
> **输入:** A = 7，B = 9，C = 6
> T3】输出: 11

**进场:**思路是用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决问题。按照以下步骤解决问题:

*   将三元组存储在[数组](https://www.geeksforgeeks.org/array-data-structure/)中。
*   初始化一个变量，比如**计数**，以存储可以在三元组上执行的最大可能缩减。
*   重复一个循环，直到前两个数组元素减少到 **0** ，并执行以下操作:
    *   [按递增顺序排列数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
    *   拾取两个最大数组元素，并将其减少 **1** 。
    *   将**计数**增加 **1** 。
*   打印**的值，将**计为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the maximum
// number of pair reductions
// possible on a given triplet
void maxOps(int a, int b, int c)
{

    // Convert them into an array
    int arr[] = { a, b, c };

    // Stores count of operations
    int count = 0;

    while (1) {

        // Sort the array
        sort(arr, arr + 3);

        // If the first two array
        // elements reduce to 0
        if (!arr[0] && !arr[1])
            break;

        // Apply the operations
        arr[1] -= 1;
        arr[2] -= 1;

        // Increment count
        count += 1;
    }

    // Print the maximum count
    cout << count;
}

// Driver Code
int main()
{
    // Given triplet
    int a = 4, b = 3, c = 2;
    maxOps(a, b, c);
    return 0;
}

// This code is contributed by subhammahato348.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to count the maximum
  // number of pair reductions
  // possible on a given triplet
  static void maxOps(int a, int b, int c)
  {

    // Convert them into an array
    int arr[] = { a, b, c };

    // Stores count of operations
    int count = 0;
    while (1 != 0)
    {

      // Sort the array
      Arrays.sort(arr);

      // If the first two array
      // elements reduce to 0
      if (arr[0] == 0 && arr[1] == 0)
        break;

      // Apply the operations
      arr[1] -= 1;
      arr[2] -= 1;

      // Increment count
      count += 1;
    }

    // Print the maximum count
    System.out.print(count);
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given triplet
    int a = 4, b = 3, c = 2;
    maxOps(a, b, c);
  }
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the maximum
# number of pair reductions
# possible on a given triplet
def maxOps(a, b, c):

  # Convert them into an array
  arr = [a, b, c]

  # Stores count of operations
  count = 0

  while True:

    # Sort the array
    arr.sort()

    # If the first two array
    # elements reduce to 0
    if not arr[0] and not arr[1]:
      break

    # Apply the operations
    arr[1] -= 1
    arr[2] -= 1

    # Increment count
    count += 1

  # Print the maximum count
  print(count)

# Given triplet
a, b, c = 4, 3, 2
maxOps(a, b, c)
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to count the maximum
  // number of pair reductions
  // possible on a given triplet
  static void maxOps(int a, int b, int c)
  {

    // Convert them into an array
    int[] arr = { a, b, c };

    // Stores count of operations
    int count = 0;
    while (1 != 0)
    {

      // Sort the array
      Array.Sort(arr);

      // If the first two array
      // elements reduce to 0
      if (arr[0] == 0 && arr[1] == 0)
        break;

      // Apply the operations
      arr[1] -= 1;
      arr[2] -= 1;

      // Increment count
      count += 1;
    }

    // Print the maximum count
    Console.WriteLine(count);
  }

// Driver Code
public static void Main(String[] args)
{
    // Given triplet
    int a = 4, b = 3, c = 2;
    maxOps(a, b, c);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the maximum
// number of pair reductions
// possible on a given triplet
function maxOps(a, b, c)
{

    // Convert them into an array
    let arr = [ a, b, c ];

    // Stores count of operations
    let count = 0;

    while (1) {

        // Sort the array
        arr.sort();

        // If the first two array
        // elements reduce to 0
        if (!arr[0] && !arr[1])
            break;

        // Apply the operations
        arr[1] -= 1;
        arr[2] -= 1;

        // Increment count
        count += 1;
    }

    // Print the maximum count
    document.write(count);
}

// Driver Code
    // Given triplet
    let a = 4, b = 3, c = 2;
    maxOps(a, b, c);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(max(arr[I])*(3 * log(3)))*
***辅助空间:** O(1)*