# 在 N 大小的数组中选择 3 个递增元素的最小成本

> 原文:[https://www . geeksforgeeks . org/最小选择成本-3-增加元素数组大小-n/](https://www.geeksforgeeks.org/minimum-cost-of-choosing-3-increasing-elements-in-an-array-of-size-n/)

给定两个数组 **arr[]** 和 **cost[]** ，其中 **cost[i]** 是与 **arr[i]** 相关联的成本，任务是找到从数组中选择三个元素的最小成本，使得**arr[I]<arr[j]<arr[j]**。

**示例:**

> **输入:** arr[] = {2，4，5，4，10}，成本[] = {40，30，20，10，40}
> **输出:** 90
> (2，4，5)，(2，4，10)和(4，5，10)是
> 唯一有效的成本为 90 的三胞胎。
> 
> **输入:** arr[] = {1，2，3，4，5，6}，成本[] = {10，13，11，14，15，12}
> **输出:** 33

**天真的方法:**基本的方法是两次运行三个嵌套循环，并检查每个可能的三元组。这种方法的时间复杂度将是 **O(n <sup>3</sup> )** 。

**高效的方法:**一种高效的方法是固定中间元素，并在给定数组中搜索其左边成本最小的较小元素和其右边成本最小的较大元素。如果找到一个有效的三元组，那么更新最小成本。这种方法的时间复杂度将是 **O(n <sup>2</sup> )** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum required cost
int minCost(int arr[], int cost[], int n)
{

    // To store the cost of choosing three elements
    int costThree = INT_MAX;

    // Fix the middle element
    for (int j = 0; j < n; j++) {

        // Initialize cost of the first
        // and the third element
        int costI = INT_MAX, costK = INT_MAX;

        // Search for the first element
        // in the left subarray
        for (int i = 0; i < j; i++) {

            // If smaller element is found
            // then update the cost
            if (arr[i] < arr[j])
                costI = min(costI, cost[i]);
        }

        // Search for the third element
        // in the right subarray
        for (int k = j + 1; k < n; k++) {

            // If greater element is found
            // then update the cost
            if (arr[k] > arr[j])
                costK = min(costK, cost[k]);
        }

        // If a valid triplet was found then
        // update the minimum cost so far
        if (costI != INT_MAX && costK != INT_MAX) {
            costThree = min(costThree, cost[j]
                                           + costI
                                           + costK);
        }
    }

    // No such triplet found
    if (costThree == INT_MAX)
        return -1;
    return costThree;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 5, 4, 10 };
    int cost[] = { 40, 30, 20, 10, 40 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minCost(arr, cost, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum required cost
static int minCost(int arr[], int cost[], int n)
{

    // To store the cost of choosing three elements
    int costThree = Integer.MAX_VALUE;

    // Fix the middle element
    for (int j = 0; j < n; j++)
    {

        // Initialize cost of the first
        // and the third element
        int costI = Integer.MAX_VALUE;
        int costK = Integer.MAX_VALUE;

        // Search for the first element
        // in the left subarray
        for (int i = 0; i < j; i++)
        {

            // If smaller element is found
            // then update the cost
            if (arr[i] < arr[j])
                costI = Math.min(costI, cost[i]);
        }

        // Search for the third element
        // in the right subarray
        for (int k = j + 1; k < n; k++)
        {

            // If greater element is found
            // then update the cost
            if (arr[k] > arr[j])
                costK = Math.min(costK, cost[k]);
        }

        // If a valid triplet was found then
        // update the minimum cost so far
        if (costI != Integer.MAX_VALUE &&
            costK != Integer.MAX_VALUE)
        {
            costThree = Math.min(costThree, cost[j] +
                                    costI + costK);
        }
    }

    // No such triplet found
    if (costThree == Integer.MAX_VALUE)
        return -1;

    return costThree;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 2, 4, 5, 4, 10 };
    int cost[] = { 40, 30, 20, 10, 40 };
    int n = arr.length;

    System.out.println(minCost(arr, cost, n));
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum required cost
def minCost(arr, cost, n):

    # To store the cost of choosing three elements
    costThree = 10**9

    # Fix the middle element
    for j in range(n):

        # Initialize cost of the first
        # and the third element
        costI = 10**9
        costK = 10**9

        # Search for the first element
        # in the left subarray
        for i in range(j):

            # If smaller element is found
            # then update the cost
            if (arr[i] < arr[j]):
                costI = min(costI, cost[i])

        # Search for the third element
        # in the right subarray
        for k in range(j + 1, n):

            # If greater element is found
            # then update the cost
            if (arr[k] > arr[j]):
                costK = min(costK, cost[k])

        # If a valid triplet was found then
        # update the minimum cost so far
        if (costI != 10**9 and costK != 10**9):
            costThree = min(costThree, cost[j] +
                               costI + costK)

    # No such triplet found
    if (costThree == 10**9):
        return -1
    return costThree

# Driver code
arr = [2, 4, 5, 4, 10]
cost = [40, 30, 20, 10, 40]
n = len(arr)

print(minCost(arr, cost, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the
// minimum required cost
static int minCost(int []arr,
                   int []cost, int n)
{

    // To store the cost of
    // choosing three elements
    int costThree = int.MaxValue;

    // Fix the middle element
    for (int j = 0; j < n; j++)
    {

        // Initialize cost of the first
        // and the third element
        int costI = int.MaxValue;
        int costK = int.MaxValue;

        // Search for the first element
        // in the left subarray
        for (int i = 0; i < j; i++)
        {

            // If smaller element is found
            // then update the cost
            if (arr[i] < arr[j])
                costI = Math.Min(costI, cost[i]);
        }

        // Search for the third element
        // in the right subarray
        for (int k = j + 1; k < n; k++)
        {

            // If greater element is found
            // then update the cost
            if (arr[k] > arr[j])
                costK = Math.Min(costK, cost[k]);
        }

        // If a valid triplet was found then
        // update the minimum cost so far
        if (costI != int.MaxValue &&
            costK != int.MaxValue)
        {
            costThree = Math.Min(costThree, cost[j] +
                                    costI + costK);
        }
    }

    // No such triplet found
    if (costThree == int.MaxValue)
        return -1;

    return costThree;
}

// Driver code
static public void Main ()
{
    int []arr = { 2, 4, 5, 4, 10 };
    int []cost = { 40, 30, 20, 10, 40 };
    int n = arr.Length;

    Console.Write(minCost(arr, cost, n));
}
}

// This code is contributed by Sachin..
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the minimum required cost
function minCost(arr,cost,n)
{
    // To store the cost of choosing three elements
    let costThree = Number.MAX_VALUE;

    // Fix the middle element
    for (let j = 0; j < n; j++)
    {

        // Initialize cost of the first
        // and the third element
        let costI = Number.MAX_VALUE;
        let costK = Number.MAX_VALUE;

        // Search for the first element
        // in the left subarray
        for (let i = 0; i < j; i++)
        {

            // If smaller element is found
            // then update the cost
            if (arr[i] < arr[j])
                costI = Math.min(costI, cost[i]);
        }

        // Search for the third element
        // in the right subarray
        for (let k = j + 1; k < n; k++)
        {

            // If greater element is found
            // then update the cost
            if (arr[k] > arr[j])
                costK = Math.min(costK, cost[k]);
        }

        // If a valid triplet was found then
        // update the minimum cost so far
        if (costI != Number.MAX_VALUE &&
            costK != Number.MAX_VALUE)
        {
            costThree = Math.min(costThree, cost[j] +
                                    costI + costK);
        }
    }

    // No such triplet found
    if (costThree == Number.MAX_VALUE)
        return -1;

    return costThree;
}

// Driver code
let arr=[2, 4, 5, 4, 10];
let cost=[40, 30, 20, 10, 40 ];
let n = arr.length;
document.write(minCost(arr, cost, n));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
90
```