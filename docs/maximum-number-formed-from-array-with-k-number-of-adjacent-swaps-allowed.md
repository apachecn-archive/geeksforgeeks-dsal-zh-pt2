# 允许 K 个相邻交换的数组形成的最大数量

> 原文:[https://www . geeksforgeeks . org/允许从 k 个相邻交换的数组中形成最大数量/](https://www.geeksforgeeks.org/maximum-number-formed-from-array-with-k-number-of-adjacent-swaps-allowed/)

给定一个数组 **a[ ]** ，允许的相邻交换操作数为 **K** 。任务是找到使用这些交换操作可以形成的最大数量。
**例:**

> **输入:** a[]={ 1，2，9，8，1，4，9，9，9 }， K = 4
> **输出:**9 8 1 2 1 4 9 9 9
> 1<sup>ST</sup>交换 a[ ]后变为 1 9 2 8 1 4 9 9
> 2<sup>nd</sup>交换 a[ ]后变为 9 1 2 8 1 4 9 9
> 3<sup>rd</sup>交换 a[ ] 变成 9 1 8 2 1 4 9 9 9
> 4<sup>th</sup>交换 a[ ]变成 9 8 1 2 1 4 9 9 9
> **输入:** a[]={2，5，8，7，9}，K = 2
> **输出:** 8 2 5 7 9

**进场:**

*   从第一个数字开始，检查下一个 **K** 数字，并存储最大数字的索引。
*   通过交换相邻的数字，将最大的数字带到顶部。
*   通过相邻交换的次数减少到 **K** 的值。
*   重复上述步骤，直到交换次数为零。

以下是上述方法的实施

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the
// elements of the array
void print(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

// Exchange array elements one by
// one from  right to left side
// starting from the current position
// and ending at the target position
void swapMax(int* arr, int target_position,
                      int current_position)
{
    int aux = 0;
    for (int i = current_position;
         i > target_position; i--) {
        aux = arr[i - 1];
        arr[i - 1] = arr[i];
        arr[i] = aux;
    }
}

// Function to return the
// maximum number array
void maximizeArray(int* arr,
                   int length, int swaps)
{
    // Base condition
    if (swaps == 0)
        return;

    // Start from the first index
    for (int i = 0; i < length; i++) {
        int max_index = 0, max = INT_MIN;

        // Search for the next K elements
        int limit = (swaps + i) > length ?
                        length : swaps + i;

        // Find index of the maximum
        // element in next K elements
        for (int j = i; j <= limit; j++) {
            if (arr[j] > max) {
                max = arr[j];
                max_index = j;
            }
        }

        // Update the value of
        // number of swaps
        swaps -= (max_index - i);

        // Update the array elements by
        // swapping adjacent elements
        swapMax(arr, i, max_index);

        if (swaps == 0)
            break;
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 9, 8, 1, 4, 9, 9, 9 };
    int length = sizeof(arr) / sizeof(int);
    int swaps = 4;
    maximizeArray(arr, length, swaps);

    print(arr, length);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Function to print the
// elements of the array
static void print(int arr[], int n)
{
    for (int i = 0; i < n; i++)
    {
        System.out.print(arr[i] + " ");
    }
    System.out.println();
}

// Exchange array elements one by
// one from right to left side
// starting from the current position
// and ending at the target position
static void swapMax(int[] arr, int target_position,
                    int current_position)
{
    int aux = 0;
    for (int i = current_position;
        i > target_position; i--)
    {
        aux = arr[i - 1];
        arr[i - 1] = arr[i];
        arr[i] = aux;
    }
}

// Function to return the
// maximum number array
static void maximizeArray(int[] arr,
                int length, int swaps)
{
    // Base condition
    if (swaps == 0)
        return;

    // Start from the first index
    for (int i = 0; i < length; i++)
    {
        int max_index = 0, max = Integer.MIN_VALUE;

        // Search for the next K elements
        int limit = (swaps + i) > length ?
                        length : swaps + i;

        // Find index of the maximum
        // element in next K elements
        for (int j = i; j <= limit; j++)
        {
            if (arr[j] > max)
            {
                max = arr[j];
                max_index = j;
            }
        }

        // Update the value of
        // number of swaps
        swaps -= (max_index - i);

        // Update the array elements by
        // swapping adjacent elements
        swapMax(arr, i, max_index);

        if (swaps == 0)
            break;
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 9, 8, 1, 4, 9, 9, 9 };
    int length = arr.length;
    int swaps = 4;
    maximizeArray(arr, length, swaps);

    print(arr, length);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import sys

# Function to print the
# elements of the array
def print_ele(arr, n) :

    for i in range(n) :
        print(arr[i],end=" ");

    print();

# Exchange array elements one by
# one from right to left side
# starting from the current position
# and ending at the target position
def swapMax(arr, target_position,
                    current_position) :

    aux = 0;
    for i in range(current_position, target_position,-1) :
        aux = arr[i - 1];
        arr[i - 1] = arr[i];
        arr[i] = aux;

# Function to return the
# maximum number array
def maximizeArray(arr, length, swaps) :

    # Base condition
    if (swaps == 0) :
        return;

    # Start from the first index
    for i in range(length) :
        max_index = 0; max = -(sys.maxsize-1);

        # Search for the next K elements
        if (swaps + i) > length :
            limit = length
        else:
            limit = swaps + i

        # Find index of the maximum
        # element in next K elements
        for j in range(i, limit + 1) :
            if (arr[j] > max) :
                max = arr[j];
                max_index = j;

        # Update the value of
        # number of swaps
        swaps -= (max_index - i);

        # Update the array elements by
        # swapping adjacent elements
        swapMax(arr, i, max_index);

        if (swaps == 0) :
            break;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 9, 8, 1, 4, 9, 9, 9 ];
    length = len(arr);
    swaps = 4;
    maximizeArray(arr, length, swaps);

    print_ele(arr, length);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the sum
// and product of k smallest and
// k largest prime numbers in an array

using System;

class GFG
{

// Function to print the
// elements of the array
static void print(int []arr, int n)
{
    for (int i = 0; i < n; i++)
    {
        Console.Write(arr[i] + " ");
    }
    Console.WriteLine();
}

// Exchange array elements one by
// one from right to left side
// starting from the current position
// and ending at the target position
static void swapMax(int[] arr, int target_position,
                    int current_position)
{
    int aux = 0;
    for (int i = current_position;
        i > target_position; i--)
    {
        aux = arr[i - 1];
        arr[i - 1] = arr[i];
        arr[i] = aux;
    }
}

// Function to return the
// maximum number array
static void maximizeArray(int[] arr,
                int length, int swaps)
{
    // Base condition
    if (swaps == 0)
        return;

    // Start from the first index
    for (int i = 0; i < length; i++)
    {
        int max_index = 0, max = int.MinValue;

        // Search for the next K elements
        int limit = (swaps + i) > length ?
                        length : swaps + i;

        // Find index of the maximum
        // element in next K elements
        for (int j = i; j <= limit; j++)
        {
            if (arr[j] > max)
            {
                max = arr[j];
                max_index = j;
            }
        }

        // Update the value of
        // number of swaps
        swaps -= (max_index - i);

        // Update the array elements by
        // swapping adjacent elements
        swapMax(arr, i, max_index);

        if (swaps == 0)
            break;
    }
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 9, 8, 1, 4, 9, 9, 9 };
    int length = arr.Length;
    int swaps = 4;
    maximizeArray(arr, length, swaps);

    print(arr, length);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to print the
// elements of the array
function print(arr, n) {
    for (let i = 0; i < n; i++) {
        document.write(arr[i] + " ");
    }
    document.write("<br>");
}

// Exchange array elements one by
// one from right to left side
// starting from the current position
// and ending at the target position
function swapMax(arr, target_position, current_position) {
    let aux = 0;
    for (let i = current_position; i > target_position; i--) {
        aux = arr[i - 1];
        arr[i - 1] = arr[i];
        arr[i] = aux;
    }
}

// Function to return the
// maximum number array
function maximizeArray(arr, length, swaps) {
    // Base condition
    if (swaps == 0)
        return;

    // Start from the first index
    for (let i = 0; i < length; i++) {
        let max_index = 0, max = Number.MIN_SAFE_INTEGER;

        // Search for the next K elements
        let limit = (swaps + i) > length ?
            length : swaps + i;

        // Find index of the maximum
        // element in next K elements
        for (let j = i; j <= limit; j++) {
            if (arr[j] > max) {
                max = arr[j];
                max_index = j;
            }
        }

        // Update the value of
        // number of swaps
        swaps -= (max_index - i);

        // Update the array elements by
        // swapping adjacent elements
        swapMax(arr, i, max_index);

        if (swaps == 0)
            break;
    }
}

// Driver code

let arr = [1, 2, 9, 8, 1, 4, 9, 9, 9];
let length = arr.length;
let swaps = 4;
maximizeArray(arr, length, swaps);

print(arr, length);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
9 8 1 2 1 4 9 9 9
```

**时间复杂度:** O(N*N)其中 N 是给定数组的长度