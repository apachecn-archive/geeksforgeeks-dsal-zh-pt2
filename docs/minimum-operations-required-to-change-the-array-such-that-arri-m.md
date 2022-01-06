# 改变数组所需的最小操作，使得| arr[I]–M |<= 1

> 原文:[https://www . geeksforgeeks . org/更改阵列所需的最小操作数-arri-m/](https://www.geeksforgeeks.org/minimum-operations-required-to-change-the-array-such-that-arri-m/)

给定一个整数的**数组[]** ，任务是找到改变数组元素所需的最小操作数，使得对于任何正整数 **M** 、**arr[I]–M |≤1**对于所有有效的 **i** 。
在单次操作中，数组的任何元素都可以递增或递减 1。
**举例:**

> **输入:** arr[] = {10，1，4}
> **输出:** 7
> 如果我们将 1 变成 2，将 10 变成 4，运算次数为| 1–2 |+| 10–4 | = 7
> 改变后，数组变成{4，2，4}，其中每个元素与 M = 3 的绝对差值≤ 1
> **输入:** arr[] = {5，7，4，1，4}
> **输出**

**方法:**从数组的最小元素开始到数组的最大元素说**数**，计算改变每个元素所需的操作数，使其与**数**的绝对差为 **≤ 1** 。在所有可能的操作中，最小的是所需的答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// number of operations required
int changeTheArray(int arr[], int n)
{

    // Minimum and maximum elements from the array
    int minEle = *(std::min_element(arr, arr + n));
    int maxEle = *(std::max_element(arr, arr + n));

    // To store the minimum number of
    // operations required
    int minOperations = INT_MAX;
    for (int num = minEle; num <= maxEle; num++) {

        // To store the number of operations required
        // to change every element to either
        // (num - 1), num or (num + 1)
        int operations = 0;
        for (int i = 0; i < n; i++) {

            // If current element is not already num
            if (arr[i] != num) {

                // Add the count of operations
                // required to change arr[i]
                operations += (abs(num - arr[i]) - 1);
            }
        }

        // Update the minimum operations so far
        minOperations = min(minOperations, operations);
    }

    return minOperations;
}

// Driver code
int main()
{
    int arr[] = { 10, 1, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << changeTheArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to return the minimum
    // number of operations required
    static int changeTheArray(int arr[], int n)
    {

        // Minimum and maximum elements from the array
        int minEle = Arrays.stream(arr).min().getAsInt();
        int maxEle = Arrays.stream(arr).max().getAsInt();

        // To store the minimum number of
        // operations required
        int minOperations = Integer.MAX_VALUE;
        for (int num = minEle; num <= maxEle; num++) {

            // To store the number of operations required
            // to change every element to either
            // (num - 1), num or (num + 1)
            int operations = 0;
            for (int i = 0; i < n; i++) {

                // If current element is not already num
                if (arr[i] != num) {

                    // Add the count of operations
                    // required to change arr[i]
                    operations += (Math.abs(num - arr[i]) - 1);
                }
            }

            // Update the minimum operations so far
            minOperations = Math.min(minOperations, operations);
        }

        return minOperations;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 10, 1, 4 };
        int n = arr.length;
        System.out.println(changeTheArray(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math
import sys

# Function to return the minimum
# number of operations required
def changeTheArray(arr, n):

    # Minimum and maximum elements
    # from the array
    minEle = min(arr)
    maxEle = max(arr)

    # To store the minimum number of
    # operations required
    minOperations = sys.maxsize

    for num in range(minEle, maxEle + 1):

        # To store the number of operations required
        # to change every element to either
        # (num - 1), num or (num + 1)
        operations = 0
        for i in range(n):

                # If current element is not already num
                if arr[i] != num:
                        operations += (abs(num - arr[i]) - 1)

        # Update the minimum operations so far
        minOperations = min(minOperations, operations)
    return minOperations

# Driver code
if __name__=='__main__':
    arr = [10, 1, 4]
    n = len(arr)
    print(changeTheArray(arr, n))

# This code is contributed by Vikash Kumar 37
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;

class GFG
{

    // Function to return the minimum
    // number of operations required
    static int changeTheArray(int []arr, int n)
    {

        // Minimum and maximum elements from the array
        int minEle = arr.Min();
        int maxEle = arr.Max();

        // To store the minimum number of
        // operations required
        int minOperations = int.MaxValue;
        for (int num = minEle; num <= maxEle; num++)
        {

            // To store the number of operations required
            // to change every element to either
            // (num - 1), num or (num + 1)
            int operations = 0;
            for (int i = 0; i < n; i++)
            {

                // If current element is not already num
                if (arr[i] != num)
                {

                    // Add the count of operations
                    // required to change arr[i]
                    operations += (Math.Abs(num - arr[i]) - 1);
                }
            }

            // Update the minimum operations so far
            minOperations = Math.Min(minOperations, operations);
        }

        return minOperations;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = { 10, 1, 4 };
        int n = arr.Length;
        Console.WriteLine(changeTheArray(arr, n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum
// number of operations required
function changeTheArray(arr, n)
{

    // Minimum and maximum elements from the array
    let minEle = Math.min(...arr);
    let maxEle = Math.max(...arr);

    // To store the minimum number of
    // operations required
    let minOperations = Number.MAX_VALUE;
    for (let num = minEle; num <= maxEle; num++) {

        // To store the number of operations required
        // to change every element to either
        // (num - 1), num or (num + 1)
        let operations = 0;
        for (let i = 0; i < n; i++) {

            // If current element is not already num
            if (arr[i] != num) {

                // Add the count of operations
                // required to change arr[i]
                operations += (Math.abs(num - arr[i]) - 1);
            }
        }

        // Update the minimum operations so far
        minOperations = Math.min(minOperations, operations);
    }

    return minOperations;
}

// Driver code
    let arr = [ 10, 1, 4 ];
    let n = arr.length;
    document.write(changeTheArray(arr, n));

</script>
```

**Output:** 

```
7
```