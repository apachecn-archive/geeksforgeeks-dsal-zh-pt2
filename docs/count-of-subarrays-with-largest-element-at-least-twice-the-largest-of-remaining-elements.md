# 元素最大的子阵列的计数至少是剩余元素最大值的两倍

> 原文:[https://www . geeksforgeeks . org/剩余元素数至少为最大元素数的两倍的子数组数/](https://www.geeksforgeeks.org/count-of-subarrays-with-largest-element-at-least-twice-the-largest-of-remaining-elements/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算子数组的个数，使得子数组的最大元素大于数组所有其他元素的最大元素[的两倍。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

**示例:**

> **输入:** arr[] = {1，6，10，9，7，3}
> **输出:** 4
> **说明:**
> 下面是满足给定条件的子阵:
> 
> 1.  考虑一下子阵列{6，10，9，7}。现在这个子阵列的最大元素是 10，大于剩余阵列元素最大元素的两倍，即 2*max{1，3} = 2*3 = 6。
> 2.  考虑一下子阵列{6，10，9，7，3}。现在这个子阵列的最大元素是 10，大于剩余阵列元素最大元素的两倍，即 2*max{1} = 2*1 = 2。
> 3.  考虑一下子阵列{1，6，10，9，7}。现在，这个子阵列的最大元素是 10，大于剩余阵列元素最大元素的两倍，即 2*max{3} = 2*3 = 6。
> 4.  考虑一下子阵列{1，6，10，9，7，3}。现在这个子阵列的最大元素是 10，大于剩余阵列元素最大元素的两倍，即 2*max{} = 2*0 = 0。
> 
> 因此，子阵列的总数是 4。
> 
> **输入:** arr[] = {1，10，2，3}
> **输出:** 6

**天真方法:**解决给定问题的最简单方法是[生成给定阵列的所有可能子阵列 **arr[]**](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/) 然后计算最大元素大于所有其他元素最大值两倍的子阵列数量。检查所有子阵列后，打印获得的子阵列计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to find count of subarrays
// which have max element greater than
// twice maximum of all other elements
void countSubarray(int arr[], int n)
{
    // Stores the count of subarrays
    int count = 0;

    // Generate all possible subarrays
    for (int i = 0; i < n; i++) {

        for (int j = i; j < n; j++) {

            // Stores the maximum element
            // of the subarray
            int mxSubarray = 0;

            // Stores the maximum of all
            // other elements
            int mxOther = 0;

            // Find the maximum element
            // in the subarray [i, j]
            for (int k = i; k <= j; k++) {
                mxSubarray = max(mxSubarray,
                                 arr[k]);
            }

            // Find the maximum of all
            // other elements
            for (int k = 0; k < i; k++) {
                mxOther = max(
                    mxOther, arr[k]);
            }

            for (int k = j + 1; k < n; k++) {
                mxOther = max(
                    mxOther, arr[k]);
            }

            // If the maximum of subarray
            // is greater than twice the
            // maximum of other elements
            if (mxSubarray > (2 * mxOther))
                count++;
        }
    }

    // Print the maximum value obtained
    cout << count;
}

// Driver Code
int main()
{
    int arr[] = { 1, 6, 10, 9, 7, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    countSubarray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find count of subarrays
// which have max element greater than
// twice maximum of all other elements
public static void countSubarray(int arr[], int n)
{

    // Stores the count of subarrays
    int count = 0;

    // Generate all possible subarrays
    for(int i = 0; i < n; i++)
    {
        for(int j = i; j < n; j++)
        {

            // Stores the maximum element
            // of the subarray
            int mxSubarray = 0;

            // Stores the maximum of all
            // other elements
            int mxOther = 0;

            // Find the maximum element
            // in the subarray [i, j]
            for(int k = i; k <= j; k++)
            {
                mxSubarray = Math.max(
                    mxSubarray, arr[k]);
            }

            // Find the maximum of all
            // other elements
            for(int k = 0; k < i; k++)
            {
                mxOther = Math.max(mxOther, arr[k]);
            }

            for(int k = j + 1; k < n; k++)
            {
                mxOther = Math.max(mxOther, arr[k]);
            }

            // If the maximum of subarray
            // is greater than twice the
            // maximum of other elements
            if (mxSubarray > (2 * mxOther))
                count++;
        }
    }

    // Print the maximum value obtained
    System.out.println(count);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 6, 10, 9, 7, 3 };
    int N = arr.length;

    countSubarray(arr, N);
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find count of subarrays
# which have max element greater than
# twice maximum of all other elements
def countSubarray(arr, n):
    # Stores the count of subarrays
    count = 0

    # Generate all possible subarrays
    for i in range(n):
        for j in range(i, n, 1):
            # Stores the maximum element
            # of the subarray
            mxSubarray = 0

            # Stores the maximum of all
            # other elements
            mxOther = 0

            # Find the maximum element
            # in the subarray [i, j]
            for k in range(i, j + 1, 1):
                mxSubarray = max(mxSubarray, arr[k])

            # Find the maximum of all
            # other elements
            for k in range(0, i, 1):
                mxOther = max(mxOther, arr[k])

            for k in range(j + 1,n,1):
                mxOther = max(mxOther, arr[k])

            # If the maximum of subarray
            # is greater than twice the
            # maximum of other elements
            if (mxSubarray > (2 * mxOther)):
                count += 1

    # Print the maximum value obtained
    print(count)

# Driver Code
if __name__ == '__main__':
    arr = [1, 6, 10, 9, 7, 3]
    N = len(arr)
    countSubarray(arr, N)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find count of subarrays
// which have max element greater than
// twice maximum of all other elements
static void countSubarray(int []arr, int n)
{

    // Stores the count of subarrays
    int count = 0;

    // Generate all possible subarrays
    for(int i = 0; i < n; i++)
    {
        for(int j = i; j < n; j++)
        {

            // Stores the maximum element
            // of the subarray
            int mxSubarray = 0;

            // Stores the maximum of all
            // other elements
            int mxOther = 0;

            // Find the maximum element
            // in the subarray [i, j]
            for(int k = i; k <= j; k++)
            {
                mxSubarray = Math.Max(mxSubarray,
                                      arr[k]);
            }

            // Find the maximum of all
            // other elements
            for(int k = 0; k < i; k++)
            {
                mxOther = Math.Max(mxOther, arr[k]);
            }

            for(int k = j + 1; k < n; k++)
            {
                mxOther = Math.Max(mxOther, arr[k]);
            }

            // If the maximum of subarray
            // is greater than twice the
            // maximum of other elements
            if (mxSubarray > (2 * mxOther))
                count++;
        }
    }

    // Print the maximum value obtained
    Console.Write(count);
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 6, 10, 9, 7, 3 };
    int N = arr.Length;

    countSubarray(arr, N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find count of subarrays
// which have max element greater than
// twice maximum of all other elements
function countSubarray(arr, n)
{

    // Stores the count of subarrays
    let count = 0;

    // Generate all possible subarrays
    for(let i = 0; i < n; i++)
    {
        for(let j = i; j < n; j++)
        {

            // Stores the maximum element
            // of the subarray
            let mxSubarray = 0;

            // Stores the maximum of all
            // other elements
            let mxOther = 0;

            // Find the maximum element
            // in the subarray [i, j]
            for(let k = i; k <= j; k++)
            {
                mxSubarray = Math.max(mxSubarray,
                                      arr[k]);
            }

            // Find the maximum of all
            // other elements
            for(let k = 0; k < i; k++)
            {
                mxOther = Math.max(mxOther, arr[k]);
            }

            for(let k = j + 1; k < n; k++)
            {
                mxOther = Math.max(
                    mxOther, arr[k]);
            }

            // If the maximum of subarray
            // is greater than twice the
            // maximum of other elements
            if (mxSubarray > (2 * mxOther))
                count++;
        }
    }

    // Print the maximum value obtained
    document.write(count);
}

// Driver Code
let arr = [ 1, 6, 10, 9, 7, 3 ];
let N = arr.length;

countSubarray(arr, N);

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(N<sup>3</sup>)
T5】辅助空间: O(1)

**有效方法:**上述方法也可以通过观察来优化，即阵列的[最大元素将始终是子阵列的一部分，并且值大于最大元素一半的所有元素也包含在子阵列中。按照以下步骤解决问题:](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

*   初始化一个变量，比如说 **mx** ，它存储数组的[最大元素。](https://www.geeksforgeeks.org/how-to-find-the-maximum-element-of-an-array-using-stl-in-c/)
*   初始化两个变量 **L** 和 **R** 来存储子阵列的左右端点。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，如果**2 * arr【I】**的值大于 **mx** ，则初始化 **L** 到 **i** 和[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   使用变量 **i** 以相反的方式迭代范围**【N–1，0】**，如果 **2*arr[i]** 的值大于 **mx** ，则初始化 **R** 到 **i** 和[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，打印**(L+1)*(N–R)**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find count of subarrays
// which have max element greater than
// twice maximum of all other elements
void countSubarray(int arr[], int n)
{
    int count = 0, L = 0, R = 0;

    // Stores the maximum element of
    // the array
    int mx = *max_element(arr, arr + n);

    // Traverse the given array
    for (int i = 0; i < n; i++) {

        // If the value of 2*arr[i] is
        // greater than mx
        if (arr[i] * 2 > mx) {

            // Update the value of L
            // and break out of loop
            L = i;
            break;
        }
    }

    for (int i = n - 1; i >= 0; i--) {

        // If the value 2*arr[i] is
        // greater than mx
        if (arr[i] * 2 > mx) {

            // Update the value of R
            // and break out of loop
            R = i;
            break;
        }
    }

    // Print the final answer
    cout << (L + 1) * (n - R);
}

// Driver Code
int main()
{
    int arr[] = { 1, 6, 10, 9, 7, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    countSubarray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find count of subarrays
    // which have max element greater than
    // twice maximum of all other elements
    static void countSubarray(int[] arr, int n)
    {
        int L = 0, R = 0;

        // Stores the maximum element of
        // the array

        int mx = Integer.MIN_VALUE;
        for (int i = 0; i < n; i++)
            mx = Math.max(mx, arr[i]);

        // Traverse the given array
        for (int i = 0; i < n; i++) {

            // If the value of 2*arr[i] is
            // greater than mx
            if (arr[i] * 2 > mx) {

                // Update the value of L
                // and break out of loop
                L = i;
                break;
            }
        }

        for (int i = n - 1; i >= 0; i--) {

            // If the value 2*arr[i] is
            // greater than mx
            if (arr[i] * 2 > mx) {

                // Update the value of R
                // and break out of loop
                R = i;
                break;
            }
        }

        // Print the final answer
        System.out.println((L + 1) * (n - R));
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 6, 10, 9, 7, 3 };
        int N = arr.length;
        countSubarray(arr, N);
    }
}

// This code is contributed by rishavmahato348.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find count of subarrays
# which have max element greater than
# twice maximum of all other elements
def countSubarray(arr, n):

    count = 0
    L = 0
    R = 0

    # Stores the maximum element of
    # the array
    mx = max(arr)

    # Traverse the given array
    for i in range(n):

        # If the value of 2*arr[i] is
        # greater than mx
        if (arr[i] * 2 > mx):

            # Update the value of L
            # and break out of loop
            L = i
            break

    i = n - 1

    while (i >= 0):

        # If the value 2*arr[i] is
        # greater than mx
        if (arr[i] * 2 > mx):

            # Update the value of R
            # and break out of loop
            R = i
            break

        i -= 1

    # Print the final answer
    print((L + 1) * (n - R))

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 6, 10, 9, 7, 3 ]
    N = len(arr)

    countSubarray(arr, N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find count of subarrays
    // which have max element greater than
    // twice maximum of all other elements
    static void countSubarray(int[] arr, int n)
    {
        int L = 0, R = 0;

        // Stores the maximum element of
        // the array

        int mx = Int32.MinValue;
        for (int i = 0; i < n; i++)
            mx = Math.Max(mx, arr[i]);

        // Traverse the given array
        for (int i = 0; i < n; i++) {

            // If the value of 2*arr[i] is
            // greater than mx
            if (arr[i] * 2 > mx) {

                // Update the value of L
                // and break out of loop
                L = i;
                break;
            }
        }

        for (int i = n - 1; i >= 0; i--) {

            // If the value 2*arr[i] is
            // greater than mx
            if (arr[i] * 2 > mx) {

                // Update the value of R
                // and break out of loop
                R = i;
                break;
            }
        }

        // Print the final answer
        Console.WriteLine((L + 1) * (n - R));
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 6, 10, 9, 7, 3 };
        int N = arr.Length;
        countSubarray(arr, N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to find count of subarrays
// which have max element greater than
// twice maximum of all other elements
function countSubarray(arr, n)
{
    var count = 0, L = 0, R = 0;

    // Stores the maximum element of
    // the array
    var mx = Math.max.apply(null, arr);

    var i;
    // Traverse the given array
    for (i = 0; i < n; i++) {

        // If the value of 2*arr[i] is
        // greater than mx
        if (arr[i] * 2 > mx) {

            // Update the value of L
            // and break out of loop
            L = i;
            break;
        }
    }

    for (i = n - 1; i >= 0; i--) {

        // If the value 2*arr[i] is
        // greater than mx
        if (arr[i] * 2 > mx) {

            // Update the value of R
            // and break out of loop
            R = i;
            break;
        }
    }

    // Print the final answer
    document.write((L + 1) * (n - R));
}

// Driver Code

    var arr = [1, 6, 10, 9, 7, 3]
    var N = arr.length;
    countSubarray(arr, N);

// This code is contributed by ipg2016107.
</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)