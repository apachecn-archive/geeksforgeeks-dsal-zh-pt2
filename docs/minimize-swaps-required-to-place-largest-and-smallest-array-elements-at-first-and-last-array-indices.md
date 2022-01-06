# 最小化将最大和最小数组元素放置在第一个和最后一个数组索引处所需的交换

> 原文:[https://www . geesforgeks . org/minimum-swaps-按要求放置最大和最小数组元素-按第一个和最后一个数组索引/](https://www.geeksforgeeks.org/minimize-swaps-required-to-place-largest-and-smallest-array-elements-at-first-and-last-array-indices/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到重新排列数组元素所需的相邻交换的最小计数，使得最大和最小的数组元素分别出现在数组的第一个和最后一个索引上。

**示例:**

> **输入:** arr[] = {33，44，11，12 }
> T3】输出: 2
> **解释:**
> 交换对(arr[0]，arr[1])将 arr[]修改为{44，33，11，12}
> 交换对(arr[2]，arr[3])将 arr[]修改为{44，33，12，11}
> 因此，所需输出为 2。
> 
> **输入:** arr[]={11，12，58，1，78，40，76}
> **输出:** 6

**方法:**按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)计算第一次出现的[最大数组](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)元素 say、 **X** 和最后一次出现的[最小数组元素](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/) say、 **Y** 的索引。
*   移动第一个索引处的最大数组元素所需的相邻交换数等于 **X** 。
*   移动最后一个索引处的最小数组元素所需的相邻交换数等于**N–1–Y**。
*   如果 **X > Y** ，则一个相邻的交换在移动第一个索引处的最大元素和最后一个索引处的最小元素时是常见的。因此，所需的相邻互换总数等于**X+(N–1–Y)–1**。
*   否则，所需的相邻交换总数等于**X+(N–1–Y)**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to  find the minimum count of adjacent
// swaps to move largest and smallest element at the
// first and the last index of the array, respectively
int minimumMoves(int* a, int n)
{

    // Stores the smallest array element
    int min_element = INT_MAX;

    // Stores the smallest array element
    int max_element = INT_MIN;

    // Stores the last occurrence of
    // the smallest array element
    int min_ind = -1;

    // Stores the first occurrence of
    // the largest array element
    int max_ind = -1;

    // Traverse the array arr[]
    for (int i = 0; i < n; i++) {

        // If a[i] is less than
        // min_element
        if (a[i] <= min_element) {

            // Update min_element
            min_element = a[i];

            // Update min_ind
            min_ind = i;
        }

        // If a[i] is greater than
        // max_element
        if (a[i] > max_element) {

            // Update max_element
            max_element = a[i];

            // Update max_ind
            max_ind = i;
        }
    }

    // If max_ind is equal
    // to min_ind
    if (max_ind == min_ind) {
        // Return 0
        return 0;
    }

    // If max_ind is greater than min_ind
    else if (max_ind > min_ind) {

        return max_ind + (n - min_ind - 2);
    }

    // Otherwise
    else {

        return max_ind + n - min_ind - 1;
    }
}

