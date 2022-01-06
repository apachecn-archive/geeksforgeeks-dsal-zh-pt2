# 最大化任何一对可能的数组元素之间的乘积和差的和

> 原文:[https://www . geeksforgeeks . org/最大化任意对数组元素之间的乘积和差值-可能/](https://www.geeksforgeeks.org/maximize-sum-of-product-and-difference-between-any-pair-of-array-elements-possible/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是为给定数组中的任意一对 **(arr[i]，arr[j])** 找到**arr[I]∫arr[j]+arr[I]—arr[j]**的最大值，其中 **i！= j** 和 **0 < i，j<N–1**。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 21
> **解释:**
> 在数组的所有对中，获得对的最大值(arr[4]，arr[3])，等于
> =>arr[4]* arr[3]+arr[4]–arr[3]= 5 * 4+5–4 = 20+1 = 21。
> 
> **输入:** {-4，-5，0，1，3}
> **输出:** 21
> **说明:**
> 在数组的所有对中，取对(arr[0]，arr[1])的最大值，等于
> =>arr[0]* arr[1]+arr[0]–arr[1]=(-4)*(-5)+(-4)–(-5)= 20+1

**天真法:**解决问题最简单的方法就是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) **(arr[i]，arr[j])** ( **i！= j** )并计算所有对的表达式。最后，打印所有对的最大值。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**最优思想基于以下两种情况下表达式的值可以最大的观察:

*   如果该对包括最大的[和第二大的数组元素](https://www.geeksforgeeks.org/find-second-largest-element-array/)。
*   如果该对包括一个最小的[和第二个最小的阵列元素](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)，则被选择。当最小元素和第二小元素都是负数，并且它们的乘积将产生正数时，可能会出现这种情况。

按照以下步骤解决问题:

*   [按升序排列数组**arr[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   评估配对**arr[N–1]**和**arr[N–2]**的表达式，并将其存储在一个变量中，比如 **max1** 。
*   类似地，计算对 **arr[1]** 和 **arr[0]** 的表达式，并将其存储在一个变量中，比如 **max2** 。
*   将**最大值**和**最大值**最大值存储在一个变量中，比如 **ans** 。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to evaluate given expression
int compute(int a, int b)
{
    // Store the result
    int ans = a * b + a - b;
    return ans;
}

// Function to find the maximum value of
// the given expression possible for any
// unique pair from the given array
void findMaxValue(int arr[], int N)
{
    // Sort the array in ascending order
    sort(arr, arr + N);

    // Evaluate the expression for
    // the two largest elements
    int maxm = compute(arr[N - 1], arr[N - 2]);

    // Evaluate the expression for
    // the two smallest elements
    maxm = max(maxm, compute(arr[1], arr[0]));

    // Print the maximum
    cout << maxm;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { -4, -5, 0, 1, 3 };

    // Store the size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    findMaxValue(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to evaluate given expression
  static int compute(int a, int b)
  {
    // Store the result
    int ans = a * b + a - b;
    return ans;
  }

  // Function to find the maximum value of
  // the given expression possible for any
  // unique pair from the given array
  static void findMaxValue(int arr[], int N)
  {
    // Sort the array in ascending order
    Arrays.sort(arr);

    // Evaluate the expression for
    // the two largest elements
    int maxm = compute(arr[N - 1], arr[N - 2]);

    // Evaluate the expression for
    // the two smallest elements
    maxm = Math.max(maxm, compute(arr[1], arr[0]));

    // Print the maximum
    System.out.print(maxm);
  }

  // Driver Code
  public static void main(String[] args)
  {
    // Given array
    int arr[] = { -4, -5, 0, 1, 3 };

    // Store the size of the array
    int N = arr.length;

    findMaxValue(arr, N);
  }
}

// This code is contributed by saanjoy_62
```

## 蟒蛇 3

```
# Python Program for the above approach
# Function to evaluate given expression
def compute(a, b):

    # Store the result
    res = (a * b) + (a - b)
    return res

# Function to find the maximum value of
# the given expression possible for any
# unique pair from the given array
def findMaxValue(arr, N):

    # Sort the list in ascending order
    arr.sort()

    # Evaluate the expression for
    # the two largest elements
    maxm = compute(arr[N - 1], arr[N - 2])

    # Evaluate the expression for
    # the two smallest elements
    maxm = max(maxm, compute(arr[1], arr[0]));
    print(maxm)

# Driver code
# given list
arr = [-4, -5, 0, 1, 3]

# store the size of the list
N = len(arr)
findMaxValue(arr, N)

# This code is contributed by santhoshcharan.
```

## C#

```
// C# program for above approach
using System;
public class GFG
{

  // Function to evaluate given expression
  static int compute(int a, int b)
  {
    // Store the result
    int ans = a * b + a - b;
    return ans;
  }

  // Function to find the maximum value of
  // the given expression possible for any
  // unique pair from the given array
  static void findMaxValue(int[] arr, int N)
  {
    // Sort the array in ascending order
    Array.Sort(arr);

    // Evaluate the expression for
    // the two largest elements
    int maxm = compute(arr[N - 1], arr[N - 2]);

    // Evaluate the expression for
    // the two smallest elements
    maxm = Math.Max(maxm, compute(arr[1], arr[0]));

    // Print the maximum
    Console.WriteLine(maxm);
  }

// Driver code
public static void Main(String[] args)
{

    // Given array
    int[] arr = { -4, -5, 0, 1, 3 };

    // Store the size of the array
    int N = arr.Length;

    findMaxValue(arr, N);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to evaluate given expression
function compute(a, b)
{
    // Store the result
    var ans = a * b + a - b;
    return ans;
}

// Function to find the maximum value of
// the given expression possible for any
// unique pair from the given array
function findMaxValue(arr, N)
{
    // Sort the array in ascending order
    arr.sort(function(a,b){return a - b});

    // Evaluate the expression for
    // the two largest elements
    var maxm = compute(arr[N - 1], arr[N - 2]);

    // Evaluate the expression for
    // the two smallest elements
    maxm = Math.max(maxm, compute(arr[1], arr[0]));

    // Print the maximum
    document.write(maxm);
}

// Driver Code
var arr = [-4, -5, 0, 1, 3];
var N = arr.length;
findMaxValue(arr, N);

// This code is contributed by Shubhamsingh10
</script>
```

**Output**

```
21
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*