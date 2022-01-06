# 翻转给定数组中最多 K 个元素的符号后，求子序列的最大和

> 原文:[https://www . geeksforgeeks . org/find-给定数组中最多 k 个元素的翻转符号后子序列的最大和/](https://www.geeksforgeeks.org/find-maximum-sum-of-subsequence-after-flipping-signs-of-at-most-k-elements-in-given-array/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr** ，任务是在翻转最多 **K** 个元素的符号后，找到子序列的最大和。

**示例:**

> **输入**:arr =【6，-10，-1，0，-4，2】，K = 2
> **输出** : 22
> **说明**:分别翻转-10 和-4 到 10 和 4 可以得到最大和
> 
> **输入** : arr = [1，2，3]，K = 3
> **输出** : 6

**接近**:按照以下步骤解决问题:

*   [排序](https://www.geeksforgeeks.org/sorting-algorithms/)数组
*   将变量**和**初始化为 0，以存储子序列的最大和
*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并将负元素转换为正并递减 **k** 直到 **k > 0**
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并只将正的值相加
*   返回答案**总和**

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// the max sum of subsequence
int maxSubseq(int arr[], int N, int K)
{
    // Variable to store the max sum
    int sum = 0;

    // Sort the array
    sort(arr, arr + N);

    // Iterate over the array
    for (int i = 0; i < N; i++) {
        if (K == 0)
            break;

        if (arr[i] < 0) {

            // Flip sign
            arr[i] = -arr[i];

            // Decrement k
            K--;
        }
    }

    // Traverse over the array
    for (int i = 0; i < N; i++)

        // Add only positive elements
        if (arr[i] > 0)
            sum += arr[i];

    // Return the max sum
    return sum;
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 6, -10, -1, 0, -4, 2 };

    // Variable to store number
    // of flips are allowed
    int K = 2;
    int N = sizeof(arr)
            / sizeof(arr[0]);

    // Function call to find
    // the maximum sum of subsequence
    cout << maxSubseq(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;

class GFG
{

  // Function to calculate
  // the max sum of subsequence
  static int maxSubseq(int arr[], int N, int K)
  {

    // Variable to store the max sum
    int sum = 0;

    // Sort the array
    Arrays.sort(arr);

    // Iterate over the array
    for (int i = 0; i < N; i++) {
      if (K == 0)
        break;

      if (arr[i] < 0) {

        // Flip sign
        arr[i] = -arr[i];

        // Decrement k
        K--;
      }
    }

    // Traverse over the array
    for (int i = 0; i < N; i++)

      // Add only positive elements
      if (arr[i] > 0)
        sum += arr[i];

    // Return the max sum
    return sum;
  }

  // Driver Code
  public static void main(String []args)
  {

    // Given array
    int []arr = { 6, -10, -1, 0, -4, 2 };

    // Variable to store number
    // of flips are allowed
    int K = 2;
    int N = arr.length;

    // Function call to find
    // the maximum sum of subsequence
    System.out.println(maxSubseq(arr, N, K));
  }
}

// This code is contributed by ipg2016107.
```

## 蟒蛇 3

```
# Python 3 implementation for the above approach

# Function to calculate
# the max sum of subsequence
def maxSubseq(arr, N, K):

    # Variable to store the max sum
    sum = 0

    # Sort the array
    arr.sort()

    # Iterate over the array
    for i in range(N):
        if (K == 0):
            break

        if (arr[i] < 0):

            # Flip sign
            arr[i] = -arr[i]

            # Decrement k
            K -= 1

    # Traverse over the array
    for i in range(N):

        # Add only positive elements
        if (arr[i] > 0):
            sum += arr[i]

    # Return the max sum
    return sum

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [6, -10, -1, 0, -4, 2]

    # Variable to store number
    # of flips are allowed
    K = 2
    N = len(arr)

    # Function call to find
    # the maximum sum of subsequence
    print(maxSubseq(arr, N, K))

    # This code is contributed by ukasp.
```

## C#

```
// C++ implementation for the above approach
using System;

class GFG
{

// Function to calculate
// the max sum of subsequence
static int maxSubseq(int []arr, int N, int K)
{

    // Variable to store the max sum
    int sum = 0;

    // Sort the array
    Array.Sort(arr);

    // Iterate over the array
    for (int i = 0; i < N; i++) {
        if (K == 0)
            break;

        if (arr[i] < 0) {

            // Flip sign
            arr[i] = -arr[i];

            // Decrement k
            K--;
        }
    }

    // Traverse over the array
    for (int i = 0; i < N; i++)

        // Add only positive elements
        if (arr[i] > 0)
            sum += arr[i];

    // Return the max sum
    return sum;
}

// Driver Code
public static void Main(string[] args)
    {

    // Given array
    int []arr = { 6, -10, -1, 0, -4, 2 };

    // Variable to store number
    // of flips are allowed
    int K = 2;
    int N = arr.Length;

    // Function call to find
    // the maximum sum of subsequence
    Console.Write(maxSubseq(arr, N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
    // JavaScript implementation for the above approach

    // Function to calculate
    // the max sum of subsequence
    const maxSubseq = (arr, N, K) => {
        // Variable to store the max sum
        let sum = 0;

        // Sort the array
        arr.sort((a, b) => a - b);

        // Iterate over the array
        for (let i = 0; i < N; i++) {
            if (K == 0)
                break;

            if (arr[i] < 0) {

                // Flip sign
                arr[i] = -arr[i];

                // Decrement k
                K--;
            }
        }

        // Traverse over the array
        for (let i = 0; i < N; i++)

            // Add only positive elements
            if (arr[i] > 0)
                sum += arr[i];

        // Return the max sum
        return sum;
    }

    // Driver Code

    // Given array
    let arr = [6, -10, -1, 0, -4, 2];

    // Variable to store number
    // of flips are allowed
    let K = 2;
    let N = arr.length

    // Function call to find
    // the maximum sum of subsequence
    document.write(maxSubseq(arr, N, K));

    // This code is contributed by rakeshsahni

</script>
```

**Output:** 

```
22
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)