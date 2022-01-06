# 给定数组的最大和组合

> 原文:[https://www . geesforgeks . org/给定数组的最大和组合/](https://www.geeksforgeeks.org/maximum-sum-combination-from-the-given-array/)

给定一个由 **N** 整数和三个整数**X****Y**和 **Z** 组成的数组 **arr[]** 。任务是求**(arr[I]* X)+(arr[j]* Y)+(arr[k]* Z)**的最大值，其中**0≤I≤j≤k≤N–1**。

**示例:**

> **输入:** arr[] = {1，5，-3，4，-2}，X = 2，Y = 1，Z =-1
> T3】输出:18
> (2 * 5)+(1 * 5)+(-1 *-3)= 18
> 为最大可能和。
> 
> **输入:** arr[] = {2，4，-9，-64，7，3}，X = -1，Y = 1，Z = 1
> **输出:** 78

**方法:**从数组中找出最大和最小的正负值。另外，检查阵列中是否存在 **0** 。现在，对于 **X** 、 **Y** 和 **Z** 的给定值。从数组中选择之前找到的最大化总和的值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum possible
// value of the given equation
int maxSum(int arr[], int n, int x, int y, int z)
{

    // To store the minimum and the maximum negative
    // and positive values from the array
    int minNeg = INT_MAX, maxNeg = INT_MAX;
    int minPos = INT_MIN, maxPos = INT_MIN;

    // To store whether 0 is present in the array
    bool isZeroPresent = false;

    // Update the values of the
    // above defined variables
    for (int i = 0; i < n; i++) {
        if (arr[i] == 0) {
            isZeroPresent = true;
        }
        else if (arr[i] < 0) {
            minNeg = min(minNeg, arr[i]);
            maxNeg = max(maxNeg, arr[i]);
        }
        else {
            minPos = min(minPos, arr[i]);
            maxPos = max(maxPos, arr[i]);
        }
    }

    // To store the resultant sum
    int sum = 0;

    // x will not contribute to the
    // sum if it is equal to 0
    if (x != 0) {

        // If x is negative
        if (x < 0) {

            // Either multiply it with the minimum
            // negative number from the array
            if (minNeg != INT_MAX)
                sum += (x * minNeg);

            // Or multiply it with the minimum
            // positive element if zero is
            // not present in the array
            else if (!isZeroPresent)
                sum += (x * minPos);
        }

        // If x is positive
        else {

            // Multiply it with the maximum
            // positive value from the array
            if (maxPos != INT_MIN)
                sum += (x * maxPos);

            // Or multiply it with the maximum
            // negative element if zero is
            // not present in the array
            else if (!isZeroPresent)
                sum += (x * maxPos);
        }
    }

    // Same as x
    if (y != 0) {
        if (y < 0) {
            if (minNeg != INT_MAX)
                sum += (y * minNeg);
            else if (!isZeroPresent)
                sum += (y * minPos);
        }
        else {
            if (maxPos != INT_MIN)
                sum += (y * maxPos);
            else if (!isZeroPresent)
                sum += (y * maxPos);
        }
    }

    // Same as x
    if (z != 0) {
        if (z < 0) {
            if (minNeg != INT_MAX)
                sum += (z * minNeg);
            else if (!isZeroPresent)
                sum += (z * minPos);
        }
        else {
            if (maxPos != INT_MIN)
                sum += (z * maxPos);
            else if (!isZeroPresent)
                sum += (z * maxPos);
        }
    }

    return sum;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, -9, -64, 7, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = -1, y = 1, z = 1;

    cout << maxSum(arr, n, x, y, z);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum possible
// value of the given equation
static int maxSum(int arr[], int n, int x, int y, int z)
{

    // To store the minimum and the maximum negative
    // and positive values from the array
    int minNeg = Integer.MAX_VALUE,
        maxNeg = Integer.MAX_VALUE;
    int minPos = Integer.MIN_VALUE,
        maxPos = Integer.MIN_VALUE;

    // To store whether 0 is present in the array
    boolean isZeroPresent = false;

    // Update the values of the
    // above defined variables
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == 0)
        {
            isZeroPresent = true;
        }
        else if (arr[i] < 0)
        {
            minNeg = Math.min(minNeg, arr[i]);
            maxNeg = Math.max(maxNeg, arr[i]);
        }
        else
        {
            minPos = Math.min(minPos, arr[i]);
            maxPos = Math.max(maxPos, arr[i]);
        }
    }

    // To store the resultant sum
    int sum = 0;

    // x will not contribute to the
    // sum if it is equal to 0
    if (x != 0)
    {

        // If x is negative
        if (x < 0)
        {

            // Either multiply it with the minimum
            // negative number from the array
            if (minNeg != Integer.MAX_VALUE)
                sum += (x * minNeg);

            // Or multiply it with the minimum
            // positive element if zero is
            // not present in the array
            else if (!isZeroPresent)
                sum += (x * minPos);
        }

        // If x is positive
        else
        {

            // Multiply it with the maximum
            // positive value from the array
            if (maxPos != Integer.MIN_VALUE)
                sum += (x * maxPos);

            // Or multiply it with the maximum
            // negative element if zero is
            // not present in the array
            else if (!isZeroPresent)
                sum += (x * maxPos);
        }
    }

    // Same as x
    if (y != 0)
    {
        if (y < 0)
        {
            if (minNeg != Integer.MAX_VALUE)
                sum += (y * minNeg);
            else if (!isZeroPresent)
                sum += (y * minPos);
        }
        else
        {
            if (maxPos != Integer.MIN_VALUE)
                sum += (y * maxPos);
            else if (!isZeroPresent)
                sum += (y * maxPos);
        }
    }

    // Same as x
    if (z != 0)
    {
        if (z < 0)
        {
            if (minNeg != Integer.MAX_VALUE)
                sum += (z * minNeg);
            else if (!isZeroPresent)
                sum += (z * minPos);
        }
        else
        {
            if (maxPos != Integer.MIN_VALUE)
                sum += (z * maxPos);
            else if (!isZeroPresent)
                sum += (z * maxPos);
        }
    }
    return sum;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 4, -9, -64, 7, 3 };
    int n = arr.length;
    int x = -1, y = 1, z = 1;

    System.out.print(maxSum(arr, n, x, y, z));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum possible
