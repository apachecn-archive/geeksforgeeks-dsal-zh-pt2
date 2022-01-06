# 通过重复移除 K 个数组元素来最大化清空给定数组的成本

> 原文:[https://www . geesforgeks . org/通过重复移除 k 个数组元素来最大化空给定数组的成本/](https://www.geeksforgeeks.org/maximize-cost-to-empty-given-array-by-repetitively-removing-k-array-elements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** 和一个整数**K**T8】(N % K = 0)，任务是找出移除所有数组元素的最大开销。在每次操作中，确切地说 **K** 阵列元素可以被移除，并且移除的成本等于移除的第二小元素。

**示例:**

> **输入:** arr[] = { 1，3，4，1，5，1，5，3 }，K = 4
> **输出:** 5
> **解释:**
> 移除{arr[0]，arr[3]，arr[5]，arr[7]}将 arr[]修改为{3，4，5，5}。移除的第二小元素= 1。因此，成本= 1
> 移除{arr[0]，arr[1]，arr[2]，arr[3]}会将 arr[]修改为{}。移除的第二小元素= 4。因此，成本= 1 + 4 = 5
> 因此，所需的输出为= 5
> 
> **输入:** arr[] = { 1，2，3，4}，K = 4
> T3】输出: 2

**进场:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。其思想是[对数组](https://www.geeksforgeeks.org/sort-c-stl/)进行排序，并在每次操作中重复移除 **K** 个最小的数组元素。按照以下步骤解决问题:

*   初始化一个变量，比如 **maxCost** ，来存储移除所有数组元素的最大代价。
*   [按升序排列数组](https://www.geeksforgeeks.org/sort-c-stl/)。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，更新 **maxCost = arr[i + 1]** 和 **i = i + K** 的值。
*   最后打印 **maxCost** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum cost to
// remove all array elements
int maxCostToRemove(int arr[], int N,
                             int K)
{

    // Stores maximum cost to
    // remove array elements
    int maxCost = 0;

    // Sort array in
    // ascending order   
    sort(arr, arr + N);

    // Traverse the array
    for (int i = 0; i < N;
                i += K) {

        // Update maxCost
        maxCost += arr[i + 1];
    }

    return maxCost;
}

// Driver Code
int main()
{
    int arr[]= { 1, 3, 4, 1, 5, 1, 5, 3};
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 4;
    cout<< maxCostToRemove(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Arrays;

class GFG{

// Function to find the maximum cost to
// remove all array elements
static int maxCostToRemove(int arr[], int N,
                             int K)
{

    // Stores maximum cost to
    // remove array elements
    int maxCost = 0;

    // Sort array in
    // ascending order   
    Arrays.sort(arr);

    // Traverse the array
    for (int i = 0; i < N;
                i += K) {

        // Update maxCost
        maxCost += arr[i + 1];
    }

    return maxCost;
}

// Drive Code
public static void main(String[] args)
{
    int arr[]= { 1, 3, 4, 1, 5, 1, 5, 3};
    int N = arr.length;
    int K = 4;
    System.out.print(maxCostToRemove(arr, N, K));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum cost to
# remove all array elements
def maxCostToRemove(arr, N, K):

    # Stores maximum cost to
    # remove array elements
    maxCost = 0

    # Sort array in
    # ascending order
    arr = sorted(arr)

    # Traverse the array
    for i in range(0, N, K):

        # Update maxCost
        maxCost += arr[i + 1]

    return maxCost

# Driver Code
if __name__ == '__main__':
    arr= [1, 3, 4, 1, 5, 1, 5, 3]
    N = len(arr)
    K = 4
    print(maxCostToRemove(arr, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the maximum cost to
// remove all array elements
static int maxCostToRemove(int []arr, int N,
                             int K)
{

    // Stores maximum cost to
    // remove array elements
    int maxCost = 0;

    // Sort array in
    // ascending order   
    Array.Sort(arr);

    // Traverse the array
    for (int i = 0; i < N;
                i += K) {

        // Update maxCost
        maxCost += arr[i + 1];
    }

    return maxCost;
}

// Drive Code
public static void Main(String[] args)
{
    int []arr= { 1, 3, 4, 1, 5, 1, 5, 3};
    int N = arr.Length;
    int K = 4;
    Console.Write(maxCostToRemove(arr, N, K));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the maximum cost to
// remove all array elements
function maxCostToRemove(arr, N, K)
{

    // Stores maximum cost to
    // remove array elements
    let maxCost = 0;

    // Sort array in
    // ascending order  
    arr.sort();

    // Traverse the array
    for(let i = 0; i < N; i += K)
    {

        // Update maxCost
        maxCost += arr[i + 1];
    }
    return maxCost;
}

// Driver code
let arr = [ 1, 3, 4, 1, 5, 1, 5, 3 ];
let N = arr.length;
let K = 4;

document.write(maxCostToRemove(arr, N, K));

// This code is contributed by code_hunt

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N * log N)*
T5**辅助空间** O(1)