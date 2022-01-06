# 正积最长子阵列的长度

> 原文:[https://www . geeksforgeeks . org/带正积的最长子阵列长度/](https://www.geeksforgeeks.org/length-of-longest-subarray-with-positive-product/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是用一个正整数打印最长子数组的长度。

**示例:**

> **输入:** arr[] ={0，1，-2，-3，-4}
> 输出:3
> ***解释:***
> 正积最长的子阵是:{1，-2，-3}。因此，所需长度为 3。
> 
> **输入:** arr[]={-1，-2，0，1，2}
> **输出:** 2
> **解释:**
> 正积最长的子阵是:{-1，-2}，{1，2}。因此，所需长度为 2。

**天真方法:**解决问题最简单的方法是[生成所有可能的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并检查其乘积是否为正。在所有这样的子阵列中，打印获得的最长子阵列的长度。
***时间复杂度:**(N<sup>3</sup>)*
***辅助空间:** O(1)*
**高效途径:**问题可以使用[动态规划解决。](https://www.geeksforgeeks.org/dynamic-programming/)这里的想法是保持正元素和负元素的计数，使得它们的乘积为正。按照以下步骤解决问题:

1.  初始化变量，比如 **res** ，以存储正积的最长子阵列的长度。
2.  初始化两个变量 **Pos** 和 **Neg** ，分别存储当前子阵列的长度和正负乘积。
3.  迭代数组。
4.  **如果 arr[i] = 0:** 重置**位置**和**位置**的值。
5.  **如果 arr[i] > 0:** 将**位置**增加 1。如果负乘积的子阵列中至少存在一个元素，则将 **Neg** 增加 1。
6.  **如果 arr[i] < 0:** 交换**位置**和**位置**并将**位置**增加 1。如果至少有一个元素存在于正积的子阵列中，则也递增**位置**。
7.  更新 **res=max(res，Pos)。**

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// longest subarray whose product
// is positive
int maxLenSub(int arr[], int N)
{
    // Stores the length of current
    // subarray with positive product
    int Pos = 0;

    // Stores the length of current
    // subarray with negative product
    int Neg = 0;

    // Stores the length of the longest
    // subarray with positive product
    int res = 0;

    for (int i = 0; i < N; i++) {

        if (arr[i] == 0) {

            // Reset the value
            Pos = Neg = 0;
        }

        // If current element is positive
        else if (arr[i] > 0) {

            // Increment the length of
            // subarray with positive product
            Pos += 1;

            // If at least one element is
            // present in the subarray with
            // negative product
            if (Neg != 0) {

                Neg += 1;
            }

            // Update res
            res = max(res, Pos);
        }

        // If current element is negative
        else {

            swap(Pos, Neg);

            // Increment the length of subarray
            // with negative product
            Neg += 1;

            // If at least one element is present
            // in the subarray with positive product
            if (Pos != 0) {

                Pos += 1;
            }

            // Update res
            res = max(res, Pos);
        }
    }
    return res;
}

// Driver Code
int main()
{
    int arr[] = { -1, -2, -3, 0, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maxLenSub(arr, N);
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the length of
# longest subarray whose product
# is positive
def maxLenSub(arr, N):

    # Stores the length of current
    # subarray with positive product
    Pos = 0

    # Stores the length of current
    # subarray with negative product
    Neg = 0

    # Stores the length of the longest
    # subarray with positive product
    res = 0

    for i in range(N):
        if (arr[i] == 0):

            # Reset the value
            Pos = Neg = 0

        # If current element is positive
        elif (arr[i] > 0):

            # Increment the length of
            # subarray with positive product
            Pos += 1

            # If at least one element is
            # present in the subarray with
            # negative product
            if (Neg != 0):
                Neg += 1

            # Update res
            res = max(res, Pos)

        # If current element is negative
        else:
            Pos, Neg = Neg, Pos

            # Increment the length of subarray
            # with negative product
            Neg += 1

            # If at least one element is present
            # in the subarray with positive product
            if (Pos != 0):
                Pos += 1

            # Update res
            res = max(res, Pos)

    return res

# Driver Code
if __name__ == '__main__':

    arr = [ -1, -2, -3, 0, 1 ]
    N = len(arr)

    print(maxLenSub(arr, N))

# This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the length of
// longest subarray whose product
// is positive
static int maxLenSub(int arr[], int N)
{
    // Stores the length of current
    // subarray with positive product
    int Pos = 0;

    // Stores the length of current
    // subarray with negative product
    int Neg = 0;

    // Stores the length of the longest
    // subarray with positive product
    int res = 0;

    for (int i = 0; i < N; i++)
    {
        if (arr[i] == 0)
        {
            // Reset the value
            Pos = Neg = 0;
        }

        // If current element is positive
        else if (arr[i] > 0)
        {
            // Increment the length of
            // subarray with positive product
            Pos += 1;

            // If at least one element is
            // present in the subarray with
            // negative product
            if (Neg != 0)
            {
                Neg += 1;
            }

            // Update res
            res = Math.max(res, Pos);
        }

        // If current element is negative
        else
        {
            Pos = Pos + Neg;
            Neg = Pos - Neg;
            Pos = Pos - Neg;

            // Increment the length of subarray
            // with negative product
            Neg += 1;

            // If at least one element is present
            // in the subarray with positive product
            if (Pos != 0)
            {
                Pos += 1;
            }

            // Update res
            res = Math.max(res, Pos);
        }
    }
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = {-1, -2, -3, 0, 1};
    int N = arr.length;
    System.out.print(maxLenSub(arr, N));
}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to find the length of
// longest subarray whose product
// is positive
static int maxLenSub(int[] arr, int N)
{
    // Stores the length of current
    // subarray with positive product
    int Pos = 0;

    // Stores the length of current
    // subarray with negative product
    int Neg = 0;

    // Stores the length of the longest
    // subarray with positive product
    int res = 0;

    for (int i = 0; i < N; i++)
    {
        if (arr[i] == 0)
        {
            // Reset the value
            Pos = Neg = 0;
        }

        // If current element is positive
        else if (arr[i] > 0)
        {
            // Increment the length of
            // subarray with positive product
            Pos += 1;

            // If at least one element is
            // present in the subarray with
            // negative product
            if (Neg != 0)
            {
                Neg += 1;
            }

            // Update res
            res = Math.Max(res, Pos);
        }

        // If current element is negative
        else
        {
            Pos = Pos + Neg;
            Neg = Pos - Neg;
            Pos = Pos - Neg;

            // Increment the length of subarray
            // with negative product
            Neg += 1;

            // If at least one element is present
            // in the subarray with positive product
            if (Pos != 0)
            {
                Pos += 1;
            }

            // Update res
            res = Math.Max(res, Pos);
        }
    }
    return res;
}

// Driver Code
public static void Main()
{
    int[] arr = {-1, -2, -3, 0, 1};
    int N = arr.Length;
    Console.Write(maxLenSub(arr, N));
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the length of
// longest subarray whose product
// is positive
function maxLenSub(arr, N)
{
    // Stores the length of current
    // subarray with positive product
    var Pos = 0;

    // Stores the length of current
    // subarray with negative product
    var Neg = 0;

    // Stores the length of the longest
    // subarray with positive product
    var res = 0;

    for (var i = 0; i < N; i++) {

        if (arr[i] == 0) {

            // Reset the value
            Pos = Neg = 0;
        }

        // If current element is positive
        else if (arr[i] > 0) {

            // Increment the length of
            // subarray with positive product
            Pos += 1;

            // If at least one element is
            // present in the subarray with
            // negative product
            if (Neg != 0) {

                Neg += 1;
            }

            // Update res
            res = Math.max(res, Pos);
        }

        // If current element is negative
        else {

            [Pos, Neg] = [Neg, Pos];

            // Increment the length of subarray
            // with negative product
            Neg += 1;

            // If at least one element is present
            // in the subarray with positive product
            if (Pos != 0) {

                Pos += 1;
            }

            // Update res
            res = Math.max(res, Pos);
        }
    }
    return res;
}

// Driver Code
var arr = [-1, -2, -3, 0, 1];
var N = arr.length;
document.write( maxLenSub(arr, N));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)