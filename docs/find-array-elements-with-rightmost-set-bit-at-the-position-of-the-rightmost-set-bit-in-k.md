# 在 K 中最右边设置位的位置找到最右边设置位的数组元素

> 原文:[https://www . geeksforgeeks . org/find-array-elements-with-right-set-bit-in-k/](https://www.geeksforgeeks.org/find-array-elements-with-rightmost-set-bit-at-the-position-of-the-rightmost-set-bit-in-k/)

给定一个由 **N** 和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是打印 **arr[]** 的元素，其最右边的设置位与 **K** 中最右边的设置位处于相同的[位置。](https://www.geeksforgeeks.org/position-of-rightmost-set-bit/)

**示例:**

> **输入:** arr[] = { 3，4，6，7，9，12，15 }，K = 7
> **输出:** { 3，7，9，15 }
> **解释:**
> 二进制表示 **K** (= **7** )为 **0111** 。
> **7 中最右边的置位位位在位置 1。**
> 因此，所有奇数阵列元素在位置 1 将具有最右边的设置位。
> 
> **输入:** arr[] = { 1，2，3，4，5}，K = 3
> T3】输出: {1，3，5 }

**方法:**按照以下步骤解决问题:

1.  初始化一个变量，说**掩码**，存储 **K** 的掩码。
2.  初始化一个变量，比如**位置**，将最右边的设置位的位置存储在 **K** 中。
3.  计算**遮罩**和 **K** 的[位“与”](https://www.geeksforgeeks.org/tag/bitwise-and/)，即**位置** = **(遮罩& K)**
4.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每个数组元素:
    *   如果面具&停止[i] ==位置:打印停止[i]。
    *   否则，[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to find the mask for
// finding rightmost set bit in K
    int findMask(int K)
    {
        int mask = 1;
        while ((K & mask) == 0)
        {
            mask = mask << 1;
        }
        return mask;
    }

    // Function to find all array elements
    // with rightmost set bit same as that in K
    void sameRightSetBitPos(
        int arr[], int N, int K)
    {

        // Stores mask of K
        int mask = findMask(K);

        // Store position of rightmost set bit
        int pos = (K & mask);

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // Check if rightmost set bit of
            // current array element is same as
            // position of rightmost set bit in K
            if ((arr[i] & mask) == pos)
                cout << arr[i] << " ";
        }
    }

// Driver Code
int main()
{
    // Input
        int arr[] = { 3, 4, 6, 7, 9, 12, 15 };
        int N = sizeof(arr) / sizeof(arr[0]);
        int K = 7;

        // Function call to find
        // the elements having same
        // rightmost set bit as of K
        sameRightSetBitPos(arr, N, K);

    return 0;
}

// This code is contributed by susmitakundugoaldanga.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach

import java.io.*;

class GFG {

    // Function to find the mask for
    // finding rightmost set bit in K
    static int findMask(int K)
    {
        int mask = 1;
        while ((K & mask) == 0) {
            mask = mask << 1;
        }
        return mask;
    }

    // Function to find all array elements
    // with rightmost set bit same as that in K
    public static void sameRightSetBitPos(
        int[] arr, int N, int K)
    {
        // Stores mask of K
        int mask = findMask(K);

        // Store position of rightmost set bit
        final int pos = (K & mask);

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Check if rightmost set bit of
            // current array element is same as
            // position of rightmost set bit in K
            if ((arr[i] & mask) == pos)
                System.out.print(arr[i] + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Input
        int[] arr = { 3, 4, 6, 7, 9, 12, 15 };
        int N = arr.length;
        int K = 7;

        // Function call to find
        // the elements having same
        // rightmost set bit as of K
        sameRightSetBitPos(arr, N, K);
    }
}
```

## 蟒蛇 3

```
# Python program for
# the above approach

# Function to find the mask for
# finding rightmost set bit in K
def findMask(K):
    mask = 1;
    while ((K & mask) == 0):
        mask = mask << 1;

    return mask;

# Function to find all array elements
# with rightmost set bit same as that in K
def sameRightSetBitPos(arr, N, K):

    # Stores mask of K
    mask = findMask(K);

    # Store position of rightmost set bit
    pos = (K & mask);

    # Traverse the array
    for i in range(N):

        # Check if rightmost set bit of
        # current array element is same as
        # position of rightmost set bit in K
        if ((arr[i] & mask) == pos):
            print(arr[i], end=" ");

# Driver Code
if __name__ == '__main__':
    # Input
    arr = [3, 4, 6, 7, 9, 12, 15];
    N = len(arr);
    K = 7;

    # Function call to find
    # the elements having same
    # rightmost set bit as of K
    sameRightSetBitPos(arr, N, K);

    # This code contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to find the mask for
  // finding rightmost set bit in K
  static int findMask(int K)
  {
    int mask = 1;
    while ((K & mask) == 0) {
      mask = mask << 1;
    }
    return mask;
  }

  // Function to find all array elements
  // with rightmost set bit same as that in K
  public static void sameRightSetBitPos(
    int[] arr, int N, int K)
  {
    // Stores mask of K
    int mask = findMask(K);

    // Store position of rightmost set bit
    int pos = (K & mask);

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Check if rightmost set bit of
      // current array element is same as
      // position of rightmost set bit in K
      if ((arr[i] & mask) == pos)
        Console.Write(arr[i] + " ");
    }
  }

  // Driver Code
  static public void Main ()
  {
    // Input
    int[] arr = { 3, 4, 6, 7, 9, 12, 15 };
    int N = arr.Length;
    int K = 7;

    // Function call to find
    // the elements having same
    // rightmost set bit as of K
    sameRightSetBitPos(arr, N, K);
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find the mask for
// finding rightmost set bit in K
    function findMask(K)
    {
        let mask = 1;
        while ((K & mask) == 0)
        {
            mask = mask << 1;
        }
        return mask;
    }

    // Function to find all array elements
    // with rightmost set bit same as that in K
    function sameRightSetBitPos(arr, N, K)
    {

        // Stores mask of K
        let mask = findMask(K);

        // Store position of rightmost set bit
        let pos = (K & mask);

        // Traverse the array
        for (let i = 0; i < N; i++)
        {

            // Check if rightmost set bit of
            // current array element is same as
            // position of rightmost set bit in K
            if ((arr[i] & mask) == pos)
                document.write(arr[i] + " ");
        }
    }

// Driver Code

    // Input
        let arr = [ 3, 4, 6, 7, 9, 12, 15 ];
        let N = arr.length;
        let K = 7;

        // Function call to find
        // the elements having same
        // rightmost set bit as of K
        sameRightSetBitPos(arr, N, K);

// This code is contributed by Manoj.
</script>
```

**Output:** 

```
3 7 9 15
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)