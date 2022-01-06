# 阵列上满足给定条件所需的最小增量/减量操作

> 原文:[https://www . geesforgeks . org/最小增量-减量-操作-阵列上需要满足给定条件/](https://www.geeksforgeeks.org/minimum-increment-decrement-operations-required-on-array-to-satisfy-given-conditions/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出任意索引 I 所需的最小增量或减量操作数，使得对于每个 **i** **(1 ≤ i < N)** 如果索引处从 **1** 到 **i** 的元素之和为**正**，则从 **1** 到的元素之和

**注意:**将数组视为基于 1 的索引。

**示例:**

> **输入:** arr[] = {3，-4，5，0，1}
> **输出:** 6
> **解释:**
> 将数组转换为{3，-4，5，-5，2}。这里，直到 I 的元素之和表示为 s <sub>i.</sub>
> 对于 i = 1，s <sub>1</sub> = 3，s <sub>2</sub> = 3 + (-4) = -1。s <sub>1</sub> 为正，s <sub>2</sub> 为负。
> 为 i=2，s <sub>2</sub> = -1，s <sub>3</sub> = 3 + (-4) + 5 = 4。s <sub>2</sub> 为阴性，s <sub>3</sub> 为阳性。
> 对于 i = 3，s <sub>3</sub> = 4，s <sub>4</sub> = 3 + (-4) + 5 + (-5) = -1。s <sub>3</sub> 为正，s <sub>4</sub> 为负。
> 为 i = 4，s <sub>4</sub> = -1，s <sub>5</sub> = 3 + (-4) + 5 +(-5) + 2 = 1。s <sub>4</sub> 为负，s <sub>5</sub> 为正。
> 
> **输入:** arr[] = {1，-2，2，-3}
> **输出:** 0
> **说明:**
> 给定数组已经满足条件。因此，不需要执行任何操作。

**方法:**如果对于从 **1 到 N–1**的每个 I，阵列将满足条件:

*   如果 I 为**奇数**，那么从 1 到 I 的元素之和为**正**。
*   如果 I 是**甚至**，那么从 1 到 I 的元素之和就是**负**，反之亦然。

尝试以上两种可能性，选择操作次数最少的一种。以下是步骤:

1.  初始化一个变量 *num_of_ops* = 0，它标志着到目前为止完成的操作数量。
2.  对于任意指标 **i** ，如果 **i** 为**偶**，1 到 i 的元素之和为**负**，则在**arr【I】**中加上 **(1+|sum|)** 使其为**正**。现在从 1 到 I 的元素之和为 **1** 。同时在 *num_of_ops 中加入 **(1+|sum|)** ，即计算操作次数。*
3.  如果 **i** 为**奇数**且 1 到 I 的元素之和为**正**，则从**a【I】**中减去 **(1+|sum|)** 使其为**负**。现在从 1 到 I 的元素之和将是 **-1。**还在 *num_of_ops 中增加 **(1+|sum|)** 。即计算操作的次数。*
4.  同样，求偶 I，元素之和直到 I 为负，奇 I，元素之和直到 I 为正的运算次数。
5.  从以上两个程序中选择最小操作数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find minimum number
// of operations to get desired array
int minOperations(int a[], int N)
{
    int num_of_ops1, num_of_ops2, sum;
    num_of_ops1 = num_of_ops2 = sum = 0;

    // For even 'i', sum of
    // elements till 'i' is negative

    // For odd 'i', sum of
    // elements till 'i' is positive
    for (int i = 0; i < N; i++) {
        sum += a[i];

        // If i is even and sum is positive,
        // make it negative by subtracting
        // 1 + |s| from a[i]
        if (i % 2 == 0 && sum >= 0) {
            num_of_ops1 += (1 + abs(sum));
            sum = -1;
        }

        // If i is odd and sum is negative,
        // make it positive by
        // adding 1 + |s| into a[i]
        else if (i % 2 == 1 && sum <= 0) {
            num_of_ops1 += (1 + abs(sum));
            sum = 1;
        }
    }

    sum = 0;

    // For even 'i', the sum of
    // elements till 'i' is positive

    // For odd 'i', sum of
    // elements till 'i' is negative
    for (int i = 0; i < N; i++) {
        sum += a[i];

        // Check if 'i' is odd and sum is
        // positive, make it negative by
        // subtracting  1 + |s| from a[i]
        if (i % 2 == 1 && sum >= 0) {
            num_of_ops2 += (1 + abs(sum));
            sum = -1;
        }

        // Check if 'i' is even and sum
        // is negative, make it positive
        // by adding 1 + |s| into a[i]
        else if (i % 2 == 0 && sum <= 0) {
            num_of_ops2 += (1 + abs(sum));
            sum = 1;
        }
    }

    // Return the minimum of the two
    return min(num_of_ops1, num_of_ops2);
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 3, -4, 5, 0, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << minOperations(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find minimum number
// of operations to get desired array
static int minOperations(int a[], int N)
{
    int num_of_ops1, num_of_ops2, sum;
    num_of_ops1 = num_of_ops2 = sum = 0;

    // For even 'i', sum of
    // elements till 'i' is negative

    // For odd 'i', sum of
    // elements till 'i' is positive
    for (int i = 0; i < N; i++)
    {
        sum += a[i];

        // If i is even and sum is positive,
        // make it negative by subtracting
        // 1 + |s| from a[i]
        if (i % 2 == 0 && sum >= 0)
        {
            num_of_ops1 += (1 + Math.abs(sum));
            sum = -1;
        }

        // If i is odd and sum is negative,
        // make it positive by
        // adding 1 + |s| into a[i]
        else if (i % 2 == 1 && sum <= 0)
        {
            num_of_ops1 += (1 + Math.abs(sum));
            sum = 1;
        }
    }

    sum = 0;

    // For even 'i', the sum of
    // elements till 'i' is positive

    // For odd 'i', sum of
    // elements till 'i' is negative
    for (int i = 0; i < N; i++)
    {
        sum += a[i];

        // Check if 'i' is odd and sum is
        // positive, make it negative by
        // subtracting  1 + |s| from a[i]
        if (i % 2 == 1 && sum >= 0)
        {
            num_of_ops2 += (1 + Math.abs(sum));
            sum = -1;
        }

        // Check if 'i' is even and sum
        // is negative, make it positive
        // by adding 1 + |s| into a[i]
        else if (i % 2 == 0 && sum <= 0)
        {
            num_of_ops2 += (1 + Math.abs(sum));
            sum = 1;
        }
    }

    // Return the minimum of the two
    return Math.min(num_of_ops1, num_of_ops2);
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int arr[] = { 3, -4, 5, 0, 1 };
    int N = arr.length;

    // Function Call
    System.out.print(minOperations(arr, N));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find minimum number
# of operations to get desired array
def minOperations(a, N):

    num_of_ops1 = num_of_ops2 = sum = 0;

    # For even 'i', sum of
    # elements till 'i' is negative

    # For odd 'i', sum of
    # elements till 'i' is positive
    for i in range(N):
        sum += a[i]

        # If i is even and sum is positive,
        # make it negative by subtracting
        # 1 + |s| from a[i]
        if (i % 2 == 0 and sum >= 0):
            num_of_ops1 += (1 + abs(sum))
            sum = -1

        # If i is odd and sum is negative,
        # make it positive by
        # adding 1 + |s| into a[i]
        elif (i % 2 == 1 and sum <= 0):
            num_of_ops1 += (1 + abs(sum))
            sum = 1

    sum = 0

    # For even 'i', the sum of
    # elements till 'i' is positive

    # For odd 'i', sum of
    # elements till 'i' is negative
    for i in range (N):
        sum += a[i]

        # Check if 'i' is odd and sum is
        # positive, make it negative by
        # subtracting 1 + |s| from a[i]
        if (i % 2 == 1 and sum >= 0):
            num_of_ops2 += (1 + abs(sum))
            sum = -1

        # Check if 'i' is even and sum
        # is negative, make it positive
        # by adding 1 + |s| into a[i]
        elif (i % 2 == 0 and sum <= 0):
            num_of_ops2 += (1 + abs(sum))
            sum = 1

    # Return the minimum of the two
    return min(num_of_ops1, num_of_ops2)

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [ 3, -4, 5, 0, 1 ]
    N = len(arr)

    # Function call
    print(minOperations(arr, N))

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find minimum number
// of operations to get desired array
static int minOperations(int []a, int N)
{
    int num_of_ops1, num_of_ops2, sum;
    num_of_ops1 = num_of_ops2 = sum = 0;

    // For even 'i', sum of
    // elements till 'i' is negative

    // For odd 'i', sum of
    // elements till 'i' is positive
    for(int i = 0; i < N; i++)
    {
        sum += a[i];

        // If i is even and sum is positive,
        // make it negative by subtracting
        // 1 + |s| from a[i]
        if (i % 2 == 0 && sum >= 0)
        {
            num_of_ops1 += (1 + Math.Abs(sum));
            sum = -1;
        }

        // If i is odd and sum is negative,
        // make it positive by
        // adding 1 + |s| into a[i]
        else if (i % 2 == 1 && sum <= 0)
        {
            num_of_ops1 += (1 + Math.Abs(sum));
            sum = 1;
        }
    }

    sum = 0;

    // For even 'i', the sum of
    // elements till 'i' is positive

    // For odd 'i', sum of
    // elements till 'i' is negative
    for(int i = 0; i < N; i++)
    {
        sum += a[i];

        // Check if 'i' is odd and sum is
        // positive, make it negative by
        // subtracting 1 + |s| from a[i]
        if (i % 2 == 1 && sum >= 0)
        {
            num_of_ops2 += (1 + Math.Abs(sum));
            sum = -1;
        }

        // Check if 'i' is even and sum
        // is negative, make it positive
        // by adding 1 + |s| into a[i]
        else if (i % 2 == 0 && sum <= 0)
        {
            num_of_ops2 += (1 + Math.Abs(sum));
            sum = 1;
        }
    }

    // Return the minimum of the two
    return Math.Min(num_of_ops1, num_of_ops2);
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 3, -4, 5, 0, 1 };
    int N = arr.Length;

    // Function call
    Console.Write(minOperations(arr, N));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find minimum number
// of operations to get desired array
function minOperations(a, N)
{
    var num_of_ops1, num_of_ops2, sum;
    num_of_ops1 = num_of_ops2 = sum = 0;

    // For even 'i', sum of
    // elements till 'i' is negative

    // For odd 'i', sum of
    // elements till 'i' is positive
    for(i = 0; i < N; i++)
    {
        sum += a[i];

        // If i is even and sum is positive,
        // make it negative by subtracting
        // 1 + |s| from a[i]
        if (i % 2 == 0 && sum >= 0)
        {
            num_of_ops1 += (1 + Math.abs(sum));
            sum = -1;
        }

        // If i is odd and sum is negative,
        // make it positive by
        // adding 1 + |s| into a[i]
        else if (i % 2 == 1 && sum <= 0)
        {
            num_of_ops1 += (1 + Math.abs(sum));
            sum = 1;
        }
    }

    sum = 0;

    // For even 'i', the sum of
    // elements till 'i' is positive

    // For odd 'i', sum of
    // elements till 'i' is negative
    for(i = 0; i < N; i++)
    {
        sum += a[i];

        // Check if 'i' is odd and sum is
        // positive, make it negative by
        // subtracting 1 + |s| from a[i]
        if (i % 2 == 1 && sum >= 0)
        {
            num_of_ops2 += (1 + Math.abs(sum));
            sum = -1;
        }

        // Check if 'i' is even and sum
        // is negative, make it positive
        // by adding 1 + |s| into a[i]
        else if (i % 2 == 0 && sum <= 0)
        {
            num_of_ops2 += (1 + Math.abs(sum));
            sum = 1;
        }
    }

    // Return the minimum of the two
    return Math.min(num_of_ops1, num_of_ops2);
}

// Driver Code

// Given array arr
var arr = [ 3, -4, 5, 0, 1 ];
var N = arr.length;

// Function Call
document.write(minOperations(arr, N));

// This code is contributed by aashish1995

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)