# 通过选择大小为 K 的 M 个子阵列

最大化子阵列和

> 原文:[https://www . geeksforgeeks . org/通过选择 k 大小的 m 个子阵列来最大化子阵列总和/](https://www.geeksforgeeks.org/maximize-the-subarray-sum-by-choosing-m-subarrays-of-size-k/)

给定一个包含 **N** 正整数和两个整数 **K** 和 **M** 的数组 **arr** ，任务是计算大小为 **K** 的 **M** 子数组的最大和。

**示例:**

> **输入:** arr[] = {1，2，1，2，6，7，5，1}，M = 3，K = 2
> **输出:** 33
> **说明:**选择的三个子阵分别为[2，6]，[6，7]和[7，5]。所以，总和:8 +12 +13 = 33
> 
> **输入:** arr[] = {1，4，1，0，6，7，5，9}，M = 4，，K = 5
> **输出:** 76

**方法:**这个问题可以通过预先计算前缀和直到每个索引 **i** 来解决，它将告诉我们从 **0** 到 **i** 的子阵列的和。现在，这个前缀和可以用来找到大小为 K 的每个子阵列的和，使用公式:

> **从 I 到 j 的子阵列和=直到 j 的前缀和–直到 I 的前缀和**

找到所有子阵和后，选择最大 **M** 个子阵和计算答案。
要解决此问题，请遵循以下步骤:

1.  创建一个向量**前缀**，其中每个节点代表直到该索引的前缀和，以及另一个向量**子矩阵**，以存储所有大小的子矩阵和 **K** 。
2.  现在，运行一个从 **i=K** 到 **i=N** 的循环，并使用公式 **subarraySum[i-K，I]**=**prefixSum[I]-prefixSum[I-K]**计算每个子阵列的和，并将其推入向量 **subarraySum** 。
3.  将 **subarraySum** 按降序排序，加上最上面的 **M** 元素即可得到答案。
4.  根据以上观察打印答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the maximum
// sum of M subarrays of size K
int maximumSum(vector<int>& arr, int M, int K)
{
    int N = arr.size();
    vector<int> prefixSum(N + 1, 0);

    // Calculating prefix sum
    for (int i = 1; i <= N; ++i) {
        prefixSum[i] = prefixSum[i - 1]
                       + arr[i - 1];
    }

    vector<int> subarraysSum;

    // Finding sum of each subarray of size K
    for (int i = K; i <= N; i++) {
        subarraysSum.push_back(
            prefixSum[i]
            - prefixSum[i - K]);
    }

    sort(subarraysSum.begin(),
         subarraysSum.end(),
         greater<int>());

    int sum = 0;

    // Selecting the M maximum sums
    // to calculate the answer
    for (int i = 0; i < M; ++i) {
        sum += subarraysSum[i];
    }
    return sum;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 4, 1, 0, 6, 7, 5, 9 };
    int M = 4, K = 5;
    cout << maximumSum(arr, M, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate the maximum
// sum of M subarrays of size K
static  int maximumSum(int []arr, int M, int K)
{
    int N = arr.length;
    int []prefixSum = new int[N + 1];

    // Calculating prefix sum
    for (int i = 1; i <= N; ++i) {
        prefixSum[i] = prefixSum[i - 1]
                       + arr[i - 1];
    }

    Vector<Integer> subarraysSum = new Vector<Integer>();

    // Finding sum of each subarray of size K
    for (int i = K; i <= N; i++) {
        subarraysSum.add(
            prefixSum[i]
            - prefixSum[i - K]);
    }

    Collections.sort(subarraysSum,Collections.reverseOrder());

    int sum = 0;

    // Selecting the M maximum sums
    // to calculate the answer
    for (int i = 0; i < M; ++i) {
        sum += subarraysSum.get(i);
    }
    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 4, 1, 0, 6, 7, 5, 9 };
    int M = 4, K = 5;
    System.out.print(maximumSum(arr, M, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python program for the above approach

# Function to calculate the maximum
# sum of M subarrays of size K
def maximumSum(arr, M, K):

    N = len(arr)
    prefixSum = [0 for _ in range(N + 1)]

    # Calculating prefix sum
    for i in range(1, N+1):
        prefixSum[i] = prefixSum[i - 1] + arr[i - 1]

    subarraysSum = []

    # Finding sum of each subarray of size K
    for i in range(K, N+1):
        subarraysSum.append(prefixSum[i] - prefixSum[i - K])

    subarraysSum.sort()
    sum = 0

    # Selecting the M maximum sums
    # to calculate the answer
    for i in range(0, M):
        sum += subarraysSum[i]

    return sum

# Driver Code
if __name__ == "__main__":

    arr = [1, 4, 1, 0, 6, 7, 5, 9]
    M = 4
    K = 5
    print(maximumSum(arr, M, K))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{
// Function to calculate the maximum
// sum of M subarrays of size K
static  int maximumSum(int []arr, int M, int K)
{
    int N = arr.Length;
    int []prefixSum = new int[N + 1];

    // Calculating prefix sum
    for (int i = 1; i <= N; ++i) {
        prefixSum[i] = prefixSum[i - 1]
                       + arr[i - 1];
    }

    List<int> subarraysSum = new List<int>();

    // Finding sum of each subarray of size K
    for (int i = K; i <= N; i++) {
        subarraysSum.Add(
            prefixSum[i]
            - prefixSum[i - K]);
    }

    subarraysSum.Sort();
    subarraysSum.Reverse();

    int sum = 0;

    // Selecting the M maximum sums
    // to calculate the answer
    for (int i = 0; i < M; ++i) {
        sum += subarraysSum[i];
    }
    return sum;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 4, 1, 0, 6, 7, 5, 9 };
    int M = 4, K = 5;
    Console.Write(maximumSum(arr, M, K));
}
}

// This code is contributed by Samim Hossain Mondal
```

## java 描述语言

```
<script>
// Javascript code for the above approach

// Function to calculate the maximum
// sum of M subarrays of size K
function maximumSum(arr, M, K)
{
    var N = arr.length;
    var prefixSum = Array(N + 1).fill(0);

    // Calculating prefix sum
    for (var i = 1; i <= N; ++i) {
        prefixSum[i] = prefixSum[i - 1]
                       + arr[i - 1];
    }
    var subarraysSum = [];
    var t = 0;

    // Finding sum of each subarray of size K
    for (var i = K; i <= N; i++) {
        subarraysSum[t++] =
            (prefixSum[i] - prefixSum[i - K]);
    }

    subarraysSum.sort();
    subarraysSum.reverse();
    var sum = 0;

    // Selecting the M maximum sums
    // to calculate the answer
    for (var i = 0; i < M; ++i) {
        sum += subarraysSum[i];
    }
    return sum;
}

// Driver Code
var arr = [ 1, 4, 1, 0, 6, 7, 5, 9 ];
var M = 4, K = 5;
document.write(maximumSum(arr, M, K));

// This code is contributed by Samim Hossain Mondal
</script>
```

**Output**

```
76
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)