# 通过减少数组元素使其不包含三元组(I，j，k)来最大化数组的和，其中 a[i] < a[j]和 a[i] < a[k]和 j

 *> Original: [https://www.geeksforgeeks.org/Maximize the sum of arrays by reducing the array elements to not contain triples-I-j-k-where-AI-AJ-and-AI-AK-and-J-I-k/](https://www.geeksforgeeks.org/maximize-sum-of-array-by-reducing-array-elements-to-contain-no-triplets-i-j-k-where-ai-aj-and-ai-ak-and-j-i-k/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出数组元素减 1 任意次(可能为零)形成的数组的最大和，使得不存在三元组 **(i，j，k)** ( *基于 1 的索引*)使得**arr【j】>arr【I】**和**arr【k】>arr【I】执行减量操作后，也打印结果数组。**

**示例:**

> **输入:** arr[] = {1，2，1，2，1，3，1}
> **输出:**
> Sum = 9
> 最终数组= {1，1，1，1，3，1}
> 
> **输入:** arr[] = {2，4，1，2，3，1，2}
> **输出** :
> Sum = 11
> 最终数组:{2，4，1，1，1，1，1}

**天真法:**思路是要么递增要么递减要么先递增后递减更新数组，得到更新后所有数组元素的最大和。按照以下步骤解决问题:

1.  [在**【0，N–1】**范围内遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
2.  对于每个索引 **j** 更新 **arr[j]** 为 **min(arr[j]，b[j+1])** ，其中 **b[]** 存储符合要求条件的临时数组和 **0 < = j < i** 。
3.  对于每个索引 **j** 更新**arr【j】**为**min(arr【j】，b【j-1】)**，其中 **i + 1 < = j < N** 。
4.  从每个生成的 **b[]** 计算最大和。
5.  打印总和最大的数组 **b[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find and print maximum
// sum and corresponding array
void maximumSum(int m[], int n)
{
    int cnt = 0, ans = 0;

    // b stores temporary array when
    // element at index i is peak
    // c stores final array
    vector<int> b(n), c(n);

    // Check the array for each index
    for (int i = 0; i < n; i++) {

        // Choose m[i] as peak
        b[i] = m[i];
        cnt = b[i];

        // Check left
        for (int j = i - 1; j >= 0; j--) {
            b[j] = min(b[j + 1], m[j]);
            cnt += b[j];
        }

        // Check right
        for (int j = i + 1; j < n; j++) {
            b[j] = min(b[j - 1], m[j]);
            cnt += b[j];
        }

        // Check if sum is maximum
        if (ans < cnt) {
            ans = cnt;

            // Store the current array
            for (int j = 0; j < n; j++) {
                c[j] = b[j];
            }
        }
    }

    // Calculate sum
    int sum = 0;

    for (int i = 0; i < n; i++) {
        sum += c[i];
    }
    cout << "Sum = " << sum << endl;

    // Print array
    cout << "Final Array = ";
    for (int i = 0; i < n; i++) {
        cout << c[i] << " ";
    }
}

// Drive Code
int main()
{
    // Given array
    int arr[] = { 1, 2, 1, 2, 1, 3, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maximumSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to find and print maximum
// sum and corresponding array
static void maximumSum(int m[], int n)
{
  int cnt = 0, ans = 0;

  // b stores temporary array when
  // element at index i is peak
  // c stores final array
  int []b = new int[n];
  int []c = new int[n];

  // Check the array for each index
  for (int i = 0; i < n; i++)
  {
    // Choose m[i] as peak
    b[i] = m[i];
    cnt = b[i];

    // Check left
    for (int j = i - 1; j >= 0; j--)
    {
      b[j] = Math.min(b[j + 1], m[j]);
      cnt += b[j];
    }

    // Check right
    for (int j = i + 1; j < n; j++)
    {
      b[j] = Math.min(b[j - 1], m[j]);
      cnt += b[j];
    }

    // Check if sum is maximum
    if (ans < cnt)
    {
      ans = cnt;

      // Store the current array
      for (int j = 0; j < n; j++)
      {
        c[j] = b[j];
      }
    }
  }

  // Calculate sum
  int sum = 0;

  for (int i = 0; i < n; i++)
  {
    sum += c[i];
  }
  System.out.print("Sum = " + 
                    sum + "\n");

  // Print array
  System.out.print("Final Array = ");
  for (int i = 0; i < n; i++)
  {
    System.out.print(c[i] + " ");
  }
}

// Drive Code
public static void main(String[] args)
{
  // Given array
  int arr[] = {1, 2, 1, 2, 1, 3, 1};

  int N = arr.length;

  // Function Call
  maximumSum(arr, N);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find and print maximum
# sum and corresponding array
def maximumSum(m, n):

    cnt = 0
    ans = 0

    # b stores temporary array when
    # element at index i is peak
    # c stores final array
    b = [0 for i in range(n)]
    c = [0 for i in range(n)]

    # Check the array for each index
    for i in range(n):

        # Choose m[i] as peak
        b[i] = m[i]
        cnt = b[i]

        # Check left
        for j in range(i - 1, -1, -1):
            b[j] = min(b[j + 1], m[j])
            cnt += b[j]

        # Check right
        for j in range(i + 1, n):
            b[j] = min(b[j - 1], m[j])
            cnt += b[j]

        # Check if sum is maximum
        if (ans < cnt):
            ans = cnt

            # Store the current array
            for j in range(n):
                c[j] = b[j]

    # Calculate sum and printing
    print("Sum = ", sum(c))
    print("Final Array = ", *c)

# Driver Code
arr = [ 1, 2, 1, 2, 1, 3, 1 ]

N = len(arr) // arr[0]

# Function call
maximumSum(arr, N)

# This code is contributed by dadi madhav
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find and print maximum
// sum and corresponding array
static void maximumSum(int []m, int n)
{
    int cnt = 0, ans = 0;

    // b stores temporary array when
    // element at index i is peak
    // c stores readonly array
    int []b = new int[n];
    int []c = new int[n];

    // Check the array for each index
    for(int i = 0; i < n; i++)
    {

        // Choose m[i] as peak
        b[i] = m[i];
        cnt = b[i];

        // Check left
        for(int j = i - 1; j >= 0; j--)
        {
            b[j] = Math.Min(b[j + 1], m[j]);
            cnt += b[j];
        }

        // Check right
        for(int j = i + 1; j < n; j++)
        {
            b[j] = Math.Min(b[j - 1], m[j]);
            cnt += b[j];
        }

        // Check if sum is maximum
        if (ans < cnt)
        {
            ans = cnt;

            // Store the current array
            for(int j = 0; j < n; j++)
            {
                c[j] = b[j];
            }
        }
    }

    // Calculate sum
    int sum = 0;

    for(int i = 0; i < n; i++)
    {
        sum += c[i];
    }
    Console.Write("Sum = " + 
                   sum + "\n");

    // Print array
    Console.Write("Final Array = ");
    for(int i = 0; i < n; i++)
    {
        Console.Write(c[i] + " ");
    }
}

// Drive Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 1, 2, 1, 2, 1, 3, 1 };

    int N = arr.Length;

    // Function call
    maximumSum(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

// Function to find and print maximum
// sum and corresponding array
function  maximumSum(m,n)
{
    let cnt = 0, ans = 0;

  // b stores temporary array when
  // element at index i is peak
  // c stores final array
  let b = new Array(n);
  let c = new Array(n);

  // Check the array for each index
  for (let i = 0; i < n; i++)
  {
    // Choose m[i] as peak
    b[i] = m[i];
    cnt = b[i];

    // Check left
    for (let j = i - 1; j >= 0; j--)
    {
      b[j] = Math.min(b[j + 1], m[j]);
      cnt += b[j];
    }

    // Check right
    for (let j = i + 1; j < n; j++)
    {
      b[j] = Math.min(b[j - 1], m[j]);
      cnt += b[j];
    }

    // Check if sum is maximum
    if (ans < cnt)
    {
      ans = cnt;

      // Store the current array
      for (let j = 0; j < n; j++)
      {
        c[j] = b[j];
      }
    }
  }

  // Calculate sum
  let sum = 0;

  for (let i = 0; i < n; i++)
  {
    sum += c[i];
  }
  document.write("Sum = " +
                    sum + "<br>");

  // Print array
  document.write("Final Array = ");
  for (let i = 0; i < n; i++)
  {
    document.write(c[i] + " ");
  }
}

// Drive Code
// Given array
let arr=[1, 2, 1, 2, 1, 3, 1];
let N = arr.length;

// Function Call
maximumSum(arr, N);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
Sum = 9
Final Array = 1 1 1 1 1 3 1
```

***时间复杂度:** O(N <sup>2</sup> ，其中 N 为*给定数组的*大小。*
***辅助空间:** O(N)*

**高效方法:**思路是使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)高效解决这个问题。按照以下步骤解决上述问题:

*   创建一个[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)，返回范围**【l，r】**中最小元素的索引。
*   在**【l，r】**中搜索最小元素。假设是在**mini dex**。
*   然后进行 2 次递归调用:
    *   假设所有的**都在【l】。minidex]**已更改为**arr【minidex】**。因此，所有值的总和由下式给出:

> arr[miniindex]*(miniindex–l+1)

*   然后在**【minidex+1，r】**上进行递归调用，将所有**arr【minidex+1，r】改为 arr【minidex】**。因此，所有值的总和由下式给出:

> arr[miniindex]*(r–miniindex+1)

*   在基本情况下，如果 **l==r** ，则当 **l 或 r** 为峰值时，即为数组的最终和。
*   然后简单地找到最佳峰值，即具有最大值的峰值。
*   找到最佳峰值后，打印阵列及其总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
int peak, maxi = -1;

// For storing segment tree
int seg[4 * 500001];

// Initialize segment tree
void built(int l, int r, int index,
        int a[])
{
    // Base Case
    if (l == r) {
        seg[index] = l;
        return;
    }

    // Get mid
    int m = l + (r - l) / 2;

    // Recurr from l to m
    built(l, m, 2 * index, a);

    // Recurr from m+1 to r
    built(m + 1, r, 2 * index + 1, a);

    if (a[seg[2 * index]]
        < a[seg[2 * index + 1]])
        seg[index] = seg[2 * index];
    else
        seg[index] = seg[2 * index + 1];
}

// Query to find minimum value index
// between l and r
int query(int l, int r, int s, int e,
        int index, int a[])
{
    // If segment is invalid
    if (s > r || e < l)
        return -1;

    // If segment is inside the
    // desired segment
    if (s >= l && e <= r)
        return seg[index];

    // Find the mid
    int m = s + (e - s) / 2;

    // Recurr for the left
    int d1 = query(l, r, s, m,
                2 * index, a);

    // Recurr for the right
    int d2 = query(l, r, m + 1, e,
                2 * index + 1, a);

    // Update the query
    if (d1 == -1)
        return d2;
    if (d2 == -1)
        return d1;
    if (a[d1] < a[d2])
        return d1;
    else
        return d2;
}

// Function for finding the optimal peak
void optimalPeak(int l, int r, int value,
                int n, int a[])
{
    if (l > r)
        return;

    // Check if its the peak
    if (l == r) {

        // Update the value for the
        // maximum sum
        if (value + a[l] > maxi) {
            maxi = a[l] + value;
            peak = l;
            return;
        }
        return;
    }

    // Index of minimum element in
    // l and r
    int indexmini = query(l, r, 0,
                        n - 1, 1, a);

    int value1 = a[indexmini]
                * (indexmini - l + 1);

    // Recurr right of minimum index
    optimalPeak(indexmini + 1, r,
                value + value1, n, a);

    // Update the max and peak value
    if (indexmini + 1 > r) {
        if (value + value1 > maxi) {
            maxi = value + value1;
            peak = indexmini;
        }
    }

    int value2 = a[indexmini]
                * (r - indexmini + 1);

    // Recurr left of minimum index
    optimalPeak(l, indexmini - 1,
                value + value2, n, a);

    // Update the max and peak value
    if (l > indexmini - 1) {
        if (value + value2 > maxi) {
            maxi = value + value2;
            peak = l;
        }
    }
}

// Print maximum sum and the array
void maximumSum(int a[], int n)
{
    // Initialize segment tree
    built(0, n - 1, 1, a);

    // Get the peak
    optimalPeak(0, n - 1, 0, n, a);

    // Store the required array
    int ans[n];
    ans[peak] = a[peak];

    // Update the ans[]
    for (int i = peak + 1; i < n; i++) {
        ans[i] = min(ans[i - 1], a[i]);
    }

    for (int i = peak - 1; i >= 0; i--) {
        ans[i] = min(a[i], ans[i + 1]);
    }

    // Find the maximum sum
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += ans[i];
    }

    // Print sum and optimal array
    cout << "Sum = "
        << sum << endl;

    cout << "Final Array = ";
    for (int i = 0; i < n; i++) {
        cout << ans[i] << " ";
    }
}

// Drive Code
int main()
{
    // Given array
    int arr[] = { 1, 2, 1, 2, 1, 3, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maximumSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG{
static int peak, maxi = -1;

// For storing segment tree
static int []seg = new int[4 * 500001];

// Initialize segment tree
static void built(int l, int r, int index,
        int a[])
{
    // Base Case
    if (l == r) {
        seg[index] = l;
        return;
    }

    // Get mid
    int m = l + (r - l) / 2;

    // Recurr from l to m
    built(l, m, 2 * index, a);

    // Recurr from m+1 to r
    built(m + 1, r, 2 * index + 1, a);

    if (a[seg[2 * index]]
        < a[seg[2 * index + 1]])
        seg[index] = seg[2 * index];
    else
        seg[index] = seg[2 * index + 1];
}

// Query to find minimum value index
// between l and r
static int query(int l, int r, int s, int e,
        int index, int a[])
{
    // If segment is invalid
    if (s > r || e < l)
        return -1;

    // If segment is inside the
    // desired segment
    if (s >= l && e <= r)
        return seg[index];

    // Find the mid
    int m = s + (e - s) / 2;

    // Recurr for the left
    int d1 = query(l, r, s, m,
                2 * index, a);

    // Recurr for the right
    int d2 = query(l, r, m + 1, e,
                2 * index + 1, a);

    // Update the query
    if (d1 == -1)
        return d2;
    if (d2 == -1)
        return d1;
    if (a[d1] < a[d2])
        return d1;
    else
        return d2;
}

// Function for finding the optimal peak
static void optimalPeak(int l, int r, int value,
                int n, int a[])
{
    if (l > r)
        return;

    // Check if its the peak
    if (l == r) {

        // Update the value for the
        // maximum sum
        if (value + a[l] > maxi) {
            maxi = a[l] + value;
            peak = l;
            return;
        }
        return;
    }

    // Index of minimum element in
    // l and r
    int indexmini = query(l, r, 0,
                        n - 1, 1, a);

    int value1 = a[indexmini]
                * (indexmini - l + 1);

    // Recurr right of minimum index
    optimalPeak(indexmini + 1, r,
                value + value1, n, a);

    // Update the max and peak value
    if (indexmini + 1 > r) {
        if (value + value1 > maxi) {
            maxi = value + value1;
            peak = indexmini;
        }
    }

    int value2 = a[indexmini]
                * (r - indexmini + 1);

    // Recurr left of minimum index
    optimalPeak(l, indexmini - 1,
                value + value2, n, a);

    // Update the max and peak value
    if (l > indexmini - 1) {
        if (value + value2 > maxi) {
            maxi = value + value2;
            peak = l;
        }
    }
}

// Print maximum sum and the array
static void maximumSum(int a[], int n)
{
    // Initialize segment tree
    built(0, n - 1, 1, a);

    // Get the peak
    optimalPeak(0, n - 1, 0, n, a);

    // Store the required array
    int []ans = new int[n];
    ans[peak] = a[peak];

    // Update the ans[]
    for (int i = peak + 1; i < n; i++) {
        ans[i] = Math.min(ans[i - 1], a[i]);
    }

    for (int i = peak - 1; i >= 0; i--) {
        ans[i] = Math.min(a[i], ans[i + 1]);
    }

    // Find the maximum sum
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += ans[i];
    }

    // Print sum and optimal array
    System.out.print("Sum = "
        + sum +"\n");

    System.out.print("Final Array = ");
    for (int i = 0; i < n; i++) {
        System.out.print(ans[i]+ " ");
    }
}

// Drive Code
public static void main(String[] args)
{
    // Given array
    int arr[] = { 1, 2, 1, 2, 1, 3, 1 };

    int N = arr.length;

    // Function Call
    maximumSum(arr, N);

}
}

// This code contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach
peak = 0
maxi = -1

# For storing segment tree
seg = [0 for i in range(4 * 500001)]

# Initialize segment tree
def built(l, r, index, a):

    # Base Case
    if (l == r):
        seg[index] = l
        return

    # Get mid
    m = int(l + (r - l) / 2)

    # Recurr from l to m
    built(l, m, 2 * index, a)

    # Recurr from m+1 to r
    built(m + 1, r, 2 * index + 1, a)

    if (a[seg[2 * index]] <
        a[seg[2 * index + 1]]):
        seg[index] = seg[2 * index]
    else:
        seg[index] = seg[2 * index + 1]

# Query to find minimum value index
# between l and r
def query(l, r, s, e, index, a):

    # If segment is invalid
    if (s > r or e < l):
        return -1

    # If segment is inside the
    # desired segment
    if (s >= l and e <= r):
        return seg[index]

    # Find the mid
    m = int(s + (e - s) / 2)

    # Recurr for the left
    d1 = query(l, r, s, m,
               2 * index, a)

    # Recurr for the right
    d2 = query(l, r, m + 1, e,
             2 * index + 1, a)

    # Update the query
    if (d1 == -1):
        return d2
    if (d2 == -1):
        return d1
    if (a[d1] < a[d2]):
        return d1
    else:
        return d2

# Function for finding the optimal peak
def optimalPeak(l, r, value, n, a):

    global maxi, peak

    if (l > r):
        return

    # Check if its the peak
    if (l == r):

        # Update the value for the
        # maximum sum
        if (value + a[l] > maxi):
            maxi = a[l] + value
            peak = l
            return

        return

    # Index of minimum element in
    # l and r
    indexmini = query(l, r, 0, n - 1, 1, a)
    value1 = a[indexmini] * (indexmini - l + 1)

    # Recurr right of minimum index
    optimalPeak(indexmini + 1, r,
                    value + value1, n, a)

    # Update the max and peak value
    if (indexmini + 1 > r):
        if (value + value1 > maxi):
            maxi = value + value1
            peak = indexmini

    value2 = (a[indexmini] *
            (r - indexmini + 1))

    # Recurr left of minimum index
    optimalPeak(l, indexmini - 1,
                value + value2, n, a)

    # Update the max and peak value
    if (l > indexmini - 1):
        if (value + value2 > maxi):
            maxi = value + value2
            peak = l

# Print maximum sum and the array
def maximumSum(a, n):

    # Initialize segment tree
    built(0, n - 1, 1, a)

    # Get the peak
    optimalPeak(0, n - 1, 0, n, a)

    # Store the required array
    ans = [0 for i in range(n)]

    ans[peak] = a[peak]

    # Update the ans[]
    for i in range(peak + 1, n):
        ans[i] = min(ans[i - 1], a[i])
    for i in range(peak - 1, -1, -1):
        ans[i] = min(a[i], ans[i + 1])

    # Find the maximum sum
    Sum = 0
    Sum = sum(ans)

    # Print sum and optimal array
    print("Sum = ", Sum)

    print("Final Array = ", end = "")
    print(*ans, sep = " ")

# Driver Code

# Given array
arr = [ 1, 2, 1, 2, 1, 3, 1 ]
N = len(arr)

# Function Call
maximumSum(arr, N)

# This code is contributed by rag2127
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

static int peak, maxi = -1;

// For storing segment tree
static int []seg = new int[4 * 500001];

// Initialize segment tree
static void built(int l, int r,
                int index, int []a)
{
// Base Case
if (l == r)
{
    seg[index] = l;
    return;
}

// Get mid
int m = l + (r - l) / 2;

// Recurr from l to m
built(l, m, 2 * index, a);

// Recurr from m+1 to r
built(m + 1, r, 2 * index + 1, a);

if (a[seg[2 * index]] <
    a[seg[2 * index + 1]])
    seg[index] = seg[2 * index];
else
    seg[index] = seg[2 * index + 1];
}

// Query to find minimum value index
// between l and r
static int query(int l, int r,
                int s, int e,
                int index, int []a)
{
// If segment is invalid
if (s > r || e < l)
    return -1;

// If segment is inside the
// desired segment
if (s >= l && e <= r)
    return seg[index];

// Find the mid
int m = s + (e - s) / 2;

// Recurr for the left
int d1 = query(l, r, s, m,
                2 * index, a);

// Recurr for the right
int d2 = query(l, r, m + 1, e,
                2 * index + 1, a);

// Update the query
if (d1 == -1)
    return d2;
if (d2 == -1)
    return d1;
if (a[d1] < a[d2])
    return d1;
else
    return d2;
}

// Function for finding the optimal peak
static void optimalPeak(int l, int r,
                        int value, int n, int []a)
{
if (l > r)
    return;

// Check if its the peak
if (l == r)
{
    // Update the value for the
    // maximum sum
    if (value + a[l] > maxi)
    {
    maxi = a[l] + value;
    peak = l;
    return;
    }
    return;
}

// Index of minimum element in
// l and r
int indexmini = query(l, r, 0,
                        n - 1, 1, a);

int value1 = a[indexmini] *
                (indexmini - l + 1);

// Recurr right of minimum index
optimalPeak(indexmini + 1, r,
            value + value1, n, a);

// Update the max and peak value
if (indexmini + 1 > r)
{
    if (value + value1 > maxi)
    {
    maxi = value + value1;
    peak = indexmini;
    }
}

int value2 = a[indexmini] *
                (r - indexmini + 1);

// Recurr left of minimum index
optimalPeak(l, indexmini - 1,
            value + value2, n, a);

// Update the max and peak value
if (l > indexmini - 1)
{
    if (value + value2 > maxi)
    {
    maxi = value + value2;
    peak = l;
    }
}
}

// Print maximum sum and the array
static void maximumSum(int []a, int n)
{
// Initialize segment tree
built(0, n - 1, 1, a);

// Get the peak
optimalPeak(0, n - 1, 0, n, a);

// Store the required array
int []ans = new int[n];
ans[peak] = a[peak];

// Update the ans[]
for (int i = peak + 1; i < n; i++)
{
    ans[i] = Math.Min(ans[i - 1], a[i]);
}

for (int i = peak - 1; i >= 0; i--)
{
    ans[i] = Math.Min(a[i], ans[i + 1]);
}

// Find the maximum sum
int sum = 0;
for (int i = 0; i < n; i++)
{
    sum += ans[i];
}

// Print sum and optimal array
Console.Write("Sum = " +
                sum + "\n");

Console.Write("Final Array = ");
for (int i = 0; i < n; i++)
{
    Console.Write(ans[i] + " ");
}
}

// Drive Code
public static void Main(String[] args)
{
// Given array
int []arr = {1, 2, 1, 2, 1, 3, 1};

int N = arr.Length;

// Function Call
maximumSum(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program for the above approach

let peak, maxi = -1;

let seg = new Array(4 * 500001);

// Initialize segment tree
function built(l,r,index,a)
{
    // Base Case
    if (l == r) {
        seg[index] = l;
        return;
    }

    // Get mid
    let m = l + Math.floor((r - l) / 2);

    // Recurr from l to m
    built(l, m, 2 * index, a);

    // Recurr from m+1 to r
    built(m + 1, r, 2 * index + 1, a);

    if (a[seg[2 * index]]
        < a[seg[2 * index + 1]])
        seg[index] = seg[2 * index];
    else
        seg[index] = seg[2 * index + 1];
}

// Query to find minimum value index
// between l and r
function query(l,r,s,e,index,a)
{
    // If segment is invalid
    if (s > r || e < l)
        return -1;

    // If segment is inside the
    // desired segment
    if (s >= l && e <= r)
        return seg[index];

    // Find the mid
    let m = s + Math.floor((e - s) / 2);

    // Recurr for the left
    let d1 = query(l, r, s, m,
                2 * index, a);

    // Recurr for the right
    let d2 = query(l, r, m + 1, e,
                2 * index + 1, a);

    // Update the query
    if (d1 == -1)
        return d2;
    if (d2 == -1)
        return d1;
    if (a[d1] < a[d2])
        return d1;
    else
        return d2;
}

// Function for finding the optimal peak
function optimalPeak(l,r,value,n,a)
{
    if (l > r)
        return;

    // Check if its the peak
    if (l == r) {

        // Update the value for the
        // maximum sum
        if (value + a[l] > maxi) {
            maxi = a[l] + value;
            peak = l;
            return;
        }
        return;
    }

    // Index of minimum element in
    // l and r
    let indexmini = query(l, r, 0,
                        n - 1, 1, a);

    let value1 = a[indexmini]
                * (indexmini - l + 1);

    // Recurr right of minimum index
    optimalPeak(indexmini + 1, r,
                value + value1, n, a);

    // Update the max and peak value
    if (indexmini + 1 > r) {
        if (value + value1 > maxi) {
            maxi = value + value1;
            peak = indexmini;
        }
    }

    let value2 = a[indexmini]
                * (r - indexmini + 1);

    // Recurr left of minimum index
    optimalPeak(l, indexmini - 1,
                value + value2, n, a);

    // Update the max and peak value
    if (l > indexmini - 1) {
        if (value + value2 > maxi) {
            maxi = value + value2;
            peak = l;
        }
    }
}

// Print maximum sum and the array
function maximumSum(a,n)
{
    // Initialize segment tree
    built(0, n - 1, 1, a);

    // Get the peak
    optimalPeak(0, n - 1, 0, n, a);

    // Store the required array
    let ans = new Array(n);
    ans[peak] = a[peak];

    // Update the ans[]
    for (let i = peak + 1; i < n; i++) {
        ans[i] = Math.min(ans[i - 1], a[i]);
    }

    for (let i = peak - 1; i >= 0; i--) {
        ans[i] = Math.min(a[i], ans[i + 1]);
    }

    // Find the maximum sum
    let sum = 0;
    for (let i = 0; i < n; i++) {
        sum += ans[i];
    }

    // Print sum and optimal array
    document.write("Sum = "
        + sum +"<br>");

    document.write("Final Array = ");
    for (let i = 0; i < n; i++) {
        document.write(ans[i]+ " ");
    }
}

// Drive Code
let arr=[1, 2, 1, 2, 1, 3, 1];
let N = arr.length;
// Function Call
maximumSum(arr, N);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
Sum = 9
Final Array = 1 1 1 1 1 3 1
```

***时间复杂度:** O(N*logN)，其中 N 是给定数组的大小。*
***辅助空间:** O(N)**