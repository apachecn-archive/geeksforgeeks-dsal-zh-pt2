# 通过与另一个阵列的元素交换，最大化一个阵列的最大可能子阵列和

> 原文:[https://www . geeksforgeeks . org/通过与另一个阵列中的元素进行交换来最大化最大可能的子阵列总和/](https://www.geeksforgeeks.org/maximize-maximum-possible-subarray-sum-of-an-array-by-swapping-with-elements-from-another-array/)

给定两个分别由 **N** 和 **K** 元素组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和**brr【】**，任务是通过将数组**arr【】**中的任何元素与数组**brr【】**中的任何元素进行任意次数的交换，从数组**arr【】**中找到最大可能的子数组和。

**示例:**

> **输入:** N = 5，K = 4，arr[] = { 7，2，-1，4，5 }，brr[] = { 1，2，3，2 }
> **输出:** 21
> **解释:**用 brr[2]交换 arr[2]将 arr[]修改为{ 7，2，3，4，5}
> 数组 arr[] = 21 的最大子数组和
> 
> **输入:** N = 2，K = 2，arr[] = { -4，-4 }，brr[] = { 8，8 }
> **输出:** 16
> **解释:**用 brr[0]交换 arr[0]，用 brr[1]交换 arr[1]将 arr[]修改为{ 8，8}
> 数组 arr[] = 16 的最大和子数组

**方法:**解决这个问题的思路是通过**交换数组 **arr** 和 **brr 的元素**，arr 内的元素**也可以进行三次交换。以下是一些观察结果:

*   如果需要交换数组**arr【】**中具有索引 **i** 和 **j** 的两个元素，则从数组 **brr【】、**中取出任意临时元素，比如在索引 **k** 处，并执行以下操作:
    *   **交换 arr[i]和 brr[k]。**
    *   **交换 brr[k]和 arr[j]。**
    *   **交换 arr[i]和 brr[k]。**
*   现在阵列 **arr[]** 和 **brr[]** 之间的元素也可以在阵列 **arr[]** 内交换。因此，贪婪地排列数组**arr【】**中的元素，使其以连续的方式包含所有正整数。

按照以下步骤解决问题:

*   将数组 **arr[]** 和 **brr[]** 的所有元素存储在另一个数组 **crr[]** 中。
*   [按降序排列](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)**【crr】**。
*   计算包含正元素的数组 **crr[]** 中直到最后一个指数(*小于 **N*** )的总和。
*   打印得出的总和。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum subarray sum
// possible by swapping elements from array
// arr[] with that from array brr[]
void maxSum(int* arr, int* brr, int N, int K)
{
    // Stores elements from the
    // arrays arr[] and brr[]
    vector<int> crr;

    // Store elements of array arr[]
    // and brr[] in the vector crr
    for (int i = 0; i < N; i++) {
        crr.push_back(arr[i]);
    }
    for (int i = 0; i < K; i++) {
        crr.push_back(brr[i]);
    }

    // Sort the vector crr
    // in descending order
    sort(crr.begin(), crr.end(),
         greater<int>());

    // Stores maximum sum
    int sum = 0;

    // Calculate the sum till the last
    // index in crr[] which is less than
    // N which contains a positive element
    for (int i = 0; i < N; i++) {
        if (crr[i] > 0) {
            sum += crr[i];
        }
        else {
            break;
        }
    }

    // Print the sum
    cout << sum << endl;
}

// Driver code
int main()
{
    // Given arrays and respective lengths
    int arr[] = { 7, 2, -1, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int brr[] = { 1, 2, 3, 2 };
    int K = sizeof(brr) / sizeof(brr[0]);

    // Calculate maximum subarray sum
    maxSum(arr, brr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to find the maximum subarray sum
  // possible by swapping elements from array
  // arr[] with that from array brr[]
  static void maxSum(int arr[], int brr[], int N, int K)
  {

    // Stores elements from the
    // arrays arr[] and brr[]
    Vector<Integer> crr = new Vector<Integer>();

    // Store elements of array arr[]
    // and brr[] in the vector crr
    for (int i = 0; i < N; i++)
    {
      crr.add(arr[i]);
    }
    for (int i = 0; i < K; i++)
    {
      crr.add(brr[i]);
    }

    // Sort the vector crr
    // in descending order
    Collections.sort(crr);
    Collections.reverse(crr);

    // Stores maximum sum
    int sum = 0;

    // Calculate the sum till the last
    // index in crr[] which is less than
    // N which contains a positive element
    for (int i = 0; i < N; i++)
    {
      if (crr.get(i) > 0)
      {
        sum += crr.get(i);
      }
      else
      {
        break;
      }
    }

    // Print the sum
    System.out.println(sum);
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given arrays and respective lengths
    int arr[] = { 7, 2, -1, 4, 5 };
    int N = arr.length;
    int brr[] = { 1, 2, 3, 2 };
    int K = brr.length;

    // Calculate maximum subarray sum
    maxSum(arr, brr, N, K);
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum subarray sum
# possible by swapping elements from array
# arr[] with that from array brr[]
def maxSum(arr, brr, N, K):

    # Stores elements from the
    # arrays arr[] and brr[]
    crr = []

    # Store elements of array arr[]
    # and brr[] in the vector crr
    for i in range(N):
        crr.append(arr[i])

    for i in range(K):
        crr.append(brr[i])

    # Sort the vector crr
    # in descending order
    crr = sorted(crr)[::-1]

    # Stores maximum sum
    sum = 0

    # Calculate the sum till the last
    # index in crr[] which is less than
    # N which contains a positive element
    for i in range(N):
        if (crr[i] > 0):
            sum += crr[i]
        else:
            break

    # Print the sum
    print(sum)

# Driver code
if __name__ == '__main__':

    # Given arrays and respective lengths
    arr = [ 7, 2, -1, 4, 5 ]
    N = len(arr)
    brr = [ 1, 2, 3, 2 ]
    K = len(brr)

    # Calculate maximum subarray sum
    maxSum(arr, brr, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum subarray sum
// possible by swapping elements from array
// arr[] with that from array brr[]
static void maxSum(int[] arr, int[] brr,
                   int N, int K)
{

    // Stores elements from the
    // arrays arr[] and brr[]
    List<int> crr = new List<int>();

    // Store elements of array arr[]
    // and brr[] in the vector crr
    for(int i = 0; i < N; i++)
    {
        crr.Add(arr[i]);
    }
    for(int i = 0; i < K; i++)
    {
        crr.Add(brr[i]);
    }

    // Sort the vector crr
    // in descending order
    crr.Sort();
    crr.Reverse();

    // Stores maximum sum
    int sum = 0;

    // Calculate the sum till the last
    // index in crr[] which is less than
    // N which contains a positive element
    for(int i = 0; i < N; i++)
    {
        if (crr[i] > 0)
        {
            sum += crr[i];
        }
        else
        {
            break;
        }
    }

    // Print the sum
    Console.WriteLine(sum);
}

// Driver Code
static void Main()
{

    // Given arrays and respective lengths
    int[] arr = { 7, 2, -1, 4, 5 };
    int N = arr.Length;
    int[] brr = { 1, 2, 3, 2 };
    int K = brr.Length;

    // Calculate maximum subarray sum
    maxSum(arr, brr, N, K);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to find the maximum subarray sum
    // possible by swapping elements from array
    // arr[] with that from array brr[]
    function maxSum(arr, brr, N, K)
    {

        // Stores elements from the
        // arrays arr[] and brr[]
        let crr = [];

        // Store elements of array arr[]
        // and brr[] in the vector crr
        for(let i = 0; i < N; i++)
        {
            crr.push(arr[i]);
        }
        for(let i = 0; i < K; i++)
        {
            crr.push(brr[i]);
        }

        // Sort the vector crr
        // in descending order
        crr.sort(function(a, b){return a - b});
        crr.reverse();

        // Stores maximum sum
        let sum = 0;

        // Calculate the sum till the last
        // index in crr[] which is less than
        // N which contains a positive element
        for(let i = 0; i < N; i++)
        {
            if (crr[i] > 0)
            {
                sum += crr[i];
            }
            else
            {
                break;
            }
        }

        // Print the sum
        document.write(sum);
    }

    // Given arrays and respective lengths
    let arr = [ 7, 2, -1, 4, 5 ];
    let N = arr.length;
    let brr = [ 1, 2, 3, 2 ];
    let K = brr.length;

    // Calculate maximum subarray sum
    maxSum(arr, brr, N, K);

</script>
```

**Output:** 

```
21
```

***时间复杂度:*****O((N+K)* log(N+K))
***辅助空间:*** O(N+K)**