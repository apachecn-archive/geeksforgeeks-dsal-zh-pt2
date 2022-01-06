# 查找给定数组中不存在的[1，N]范围内的所有数字

> 原文:[https://www . geesforgeks . org/find-all-numbers-in-range-1-n-给定数组中不存在的数字/](https://www.geeksforgeeks.org/find-all-numbers-in-range-1-n-that-are-not-present-in-given-array/)

给定一个大小为 **N、**的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr[]** ，其中 **arr[i]** 是小于或等于 **N** 的自然数，任务是找出给定数组中不存在的**【1，N】**范围内的所有数字。

**示例:**

> **输入:** arr[ ] = {5，5，4，4，2}
> **输出:** 1 3
> **解释:**
> 对于范围[1，5]内的所有数字，数组中不存在 1 和 3。
> 
> **输入:** arr[ ] = {3，2，3，1}
> **输出:** 4

**简单方法:**最简单的方法是使用任何数据结构(如[字典](https://www.geeksforgeeks.org/python-dictionary/)对每个数组元素进行哈希，然后[遍历范围](https://www.geeksforgeeks.org/python-program-to-print-all-even-numbers-in-a-range/)**【1，N】**，并打印哈希中不存在的所有数字。

d

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**方法:**通过标记位置**arr[I]–1 处的数字，可以进一步优化上述方法，**否定标记 **i** 存在于数组中。然后打印数组元素缺失时的所有正位置。按照以下步骤解决问题:

*   [迭代数组，](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/) arr[]，对于每个当前元素， **num** 执行以下步骤:
    *   更新**arr[ABS(num)-1]**to**ABS(arr[ABS(num)-1)]。**
*   [使用变量 **i** 迭代数组，](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/) **arr[]** ，如果 **arr[i]** 为正，则打印 **i+1** 。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <iostream>
using namespace std;

// Function to find the missing numbers
void getMissingNumbers(int arr[], int N)
{
    // traverse the array arr[]
    for (int i = 0; i < N; i++) {
        // Update
        arr[abs(arr[i]) - 1] = -(abs(arr[abs(arr[i]) - 1]));
    }
    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        // If Num is not present
        if (arr[i] > 0)
            cout << i + 1 << " ";
    }
}

// Driver Code
int main()
{

    // Given Input
    int N = 5;
    int arr[] = { 5, 5, 4, 4, 2 };

    // Function Call
    getMissingNumbers(arr, N);
    return 0;
}
// This codeis contributed by dwivediyash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to find the missing numbers
    static void getMissingNumbers(int arr[], int N)
    {

        // traverse the array arr[]
        for (int i = 0; i < N; i++)
        {

            // Update
            arr[Math.abs(arr[i]) - 1]
                = -(Math.abs(arr[Math.abs(arr[i]) - 1]));
        }

        // Traverse the array arr[]
        for (int i = 0; i < N; i++)
        {

            // If Num is not present
            if (arr[i] > 0)
                System.out.print(i + 1 + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        int N = 5;
        int arr[] = { 5, 5, 4, 4, 2 };

        // Function Call
        getMissingNumbers(arr, N);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the missing numbers
def getMissingNumbers(arr):

    # Traverse the array arr[]
    for num in arr:

        # Update
        arr[abs(num)-1] = -(abs(arr[abs(num)-1]))

    # Traverse the array arr[]
    for pos, num in enumerate(arr):

        # If Num is not present
        if num > 0:
            print(pos + 1, end =' ')

# Given Input
arr = [5, 5, 4, 4, 2]

# Function Call
getMissingNumbers(arr)
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the missing numbers
static void getMissingNumbers(int []arr, int N)
{

    // traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

        // Update
        arr[Math.Abs(arr[i]) - 1] = -(Math.Abs(arr[Math.Abs(arr[i]) - 1]));
    }

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

        // If Num is not present
        if (arr[i] > 0)
          Console.Write(i + 1 + " ");
    }
}

// Driver Code
public static void Main()
{

    // Given Input
    int N = 5;
    int []arr = { 5, 5, 4, 4, 2 };

    // Function Call
    getMissingNumbers(arr, N);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the missing numbers
function getMissingNumbers(arr){

    // Traverse the array arr[]
    for(let num of arr)
        // Update
        arr[Math.abs(num)-1] = -(Math.abs(arr[Math.abs(num)-1]))

    // Traverse the array arr[]
    for (pos in arr)

        // If Num is not present
        if(arr[pos] > 0)
            document.write(`${parseInt(pos) + 1} `)
}

// Given Input
let arr = [5, 5, 4, 4, 2]

// Function Call
getMissingNumbers(arr)

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
1 3 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)