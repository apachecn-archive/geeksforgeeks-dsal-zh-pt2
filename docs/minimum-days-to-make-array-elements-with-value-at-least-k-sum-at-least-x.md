# 使值至少为 K 的数组元素总和至少为 X 的最短天数

> 原文:[https://www . geeksforgeeks . org/最少天数-用至少-k-sum-至少-x/](https://www.geeksforgeeks.org/minimum-days-to-make-array-elements-with-value-at-least-k-sum-at-least-x/) 值制作数组元素

给定两个整数 **X** 、 **K** ，以及两个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和**R【】**均由 **N** 正整数组成，其中 **R[i]** 表示 **arr[i]** 在一天内增加的量，任务是找出最小天数，在此之后数组元素的[和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)的值大于或等于

**示例:**

> **输入:** X = 100，K = 45，arr[] = {2，5，2，6}，R[] = {10，13，15，12}
> **输出:** 4
> **解释:**
> 每天后考虑数组的以下值:
> 
> 1.  **第 1 天:**第 1 天之后，所有数组元素修改为{12，18，17，18}。具有值> = K(= 45)的元素之和为 0。
> 2.  **第 2 天:**第 2 天之后，所有数组元素修改为{22，31，32，30}。具有值> = K(= 45)的元素之和为 0。
> 3.  **第 3 天:**第 3 天之后，所有数组元素修改为{32，44，47，42}。具有值> = K(= 45)的元素之和为 47。
> 4.  **第 4 天:**第 4 天之后，所有数组元素修改为{42，57，62，54}。具有值> = K(= 45)的元素之和为 57 + 62 + 54 = 167，至少为 X(= 100)。
> 
> 因此，所需的最小天数为 4 天。
> 
> **输入:** X = 65，K = 10，arr[] = {1，1，1，1，3}，R[] = {2，1，2，2，1}
> 输出: 9

**天真方法:**解决给定问题的最简单方法是不断增加天数，并且每当具有至少为 K 的值**的数组元素的[和大于或等于 **X** 时。递增 **D** 天后，打印当前获得的天数值。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)**

***时间复杂度:** O(N*X)*
***辅助空间:** O(1)*

**高效途径:**上述途径也可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)进行优化。按照以下步骤解决问题:

*   初始化两个变量，说**低**为 **0** 和**高**为 **X** 。
*   初始化一个变量，比如说 **minDays** 存储最小天数。
*   [迭代直到](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)的值**低**最多**高**并执行以下步骤:
    *   将一个变量**中的**初始化为**低+(高–低)/2** 和变量，将**和**设为 **0** ，在**中的**天数后存储数组元素的[和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)。
    *   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr[]** ，并执行以下步骤:
        *   将变量**温度**初始化为 **(arr[i] + R[i]*mid)** 。
        *   如果**温度**的值不小于 **K** 将**温度**的值加到**和**上。
    *   如果**和**的值至少为**X**，那么将**的值更新为**到**中间**，将**高的值更新为**到**(中间–1)**。
    *   否则，将**低值**更新为**(中+ 1)** 。
*   完成上述步骤后，打印 **minDays** 的值作为最终的最小天数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of days such that the sum of array
// elements >= K is at least X
void findMinDays(int arr[], int R[],
                 int N, int X, int K)
{
    // Initialize the boundaries of
    // search space
    int low = 0, high = X;
    int minDays;

    // Perform the binary search
    while (low <= high) {

        // Find the value of mid
        int mid = (low + high) / 2;

        int sum = 0;

        // Traverse the array, arr[]
        for (int i = 0; i < N; i++) {

            // Find the value of arr[i]
            // after mid number of days
            int temp = arr[i] + R[i] * mid;

            // Check if temp is not
            // less than K
            if (temp >= K) {

                // Update the value
                // of sum
                sum += temp;
            }
        }

        // Check if the value of sum
        // is greater than X
        if (sum >= X) {

            // Update value of high
            minDays = mid;
            high = mid - 1;
        }

        // Update the value of low
        else {
            low = mid + 1;
        }
    }

    // Print the minimum number
    // of days
    cout << minDays;
}

