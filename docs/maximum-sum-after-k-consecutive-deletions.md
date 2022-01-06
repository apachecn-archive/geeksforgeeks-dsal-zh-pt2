# K 次连续删除后的最大和

> 原文:[https://www . geeksforgeeks . org/k 次连续删除后的最大总和/](https://www.geeksforgeeks.org/maximum-sum-after-k-consecutive-deletions/)

给定一个大小为 **N** 的数组**arr【】**和一个整数 **K** ，任务是从数组中删除 **K** 个连续元素，使得剩余元素的总和最大。这里我们需要打印数组的剩余元素。

**示例:**

> **输入:** arr[] = {-1，1，2，-3，2，2}，K = 3
> **输出:** -1 2 2
> 删除 1，2，-3，剩余
> 元素之和为 3，最大可能。
> **输入:** arr[] = {1，2，-3，4，5}，K = 1
> **输出:** 1 2 4 5

**方法:**计算 k 个连续元素的和，去掉和最小的元素。打印数组的其余元素。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the array after removing
// k consecutive elements such that the sum
// of the remaining elements is maximized
void maxSumArr(int arr[], int n, int k)
{
    int cur = 0, index = 0;

    // Find the sum of first k elements
    for (int i = 0; i < k; i++)
        cur += arr[i];

    // To store the minimum sum of k
    // consecutive elements of the array
    int min = cur;
    for (int i = 0; i < n - k; i++) {

        // Calculating sum of next k elements
        cur = cur - arr[i] + arr[i + k];

        // Update the minimum sum so far and the
        // index of the first element
        if (cur < min) {
            cur = min;
            index = i + 1;
        }
    }

    // Printing result
    for (int i = 0; i < index; i++)
        cout << arr[i] << " ";
    for (int i = index + k; i < n; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { -1, 1, 2, -3, 2, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    maxSumArr(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to print the array after removing
    // k consecutive elements such that the sum
    // of the remaining elements is maximized
    static void maxSumArr(int arr[], int n, int k)
    {
        int cur = 0, index = 0;

        // Find the sum of first k elements
        for (int i = 0; i < k; i++)
            cur += arr[i];

        // To store the minimum sum of k
        // consecutive elements of the array
        int min = cur;
        for (int i = 0; i < n - k; i++) {

            // Calculating sum of next k elements
            cur = cur - arr[i] + arr[i + k];

            // Update the minimum sum so far and the
            // index of the first element
            if (cur < min) {
                cur = min;
                index = i + 1;
            }
        }

        // Printing result
        for (int i = 0; i < index; i++)
            System.out.print(arr[i] + " ");
        for (int i = index + k; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { -1, 1, 2, -3, 2, 2 };
        int n = arr.length;
        int k = 3;

        maxSumArr(arr, n, k);
    }
}
```

## 计算机编程语言

```
# Pyhton3 implementation of the approach

# Function to print the array after removing
# k consecutive elements such that the sum
# of the remaining elements is maximized
def maxSumArr(arr,  n, k):
    cur = 0
    index = 0

    # Find the sum of first k elements
    for i in range(k):
        cur += arr[i]

    # To store the minimum sum of k
    # consecutive elements of the array
    min = cur;
    for i in range(n-k):

        # Calculating sum of next k elements
        cur = cur-arr[i]+arr[i + k]

        # Update the minimum sum so far and the
        # index of the first element
        if(cur<min):
            cur = min
            index = i + 1

    # Printing result
    for i in range(index):
        print(arr[i], end =" ")
    i = index + k
    while i<n:
        print(arr[i], end =" ")
        i += 1

# Driver code
arr = [-1, 1, 2, -3, 2, 2]
n = len(arr)
k = 3

maxSumArr(arr, n, k)
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to print the array after removing
    // k consecutive elements such that the sum
    // of the remaining elements is maximized
    static void maxSumArr(int []arr, int n, int k)
    {
        int cur = 0, index = 0;

        // Find the sum of first k elements
        for (int i = 0; i < k; i++)
            cur = cur + arr[i];

        // To store the minimum sum of k
        // consecutive elements of the array
        int min = cur;
        for (int i = 0; i < n - k; i++)
        {

            // Calculating sum of next k elements
            cur = (cur - arr[i]) + (arr[i + k]);

            // Update the minimum sum so far and the
            // index of the first element
            if (cur < min)
            {
                cur = min;
                index = i + 1;
            }
        }

        // Printing result
        for (int i = 0; i < index; i++)
            Console.Write(arr[i] + " ");
        for (int i = index + k; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver code
    static public void Main ()
    {
        int []arr = { -1, 1, 2, -3, 2, 2 };
        int n = arr.Length;
        int k = 3;

        maxSumArr(arr, n, k);
    }
}

// This code is contributed by ajit..
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Function to print the array after removing
    // k consecutive elements such that the sum
    // of the remaining elements is maximized
    function maxSumArr(arr, n, k)
    {
        let cur = 0, index = 0;

        // Find the sum of first k elements
        for (let i = 0; i < k; i++)
            cur = cur + arr[i];

        // To store the minimum sum of k
        // consecutive elements of the array
        let min = cur;
        for (let i = 0; i < n - k; i++)
        {

            // Calculating sum of next k elements
            cur = (cur - arr[i]) + (arr[i + k]);

            // Update the minimum sum so far and the
            // index of the first element
            if (cur < min)
            {
                cur = min;
                index = i + 1;
            }
        }

        // Printing result
        for (let i = 0; i < index; i++)
            document.write(arr[i] + " ");
        for (let i = index + k; i < n; i++)
            document.write(arr[i] + " ");
    }

    let arr = [ -1, 1, 2, -3, 2, 2 ];
    let n = arr.length;
    let k = 3;

    maxSumArr(arr, n, k);

</script>
```

**Output:** 

```
-1 2 2
```

**时间复杂度:** O(n)