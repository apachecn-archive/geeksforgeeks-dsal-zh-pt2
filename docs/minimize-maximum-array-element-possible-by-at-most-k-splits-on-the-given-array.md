# 在给定的数组上最多通过 K 个拆分来最小化最大可能的数组元素

> 原文:[https://www . geeksforgeeks . org/minimum-max-array-element-by-至多-k-splits-on-the-给定数组/](https://www.geeksforgeeks.org/minimize-maximum-array-element-possible-by-at-most-k-splits-on-the-given-array/)

给定一个由 **N** 个正整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是通过将**个最多为 K 的**个数组元素拆分为两个与其值相等的数字，来最小化数组[个最大元素。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

**示例:**

> **输入:** arr[] = {2，4，8，2}，K = 4
> **输出:** 2
> **解释:**
> 需要执行以下操作顺序:
> **操作 1:** 将 arr[1] (= 4)拆分为{2，2}将数组修改为{2，2，2，8，2}。
> **操作 2:** 将 arr[3] (= 8)拆分为{2，6}将数组修改为{2，2，2，2，6，2}。
> **操作 3:** 将 arr[4] (= 6)拆分为{2，4}将数组修改为{2，2，2，2，2，2，4，2}。
> **操作 4:** 将 arr[5] (= 4)拆分为{2，2}会将数组修改为{2，2，2，2，2，2，2，2，2}。
> 完成上述操作后，数组中出现的最大元素为 2。
> 
> **输入:** arr[] = {7，17}，K = 2
> T3】输出: 7

**方法:**给定的问题可以基于以下观察来解决:

*   如果通过最多执行 **K** 运算 **X** 可以是数组**arr【】**T5】中的[最大元素，那么存在某个值 **K (K > X)** ，该值也可以是通过最多执行数组元素的 **K** 分裂而存在于数组**arr【】**](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)**中的[最大元素。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)**
*   **如果通过最多执行 **K** 运算 **X** 不能成为数组**A【】**中的最大元素，那么存在一些值 **K (K < X)** 通过最多执行数组元素的 **K** 拆分也不能成为数组**arr【】**中的最大元素。**
*   **所以思路是用[二分搜索法](https://www.geeksforgeeks.org/the-ubiquitous-binary-search-set-1/)寻找范围内的值**【1、**[**INT _ MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/)**，最多可以是**K**拆分后可能的最大值。****

****按照以下步骤解决问题:****

*   ****初始化两个变量，将**低**和**高**分别设为 **1** 和 [**数组中的最大元素 arr[]**](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) 。****
*   ****重复直到**低电平**小于**高电平**，并执行以下步骤:

    *   找到范围**【低，高】**的中间值作为**中间=(低+高)/2** 。
    *   初始化一个变量，比如**计数**，以存储使最大元素等于**中间**所需的数组元素的最大拆分数。
    *   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并将**计数**的值更新为**(arr[I]–1)/mid**以计算所需拆分的数量。
    *   如果**计数**的值最多为**K**，则将**高**的值更新为**中**。
    *   否则，将**低**的值更新为**(中+ 1)** 。**** 
*   ****完成上述步骤后，将**高值**打印为获得的数组中存在的合成[最大元素。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if all array
// elements can be reduced to at
// most mid by at most K splits
int possible(int A[], int N,
             int mid, int K)
{
    // Stores the number
    // of splits required
    int count = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Update count
        count += (A[i] - 1) / mid;
    }

    // If possible, return true.
    // Otherwise return false
    return count <= K;
}

// Function to find the minimum possible
// value of maximum array element that
// can be obtained by at most K splits
int minimumMaximum(int A[], int N, int K)
{
    // Set lower and upper limits
    int lo = 1;
    int hi = *max_element(A, A + N);
    int mid;

    // Perform Binary Search
    while (lo < hi) {

        // Calculate mid
        mid = (lo + hi) / 2;

        // Check if all array elements
        // can be reduced to at most
        // mid value by at most K splits
        if (possible(A, N, mid, K)) {

            // Update the value of hi
            hi = mid;
        }

        // Otherwise
        else {

            // Update the value of lo
            lo = mid + 1;
        }
    }

    // Return the minimized maximum
    // element in the array
    return hi;
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 8, 2 };
    int K = 4;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << minimumMaximum(arr, N, K);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if all array
// elements can be reduced to at
// most mid by at most K splits
static boolean possible(int A[], int N,
                        int mid, int K)
{

    // Stores the number
    // of splits required
    int count = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Update count
        count += (A[i] - 1) / mid;
    }

    // If possible, return true.
    // Otherwise return false
    return count <= K;
}

// Function to find the minimum possible
// value of maximum array element that
// can be obtained by at most K splits
static int minimumMaximum(int A[], int N, int K)
{

    // Set lower and upper limits
    int lo = 1;
    Arrays.sort(A);

    int hi = A[N - 1];
    int mid;

    // Perform Binary Search
    while (lo < hi)
    {

        // Calculate mid
        mid = (lo + hi) / 2;

        // Check if all array elements
        // can be reduced to at most
        // mid value by at most K splits
        if (possible(A, N, mid, K))
        {

            // Update the value of hi
            hi = mid;
        }

        // Otherwise
        else
        {

            // Update the value of lo
            lo = mid + 1;
        }
    }

    // Return the minimized maximum
    // element in the array
    return hi;
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 2, 4, 8, 2 };
    int K = 4;
    int N = arr.length;

    System.out.println(minimumMaximum(arr, N, K));
}
}

