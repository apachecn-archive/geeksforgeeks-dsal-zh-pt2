# 从给定的两个数组中计数相等的值对，使得 a[i]等于 b[j]

> 原文:[https://www . geeksforgeeks . org/从给定的两个数组中计算相等的值对-这样-ai-equals-bj/](https://www.geeksforgeeks.org/count-of-equal-value-pairs-from-given-two-arrays-such-that-ai-equals-bj/)

分别给定长度为 **N** 和 **M** 的两个[数组](https://www.geeksforgeeks.org/array-data-structure/) **a[]** 和 **b[]** ，按照非递减顺序排序。任务是找到配对数 **(i，j)** ，使得**a【I】**等于**b【j】**。

**示例:**

> **输入:** a[] = {1，1，3，3，3，5，8，8}，b[] = {1，3，3，4，5，5，5 }
> T3】输出: 11
> **说明:**以下是给定条件的 11 对，这 11 对是{{1，1}，{1，1}，{3，3}，{3，3}，{3，3}，{3，3}，{3，3}，{3，3}
> 
> **输入:** a[] = {1，2，3，4}，b[] = {1，1，2}
> **输出:** 3

**进场:**这个问题可以用[双指针进场](https://www.geeksforgeeks.org/two-pointers-technique/)解决。让 **i** 指向数组的第一个元素 **a[]** ， **j** 指向数组的第一个元素 **b[]** 。[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)时，会出现 3 种情况。

> **情况 1: a[i] = b[j]** 让 target 表示 arr[i]，cnt1 表示数组 a 中等于 target 的元素个数，cnt2 表示数组 b 中等于 target 的元素个数。所以 a[i] = b[j]的总对数是 cnt1 * cnt2。所以我们的答案增加了 cnt1 * cnt2。
> **案例二:a[i] < b[j]** 未来得到 a[i] = b[j]的唯一可能就是递增 I，所以我们做 i++。
> **案例三:a[i] > b[j]** 未来得到 a[i] = b[j]的唯一可能就是递增 j，所以我们做 j++。

按照以下步骤解决给定的问题。

*   初始化变量 **ans，i** 和 **j** 为 **0。**
*   初始化答案， **i** ，和 **j** 到 **0** ，开始[遍历两个数组](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到 **i** 小于 **N** 或 **j** 小于 **M** 。
    *   如果 **a[i]** 等于 **b[j]，**计算 **cnt1** 和 **cnt2** ，并将答案增加 **cnt1 * cnt2** 。
    *   如果 **a[i]** 小于 **b[j]，**增量 **i** 。
    *   如果 **a[i]** 大于 **b[j]，**增量 **j** 。
*   执行上述步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ Program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find number of pairs with
// satisfying the given condition
int findPairs(int* a, int* b, int n, int m)
{

    // Initialize ans, i, j to 0 .
    int ans = 0, i = 0, j = 0;

    // Use the two pointer approach to
    // calculate the answer .
    while (i < n && j < m) {

        // Case - 1
        if (a[i] == b[j]) {

            // Target denotes a[i]
            // or b[j] as a[i] = b[j].

            // cnt1 denotes the number
            // of elements in array
            // a that are equal to target.

            // cnt2 denotes the number
            // of elements in array
            // b that are equal to target
            int target = a[i], cnt1 = 0, cnt2 = 0;

            // Calculate cnt1
            while (i < n && a[i] == target) {
                cnt1++;
                i++;
            }

            // Calculate cnt2
            while (j < m && b[j] == target) {
                cnt2++;
                j++;
            }

            // Increment the answer by (cnt1 * cnt2)
            ans += (cnt1 * cnt2);
        }

        // Case - 2
        else if (a[i] < b[j])
            i++;

        // Case - 3
        else
            j++;
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    int N = 8, M = 7;
    int a[] = { 1, 1, 3, 3, 3, 5, 8, 8 };
    int b[] = { 1, 3, 3, 4, 5, 5, 5 };

    cout << findPairs(a, b, N, M);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;

class GFG{

// Function to find number of pairs with
// satisfying the given condition
static int findPairs(int[] a, int[] b, int n, int m)
{

    // Initialize ans, i, j to 0 .
    int ans = 0, i = 0, j = 0;

    // Use the two pointer approach to
    // calculate the answer .
    while (i < n && j < m)
    {

        // Case - 1
        if (a[i] == b[j])
        {

            // Target denotes a[i]
            // or b[j] as a[i] = b[j].

            // cnt1 denotes the number
            // of elements in array
            // a that are equal to target.

            // cnt2 denotes the number
            // of elements in array
            // b that are equal to target
            int target = a[i], cnt1 = 0, cnt2 = 0;

            // Calculate cnt1
            while (i < n && a[i] == target)
            {
                cnt1++;
                i++;
            }

            // Calculate cnt2
            while (j < m && b[j] == target)
            {
                cnt2++;
                j++;
            }

            // Increment the answer by (cnt1 * cnt2)
            ans += (cnt1 * cnt2);
        }

        // Case - 2
        else if (a[i] < b[j])
            i++;

        // Case - 3
        else
            j++;
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int N = 8, M = 7;
    int a[] = { 1, 1, 3, 3, 3, 5, 8, 8 };
    int b[] = { 1, 3, 3, 4, 5, 5, 5 };

    System.out.println(findPairs(a, b, N, M));
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to find number of pairs with
# satisfying the given condition
def findPairs(a, b, n, m):

    # Initialize ans, i, j to 0 .
    ans = 0
    i = 0
    j = 0

    # Use the two pointer approach to
    # calculate the answer .
    while (i < n and j < m):

        # Case - 1
        if (a[i] == b[j]):

            # Target denotes a[i]
            # or b[j] as a[i] = b[j].

            # cnt1 denotes the number
            # of elements in array
            # a that are equal to target.

            # cnt2 denotes the number
            # of elements in array
            # b that are equal to target
            target = a[i]
            cnt1 = 0
            cnt2 = 0

            # Calculate cnt1
            while (i < n and a[i] == target):
                cnt1 += 1
                i += 1

            # Calculate cnt2
            while (j < m and b[j] == target):
                cnt2 += 1
                j += 1

            # Increment the answer by (cnt1 * cnt2)
            ans += (cnt1 * cnt2)

        # Case - 2
        elif (a[i] < b[j]):
            i += 1

        # Case- 3
        else:
            j += 1

    # Return the answer
    return ans

# Driver Code
if __name__ == "__main__":

    N = 8
    M = 7
    a = [ 1, 1, 3, 3, 3, 5, 8, 8 ]
    b = [ 1, 3, 3, 4, 5, 5, 5 ]

    print(findPairs(a, b, N, M))

# This code is contributed by ukasp
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to find number of pairs with
// satisfying the given condition
static int findPairs(int[] a, int[] b, int n, int m)
{

    // Initialize ans, i, j to 0 .
    int ans = 0, i = 0, j = 0;

    // Use the two pointer approach to
    // calculate the answer .
    while (i < n && j < m)
    {

        // Case - 1
        if (a[i] == b[j])
        {

            // Target denotes a[i]
            // or b[j] as a[i] = b[j].

            // cnt1 denotes the number
            // of elements in array
            // a that are equal to target.

            // cnt2 denotes the number
            // of elements in array
            // b that are equal to target
            int target = a[i], cnt1 = 0, cnt2 = 0;

            // Calculate cnt1
            while (i < n && a[i] == target)
            {
                cnt1++;
                i++;
            }

            // Calculate cnt2
            while (j < m && b[j] == target)
            {
                cnt2++;
                j++;
            }

            // Increment the answer by (cnt1 * cnt2)
            ans += (cnt1 * cnt2);
        }

        // Case - 2
        else if (a[i] < b[j])
            i++;

        // Case - 3
        else
            j++;
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void Main()
{
    int N = 8, M = 7;
    int []a = { 1, 1, 3, 3, 3, 5, 8, 8 };
    int []b = { 1, 3, 3, 4, 5, 5, 5 };

    Console.Write(findPairs(a, b, N, M));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript Program for above approach

// Function to find number of pairs with
// satisfying the given condition
function findPairs(a, b, n, m)
{

    // Initialize ans, i, j to 0 .
    let ans = 0, i = 0, j = 0;

    // Use the two pointer approach to
    // calculate the answer .
    while (i < n && j < m) {

        // Case - 1
        if (a[i] == b[j]) {

            // Target denotes a[i]
            // or b[j] as a[i] = b[j].

            // cnt1 denotes the number
            // of elements in array
            // a that are equal to target.

            // cnt2 denotes the number
            // of elements in array
            // b that are equal to target
            let target = a[i], cnt1 = 0, cnt2 = 0;

            // Calculate cnt1
            while (i < n && a[i] == target) {
                cnt1++;
                i++;
            }

            // Calculate cnt2
            while (j < m && b[j] == target) {
                cnt2++;
                j++;
            }

            // Increment the answer by (cnt1 * cnt2)
            ans += (cnt1 * cnt2);
        }

        // Case - 2
        else if (a[i] < b[j])
            i++;

        // Case - 3
        else
            j++;
    }

    // Return the answer
    return ans;
}

// Driver Code
let N = 8, M = 7;
let a = [ 1, 1, 3, 3, 3, 5, 8, 8 ];
let b = [ 1, 3, 3, 4, 5, 5, 5 ];

document.write(findPairs(a, b, N, M));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
11
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(1)*