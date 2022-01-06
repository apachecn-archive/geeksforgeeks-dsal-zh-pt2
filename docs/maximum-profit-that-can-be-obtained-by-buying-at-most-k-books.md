# 最多买 K 本书可以获得的最大利润

> 原文:[https://www . geeksforgeeks . org/通过购买最多 k 本书可以获得的最大利润/](https://www.geeksforgeeks.org/maximum-profit-that-can-be-obtained-by-buying-at-most-k-books/)

给定一个整数 **K** 和一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，其中数组元素**arr【I】**代表 **i <sup>第</sup>** 本书的价格。购买 i <sup>的利润第</sup>本书代表**最大值(0，-1 * arr[i])** ，任务是通过最多购买 **K** 本书找到可能的最大利润。

**示例:**

> **输入:** arr[] = {-10，20，-30，50，-19}，K = 2
> **输出:** 49
> **说明:**
> 买书 arr[2](= -30)可以获得最大利润。利润= 30 和书，arr[4](= -19)为利润 19。
> 因此，获得的总最大利润为，(30+19 = 49)。
> 
> **输入:** arr[] = {10，20，16，25}，K = 3
> T3】输出: 0

**方法:**基于只有负价格的书籍才有助于最大利润的观察，使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决这个问题。按照以下步骤解决此问题:

*   [按升序排列数组 arr[]](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   初始化一个变量，比如说**最大利润**为 **0** 存储最大利润。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤:
    *   如果 **K** 大于 **0** 且**arr【I】**为负，则将**ABS(arr【I】)**加到**最大受益**上，然后将 **K** 的值减 **1。**
*   最后打印**最大利益**的值作为获得的最大利润。

下面是上述方法的实现:

## C++

```
// C++ program for above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// profit that can be obtained
// by buying at most K books
int maxProfit(int arr[], int N, int K)
{

    // Sort the array in
    // ascending order
    sort(arr, arr + N);

    // Stores the maximum profit
    int maxBenefit = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // If arr[i] is less than 0
        // and K is greater than 0
        if (arr[i] < 0 && K > 0) {

            // Increment the maxBenefit
            // by abs(arr[i])
            maxBenefit += abs(arr[i]);

            // Decrement K by 1
            K--;
        }
    }

    // Return the profit
    return maxBenefit;
}

// Driver Code
int main()
{

    // Given Input
    int arr[] = { -10, 20, -30, 50, -19 };
    int K = 2;
    int N = sizeof(arr) / sizeof(int);

    // Function call
    cout << maxProfit(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Arrays;

class GFG
{

  // Function to find the maximum
// profit that can be obtained
// by buying at most K books
    public static int maxProfit(int arr[], int N, int K)
    {

        // Sort the array in
        // ascending order
        Arrays.sort(arr);

        // Stores the maximum profit
        int maxBenefit = 0;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // If arr[i] is less than 0
            // and K is greater than 0
            if (arr[i] < 0 && K > 0) {

                // Increment the maxBenefit
                // by abs(arr[i])
                maxBenefit += Math.abs(arr[i]);

                // Decrement K by 1
                K--;
            }
        }

        // Return the profit
        return maxBenefit;
    }

// Driver Code
    public static void main(String[] args)
    {

      // Given input
        int arr[] = { -10, 20, -30, 50, -19 };
        int K = 2;
        int N = 5;

        // Function call
        int res = maxProfit(arr, N, K);
        System.out.println(res);
    }
}

// This code is contributed by lokeshpotta20.
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to find the maximum
# profit that can be obtained
# by buying at most K books
def maxProfit(arr, N, K):

    # Sort the array in
    # ascending order
    arr.sort()

    # Stores the maximum profit
    maxBenefit = 0

    # Traverse the array arr[]
    for i in range(0, N, 1):

        # If arr[i] is less than 0
        # and K is greater than 0
        if (arr[i] < 0 and K > 0):

            # Increment the maxBenefit
            # by abs(arr[i])
            maxBenefit += abs(arr[i])

            # Decrement K by 1
            K -= 1

    # Return the profit
    return maxBenefit

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ -10, 20, -30, 50, -19 ]
    K = 2
    N = len(arr)

    # Function call
    print(maxProfit(arr, N, K))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to find the maximum
    // profit that can be obtained
    // by buying at most K books
    public static int maxProfit(int[] arr, int N, int K)
    {

        // Sort the array in
        // ascending order
        Array.Sort(arr);

        // Stores the maximum profit
        int maxBenefit = 0;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // If arr[i] is less than 0
            // and K is greater than 0
            if (arr[i] < 0 && K > 0) {

                // Increment the maxBenefit
                // by abs(arr[i])
                maxBenefit += Math.Abs(arr[i]);

                // Decrement K by 1
                K--;
            }
        }

        // Return the profit
        return maxBenefit;
    }

    // Driver Code
    public static void Main()
    {

        // Given input
        int[] arr = { -10, 20, -30, 50, -19 };
        int K = 2;
        int N = 5;

        // Function call
        int res = maxProfit(arr, N, K);
        Console.Write(res);
    }
}

// This code is contributed by subhammahato348.
```

## java 描述语言

```
<script>
        // JavaScript program for above approach

        // Function to find the maximum
        // profit that can be obtained
        // by buying at most K books
        function maxProfit(arr, N, K) {

            // Sort the array in
            // ascending order
            arr.sort(function (a, b) { return a - b });
            // Stores the maximum profit
            var maxBenefit = 0;

            // Traverse the array arr[]
            for (let i = 0; i < N; i++) {

                // If arr[i] is less than 0
                // and K is greater than 0
                if (arr[i] < 0 && K > 0) {

                    // Increment the maxBenefit
                    // by abs(arr[i])
                    maxBenefit += Math.abs(arr[i]);

                    // Decrement K by 1
                    K--;
                }
            }

            // Return the profit
            return maxBenefit;
        }

        // Driver Code

        // Given Input
        var arr = [-10, 20, -30, 50, -19];
        var K = 2;
        var N = 5;

        // Function call
        document.write(maxProfit(arr, N, K));

// This code is contributed by lokeshpotta20.

    </script>
```

**Output:** 

```
49
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*