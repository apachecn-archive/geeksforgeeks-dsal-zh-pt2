# 总和等于 X 的子集计数

> 原文:[https://www . geesforgeks . org/sum 等于 x 的子集计数/](https://www.geeksforgeeks.org/count-of-subsets-with-sum-equal-to-x/)

给定一个长度为 **N** 的数组**arr【】**和一个整数 **X** ，任务是找出和等于 **X** 的子集数。

**示例:**

> **输入:** arr[] = {1，2，3，3}，X = 6
> **输出:** 3
> 所有可能的子集为{1，2，3}、
> {1，2，3}和{3，3}
> 
> **输入:** arr[] = {1，1，1，1}，X = 1
> T3】输出: 4

**方法:**一个简单的方法是通过生成所有可能的子集，然后检查子集是否具有所需的和来解决这个问题。这种方法的时间复杂度是指数级的。但是对于较小的 **X** 和数组元素的值，这个问题可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来解决。
我们先来看看递归关系。

**该方法对所有整数都有效。**

> DP[I][c]= DP[I–1][c–arr[I]]+DP[I–1][c]

现在让我们了解一下 DP 的状态。这里， **dp[i][C]** 存储子阵列的子集数量 **arr[i…N-1]** ，使得它们的和等于 **C** 。
因此，递归非常简单，因为只有两个选择，即要么考虑子集中的 **i <sup>th</sup>** 元素，要么不考虑。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define maxN 20
#define maxSum 50
#define minSum 50
#define base 50

// To store the states of DP
int dp[maxN][maxSum + minSum];
bool v[maxN][maxSum + minSum];

// Function to return the required count
int findCnt(int* arr, int i, int required_sum, int n)
{
    // Base case
    if (i == n) {
        if (required_sum == 0)
            return 1;
        else
            return 0;
    }

    // If the state has been solved before
    // return the value of the state
    if (v[i][required_sum + base])
        return dp[i][required_sum + base];

    // Setting the state as solved
    v[i][required_sum + base] = 1;

    // Recurrence relation
    dp[i][required_sum + base]
        = findCnt(arr, i + 1, required_sum, n)
          + findCnt(arr, i + 1, required_sum - arr[i], n);
    return dp[i][required_sum + base];
}

// Driver code
int main()
{
    int arr[] = { 3, 3, 3, 3 };
    int n = sizeof(arr) / sizeof(int);
    int x = 6;

    cout << findCnt(arr, 0, x, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int maxN = 20;
static int maxSum = 50;
static int minSum = 50;
static int base = 50;

// To store the states of DP
static int [][]dp = new int[maxN][maxSum + minSum];
static boolean [][]v = new boolean[maxN][maxSum + minSum];

// Function to return the required count
static int findCnt(int []arr, int i,
                   int required_sum, int n)
{
    // Base case
    if (i == n)
    {
        if (required_sum == 0)
            return 1;
        else
            return 0;
    }

    // If the state has been solved before
    // return the value of the state
    if (v[i][required_sum + base])
        return dp[i][required_sum + base];

    // Setting the state as solved
    v[i][required_sum + base] = true;

    // Recurrence relation
    dp[i][required_sum + base] =
          findCnt(arr, i + 1, required_sum, n) +
          findCnt(arr, i + 1, required_sum - arr[i], n);
    return dp[i][required_sum + base];
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 3, 3, 3, 3 };
    int n = arr.length;
    int x = 6;

    System.out.println(findCnt(arr, 0, x, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np

maxN = 20
maxSum = 50
minSum = 50
base = 50

# To store the states of DP
dp = np.zeros((maxN, maxSum + minSum));
v = np.zeros((maxN, maxSum + minSum));

# Function to return the required count
def findCnt(arr, i, required_sum, n) :

    # Base case
    if (i == n) :
        if (required_sum == 0) :
            return 1;
        else :
            return 0;

    # If the state has been solved before
    # return the value of the state
    if (v[i][required_sum + base]) :
        return dp[i][required_sum + base];

    # Setting the state as solved
    v[i][required_sum + base] = 1;

    # Recurrence relation
    dp[i][required_sum + base] = findCnt(arr, i + 1,
                                         required_sum, n) + \
                                 findCnt(arr, i + 1,
                                         required_sum - arr[i], n);

    return dp[i][required_sum + base];

# Driver code
if __name__ == "__main__" :

    arr = [ 3, 3, 3, 3 ];
    n = len(arr);
    x = 6;

    print(findCnt(arr, 0, x, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int maxN = 20;
static int maxSum = 50;
static int minSum = 50;
static int Base = 50;

// To store the states of DP
static int [,]dp = new int[maxN, maxSum + minSum];
static Boolean [,]v = new Boolean[maxN, maxSum + minSum];

// Function to return the required count
static int findCnt(int []arr, int i,
                   int required_sum, int n)
{
    // Base case
    if (i == n)
    {
        if (required_sum == 0)
            return 1;
        else
            return 0;
    }

    // If the state has been solved before
    // return the value of the state
    if (v[i, required_sum + Base])
        return dp[i, required_sum + Base];

    // Setting the state as solved
    v[i, required_sum + Base] = true;

    // Recurrence relation
    dp[i, required_sum + Base] =
          findCnt(arr, i + 1, required_sum, n) +
          findCnt(arr, i + 1, required_sum - arr[i], n);
    return dp[i,required_sum + Base];
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 3, 3, 3, 3 };
    int n = arr.Length;
    int x = 6;

    Console.WriteLine(findCnt(arr, 0, x, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var maxN = 20
var maxSum = 50
var minSum = 50
var base = 50

// To store the states of DP
var dp = Array.from(Array(maxN),
()=>Array(maxSum+minSum));
var v = Array.from(Array(maxN),
()=>Array(maxSum+minSum));

// Function to return the required count
function findCnt(arr, i, required_sum, n)
{
    // Base case
    if (i == n) {
        if (required_sum == 0)
            return 1;
        else
            return 0;
    }

    // If the state has been solved before
    // return the value of the state
    if (v[i][required_sum + base])
        return dp[i][required_sum + base];

    // Setting the state as solved
    v[i][required_sum + base] = 1;

    // Recurrence relation
    dp[i][required_sum + base]
        = findCnt(arr, i + 1,
          required_sum, n)
          + findCnt(arr, i + 1,
          required_sum - arr[i], n);
    return dp[i][required_sum + base];
}

// Driver code
var arr = [3, 3, 3, 3];
var n = arr.length;
var x = 6;
document.write( findCnt(arr, 0, x, n));

</script>
```

**Output**

```
6
```

#### **方法二:采用制表法:**

```
This method is valid only for those arrays which contains positive elements.
In this method we use a 2D array of size (arr.size() + 1) * (target + 1) of type integer.
Initialization of Matrix:
mat[0][0] = 1 because If the size of sum is 
```

```
if (A[i] > j)
DP[i][j] = DP[i-1][j]
else 
DP[i][j] = DP[i-1][j] + DP[i-1][j-A[i]]
```

这意味着，如果当前元素的值大于“当前总和值”，我们将复制以前案例的答案

如果当前的和值大于“ith”元素，我们将看到是否有任何先前的状态已经经历了和=“j ”,以及是否有任何先前的状态经历了值“j–A[I ],这将解决我们的目的

## C++

```
#include <bits/stdc++.h>
using namespace std;

int subsetSum(int a[], int n, int sum)
{
    // Initializing the matrix
    int tab[n + 1][sum + 1];
  // Initializing the first value of matrix
    tab[0][0] = 1;
    for (int i = 1; i <= sum; i++)
        tab[0][i] = 0;
    for (int i = 1; i <= n; i++)
        tab[i][0] = 1;

    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= sum; j++)
        {
          // if the value is greater than the sum
            if (a[i - 1] > j)
                tab[i][j] = tab[i - 1][j];
            else
            {
                tab[i][j] = tab[i - 1][j] + tab[i - 1][j - a[i - 1]];
            }
        }
    }

    return tab[n][sum];
}

int main()
{
    int n = 4;
    int a[] = {3,3,3,3};
    int sum = 6;

    cout << (subsetSum(a, n, sum));
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

static int subsetSum(int a[], int n, int sum)
{

    // Initializing the matrix
    int tab[][] = new int[n + 1][sum + 1];

    // Initializing the first value of matrix
    tab[0][0] = 1;

    for(int i = 1; i <= sum; i++)
        tab[0][i] = 0;

    for(int i = 1; i <= n; i++)
        tab[i][0] = 1;

    for(int i = 1; i <= n; i++)
    {
        for(int j = 1; j <= sum; j++)
        {

            // If the value is greater than the sum
            if (a[i - 1] > j)
                tab[i][j] = tab[i - 1][j];

            else
            {
                tab[i][j] = tab[i - 1][j] +
                            tab[i - 1][j - a[i - 1]];
            }
        }
    }

    return tab[n][sum];
}

// Driver Code
public static void main(String[] args)
{
    int n = 4;
    int a[] = { 3, 3, 3, 3 };
    int sum = 6;

    System.out.print(subsetSum(a, n, sum));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
def subset_sum(a: list, n: int, sum: int):

    # Initializing the matrix
    tab = [[0] * (sum + 1) for i in range(n + 1)]
    for i in range(1, sum + 1):
        tab[0][i] = 0
    for i in range(n+1):

        # Initializing the first value of matrix
        tab[i][0] = 1
    for i in range(1, n+1):
        for j in range(1, sum + 1):
            if a[i-1] <= j:
                tab[i][j] = tab[i-1][j] + tab[i-1][j-a[i-1]]
            else:
                tab[i][j] = tab[i-1][j]
    return tab[n][sum]

if __name__ == '__main__':
    a = [3, 3, 3, 3]
    n = 4
    sum = 6
    print(subset_sum(a, n, sum))

    # This code is contributed by Premansh2001.
```

## C#

```
using System;

class GFG{

static int subsetSum(int []a, int n, int sum)
{

    // Initializing the matrix
    int [,]tab = new int[n + 1, sum + 1];

    // Initializing the first value of matrix
    tab[0, 0] = 1;

    for(int i = 1; i <= sum; i++)
        tab[0, i] = 0;

    for(int i = 1; i <= n; i++)
        tab[i, 0] = 1;

    for(int i = 1; i <= n; i++)
    {
        for(int j = 1; j <= sum; j++)
        {

            // If the value is greater than the sum
            if (a[i - 1] > j)
                tab[i, j] = tab[i - 1, j];
            else
            {
                tab[i, j] = tab[i - 1, j] +
                            tab[i - 1, j - a[i - 1]];
            }
        }
    }
    return tab[n, sum];
}

// Driver Code
public static void Main(String[] args)
{
    int n = 4;
    int []a = { 3, 3, 3, 3 };
    int sum = 6;

    Console.Write(subsetSum(a, n, sum));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

function subsetSum( a,  n, sum)
{
    // Initializing the matrix
    var tab = new Array(n + 1);
    for (let i = 0; i< n+1; i++)
      tab[i] = new Array(sum + 1);
  // Initializing the first value of matrix
    tab[0][0] = 1;
    for (let i = 1; i <= sum; i++)
        tab[0][i] = 0;
    for (let i = 1; i <= n; i++)
        tab[i][0] = 1;

    for (let i = 1; i <= n; i++)
    {
        for (let j = 1; j <= sum; j++)
        {
          // if the value is greater than the sum
            if (a[i - 1] > j)
                tab[i][j] = tab[i - 1][j];
            else
            {
                tab[i][j] = tab[i - 1][j] + tab[i - 1][j - a[i - 1]];
            }
        }
    }

    return tab[n][sum];
}

var n = 4;
var a = new Array(3,3,3,3);
var sum = 6;

console.log(subsetSum(a, n, sum));

// This code is contributed by ukasp.
</script>
```

**Output**

```
6
```

**时间复杂度:** O(和*n)，其中和为‘目标和’，n 为数组大小。

**辅助空间:** O(和*n)，作为二维数组的大小，是和*n。