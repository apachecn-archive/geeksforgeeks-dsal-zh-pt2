# 将每一个正元素的 K 个相邻元素递增 M 次后求数组和

> 原文:[https://www . geeksforgeeks . org/find-array-递增 k 后的和-每个正元素的相邻元素-m-times/](https://www.geeksforgeeks.org/find-array-sum-after-incrementing-by-k-adjacent-elements-of-every-positive-element-m-times/)

给定一个由 **N 个**整数和两个整数 **M** 和 **K** 组成的[圆形数组](https://www.geeksforgeeks.org/circular-array/)**arr【】**，任务是在执行 **M** 运算后[求数组元素的和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)**arr【】**，使得在每次运算中，所有正数组元素的相邻数组元素递增 **K** ，即如果

**示例:**

> **输入:** arr[] = {0，1，0，1，0，0}，M = 2，K = 1
> **输出:** 16
> **解释:**
> 在递增 arr[] > 0 的相邻数组元素后的第一次操作中，给定数组修改为 arr[] = {1，1，2，1，1，0}。
> 在递增 arr[] > 0 的相邻数组元素后的第二次操作中，给定数组修改为 arr[] = {2，3，4，3，2，2}。所以 arr[]的所有元素之和是 16。
> 
> **输入:** arr[] = {1，2，3}，M = 10，K = 2
> T3】输出: 126

**方法:**给定的问题可以基于以下观察来解决:

*   任何非零元素总是会在一次移动中使数组的和增加 **2 * K** 。
*   从 **0** 到非零值增加一个整数所需的移动次数始终等于最近的非零元素的距离。

按照以下步骤解决问题:

*   创建一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **步骤[]** ，存储当前元素到最近的非零元素的距离。
*   创建一个[函数](https://www.geeksforgeeks.org/functions-in-c/) **nearestLeft()** 来查找最近的非零元素的索引，同时使用本文[中讨论的方法在左侧遍历数组](https://www.geeksforgeeks.org/distance-closest-zero-every-element/)。
*   类似地，创建一个函数**nearethright()**来寻找最近的非零元素的索引，同时[以正确的方向遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   从 **0** 增加**I<sup>th</sup>T3】元素的值所需的操作次数由**步骤【I】**给出，之后，它将在每次操作后对最终总和贡献 **2 * K** 。因此 **i <sup>th</sup>** 整数在 **M** 运算后的最终和中的总贡献为**2 * K *(M–steps[I])**。**
*   [遍历**【1，N】**范围内的数组**arr【】**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并跟踪变量中每个指标贡献的和，比如**和**。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the nearest non-zero
// element in the left direction
void nearestLeft(int arr[], int N,
                 vector<int>& steps)
{
    // Stores the index of the first element
    // greater than 0 from the right side
    int L = -N;

    // Traverse the array in the range [1, N]
    for (int i = N - 1; i >= 0; i--) {
        // Check arr[i] is greater than 0
        if (arr[i] > 0) {
            // Update the value of L
            L = -(N - i);
            break;
        }
    }

    // Traverse the array from the left side
    for (int i = 0; i < N; i++) {
        // Check arr[i] is greater than 0
        if (arr[i] > 0) {
            // Update the value of L
            L = i;
        }

        // Update the value of steps[i]
        steps[i] = i - L;
    }
}

// Function to find the nearest non-zero
// element in the right direction
void nearestRight(int arr[], int N,
                  vector<int>& steps)
{
    // Stores the index of the first element
    // greater than 0 from the left side
    int R = 2 * N;

    // Traverse the array from the left side
    for (int i = 0; i < N; i++) {

        // Check arr[i] is greater than 0
        if (arr[i] > 0) {

            // Update the value of R
            R = N + i;
            break;
        }
    }

    // Traverse the array from the right side
    for (int i = N - 1; i >= 0; i--) {
        // Check arr[i] is greater than 0
        if (arr[i] > 0) {
            // Update the value of R
            R = i;
        }

        // Update the value of steps[i]
        steps[i] = min(steps[i], R - i);
    }
}

// Function to find the sum of the array
// after the given operation M times
int findSum(int arr[], int N, int M, int K)
{
    // Stores the distance of the nearest
    // non zero element.
    vector<int> steps(N);

    // Stores sum of the initial array arr[]
    int sum = accumulate(arr, arr + N, 0);

    if (sum == 0) {
        return 0;
    }

    nearestLeft(arr, N, steps);
    nearestRight(arr, N, steps);

    // Traverse the array from the left side
    for (int i = 0; i < N; i++)

        // Update the value of sum
        sum += 2 * K * max(0, M - steps[i]);

    // Print the total sum of the array
    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 0, 1, 0, 0 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = 2;
    int K = 1;

    cout << findSum(arr, N, M, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the nearest non-zero
// element in the left direction
static void nearestLeft(int arr[], int N,
                 int[] steps)
{

    // Stores the index of the first element
    // greater than 0 from the right side
    int L = -N;

    // Traverse the array in the range [1, N]
    for (int i = N - 1; i >= 0; i--)
    {

        // Check arr[i] is greater than 0
        if (arr[i] > 0)
        {

            // Update the value of L
            L = -(N - i);
            break;
        }
    }

    // Traverse the array from the left side
    for (int i = 0; i < N; i++)
    {

        // Check arr[i] is greater than 0
        if (arr[i] > 0)
        {

            // Update the value of L
            L = i;
        }

        // Update the value of steps[i]
        steps[i] = i - L;
    }
}

// Function to find the nearest non-zero
// element in the right direction
static void nearestRight(int arr[], int N,
                 int[] steps)
{

    // Stores the index of the first element
    // greater than 0 from the left side
    int R = 2 * N;

    // Traverse the array from the left side
    for (int i = 0; i < N; i++) {

        // Check arr[i] is greater than 0
        if (arr[i] > 0) {

            // Update the value of R
            R = N + i;
            break;
        }
    }

    // Traverse the array from the right side
    for (int i = N - 1; i >= 0; i--)
    {

        // Check arr[i] is greater than 0
        if (arr[i] > 0)
        {

            // Update the value of R
            R = i;
        }

        // Update the value of steps[i]
        steps[i] = Math.min(steps[i], R - i);
    }
}
static int accumulate(int[] arr, int start, int end){
    int sum = 0;
    for(int i= 0; i < arr.length; i++)
        sum += arr[i];
    return sum;
}

// Function to find the sum of the array
// after the given operation M times
static int findSum(int arr[], int N, int M, int K)
{

    // Stores the distance of the nearest
    // non zero element.
    int []steps = new int[N];

    // Stores sum of the initial array arr[]
    int sum = accumulate(arr, 0, N);

    if (sum == 0) {
        return 0;
    }

    nearestLeft(arr, N, steps);
    nearestRight(arr, N, steps);

    // Traverse the array from the left side
    for (int i = 0; i < N; i++)

        // Update the value of sum
        sum += 2 * K * Math.max(0, M - steps[i]);

    // Print the total sum of the array
    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 0, 1, 0, 1, 0, 0 };
    int N = arr.length;
    int M = 2;
    int K = 1;

    System.out.print(findSum(arr, N, M, K));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the nearest non-zero
# element in the left direction
def nearestLeft(arr, N, steps):

    # Stores the index of the first element
    # greater than 0 from the right side
    L = -N

    # Traverse the array in the range [1, N]
    for i in range(N - 1, -1, -1):

        # Check arr[i] is greater than 0
        if (arr[i] > 0):

            # Update the value of L
            L = -(N - i)
            break

    # Traverse the array from the left side
    for i in range(N):

        # Check arr[i] is greater than 0
        if (arr[i] > 0):

            # Update the value of L
            L = i

        # Update the value of steps[i]
        steps[i] = i - L

# Function to find the nearest non-zero
# element in the right direction
def nearestRight(arr, N, steps):

    # Stores the index of the first element
    # greater than 0 from the left side
    R = 2 * N

    # Traverse the array from the left side
    for i in range(N):

        # Check arr[i] is greater than 0
        if (arr[i] > 0):

            # Update the value of R
            R = N + i
            break

    # Traverse the array from the right side
    for i in range(N - 1, -1, -1):

        # Check arr[i] is greater than 0
        if (arr[i] > 0):

            # Update the value of R
            R = i

        # Update the value of steps[i]
        steps[i] = min(steps[i], R - i)

# Function to find the sum of the array
# after the given operation M times
def findSum(arr, N, M, K):

    # Stores the distance of the nearest
    # non zero element.
    steps = [0] * N

    # Stores sum of the initial array arr[]
    s = sum(arr)

    if (s == 0):
        return 0

    nearestLeft(arr, N, steps)
    nearestRight(arr, N, steps)

    # Traverse the array from the left side
    for i in range(N):

        # Update the value of sum
        s += 2 * K * max(0, M - steps[i])

    # Print the total sum of the array
    return s

# Driver Code
if __name__ == "__main__":

    arr = [ 0, 1, 0, 1, 0, 0 ]
    N = len(arr)
    M = 2
    K = 1

    print(findSum(arr, N, M, K))

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;
public class GFG{

// Function to find the nearest non-zero
// element in the left direction
static void nearestLeft(int []arr, int N,
                 int[] steps)
{

    // Stores the index of the first element
    // greater than 0 from the right side
    int L = -N;

    // Traverse the array in the range [1, N]
    for (int i = N - 1; i >= 0; i--)
    {

        // Check arr[i] is greater than 0
        if (arr[i] > 0)
        {

            // Update the value of L
            L = -(N - i);
            break;
        }
    }

    // Traverse the array from the left side
    for (int i = 0; i < N; i++)
    {

        // Check arr[i] is greater than 0
        if (arr[i] > 0)
        {

            // Update the value of L
            L = i;
        }

        // Update the value of steps[i]
        steps[i] = i - L;
    }
}

// Function to find the nearest non-zero
// element in the right direction
static void nearestRight(int []arr, int N,
                 int[] steps)
{

    // Stores the index of the first element
    // greater than 0 from the left side
    int R = 2 * N;

    // Traverse the array from the left side
    for (int i = 0; i < N; i++) {

        // Check arr[i] is greater than 0
        if (arr[i] > 0) {

            // Update the value of R
            R = N + i;
            break;
        }
    }

    // Traverse the array from the right side
    for (int i = N - 1; i >= 0; i--)
    {

        // Check arr[i] is greater than 0
        if (arr[i] > 0)
        {

            // Update the value of R
            R = i;
        }

        // Update the value of steps[i]
        steps[i] = Math.Min(steps[i], R - i);
    }
}
static int accumulate(int[] arr, int start, int end){
    int sum = 0;
    for(int i= 0; i < arr.Length; i++)
        sum += arr[i];
    return sum;
}

// Function to find the sum of the array
// after the given operation M times
static int findSum(int []arr, int N, int M, int K)
{

    // Stores the distance of the nearest
    // non zero element.
    int []steps = new int[N];

    // Stores sum of the initial array []arr
    int sum = accumulate(arr, 0, N);

    if (sum == 0) {
        return 0;
    }

    nearestLeft(arr, N, steps);
    nearestRight(arr, N, steps);

    // Traverse the array from the left side
    for (int i = 0; i < N; i++)

        // Update the value of sum
        sum += 2 * K * Math.Max(0, M - steps[i]);

    // Print the total sum of the array
    return sum;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 0, 1, 0, 1, 0, 0 };
    int N = arr.Length;
    int M = 2;
    int K = 1;

    Console.Write(findSum(arr, N, M, K));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the nearest non-zero
        // element in the left direction
        function nearestLeft(arr, N,
            steps)
        {

            // Stores the index of the first element
            // greater than 0 from the right side
            let L = -N;

            // Traverse the array in the range [1, N]
            for (let i = N - 1; i >= 0; i--)
            {

                // Check arr[i] is greater than 0
                if (arr[i] > 0)
                {

                    // Update the value of L
                    L = -(N - i);
                    break;
                }
            }

            // Traverse the array from the left side
            for (let i = 0; i < N; i++)
            {

                // Check arr[i] is greater than 0
                if (arr[i] > 0)
                {

                    // Update the value of L
                    L = i;
                }

                // Update the value of steps[i]
                steps[i] = i - L;
            }
        }

        // Function to find the nearest non-zero
        // element in the right direction
        function nearestRight(arr, N,
            steps)
        {

            // Stores the index of the first element
            // greater than 0 from the left side
            let R = 2 * N;

            // Traverse the array from the left side
            for (let i = 0; i < N; i++) {

                // Check arr[i] is greater than 0
                if (arr[i] > 0) {

                    // Update the value of R
                    R = N + i;
                    break;
                }
            }

            // Traverse the array from the right side
            for (let i = N - 1; i >= 0; i--)
            {

                // Check arr[i] is greater than 0
                if (arr[i] > 0)
                {

                    // Update the value of R
                    R = i;
                }

                // Update the value of steps[i]
                steps[i] = Math.min(steps[i], R - i);
            }
        }

        // Function to find the sum of the array
        // after the given operation M times
        function findSum(arr, N, M, K)
        {

            // Stores the distance of the nearest
            // non zero element.
            let steps = new Array(N);

            // Stores sum of the initial array arr[]
            let sum = 0;
            for (let i = 0; i < N; i++) {
                sum = sum + arr[i];
            }

            if (sum == 0) {
                return 0;
            }

            nearestLeft(arr, N, steps);
            nearestRight(arr, N, steps);

            // Traverse the array from the left side
            for (let i = 0; i < N; i++)

                // Update the value of sum
                sum += 2 * K * Math.max(0, M - steps[i]);

            // Print the total sum of the array
            return sum;
        }

        // Driver Code
        let arr = [0, 1, 0, 1, 0, 0];
        let N = arr.length;
        let M = 2;
        let K = 1;

        document.write(findSum(arr, N, M, K));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
16
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)