# 通过将数组元素拆分为最多 K 次的 2 的幂来最小化最大数组元素

> 原文:[https://www . geeksforgeeks . org/通过将数组元素拆分为最多 k 倍的二次幂来最小化最大数组元素/](https://www.geeksforgeeks.org/minimize-maximum-array-element-by-splitting-array-elements-into-powers-of-two-at-most-k-times/)

给定一个由 **N** 正整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是通过将数组元素拆分为**2**T13】的[次幂，最多 **K** 次，最小化数组](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)的[最大值。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

**示例:**

> **输入:** arr[] = {2，4，11，2}，K = 2
> **输出:** 2
> **解释:**
> 以下是对数组元素最多 K(= 2)次执行的操作:
> **操作 1:** 删除索引 2 处的元素，即 arr[2] = 11，替换为其中的 11 个 1。现在数组 arr[]修改为{2，4，1，1，1，1，1，1，1，1，1，1，1，1，1，1，2}。
> **操作 2:** 删除索引 1 处的元素，即 arr[1] = 4，并用其中的 4 个 1 替换。现在数组 arr[]修改为{2，1，1，1，1，1，1，1，1，1，1，1，1，1，1，1，1，1，2}。
> 
> 执行上述操作后，数组的最大值为 2，这是最小可能值。
> 
> **输入:** arr[]= {9}，K = 2
> T3】输出: 1

**逼近:**利用每个数都可以表示为 **1** 的和，这个和是 2 的**次方，可以解决给定的问题。按照以下步骤解决问题:**

*   [按降序排列数组 arr[]](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   [在数组**arr【】**](https://www.geeksforgeeks.org/find-number-zeroes/)中找到 0 的计数，如果计数的值为 **N** ，则打印 **0** 作为数组的最小最大值
*   否则，如果 **K** 的值至少为**N**，则打印 **1** 作为数组的合成最小最大值
*   否则，打印**arr【K】**的值作为数组的最小最大值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum value
// of the maximum element of the array
// by splitting at most K array element
// into perfect powers of 2
void minimumSize(int arr[], int N, int K)
{
    // Sort the array element in
    // the ascending order
    sort(arr, arr + N);

    // Reverse the array
    reverse(arr, arr + N);

    // If count of 0 is equal to N
    if (count(arr, arr + N, 0) == N)
        cout << 0;

    // Otherwise, if K is greater
    // than or equal to N
    else if (K >= N)
        cout << 1 << endl;

    // Otherwise
    else
        cout << arr[K] << endl;
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 8, 2 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);
    minimumSize(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the minimum value
// of the maximum element of the array
// by splitting at most K array element
// into perfect powers of 2
static void minimumSize(int arr[], int N, int K)
{

    // Sort the array element in
    // the ascending order
    Arrays.sort(arr);

    // Reverse the array
    reverse(arr);

    // If count of 0 is equal to N
    if (count(arr, 0) == N)
        System.out.println(0);

    // Otherwise, if K is greater
    // than or equal to N
    else if (K >= N)
        System.out.println(1);

    // Otherwise
    else
        System.out.println(arr[K]);
}

static void reverse(int[] a)
{
    int i, k, t;
    int n = a.length;

    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}

static int count(int[] a, int n)
{
    int freq = 0;

    for(int i = 0; i < a.length; i++)
    {
        if (a[i] == n)
            freq++;
    }
    return freq;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 4, 8, 2 };
    int K = 2;
    int N = arr.length;

    minimumSize(arr, N, K);
}
}

// This code is contributed by offbeat
```

## 计算机编程语言

```
# Python program for the above approach

# Function to find the minimum value
# of the maximum element of the array
# by splitting at most K array element
# into perfect powers of 2
def minimumSize(arr, N, K):

    # Sort the array element in
    # the ascending order
    arr.sort()

    # Reverse the array
    arr.reverse()

    # If count of 0 is equal to N
    zero = arr.count(0)
    if zero == N:
        print(0)

    # Otherwise, if K is greater
    # than or equal to N
    elif K >= N:
        print(1)

    # Otherwise
    else:
        print(arr[K])

# Driver Code
arr = [2, 4, 8, 2]
K = 2
N = len(arr)
minimumSize(arr, N, K)

# This code is contributed by sudhanshugupta2019a.
```

## C#

```
// C#program for the above approach
using System;
class GFG
{

    // Function to find the minimum value
    // of the maximum element of the array
    // by splitting at most K array element
    // into perfect powers of 2
    static void minimumSize(int[] arr, int N, int K)
    {

        // Sort the array element in
        // the ascending order
        Array.Sort(arr);

        // Reverse the array
        Array.Reverse(arr);

        // If count of 0 is equal to N
        if (count(arr, 0) == N)
            Console.WriteLine(0);

        // Otherwise, if K is greater
        // than or equal to N
        else if (K >= N)
            Console.WriteLine(1);

        // Otherwise
        else
            Console.WriteLine(arr[K]);
    }

    static void reverse(int[] a)
    {
        int i, t;
        int n = a.Length;

        for (i = 0; i < n / 2; i++) {
            t = a[i];
            a[i] = a[n - i - 1];
            a[n - i - 1] = t;
        }
    }

    static int count(int[] a, int n)
    {
        int freq = 0;

        for (int i = 0; i < a.Length; i++) {
            if (a[i] == n)
                freq++;
        }
        return freq;
    }

    // Driver code
    public static void Main(string[] args)
    {
        int[] arr = { 2, 4, 8, 2 };
        int K = 2;
        int N = arr.Length;

        minimumSize(arr, N, K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum value
// of the maximum element of the array
// by splitting at most K array element
// into perfect powers of 2
function minimumSize(arr,N,K)
{
    // Sort the array element in
    // the ascending order
    (arr).sort(function(a,b){return a-b;});

    // Reverse the array
    reverse(arr);

    // If count of 0 is equal to N
    if (count(arr, 0) == N)
        document.write(0);

    // Otherwise, if K is greater
    // than or equal to N
    else if (K >= N)
        document.write(1);

    // Otherwise
    else
        document.write(arr[K]);
}

function reverse(a)
{
    let i, k, t;
    let n = a.length;

    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}

function count(a,n)
{
    let freq = 0;

    for(let i = 0; i < a.length; i++)
    {
        if (a[i] == n)
            freq++;
    }
    return freq;
}

// Driver code
let arr=[2, 4, 8, 2];
let K = 2;
let N = arr.length;
minimumSize(arr, N, K);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(1)*