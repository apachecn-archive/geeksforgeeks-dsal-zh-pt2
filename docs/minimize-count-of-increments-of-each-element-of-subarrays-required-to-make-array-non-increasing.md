# 最小化使阵列不增加所需的子阵列每个元素的增量计数

> 原文:[https://www . geeksforgeeks . org/最小化子数组中每个元素的增量计数-需要使数组不增加/](https://www.geeksforgeeks.org/minimize-count-of-increments-of-each-element-of-subarrays-required-to-make-array-non-increasing/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到最小操作数，包括将[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的所有元素递增 1，使数组不递增。
**示例:**

> **输入:** arr[] = {1，3，4，1，2}
> **输出:** 4
> **说明:**
> 操作 1:选择子阵列{1}并将其值增加 1。现在 arr[] = {2，3，4，1，2}
> 在操作 2:选择子阵列{2}并将其值增加 1。现在 arr[] = {3，3，4，1，2}
> 在操作 3:选择子阵列{3，3}并将其值增加 1。现在 arr[] = {4，4，4，1，2}
> 在操作 4:选择子阵列{1}并将其值增加 1。现在 arr[] = {4，4，4，2，2}
> 因此，需要 4 次操作才能使数组不增加。
> 
> **输入:** arr[] = {10，9，8，7，7}
> **输出:** 0
> **说明:**
> 数组已经不递增了

**方法:**该方法基于只能在子阵列上执行操作的事实。所以只检查连续的元素。以下是步骤:

1.  否则，初始化一个变量，比如 **res** ，以存储所需的操作计数。
2.  现在，遍历数组，对于每个元素，检查索引 **i** 处的元素是否小于索引 **(i + 1)** 处的元素。如果发现是真的，那么将它们之间的差值加到 **res** 上，因为两个元素需要相等才能使数组不增加。
3.  否则，移动到下一个元素并重复上述步骤。
4.  最后，完成数组遍历后，打印 **res** 的最终值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number of operations required to
// make the array non-increasing
int getMinOps(int arr[], int n)
{

    // Stores the count of
    // required operations
    int res = 0;

    for (int i = 0; i < n - 1; i++)
    {

        // If arr[i] > arr[i+1],
        // no increments required.
        // Otherwise, add their
        // difference to the answer
        res += max(arr[i + 1] - arr[i], 0);
    }

    // Return the result res
    return res;
}

// Driver Code
int main()
{
    int arr[] = {1, 3, 4, 1, 2};
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << getMinOps(arr, N);
}

// This code is contributed by shikhasingrajput
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to find the minimum
    // number of operations required to
    // make the array non-increasing
    public static int getMinOps(int[] arr)
    {
        // Stores the count of
        // required operations
        int res = 0;

        for (int i = 0;
             i < arr.length - 1; i++)
        {

            // If arr[i] > arr[i+1],
            // no increments required.
            // Otherwise, add their
            // difference to the answer
            res += Math.max(arr[i + 1]
                            - arr[i],
                            0);
        }

        // Return the result res
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 3, 4, 1, 2 };
        System.out.println(getMinOps(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to find the minimum
# number of operations required to
# make the array non-increasing
def getMinOps(arr):

    # Stores the count of
    # required operations
    res = 0

    for i in range(len(arr) - 1):

        # If arr[i] > arr[i+1],
        # no increments required.
        # Otherwise, add their
        # difference to the answer
        res += max(arr[i + 1] - arr[i], 0)

    # Return the result res
    return res

# Driver Code

# Given array
arr = [ 1, 3, 4, 1, 2 ]

# Function call
print(getMinOps(arr))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum
// number of operations required to
// make the array non-increasing
public static int getMinOps(int[] arr)
{

    // Stores the count of
    // required operations
    int res = 0;

    for(int i = 0; i < arr.Length - 1; i++)
    {

        // If arr[i] > arr[i+1],
        // no increments required.
        // Otherwise, add their
        // difference to the answer
        res += Math.Max(arr[i + 1] -
                        arr[i], 0);
    }

    // Return the result res
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 1, 3, 4, 1, 2 };

    Console.WriteLine(getMinOps(arr));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program for the above approach

    // Function to find the minimum
    // number of operations required to
    // make the array non-increasing
    function getMinOps(arr) {
        // Stores the count of
        // required operations
        var res = 0;

        for (i = 0; i < arr.length - 1; i++) {

            // If arr[i] > arr[i+1],
            // no increments required.
            // Otherwise, add their
            // difference to the answer
            res += Math.max(arr[i + 1] - arr[i], 0);
        }

        // Return the result res
        return res;
    }

    // Driver Code

        var arr = [ 1, 3, 4, 1, 2 ];
        document.write(getMinOps(arr));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)