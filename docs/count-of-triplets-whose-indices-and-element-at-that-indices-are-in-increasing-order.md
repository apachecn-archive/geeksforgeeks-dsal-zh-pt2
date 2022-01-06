# 索引和索引处元素按递增顺序排列的三元组计数

> 原文:[https://www . geeksforgeeks . org/三胞胎计数——其索引和索引处的元素按递增顺序排列/](https://www.geeksforgeeks.org/count-of-triplets-whose-indices-and-element-at-that-indices-are-in-increasing-order/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出索引和该索引处的元素按递增顺序排列的三元组的数量。

**示例:**

> **输入:** arr[] = {1，2，4，3}
> **输出:** 2
> **解释:**给定数组中有两个可能的三元组，元素按递增顺序排列，即{1，2，4}和{1，2，3}。
> 
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 10

**天真方法:**给定的问题可以通过迭代给定数组的所有可能的三元组 **(i，j，k)** 并跟踪其索引和该索引处的元素按递增顺序排列的三元组的数量来解决。检查所有三胞胎后，打印获得的三胞胎总数。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法还可以通过以下观察进行优化:对于任何给定的索引 I，以 arr[i]作为中间元素的三元组的数量将是在*范围[1，I–1]*内小于 arr[i]的整数的*计数。*以下是使用上述观察结果解决给定问题的步骤:*

*   初始化一个变量， **totalCount** 为 0，存储有效三元组的计数。
*   使用变量 **i** 在范围**【1，N–2】**内迭代数组 **arr[]** ，并执行以下步骤:
    *   计算在范围**【0，I–1】**内小于**arr【I】**的值的数量，并将该值存储在变量 **K1** 中。
    *   计算在范围**【I+1，N-1】**内大于**arr【I】**的数值，并将该数值存储在变量 **K2** 中。
    *   将 **K1*K2** 的值加到**总数**中。
*   存储在 **totalCount** 中的值是必需的答案。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find number of integers
// smaller than value in range [0, N]
int countSmaller(int arr[], int N, int value)
{
    // Stores the count of integers
    int count = 0;

    // Iterate the given array
    for (int i = 0; i < N; i++) {
        if (arr[i] < value)
            count++;
    }

    // Return total count
    return count;
}

// Function to find number of integers
// greater than value in range [i, N]
int countLarger(int arr[], int i, int N,
                int value)
{
    // Stores the count of integers
    int count = 0;

    // Iterate the given array
    while (i < N) {
        if (arr[i] > value)
            count++;
        i++;
    }

    // Return total count
    return count;
}

// Function to find the count of triplets
// whose indices and elements at that indices
// are also in increasing order
int countTriplets(int arr[], int N)
{
    // Stores the count of valid triplets
    int totalCount = 0;

    // Loop to iterate over the array
    for (int i = 1; i < N - 1; i++) {

        // Count of smaller elements than
        // arr[i] in range [0, i-1]
        int K1 = countSmaller(arr, i,
                              arr[i]);

        // Count of greater elements than
        // arr[i] in range [i+1, N]
        int K2 = countLarger(arr, i + 1,
                             N, arr[i]);

        // Add to total count
        totalCount += K1 * K2;
    }

    // Return Answer
    return totalCount;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << countTriplets(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.io.*;

class GFG {

    // Function to find number of integers
    // smaller than value in range [0, N]
    static int countSmaller(int arr[], int N, int value)
    {

        // Stores the count of integers
        int count = 0;

        // Iterate the given array
        for (int i = 0; i < N; i++) {
            if (arr[i] < value)
                count++;
        }

        // Return total count
        return count;
    }

    // Function to find number of integers
    // greater than value in range [i, N]
    static int countLarger(int arr[], int i, int N,
                           int value)
    {
        // Stores the count of integers
        int count = 0;

        // Iterate the given array
        while (i < N) {
            if (arr[i] > value)
                count++;
            i++;
        }

        // Return total count
        return count;
    }

    // Function to find the count of triplets
    // whose indices and elements at that indices
    // are also in increasing order
    static int countTriplets(int arr[], int N)
    {
        // Stores the count of valid triplets
        int totalCount = 0;

        // Loop to iterate over the array
        for (int i = 1; i < N - 1; i++) {

            // Count of smaller elements than
            // arr[i] in range [0, i-1]
            int K1 = countSmaller(arr, i, arr[i]);

            // Count of greater elements than
            // arr[i] in range [i+1, N]
            int K2 = countLarger(arr, i + 1, N, arr[i]);

            // Add to total count
            totalCount += K1 * K2;
        }

        // Return Answer
        return totalCount;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5 };
        int N = arr.length;

        System.out.println(countTriplets(arr, N));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python program of the above approach
# Function to find number of integers
# smaller than value in range [0, N]
def countSmaller(arr, N, value):

    # Stores the count of integers
    count = 0

    # Iterate the given array
    for i in range (N):
        if (arr[i] < value):
            count += 1

    # Return total count
    return count

# Function to find number of integers
# greater than value in range [i, N]
def countLarger( arr, i, N, value):

    # Stores the count of integers
    count = 0

    # Iterate the given array
    while (i < N):
        if (arr[i] > value):
            count += 1
        i += 1

    # Return total count
    return count

# Function to find the count of triplets
# whose indices and elements at that indices
# are also in increasing order
def countTriplets( arr,  N):

    # Stores the count of valid triplets
    totalCount = 0

    # Loop to iterate over the array
    for i in range(0, N - 1):

        # Count of smaller elements than
        # arr[i] in range [0, i-1]
        K1 = countSmaller(arr, i, arr[i])

        # Count of greater elements than
        # arr[i] in range [i+1, N]
        K2 = countLarger(arr, i + 1, N, arr[i])

        # Add to total count
        totalCount += K1 * K2

    # Return Answer
    return totalCount

# Driver Code
arr = [ 1, 2, 3, 4, 5 ];
N = len(arr)
print(countTriplets(arr, N))

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program of the above approach
using System;

class GFG {

    // Function to find number of integers
    // smaller than value in range [0, N]
    static int countSmaller(int[] arr, int N, int value)
    {

        // Stores the count of integers
        int count = 0;

        // Iterate the given array
        for (int i = 0; i < N; i++) {
            if (arr[i] < value)
                count++;
        }

        // Return total count
        return count;
    }

    // Function to find number of integers
    // greater than value in range [i, N]
    static int countLarger(int[] arr, int i, int N,
                           int value)
    {
        // Stores the count of integers
        int count = 0;

        // Iterate the given array
        while (i < N) {
            if (arr[i] > value)
                count++;
            i++;
        }

        // Return total count
        return count;
    }

    // Function to find the count of triplets
    // whose indices and elements at that indices
    // are also in increasing order
    static int countTriplets(int[] arr, int N)
    {
        // Stores the count of valid triplets
        int totalCount = 0;

        // Loop to iterate over the array
        for (int i = 1; i < N - 1; i++) {

            // Count of smaller elements than
            // arr[i] in range [0, i-1]
            int K1 = countSmaller(arr, i, arr[i]);

            // Count of greater elements than
            // arr[i] in range [i+1, N]
            int K2 = countLarger(arr, i + 1, N, arr[i]);

            // Add to total count
            totalCount += K1 * K2;
        }

        // Return Answer
        return totalCount;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 1, 2, 3, 4, 5 };
        int N = arr.Length;

        Console.WriteLine(countTriplets(arr, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find number of integers
        // smaller than value in range [0, N]
        function countSmaller(arr, N, value)
        {

            // Stores the count of integers
            let count = 0;

            // Iterate the given array
            for (let i = 0; i < N; i++) {
                if (arr[i] < value)
                    count++;
            }

            // Return total count
            return count;
        }

        // Function to find number of integers
        // greater than value in range [i, N]
        function countLarger(arr, i, N,
            value) {
            // Stores the count of integers
            let count = 0;

            // Iterate the given array
            while (i < N) {
                if (arr[i] > value)
                    count++;
                i++;
            }

            // Return total count
            return count;
        }

        // Function to find the count of triplets
        // whose indices and elements at that indices
        // are also in increasing order
        function countTriplets(arr, N) {
            // Stores the count of valid triplets
            let totalCount = 0;

            // Loop to iterate over the array
            for (let i = 1; i < N - 1; i++) {

                // Count of smaller elements than
                // arr[i] in range [0, i-1]
                let K1 = countSmaller(arr, i,
                    arr[i]);

                // Count of greater elements than
                // arr[i] in range [i+1, N]
                let K2 = countLarger(arr, i + 1,
                    N, arr[i]);

                // Add to total count
                totalCount += K1 * K2;
            }

            // Return Answer
            return totalCount;
        }

        // Driver Code

        let arr = [1, 2, 3, 4, 5];
        let N = arr.length;
        document.write(countTriplets(arr, N));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
10
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*