# 为使剩余元素连续需要移除的最小子阵列的长度

> 原文:[https://www . geeksforgeeks . org/最小子阵列长度-需要移除才能使剩余元素连续/](https://www.geeksforgeeks.org/length-of-smallest-subarray-required-to-be-removed-to-make-remaining-elements-consecutive/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到需要移除的最小子数组的长度，以使剩余的[数组元素连续](https://www.geeksforgeeks.org/check-if-array-elements-are-consecutive/)。

**示例:**

> **输入:** arr[] = {1，2，3，7，5，4，5}
> **输出:** 2
> **解释:**
> 从数组 arr[]中移除子数组{7，5}会将数组修改为{1，2，3，4，5}，这将使所有数组元素连续。因此，移除的子阵列长度为 2，这是最小长度。
> 
> **输入:** arr[] = {4，5，6，8，9，10 }
> T3】输出: 3

**天真方法:**解决给定问题的最简单方法是移除[生成阵列的所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)**arr【】**并且对于它们中的每一个，检查它们的移除是否使得剩余的阵列元素连续。检查所有子阵列后，打印满足条件的最小子阵列长度。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过存储连续元素的最长前缀和后缀的长度，然后找到需要移除的子阵列的最小长度，使得前缀和后缀的串联形成连续元素的序列来优化。
按照以下步骤解决问题:

*   初始化两个变量，说 **L** 为 **0** 和 **R** 为**(N–1)**分别存储连续元素最长前缀的结束索引和最长后缀的开始索引。
*   将 **L** 的值更新为第一个索引，其中 **arr[i] + 1** 不等于 **arr[i + 1]** ，这样 **arr[0，…，L]** 就是一个连续的前缀数组。
*   将 **R** 的值更新为从末端开始的第一个索引，其中 **arr[i]** 不等于**arr[I–1]+1**，这样 **arr[R，…，N–1]**就是一个连续的后缀数组。
*   初始化一个变量，说 **ans，**存储**(N–L–1)**和 **R** 的[最小值，存储需要的结果。](https://www.geeksforgeeks.org/stdmin-in-cpp/)
*   如果 **arr[R] ≤ arr[L] + 1** 的值，则存储右索引， **R1** 为 **arr[0，…，L，R1，…，N–1]**为连续数组。
*   如果**(R1–L–1)**的值小于 **ans** 的值，则将 **ans** 的值更新为**(R1–L–1)**。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// smallest subarray to be removed to
// make remaining array elements consecutive
void shortestSubarray(int* A, int N)
{
    int i;

    // Store the ending index of the
    // longest prefix consecutive array
    int left_index;

    // Traverse the array to find the
    // longest prefix consecutive sequence
    for (i = 0; i < N - 1; i++) {
        if (A[i] + 1 != A[i + 1])
            break;
    }

    // A[0...left_index] is the
    // prefix consecutive sequence
    left_index = i;

    // Store the starting index of the
    // longest suffix consecutive sequence
    int right_index;

    // Traverse the array to find the
    // longest suffix consecutive sequence
    for (i = N - 1; i >= 1; i--) {
        if (A[i] != A[i - 1] + 1)
            break;
    }

    // A[right_index...N-1] is
    // the consecutive sequence
    right_index = i;

    int updated_right;

    // Store the smallest subarray
    // required to be removed
    int minLength = min(N - left_index - 1,
                        right_index);

    // Check if subarray from the
    // middle can be removed
    if (A[right_index]
        <= A[left_index] + 1) {

        // Update the right index s.t.
        // A[0, N-1] is consecutive
        updated_right = right_index
                        + A[left_index]
                        - A[right_index] + 1;

        // If updated_right < N, then
        // update the minimumLength
        if (updated_right < N)
            minLength = min(minLength,
                            updated_right
                                - left_index - 1);
    }

    // Print the required result
    cout << minLength;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 7, 4, 3, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    shortestSubarray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the length of the
// smallest subarray to be removed to
// make remaining array elements consecutive
static void shortestSubarray(int A[], int N)
{
    int i;

    // Store the ending index of the
    // longest prefix consecutive array
    int left_index;

    // Traverse the array to find the
    // longest prefix consecutive sequence
    for(i = 0; i < N - 1; i++)
    {
        if (A[i] + 1 != A[i + 1])
            break;
    }

    // A[0...left_index] is the
    // prefix consecutive sequence
    left_index = i;

    // Store the starting index of the
    // longest suffix consecutive sequence
    int right_index;

    // Traverse the array to find the
    // longest suffix consecutive sequence
    for(i = N - 1; i >= 1; i--)
    {
        if (A[i] != A[i - 1] + 1)
            break;
    }

    // A[right_index...N-1] is
    // the consecutive sequence
    right_index = i;

    int updated_right;

    // Store the smallest subarray
    // required to be removed
    int minLength = Math.min(N - left_index - 1,
                             right_index);

    // Check if subarray from the
    // middle can be removed
    if (A[right_index] <= A[left_index] + 1)
    {

        // Update the right index s.t.
        // A[0, N-1] is consecutive
        updated_right = right_index + A[left_index] -
                     A[right_index] + 1;

        // If updated_right < N, then
        // update the minimumLength
        if (updated_right < N)
            minLength = Math.min(minLength,
                                 updated_right -
                                 left_index - 1);
    }

    // Print the required result
    System.out.println(minLength);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 7, 4, 3, 5 };
    int N = arr.length;

    shortestSubarray(arr, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the length of the
# smallest subarray to be removed to
# make remaining array elements consecutive
def shortestSubarray(A, N):

    i = 0

    # Store the ending index of the
    # longest prefix consecutive array
    left_index = 0

    # Traverse the array to find the
    # longest prefix consecutive sequence
    for i in range(N - 1):
        if (A[i] + 1 != A[i + 1]):
            break

    # A[0...left_index] is the
    # prefix consecutive sequence
    left_index = i

    # Store the starting index of the
    # longest suffix consecutive sequence
    right_index = 0

    # Traverse the array to find the
    # longest suffix consecutive sequence
    i = N - 1

    while (i >= 1):
        if (A[i] != A[i - 1] + 1):
            break

        i -= 1

    # A[right_index...N-1] is
    # the consecutive sequence
    right_index = i

    updated_right = 0

    # Store the smallest subarray
    # required to be removed
    minLength = min(N - left_index - 1, right_index)

    # Check if subarray from the
    # middle can be removed
    if (A[right_index] <= A[left_index] + 1):

        # Update the right index s.t.
        # A[0, N-1] is consecutive
        updated_right = (right_index + A[left_index] -
                                       A[right_index] + 1)

        # If updated_right < N, then
        # update the minimumLength
        if (updated_right < N):
            minLength = min(minLength, updated_right -
                                       left_index - 1)

    # Print the required result
    print(minLength)

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 7, 4, 3, 5 ]
    N = len(arr)

    shortestSubarray(arr, N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the length of the
// smallest subarray to be removed to
// make remaining array elements consecutive
static void shortestSubarray(int[] A, int N)
{
    int i;

    // Store the ending index of the
    // longest prefix consecutive array
    int left_index;

    // Traverse the array to find the
    // longest prefix consecutive sequence
    for(i = 0; i < N - 1; i++)
    {
        if (A[i] + 1 != A[i + 1])
            break;
    }

    // A[0...left_index] is the
    // prefix consecutive sequence
    left_index = i;

    // Store the starting index of the
    // longest suffix consecutive sequence
    int right_index;

    // Traverse the array to find the
    // longest suffix consecutive sequence
    for(i = N - 1; i >= 1; i--)
    {
        if (A[i] != A[i - 1] + 1)
            break;
    }

    // A[right_index...N-1] is
    // the consecutive sequence
    right_index = i;

    int updated_right;

    // Store the smallest subarray
    // required to be removed
    int minLength = Math.Min(N - left_index - 1,
                             right_index);

    // Check if subarray from the
    // middle can be removed
    if (A[right_index] <= A[left_index] + 1)
    {

        // Update the right index s.t.
        // A[0, N-1] is consecutive
        updated_right = right_index + A[left_index] -
                     A[right_index] + 1;

        // If updated_right < N, then
        // update the minimumLength
        if (updated_right < N)
            minLength = Math.Min(minLength,
                                 updated_right -
                                 left_index - 1);
    }

    // Print the required result
    Console.WriteLine(minLength);
}

// Driver code
static public void Main()
{
    int[] arr = { 1, 2, 3, 7, 4, 3, 5 };
    int N = arr.Length;

    shortestSubarray(arr, N);
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the length of the
// smallest subarray to be removed to
// make remaining array elements consecutive
function shortestSubarray(A, N)
{
    let i;

    // Store the ending index of the
    // longest prefix consecutive array
    let left_index;

    // Traverse the array to find the
    // longest prefix consecutive sequence
    for(i = 0; i < N - 1; i++)
    {
        if (A[i] + 1 != A[i + 1])
            break;
    }

    // A[0...left_index] is the
    // prefix consecutive sequence
    left_index = i;

    // Store the starting index of the
    // longest suffix consecutive sequence
    let right_index;

    // Traverse the array to find the
    // longest suffix consecutive sequence
    for(i = N - 1; i >= 1; i--)
    {
        if (A[i] != A[i - 1] + 1)
            break;
    }

    // A[right_index...N-1] is
    // the consecutive sequence
    right_index = i;

    let updated_right;

    // Store the smallest subarray
    // required to be removed
    let minLength = Math.min(N - left_index - 1,
                             right_index);

    // Check if subarray from the
    // middle can be removed
    if (A[right_index] <= A[left_index] + 1)
    {

        // Update the right index s.t.
        // A[0, N-1] is consecutive
        updated_right = right_index + A[left_index] -
                     A[right_index] + 1;

        // If updated_right < N, then
        // update the minimumLength
        if (updated_right < N)
            minLength = Math.min(minLength,
                                 updated_right -
                                 left_index - 1);
    }

    // Print the required result
    document.write(minLength);
}

// Driver code
    let arr = [ 1, 2, 3, 7, 4, 3, 5 ];
    let N = arr.length;

    shortestSubarray(arr, N);

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)