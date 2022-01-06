# 将最大和最小数组元素之间的差异精确地缩小 K 倍

> 原文:[https://www . geeksforgeeks . org/最小化最大和最小数组元素之间的差异精确 k-removes/](https://www.geeksforgeeks.org/minimize-difference-between-maximum-and-minimum-array-elements-by-exactly-k-removals/)

给定一个由 **N** 个正整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是在精确移除 **K** 个元素后，最小化给定数组[个最大和最小元素之间的差异。](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)

**示例:**

> **输入:** arr[] = {5，1，6，7，12，10}，K = 3
> **输出:** 2
> **解释:**
> 从给定数组中移除元素 12，10 和 1。
> 数组修改为{5，6，7}。
> 最小和最大元素之差为 7–5 = 2。
> 
> **输入:** arr[] = {14，5，61，10，21，12，54}，K = 4
> **输出:** 4
> **解释:**
> 从给定数组中移除元素 61，54，5 和 21。
> 数组修改为{14，10，12}。
> 最小和最大元素之差为 14–10 = 4。

**方法:**解决给定问题的思路是通过移除数组中的最小元素或数组中的[最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)来最小化差异。按照以下步骤解决问题:

*   [按升序排列数组**arr[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   初始化变量**左= 0** 和**右=(N–1)**。
*   迭代 **K** 次，根据以下条件将最大值或最小值改为 0:
    *   如果**arr[right–1]–arr[left]**<**arr[right]–arr[left+1]**，则通过 **1** 将 **arr[right]** 更改为 **0** 和**递减**右指针。
    *   否则，将**改为【左】**为 **0** ，**将左指针增加 **1** 。**
*   经过上述步骤后，**左侧**和**右侧**指标处的元素之间的差值即为所需的最小差值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to minimize the difference
// of the maximum and minimum array
// elements by removing K elements
void minimumRange(int arr[], int N, int K)
{
    // Base Condition
    if (K >= N)
    {
        cout << 0;
        return;
    }

    // Sort the array
    sort(arr, arr + N);

    // Initialize left and right pointers
    int left = 0, right = N - 1, i;

    // Iterate for K times
    for (i = 0; i < K; i++)
    {

        // Removing right element
        // to reduce the difference
        if (arr[right - 1] - arr[left]
            < arr[right] - arr[left + 1])
            right--;

        // Removing the left element
        // to reduce the difference
        else
            left++;
    }

    // Print the minimum difference
    cout << arr[right] - arr[left];
}

// Driver Code
int main()
{
    int arr[] = { 5, 10, 12, 14, 21, 54, 61 };
    int N = sizeof(arr) / sizeof(arr[0]);

    int K = 4;

    // Function Call
    minimumRange(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to minimize the difference
// of the maximum and minimum array
// elements by removing K elements
static void minimumRange(int arr[], int N,
                         int K)
{

    // Base Condition
    if (K >= N)
    {
        System.out.print(0);
        return;
    }

    // Sort the array
    Arrays.sort(arr);

    // Initialize left and right pointers
    int left = 0, right = N - 1, i;

    // Iterate for K times
    for(i = 0; i < K; i++)
    {

        // Removing right element
        // to reduce the difference
        if (arr[right - 1] - arr[left] <
            arr[right] - arr[left + 1])
            right--;

        // Removing the left element
        // to reduce the difference
        else
            left++;
    }

    // Print the minimum difference
    System.out.print(arr[right] - arr[left]);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, 10, 12, 14, 21, 54, 61 };
    int N = arr.length;
    int K = 4;

    // Function Call
    minimumRange(arr, N, K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to minimize the difference
# of the maximum and minimum array
# elements by removing K elements
def minimumRange(arr, N, K) :

    # Base Condition
    if (K >= N) :
        print(0, end = '');
        return;

    # Sort the array
    arr.sort();

    # Initialize left and right pointers
    left = 0; right = N - 1;

    # Iterate for K times
    for i in range(K) :

        # Removing right element
        # to reduce the difference
        if (arr[right - 1] - arr[left] < arr[right] - arr[left + 1]) :
            right -= 1;

        # Removing the left element
        # to reduce the difference
        else :
            left += 1;

    # Print the minimum difference
    print(arr[right] - arr[left], end = '');

# Driver Code
if __name__ == "__main__" :

    arr = [ 5, 10, 12, 14, 21, 54, 61 ];
    N = len(arr);

    K = 4;

    # Function Call
    minimumRange(arr, N, K);

    # This code is contributed by AnkitRai01
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to minimize the difference
// of the maximum and minimum array
// elements by removing K elements
static void minimumRange(int []arr, int N,
                         int K)
{

    // Base Condition
    if (K >= N)
    {
        Console.Write(0);
        return;
    }

    // Sort the array
    Array.Sort(arr);

    // Initialize left and right pointers
    int left = 0, right = N - 1, i;

    // Iterate for K times
    for(i = 0; i < K; i++)
    {

        // Removing right element
        // to reduce the difference
        if (arr[right - 1] - arr[left] <
            arr[right] - arr[left + 1])
            right--;

        // Removing the left element
        // to reduce the difference
        else
            left++;
    }

    // Print the minimum difference
    Console.Write(arr[right] - arr[left]);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 5, 10, 12, 14, 21, 54, 61 };
    int N = arr.Length;
    int K = 4;

    // Function Call
    minimumRange(arr, N, K);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to minimize the difference
// of the maximum and minimum array
// elements by removing K elements
function minimumRange(arr, N, K)
{
    // Base Condition
    if (K >= N)
    {
        document.write( 0);
        return;
    }

    // Sort the array
    arr.sort((a,b)=> a-b);

    // Initialize left and right pointers
    var left = 0, right = N - 1, i;

    // Iterate for K times
    for (i = 0; i < K; i++)
    {

        // Removing right element
        // to reduce the difference
        if (arr[right - 1] - arr[left]
            < arr[right] - arr[left + 1])
            right--;

        // Removing the left element
        // to reduce the difference
        else
            left++;
    }

    // Print the minimum difference
    document.write( arr[right] - arr[left]);
}

// Driver Code
var arr = [5, 10, 12, 14, 21, 54, 61];
var N = arr.length;
var K = 4;

// Function Call
minimumRange(arr, N, K);

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*