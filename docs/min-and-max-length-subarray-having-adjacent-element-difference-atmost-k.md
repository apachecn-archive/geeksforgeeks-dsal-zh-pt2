# 具有相邻元素差异的子阵列的最小和最大长度 K

> 原文:[https://www . geesforgeks . org/min-and-max-length-subarray-having-element-difference-Atmos-k/](https://www.geeksforgeeks.org/min-and-max-length-subarray-having-adjacent-element-difference-atmost-k/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是找到最大和最小长度的子数组，使得相邻元素之间的差值最多为 K.
**示例:**

> **输入:** arr[] = {2，4，6}，K = 2
> **输出:** 3，3
> **解释:**
> 最小和最大长度子数组，使得相邻元素之间的差异
> 最多为 3，即{2，4，2}
> **输入:** arr[] = {2，3，6，7，8}，K = 2
> **输出:** 2，3

**方法:**思路是[遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，从每个元素开始，向其左右方向移动，直到相邻元素之差小于 k，最后用当前长度更新最大和最小长度子数组，定义如下–

```
if (current_length  maximum_length)
   maximum_length = current_length
```

以下是上述方法的实现:

## C++

```
// C++ program to find the minimum
// and maximum length subarray such
// that difference between adjacent
// elements is atmost K

#include <iostream>

using namespace std;

// Function to find the maximum and
// minimum length subarray
void findMaxMinSubArray(int arr[],
                        int K, int n)
{
    // Initialise minimum and maximum
    // size of subarray in worst case
    int min = n;
    int max = 0;

    // Left will scan the size of
    // possible subarray in left
    // of selected element
    int left;

    // Right will scan the size of
    // possible subarray in right
    // of selected element
    int right;

    // Temp will store size of group
    // associateed with every element
    int tmp;

    // Loop to find size of subarray
    // for every element of array
    for (int i = 0; i < n; i++) {
        tmp = 1;
        left = i;

        // Left will move in left direction
        // and compare difference between
        // itself and element left to it
        while (left - 1 >= 0
               && abs(arr[left] - arr[left - 1])
                      <= K) {
            left--;
            tmp++;
        }

        // right will move in right direction
        // and compare difference between
        // itself and element right to it
        right = i;
        while (right + 1 <= n - 1
               && abs(arr[right] - arr[right + 1])
                      <= K) {
            right++;
            tmp++;
        }

        // if subarray of much lesser or much
        // greater is found than yet
        // known then update
        if (min > tmp)
            min = tmp;
        if (max < tmp)
            max = tmp;
    }

    // Print minimum and maximum
    // possible size of subarray
    cout << min << ", "
         << max << endl;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 5, 6, 7 };
    int K = 2;
    int n = sizeof(arr) / sizeof(arr[0]);

    // function call to find maximum
    // and minimum possible sub array
    findMaxMinSubArray(arr, K, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// and maximum length subarray such
// that difference between adjacent
// elements is atmost K
import java.io.*;
import java.util.*;

class GFG {

// Function to find the maximum and
// minimum length subarray
static void findMaxMinSubArray(int arr[],
                               int K, int n)
{

    // Initialise minimum and maximum
    // size of subarray in worst case
    int min = n;
    int max = 0;

    // Left will scan the size of
    // possible subarray in left
    // of selected element
    int left;

    // Right will scan the size of
    // possible subarray in right
    // of selected element
    int right;

    // Temp will store size of group
    // associateed with every element
    int tmp;

    // Loop to find size of subarray
    // for every element of array
    for(int i = 0; i < n; i++)
    {
       tmp = 1;
       left = i;

       // Left will move in left direction
       // and compare difference between
       // itself and element left to it
       while (left - 1 >= 0 &&
              Math.abs(arr[left] -
                       arr[left - 1]) <= K)
       {
           left--;
           tmp++;
       }

       // Right will move in right direction
       // and compare difference between
       // itself and element right to it
       right = i;

       while (right + 1 <= n - 1 &&
              Math.abs(arr[right] -
                       arr[right + 1]) <= K)
       {
           right++;
           tmp++;
       }

       // If subarray of much lesser or much
       // greater is found than yet
       // known then update
       if (min > tmp)
           min = tmp;
       if (max < tmp)
           max = tmp;
    }

    // Print minimum and maximum
    // possible size of subarray
    System.out.print(min);
    System.out.print(", ");
    System.out.print(max);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 5, 6, 7 };
    int K = 2;
    int n = arr.length;

    // Function call to find maximum
    // and minimum possible sub array
    findMaxMinSubArray(arr, K, n);
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# and maximum length subarray such
# that difference between adjacent
# elements is atmost K

# Function to find the maximum and
# minimum length subarray
def findMaxMinSubArray(arr, K, n):

    # Initialise minimum and maximum
    # size of subarray in worst case
    min = n
    max = 0

    # Left will scan the size of
    # possible subarray in left
    # of selected element
    left = 0

    # Right will scan the size of
    # possible subarray in right
    # of selected element
    right = n

    # Temp will store size of group
    # associateed with every element
    tmp = 0

    # Loop to find size of subarray
    # for every element of array
    for i in range(0, n):
        tmp = 1
        left = i

        # Left will move in left direction
        # and compare difference between
        # itself and element left to it
        while (left - 1 >= 0 and
               abs(arr[left] -
                   arr[left - 1]) <= K):

            left = left - 1
            tmp = tmp + 1

        # Right will move in right direction
        # and compare difference between
        # itself and element right to it
        right = i
        while (right + 1 <= n - 1 and
               abs(arr[right] -
                   arr[right + 1]) <= K):

            right = right + 1
            tmp = tmp + 1

        # If subarray of much lesser or much
        # greater is found than yet
        # known then update
        if (min > tmp):
            min = tmp
        if (max < tmp):
            max = tmp

    # Print minimum and maximum
    # possible size of subarray
    print(min, end = ', ')
    print(max, end = '\n')

# Driver Code
arr = [ 1, 2, 5, 6, 7 ]
K = 2
n = len(arr)

# Function call to find maximum
# and minimum possible sub array
findMaxMinSubArray(arr, K, n)

# This code is contributed by Pratik
```

## C#

```
// C# program to find the minimum
// and maximum length subarray such
// that difference between adjacent
// elements is atmost K
using System;
class GFG{

// Function to find the maximum and
// minimum length subarray
static void findMaxMinSubArray(int[] arr,
                               int K, int n)
{

    // Initialise minimum and maximum
    // size of subarray in worst case
    int min = n;
    int max = 0;

    // Left will scan the size of
    // possible subarray in left
    // of selected element
    int left;

    // Right will scan the size of
    // possible subarray in right
    // of selected element
    int right;

    // Temp will store size of group
    // associateed with every element
    int tmp;

    // Loop to find size of subarray
    // for every element of array
    for(int i = 0; i < n; i++)
    {
       tmp = 1;
       left = i;

       // Left will move in left direction
       // and compare difference between
       // itself and element left to it
       while (left - 1 >= 0 &&
              Math.Abs(arr[left] -
                       arr[left - 1]) <= K)
       {
           left--;
           tmp++;
       }

       // Right will move in right direction
       // and compare difference between
       // itself and element right to it
       right = i;
       while (right + 1 <= n - 1 &&
              Math.Abs(arr[right] -
                       arr[right + 1]) <= K)
       {
        right++;
        tmp++;
       }

       // If subarray of much lesser or much
       // greater is found than yet
       // known then update
       if (min > tmp)
           min = tmp;
       if (max < tmp)
           max = tmp;
    }

    // Print minimum and maximum
    // possible size of subarray
    Console.Write(min);
    Console.Write(", ");
    Console.Write(max);
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 2, 5, 6, 7 };
    int K = 2;
    int n = arr.Length;

    // Function call to find maximum
    // and minimum possible sub array
    findMaxMinSubArray(arr, K, n);
}
}

// This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>
// Java Script program to find the minimum
// and maximum length subarray such
// that difference between adjacent
// elements is atmost K

// Function to find the maximum and
// minimum length subarray
function findMaxMinSubArray(arr, k, n)
{

    // Initialise minimum and maximum
    // size of subarray in worst case
    let min = n;
    let max = 0;

    // Left will scan the size of
    // possible subarray in left
    // of selected element
    let left;

    // Right will scan the size of
    // possible subarray in right
    // of selected element
    let right;

    // Temp will store size of group
    // associateed with every element
    let tmp;

    // Loop to find size of subarray
    // for every element of array
    for(let i = 0; i < n; i++)
    {
    tmp = 1;
    left = i;

    // Left will move in left direction
    // and compare difference between
    // itself and element left to it
    while (left - 1 >= 0 &&
            Math.abs(arr[left] -
                    arr[left - 1]) <= K)
    {
        left--;
        tmp++;
    }

    // Right will move in right direction
    // and compare difference between
    // itself and element right to it
    right = i;

    while (right + 1 <= n - 1 &&
            Math.abs(arr[right] -
                    arr[right + 1]) <= K)
    {
        right++;
        tmp++;
    }

    // If subarray of much lesser or much
    // greater is found than yet
    // known then update
    if (min > tmp)
        min = tmp;
    if (max < tmp)
        max = tmp;
    }

    // Print minimum and maximum
    // possible size of subarray
    document.write(min);
    document.write(", ");
    document.write(max);
}

// Driver code

    let arr = [1, 2, 5, 6, 7 ];
    let K = 2;
    let n = arr.length;

    // Function call to find maximum
    // and minimum possible sub array
    findMaxMinSubArray(arr, K, n);

// This code is contributed by sravan
</script>
```

**Output:** 

```
2, 3
```