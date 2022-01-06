# 使数组元素相等的最小增量/减量

> 原文:[https://www . geesforgeks . org/最小-增量-减量-使数组元素相等/](https://www.geeksforgeeks.org/minimum-increment-decrement-to-make-array-elements-equal/)

给定一个整数数组，其中![1 \leq A[i] \leq 10^{18} ](img/f42ec5ec711971455c7d35ba346286d8.png "Rendered by QuickLaTeX.com")。在一个操作中，您可以将任何元素递增/递减 1。任务是找到需要对数组元素执行的最小操作，以使所有数组元素相等。
**示例** :

```
Input : A[] = { 1, 5, 7, 10 }
Output : 11
Increment 1 by 4, 5 by 0.
Decrement 7 by 2, 10 by 5.
New array A = { 5, 5, 5, 5 } with 
cost of operations = 4 + 0 + 2 + 5 = 11.

Input : A = { 10, 2, 20 }
Output : 18
```

**进场:**

1.  按递增顺序对整数数组进行排序。
2.  现在，使所有元素与最小成本相等。我们必须使元素等于这个排序数组的中间元素。所以，选择中间值，让它是 K.
    **注**:如果元素是偶数，我们就要检查两个中间元素的成本，取最小值。
3.  如果 **A[i] < K** ，则增加**K–A[I]**元素。
4.  如果 **A[i] > K** ，则按**A[I]–K**递减元素。
5.  更新执行的每个操作的成本。

以下是上述方法的实现:

## C++

```
// C++ program to find minimum Increment or
// decrement to make array elements equal
#include <bits/stdc++.h>
using namespace std;

// Function to return minimum operations need
// to be make each element of array equal
int minCost(int A[], int n)
{
    // Initialize cost to 0
    int cost = 0;

    // Sort the array
    sort(A, A + n);

    // Middle element
    int K = A[n / 2];

    // Find Cost
    for (int i = 0; i < n; ++i)
        cost += abs(A[i] - K);

    // If n, is even. Take minimum of the
    // Cost obtained by considering both
    // middle elements
    if (n % 2 == 0) {
        int tempCost = 0;

        K = A[(n / 2) - 1];

        // Find cost again
        for (int i = 0; i < n; ++i)
            tempCost += abs(A[i] - K);

        // Take minimum of two cost
        cost = min(cost, tempCost);
    }

    // Return total cost
    return cost;
}

// Driver Code
int main()
{
    int A[] = { 1, 6, 7, 10 };

    int n = sizeof(A) / sizeof(A[0]);

    cout << minCost(A, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum Increment or
// decrement to make array elements equal
import java.util.*;
class GfG {

// Function to return minimum operations need
// to be make each element of array equal
static int minCost(int A[], int n)
{
    // Initialize cost to 0
    int cost = 0;

    // Sort the array
    Arrays.sort(A);

    // Middle element
    int K = A[n / 2];

    // Find Cost
    for (int i = 0; i < n; ++i)
        cost += Math.abs(A[i] - K);

    // If n, is even. Take minimum of the
    // Cost obtained by considering both
    // middle elements
    if (n % 2 == 0) {
        int tempCost = 0;

        K = A[(n / 2) - 1];

        // Find cost again
        for (int i = 0; i < n; ++i)
            tempCost += Math.abs(A[i] - K);

        // Take minimum of two cost
        cost = Math.min(cost, tempCost);
    }

    // Return total cost
    return cost;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 1, 6, 7, 10 };

    int n = A.length;

    System.out.println(minCost(A, n));
}
}
```

## 蟒蛇 3

```
# Python3 program to find minimum Increment or
# decrement to make array elements equal

# Function to return minimum operations need
# to be make each element of array equal
def minCost(A, n):

    # Initialize cost to 0
    cost = 0

    # Sort the array
    A.sort();

    # Middle element
    K = A[int(n / 2)]

    #Find Cost
    for i in range(0, n):
        cost = cost + abs(A[i] - K)

    # If n, is even. Take minimum of the
    # Cost obtained by considering both
    # middle elements
    if n % 2 == 0:
        tempCost = 0
        K = A[int(n / 2) - 1]

        # FInd cost again
        for i in range(0, n):
            tempCost = tempCost + abs(A[i] - K)

        # Take minimum of two cost
        cost = min(cost, tempCost)

    # Return total cost
    return cost

# Driver code
A = [1, 6, 7, 10]
n = len(A)

print(minCost(A, n))

# This code is contributed
# by Shashank_Sharma
```

## C#

```
// C# program to find minimum Increment or
// decrement to make array elements equal
using System;

class GFG {

// Function to return minimum operations need
// to be make each element of array equal
static int minCost(int []A, int n)
{
    // Initialize cost to 0
    int cost = 0;

    // Sort the array
    Array.Sort(A);

    // Middle element
    int K = A[n / 2];

    // Find Cost
    for (int i = 0; i < n; ++i)
        cost += Math.Abs(A[i] - K);

    // If n, is even. Take minimum of the
    // Cost obtained by considering both
    // middle elements
    if (n % 2 == 0) {
        int tempCost = 0;

        K = A[(n / 2) - 1];

        // Find cost again
        for (int i = 0; i < n; ++i)
            tempCost += Math.Abs(A[i] - K);

        // Take minimum of two cost
        cost = Math.Min(cost, tempCost);
    }

    // Return total cost
    return cost;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = new int []{ 1, 6, 7, 10 };

    int n = A.Length;

    Console.WriteLine(minCost(A, n));
}
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum Increment or
// decrement to make array elements equal

// Function to return minimum operations need
// to be make each element of array equal
function minCost($A, $n)
{
    // Initialize cost to 0
    $cost = 0;

    // Sort the array
    sort($A);

    // Middle element
    $K = $A[$n / 2];
    // Find Cost
    for ($i = 0; $i < $n; ++$i)
        $cost += abs($A[$i] - $K);

    // If n, is even. Take minimum of the
    // Cost obtained by considering both
    // middle elements
    if ($n % 2 == 0)
    {
        $tempCost = 0;

        $K = $A[($n / 2) - 1];

        // Find cost again
        for ($i = 0; $i < $n; ++$i)
            $tempCost += abs($A[$i] - $K);

        // Take minimum of two cost
        $cost = min($cost, $tempCost);
    }

    // Return total cost
    return $cost;
}

// Driver Code
$A = array( 1, 6, 7, 10 );
$n = sizeof($A);
echo minCost($A, $n);

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum Increment or
// decrement to make array elements equal

// Function to return minimum operations need
// to be make each element of array equal
function minCost(A,n)
{
    // Initialize cost to 0
    var cost = 0;

    // Sort the array
    A.sort();

    // Middle element
    var K = A[parseInt(n/2)];
    var i;
    // Find Cost
    for (i = 0; i < n; ++i)
        cost += Math.abs(A[i] - K);

    // If n, is even. Take minimum of the
    // Cost obtained by considering both
    // middle elements
    if (n % 2 == 0) {
        var tempCost = 0;

        K = A[parseInt(n / 2) - 1];

        // Find cost again
        for (i = 0; i < n; ++i)
            tempCost += Math.abs(A[i] - K);

        // Take minimum of two cost
        cost = Math.min(cost, tempCost);
    }

    // Return total cost
    return cost;
}

// Driver Code
    var A = [1, 6, 7, 10];

    var n = A.length;
    document.write(minCost(A, n));

</script>
```

**Output:** 

```
10
```

**时间复杂度:** O(N*log(N))
**进一步优化**我们可以[在线性时间内找到中值](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)并将时间复杂度降低到 O(N)