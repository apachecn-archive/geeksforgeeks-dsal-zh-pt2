# 用和 K 最大化数组中相邻元素的绝对差之和

> 原文:[https://www . geesforgeks . org/sum-k 数组中相邻元素的绝对差之和最大化/](https://www.geeksforgeeks.org/maximize-sum-of-absolute-difference-between-adjacent-elements-in-array-with-sum-k/)

给定两个**整数 N 和 K** ，任务是**最大化长度数组相邻元素间绝对差的和****N**和和 **K** 。
**举例:**

> **输入:** N = 5，K = 10
> **输出:** 20
> **说明:**
> 求和为 10 的数组 arr[]可以是{0，5，0，5，0}，最大化相邻元素的绝对差之和(5 + 5 + 5 + 5 = 20)
> **输入:** N = 2，K = 10
> **输出:** 10

**方法:**
要最大化相邻元素的总和，请按照以下步骤操作:

*   如果 **N** 为 2，则最大可能和为 **K** ，方法是将 **K** 放在 1 个索引中，将 **0** 放在另一个索引中。
*   如果 **N** 为 1，最大可能和将始终为 0。
*   对于 **N** 的所有其他值，答案将是 **2 * K** 。

> **图解:**
> 对于 **N = 3** ，排列 **{0，K，0}** 将相邻元素间的绝对差之和最大化为 **2 * K** 。
> 对于 **N = 4** ，排列 **{0，K/2，0，K/2}** 或 **{0，K，0，0}** 最大化相邻元素间绝对差的所需和为 **2 * K** 。

以下是上述方法的实现:

## C++

```
// C++ program to maximize the
// sum of absolute differences
// between adjacent elements
#include <bits/stdc++.h>
using namespace std;

// Function for maximizing the sum
int maxAdjacentDifference(int N, int K)
{
    // Difference is 0 when only
    // one element is present
    // in array
    if (N == 1) {
        return 0;
    }

    // Difference is K when
    // two elements are
    // present in array
    if (N == 2) {
        return K;
    }

    // Otherwise
    return 2 * K;
}

// Driver code
int main()
{

    int N = 6;
    int K = 11;

    cout << maxAdjacentDifference(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to maximize the
// sum of absolute differences
// between adjacent elements
import java.util.*;

class GFG{

// Function for maximising the sum
static int maxAdjacentDifference(int N, int K)
{

    // Difference is 0 when only
    // one element is present
    // in array
    if (N == 1)
    {
        return 0;
    }

    // Difference is K when
    // two elements are
    // present in array
    if (N == 2) 
    {
        return K;
    }

    // Otherwise
    return 2 * K;
}

// Driver code
public static void main(String[] args)
{
    int N = 6;
    int K = 11;

    System.out.print(maxAdjacentDifference(N, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to maximize the
# sum of absolute differences
# between adjacent elements

# Function for maximising the sum
def maxAdjacentDifference(N, K):

    # Difference is 0 when only
    # one element is present
    # in array
    if (N == 1):
        return 0;

    # Difference is K when
    # two elements are
    # present in array
    if (N == 2):
        return K;

    # Otherwise
    return 2 * K;

# Driver code
N = 6;
K = 11;
print(maxAdjacentDifference(N, K));

# This code is contributed by Code_Mech
```

## C#

```
// C# program to maximize the
// sum of absolute differences
// between adjacent elements
using System;

class GFG{

// Function for maximising the sum
static int maxAdjacentDifference(int N, int K)
{

    // Difference is 0 when only
    // one element is present
    // in array
    if (N == 1)
    {
        return 0;
    }

    // Difference is K when
    // two elements are
    // present in array
    if (N == 2) 
    {
        return K;
    }

    // Otherwise
    return 2 * K;
}

// Driver code
public static void Main(String[] args)
{
    int N = 6;
    int K = 11;

    Console.Write(maxAdjacentDifference(N, K));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to maximize the
// sum of absolute differences
// between adjacent elements

// Function for maximising the sum
function maxAdjacentDifference(N, K)
{

    // Difference is 0 when only
    // one element is present
    // in array
    if (N == 1)
    {
        return 0;
    }

    // Difference is K when
    // two elements are
    // present in array
    if (N == 2) 
    {
        return K;
    }

    // Otherwise
    return 2 * K;
}

// Driver Code

    let N = 6;
    let K = 11;

    document.write(maxAdjacentDifference(N, K));

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
22
```

***时间复杂度:** O(1)* 。