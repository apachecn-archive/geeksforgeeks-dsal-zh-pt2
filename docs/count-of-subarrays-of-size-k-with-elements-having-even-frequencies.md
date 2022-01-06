# 具有偶数频率的 K 尺寸子阵列的计数

> 原文:[https://www . geeksforgeeks . org/具有偶频率元素的 k 尺寸子阵列计数/](https://www.geeksforgeeks.org/count-of-subarrays-of-size-k-with-elements-having-even-frequencies/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是计算大小为 **K** 的子阵列，其中每个元素在子阵列中出现偶数次。

**示例:**

> **输入:** arr[] = {1，4，2，10，2，10，0，20}，K = 4
> **输出:** 1
> **说明:**只有子阵{2，10，2，10}满足要求条件。
> 
> **输入:** arr[] = {1，4，2，10，2，3，1，0，20}，K = 3
> **输出:** 0

**天真方法:**
想法是生成大小为 **K** 的所有子阵列，并检查每一个子阵列的所有元素是否存在甚至多次。

***时间复杂度:** O(N*K)*
**高效进场:**

这里的思路是用 [**窗口滑动**](https://www.geeksforgeeks.org/window-sliding-technique/) 和 [**异或**](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 的概念。

1.  如果给定的 **K** 为**奇数**，则**返回 0** ，因为如果 K 为奇数，则保证至少有一个数字出现奇数次。
2.  检查 K 是否大于 arr[]的长度，然后返回 0。
3.  初始化以下变量:
    *   **计数:**存储具有所有元素的大小为 **K** 的子阵列的计数。
    *   **开始:**移除最左边的元素，它不再是 k 尺寸子阵列的一部分。
    *   **currXor:** 存储当前子阵列的 Xor。
4.  计算第一个 K 尺寸子阵列的**异或**并检查 *currXor* 是否变为 **0** ，然后将*计数*递增，并通过用**arr【start】**消除**异或**来更新 *currXor* ，并将 **start** 递增 1。
5.  从 **K** 到 arr[]的长度遍历 arr[]:
    *   通过与*arr【I】*进行异或运算来更新 *currXor* 。
    *   如果*电流*变为 **0** ，则增加*计数*否则忽略。
    *   通过消除与 *arr【开始】*的异或来更新 *currXor* 。
    *   将*增加 1，开始*。
6.  返回*计数*。

以下是上述方法的实现:

## C++

```
// C++ program to count subarrays
// of size K with all elements
// having even frequencies
#include<bits/stdc++.h>
using namespace std;

// Function to return count of
// required subarrays
int countSubarray(int arr[], int K,
                             int N)
{

    // If K is odd
    if (K % 2 != 0)

        // Not possible to have
        // any such subarrays
        return 0;

    if (N < K)
        return 0;

    // Stores the starting index
    // of every subarrays
    int start = 0;

    int i = 0;

    // Stores the count of
    // required subarrays
    int count = 0;

    // Stores Xor of the
    // current subarray.
    int currXor = arr[i++];

    // Xor of first subarray
    // of size K
    while (i < K)
    {
        currXor ^= arr[i];
        i++;
    }

    // If all elements appear
    // even number of times,
    // increase the count of
    // such subarrays
    if (currXor == 0)
        count++;

    // Remove the starting element
    // from the current subarray
    currXor ^= arr[start++];

    // Traverse the array
    // for the remaining
    // subarrays
    while (i < N)
    {

        // Update Xor by adding the
        // last element of the
        // current subarray
        currXor ^= arr[i];

        // Increment i
        i++;

        // If currXor becomes 0,
        // then increment count
        if (currXor == 0)
            count++;

        // Update currXor by removing
        // the starting element of the
        // current subarray
        currXor ^= arr[start++];
    }

    // Return count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 4, 2, 2, 4 };
    int K = 4;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << (countSubarray(arr, K, N));
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count subarrays
// of size K with all elements
// having even frequencies

import java.util.*;

class GFG {

    // Function to return count of
    // required subarrays
    static int countSubarray(int[] arr,
                             int K, int N)
    {
        // If K is odd
        if (K % 2 != 0)
            // Not possible to have
            // any such subarrays
            return 0;

        if (N < K)
            return 0;

        // Stores the starting index
        // of every subarrays
        int start = 0;

        int i = 0;
        // Stores the count of
        // required subarrays
        int count = 0;
        // Stores Xor of the
        // current subarray.
        int currXor = arr[i++];

        // Xor of first subarray
        // of size K
        while (i < K) {
            currXor ^= arr[i];
            i++;
        }

        // If all elements appear
        // even number of times,
        // increase the count of
        // such subarrays
        if (currXor == 0)
            count++;

        // Remove the starting element
        // from the current subarray
        currXor ^= arr[start++];

        // Traverse the array
        // for the remaining
        // subarrays
        while (i < N) {
            // Update Xor by adding the
            // last element of the
            // current subarray
            currXor ^= arr[i];
            // Increment i
            i++;

            // If currXor becomes 0,
            // then increment count
            if (currXor == 0)
                count++;

            // Update currXor by removing
            // the starting element of the
            // current subarray
            currXor ^= arr[start++];
        }

        // Return count
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 2, 4, 4, 2, 2, 4 };
        int K = 4;
        int N = arr.length;
        System.out.println(
            countSubarray(arr, K, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program to count subarrays
# of size K with all elements
# having even frequencies

# Function to return count of
# required subarrays
def countSubarray(arr, K, N):

    # If K is odd
    if (K % 2 != 0):

        # Not possible to have
        # any such subarrays
        return 0

    if (N < K):
        return 0

    # Stores the starting index
    # of every subarrays
    start = 0
    i = 0

    # Stores the count of
    # required subarrays
    count = 0

    # Stores Xor of the
    # current subarray.
    currXor = arr[i]
    i += 1

    # Xor of first subarray
    # of size K
    while (i < K):
        currXor ^= arr[i]
        i += 1

    # If all elements appear
    # even number of times,
    # increase the count of
    # such subarrays
    if (currXor == 0):
        count += 1

    # Remove the starting element
    # from the current subarray
    currXor ^= arr[start]
    start += 1

    # Traverse the array
    # for the remaining
    # subarrays
    while (i < N):

        # Update Xor by adding the
        # last element of the
        # current subarray
        currXor ^= arr[i]

        # Increment i
        i += 1

        # If currXor becomes 0,
        # then increment count
        if (currXor == 0):
            count += 1

        # Update currXor by removing
        # the starting element of the
        # current subarray
        currXor ^= arr[start]
        start += 1

    # Return count
    return count

# Driver Code
if __name__ == '__main__':

    arr = [ 2, 4, 4, 2, 2, 4 ]
    K = 4
    N = len(arr)

    print(countSubarray(arr, K, N))

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# program to count subarrays
// of size K with all elements
// having even frequencies
using System;
class GFG{

// Function to return count of
// required subarrays
static int countSubarray(int[] arr,
                         int K, int N)
{
    // If K is odd
    if (K % 2 != 0)

        // Not possible to have
        // any such subarrays
        return 0;

    if (N < K)
        return 0;

    // Stores the starting index
    // of every subarrays
    int start = 0;

    int i = 0;

    // Stores the count of
    // required subarrays
    int count = 0;

    // Stores Xor of the
    // current subarray.
    int currXor = arr[i++];

    // Xor of first subarray
    // of size K
    while (i < K)
    {
        currXor ^= arr[i];
        i++;
    }

    // If all elements appear
    // even number of times,
    // increase the count of
    // such subarrays
    if (currXor == 0)
        count++;

    // Remove the starting element
    // from the current subarray
    currXor ^= arr[start++];

    // Traverse the array
    // for the remaining
    // subarrays
    while (i < N)
    {
        // Update Xor by adding the
        // last element of the
        // current subarray
        currXor ^= arr[i];

        // Increment i
        i++;

        // If currXor becomes 0,
        // then increment count
        if (currXor == 0)
            count++;

        // Update currXor by removing
        // the starting element of the
        // current subarray
        currXor ^= arr[start++];
    }

    // Return count
    return count;
}

// Driver Code
public static void Main()
{
    int[] arr = { 2, 4, 4, 2, 2, 4 };
    int K = 4;
    int N = arr.Length;
    Console.Write(countSubarray(arr, K, N));
}
}

// This code is contributed by Akanksha_Rai
```

## java 描述语言

```
<script>

// Javascript program to count subarrays
// of size K with all elements
// having even frequencies

// Function to return count of
// required subarrays
function countSubarray(arr, K, N)
{

    // If K is odd
    if (K % 2 != 0)

        // Not possible to have
        // any such subarrays
        return 0;

    if (N < K)
        return 0;

    // Stores the starting index
    // of every subarrays
    var start = 0;

    var i = 0;

    // Stores the count of
    // required subarrays
    var count = 0;

    // Stores Xor of the
    // current subarray.
    var currXor = arr[i];
    i++;

    // Xor of first subarray
    // of size K
    while (i < K)
    {
        currXor ^= arr[i];
        i++;
    }

    // If all elements appear
    // even number of times,
    // increase the count of
    // such subarrays
    if (currXor == 0)
        count++;

    // Remove the starting element
    // from the current subarray
    currXor ^= arr[start];
    start++;

    // Traverse the array
    // for the remaining
    // subarrays
    while (i < N)
    {

        // Update Xor by adding the
        // last element of the
        // current subarray
        currXor ^= arr[i];

        // Increment i
        i++;

        // If currXor becomes 0,
        // then increment count
        if (currXor == 0)
            count++;

        // Update currXor by removing
        // the starting element of the
        // current subarray
        currXor ^= arr[start];
        start++;
    }

    // Return count
    return count;
}

// Driver Code
    var arr = [2, 4, 4, 2, 2, 4];
    var K = 4;
    var N = arr.length;

    document.write(countSubarray(arr, K, N));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N)*
***空间复杂度:** O(1)*