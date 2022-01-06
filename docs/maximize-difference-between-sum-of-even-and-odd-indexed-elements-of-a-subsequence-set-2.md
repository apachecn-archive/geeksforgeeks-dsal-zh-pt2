# 最大化子序列偶数和奇数索引元素之和的差值|集合 2

> 原文:[https://www . geeksforgeeks . org/最大化偶数和奇数索引元素之和-子序列集-2/](https://www.geeksforgeeks.org/maximize-difference-between-sum-of-even-and-odd-indexed-elements-of-a-subsequence-set-2/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是为数组的任意[子序列](http://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)找到偶数和奇数索引处元素的[和之间的最大差值。](https://www.geeksforgeeks.org/even-numbers-even-index-odd-numbers-odd-index/)

> **注意:**的 **N** 的值总是大于 **1。**

**示例:**

> ***输入:** arr[] = { 3，2，1，4，5，2，1，7，8，9 }*
> ***输出:** 15*
> ***解释:***
> *考虑子序列{ 3，1，5，1， 9 }从数组中*
> *偶数索引数组元素之和= 3 + 5 + 9 = 17*
> *奇数索引数组元素之和=是 1 + 1 = 2*
> *因此，子序列中存在的偶数和奇数索引元素之和之差=(17–2)= 15，这是最大可能。*
> 
> ***输入:** arr[] = {1，2，3，4，5，6}*
> ***输出:** 6*

**天真方法:**解决给定问题的简单方法是[生成给定数组](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)的所有可能子序列，并为每个子序列最大化偶数和奇数索引处元素之和之间的差异。检查所有子序列后，打印获得的最大值。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**局部最大值方法:**使用局部最大值和局部最小值[解决这个问题的方法将在本文](https://www.geeksforgeeks.org/maximize-difference-between-sum-of-even-and-odd-indexed-elements-of-a-subsequence/)中讨论。在本文中，我们讨论了动态编程方法。

**高效方法:**上述方法也可以使用[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)进行优化，因为上述方法具有[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)和[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。按照以下步骤解决给定的问题:

*   初始化大小为 **N** 的两个[数组](https://www.geeksforgeeks.org/array-data-structure/)、**dp1【】**和**dp2【】**，并用值 **-1** 初始化，使得**dp1【I】**存储从奇数长度的子序列直到第 **i <sup>第</sup>T15】索引的最大和，而**dp2【I】**存储从偶数长度的子序列的最大和**
*   将 **dp1[0]** 的值更新为 **arr[0]** ，将 **dp2[0]** 的值更新为 **0** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，并执行以下步骤:
    *   将 **dp1[i]** 的值更新为**dp1[I]= max(dp1[I–1]，dp2[I–1]+arr[I])**，因为带有元素的**将被追加到子序列中的偶数索引处。因此，添加了数组元素**arr【I】**。**
    *   将 **dp2[i]** 的值更新为**dp2[I]= max(dp2[I–1]，dp1[I–1]–arr[I])**，因为带有元素的**将被追加到子序列的奇数索引处。因此，阵列元素**arr【I】**被减去。**
*   执行上述步骤后，打印**(dp1[N–1]、dp2[N–1])**的最大值作为结果。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum value
// of difference between the sum of
// elements at even and odd indices of
// any subsequence of the array
void findMaximumPeakSum(int arr[], int n)
{
    // Initialize the two arrays
    int dp1[n], dp2[n];
    for (int i = 0; i < n; i++) {
        dp1[i] = -1;
        dp2[i] = -1;
    }
    dp2[0] = 0;
    dp1[0] = arr[0];

    // Iterate over the range
    for (int i = 1; i < n; i++) {

        // Find the maximum sum upto the
        // i-th odd and even subsequence
        dp1[i] = max(dp1[i - 1],
                     dp2[i - 1] + arr[i]);
        dp2[i] = max(dp2[i - 1],
                     dp1[i - 1] - arr[i]);
    }

    // Find the maximum value
    int ans = max(dp1[n - 1], dp2[n - 1]);

    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 1, 4, 5, 2, 1, 7, 8, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);

    findMaximumPeakSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum value
// of difference between the sum of
// elements at even and odd indices of
// any subsequence of the array
static void findMaximumPeakSum(int arr[], int n)
{

    // Initialize the two arrays
    int []dp1 = new int[n];
    int []dp2 = new int[n];
    for (int i = 0; i < n; i++) {
        dp1[i] = -1;
        dp2[i] = -1;
    }
    dp2[0] = 0;
    dp1[0] = arr[0];

    // Iterate over the range
    for (int i = 1; i < n; i++) {

        // Find the maximum sum upto the
        // i-th odd and even subsequence
        dp1[i] = Math.max(dp1[i - 1],
                     dp2[i - 1] + arr[i]);
        dp2[i] = Math.max(dp2[i - 1],
                     dp1[i - 1] - arr[i]);
    }

    // Find the maximum value
    int ans = Math.max(dp1[n - 1], dp2[n - 1]);

    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 2, 1, 4, 5, 2, 1, 7, 8, 9 };
    int N = arr.length;

    findMaximumPeakSum(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find the maximum value
# of difference between the sum of
# elements at even and odd indices of
# any subsequence of the array
def findMaximumPeakSum(arr, n):

    # Initialize the two arrays
    dp1 = [0] * n
    dp2 = [0] * n
    for i in range(n):
        dp1[i] = -1
        dp2[i] = -1

    dp2[0] = 0
    dp1[0] = arr[0]

    # Iterate over the range
    for i in range(1, n):

        # Find the maximum sum upto the
        # i-th odd and even subsequence
        dp1[i] = max(dp1[i - 1],
                     dp2[i - 1] + arr[i])
        dp2[i] = max(dp2[i - 1],
                     dp1[i - 1] - arr[i])

    # Find the maximum value
    ans = max(dp1[n - 1], dp2[n - 1])

    print(ans)

# Driver Code
arr = [3, 2, 1, 4, 5, 2, 1, 7, 8, 9]
N = len(arr)

findMaximumPeakSum(arr, N)

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

// Function to find the maximum value
// of difference between the sum of
// elements at even and odd indices of
// any subsequence of the array
static void findMaximumPeakSum(int []arr, int n)
{

    // Initialize the two arrays
    int []dp1 = new int[n];
    int []dp2 = new int[n];
    for (int i = 0; i < n; i++) {
        dp1[i] = -1;
        dp2[i] = -1;
    }
    dp2[0] = 0;
    dp1[0] = arr[0];

    // Iterate over the range
    for (int i = 1; i < n; i++) {

        // Find the maximum sum upto the
        // i-th odd and even subsequence
        dp1[i] = Math.Max(dp1[i - 1],
                     dp2[i - 1] + arr[i]);
        dp2[i] = Math.Max(dp2[i - 1],
                     dp1[i - 1] - arr[i]);
    }

    // Find the maximum value
    int ans = Math.Max(dp1[n - 1], dp2[n - 1]);

    Console.Write(ans);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 3, 2, 1, 4, 5, 2, 1, 7, 8, 9 };
    int N = arr.Length;

    findMaximumPeakSum(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to find the maximum value
       // of difference between the sum of
       // elements at even and odd indices of
       // any subsequence of the array
       function findMaximumPeakSum(arr, n) {
           // Initialize the two arrays
           let dp1 = new Array(n);
           let dp2 = new Array(n);
           for (let i = 0; i < n; i++) {
               dp1[i] = -1;
               dp2[i] = -1;
           }
           dp2[0] = 0;
           dp1[0] = arr[0];

           // Iterate over the range
           for (let i = 1; i < n; i++) {

               // Find the maximum sum upto the
               // i-th odd and even subsequence
               dp1[i] = Math.max(dp1[i - 1],
                   dp2[i - 1] + arr[i]);
               dp2[i] = Math.max(dp2[i - 1],
                   dp1[i - 1] - arr[i]);
           }

           // Find the maximum value
           let ans = Math.max(dp1[n - 1], dp2[n - 1]);

           document.write(ans);
       }

       // Driver Code
       let arr = [3, 2, 1, 4, 5, 2, 1, 7, 8, 9];
       let N = arr.length;

       findMaximumPeakSum(arr, N);

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
15
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**优化方法:**上述方法可以通过使用两个变量**奇数**和**偶数**来进一步优化，而不是两个数组**dp1【】**和**dp2【】**来保持偶数和奇数索引处元素之和的最大差异。对于每个索引 **i** ，只需要前一个索引的偶数和奇数长度[子序列](http://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最大和来计算当前状态。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum value
// of difference between the sum of
// elements at even and odd indices of
// any subsequence of the array
void findMaximumPeakSum(int arr[], int n)
{
    // Initialize the variables
    int even = 0;
    int odd = arr[0];

    // Iterat over the range
    for (int i = 1; i < n; i++) {

        // Find the maximum sum upto the
        // i-th odd and even subsequence
        int temp = odd;
        odd = max(odd, even + arr[i]);
        even = max(even, temp - arr[i]);
    }

    // Find the resultant maximum value
    int ans = max(odd, even);

    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 1, 4, 5, 2, 1, 7, 8, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);

    findMaximumPeakSum(arr, N);

    return 0;
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the maximum value
# of difference between the sum of
# elements at even and odd indices of
# any subsequence of the array
def findMaximumPeakSum(arr, n):

    # Initialize the variables
    even = 0
    odd = arr[0]

    # Iterat over the range
    for i in range(1,  n):

        # Find the maximum sum upto the
        # i-th odd and even subsequence
        temp = odd
        odd = max(odd, even + arr[i])
        even = max(even, temp - arr[i])

    # Find the resultant maximum value
    ans = max(odd, even)

    print(ans)

# Driver Code
if __name__ == "__main__":

    arr = [3, 2, 1, 4, 5, 2, 1, 7, 8, 9]
    N = len(arr)

    findMaximumPeakSum(arr, N)

    # This code is contributed by ukasp.
```

**Output**

```
15
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)