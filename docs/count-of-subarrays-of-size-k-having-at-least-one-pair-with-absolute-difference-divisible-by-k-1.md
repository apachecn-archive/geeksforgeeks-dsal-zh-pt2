# 至少有一对绝对差可被 K-1 整除的大小为 K 的子阵列的计数

> 原文:[https://www . geeksforgeeks . org/k 大小的子阵列计数至少有一对绝对差可被 k-1 整除/](https://www.geeksforgeeks.org/count-of-subarrays-of-size-k-having-at-least-one-pair-with-absolute-difference-divisible-by-k-1/)

给定一个由 **N** 元素组成的**arr【】**，任务是计算所有大小为 **K** 的子阵列，其中至少有一对子阵列的绝对差可被**K–1**整除。
**举例:**

> **输入:** arr[] = {1，5，3，2，17，18}，K = 4
> **输出:** 3
> **解释:**
> 大小为 4 的三个子阵列是:
> {1，5，3，2}: Pair {5，2}有被 3 除尽的差
> {5，3，2，17}:Pair {5，2}，{ 5，17}，{2，17 }有可除尽的差 17}有可被 3 整除的差
> **输入:** arr[] = {1，2，3，4，5}，K = 5
> **输出:** 1
> **解释:**
> {1，2，3，4，5}: Pair {1，5}可被 4
> 整除

**天真方法:**
解决问题最简单的方法是迭代所有**大小的子阵****K**并检查是否存在任何其差可被**K–1**整除的对。
***时间复杂度:** O(N * K * K)*
**高效途径:**以上途径可以利用[鸽子洞原理](https://www.geeksforgeeks.org/discrete-mathematics-the-pigeonhole-principle/)进行优化。按照以下步骤解决问题:

*   分别考虑标有 **0、1、2、…、K-2** 的 **K-1** 框。当数组中的任意数字 x 被 **K-1** 除时，它们代表**余数**，这意味着这些框存储数组元素的**模 K-1** 。

*   现在，在尺寸为 **K** 的**子阵列**中，根据**鸽巢原理**，必须至少有一对具有相同余数的箱子。这意味着**至少有一对**的差甚至总和可以被 **K** 整除。

*   从这个定理我们可以得出结论:**每一个大小为 **K** 的**子阵列，总会有至少一对其差可以被 **K-1** 整除。

*   因此，答案将等于给定阵列中可能的大小为 **K** 的子阵列的数量，等于**N–K+1**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required
// number of subarrays
int findSubarrays(int arr[],
                  int N,
                  int K)
{
    // Return number of possible
    // subarrays of length K
    return N - K + 1;
}

// Driver Code
int main()
{
    int arr[] = { 1, 5, 3, 2, 17, 18 };
    int K = 4;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << findSubarrays(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
class GFG{

// Function to return the required
// number of subarrays
static int findSubarrays(int arr[], int N,
                                    int K)
{

    // Return number of possible
    // subarrays of length K
    return N - K + 1;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 5, 3, 2, 17, 18 };
    int K = 4;
    int N = arr.length;

    System.out.print(findSubarrays(arr, N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to return the required
# number of subarrays
def findSubarrays(arr, N, K):

    # Return number of possible
    # subarrays of length K
    return N - K + 1;

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 5, 3, 2, 17, 18 ];
    K = 4;
    N = len(arr);

    print(findSubarrays(arr, N, K));

# This code is contributed by Rohit_ranjan
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG{

// Function to return the required
// number of subarrays
static int findSubarrays(int []arr, int N,
                                    int K)
{

    // Return number of possible
    // subarrays of length K
    return N - K + 1;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 5, 3, 2, 17, 18 };
    int K = 4;
    int N = arr.Length;

    Console.Write(findSubarrays(arr, N, K));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to return the required
// number of subarrays
function findSubarrays(arr, N, K)
{

    // Return number of possible
    // subarrays of length K
    return N - K + 1;
}

    // Driver Code

    let arr = [ 1, 5, 3, 2, 17, 18 ];
    let K = 4;
    let N = arr.length;

    document.write(findSubarrays(arr, N, K));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*