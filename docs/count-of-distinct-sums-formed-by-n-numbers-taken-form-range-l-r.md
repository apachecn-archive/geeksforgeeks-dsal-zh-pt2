# 从[L，R]

范围内取 N 个数形成的不同和的计数

> 原文:[https://www . geesforgeks . org/count-of-distinct-sum-by-n-numbers-take-form-range-l-r/](https://www.geeksforgeeks.org/count-of-distinct-sums-formed-by-n-numbers-taken-form-range-l-r/)

给定三个整数 **N** 、 **L** 和 **R** 。任务是从范围**【L，R】**中计算通过使用 **N** 个数字形成的不同和，其中任何数字都可以被取无限次。

**示例:**

> **输入:** N = 2，L = 1，R = 3
> **输出:** 5
> **解释:**从范围【1，3】
> { 1，1} = > sum = 2
> {1，2} = > sum = 3
> {1，3} = > sum = 4
> {2，2 } =>sum = 4> 3} = >和= 6
> 因此，有 5 种(2，3，4，5，6)可能的不同和，其中 2 个数字取自范围[1，3]。
> 
> **输入:** N = 3，L = 1，R = 9
> T3】输出: 10

**天真的方法:**解决给定问题的最简单方法是[从范围**【L，R】**和中生成所有可能的 **N** 数字的组合](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/)，然后计算这些组合形成的不同总和。

***时间复杂度:**O((R–L)<sup>N</sup>)*
***辅助空间:** O(1)*

**有效方法:****给定的问题可以通过一些观察和一些数学方法来解决。这里可以使用的最小和最大数字分别是 **L** 和 **R** 。所以，可以形成的最小和最大可能和分别是 **L*N** (所有 N 个数字都是 L)和 **R*N** (所有 N 个数字都是 R)，同样，也可以形成这个范围之间的所有其他和。按照以下步骤解决给定的问题。**

*   **初始化一个变量，比如 **minSum = L*N** ，来存储最小可能和。**
*   **初始化一个变量，比如 **maxSum = R*N** ，来存储最大可能的和。**
*   **最终答案是**【minSum，maxSum】**范围内的总数，即**(maxSum–minSum+1)**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find total number of
// different sums of N numbers in
// the range [L, R]
int countDistinctSums(int N, int L, int R)
{

    // To store minimum possible sum with
    // N numbers with all as L
    int minSum = L * N;

    // To store maximum possible sum with
    // N numbers with all as R
    int maxSum = R * N;

    // All other numbers in between maxSum
    // and minSum can also be formed so numbers
    // in this range is the final answer
    return maxSum - minSum + 1;
}

// Driver Code
int main()
{
    int N = 2, L = 1, R = 3;
    cout << countDistinctSums(N, L, R);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach

import java.util.*;

class GFG{

// Function to find total number of
// different sums of N numbers in
// the range [L, R]
static int countDistinctSums(int N, int L, int R)
{

    // To store minimum possible sum with
    // N numbers with all as L
    int minSum = L * N;

    // To store maximum possible sum with
    // N numbers with all as R
    int maxSum = R * N;

    // All other numbers in between maxSum
    // and minSum can also be formed so numbers
    // in this range is the final answer
    return maxSum - minSum + 1;
}

// Driver Code
public static void main(String[] args)
{
    int N = 2, L = 1, R = 3;
    System.out.print(countDistinctSums(N, L, R));

}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python program for the above approach

# Function to find total number of
# different sums of N numbers in
# the range [L, R]
def countDistinctSums(N, L, R):

    # To store minimum possible sum with
    # N numbers with all as L
    minSum = L * N

    # To store maximum possible sum with
    # N numbers with all as R
    maxSum = R * N

    # All other numbers in between maxSum
    # and minSum can also be formed so numbers
    # in this range is the final answer
    return maxSum - minSum + 1

# Driver Code
if __name__ == "__main__":
    N = 2
    L = 1
    R = 3
    print(countDistinctSums(N, L, R))

    # This code is contributed by rakeshsahni
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find total number of
// different sums of N numbers in
// the range [L, R]
static int countDistinctSums(int N, int L, int R)
{

    // To store minimum possible sum with
    // N numbers with all as L
    int minSum = L * N;

    // To store maximum possible sum with
    // N numbers with all as R
    int maxSum = R * N;

    // All other numbers in between maxSum
    // and minSum can also be formed so numbers
    // in this range is the final answer
    return maxSum - minSum + 1;
}

// Driver Code
public static void Main()
{
    int N = 2, L = 1, R = 3;
    Console.Write(countDistinctSums(N, L, R));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## **java 描述语言**

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find total number of
        // different sums of N numbers in
        // the range [L, R]
        function countDistinctSums(N, L, R) {

            // To store minimum possible sum with
            // N numbers with all as L
            let minSum = L * N;

            // To store maximum possible sum with
            // N numbers with all as R
            let maxSum = R * N;

            // All other numbers in between maxSum
            // and minSum can also be formed so numbers
            // in this range is the final answer
            return maxSum - minSum + 1;
        }

        // Driver Code

        let N = 2, L = 1, R = 3;
        document.write(countDistinctSums(N, L, R));

// This code is contributed by Potta Lokesh
    </script>
```

****Output:** 

```
5
```** 

*****时间复杂度:**O(1)*
T5**辅助空间:** O(1)**