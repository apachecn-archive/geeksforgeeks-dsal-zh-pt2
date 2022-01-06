# 修改数组的最小增量，这样任何数组元素的值都可以被拆分，使所有剩余的元素相等

> 原文:[https://www . geeksforgeeks . org/最小增量-修改数组-这样任何数组元素的值都可以被拆分-使所有剩余元素相等/](https://www.geeksforgeeks.org/minimum-increments-to-modify-array-such-that-value-of-any-array-element-can-be-splitted-to-make-all-remaining-elements-equal/)

给定一个由 **N** 个元素组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到在给定数组上需要执行的最小增量数，以便在任何索引处选择任何数组元素并将其值拆分为其他数组元素后，使所有其他**N–1**个元素相等。

**示例:**

> **输入:** N = 3，arr[] = {2，3，7}
> **输出:** 2
> **解释:**
> 将 arr[0]和 arr[1]递增 1 将 arr[]修改为{3，4，7}。
> 移除 arr[0]并添加到 arr[1]使数组成为{7，7}。
> 移除 arr[1]并添加到 arr[0]组成数组{7，7}
> 移除 arr[2]并添加 3 到 arr[1]并添加 4 到 arr[0]组成数组{7，7}。
> 因此，所需的增量计数为 2。
> 
> **输入:** N = 3，arr[] = {0，2，0 }
> T3】输出: 2

**接近**:按照以下步骤解决问题:

1.  找到给定数组元素和[的总和，即该数组](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)中存在的最大元素，并将其存储在变量中，比如**总和**和**最大元素**。
2.  所有剩余的**N–1**元素必须等于**上限(总和/ N-1)** 。让这个值为 **K** 。
3.  由于元素只能增加 **1** ，如果 **maxelement** 大于 **K** ，则将 **K** 设置为等于 **maxelement** 。
4.  现在，每个**N–1**值应该等于 **K** 。所以最终的总和应该是 **K * (N-1)** 。
5.  因此，所需的移动总数为**K *(N–1)–总和**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count minimum moves
void minimumMoves(int arr[], int N)
{
    // Stores sum of given array
    int sum = 0;

    // Stores maximum array element
    int maxelement = -1;

    // Base Case
    if (N == 2) {

        // If N is 2, the answer
        // will always be 0
        cout << 0;
    }

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Calculate sum of the array
        sum += arr[i];

        // Finding maximum element
        maxelement = max(maxelement, arr[i]);
    }

    // Calculate ceil(sum/N-1)
    int K = (sum + N - 2) / (N - 1);

    // If k is smaller than maxelement
    K = max(maxelement, K);

    // Final sum - original sum
    int ans = K * (N - 1) - sum;

    // Print the minimum number
    // of increments required
    cout << ans;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 3, 7 };

    // Size of given array
    int N = 3;

    // Function Call
    minimumMoves(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to find the minimum moves
    public static void minimumMoves(
        int[] arr, int N)
    {
        // Stores the sum of the array
        int sum = 0;

        // Store the maximum element
        int maxelement = -1;

        // Base Case
        if (N == 2) {

            // If N is 2, the answer
            // will always be 0
            System.out.print("0");
            return;
        }

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Calculate sum of the array
            sum += arr[i];

            // Finding maximum element
            maxelement = Math.max(
                maxelement, arr[i]);
        }

        // Calculate ceil(sum/N-1)
        int k = (sum + N - 2) / (N - 1);

        // If k is smaller than maxelement
        k = Math.max(maxelement, k);

        // Final sum - original sum
        int ans = k * (N - 1) - sum;

        // Print the minimum number
        // of increments required
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array
        int[] arr = { 2, 3, 7 };

        // Size of given array
        int N = arr.length;

        // Function Call
        minimumMoves(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count minimum moves
def minimumMoves(arr, N):

    # Stores sum of given array
    sum = 0

    # Stores maximum array element
    maxelement = -1

    # Base Case
    if (N == 2):

        # If N is 2, the answer
        # will always be 0
        print(0, end = "")

    # Traverse the array
    for i in range(N):

        # Calculate sum of the array
        sum += arr[i]

        # Finding maximum element
        maxelement = max(maxelement, arr[i])

    # Calculate ceil(sum/N-1)
    K = (sum + N - 2) // (N - 1)

    # If k is smaller than maxelement
    K = max(maxelement, K)

    # Final sum - original sum
    ans = K * (N - 1) - sum

    # Print the minimum number
    # of increments required
    print(ans)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 2, 3, 7 ]

    # Size of given array
    N = 3

    # Function Call
    minimumMoves(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find the minimum moves
  static void minimumMoves(int[] arr, int N)
  {

    // Stores the sum of the array
    int sum = 0;

    // Store the maximum element
    int maxelement = -1;

    // Base Case
    if (N == 2)
    {

      // If N is 2, the answer
      // will always be 0
      Console.Write("0");
      return;
    }

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // Calculate sum of the array
      sum += arr[i];

      // Finding maximum element
      maxelement = Math.Max(
        maxelement, arr[i]);
    }

    // Calculate ceil(sum/N-1)
    int k = (sum + N - 2) / (N - 1);

    // If k is smaller than maxelement
    k = Math.Max(maxelement, k);

    // Final sum - original sum
    int ans = k * (N - 1) - sum;

    // Print the minimum number
    // of increments required
    Console.WriteLine(ans);
  }

  // Driver code
  static void Main()
  {

    // Given array
    int[] arr = { 2, 3, 7 };

    // Size of given array
    int N = arr.Length;

    // Function Call
    minimumMoves(arr, N);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find the minimum moves
    function minimumMoves(arr, N)
    {

      // Stores the sum of the array
      let sum = 0;

      // Store the maximum element
      let maxelement = -1;

      // Base Case
      if (N == 2)
      {

        // If N is 2, the answer
        // will always be 0
        document.write("0");
        return;
      }

      // Traverse the array
      for (let i = 0; i < N; i++)
      {

        // Calculate sum of the array
        sum += arr[i];

        // Finding maximum element
        maxelement = Math.max(
          maxelement, arr[i]);
      }

      // Calculate ceil(sum/N-1)
      let k = (sum + N - 2) / (N - 1);

      // If k is smaller than maxelement
      k = Math.max(maxelement, k);

      // Final sum - original sum
      let ans = k * (N - 1) - sum;

      // Print the minimum number
      // of increments required
      document.write(ans);
    }

    // Given array
    let arr = [ 2, 3, 7 ];

    // Size of given array
    let N = arr.length;

    // Function Call
    minimumMoves(arr, N);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)