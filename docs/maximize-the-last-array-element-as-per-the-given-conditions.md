# 根据给定条件

最大化最后一个数组元素

> 原文:[https://www . geeksforgeeks . org/按给定条件最大化最后一个数组元素/](https://www.geeksforgeeks.org/maximize-the-last-array-element-as-per-the-given-conditions/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，重新排列该数组，使其满足以下条件:

1.  **arr[0]** 必须是 **1** 。
2.  相邻数组元素之差不应超过 **1** ，即所有 **1 ≤ i < N** 的**arr[I]–arr[I-1]≤1**。

允许的操作如下:

1.  以任何方式重新排列元素。
2.  **将**任意元素减少到任意数量≥ **1** 。

任务是找到可以放在数组最后一个索引处的最大可能值。

**示例:**

> **输入:** arr[] = {3，1，3，4}
> **输出:** 4
> **解释:**
> 从第一个元素中减去 1 会将数组修改为{2，1，3，4}。
> 交换前两个元素会将数组修改为{1，2，3，4}。
> 因此，放在最后一个索引处的最大值为 4。
> **输入:** arr[] = {1，1，1，1}
> **输出:** 1

**逼近:**
求解给定问题，对给定数组进行排序，按照给定条件从左向右进行平衡。按照以下步骤解决问题:

*   按升序对数组进行排序。
*   如果第一个元素不是 **1** ，那就变成 **1** 。
*   在索引**【1，N-1)**上遍历数组，检查每个相邻元素是否有 **≤ 1** 的差异。
*   如果不是，则递减该值，直到差值变为 **≤ 1** 。
*   返回数组的最后一个元素。

下面是上述问题的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum possible value
// that can be placed at the last index
int maximizeFinalElement(int arr[], int n)
{
    // Sort array in ascending order
    sort(arr, arr + n);

    // If the first element
    // is not equal to 1
    if (arr[0] != 1)
        arr[0] = 1;

    // Traverse the array to make
    // difference between adjacent
    // elements <=1
    for (int i = 1; i < n; i++) {
        if (arr[i] - arr[i - 1] > 1) {
            arr[i] = arr[i - 1] + 1;
        }
    }
    return arr[n - 1];
}

// Driver Code
int main()
{
    int n = 4;
    int arr[] = { 3, 1, 3, 4 };

    int max = maximizeFinalElement(arr, n);
    cout << max;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the maximum possible value
// that can be placed at the last index
public static int maximizeFinalElement(int arr[],
                                       int n)
{

    // Sort the array elements
    // in ascending order
    Arrays.sort(arr);

    // If the first element is
    // is not equal to 1
    if (arr[0] != 1)
        arr[0] = 1;

    // Traverse the array to make
    // difference between adjacent
    // elements <=1
    for(int i = 1; i < n; i++)
    {
        if (arr[i] - arr[i - 1] > 1)
        {
            arr[i] = arr[i - 1] + 1;
        }
    }
    return arr[n - 1];
}

// Driver Code
public static void main (String[] args)
{
    int n = 4;
    int arr[] = { 3, 1, 3, 4 };

    int max = maximizeFinalElement(arr, n);
    System.out.print(max);
}
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum possible value
# that can be placed at the last index
def maximizeFinalElement(arr, n):

    # Sort the array elements
    # in ascending order
    arr.sort();

    # If the first element is
    # is not equal to 1
    if (arr[0] != 1):
        arr[0] = 1;

    # Traverse the array to make
    # difference between adjacent
    # elements <=1
    for i in range(1, n):
        if (arr[i] - arr[i - 1] > 1):
            arr[i] = arr[i - 1] + 1;

    return arr[n - 1];

# Driver Code
if __name__ == '__main__':

    n = 4;
    arr = [3, 1, 3, 4];

    max = maximizeFinalElement(arr, n);
    print(max);

# This code is contributed by Princi Singh
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Function to find the maximum possible value
// that can be placed at the last index
public static int maximizeFinalElement(int []arr,
                                       int n)
{
    // Sort the array elements
    // in ascending order
    Array.Sort(arr);

    // If the first element is
    // is not equal to 1
    if (arr[0] != 1)
        arr[0] = 1;

    // Traverse the array to make
    // difference between adjacent
    // elements <=1
    for (int i = 1; i < n; i++)
    {
        if (arr[i] - arr[i - 1] > 1)
        {
            arr[i] = arr[i - 1] + 1;
        }
    }

    return arr[n - 1];
}

// Driver Code
public static void Main(String[] args)
{
    int n = 4;
    int []arr = { 3, 1, 3, 4 };

    int max = maximizeFinalElement(arr, n);
    Console.WriteLine(max);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

// Function to find the maximum possible value
// that can be placed at the last index
function maximizeFinalElement(arr, n)
{
    // Sort array in ascending order
    arr.sort((a, b) => a - b);

    // If the first element
    // is not equal to 1
    if (arr[0] != 1)
        arr[0] = 1;

    // Traverse the array to make
    // difference between adjacent
    // elements <=1
    for (let i = 1; i < n; i++) {
        if (arr[i] - arr[i - 1] > 1) {
            arr[i] = arr[i - 1] + 1;
        }
    }
    return arr[n - 1];
}

// Driver Code

    let n = 4;
    let arr = [ 3, 1, 3, 4 ];

    let max = maximizeFinalElement(arr, n);
    document.write(max);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*