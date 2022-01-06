# 从给定阵列元素形成排列的子阵列的计数

> 原文:[https://www . geeksforgeeks . org/从给定数组元素形成排列的子数组计数/](https://www.geeksforgeeks.org/count-of-subarrays-which-forms-a-permutation-from-given-array-elements/)

给定一个由整数**【1，N】**组成的数组 **A[]** ，任务是计算所有可能长度的子阵列的总数 **x** ( **1 ≤ x ≤ N** )，由给定数组中的整数**【1，x】**排列组成。

**示例:**

> **输入:** A[] = {3，1，2，5，4} **输出:** 4
> **解释:**
> 形成排列的子阵有{1}、{1，2}、{3，1，2}和{3，1，2，5，4}。
> 
> **输入:** A[] = {4，5，1，3，2，6} **输出:** 4
> **解释:**
> 形成排列的子阵有{1}、{1，3，2}、{4，5，1，3，2}和{4，5，1，3，2，6}。

**天真方法:**
按照以下步骤解决问题:

*   解决问题最简单的方法就是[生成所有可能的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)。
*   对于每个子阵列，检查它是否是范围**【1，子阵列长度】**中元素的排列。
*   每发现一个这样的子阵列，增加**计数**。最后，打印**计数**。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**
要优化上述方法，请按照以下步骤操作:

*   对于从**I =【1，N】**开始的每个元素，检查**最大值**和**最小指数**，在此处存在排列**【1，I】**的元素。
*   如果**最大值**和**最小指数**之差等于 **i** ，则意味着 I 存在有效的连续排列
*   对于每一个这样的排列，增加**计数**。最后，打印**计数**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function returns the required count
int PermuteTheArray(int A[], int n)
{

    int arr[n];

    // Store the indices of the
    // elements present in A[].
    for (int i = 0; i < n; i++) {
        arr[A[i] - 1] = i;
    }

    // Store the maximum and
    // minimum index of the
    // elements from 1 to i.
    int mini = n, maxi = 0;
    int count = 0;

    for (int i = 0; i < n; i++) {

        // Update maxi and mini, to
        // store minimum and maximum
        // index for permutation
        // of elements from 1 to i+1
        mini = min(mini, arr[i]);
        maxi = max(maxi, arr[i]);

        // If difference between maxi
        // and mini is equal to i
        if (maxi - mini == i)

            // Increase count
            count++;
    }

    // Return final count
    return count;
}

// Driver Code
int main()
{

    int A[] = { 4, 5, 1, 3, 2, 6 };
    cout << PermuteTheArray(A, 6);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function returns the required count
static int PermuteTheArray(int A[], int n)
{
    int []arr = new int[n];

    // Store the indices of the
    // elements present in A[].
    for(int i = 0; i < n; i++)
    {
        arr[A[i] - 1] = i;
    }

    // Store the maximum and
    // minimum index of the
    // elements from 1 to i.
    int mini = n, maxi = 0;
    int count = 0;

    for(int i = 0; i < n; i++)
    {

        // Update maxi and mini, to
        // store minimum and maximum
        // index for permutation
        // of elements from 1 to i+1
        mini = Math.min(mini, arr[i]);
        maxi = Math.max(maxi, arr[i]);

        // If difference between maxi
        // and mini is equal to i
        if (maxi - mini == i)

            // Increase count
            count++;
    }

    // Return final count
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 4, 5, 1, 3, 2, 6 };

    System.out.print(PermuteTheArray(A, 6));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function returns the required count
def PermuteTheArray(A, n):

    arr = [0] * n

    # Store the indices of the
    # elements present in A[].
    for i in range(n):
        arr[A[i] - 1] = i

    # Store the maximum and
    # minimum index of the
    # elements from 1 to i.
    mini = n
    maxi = 0
    count = 0

    for i in range(n):

        # Update maxi and mini, to
        # store minimum and maximum
        # index for permutation
        # of elements from 1 to i+1
        mini = min(mini, arr[i])
        maxi = max(maxi, arr[i])

        # If difference between maxi
        # and mini is equal to i
        if (maxi - mini == i):

            # Increase count
            count += 1

    # Return final count
    return count

# Driver Code
if __name__ == "__main__":

    A = [ 4, 5, 1, 3, 2, 6 ]

    print(PermuteTheArray(A, 6))

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function returns the required count
static int PermuteTheArray(int []A, int n)
{
    int []arr = new int[n];

    // Store the indices of the
    // elements present in []A.
    for(int i = 0; i < n; i++)
    {
        arr[A[i] - 1] = i;
    }

    // Store the maximum and
    // minimum index of the
    // elements from 1 to i.
    int mini = n, maxi = 0;
    int count = 0;

    for(int i = 0; i < n; i++)
    {

        // Update maxi and mini, to
        // store minimum and maximum
        // index for permutation
        // of elements from 1 to i+1
        mini = Math.Min(mini, arr[i]);
        maxi = Math.Max(maxi, arr[i]);

        // If difference between maxi
        // and mini is equal to i
        if (maxi - mini == i)

            // Increase count
            count++;
    }

    // Return final count
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 4, 5, 1, 3, 2, 6 };

    Console.Write(PermuteTheArray(A, 6));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function returns the required count
function PermuteTheArray(A, n)
{

    var arr = Array(n);

    // Store the indices of the
    // elements present in A[].
    for (var i = 0; i < n; i++) {
        arr[A[i] - 1] = i;
    }

    // Store the maximum and
    // minimum index of the
    // elements from 1 to i.
    var mini = n, maxi = 0;
    var count = 0;

    for (var i = 0; i < n; i++) {

        // Update maxi and mini, to
        // store minimum and maximum
        // index for permutation
        // of elements from 1 to i+1
        mini = Math.min(mini, arr[i]);
        maxi = Math.max(maxi, arr[i]);

        // If difference between maxi
        // and mini is equal to i
        if (maxi - mini == i)

            // Increase count
            count++;
    }

    // Return final count
    return count;
}

// Driver Code
var A = [4, 5, 1, 3, 2, 6];
document.write( PermuteTheArray(A, 6));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*