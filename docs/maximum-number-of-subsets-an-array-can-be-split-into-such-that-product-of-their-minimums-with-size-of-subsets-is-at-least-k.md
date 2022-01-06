# 一个数组可以分成的最大子集数，使得它们的最小值与子集大小的乘积至少为 K

> 原文:[https://www . geeksforgeeks . org/最大子集数-一个数组可以被拆分成这样的子集合大小的最小乘积至少是-k/](https://www.geeksforgeeks.org/maximum-number-of-subsets-an-array-can-be-split-into-such-that-product-of-their-minimums-with-size-of-subsets-is-at-least-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找到给定数组可以拆分成的不相交子集的最大数量，使得每个子集的最小元素与子集的[大小的乘积至少为 **K** 。](https://www.geeksforgeeks.org/print-subsets-given-size-set/)

**示例:**

> **输入:** arr[] = {7，11，2，9，5}，K = 10
> **输出:** 2
> **解释:**
> 所有这些不相交的子集都可能是:
> **子集{11}:** 子集的最小值和大小的乘积= 11 * 1 = 11 ( > 10)。
> **子集{5，9，7}:** 子集的最小值和大小的乘积= 5 * 3 = 15( > 10)。
> 因此，形成的子集总数为 2。
> 
> **输入:** arr[] = {1，3，3，7}，K = 12
> T3】输出: 0

**方法:**给定的问题可以通过[贪婪地](https://www.geeksforgeeks.org/greedy-algorithms/)基于以下观察来解决:

*   如问题陈述中所给出的，所形成的子集的[最小元素](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)和子集长度的乘积必须至少为**K**，因此为了最大化子集的数量，数组的[最大元素可以被分组到子集的最小元素。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
*   所以思路就是把子集的最小元素一个个最大化，这样就把子集的个数最大化了。

按照以下步骤解决问题:

*   初始化一个变量，比如说**将**计数为 **0** ，以存储形成的最大子集数。
*   初始化一个变量，将**长度**设为 **0** ，以存储子集的长度。
*   [按降序排列数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   将**长度**的值增加 **1** 。
    *   如果 **(arr[i] * length)** 的值大于 **K** ，则将**计数**的值增加 **1** ，并将**长度**的值更新为 **0** 。
*   完成上述步骤后，打印**计数**的值，作为最终形成的最大子集数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of subsets possible such that
// product of their minimums and the
// size of subsets are at least K
int maximumSubset(int arr[], int N,
                  int K)
{
    // Sort the array in
    // descending order
    sort(arr, arr + N, greater<int>());

    // Stores the size of
    // the current subset
    int len = 0;

    // Stores the count of subsets
    int ans = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Increment length of the
        // subsets by 1
        len++;

        // If arr[i] * len >= K
        if (arr[i] * len >= K) {

            // Increment ans by one
            ans++;

            // Update len
            len = 0;
        }
    }

    // Return the maximum possible
    // subsets formed
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 7, 11, 2, 9, 5 };
    int K = 10;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maximumSubset(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
public class GFG
{

  // Function to reverse the sorted array
  public static void reverse(int[] arr)
  {

    // Length of the array
    int n = arr.length;

    // Swaping the first half elements with last half
    // elements
    for (int i = 0; i < n / 2; i++) {

      // Storing the first half elements temporarily
      int temp = arr[i];

      // Assigning the first half to the last half
      arr[i] = arr[n - i - 1];

      // Assigning the last half to the first half
      arr[n - i - 1] = temp;
    }
  }

  // Function to find the maximum number
  // of subsets possible such that
  // product of their minimums and the
  // size of subsets are at least K
  public static int maximumSubset(int arr[], int N, int K)
  {

    // Sort the array in
    // descending order
    Arrays.sort(arr);
    reverse(arr);
    // Stores the size of
    // the current subset
    int len = 0;

    // Stores the count of subsets
    int ans = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

      // Increment length of the
      // subsets by 1
      len++;

      // If arr[i] * len >= K
      if (arr[i] * len >= K) {

        // Increment ans by one
        ans++;

        // Update len
        len = 0;
      }
    }

    // Return the maximum possible
    // subsets formed
    return ans;
  }

  // Driver Code
  public static void main(String args[]) {
    int arr[] = { 7, 11, 2, 9, 5 };
    int K = 10;
    int N =arr.length;
    System.out.println(maximumSubset(arr, N, K));
  }
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the maximum number
# of subsets possible such that
# product of their minimums and the
# size of subsets are at least K
def maximumSubset(arr, N,
                  K):

    # Sort the array in
    # descending order
    arr.sort(reverse = True)

    # Stores the size of
    # the current subset
    len = 0

    # Stores the count of subsets
    ans = 0

    # Traverse the array arr[]
    for i in range(N):

        # Increment length of the
        # subsets by 1
        len += 1

        # If arr[i] * len >= K
        if (arr[i] * len >= K):

            # Increment ans by one
            ans += 1

            # Update len
            len = 0

    # Return the maximum possible
    # subsets formed
    return ans

# Driver Code
if __name__ == "__main__":

    arr = [7, 11, 2, 9, 5]
    K = 10
    N = len(arr)
    print(maximumSubset(arr, N, K))

    # This code is contributed by ukasp.
```

## C#

```
using System;

public class GFG
{

    // Function to reverse the sorted array
    public static void reverse(int[] arr)
    {

        // Length of the array
        int n = arr.Length;

        // Swaping the first half elements with last half
        // elements
        for (int i = 0; i < n / 2; i++) {

            // Storing the first half elements temporarily
            int temp = arr[i];

            // Assigning the first half to the last half
            arr[i] = arr[n - i - 1];

            // Assigning the last half to the first half
            arr[n - i - 1] = temp;
        }
    }

    // Function to find the maximum number
    // of subsets possible such that
    // product of their minimums and the
    // size of subsets are at least K
    public static int maximumSubset(int []arr, int N, int K)
    {

        // Sort the array in
        // descending order
        Array.Sort(arr);
        reverse(arr);

        // Stores the size of
        // the current subset
        int len = 0;

        // Stores the count of subsets
        int ans = 0;

        // Traverse the array []arr
        for (int i = 0; i < N; i++)
        {

            // Increment length of the
            // subsets by 1
            len++;

            // If arr[i] * len >= K
            if (arr[i] * len >= K)
            {

                // Increment ans by one
                ans++;

                // Update len
                len = 0;
            }
        }

        // Return the maximum possible
        // subsets formed
        return ans;
    }

    // Driver Code
    public static void Main(String []args)
    {
        int []arr = { 7, 11, 2, 9, 5 };
        int K = 10;
        int N = arr.Length;
        Console.WriteLine(maximumSubset(arr, N, K));
    }
}

// This code is contributed by aashish1995.
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

  // Function to reverse the sorted array
  function reverse(arr)
  {

    // Length of the array
    let n = arr.length;

    // Swaping the first half elements with last half
    // elements
    for (let i = 0; i < n / 2; i++) {

      // Storing the first half elements temporarily
      let temp = arr[i];

      // Assigning the first half to the last half
      arr[i] = arr[n - i - 1];

      // Assigning the last half to the first half
      arr[n - i - 1] = temp;
    }
  }

  // Function to find the maximum number
  // of subsets possible such that
  // product of their minimums and the
  // size of subsets are at least K
  function maximumSubset(arr, N, K)
  {

    // Sort the array in
    // descending order
    arr.sort();
    arr.reverse();
    // Stores the size of
    // the current subset
    let len = 0;

    // Stores the count of subsets
    let ans = 0;

    // Traverse the array arr[]
    for (let i = 0; i < N; i++) {

      // Increment length of the
      // subsets by 1
      len++;

      // If arr[i] * len >= K
      if (arr[i] * len >= K) {

        // Increment ans by one
        ans++;

        // Update len
        len = 0;
      }
    }

    // Return the maximum possible
    // subsets formed
    return ans;
  }

// Driver code

    let arr = [ 7, 11, 2, 9, 5 ];
    let K = 10;
    let N =arr.length;
    document.write(maximumSubset(arr, N, K));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(1)*