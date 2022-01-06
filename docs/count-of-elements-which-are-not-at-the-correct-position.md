# 不在正确位置的元素计数

> 原文:[https://www . geeksforgeeks . org/不在正确位置的元素计数/](https://www.geeksforgeeks.org/count-of-elements-which-are-not-at-the-correct-position/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是计算该数组中不在正确位置的元素数量。当数组被排序时，如果一个元素在数组中的位置发生变化，则称该元素处于不正确的位置。
**例:**

> **输入:** arr[] = {1，2，6，2，4，5}
> **输出:** 4
> 数组在排序后的形式会是{1，2， **2，4，5，6** }
> **输入:** arr[] = {1，2，3，4}
> **输出:** 0
> 所有元素都已经排序好了。

**方法:**首先复制另一个数组中的数组元素比如 **B[]** 然后给定数组排序。开始遍历数组，对于每个元素，如果 **arr[i]！= B[i]** 则该元素不在给定数组中的正确位置。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// elements which are not in
// the correct position when sorted
int cntElements(int arr[], int n)
{

    // To store a copy of the
    // original array
    int copy_arr[n];

    // Copy the elements of the given
    // array to the new array
    for (int i = 0; i < n; i++)
        copy_arr[i] = arr[i];

    // To store the required count
    int count = 0;

    // Sort the original array
    sort(arr, arr + n);
    for (int i = 0; i < n; i++) {

        // If current element was not
        // at the right position
        if (arr[i] != copy_arr[i]) {
            count++;
        }
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 6, 2, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << cntElements(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the count of
    // elements which are not in
    // the correct position when sorted
    static int cntElements(int arr[], int n)
    {

        // To store a copy of the
        // original array
        int copy_arr[] = new int[n];

        // Copy the elements of the given
        // array to the new array
        for (int i = 0; i < n; i++)
            copy_arr[i] = arr[i];

        // To store the required count
        int count = 0;

        // Sort the original array
        Arrays.sort(arr);

        for (int i = 0; i < n; i++)
        {

            // If current element was not
            // at the right position
            if (arr[i] != copy_arr[i])
            {
                count++;
            }
        }
        return count;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 6, 2, 4, 5 };
        int n = arr.length;

        System.out.println(cntElements(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# elements which are not in
# the correct position when sorted
def cntElements(arr, n) :

    # To store a copy of the
    # original array
    copy_arr = [0] * n

    # Copy the elements of the given
    # array to the new array
    for i in range(n):
        copy_arr[i] = arr[i]

    # To store the required count
    count = 0

    # Sort the original array
    arr.sort()
    for i in range(n):

        # If current element was not
        # at the right position
        if (arr[i] != copy_arr[i]) :
            count += 1

    return count

# Driver code
arr = [ 1, 2, 6, 2, 4, 5 ]
n = len(arr)

print(cntElements(arr, n))

# This code is contributed by
# divyamohan123
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count of
    // elements which are not in
    // the correct position when sorted
    static int cntElements(int [] arr, int n)
    {

        // To store a copy of the
        // original array
        int [] copy_arr = new int[n];

        // Copy the elements of the given
        // array to the new array
        for (int i = 0; i < n; i++)
            copy_arr[i] = arr[i];

        // To store the required count
        int count = 0;

        // Sort the original array
        Array.Sort(arr);

        for (int i = 0; i < n; i++)
        {

            // If current element was not
            // at the right position
            if (arr[i] != copy_arr[i])
            {
                count++;
            }
        }
        return count;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int [] arr = { 1, 2, 6, 2, 4, 5 };
        int n = arr.Length;

        Console.WriteLine(cntElements(arr, n));
    }
}

// This code is contributed by Mohit kumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the count of
// elements which are not in
// the correct position when sorted
function cntElements(arr, n) {

    // To store a copy of the
    // original array
    let copy_arr = new Array(n);

    // Copy the elements of the given
    // array to the new array
    for (let i = 0; i < n; i++)
        copy_arr[i] = arr[i];

    // To store the required count
    let count = 0;

    // Sort the original array
    arr.sort((a, b) => a - b);
    for (let i = 0; i < n; i++) {

        // If current element was not
        // at the right position
        if (arr[i] != copy_arr[i]) {
            count++;
        }
    }
    return count;
}

// Driver code

let arr = [1, 2, 6, 2, 4, 5];
let n = arr.length;

document.write(cntElements(arr, n));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
4
```