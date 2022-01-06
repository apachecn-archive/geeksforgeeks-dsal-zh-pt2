# 给定数组的最大子序列和，该数组是一个完美的正方形

> 原文:[https://www . geeksforgeeks . org/给定数组的最大子序列和是完美平方/](https://www.geeksforgeeks.org/maximum-subsequence-sum-from-a-given-array-which-is-a-perfect-square/)

给定一个数组 **arr[]** ，任务是找到一个**子序列**的**和**，形成一个**完美正方形**。如果有多个子序列的和等于一个完美平方，打印**最大值**和。
**说明:**

> **输入:** arr[] = {1，2，3，4，5，6，7，8，9}
> **输出:** 36
> **解释:**
> 可以从数组中获得的完美平方的最大可能和是从子序列{1，5，6，7，8，9}中获得的 36。
> **输入:** arr[] = {9，10}
> **输出:** 9

**天真方法:**生成给定数组的所有可能子序列[，对于每个子序列，检查其和是否为**完美平方**。如果找到这样的总和，更新**最大总和**。最后，打印得到的最大和。
***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N)*](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/) 

**高效方法:**
上述方法可以通过 [**动态规划**](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/) 方法进行优化。
按照以下步骤操作:

*   计算数组的**和**。
*   在范围[√和，0]内迭代 **k** ，并检查是否存在具有该和的子序列 **k <sup>2</sup>** 。对于每一个 **k** ，遵循以下步骤:
    *   初始化维度 **N *和**的布尔矩阵**子集[][]** ，其中**和**表示**k<sup>2</sup>T9】的当前值。**
    *   **子集【I】【j】**表示具有和 **j** 的大小 **i** 的子序列是否存在。
    *   将第一列和第一行分别初始化为**子集[][]** 的真和假。
    *   运行两个嵌套循环，从范围**【1，N】**中的 **i** 外部和范围**【1，求和】**中的 **j** 内部，根据以下条件以自下而上[的方式填充子集[][]矩阵:](https://www.geeksforgeeks.org/difference-between-bottom-up-model-and-top-down-model/)
        *   如果(j < arr[I–1])，则子集[i][j] =子集[I–1][j]
        *   如果(j > = arr[I–1])，则子集[i][j] =子集[I–1][j]| |子集[I–1][j–arr[I–1]]
    *   最后，返回**子集【n】【和】**。
*   子集[n][k]为真的第一个 **k** 给出了所需的最大可能子序列和 **k <sup>2</sup>** 。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;
bool isSubsetSum(int arr[], int n, int sum)
{
    bool subset[n + 1][sum + 1];

    // If sum is 0, then answer is true
    for (int i = 0; i <= n; i++)
        subset[i][0] = true;

    // If sum is not 0 and arr[] is empty,
    // then answer is false
    for (int i = 1; i <= sum; i++)
        subset[0][i] = false;

    // Fill the subset table in bottom up manner
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= sum; j++) {

            if (j < arr[i - 1])
                subset[i][j] = subset[i - 1][j];

            if (j >= arr[i - 1])
                subset[i][j]
                    = subset[i - 1][j]
                      || subset[i - 1][j - arr[i - 1]];
        }
    }

    return subset[n][sum];
}
// Function to find the sum
int findSum(int* arr, int n)
{
    int sum = 0;
    // Find sum of all values
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }

    int val = sqrt(sum);

    for (int i = val; i >= 0; i--) {
        if (isSubsetSum(arr, n, i * i)) {
            // return the value;
            return i * i;
        }
    }

    return 0;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findSum(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static boolean isSubsetSum(int arr[],
                           int n, int sum)
{
    boolean[][] subset = new boolean[n + 1][sum + 1];

    // If sum is 0, then answer is true
    for(int i = 0; i <= n; i++)
        subset[i][0] = true;

    // If sum is not 0 and arr[] is empty,
    // then answer is false
    for(int i = 1; i <= sum; i++)
        subset[0][i] = false;

    // Fill the subset table in bottom up manner
    for(int i = 1; i <= n; i++)
    {
        for(int j = 1; j <= sum; j++)
        {
            if (j < arr[i - 1])
                subset[i][j] = subset[i - 1][j];

            if (j >= arr[i - 1])
                subset[i][j] = subset[i - 1][j] ||
                subset[i - 1][j - arr[i - 1]];
        }
    }
    return subset[n][sum];
}

// Function to find the sum
static int findSum(int[] arr, int n)
{
    int sum = 0;

    // Find sum of all values
    for(int i = 0; i < n; i++)
    {
        sum += arr[i];
    }

    int val = (int)Math.sqrt(sum);

    for(int i = val; i >= 0; i--)
    {
        if (isSubsetSum(arr, n, i * i))
        {

            // return the value;
            return i * i;
        }
    }
    return 0;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    int n = arr.length;

    System.out.println(findSum(arr, n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import math

def isSubsetSum(arr, n, sum):

    subset = [ [ True for x in range(sum + 1) ]
                      for y in range(n + 1) ]

    # If sum is 0, then answer is true
    for i in range(n + 1):
        subset[i][0] = True

    # If sum is not 0 and arr[] is empty,
    # then answer is false
    for i in range(1, sum + 1):
        subset[0][i] = False

    # Fill the subset table in bottom up manner
    for i in range(1, n + 1):
        for j in range(1, sum + 1):

            if (j < arr[i - 1]):
                subset[i][j] = subset[i - 1][j]

            if (j >= arr[i - 1]):
                subset[i][j] = (subset[i - 1][j] or
                                subset[i - 1][j -
                                   arr[i - 1]])

    return subset[n][sum]

# Function to find the sum
def findSum(arr, n):

    sum = 0

    # Find sum of all values
    for i in range(n):
        sum += arr[i]

    val = int(math.sqrt(sum))

    for i in range(val, -1, -1):
        if (isSubsetSum(arr, n, i * i)):

            # Return the value;
            return i * i

    return 0

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 3, 4, 5, 6, 7, 8, 9]
    n = len(arr)

    print(findSum(arr, n))

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

static bool isSubsetSum(int []arr,
                        int n, int sum)
{
    bool[,] subset = new bool[n + 1, sum + 1];

    // If sum is 0, then answer is true
    for(int i = 0; i <= n; i++)
        subset[i, 0] = true;

    // If sum is not 0 and []arr is empty,
    // then answer is false
    for(int i = 1; i <= sum; i++)
        subset[0, i] = false;

    // Fill the subset table in bottom up manner
    for(int i = 1; i <= n; i++)
    {
        for(int j = 1; j <= sum; j++)
        {
            if (j < arr[i - 1])
                subset[i, j] = subset[i - 1, j];

            if (j >= arr[i - 1])
                subset[i, j] = subset[i - 1, j] ||
                subset[i - 1, j - arr[i - 1]];
        }
    }
    return subset[n, sum];
}

// Function to find the sum
static int findSum(int[] arr, int n)
{
    int sum = 0;

    // Find sum of all values
    for(int i = 0; i < n; i++)
    {
        sum += arr[i];
    }

    int val = (int)Math.Sqrt(sum);

    for(int i = val; i >= 0; i--)
    {
        if (isSubsetSum(arr, n, i * i))
        {

            // return the value;
            return i * i;
        }
    }
    return 0;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    int n = arr.Length;

    Console.WriteLine(findSum(arr, n));
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

function isSubsetSum(arr, n, sum)
{
    let subset = new Array(n + 1);
    for (var i = 0; i < subset.length; i++) {
    subset[i] = new Array(2);
    }

    // If sum is 0, then answer is true
    for(let i = 0; i <= n; i++)
        subset[i][0] = true;

    // If sum is not 0 and arr[] is empty,
    // then answer is false
    for(let i = 1; i <= sum; i++)
        subset[0][i] = false;

    // Fill the subset table in bottom up manner
    for(let i = 1; i <= n; i++)
    {
        for(let j = 1; j <= sum; j++)
        {
            if (j < arr[i - 1])
                subset[i][j] = subset[i - 1][j];

            if (j >= arr[i - 1])
                subset[i][j] = subset[i - 1][j] ||
                subset[i - 1][j - arr[i - 1]];
        }
    }
    return subset[n][sum];
}

// Function to find the sum
function findSum(arr, n)
{
    let sum = 0;

    // Find sum of all values
    for(let i = 0; i < n; i++)
    {
        sum += arr[i];
    }

    let val = Math.floor(Math.sqrt(sum));

    for(let i = val; i >= 0; i--)
    {
        if (isSubsetSum(arr, n, i * i))
        {

            // return the value;
            return i * i;
        }
    }
    return 0;
}

    // Driver Code

    let arr = [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ];
    let n = arr.length;

    document.write(findSum(arr, n));

</script>
```

**Output:** 

```
36
```

***时间复杂度:** O(N * SUM)*
***辅助空间:** O(N * SUM)*