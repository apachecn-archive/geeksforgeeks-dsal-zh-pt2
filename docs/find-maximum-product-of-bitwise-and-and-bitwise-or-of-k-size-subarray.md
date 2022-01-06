# 求 K 尺寸子阵列的按位“与”和按位“或”的最大乘积

> 原文:[https://www . geeksforgeeks . org/find-k 大小的最大位积和位或子数组/](https://www.geeksforgeeks.org/find-maximum-product-of-bitwise-and-and-bitwise-or-of-k-size-subarray/)

给定一个包含 **N** 个整数和一个整数 **K** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找到**位“与”**和**位“或”**的乘积的最大值，该乘积是一个 **K** 大小的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的所有元素。

**示例:**

> ***输入:*** arr[] = {1，2，3，4}，K = 2
> ***输出:** 6*
> ***说明:**所有 K 大小子阵列的按位 AND 和按位 XOR 分别为{(0，3)、(2，3)、(0，7)}。因此，他们乘积的最大可能值是 2 * 3 = 6，这是必需的答案。*
> 
> ***输入:*** arr[] = {6，7，7，10，8，2}，K = 3
> ***输出:*** 42

**方法:**给定的问题可以使用[滑动窗口技术](http://www.geeksforgeeks.org/window-sliding-technique/)来解决。其思想是为 K 大小的子阵列窗口维护[位](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) AND 和位“或”的值，这可以通过维护一个[数组](https://www.geeksforgeeks.org/array-data-structure/)来完成，该数组存储当前窗口所有元素上每个位的计数。如果第 **i <sup>th</sup>** 位的计数为 **K** ，则该位必须包含在按位“与”中，如果该位的计数大于 **1** ，则必须包含在按位“或”中。在变量**和**中存储所有窗口的产品最大值，这是必需的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert bit array to
// decimal number representing OR
int build_or(int bit[])
{
    int ans = 0;

    for (int i = 0; i < 32; i++)
        if (bit[i])
            ans += (1 << i);

    return ans;
}

// Function to convert bit array to
// decimal number representing AND
int build_and(int bit[], int k)
{
    int ans = 0;

    for (int i = 0; i < 32; i++)
        if (bit[i] == k)
            ans += (1 << i);

    return ans;
}

// Function to find maximum value of
// AND * OR over all K sized subarrays
int maximizeAndOr(int arr[], int N, int K)
{
    // Maintain an integer array bit[]
    // of size 32 all initialized to 0
    int bit[32] = { 0 };

    // Create a sliding window of size k
    for (int i = 0; i < K; i++) {
        for (int j = 0; j < 32; j++) {
            if (arr[i] & (1 << j))
                bit[j]++;
        }
    }

    int ans = build_and(bit, K) * build_or(bit);

    for (int i = K; i < N; i++) {

        // Perform operation for
        // removed element
        for (int j = 0; j < 32; j++) {
            if (arr[i - K] & (1 << j))
                bit[j]--;
        }

        // Perform operation for
        // added_element
        for (int j = 0; j < 32; j++) {
            if (arr[i] & (1 << j))
                bit[j]++;
        }

        // Taking maximum value
        ans = max(ans, build_and(bit, K)
                  * build_or(bit));
    }

    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 6, 7, 7, 10, 8, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;

    cout << maximizeAndOr(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to convert bit array to
// decimal number representing OR
static int build_or(int[] bit)
{
    int ans = 0;

    for(int i = 0; i < 32; i++)
        if (bit[i] > 0)
            ans += (1 << i);

    return ans;
}

// Function to convert bit array to
// decimal number representing AND
static int build_and(int[] bit, int k)
{
    int ans = 0;

    for(int i = 0; i < 32; i++)
        if (bit[i] == k)
            ans += (1 << i);

    return ans;
}

// Function to find maximum value of
// AND * OR over all K sized subarrays
static int maximizeAndOr(int[] arr, int N, int K)
{

    // Maintain an integer array bit[]
    // of size 32 all initialized to 0
    int[] bit = new int[32];

    // Create a sliding window of size k
    for(int i = 0; i < K; i++)
    {
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }
    }

    int ans = build_and(bit, K) * build_or(bit);

    for(int i = K; i < N; i++)
    {

        // Perform operation for
        // removed element
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i - K] & (1 << j)) > 0)
                bit[j]--;
        }

        // Perform operation for
        // added_element
        for(int j = 0; j < 32; j++)
        {
            if ((arr[i] & (1 << j)) > 0)
                bit[j]++;
        }

        // Taking maximum value
        ans = Math.max(ans, build_and(bit, K) *
                            build_or(bit));
    }
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int[] arr = { 6, 7, 7, 10, 8, 2 };
    int N = arr.length;
    int K = 3;

    System.out.println(maximizeAndOr(arr, N, K));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to convert bit array to
