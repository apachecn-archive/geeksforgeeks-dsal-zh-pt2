# 最小化成本将一个数组拆分成 K 个子集，这样每个元素的成本就是它在子集中的位置的乘积

> 原文:[https://www . geeksforgeeks . org/最小化将数组拆分成 k 个子集的成本，这样每个元素的成本就是它在子集中的位置的乘积/](https://www.geeksforgeeks.org/minimize-cost-to-split-an-array-into-k-subsets-such-that-the-cost-of-each-element-is-its-product-with-its-position-in-the-subset/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个正整数 **K** ，任务是找到将数组拆分为**K**T10】子集的最小可能成本，其中每个子集的**I<sup>th</sup>T15】元素( *1 基索引*)的成本等于该元素与 **i** 的乘积**

**示例:**

> **输入:** arr[] = { 2，3，4，1 }，K = 3
> **输出:** 11
> **解释:**
> 将数组 arr[]拆分为 K(= 3)个子集{ { 4，1 }，{ 2 }， { 3 } }
> 第一子集总成本= 4 * 1 + 1 * 2 = 6
> 第二子集总成本= 2 * 1 = 2
> 第三子集总成本= 3 * 1 = 3
> 因此，K(= 3)个子集总成本为 6 + 2 + 3 = 11。
> 
> **输入:** arr[] = { 9，20，7，8 }，K=2
> **输出:** 59
> **解释:**
> 将数组 arr[]分成 K(= 3)个子集{ { 20，8 }，{ 9，7 } }
> 第一个子集的总成本= 20 * 1 + 8 * 2 = 36
> 第二个子集的总成本= 9 * 1 + 7 * 2 = 23
> 因此，总成本

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。其思想是划分数组元素，使得各个[子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)中的所有元素按降序排列。按照以下步骤解决问题:

*   [给定数组按降序排序](https://www.geeksforgeeks.org/different-ways-to-sort-an-array-in-descending-order-in-c-sharp/)。
*   初始化一个变量，比如 **totalCost** ，来存储将数组拆分成 **K** 子集的最小成本。
*   初始化一个变量，比如说 **X** ，来存储一个元素在一个子集中的位置。
*   使用变量 **i** 迭代范围**【1，N】**。每进行一次 **i <sup>次</sup>T7】操作，将 **totalCost** 的值增加**((arr[I]+…+arr[I+K])* X)**并更新 **i = i + K** 、 **X += 1** 。**
*   最后，打印**合计成本**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost to
// split array into K subsets
int getMinCost(int* arr, int n, int k)
{
    // Sort the array in descending order
    sort(arr, arr + n, greater<int>());

    // Stores minimum cost to split
    // the array into K subsets
    int min_cost = 0;

    // Stores position of
    // elements of a subset
    int X = 0;

    // Iterate over the range [1, N]
    for (int i = 0; i < n; i += k) {

        // Calculate the cost to select
        // X-th element of every subset
        for (int j = i; j < i + k && j < n; j++) {

            // Update min_cost
            min_cost += arr[j] * (X + 1);
        }

        // Update X
        X++;
    }

    return min_cost;
}

// Driver Code
int main()
{
    int arr[] = { 9, 20, 7, 8 };

    int K = 2;

    int N = sizeof(arr)
            / sizeof(arr[0]);

    // Function call
    cout << getMinCost(arr, N, K) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// reverses an array
static void reverse(int a[], int n)
{
    int i, k, t;
    for (i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}

// Function to find the minimum cost to
// split array into K subsets
static int getMinCost(int[] arr, int n, int k)
{

    // Sort the array in descending order
    Arrays.sort(arr);
    reverse(arr, n);

    // Stores minimum cost to split
    // the array into K subsets
    int min_cost = 0;

    // Stores position of
    // elements of a subset
    int X = 0;

    // Iterate over the range [1, N]
    for (int i = 0; i < n; i += k)
    {

        // Calculate the cost to select
        // X-th element of every subset
        for (int j = i; j < i + k && j < n; j++)
        {

            // Update min_cost
            min_cost += arr[j] * (X + 1);
        }

        // Update X
        X++;
    }
    return min_cost;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 9, 20, 7, 8 };
    int K = 2;
    int N = arr.length;

    // Function call
    System.out.println( getMinCost(arr, N, K));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find the minimum cost to
# split array into K subsets
def getMinCost(arr, n, k):

    # Sort the array in descending order
    arr.sort(reverse = True)

    # Stores minimum cost to split
    # the array into K subsets
    min_cost = 0;

    # Stores position of
    # elements of a subset
    X = 0;

    # Iterate over the range [1, N]
    for i in range(0, n, k):

        # Calculate the cost to select
        # X-th element of every subset
        for j in range(i, n, 1):

            # Update min_cost
            if(j < i + k):
                min_cost += arr[j] * (X + 1);

        # Update X
        X += 1;
    return min_cost;

# Driver code
if __name__ == '__main__':
    arr = [9, 20, 7, 8];
    K = 2;
    N = len(arr);

    # Function call
    print(getMinCost(arr, N, K));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

// reverses an array
static void reverse(int []a, int n)
{
    int i, k, t;
    for (i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}

// Function to find the minimum cost to
// split array into K subsets
static int getMinCost(int[] arr, int n, int k)
{

    // Sort the array in descending order
    Array.Sort(arr);
    reverse(arr, n);

    // Stores minimum cost to split
    // the array into K subsets
    int min_cost = 0;

    // Stores position of
    // elements of a subset
    int X = 0;

    // Iterate over the range [1, N]
    for (int i = 0; i < n; i += k)
    {

        // Calculate the cost to select
        // X-th element of every subset
        for (int j = i; j < i + k && j < n; j++)
        {

            // Update min_cost
            min_cost += arr[j] * (X + 1);
        }

        // Update X
        X++;
    }
    return min_cost;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 9, 20, 7, 8 };
    int K = 2;
    int N = arr.Length;

    // Function call
    Console.WriteLine( getMinCost(arr, N, K));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Reverses an array
function reverse(a, n)
{
    var i, k, t;
    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}

// Function to find the minimum cost to
// split array into K subsets
function getMinCost(arr, n, k)
{

    // Sort the array in descending order
    arr.sort((a, b) => b - a);

    // Stores minimum cost to split
    // the array into K subsets
    var min_cost = 0;

    // Stores position of
    // elements of a subset
    var X = 0;

    // Iterate over the range [1, N]
    for(var i = 0; i < n; i += k)
    {

        // Calculate the cost to select
        // X-th element of every subset
        for(var j = i; j < i + k && j < n; j++)
        {

            // Update min_cost
            min_cost += arr[j] * (X + 1);
        }

        // Update X
        X++;
    }
    return min_cost;
}

// Driver code
var arr = [ 9, 20, 7, 8 ];
var K = 2;
var N = arr.length;

// Function call
document.write(getMinCost(arr, N, K));

// This code is contributed by rdtank

</script>
```

**Output:** 

```
59
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*