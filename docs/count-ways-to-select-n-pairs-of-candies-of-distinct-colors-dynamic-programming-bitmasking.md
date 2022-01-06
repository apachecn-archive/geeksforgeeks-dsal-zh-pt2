# 计算选择 N 对不同颜色糖果的方法(动态编程+位屏蔽)

> 原文:[https://www . geesforgeks . org/count-way-to-select-n-pairs-of-distinct-colors-dynamic-programming-bit masking/](https://www.geeksforgeeks.org/count-ways-to-select-n-pairs-of-candies-of-distinct-colors-dynamic-programming-bitmasking/)

给定一个代表红蓝糖果数量的整数 **N** 和一个大小为 **N * N** 的矩阵**mat【】【】**，其中 **mat[i][j] = 1** 代表在**I<sup>th</sup>T11】红糖果和**j<sup>th</sup>T15】蓝糖果之间存在一对，任务是找出选择 **N** 对的方法数****

**示例:**

> **输入:** N = 2，mat[][] = { { 1，1 }，{ 1，1 } }
> **输出:** 2
> **解释:**
> 选择 N (= 2)对糖果的可能方式有{ (1，1)，(2，2) }，{ (1，2)，(2，1) } }。
> 因此，要求的输出为 2。
> 
> **输入:** N = 3，mat[][] = { { 0，1，1 }，{ 1，0，1 }，{ 1，1，1 } }
> **输出:** 3
> **说明:**
> 选择 N (= 3)对糖果的可能方式有:{ (1，2)、(2，1)、(3，3) }、{ (1，2)、(2，3)、(3)、(3，1) }、{ (1，3)、(2，1)、(2)、(3，2) }、{(1，3)、(2，1)}

