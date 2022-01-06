# 计算每个数组元素的子序列，其中它们是最大的

> 原文:[https://www . geesforgeks . org/count-subseries-for-ever-array-element-in-the-max/](https://www.geeksforgeeks.org/count-subsequences-for-every-array-element-in-which-they-are-the-maximum/)

给定一个由 **N** 个唯一元素组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是生成一个长度为 **N** 的数组 **B[]** ，使得 **B[i]** 是[个子序列](https://www.geeksforgeeks.org/print-subsequences-string/) 的数量，其中 **arr[i]** 是最大元素。

**示例:**

> **输入:** arr[] = {2，3，1}
> **输出:** {2，4，1}
> **解释:**arr[0](= 2)最大的子序列为{2}、{2，1}。
> arr[1](= 3)最大的子序列是{3}、{1，3，2}、{2，3}、{1，3}。
> arr[2](= 1)最大的子序列是{1}。
> 
> **输入:** arr[] = {23，34，12，7，15，31}
> **输出:** {8，32，2，1，4，16}

**方法:**通过观察一个元素**arr【I】**出现的所有子序列，可以解决这个问题，因为最大值将包含比**arr【I】**少的所有元素。因此，[不同子序列](https://www.geeksforgeeks.org/count-distinct-subsequences/)的总数将为 **2 <sup>(小于 arr[i]的元素数)</sup>** 。按照以下步骤解决问题:

1.  [根据给定数组中的相应值对数组](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/) **arr[]** 索引进行排序，并将该索引存储在数组**indexes[]**中，其中**arr[indexes[I]]【T8]arr[indexes[I+1]]【T7]。**
2.  初始化一个整数，用 **1** 对**子序列**进行初始化，以存储可能的子序列的数量。
3.  用指针在范围**【0，N-1】**上使用变量 **i** 迭代 **N 次。**
    1.  **B[indexes[I]]**是子序列的数量，其中**arr[indexes[I]]【T3]最大，即**2<sup>I</sup>T7】，因为将有小于**arr[indexes[I]]的 **i** 元素。******
    2.  将 **B【指数[I]】**的答案存储为 **B【指数[I]】=子 q** 。
    3.  通过将其乘以 **2** 来更新**子节**。
4.  打印数组的元素 **B[]** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to merge the subarrays
// arr[l .. m] and arr[m + 1, .. r]
// based on indices[]
void merge(int* indices, int* a, int l,
           int mid, int r)
{
    int temp_ind[r - l + 1], j = mid + 1;
    int i = 0, temp_l = l, k;
    while (l <= mid && j <= r) {

        // If a[indices[l]] is less than
        // a[indices[j]], add indice[l] to temp
        if (a[indices[l]] < a[indices[j]])
            temp_ind[i++] = indices[l++];

        // Else add indices[j]
        else
            temp_ind[i++] = indices[j++];
    }

    // Add remaining elements
    while (l <= mid)
        temp_ind[i++] = indices[l++];

    // Add remainging elements
    while (j <= r)
        temp_ind[i++] = indices[j++];
    for (k = 0; k < i; k++)
        indices[temp_l++] = temp_ind[k];
}

// Recursive function to divide
// the array into to parts
void divide(int* indices, int* a, int l, int r)
{
    if (l >= r)
        return;
    int mid = l / 2 + r / 2;

    // Recursive call for elements before mid
    divide(indices, a, l, mid);

    // Recursive call for elements after mid
    divide(indices, a, mid + 1, r);

    // Merge the two sorted arrays
    merge(indices, a, l, mid, r);
}

