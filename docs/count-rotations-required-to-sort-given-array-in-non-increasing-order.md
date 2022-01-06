# 以非递增顺序对给定数组进行排序所需的旋转计数

> 原文:[https://www . geeksforgeeks . org/count-rotations-按非递增顺序对给定数组进行排序所需的次数/](https://www.geeksforgeeks.org/count-rotations-required-to-sort-given-array-in-non-increasing-order/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是[按照非递增顺序](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)对数组进行逆时针旋转最小次数的排序。如果无法排序数组，则打印**-1”**。否则，打印旋转计数。

**示例:**

> **输入:** arr[] = {2，1，5，4，3}
> **输出:** 2
> **解释:**需要两次逆时针旋转才能按降序对数组进行排序，即{5，4，3，2，1}
> 
> **输入:** arr[] = {2，3，1}
> **输出:** -1

**方法:**思路是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并统计满足**arr【I+1】>arr【I】**的索引数。按照以下步骤解决问题:

*   将 **arr[i + 1] > arr[i]** 的计数存储在一个变量中，并在 **arr[i+1] > arr[i]** 时存储索引。
*   如果**计数**的值为**N–1**，则数组按非递减顺序排序。所需步骤完全是**(N-1)**。
*   如果**计数**的值为 **0** ，则数组已经按照非递增顺序排序。
*   如果**计数**的值为 **1** 和**arr[0]≤arr[N–1]**，则通过将所有数字移动到该指数，所需的转数等于**(指数+ 1)** 。此外，检查**arr[0]≤arr[N–1]**以确保序列不增加。
*   否则无法[对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行非递增排序。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count minimum anti-
// clockwise rotations required to
// sort the array in non-increasing order
void minMovesToSort(int arr[], int N)
{
    // Stores count of arr[i + 1] > arr[i]
    int count = 0;

    // Store last index of arr[i+1] > arr[i]
    int index;

    // Traverse the given array
    for (int i = 0; i < N - 1; i++) {

        // If the adjacent elements are
        // in increasing order
        if (arr[i] < arr[i + 1]) {

            // Increment count
            count++;

            // Update index
            index = i;
        }
    }

    // Print the result according
    // to the following conditions
    if (count == 0) {
        cout << "0";
    }
    else if (count == N - 1) {
        cout << N - 1;
    }
    else if (count == 1
             && arr[0] <= arr[N - 1]) {
        cout << index + 1;
    }

    // Otherwise, it is not
    // possible to sort the array
    else {
        cout << "-1";
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 1, 5, 4, 2 };
    int N = sizeof(arr)
            / sizeof(arr[0]);

    // Function Call
    minMovesToSort(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count minimum anti-
// clockwise rotations required to
// sort the array in non-increasing order
static void minMovesToSort(int arr[], int N)
{

    // Stores count of arr[i + 1] > arr[i]
    int count = 0;

    // Store last index of arr[i+1] > arr[i]
    int index = 0;

    // Traverse the given array
    for(int i = 0; i < N - 1; i++)
    {

        // If the adjacent elements are
        // in increasing order
        if (arr[i] < arr[i + 1])
        {

            // Increment count
            count++;

            // Update index
            index = i;
        }
    }

    // Print the result according
    // to the following conditions
    if (count == 0)
    {
        System.out.print("0");
    }
    else if (count == N - 1)
    {
        System.out.print(N - 1);
    }
    else if (count == 1 &&
            arr[0] <= arr[N - 1])
    {
        System.out.print(index + 1);
    }

    // Otherwise, it is not
    // possible to sort the array
    else
    {
        System.out.print("-1");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int[] arr = { 2, 1, 5, 4, 2 };
    int N = arr.length;

    // Function Call
    minMovesToSort(arr, N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count minimum anti-
# clockwise rotations required to
# sort the array in non-increasing order
def minMovesToSort(arr, N) :

    # Stores count of arr[i + 1] > arr[i]
    count = 0

    # Store last index of arr[i+1] > arr[i]
    index = 0

    # Traverse the given array
    for i in range(N-1):

        # If the adjacent elements are
        # in increasing order
        if (arr[i] < arr[i + 1]) :

            # Increment count
            count += 1

            # Update index
            index = i

    # Print result according
    # to the following conditions
    if (count == 0) :
        print("0")

    elif (count == N - 1) :
        print( N - 1)

    elif (count == 1
            and arr[0] <= arr[N - 1]) :
        print(index + 1)

    # Otherwise, it is not
    # possible to sort the array
    else :
        print("-1")

# Driver Code

# Given array
arr = [ 2, 1, 5, 4, 2 ]
N = len(arr)

# Function Call
minMovesToSort(arr, N)

# This code i contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count minimum anti-
// clockwise rotations required to
// sort the array in non-increasing order
static void minMovesToSort(int[] arr, int N)
{

    // Stores count of arr[i + 1] > arr[i]
    int count = 0;

    // Store last index of arr[i+1] > arr[i]
    int index = 0;

    // Traverse the given array
    for(int i = 0; i < N - 1; i++)
    {

        // If the adjacent elements are
        // in increasing order
        if (arr[i] < arr[i + 1])
        {

            // Increment count
            count++;

            // Update index
            index = i;
        }
    }

    // Print the result according
    // to the following conditions
    if (count == 0)
    {
        Console.Write("0");
    }
    else if (count == N - 1)
    {
        Console.Write(N - 1);
    }
    else if (count == 1 &&
             arr[0] <= arr[N - 1])
    {
        Console.Write(index + 1);
    }

    // Otherwise, it is not
    // possible to sort the array
    else
    {
        Console.Write("-1");
    }
}

// Driver Code
public static void Main()
{

    // Given array
    int[] arr = { 2, 1, 5, 4, 2 };
    int N = arr.Length;

    // Function Call
    minMovesToSort(arr, N);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count minimum anti-
// clockwise rotations required to
// sort the array in non-increasing order
function minMovesToSort(arr, N)
{

    // Stores count of arr[i + 1] > arr[i]
    let count = 0;

    // Store last index of arr[i+1] > arr[i]
    let index = 0;

    // Traverse the given array
    for(let i = 0; i < N - 1; i++)
    {

        // If the adjacent elements are
        // in increasing order
        if (arr[i] < arr[i + 1])
        {

            // Increment count
            count++;

            // Update index
            index = i;
        }
    }

    // Print result according
    // to the following conditions
    if (count == 0)
    {
        document.write("0");
    }
    else if (count == N - 1)
    {
        document.write(N - 1);
    }
    else if (count == 1 &&
             arr[0] <= arr[N - 1])
    {
        document.write(index + 1);
    }

    // Otherwise, it is not
    // possible to sort the array
    else
    {
        document.write("-1");
    }
}

// Driver Code

// Given array
let arr = [2, 1, 5, 4, 2];
let N = arr.length;

// Function Call
minMovesToSort(arr, N);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)