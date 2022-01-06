# 最小化要移除的数组元素的数量，以最大化任意对之间的差异，直到 K

> 原文:[https://www . geeksforgeeks . org/最小化-要移除的数组元素数-最大化-k 上任意对之间的差异/](https://www.geeksforgeeks.org/minimize-count-of-array-elements-to-be-removed-to-maximize-difference-between-any-pair-up-to-k/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是计算要从数组中移除的元素的数量，使得剩余的最大和最小数量之差不超过 K

**示例:**

> **输入:** K = 1，arr[] = {1，2，3，4，5}
> **输出:** 3
> **解释:**
> 移除{5，4，3}将数组修改为{1，2}，其中最大差异为 1(= K)。
> **输入:** K = 3，arr[] = {1，2，3，4，5}
> **输出:** 1
> **解释:**
> 移除{5}会将数组修改为{1，2，3，4}，其中最大差异为 3(= K)。

**进场:**
任务是找出**最大**和**最小**阵元之间的差，不要超过 **K** 。

*   按升序对数组进行排序，并将变量初始化为最小值。
*   迭代数组至[生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，并检查任一对之间的差值是否小于或等于 **K** 。
*   更新每对的最小移除次数。
*   最后，打印获得的最小清除量。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// elements to be removed from the
// array based on the given condition
int min_remove(int arr[], int n, int k)
{
    // Sort the array
    sort(arr, arr + n);

    /// Initialize the variable
    int ans = INT_MAX;

    // Iterate for all possible pairs
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {

            // Check the difference
            // between the numbers
            if (arr[j] - arr[i] <= k) {

                // Update the minimum removals
                ans = min(ans, n - j + i - 1);
            }
        }
    }
    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    int k = 3;
    int arr[] = { 1, 2, 3, 4, 5 };

    int n = sizeof arr / sizeof arr[0];

    cout << min_remove(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to count the number of
// elements to be removed from the
// array based on the given condition
static int min_remove(int arr[], int n, int k)
{
    // Sort the array
    Arrays.sort(arr);

    /// Initialize the variable
    int ans = Integer.MAX_VALUE;

    // Iterate for all possible pairs
    for (int i = 0; i < n; i++)
    {
        for (int j = i; j < n; j++)
        {

            // Check the difference
            // between the numbers
            if (arr[j] - arr[i] <= k)
            {

                // Update the minimum removals
                ans = Math.min(ans, n - j + i - 1);
            }
        }
    }
    // Return the answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int k = 3;
    int arr[] = { 1, 2, 3, 4, 5 };

    int n = arr.length;

    System.out.print(min_remove(arr, n, k));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to count the number of
# elements to be removed from the
# array based on the given condition
def min_remove(arr, n, k):

    # Sort the array
    arr.sort()

    # Initialize the variable
    ans = sys.maxsize

    # Iterate for all possible pairs
    for i in range(n):
        for j in range(i, n):

            # Check the difference
            # between the numbers
            if (arr[j] - arr[i] <= k):

                # Update the minimum removals
                ans = min(ans, n - j + i - 1)

    # Return the answer
    return ans

# Driver Code
if __name__ == "__main__":

    k = 3
    arr = [ 1, 2, 3, 4, 5 ]

    n = len(arr)

    print (min_remove(arr, n, k))

# This code is contributed by chitranayal
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Function to count the number of
// elements to be removed from the
// array based on the given condition
static int min_remove(int []arr, int n, int k)
{
    // Sort the array
    Array.Sort(arr);

    /// Initialize the variable
    int ans = int.MaxValue;

    // Iterate for all possible pairs
    for (int i = 0; i < n; i++)
    {
        for (int j = i; j < n; j++)
        {

            // Check the difference
            // between the numbers
            if (arr[j] - arr[i] <= k)
            {

                // Update the minimum removals
                ans = Math.Min(ans, n - j + i - 1);
            }
        }
    }
    // Return the answer
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int k = 3;
    int []arr = { 1, 2, 3, 4, 5 };

    int n = arr.Length;

    Console.Write(min_remove(arr, n, k));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to count the number of
// elements to be removed from the
// array based on the given condition
function min_remove(arr, n, k)
{
    // Sort the array
    arr.sort();

    /// Initialize the variable
    let ans = Number.MAX_VALUE;

    // Iterate for all possible pairs
    for (let i = 0; i < n; i++)
    {
        for (let j = i; j < n; j++)
        {

            // Check the difference
            // between the numbers
            if (arr[j] - arr[i] <= k)
            {

                // Update the minimum removals
                ans = Math.min(ans, n - j + i - 1);
            }
        }
    }
    // Return the answer
    return ans;
}

// Driver Code

    let k = 3;
    let arr = [ 1, 2, 3, 4, 5 ];

    let n = arr.length;

    document.write(min_remove(arr, n, k));

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*