// This code is contributed by AnkThon**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach

# Function to check if all array
# elements can be reduced to at
# most mid by at most K splits
def possible(A, N, mid, K):

    # Stores the number
    # of splits required
    count = 0

    # Traverse the array arr[]
    for i in range(N):

        # Update count
        count += (A[i] - 1) // mid

    # If possible, return true.
    # Otherwise return false
    return count <= K

# Function to find the minimum possible
# value of maximum array element that
# can be obtained by at most K splits
def minimumMaximum(A, N, K):

    # Set lower and upper limits
    lo = 1
    hi = max(A)

    # Perform Binary Search
    while (lo < hi):

        # Calculate mid
        mid = (lo + hi) // 2

        # Check if all array elements
        # can be reduced to at most
        # mid value by at most K splits
        if (possible(A, N, mid, K)):

            # Update the value of hi
            hi = mid

        # Otherwise
        else:

            # Update the value of lo
            lo = mid + 1

    # Return the minimized maximum
    # element in the array
    return hi

# Driver Code
if __name__ == '__main__':

    arr =  [ 2, 4, 8, 2 ]
    K = 4
    N = len(arr)

    print(minimumMaximum(arr, N, K))

# This code is contributed by ipg2016107**
```

## ****C#****

```
**// C# program for the above approach
using System;

class GFG{

// Function to check if all array
// elements can be reduced to at
// most mid by at most K splits
static bool possible(int[] A, int N,
                     int mid, int K)
{

    // Stores the number
    // of splits required
    int count = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Update count
        count += (A[i] - 1) / mid;
    }

    // If possible, return true.
    // Otherwise return false
    return count <= K;
}

// Function to find the minimum possible
// value of maximum array element that
// can be obtained by at most K splits
static int minimumMaximum(int[] A, int N, int K)
{

    // Set lower and upper limits
    int lo = 1;
    Array.Sort(A);

    int hi = A[N - 1];
    int mid;

    // Perform Binary Search
    while (lo < hi)
    {

        // Calculate mid
        mid = (lo + hi) / 2;

        // Check if all array elements
        // can be reduced to at most
        // mid value by at most K splits
        if (possible(A, N, mid, K))
        {

            // Update the value of hi
            hi = mid;
        }

        // Otherwise
        else
        {

            // Update the value of lo
            lo = mid + 1;
        }
    }

    // Return the minimized maximum
    // element in the array
    return hi;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 2, 4, 8, 2 };
    int K = 4;
    int N = arr.Length;

    Console.WriteLine(minimumMaximum(arr, N, K));
}
}

// This code is contributed by ukasp**
```

## ****java 描述语言****

```
**<script>

// javascript program for the above approach

// Function to check if all array
// elements can be reduced to at
// most mid by at most K splits

function possible(A, N, mid, K)
{

    // Stores the number
    // of splits required
    var count = 0;

     var i;
    // Traverse the array arr[]
    for (i = 0; i < N; i++) {

        // Update count
        count += Math.floor((A[i] - 1) / mid);
    }

    // If possible, return true.
    // Otherwise return false
    if(count <= K)
      return true;
    else
      return false
}

// Function to find the minimum possible
// value of maximum array element that
// can be obtained by at most K splits
function minimumMaximum(A, N, K)
{

    // Set lower and upper limits
    var lo = 1;
    var hi = Math.max.apply(Math,A);
    var mid;

    // Perform Binary Search
    while (lo < hi) {

        // Calculate mid
        mid = Math.floor((lo + hi) / 2);

        // Check if all array elements
        // can be reduced to at most
        // mid value by at most K splits
        if (possible(A, N, mid, K)) {

            // Update the value of hi
            hi = mid;
        }

        // Otherwise
        else {

            // Update the value of lo
            lo = mid + 1;
        }
    }

    // Return the minimized maximum
    // element in the array
    return hi;
}

// Driver Code
    var arr = [2, 4, 8, 2];
    var K = 4;
    var N = arr.length;

    document.write(minimumMaximum(arr, N, K));

// This code is contributed by SURENDRA_GANGWAR.
</script>**
```

******Output:** 

```
2
```**** 

*******时间复杂度:** O(N * log M)，其中 M 为* [*阵的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(1)*****