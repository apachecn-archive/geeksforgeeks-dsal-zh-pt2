# 如果 K 大于

，通过交换 K 和 arr[i]来最小化给定数组的排序操作

> 原文:[https://www . geesforgeks . org/minimum-operations-to-sort-给定数组-通过交换-k-and-arri-if-k-大于/](https://www.geeksforgeeks.org/minimize-operations-to-sort-given-array-by-swapping-k-and-arri-if-k-is-greater/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **K** ，任务是找出[按非递减顺序](https://www.geeksforgeeks.org/find-the-non-decreasing-order-array-from-given-array/)对数组进行排序所需的最小操作数，以便在每个操作中，如果 **(arr[i] > K)** 的值为**的话，任何数组元素 **arr[i]** 都可以与 **K** 进行交换。**

**示例:**

> **输入:** arr[] = {0，2，3，5，4}，K = 1
> **输出:** 3
> **解释:**
> 给定的数组可以使用以下步骤排序:
> 
> 1.  对于 i = 1，由于 arr[1] > K，交换 arr[1]和 K 的值。因此，数组变成{0，1，3，5，4}，K = 2。
> 2.  对于 i = 2，由于 arr[2] > K，交换 arr[2]和 K 的值。因此，数组变成{0，1，2，5，4}，K = 3。
> 3.  对于 i = 3，由于 arr[3] > K，交换 arr[3]和 K 的值。因此，数组变成{0，1，2，3，4}，K = 5。
> 
> 在上述操作之后，给定的数组已经被排序。
> 
> **输入:** arr[] = {1，3，5，9，7}，K = 10
> T3】输出: -1

**方法:**给定的问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，其思想是对于范围**【0，N–1】**中的所有 **i** 在每一步最小化**arr【I】**的值，这是要排序的另一个数组的最佳选择。因此，如果 **arr[i] > K** ，[交换](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)的值 **arr[i]** 和 **K** 是最理想的选择。按照以下步骤解决给定的问题:

*   创建一个变量 **cnt** ，它存储所执行操作的计数。最初 **cnt = 0** 。
*   使用范围**【0，N-1】**中的变量 **i** 按照 **i** 的递增顺序遍历数组**arr【】**。
*   对于每个指标，如果 **arr[i] > K** ，则交换 **K** 和 **arr[i]** 的值，并将 **cnt** 的值增加 **1** 。
*   每次操作后，使用本文[中讨论的方法](https://www.geeksforgeeks.org/stdis_sorted-in-cpp/)检查数组 **arr[]** 是否排序。如果数组 **arr[]** 已排序，则返回 **cnt** 的值作为所需答案。
*   如果执行上述步骤后数组没有排序，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of given operations in order to sort
// the array arr[] in non-decreasing order
int minimumswaps(int arr[], int N, int K)
{
    // If arr[] is already sorted, return 0
    if (is_sorted(arr, arr + N)) {
        return 0;
    }

    // Stores the count of operations
    int cnt = 0;

    // Loop to iterate over the array
    for (int i = 0; i < N; i++) {

        // If arr[i] is greater than K,
        // minimuze the value of arr[i]
        if (arr[i] > K) {
            swap(arr[i], K);

            // Increment the count by 1
            cnt++;

            // Check if the array is sorted
            // after the last operation
            if (is_sorted(arr, arr + N)) {

                // Return answer
                return cnt;
            }
        }
    }

    // Not Possible to sort the array using
    // given operation, hence return -1
    return -1;
}

// Driver Code
int main()
{
    int arr[] = { 0, 2, 3, 5, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 1;

    cout << minimumswaps(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.io.*;
class GFG
{
    static boolean is_sorted(int arr[], int N)
    {
        for (int i = 0; i < N - 1; i++)
        {

            if (arr[i] > arr[i + 1])
                return false;
        }

        return true;
    }

    // Function to find the minimum number
    // of given operations in order to sort
    // the array arr[] in non-decreasing order
    static int minimumswaps(int arr[], int N, int K)
    {

        // If arr[] is already sorted, return 0
        if (is_sorted(arr, N)) {
            return 0;
        }

        // Stores the count of operations
        int cnt = 0;

        // Loop to iterate over the array
        for (int i = 0; i < N; i++) {

            // If arr[i] is greater than K,
            // minimuze the value of arr[i]
            if (arr[i] > K) {
                int temp = arr[i];
                  arr[i] = K;
                  K = temp;

                // Increment the count by 1
                cnt++;

                // Check if the array is sorted
                // after the last operation
                if (is_sorted(arr, N)) {

                    // Return answer
                    return cnt;
                }
            }
        }

        // Not Possible to sort the array using
        // given operation, hence return -1
        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 0, 2, 3, 5, 4 };
        int N = arr.length;
           int K = 1;

        System.out.println(minimumswaps(arr, N, K));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python 3 program of the above approach
def is_sort(arr):
    for i in range(len(arr)-1):
        if arr[i]>arr[i+1]:
            return False
    return True

# Function to find the minimum number
# of given operations in order to sort
# the array arr[] in non-decreasing order
def minimumswaps(arr, N, K):

    # If arr[] is already sorted, return 0
    if is_sort(arr):
        return 0

    # Stores the count of operations
    cnt = 0

    # Loop to iterate over the array
    for i in range(N):
        # If arr[i] is greater than K,
        # minimuze the value of arr[i]
        if(arr[i] > K):
            temp = arr[i]
            arr[i] = K
            K = temp

            # Increment the count by 1
            cnt += 1

            # Check if the array is sorted
            # after the last operation
            if is_sort(arr):
                # Return answer
                return cnt

    # Not Possible to sort the array using
    # given operation, hence return -1
    return -1

# Driver Code
if __name__ == '__main__':
    arr = [0, 2, 3, 5, 4]
    N = len(arr)
    K = 1
    print(minimumswaps(arr, N, K))

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program of the above approach
using System;
class GFG {
    static bool is_sorted(int[] arr, int N)
    {
        for (int i = 0; i < N - 1; i++) {

            if (arr[i] > arr[i + 1])
                return false;
        }

        return true;
    }

    // Function to find the minimum number
    // of given operations in order to sort
    // the array arr[] in non-decreasing order
    static int minimumswaps(int[] arr, int N, int K)
    {

        // If arr[] is already sorted, return 0
        if (is_sorted(arr, N)) {
            return 0;
        }

        // Stores the count of operations
        int cnt = 0;

        // Loop to iterate over the array
        for (int i = 0; i < N; i++) {

            // If arr[i] is greater than K,
            // minimuze the value of arr[i]
            if (arr[i] > K) {
                int temp = arr[i];
                arr[i] = K;
                K = temp;

                // Increment the count by 1
                cnt++;

                // Check if the array is sorted
                // after the last operation
                if (is_sorted(arr, N)) {

                    // Return answer
                    return cnt;
                }
            }
        }

        // Not Possible to sort the array using
        // given operation, hence return -1
        return -1;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 0, 2, 3, 5, 4 };
        int N = arr.Length;
        int K = 1;

        Console.WriteLine(minimumswaps(arr, N, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach
        function is_sorted(arr, N) {
            for (let i = 0; i < N - 1; i++) {

                if (arr[i] > arr[i + 1])
                    return false;
            }

            return true;
        }

        // Function to find the minimum number
        // of given operations in order to sort
        // the array arr[] in non-decreasing order
        function minimumswaps(arr, N, K)
        {

            // If arr[] is already sorted, return 0
            if (is_sorted(arr, N)) {
                return 0;
            }

            // Stores the count of operations
            let cnt = 0;

            // Loop to iterate over the array
            for (let i = 0; i < N; i++) {

                // If arr[i] is greater than K,
                // minimuze the value of arr[i]
                if (arr[i] > K) {
                    let temp = arr[i];
                    arr[i] = K;
                    K = temp;

                    // Increment the count by 1
                    cnt++;

                    // Check if the array is sorted
                    // after the last operation
                    if (is_sorted(arr, N)) {

                        // Return answer
                        return cnt;
                    }
                }
            }

            // Not Possible to sort the array using
            // given operation, hence return -1
            return -1;
        }

        // Driver Code
        let arr = [0, 2, 3, 5, 4];
        let N = arr.length;
        let K = 1;

        document.write(minimumswaps(arr, N, K));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*