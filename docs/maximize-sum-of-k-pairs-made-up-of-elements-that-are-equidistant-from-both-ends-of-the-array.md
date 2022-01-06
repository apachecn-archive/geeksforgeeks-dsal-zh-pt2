# 最大化由与数组两端等距的元素组成的 K 对的总和

> 原文:[https://www . geeksforgeeks . org/最大化 k 对之和-由与数组两端等距的元素组成/](https://www.geeksforgeeks.org/maximize-sum-of-k-pairs-made-up-of-elements-that-are-equidistant-from-both-ends-of-the-array/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是求 **(arr[i]，arr[N–I–1])**形式的 **K** 对的最大和，其中**(0≤I≤N–1)**。

**示例:**

> **输入:** arr[] = {2，-4，3，-1，2，5}，K = 2
> **输出:** 9
> **解释:**该形式的所有可能性对(arr[i]，arr[N–I+1])为:
> 
> 1.  (2, 5)
> 2.  (-1, 3)
> 3.  (-4, 2)
> 
> 从以上对中，具有最大和的 K(= 2)对是(2，5)和(-1，3)。因此，最大和= 2 + 5 + (-1) + 3 = 9。
> 
> **输入:** arr[] = {2，-4，-2，4}，K = 2
> T3】输出: 0

**天真方法:**解决问题最简单的方法是[从数组中生成给定形式的所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，并计算 K 个这样的对的最大和。检查所有对后，打印所有可能总和中的最大总和。

***时间复杂度:**O(N<sup>2</sup>* K)*
***辅助空间:** O(N <sup>2</sup> )*

**高效进场:**以上进场可优化[贪婪](https://www.geeksforgeeks.org/greedy-algorithms/)。想法是只选择成本最高的 K 对。按照以下步骤解决问题:

*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说 **pairwiseSum[]** ，来存储数组中所需对的和。
*   [通过](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，从给定数组中生成对 **(arr[i]，arr[N–I+1])**。将它们的和存储在向量 **pairwiseSum[]** 中。
*   [按降序排列向量**成对求和[]**](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   完成上述步骤后，打印向量**的第一个 **K** 元素的和作为合成和。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// K pairs of the form (arr[i],
// arr[N - i - 1])
int maxSum(int arr[], int N, int K)
{
    // Stores the resultant pairwise
    // sum
    vector<int> pairwiseSum;

    // Traverse till half of the array
    for (int i = 0; i < N / 2; i++) {

        // Update the value of curSum
        int curSum = arr[i] + arr[i + N / 2];
        pairwiseSum.push_back(curSum);
    }

    // Sort in the descending order
    sort(pairwiseSum.begin(),
         pairwiseSum.end(),
         greater<int>());

    // Stores the resultant maximum sum
    int maxSum = 0;

    // Add K maximum sums obtained
    for (int i = 0; i < K; i++) {

        // Update the value of maxSum
        maxSum += pairwiseSum[i];
    }

    // Print the maximum sum
    cout << maxSum;
}

// Driver Code
int main()
{
    int arr[] = { 2, -4, 3, 5, 2, -1 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);
    maxSum(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.Collections;
class GFG{

// Function to find the maximum sum of
// K pairs of the form (arr[i],
// arr[N - i - 1])
public static void maxSum(int arr[], int N, int K)
{
    // Stores the resultant pairwise
    // sum
    ArrayList<Integer> pairwiseSum = new ArrayList<Integer>();

    // Traverse till half of the array
    for (int i = 0; i < N / 2; i++) {

        // Update the value of curSum
        int curSum = arr[i] + arr[i + N / 2];
        pairwiseSum.add(curSum);
    }

    // Sort in the descending order
    Collections.sort(pairwiseSum);
    Collections.reverse(pairwiseSum);

    // Stores the resultant maximum sum
    int maxSum = 0;

    // Add K maximum sums obtained
    for (int i = 0; i < K; i++) {

        // Update the value of maxSum
        maxSum += pairwiseSum.get(i);
    }

    // Print the maximum sum
    System.out.println(maxSum);
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 2, -4, 3, 5, 2, -1 };
    int K = 2;
    int N = arr.length;
    maxSum(arr, N, K);
}
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum sum of
# K pairs of the form (arr[i],
# arr[N - i - 1])
def maxSum(arr, N, K):

    # Stores the resultant pairwise
    # sum
    pairwiseSum = []

    # Traverse till half of the array
    for i in range(N // 2):

        # Update the value of curSum
        curSum = arr[i] + arr[i + N // 2]
        pairwiseSum.append(curSum)

    # Sort in the descending order
    pairwiseSum.sort(reverse = True)

    # Stores the resultant maximum sum
    maxSum = 0

    # Add K maximum sums obtained
    for i in range(K):

        # Update the value of maxSum
        maxSum += pairwiseSum[i]

    # Print the maximum sum
    print(maxSum)

# Driver Code
if __name__ == '__main__':

    arr = [ 2, -4, 3, 5, 2, -1 ]
    K = 2
    N = len(arr)

    maxSum(arr, N, K)

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum sum of
// K pairs of the form (arr[i],
// arr[N - i - 1])
static void maxSum(int []arr, int N, int K)
{
    // Stores the resultant pairwise
    // sum
    List<int> pairwiseSum = new List<int>();

    // Traverse till half of the array
    for (int i = 0; i < N / 2; i++) {

        // Update the value of curSum
        int curSum = arr[i] + arr[i + N / 2];
        pairwiseSum.Add(curSum);
    }

    // Sort in the descending order
    pairwiseSum.Sort();
    pairwiseSum.Reverse();
    // Stores the resultant maximum sum
    int maxSum = 0;

    // Add K maximum sums obtained
    for (int i = 0; i < K; i++) {

        // Update the value of maxSum
        maxSum += pairwiseSum[i];
    }

    // Print the maximum sum
    Console.Write(maxSum);
}

// Driver Code
public static void Main()
{
    int []arr = { 2, -4, 3, 5, 2, -1 };
    int K = 2;
    int N = arr.Length;
    maxSum(arr, N, K);

}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach

      // Function to find the maximum sum of
      // K pairs of the form (arr[i],
      // arr[N - i - 1])
      function maxSum(arr, N, K) {
          // Stores the resultant pairwise
          // sum
          let pairwiseSum = [];

          // Traverse till half of the array
          for (let i = 0; i < N / 2; i++) {

              // Update the value of curSum
              let curSum = arr[i] + arr[i + parseInt(N / 2)];
              pairwiseSum.push(curSum);
          }

          // Sort in the descending order
          pairwiseSum.sort(function (a, b) { return b - a });

          // Stores the resultant maximum sum
         let maxSum = 0;

          // Add K maximum sums obtained
          for (let i = 0; i < K; i++) {

              // Update the value of maxSum
              maxSum += pairwiseSum[i];
          }

          // Print the maximum sum
          document.write(maxSum);
      }

      // Driver Code

      let arr = [2, -4, 3, 5, 2, -1];
      let K = 2;
      let N = arr.length;
      maxSum(arr, N, K);

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
9
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*