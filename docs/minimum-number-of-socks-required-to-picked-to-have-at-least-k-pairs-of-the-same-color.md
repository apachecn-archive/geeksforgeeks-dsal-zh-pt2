# 至少挑选 K 双相同颜色的袜子所需的最少数量

> 原文:[https://www . geeksforgeeks . org/最少需要挑选多少双袜子才能拥有至少 k 双相同颜色的袜子/](https://www.geeksforgeeks.org/minimum-number-of-socks-required-to-picked-to-have-at-least-k-pairs-of-the-same-color/)

给定一个由 **N** 个整数组成的[数组**arr【】】**,使得**arr【I】**代表颜色 **i** 的袜子数量，以及一个整数 **K** ，任务是找到需要挑选的最小袜子数量，以获得至少 K 双**相同颜色的袜子。**](https://www.geeksforgeeks.org/introduction-to-arrays/)

**示例:**

> **输入:** arr[] = {3，4，5，3}，K = 6
> **输出:** 15
> **说明:**一个人需要挑选所有的袜子才能得到至少 6 双匹配的袜子。
> 
> **输入:** arr[] = {4，5，6}，K = 3
> T3】输出: 8

**方法:**给定的问题可以基于以下观察来解决:

*   根据[鸽子洞原理](https://www.geeksforgeeks.org/discrete-mathematics-the-pigeonhole-principle/)，即在最坏的情况下，如果已经挑选了不同颜色的 **N** 袜子，那么下一个挑选将形成一双匹配的袜子。
*   假设一个人挑选了不同颜色的 **N** 袜子，那么对于每双**(K–1)**袜子，一个人将需要挑选两只袜子，一只用于形成一双，另一只用于保持所有不同颜色的 **N** 袜子，对于最后一双，只需要挑选一只任何颜色的袜子。

因此，想法是找出相同颜色可以组成的对的总数，如果**总数**最多为**K**，则打印**(2 * K+N–1)**作为要拾取的对的最小数量。否则，打印**-1”**，因为没有足够的袜子形成 **K** 双。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to count the minimum
// number of socks to be picked
int findMin(int arr[], int N, int k)
{
    // Stores the total count
    // of pairs of socks
    int pairs = 0;

    // Find the total count of pairs
    for (int i = 0; i < N; i++) {
        pairs += arr[i] / 2;
    }

    // If K is greater than pairs
    if (k > pairs)
        return -1;

    // Otherwise
    else
        return 2 * k + N - 1;
}

int main()
{
    int arr[3] = { 4, 5, 6 };
    int K = 3;
    cout << findMin(arr, 3, K);
    return 0;
}

// This code is contributed by RohitOberoi.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to count the minimum
    // number of socks to be picked
    public static int findMin(
        int[] arr, int N, int k)
    {
        // Stores the total count
        // of pairs of socks
        int pairs = 0;

        // Find the total count of pairs
        for (int i = 0; i < N; i++) {
            pairs += arr[i] / 2;
        }

        // If K is greater than pairs
        if (k > pairs)
            return -1;

        // Otherwise
        else
            return 2 * k + N - 1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 4, 5, 6 };
        int K = 3;
        int N = arr.length;
        System.out.println(findMin(arr, N, K));
    }
}
```

## C#

```
// C# program for the above approach

using System;

class GFG {

    // Function to count the minimum
    // number of socks to be picked
    public static int findMin(int[] arr, int N, int k)
    {
        // Stores the total count
        // of pairs of socks
        int pairs = 0;

        // Find the total count of pairs
        for (int i = 0; i < N; i++) {
            pairs += arr[i] / 2;
        }

        // If K is greater than pairs
        if (k > pairs)
            return -1;

        // Otherwise
        else
            return 2 * k + N - 1;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 4, 5, 6 };
        int K = 3;
        int N = arr.Length;
        Console.WriteLine(findMin(arr, N, K));
    }
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count the minimum
# number of socks to be picked
def findMin(arr, N, k):

    # Stores the total count
    # of pairs of socks
    pairs = 0

    # Find the total count of pairs
    for i in range(N):
        pairs += arr[i] / 2

    # If K is greater than pairs
    if (k > pairs):
        return -1

    # Otherwise
    else:
        return 2 * k + N - 1

arr = [4, 5, 6]
k = 3
print(findMin(arr, 3, k));

# This code is contributed by SoumikMondal.
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

    // Function to count the minimum
    // number of socks to be picked
    function findMin(
        arr, N, k)
    {
        // Stores the total count
        // of pairs of socks
        let pairs = 0;

        // Find the total count of pairs
        for (let i = 0; i < N; i++) {
            pairs += arr[i] / 2;
        }

        // If K is greater than pairs
        if (k > pairs)
            return -1;

        // Otherwise
        else
            return 2 * k + N - 1;
    }

// Driver code

        let arr = [ 4, 5, 6 ];
        let K = 3;
        let N = arr.length;
        document.write(findMin(arr, N, K));

</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)