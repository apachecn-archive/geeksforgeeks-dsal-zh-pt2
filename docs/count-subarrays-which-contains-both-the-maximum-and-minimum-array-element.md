# 计数包含最大和最小阵列元素的子阵列

> 原文:[https://www . geesforgeks . org/count-subarrays-其中包含最大和最小数组元素/](https://www.geeksforgeeks.org/count-subarrays-which-contains-both-the-maximum-and-minimum-array-element/)

给定一个由 **N** 个不同整数组成的数组 **arr[]** ，任务是从给定的数组中找出包含最大和最小元素的子数组的数量。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 1
> **解释:**
> 只有单个子阵列{1，2，3，4}由最大值(= 4)和最小值(= 1)数组元素组成。
> 
> **输入:** arr[] = {4，1，2，3}
> **输出:** 3
> **解释:**
> 子阵{4，1}、{4，1，2}、{4，1，2，3}由最大值(= 4)和最小值(= 1)数组元素组成。

**天真法:**最简单的方法是，首先[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)找到数组的最大值和[最小值，然后](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)[生成给定数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的所有可能的子数组。对于每个子阵列，检查其是否包含 ***最大*** 和 ***最小*** 阵列元素。对于所有这样的子阵列，将计数增加 1。最后，打印此类子阵列的计数。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**按照以下步骤优化上述方法:

*   找到 ***最大*** 和 ***最小*** 元素的索引。让 **i** 和 **j** 分别作为指标，使得 **i < j** 。
*   从索引开始直到 **i** 并在 **j** 之后的索引处结束的所有子阵列将包含最大和最小阵列元素。
*   因此，子阵列起始指标的可能指标为**【0，I】**(合计= **i + 1** )。
*   因此，子阵列结束指标的可能指标为**【j，N–1】**(合计=**N–j**)。
*   因此，子阵列的计数由**(I+1)*(N–j)**给出。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count subarray
// containing  both maximum and
// minimum array elements
int countSubArray(int arr[], int n)
{
    // If the length of the
    // array is less than 2
    if (n < 2)
        return n;

    // Find the index of maximum element
    int i
        = max_element(arr, arr + n) - arr;

    // Find the index of minimum element
    int j
        = min_element(arr, arr + n) - arr;

    // If i > j, then swap
    // the value of i and j
    if (i > j)
        swap(i, j);

    // Return the answer
    return (i + 1) * (n - j);
}

// Driver Code
int main()
{
    int arr[] = { 4, 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    // Function call
    cout << countSubArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to count subarray
// containing both maximum and
// minimum array elements
static int countSubArray(int arr[], int n)
{

    // If the length of the
    // array is less than 2
    if (n < 2)
        return n;

    // Find the index of maximum element
    int i = max_element(arr);

    // Find the index of minimum element
    int j = min_element(arr);

    // If i > j, then swap
    // the value of i and j
    if (i > j)
    {
        int tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    }

    // Return the answer
    return (i + 1) * (n - j);
}

// Function to return max_element index
static int max_element(int[] arr)
{
    int idx = 0;
    int max = arr[0];
    for(int i = 1; i < arr.length; i++)
    {
        if(max < arr[i])
        {
            max = arr[i];
            idx = i;
        }
    }
    return idx;
}

// Function to return min_element index
static int min_element(int[] arr)
{
    int idx = 0;
    int min = arr[0];
    for(int i = 1; i < arr.length; i++)
    {
        if (arr[i] < min)
        {
            min = arr[i];
            idx = i;
        }
    }
    return idx;
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 4, 1, 2, 3 };
    int n = arr.length;

    // Function call
    System.out.println(countSubArray(arr, n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to count subarray
# containing both maximum and
# minimum array elements
def countSubArray(arr, n):

    # If the length of the
    # array is less than 2
    if (n < 2):
        return n;

    # Find the index of
    # maximum element
    i = max_element(arr);

    # Find the index of
    # minimum element
    j = min_element(arr);

    # If i > j, then swap
    # the value of i and j
    if (i > j):
        tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;

    # Return the answer
    return (i + 1) * (n - j);

# Function to return
# max_element index
def max_element(arr):
    idx = 0;
    max = arr[0];

    for i in range(1, len(arr)):
        if (max < arr[i]):
            max = arr[i];
            idx = i;
    return idx;

# Function to return
# min_element index
def min_element(arr):
    idx = 0;
    min = arr[0];

    for i in range(1, len(arr)):
        if (arr[i] < min):
            min = arr[i];
            idx = i;

    return idx;

# Driver Code
if __name__ == '__main__':
    arr = [4, 1, 2, 3];
    n = len(arr);

    # Function call
    print(countSubArray(arr, n));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to count subarray
// containing both maximum and
// minimum array elements
static int countSubArray(int []arr,
                         int n)
{   
  // If the length of the
  // array is less than 2
  if (n < 2)
    return n;

  // Find the index of maximum element
  int i = max_element(arr);

  // Find the index of minimum element
  int j = min_element(arr);

  // If i > j, then swap
  // the value of i and j
  if (i > j)
  {
    int tmp = arr[i];
    arr[i] = arr[j];
    arr[j] = tmp;
  }

  // Return the answer
  return (i + 1) * (n - j);
}

// Function to return max_element index
static int max_element(int[] arr)
{
  int idx = 0;
  int max = arr[0];
  for(int i = 1; i < arr.Length; i++)
  {
    if(max < arr[i])
    {
      max = arr[i];
      idx = i;
    }
  }
  return idx;
}

// Function to return min_element index
static int min_element(int[] arr)
{
  int idx = 0;
  int min = arr[0];
  for(int i = 1; i < arr.Length; i++)
  {
    if (arr[i] < min)
    {
      min = arr[i];
      idx = i;
    }
  }
  return idx;
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {4, 1, 2, 3};
  int n = arr.Length;

  // Function call
  Console.WriteLine(countSubArray(arr, n));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to count subarray
// containing both maximum and
// minimum array elements
function countSubArray(arr, n)
{

    // If the length of the
    // array is less than 2
    if (n < 2)
        return n;

    // Find the index of maximum element
    let i = max_element(arr);

    // Find the index of minimum element
    let j = min_element(arr);

    // If i > j, then swap
    // the value of i and j
    if (i > j)
    {
        let tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    }

    // Return the answer
    return (i + 1) * (n - j);
}

// Function to return max_element index
function max_element(arr)
{
    let idx = 0;
    let max = arr[0];
    for(let i = 1; i < arr.length; i++)
    {
        if(max < arr[i])
        {
            max = arr[i];
            idx = i;
        }
    }
    return idx;
}

// Function to return min_element index
function min_element(arr)
{
    let idx = 0;
    let min = arr[0];
    for(let i = 1; i < arr.length; i++)
    {
        if (arr[i] < min)
        {
            min = arr[i];
            idx = i;
        }
    }
    return idx;
}

// Driver Code

     let arr = [ 4, 1, 2, 3 ];
    let n = arr.length;

    // Function call
    document.write(countSubArray(arr, n));

 // This code is contributed by avijitmondal1998
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)