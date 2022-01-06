# 大于其左侧所有元素的数组元素计数

> 原文:[https://www . geeksforgeeks . org/大于其左侧所有元素的数组元素计数/](https://www.geeksforgeeks.org/count-of-array-elements-which-are-greater-than-all-elements-on-its-left/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是计算数组元素的数量，使得它左边的所有元素都严格小于它。
**注:**数组的第一个元素将被认为始终满足条件。

**示例**:

> **输入** : arr[] = { 2，4，5，6 }
> **输出** : 4
> **说明:**
> 由于数组是递增顺序，所以所有数组元素都满足条件。
> 因此，这种元素的计数等于阵列的大小，即等于 4。
> 
> **输入** : { 3，3，3，3，3，3 }
> **输出** : 1
> **说明:**第一个数组元素是唯一满足条件的元素。

**方法:**
按照以下步骤解决问题:

*   设置**计数= 1** ，因为第一个数组元素将被认为满足条件。
*   将第一个数组元素(即**arr【0】**)设置为**最大值**。
*   从 **i =1** 开始遍历数组，将每个数组元素与当前的**最大值**进行比较。
*   如果发现一个数组元素大于当前的**最大值**，则该元素满足条件，因为它左边的所有元素都小于它。因此，*增加**计数**T5，*更新**最大值。****
*   最后，打印 ***计数。**T3】*

下面是上述方法的实现:

## C++

```
// C++ program to implement the
//above approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the count
// of array elements with all
// elements to its left smaller
// than it
int count_elements(int arr[], int n)
{

    // Stores the count
    int count = 1;

    // Stores the maximum
    int max = arr[0];

    // Iterate over the array
    for(int i = 1; i < n; i++)
    {

        // If an element greater
        // than maximum is obtained
        if (arr[i] > max)
        {

            // Increase count
            count += 1;

            // Update maximum
            max = arr[i];
        }
    }
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 2, 1, 4, 6, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << (count_elements(arr, n));
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
//above approach
import java.util.*;

class GFG{

// Function to return the count
// of array elements with all
// elements to its left smaller
// than it
static int count_elements(int arr[], int n)
{

    // Stores the count
    int count = 1;

    // Stores the maximum
    int max = arr[0];

    // Iterate over the array
    for(int i = 1; i < n; i++)
    {

        // If an element greater
        // than maximum is obtained
        if (arr[i] > max)
        {

            // Increase count
            count += 1;

            // Update maximum
            max = arr[i];
        }
    }
    return count;
}

// Driver Code
public static void main(String s[])
{
    int arr[] = { 2, 1, 4, 6, 3 };
    int n = arr.length;

    System.out.print(count_elements(arr, n));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to return the count
# of array elements with all
# elements to its left smaller
# than it

def count_elements(arr):

    # Stores the count
    count = 1

    # Stores the maximum
    max = arr[0]

    # Iterate over the array
    for i in range(1, len(arr)):

        # If an element greater
        # than maximum is obtained
        if arr[i] > max:

            # Increase count
            count += 1

            # Update maximum
            max = arr[i]
    return count

# Driver Code
arr = [2, 1, 4, 6, 3]
print(count_elements(arr))
```

## C#

```
// C# program to implement the
// above approach
using System;

class GFG{

// Function to return the count
// of array elements with all
// elements to its left smaller
// than it
static int count_elements(int[] arr, int n)
{

    // Stores the count
    int count = 1;

    // Stores the maximum
    int max = arr[0];

    // Iterate over the array
    for(int i = 1; i < n; i++)
    {

        // If an element greater
        // than maximum is obtained
        if (arr[i] > max)
        {

            // Increase count
            count += 1;

            // Update maximum
            max = arr[i];
        }
    }
    return count;
}

// Driver Code
public static void Main()
{
    int[] arr = { 2, 1, 4, 6, 3 };
    int n = arr.Length;

    Console.Write(count_elements(arr, n));
}
}

// This code is contributed by jrishabh99
```

## java 描述语言

```
<script>

// Javascript program to implement the
// above approach

// Function to return the count
// of array elements with all
// elements to its left smaller
// than it
function count_elements(arr, n)
{

    // Stores the count
    let count = 1;

    // Stores the maximum
    let max = arr[0];

    // Iterate over the array
    for(let i = 1; i < n; i++)
    {

        // If an element greater
        // than maximum is obtained
        if (arr[i] > max)
        {

            // Increase count
            count += 1;

            // Update maximum
            max = arr[i];
        }
    }
    return count;
}

// Driver Code
let arr = [ 2, 1, 4, 6, 3 ];
let n = arr.length;

document.write(count_elements(arr, n));

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
3
```

**时间复杂度:** *O(N)*
***辅助空间:** O(1)*