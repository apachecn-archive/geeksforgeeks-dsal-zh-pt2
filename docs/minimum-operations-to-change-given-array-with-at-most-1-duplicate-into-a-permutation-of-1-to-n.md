# 将最多 1 个副本的给定数组变成 1 到 N 的排列的最小操作

> 原文:[https://www . geeksforgeeks . org/最少操作-更改-给定-最多 1 个数组-复制到 1 到 n 的排列中/](https://www.geeksforgeeks.org/minimum-operations-to-change-given-array-with-at-most-1-duplicate-into-a-permutation-of-1-to-n/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**的 **N** 个整数在**【1，N】**的范围内，最多有一个重复的元素，任务是找到使给定数组成为从 **1** 到 **N** 的数字排列所需的最小增量或减量操作数。

**示例:**

> **输入:** arr[] = {1，2，5，3，2}
> **输出:** 2
> **解释:**给定数组两次包含 2，数组中缺少 4。因此，可以使用两个增量操作将 2 变成 4，这是最小可能的。
> 
> **输入:** arr[] = {1，2，5，3，4}
> **输出:** 0
> **解释:**给定的数组已经代表了 1 到 5 的整数排列。

**天真方法:**给定的问题可以简单地通过[找到给定数组中的重复元素](https://www.geeksforgeeks.org/find-duplicates-in-on-time-and-constant-extra-space/)和缺失元素来解决。这可以通过[对给定数组](https://www.geeksforgeeks.org/sorting-algorithms/)进行排序并检查重复和缺失的元素来轻松完成。

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*

**有效方法:**给定的问题可以通过一个简单的观察来解决，即 **N** 个整数的排列的所有元素的和总是等于 **N*(N+1)/ 2** 。因此，所需操作的数量可以简单地通过公式| **数组元素的总和–N *(N+1)/2)|**来计算。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of
// increment/decrement operations to change
// the given array into a permutation
int minCost(int arr[], int N)
{
    // Stores the sum of array elements
    int sumOfArray = 0;

    // Loop to iterate through the array
    for (int i = 0; i < N; i++) {
        sumOfArray += arr[i];
    }

    // Finding sum of first
    // N natural numbers
    int sumOfN = N * (N + 1) / 2;

    // Find the absolute difference
    int diff = sumOfArray - sumOfN;
    diff = diff < 0 ? -1 * diff : diff;

    // Return Answer
    return diff;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 5, 3, 2 };
    int n = sizeof(arr) / sizeof(int);

    cout << minCost(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach

public class GFG {

    // Function to find the minimum number of
    // increment/decrement operations to change
    // the given array into a permutation
    static int minCost(int []arr, int N)
    {
        // Stores the sum of array elements
        int sumOfArray = 0;

        // Loop to iterate through the array
        for (int i = 0; i < N; i++) {
            sumOfArray += arr[i];
        }

        // Finding sum of first
        // N natural numbers
        int sumOfN = N * (N + 1) / 2;

        // Find the absolute difference
        int diff = sumOfArray - sumOfN;
        diff = diff < 0 ? -1 * diff : diff;

        // Return Answer
        return diff;
    }

    // Driver code
    public static void main (String[] args) {

        int arr[] = { 1, 2, 5, 3, 2 };
        int n = arr.length;

        System.out.println(minCost(arr, n));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# python program of the above approach

# Function to find the minimum number of
# increment/decrement operations to change
# the given array into a permutation
def minCost(arr, N):

    # Stores the sum of array elements
    sumOfArray = 0

    # Loop to iterate through the array
    for i in range(0, N):
        sumOfArray += arr[i]

        # Finding sum of first
        # N natural numbers
    sumOfN = N * (N + 1) // 2

    # Find the absolute difference
    diff = sumOfArray - sumOfN
    if diff < 0:
        diff = -1 * diff

        # Return Answer
    return diff

# Driver code
if __name__ == "__main__":

    arr = [1, 2, 5, 3, 2]
    n = len(arr)

    print(minCost(arr, n))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program of the above approach
using System;
class GFG {

    // Function to find the minimum number of
    // increment/decrement operations to change
    // the given array into a permutation
    static int minCost(int []arr, int N)
    {
        // Stores the sum of array elements
        int sumOfArray = 0;

        // Loop to iterate through the array
        for (int i = 0; i < N; i++) {
            sumOfArray += arr[i];
        }

        // Finding sum of first
        // N natural numbers
        int sumOfN = N * (N + 1) / 2;

        // Find the absolute difference
        int diff = sumOfArray - sumOfN;
        diff = diff < 0 ? -1 * diff : diff;

        // Return Answer
        return diff;
    }

    // Driver code
    public static void Main () {

        int []arr = { 1, 2, 5, 3, 2 };
        int n = arr.Length;

        Console.Write(minCost(arr, n));
    }
}
// This code is contributed by Samim Hossain Mondal
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum number of
        // increment/decrement operations to change
        // the given array into a permutation
        function minCost(arr, N)
        {

            // Stores the sum of array elements
            let sumOfArray = 0;

            // Loop to iterate through the array
            for (let i = 0; i < N; i++) {
                sumOfArray += arr[i];
            }

            // Finding sum of first
            // N natural numbers
            let sumOfN = N * (N + 1) / 2;

            // Find the absolute difference
            let diff = sumOfArray - sumOfN;
            diff = diff < 0 ? -1 * diff : diff;

            // Return Answer
            return diff;
        }

        // Driver code
        let arr = [1, 2, 5, 3, 2];
        let n = arr.length;

        document.write(minCost(arr, n));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)