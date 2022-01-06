# 对于给定数组的任何排列，最大化第一个元素与剩余元素的补码的按位“与”

> 原文:[https://www . geeksforgeeks . org/给定数组的任意排列的第一个元素的按位最大化和剩余元素的补数/](https://www.geeksforgeeks.org/maximize-bitwise-and-of-first-element-with-complement-of-remaining-elements-for-any-permutation-of-given-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是为该数组的任何排列找到第一个元素的按位“与”的最大值以及剩余元素的补数，即

> **A<sub>1</sub>T10(~ A<sub>2</sub>)&(~ A<sub>3</sub>)&……&(~ A<sub>n</sub>)**

**示例:**

> **输入:** arr[] = {1，2，4，8，16}
> **输出:** 16
> **解释:**
> 对于排列{16，1，2，4，8}，可以得到表达式的最大值。
> 
> **输入:** arr[] = {0，2，3，4，9，8}
> **输出:** 4
> **解释:**
> 对于排列{4，8，9，3，2，0}，可以得到表达式的最大值

**天真法:**解决问题最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)的所有可能的排列，并找到每个排列所需的值，打印其中的最大值。
***时间复杂度:** O(N * N！)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以通过以下观察进行优化:

*   表达式**A<sub>1</sub>&(~ A<sub>2</sub>)&(~ A<sub>3</sub>)&……&(~ A<sub>n</sub>)**仅取决于 A <sub>1 的值。</sub>
*   因此，为了从表达式中获得最大值，选择 A <sub>1</sub> ，使得它具有尽可能最高意义的 [**设置位**](https://www.geeksforgeeks.org/find-position-of-the-only-set-bit/) ，该设置位在所有其他数组元素中是未设置的。
*   因为剩余数组元素的顺序无关紧要，所以打印任何将获得的 A <sub>1</sub> 作为第一个元素的排列。

> **图解:**
> 对于 arr[] = {1，2，4，8，16}
> 数组元素的二进制表示:
> (16)<sub>10</sub>=(10000)<sub>2</sub>
> (8)<sub>10</sub>=(01000)<sub>2</sub>
> (4)<sub>10</sub>=(00100)<sub>因此，给定置换所需的置换将包含 16 作为第一个元素。
> 因此，对于第一个元素为 16 的置换，所需的按位“与”是最大值，在这种情况下等于 16。</sub>

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

#define size_int 32

// Function to maximize the value for
// the given function and the array elements
int functionMax(int arr[], int n)
{
    // Vector array to maintain which bit is set
    // for which integer in the given array by
    // saving index of that integer
    vector<int> setBit[32];

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < size_int; j++) {

            // Check if j-th bit is set for
            // i-th integer
            if (arr[i] & (1 << j))

                // Push the index of that
                // integer in setBit[j]
                setBit[j].push_back(i);
        }
    }

    // Find the element having
    // highest significant set bit
    // unset in other elements
    for (int i = size_int; i >= 0; i--) {
        if (setBit[i].size() == 1) {

            // Place that integer at 0-th index
            swap(arr[0], arr[setBit[i][0]]);
            break;
        }
    }

    // Store the maximum AND value
    int maxAnd = arr[0];
    for (int i = 1; i < n; i++) {
        maxAnd = maxAnd & (~arr[i]);
    }

    // Return the answer
    return maxAnd;
}

