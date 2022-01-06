# 访问位于环形道路周边的所有节点的最小成本路径

> 原文:[https://www . geeksforgeeks . org/最低成本-所有节点的访问路径-位于环形道路的圆周上/](https://www.geeksforgeeks.org/minimum-cost-path-to-visit-all-nodes-situated-at-the-circumference-of-circular-road/)

给定圆的**周长**和一个**数组 pos【】**，该数组标记了顺时针方向上圆上 N 个点相对于一个固定点的距离。我们必须找到一个最小的距离，通过它我们可以访问所有的点。我们可以从任何一点开始。
**例:**

> **输入:**周长= 20，pos = [3，6，9]
> **输出:**最小路径成本=6
> **解释:**
> 如果我们从 3 开始，我们去 6，然后我们去 9。因此，第一次移动的总路径成本为 3 个单位，第二次移动的总路径成本为 3 个单位，总计为 6。
> **输入:**周长=20 pos = [3，6，19]
> **输出:**最小路径成本= 7
> **解释:**
> 如果我们从 19 开始，我们去 3，它将花费 4 个单位，因为我们从 19->20->1->2->3 给出 4 个单位，然后 3 到 6 给出 3 个单位。总的来说，最低成本将是 4 + 3 = 7。

**方法:**
要解决上面提到的问题，我们必须遵循下面给出的步骤:

*   对标记圆上 N 个点的距离的数组进行排序。
*   通过添加值为 **arr[i + n] =周长+ arr[i]** 的 N 个元素，使数组大小加倍。
*   对于值 I 的所有有效迭代，求最小值**(arr[I+(n-1)]–arr[I])**

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// Minimum Cost Path to visit all nodes
// situated at the Circumference of
// Circular Road

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost
int minCost(int arr[], int n, int circumference)
{
    // Sort the given array
    sort(arr, arr + n);

    // Initialise a new array of double size
    int arr2[2 * n];

    // Fill the array elements
    for (int i = 0; i < n; i++) {
        arr2[i] = arr[i];
        arr2[i + n] = arr[i] + circumference;
    }

    // Find the minimum path cost
    int res = INT_MAX;

    for (int i = 0; i < n; i++)
        res = min(res, arr2[i + (n - 1)] - arr2[i]);

    // Return the final result
    return res;
}

// Driver code
int main()
{
    int arr[] = { 19, 3, 6 };

    int n = sizeof(arr) / sizeof(arr[0]);

    int circumference = 20;

    cout << minCost(arr, n, circumference);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// Minimum Cost Path to visit all nodes
// situated at the Circumference of
// Circular Road
import java.util.*;
import java. util. Arrays;

class GFG {

// Function to find the minimum cost
static int minCost(int arr[], int n,
                   int circumference)
{
    // Sort the given array
    Arrays.sort(arr);

    // Initialise a new array of double size
    int[] arr2 = new int[2 * n];

    // Fill the array elements
    for(int i = 0; i < n; i++)
    {
       arr2[i] = arr[i];
       arr2[i + n] = arr[i] + circumference;
    }

    // Find the minimum path cost
    int res = Integer.MAX_VALUE;

    for(int i = 0; i < n; i++)
       res = Math.min(res,
                      arr2[i + (n - 1)] -
                      arr2[i]);

    // Return the final result
    return res;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 19, 3, 6 };
    int n = arr.length;
    int circumference = 20;

    System.out.println(minCost(arr, n,
                               circumference));
}

}

// This code is contributed by ANKITKUMAR34
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum cost path to visit all nodes
# situated at the circumference of
# circular Road

# Function to find the minimum cost
def minCost(arr, n, circumference):

    # Sort the given array
    arr.sort()

    #Initialise a new array of double size
    arr2 = [0] * (2 * n)

    # Fill the array elements
    for i in range(n):
        arr2[i] = arr[i]
        arr2[i + n] = arr[i] + circumference

    # Find the minimum path cost
    res = 9999999999999999999;

    for i in range(n):
        res = min(res,
                  arr2[i + (n - 1)] -
                  arr2[i]);

    # Return the final result
    return res;

# Driver code
arr = [ 19, 3, 6 ];
n = len(arr)
circumference = 20;

print(minCost(arr, n, circumference))

# This code is contributed by ANKITKUMAR34
```

## C#

```
// C# implementation to find the
// Minimum Cost Path to visit all nodes
// situated at the Circumference of
// Circular Road
using System;

class GFG{

// Function to find the minimum cost
static int minCost(int []arr, int n,
                   int circumference)
{
    // Sort the given array
    Array.Sort(arr);

    // Initialise a new array of double size
    int[] arr2 = new int[2 * n];

    // Fill the array elements
    for(int i = 0; i < n; i++)
    {
       arr2[i] = arr[i];
       arr2[i + n] = arr[i] + circumference;
    }

    // Find the minimum path cost
    int res = int.MaxValue;

    for(int i = 0; i < n; i++)
       res = Math.Min(res, arr2[i + (n - 1)] -
                           arr2[i]);

    // Return the readonly result
    return res;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 19, 3, 6 };
    int n = arr.Length;
    int circumference = 20;

    Console.WriteLine(minCost(arr, n, circumference));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// Minimum Cost Path to visit all nodes
// situated at the Circumference of
// Circular Road

// Function to find the minimum cost
function minCost(arr, n,circumference)
{
    // Sort the given array
    arr.sort((a,b)=>a-b)

    // Initialise a new array of double size
    var arr2 = Array(2* n).fill(0);

    // Fill the array elements
    for (var i = 0; i < n; i++) {
        arr2[i] = arr[i];
        arr2[i + n] = arr[i] + circumference;
    }

    // Find the minimum path cost
    var res = 1000000000;

    for (var i = 0; i < n; i++)
        res = Math.min(res, arr2[i + (n - 1)] - arr2[i]);

    // Return the final result
    return res;
}

// Driver code
var arr = [19, 3, 6 ];
var n = arr.length;
var circumference = 20;
document.write( minCost(arr, n, circumference));

</script>
```

**Output:** 

```
7
```

时间复杂度:O(n * log n)

辅助空间:O(n)