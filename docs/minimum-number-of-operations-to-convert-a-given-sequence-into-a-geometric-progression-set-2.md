# 将给定序列转换为几何级数的最小运算次数|集合 2

> 原文:[https://www . geeksforgeeks . org/将给定序列转换为几何级数集的最小操作数-2/](https://www.geeksforgeeks.org/minimum-number-of-operations-to-convert-a-given-sequence-into-a-geometric-progression-set-2/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，可以对任意一个元素一次执行以下三个操作:

*   向元素中添加一个。
*   从元素中减去一。
*   保持元素不变。

任务是找到将其转换为[几何级数](https://www.geeksforgeeks.org/geometric-progression/)所需的最小成本，并找到[公比](https://en.wikipedia.org/wiki/Geometric_series)。
***注:**每次加减运算花费 1 个单位。*

**示例:**

> **输入:** N = 6，arr[] = {1，11，4，27，15，33}
> **输出:** 28 2
> **解释:**
> 对于 r = 1，arr[] = {1，4，11，15，27，33}
> 预期[] = {1，1，1，1，1，1}
> 成本[] = {0，3，10，14，26，32
> 
> 对于 r = 2，arr[] = {1，4，11，15，27，33}
> 预期[] = {1，2，4，8，16，32}
> 成本[] = {0，2，7，7，11，1}
> 总成本:∑成本= 28
> 对于 r = 3，arr[] = {1，4，11，15，27，33}
> 预期[] = {1，3，9，27，81
> 
> 最小成本= 28
> 公共比率= 2
> 
> **输入:** N = 7，arr[] = {1，2，4，8，9，6，7}
> **输出:** 30 1

**方法:**想法是在可能的公共比率范围内迭代，并检查所需的最小操作。按照以下步骤解决问题:

*   [排序数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   使用公式**Cell(arr[maximum _ element]/(N–1))**找到可能的常见比率范围。
*   计算所有可能的公共比率所需的运算次数。
*   找出任何常见比率所需的最小运算量。

下面是上述方法的实现:

## C++

```
// C++ program for above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum cost
void minCost(int arr[], int n)
{
    if (n == 1) {
        cout << 0 << endl;
        return;
    }

    // Sort the array
    sort(arr, arr + n);

    // Maximum possible common ratios
    float raised = 1 / float(n - 1);
    float temp = pow(arr[n - 1], raised);
    int r = round(temp) + 1;

    int i, j, min_cost = INT_MAX;
    int common_ratio = 1;

    // Iterate over all possible common ratios
    for (j = 1; j <= r; j++) {
        int curr_cost = 0, prod = 1;

        // Calculate operations required
        // for the current common ratio
        for (i = 0; i < n; i++) {

            curr_cost += abs(arr[i] - prod);
            prod *= j;
            if (curr_cost >= min_cost)
                break;
        }

        // Calculate minimum cost
        if (i == n) {
            min_cost = min(min_cost,
                           curr_cost);
            common_ratio = j;
        }
    }

    cout << min_cost << ' ';
    cout << common_ratio << ' ';
}

// Driver Code
int main()
{
    // Given N
    int N = 6;

    // Given arr[]
    int arr[] = { 1, 11, 4, 27, 15, 33 };

    // Function Calling
    minCost(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to find minimum cost
static void minCost(int arr[],
                    int n)
{
  if (n == 1)
  {
    System.out.print(0 + "\n");
    return;
  }

  // Sort the array
  Arrays.sort(arr);

  // Maximum possible common ratios
  float raised = 1 / (float)(n - 1);
  float temp = (float)Math.pow(arr[n - 1],
                               raised);
  int r = (int)(temp) + 1;

  int i, j, min_cost = Integer.MAX_VALUE;
  int common_ratio = 1;

  // Iterate over all possible
  // common ratios
  for (j = 1; j <= r; j++)
  {
    int curr_cost = 0, prod = 1;

    // Calculate operations required
    // for the current common ratio
    for (i = 0; i < n; i++)
    {
      curr_cost += Math.abs(arr[i] -
                            prod);
      prod *= j;
      if (curr_cost >= min_cost)
        break;
    }

    // Calculate minimum cost
    if (i == n)
    {
      min_cost = Math.min(min_cost,
                          curr_cost);
      common_ratio = j;
    }
  }

  System.out.print(min_cost + " ");
  System.out.print(common_ratio + " ");
}

// Driver Code
public static void main(String[] args)
{
  // Given N
  int N = 6;

  // Given arr[]
  int arr[] = {1, 11, 4,
               27, 15, 33};

  // Function Calling
  minCost(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for above approach
import sys

# Function to find minimum cost
def minCost(arr, n):

    if (n == 1):
        print(0)
        return

    # Sort the array
    arr = sorted(arr)

    # Maximum possible common ratios
    raised = 1 / (n - 1)
    temp = pow(arr[n - 1], raised)
    r = round(temp) + 1

    min_cost = sys.maxsize
    common_ratio = 1

    # Iterate over all possible
    # common ratios
    for j in range(1, r + 1):
        curr_cost = 0
        prod = 1

        # Calculate operations required
        # for the current common ratio
        i = 0
        while i < n:
            curr_cost += abs(arr[i] - prod)
            prod *= j

            if (curr_cost >= min_cost):
                break

            i += 1

        # Calculate minimum cost
        if (i == n):
            min_cost = min(min_cost,
                          curr_cost)
            common_ratio = j

    print(min_cost, common_ratio)

# Driver Code
if __name__ == '__main__':

    # Given N
    N = 6

    # Given arr[]
    arr = [ 1, 11, 4, 27, 15, 33 ]

    # Function calling
    minCost(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;

class GFG{

// Function to find minimum cost
static void minCost(int []arr,
                    int n)
{
  if (n == 1)
  {
    Console.Write(0 + "\n");
    return;
  }

  // Sort the array
  Array.Sort(arr);

  // Maximum possible common ratios
  float raised = 1 / (float)(n - 1);
  float temp = (float)Math.Pow(arr[n - 1],
                               raised);
  int r = (int)(temp) + 1;

  int i, j, min_cost = int.MaxValue;
  int common_ratio = 1;

  // Iterate over all possible
  // common ratios
  for (j = 1; j <= r; j++)
  {
    int curr_cost = 0, prod = 1;

    // Calculate operations required
    // for the current common ratio
    for (i = 0; i < n; i++)
    {
      curr_cost += Math.Abs(arr[i] -
                            prod);
      prod *= j;

      if (curr_cost >= min_cost)
        break;
    }

    // Calculate minimum cost
    if (i == n)
    {
      min_cost = Math.Min(min_cost,
                          curr_cost);
      common_ratio = j;
    }
  }

  Console.Write(min_cost + " ");
  Console.Write(common_ratio + " ");
}

// Driver Code
public static void Main(String[] args)
{

  // Given N
  int N = 6;

  // Given []arr
  int []arr = { 1, 11, 4,
                27, 15, 33 };

  // Function Calling
  minCost(arr, N);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Function to find minimum cost
function minCost(arr, n)
{
    if (n == 1) {
        document.write( 0 );
        return;
    }

    // Sort the array
    arr.sort((a,b) => a-b);

    // Maximum possible common ratios
    var raised = 1 / (n - 1);
    var temp = Math.pow(arr[n - 1], raised);
    var r = Math.round(temp) + 1;

    var i, j, min_cost = 1000000000;
    var common_ratio = 1;

    // Iterate over all possible common ratios
    for (j = 1; j <= r; j++) {
        var curr_cost = 0, prod = 1;

        // Calculate operations required
        // for the current common ratio
        for (i = 0; i < n; i++) {

            curr_cost += Math.abs(arr[i] - prod);
            prod *= j;
            if (curr_cost >= min_cost)
                break;
        }

        // Calculate minimum cost
        if (i == n) {
            min_cost = Math.min(min_cost,
                           curr_cost);
            common_ratio = j;
        }
    }

    document.write( min_cost + ' ');
    document.write( common_ratio + ' ');
}

// Driver Code

// Given N
var N = 6;

// Given arr[]
var arr = [1, 11, 4, 27, 15, 33];

// Function Calling
minCost(arr, N);

</script>
```

**Output:** 

```
28 2
```

***时间复杂度:** O(N * K)，其中 K 是最大可能公比。*
***辅助空间:** O(1)*