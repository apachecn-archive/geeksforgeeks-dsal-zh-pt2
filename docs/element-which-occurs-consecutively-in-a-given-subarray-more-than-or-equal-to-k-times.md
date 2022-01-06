# 在给定子阵列中连续出现大于或等于 K 次的元素

> 原文:[https://www . geeksforgeeks . org/element-在给定的子阵列中连续出现的次数大于或等于 k 次/](https://www.geeksforgeeks.org/element-which-occurs-consecutively-in-a-given-subarray-more-than-or-equal-to-k-times/)

给定一个大小为 N 和 Q 的查询数组，每个查询由 L、R 和 K 组成(考虑 L 和 R 的基于 1 的索引)。任务是为子阵列[L，R]中连续出现大于或等于 K 次的每个查询找到一个元素。k 永远大于**楼层((R-L+1)/2)** 。如果不存在这样的元素，打印-1。
**例:**

> **输入:**arr[]=【1，3，3，3，4】
> Q = 1
> L = 1，R = 5，K = 3
> T5】输出: 3
> 元素 3 在范围【1，5】
> **内连续出现 3 次输入:**arr[]=【3，2，1，1，2，2，2，2，2】
> Q = 2
> L = 2，R = 6，K = 3

**方法:**创建两个辅助数组 ***左*** 和 ***右*** 大小为 n，*左*数组将存储数组中连续出现的从开始的元素计数。*右侧*数组将存储数组中连续出现的元素计数。因为问题中给出了 k 永远大于**楼层((R-L+1)/2)** 。因此，如果任何这样的元素存在于给定的范围内，它总是位于索引**中间**。数学上，**min { right[mid]+mid-1，r-1 }-max { mid-left[mid]+1，l-1 }+1**将给出位于索引 mid 的子阵列 L-R 中的元素范围。如果范围超过或等于 k，则返回 a[mid]元素。如果不是，则返回-1。
以下是上述办法的实施:

## C++

```
// CPP program to find the element for each
// query that occurs consecutively in the
// subarray [L, R] more than or equal to K times.
#include <bits/stdc++.h>
using namespace std;

/// Function to find the element for each
/// query that occurs consecutively in the
/// subarray [L, R] more than or equal to K times.
int findElement(int arr[], int left[], int right[],
                int n, int l, int r, int k)
{
    // find mid point of subarray [L, R]
    int mid = (l - 1 + r - 1) / 2;

    // find starting and ending index of range
    int s = max(mid - left[mid] + 1, l - 1);
    int e = min(right[mid] + mid - 1, r - 1);

    int range = e - s + 1;

    // compare this range with k
    // if it is greater than or
    // equal to k, return element
    if (range >= k)
        return arr[mid];
    // if not then return -1
    else
        return -1;
}

// function to answer query in range [L, R]
int answerQuery(int arr[], int n, int l, int r, int k)
{
    int left[n], right[n];

    // store count of elements that occur
    // consecutively in the array [1, n]
    int count = 1;
    for (int i = 0; i < n - 1; i++) {
        if (arr[i] == arr[i + 1]) {
            left[i] = count;
            count++;
        }
        else {
            left[i] = count;
            count = 1;
        }
    }
    left[n - 1] = count;

    // store count of elements that occur
    // consecutively in the array [n, 1]
    count = 1;
    for (int i = n - 1; i > 0; i--) {
        if (arr[i] == arr[i - 1]) {
            right[i] = count;
            count++;
        }
        else {
            right[i] = count;
            count = 1;
        }
    }
    right[0] = count;

    // Function to return the element
    return findElement(arr, left, right, n, l, r, k);
}

// Driver Code
int main()
{
    int a[] = { 3, 2, 1, 1, 2, 2, 2, 2 };
    int n = sizeof(a) / sizeof(a[0]);

    // 1st query
    int L = 2, R = 6, k = 3;
    cout << answerQuery(a, n, L, R, k) << "\n";

    // 2nd query
    L = 3, R = 8, k = 4;
    cout << answerQuery(a, n, L, R, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the element for each
// query that occurs consecutively in the
// subarray [L, R] more than or equal to K times.
import java.util.*;

class solution
{

/// Function to find the element for each
/// query that occurs consecutively in the
/// subarray [L, R] more than or equal to K times.
static int findElement(int[] arr, int[] left, int[] right,
                int n, int l, int r, int k)
{
    // find mid point of subarray [L, R]
    int mid = (l - 1 + r - 1) / 2;

    // find starting and ending index of range
    int s = Math.max(mid - left[mid] + 1, l - 1);
    int e = Math.min(right[mid] + mid - 1, r - 1);

    int range = e - s + 1;

    // compare this range with k
    // if it is greater than or
    // equal to k, return element
    if (range >= k)
        return arr[mid];
    // if not then return -1
    else
        return -1;
}

// function to answer query in range [L, R]
static int answerQuery(int arr[], int n, int l, int r, int k)
{
    int[] left = new int[n];
    int[] right = new int[n];

    // store count of elements that occur
    // consecutively in the array [1, n]
    int count = 1;
    for (int i = 0; i < n - 1; i++) {
        if (arr[i] == arr[i + 1]) {
            left[i] = count;
            count++;
        }
        else {
            left[i] = count;
            count = 1;
        }
    }
    left[n - 1] = count;

    // store count of elements that occur
    // consecutively in the array [n, 1]
    count = 1;
    for (int i = n - 1; i > 0; i--) {
        if (arr[i] == arr[i - 1]) {
            right[i] = count;
            count++;
        }
        else {
            right[i] = count;
            count = 1;
        }
    }
    right[0] = count;

    // Function to return the element
    return findElement(arr, left, right, n, l, r, k);
}

// Driver Code
public static void main(String args[])
{
    int[] a = { 3, 2, 1, 1, 2, 2, 2, 2 };
    int n = a.length;

    // 1st query
    int L = 2, R = 6, k = 3;
    System.out.println(answerQuery(a, n, L, R, k));

    // 2nd query
    L = 3;
    R = 8;
    k = 4;
    System.out.println(answerQuery(a, n, L, R, k));
}

}
// This code is contributed by
// Shashank_Sharma
```

## 蟒蛇 3

```
# Python3 program to find the element for each
# query that occurs consecutively in the
# subarray [L, R] more than or equal to K times.

# Function to find the element for each
# query that occurs consecutively in the
# subarray [L, R] more than or equal to K times.
def findElement(arr, left, right, n, l, r, k):

    # find mid point of subarray [L, R]
    mid = (l - 1 + r - 1) // 2

    # find starting and ending index of range
    s = max(mid - left[mid] + 1, l - 1)
    e = min(right[mid] + mid - 1, r - 1)

    _range = e - s + 1

    # compare this range with k
    # if it is greater than or
    # equal to k, return element
    if _range >= k:
        return arr[mid]
    # if not then return -1
    else:
        return -1

# function to answer query in range [L, R]
def answerQuery(arr, n, l, r, k):

    left, right = [None] * n, [None] * n

    # store count of elements that occur
    # consecutively in the array [1, n]
    count = 1
    for i in range(0, n - 1): 
        if arr[i] == arr[i + 1]: 
            left[i] = count
            count += 1

        else:
            left[i] = count
            count = 1

    left[n - 1] = count

    # store count of elements that occur
    # consecutively in the array [n, 1]
    count = 1
    for i in range(n - 1, 0, -1): 
        if arr[i] == arr[i - 1]: 
            right[i] = count
            count += 1

        else:
            right[i] = count
            count = 1

    right[0] = count

    # Function to return the element
    return findElement(arr, left, right, n, l, r, k)

# Driver Code
if __name__ == "__main__":

    a = [3, 2, 1, 1, 2, 2, 2, 2] 
    n = len(a)

    # 1st query
    L, R, k = 2, 6, 3
    print(answerQuery(a, n, L, R, k))

    # 2nd query
    L, R, k = 3, 8, 4
    print(answerQuery(a, n, L, R, k))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find the element for each
// query that occurs consecutively in the
// subarray [L, R] more than or equal to K times.
using System;

class GFG
{

// Function to find the element for each
// query that occurs consecutively in the
// subarray [L, R] more than or equal to K times.
static int findElement(int[] arr, int[] left, int[] right,
                int n, int l, int r, int k)
{
    // find mid point of subarray [L, R]
    int mid = (l - 1 + r - 1) / 2;

    // find starting and ending index of range
    int s = Math.Max(mid - left[mid] + 1, l - 1);
    int e = Math.Min(right[mid] + mid - 1, r - 1);

    int range = e - s + 1;

    // compare this range with k
    // if it is greater than or
    // equal to k, return element
    if (range >= k)
        return arr[mid];

    // if not then return -1
    else
        return -1;
}

// function to answer query in range [L, R]
static int answerQuery(int []arr, int n,
                        int l, int r, int k)
{
    int[] left = new int[n];
    int[] right = new int[n];

    // store count of elements that occur
    // consecutively in the array [1, n]
    int count = 1;
    for (int i = 0; i < n - 1; i++)
    {
        if (arr[i] == arr[i + 1])
        {
            left[i] = count;
            count++;
        }
        else
        {
            left[i] = count;
            count = 1;
        }
    }
    left[n - 1] = count;

    // store count of elements that occur
    // consecutively in the array [n, 1]
    count = 1;
    for (int i = n - 1; i > 0; i--)
    {
        if (arr[i] == arr[i - 1])
        {
            right[i] = count;
            count++;
        }
        else
        {
            right[i] = count;
            count = 1;
        }
    }
    right[0] = count;

    // Function to return the element
    return findElement(arr, left, right, n, l, r, k);
}

// Driver Code
static public void Main ()
{

    int[] a = { 3, 2, 1, 1, 2, 2, 2, 2 };
    int n = a.Length;

    // 1st query
    int L = 2, R = 6, k = 3;
    Console.WriteLine(answerQuery(a, n, L, R, k));

    // 2nd query
    L = 3;
    R = 8;
    k = 4;
    Console.WriteLine(answerQuery(a, n, L, R, k));
}
}

// This code is contributed by ajit..
```

## java 描述语言

```
<script>

// Javascript program to find the element for each
// query that occurs consecutively in the
// subarray [L, R] more than or equal to K times.

/// Function to find the element for each
/// query that occurs consecutively in the
/// subarray [L, R] more than or equal to K times.
function findElement(arr, left, right,
                n, l, r, k)
{
    // find mid point of subarray [L, R]
    let mid = Math.floor((l - 1 + r - 1) / 2);

    // find starting and ending index of range
    let s = Math.max(mid - left[mid] + 1, l - 1);
    let e = Math.min(right[mid] + mid - 1, r - 1);

    let range = e - s + 1;

    // compare this range with k
    // if it is greater than or
    // equal to k, return element
    if (range >= k)
        return arr[mid];
    // if not then return -1
    else
        return -1;
}

// function to answer query in range [L, R]
function answerQuery(arr, n, l, r, k)
{
    let left = new Array(n).fill(0);
    let right = new Array(n).fill(0);

    // store count of elements that occur
    // consecutively in the array [1, n]
    let count = 1;
    for (let i = 0; i < n - 1; i++) {
        if (arr[i] == arr[i + 1]) {
            left[i] = count;
            count++;
        }
        else {
            left[i] = count;
            count = 1;
        }
    }
    left[n - 1] = count;

    // store count of elements that occur
    // consecutively in the array [n, 1]
    count = 1;
    for (let i = n - 1; i > 0; i--) {
        if (arr[i] == arr[i - 1]) {
            right[i] = count;
            count++;
        }
        else {
            right[i] = count;
            count = 1;
        }
    }
    right[0] = count;

    // Function to return the element
    return findElement(arr, left, right, n, l, r, k);
}

// driver program

    let a = [ 3, 2, 1, 1, 2, 2, 2, 2 ];
    let n = a.length;

    // 1st query
    let L = 2, R = 6, k = 3;
    document.write(answerQuery(a, n, L, R, k) + "<br/>" );

    // 2nd query
    L = 3;
    R = 8;
    k = 4;
    document.write(answerQuery(a, n, L, R, k));

</script>
```

**Output:** 

```
-1
2
```

**时间复杂度:** O(N)预先计算左右数组，O(1)回答每个查询。
**辅助空间:** O(N)