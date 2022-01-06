# 给定阵列中峰值元素之间的最小距离

> 原文:[https://www . geesforgeks . org/给定阵列中峰间元素的最小距离/](https://www.geeksforgeeks.org/minimum-distance-between-peak-elements-in-a-given-array/)

给定一个[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到给定阵中两个[峰元素](https://www.geeksforgeeks.org/find-a-peak-in-a-given-array/)之间的最小距离。

**示例:**

> **输入:** arr[] = {2，3，1，2，4，1，2}
> **输出:** 2
> **说明:**给定数组中的峰元素为{2， **3** ，1，2， **4** ，1， **2** }。因此，4 和 2 之间的距离是(6–4)= 2，这是最小可能的距离。
> 
> **输入:** arr[] = {1，2}
> **输出:** -1
> **说明:**给定数组中只有一个峰元素。

**方法:**给定的问题可以通过观察这样一个事实来解决:为了使距离最小，只需要考虑相邻的[峰元素](https://www.geeksforgeeks.org/find-a-peak-in-a-given-array/)的距离。因此，[迭代给定的数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，对于每个峰值元素，计算它与最后找到的峰值元素的距离，该峰值元素的索引可以保持在变量 **idx** 中。所有这些距离中的最小值就是所需的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum distance
// between two peak elements
void MinimumDistance(int arr[], int n)
{

    // Stores the minimum distance between
    // two peak elements
    int mn = INT_MAX;

    // Store the index of peak element
    int idx = -1;

    // Checking for the 1st elements of array
    if (arr[0] >= arr[1]) {
        idx = 0;
    }
    for (int i = 1; i < n - 1; i++) {
        if (arr[i] >= arr[i - 1]
            && arr[i] >= arr[i + 1]) {
            if (idx == -1) {
                idx = i;
            }
            else {
                mn = min(mn, i - idx);
            }
            idx = i;
        }
    }

    // Checking for last element of the array
    if (arr[n - 1] >= arr[n - 2] && idx != -1) {
        mn = min(mn, n - 1 - idx);
    }

    // If number of peak elements is less than 2
    if (mn == INT_MAX)
        cout << -1;

    // Print Answer
    else
        cout << mn;
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 1, 2, 4, 1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    MinimumDistance(arr, n);

    return 0;
}

// This code is contributed by Samim Hossain Mondal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
import java.util.*;
class GFG {

    // Function to find the minimum distance
    // between two peak elements
    public static void MinimumDistance(int[] arr)
    {
        // Stores the minimum distance between
        // two peak elements
        int min = Integer.MAX_VALUE;

        // Store the index of peak element
        int idx = -1;
        int n = arr.length;

        // Checking for the 1st elements of array
        if (arr[0] >= arr[1]) {
            idx = 0;
        }
        for (int i = 1; i < n - 1; i++) {
            if (arr[i] >= arr[i - 1]
                && arr[i] >= arr[i + 1]) {
                if (idx == -1) {
                    idx = i;
                }
                else {
                    min = Math.min(min, i - idx);
                }
                idx = i;
            }
        }

        // Checking for last element of the array
        if (arr[n - 1] >= arr[n - 2] && idx != -1) {
            min = Math.min(min, n - 1 - idx);
        }

        // If number of peak elements is less than 2
        if (min == Integer.MAX_VALUE)
            System.out.println(-1);

        // Print Answer
        else
            System.out.println(min);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 1, 2, 4, 1, 2 };
        MinimumDistance(arr);
    }
}
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to find the minimum distance
# between two peak elements
def MinimumDistance(arr):

  # Stores the minimum distance between
  # two peak elements
  less = 10**9;

  # Store the index of peak element
  idx = -1;
  n = len(arr);

  # Checking for the 1st elements of array
  if (arr[0] >= arr[1]):
    idx = 0;

  for i in range(1, n - 1):
    if (arr[i] >= arr[i - 1] and arr[i] >= arr[i + 1]):
      if (idx == -1):
        idx = i;
      else:
        less = min(less, i - idx);
      idx = i;

  # Checking for last element of the array
  if (arr[n - 1] >= arr[n - 2] and idx != -1):
    less = min(less, n - 1 - idx);

  # If number of peak elements is less than 2
  if (less == 10**9):
    print(-1);

  # Prlet Answer
  else:
    print(less);

# Driver Code

arr = [2, 3, 1, 2, 4, 1, 2];
MinimumDistance(arr);

# This code is contributed by gfgking
```

## C#

```
// C# implementation of the above approach
using System;
class GFG
{

    // Function to find the minimum distance
    // between two peak elements
    public static void MinimumDistance(int[] arr)
    {

        // Stores the minimum distance between
        // two peak elements
        int min = int.MaxValue;

        // Store the index of peak element
        int idx = -1;
        int n = arr.Length;

        // Checking for the 1st elements of array
        if (arr[0] >= arr[1])
        {
            idx = 0;
        }
        for (int i = 1; i < n - 1; i++)
        {
            if (arr[i] >= arr[i - 1]
                && arr[i] >= arr[i + 1])
            {
                if (idx == -1)
                {
                    idx = i;
                }
                else
                {
                    min = Math.Min(min, i - idx);
                }
                idx = i;
            }
        }

        // Checking for last element of the array
        if (arr[n - 1] >= arr[n - 2] && idx != -1)
        {
            min = Math.Min(min, n - 1 - idx);
        }

        // If number of peak elements is less than 2
        if (min == int.MaxValue)
            Console.Write(-1);

        // Print Answer
        else
            Console.Write(min);
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 2, 3, 1, 2, 4, 1, 2 };
        MinimumDistance(arr);
    }
}

// This code is contributed by gfgking
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the minimum distance
// between two peak elements
function MinimumDistance(arr) {
  // Stores the minimum distance between
  // two peak elements
  let min = Number.MAX_SAFE_INTEGER;

  // Store the index of peak element
  let idx = -1;
  let n = arr.length;

  // Checking for the 1st elements of array
  if (arr[0] >= arr[1]) {
    idx = 0;
  }
  for (let i = 1; i < n - 1; i++) {
    if (arr[i] >= arr[i - 1]
      && arr[i] >= arr[i + 1]) {
      if (idx == -1) {
        idx = i;
      }
      else {
        min = Math.min(min, i - idx);
      }
      idx = i;
    }
  }

  // Checking for last element of the array
  if (arr[n - 1] >= arr[n - 2] && idx != -1) {
    min = Math.min(min, n - 1 - idx);
  }

  // If number of peak elements is less than 2
  if (min == Number.MAX_SAFE_INTEGER)
    document.write(-1);

  // Prlet Answer
  else
    document.write(min);
}

// Driver Code

let arr = [2, 3, 1, 2, 4, 1, 2];
MinimumDistance(arr);
// This code is contributed by gfgking

</script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O (1)