// Driver Code
int main()
{
    int X = 100, K = 45;
    int arr[] = { 2, 5, 2, 6 };
    int R[] = { 10, 13, 15, 12 };
    int N = sizeof(arr) / sizeof(arr[0]);
    findMinDays(arr, R, N, X, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the minimum number
// of days such that the sum of array
// elements >= K is at least X
static void findMinDays(int arr[], int R[], int N,
                        int X, int K)
{

    // Initialize the boundaries of
    // search space
    int low = 0, high = X;
    int minDays = -1;

    // Perform the binary search
    while (low <= high)
    {

        // Find the value of mid
        int mid = (low + high) / 2;

        int sum = 0;

        // Traverse the array, arr[]
        for(int i = 0; i < N; i++)
        {

            // Find the value of arr[i]
            // after mid number of days
            int temp = arr[i] + R[i] * mid;

            // Check if temp is not
            // less than K
            if (temp >= K)
            {

                // Update the value
                // of sum
                sum += temp;
            }
        }

        // Check if the value of sum
        // is greater than X
        if (sum >= X)
        {

            // Update value of high
            minDays = mid;
            high = mid - 1;
        }

        // Update the value of low
        else
        {
            low = mid + 1;
        }
    }

    // Print the minimum number
    // of days
    System.out.println(minDays);
}

// Driver Code
public static void main(String[] args)
{
    int X = 100, K = 45;
    int arr[] = { 2, 5, 2, 6 };
    int R[] = { 10, 13, 15, 12 };
    int N = arr.length;

    findMinDays(arr, R, N, X, K);
}
}

// This code is contributed by Potta Lokesh
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the minimum number
    // of days such that the sum of array
    // elements >= K is at least X
    static void findMinDays(int[] arr, int[] R, int N,
                            int X, int K)
    {

        // Initialize the boundaries of
        // search space
        int low = 0, high = X;
        int minDays = -1;

        // Perform the binary search
        while (low <= high) {

            // Find the value of mid
            int mid = (low + high) / 2;

            int sum = 0;

            // Traverse the array, arr[]
            for (int i = 0; i < N; i++) {

                // Find the value of arr[i]
                // after mid number of days
                int temp = arr[i] + R[i] * mid;

                // Check if temp is not
                // less than K
                if (temp >= K) {

                    // Update the value
                    // of sum
                    sum += temp;
                }
            }

            // Check if the value of sum
            // is greater than X
            if (sum >= X) {

                // Update value of high
                minDays = mid;
                high = mid - 1;
            }

            // Update the value of low
            else {
                low = mid + 1;
            }
        }

        // Print the minimum number
        // of days
        Console.Write(minDays);
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int X = 100, K = 45;
        int[] arr = { 2, 5, 2, 6 };
        int[] R = { 10, 13, 15, 12 };
        int N = arr.Length;

        findMinDays(arr, R, N, X, K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum number
// of days such that the sum of array
// elements >= K is at least X
function findMinDays(arr, R, N, X, K) {
    // Initialize the boundaries of
    // search space
    let low = 0, high = X;
    let minDays;

    // Perform the binary search
    while (low <= high) {

        // Find the value of mid
        let mid = Math.floor((low + high) / 2);

        let sum = 0;

        // Traverse the array, arr[]
        for (let i = 0; i < N; i++) {

            // Find the value of arr[i]
            // after mid number of days
            let temp = arr[i] + R[i] * mid;

            // Check if temp is not
            // less than K
            if (temp >= K) {

                // Update the value
                // of sum
                sum += temp;
            }
        }

        // Check if the value of sum
        // is greater than X
        if (sum >= X) {

            // Update value of high
            minDays = mid;
            high = mid - 1;
        }

        // Update the value of low
        else {
            low = mid + 1;
        }
    }

    // Print the minimum number
    // of days
    document.write(minDays);
}

// Driver Code
let X = 100, K = 45;
let arr = [2, 5, 2, 6];
let R = [10, 13, 15, 12];
let N = arr.length
findMinDays(arr, R, N, X, K);

// This code is contributed by _saurabh_jaiswal.
</script>
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the minimum number
# of days such that the sum of array
# elements >= K is at least X
def findMinDays(arr, R, N, X, K):

    # Initialize the boundaries of
    # search space
    low = 0
    high = X
    minDays = 0

    # Perform the binary search
    while (low <= high):
        # Find the value of mid
        mid = (low + high) // 2

        sum = 0

        # Traverse the array, arr[]
        for i in range(N):
            # Find the value of arr[i]
            # after mid number of days
            temp = arr[i] + R[i] * mid

            # Check if temp is not
            # less than K
            if (temp >= K):
                # Update the value
                # of sum
                sum += temp

        # Check if the value of sum
        # is greater than X
        if (sum >= X):

            # Update value of high
            minDays = mid
            high = mid - 1

        # Update the value of low
        else:
            low = mid + 1

    # Print the minimum number
    # of days
    print(minDays)

# Driver Code
if __name__ == '__main__':
    X = 100
    K = 45
    arr = [2, 5, 2, 6]
    R = [10, 13, 15, 12]
    N = len(arr)
    findMinDays(arr, R, N, X, K)

    # This code is contributed by SURENDRA_GANGWAR.
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log X)*
***辅助空间:** O(1)*