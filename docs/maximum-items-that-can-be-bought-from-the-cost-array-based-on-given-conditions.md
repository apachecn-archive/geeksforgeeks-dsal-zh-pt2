# 根据给定条件可以从成本数组中购买的最大项目

> 原文:[https://www . geeksforgeeks . org/基于给定条件从成本阵列中可以购买的最大项目数/](https://www.geeksforgeeks.org/maximum-items-that-can-be-bought-from-the-cost-array-based-on-given-conditions/)

给定一个大小为 **N** 的数组**arr【】**，数组中的每个指数代表购买一件物品的成本，以及两个数字 **P，K** 。任务是找到可以购买的物品的最大数量，以便:

1.  如果从数组中购买了第 I 个对象，剩余的数量将变为**P–arr[I]**。
2.  我们可以通过只为其中成本最高的项目付费，一次购买 **K** 个项目，不一定是连续的。现在，剩余金额将是**P–max(K 物品成本)**。

**示例:**

> **输入:** arr[] = {2，4，3，5，7}，P = 6，K = 2
> **输出:** 3
> **说明:**
> 我们可以买第一个成本为 2 的物品。所以，剩余的数量是 P = 6–2 = 4。
> 现在，我们可以选择第二项和第三项，支付最大的一项，即 max(4，3) = 4，剩余金额为 4–4 = 0。
> 因此，购买的物品总数为 3 件。
> 
> **输入:** arr[] = {2，4，3，5，7}，P = 11，K = 2
> **输出:** 4
> **说明:**
> 我们可以一起购买第一个和第三个物品，只支付最大的一个，即 max(2，3) = 3。剩余金额为 P = 11–3 = 8。
> 现在，我们可以购买第二个和第四个项目，并支付最大的一个(4，5) = 5。剩余金额为 P = 8–5 = 3。现在，我们不能再买任何东西了。

**做法:**思路是用[的概念排序](https://www.geeksforgeeks.org/sorting-algorithms/)和[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。

*   给定数组 arr[]排序。
*   找到数组 arr[]的前缀和。
*   排序背后的想法是，只有当我们以更低的成本购买项目时，才能购买最大数量的项目。这种算法被称为[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)。
*   并且，我们使用前缀和数组来计算购买物品的成本。

下面是上述方法的实现:

## C++

```
// C++ program to find the
// maximum number of items
// that can be bought from
// the given cost array

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// maximum number of items
// that can be bought from
// the given cost array
int number(int a[], int n, int p, int k)
{
    // Sort the given array
    sort(a, a + n);

    // Variables to store the prefix
    // sum, answer and the counter
    // variables
    int pre[n] = { 0 }, val, i,
        j, ans = 0;

    // Initializing the first element
    // of the prefix array
    pre[0] = a[0];

    // If we can buy at least one item
    if (pre[0] <= p)
        ans = 1;

    // Iterating through the first
    // K items and finding the
    // prefix sum
    for (i = 1; i < k - 1; i++) {
        pre[i] = pre[i - 1] + a[i];

        // Check the number of items
        // that can be bought
        if (pre[i] <= p)
            ans = i + 1;
    }

    pre[k - 1] = a[k - 1];

    // Finding the prefix sum for
    // the remaining elements
    for (i = k - 1; i < n; i++) {
        if (i >= k) {
            pre[i] += pre[i - k] + a[i];
        }

        // Check the number of iteams
        // that can be bought
        if (pre[i] <= p)
            ans = i + 1;
    }

    return ans;
}

// Driver code
int main()
{
    int n = 5;
    int arr[] = { 2, 4, 3, 5, 7 };
    int p = 11;
    int k = 2;

    cout << number(arr, n, p, k) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// number of items that can be bought
// from the given cost array
import java.io.*;
import java.util.*;

class GFG{

// Function to find the
// maximum number of items
// that can be bought from
// the given cost array
static int number(int[] a, int n,
                  int p, int k)
{

    // Sort the given array
    Arrays.sort(a);

    // Variables to store the prefix
    // sum, answer and the counter
    // variables
    int[] pre = new int[n];
    int val, i, j, ans = 0;

    // Initializing the first element
    // of the prefix array
    pre[0] = a[0];

    // If we can buy at least one item
    if (pre[0] <= p)
        ans = 1;

    // Iterating through the first
    // K items and finding the
    // prefix sum
    for(i = 1; i < k - 1; i++)
    {
        pre[i] = pre[i - 1] + a[i];

        // Check the number of items
        // that can be bought
        if (pre[i] <= p)
            ans = i + 1;
    }
    pre[k - 1] = a[k - 1];

    // Finding the prefix sum for
    // the remaining elements
    for(i = k - 1; i < n; i++)
    {
        if (i >= k)
        {
            pre[i] += pre[i - k] + a[i];
        }

        // Check the number of iteams
        // that can be bought
        if (pre[i] <= p)
            ans = i + 1;
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    int[] arr = { 2, 4, 3, 5, 7 };
    int p = 11;
    int k = 2;

    System.out.println(number(arr, n, p, k));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# number of items that can be bought
# from the given cost array

# Function to find the maximum
# number of items that can be
# bought from the given cost array
def number(a, n, p, k):

    # Sort the given array
    a.sort()

    # Variables to store the prefix
    # sum, answer and the counter
    # variables
    pre = [ ]
    for i in range(n):
        pre.append(0)

    ans = 0
    val = 0
    i = 0
    j = 0

    # Initializing the first element
    # of the prefix array
    pre[0] = a[0]

    # If we can buy at least one item
    if pre[0] <= p:
        ans = 1

    # Iterating through the first
    # K items and finding the
    # prefix sum
    for i in range(1, k - 1):
        pre[i] = pre[i - 1] + a[i]

        # Check the number of items
        # that can be bought
        if pre[i] <= p:
            ans = i + 1

    pre[k - 1] = a[k - 1]

    # Finding the prefix sum for
    # the remaining elements
    for i in range(k - 1, n):
        if i >= k:
            pre[i] += pre[i - k] + a[i]

        # Check the number of iteams
        # that can be bought
        if pre[i] <= p:
            ans = i+ 1

    return ans

# Driver code
n = 5
arr = [ 2, 4, 3, 5, 7 ]
p = 11
k = 2

print(number(arr, n, p, k))

# This code is contributed by ishayadav181
```

## C#

```
// C# program to find the maximum
// number of items that can be
// bought from the given cost array
using System;
using System.Collections;

class GFG{

// Function to find the
// maximum number of items
// that can be bought from
// the given cost array
static int number(int[] a, int n,
                  int p, int k)
{

    // Sort the given array
    Array.Sort(a);

    // Variables to store the prefix
    // sum, answer and the counter
    // variables
    int[] pre = new int[n];
    int i, ans = 0;

    // Initializing the first element
    // of the prefix array
    pre[0] = a[0];

    // If we can buy at least one item
    if (pre[0] <= p)
        ans = 1;

    // Iterating through the first
    // K items and finding the
    // prefix sum
    for(i = 1; i < k - 1; i++)
    {
        pre[i] = pre[i - 1] + a[i];

        // Check the number of items
        // that can be bought
        if (pre[i] <= p)
            ans = i + 1;
    }

    pre[k - 1] = a[k - 1];

    // Finding the prefix sum for
    // the remaining elements
    for(i = k - 1; i < n; i++)
    {
        if (i >= k)
        {
            pre[i] += pre[i - k] + a[i];
        }

        // Check the number of iteams
        // that can be bought
        if (pre[i] <= p)
            ans = i + 1;
    }
    return ans;
}

// Driver code
static public void Main ()
{
    int n = 5;
    int[] arr = { 2, 4, 3, 5, 7 };
    int p = 11;
    int k = 2;

    Console.WriteLine(number(arr, n, p, k));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program to find the
// maximum number of items
// that can be bought from
// the given cost array

// Function to find the
// maximum number of items
// that can be bought from
// the given cost array
function number(a, n, p, k)
{
    // Sort the given array
    a.sort();

    // Variables to store the prefix
    // sum, answer and the counter
    // variables
    var pre = Array(n).fill(0), val, i,
        j, ans = 0;

    // Initializing the first element
    // of the prefix array
    pre[0] = a[0];

    // If we can buy at least one item
    if (pre[0] <= p)
        ans = 1;

    // Iterating through the first
    // K items and finding the
    // prefix sum
    for (i = 1; i < k - 1; i++) {
        pre[i] = pre[i - 1] + a[i];

        // Check the number of items
        // that can be bought
        if (pre[i] <= p)
            ans = i + 1;
    }

    pre[k - 1] = a[k - 1];

    // Finding the prefix sum for
    // the remaining elements
    for (i = k - 1; i < n; i++) {
        if (i >= k) {
            pre[i] += pre[i - k] + a[i];
        }

        // Check the number of iteams
        // that can be bought
        if (pre[i] <= p)
            ans = i + 1;
    }

    return ans;
}

// Driver code
var n = 5;
var arr = [2, 4, 3, 5, 7];
var p = 11;
var k = 2;
document.write( number(arr, n, p, k));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N*logN)

**辅助空间:** O(N)