# 使所有元素为 0 的最小数组运算次数

> 原文:[https://www . geeksforgeeks . org/最小数组操作数使所有元素-0/](https://www.geeksforgeeks.org/minimum-number-of-operations-on-an-array-to-make-all-elements-0/)

给定一个 **N** 整数的数组 **arr[]** 和一个整数**成本**，任务是计算用给定操作制作数组 **0** 所有元素的成本。在单次操作中，可以选择一个索引 **0 ≤ i < N** 和一个整数 **X > 0** ，使得 **0 ≤ i + X < N** 那么元素可以更新为**arr[I]= arr[I]–1**和 **arr[i + X] = arr[i + X] + 1** 。如果 **i + X ≥ N** ，则只会更新**arr【I】**，但费用是常规费用的两倍。打印所需的最低成本。
**举例:**

> **输入:** arr[] = {1，2，4，5}，成本= 1
> **输出:** 31
> **招式 1:** i = 0，X = 3，arr[] = {0，2，4，6}(成本= 1)
> **招式 2 和 3:** i = 1，X = 2，arr[] = {0，0，4，8}(成本= 2)
> **招式 4，5，6 12}(成本= 4)
> **移动 8:** i = 3，X > 0，arr[] = {0，0，0，0}(成本= 24)
> 总成本= 1 + 2 + 4 + 24 = 31
> **输入:** arr[] = {1，1，0，5}，成本= 2
> **输出:** 32**

**方法:**为了最小化成本，对于每个指标 **i** 总是选择 **X** ，这样**I+X = N–1**即最后一个要素，那么最小成本可以计算为:

*   将 **arr[0]** 到**arr[n–2]**的元素之和存储在 **sum** 中，然后更新 **totalCost = cost * sum** 和**arr[n–1]= arr[n–1]+sum**。
*   现在制作除最后一个元素外的所有元素 **0** 的成本已经计算出来了。制作最后一个元素 **0** 的成本可以计算为**总成本=总成本+ (2 *成本* arr[n–1])**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum cost
int minCost(int n, int arr[], int cost)
{
    int sum = 0, totalCost = 0;

    // Sum of all the array elements
    // except the last element
    for (int i = 0; i < n - 1; i++)
        sum += arr[i];

    // Cost of making all the array elements 0
    // except the last element
    totalCost += cost * sum;

    // Update the last element
    arr[n - 1] += sum;

    // Cost of making the last element 0
    totalCost += (2 * cost * arr[n - 1]);

    return totalCost;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int cost = 1;
    cout << minCost(n, arr, cost);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GfG
{

    // Function to return the minimum cost
    static int minCost(int n, int arr[], int cost)
    {
        int sum = 0, totalCost = 0;

        // Sum of all the array elements
        // except the last element
        for (int i = 0; i < n - 1; i++)
            sum += arr[i];

        // Cost of making all the array elements 0
        // except the last element
        totalCost += cost * sum;

        // Update the last element
        arr[n - 1] += sum;

        // Cost of making the last element 0
        totalCost += (2 * cost * arr[n - 1]);

        return totalCost;
    }

    // Driver code
    public static void main(String []args)
    {

        int arr[] = { 1, 2, 4, 5 };
        int n = arr.length;
        int cost = 1;
        System.out.println(minCost(n, arr, cost));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum cost
def minCost(n, arr, cost):

    Sum, totalCost = 0, 0

    # Sum of all the array elements
    # except the last element
    for i in range(0, n - 1):
        Sum += arr[i]

    # Cost of making all the array elements 0
    # except the last element
    totalCost += cost * Sum

    # Update the last element
    arr[n - 1] += Sum

    # Cost of making the last element 0
    totalCost += (2 * cost * arr[n - 1])

    return totalCost

# Driver code
if __name__ == "__main__":

    arr = [1, 2, 4, 5]
    n = len(arr)
    cost = 1
    print(minCost(n, arr, cost))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System ;

class GfG
{

    // Function to return the minimum cost
    static int minCost(int n, int []arr, int cost)
    {
        int sum = 0, totalCost = 0;

        // Sum of all the array elements
        // except the last element
        for (int i = 0; i < n - 1; i++)
            sum += arr[i];

        // Cost of making all the array elements 0
        // except the last element
        totalCost += cost * sum;

        // Update the last element
        arr[n - 1] += sum;

        // Cost of making the last element 0
        totalCost += (2 * cost * arr[n - 1]);

        return totalCost;
    }

    // Driver code
    public static void Main()
    {

        int []arr = { 1, 2, 4, 5 };
        int n = arr.Length;
        int cost = 1;
        Console.WriteLine(minCost(n, arr, cost));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum cost
function minCost($n, $arr, $cost)
{
    $sum = 0;
    $totalCost = 0;

    // Sum of all the array elements
    // except the last element
    for ($i = 0; $i < ($n - 1); $i++)
        $sum += $arr[$i];

    // Cost of making all the array
    // elements 0 except the last element
    $totalCost += $cost * $sum;

    // Update the last element
    $arr[$n - 1] += $sum;

    // Cost of making the last element 0
    $totalCost += (2 * $cost * $arr[$n - 1]);

    return $totalCost;
}

// Driver code
$arr = array( 1, 2, 4, 5 );
$n = sizeof($arr);
$cost = 1;
echo minCost($n, $arr, $cost);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the minimum cost
    function minCost(n, arr, cost)
    {
        let sum = 0, totalCost = 0;

        // Sum of all the array elements
        // except the last element
        for (let i = 0; i < n - 1; i++)
            sum += arr[i];

        // Cost of making all the array elements 0
        // except the last element
        totalCost += cost * sum;

        // Update the last element
        arr[n - 1] += sum;

        // Cost of making the last element 0
        totalCost += (2 * cost * arr[n - 1]);

        return totalCost;
    }

    let arr = [ 1, 2, 4, 5 ];
    let n = arr.length;
    let cost = 1;
    document.write(minCost(n, arr, cost));

</script>
```

**Output:** 

```
31
```

**时间复杂度:** O(n)