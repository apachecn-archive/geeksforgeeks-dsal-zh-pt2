# 最小化插入，使每对连续数组元素之和最多为 K

> 原文:[https://www . geesforgeks . org/minimum-insertions-to-make-sum-of-每对连续数组元素-至多-k/](https://www.geeksforgeeks.org/minimize-insertions-to-make-sum-of-every-pair-of-consecutive-array-elements-at-most-k/)

给定一个由 **N** 个正整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找到任意正整数所需的最小插入次数，使得每个相邻元素的总和最多为**K**。如果不可能，则打印【T10 "-" 1 "。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 6
> **输出:** 2
> **解释:**
> 需要以下插入:
> **操作 1:** 在索引 2 和 3 之间插入 1。因此，数组修改为{1，2，3，1，4，5}。
> **操作 2:** 在索引 4 和索引 5 之间插入 1。因此，数组修改为{1，2，3，1，4，1，5}。因此，所需的最小插入次数是 2。
> 
> **输入:** arr[] = {4，5，6，7，7，8}，K = 8
> **输出:** -1

**方法:**这个想法是基于这样一个事实:如果元素本身不等于或大于 **K** ，那么在总和超过 **K** 的元素之间插入 **1** 会使连续元素的总和小于 **K** 。按照以下步骤解决给定的问题:

*   初始化三个变量，比如 **res = 0** 、**可能= 1** 、 **last = 0** 来存储最小插入的计数，检查是否有可能使所有连续对的总和**最多为 K** ，并将之前的数字分别存储到当前元素。
*   [遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 并执行以下步骤:
    *   如果**arr【I】**的值至少为 **K** ，则不可能使所有连续对 **的[和最多为 K](https://www.geeksforgeeks.org/sum-consecutive-elements-array/)** 。
    *   如果**最后一个**和 **arr[i]** 之和大于 **K** ，那么将 **res** 增加 **1** 和分配**最后一个= arr[i]** 。
*   完成上述步骤后，如果**可能**的值为 **1** ，则打印 **res** 的值作为所需的最小插入次数。否则，打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count minimum number of
// insertions required to make sum of
// every pair of adjacent elements at most K
void minimumInsertions(int arr[],
                       int N, int K)
{
    // Stores if it is possible to
    // make sum of each pair of
    // adjacent elements at most K
    bool possible = 1;

    // Stores the count of insertions
    int res = 0;

    // Stores the previous
    // value to index i
    int last = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If arr[i] is greater
        // than or equal to K
        if (arr[i] >= K) {

            // Mark possible 0
            possible = 0;
            break;
        }

        // If last + arr[i]
        // is greater than K
        if (last + arr[i] > K)

            // Increment res by 1
            res++;

        // Assign arr[i] to last
        last = arr[i];
    }

    // If possible to make the sum of
    // pairs of adjacent elements at most K
    if (possible) {
        cout << res;
    }

    // Otherwise print "-1"
    else {

        cout << "-1";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int K = 6;
    int N = sizeof(arr) / sizeof(arr[0]);

    minimumInsertions(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to count minimum number of
  // insertions required to make sum of
  // every pair of adjacent elements at most K
  static void minimumInsertions(int arr[],
                                int N, int K)
  {

    // Stores if it is possible to
    // make sum of each pair of
    // adjacent elements at most K
    boolean possible = true;

    // Stores the count of insertions
    int res = 0;

    // Stores the previous
    // value to index i
    int last = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // If arr[i] is greater
      // than or equal to K
      if (arr[i] >= K) {

        // Mark possible 0
        possible = false;
        break;
      }

      // If last + arr[i]
      // is greater than K
      if (last + arr[i] > K)

        // Increment res by 1
        res++;

      // Assign arr[i] to last
      last = arr[i];
    }

    // If possible to make the sum of
    // pairs of adjacent elements at most K
    if (possible) {
      System.out.print(res);
    }

    // Otherwise print "-1"
    else {

      System.out.print("-1");
    }
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 1, 2, 3, 4, 5 };
    int K = 6;
    int N = arr.length;

    minimumInsertions(arr, N, K);

  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to count minimum number of
# insertions required to make sum of
# every pair of adjacent elements at most K
def minimumInsertions(arr, N, K):

    # Stores if it is possible to
    # make sum of each pair of
    # adjacent elements at most K
    possible = 1

    # Stores the count of insertions
    res = 0

    # Stores the previous
    # value to index i
    last = 0

    # Traverse the array
    for i in range(N):

        # If arr[i] is greater
        # than or equal to K
        if (arr[i] >= K):

            # Mark possible 0
            possible = 0
            break

        # If last + arr[i]
        # is greater than K
        if (last + arr[i] > K):

            # Increment res by 1
            res += 1

        # Assign arr[i] to last
        last = arr[i]

    # If possible to make the sum of
    # pairs of adjacent elements at most K
    if (possible):
        print(res)

    # Otherwise print "-1"
    else:
        print("-1")

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 3, 4, 5]
    K = 6
    N = len(arr)

    minimumInsertions(arr, N, K)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

  // Function to count minimum number of
  // insertions required to make sum of
  // every pair of adjacent elements at most K
  static void minimumInsertions(int[] arr,
                                int N, int K)
  {

    // Stores if it is possible to
    // make sum of each pair of
    // adjacent elements at most K
    bool possible = true;

    // Stores the count of insertions
    int res = 0;

    // Stores the previous
    // value to index i
    int last = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // If arr[i] is greater
      // than or equal to K
      if (arr[i] >= K) {

        // Mark possible 0
        possible = false;
        break;
      }

      // If last + arr[i]
      // is greater than K
      if (last + arr[i] > K)

        // Increment res by 1
        res++;

      // Assign arr[i] to last
      last = arr[i];
    }

    // If possible to make the sum of
    // pairs of adjacent elements at most K
    if (possible) {
      Console.Write(res);
    }

    // Otherwise print "-1"
    else {

      Console.Write("-1");
    }
  }

  // Driver code
  static void Main()
  {

    int[] arr = { 1, 2, 3, 4, 5 };
    int K = 6;
    int N = arr.Length;

    minimumInsertions(arr, N, K);
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to count minimum number of
    // insertions required to make sum of
    // every pair of adjacent elements at most K
    function minimumInsertions(arr , N , K) {

        // Stores if it is possible to
        // make sum of each pair of
        // adjacent elements at most K
        var possible = true;

        // Stores the count of insertions
        var res = 0;

        // Stores the previous
        // value to index i
        var last = 0;

        // Traverse the array
        for (i = 0; i < N; i++) {

            // If arr[i] is greater
            // than or equal to K
            if (arr[i] >= K) {

                // Mark possible 0
                possible = false;
                break;
            }

            // If last + arr[i]
            // is greater than K
            if (last + arr[i] > K)

                // Increment res by 1
                res++;

            // Assign arr[i] to last
            last = arr[i];
        }

        // If possible to make the sum of
        // pairs of adjacent elements at most K
        if (possible) {
            document.write(res);
        }

        // Otherwise print "-1"
        else {

            document.write("-1");
        }
    }

    // Driver Code

        var arr = [ 1, 2, 3, 4, 5 ];
        var K = 6;
        var N = arr.length;

        minimumInsertions(arr, N, K);

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)