**天真方法:**解决这个问题最简单的方法是[生成包含不同颜色的不同糖果的 **N** 对的所有可能排列](https://www.geeksforgeeks.org/heaps-algorithm-for-generating-permutations/)。最后，打印获得的计数。

下面是上述方法的实现:

## C++14

```
// C++14 program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count ways to select N distinct
// pairs of candies with different colours
int numOfWays(vector<vector<int>> a, int n,
                 int i, set<int> &blue)
{

    // If n pairs are selected
    if (i == n)
        return 1;

    // Stores count of ways
    // to select the i-th pair
    int count = 0;

    // Iterate over the range [0, n]
    for(int j = 0; j < n; j++)
    {

        // If pair (i, j) is not included
        if (a[i][j] == 1 && blue.find(j) == blue.end())
        {
            blue.insert(j);
            count += numOfWays(a, n, i + 1, blue);
            blue.erase(j);
        }
    }
    return count;
}

// Driver Code
int main()
{
    int n = 3;
    vector<vector<int>> mat = { { 0, 1, 1 },
                                { 1, 0, 1 },
                                { 1, 1, 1 } };
    set<int> mpp;

    cout << (numOfWays(mat, n, 0, mpp));
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to count ways to select N distinct
// pairs of candies with different colours
static int numOfWays(int a[][], int n, int i,
                     HashSet<Integer> blue)
{

    // If n pairs are selected
    if (i == n)
        return 1;

    // Stores count of ways
    // to select the i-th pair
    int count = 0;

    // Iterate over the range [0, n]
    for(int j = 0; j < n; j++)
    {

        // If pair (i, j) is not included
        if (a[i][j] == 1 && !blue.contains(j))
        {
            blue.add(j);
            count += numOfWays(a, n, i + 1, blue);
            blue.remove(j);
        }
    }
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int n = 3;
    int mat[][] = { { 0, 1, 1 },
                    { 1, 0, 1 },
                    { 1, 1, 1 } };
    HashSet<Integer> mpp = new HashSet<>();

    System.out.println((numOfWays(mat, n, 0, mpp)));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count ways to select N distinct
# pairs of candies with different colours
def numOfWays(a, n, i = 0, blue = []):

    # If n pairs are selected
    if i == n:
        return 1

    # Stores count of ways
    # to select the i-th pair
    count = 0

    # Iterate over the range [0, n]
    for j in range(n):

        # If pair (i, j) is not included
        if mat[i][j] == 1 and j not in blue:
            count += numOfWays(mat, n, i + 1,
                                blue + [j])

    return count

# Driver Code
if __name__ == "__main__":
    n = 3
    mat = [ [0, 1, 1],
            [1, 0, 1],
            [1, 1, 1] ]
    print(numOfWays(mat, n))
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count ways to select N distinct
// pairs of candies with different colours
static int numOfWays(int[,] a, int n, int i,
                     HashSet<int> blue)
{

    // If n pairs are selected
    if (i == n)
        return 1;

    // Stores count of ways
    // to select the i-th pair
    int count = 0;

    // Iterate over the range [0, n]
    for(int j = 0; j < n; j++)
    {

        // If pair (i, j) is not included
        if (a[i, j] == 1 && !blue.Contains(j))
        {
            blue.Add(j);
            count += numOfWays(a, n, i + 1, blue);
            blue.Remove(j);
        }
    }
    return count;
}

// Driver Code
public static void Main()
{
    int n = 3;
    int[,] mat = { { 0, 1, 1 },
                   { 1, 0, 1 },
                   { 1, 1, 1 } };
    HashSet<int> mpp = new HashSet<int>();

    Console.WriteLine((numOfWays(mat, n, 0, mpp)));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to count ways to select N distinct
// pairs of candies with different colours
function numOfWays(a, n, i, blue)
{

    // If n pairs are selected
    if (i == n)
        return 1;

    // Stores count of ways
    // to select the i-th pair
    let count = 0;

    // Iterate over the range [0, n]
    for(let j = 0; j < n; j++)
    {

        // If pair (i, j) is not included
        if (a[i][j] == 1 && !blue.has(j))
        {
            blue.add(j);
            count += numOfWays(a, n, i + 1, blue);
            blue.delete(j);
        }
    }
    return count;
}

// Driver Code

    let n = 3;
    let mat = [ [ 0, 1, 1 ],
                [ 1, 0, 1 ],
                [ 1, 1, 1 ] ];
    let mpp = new Set();

    document.write(numOfWays(mat, n, 0, mpp));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N！)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过位屏蔽针对[动态编程进行优化。对于每一颗红色糖果，不要生成所有排列的 **N** 蓝色糖果，而是使用**掩码**，其中**掩码**的 **j <sup>第</sup>位检查 **j <sup>第</sup>T17】蓝色糖果是否可用于选择当前对。
解决问题的递推关系如下:****](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)

> 如果掩码的第 K <sup>位</sup>未置位且 mat[I][K]= 1:
> DP[I+1][j |(1<<K)]+= DP[I][j]
> 
> 其中，(j | (1 << k)) marks the kth blue candy as selected.
> dp[i][j] =在 I 个红色糖果和 N 个蓝色糖果之间配对的方式计数，其中 j 是范围从 0 到 2 的 N 位数字的排列<sup>N</sup>–1)。

按照以下步骤解决问题:

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如说 **dp[][]** ，其中 **dp[i][j]** 存储 **i** 红色糖果和 **N** 蓝色糖果之间配对的方式数。 **j** 表示从 **0** 到 **2 <sup>N</sup> -1** 的位号排列。
*   使用上述递归关系并填充递归关系的所有可能的 dp 状态。
*   最后打印有 **N** 红色糖果和 **N** 蓝色糖果选择的 dp 状态，即**DP【I】【2】<sup>N</sup>-1】**。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to count ways to select N distinct
# pairs of candies with different colors
def numOfWays(a, n):

    # dp[i][j]: Stores count of ways to make
    # pairs between i red candies and N blue candies
    dp = [[0]*((1 << n)+1) for _ in range(n + 1)]

    # If there is no red and blue candy,
    # the count of ways to make n pairs is 1
    dp[0][0] = 1

    # i: Stores count of red candy
    for i in range(n):

        # j generates a permutation of blue
        # candy of selected / not selected
        # as a binary number with n bits
        for j in range(1 << n):

            if dp[i][j] == 0:
                continue

            # Iterate over the range [0, n]   
            for k in range(n):

                # Create a mask with only
                # the k-th bit as set
                mask = 1 << k

                # If Kth bit of mask is
                # unset  and mat[i][k] = 1
                if not(mask & j) and a[i][k]:
                    dp[i + 1][j | mask] += dp[i][j]

    # Return the dp states, where n red
    # and n blue candies are selected
    return dp[n][(1 << n)-1]

# Driver Code
if __name__ == "__main__":
    n = 3
    mat = [[0, 1, 1],
           [1, 0, 1],
           [1, 1, 1]]
    print(numOfWays(mat, n))
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>* 2<sup>N</sup>)*
***辅助空间:** O(N * 2 <sup>N</sup> )*