// Driver Code
int main()
{

    int arr[] = { 1, 2, 4, 8, 16 };
    int n = sizeof arr / sizeof arr[0];

    // Function call
    cout << functionMax(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

static final int size_int = 32;

// Function to maximize the value for
// the given function and the array elements
static int functionMax(int arr[], int n)
{
    // Vector array to maintain which bit is set
    // for which integer in the given array by
    // saving index of that integer
    Vector<Integer> []setBit = new Vector[32 + 1];
    for (int i = 0; i < setBit.length; i++)
        setBit[i] = new Vector<Integer>();
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < size_int; j++)
        {

            // Check if j-th bit is set for
            // i-th integer
            if ((arr[i] & (1 << j)) > 0)

                // Push the index of that
                // integer in setBit[j]
                setBit[j].add(i);
        }
    }

    // Find the element having
    // highest significant set bit
    // unset in other elements
    for (int i = size_int; i >= 0; i--)
    {
        if (setBit[i].size() == 1)
        {

            // Place that integer at 0-th index
            swap(arr, 0, setBit[i].get(0));
            break;
        }
    }

    // Store the maximum AND value
    int maxAnd = arr[0];
    for (int i = 1; i < n; i++)
    {
        maxAnd = maxAnd & (~arr[i]);
    }

    // Return the answer
    return maxAnd;
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver Code
public static void main(String[] args)
{

    int arr[] = { 1, 2, 4, 8, 16 };
    int n = arr.length;

    // Function call
    System.out.print(functionMax(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 Program to
# implement the above approach

# Function to maximize the
# value for the given function
# and the array elements
def functionMax(arr, n):

    # Vector array to maintain
    # which bit is set for which
    # integer in the given array by
    # saving index of that integer
    setBit = [[] for i in range(32)]

    for i in range(n):
        for j in range(32):

            # Check if j-th bit is
            # set for i-th integer
            if (arr[i] & (1 << j)):

                # Push the index of that
                # integer in setBit[j]
                setBit[j].append(i)

    # Find the element having
    # highest significant set bit
    # unset in other elements
    i = 31

    while(i >= 0):
        if (len(setBit[i]) == 1):

            # Place that integer
            # at 0-th index
            temp = arr[0]
            arr[0] = arr[setBit[i][0]]
            arr[setBit[i][0]] = temp
            break
        i -= 1

    # Store the maximum
    # AND value
    maxAnd = arr[0]
    for i in range(1, n, 1):
        maxAnd = (maxAnd & (~arr[i]))

    # Return the answer
    return maxAnd

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 4, 8, 16]
    n = len(arr)

    # Function call
    print(functionMax(arr, n))

# This code is contributed by bgangwar59
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

static readonly int size_int = 32;

// Function to maximize the value for
// the given function and the array elements
static int functionMax(int []arr, int n)
{
    // List array to maintain which bit is set
    // for which integer in the given array by
    // saving index of that integer
    List<int> []setBit = new List<int>[32 + 1];
    for (int i = 0; i < setBit.Length; i++)
        setBit[i] = new List<int>();
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < size_int; j++)
        {

            // Check if j-th bit is set for
            // i-th integer
            if ((arr[i] & (1 << j)) > 0)

                // Push the index of that
                // integer in setBit[j]
                setBit[j].Add(i);
        }
    }

    // Find the element having
    // highest significant set bit
    // unset in other elements
    for (int i = size_int; i >= 0; i--)
    {
        if (setBit[i].Count == 1)
        {

            // Place that integer at 0-th index
            swap(arr, 0, setBit[i][0]);
            break;
        }
    }

    // Store the maximum AND value
    int maxAnd = arr[0];
    for (int i = 1; i < n; i++)
    {
        maxAnd = maxAnd & (~arr[i]);
    }

    // Return the answer
    return maxAnd;
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver Code
public static void Main(String[] args)
{

    int []arr = { 1, 2, 4, 8, 16 };
    int n = arr.Length;

    // Function call
    Console.Write(functionMax(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach
var size_int = 32;

// Function to maximize the value for
// the given function and the array elements
function functionMax( arr, n)
{
    // Vector array to maintain which bit is set
    // for which integer in the given array by
    // saving index of that integer
    var setBit = Array.from(Array(32), ()=>new Array());

    for (var i = 0; i < n; i++) {
        for (var j = 0; j < size_int; j++) {

            // Check if j-th bit is set for
            // i-th integer
            if (arr[i] & (1 << j))

                // Push the index of that
                // integer in setBit[j]
                setBit[j].push(i);
        }
    }

    // Find the element having
    // highest significant set bit
    // unset in other elements
    for (var i = size_int-1; i >= 0; i--) {
        if (setBit[i].length == 1) {

            // Place that integer at 0-th index
            [arr[0], arr[setBit[i][0]]] = [arr[setBit[i][0]], arr[0]];
            break;
        }
    }

    // Store the maximum AND value
    var maxAnd = arr[0];
    for (var i = 1; i < n; i++) {
        maxAnd = maxAnd & (~arr[i]);
    }

    // Return the answer
    return maxAnd;
}

// Driver Code
var arr = [1, 2, 4, 8, 16];
var n = arr.length;

// Function call
document.write( functionMax(arr, n));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
16
```

***时间复杂度:** O(N * sizeof(int))，其中 sizeof(int)为 32*
***辅助空间:** O(N)*