# value of the given equation
def maxSum(arr, n, x, y, z):

    # To store the minimum and the maximum negative
    # and positive values from the array
    minNeg = 10**9
    maxNeg = 10**9
    minPos = -10**9
    maxPos = -10**9

    # To store whether 0 is present in the array
    isZeroPresent = False

    # Update the values of the
    # above defined variables
    for i in range(n):
        if (arr[i] == 0):
            isZeroPresent = True
        elif (arr[i] < 0):
            minNeg = min(minNeg, arr[i])
            maxNeg = max(maxNeg, arr[i])
        else:
            minPos = min(minPos, arr[i])
            maxPos = max(maxPos, arr[i])

    # To store the resultant summ
    summ = 0

    # x will not contribute to the
    # summ if it is equal to 0
    if (x != 0):

        # If x is negative
        if (x < 0):

            # Either multiply it with the minimum
            # negative number from the array
            if (minNeg != 10**9):
                summ += (x * minNeg)

            # Or multiply it with the minimum
            # positive element if zero is
            # not present in the array
        elif (isZeroPresent == False):
                summ += (x * minPos)

        # If x is positive
        else:

            # Multiply it with the maximum
            # positive value from the array
            if (maxPos != -10**9):
                summ += (x * maxPos)

            # Or multiply it with the maximum
            # negative element if zero is
            # not present in the array
            elif (isZeroPresent == False):
                summ += (x * maxPos)

    # Same as x
    if (y != 0):
        if (y < 0):
            if (minNeg != 10**9):
                summ += (y * minNeg)
            elif (isZeroPresent == False):
                summ += (y * minPos)

        else:
            if (maxPos != -10**9):
                summ += (y * maxPos)
            elif (isZeroPresent == False):
                summ += (y * maxPos)

    # Same as x
    if (z != 0):
        if (z < 0):
            if (minNeg != 10**9):
                summ += (z * minNeg)
            elif (isZeroPresent == False):
                summ += (z * minPos)

        else:
            if (maxPos != -10**9):
                summ += (z * maxPos)
            elif (isZeroPresent == False):
                summ += (z * maxPos)

    return summ

# Driver code
arr = [2, 4, -9, -64, 7, 3]
n = len(arr)
x = -1
y = 1
z = 1

