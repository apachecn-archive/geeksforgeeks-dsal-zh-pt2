# 使前 N 个自然数的排列相等所需的最小运算次数

> 原文:[https://www . geesforgeks . org/最小操作数-对第一个 n 个自然数进行置换所需的操作数-相等/](https://www.geeksforgeeks.org/minimum-number-of-operations-required-to-make-a-permutation-of-first-n-natural-numbers-equal/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，包含第一个 **N** 自然数的[排列和一个整数 **K** ，任务是通过选择 **K** ( *1 < K ≤ N* )个连续数组元素并用所选元素的最小值替换它们来找到使所有数组元素相等所需的最小操作数。](https://www.geeksforgeeks.org/check-if-an-array-is-a-permutation-of-numbers-from-1-to-n/)

**示例:**

> **输入:** A[] = {4，2，1，5，3}，K = 3，N = 5
> **输出:** 2
> **说明:**从索引 1 到 3 中选择连续的元素，替换为最小的{4，2，1}。因此，A[]变成了{1，1，1，5，3}。
> 从 3 到 5 的索引中选择连续的元素，并用最少{1，5，3}替换。因此，A 变成了{1，1，1，1，1}。
> 因此，所需操作总数为 2。
> 
> **输入:** A[] = {3，6，2，1，4，5}，K = 2，N=6
> **输出:** 5
> **说明:**从索引 4 到索引 5 中选择连续的元素，替换为{1，4}的最小值为 1。因此，A[]变成{3，6，2，1，1，5}
> 从索引 5 到 6 中选择连续的元素，并替换为{1，5}的最小值为 1。因此，A[]变成{3，6，2，1，1，1}
> 从索引 3 到 4 中选择连续的元素，并替换为{2，1}的最小值为 1。因此，A[]变成了{3，6，1，1，1}
> 从索引 2 到 3 中选择连续的元素，并替换为{6，1}的最小值为 1。因此，A[]变成{3，1，1，1，1}
> 从索引 1 到 2 中选择连续的元素，并替换为{3，1}的最小值为 1。因此，A[]变为{1，1，1，1，1}
> 因此，操作总数为 5。

**方法:**该想法基于以下观察:

*   排列无关紧要。这和把最小值放在开头是一样的。
*   从最小指标开始向前移动 **K** 即可计算出所需的最佳操作次数。

这个问题可以通过想象最小值在数组的开始处并从那里开始，选择 **K** 个连续的元素来解决。按照以下步骤解决问题:

*   初始化变量 **i** 和**计数**为 **0** ，分别迭代和计数最小操作数。
*   [循环而](https://www.geeksforgeeks.org/c-c-do-while-loop-with-examples/) **i** 小于**N–1**，因为当 **i** 到达**N–1**时，所有元素都已相等。在每个当前迭代中，执行以下步骤:
    *   将**计数**增加 **1** 。
    *   将 **i** 增加 **K-1** ，因为最右边的更新元素将再次用于下一个片段。
*   打印**的值，计算**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number of operations required
// to make all array elements equal
int MinimumOperations(int A[],
                      int N, int K)
{
    // Store the count of
    // operations required
    int Count = 0;

    int i = 0;

    while (i < N - 1) {

        // Increment by K - 1, as the last
        // element will be used again for
        // the next K consecutive elements
        i = i + K - 1;

        // Increment count by 1
        Count++;
    }

    // Return the result
    return Count;
}

// Driver Code
int main()
{
    // Given Input
    int A[] = { 5, 4, 3, 1, 2 };
    int K = 3;
    int N = sizeof(A) / sizeof(A[0]);

    cout << MinimumOperations(A, N, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

      // Function to find the minimum
    // number of operations required
    // to make all array elements equal

    static int MinimumOperations(int[] A, int N, int K)
    {
        // Store the count of
        // operations required
        int Count = 0;

        int i = 0;

        while (i < N - 1) {

            // Increment by K - 1, as the last
            // element will be used again for
            // the next K consecutive elements
            i = i + K - 1;

            // Increment count by 1
            Count++;
        }

        // Return the result
        return Count;
    }

    // Driver Code
    public static void main (String[] args) {
        // Given Input
        int[] A = { 5, 4, 3, 1, 2 };
        int K = 3;
        int N = A.length;

        System.out.println(MinimumOperations(A, N, K));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum
# number of operations required
# to make all array elements equal
def MinimumOperations(A, N, K):

    # Store the count of
    # operations required
    Count = 0

    i = 0

    while (i < N - 1):

        # Increment by K - 1, as the last
        # element will be used again for
        # the next K consecutive elements
        i = i + K - 1

        # Increment count by 1
        Count += 1

    # Return the result
    return Count

# Driver Code
if __name__ == '__main__':

    # Given Input
    A = [ 5, 4, 3, 1, 2 ]
    K = 3
    N = len(A)

    print (MinimumOperations(A, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG {
    // Function to find the minimum
    // number of operations required
    // to make all array elements equal

    static int MinimumOperations(int[] A, int N, int K)
    {
        // Store the count of
        // operations required
        int Count = 0;

        int i = 0;

        while (i < N - 1) {

            // Increment by K - 1, as the last
            // element will be used again for
            // the next K consecutive elements
            i = i + K - 1;

            // Increment count by 1
            Count++;
        }

        // Return the result
        return Count;
    }

    // Driver Code
    public static void Main()
    {
        // Given Input
        int[] A = { 5, 4, 3, 1, 2 };
        int K = 3;
        int N = A.Length;

        Console.WriteLine(MinimumOperations(A, N, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find the minimum
        // number of operations required
        // to make all array elements equal

        function MinimumOperations(A, N, K) {
            // Store the count of
            // operations required
            let Count = 0;

            let i = 0;

            while (i < N - 1) {

                // Increment by K - 1, as the last
                // element will be used again for
                // the next K consecutive elements
                i = i + K - 1;

                // Increment count by 1
                Count++;
            }

            // Return the result
            return Count;
        }

        // Driver Code
        // Given Input
        let A = [5, 4, 3, 1, 2];
        let K = 3;
        let N = A.length;

        document.write(MinimumOperations(A, N, K));

        // This code is contributed by Hritik

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)