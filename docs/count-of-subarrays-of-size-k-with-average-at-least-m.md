# K 大小的子阵列计数，平均值至少为 M

> 原文:[https://www . geeksforgeeks . org/k 大小的子阵列计数，平均值至少为-m/](https://www.geeksforgeeks.org/count-of-subarrays-of-size-k-with-average-at-least-m/)

给定一个由 **N** 个整数和两个正整数 **K** 和 **M** 组成的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出大小为 **K** 的子阵列数量，其[平均值](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)至少为**M**。

**示例:**

> **输入:** arr[] = {2，3，3，4，4，4，5，6，6}，K = 3，M = 4
> **输出:** 4
> **说明:**
> 以下是大小为 K(= 3)的子阵列，其平均值至少为 M(= 4)如下:
> 
> 1.  **arr[3，5]:** 平均值为 4，至少为 M(= 4)。
> 2.  **arr[4，6]:** 平均值为 4.33，至少为 M(= 4)。
> 3.  **arr[5，7]:** 平均值为 5，至少为 M(= 4)。
> 4.  **arr[6，8]:** 平均值为 5.66，至少为 M(= 4)。
> 
> 因此，子阵列的计数由 4 给出。
> 
> **输入:** arr[] = {3，6，3，2，1，3，9] K = 2，M = 4
> **输出:** 3

**方法:**给定的问题可以使用[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)和[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)来解决。按照以下步骤解决给定的问题:

*   初始化一个变量，比如说**计数**为 **0** ，存储所有可能的子阵列的计数。
*   初始化一个变量，将 **sum** 设为 **0** ，该变量存储大小为 **K** 的子阵列的元素之和。
*   [求第一个 **K** 数组元素](https://www.geeksforgeeks.org/find-maximum-minimum-sum-subarray-size-k/)的和，存储在变量 **sum** 中。如果**和**的值至少为**M * K**，则**计数**的值增加 **1** 。
*   [使用变量 **i** 在范围**【K，N–1】**内遍历给定数组 **arr[]**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) ，并执行以下步骤:
    *   将 **arr[i]** 的值加到变量**和**上，并从**和**中减去**arr[I–K]**的值。
    *   如果**和**的值至少为**M * K**，则**的值递增**1。
*   完成上述步骤后，打印**计数**的值作为子阵列的合成计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to count the subarrays of
// size K having average at least M
int countSubArrays(int arr[], int N,
                   int K, int M)
{
    // Stores the resultant count of
    // subarray
    int count = 0;

    // Stores the sum of subarrays of
    // size K
    int sum = 0;

    // Add the values of first K elements
    // to the sum
    for (int i = 0; i < K; i++) {
        sum += arr[i];
    }

    // Increment the count if the
    // current subarray is valid
    if (sum >= K * M)
        count++;

    // Traverse the given array
    for (int i = K; i < N; i++) {

        // Find the updated sum
        sum += (arr[i] - arr[i - K]);

        // Check if current subarray
        // is valid or not
        if (sum >= K * M)
            count++;
    }

    // Return the count of subarrays
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 3, 6, 3, 2, 1, 3, 9 };
    int K = 2, M = 4;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << countSubArrays(arr, N, K, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 3, 6, 3, 2, 1, 3, 9 };
        int K = 2, M = 4;
        System.out.println(countSubArrays(arr, K, M));
    }

    // Function to count the subarrays of
    // size K having average at least M
    public static int countSubArrays(int[] arr, int K,
                                     int M)
    {

        // Stores the resultant count of
        // subarray
        int count = 0;

        // Stores the sum of subarrays of
        // size K
        int sum = 0;

        // Add the values of first K elements
        // to the sum
        for (int i = 0; i < K; i++) {
            sum += arr[i];
        }

        // Increment the count if the
        // current subarray is valid
        if (sum >= K * M)
            count++;

        // Traverse the given array
        for (int i = K; i < arr.length; i++) {

            // Find the updated sum
            sum += (arr[i] - arr[i - K]);

            // Check if current subarray
            // is valid or not
            if (sum >= K * M)
                count++;
        }

        // Return the count of subarrays
        return count;
    }
}

// This code is contributed by Kdheeraj.
```

## 蟒蛇 3

```
# Python 3 code for the above approach

# Function to count the subarrays of
# size K having average at least M
def countSubArrays(arr, N, K, M):

    # Stores the resultant count of
    # subarray
    count = 0

    # Stores the sum of subarrays of
    # size K
    sum = 0

    # Add the values of first K elements
    # to the sum
    for i in range(K):
        sum += arr[i]

    # Increment the count if the
    # current subarray is valid
    if sum >= K*M:
        count += 1

    # Traverse the given array
    for i in range(K, N):

        # Find the updated sum
        sum += (arr[i] - arr[i - K])

        # Check if current subarray
        # is valid or not
        if sum >= K*M:
            count += 1

    # Return the count of subarrays
    return count

# Driver Code
if __name__ == '__main__':
    arr = [3, 6, 3, 2, 1, 3, 9]
    K = 2
    M = 4
    N = len(arr)
    count = countSubArrays(arr, N, K, M)
    print(count)

    # This code is contributed by Kdheeraj.
```

## C#

```
// C# program for the above approach

using System;

public class GFG
{

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 3, 6, 3, 2, 1, 3, 9 };
        int K = 2, M = 4;
        Console.WriteLine(countSubArrays(arr, K, M));
    }

    // Function to count the subarrays of
    // size K having average at least M
    public static int countSubArrays(int[] arr, int K,
                                     int M)
    {

        // Stores the resultant count of
        // subarray
        int count = 0;

        // Stores the sum of subarrays of
        // size K
        int sum = 0;

        // Add the values of first K elements
        // to the sum
        for (int i = 0; i < K; i++) {
            sum += arr[i];
        }

        // Increment the count if the
        // current subarray is valid
        if (sum >= K * M)
            count++;

        // Traverse the given array
        for (int i = K; i < arr.Length; i++) {

            // Find the updated sum
            sum += (arr[i] - arr[i - K]);

            // Check if current subarray
            // is valid or not
            if (sum >= K * M)
                count++;
        }

        // Return the count of subarrays
        return count;
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to count the subarrays of
       // size K having average at least M
       function countSubArrays(arr, N,
           K, M)
       {
           // Stores the resultant count of
           // subarray
           let count = 0;

           // Stores the sum of subarrays of
           // size K
           let sum = 0;

           // Add the values of first K elements
           // to the sum
           for (let i = 0; i < K; i++) {
               sum += arr[i];
           }

           // Increment the count if the
           // current subarray is valid
           if (sum >= K * M)
               count++;

           // Traverse the given array
           for (let i = K; i < N; i++) {

               // Find the updated sum
               sum += (arr[i] - arr[i - K]);

               // Check if current subarray
               // is valid or not
               if (sum >= K * M)
                   count++;
           }

           // Return the count of subarrays
           return count;
       }

       // Driver Code
       let arr = [3, 6, 3, 2, 1, 3, 9];
       let K = 2, M = 4;
       let N = arr.length;

       document.write(countSubArrays(arr, N, K, M));

    // This code is contributed by Potta Lokesh

   </script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)