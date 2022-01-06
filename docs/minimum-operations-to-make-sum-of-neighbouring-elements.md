# 求相邻元素之和的最小运算< = X

> 原文:[https://www . geeksforgeeks . org/对相邻元素求和的最小操作数/](https://www.geeksforgeeks.org/minimum-operations-to-make-sum-of-neighbouring-elements/)

给定一个由 **N** 元素组成的数组 **arr[]** 和一个整数 **X** ，任务是找到使相邻元素之和小于给定数量 **X** 所需的最小运算次数。在单次操作中，您可以选择一个元素 **arr[i]** ，并将其值减少 **1** 。
**示例:**

> **输入:** arr[] = {2，2，2}，X = 3
> **输出:** 1
> 将 arr[1]减 1，数组变成{2，1，2}。
> 现在，2 + 1 = 3 和 1 + 2 = 3
> **输入:** arr[] = {1，6，1，2，0，4}，X = 1
> **输出:** 11

**方法:**假设数组的元素是 **a1，a2，…，和**。假设所有**a【I】**都大于 **X** 的情况。
首先我们需要让所有的**a【I】**等于 **x** 。我们将计算它所需的操作次数。
现在，所有元素都将是 **x，x，x，x…，x** N 次的形式。这里我们可以观察到最大相邻和等于 **2 * X** 。
现在，从左到右遍历数组，对于每个 **i** ，如果两个左邻的和为**a[I]+a[I–1]>X**，则将 **a[i]** 更改为它们的净和等于 **X** 的值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// number of operations required
int MinOperations(int n, int x, int* arr)
{

    // To store total operations required
    int total = 0;
    for (int i = 0; i < n; ++i) {

        // First make all elements equal to x
        // which are currenctly greater
        if (arr[i] > x) {
            int difference = arr[i] - x;
            total = total + difference;
            arr[i] = x;
        }
    }

    // Left scan the array
    for (int i = 1; i < n; ++i) {
        int LeftNeigbouringSum = arr[i] + arr[i - 1];

        // Update the current element such that
        // neighbouring sum is < x
        if (LeftNeigbouringSum > x) {
            int current_diff = LeftNeigbouringSum - x;
            arr[i] = max(0, arr[i] - current_diff);
            total = total + current_diff;
        }
    }
    return total;
}

// Driver code
int main()
{
    int X = 1;
    int arr[] = { 1, 6, 1, 2, 0, 4 };
    int N = sizeof(arr) / sizeof(int);
    cout << MinOperations(N, X, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum
// number of operations required
static int MinOperations(int n, int x, int[] arr)
{

    // To store total operations required
    int total = 0;
    for (int i = 0; i < n; ++i)
    {

        // First make all elements equal to x
        // which are currenctly greater
        if (arr[i] > x)
        {
            int difference = arr[i] - x;
            total = total + difference;
            arr[i] = x;
        }
    }

    // Left scan the array
    for (int i = 1; i < n; ++i)
    {
        int LeftNeigbouringSum = arr[i] + arr[i - 1];

        // Update the current element such that
        // neighbouring sum is < x
        if (LeftNeigbouringSum > x)
        {
            int current_diff = LeftNeigbouringSum - x;
            arr[i] = Math.max(0, arr[i] - current_diff);
            total = total + current_diff;
        }
    }
    return total;
}

// Driver code
public static void main(String args[])
{
    int X = 1;
    int arr[] = { 1, 6, 1, 2, 0, 4 };
    int N = arr.length;
    System.out.println(MinOperations(N, X, arr));
}
}

// This code is contributed by 29AjayKumar
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the minimum
# number of operations required
def MinOperations(n, x, arr):

    # To store total operations required
    total = 0
    for i in range(n):

        # First make all elements equal to x
        # which are currenctly greater
        if (arr[i] > x):
            difference = arr[i] - x
            total = total + difference
            arr[i] = x

    # Left scan the array
    for i in range(n):
        LeftNeigbouringSum = arr[i] + arr[i - 1]

        # Update the current element such that
        # neighbouring sum is < x
        if (LeftNeigbouringSum > x):
            current_diff = LeftNeigbouringSum - x
            arr[i] = max(0, arr[i] - current_diff)
            total = total + current_diff

    return total

# Driver code
X = 1
arr=[1, 6, 1, 2, 0, 4 ]
N = len(arr)
print(MinOperations(N, X, arr))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum
// number of operations required
static int MinOperations(int n, int x, int[] arr)
{

    // To store total operations required
    int total = 0;
    for (int i = 0; i < n; ++i)
    {

        // First make all elements equal to x
        // which are currenctly greater
        if (arr[i] > x)
        {
            int difference = arr[i] - x;
            total = total + difference;
            arr[i] = x;
        }
    }

    // Left scan the array
    for (int i = 1; i < n; ++i)
    {
        int LeftNeigbouringSum = arr[i] + arr[i - 1];

        // Update the current element such that
        // neighbouring sum is < x
        if (LeftNeigbouringSum > x)
        {
            int current_diff = LeftNeigbouringSum - x;
            arr[i] = Math.Max(0, arr[i] - current_diff);
            total = total + current_diff;
        }
    }
    return total;
}

// Driver code
public static void Main(String []args)
{
    int X = 1;
    int []arr = { 1, 6, 1, 2, 0, 4 };
    int N = arr.Length;
    Console.WriteLine(MinOperations(N, X, arr));
}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the minimum
// number of operations required
function MinOperations(n, x, arr)
{

    // To store total operations required
    let total = 0;
    for (let i = 0; i < n; ++i)
    {

        // First make all elements equal to x
        // which are currenctly greater
        if (arr[i] > x)
        {
            let difference = arr[i] - x;
            total = total + difference;
            arr[i] = x;
        }
    }

    // Left scan the array
    for (let i = 1; i < n; ++i)
    {
        let LeftNeigbouringSum = arr[i] + arr[i - 1];

        // Update the current element such that
        // neighbouring sum is < x
        if (LeftNeigbouringSum > x)
        {
            let current_diff = LeftNeigbouringSum - x;
            arr[i] = Math.max(0, arr[i] - current_diff);
            total = total + current_diff;
        }
    }
    return total;
}

// Driver code
let X = 1;
let arr = [ 1, 6, 1, 2, 0, 4 ];
let N = arr.length;
document.write(MinOperations(N, X, arr)+"<br>");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
11
```