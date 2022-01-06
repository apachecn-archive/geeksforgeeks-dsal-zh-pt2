# 使阵列不减少所需的不减少子阵列的最小增量

> 原文:[https://www . geeksforgeeks . org/非递减子数组的最小增量-要求使数组非递减/](https://www.geeksforgeeks.org/minimum-increments-of-non-decreasing-subarrays-required-to-make-array-non-decreasing/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找到使数组不递减所需的最小操作数，其中，每个操作包括将给定数组中不递减子数组的所有元素递增 **1** 。

**示例:**

> **输入:** arr[] = {1，3，1，2，4}
> **输出:** 2
> **解释:**
> 操作 1:递增 arr[2]将数组修改为{1，3，2，2，4}
> 操作 2:递增子数组{arr[2]，arr[3]}将数组修改为{1，3，3，4}
> 因此，最终的数组是非递减的。
> **输入:** arr[] = {1，3，5，10}
> **输出:** 0
> **说明:**数组已经不减了。

**方法:**按照以下步骤解决问题:

*   如果阵列已经是非递减阵列，则不需要更改。
*   否则，对于任何指数 **i** ，其中 **0 ≤ i < N** ，如果**arr【I】>arr【I+1】**，将差值加到**和**上。
*   最后打印 **ans** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return to the minimum
// number of operations required to
// make the array non-decreasing
int getMinOps(int arr[], int n)
{

    // Stores the count of operations
    int ans = 0;
    for(int i = 0; i < n - 1; i++)
    {

        // If arr[i] > arr[i + 1], add
        // arr[i] - arr[i + 1] to the answer
        // Otherwise, add 0
        ans += max(arr[i] - arr[i + 1], 0);
    }
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 1, 2, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << (getMinOps(arr, n));
}

// This code is contributed by PrinciRaj1992
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement the
// above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to return to the minimum
    // number of operations required to
    // make the array non-decreasing
    public static int getMinOps(int[] arr)
    {
        // Stores the count of operations
        int ans = 0;
        for (int i = 0; i < arr.length - 1; i++) {

            // If arr[i] > arr[i + 1], add
            // arr[i] - arr[i + 1] to the answer
            // Otherwise, add 0
            ans += Math.max(arr[i] - arr[i + 1], 0);
        }

        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 3, 1, 2, 4 };

        System.out.println(getMinOps(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to return to the minimum
# number of operations required to
# make the array non-decreasing
def getMinOps(arr):

    # Stores the count of operations
    ans = 0

    for i in range(len(arr) - 1):

        # If arr[i] > arr[i + 1], add
        # arr[i] - arr[i + 1] to the answer
        # Otherwise, add 0
        ans += max(arr[i] - arr[i + 1], 0)

    return ans

# Driver Code

# Given array arr[]
arr = [ 1, 3, 1, 2, 4 ]

# Function call
print(getMinOps(arr))

# This code is contributed by Shivam Singh
```

## C#

```
// C# Program to implement the
// above approach
using System;
class GFG
{

  // Function to return to the minimum
  // number of operations required to
  // make the array non-decreasing
  public static int getMinOps(int[] arr)
  {
    // Stores the count of operations
    int ans = 0;
    for (int i = 0; i < arr.Length - 1; i++)
    {

      // If arr[i] > arr[i + 1], add
      // arr[i] - arr[i + 1] to the answer
      // Otherwise, add 0
      ans += Math.Max(arr[i] - arr[i + 1], 0);
    }
    return ans;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int[] arr = { 1, 3, 1, 2, 4 };

    Console.WriteLine(getMinOps(arr));
  }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Java Script  Program to implement the
// above approach

    // Function to return to the minimum
    // number of operations required to
    // make the array non-decreasing
    function getMinOps( arr)
    {
        // Stores the count of operations
        let ans = 0;
        for (let i = 0; i < arr.length - 1; i++) {

            // If arr[i] > arr[i + 1], add
            // arr[i] - arr[i + 1] to the answer
            // Otherwise, add 0
            ans += Math.max(arr[i] - arr[i + 1], 0);
        }

        return ans;
    }

    // Driver Code

        let arr = [ 1, 3, 1, 2, 4 ];

        document.write(getMinOps(arr));

//contributed by bobby

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)