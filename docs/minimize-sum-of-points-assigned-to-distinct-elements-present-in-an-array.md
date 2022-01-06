# 最小化分配给数组中不同元素的点数总和

> 原文:[https://www . geeksforgeeks . org/最小化分配给不同元素的点数总和-数组中存在/](https://www.geeksforgeeks.org/minimize-sum-of-points-assigned-to-distinct-elements-present-in-an-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是为每个不同的[数组](https://www.geeksforgeeks.org/array-data-structure/)元素分配点，使得分配的点的总和尽可能最小。

分配点数时，需要满足以下条件:

*   一个数的最小点数是 1。
*   每个不同的元素都应该被赋予一个唯一的值。
*   点数应根据数字的值进行分配，即与较大的数字相比，较小的数字应被分配较低的点数。

**示例:**

> **输入:** N = 5，arr[] = {10，20，10，25}
> **输出:** 7
> **说明:**给 10 分配 1 分，给 20 分配 2 分，给 25 分配 3 分。点数之和= 1 + 2 + 1 + 3 = 7，这是最小可能。
> 
> **输入:** N = 4，arr[] = {7，7，7，7}
> **输出:** 4
> **说明:**给 7 赋 1 分。点的总和= 1 + 1 + 1 + 1 = 4，这是最小可能。

**方法:**这个问题可以通过将较低的点分配给较小的元素来解决[贪婪地](https://www.geeksforgeeks.org/greedy-algorithms/)。按照以下步骤解决问题:

*   将变量**和**初始化为 **1** ，以存储所需的结果。
*   [给定数组按递增顺序排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   将变量**点**初始化为 **1** 来存储当前元素的点。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代
    *   如果 **arr[i]** 等于 **arr[i+1]** ，则按**点**递增 **ans** 。
    *   否则将**点**的值增加 **1** ，然后将**点**加到**和**上。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to assign points to each
// number in an array such that the
// sum of points assigned is minimized
void findMinimumSum(int arr[], int n)
{
    // Sort the array in increasing order
    sort(arr, arr + n);

    // Assign point_value to 1
    int point_value = 1;

    // Store the required result
    int total_points = 1;

    // Traverse the array, arr[]
    for (int i = 0; i < n - 1; i++) {

        // If adjacent elements are same add
        // current point_value to total_point
        if (arr[i] == arr[i + 1])
            total_points += point_value;

        // Otherwise, assign a new point_value
        // and add it to total_points
        else {
            point_value = point_value + 1;
            total_points += point_value;
        }
    }

    // Print the result
    cout << total_points;
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 10, 20, 10, 25 };
    int n = 4;

    // Function Call
    findMinimumSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to assign points to each
// number in an array such that the
// sum of points assigned is minimized
static void findMinimumSum(int []arr, int n)
{

    // Sort the array in increasing order
    Arrays.sort(arr);

    // Assign point_value to 1
    int point_value = 1;

    // Store the required result
    int total_points = 1;

    // Traverse the array, arr[]
    for(int i = 0; i < n - 1; i++)
    {

        // If adjacent elements are same add
        // current point_value to total_point
        if (arr[i] == arr[i + 1])
            total_points += point_value;

        // Otherwise, assign a new point_value
        // and add it to total_points
        else
        {
            point_value = point_value + 1;
            total_points += point_value;
        }
    }

    // Print the result
    System.out.print(total_points);
}

// Driver Code
public static void main(String[] args)
{
    // Given Input
    int []arr = { 10, 20, 10, 25 };
    int n = 4;

    // Function Call
    findMinimumSum(arr, n);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to assign points to each
# number in an array such that the
# sum of points assigned is minimized
def findMinimumSum(arr, n):

    # Sort the array in increasing order
    arr = sorted(arr)

    # Assign point_value to 1
    point_value = 1

    # Store the required result
    total_points = 1

    # Traverse the array, arr[]
    for i in range(n - 1):

        # If adjacent elements are same add
        # current point_value to total_point
        if (arr[i] == arr[i + 1]):
            total_points += point_value

        # Otherwise, assign a new point_value
        # and add it to total_points
        else:
            point_value = point_value + 1
            total_points += point_value

    # Print the result
    print(total_points)

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ 10, 20, 10, 25 ]
    n = 4

    # Function Call
    findMinimumSum(arr, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to assign points to each
// number in an array such that the
// sum of points assigned is minimized
static void findMinimumSum(int []arr, int n)
{

    // Sort the array in increasing order
    Array.Sort(arr);

    // Assign point_value to 1
    int point_value = 1;

    // Store the required result
    int total_points = 1;

    // Traverse the array, arr[]
    for(int i = 0; i < n - 1; i++)
    {

        // If adjacent elements are same add
        // current point_value to total_point
        if (arr[i] == arr[i + 1])
            total_points += point_value;

        // Otherwise, assign a new point_value
        // and add it to total_points
        else
        {
            point_value = point_value + 1;
            total_points += point_value;
        }
    }

    // Print the result
    Console.Write(total_points);
}

// Driver Code
public static void Main()
{

    // Given Input
    int []arr = { 10, 20, 10, 25 };
    int n = 4;

    // Function Call
    findMinimumSum(arr, n);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to assign points to each
// number in an array such that the
// sum of points assigned is minimized
function findMinimumSum(arr, n) {
    // Sort the array in increasing order
    arr.sort((a, b) => a - b);

    // Assign point_value to 1
    let point_value = 1;

    // Store the required result
    let total_points = 1;

    // Traverse the array, arr[]
    for (let i = 0; i < n - 1; i++) {

        // If adjacent elements are same add
        // current point_value to total_point
        if (arr[i] == arr[i + 1])
            total_points += point_value;

        // Otherwise, assign a new point_value
        // and add it to total_points
        else {
            point_value = point_value + 1;
            total_points += point_value;
        }
    }

    // Print the result
    document.write(total_points);
}

// Driver Code

// Given Input
let arr = [10, 20, 10, 25];
let n = 4;

// Function Call
findMinimumSum(arr, n);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N * logN)* *****辅助空间:** O(1)***