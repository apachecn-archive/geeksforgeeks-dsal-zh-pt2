# 对数组进行排序所需的最小增量或减量|自上而下的方法

> 原文:[https://www . geesforgeks . org/最小增量-或-减量-需要对数组进行排序-自上而下-方法/](https://www.geeksforgeeks.org/minimum-increment-or-decrement-required-to-sort-the-array-top-down-approach/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过执行最少数量的操作来按升序对数组进行排序。在单个操作中，数组的一个元素可以递增或递减 1。打印所需的最小操作数。
**示例:**

> **输入:** arr[] = {5，4，3，2，1}
> **输出:** 6
> **解释:**
> arr[]的排序数组为{3，3，3，3，3}
> 因此最小增量/减量为:
> 在索引 0，5–**3**= 2(减量 2)
> 在索引 1，4–**3**= 1(减量 1) 1 + 2 = **3** (增量 2)
> 总增量/减量为 2 + 1 + 1 + 2 = 6。
> **输入:** arr[] = {1，2，3，4}
> **输出:** 0
> **说明:**
> 数组已经排序。

**自下而上的方法:**这个问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。在[这篇](https://www.geeksforgeeks.org/minimum-increment-or-decrement-operations-required-to-make-the-array-sorted/)文章中讨论了一种[自下而上的方法](https://www.geeksforgeeks.org/tabulation-vs-memoization/)来解决这个问题。
**自上而下的方法:**这里我们就用[自上而下的动态规划](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)来解决这个问题。
让 2D 数组(比如 dp[i][j])用来存储 up 索引 **i** ，其中最后一个元素在索引 **j** 处。
以下是步骤:

1.  为了使用给定的操作来对数组元素进行排序，我们知道一个元素不能以递增或递减的方式大于数组的最大值而小于数组的最小值(比如 **m** )。
2.  因此，将一个元素(比如说 **X** )固定在**位置，那么 **(i-1)第**位置值(比如说 **Y** )可以在**【m，X】**范围内。**
3.  **对于**arr【】**的每个指标 **i** ，保持将小于或等于 **arr[i]** 的较小元素放置在 **(i-1)第**位置，并通过添加**ABS(arr[I]–Y)**计算最小增量或减量。**
4.  **因此，上述方法的递推关系可以写成:** 

> **dp[i][j] = min(dp[i][j]，ABS(arr[I]–Y)+recursive _ function(I-1，Y))
> 其中 m ≤ Y ≤ arr[j]。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Dp array to memoized
// the value recursive call
int dp[1000][1000];

// Function to find the minimum increment
// or decrement needed to make the array
// sorted
int minimumIncDec(int arr[], int N,
                  int maxE, int minE)
{
    // If only one element is present,
    // then arr[] is sorted
    if (N == 0) {
        return 0;
    }

    // If dp[N][maxE] is precalculated,
    // then return the result
    if (dp[N][maxE])
        return dp[N][maxE];

    int ans = INT_MAX;

    // Iterate from minE to maxE which
    // placed at previous index
    for (int k = minE; k <= maxE; k++) {

        // Update the answer according to
        // recurrence relation
        int x = minimumIncDec(arr, N - 1, k, minE);
        ans = min(ans,x + abs(arr[N - 1] - k));
    }

    // Memoized the value
    // for dp[N][maxE]
    dp[N][maxE] = ans;

    // Return the final result
    return dp[N][maxE];
}

// Driver Code
int main()
{
    int arr[] = { 5, 4, 3, 2, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Find the minimum and maximum
    // element from the arr[]
    int minE = *min_element(arr, arr + N);
    int maxE = *max_element(arr, arr + N);

    // Function Call
    cout << minimumIncDec(
        arr, N, maxE, minE);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program of the above approach
import java.util.*;

class GFG{

// Dp array to memoized
// the value recursive call
static int [][]dp = new int[1000][1000];

// Function to find the minimum increment
// or decrement needed to make the array
// sorted
static int minimumIncDec(int arr[], int N,
                         int maxE, int minE)
{

    // If only one element is present,
    // then arr[] is sorted
    if (N == 0)
    {
        return 0;
    }

    // If dp[N][maxE] is precalculated,
    // then return the result
    if (dp[N][maxE] != 0)
        return dp[N][maxE];

    int ans = Integer.MAX_VALUE;

    // Iterate from minE to maxE which
    // placed at previous index
    for(int k = minE; k <= maxE; k++)
    {

        // Update the answer according to
        // recurrence relation
        int x = minimumIncDec(arr, N - 1, k, minE);
        ans = Math.min(ans,
                       x + Math.abs(arr[N - 1] - k));
    }

    // Memoized the value
    // for dp[N][maxE]
    dp[N][maxE] = ans;

    // Return the final result
    return dp[N][maxE];
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, 4, 3, 2, 1 };
    int N = arr.length;

    // Find the minimum and maximum
    // element from the arr[]
    int minE = Arrays.stream(arr).min().getAsInt();
    int maxE = Arrays.stream(arr).max().getAsInt();

    // Function call
    System.out.print(minimumIncDec(
        arr, N, maxE, minE));
}
}

// This code is contributed by amal kumar choubey
```

## **蟒蛇 3**

```
# Python3 program of the above approach
import sys

# Dp array to memoized
# the value recursive call
dp = [[ 0 for x in range(1000)]
          for y in range(1000)]

# Function to find the minimum increment
# or decrement needed to make the array
# sorted
def minimumIncDec(arr, N, maxE, minE):

    # If only one element is present,
    # then arr[] is sorted
    if (N == 0):
        return 0

    # If dp[N][maxE] is precalculated,
    # then return the result
    if (dp[N][maxE]):
        return dp[N][maxE]

    ans = sys.maxsize

    # Iterate from minE to maxE which
    # placed at previous index
    for k in range(minE, maxE + 1):

        # Update the answer according to
        # recurrence relation
        x = minimumIncDec(arr, N - 1, k, minE)
        ans = min(ans, x + abs(arr[N - 1] - k))

    # Memoized the value
    # for dp[N][maxE]
    dp[N][maxE] = ans

    # Return the final result
    return dp[N][maxE]

# Driver Code
if __name__ == "__main__":

    arr = [ 5, 4, 3, 2, 1 ]
    N = len(arr)

    # Find the minimum and maximum
    # element from the arr[]
    minE = min(arr)
    maxE = max(arr)

    # Function Call
    print(minimumIncDec(arr, N, maxE, minE))

# This code is contributed by chitranayal
```

## **C#**

```
// C# program of the above approach
using System;
using System.Linq;

class GFG{

// Dp array to memoized
// the value recursive call
static int [,]dp = new int[1000, 1000];

// Function to find the minimum increment
// or decrement needed to make the array
// sorted
static int minimumIncDec(int []arr, int N,
                         int maxE, int minE)
{

    // If only one element is present,
    // then []arr is sorted
    if (N == 0)
    {
        return 0;
    }

    // If dp[N,maxE] is precalculated,
    // then return the result
    if (dp[N, maxE] != 0)
        return dp[N, maxE];

    int ans = int.MaxValue;

    // Iterate from minE to maxE which
    // placed at previous index
    for(int k = minE; k <= maxE; k++)
    {

        // Update the answer according to
        // recurrence relation
        int x = minimumIncDec(arr, N - 1, k, minE);
        ans = Math.Min(ans,
                       x + Math.Abs(arr[N - 1] - k));
    }

    // Memoized the value
    // for dp[N,maxE]
    dp[N, maxE] = ans;

    // Return the readonly result
    return dp[N,maxE];
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 5, 4, 3, 2, 1 };
    int N = arr.Length;

    // Find the minimum and maximum
    // element from the []arr
    int minE = arr.Min();
    int maxE = arr.Max();

    // Function call
    Console.Write(minimumIncDec(arr, N,
                                maxE, minE));
}
}

// This code is contributed by Rohit_ranjan
```

## **java 描述语言**

```
<script>

// JavaScript program of the above approach

// Dp array to memoized
// the value recursive call
let dp = new Array();

for(let i = 0; i < 1000; i++){
    let temp = [];
    for(let j = 0; j < 1000; j++){
        temp.push([])
    }
    dp.push(temp)
}

// Function to find the minimum increment
// or decrement needed to make the array
// sorted

function minimumIncDec(arr, N, maxE, minE)
{
    // If only one element is present,
    // then arr[] is sorted
    if (N == 0) {
        return 0;
    }
    // If dp[N][maxE] is precalculated,
    // then return the result
    if (!dp[N][maxE])
        return dp[N][maxE];

    let ans = Number.MAX_SAFE_INTEGER;

    // Iterate from minE to maxE which
    // placed at previous index
    for (let k = minE; k <= maxE; k++) {

        // Update the answer according to
        // recurrence relation
        let x = minimumIncDec(arr, N - 1, k, minE);
        ans = Math.min(ans,x + Math.abs(arr[N - 1] - k));
    }

    // Memoized the value
    // for dp[N][maxE]
    dp[N][maxE] = ans;

    // Return the final result
    return dp[N][maxE];
}

// Driver Code

    let arr = [ 5, 4, 3, 2, 1 ];
    let N = arr.length;

    // Find the minimum and maximum
    // element from the arr[]
    let minE = arr.sort((a, b) => a - b)[0];
    let maxE = arr.sort((a, b) => b - a)[0];

    // Function Call
    document.write(minimumIncDec(arr, N, maxE, minE));

// This code is contributed by _saurabh_jaiswal

</script>
```

****Output:** 

```
6
```** 

*****时间复杂度:** O(N*maxE)*
***辅助空间:** O(N <sup>2</sup> )***