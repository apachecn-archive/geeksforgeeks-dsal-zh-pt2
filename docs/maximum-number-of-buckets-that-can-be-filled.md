# 可灌装的最大桶数

> 原文:[https://www . geesforgeks . org/最大可灌装桶数/](https://www.geeksforgeeks.org/maximum-number-of-buckets-that-can-be-filled/)

给定一个由 **N** 个桶的容量组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，其中 **arr[i]** 表示第 **i <sup>个</sup>** 个桶的容量。如果可用水的总量是数组索引的总和(*基于 1 的索引*)，任务是找到可用水可以完全充满的最大桶数。

**示例:**

> **输入:** arr[] = {1，5，3，4，7，9}
> **输出:** 4
> **说明:**
> 总可利用水量= arr[]= 1+2+3+4+5 的 arrayindices 之和= 15。
> 按升序对数组进行排序会将数组修改为{1，3，4，5，7，9}。
> 然后将容量为 1 的铲斗装满。现在，可用水量= 14。
> 装满容量为 3 的铲斗。现在，可用水量= 11。
> 容量为 4 的灌装桶。现在，可用水量= 7。
> 容量为 5 的灌装桶。现在，可用水量= 2。
> 因此，能装满水的水桶总数为 4 个。
> 
> **输入:** arr[] = {2，5，8，3，2，10，8 }
> T3】输出: 5

**进场:**给定的问题可以解决[贪婪地](https://www.geeksforgeeks.org/greedy-algorithms/)。按照以下步骤解决给定的问题:

*   通过计算第一个 **N 个**自然数的[和来计算总水资源量。](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)
*   [按升序排列数组**arr[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并找到数组元素的[和直到该索引，比如 **i** ，其中和超过了总可用性。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   完成上述步骤后，打印索引 **i** 的值作为可填充的最大桶数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of buckets that can be filled with
// the amount of water available
int getBuckets(int arr[], int N)
{
    // Find the total available water
    int availableWater = N * (N - 1) / 2;

    // Sort the array in ascending order
    sort(arr, arr + N);

    int i = 0, sum = 0;

    // Check if bucket can be
    // filled with available water
    while (sum <= availableWater) {
        sum += arr[i];
        i++;
    }

    // Print count of buckets
    cout << i - 1;
}

// Driver Code
int main()
{
    int arr[] = { 1, 5, 3, 4, 7, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);

    getBuckets(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

  // Function to find the maximum number
  // of buckets that can be filled with
  // the amount of water available
  static void getBuckets(int[] arr, int N)
  {
    // Find the total available water
    int availableWater = N * (N - 1) / 2;

    // Sort the array in ascending order
    Arrays.sort(arr);

    int i = 0, sum = 0;

    // Check if bucket can be
    // filled with available water
    while (sum <= availableWater) {
      sum += arr[i];
      i++;
    }

    // Print count of buckets
    System.out.println(i - 1);
  }

  // Driver code
  public static void main(String[] args)
  {
    int[] arr = { 1, 5, 3, 4, 7, 9 };
    int N = arr.length;

    getBuckets(arr, N);
  }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum number
# of buckets that can be filled with
# the amount of water available
def getBuckets(arr, N) :

    # Find the total available water
    availableWater = N * (N - 1) // 2

    # Sort the array in ascending order
    arr.sort()

    i, Sum = 0, 0

    # Check if bucket can be
    # filled with available water
    while (Sum <= availableWater) :
        Sum += arr[i]
        i += 1

    # Print count of buckets
    print(i - 1, end = "")

arr = [ 1, 5, 3, 4, 7, 9 ]
N = len(arr)

getBuckets(arr, N);

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG
{

  // Function to find the maximum number
  // of buckets that can be filled with
  // the amount of water available
  static void getBuckets(int[] arr, int N)
  {

    // Find the total available water
    int availableWater = N * (N - 1) / 2;

    // Sort the array in ascending order
    Array.Sort(arr);
    int i = 0, sum = 0;

    // Check if bucket can be
    // filled with available water
    while (sum <= availableWater)
    {
      sum += arr[i];
      i++;
    }

    // Print count of buckets
    Console.Write(i - 1);
  }

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 1, 5, 3, 4, 7, 9 };
    int N = arr.Length;

    getBuckets(arr, N);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

    // Javascript program to implement
    // the above approach

    // Function to find the maximum number
    // of buckets that can be filled with
    // the amount of water available
    function getBuckets(arr, N)
    {

      // Find the total available water
      let availableWater = N * (N - 1) / 2;

      // Sort the array in ascending order
      arr.sort(function(a, b){return a - b});
      let i = 0, sum = 0;

      // Check if bucket can be
      // filled with available water
      while (sum <= availableWater)
      {
        sum += arr[i];
        i++;
      }

      // Print count of buckets
      document.write(i - 1);
    }

    let arr = [ 1, 5, 3, 4, 7, 9 ];
    let N = arr.length;

    getBuckets(arr, N);

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*