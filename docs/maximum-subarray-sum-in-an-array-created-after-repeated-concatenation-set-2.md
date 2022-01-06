# 重复连接后创建的数组中的最大子数组和| Set-2

> 原文:[https://www . geesforgeks . org/maximum-subarray-sum-in-array-created-after-repeated-concation-set-2/](https://www.geeksforgeeks.org/maximum-subarray-sum-in-an-array-created-after-repeated-concatenation-set-2/)

给定一个由 **N** 个整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr[]** ，任务是[在通过重复给定数组 **K** 次而形成的修改后的数组中找到任意连续子数组](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/) [](https://www.geeksforgeeks.org/tag/subarray/)的最大和。

**示例:**

> **输入:** arr[] = {-1，10，20}，K = 2
> **输出:** 59
> **解释:**
> 将数组串联两次后，数组修改为{-1，10，20，-1，10，20}。
> 总和最大的子阵在[1，5]范围内，即{10，20，-1，10，20}。
> 
> **输入:** arr[] = {10，20，-30，-1，40}，K =10
> **输出:** 391

**天真方法:**解决问题最简单的方法在[集-1](https://www.geeksforgeeks.org/maximum-subarray-sum-array-created-repeated-concatenation/) 中讨论。

**高效方法:**上述方法可以基于以下观察进一步优化:

1.  如果数组的[和大于 **0** ，则有助于回答。否则，将所有数组元素都包含在最大子数组中是不好的。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
2.  假设变量 **maxPrefix** 和 **maxSufix** 存储两次重复数组的最大前缀和最大后缀和。
3.  因此，最大和子阵列可以通过以下方式之一形成:
    1.  追加由前两个数组组合而成的数组的 **maxSufix** 的元素，然后追加剩余的 **N-2** 数组。
    2.  首先追加 **N-2 个**数组，然后追加最后两个数组组合而成的数组的 **maxPrefix** 的元素。
    3.  取两次重复阵列的最大和子阵的所有元素。

按照以下步骤解决问题:

*   [求数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)**arr【】**的和并存储在变量中，比如 **sum1** 。
*   初始化一个变量，将**和**以及**和**设为 **0** 来存储当前最大和以及答案。
*   如果 **K = 1** ，[打印阵列的最大子阵列和](https://www.geeksforgeeks.org/print-the-maximum-subarray-sum/) **arr[]。**
*   否则，将**【0，N-1】**中的数组 **arr[]** 的元素插入到[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中，说 **V[]** 两次。
*   [求数组的最大前缀和](https://www.geeksforgeeks.org/maximum-prefix-sum-possible-by-merging-two-given-arrays/) **V[]** 存储在变量中，比如 **maxPrefix** 。
*   [求数组](https://www.geeksforgeeks.org/index-with-minimum-sum-of-prefix-and-suffix-sums-in-an-array/) **V[]** 的最大后缀和，存储在变量中，比如 **maxSufix** 。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，2 * N-1】**中迭代，并执行以下步骤:
    *   将 **sum** 的值修改为 **max(sum + arr[i]，arr[i])** ，将 **ans** 的值更新为 **max(ans，sum)。**
*   如果 **sum1 > 0，**则更新 **ans** 至最大值 **{ans，sum1*(K-2)+maxPrefix，sum1*(K-2)*maxSufix}。**
*   最后，完成以上步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find contiguous subarray with
// maximum sum if array is repeated K times
int maxSubArraySumRepeated(int arr[], int N, int K)
{
    // Store the sum of the array arr[]
    int sum = 0;

    // Traverse the array and find sum
    for (int i = 0; i < N; i++)
        sum += arr[i];

    int curr = arr[0];

    // Store the answer
    int ans = arr[0];

    // If K = 1
    if (K == 1) {

        // Apply Kadane algorithm to find sum
        for (int i = 1; i < N; i++) {
            curr = max(arr[i], curr + arr[i]);
            ans = max(ans, curr);
        }
        // Return the answer
        return ans;
    }

    // Stores the twice repeated array
    vector<int> V;

    // Traverse the range [0, 2*N]
    for (int i = 0; i < 2 * N; i++) {
        V.push_back(arr[i % N]);
    }

    // Stores the maximum suffix sum
    int maxSuf = V[0];

    // Stores the maximum prefix sum
    int maxPref = V[2 * N - 1];

    curr = V[0];

    for (int i = 1; i < 2 * N; i++) {
        curr += V[i];
        maxPref = max(maxPref, curr);
    }

    curr = V[2 * N - 1];
    for (int i = 2 * N - 2; i >= 0; i--) {
        curr += V[i];
        maxSuf = max(maxSuf, curr);
    }

    curr = V[0];
    // Apply Kadane algorithm for 2 repetition
    // of the array
    for (int i = 1; i < 2 * N; i++) {
        curr = max(V[i], curr + V[i]);
        ans = max(ans, curr);
    }

    // If the sum of the array is greater than 0
    if (sum > 0) {
        int temp = 1LL * sum * (K - 2);
        ans = max(ans, max(temp + maxPref, temp + maxSuf));
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 10, 20, -30, -1, 40 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 10;

    // Function Call
    cout << maxSubArraySumRepeated(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find contiguous subarray with
// maximum sum if array is repeated K times
static int maxSubArraySumRepeated(int[] arr, int N,
                                  int K)
{

    // Store the sum of the array arr[]
    int sum = 0;

    // Traverse the array and find sum
    for(int i = 0; i < N; i++)
        sum += arr[i];

    int curr = arr[0];

    // Store the answer
    int ans = arr[0];

    // If K = 1
    if (K == 1)
    {

        // Apply Kadane algorithm to find sum
        for(int i = 1; i < N; i++)
        {
            curr = Math.max(arr[i], curr + arr[i]);
            ans = Math.max(ans, curr);
        }

        // Return the answer
        return ans;
    }

    // Stores the twice repeated array
    ArrayList<Integer> V = new  ArrayList<Integer>();

    // Traverse the range [0, 2*N]
    for(int i = 0; i < 2 * N; i++)
    {
        V.add(arr[i % N]);
    }

    // Stores the maximum suffix sum
    int maxSuf = V.get(0);

    // Stores the maximum prefix sum
    int maxPref = V.get(2 * N - 1);

    curr = V.get(0);

    for(int i = 1; i < 2 * N; i++)
    {
        curr += V.get(i);
        maxPref = Math.max(maxPref, curr);
    }

    curr = V.get(2 * N - 1);
    for(int i = 2 * N - 2; i >= 0; i--)
    {
        curr += V.get(i);
        maxSuf = Math.max(maxSuf, curr);
    }

    curr = V.get(0);

    // Apply Kadane algorithm for 2 repetition
    // of the array
    for(int i = 1; i < 2 * N; i++)
    {
        curr = Math.max(V.get(i), curr + V.get(i));
        ans = Math.max(ans, curr);
    }

    // If the sum of the array is greater than 0
    if (sum > 0)
    {
        int temp = sum * (K - 2);
        ans = Math.max(ans, Math.max(temp + maxPref,
                                     temp + maxSuf));
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void main(String args[])
{

    // Given Input
    int []arr = { 10, 20, -30, -1, 40 };
    int N = arr.length;
    int K = 10;

    // Function Call
    System.out.print(maxSubArraySumRepeated(arr, N, K));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {
    // Function to find contiguous subarray with
    // maximum sum if array is repeated K times
    static int maxSubArraySumRepeated(int[] arr, int N,
                                      int K)
    {
        // Store the sum of the array arr[]
        int sum = 0;

        // Traverse the array and find sum
        for (int i = 0; i < N; i++)
            sum += arr[i];

        int curr = arr[0];

        // Store the answer
        int ans = arr[0];

        // If K = 1
        if (K == 1) {

            // Apply Kadane algorithm to find sum
            for (int i = 1; i < N; i++) {
                curr = Math.Max(arr[i], curr + arr[i]);
                ans = Math.Max(ans, curr);
            }
            // Return the answer
            return ans;
        }

        // Stores the twice repeated array
        List<int> V = new List<int>();

        // Traverse the range [0, 2*N]
        for (int i = 0; i < 2 * N; i++) {
            V.Add(arr[i % N]);
        }

        // Stores the maximum suffix sum
        int maxSuf = V[0];

        // Stores the maximum prefix sum
        int maxPref = V[2 * N - 1];

        curr = V[0];

        for (int i = 1; i < 2 * N; i++) {
            curr += V[i];
            maxPref = Math.Max(maxPref, curr);
        }

        curr = V[2 * N - 1];
        for (int i = 2 * N - 2; i >= 0; i--) {
            curr += V[i];
            maxSuf = Math.Max(maxSuf, curr);
        }

        curr = V[0];
        // Apply Kadane algorithm for 2 repetition
        // of the array
        for (int i = 1; i < 2 * N; i++) {
            curr = Math.Max(V[i], curr + V[i]);
            ans = Math.Max(ans, curr);
        }

        // If the sum of the array is greater than 0
        if (sum > 0) {
            int temp = sum * (K - 2);
            ans = Math.Max(ans, Math.Max(temp + maxPref,
                                         temp + maxSuf));
        }

        // Return the answer
        return ans;
    }

    // Driver Code
    public static void Main()
    {
        // Given Input
        int[] arr = { 10, 20, -30, -1, 40 };
        int N = arr.Length;
        int K = 10;

        // Function Call
        Console.WriteLine(
            maxSubArraySumRepeated(arr, N, K));
    }
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to find contiguous subarray with
# maximum sum if array is repeated K times
def maxSubArraySumRepeated(arr, N, K):

    # Store the sum of the array arr[]
    sum = 0

    # Traverse the array and find sum
    for i in range(N):
        sum += arr[i]

    curr = arr[0]

    # Store the answer
    ans = arr[0]

    # If K = 1
    if (K == 1):

        # Apply Kadane algorithm to find sum
        for i in range(1,N,1):
            curr = max(arr[i], curr + arr[i])
            ans = max(ans, curr)

        # Return the answer
        return ans

    # Stores the twice repeated array
    V = []

    # Traverse the range [0, 2*N]
    for i in range(2 * N):
        V.append(arr[i % N])

    # Stores the maximum suffix sum
    maxSuf = V[0]

    # Stores the maximum prefix sum
    maxPref = V[2 * N - 1]

    curr = V[0]

    for i in range(1,2 * N,1):
        curr += V[i]
        maxPref = max(maxPref, curr)

    curr = V[2 * N - 1]
    i = 2 * N - 2
    while(i >= 0):
        curr += V[i]
        maxSuf = max(maxSuf, curr)
        i -= 1

    curr = V[0]

    # Apply Kadane algorithm for 2 repetition
    # of the array
    for i in range(1, 2 * N, 1):
        curr = max(V[i], curr + V[i])
        ans = max(ans, curr)

    # If the sum of the array is greater than 0
    if (sum > 0):
        temp = sum * (K - 2)
        ans = max(ans, max(temp + maxPref, temp + maxSuf))

    # Return the answer
    return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [10, 20, -30, -1, 40]
    N = len(arr)
    K = 10

    # Function Call
    print(maxSubArraySumRepeated(arr, N, K))

    # This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find contiguous subarray with
// maximum sum if array is repeated K times
function maxSubArraySumRepeated(arr, N, K) {
    // Store the sum of the array arr[]
    let sum = 0;

    // Traverse the array and find sum
    for (let i = 0; i < N; i++)
        sum += arr[i];

    let curr = arr[0];

    // Store the answer
    let ans = arr[0];

    // If K = 1
    if (K == 1) {

        // Apply Kadane algorithm to find sum
        for (let i = 1; i < N; i++) {
            curr = Math.max(arr[i], curr + arr[i]);
            ans = Math.max(ans, curr);
        }
        // Return the answer
        return ans;
    }

    // Stores the twice repeated array
    let V = [];

    // Traverse the range [0, 2*N]
    for (let i = 0; i < 2 * N; i++) {
        V.push(arr[i % N]);
    }

    // Stores the maximum suffix sum
    let maxSuf = V[0];

    // Stores the maximum prefix sum
    let maxPref = V[2 * N - 1];

    curr = V[0];

    for (let i = 1; i < 2 * N; i++) {
        curr += V[i];
        maxPref = Math.max(maxPref, curr);
    }

    curr = V[2 * N - 1];
    for (let i = 2 * N - 2; i >= 0; i--) {
        curr += V[i];
        maxSuf = Math.max(maxSuf, curr);
    }

    curr = V[0];
    // Apply Kadane algorithm for 2 repetition
    // of the array
    for (let i = 1; i < 2 * N; i++) {
        curr = Math.max(V[i], curr + V[i]);
        ans = Math.max(ans, curr);
    }

    // If the sum of the array is greater than 0
    if (sum > 0) {
        let temp = sum * (K - 2);
        ans = Math.max(ans, Math.max(temp + maxPref, temp + maxSuf));
    }

    // Return the answer
    return ans;
}

// Driver Code

// Given Input
let arr = [10, 20, -30, -1, 40];
let N = arr.length;
let K = 10;

// Function Call
document.write(maxSubArraySumRepeated(arr, N, K));

</script>
```

**Output**

```
391
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)