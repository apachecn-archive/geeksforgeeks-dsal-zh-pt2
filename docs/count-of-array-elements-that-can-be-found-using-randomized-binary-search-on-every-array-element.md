# 在每个数组元素上使用随机二分搜索法可以找到的数组元素的计数

> 原文:[https://www . geesforgeks . org/数组元素计数-可以使用-随机化-二进制-对每个数组元素进行搜索/](https://www.geeksforgeeks.org/count-of-array-elements-that-can-be-found-using-randomized-binary-search-on-every-array-element/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过对每个数组元素应用[随机化二分搜索法](https://www.geeksforgeeks.org/randomized-binary-search-algorithm/)来找到数组元素的最小计数。

**示例:**

> **输入:** arr[] = { 5，4，9 }
> **输出:** 2
> **解释:**
> 对数组中的 arr[0]应用随机化二分搜索法。
> 最初，搜索空间为[0，2]
> 假设 pivot = 1，arr[pivot] < arr[0]。因此，新的搜索空间是[2，2]，并且在搜索空间中找不到 arr[0]。
> 对于 arr[1]，搜索空间为[0，2]。
> 假设 pivot = 0，arr[pivot] > arr[0]。因此，新的搜索空间是[0，0]，并且在搜索空间中找不到 arr[1]。
> 对于 arr[2]，搜索空间为[0，2]。
> 选择任意元素作为轴心，可以找到 arr[2]。
> 
> **输入:** arr[] = { 1，2，3，4 }
> **输出:** 4

**方法:**思路是[数阵元，之前所有阵元都比它小，之后都比它大](https://www.geeksforgeeks.org/find-the-element-before-which-all-the-elements-are-smaller-than-it-and-after-which-all-are-greater-than-it/)。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说**smallestRight【】**来存储每个数组元素右侧的最小元素。
*   [反向遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并更新**smallestRight[I]= min(smallestRight[I+1]，arr[i])** 。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并在每个数组元素左侧存储最大元素，检查左侧最大元素是否小于右侧最小元素。如果发现为真，则增加计数。
*   最后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum count of
// array elements found by repeatedly
// applying Randomized Binary Search
int getDefiniteFinds(vector<int>& arr)
{

    // Stores count of array elements
    int n = arr.size();

    // smallestRight[i]: Stores the smallest
    // array element on the right side of i
    vector<int> smallestRight(n + 1);

    // Update smallestRight[0]
    smallestRight[n] = INT_MAX;

    // Traverse the array from right to left
    for (int i = n - 1; i >= 0; i--) {

        // Update smallestRight[i]
        smallestRight[i]
            = min(smallestRight[i + 1], arr[i]);
    }

    // Stores the largest element
    // upto i-th index
    int mn = INT_MIN;

    // Stores the minimum count of
    // elements found by repeatedly
    // applying Randomized Binary Search
    int ans = 0;
    for (int i = 0; i < n; i++) {

        // If largest element on left side is
        // less than smallest element on right side
        if (mn < arr[i] and arr[i] < smallestRight[i + 1]) {

            // Update ans
            ans++;
        }

        // Update mn
        mn = max(arr[i], mn);
    }

    return ans;
}

// Driver Code
int main()
{

    // Given array
    vector<int> arr = { 5, 4, 9 };

    // Function Call
    cout << getDefiniteFinds(arr) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG
{

  // Function to find minimum count of
  // array elements found by repeatedly
  // applying Randomized Binary Search
  static int getDefiniteFinds(int[] arr)
  {

    // Stores count of array elements
    int n = arr.length;

    // smallestRight[i]: Stores the smallest
    // array element on the right side of i
    int[] smallestRight = new int[n + 1];

    // Update smallestRight[0]
    smallestRight[n] = Integer.MAX_VALUE;

    // Traverse the array from right to left
    for (int i = n - 1; i >= 0; i--)
    {

      // Update smallestRight[i]
      smallestRight[i]
        = Math.min(smallestRight[i + 1], arr[i]);
    }

    // Stores the largest element
    // upto i-th index
    int mn = Integer.MIN_VALUE;

    // Stores the minimum count of
    // elements found by repeatedly
    // applying Randomized Binary Search
    int ans = 0;
    for (int i = 0; i < n; i++)
    {

      // If largest element on left side is
      // less than smallest element on right side
      if (mn < arr[i]
          && arr[i] < smallestRight[i + 1])
      {

        // Update ans
        ans++;
      }

      // Update mn
      mn = Math.max(arr[i], mn);
    }
    return ans;
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given array
    int[] arr = new int[] { 5, 4, 9 };

    // Function Call
    System.out.println(getDefiniteFinds(arr));
  }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find minimum count of
# array elements found by repeatedly
# applying Randomized Binary Search
def getDefiniteFinds(arr):

    # Stores count of array elements
    n = len(arr)

    # smallestRight[i]: Stores the smallest
    # array element on the right side of i
    smallestRight = [0] * (n + 1)

    # Update smallestRight[0]
    smallestRight[n] = sys.maxsize

    # Traverse the array from right to left
    for i in range(n - 1, -1, -1):

        # Update smallestRight[i]
        smallestRight[i] = min(
            smallestRight[i + 1], arr[i])

    # Stores the largest element
    # upto i-th index
    mn = -sys.maxsize - 1

    # Stores the minimum count of
    # elements found by repeatedly
    # applying Randomized Binary Search
    ans = 0

    for i in range(n):

        # If largest element on left side is
        # less than smallest element on right side
        if (mn < arr[i] and
        arr[i] < smallestRight[i + 1]):

            # Update ans
            ans += 1

        # Update mn
        mn = max(arr[i], mn)

    return ans

# Driver Code

# Given array
arr = [ 5, 4, 9 ]

# Function Call
print(getDefiniteFinds(arr))

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function to find minimum count of
    // array elements found by repeatedly
    // applying Randomized Binary Search
    static int getDefiniteFinds(int[] arr)
    {

        // Stores count of array elements
        int n = arr.Length;

        // smallestRight[i]: Stores the smallest
        // array element on the right side of i
        int[] smallestRight = new int[n + 1];

        // Update smallestRight[0]
        smallestRight[n] = Int32.MaxValue;

        // Traverse the array from right to left
        for (int i = n - 1; i >= 0; i--)
        {

            // Update smallestRight[i]
            smallestRight[i]
                = Math.Min(smallestRight[i + 1], arr[i]);
        }

        // Stores the largest element
        // upto i-th index
        int mn = Int32.MinValue;

        // Stores the minimum count of
        // elements found by repeatedly
        // applying Randomized Binary Search
        int ans = 0;
        for (int i = 0; i < n; i++)
        {

            // If largest element on left side is
            // less than smallest element on right side
            if (mn < arr[i]
                && arr[i] < smallestRight[i + 1])
            {

                // Update ans
                ans++;
            }

            // Update mn
            mn = Math.Max(arr[i], mn);
        }
        return ans;
    }

    // Driver Code
    static public void Main()
    {

        // Given array
        int[] arr = new int[] { 5, 4, 9 };

        // Function Call
        Console.WriteLine(getDefiniteFinds(arr));
    }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>
// javascript program of the above approach

  // Function to find minimum count of
  // array elements found by repeatedly
  // applying Randomized Binary Search
  function getDefiniteFinds(arr)
  {

    // Stores count of array elements
    let n = arr.length;

    // smallestRight[i]: Stores the smallest
    // array element on the right side of i
    let smallestRight = new Array(n+1).fill(0);

    // Update smallestRight[0]
    smallestRight[n] = Number.MAX_VALUE;

    // Traverse the array from right to left
    for (let i = n - 1; i >= 0; i--)
    {

      // Update smallestRight[i]
      smallestRight[i]
        = Math.min(smallestRight[i + 1], arr[i]);
    }

    // Stores the largest element
    // upto i-th index
    let mn = Number.MIN_VALUE;

    // Stores the minimum count of
    // elements found by repeatedly
    // applying Randomized Binary Search
    let ans = 0;
    for (let i = 0; i < n; i++)
    {

      // If largest element on left side is
      // less than smallest element on right side
      if (mn < arr[i]
          && arr[i] < smallestRight[i + 1])
      {

        // Update ans
        ans++;
      }

      // Update mn
      mn = Math.max(arr[i], mn);
    }
    return ans;
  }

    // Driver Code

   // Given array
    let arr = [ 5, 4, 9 ];

    // Function Call
    document.write(getDefiniteFinds(arr));

 // This code is contributed by chinmoy1997pal.
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)