print(maxSum(arr, n, x, y, z))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the maximum possible
    // value of the given equation
    static int maxSum(int []arr, int n,
                      int x, int y, int z)
    {

        int INT_MAX = int.MaxValue;
        int INT_MIN = int.MinValue;

        // To store the minimum and the maximum negative
        // and positive values from the array
        int minNeg = INT_MAX, maxNeg = INT_MAX;
        int minPos = INT_MIN, maxPos = INT_MIN;

        // To store whether 0 is present in the array
        bool isZeroPresent = false;

        // Update the values of the
        // above defined variables
        for (int i = 0; i < n; i++)
        {
            if (arr[i] == 0)
            {
                isZeroPresent = true;
            }
            else if (arr[i] < 0)
            {
                minNeg = Math.Min(minNeg, arr[i]);
                maxNeg = Math.Max(maxNeg, arr[i]);
            }
            else
            {
                minPos = Math.Min(minPos, arr[i]);
                maxPos = Math.Max(maxPos, arr[i]);
            }
        }

        // To store the resultant sum
        int sum = 0;

        // x will not contribute to the
        // sum if it is equal to 0
        if (x != 0)
        {

            // If x is negative
            if (x < 0)
            {

                // Either multiply it with the minimum
                // negative number from the array
                if (minNeg != INT_MAX)
                    sum += (x * minNeg);

                // Or multiply it with the minimum
                // positive element if zero is
                // not present in the array
                else if (!isZeroPresent)
                    sum += (x * minPos);
            }

            // If x is positive
            else
            {

                // Multiply it with the maximum
                // positive value from the array
                if (maxPos != INT_MIN)
                    sum += (x * maxPos);

                // Or multiply it with the maximum
                // negative element if zero is
                // not present in the array
                else if (!isZeroPresent)
                    sum += (x * maxPos);
            }
        }

        // Same as x
        if (y != 0)
        {
            if (y < 0)
            {
                if (minNeg != INT_MAX)
                    sum += (y * minNeg);
                else if (!isZeroPresent)
                    sum += (y * minPos);
            }
            else
            {
                if (maxPos != INT_MIN)
                    sum += (y * maxPos);
                else if (!isZeroPresent)
                    sum += (y * maxPos);
            }
        }

        // Same as x
        if (z != 0)
        {
            if (z < 0)
            {
                if (minNeg != INT_MAX)
                    sum += (z * minNeg);
                else if (!isZeroPresent)
                    sum += (z * minPos);
            }
            else
            {
                if (maxPos != INT_MIN)
                    sum += (z * maxPos);
                else if (!isZeroPresent)
                    sum += (z * maxPos);
            }
        }
        return sum;
    }

    // Driver code
    static public void Main ()
    {
        int []arr = { 2, 4, -9, -64, 7, 3 };
        int n = arr.Length;
        int x = -1, y = 1, z = 1;

        Console.Write(maxSum(arr, n, x, y, z));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum possible
// value of the given equation
function maxSum(arr, n, x, y, z) {

    // To store the minimum and the maximum negative
    // and positive values from the array
    let minNeg = Number.MAX_SAFE_INTEGER,
    maxNeg = Number.MAX_SAFE_INTEGER;

    let minPos = Number.MIN_SAFE_INTEGER,
    maxPos = Number.MIN_SAFE_INTEGER;

    // To store whether 0 is present in the array
    let isZeroPresent = false;

    // Update the values of the
    // above defined variables
    for (let i = 0; i < n; i++) {
        if (arr[i] == 0) {
            isZeroPresent = true;
        }
        else if (arr[i] < 0) {
            minNeg = Math.min(minNeg, arr[i]);
            maxNeg = Math.max(maxNeg, arr[i]);
        }
        else {
            minPos = Math.min(minPos, arr[i]);
            maxPos = Math.max(maxPos, arr[i]);
        }
    }

    // To store the resultant sum
    let sum = 0;

    // x will not contribute to the
    // sum if it is equal to 0
    if (x != 0) {

        // If x is negative
        if (x < 0) {

            // Either multiply it with the minimum
            // negative number from the array
            if (minNeg != Number.MAX_SAFE_INTEGER)
                sum += (x * minNeg);

            // Or multiply it with the minimum
            // positive element if zero is
            // not present in the array
            else if (!isZeroPresent)
                sum += (x * minPos);
        }

        // If x is positive
        else {

            // Multiply it with the maximum
            // positive value from the array
            if (maxPos != Number.MIN_SAFE_INTEGER)
                sum += (x * maxPos);

            // Or multiply it with the maximum
            // negative element if zero is
            // not present in the array
            else if (!isZeroPresent)
                sum += (x * maxPos);
        }
    }

    // Same as x
    if (y != 0) {
        if (y < 0) {
            if (minNeg != Number.MAX_SAFE_INTEGER)
                sum += (y * minNeg);
            else if (!isZeroPresent)
                sum += (y * minPos);
        }
        else {
            if (maxPos != Number.MIN_SAFE_INTEGER)
                sum += (y * maxPos);
            else if (!isZeroPresent)
                sum += (y * maxPos);
        }
    }

    // Same as x
    if (z != 0) {
        if (z < 0) {
            if (minNeg != Number.MAX_SAFE_INTEGER)
                sum += (z * minNeg);
            else if (!isZeroPresent)
                sum += (z * minPos);
        }
        else {
            if (maxPos != Number.MIN_SAFE_INTEGER)
                sum += (z * maxPos);
            else if (!isZeroPresent)
                sum += (z * maxPos);
        }
    }

    return sum;
}

// Driver code

let arr = [2, 4, -9, -64, 7, 3];
let n = arr.length;
let x = -1, y = 1, z = 1;

document.write(maxSum(arr, n, x, y, z));

</script>
```

**Output:** 

```
78
```