# 一个数组中不同的三元组对之间绝对差的最大和

> 原文:[https://www . geeksforgeeks . org/数组中三个不同对之间的最大绝对差值总和/](https://www.geeksforgeeks.org/maximum-sum-of-absolute-differences-between-distinct-pairs-of-a-triplet-from-an-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出数组中所有不同的[三元组](https://www.geeksforgeeks.org/find-a-triplet-that-sum-to-a-given-value/)对之间的绝对差的最大和。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 6
> **解释:**
> 有效三元组为(1，3，4)作为和= | 1–4 |+| 1–3 |+| 3–4 | = 6，是所有三元组中最大的。
> 
> **输入:** arr[] = {2，2，2 }
> T3】输出: 0

**方法:**解决给定问题的思路是[按升序排序数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)，求[数组](https://www.geeksforgeeks.org/array-data-structure/)的前、后两个元素对的绝对差之和。按照以下步骤解决问题:

*   初始化一个变量，比如**和**，来存储最大可能的和。
*   [按升序排列给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **arr[]** 。
*   求[数组](https://www.geeksforgeeks.org/array-data-structure/)的第一个和最后两个元素对之间的差的和，即**和=(arr[N–2]–arr[0])+(arr[N–1]–arr[0])+(arr[N–2]–arr[N–1])**。
*   完成以上步骤后，打印**和**的值作为结果**。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// absolute differences between
// distinct pairs of triplet in array
void maximumSum(int arr[], int N)
{
    // Stores the maximum sum
    int sum;

    // Sort the array in
    // ascending order
    sort(arr, arr + N);

    // Sum of differences between
    // pairs of the triplet
    sum = (arr[N - 1] - arr[0])
          + (arr[N - 2] - arr[0])
          + (arr[N - 1] - arr[N - 2]);

    // Print the sum
    cout << sum;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 4, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    maximumSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to find the maximum sum of
  // absolute differences between
  // distinct pairs of triplet in array
  static void maximumSum(int[] arr, int N)
  {

    // Stores the maximum sum
    int sum;

    // Sort the array in
    // ascending order
    Arrays.sort(arr);

    // Sum of differences between
    // pairs of the triplet
    sum = (arr[N - 1] - arr[0]) + (arr[N - 2] - arr[0])
      + (arr[N - 1] - arr[N - 2]);

    // Print the sum
    System.out.println(sum);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int[] arr = { 1, 3, 4, 2 };
    int N = arr.length;
    maximumSum(arr, N);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the maximum sum of
# absolute differences between
# distinct pairs of triplet in array
def maximumSum(arr, N):

    # Stores the maximum sum
    sum = 0

    # Sort the array in
    # ascending order
    arr.sort()

    # Sum of differences between
    # pairs of the triplet
    sum = (arr[N - 1] - arr[0]) + (arr[N - 2] - arr[0]) + (arr[N - 1] - arr[N - 2]);

    # Print the sum
    print(sum)

# Driver Code
arr = [ 1, 3, 4, 2 ]
N = len(arr)
maximumSum(arr, N)

# This code is contributed by rohitsingh07052.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find the maximum sum of
    // absolute differences between
    // distinct pairs of triplet in array
    static void maximumSum(int[] arr, int N)
    {

        // Stores the maximum sum
        int sum;

        // Sort the array in
        // ascending order
        Array.Sort(arr);

        // Sum of differences between
        // pairs of the triplet
        sum = (arr[N - 1] - arr[0]) + (arr[N - 2] - arr[0])
              + (arr[N - 1] - arr[N - 2]);

        // Print the sum
        Console.Write(sum);
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 3, 4, 2 };
        int N = arr.Length;
        maximumSum(arr, N);
    }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the maximum sum of
// absolute differences between
// distinct pairs of triplet in array
function maximumSum(arr, N)
{
    // Stores the maximum sum
    let sum;

    // Sort the array in
    // ascending order
    arr.sort();

    // Sum of differences between
    // pairs of the triplet
    sum = (arr[N - 1] - arr[0])
        + (arr[N - 2] - arr[0])
        + (arr[N - 1] - arr[N - 2]);

    // Print the sum
    document.write(sum);
}

// Driver Code

    let arr = [ 1, 3, 4, 2 ];
    let N = arr.length;
    maximumSum(arr, N);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*