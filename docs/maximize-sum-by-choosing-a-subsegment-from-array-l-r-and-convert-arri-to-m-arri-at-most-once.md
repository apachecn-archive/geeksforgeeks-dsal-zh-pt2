# 通过从数组[l，r]中选择一个子段来最大化总和，最多将 arr[i]转换为(M–arr[I])

> 原文:[https://www . geesforgeks . org/通过选择一个子段来最大化总和-从数组-l-r-and-convert-arri-m-arri-至多一次/](https://www.geeksforgeeks.org/maximize-sum-by-choosing-a-subsegment-from-array-l-r-and-convert-arri-to-m-arri-at-most-once/)

给定一个由 **N** 个正整数和一个正整数 **M** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、 **arr[]** ，任务是在最多执行一次运算后使数组的和最大化。在一个操作中，从数组**【l，r】**中选择一个子段，并将 **arr[i]** 转换为**M–arr[I]**，其中 **l≤i≤r** 。

**示例:**

> **输入:** arr[] = {2，4，3}，M = 5
> **输出:** 10
> **解释:**将子阵中的数字从索引 0 替换为索引 0，这样新的数组就变成了[5-2，4，3]，所以最大和就是(5-2) + 4 + 3 = 10
> 
> **输入:** arr[] = {4，3，4}，M = 5
> T3】输出: 11

**天真法:**解决问题最简单的方法是对阵列的所有子阵列应用运算，并应用给定的运算找到最大和。

**时间复杂度:**O(N<sup>3</sup>)
T5】辅助空间: O(1)

**高效方法:**上述方法可以通过[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)进一步优化。按照以下步骤解决问题:

*   初始化一个变量，比如 sum 为 0 来存储数组的和。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并将变量 **arr[i]** 添加到变量 **sum** 中，并将 **arr[i]** 的值修改为**M–2×arr[I]**。
*   现在将[卡丹的算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)应用到[阵](https://www.geeksforgeeks.org/array-data-structure/)T4【arr】上。
*   初始化两个变量，说 **mx** 和 **ans** 为 **0** 。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤:
    *   将**arr【I】**添加到 **ans** 中。
    *   如果 **ans < 0** ，则将 **ans** 的值修改为 **0** 。
    *   将 **mx** 的值修改为 **max(mx，ans)** 。
*   打印 **sum + mx** 的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to maximize the sum after
// performing atmost one operation
int MaxSum(int arr[], int n, int M)
{
    // Variable to store the sum
    int sum = 0;

    // Traverse the array and modify arr[]
    for (int i = 0; i < n; i++) {
        sum += arr[i];
        arr[i] = (M - 2 * arr[i]);
    }

    int ans = 0, mx = 0;

    // Apply Kadane's algorithm
    for (int i = 0; i < n; i++) {
        // Add a[i] to ans
        ans += arr[i];

        // If ans<0, modify the value
        // of ans as 0
        if (ans < 0)
            ans = 0;

        // Update the value of mx
        mx = max(mx, ans);
    }

    // Return the maximum sum
    return mx + sum;
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 2, 4, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = 5;

    // Function Call
    cout << MaxSum(arr, N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to maximize the sum after
// performing atmost one operation
static int MaxSum(int arr[], int n, int M)
{

    // Variable to store the sum
    int sum = 0;

    // Traverse the array and modify arr[]
    for (int i = 0; i < n; i++) {
        sum += arr[i];
        arr[i] = (M - 2 * arr[i]);
    }

    int ans = 0, mx = 0;

    // Apply Kadane's algorithm
    for (int i = 0; i < n; i++)
    {

        // Add a[i] to ans
        ans += arr[i];

        // If ans<0, modify the value
        // of ans as 0
        if (ans < 0)
            ans = 0;

        // Update the value of mx
        mx = Math.max(mx, ans);
    }

    // Return the maximum sum
    return mx + sum;
}

// Driver Code
    public static void main (String[] args) {
       // Given Input
    int arr[] = { 2, 4, 3 };
    int N = arr.length;
    int M = 5;

    // Function Call

        System.out.println(MaxSum(arr, N, M));
    }
}

// This code is contributed by potta lokesh.
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to maximize the sum after
# performing atmost one operation
def MaxSum(arr, n, M):
    # Variable to store the sum
    sum = 0

    # Traverse the array and modify arr[]
    for i in range(n):
        sum += arr[i]
        arr[i] = (M - 2 * arr[i])

    ans = 0
    mx = 0

    # Apply Kadane's algorithm
    for i in range(n):

        # Add a[i] to ans
        ans += arr[i]

        # If ans<0, modify the value
        # of ans as 0
        if (ans < 0):
            ans = 0

        # Update the value of mx
        mx = max(mx, ans)

    # Return the maximum sum
    return mx + sum

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [2, 4, 3]
    N = len(arr)
    M = 5

    # Function Call
    print(MaxSum(arr, N, M))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to maximize the sum after
    // performing atmost one operation
    static int MaxSum(int[] arr, int n, int M)
    {

        // Variable to store the sum
        int sum = 0;

        // Traverse the array and modify arr[]
        for (int i = 0; i < n; i++) {
            sum += arr[i];
            arr[i] = (M - 2 * arr[i]);
        }

        int ans = 0, mx = 0;

        // Apply Kadane's algorithm
        for (int i = 0; i < n; i++) {

            // Add a[i] to ans
            ans += arr[i];

            // If ans<0, modify the value
            // of ans as 0
            if (ans < 0)
                ans = 0;

            // Update the value of mx
            mx = Math.Max(mx, ans);
        }

        // Return the maximum sum
        return mx + sum;
    }

    // Driver Code
    public static void Main()
    {
        // Given Input
        int[] arr = { 2, 4, 3 };
        int N = arr.Length;
        int M = 5;

        // Function Call

        Console.WriteLine(MaxSum(arr, N, M));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        // Function to maximize the sum after
        // performing atmost one operation
        function MaxSum(arr, n, M) {
            // Variable to store the sum
            let sum = 0;

            // Traverse the array and modify arr[]
            for (let i = 0; i < n; i++) {
                sum += arr[i];
                arr[i] = (M - 2 * arr[i]);
            }

            let ans = 0, mx = 0;

            // Apply Kadane's algorithm
            for (let i = 0; i < n; i++) {
                // Add a[i] to ans
                ans += arr[i];

                // If ans<0, modify the value
                // of ans as 0
                if (ans < 0)
                    ans = 0;

                // Update the value of mx
                mx = Math.max(mx, ans);
            }

            // Return the maximum sum
            return mx + sum;
        }

        // Driver Code

        // Given Input
        let arr = [2, 4, 3];
        let N = arr.length;
        let M = 5;

        // Function Call
        document.write(MaxSum(arr, N, M));

    // This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
10
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)