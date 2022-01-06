# 卖票后利润最大化|第 2 集(针对范围[1，10^6]内的元素)

> 原文:[https://www . geeksforgeeks . org/卖票后利润最大化-set-2/](https://www.geeksforgeeks.org/maximize-the-profit-after-selling-the-tickets-set-2/)

给定一个数组，大小为 **N** 的 **arr[]** ，其中 arr[i]代表门票数量，第 I 个卖家有一个正整数 **K** 。票的价格是卖票人剩余的票的数量。他们总共可以卖出 **K** 的票。找到他们卖 K 票能赚到的最大金额。以 **10 <sup>9</sup> + 7 为模给出答案。**

**示例:**

> **输入:**席[] = {2，1，1}，K= 3
> **输出:** 4
> **说明:**考虑基于 0 的索引。前两轮，第二个卖家卖出。第三个回合，第 0 或第 2 个卖家都可以卖出。所以总数变成了 6 + 5 + 4 = 15。
> 
> **输入:**席[] = {2，3，4，5，1}，K = 6
> T3】输出: 22

**方法:**幼稚的方法和高效的方法在这篇[文章](https://www.geeksforgeeks.org/maximize-the-profit-after-selling-the-tickets/)中讨论。
文章中提到的方法可以通过观察来进一步优化，因为所有元素的**都小于或等于 10^6** ，因此，我们可以将所有元素的[频率存储在一个数组](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/) A[]中。按照以下步骤解决问题:

*   创建一个数组 **A[]** ，存储数组中每个元素的频率 **arr[]** 。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并将**A【arr[I]】**的值增加 **1** 。
*   初始化一个变量，比如说 **j** 来跟踪数组元素的位置。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，1000000】**中迭代，并执行以下步骤:
    *   而 **A[i]！= 0** ，将**arr【j】**的值修改为 I，并将**A【I】**的值递减 **1** 。
*   初始化两个变量，说 **i** 为 **N-1** 和 **j** 为 **N-2** 。
*   初始化一个变量，说 **ans** 为 **0** 。
*   当 **k > 0** 和 **j > =0** 时迭代，并执行以下步骤:
    1.  如果**arr【I】>arr【j】**，
        *   然后在答案中加上 **min(K，i-j)*arr[i]** 。
        *   将 **K** 的值减 **i-j** 并将 arr【I】的值减 1。
    2.  否则，
        *   当 **arr[j] = arr[i]** 时，递减 **j** 的值。
        *   然后将 **min(K，I-j)* arr【I】**添加到答案 **ans** 中。
        *   将 **K** 的值减 **i-j** 并将 arr【I】的值减 1。
*   在 **K > 0** 和**arr【I】>0**时迭代，并执行以下步骤:
    *   然后将 **min(K，N)*arr[i]** 添加到答案**和**中。
    *   将 **K** 的值减 **N** 并将 arr【I】的值减 1。
*   执行上述步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum profit
// after selling K tickets
int maxAmount(int n, int k, int arr[])
{
    // Frequency array to store freq
    // of every element of the array
    int A[1000001] = { 0 };
    for (int i = 0; i < n; i++) {
        A[arr[i]]++;
    }

    int j = 0;
    // Modify the arr[] so that the
    // array is sorted in O(N)
    for (int i = 0; i < 1000001; i++) {
        while (A[i] != 0) {
            arr[j++] = i;
            A[i]--;
        }
    }

    // Variable to store answer
    long long int ans = 0;
    int mod = 1e9 + 7;
    int i = n - 1;
    j = n - 2;

    // Traverse the array while K>0
    // and j>=0
    while (k > 0 && j >= 0) {

        // If arr[i] > arr[j] then
        // ticket can be brought from
        // counter [j+1, N]
        if (arr[i] > arr[j]) {
            ans = ans + min(k, (i - j)) * arr[i];
            k = k - (i - j);
            arr[i]--;
        }
        else {

            // If arr[j] == arr[i] decrement j until
            // arr[j] != arr[i]
            while (j >= 0 && arr[j] == arr[i])
                j--;
            if (j < 0)
                break;

            // Sell tickets from counter [j+1, N]
            ans = ans + min(k, (i - j)) * arr[i];
            k = k - (i - j);
            arr[i]--;
        }
    }

    // All elements of array are equal
    // Send tickets from each counter 1
    // time until K > 0.
    while (k > 0 && arr[i] != 0) {
        ans = ans + min(n, k) * arr[i];
        k -= n;
        arr[i]--;
    }
    ans = ans % mod;

    // Converting answer from long long
    // to int
    int x = ans;
    return x;
}

// Driver Code
int main()
{
    // Given Input
    int n = 5;
    int k = 3;
    int arr[n] = { 4, 3, 6, 2, 4 };

    // Function Call
    int ans = maxAmount(n, k, arr);
    cout << ans;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find maximum profit
// after selling K tickets
static int maxAmount(int n, int k, int arr[])
{
    // Frequency array to store freq
    // of every element of the array
    int A[] = new int[1000001];
    for (int i = 0; i < n; i++) {
        A[arr[i]]++;
    }

    int j = 0;

    // Modify the arr[] so that the
    // array is sorted in O(N)
    for (int i = 0; i < 1000001; i++) {
        while (A[i] != 0) {
            arr[j++] = i;
            A[i]--;
        }
    }

    // Variable to store answer
    int ans = 0;
    int mod = (int) (1e9 + 7);
    int i = n - 1;
    j = n - 2;

    // Traverse the array while K>0
    // and j>=0
    while (k > 0 && j >= 0) {

        // If arr[i] > arr[j] then
        // ticket can be brought from
        // counter [j+1, N]
        if (arr[i] > arr[j]) {
            ans = ans + Math.min(k, (i - j)) * arr[i];
            k = k - (i - j);
            arr[i]--;
        }
        else {

            // If arr[j] == arr[i] decrement j until
            // arr[j] != arr[i]
            while (j >= 0 && arr[j] == arr[i])
                j--;
            if (j < 0)
                break;

            // Sell tickets from counter [j+1, N]
            ans = ans + Math.min(k, (i - j)) * arr[i];
            k = k - (i - j);
            arr[i]--;
        }
    }

    // All elements of array are equal
    // Send tickets from each counter 1
    // time until K > 0.
    while (k > 0 && arr[i] != 0) {
        ans = ans + Math.min(n, k) * arr[i];
        k -= n;
        arr[i]--;
    }
    ans = ans % mod;

    // Converting answer from long long
    // to int
    int x = ans;
    return x;
}

// Driver Code
public static void main(String[] args)
{
    // Given Input
    int n = 5;
    int k = 3;
    int arr[] = { 4, 3, 6, 2, 4 };

    // Function Call
    int ans = maxAmount(n, k, arr);
    System.out.print(ans);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find maximum profit
# after selling K tickets
def maxAmount(n, k, arr):

    # Frequency array to store freq
    # of every element of the array
    A = [0 for i in range(1000001)]
    for i in range(n):
        A[arr[i]] += 1

    j = 0

    # Modify the arr[] so that the
    # array is sorted in O(N)
    for j in range(1000001):
        while(A[i] != 0):
            arr[j] = i;
            j += 1
            A[i] -= 1

    # Variable to store answer
    ans = 6
    mod = 1000000007
    i = n - 1
    j = n - 2

    # Traverse the array while K>0
    # and j>=0
    while (k > 0 and j >= 0):

        # If arr[i] > arr[j] then
        # ticket can be brought from
        # counter [j+1, N]
        if (arr[i] > arr[j]):
            ans = ans + min(k, (i - j)) * arr[i]
            k = k - (i - j)
            arr[i] -= 1
        else:

            # If arr[j] == arr[i] decrement j until
            # arr[j] != arr[i]
            while (j >= 0 and arr[j] == arr[i]):
                j -= 1

            if (j < 0):
                break

            # Sell tickets from counter [j+1, N]
            ans = ans + min(k, (i - j)) * arr[i]
            k = k - (i - j)
            arr[i] -= 1

    # All elements of array are equal
    # Send tickets from each counter 1
    # time until K > 0.
    while (k > 0 and arr[i] != 0):
        ans = ans + min(n, k) * arr[i]
        k -= n
        arr[i] -= 1

    ans = ans % mod

    # Converting answer from long long
    # to int
    x = ans
    return x

# Driver Code
if __name__ == '__main__':

    # Given Input
    n = 5
    k = 3
    arr = [ 4, 3, 6, 2, 4 ]

    # Function Call
    ans = maxAmount(n, k, arr)
    print(ans)

# This code is contributed by avijitmondal1998
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find maximum profit
// after selling K tickets
static int maxAmount(int n, int k, int []arr)
{
    // Frequency array to store freq
    // of every element of the array
  int i;
    int []A = new int[1000001];
    Array.Clear(A,0,1000001);
    for (i = 0; i < n; i++) {
        A[arr[i]]++;
    }

    int j = 0;
    // Modify the arr[] so that the
    // array is sorted in O(N)
    for (i = 0; i < 1000001; i++) {
        while (A[i] != 0) {
            arr[j++] = i;
            A[i]--;
        }
    }

    // Variable to store answer
    int ans = 0;
    int mod = 1000000007;
    i = n - 1;
    j = n - 2;

    // Traverse the array while K>0
    // and j>=0
    while (k > 0 && j >= 0) {

        // If arr[i] > arr[j] then
        // ticket can be brought from
        // counter [j+1, N]
        if (arr[i] > arr[j]) {
            ans = ans + Math.Min(k, (i - j)) * arr[i];
            k = k - (i - j);
            arr[i]--;
        }
        else {

            // If arr[j] == arr[i] decrement j until
            // arr[j] != arr[i]
            while (j >= 0 && arr[j] == arr[i])
                j--;
            if (j < 0)
                break;

            // Sell tickets from counter [j+1, N]
            ans = ans + Math.Min(k, (i - j)) * arr[i];
            k = k - (i - j);
            arr[i]--;
        }
    }

    // All elements of array are equal
    // Send tickets from each counter 1
    // time until K > 0.
    while (k > 0 && arr[i] != 0) {
        ans = ans + Math.Min(n, k) * arr[i];
        k -= n;
        arr[i]--;
    }
    ans = ans % mod;

    // Converting answer from long long
    // to int
    int x = ans;
    return x;
}

// Driver Code
public static void Main()
{
    // Given Input
    int n = 5;
    int k = 3;
    int []arr = { 4, 3, 6, 2, 4 };

    // Function Call
    int ans = maxAmount(n, k, arr);
    Console.Write(ans);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
   <script>
        // JavaScript program for the above approach;

        // Function to find maximum profit
        // after selling K tickets
        function maxAmount(n, k, arr)
        {

            // Frequency array to store freq
            // of every element of the array
            let A = new Array(1000001).fill(0);
            for (let i = 0; i < n; i++)
            {
                A[arr[i]]++;
            }

            let j = 0;

            // Modify the arr[] so that the
            // array is sorted in O(N)
            for (let i = 0; i < 1000001; i++) {
                while (A[i] != 0) {
                    arr[j++] = i;
                    A[i]--;
                }
            }

            // Variable to store answer
            let ans = 0;
            let mod = 1e9 + 7;
            let i = n - 1;
            j = n - 2;

            // Traverse the array while K>0
            // and j>=0
            while (k > 0 && j >= 0) {

                // If arr[i] > arr[j] then
                // ticket can be brought from
                // counter [j+1, N]
                if (arr[i] > arr[j]) {
                    ans = ans + Math.min(k, (i - j)) * arr[i];
                    k = k - (i - j);
                    arr[i]--;
                }
                else {

                    // If arr[j] == arr[i] decrement j until
                    // arr[j] != arr[i]
                    while (j >= 0 && arr[j] == arr[i])
                        j--;
                    if (j < 0)
                        break;

                    // Sell tickets from counter [j+1, N]
                    ans = ans + Math.min(k, (i - j)) * arr[i];
                    k = k - (i - j);
                    arr[i]--;
                }
            }

            // All elements of array are equal
            // Send tickets from each counter 1
            // time until K > 0.
            while (k > 0 && arr[i] != 0) {
                ans = ans + Math.min(n, k) * arr[i];
                k -= n;
                arr[i]--;
            }
            ans = ans % mod;

            // Converting answer from long long
            // to let
            let x = ans;
            return x;
        }

        // Driver Code

        // Given Input
        let n = 5;
        let k = 3;
        let arr = [4, 3, 6, 2, 4];

        // Function Call
        let ans = maxAmount(n, k, arr);
        document.write(ans);

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
15
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)