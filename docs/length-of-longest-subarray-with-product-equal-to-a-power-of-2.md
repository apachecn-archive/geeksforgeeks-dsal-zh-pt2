# 乘积等于 2 的幂的最长子阵列的长度

> 原文:[https://www . geeksforgeeks . org/最长子阵列长度与 2 的幂的乘积之和/](https://www.geeksforgeeks.org/length-of-longest-subarray-with-product-equal-to-a-power-of-2/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找出最长的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度，该子数组元素的乘积等于 2 的[完美幂。](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)

**示例:**

> **输入:** arr[] = {2，5，4，4，6}
> **输出:** 2
> **解释:**
> 乘积为 2 的完美幂的最大长度的子阵为{4，4}。
> 乘积= 4 * 4 = 16，是 2 的完美幂。
> 
> **输入** : arr[] = {2，5，4，6，8，8，2}
> **输出:** 3
> **解释:**
> 乘积为 2 的完美幂的最大长度的子阵为{8，8，2}。
> 乘积= 8 * 8 * 2 = 128，是 2 的完美幂。

**天真方法:**最简单的方法是[生成给定阵列的所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并检查任何子阵列的元素的[乘积是否为 2 的**完美幂**。如果发现为真，则将最大长度更新为此子阵列的长度。最后，打印检查所有可能的子阵列后获得的子阵列的最大长度。](https://www.geeksforgeeks.org/program-for-product-of-array/)

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**有效方法:**为了优化上述方法，该思想基于这样一个事实，即对于任何 2 的幂，它也可以表示为具有 2 的完美幂的数的乘积。因此，想法是使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)来找到子阵列的最大长度，该子阵列的所有元素都具有 2 的**完美幂。以下是步骤:**

*   将**最大长度**和 **ans** 初始化为 **0** ，分别存储子阵列的最大长度和合成的子阵列的最大长度。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下操作:
    *   如果[电流元素是 2](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/) 的完美幂，那么将**最大长度**增加 **1** 。否则更新**最大长度**为 **0** 。
    *   完成上述步骤后，将 **ans** 更新为 ans 和**最大长度**的最大值。
*   经过上述步骤后，将**和**的值打印为最大长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check whether a number
// is power of 2 or not
bool isPower(int x)
{
    return (x && (!(x & (x - 1))));
}

// Function to find maximum length
// subarray having product of element
// as a perfect power of 2
int maximumlength(int arr[], int N)
{
    // Stores current subarray length
    int max_length = 0;

    // Stores maximum subarray length
    int max_len_subarray = 0;

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        // If arr[i] is power of 2
        if (isPower(arr[i]) == 1) {

            // Increment max_length
            max_length++;

            // Update max_len_subarray
            max_len_subarray
                = max(max_length,
                      max_len_subarray);
        }

        // Otherwise
        else {
            max_length = 0;
        }
    }

    // Print the maximum length
    cout << max_len_subarray;
}

// Driver Code
int main()
{
    // Given arr[]
    int arr[] = { 2, 5, 4, 6, 8, 8, 2 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maximumlength(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check whether a number
// is power of 2 or not
public static boolean isPower(int x)
{
    if (x != 0 && (x & (x - 1)) == 0)
        return true;

    return false;
}

// Function to find maximum length
// subarray having product of element
// as a perfect power of 2
public static void maximumlength(int arr[],
                                 int N)
{

    // Stores current subarray length
    int max_length = 0;

    // Stores maximum subarray length
    int max_len_subarray = 0;

    // Traverse the given array
    for(int i = 0; i < N; i++)
    {

        // If arr[i] is power of 2
        if (isPower(arr[i]))
        {

            // Increment max_length
            max_length++;

            // Update max_len_subarray
            max_len_subarray = Math.max(max_length,
                                        max_len_subarray);
        }

        // Otherwise
        else
        {
            max_length = 0;
        }
    }

    // Print the maximum length
    System.out.println(max_len_subarray);
}

// Driver Code
public static void main(String args[])
{

    // Given arr[]
    int arr[] = { 2, 5, 4, 6, 8, 8, 2 };

    int N = arr.length;

    // Function Call
    maximumlength(arr, N);
}
}

// This code is contributed by hemanthswarna1506
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to check whether
# a number is power of 2
# or not
def isPower(x):

    if (x != 0 and
       (x & (x - 1)) == 0):
        return True;

    return False;

# Function to find maximum
# length subarray having
# product of element
# as a perfect power of 2
def maximumlength(arr, N):

    # Stores current
    # subarray length
    max_length = 0;

    # Stores maximum
    # subarray length
    max_len_subarray = 0;

    # Traverse the given array
    for i in range(N):

        # If arr[i] is power of 2
        if (isPower(arr[i])):

            # Increment max_length
            max_length += 1;

            # Update max_len_subarray
            max_len_subarray = max(max_length,
                                   max_len_subarray);

        # Otherwise
        else:
            max_length = 0;

    # Print maximum length
    print(max_len_subarray);

# Driver Code
if __name__ == '__main__':

    # Given arr
    arr = [2, 5, 4,
           6, 8, 8, 2];

    N = len(arr);

    # Function Call
    maximumlength(arr, N);

# This code is contributed by gauravrajput1
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check whether a number
// is power of 2 or not
public static bool isPower(int x)
{
    if (x != 0 && (x & (x - 1)) == 0)
        return true;

    return false;
}

// Function to find maximum length
// subarray having product of element
// as a perfect power of 2
public static void maximumlength(int[] arr,
                                 int N)
{

    // Stores current subarray length
    int max_length = 0;

    // Stores maximum subarray length
    int max_len_subarray = 0;

    // Traverse the given array
    for(int i = 0; i < N; i++)
    {

        // If arr[i] is power of 2
        if (isPower(arr[i]))
        {

            // Increment max_length
            max_length++;

            // Update max_len_subarray
            max_len_subarray = Math.Max(max_length,
                                        max_len_subarray);
        }

        // Otherwise
        else
        {
            max_length = 0;
        }
    }

    // Print the maximum length
    Console.WriteLine(max_len_subarray);
}

// Driver Code
public static void Main()
{

    // Given arr[]
    int[] arr = { 2, 5, 4, 6, 8, 8, 2 };

    int N = arr.Length;

    // Function Call
    maximumlength(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check whether a number
// is power of 2 or not
function isPower(x)
{
    return (x && (!(x & (x - 1))));
}

// Function to find maximum length
// subarray having product of element
// as a perfect power of 2
function maximumlength(arr, N)
{
    // Stores current subarray length
    var max_length = 0;

    // Stores maximum subarray length
    var max_len_subarray = 0;

    // Traverse the given array
    for (var i = 0; i < N; i++) {

        // If arr[i] is power of 2
        if (isPower(arr[i]) == 1) {

            // Increment max_length
            max_length++;

            // Update max_len_subarray
            max_len_subarray
                = Math.max(max_length,
                      max_len_subarray);
        }

        // Otherwise
        else {
            max_length = 0;
        }
    }

    // Print the maximum length
    document.write( max_len_subarray);
}

// Driver Code

// Given arr[]
var arr = [2, 5, 4, 6, 8, 8, 2];
var N = arr.length;

// Function Call
maximumlength(arr, N);

</script>
```

**Output**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)