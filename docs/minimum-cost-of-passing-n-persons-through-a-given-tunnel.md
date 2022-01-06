# N 人通过给定隧道的最小成本

> 原文:[https://www . geesforgeks . org/通过给定隧道的最小通行成本 n 人/](https://www.geeksforgeeks.org/minimum-cost-of-passing-n-persons-through-a-given-tunnel/)

给定两个正整数 **X** 和 **Y** 和一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr【】使得**arr【I】**代表第 **i <sup>个</sup>人**的高度，并且有一个高度为 **H** 的隧道， 任务是找出所有 **N 人**通过给定隧道所需的总最小费用，这样高度之和小于 **H** 的最多两人**可以按照以下规则一次通过:

*   两个人一次通过隧道，那么费用为 **Y** 。
*   当一个人一次通过隧道，那么成本就是 **X** 。

***注:**所有阵元小于 **H** 。*

**示例:**

> **输入:** arr[] = {1，3，4，4，2}，X = 4，Y = 6，H = 9
> **输出:** 16
> **解释:**
> 按照以下顺序考虑人员的通过:
> 
> 1.  分别具有高度 1 和 4 的人 1 和人 4 的高度之和为 1 + 4 = 5 < H(= 9)。因此，该操作的成本为 Y(= 6)。
> 2.  分别具有高度 3 和 4 的人 2 和人 3 的高度之和为 3 + 4 = 7 < H(= 9)。因此，该操作的成本为 Y(= 6)。
> 3.  人 5 的身高 3 小于 H(= 9)。因此，这项操作的成本是 X( = 4)。
> 
> 因此，总成本为 6 + 6 + 4 = 16，这在所有可能的组合中是最小的。
> 
> **输入:** arr[] = {1，3，4}，X = 4，Y = 6，H = 9
> **输出:** 10

**方法:**使用 [**贪婪方法**](https://www.geeksforgeeks.org/greedy-algorithms/) 和使用 [**双指针技术**](https://www.geeksforgeeks.org/two-pointers-technique/) 可以解决给定的问题。想法是用 **Y** 的代价选择那两个高度之和小于 **H** 的人。否则，在两人中选择最大高度的人，以 **X** 的费用通过进入隧道。按照以下步骤解决问题:

*   [按照递增顺序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对给定数组 **arr[]** 进行排序。
*   初始化两个指针，分别将 **i** 和 **j** 设为 **0** 和**(N–1)**指向数组的末端。
*   [迭代直到 **i** 的值小于**j**T5】并执行以下步骤:](https://www.geeksforgeeks.org/range-based-loop-c/)
    *   如果**arr【I】**和**arr【j】**的值之和小于 **H** ，那么将 **cost** 的值增加 **Y** ，将 **i** 的值增加 **j** 的值减少 **1** 。
    *   否则，将 **j** 的值递减 **1** ，将**成本**的值更新 **X** 。
*   如果 **i** 和 **j** 的值相等，则成本值增加 **X** 。
*   完成上述步骤后，打印**成本**的值作为最终最小成本。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function to find the minimum total
// cost of passing at most two-person
// at a time through the tunnel
int minimumCost(int arr[], int N, int H,
                int X, int Y)
{

    // Stores the resultant cost
    int cost = 0;

    // Sort the given array
    sort(arr, arr + N);

    // Initialize two pointers
    int i = 0, j = N - 1;

    // Iterate until i is less than j
    while (i < j) {

        // If the sum of values at
        // i and j is less than H
        if (arr[i] + arr[j] < H) {

            // Increment the cost
            cost += Y;

            // Update the pointers
            i++;
            j--;
        }

        // Otherwise
        else {
            cost += X;
            j--;
        }
    }

    // If i and j points to the same
    // element, then that person is
    // not passed to the tunnel
    if (i == j)
        cost += X;

    // Return the minimum of the total
    // cost and cost of passing all the
    // person individually
    return min(cost, N * X);
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 4, 4, 2 };
    int X = 4, Y = 6, H = 9;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << minimumCost(arr, N, H, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Arrays;

class GFG{

// Function to find the minimum total
// cost of passing at most two-person
// at a time through the tunnel
public static int minimumCost(int arr[], int N, int H,
                              int X, int Y)
{

    // Stores the resultant cost
    int cost = 0;

    // Sort the given array
    Arrays.sort(arr);

    // Initialize two pointers
    int i = 0, j = N - 1;

    // Iterate until i is less than j
    while (i < j)
    {

        // If the sum of values at
        // i and j is less than H
        if (arr[i] + arr[j] < H)
        {

            // Increment the cost
            cost += Y;

            // Update the pointers
            i++;
            j--;
        }

        // Otherwise
        else
        {
            cost += X;
            j--;
        }
    }

    // If i and j points to the same
    // element, then that person is
    // not passed to the tunnel
    if (i == j)
        cost += X;

    // Return the minimum of the total
    // cost and cost of passing all the
    // person individually
    return Math.min(cost, N * X);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 3, 4, 4, 2 };
    int X = 4, Y = 6, H = 9;
    int N = arr.length;

    System.out.println(minimumCost(arr, N, H, X, Y));
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the minimum total
# cost of passing at most two-person
# at a time through the tunnel
def minimumCost(arr, N, H, X, Y):

    # Stores the resultant cost
    cost = 0

    # Sort the given array
    arr.sort()

    # Initialize two pointers
    i = 0
    j = N - 1

    # Iterate until i is less than j
    while (i < j):

        # If the sum of values at
        # i and j is less than H
        if (arr[i] + arr[j] < H):

            # Increment the cost
            cost += Y

            # Update the pointers
            i += 1
            j -= 1

        # Otherwise
        else:
            cost += X
            j -= 1

    # If i and j points to the same
    # element, then that person is
    # not passed to the tunnel
    if (i == j):
        cost += X

    # Return the minimum of the total
    # cost and cost of passing all the
    # person individually
    return min(cost, N * X)

# Driver Code
if __name__ == '__main__':
    arr = [1, 3, 4, 4, 2]
    X = 4
    Y = 6
    H = 9
    N = len(arr)
    print(minimumCost(arr, N, H, X, Y))

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the minimum total
    // cost of passing at most two-person
    // at a time through the tunnel
    static int minimumCost(int[] arr, int N, int H, int X,
                           int Y)
    {

        // Stores the resultant cost
        int cost = 0;

        // Sort the given array
        Array.Sort(arr);

        // Initialize two pointers
        int i = 0, j = N - 1;

        // Iterate until i is less than j
        while (i < j) {

            // If the sum of values at
            // i and j is less than H
            if (arr[i] + arr[j] < H) {

                // Increment the cost
                cost += Y;

                // Update the pointers
                i++;
                j--;
            }

            // Otherwise
            else {
                cost += X;
                j--;
            }
        }

        // If i and j points to the same
        // element, then that person is
        // not passed to the tunnel
        if (i == j)
            cost += X;

        // Return the minimum of the total
        // cost and cost of passing all the
        // person individually
        return Math.Min(cost, N * X);
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, 3, 4, 4, 2 };
        int X = 4, Y = 6, H = 9;
        int N = arr.Length;

        Console.WriteLine(minimumCost(arr, N, H, X, Y));
    }
}

// This code is contributed by subhammahato348.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum total
// cost of passing at most two-person
// at a time through the tunnel
function minimumCost(arr, N, H, X, Y)
{

    // Stores the resultant cost
    let cost = 0;

    // Sort the given array
    arr.sort(function(a, b){return a - b});

    // Initialize two pointers
    let i = 0, j = N - 1;

    // Iterate until i is less than j
    while (i < j)
    {

        // If the sum of values at
        // i and j is less than H
        if (arr[i] + arr[j] < H)
        {

            // Increment the cost
            cost += Y;

            // Update the pointers
            i++;
            j--;
        }

        // Otherwise
        else
        {
            cost += X;
            j--;
        }
    }

    // If i and j points to the same
    // element, then that person is
    // not passed to the tunnel
    if (i == j)
        cost += X;

    // Return the minimum of the total
    // cost and cost of passing all the
    // person individually
    return Math.min(cost, N * X);
}

// Driver Code
let arr = [ 1, 3, 4, 4, 2 ];
let X = 4, Y = 6, H = 9;
let N = arr.length;

document.write(minimumCost(arr, N, H, X, Y));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
16
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*