// Driver Code
int main()
{

    // Input
    int arr[] = { 35, 46, 17, 23 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Print the result
    cout << minimumMoves(arr, N) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to  find the minimum count of adjacent
// swaps to move largest and smallest element at the
// first and the last index of the array, respectively
static int minimumMoves(int []a, int n)
{

    // Stores the smallest array element
    int min_element = Integer.MAX_VALUE;

    // Stores the smallest array element
    int max_element = Integer.MIN_VALUE;

    // Stores the last occurrence of
    // the smallest array element
    int min_ind = -1;

    // Stores the first occurrence of
    // the largest array element
    int max_ind = -1;

    // Traverse the array arr[]
    for (int i = 0; i < n; i++)
    {

        // If a[i] is less than
        // min_element
        if (a[i] <= min_element)
        {

            // Update min_element
            min_element = a[i];

            // Update min_ind
            min_ind = i;
        }

        // If a[i] is greater than
        // max_element
        if (a[i] > max_element) {

            // Update max_element
            max_element = a[i];

            // Update max_ind
            max_ind = i;
        }
    }

    // If max_ind is equal
    // to min_ind
    if (max_ind == min_ind) {
        // Return 0
        return 0;
    }

    // If max_ind is greater than min_ind
    else if (max_ind > min_ind) {

        return max_ind + (n - min_ind - 2);
    }

    // Otherwise
    else {

        return max_ind + n - min_ind - 1;
    }
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int arr[] = { 35, 46, 17, 23 };
    int N = arr.length;

    // Print the result
    System.out.print(minimumMoves(arr, N) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys

# Function to  find the minimum count of adjacent
# swaps to move largest and smallest element at the
# first and the last index of the array, respectively
def minimumMoves(a, n):

    # Stores the smallest array element
    min_element = sys.maxsize

    # Stores the smallest array element
    max_element = -sys.maxsize - 1

    # Stores the last occurrence of
    # the smallest array element
    min_ind = -1

    # Stores the first occurrence of
    # the largest array element
    max_ind = -1

    # Traverse the array arr[]
    for i in range(n):

        # If a[i] is less than
        # min_element
        if (a[i] <= min_element):

            # Update min_element
            min_element = a[i]

            # Update min_ind
            min_ind = i

        # If a[i] is greater than
        # max_element
        if (a[i] > max_element):

            # Update max_element
            max_element = a[i]

            # Update max_ind
            max_ind = i

    # If max_ind is equal
    # to min_ind
    if (max_ind == min_ind):

        # Return 0
        return 0

    # If max_ind is greater than min_ind
    elif(max_ind > min_ind):
        return max_ind + (n - min_ind - 2)

    # Otherwise
    else:
        return max_ind + n - min_ind - 1

# Driver Code
if __name__ == '__main__':

    # Input
    arr =  [35, 46, 17, 23]
    N = len(arr)

    # Print the result
    print(minimumMoves(arr, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to  find the minimum count of adjacent
  // swaps to move largest and smallest element at the
  // first and the last index of the array, respectively
  static int minimumMoves(int []a, int n)
  {

    // Stores the smallest array element
    int min_element = int.MaxValue;

    // Stores the smallest array element
    int max_element = int.MinValue;

    // Stores the last occurrence of
    // the smallest array element
    int min_ind = -1;

    // Stores the first occurrence of
    // the largest array element
    int max_ind = -1;

    // Traverse the array []arr
    for (int i = 0; i < n; i++)
    {

      // If a[i] is less than
      // min_element
      if (a[i] <= min_element)
      {

        // Update min_element
        min_element = a[i];

        // Update min_ind
        min_ind = i;
      }

      // If a[i] is greater than
      // max_element
      if (a[i] > max_element)
      {

        // Update max_element
        max_element = a[i];

        // Update max_ind
        max_ind = i;
      }
    }

    // If max_ind is equal
    // to min_ind
    if (max_ind == min_ind)
    {

      // Return 0
      return 0;
    }

    // If max_ind is greater than min_ind
    else if (max_ind > min_ind)
    {
      return max_ind + (n - min_ind - 2);
    }

    // Otherwise
    else
    {
      return max_ind + n - min_ind - 1;
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Input
    int []arr = { 35, 46, 17, 23 };
    int N = arr.Length;

    // Print the result
    Console.Write(minimumMoves(arr, N) +"\n");
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program of the above approach

// Function to  find the minimum count of adjacent
// swaps to move largest and smallest element at the
// first and the last index of the array, respectively
function minimumMoves(a, n)
{

    // Stores the smallest array element
    let min_element = Number.MAX_VALUE;

    // Stores the smallest array element
    let max_element = Number.MIN_VALUE;

    // Stores the last occurrence of
    // the smallest array element
    let min_ind = -1;

    // Stores the first occurrence of
    // the largest array element
    let max_ind = -1;

    // Traverse the array arr[]
    for (let i = 0; i < n; i++)
    {

        // If a[i] is less than
        // min_element
        if (a[i] <= min_element)
        {

            // Update min_element
            min_element = a[i];

            // Update min_ind
            min_ind = i;
        }

        // If a[i] is greater than
        // max_element
        if (a[i] > max_element) {

            // Update max_element
            max_element = a[i];

            // Update max_ind
            max_ind = i;
        }
    }

    // If max_ind is equal
    // to min_ind
    if (max_ind == min_ind) {
        // Return 0
        return 0;
    }

    // If max_ind is greater than min_ind
    else if (max_ind > min_ind) {

        return max_ind + (n - min_ind - 2);
    }

    // Otherwise
    else {

        return max_ind + n - min_ind - 1;
    }
}

    // Driver Code

       // Input
    let arr = [ 35, 46, 17, 23 ];
    let N = arr.length;

    // Print the result
    document.write(minimumMoves(arr, N) +"\n");

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)