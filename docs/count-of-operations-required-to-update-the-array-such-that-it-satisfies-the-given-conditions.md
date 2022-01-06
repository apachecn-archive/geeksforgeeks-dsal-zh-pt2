# 更新数组使其满足给定条件所需的操作计数

> 原文:[https://www . geeksforgeeks . org/更新阵列所需的操作数，以便它满足给定的条件/](https://www.geeksforgeeks.org/count-of-operations-required-to-update-the-array-such-that-it-satisfies-the-given-conditions/)

给定一个大小为 **N** 的数组 **arr[]** 和一个整数 **K** 。任务是找到更新数组所需的操作，以便在可以从索引 **i** 访问任何索引 **j** 时，如果索引 **j** 与索引 **i** 和**ABS(arr[I]–arr[j])≤K**相邻，则可以从索引 **0** 移动到索引**N–1**。在一次操作中，数组的任何元素都可以增加或减少 1。
**例:**

> **输入:** arr[] = {1，2，5，9}，K = 2
> **输出:** 4
> 操作 1:arr[2]= arr[2]–1
> 操作 2:arr[3]= arr[3]–3
> 新数组变成满足给定条件的 arr[] = {1，2，4，6}
> 。
> **输入:** arr[] = {-2，0，1，4}，K = 5
> **输出:** 0

**进场:**

*   从第二个元素开始遍历数组，计算当前元素和前一个元素之间的绝对差值。
*   如果绝对差值大于 **K** ，则需要更新当前元素，即将该值添加到较小的元素或从较大的元素中减去该值，这样绝对差值就变成了 **K** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// operations required to update
// the array such that it is possible
// to move from index 0 to index n - 1
int countOp(int arr[], int n, int k)
{

    int operations = 0;
    for (int i = 1; i < n; i++) {

        // Current element needs to be updated
        if (abs(arr[i] - arr[i - 1]) > k) {

            // Get the absolute difference
            int absDiff = abs(arr[i] - arr[i - 1]);

            // The value which needs to
            // be added or subtracted
            int currOp = absDiff - k;

            // Add value to arr[i]
            if (arr[i] < arr[i - 1])
                arr[i] += currOp;

            // Subtract value from arr[i]
            else
                arr[i] -= currOp;

            // Update the operations
            operations += currOp;
        }
    }

    return operations;
}

// Driver code
int main()
{

    int arr[] = { 1, 2, 5, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;

    cout << countOp(arr, n, k);

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
// operations required to update
// the array such that it is possible
// to move from index 0 to index n - 1
static int countOp(int arr[], int n, int k)
{
    int operations = 0;
    for (int i = 1; i < n; i++)
    {

        // Current element needs to be updated
        if (Math.abs(arr[i] - arr[i - 1]) > k)
        {

            // Get the absolute difference
            int absDiff = Math.abs(arr[i] - arr[i - 1]);

            // The value which needs to
            // be added or subtracted
            int currOp = absDiff - k;

            // Add value to arr[i]
            if (arr[i] < arr[i - 1])
                arr[i] += currOp;

            // Subtract value from arr[i]
            else
                arr[i] -= currOp;

            // Update the operations
            operations += currOp;
        }
    }
    return operations;
}

// Driver code
static public void main (String []arg)
{
    int arr[] = { 1, 2, 5, 9 };
    int n = arr.length;
    int k = 2;

    System.out.println(countOp(arr, n, k));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# operations required to update
# the array such that it is possible
# to move from index 0 to index n - 1
def countOp(arr, n, k) :

    operations = 0;
    for i in range(1, n) :

        # Current element needs to be updated
        if (abs(arr[i] - arr[i - 1]) > k) :

            # Get the absolute difference
            absDiff = abs(arr[i] - arr[i - 1]);

            # The value which needs to
            # be added or subtracted
            currOp = absDiff - k;

            # Add value to arr[i]
            if (arr[i] < arr[i - 1]) :
                arr[i] += currOp;

            # Subtract value from arr[i]
            else :
                arr[i] -= currOp;

            # Update the operations
            operations += currOp;

    return operations;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 5, 9 ];
    n = len(arr);
    k = 2;

    print(countOp(arr, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// operations required to update
// the array such that it is possible
// to move from index 0 to index n - 1
static int countOp(int []arr, int n, int k)
{
    int operations = 0;
    for (int i = 1; i < n; i++)
    {

        // Current element needs to be updated
        if (Math.Abs(arr[i] - arr[i - 1]) > k)
        {

            // Get the absolute difference
            int absDiff = Math.Abs(arr[i] -
                                   arr[i - 1]);

            // The value which needs to
            // be added or subtracted
            int currOp = absDiff - k;

            // Add value to arr[i]
            if (arr[i] < arr[i - 1])
                arr[i] += currOp;

            // Subtract value from arr[i]
            else
                arr[i] -= currOp;

            // Update the operations
            operations += currOp;
        }
    }
    return operations;
}

// Driver code
static public void Main (String []arg)
{
    int []arr = { 1, 2, 5, 9 };
    int n = arr.Length;
    int k = 2;

    Console.WriteLine(countOp(arr, n, k));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the count of
    // operations required to update
    // the array such that it is possible
    // to move from index 0 to index n - 1
    function countOp(arr, n, k)
    {

        let operations = 0;
        for (let i = 1; i < n; i++) {

            // Current element needs to be updated
            if (Math.abs(arr[i] - arr[i - 1]) > k) {

                // Get the absolute difference
                let absDiff = Math.abs(arr[i] - arr[i - 1]);

                // The value which needs to
                // be added or subtracted
                let currOp = absDiff - k;

                // Add value to arr[i]
                if (arr[i] < arr[i - 1])
                    arr[i] += currOp;

                // Subtract value from arr[i]
                else
                    arr[i] -= currOp;

                // Update the operations
                operations += currOp;
            }
        }

        return operations;
    }

    let arr = [ 1, 2, 5, 9 ];
    let n = arr.length;
    let k = 2;

    document.write(countOp(arr, n, k));

</script>
```

**Output:** 

```
4
```