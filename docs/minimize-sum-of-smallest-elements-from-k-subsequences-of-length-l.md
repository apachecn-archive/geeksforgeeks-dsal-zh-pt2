# 最小化长度为 L 的 K 个子序列中最小元素的和

> 原文:[https://www . geeksforgeeks . org/minimum-sum-of-minimum-elements-from-k-sequence-of-length-l/](https://www.geeksforgeeks.org/minimize-sum-of-smallest-elements-from-k-subsequences-of-length-l/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是通过从长度为 **L** 的 **arr[]** 的任何 **K** 子序列中提取最小元素来找到最小可能和，使得每个子序列没有共享元素。如果无法获得所需的总和，请打印-1。

**示例:**

> **输入:** arr[] = {2，15，5，1，35，16，67，10}，K = 3，L = 2
> **输出:** 8
> **说明:**
> 长度为 2 的三个子序列可以是{1，35}、{2，15}、{5，16}
> 最小元素为{1，35 } 1。
> 最小元素{2，15}为 2。
> 最小元素{5，16}为 5。
> 它们的和等于 8，这是最小可能值。
> 
> **输入:** arr[] = {19，11，21，16，22，18，14，12}，K = 3，L = 3
> **输出:** -1
> **解释:**
> 不可能从 arr[]，构造 3 个长度为 3 的子序列。

**进场:**
要优化以上进场，我们需要观察以下细节:

*   数组的最小元素有助于找到 K 个子序列的最小元素的最小和。
*   为了形成长度为 L 的 K 个子序列，数组的长度必须大于或等于(K * L)

按照以下步骤解决问题:

*   检查数组 **arr[]** 的大小是否大于等于 **(K * L)** 。
*   如果是，对数组 **arr[]** 进行排序，排序后打印数组第一个 **K** 元素的和。
*   否则，返回-1。

下面是上述方法的实现:

## C++

```
// C++ Program to find the minimum
// possible sum of the smallest
// elements from K subsequences

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum sum
int findMinSum(int arr[], int K,
               int L, int size)
{

    if (K * L > size)
        return -1;

    int minsum = 0;

    // Sort the array
    sort(arr, arr + size);

    // Calculate sum of smallest
    // K elements
    for (int i = 0; i < K; i++)
        minsum += arr[i];

    // Return the sum
    return minsum;
}

// Driver Code
int main()
{
    int arr[] = { 2, 15, 5, 1,
                  35, 16, 67, 10 };
    int K = 3;
    int L = 2;

    int length = sizeof(arr)
                / sizeof(arr[0]);

    cout << findMinSum(arr, K,
                       L, length);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// possible sum of the smallest
// elements from K subsequences
import java.util.Arrays;

class GFG{

// Function to find the minimum sum
static int findMinSum(int []arr, int K,
                      int L, int size)
{
    if (K * L > size)
        return -1;

    int minsum = 0;

    // Sort the array
    Arrays.sort(arr);

    // Calculate sum of smallest
    // K elements
    for(int i = 0; i < K; i++)
        minsum += arr[i];

    // Return the sum
    return minsum;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 2, 15, 5, 1,
                  35, 16, 67, 10 };
    int K = 3;
    int L = 2;
    int length = arr.length;

    System.out.print(findMinSum(arr, K,
                                L, length));
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# possible sum of the smallest
# elements from K subsequences

# Function to find the minimum sum

def findMinSum(arr, K, L, size):

    if (K * L > size):
        return -1

    minsum = 0

    # Sort the array
    arr.sort()

    # Calculate sum of smallest
    # K elements
    for i in range(K):
        minsum += arr[i]

    # Return the sum
    return minsum

# Driver code
if __name__ == '__main__':

    arr = [2, 15, 5, 1,
           35, 16, 67, 10]
    K = 3
    L = 2

    length = len(arr)

    print(findMinSum(arr, K, L, length))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to find the minimum
// possible sum of the smallest
// elements from K subsequences
using System;

class GFG{

// Function to find the minimum sum
static int findMinSum(int []arr, int K,
                      int L, int size)
{
    if (K * L > size)
        return -1;

    int minsum = 0;

    // Sort the array
    Array.Sort(arr); 

    // Calculate sum of smallest
    // K elements
    for(int i = 0; i < K; i++)
        minsum += arr[i];

    // Return the sum
    return minsum;
}

// Driver Code
public static void Main() 
{
    int[] arr = { 2, 15, 5, 1,
                  35, 16, 67, 10 };
    int K = 3;
    int L = 2;
    int length = arr.Length;

    Console.Write(findMinSum(arr, K,
                             L, length));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
// Javascript program to find the minimum
// possible sum of the smallest
// elements from K subsequences

// Function to find the minimum sum
function findMinSum(arr, K, L, size)
{
    if (K * L > size)
        return -1;

    let minsum = 0;

    // Sort the array
    arr.sort((a, b) => a - b);

    // Calculate sum of smallest
    // K elements
    for(let i = 0; i < K; i++)
        minsum += arr[i];

    // Return the sum
    return minsum;
}

    // Driver Code

    let arr = [ 2, 15, 5, 1,
                  35, 16, 67, 10 ];
    let K = 3;
    let L = 2;
    let length = arr.length;

   document.write(findMinSum(arr, K,
                                L, length));

</script>
```

**Output**

```
8
```

***时间复杂度:** O(N * log(N))*
***空间复杂度:** O(1)*