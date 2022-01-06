# 将所有元素移动到相同位置所需的最小成本

> 原文:[https://www . geeksforgeeks . org/将所有元素移动到相同位置所需的最低成本/](https://www.geeksforgeeks.org/minimum-cost-required-to-move-all-elements-to-the-same-position/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **位置[]** ，其中**位置【I】**表示 **i** <sup>第</sup>个元素的位置，任务是通过执行以下两个操作之一找到将所有元素移动到相同位置所需的最小成本:

*   从**位置【I】**移动到**位置【I】+2**或**位置【I】–2**。成本= 0。
*   从**位置【I】**移动到**位置【I】+1**或**位置【I】–1**。成本= 1。

**示例:**

> **输入:**位置[] = {1，2，3}
> **输出:** 1
> **说明:**
> 操作 1:将位置 3 的元素移到位置 1。成本= 0。
> 操作 2:将位置 2 的元素移动到位置 1。成本= 1。
> 因此，总成本= 1。
> 
> **输入:**位置[] = {2，2，2，3，3}
> **输出:** 2
> **说明:**将位置 3 的两个元素移到位置 2。每次操作的成本= 1。因此，总成本= 2。

**进场:**思路是[遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[统计奇偶元素数量](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)。对于涉及两个索引的增量或减量的每个操作，成本总是为 0。成本仅在元素从奇数位置移动到偶数位置时发生变化，反之亦然。因此，所需的最小成本是阵列**位置【】**中存在的奇数和偶数元素的数量的最小值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <iostream>
using namespace std;

// Function to find the minimum
// cost required to place all
// elements in the same position
int minCost(int arr[], int arr_size)
{

    // Stores the count of even
    // and odd elements
    int odd = 0, even = 0;

    // Traverse the array arr[]
    for(int i = 0; i < arr_size; i++)
    {

        // Count even elements
        if (arr[i] % 2 == 0)
            even++;

        // Count odd elements
        else
            odd++;
    }

    // Print the minimum count
    cout << min(even, odd);
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 1, 2, 3 };
    int arr_size = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    minCost(arr, arr_size);
}

// This code is contributed by khushboogoyal499
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;
class GFG {

    // Function to find the minimum
    // cost required to place all
    // elements in the same position
    public void minCost(int[] arr)
    {
        // Stores the count of even
        // and odd elements
        int odd = 0, even = 0;

        // Traverse the array arr[]
        for (int i = 0;
             i < arr.length;  i++) {

            // Count even elements
            if (arr[i] % 2 == 0)
                even++;

            // Count odd elements
            else
                odd++;
        }

        // Print the minimum count
        System.out.print(
            Math.min(even, odd));
    }

    // Driver Code
    public static void main(String[] args)
    {
        GFG obj = new GFG();

        // Given array
        int arr[] = { 1, 2, 3 };

        // Function Call
        obj.minCost(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum
# cost required to place all
# elements in the same position
def minCost(arr):

    # Stores the count of even
    # and odd elements
    odd = 0
    even = 0

    # Traverse the array arr[]
    for i in range(len(arr)):

        # Count even elements
        if (arr[i] % 2 == 0):
            even += 1

        # Count odd elements
        else:
            odd += 1

    # Print the minimum count
    print(min(even, odd))

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 1, 2, 3 ]

    # Function Call
    minCost(arr)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to find the minimum
// cost required to place all
// elements in the same position
public void minCost(int[] arr)
{

    // Stores the count of even
    // and odd elements
    int odd = 0, even = 0;

    // Traverse the array arr[]
    for(int i = 0; i < arr.Length; i++)
    {

        // Count even elements
        if (arr[i] % 2 == 0)
            even++;

        // Count odd elements
        else
            odd++;
    }

    // Print the minimum count
    Console.Write(Math.Min(even, odd));
}

// Driver Code
public static void Main()
{
    GFG obj = new GFG();

    // Given array
    int[] arr = { 1, 2, 3 };

    // Function Call
    obj.minCost(arr);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

    // Function to find the minimum
    // cost required to place all
    // elements in the same position
    function minCost(arr)
    {
        // Stores the count of even
        // and odd elements
        let odd = 0, even = 0;

        // Traverse the array arr[]
        for (let i = 0;
             i < arr.length;  i++) {

            // Count even elements
            if (arr[i] % 2 == 0)
                even++;

            // Count odd elements
            else
                odd++;
        }

        // Print the minimum count
        document.write(
            Math.min(even, odd));
    }

// Driver code

    // Given array
        let arr = [ 1, 2, 3 ];

        // Function Call
        minCost(arr);

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)