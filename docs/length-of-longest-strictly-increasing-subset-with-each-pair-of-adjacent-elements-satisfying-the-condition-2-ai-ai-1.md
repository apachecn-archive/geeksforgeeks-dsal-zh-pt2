# 每对相邻元素满足条件 2 * A[i] ≥ A[i + 1]

的最长严格递增子集的长度

> 原文:[https://www . geeksforgeeks . org/每对相邻元素满足条件-2-ai-ai-1/](https://www.geeksforgeeks.org/length-of-longest-strictly-increasing-subset-with-each-pair-of-adjacent-elements-satisfying-the-condition-2-ai-ai-1/) 的最长严格递增子集长度

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，任务是找出最长严格递增的[子集](https://www.geeksforgeeks.org/power-set/)的长度，每对相邻元素满足条件 **A[i + 1] ≤ 2 * A[i]** 。如果存在多个这样的子集，则打印其中任何一个。

**示例:**

> **输入:** A[] = {3，1，5，11}
> **输出:** 3，5
> **说明:**在数组所有可能的子集中，{3，5}是满足给定条件的最长子集。
> 
> **输入:** A[] = {3，1，7，12}
> **输出:** 7，12
> **说明:**在数组的所有可能子集中，{7，12}是满足给定条件的最长子集。

**天真法:**解决问题最简单的方法是[对数组进行升序排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)、[生成给定数组的所有可能子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)，找到满足给定条件的最长子集的长度。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**该思想基于这样的观察，即只有从[排序数组](https://www.geeksforgeeks.org/search-an-element-in-a-sorted-and-pivoted-array/)中获取满足给定条件的连续元素时，才会生成最长子集。

按照以下步骤解决问题:

*   初始化两个变量，比如**索引**和 **maxLen** ，存储所需子集的起始索引和最大长度。
*   [按升序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对数组 **A[]** 进行排序。
*   初始化一个变量，说 **i** ，进行遍历，[迭代，而**I<N**T5】执行以下步骤:](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)
    *   初始化另一个变量 **j = i** ，以存储当前子集的端点。
    *   [迭代，当**j<N–1**](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)和 **2 * A[j] ≥ A[j + 1]** 成立时，增加当前子集的长度，比如 **L** ，将 **j** 增加 **1** 。
    *   如果 **L** 的值大于 **maxLen** ，则将 **maxLen** 更新为 **L** 和**索引**为 **i** 。
    *   将 **i** 的值更新为 **j + 1** 。
*   通过[打印](https://www.geeksforgeeks.org/range-based-loop-c/) **【索引，索引+maxLen-1】**范围内的元素，打印所需子集。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// longest subset satisfying given conditions
void maxLenSubset(int a[], int n)
{
    // Sort the array in ascending order
    sort(a, a + n);

    // Stores the starting index and maximum
    // length of the required subset
    int index = 0, maxlen = -1;

    // Pointer to traverse the array
    int i = 0;

    // Iterate while i < n
    while (i < n) {

        // Stores end point
        // of current subset
        int j = i;

        // Store the length of
        // the current subset
        int len = 1;

        // Continue adding elements to the current
        // subset till the condition satisfies
        while (j < n - 1) {

            if (2 * a[j] >= a[j + 1]) {

                // Increment length of
                // the current subset
                len++;
            }
            else
                break;

            // Increment the pointer j
            j++;
        }

        // If length of the current subset
        // exceeds overall maximum length
        if (maxlen < len) {

            // Update maxlen
            maxlen = len;

            // Update index
            index = i;
        }

        // Increment j
        j++;

        // Update i
        i = j;
    }

    // Store the starting index of
    // the required subset in i
    i = index;

    // Print the required subset
    while (maxlen > 0) {

        // Print the array element
        cout << a[i] << " ";

        // Decrement maxlen
        maxlen--;

        // Increment i
        i++;
    }
}

// Driver Code
int main()
{
    // Given array
    int a[] = { 3, 1, 5, 11 };

    // Store the size of the array
    int n = sizeof(a) / sizeof(int);

    maxLenSubset(a, n);

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
// longest subset satisfying given conditions
static void maxLenSubset(int a[], int n)
{

    // Sort the array in ascending order
    Arrays.sort(a);

    // Stores the starting index and maximum
    // length of the required subset
    int index = 0, maxlen = -1;

    // Pointer to traverse the array
    int i = 0;

    // Iterate while i < n
    while (i < n)
    {

        // Stores end point
        // of current subset
        int j = i;

        // Store the length of
        // the current subset
        int len = 1;

        // Continue adding elements to the current
        // subset till the condition satisfies
        while (j < n - 1)
        {
            if (2 * a[j] >= a[j + 1])
            {

                // Increment length of
                // the current subset
                len++;
            }
            else
                break;

            // Increment the pointer j
            j++;
        }

        // If length of the current subset
        // exceeds overall maximum length
        if (maxlen < len)
        {

            // Update maxlen
            maxlen = len;

            // Update index
            index = i;
        }

        // Increment j
        j++;

        // Update i
        i = j;
    }

    // Store the starting index of
    // the required subset in i
    i = index;

    // Print the required subset
    while (maxlen > 0)
    {

        // Print the array element
        System.out.print(a[i] + " ");

        // Decrement maxlen
        maxlen--;

        // Increment i
        i++;
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int a[] = { 3, 1, 5, 11 };

    // Store the size of the array
    int n = a.length;

    maxLenSubset(a, n);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the length of the
# longest subset satisfying given conditions
def maxLenSubset(a, n):

    # Sort the array in ascending order
    a.sort(reverse = False)

    # Stores the starting index and maximum
    # length of the required subset
    index = 0
    maxlen = -1

    # Pointer to traverse the array
    i = 0

    # Iterate while i < n
    while (i < n):

        # Stores end point
        # of current subset
        j = i

        # Store the length of
        # the current subset
        len1 = 1

        # Continue adding elements to the current
        # subset till the condition satisfies
        while (j < n - 1):
            if (2 * a[j] >= a[j + 1]):

                # Increment length of
                # the current subset
                len1 += 1
            else:
                break

            # Increment the pointer j
            j += 1

        # If length of the current subset
        # exceeds overall maximum length
        if (maxlen < len1):

            # Update maxlen
            maxlen = len1

            # Update index
            index = i

        # Increment j
        j += 1

        # Update i
        i = j

    # Store the starting index of
    # the required subset in i
    i = index

    # Print the required subset
    while (maxlen > 0):

        # Print the array element
        print(a[i], end = " ")

        # Decrement maxlen
        maxlen -= 1

        # Increment i
        i += 1

# Driver Code
if __name__ == '__main__':

    # Given array
    a =  [3, 1, 5, 11]

    # Store the size of the array
    n = len(a)

    maxLenSubset(a, n)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the length of the
// longest subset satisfying given conditions
static void maxLenSubset(int[] a, int n)
{

    // Sort the array in ascending order
    Array.Sort(a);

    // Stores the starting index and maximum
    // length of the required subset
    int index = 0, maxlen = -1;

    // Pointer to traverse the array
    int i = 0;

    // Iterate while i < n
    while (i < n)
    {

        // Stores end point
        // of current subset
        int j = i;

        // Store the length of
        // the current subset
        int len = 1;

        // Continue adding elements to the current
        // subset till the condition satisfies
        while (j < n - 1)
        {
            if (2 * a[j] >= a[j + 1])
            {

                // Increment length of
                // the current subset
                len++;
            }
            else
                break;

            // Increment the pointer j
            j++;
        }

        // If length of the current subset
        // exceeds overall maximum length
        if (maxlen < len)
        {

            // Update maxlen
            maxlen = len;

            // Update index
            index = i;
        }

        // Increment j
        j++;

        // Update i
        i = j;
    }

    // Store the starting index of
    // the required subset in i
    i = index;

    // Print the required subset
    while (maxlen > 0)
    {

        // Print the array element
        Console.Write(a[i] + " ");

        // Decrement maxlen
        maxlen--;

        // Increment i
        i++;
    }
}

// Driver Code
public static void Main(string[] args)
{

    // Given array
    int[] a = { 3, 1, 5, 11 };

    // Store the size of the array
    int n = a.Length;

    maxLenSubset(a, n);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

        // Javascript program for
        // the above approach

        // Function to find the
        // length of the
        // longest subset satisfying
        // given conditions
        function maxLenSubset(a, n)
        {
            // Sort the array in ascending order
            a.sort( function(a, b) {
                return a - b;
            })

            // Stores the starting
            // index and maximum
            // length of the required subset
            let index = 0, maxlen = -1;

            // Pointer to traverse the array
            let i = 0;

            // Iterate while i < n
            while (i < n) {

                // Stores end point
                // of current subset
                let j = i;

                // Store the length of
                // the current subset
                let len = 1;

                // Continue adding elements
                // to the current
                // subset till the
                // condition satisfies
                while (j < n - 1) {

                    if (2 * a[j] >= a[j + 1])
                    {

                        // Increment length of
                        // the current subset
                        len++;
                    }
                    else
                        break;

                    // Increment the pointer j
                    j++;
                }

                // If length of the current subset
                // exceeds overall maximum length
                if (maxlen < len) {

                    // Update maxlen
                    maxlen = len;

                    // Update index
                    index = i;
                }

                // Increment j
                j++;

                // Update i
                i = j;
            }

            // Store the starting index of
            // the required subset in i
            i = index;

            // Print the required subset
            while (maxlen > 0) {

                // Print the array element
                document.write(a[i]+" ")
                // Decrement maxlen
                maxlen--;

                // Increment i
                i++;
            }
        }

        // Driver Code

        // Given array
        let a = [3, 1, 5, 11];

        // Store the size of the array
        let n = a.length

        maxLenSubset(a, n)

        // This code is contributed by Hritik

    </script>
```

**Output:** 

```
3 5
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*