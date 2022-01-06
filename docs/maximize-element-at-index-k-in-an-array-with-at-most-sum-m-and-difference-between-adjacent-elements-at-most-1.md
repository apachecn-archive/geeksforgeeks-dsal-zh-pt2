# 将数组中索引 K 处的元素最大化，数组中的元素之和最多为 M，相邻元素之差最多为 1

> 原文:[https://www . geeksforgeeks . org/index-k 数组中最大元素与相邻元素之和最多为 1/](https://www.geeksforgeeks.org/maximize-element-at-index-k-in-an-array-with-at-most-sum-m-and-difference-between-adjacent-elements-at-most-1/)

给定一个正整数 **N** ，任务是构造一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)，求索引 **K** 处的最大值，使得所有数组元素的[和最多为 **M** ，任意两个连续数组元素的绝对差最多为 **1** 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** N = 3，M = 7，K = 1
> **输出:** 3
> **解释:**
> 根据给定的约束，值为{2，3，2 }的数组在索引 1 处最大化值。因此，所需的输出为 3。
> 
> **输入:** N = 3，M = 8，K = 1
> T3】输出: 3

**方法:**思路是在指标 **K** 处达到最大值，其他元素之和减少，满足数组之和的标准为最多 **M** 。请遵循以下步骤:

*   让索引 **K** 处的值为 **X** 。所以**K–1**处的元素是**X–1**，在**K–2**处的元素是**X–2**等等。
*   在索引 **0** 处，该值为**X–K**。同样，在索引 **K + 1** 处，该值为**X–1**以此类推，直到索引**N–1**处的(N–K–1)。
*   因此，为了在索引 **K** 处获得最大值，数组结构将是**X–K，X –( K–1)，…。，X–2，X–1，X，X–1，X–2，…..，X –( N–K–1)**。
*   所以整理好方程后，就变成了**K * X –( 1+2+…。+K)+X+(N–K–1)* X –( 1+2+…。+(N–K–1))≤M**。

按照以下步骤求解上述方程:

*   计算 **(1 + 2 + …。+ K)** 使用 **K * (K + 1) / 2** 和 **(1 + 2 + …..+(N–K–1))**使用**(N–K–1)*(N–K)/2**并分别存放在 **S1** 和 **S2** 中。
*   这将方程式简化为**X *(K+1+N–K–1)≤M+S1+S2**。
*   现在 **X** 的最大值可以通过计算 **(M + S1 + S2) / N** 得到。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the maximum
// possible value at index K
void maxValueAtIndexK(int N, int K, int M)
{
    // Stores the sum of elements
    // in the left and right of index K
    int S1 = 0, S2 = 0;

    S1 = K * (K + 1) / 2;
    S2 = (N - K - 1) * (N - K) / 2;

    // Stores the maximum
    // possible value at index K
    int X = (M + S1 + S2) / N;

    // Print the answer
    cout << X;
}

// Driver Code
int main()
{
    // Given N, K & M
    int N = 3, K = 1, M = 7;
    maxValueAtIndexK(N, K, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to calculate the maximum
// possible value at index K
static void maxValueAtIndexK(int N, int K,
                             int M)
{

    // Stores the sum of elements
    // in the left and right of index K
    int S1 = 0, S2 = 0;

    S1 = K * (K + 1) / 2;
    S2 = (N - K - 1) * (N - K) / 2;

    // Stores the maximum
    // possible value at index K
    int X = (M + S1 + S2) / N;

    // Print the answer
    System.out.println(X);
}

// Driver Code
public static void main(String[] args)
{

    // Given N, K & M
    int N = 3, K = 1, M = 7;

    maxValueAtIndexK(N, K, M);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to calculate the maximum
# possible value at index K
def maxValueAtIndexK(N, K, M):

    # Stores the sum of elements
    # in the left and right of index K
    S1 = 0; S2 = 0;
    S1 = K * (K + 1) // 2;
    S2 = (N - K - 1) * (N - K) // 2;

    # Stores the maximum
    # possible value at index K
    X = (M + S1 + S2) // N;

    # Prthe answer
    print(X);

# Driver Code
if __name__ == '__main__':

    # Given N, K & M
    N = 3; K = 1; M = 7;
    maxValueAtIndexK(N, K, M);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate the maximum
// possible value at index K
static void maxValueAtIndexK(int N, int K,
                             int M)
{

    // Stores the sum of elements
    // in the left and right of index K
    int S1 = 0, S2 = 0;

    S1 = K * (K + 1) / 2;
    S2 = (N - K - 1) * (N - K) / 2;

    // Stores the maximum
    // possible value at index K
    int X = (M + S1 + S2) / N;

    // Print the answer
    Console.WriteLine(X);
}

// Driver Code
static public void Main()
{

    // Given N, K & M
    int N = 3, K = 1, M = 7;

    maxValueAtIndexK(N, K, M);
}
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>
// JavaScript program for
// the above approach

// Function to calculate the maximum
// possible value at index K
function maxValueAtIndexK(N, K, M)
{
    // Stores the sum of elements
    // in the left and right of index K
    let S1 = 0, S2 = 0;

    S1 = K * (K + 1) / 2;
    S2 = (N - K - 1) * (N - K) / 2;

    // Stores the maximum
    // possible value at index K
    let X = (M + S1 + S2) / N;

    // Print the answer
     document.write(X);
}

// Driver Code

    // Given N, K & M
    let N = 3, K = 1, M = 7;
    maxValueAtIndexK(N, K, M);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)