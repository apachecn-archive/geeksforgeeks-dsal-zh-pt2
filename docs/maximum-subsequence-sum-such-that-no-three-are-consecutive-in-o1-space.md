# 最大子序列和，使得在 O(1)空间中没有三个连续的

> 原文:[https://www . geesforgeks . org/maximum-sub-sequence-sum-so-no-3 是 o1-space 中的连续序列/](https://www.geeksforgeeks.org/maximum-subsequence-sum-such-that-no-three-are-consecutive-in-o1-space/)

给定一个由 N 个正数组成的数组 A[]，任务是找到可以形成的最大和，其中不存在三个连续的元素。

**示例:**

> **输入:** A[] = {1，2，3}，N=3
> **输出:** 5
> **说明:**三者不能合在一起所以答案是 2 + 3 = 5
> 
> **输入:** A[] = {3000，2000，1000，3，10}，N = 5
> T3】输出: 5013

这里[已经讨论了一种采用 **O(N)** 辅助空间的 **O(N)** 方法](https://www.geeksforgeeks.org/maximum-subsequence-sum-such-that-no-three-are-consecutive/)。这可以通过以下占用 **O(1)** 额外空间的方法进一步优化。

**O(1)空间方法:**从上述方法，我们可以得出结论:对于计算**和【I】，**只有**和【i-1】、和【I-2】**和**和【I-3】**的值是相关的。这种观察可以帮助完全丢弃和数组，取而代之的是只维护一些变量来使用 O(1)辅助空间解决问题。

按照以下步骤解决问题:

*   初始化要使用的以下变量:
    *   **总和:**这存储最终总和，使得没有三个元素是连续的。
    *   **首先:**这将子序列总和存储到索引 **i-1** 中。
    *   **秒:**这将子序列总和存储到索引 **i-2** 中。
    *   **第三个:**这存储了索引 **i-3** 的子序列和。
*   如果 **N < 3** ，答案将是所有元素的总和，因为没有连续性。
*   否则，请执行以下操作:
    *   用**A【0】**初始化第三个
    *   **用 **A[0]+A[1]** 初始化**秒****
    *   **首先用**最大值初始化**(其次，A[1]+A[2])******
    *   **将**第一**、**第二**、**第三**中最大的相加初始化。**
    *   **从 **3** 迭代到 **N-1** ，对每个当前指标 **i** 进行如下操作:

        *   可能有以下三种情况:
            *   排除 **A[i]，**即**和=第一**
            *   排除 **A[i-1]，**即**和=秒+ A[i]**
            *   排除 **A[i-2]** ，即**和=三分之一+ A[i] + A[i-1]**
        *   因此，**总和**被更新为**第一**、**(第二+A[i])** 和**(第三+A[i]+A[i-1])**
        *   用**更新**第三**，用**更新**第二**，用**第一**更新**第一**，用**和**更新。** 
*   **最后，返回**总和**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the  maximum subsequence sum such
// that no three elements are consecutive
int maxSumWO3Consec(int A[], int N)
{
    // when N is 1, answer would be the only element present
    if (N == 1)
        return A[0];
    // when N is 2, answer would be sum of elements
    if (N == 2)
        return A[0] + A[1];
    // variable to store sum up to i - 3
    int third = A[0];

    // variable to store sum up to i - 2
    int second = third + A[1];

    // variable to store sum up to i - 1
    int first = max(second, A[1] + A[2]);

    // variable to store the final sum of the subsequence
    int sum = max(max(third, second), first);

    for (int i = 3; i < N; i++) {
        // find the maximum subsequence sum up to index i
        sum = max(max(first, second + A[i]),
                  third + A[i] + A[i - 1]);

        // update first, second and third
        third = second;
        second = first;
        first = sum;
    }
    // return ans;
    return sum;
}

// Driver code
int main()
{
    // Input
    int A[] = { 3000, 2000, 1000, 3, 10 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    cout << maxSumWO3Consec(A, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to calculate the  maximum subsequence sum
    // such
    // that no three elements are consecutive
    public static int maxSumWO3Consec(int A[], int N)
    {

        // when N is 1, answer would be the only element
        // present
        if (N == 1)
            return A[0];
        // when N is 2, answer would be sum of elements
        if (N == 2)
            return A[0] + A[1];
        // variable to store sum up to i - 3
        int third = A[0];

        // variable to store sum up to i - 2
        int second = third + A[1];

        // variable to store sum up to i - 1
        int first = Math.max(second, A[1] + A[2]);

        // variable to store the final sum of the
        // subsequence
        int sum = Math.max(Math.max(third, second), first);

        for (int i = 3; i < N; i++)
        {

            // find the maximum subsequence sum up to index
            // i
            sum = Math.max(Math.max(first, second + A[i]),
                           third + A[i] + A[i - 1]);

            // update first, second and third
            third = second;
            second = first;
            first = sum;
        }
        // return ans;
        return sum;
    }

    public static void main(String[] args)
    {
        // Input
        int A[] = { 3000, 2000, 1000, 3, 10 };
        int N = A.length;

        // Function call
        int res = maxSumWO3Consec(A, N);
        System.out.println(res);

    }
}

//This code is contributed by Potta Lokesh
```

## **蟒蛇 3**

```
# Python 3 implementation for the above approach

# Function to calculate the  maximum subsequence sum such
# that no three elements are consecutive
def maxSumWO3Consec(A, N):

    # when N is 1, answer would be the only element present
    if (N == 1):
        return A[0]

    # when N is 2, answer would be sum of elements
    if (N == 2):
        return A[0] + A[1]

    # variable to store sum up to i - 3
    third = A[0]

    # variable to store sum up to i - 2
    second = third + A[1]

    # variable to store sum up to i - 1
    first = max(second, A[1] + A[2])

    # variable to store the final sum of the subsequence
    sum = max(max(third, second), first)

    for i in range(3,N,1):

        # find the maximum subsequence sum up to index i
        sum = max(max(first, second + A[i]), third + A[i] + A[i - 1])

        # update first, second and third
        third = second
        second = first
        first = sum
    # return ans;
    return sum

# Driver code
if __name__ == '__main__':

    # Input
    A = [3000, 2000, 1000, 3, 10]
    N = len(A)

    # Function call
    print(maxSumWO3Consec(A, N))

    # This code is contributed by ipg2016107.
```

## **C#**

```
// C# program for the above approach
using System;

class GFG {

    // Function to calculate the  maximum subsequence sum
    // such
    // that no three elements are consecutive
    public static int maxSumWO3Consec(int[] A, int N)
    {

        // when N is 1, answer would be the only element
        // present
        if (N == 1)
            return A[0];
        // when N is 2, answer would be sum of elements
        if (N == 2)
            return A[0] + A[1];
        // variable to store sum up to i - 3
        int third = A[0];

        // variable to store sum up to i - 2
        int second = third + A[1];

        // variable to store sum up to i - 1
        int first = Math.Max(second, A[1] + A[2]);

        // variable to store the final sum of the
        // subsequence
        int sum = Math.Max(Math.Max(third, second), first);

        for (int i = 3; i < N; i++) {

            // find the maximum subsequence sum up to index
            // i
            sum = Math.Max(Math.Max(first, second + A[i]),
                           third + A[i] + A[i - 1]);

            // update first, second and third
            third = second;
            second = first;
            first = sum;
        }
        // return ans;
        return sum;
    }

    // Driver Code
    public static void Main()
    {
        // Input
        int[] A = { 3000, 2000, 1000, 3, 10 };
        int N = A.Length;

        // Function call
        int res = maxSumWO3Consec(A, N);
        Console.Write(res);
    }
}
```

## **java 描述语言**

```
<script>
        // JavaScript implementation for the above approach

        // Function to calculate the  maximum subsequence sum such
        // that no three elements are consecutive
        function maxSumWO3Consec(A, N)
        {

            // when N is 1, answer would be the only element present
            if (N == 1)
                return A[0];
            // when N is 2, answer would be sum of elements
            if (N == 2)
                return A[0] + A[1];
            // variable to store sum up to i - 3
            let third = A[0];

            // variable to store sum up to i - 2
            let second = third + A[1];

            // variable to store sum up to i - 1
            let first = Math.max(second, A[1] + A[2]);

            // variable to store the final sum of the subsequence
            let sum = Math.max(Math.max(third, second), first);

            for (let i = 3; i < N; i++) {
                // find the maximum subsequence sum up to index i
                sum = Math.max(Math.max(first, second + A[i]),
                    third + A[i] + A[i - 1]);

                // update first, second and third
                third = second;
                second = first;
                first = sum;
            }
            // return ans;
            return sum;
        }

        // Driver code

        // Input
        let A = [3000, 2000, 1000, 3, 10];
        let N = A.length;

        // Function call
        document.write(maxSumWO3Consec(A, N));

//This code is contributed by Potta Lokesh
    </script>
```

****Output:** 

```
5013
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**