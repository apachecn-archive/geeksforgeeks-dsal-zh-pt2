# 通过与另一个数组交换最多 K 个元素来最大化数组和

> 原文:[https://www . geeksforgeeks . org/通过用另一个数组交换最多 k 个元素来最大化数组总和/](https://www.geeksforgeeks.org/maximize-array-sum-by-swapping-at-most-k-elements-with-another-array/)

给定两个大小为 **N** 的数组 **A** 和 **B** 以及一个整数 **K** ，任务是通过与数组 B 交换最多 K 个元素来找到数组 A 的**最大**可能和。
**示例:**

> **输入:** A[] = {2，3，4}，B[] = {6，8，5}，K = 1
> **输出:** 15
> **解释:**
> 交换 A[0]和 B[1]。因此总和= 8 + 3 + 4 = 15。
> **输入:** A[] = {9，7}，B[] = {5，1}，K = 2
> **输出:** 16
> **说明:**
> 由于数组 A 的所有元素都大于数组 B 的元素，所以不需要进行互换。

**进场:**

1.  [按非递减顺序对数组](https://www.geeksforgeeks.org/sorting-algorithms/) A 和 B 进行排序。

2.  [从头开始迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) A，从尾开始迭代数组 B，这样我们就可以用数组 B 的最大元素交换数组 A 的最小元素了.

3.  如果数组 A 的元素小于数组 B 的元素，则交换它们。否则，打破循环。

4.  最多对 K 个元素执行此操作。

5.  求结果数组 a 的和

下面是上述方法的实现。

## C++

```
// C++ implementation to find maximum
// sum of array A by swapping
// at most K elements with array B

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
void maximumSum(int a[], int b[],
                int k, int n)
{
    int i, j;
    sort(a, a + n);
    sort(b, b + n);

    // If element of array a is
    // smaller than that of
    // array b, swap them.
    for (i = 0, j = n - 1; i < k;
         i++, j--) {
        if (a[i] < b[j])
            swap(a[i], b[j]);
        else
            break;
    }

    // Find sum of resultant array
    int sum = 0;
    for (i = 0; i < n; i++)
        sum += a[i];
    cout << sum << endl;
}

int main()
{
    int K = 1;
    int A[] = { 2, 3, 4 };
    int B[] = { 6, 8, 5 };

    int N = sizeof(A) / sizeof(A[0]);

    maximumSum(A, B, K, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find maximum
// sum of array A by swapping
// at most K elements with array B
import java.util.*;
class GFG{

// Function to find the maximum sum
static void maximumSum(int a[], int b[],
                       int k, int n)
{
    int i, j;
    Arrays.sort(a);
    Arrays.sort(b);

    // If element of array a is
    // smaller than that of
    // array b, swap them.
    for (i = 0, j = n - 1; i < k; i++, j--)
    {
        if (a[i] < b[j])
        {
            int temp = a[i];
            a[i] = b[j];
            b[j] = temp;
        }
        else
            break;
    }

    // Find sum of resultant array
    int sum = 0;
    for (i = 0; i < n; i++)
        sum += a[i];
    System.out.print(sum +"\n");
}

// Driver Code
public static void main(String[] args)
{
    int K = 1;
    int A[] = { 2, 3, 4 };
    int B[] = { 6, 8, 5 };

    int N = A.length;

    maximumSum(A, B, K, N);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to find maximum
# sum of array A by swapping
# at most K elements with array B

# Function to find the maximum sum
def maximumSum(a, b, k, n):

    a.sort()
    b.sort()

    # If element of array a is
    # smaller than that of
    # array b, swap them.
    i = 0
    j = n - 1

    while i < k:
        if (a[i] < b[j]):
            a[i], b[j] = b[j], a[i]

        else:
            break

        i += 1
        j -= 1

    # Find sum of resultant array
    sum = 0
    for i in range (n):
        sum += a[i]

    print(sum)

# Driver code
if __name__ == "__main__":

    K = 1
    A = [ 2, 3, 4 ]
    B = [ 6, 8, 5 ]

    N = len(A)

    maximumSum(A, B, K, N)

# This code is contributed by chitranayal
```

## C#

```
// C# implementation to find maximum
// sum of array A by swapping
// at most K elements with array B
using System;
class GFG{

// Function to find the maximum sum
static void maximumSum(int []a,
                       int []b,
                       int k, int n)
{
    int i, j;
    Array.Sort(a);
    Array.Sort(b);

    // If element of array a is
    // smaller than that of
    // array b, swap them.
    for (i = 0, j = n - 1; i < k; i++, j--)
    {
        if (a[i] < b[j])
        {
            int temp = a[i];
            a[i] = b[j];
            b[j] = temp;
        }
        else
            break;
    }

    // Find sum of resultant array
    int sum = 0;
    for (i = 0; i < n; i++)
        sum += a[i];
    Console.Write(sum +"\n");
}

// Driver Code
public static void Main()
{
    int K = 1;
    int []A = { 2, 3, 4 };
    int []B = { 6, 8, 5 };

    int N = A.Length;

    maximumSum(A, B, K, N);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// JavaScript implementation to find maximum
// sum of array A by swapping
// at most K elements with array B

// Function to find the maximum sum
function maximumSum(a, b, k, n)
{
    let i, j;
    a.sort();
    b.sort();

    // If element of array a is
    // smaller than that of
    // array b, swap them.
    for (i = 0, j = n - 1; i < k;
        i++, j--) {
        if (a[i] < b[j])
     {
       let temp = a[i];
       a[i] = b[j];
       b[j] = temp;
     }
        else
            break;
    }

    // Find sum of resultant array
    let sum = 0;
    for (i = 0; i < n; i++)
        sum += a[i];
    document.write(sum);
}

    let K = 1;
    let A = [2, 3, 4 ];
    let B = [ 6, 8, 5 ];

    let N = A.length;

    maximumSum(A, B, K, N);

// This code is contributed by vaibhavrabadiya117.
</script>
```

**Output:** 

```
15
```

**业绩分析:**

*   **时间复杂度:** O(N * log N)
*   **辅助空间:** O(1)