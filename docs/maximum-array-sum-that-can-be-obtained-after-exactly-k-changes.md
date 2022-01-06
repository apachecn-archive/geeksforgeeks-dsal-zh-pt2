# 恰好 k 次变化后可以得到的最大数组和

> 原文:[https://www . geeksforgeeks . org/最大数组-k-changes 后可以获得的总和/](https://www.geeksforgeeks.org/maximum-array-sum-that-can-be-obtained-after-exactly-k-changes/)

给定一个由 **n** 个整数和一个整数 **k** 组成的数组 **arr[]** 。任务是在精确地执行给定操作 **k** 次后，最大化数组的和。在一次操作中，数组的任何元素都可以乘以 **-1** ，即元素的符号可以改变。

**示例:**

> **输入:** arr[] = {-5，4，1，3，2}，k = 4
> **输出:** 13
> 将-5 的符号更改一次，然后将 1 的符号更改三次。
> 于是变为-1，和为 5 + 4 + (-1) + 3 + 2 = 13。
> **输入:** arr[] = {-1，-1，1}，k = 1
> **输出:** 1

**接近:**如果数组中负元素的个数是**个数**，

1.  如果**计数≥ k** ，则恰好 **k** 负数的符号将从最小的开始改变。
2.  如果**计数< k** ，则将所有负元素的符号改为正，对于剩余操作，即**rem = k–计数**，
    *   如果 **rem % 2 = 0** ，则不会对当前数组进行任何更改，因为两次更改元素的符号会给出原始数字。
    *   如果 **rem % 2 = 1** ，则更改更新数组中最小元素的符号。
3.  最后，打印更新后的数组元素的总和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to return the sum
// of the array elements
int sumArr(int arr[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    return sum;
}

// Function to return the maximized sum
// of the array after performing
// the given operation exactly k times
int maxSum(int arr[], int n, int k)
{
    // Sort the array elements
    sort(arr, arr + n);

    int i = 0;
    // Change signs of the negative elements
    // starting from the smallest
    while (i < n && k > 0 && arr[i] < 0) {
        arr[i] *= -1;
        k--;
        i++;
    }

    // If a single operation has to be
    // performed then it must be performed
    // on the smallest positive element
    if (k % 2 == 1) {

        // To store the index of the
        // minimum element
        int min = 0;
        for (i = 1; i < n; i++)

            // Update the minimum index
            if (arr[min] > arr[i])
                min = i;

        // Perform remaining operation
        // on the smallest element
        arr[min] *= -1;
    }

    // Return the sum of the updated array
    return sumArr(arr, n);
}

// Driver code
int main()
{
    int arr[] = { -5, 4, 1, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4;

    cout << maxSum(arr, n, k) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Arrays;

class GFG
{

// Utility function to return the sum
// of the array elements
static int sumArr(int arr[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    return sum;
}

// Function to return the maximized sum
// of the array after performing
// the given operation exactly k times
static int maxSum(int arr[], int n, int k)
{
    // Sort the array elements
    Arrays.sort(arr);

    int i = 0;

    // Change signs of the negative elements
    // starting from the smallest
    while (i < n && k > 0 && arr[i] < 0)
    {
        arr[i] *= -1;
        k--;
        i++;
    }

    // If a single operation has to be
    // performed then it must be performed
    // on the smallest positive element
    if (k % 2 == 1)
    {

        // To store the index of the
        // minimum element
        int min = 0;
        for (i = 1; i < n; i++)

            // Update the minimum index
            if (arr[min] > arr[i])
                min = i;

        // Perform remaining operation
        // on the smallest element
        arr[min] *= -1;
    }

    // Return the sum of the updated array
    return sumArr(arr, n);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { -5, 4, 1, 3, 2 };
    int n = arr.length;
    int k = 4;

    System.out.println(maxSum(arr, n, k));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Utility function to return the sum
# of the array elements
def sumArr(arr, n):
    sum = 0
    for i in range(n):
        sum += arr[i]

    return sum

# Function to return the maximized sum
# of the array after performing
# the given operation exactly k times
def maxSum(arr, n, k):

    # Sort the array elements
    arr.sort(reverse = False)

    i = 0

    # Change signs of the negative elements
    # starting from the smallest
    while (i < n and k > 0 and arr[i] < 0):
        arr[i] *= -1
        k -= 1
        i += 1

    # If a single operation has to be
    # performed then it must be performed
    # on the smallest positive element
    if (k % 2 == 1):

        # To store the index of the
        # minimum element
        min = 0
        for i in range(1, n):

            # Update the minimum index
            if (arr[min] > arr[i]):
                min = i

        # Perform remaining operation
        # on the smallest element
        arr[min] *= -1

    # Return the sum of the updated array
    return sumArr(arr, n)

# Driver code
if __name__ == '__main__':
    arr = [-5, 4, 1, 3, 2]
    n = len(arr)
    k = 4

    print(maxSum(arr, n, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;
using System.Linq;

class GFG
{

// Utility function to return the sum
// of the array elements
static int sumArr(int [] arr, int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    return sum;
}

// Function to return the maximized sum
// of the array after performing
// the given operation exactly k times
static int maxSum(int [] arr, int n, int k)
{
    // Sort the array elements
    Array.Sort(arr);

    int i = 0;

    // Change signs of the negative elements
    // starting from the smallest
    while (i < n && k > 0 && arr[i] < 0)
    {
        arr[i] *= -1;
        k--;
        i++;
    }

    // If a single operation has to be
    // performed then it must be performed
    // on the smallest positive element
    if (k % 2 == 1)
    {

        // To store the index of the
        // minimum element
        int min = 0;
        for (i = 1; i < n; i++)

            // Update the minimum index
            if (arr[min] > arr[i])
                min = i;

        // Perform remaining operation
        // on the smallest element
        arr[min] *= -1;
    }

    // Return the sum of the updated array
    return sumArr(arr, n);
}

// Driver code
static void Main()
{
    int []arr= { -5, 4, 1, 3, 2 };
    int n = arr.Length;
    int k = 4;

    Console.WriteLine(maxSum(arr, n, k));
}
}

// This code is contributed by mohit kumar 29
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Utility function to return the sum
// of the array elements
function sumArr($arr, $n)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];

    return $sum;
}

// Function to return the maximized sum
// of the array after performing
// the given operation exactly k times
function maxSum($arr, $n, $k)
{
    // Sort the array elements
    sort($arr);

    $i = 0;
    // Change signs of the negative elements
    // starting from the smallest
    while ($i < $n && $k > 0 &&
                $arr[$i] < 0)
    {
        $arr[$i] *= -1;
        $k--;
        $i++;
    }

    // If a single operation has to be
    // performed then it must be performed
    // on the smallest positive element
    if ($k % 2 == 1)
    {

        // To store the index of the
        // minimum element
        $min = 0;
        for ($i = 1; $i < $n; $i++)

            // Update the minimum index
            if ($arr[$min] > $arr[$i])
                $min = $i;

        // Perform remaining operation
        // on the smallest element
        $arr[$min] *= -1;
    }

    // Return the sum of the updated array
    return sumArr($arr, $n);
}

// Driver code
$arr = array( -5, 4, 1, 3, 2 );
$n = sizeof($arr);
$k = 4;

echo maxSum($arr, $n, $k), "\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Utility function to return the sum
    // of the array elements
    function sumArr(arr, n)
    {
        let sum = 0;
        for (let i = 0; i < n; i++)
            sum += arr[i];

        return sum;
    }

    // Function to return the maximized sum
    // of the array after performing
    // the given operation exactly k times
    function maxSum(arr, n, k)
    {
        // Sort the array elements
        arr.sort(function(a, b){return a - b});

        let i = 0;

        // Change signs of the negative elements
        // starting from the smallest
        while (i < n && k > 0 && arr[i] < 0)
        {
            arr[i] *= -1;
            k--;
            i++;
        }

        // If a single operation has to be
        // performed then it must be performed
        // on the smallest positive element
        if (k % 2 == 1)
        {

            // To store the index of the
            // minimum element
            let min = 0;
            for (i = 1; i < n; i++)

                // Update the minimum index
                if (arr[min] > arr[i])
                    min = i;

            // Perform remaining operation
            // on the smallest element
            arr[min] *= -1;
        }

        // Return the sum of the updated array
        return sumArr(arr, n);
    }

    let arr= [ -5, 4, 1, 3, 2 ];
    let n = arr.length;
    let k = 4;

    document.write(maxSum(arr, n, k));

</script>
```

**Output:** 

```
13
```