# 具有最大可能和的最小子阵列的长度

> 原文:[https://www . geeksforgeeks . org/具有最大可能总和的最小子阵列长度/](https://www.geeksforgeeks.org/length-of-the-smallest-subarray-with-maximum-possible-sum/)

给定一个由非负整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到总和最大的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最小长度。

**示例:**

> **输入:** arr[] = {0，2，0，0，12，0，0}
> **输出:** 4
> **说明:**子阵{2，0，0，12}之和= 2 + 0 + 0 + 12 = 14，这是可能的最大和，子阵长度为 4，这是最小的。
> 
> **输入:** arr[] = {2，0，0 }
> T3】输出: 1

**天真方法:**解决给定问题的最简单方法是[生成给定阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的所有可能子阵列，并打印该子阵列的长度，该子阵列的和是相同和的所有可能子阵列中具有最小长度的阵列的[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以利用所有元素都是非负的事实进行优化，因此子阵列的最大和就是阵列本身的[和。因此，想法是从阵列的任一端排除拖尾的 **0s** ，以最大和最小化最终的](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)长度。按照以下步骤解决问题:

*   初始化两个变量，比如说 **i** 为 **0** 和 **j** 为**(N–1)**，它们存储合成子阵列的开始和结束索引。
*   [从前面遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，直到遇到一个正元素，同时增加 **i** 的值。
*   如果 **i** 的值为 **N** ，则生成的子阵列的最大长度打印为 **1** ，因为它包含所有元素为 **0** 。否则，[从末尾开始遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，直到遇到正元素，同时递减 **j** 的值。
*   完成上述步骤后，打印**(j–I+1)**的值作为结果子阵列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum length
// of the subarray whose sum is maximum
int minimumSizeSubarray(int arr[],
                        int N)
{
    // Stores the starting and the
    // ending index of the resultant
    // subarray
    int i = 0, j = N - 1;

    // Traverse the array until a
    // non-zero element is encountered
    while (i < N and arr[i] == 0) {
        i++;
    }

    // If the array contains only of 0s
    if (i == N)
        return 1;

    // Traverse the array in reverse until
    // a non-zero element is encountered
    while (j >= 0 and arr[j] == 0) {
        j--;
    }

    // Return the resultant
    // size of the subarray
    return (j - i + 1);
}

// Driver Code
int main()
{
    int arr[] = { 0, 2, 0, 0, 12,
                  0, 0, 0 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << minimumSizeSubarray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find the minimum length
// of the subarray whose sum is maximum
static int minimumSizeSubarray(int arr[],
                        int N)
{

    // Stores the starting and the
    // ending index of the resultant
    // subarray
    int i = 0, j = N - 1;

    // Traverse the array until a
    // non-zero element is encountered
    while (i < N && arr[i] == 0) {
        i++;
    }

    // If the array contains only of 0s
    if (i == N)
        return 1;

    // Traverse the array in reverse until
    // a non-zero element is encountered
    while (j >= 0 && arr[j] == 0) {
        j--;
    }

    // Return the resultant
    // size of the subarray
    return (j - i + 1);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 0, 2, 0, 0, 12,
                  0, 0, 0 };
    int N = arr.length;
    System.out.print( minimumSizeSubarray(arr, N));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum length
# of the subarray whose sum is maximum
def minimumSizeSubarray(arr, N):

    # Stores the starting and the
    # ending index of the resultant
    # subarray
    i, j = 0, N - 1

    # Traverse the array until a
    # non-zero element is encountered
    while (i < N and arr[i] == 0):
        i += 1

    # If the array contains only of 0s
    if (i == N):
        return 1

    # Traverse the array in reverse until
    # a non-zero element is encountered
    while (j >= 0 and arr[j] == 0):
        j -= 1

    # Return the resultant
    # size of the subarray
    return(j - i + 1)

# Driver Code
if __name__ == '__main__':

    arr = [ 0, 2, 0, 0, 12, 0, 0, 0 ]
    N = len(arr)

    print(minimumSizeSubarray(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum length
// of the subarray whose sum is maximum
static int minimumSizeSubarray(int[] arr,
                               int N)
{

    // Stores the starting and the
    // ending index of the resultant
    // subarray
    int i = 0, j = N - 1;

    // Traverse the array until a
    // non-zero element is encountered
    while (i < N && arr[i] == 0)
    {
        i++;
    }

    // If the array contains only of 0s
    if (i == N)
        return 1;

    // Traverse the array in reverse until
    // a non-zero element is encountered
    while (j >= 0 && arr[j] == 0)
    {
        j--;
    }

    // Return the resultant
    // size of the subarray
    return (j - i + 1);
}

// Driver code
public static void Main()
{
    int[] arr = { 0, 2, 0, 0, 12, 0, 0, 0 };
    int N = arr.Length;

    Console.Write( minimumSizeSubarray(arr, N));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum length
// of the subarray whose sum is maximum
function minimumSizeSubarray(arr, N)
{
    // Stores the starting and the
    // ending index of the resultant
    // subarray
    let i = 0, j = N - 1;

    // Traverse the array until a
    // non-zero element is encountered
    while (i < N && arr[i] == 0) {
        i++;
    }

    // If the array contains only of 0s
    if (i == N)
        return 1;

    // Traverse the array in reverse until
    // a non-zero element is encountered
    while (j >= 0 && arr[j] == 0) {
        j--;
    }

    // Return the resultant
    // size of the subarray
    return (j - i + 1);
}

// Driver Code
    let arr = [ 0, 2, 0, 0, 12,
                  0, 0, 0 ];
    let N = arr.length;
    document.write(minimumSizeSubarray(arr, N));

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)