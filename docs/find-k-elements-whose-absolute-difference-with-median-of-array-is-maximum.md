# 找出与数组中值绝对差最大的 K 个元素

> 原文:[https://www . geesforgeks . org/find-k-elements-其与数组中值的绝对差为最大值/](https://www.geeksforgeeks.org/find-k-elements-whose-absolute-difference-with-median-of-array-is-maximum/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是找出数组中与数组中值绝对差最大的 K 个元素。
**注:**如果两个元素的差值相等，则考虑最大元素。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，k = 3
> **输出:** {5，1，4}
> **解释:**
> 中值 m = 3，
> 每个数组元素与中值的差，
> 1 = =>diff(1-3)= 2
> 2 = =>diff(2-3)= 1
> 3 = = =>diff(3-3)
> 
> **输入:** arr[] = {1，2，3}，K = 2
> **输出:** {3，1}

**进场:**

*   对数组排序[求数组的中值](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)
*   创建一个差异数组，存储每个元素与排序数组中值的差异。
*   差异最大的元素是数组的角元素。因此，将[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)初始化为 0 和 N–1 的数组的角元素。
*   最后，将数组中与中值差异最大的元素一个接一个地包含进来。

下面是上述方法的实现:

## C++

```
// C++ implementation to find first K
// elements whose difference with the
// median of array is maximum

#include <bits/stdc++.h>
using namespace std;

// Function for calculating median
double findMedian(int a[], int n)
{
    // check for even case
    if (n % 2 != 0)
       return (double)a[n/2];

    return (double)(a[(n-1)/2] + a[n/2])/2.0;
}

// Function to find the K maximum absolute
// difference with the median of the array
void kStrongest(int arr[], int n, int k)
{
    // Sort the array.
    sort(arr, arr + n);

    // Store median
    double median = findMedian(arr, n);
    int diff[n];

    // Find and store difference
    for (int i = 0; i < n; i++) {
        diff[i] = abs(median - arr[i]);
    }

    int i = 0, j = n - 1;
    while (k > 0) {

        // If diff[i] is greater print it
        // Else print diff[j]
        if (diff[i] > diff[j]) {
            cout << arr[i] << " ";
            i++;
        }
        else {
            cout << arr[j] << " ";
            j--;
        }
        k--;
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int k = 3;
    int n = sizeof(arr) / sizeof(arr[0]);

    kStrongest(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find first K
// elements whose difference with the
// median of array is maximum
import java.util.*;
class GFG{

// Function for calculating median
static double findMedian(int a[], int n)
{
    // check for even case
    if (n % 2 != 0)
       return (double)a[n / 2];

    return (double)(a[(n - 1) / 2] +
                    a[n / 2]) / 2.0;
}

// Function to find the K maximum absolute
// difference with the median of the array
static void kStrongest(int arr[], int n, int k)
{
    // Sort the array.
    Arrays.sort(arr);

    // Store median
    double median = findMedian(arr, n);
    int []diff = new int[n];

    // Find and store difference
    for (int i = 0; i < n; i++)
    {
        diff[i] = (int)Math.abs(median - arr[i]);
    }

    int i = 0, j = n - 1;
    while (k > 0)
    {

        // If diff[i] is greater print it
        // Else print diff[j]
        if (diff[i] > diff[j])
        {
            System.out.print(arr[i] + " ");
            i++;
        }
        else
        {
            System.out.print(arr[j] + " ");
            j--;
        }
        k--;
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int k = 3;
    int n = arr.length;

    kStrongest(arr, n, k);
}
}
// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to find first K
# elements whose difference with the
# median of array is maximum

# Function for calculating median
def findMedian(a, n):

    # Check for even case
    if (n % 2 != 0):
        return a[int(n / 2)]

    return (a[int((n - 1) / 2)] +
            a[int(n / 2)]) / 2.0

# Function to find the K maximum
# absolute difference with the
# median of the array
def kStrongest(arr, n, k):

    # Sort the array
    arr.sort()

    # Store median
    median = findMedian(arr, n)
    diff = [0] * (n)

    # Find and store difference
    for i in range(n):
        diff[i] = abs(median - arr[i])

    i = 0
    j = n - 1

    while (k > 0):

        # If diff[i] is greater print
        # it. Else print diff[j]
        if (diff[i] > diff[j]):
            print(arr[i], end = " ")
            i += 1
        else:
            print(arr[j], end = " ")
            j -= 1

        k -= 1

# Driver code
arr = [ 1, 2, 3, 4, 5 ]
k = 3
n = len(arr)

kStrongest(arr, n, k)

# This code is contributed by sanjoy_62
```

## C#

```
// C# implementation to find first K
// elements whose difference with the
// median of array is maximum
using System;

class GFG{

// Function for calculating median
static double findMedian(int []a, int n)
{
    // Check for even case
    if (n % 2 != 0)
        return (double)a[n / 2];

    return (double)(a[(n - 1) / 2] +
                    a[n / 2]) / 2.0;
}

// Function to find the K maximum absolute
// difference with the median of the array
static void kStrongest(int []arr, int n,
                                  int k)
{

    // Sort the array.
    Array.Sort(arr);

    int i = 0;

    // Store median
    double median = findMedian(arr, n);
    int []diff = new int[n];

    // Find and store difference
    for(i = 0; i < n; i++)
    {
       diff[i] = (int)Math.Abs(median - arr[i]);
    }

    int j = n - 1;
    i = 0;
    while (k > 0)
    {

        // If diff[i] is greater print it
        // Else print diff[j]
        if (diff[i] > diff[j])
        {
            Console.Write(arr[i] + " ");
            i++;
        }
        else
        {
            Console.Write(arr[j] + " ");
            j--;
        }
        k--;
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5 };
    int k = 3;
    int n = arr.Length;

    kStrongest(arr, n, k);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// JavaScript implementation to find first K
// elements whose difference with the
// median of array is maximum

// Function for calculating median
function findMedian(a, n)
{

    // Check for even case
    if (n % 2 != 0)
       return a[Math.floor(n / 2)];

    return (a[Math.floor((n - 1) / 2)] +
            a[Math.floor(n / 2)]) / 2.0;
}

// Function to find the K maximum absolute
// difference with the median of the array
function kStrongest(arr, n, k)
{

    // Sort the array.
    arr.sort();

    // Store median
    let median = findMedian(arr, n);
    let diff = Array.from({length: n}, (_, i) => 0);

    // Find and store difference
    for(let i = 0; i < n; i++)
    {
        diff[i] = Math.abs(median - arr[i]);
    }

    let i = 0, j = n - 1;
    while (k > 0)
    {

        // If diff[i] is greater print it
        // Else print diff[j]
        if (diff[i] > diff[j])
        {
            document.write(arr[i] + " ");
            i++;
        }
        else
        {
           document.write(arr[j] + " ");
            j--;
        }
        k--;
    }
}

// Driver Code
let arr = [ 1, 2, 3, 4, 5 ];
let k = 3;
let n = arr.length;

kStrongest(arr, n, k);

// This code is contributed by susmitakundugoaldanga   

</script>
```

**Output:** 

```
5 1 4
```