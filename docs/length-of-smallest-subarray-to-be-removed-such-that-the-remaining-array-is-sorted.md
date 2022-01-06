# 要移除的最小子阵列的长度，以便对剩余阵列进行排序

> 原文:[https://www . geeksforgeeks . org/待移除的最小子阵列长度，以便对剩余阵列进行排序/](https://www.geeksforgeeks.org/length-of-smallest-subarray-to-be-removed-such-that-the-remaining-array-is-sorted/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是打印要从 **arr[]** 中删除的最小子数组的长度，以便对剩余的数组进行排序。

**示例:**

> **输入:** arr[] = {1，2，3，10，4，2，3，5}
> **输出:** 3
> **解释:**
> 要移除的最小子阵列是长度为 3 的{10，4，2}。剩余的数组是{1，2，3，3，5}，它们被排序。
> 另一个正确的解决方案是移除子阵列[3，10，4]。
> 
> **输入:** arr[] = {5，4，3，2，1}
> *输出:4*
> ***说明:***
> 由于数组是严格递减的，所以数组中只需要保留一个元素。
> 因此，要求回答为 4。

**接近** ***:*** 可以通过以下三种方式移除子阵列来解决问题:

> 1.  Remove the left subarray, that is, the left suffix.
> 2.  Remove the right subarray ie, prefix.
> 3.  Remove the middle subarray and merge the left and right parts of the array.

1.  从左到右迭代 **arr[]** ，找到第一个索引**左****arr【左】> arr【左+1】**。所以需要去掉的使数组排序的子数组长度是 **N-left-1。**
2.  如果**left = = N–1**，则该数组已经排序，因此返回 0。
3.  从右到左迭代 **arr[]** ，找到第一个索引**右****arr【右】< arr【右–1】**。所以要去掉子阵长度使数组排序是**对的。**
4.  现在初始化一个变量 **mincount** ，取最小的 **N-left-1** 和 **right。**
5.  现在也计算要从阵列中间移除的子阵列的最小长度:
    1.  让 **i = 0，j =** **右**。并通过比较**arr【I】**和**arr【j】**检查 **i** 和 **j** (不含)之间的元素是否可以删除。
    2.  如果 **arr[j] > = arr[i]** ，尝试使用**j–I–1**更新答案，并增加 **i** 拧紧车窗。
    3.  如果**arr【j】<arr【I】**，中间不能删除元素，所以增加 **j** 来松开窗口。
    4.  遍历循环直到**我>离开**或 **j == N** 。并更新答案。
6.  返回**分钟数**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Find the length of the shortest subarray
int findLengthOfShortestSubarray(int arr[], int N)
{

    // To store the result
    int minlength = INT_MAX;

    int left = 0;
    int right = N - 1;

    // Calculate the possible length of
    // the sorted subarray from left
    while (left < right &&
       arr[left + 1] >= arr[left])
    {
        left++;
    }

    // Array is sorted
    if (left == N - 1)
        return 0;

    // Calculate the possible length of
    // the sorted subarray from left
    while (right > left &&
       arr[right - 1] <= arr[right])
    {
        right--;
    }

    // Update the result
    minlength = min(N - left - 1, right);

    // Calculate the possible length
    // in the middle we can delete
    // and update the result
    int j = right;
    for(int i = 0; i < left + 1; i++)
    {
        if (arr[i] <= arr[j])
        {

            // Update the result
            minlength = min(minlength, j - i - 1);
        }
        else if (j < N - 1)
        {
            j++;
        }
        else
        {
            break;
        }
    }

    // Return the result
    return minlength;
}

// Driver Code
int main()
{
    int arr[] = { 6, 3, 10, 11, 15,
                  20, 13, 3, 18, 12 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << (findLengthOfShortestSubarray(arr, N));
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG {

// Find the length of the shortest subarray
static int findLengthOfShortestSubarray(int arr[],
                                        int N)
{
  // To store the result
  int minlength = Integer.MAX_VALUE;

  int left = 0;
  int right = N - 1;

  // Calculate the possible length of
  // the sorted subarray from left
  while (left < right &&
         arr[left + 1] >= arr[left])
  {
    left++;
  }

  // Array is sorted
  if (left == N - 1)
    return 0;

  // Calculate the possible length of
  // the sorted subarray from left
  while (right > left &&
         arr[right - 1] <= arr[right])
  {
    right--;
  }

  // Update the result
  minlength = Math.min(N - left - 1,
                       right);

  // Calculate the possible length
  // in the middle we can delete
  // and update the result
  int j = right;

  for (int i = 0; i < left + 1; i++)
  {
    if (arr[i] <= arr[j])
    {
      // Update the result
      minlength = Math.min(minlength,
                           j - i - 1);
    }
    else if (j < N - 1)
    {
      j++;
    }
    else
    {
      break;
    }
  }

  // Return the result
  return minlength;
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {6, 3, 10, 11, 15,
               20, 13, 3, 18, 12};
  int N = arr.length;

  // Function call
  System.out.print(
         (findLengthOfShortestSubarray(arr, N)));
}
}

// This code is contributed by Chitranayal
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Find the length of the shortest subarray
def findLengthOfShortestSubarray(arr):

    # To store the result
    minlength = sys.maxsize

    left = 0
    right = len(arr) - 1

    # Calculate the possible length of
    # the sorted subarray from left
    while left < right and arr[left + 1] >= arr[left]:
        left += 1

    # Array is sorted
    if left == len(arr) - 1:
        return 0

    # Calculate the possible length of
    # the sorted subarray from left
    while right > left and arr[right-1] <= arr[right]:
        right -= 1

    # Update the result
    minlength = min(len(arr) - left - 1, right)

    # Calculate the possible length
    # in the middle we can delete
    # and update the result
    j = right
    for i in range(left + 1):

        if arr[i] <= arr[j]:

            # Update the result
            minlength = min(minlength, j - i - 1)

        elif j < len(arr) - 1:

            j += 1

        else:

            break

    # Return the result
    return minlength

# Driver Code
arr = [6, 3, 10, 11, 15, 20, 13, 3, 18, 12]

# Function Call
print(findLengthOfShortestSubarray(arr))
```

## C#

```
// C# program for the
// above approach
using System;

class GFG {

// Find the length of the shortest subarray
static int findLengthOfShortestSubarray(int []arr,
                                        int N)
{

  // To store the result
  int minlength = int.MaxValue;

  int left = 0;
  int right = N - 1;

  // Calculate the possible length of
  // the sorted subarray from left
  while (left < right &&
         arr[left + 1] >= arr[left])
  {
    left++;
  }

  // Array is sorted
  if (left == N - 1)
    return 0;

  // Calculate the possible length of
  // the sorted subarray from left
  while (right > left &&
         arr[right - 1] <= arr[right])
  {
    right--;
  }

  // Update the result
  minlength = Math.Min(N - left - 1,
                       right);

  // Calculate the possible length
  // in the middle we can delete
  // and update the result
  int j = right;

  for(int i = 0; i < left + 1; i++)
  {
    if (arr[i] <= arr[j])
    {

      // Update the result
      minlength = Math.Min(minlength,
                           j - i - 1);
    }
    else if (j < N - 1)
    {
      j++;
    }
    else
    {
      break;
    }
  }

  // Return the result
  return minlength;
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = { 6, 3, 10, 11, 15,
                20, 13, 3, 18, 12 };
  int N = arr.Length;

  // Function call
  Console.Write(findLengthOfShortestSubarray(
                 arr, N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Find the length of the shortest subarray
function findLengthOfShortestSubarray(arr, N)
{

    // To store the result
    let minlength = Number.MAX_VALUE;

    let left = 0;
    let right = N - 1;

    // Calculate the possible length of
    // the sorted subarray from left
    while (left < right &&
           arr[left + 1] >= arr[left])
    {
        left++;
    }

    // Array is sorted
    if (left == N - 1)
        return 0;

    // Calculate the possible length of
    // the sorted subarray from left
    while (right > left &&
           arr[right - 1] <= arr[right])
    {
        right--;
    }

    // Update the result
    minlength = Math.min(N - left - 1,
                         right);

    // Calculate the possible length
    // in the middle we can delete
    // and update the result
    let j = right;

    for(let i = 0; i < left + 1; i++)
    {
        if (arr[i] <= arr[j])
        {

            // Update the result
            minlength = Math.min(minlength,
                                 j - i - 1);
        }
        else if (j < N - 1)
        {
            j++;
        }
        else
        {
            break;
        }
    }

    // Return the result
    return minlength;
}

// Driver Code
let arr = [  6, 3, 10, 11, 15,
            20, 13, 3, 18, 12];
let N = arr.length;

// Function call
document.write(
    (findLengthOfShortestSubarray(arr, N)));

// This code is contributed by souravghosh0416

</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)