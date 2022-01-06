# 最小化减法，然后增加相邻元素，使所有数组元素相等

> 原文:[https://www . geeksforgeeks . org/minimum-减法-后跟相邻元素的增量-要求使所有数组元素相等/](https://www.geeksforgeeks.org/minimize-subtraction-followed-by-increments-of-adjacent-elements-required-to-make-all-array-elements-equal/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过重复**从任意数量的数组元素中减去 1** 并将其同时添加到相邻元素中的一个来使所有数组元素相等。如果不能使所有数组元素相等，则打印 **"-1"** 。否则，打印所需的最小操作数。

**示例:**

> **输入:** arr[] = {1，0，5}
> **输出:** 3
> **解释:**
> **运算 1:** 用 1 减去 arr[2](= 5)再加到 arr[1](= 0)。因此，数组 arr[]修改为{1，1，4}。
> **运算 2:** 用 1 减去 arr[2](= 4)再加到 arr[1](= 1)。因此，数组 arr[]修改为{1，2，3}。
> **运算 3:** 用 1 减去 arr[2](= 3)和 arr[1](= 2)，分别加到 arr[1](= 1)和 arr[2](= 2)上。因此，数组 arr[]修改为{2，2，2}。
> 
> 因此，所需的最小操作数是 3。
> 
> **输入:** arr[] = {0，3，0 }
> T3】输出: 2

**方法:**给定的问题可以基于以下观察来解决:

*   当且仅当所有数组元素的值等于[数组的平均值](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)时，所有数组元素才能相等。
*   由于一次只能从一个数组元素中减去 **1** ，因此最小移动次数是数组的[前缀和的最大值，或者是使每个元素等于数组平均值所需的移动次数。](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)

按照以下步骤解决问题:

*   计算数组元素的[和**arr【】**，比如 **S** 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   如果总和 **S** 不能被 **N** 整除，则打印**-1”**。
*   否则，请执行以下操作:
    *   将数组元素的[平均值存储在一个变量中，比如**平均值**。](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)
    *   初始化两个变量，用 **0** 表示**总计**和**计数**，存储所需结果和最小移动的前缀和，分别达到**平均值**。
    *   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
        *   将**(arr[I]–avg)**的值加到**计数**上。
        *   将**总计**的值更新为**计数**、**总计**、**(arr[I]–avg)**的[绝对值](https://www.geeksforgeeks.org/program-to-find-absolute-value-of-a-given-number/)的最大值。
*   完成上述步骤后，打印**总计**的值，作为所需的最小操作结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of moves required to make all array
// elements equal
int findMinMoves(int arr[], int N)
{
    // Store the total sum of the array
    int sum = 0;

    // Calculate total sum of the array
    for (int i = 0; i < N; i++)
        sum += arr[i];

    // If the sum is not divisible
    // by N, then print "-1"
    if (sum % N != 0)
        return -1;

    // Stores the average
    int avg = sum / N;

    // Stores the count
    // of operations
    int total = 0;

    int needCount = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Update number of moves
        // required to make current
        // element equal to avg
        needCount += (arr[i] - avg);

        // Update the overall count
        total
            = max(max(abs(needCount),
                      arr[i] - avg),
                  total);
    }

    // Return the minimum
    // operations required
    return total;
}

// Driver Code
int main()
{
    int arr[] = { 1, 0, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << findMinMoves(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the minimum number
// of moves required to make all array
// elements equal
static int findMinMoves(int[] arr, int N)
{

    // Store the total sum of the array
    int sum = 0;

    // Calculate total sum of the array
    for(int i = 0; i < N; i++)
        sum += arr[i];

    // If the sum is not divisible
    // by N, then print "-1"
    if (sum % N != 0)
        return -1;

    // Stores the average
    int avg = sum / N;

    // Stores the count
    // of operations
    int total = 0;

    int needCount = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Update number of moves
        // required to make current
        // element equal to avg
        needCount += (arr[i] - avg);

        // Update the overall count
        total = Math.max(
            Math.max(Math.abs(needCount),
                     arr[i] - avg), total);
    }

    // Return the minimum
    // operations required
    return total;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 0, 5 };
    int N = arr.length;

    System.out.println(findMinMoves(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of moves required to make all array
# elements equal
def findMinMoves(arr, N):

    # Store the total sum of the array
    sum = 0

    # Calculate total sum of the array
    for i in range(N):
        sum += arr[i]

    # If the sum is not divisible
    # by N, then print "-1"
    if(sum % N != 0):
        return -1

    # Stores the average
    avg = sum // N

    # Stores the count
    # of operations
    total = 0
    needCount = 0

    # Traverse the array arr[]
    for i in range(N):

        # Update number of moves
        # required to make current
        # element equal to avg
        needCount += (arr[i] - avg)

        # Update the overall count
        total = max(max(abs(needCount), arr[i] - avg), total)

    # Return the minimum
    # operations required
    return total

# Driver Code
if __name__ == '__main__':
    arr =  [1, 0, 5]
    N =  len(arr)
    print(findMinMoves(arr, N))

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum number
// of moves required to make all array
// elements equal
static int findMinMoves(int[] arr, int N)
{

    // Store the total sum of the array
    int sum = 0;

    // Calculate total sum of the array
    for(int i = 0; i < N; i++)
        sum += arr[i];

    // If the sum is not divisible
    // by N, then print "-1"
    if (sum % N != 0)
        return -1;

    // Stores the average
    int avg = sum / N;

    // Stores the count
    // of operations
    int total = 0;

    int needCount = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Update number of moves
        // required to make current
        // element equal to avg
        needCount += (arr[i] - avg);

        // Update the overall count
        total = Math.Max(
            Math.Max(Math.Abs(needCount),
                     arr[i] - avg), total);
    }

    // Return the minimum
    // operations required
    return total;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 0, 5 };
    int N = arr.Length;

    Console.Write(findMinMoves(arr, N));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum number
// of moves required to make all array
// elements equal
function findMinMoves(arr, N)
{

    // Store the total sum of the array
    let sum = 0;

    // Calculate total sum of the array
    for(let i = 0; i < N; i++)
        sum += arr[i];

    // If the sum is not divisible
    // by N, then print "-1"
    if (sum % N != 0)
        return -1;

    // Stores the average
    let avg = sum / N;

    // Stores the count
    // of operations
    let total = 0;

    let needCount = 0;

    // Traverse the array arr[]
    for(let i = 0; i < N; i++)
    {

        // Update number of moves
        // required to make current
        // element equal to avg
        needCount += (arr[i] - avg);

        // Update the overall count
        total = Math.max(Math.max(
                Math.abs(needCount),
                arr[i] - avg), total);
    }

    // Return the minimum
    // operations required
    return total;
}

// Driver Code
let arr = [ 1, 0, 5 ];
let N = arr.length;

document.write(findMinMoves(arr, N))

// This code is contributed by Hritik

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)