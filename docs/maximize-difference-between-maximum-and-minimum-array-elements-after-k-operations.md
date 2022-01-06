# K 次运算后最大和最小数组元素之差最大化

> 原文:[https://www . geesforgeks . org/max-k-operations 后的最大和最小数组元素之差/](https://www.geeksforgeeks.org/maximize-difference-between-maximum-and-minimum-array-elements-after-k-operations/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个正整数 **K** ，任务是通过将数组元素递增或递减 **1** 、 **K** 次，找到数组中[最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)和[最小元素](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)之间的最大差值。

**示例:**

> **输入:** arr[] = {7，7，7，7}，K = 1
> **输出:** 14
> **解释:**将 arr[0]的值减 1，将 arr[3]的值加 7 会修改 arr[] = {0，7，7，14}。因此，数组中最大元素和最小元素之间的最大差值是 14
> 
> **输入:** arr[] = {0，0，0，0，0}，K = 2
> **输出:** 0
> **解释:**由于所有数组元素都是 0，任何数组元素递减都会使该元素小于 0。因此，所需的输出为 0。

**方法:**按照以下步骤解决问题:

*   [按降序排列数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)计算前 K 个最大元素的和。
*   最后打印出[第一个 K 个数组最大元素](https://www.geeksforgeeks.org/k-largestor-smallest-elements-in-an-array/)的和。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum difference
// between the maximum and minimum in the
// array after K operations
int maxDiffLargSmallOper(int arr[],
                         int N, int K)
{
    // Stores maximum difference between
    // largest  and smallest array element
    int maxDiff = 0;

    // Sort the array in descending order
    sort(arr, arr + N, greater<int>());

    // Traverse the array arr[]
    for (int i = 0; i <= min(K, N - 1);
         i++) {

        // Update maxDiff
        maxDiff += arr[i];
    }

    return maxDiff;
}

// Driver Code
int main()
{

    int arr[] = { 7, 7, 7, 7 };
    int N = sizeof(arr)
            / sizeof(arr[0]);
    int K = 1;
    cout << maxDiffLargSmallOper(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Reverse array
static int[] reverse(int a[])
{
    int i, n = a.length, t;
    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Function to find the maximum difference
// between the maximum and minimum in the
// array after K operations
static int maxDiffLargSmallOper(int arr[],
                                int N, int K)
{

    // Stores maximum difference between
    // largest  and smallest array element
    int maxDiff = 0;

    // Sort the array in descending order
    Arrays.sort(arr);
    arr = reverse(arr);

    // Traverse the array arr[]
    for(int i = 0; i <= Math.min(K, N - 1); i++)
    {

        // Update maxDiff
        maxDiff += arr[i];
    }

    return maxDiff;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 7, 7, 7, 7 };
    int N = arr.length;
    int K = 1;

    System.out.print(maxDiffLargSmallOper(arr, N, K));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum difference
# between the maximum and minimum in the
# array after K operations
def maxDiffLargSmallOper(arr, N, K):

    # Stores maximum difference between
    # largest  and smallest array element
    maxDiff = 0;

    # Sort the array in descending order
    arr.sort(reverse = True);

    # Traverse the array arr[]
    for i  in  range(min(K + 1, N)):

        # Update maxDiff
        maxDiff += arr[i];

    return maxDiff;

# Driver Code
if __name__ == "__main__": 

    arr = [ 7, 7, 7, 7 ];
    N = len(arr)
    K = 1;
    print(maxDiffLargSmallOper(arr, N, K));
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the maximum difference
// between the maximum and minimum in the
// array after K operations
static int maxDiffLargSmallOper(int []arr, int N,
                                int K)
{

    // Stores maximum difference between
    // largest and smallest array element
    int maxDiff = 0;

    // Sort the array in descending order
    Array.Sort(arr);
    Array.Reverse(arr);

    // Traverse the array arr[]
    for(int i = 0; i <= Math.Min(K, N - 1); i++)
    {

        // Update maxDiff
        maxDiff += arr[i];
    }
    return maxDiff;
}

// Driver code
public static void Main()
{
    int [] arr = new int[]{ 7, 7, 7, 7 };
    int N = arr.Length;
    int K = 1;

    Console.Write(maxDiffLargSmallOper(arr, N, K));
}
}

// This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Reverse array
function reverse(a)
{
    var i, n = a.length, t;
    for(i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Function to find the maximum difference
// between the maximum and minimum in the
// array after K operations
function maxDiffLargSmallOper(arr, N, K)
{

    // Stores maximum difference between
    // largest and smallest array element
    var maxDiff = 0;

    // Sort the array in descending order
    arr.sort();
    arr = reverse(arr);

    // Traverse the array arr
    for(i = 0; i <= Math.min(K, N - 1); i++)
    {

        // Update maxDiff
        maxDiff += arr[i];
    }
    return maxDiff;
}

// Driver Code
var arr = [ 7, 7, 7, 7 ];
var N = arr.length;
var K = 1;

document.write(maxDiffLargSmallOper(arr, N, K));

// This code is contributed by aashish1995

</script>
```

**Output:** 

```
14
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*