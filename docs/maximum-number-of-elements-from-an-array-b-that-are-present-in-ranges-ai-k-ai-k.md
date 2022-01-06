# 数组 B[]中存在于范围[A[i] + K，A[I]–K]

中的元素的最大数量

> 原文:[https://www . geeksforgeeks . org/数组中存在的最大元素数-范围-ai-k-ai-k/](https://www.geeksforgeeks.org/maximum-number-of-elements-from-an-array-b-that-are-present-in-ranges-ai-k-ai-k/)

给定两个大小为 **N** 的[**A【】**和大小为 **M** 的**B【】**以及一个整数 **K** ，任务是为每个元素**A【I】**从](https://www.geeksforgeeks.org/array-data-structure/)[数组](https://www.geeksforgeeks.org/array-data-structure/)**B【】**中最多选择一个元素，使得该元素位于**【A【I】–K，A【I】+范围内打印可从[数组](https://www.geeksforgeeks.org/array-data-structure/) **B[]中选择的最大元素数。****

**示例:**

> **输入:** N = 4，A[] = {60，45，80，60}，M = 3，B[] = {30，60，75}，K= 5
> **输出:** 2
> **解释:**
> B[0] (= 30):不存在于任何范围[A[i] + K，A[I]–K]。
> B[1] (= 60): B[1]位于[A[0]–K，A[0] + K]范围内，即[55，65]。
> B[2] (= 75): B[2]位于[A[2]–K，A[2] + K]范围内，即[75，85]。
> 
> **输入:** N = 3 A[] = {10，20，30}，M = 3，B[] = {5，10，15}，K = 10
> T3】输出: 2

**天真法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **A[]** ，[在](https://www.geeksforgeeks.org/linear-search/)[数组](https://www.geeksforgeeks.org/array-data-structure/) **B[]** 中线性搜索，如果选择了数组 **B[]** 的值，则标记已访问。最后，从可以选择的数组 **B[]** 中打印最大数量的元素。

***时间复杂度:** O(N * M)*
***辅助空间:** O(M)*

**有效方法:**对数组 **A[]** 和 **B[]** 进行排序，并尝试分配 **B[]** 中位于**【A[I]–K，A[i] + K 范围内的元素。**按照以下步骤解决问题:

*   [排序](https://www.geeksforgeeks.org/quick-sort/)T2T4【A】和 **B[]。**
*   初始化一个变量，说 **j** 为 **0，**在数组中跟踪**B[]****计数**为 **0** 存储答案。
*   [在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**内迭代，执行以下步骤:
    *   [循环迭代](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到 **j < M** 和**B【J】<A【I】–K，**然后将 **j** 的值增加 **1。**
    *   如果 **j** 的值小于 **M** 和**B【j】**大于等于**A【I】–K**和**B【j】**小于等于**A【I】+K**则**的值增加**和**j**1。
*   完成以上步骤后，打印**计数**的值作为答案的最终值。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the maximum number of
// elements that can be selected from array
// B[] lying in the range [A[i] - K, A[i] + K]
int selectMaximumEle(int n, int m, int k,
                     int A[], int B[])
{
    // Sort both arrays
    sort(A, A + n);
    sort(B, B + m);

    int j = 0, count = 0;

    // Iterate in the range[0, N-1]
    for (int i = 0; i < n; i++) {

        // Increase the value of j till
        // B[j] is smaller than A[i]
        while (j < m && B[j] < A[i] - k) {
            j++;
        }

        // Increasing count variable when B[j]
        // lies in the range [A[i]-K, A[i]+K]
        if (j < m && B[j] >= A[i] - k
            && B[j] <= A[i] + k) {

            count++;
            j++;
        }
    }

    // Finally, return the answer
    return count;
}

// Driver Code
int main()
{
    // Given Input
    int N = 3, M = 3, K = 10;
    int A[] = { 10, 20, 30 };
    int B[] = { 5, 10, 15 };

    // Function Call
    cout << selectMaximumEle(N, M, K, A, B) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Arrays;

class GFG
{

    // Function to count the maximum number of
    // elements that can be selected from array
    // B[] lying in the range [A[i] - K, A[i] + K]
    static int selectMaximumEle(int n, int m, int k,
                                int A[], int B[])
    {
        // Sort both arrays
        Arrays.sort(A);
        Arrays.sort(B);

        int j = 0, count = 0;

        // Iterate in the range[0, N-1]
        for (int i = 0; i < n; i++) {

            // Increase the value of j till
            // B[j] is smaller than A[i]
            while (j < m && B[j] < A[i] - k) {
                j++;
            }

            // Increasing count variable when B[j]
            // lies in the range [A[i]-K, A[i]+K]
            if (j < m && B[j] >= A[i] - k
                && B[j] <= A[i] + k) {

                count++;
                j++;
            }
        }

        // Finally, return the answer
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Input
        int N = 3, M = 3, K = 10;
        int A[] = { 10, 20, 30 };
        int B[] = { 5, 10, 15 };

        // Function Call
        System.out.println(selectMaximumEle(N, M, K, A, B));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the maximum number of
# elements that can be selected from array
# B[] lying in the range [A[i] - K, A[i] + K]
def selectMaximumEle(n, m, k, A, B):

    # Sort both arrays
    A.sort()
    B.sort()

    j = 0
    count = 0

    # Iterate in the range[0, N-1]
    for i in range(n):

        # Increase the value of j till
        # B[j] is smaller than A[i]
        while (j < m and B[j] < A[i] - k):
            j += 1

        # Increasing count variable when B[j]
        # lies in the range [A[i]-K, A[i]+K]
        if (j < m and B[j] >= A[i] - k
                and B[j] <= A[i] + k):

            count += 1
            j += 1

    # Finally, return the answer
    return count

# Driver Code

# Given Input
N = 3
M = 3
K = 10
A = [ 10, 20, 30 ]
B = [ 5, 10, 15 ]

# Function Call
print(selectMaximumEle(N, M, K, A, B))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the maximum number of
// elements that can be selected from array
// B[] lying in the range [A[i] - K, A[i] + K]
static int selectMaximumEle(int n, int m, int k,
                            int[] A, int[] B)
{

    // Sort both arrays
    Array.Sort(A);
    Array.Sort(B);

    int j = 0, count = 0;

    // Iterate in the range[0, N-1]
    for(int i = 0; i < n; i++)
    {

        // Increase the value of j till
        // B[j] is smaller than A[i]
        while (j < m && B[j] < A[i] - k)
        {
            j++;
        }

        // Increasing count variable when B[j]
        // lies in the range [A[i]-K, A[i]+K]
        if (j < m && B[j] >= A[i] - k &&
                     B[j] <= A[i] + k)
        {
            count++;
            j++;
        }
    }

    // Finally, return the answer
    return count;
}

// Driver code
public static void Main()
{

    // Given Input
    int N = 3, M = 3, K = 10;
    int[] A = { 10, 20, 30 };
    int[] B = { 5, 10, 15 };

    // Function Call
    Console.WriteLine(selectMaximumEle(N, M, K, A, B));
}
}

// This code is contributed by avijitmondal1998
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

// Function to count the maximum number of
// elements that can be selected from array
// B[] lying in the range [A[i] - K, A[i] + K]
function selectMaximumEle(n, m, k, A, B) {
    // Sort both arrays
    A.sort((a, b) => a - b);
    B.sort((a, b) => a - b);

    let j = 0, count = 0;

    // Iterate in the range[0, N-1]
    for (let i = 0; i < n; i++) {

        // Increase the value of j till
        // B[j] is smaller than A[i]
        while (j < m && B[j] < A[i] - k) {
            j++;
        }

        // Increasing count variable when B[j]
        // lies in the range [A[i]-K, A[i]+K]
        if (j < m && B[j] >= A[i] - k
            && B[j] <= A[i] + k) {

            count++;
            j++;
        }
    }

    // Finally, return the answer
    return count;
}

// Driver Code

// Given Input
let N = 3, M = 3, K = 10;
let A = [10, 20, 30];
let B = [5, 10, 15];

// Function Call
document.write(selectMaximumEle(N, M, K, A, B) + "<br>");

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*