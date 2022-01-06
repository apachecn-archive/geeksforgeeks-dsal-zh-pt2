# 给定大小的子序列的所有对的最小差的最大值

> 原文:[https://www . geeksforgeeks . org/给定大小的子序列的所有对的最大/最小差值/](https://www.geeksforgeeks.org/maximum-of-minimum-difference-of-all-pairs-from-subsequences-of-given-size/)

给定一个大小为 **N** 的整数数组 **A[ ]** ，任务是找到一个大小为 **B** 的子序列，使得其中任意两个之间的最小差最大，并打印这个最大的最小差。

**示例:**

> **输入:** A[ ] = {1，2，3，5}，B = 3
> **输出:** 2
> **解释:**
> 大小为 3 的可能子序列为{1，2，3}、{1，2，5}、{1，3，5}和{2，3，5}。
> 对于{1，3，5}，可能的差异是(| 1–3 | = 2)、(| 3–5 | = 2)和(| 1–5 | = 4)，最小值(2，2，4) = 2
> 对于剩余的子序列，最小差异是 1。
> 因此，所有最小差异的最大值为 2。
> 
> **输入:** A[ ] = {5，17，11}，B = 2
> **输出:** 12
> **解释:**
> 大小为 2 的可能子序列为{5，17}、{17，11}和{5，11}。
> 对于{5，17}，可能的差异为(| 5–17 | = 12)，最小值= 12
> 对于{17，11}，可能的差异为(| 17–11 | = 6)，最小值= 6
> 对于{5，11}，可能的差异为(| 5–11 | = 6)，最小值= 6
> 最大值(12，6，6) = 12
> 因此，所有最小差异的最大值为 12。

**天真方法:**
解决这个问题最简单的方法就是[生成所有可能大小的子序列](https://www.geeksforgeeks.org/print-subsets-given-size-set/) **B** ，在所有可能的子序列对中找出最小的差异。最后，在所有最小差异中找到最大值。

***时间复杂度:**O(2<sup>N</sup>* N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**
使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)按照以下步骤优化上述方法:

*   将搜索空间从 **0** 设置为数组中的最大元素( **maxm** )
*   对于每一个计算出的**中间**，检查是否有可能得到大小为 **B** 的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，其中任意一对之间的*最小差等于**中间**T9】。*
*   如果可能，那么将 **mid** 存储在一个变量中，在右半部分找到更好的答案，丢弃 mid 的左半部分
*   否则，遍历 mid 的左半部分，检查是否存在最小对差较小的子序列。
*   最后，在二分搜索法终止后，打印最高的***中间的*** ，对于该最高的*最高的**中间的【】***找到具有等于**中间的**的最小对差的任何子序列。

> **图解:**T2【A】= { 1，2，3，4，5}，B = 3
> T4【搜索空间: {0，1，2，3，4，5}
> 二分搜索法涉及的步骤如下:
> 
> *   start = 0，end = 5，mid = (0 + 5) / 2 = 2
>     大小的子序列 **B** 与 **mid** (= 2)的最小差值为{1，3，5}。
>     因此，ans = 2
> *   现在，穿过右半部分。
>     开始=中间+1 = 3，结束= 5，中间= (3 + 5) / 2 = 4
>     尺寸 B 的子序列不可能有最小差异**中间** (= 4)。
>     所以，俺们还是 2。
> *   现在，遍历左半部分
>     开始= 3，结束=中间–1 = 3，中间= (3 + 3) / 2 = 3
>     大小的子序列 **B** 不可能有最小的中间差(= 3)。
>     所以，俺们还是 2。
> *   再一次，穿过左半边。
>     开始= 3，结束=中间–1 = 2。
>     由于**开始**超过**结束**，二分搜索法终止。
> *   最后，最大可能的最小差异是 2。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check a subsequence can
// be formed with min difference mid
bool can_place(int A[], int n,
               int B, int mid)
{
    int count = 1;
    int last_position = A[0];

    // If a subsequence of size B
    // with min diff = mid is possible
    // return true else false
    for (int i = 1; i < n; i++) {

        if (A[i] - last_position
            >= mid) {
            last_position = A[i];
            count++;
            if (count == B) {
                return true;
            }
        }
    }
    return false;
}

// Function to find the maximum of
// all minimum difference of pairs
// possible among the subsequence
int find_min_difference(int A[],
                        int n, int B)
{

    // Sort the Array
    sort(A, A + n);

    // Stores the boundaries
    // of the search space
    int s = 0;
    int e = A[n - 1] - A[0];

    // Store the answer
    int ans = 0;

    // Binary Search
    while (s <= e) {

        long long int mid = (s + e) / 2;

        // If subsequence can be formed
        // with min diff mid and size B
        if (can_place(A, n, B, mid)) {
            ans = mid;

            // Right half
            s = mid + 1;
        }
        else {

            // Left half
            e = mid - 1;
        }
    }

    return ans;
}

// Driver Code
int main()
{
    int A[] = { 1, 2, 3, 5 };
    int n = sizeof(A) / sizeof(A[0]);
    int B = 3;

    int min_difference
        = find_min_difference(A, n, B);
    cout << min_difference;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check a subsequence can
// be formed with min difference mid
static boolean can_place(int A[], int n,
                         int B, int mid)
{
    int count = 1;
    int last_position = A[0];

    // If a subsequence of size B
    // with min diff = mid is possible
    // return true else false
    for(int i = 1; i < n; i++)
    {
        if (A[i] - last_position >= mid)
        {
            last_position = A[i];
            count++;
            if (count == B)
            {
                return true;
            }
        }
    }
    return false;
}

// Function to find the maximum of
// all minimum difference of pairs
// possible among the subsequence
static int find_min_difference(int A[],
                        int n, int B)
{

    // Sort the Array
    Arrays.sort(A);

    // Stores the boundaries
    // of the search space
    int s = 0;
    int e = A[n - 1] - A[0];

    // Store the answer
    int ans = 0;

    // Binary Search
    while (s <= e)
    {
        int mid = (s + e) / 2;

        // If subsequence can be formed
        // with min diff mid and size B
        if (can_place(A, n, B, mid))
        {
            ans = mid;

            // Right half
            s = mid + 1;
        }
        else
        {

            // Left half
            e = mid - 1;
        }
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 1, 2, 3, 5 };
    int n = A.length;
    int B = 3;

    int min_difference = find_min_difference(A, n, B);

    System.out.print(min_difference);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check a subsequence can
# be formed with min difference mid
def can_place(A, n, B, mid):

    count = 1
    last_position = A[0]

    # If a subsequence of size B
    # with min diff = mid is possible
    # return true else false
    for i in range(1, n):
        if (A[i] - last_position >= mid):
            last_position = A[i]
            count = count + 1

            if (count == B):
                return bool(True)

    return bool(False)

# Function to find the maximum of
# all minimum difference of pairs
# possible among the subsequence
def find_min_difference(A, n, B):

    # Sort the Array
    A.sort()

    # Stores the boundaries
    # of the search space
    s = 0
    e = A[n - 1] - A[0]

    # Store the answer
    ans = 0

    # Binary Search
    while (s <= e):
        mid = (int)((s + e) / 2)

        # If subsequence can be formed
        # with min diff mid and size B
        if (can_place(A, n, B, mid)):
            ans = mid

            # Right half
            s = mid + 1

        else:

            # Left half
            e = mid - 1

    return ans

# Driver code
A = [ 1, 2, 3, 5 ]
n = len(A)
B = 3

min_difference = find_min_difference(A, n, B)

print(min_difference)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to check a subsequence can
// be formed with min difference mid
static bool can_place(int[] A, int n,
                      int B, int mid)
{
    int count = 1;
    int last_position = A[0];

    // If a subsequence of size B
    // with min diff = mid is possible
    // return true else false
    for(int i = 1; i < n; i++)
    {
        if (A[i] - last_position >= mid)
        {
            last_position = A[i];
            count++;
            if (count == B)
            {
                return true;
            }
        }
    }
    return false;
}

// Function to find the maximum of
// all minimum difference of pairs
// possible among the subsequence
static int find_min_difference(int[] A,
                        int n, int B)
{

    // Sort the Array
    Array.Sort(A);

    // Stores the boundaries
    // of the search space
    int s = 0;
    int e = A[n - 1] - A[0];

    // Store the answer
    int ans = 0;

    // Binary Search
    while (s <= e)
    {
        int mid = (s + e) / 2;

        // If subsequence can be formed
        // with min diff mid and size B
        if (can_place(A, n, B, mid))
        {
            ans = mid;

            // Right half
            s = mid + 1;
        }
        else
        {

            // Left half
            e = mid - 1;
        }
    }
    return ans;
}

// Driver Code
public static void Main(string[] args)
{
    int[] A = { 1, 2, 3, 5 };
    int n = A.Length;
    int B = 3;

    int min_difference = find_min_difference(A, n, B);

    Console.Write(min_difference);
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to check a subsequence can
// be formed with min difference mid
function can_place(A, n, B, mid)
{
    let count = 1;
    let last_position = A[0];

    // If a subsequence of size B
    // with min diff = mid is possible
    // return true else false
    for(let i = 1; i < n; i++)
    {
        if (A[i] - last_position >= mid)
        {
            last_position = A[i];
            count++;

            if (count == B)
            {
                return true;
            }
        }
    }
    return false;
}

// Function to find the maximum of
// all minimum difference of pairs
// possible among the subsequence
function find_min_difference(A, n, B)
{

    // Sort the Array
    A.sort();

    // Stores the boundaries
    // of the search space
    let s = 0;
    let e = A[n - 1] - A[0];

    // Store the answer
    let ans = 0;

    // Binary Search
    while (s <= e)
    {
        let mid = parseInt((s + e) / 2, 10);

        // If subsequence can be formed
        // with min diff mid and size B
        if (can_place(A, n, B, mid))
        {
            ans = mid;

            // Right half
            s = mid + 1;
        }
        else
        {

            // Left half
            e = mid - 1;
        }
    }
    return ans;
}

// Driver code
let A = [ 1, 2, 3, 5 ];
let n = A.length;
let B = 3;
let min_difference = find_min_difference(A, n, B);

document.write(min_difference);

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*