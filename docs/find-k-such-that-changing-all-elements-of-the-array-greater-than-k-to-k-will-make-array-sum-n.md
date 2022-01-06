# 求 K，将数组中大于 K 的所有元素都改为 K，会使数组和为 N

> 原文:[https://www . geesforgeks . org/find-k-so-changing-all-elements-of-the-array-大于-k-to-k-make-array-sum-n/](https://www.geeksforgeeks.org/find-k-such-that-changing-all-elements-of-the-array-greater-than-k-to-k-will-make-array-sum-n/)

给定一个数组 **arr[]** 和一个整数 **N** ，任务是从给定的数组中找到一个数字 **K** ，这样如果大于 **K** 的 **arr** 中的所有元素都变成了 **K** ，那么得到的数组中所有元素的和就是 **N** 。如果不可能，打印 **-1** 。
**举例:**

> **输入:** arr[] = {3，1，10，8，4}，N = 16
> **输出:** 4
> 如果大于 4 的所有元素都变为 4，则结果数组将为{3，1，4，4，4}
> 因此总和将为 16，这是 N 的必需值。
> **输入:** arr[] = {3，1，10，8，4}，N = 11
> 【T11

**做法:**思路是用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)解决上述问题。

*   首先，按升序对数组进行排序。
*   然后遍历数组，对于每个元素**arr【I】**。
*   假设所有的元素在它被更改为 **arr[i]** 之后，计算总和。
*   如果等于 **N** 则返回**arr【I】**。
*   如果到达数组末尾，则打印 **-1** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return K such that changing
// all elements greater than K to K will
// make array sum N otherwise return -1
int findK(int arr[], int size, int N)
{

    // Sorting the array in increasing order
    sort(arr, arr + size);
    int temp_sum = 0;

    // Loop through all the elements of the array
    for (int i = 0; i < size; i++) {
        temp_sum += arr[i];

        // Checking if sum of array equals N
        if (N - temp_sum == arr[i] * (size - i - 1)) {
            return arr[i];
        }
    }
    return -1;
}

// Driver code
int main()
{
    int arr[] = { 3, 1, 10, 4, 8 };
    int size = sizeof(arr) / sizeof(int);
    int N = 16;

    cout << findK(arr, size, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return K such that changing
    // all elements greater than K to K will
    // make array sum N otherwise return -1
    static int findK(int arr[], int size, int N)
    {

        // Sorting the array in increasing order
        Arrays.sort(arr);
        int temp_sum = 0;

        // Loop through all the elements of the array
        for (int i = 0; i < size; i++)
        {
            temp_sum += arr[i];

            // Checking if sum of array equals N
            if (N - temp_sum == arr[i] * (size - i - 1))
            {
                return arr[i];
            }
        }
        return -1;
    }

    // Driver code
    public static void main (String[] args)
    {
        int []arr = { 3, 1, 10, 4, 8 };
        int size = arr.length;
        int N = 16;

        System.out.print(findK(arr, size, N));
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return K such that changing
# all elements greater than K to K will
# make array sum N otherwise return -1
def findK(arr, size, N):

    # Sorting the array in increasing order
    arr = sorted(arr)
    temp_sum = 0

    # Loop through all the elements of the array
    for i in range(size):
        temp_sum += arr[i]

        # Checking if sum of array equals N
        if (N - temp_sum == arr[i] * (size - i - 1)):
            return arr[i]
    return -1

# Driver code
arr = [3, 1, 10, 4, 8]
size = len(arr)
N = 16

print(findK(arr, size, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return K such that changing
    // all elements greater than K to K will
    // make array sum N otherwise return -1
    static int findK(int []arr, int size, int N)
    {

        // Sorting the array in increasing order
        Array.Sort(arr);
        int temp_sum = 0;

        // Loop through all the elements of the array
        for (int i = 0; i < size; i++)
        {
            temp_sum += arr[i];

            // Checking if sum of array equals N
            if (N - temp_sum == arr[i] * (size - i - 1))
            {
                return arr[i];
            }
        }
        return -1;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 3, 1, 10, 4, 8 };
        int size = arr.Length;
        int N = 16;

        Console.Write(findK(arr, size, N));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return K such that changing
    // all elements greater than K to K will
    // make array sum N otherwise return -1
    function findK(arr, size, N)
    {

        // Sorting the array in increasing order
        arr.sort(function(a, b){return a - b});
        let temp_sum = 0;

        // Loop through all the elements of the array
        for (let i = 0; i < size; i++)
        {
            temp_sum += arr[i];

            // Checking if sum of array equals N
            if (N - temp_sum == arr[i] * (size - i - 1))
            {
                return arr[i];
            }
        }
        return -1;
    }

    let arr = [ 3, 1, 10, 4, 8 ];
    let size = arr.length;
    let N = 16;

    document.write(findK(arr, size, N));

// This code is contributed by divyesh07019.
</script>
```

**Output:** 

```
4
```