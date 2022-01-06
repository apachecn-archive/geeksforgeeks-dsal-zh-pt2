# 选择阵列元素的最小成本

> 原文:[https://www . geeksforgeeks . org/选择数组元素的最小成本/](https://www.geeksforgeeks.org/minimum-cost-of-choosing-the-array-element/)

给定一个由 **N** 个整数和一个整数 **M** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，在任何一天(比如 **d** )选择任意数组元素(比如 **x** )的成本为 **x*d** 。任务是最小化选择 1，2，3，…，N 阵列的成本，每天最多允许选择 M 个元素。
**举例:**

> **输入:** arr[] = {6，19，3，4，4，2，6，7，8}，M = 2
> **输出:** 2 5 11 18 30 43 62 83 121
> **解释:**
> 选择 1，2，3，..，每天最多允许选择 2 个元素时的 N 个元素:
> 选择 1 个元素的成本:
> 第 1 天选择一个最小元素，则成本为 2*1 = 2
> 选择 2 个元素的成本:
> 第 1 天选择两个最小元素，则成本为(2+3)*1 = 5
> 选择 3 个元素的成本:
> 第 1 天选择第 2 个和第 3 个最小元素， 那么成本为(3+4)*1 = 7
> 在第 2 天选择第 1 个最小元素，那么成本为 2*2 = 4
> 那么，总成本为 7 + 4 = 11
> 同样，我们可以发现选择 4、5、6、7、8 和 9 个元素的成本分别为 18、30、43、62、83 和 121。
> **输入:** arr[] = {6，19，12，6，7，9}，M = 3
> **输出:** 6 12 19 34 52 78

**方法:**思路是使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。

1.  按递增顺序对给定数组进行排序。
2.  将排序数组的前缀和存储在 **pref[]** 中。当允许每天选择一个元素时，该前缀和给出了选择 **1、2、3、… N** 阵列元素的最小成本。
3.  要找到允许 atmat**M**元素每天选择时的最小成本，请将前缀数组 **pref[]** 从索引 **M 更新为 N** 为:

```
pref[i] = pref[i] + pref[i-M]
```

1.  例如:

```
arr[] = {6, 9, 3, 4, 4, 2, 6, 7, 8}
After sorting arr[]:
arr[] = {2, 3, 4, 4, 6, 6, 7, 8, 9}

Prefix array is:
pref[] = {2, 5, 9, 13, 19, 25, 32, 40, 49}
Now at every index i, pref[i] gives the cost 
of selecting i array element when atmost one 
element is allowed to select each day.
```

```
Now for M = 3, when at most 3 elements
are allowed to select each day, then 
by update every index(from M to N)
of pref[] as:
pref[i] = pref[i] + pref[i-M] 

the cost of selecting elements 
from (i-M+1)th to ith index on day 1,
the cost of selecting elements 
from (i-M)th to (i-2*M)th index on day 2
...
...
...
the cost of selecting elements 
from (i-n*M)th to 0th index on day N.
```

2.  在上述步骤之后，前缀数组**pref【】**的每个索引(比如 **i** )存储了当允许 atmat**M**元素每天选择时选择 I 元素的成本。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that find the minimum cost of
// selecting array element
void minimumCost(int arr[], int N, int M) {

    // Sorting the given array in
    // increasing order
    sort(arr, arr + N);

    // To store the prefix sum of arr[]
    int pref[N];

    pref[0] = arr[0];

    for(int i = 1; i < N; i++) {
        pref[i] = arr[i] + pref[i-1];
    }

    // Update the pref[] to find the cost
    // selecting array element by selecting
    // at most M element
    for(int i = M; i < N; i++) {
        pref[i] += pref[i-M];
    }

    // Print the pref[] for the result
    for(int i = 0; i < N; i++) {
        cout << pref[i] << ' ';
    }

}

// Driver Code
int main()
{
    int arr[] = {6, 19, 3, 4, 4, 2, 6, 7, 8};
    int M = 2;
    int N = sizeof(arr)/sizeof(arr[0]);

    minimumCost(arr, N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function that find the minimum cost of
// selecting array element
static void minimumCost(int arr[], int N, int M)
{

    // Sorting the given array in
    // increasing order
    Arrays.sort(arr);

    // To store the prefix sum of arr[]
    int []pref = new int[N];
    pref[0] = arr[0];

    for(int i = 1; i < N; i++)
    {
        pref[i] = arr[i] + pref[i - 1];
    }

    // Update the pref[] to find the cost
    // selecting array element by selecting
    // at most M element
    for(int i = M; i < N; i++)
    {
        pref[i] += pref[i - M];
    }

    // Print the pref[] for the result
    for(int i = 0; i < N; i++)
    {
        System.out.print(pref[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 6, 19, 3, 4, 4, 2, 6, 7, 8 };
    int M = 2;
    int N = arr.length;

    minimumCost(arr, N, M);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that find the minimum cost
# of selecting array element
def minimumCost(arr, N, M):

    # Sorting the given array in
    # increasing order
    arr.sort()

    # To store the prefix sum of arr[]
    pref = []

    pref.append(arr[0])

    for i in range(1, N):
        pref.append(arr[i] + pref[i - 1])

    # Update the pref[] to find the cost
    # selecting array element by selecting
    # at most M element
    for i in range(M, N):
        pref[i] += pref[i - M]

    # Print the pref[] for the result
    for i in range(N):
        print(pref[i], end = ' ')

# Driver Code
arr = [ 6, 19, 3, 4, 4, 2, 6, 7, 8 ]
M = 2
N = len(arr)

minimumCost(arr, N, M);

# This code is contributed by yatinagg
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that find the minimum cost 
// of selecting array element
static void minimumCost(int []arr, int N,
                                   int M)
{

    // Sorting the given array 
    // in increasing order
    Array.Sort(arr);

    // To store the prefix sum of []arr
    int []pref = new int[N];
    pref[0] = arr[0];

    for(int i = 1; i < N; i++)
    {
       pref[i] = arr[i] + pref[i - 1];
    }

    // Update the pref[] to find the cost
    // selecting array element by selecting
    // at most M element
    for(int i = M; i < N; i++)
    {
       pref[i] += pref[i - M];
    }

    // Print the pref[] for the result
    for(int i = 0; i < N; i++)
    {
       Console.Write(pref[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 6, 19, 3, 4, 4, 
                  2, 6, 7, 8 };
    int M = 2;
    int N = arr.Length;

    minimumCost(arr, N, M);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that find the minimum cost of
// selecting array element
function minimumCost(arr, N, M)
{

    // Sorting the given array in
    // increasing order
    arr.sort((a, b) => a - b);

    // To store the prefix sum of arr[]
    let pref = Array.from({length: N}, (_, i) => 0);
    pref[0] = arr[0];

    for(let i = 1; i < N; i++)
    {
        pref[i] = arr[i] + pref[i - 1];
    }

    // Update the pref[] to find the cost
    // selecting array element by selecting
    // at most M element
    for(let i = M; i < N; i++)
    {
        pref[i] += pref[i - M];
    }

    // Prlet the pref[] for the result
    for(let i = 0; i < N; i++)
    {
       document.write(pref[i] + " ");
    }
}

// Driver Code

    let arr = [ 6, 19, 3, 4, 4, 2, 6, 7, 8 ];
    let M = 2;
    let N = arr.length;

    minimumCost(arr, N, M);

</script>
```

**Output:** 

```
2 5 11 18 30 43 62 83 121
```

**时间复杂度:** O(N*log N)，其中 N 为数组中元素的个数。