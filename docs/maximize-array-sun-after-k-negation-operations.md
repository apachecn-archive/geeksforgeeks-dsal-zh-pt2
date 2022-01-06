# K 次否定后最大化数组和|集合 1

> 原文:[https://www . geesforgeks . org/maximum-array-sun-after-k-negation-operations/](https://www.geeksforgeeks.org/maximize-array-sun-after-k-negation-operations/)

给定一个大小为 n 的数组和一个数字 K，我们必须修改数组 K 的次数。这里修改数组意味着在每个操作中，我们可以用-arr[i]替换任意数组元素 arr[i]。我们需要以这样一种方式执行这个操作，即在 K 次操作之后，数组的和必须是最大的？

**例:**

```
Input : arr[] = {-2, 0, 5, -1, 2} 
        K = 4
Output: 10
Explanation:
1\. Replace (-2) by -(-2), array becomes {2, 0, 5, -1, 2}
2\. Replace (-1) by -(-1), array becomes {2, 0, 5, 1, 2}
3\. Replace (0) by -(0), array becomes {2, 0, 5, 1, 2}
4\. Replace (0) by -(0), array becomes {2, 0, 5, 1, 2}

Input : arr[] = {9, 8, 8, 5} 
        K = 3
Output: 20
```

这个问题有非常**简单的解决方案**，我们只需要用 arr[i]替换数组中的最小元素 arr[i]进行当前操作。这样我们就可以在 K 次运算后使数组的和最大。一个有趣的情况是，一旦最小元素变成 0，我们就不需要再做任何改变。

## c++

```
// C++ program to maximize array sum after
// k operations.
#include <bits/stdc++.h>
using namespace std;

// This function does k operations on array
// in a way that maximize the array sum.
// index --> stores the index of current minimum
// element for j'th operation
int maximumSum(int arr[], int n, int k)
{
    // Modify array K number of times
    for (int i = 1; i <= k; i++)
    {
        int min = INT_MAX;
        int index = -1;

        // Find minimum element in array for
        // current operation and modify it
        // i.e; arr[j] --> -arr[j]
        for (int j = 0; j < n; j++)
        {
            if (arr[j] < min) {
                min = arr[j];
                index = j;
            }
        }

        // this the condition if we find 0 as
        // minimum element, so it will useless to
        // replace 0 by -(0) for remaining operations
        if (min == 0)
            break;

        // Modify element of array
        arr[index] = -arr[index];
    }

    // Calculate sum of array
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];
    return sum;
}

// Driver code
int main()
{
    int arr[] = { -2, 0, 5, -1, 2 };
    int k = 4;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maximumSum(arr, n, k);
    return 0;
}
```

## Java

```
// Java program to maximize array
// sum after k operations.

class GFG {
    // This function does k operations
    // on array in a way that maximize
    // the array sum. index --> stores
    // the index of current minimum
    // element for j'th operation
    static int maximumSum(int arr[], int n, int k)
    {
        // Modify array K number of times
        for (int i = 1; i <= k; i++)
        {
            int min = +2147483647;
            int index = -1;

            // Find minimum element in array for
            // current operation and modify it
            // i.e; arr[j] --> -arr[j]
            for (int j = 0; j < n; j++)
            {
                if (arr[j] < min)
                {
                    min = arr[j];
                    index = j;
                }
            }

            // this the condition if we find 0 as
            // minimum element, so it will useless to
            // replace 0 by -(0) for remaining operations
            if (min == 0)
                break;

            // Modify element of array
            arr[index] = -arr[index];
        }

        // Calculate sum of array
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];
        return sum;
    }

    // Driver code
    public static void main(String arg[])
    {
        int arr[] = { -2, 0, 5, -1, 2 };
        int k = 4;
        int n = arr.length;
        System.out.print(maximumSum(arr, n, k));
    }
}

// This code is contributed by Anant Agarwal.
```

## python 3

```
# Python3 program to maximize
# array sum after k operations.

# This function does k operations on array
# in a way that maximize the array sum.
# index --> stores the index of current
# minimum element for j'th operation

def maximumSum(arr, n, k):

    # Modify array K number of times
    for i in range(1, k + 1):

        min = +2147483647
        index = -1

        # Find minimum element in array for
        # current operation and modify it
        # i.e; arr[j] --> -arr[j]
        for j in range(n):

            if (arr[j] < min):

                min = arr[j]
                index = j

        # this the condition if we find 0 as
        # minimum element, so it will useless to
        # replace 0 by -(0) for remaining operations
        if (min == 0):
            break

        # Modify element of array
        arr[index] = -arr[index]

    # Calculate sum of array
    sum = 0
    for i in range(n):
        sum += arr[i]
    return sum

# Driver code
arr = [-2, 0, 5, -1, 2]
k = 4
n = len(arr)
print(maximumSum(arr, n, k))

# This code is contributed by Anant Agarwal.
```

## c#

```
// C# program to maximize array
// sum after k operations.
using System;

class GFG {

    // This function does k operations
    // on array in a way that maximize
    // the array sum. index --> stores
    // the index of current minimum
    // element for j'th operation
    static int maximumSum(int[] arr, int n, int k)
    {

        // Modify array K number of times
        for (int i = 1; i <= k; i++)
        {
            int min = +2147483647;
            int index = -1;

            // Find minimum element in array for
            // current operation and modify it
            // i.e; arr[j] --> -arr[j]
            for (int j = 0; j < n; j++)
            {
                if (arr[j] < min)
                {
                    min = arr[j];
                    index = j;
                }
            }

            // this the condition if we find
            // 0 as minimum element, so it
            // will useless to replace 0 by -(0)
            // for remaining operations
            if (min == 0)
                break;

            // Modify element of array
            arr[index] = -arr[index];
        }

        // Calculate sum of array
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];
        return sum;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { -2, 0, 5, -1, 2 };
        int k = 4;
        int n = arr.Length;
        Console.Write(maximumSum(arr, n, k));
    }
}

// This code is contributed by Nitin Mittal.
```

## PHP

```
<?php
// PHP program to maximize
// array sum after k operations.

// This function does k operations
// on array in a way that maximize
// the array sum. index --> stores
// the index of current minimum
// element for j'th operation
function maximumSum($arr, $n, $k)
{
    $INT_MAX = 0;
    // Modify array K
    // number of times
    for ($i = 1; $i <= $k; $i++)
    {
        $min = $INT_MAX;
        $index = -1;

        // Find minimum element in
        // array for current operation
        // and modify it i.e;
        // arr[j] --> -arr[j]
        for ($j = 0; $j < $n; $j++)
        {
            if ($arr[$j] < $min)
            {
                $min = $arr[$j];
                $index = $j;
            }
        }

        // this the condition if we
        // find 0 as minimum element, so
        // it will useless to replace 0
        // by -(0) for remaining operations
        if ($min == 0)
            break;

        // Modify element of array
        $arr[$index] = -$arr[$index];
    }

    // Calculate sum of array
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];
    return $sum;
}

// Driver Code
$arr = array(-2, 0, 5, -1, 2);
$k = 4;
$n = sizeof($arr) / sizeof($arr[0]);
echo maximumSum($arr, $n, $k);

// This code is contributed
// by nitin mittal.
?>
```

## Javascript

```
<script>

// Javascript program to maximize array
// sum after k operations.

// This function does k operations
// on array in a way that maximize
// the array sum. index --> stores
// the index of current minimum
// element for j'th operation
function maximumSum(arr, n, k)
{

    // Modify array K number of times
    for(let i = 1; i <= k; i++)
    {
        let min = +2147483647;
        let index = -1;

        // Find minimum element in array for
        // current operation and modify it
        // i.e; arr[j] --> -arr[j]
        for(let j = 0; j < n; j++)
        {
            if (arr[j] < min)
            {
                min = arr[j];
                index = j;
            }
        }

        // This the condition if we find 0 as
        // minimum element, so it will useless to
        // replace 0 by -(0) for remaining operations
        if (min == 0)
            break;

        // Modify element of array
        arr[index] = -arr[index];
    }

    // Calculate sum of array
    let sum = 0;
    for(let i = 0; i < n; i++)
        sum += arr[i];

    return sum;
}

// Driver code
let arr = [ -2, 0, 5, -1, 2 ];
let k = 4;
let n = arr.length;

document.write(maximumSum(arr, n, k));

// This code is contributed by code_hunt

</script>
```

**输出**

```
10
```