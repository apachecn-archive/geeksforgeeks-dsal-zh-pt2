# 一个数组中的最大和，每个元素恰好有一个相邻的元素

> 原文:[https://www . geeksforgeeks . org/max-sum-in-a-array-so-每个元素都有恰好一个与其相邻的元素/](https://www.geeksforgeeks.org/maximum-sum-in-an-array-such-that-every-element-has-exactly-one-adjacent-element-to-it/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，您可以选择一些索引，这样每个选定的索引都恰好有一个与其相邻的其他选定索引，并且选定索引处的元素之和应该最大。
换句话说，任务是从数组中选择元素，使得单个元素不被单独选择，三个连续索引处的元素不被选择，并且所选元素的总和应该最大。
任务是打印最大化总和。

**示例:**

> **输入:** arr[] = {1，2，3，1，4}
> **输出:**8
> arr[0]+arr[1]+arr[3]+arr[4]= 1+2+1+4 = 8
> **输入:** arr[] = {1，1，1，1}
> **输出:** 2

**方法:** [动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以用来解决这个问题。这个问题可以转化为选择相邻整数对，使得没有两对是相邻的或者有共同的元素
即如果 **(arr[i]，arr[i + 1])** 是我们选择的一对，那么既不能选择 **(arr[i + 2]，arr[i + 3])** 也不能选择 **(arr[i + 1，arr[i + 2])** 。
让我们根据上面的陈述来决定 dp 的状态。
对于每个索引 **i** ，我们将选择索引 **i** 和 **i + 1** ，即成对或不成对。如果我们配对，我们将无法选择索引 **i + 2** ，因为它将使 2 个元素与 **i + 1** 相邻。所以，接下来我们要为 **i + 3** 解决。如果不配对，就简单解为 **i + 1** 。
所以递推关系为。

> dp[i] = max（arr[i] + scar[i + 1] + dp[i + 3]， dp[i + 1]）

总共有 **N** 个状态，每个状态都需要 O(1)个时间求解。因此，时间复杂度将是 **O(N)** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define arrSize 51
using namespace std;

// To store the states of dp
int dp[arrSize];
bool v[arrSize];

// Function to return the maximized sum
int sumMax(int i, int arr[], int n)
{
    // Base case
    if (i >= n - 1)
        return 0;

    // Checks if a state is
    // already solved
    if (v[i])
        return dp[i];
    v[i] = true;

    // Recurrence relation
    dp[i] = max(arr[i] + arr[i + 1]
                    + sumMax(i + 3, arr, n),
                sumMax(i + 1, arr, n));

    // Return the result
    return dp[i];
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 1, 1 };
    int n = sizeof(arr) / sizeof(int);

    cout << sumMax(0, arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

static int arrSize = 51;

// To store the states of dp
static int dp[] = new int[arrSize];
static boolean v[] = new boolean[arrSize];

// Function to return the maximized sum
static int sumMax(int i, int arr[], int n)
{
    // Base case
    if (i >= n - 1)
        return 0;

    // Checks if a state is
    // already solved
    if (v[i])
        return dp[i];
    v[i] = true;

    // Recurrence relation
    dp[i] = Math.max(arr[i] + arr[i + 1]
                    + sumMax(i + 3, arr, n),
                sumMax(i + 1, arr, n));

    // Return the result
    return dp[i];
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 1, 1, 1 };
    int n = arr.length;

    System.out.println(sumMax(0, arr, n));
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
arrSize = 51

# To store the states of dp
dp = [0 for i in range(arrSize)]
v = [False for i in range(arrSize)]

# Function to return the maximized sum
def sumMax(i,arr,n):
    # Base case
    if (i >= n - 1):
        return 0

    # Checks if a state is
    # already solved
    if (v[i]):
        return dp[i]
    v[i] = True
    # Recurrence relation
    dp[i] = max(arr[i] + arr[i + 1] + sumMax(i + 3, arr, n),
                                        sumMax(i + 1, arr, n))
    # Return the result
    return dp[i]

# Driver code
if __name__ == '__main__':
    arr = [1, 1, 1, 1]
    n = len(arr)
    print(sumMax(0, arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int arrSize = 51;

// To store the states of dp
static int []dp = new int[arrSize];
static bool []v = new bool[arrSize];

// Function to return the maximized sum
static int sumMax(int i, int []arr, int n)
{
    // Base case
    if (i >= n - 1)
        return 0;

    // Checks if a state is
    // already solved
    if (v[i])
        return dp[i];
    v[i] = true;

    // Recurrence relation
    dp[i] = Math.Max(arr[i] + arr[i + 1]
                    + sumMax(i + 3, arr, n),
                sumMax(i + 1, arr, n));

    // Return the result
    return dp[i];
}

// Driver code
public static void Main ()
{
    int []arr = { 1, 1, 1, 1 };
    int n = arr.Length;

    Console.WriteLine(sumMax(0, arr, n));
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var arrSize = 51;

// To store the states of dp
var dp = Array(arrSize);
var v = Array(arrSize);

// Function to return the maximized sum
function sumMax(i, arr, n)
{
    // Base case
    if (i >= n - 1)
        return 0;

    // Checks if a state is
    // already solved
    if (v[i])
        return dp[i];
    v[i] = true;

    // Recurrence relation
    dp[i] = Math.max(arr[i] + arr[i + 1]
                    + sumMax(i + 3, arr, n),
                sumMax(i + 1, arr, n));

    // Return the result
    return dp[i];
}

// Driver code
var arr = [1, 1, 1, 1];
var n = arr.length;
document.write( sumMax(0, arr, n));

</script>
```

**Output:** 

```
2
```