// Function to find the number of
// subsequences for each element
void noOfSubsequences(int arr[], int N)
{
    int indices[N], i;
    for (i = 0; i < N; i++)
        indices[i] = i;

    // Sorting the indices according
    // to array arr[]
    divide(indices, arr, 0, N - 1);

    // Array to store output numbers
    int B[N];

    // Initialize subseq
    int subseq = 1;
    for (i = 0; i < N; i++) {

        // B[i] is 2^i
        B[indices[i]] = subseq;

        // Doubling the subsequences
        subseq *= 2;
    }
    // Print the final output, array B[]
    for (i = 0; i < N; i++)
        cout << B[i] << " ";
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 2, 3, 1 };

    // Given length
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    noOfSubsequences(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to merge the subarrays
// arr[l .. m] and arr[m + 1, .. r]
// based on indices[]
static void merge(int[] indices, int[] a, int l,
                  int mid, int r)
{
    int []temp_ind = new int[r - l + 1];
    int j = mid + 1;
    int i = 0, temp_l = l, k;

    while (l <= mid && j <= r)
    {

        // If a[indices[l]] is less than
        // a[indices[j]], add indice[l] to temp
        if (a[indices[l]] < a[indices[j]])
            temp_ind[i++] = indices[l++];

        // Else add indices[j]
        else
            temp_ind[i++] = indices[j++];
    }

    // Add remaining elements
    while (l <= mid)
        temp_ind[i++] = indices[l++];

    // Add remainging elements
    while (j <= r)
        temp_ind[i++] = indices[j++];

    for(k = 0; k < i; k++)
        indices[temp_l++] = temp_ind[k];
}

// Recursive function to divide
// the array into to parts
static void divide(int[] indices, int[] a,
                   int l, int r)
{
    if (l >= r)
        return;

    int mid = l / 2 + r / 2;

    // Recursive call for elements before mid
    divide(indices, a, l, mid);

    // Recursive call for elements after mid
    divide(indices, a, mid + 1, r);

    // Merge the two sorted arrays
    merge(indices, a, l, mid, r);
}

// Function to find the number of
// subsequences for each element
static void noOfSubsequences(int arr[], int N)
{
    int []indices = new int[N];
    int i;

    for(i = 0; i < N; i++)
        indices[i] = i;

    // Sorting the indices according
    // to array arr[]
    divide(indices, arr, 0, N - 1);

    // Array to store output numbers
    int[] B = new int[N];

    // Initialize subseq
    int subseq = 1;

    for(i = 0; i < N; i++)
    {

        // B[i] is 2^i
        B[indices[i]] = subseq;

        // Doubling the subsequences
        subseq *= 2;
    }

    // Print the final output, array B[]
    for(i = 0; i < N; i++)
        System.out.print(B[i] + " ");
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 2, 3, 1 };

    // Given length
    int N = arr.length;

    // Function call
    noOfSubsequences(arr, N);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to merge the subarrays
# arr[l .. m] and arr[m + 1, .. r]
# based on indices[]
def merge(indices, a, l, mid, r):

    temp_ind = [0] * (r - l + 1)
    j = mid + 1
    i = 0
    temp_l = l

    while (l <= mid and j <= r):

        # If a[indices[l]] is less than
        # a[indices[j]], add indice[l] to temp
        if (a[indices[l]] < a[indices[j]]):
            temp_ind[i] = indices[l]
            i += 1
            l += 1

        # Else add indices[j]
        else:
            temp_ind[i] = indices[j]
            i += 1
            j += 1

    # Add remaining elements
    while (l <= mid):
        temp_ind[i] = indices[l]
        i += 1
        l += 1

    # Add remainging elements
    while (j <= r):
        temp_ind[i] = indices[j]
        i += 1
        j += 1

    for k in range(i):
        indices[temp_l] = temp_ind[k]
        temp_l += 1

# Recursive function to divide
# the array into to parts
def divide(indices, a, l, r):

    if (l >= r):
        return

    mid = l // 2 + r // 2

    # Recursive call for elements
    # before mid
    divide(indices, a, l, mid)

    # Recursive call for elements
    # after mid
    divide(indices, a, mid + 1, r)

    # Merge the two sorted arrays
    merge(indices, a, l, mid, r)

# Function to find the number of
# subsequences for each element
def noOfSubsequences(arr, N):

    indices = N * [0]
    for i in range(N):
        indices[i] = i

    # Sorting the indices according
    # to array arr[]
    divide(indices, arr, 0, N - 1)

    # Array to store output numbers
    B = [0] * N

    # Initialize subseq
    subseq = 1
    for i in range(N):

        # B[i] is 2^i
        B[indices[i]] = subseq

        # Doubling the subsequences
        subseq *= 2

    # Print the final output, array B[]
    for i in range(N):
        print(B[i], end = " ")

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [ 2, 3, 1 ]

    # Given length
    N = len(arr)

    # Function call
    noOfSubsequences(arr, N)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to merge the subarrays
// arr[l .. m] and arr[m + 1, .. r]
// based on indices[]
static void merge(int[] indices, int[] a, int l,
                  int mid, int r)
{
    int []temp_ind = new int[r - l + 1];
    int j = mid + 1;
    int i = 0, temp_l = l, k;

    while (l <= mid && j <= r)
    {

        // If a[indices[l]] is less than
        // a[indices[j]], add indice[l] to temp
        if (a[indices[l]] < a[indices[j]])
            temp_ind[i++] = indices[l++];

        // Else add indices[j]
        else
            temp_ind[i++] = indices[j++];
    }

    // Add remaining elements
    while (l <= mid)
        temp_ind[i++] = indices[l++];

    // Add remainging elements
    while (j <= r)
        temp_ind[i++] = indices[j++];

    for(k = 0; k < i; k++)
        indices[temp_l++] = temp_ind[k];
}

// Recursive function to divide
// the array into to parts
static void divide(int[] indices, int[] a,
                   int l, int r)
{
    if (l >= r)
        return;

    int mid = l / 2 + r / 2;

    // Recursive call for elements before mid
    divide(indices, a, l, mid);

    // Recursive call for elements after mid
    divide(indices, a, mid + 1, r);

    // Merge the two sorted arrays
    merge(indices, a, l, mid, r);
}

// Function to find the number of
// subsequences for each element
static void noOfSubsequences(int []arr, int N)
{
    int []indices = new int[N];
    int i;

    for(i = 0; i < N; i++)
        indices[i] = i;

    // Sorting the indices according
    // to array []arr
    divide(indices, arr, 0, N - 1);

    // Array to store output numbers
    int[] B = new int[N];

    // Initialize subseq
    int subseq = 1;

    for(i = 0; i < N; i++)
    {

        // B[i] is 2^i
        B[indices[i]] = subseq;

        // Doubling the subsequences
        subseq *= 2;
    }

    // Print the readonly output, array []B
    for(i = 0; i < N; i++)
        Console.Write(B[i] + " ");
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 2, 3, 1 };

    // Given length
    int N = arr.Length;

    // Function call
    noOfSubsequences(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to merge the subarrays
// arr[l .. m] and arr[m + 1, .. r]
// based on indices[]
function merge(indices, a, l, mid, r)
{
    let temp_ind = [];
    let j = mid + 1;
    let i = 0, temp_l = l, k;

    while (l <= mid && j <= r)
    {

        // If a[indices[l]] is less than
        // a[indices[j]], add indice[l] to temp
        if (a[indices[l]] < a[indices[j]])
            temp_ind[i++] = indices[l++];

        // Else add indices[j]
        else
            temp_ind[i++] = indices[j++];
    }

    // Add remaining elements
    while (l <= mid)
        temp_ind[i++] = indices[l++];

    // Add remainging elements
    while (j <= r)
        temp_ind[i++] = indices[j++];

    for(k = 0; k < i; k++)
        indices[temp_l++] = temp_ind[k];
}

// Recursive function to divide
// the array leto to parts
function divide(indices, a, l, r)
{
    if (l >= r)
        return;

    let mid = l / 2 + r / 2;

    // Recursive call for elements before mid
    divide(indices, a, l, mid);

    // Recursive call for elements after mid
    divide(indices, a, mid + 1, r);

    // Merge the two sorted arrays
    merge(indices, a, l, mid, r);
}

// Function to find the number of
// subsequences for each element
function noOfSubsequences(arr, N)
{
    let indices = [];
    let i;

    for(i = 0; i < N; i++)
        indices[i] = i;

    // Sorting the indices according
    // to array arr[]
    divide(indices, arr, 0, N - 1);

    // Array to store output numbers
    let B = [];

    // Initialize subseq
    let subseq = 1;

    for(i = 0; i < N; i++)
    {

        // B[i] is 2^i
        B[indices[i]] = subseq;

        // Doubling the subsequences
        subseq *= 2;
    }

    // Print the final output, array B[]
    for(i = 0; i < N; i++)
        document.write(B[i] + " ");
}

// Driver code

// Given array
let arr = [ 2, 3, 1 ];

// Given length
let N = arr.length;

// Function call
noOfSubsequences(arr, N);

// This code is contributed by avijitmondal1998

</script>
```

**Output:** 

```
2 4 1
```

***时间复杂度:** O(NlogN)，其中 N 是给定数组的长度。*
***辅助空间:** O(N)*