# decimal number representing OR
def build_or(bit):

    ans = 0

    for i in range(0, 32):
        if (bit[i]):
            ans += (1 << i)

    return ans

# Function to convert bit array to
# decimal number representing AND
def build_and(bit, k):

    ans = 0

    for i in range(0, 32):
        if (bit[i] == k):
            ans += (1 << i)

    return ans

# Function to find maximum value of
# AND * OR over all K sized subarrays
def maximizeAndOr(arr, N, K):

    # Maintain an integer array bit[]
    # of size 32 all initialized to 0
    bit = [0 for _ in range(32)]

    # Create a sliding window of size k
    for i in range(0, K):
        for j in range(0, 32):
            if (arr[i] & (1 << j)):
                bit[j] += 1

    ans = build_and(bit, K) * build_or(bit)

    for i in range(K, N):

        # Perform operation for
        # removed element
        for j in range(0, 32):
            if (arr[i - K] & (1 << j)):
                bit[j] -= 1

        # Perform operation for
        # added_element
        for j in range(0, 32):
            if (arr[i] & (1 << j)):
                bit[j] += 1

        # Taking maximum value
        ans = max(ans, build_and(bit, K) *
                       build_or(bit))

    return ans

# Driver Code
if __name__ == "__main__":

    arr = [ 6, 7, 7, 10, 8, 2 ]
    N = len(arr)
    K = 3

    print(maximizeAndOr(arr, N, K))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to convert bit array to
    // decimal number representing OR
    static int build_or(int[] bit)
    {
        int ans = 0;

        for (int i = 0; i < 32; i++)
            if (bit[i] > 0)
                ans += (1 << i);

        return ans;
    }

    // Function to convert bit array to
    // decimal number representing AND
    static int build_and(int[] bit, int k)
    {
        int ans = 0;

        for (int i = 0; i < 32; i++)
            if (bit[i] == k)
                ans += (1 << i);

        return ans;
    }

    // Function to find maximum value of
    // AND * OR over all K sized subarrays
    static int maximizeAndOr(int[] arr, int N, int K)
    {
        // Maintain an integer array bit[]
        // of size 32 all initialized to 0
        int[] bit = new int[32];

        // Create a sliding window of size k
        for (int i = 0; i < K; i++) {
            for (int j = 0; j < 32; j++) {
                if ((arr[i] & (1 << j)) > 0)
                    bit[j]++;
            }
        }

        int ans = build_and(bit, K) * build_or(bit);

        for (int i = K; i < N; i++) {

            // Perform operation for
            // removed element
            for (int j = 0; j < 32; j++) {
                if ((arr[i - K] & (1 << j)) > 0)
                    bit[j]--;
            }

            // Perform operation for
            // added_element
            for (int j = 0; j < 32; j++) {
                if ((arr[i] & (1 << j)) > 0)
                    bit[j]++;
            }

            // Taking maximum value
            ans = Math.Max(ans, build_and(bit, K)
                                    * build_or(bit));
        }

        return ans;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 6, 7, 7, 10, 8, 2 };
        int N = arr.Length;
        int K = 3;

        Console.WriteLine(maximizeAndOr(arr, N, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to convert bit array to
// decimal number representing OR
function build_or(bit)
{
    let ans = 0;

    for(let i = 0; i < 32; i++)
        if (bit[i])
            ans += (1 << i);

    return ans;
}

// Function to convert bit array to
// decimal number representing AND
function build_and(bit, k)
{
    let ans = 0;

    for(let i = 0; i < 32; i++)
        if (bit[i] == k)
            ans += (1 << i);

    return ans;
}

// Function to find maximum value of
// AND * OR over all K sized subarrays
function maximizeAndOr(arr, N, K)
{

    // Maintain an integer array bit[]
    // of size 32 all initialized to 0
    let bit = new Array(32).fill(0);

    // Create a sliding window of size k
    for(let i = 0; i < K; i++)
    {
        for(let j = 0; j < 32; j++)
        {
            if (arr[i] & (1 << j))
                bit[j]++;
        }
    }

    let ans = build_and(bit, K) * build_or(bit);

    for(let i = K; i < N; i++)
    {

        // Perform operation for
        // removed element
        for(let j = 0; j < 32; j++)
        {
            if (arr[i - K] & (1 << j))
                bit[j]--;
        }

        // Perform operation for
        // added_element
        for(let j = 0; j < 32; j++)
        {
            if (arr[i] & (1 << j))
                bit[j]++;
        }

        // Taking maximum value
        ans = Math.max(ans, build_and(bit, K) *
                            build_or(bit));
    }
    return ans;
}

// Driver Code
let arr = [ 6, 7, 7, 10, 8, 2 ];
let N = arr.length;
let K = 3;

document.write(maximizeAndOr(arr, N, K));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
42
```

***时间复杂度** : O(N*log N)*
***辅助空间:** O(1)*