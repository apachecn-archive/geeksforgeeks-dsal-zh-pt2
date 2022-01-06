# 从 1 到 N 所需的最小数量，其和为 K

> 原文:[https://www . geeksforgeeks . org/从 1 到 n 的最小所需数字计数得出 k 的总和/](https://www.geeksforgeeks.org/minimum-count-of-numbers-needed-from-1-to-n-that-yields-the-sum-as-k/)

给定两个正整数 **N** 和 **K** ，任务是打印得到等于 **K** 的和所需的最小个数，只需从[前 N 个自然数](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)中添加任意元素一次。如果无法得到等于 **K** 的总和，则打印“ **-1** ”。

**示例:**

> **输入:** N = 5，K = 10
> **输出:** 3
> **说明:**
> 最优的方式是选择数{1，4，5}加起来会是 10。
> 因此，打印所需元素的最小数量 3。
> 
> **输入:** N = 5，K = 1000
> **输出:** -1
> **说明:**
> 不可能得到等于 1000 的和。

**方法:**使用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决此问题:

*   如果 **K** 大于[前 N 个自然数](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)**之和，则打印“ **-1** ”然后**返回**。**
*   **如果 **K** 小于等于 **N，**则打印 **1** ，然后**返回**。**
*   **否则，初始化变量说**求和**，**计数**为 **0** ，以存储所需数字的总和和最小计数。**
*   **[迭代直到](https://www.geeksforgeeks.org/python-while-loop/) **N** 大于等于**1****和**小于 **K** ，执行以下步骤 **:**

    *   将**计数**递增 **1，将**求和 **N** ，然后将 **N** 递减 **1** 。** 
*   **最后，如果以上情况都不满足，则打印**计数**作为答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to find minimum number of
// elements required to obtain sum K
int Minimum(int N, int K)
{

    // Stores the maximum sum that
    // can be obtained
    int sum = N * (N + 1) / 2;

    // If K is greater than the
    // Maximum sum
    if (K > sum)
        return -1;

    // If K is less than or equal
    // to to N
    if (K <= N)
        return 1;

    // Stores the sum
    sum = 0;

    // Stores the count of numbers
    // needed
    int count = 0;

    // Iterate until N is greater than
    // or equal to 1 and sum is less
    // than K
    while (N >= 1 && sum < K) {

        // Increment count by 1
        count += 1;

        // Increment sum by N
        sum += N;

        // Update the sum
        N -= 1;
    }

    // Finally, return the count
    return count;
}

// Driver Code
int main()
{
    // Given Input
    int N = 5, K = 10;

    // Function Call
    cout << (Minimum(N, K));

    return 0;
}

 // This code is contributed by Potta Lokesh
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach

import java.io.*;

// Function to find minimum number of
// elements required to obtain sum K
class GFG {

    static int Minimum(int N, int K)
    {
        // Stores the maximum sum that
        // can be obtained
        int sum = N * (N + 1) / 2;

        // If K is greater than the
        // Maximum sum
        if (K > sum)
            return -1;

        // If K is less than or equal
        // to to N
        if (K <= N)
            return 1;

        // Stores the sum
        sum = 0;

        // Stores the count of numbers
        // needed
        int count = 0;

        // Iterate until N is greater than
        // or equal to 1 and sum is less
        // than K
        while (N >= 1 && sum < K) {

            // Increment count by 1
            count += 1;

            // Increment sum by N
            sum += N;

            // Update the sum
            N -= 1;
        }

        // Finally, return the count
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        int N = 5, K = 10;

        // Function Call
        System.out.println(Minimum(N, K));
    }
}
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find minimum number of
# elements required to obtain sum K
def Minimum(N, K):

    # Stores the maximum sum that
    # can be obtained
    sum = N * (N + 1) // 2

    # If K is greater than the
    # Maximum sum
    if (K > sum):
        return -1

    # If K is less than or equal
    # to to N
    if (K <= N):
        return 1

    # Stores the sum
    sum = 0

    # Stores the count of numbers
    # needed
    count = 0

    # Iterate until N is greater than
    # or equal to 1 and sum is less
    # than K
    while (N >= 1 and sum < K):

        # Increment count by 1
        count += 1

        # Increment sum by N
        sum += N

        # Update the sum
        N -= 1

    # Finally, return the count
    return count

# Driver Code
if __name__ == '__main__':

    # Given Input
    N = 5
    K = 10

    # Function Call
    print(Minimum(N, K))

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for the above approach
using System;

// Function to find minimum number of
// elements required to obtain sum K
class GFG{

static int Minimum(int N, int K)
{

    // Stores the maximum sum that
    // can be obtained
    int sum = N * (N + 1) / 2;

    // If K is greater than the
    // Maximum sum
    if (K > sum)
        return -1;

    // If K is less than or equal
    // to to N
    if (K <= N)
        return 1;

    // Stores the sum
    sum = 0;

    // Stores the count of numbers
    // needed
    int count = 0;

    // Iterate until N is greater than
    // or equal to 1 and sum is less
    // than K
    while (N >= 1 && sum < K)
    {

        // Increment count by 1
        count += 1;

        // Increment sum by N
        sum += N;

        // Update the sum
        N -= 1;
    }

    // Finally, return the count
    return count;
}

// Driver Code
static public void Main()
{

    // Given Input
    int N = 5, K = 10;

    // Function Call
    Console.Write(Minimum(N, K));
}
}

// This code is contributed by sanjoy_62
```

## **java 描述语言**

```
<script>

// JavaScript implementation of
// the above approach

    function Minimum(N, K)
    {
        // Stores the maximum sum that
        // can be obtained
        let sum = N * (N + 1) / 2;

        // If K is greater than the
        // Maximum sum
        if (K > sum)
            return -1;

        // If K is less than or equal
        // to to N
        if (K <= N)
            return 1;

        // Stores the sum
        sum = 0;

        // Stores the count of numbers
        // needed
        let count = 0;

        // Iterate until N is greater than
        // or equal to 1 and sum is less
        // than K
        while (N >= 1 && sum < K) {

            // Increment count by 1
            count += 1;

            // Increment sum by N
            sum += N;

            // Update the sum
            N -= 1;
        }

        // Finally, return the count
        return count;
    }

// Driver Code

        // Given Input
        let N = 5, K = 10;

        // Function Call
        document.write(Minimum(N, K));

</script>
```

****Output**

```
3
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**