# 在数组上做 K 加法运算后最大化中位数

> 原文:[https://www . geeksforgeeks . org/maximum-do-k-加法-数组运算后的中值/](https://www.geeksforgeeks.org/maximize-median-after-doing-k-addition-operation-on-the-array/)

给定一个由 **N** 元素组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **K，**的任务是在数组上最多执行 **K** 操作。在一个操作中，将数组中的任何元素递增一。做 **K** 这样的操作后找到最大化中位数。

**示例:**

> **输入:** arr[] = {1，3，4，5}，K = 3
> **输出:** 5
> **解释:**这里我们在第二个元素中加两个，在第三个元素中加一个，然后我们会得到一个最大的中值。k 次运算后，数组可以变成{1，5，5，5}。所以我们能做的最大中位数是(5 + 5 ) / 2 = 5，因为这里 N 是偶数。
> 
> **输入:** arr[] **=** {1，3，6，4，2}，K = 10
> **输出:** 7

**进场:**

1.  [按递增顺序排序](https://www.geeksforgeeks.org/sorting-algorithms/)数组。
2.  由于中位数是数组的中间元素，在左半部分进行运算，因此它将毫无价值，因为它不会增加中位数。
3.  执行后半部分的操作，并开始执行从**n/2**元素到结束的操作。
4.  如果 **N** 为偶数，则从 **n/2** 元素开始操作至结束。
5.  在执行 **K** 操作后，使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)我们将检查是否有任何数字可能作为中间值。
6.  如果中间值是可能的，那么我们将检查下一个大于当前计算的中间值的数字。否则，中值的最后一个可能值就是要求的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check operation can be
// perform or not
bool possible(int arr[], int N,
              int mid, int K)
{

    int add = 0;

    for (int i = N / 2 - (N + 1) % 2;
         i < N; ++i) {

        if (mid - arr[i] > 0) {

            // Number of operation to
            // perform s.t. mid is median
            add += (mid - arr[i]);

            if (add > K)
                return false;
        }
    }

    // If mid is median of the array
    if (add <= K)
        return true;
    else
        return false;
}

// Function to find max median
// of the array
int findMaxMedian(int arr[], int N,
                  int K)
{

    // Lowest possible median
    int low = 1;
    int mx = 0;

    for (int i = 0; i < N; ++i) {
        mx = max(mx, arr[i]);
    }

    // Highest possible median
    long long int high = K + mx;

    while (low <= high) {

        int mid = (high + low) / 2;

        // Checking for mid is possible
        // for the median of array after
        // doing at most k operation
        if (possible(arr, N, mid, K)) {
            low = mid + 1;
        }

        else {
            high = mid - 1;
        }
    }

    if (N % 2 == 0) {

        if (low - 1 < arr[N / 2]) {
            return (arr[N / 2] + low - 1) / 2;
        }
    }

    // Return the max possible ans
    return low - 1;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 3, 6 };

    // Given number of operation
    int K = 10;

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Sort the array
    sort(arr, arr + N);

    // Function call
    cout << findMaxMedian(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check operation can be
// perform or not
static boolean possible(int arr[], int N,
                        int mid, int K)
{
    int add = 0;

    for(int i = N / 2 - (N + 1) % 2;
            i < N; ++i)
    {
        if (mid - arr[i] > 0)
        {

            // Number of operation to
            // perform s.t. mid is median
            add += (mid - arr[i]);

            if (add > K)
                return false;
        }
    }

    // If mid is median of the array
    if (add <= K)
        return true;
    else
        return false;
}

// Function to find max median
// of the array
static int findMaxMedian(int arr[], int N,
                                    int K)
{

    // Lowest possible median
    int low = 1;
    int mx = 0;

    for(int i = 0; i < N; ++i)
    {
        mx = Math.max(mx, arr[i]);
    }

    // Highest possible median
    int high = K + mx;

    while (low <= high)
    {
        int mid = (high + low) / 2;

        // Checking for mid is possible
        // for the median of array after
        // doing at most k operation
        if (possible(arr, N, mid, K))
        {
            low = mid + 1;
        }

        else
        {
            high = mid - 1;
        }
    }

    if (N % 2 == 0)
    {
        if (low - 1 < arr[N / 2])
        {
            return (arr[N / 2] + low - 1) / 2;
        }
    }

    // Return the max possible ans
    return low - 1;
}

// Driver code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 1, 3, 6 };

    // Given number of operation
    int K = 10;

    // Size of array
    int N = arr.length;

    // Sort the array
    Arrays.sort(arr);

    // Function call
    System.out.println(findMaxMedian(arr, N, K));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check operation can be
# perform or not
def possible(arr, N, mid, K):

    add = 0

    for i in range(N // 2 - (N + 1) % 2, N):

        if (mid - arr[i] > 0):

            # Number of operation to
            # perform s.t. mid is median
            add += (mid - arr[i])

            if (add > K):
                return False

    # If mid is median of the array
    if (add <= K):
        return True
    else:
        return False

# Function to find max median
# of the array
def findMaxMedian(arr, N,K):

    # Lowest possible median
    low = 1
    mx = 0

    for i in range(N):
        mx = max(mx, arr[i])

    # Highest possible median
    high = K + mx

    while (low <= high):

        mid = (high + low) // 2

        # Checking for mid is possible
        # for the median of array after
        # doing at most k operation
        if (possible(arr, N, mid, K)):
            low = mid + 1
        else :
            high = mid - 1

    if (N % 2 == 0):

        if (low - 1 < arr[N // 2]):
            return (arr[N // 2] + low - 1) // 2

    # Return the max possible ans
    return low - 1

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [1, 3, 6]

    # Given number of operation
    K = 10

    # Size of array
    N = len(arr)

    # Sort the array
    arr = sorted(arr)

    # Function call
    print(findMaxMedian(arr, N, K))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check operation can be
// perform or not
static bool possible(int []arr, int N,
                       int mid, int K)
{
    int add = 0;

    for(int i = N / 2 - (N + 1) % 2;
            i < N; ++i)
    {
        if (mid - arr[i] > 0)
        {

            // Number of operation to
            // perform s.t. mid is median
            add += (mid - arr[i]);

            if (add > K)
                return false;
        }
    }

    // If mid is median of the array
    if (add <= K)
        return true;
    else
        return false;
}

// Function to find max median
// of the array
static int findMaxMedian(int []arr, int N,
                                    int K)
{

    // Lowest possible median
    int low = 1;
    int mx = 0;

    for(int i = 0; i < N; ++i)
    {
        mx = Math.Max(mx, arr[i]);
    }

    // Highest possible median
    int high = K + mx;

    while (low <= high)
    {
        int mid = (high + low) / 2;

        // Checking for mid is possible
        // for the median of array after
        // doing at most k operation
        if (possible(arr, N, mid, K))
        {
            low = mid + 1;
        }

        else
        {
            high = mid - 1;
        }
    }

    if (N % 2 == 0)
    {
        if (low - 1 < arr[N / 2])
        {
            return (arr[N / 2] + low - 1) / 2;
        }
    }

    // Return the max possible ans
    return low - 1;
}

// Driver code
public static void Main(string[] args)
{

    // Given array
    int []arr = { 1, 3, 6 };

    // Given number of operation
    int K = 10;

    // Size of array
    int N = arr.Length;

    // Sort the array
    Array.Sort(arr);

    // Function call
    Console.Write(findMaxMedian(arr, N, K));
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to check operation can be
    // perform or not
    function possible(arr, N, mid, K)
    {

        let add = 0;

        for (let i = parseInt(N / 2, 10) - (N + 1) % 2; i < N; ++i) {

            if (mid - arr[i] > 0) {

                // Number of operation to
                // perform s.t. mid is median
                add += (mid - arr[i]);

                if (add > K)
                    return false;
            }
        }

        // If mid is median of the array
        if (add <= K)
            return true;
        else
            return false;
    }

    // Function to find max median
    // of the array
    function findMaxMedian(arr, N, K)
    {

        // Lowest possible median
        let low = 1;
        let mx = 0;

        for (let i = 0; i < N; ++i) {
            mx = Math.max(mx, arr[i]);
        }

        // Highest possible median
        let high = K + mx;

        while (low <= high) {

            let mid = parseInt((high + low) / 2, 10);

            // Checking for mid is possible
            // for the median of array after
            // doing at most k operation
            if (possible(arr, N, mid, K)) {
                low = mid + 1;
            }

            else {
                high = mid - 1;
            }
        }

        if (N % 2 == 0) {

            if (low - 1 < arr[parseInt(N / 2)]) {
                return parseInt((arr[parseInt(N / 2)] + low - 1) / 2, 10);
            }
        }

        // Return the max possible ans
        return low - 1;
    }

    // Given array
    let arr = [ 1, 3, 6 ];

    // Given number of operation
    let K = 10;

    // Size of array
    let N = arr.length;

    // Sort the array
    arr.sort();

    // Function call
    document.write(findMaxMedian(arr, N, K));

</script>
```

**Output:** 

```
9
```

**时间复杂度:** *O(N*log(K + M))* ，其中 M 是给定数组的最大元素。
**辅助空间:** *O(1)*