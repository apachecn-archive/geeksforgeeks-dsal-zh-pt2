# 给定数组子集的最大大小，使得三角形可以由任意三个整数组成，作为三角形的边

> 原文:[https://www . geeksforgeeks . org/给定数组子集的最大大小，使得三角形可以由任意三个整数作为三角形的边来构成/](https://www.geeksforgeeks.org/maximum-size-of-subset-of-given-array-such-that-a-triangle-can-be-formed-by-any-three-integers-as-the-sides-of-the-triangle/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到数组最大子集的大小，这样就可以由子集的三个整数中的任何一个组成一个三角形，作为三角形的边。

**示例:**

> **输入:** arr[] = {1，4，7，4}
> **输出:** 3
> **解释:**符合给定条件的可能子集是{1，4，4}和{4，4，7}。这两个子集的大小都是 3，这是可能的最大值。
> 
> **输入:** arr[] = {2，7，4，1，6，9，5，3}
> **输出:** 4

**方法:**给定的问题可以借助[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)来解决。众所周知，对于边长为 **A** 、 **B** 和 **C** 、 **A + B > C** 的三角形，当 **A** 和 **B** 是边长较小的边时，必须成立。基于以上观察，可以使用以下步骤解决给定的问题:

*   [按非递减顺序对给定数组 arr[]进行排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   维护两个变量 **i** 和 **j** ，其中 **i** 跟踪当前窗口的起点， **j** 跟踪当前窗口的终点。最初 **i = 0** 和 **j = i + 2** 。
*   增加 **j** 的值，直到**arr[I]+arr[I+1]>arr[j]**并跟踪变量 **maxSize** 中**j–I**的最大值。如果**arr[I]+arr[I+1]>arr[j]**，将 **i** 的值增加 **1** 。
*   遵循上述步骤，直到遍历完整个数组。
*   完成上述步骤后，存储在 **maxSize** 中的值即为所需结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum size of
// the subset of the given array such
// that a triangle can be formed from any
// three integers of the subset as sides
int maximizeSubset(int arr[], int N)
{
    // Sort arr[] in increasing order
    sort(arr, arr + N);

    // Stores the maximum size of a valid
    // subset of the given array
    int maxSize = 0;

    // Stores the starting index of the
    // current window
    int i = 0;

    // Stores the last index of the
    // current window
    int j = i + 2;

    // Iterate over the array arr[]
    while (i < N - 2) {

        // Increment j till the value
        // of arr[i] + arr[i + 1] >
        // arr[j] holds true
        while (arr[i] + arr[i + 1] > arr[j]) {
            j++;
        }

        // Update the value of maxSize
        maxSize = max(maxSize, j - i);

        i++;
        j = max(j, i + 2);
    }

    // Return Answer
    return maxSize;
}

// Driver Code
int main()
{
    int arr[] = { 2, 7, 4, 1, 6, 9, 5, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maximizeSubset(arr, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find the maximum size of
// the subset of the given array such
// that a triangle can be formed from any
// three integers of the subset as sides
static int maximizeSubset(int arr[], int N)
{

    // Sort arr[] in increasing order
    Arrays.sort(arr);

    // Stores the maximum size of a valid
    // subset of the given array
    int maxSize = 0;

    // Stores the starting index of the
    // current window
    int i = 0;

    // Stores the last index of the
    // current window
    int j = i + 2;

    // Iterate over the array arr[]
    while (i < N - 2) {

        // Increment j till the value
        // of arr[i] + arr[i + 1] >
        // arr[j] holds true

        while (j<N && arr[i] + arr[i + 1] > arr[j]) {
            j++;
        }

        // Update the value of maxSize
        maxSize = Math.max(maxSize, j - i);

        i++;
        j = Math.max(j, i + 2);
    }

    // Return Answer
    return maxSize;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 7, 4, 1, 6, 9, 5, 3 };
    int N = arr.length;

    System.out.print(maximizeSubset(arr, N) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the maximum size of
# the subset of the given array such
# that a triangle can be formed from any
# three integers of the subset as sides

def maximizeSubset(arr, N):
    # Sort arr[] in increasing order
    arr.sort()

    # Stores the maximum size of a valid
    # subset of the given array
    maxSize = 0

    # Stores the starting index of the
    # current window
    i = 0

    # Stores the last index of the
    # current window
    j = i + 2

    # Iterate over the array arr[]
    while (i < N - 2):

                # Increment j till the value
                # of arr[i] + arr[i + 1] >
                # arr[j] holds true
        while (j < N and arr[i] + arr[i + 1] > arr[j]):
            j = j + 1

            # Update the value of maxSize
        maxSize = max(maxSize, j - i)
        i += 1
        j = max(j, i + 2)

        # Return Answer
    return maxSize

# Driver Code
if __name__ == "__main__":

    arr = [2, 7, 4, 1, 6, 9, 5, 3]
    N = len(arr)
    print(maximizeSubset(arr, N))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum size of
// the subset of the given array such
// that a triangle can be formed from any
// three integers of the subset as sides
static int maximizeSubset(int []arr, int N)
{
    // Sort arr[] in increasing order
    Array.Sort(arr);

    // Stores the maximum size of a valid
    // subset of the given array
    int maxSize = 0;

    // Stores the starting index of the
    // current window
    int i = 0;

    // Stores the last index of the
    // current window
    int j = i + 2;

    // Iterate over the array arr[]
    while (i < N - 2) {

        // Increment j till the value
        // of arr[i] + arr[i + 1] >
        // arr[j] holds true
        if(j>=N || i+1 >=N)
           break;
        while (j<N && arr[i] + arr[i + 1] > arr[j]) {
            j++;
        }

        // Update the value of maxSize
        maxSize = Math.Max(maxSize, j - i);

        i++;
        j = Math.Max(j, i + 2);
    }

    // Return Answer
    return maxSize;
}

// Driver Code
public static void Main()
{
    int []arr = { 2, 7, 4, 1, 6, 9, 5, 3 };
    int N = arr.Length;

    Console.Write(maximizeSubset(arr, N));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to find the maximum size of
    // the subset of the given array such
    // that a triangle can be formed from any
    // three integers of the subset as sides
    const maximizeSubset = (arr, N) => {
        // Sort arr[] in increasing order
        arr.sort((a, b) => a - b)

        // Stores the maximum size of a valid
        // subset of the given array
        let maxSize = 0;

        // Stores the starting index of the
        // current window
        let i = 0;

        // Stores the last index of the
        // current window
        let j = i + 2;

        // Iterate over the array arr[]
        while (i < N - 2) {

            // Increment j till the value
            // of arr[i] + arr[i + 1] >
            // arr[j] holds true
            while (arr[i] + arr[i + 1] > arr[j]) {
                j++;
            }

            // Update the value of maxSize
            maxSize = Math.max(maxSize, j - i);

            i++;
            j = Math.max(j, i + 2);
        }

        // Return Answer
        return maxSize;
    }

    // Driver Code

    let arr = [2, 7, 4, 1, 6, 9, 5, 3];
    let N = arr.length;

    document.write(maximizeSubset(arr, N));

    // This code is contributed by rakeshsahni

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*