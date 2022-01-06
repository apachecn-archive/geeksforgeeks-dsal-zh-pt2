# 最大化所有 I 的数组和，除了来自[i，i+X]的元素，使得 arr[i] > K

> 原文:[https://www . geesforgeks . org/maximize-array-sum-except-elements-from-I-IX-for-all-I-so-arri-k/](https://www.geeksforgeeks.org/maximize-array-sum-except-elements-from-i-ix-for-all-i-such-that-arri-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和两个整数 **X** 和 **K** ，任务是通过重新排列数组的元素找到可以达到的最大得分，其中得分被计算为数组元素的总和，除了索引 **i** 中的下一个 **X** 元素，例如**arr【I】****>**

**示例:**

> **输入:** arr[] = {9，13，16，21，6}，X = 2，K = 15
> **输出:** 50
> **说明:**给定数组可以重新排列为 arr[] = {16，6，9，13，21}。使得 arr[i] > K 为{0，4}的指数。因此，索引 0 和索引 4 的下两个元素将被映射。因此，剩余元素的总和变为 16 + 13 + 21 = 50，这是最大可能值。
> 
> **输入:** arr[] = {31，20，19，23，34，21，37}，X = 3，K= 22
> **输出:** 112

**方法:**给定的问题可以用[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。创建两个包含大于 **K** 的整数的[数组](https://www.geeksforgeeks.org/array-data-structure/)、**大[]** 和包含小于 **K** 的整数的**小[]** 。可以观察到，如果总和中必须包含的大于 **K** 的元素个数为 **i** ，那么数组中至少要存在**(I 1)(X+1)+1**个元素。因此，对于每个可能的 I，从总的**和**中排除(**(I 1)(X+1)+1**)**–I**小数组的最小元素。每个 **i** 的所有可能和的最大值是要求的结果。

下面是上述方法的实现:

## C++

```
// C++ program, for the above approach
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e5;

// Utility function to calculate the
// sum of elements as a prefix array
void calc(int arr[], int N)
{
    sort(arr + 1, arr + N + 1);
    reverse(arr + 1, arr + N + 1);

    for (int i = 1; i <= N; i++) {
        arr[i] += arr[i - 1];
    }
}

// Function to find the maximum score
// that can be achieved by rearranging
// the elements of given array
int maxScore(int arr[], int X, int K, int N)
{
    // Arrays to store small and big elements
    int small[maxn + 5], big[maxn + 5];
    int k = 0, l = 0;

    // Iterate and segregate big and
    // small elements
    for (int i = 0; i < N; i++) {
        if (arr[i] > K) {
            big[++k] = arr[i];
        }
        else {
            small[++l] = arr[i];
        }
    }
    // If k = 0, return the sum
    // of small[]
    if (k == 0) {
        int sum = 0;
        for (int i = 1; i <= N; i++) {
            sum += small[i];
        }
        return sum;
    }
    // Prefix sums of small[]
    // and big[]
    calc(big, k);
    calc(small, l);

    // Initialize small[l] within the range
    fill(small + l + 1, small + N + 1, small[l]);

    // Variable to store the answer
    int res = 0;
    for (int i = (k + X) / (1 + X); i <= k; i++) {
        if (1ll * (i - 1) * (X + 1) + 1 <= N) {

            // Update res with maximum one
            res = max(
                res,
                big[i]
                    + small[N - 1ll
                           * (i - 1)
                           * (X + 1) - 1]);
        }
    }
    // Return res
    return res;
}

// Driver Code
int main()
{
    int arr[] = { 9, 13, 16, 21, 6 };
    int X = 2;
    int K = 15;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxScore(arr, X, K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program, for the above approach
import java.util.*;

class GFG{

static int maxn = (int)1e5;

// Utility function to calculate the
// sum of elements as a prefix array
static void calc(int arr[], int N)
{
    Arrays.sort(arr);
    arr = reverse(arr);

    for(int i = 1; i <= N; i++)
    {
        arr[i] += arr[i - 1];
    }
}

static int[] reverse(int a[])
{
    int i, n = a.length + 1, t;
    for(i = 1; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Function to find the maximum score
// that can be achieved by rearranging
// the elements of given array
static int maxScore(int arr[], int X, int K, int N)
{

    // Arrays to store small and big elements
    int []small = new int[maxn + 5];
    int big[] = new int[maxn + 5];
    int k = 0, l = 0;

    // Iterate and segregate big and
    // small elements
    for(int i = 0; i < N; i++)
    {
        if (arr[i] > K)
        {
            big[++k] = arr[i];
        }
        else
        {
            small[++l] = arr[i];
        }
    }

    // If k = 0, return the sum
    // of small[]
    if (k == 0)
    {
        int sum = 0;
        for(int i = 1; i <= N; i++)
        {
            sum += small[i];
        }
        return sum;
    }

    // Prefix sums of small[]
    // and big[]
    calc(big, k);
    calc(small, l);

    // Initialize small[l] within the range
    // fill(small + l + 1, small + N + 1, small[l]);
    for(int i = l + 1; i <= N; i++)
    {
        small[i] = small[l];
    }

    // Variable to store the answer
    int res = 0;
    for(int i = (k + X) / (1 + X); i <= k; i++)
    {
        if (1 * (i - 1) * (X + 1) + 1 <= N)
        {

            // Update res with maximum one
            res = Math.max(
                res, big[i] + small[N - 1 * (i - 1)  *
                                   (X + 1) - 1]);
        }
    }

    // Return res
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 9, 13, 16, 21, 6 };
    int X = 2;
    int K = 15;
    int N = arr.length;

    System.out.print(maxScore(arr, X, K, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program, for the above approach
maxn = int(1e5)

# Utility function to calculate the
# sum of elements as a prefix array
def calc(arr, N) :

    arr.sort()
    arr[::-1]

    for i in range(1, N+1):
        arr[i] += arr[i - 1]

# Function to find the maximum score
# that can be achieved by rearranging
# the elements of given array
def maxScore(arr, X, K, N) :

    # Arrays to store small and big elements
    small = [10] * (maxn + 5)
    big = [10] * (maxn + 5)
    k = 0
    l = 0

    # Iterate and segregate big and
    # small elements
    for i in range(N):
        if (arr[i] > K) :
            big[++k] = arr[i]

        else :
            small[++l] = arr[i]

    # If k = 0, return the sum
    # of small[]
    if (k == 0) :
        sum = 0
        for i in range(1, N+1):
            sum += small[i]

        return sum

    # Prefix sums of small[]
    # and big[]
    calc(big, k)
    calc(small, l)

    # Initialize small[l] within the range
    for i in range(l + 1, N+1):
        small[i] = small[l]

    # Variable to store the answer
    res = 0
    for i in range((k + X) / (1 + X), k+1):
        if (1 * (i - 1) * (X + 1) + 1 <= N) :

            # Update res with maximum one
            res = max(
                res,
                big[i]
                    + small[N - 1 * (i - 1)
                           * (X + 1) - 1])

    # Return res
    return res

# Driver Code
arr = [ 9, 13, 16, 21, 6 ]
X = 2
K = 15
N = len(arr)

print(maxScore(arr, X, K, N))

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program, for the above approach
using System;
class GFG {

    static int maxn = (int)1e5;

    // Utility function to calculate the
    // sum of elements as a prefix array
    static void calc(int[] arr, int N)
    {
        Array.Sort(arr);
        arr = reverse(arr);

        for (int i = 1; i <= N; i++) {
            arr[i] += arr[i - 1];
        }
    }

    static int[] reverse(int[] a)
    {
        int i, n = a.Length + 1, t;
        for (i = 1; i < n / 2; i++) {
            t = a[i];
            a[i] = a[n - i - 1];
            a[n - i - 1] = t;
        }
        return a;
    }

    // Function to find the maximum score
    // that can be achieved by rearranging
    // the elements of given array
    static int maxScore(int[] arr, int X, int K, int N)
    {

        // Arrays to store small and big elements
        int[] small = new int[maxn + 5];
        int[] big = new int[maxn + 5];
        int k = 0, l = 0;

        // Iterate and segregate big and
        // small elements
        for (int i = 0; i < N; i++) {
            if (arr[i] > K) {
                big[++k] = arr[i];
            }
            else {
                small[++l] = arr[i];
            }
        }

        // If k = 0, return the sum
        // of small[]
        if (k == 0) {
            int sum = 0;
            for (int i = 1; i <= N; i++) {
                sum += small[i];
            }
            return sum;
        }

        // Prefix sums of small[]
        // and big[]
        calc(big, k);
        calc(small, l);

        // Initialize small[l] within the range
        // fill(small + l + 1, small + N + 1, small[l]);
        for (int i = l + 1; i <= N; i++) {
            small[i] = small[l];
        }

        // Variable to store the answer
        int res = 0;
        for (int i = (k + X) / (1 + X); i <= k; i++) {
            if (1 * (i - 1) * (X + 1) + 1 <= N) {

                // Update res with maximum one
                res = Math.Max(
                    res,
                    big[i]
                        + small[N - 1 * (i - 1) * (X + 1)
                                - 1]);
            }
        }

        // Return res
        return res;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 9, 13, 16, 21, 6 };
        int X = 2;
        int K = 15;
        int N = arr.Length;

        Console.WriteLine(maxScore(arr, X, K, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach
       let maxn = 1e5;

       // Utility function to calculate the
       // sum of elements as a prefix array
       function calc(arr, N)
       {
           let arr1 = arr.slice(0, 1)
           let arr2 = arr.slice(1, N + 1)
           arr2.sort(function (a, b) { return a - b });
           arr2.reverse();

           arr = arr1.concat(arr2)
           for (let i = 1; i <= N; i++) {
               arr[i] += arr[i - 1];
           }
           return arr;
       }

       // Function to find the maximum score
       // that can be achieved by rearranging
       // the elements of given array
       function maxScore(arr, X, K, N)
       {

           // Arrays to store small and big elements
           let small = new Array(maxn + 5).fill(0)
           let big = new Array(maxn + 5).fill(0);
           let k = 0, l = 0;

           // Iterate and segregate big and
           // small elements
           for (let i = 0; i < N; i++) {
               if (arr[i] > K) {
                   big[++k] = arr[i];
               }
               else {
                   small[++l] = arr[i];
               }
           }

           // If k = 0, return the sum
           // of small[]
           if (k == 0) {
               let sum = 0;
               for (let i = 1; i < N; i++) {
                   sum += small[i];
               }
               return sum;
           }

           // Prefix sums of small[]
           // and big[]
           big = calc(big, k);
           small = calc(small, l);

           // Initialize small[l] within the range
           for (let i = l + 1; i <= N; i++) {
               small[i] = small[l];
           }

           // Variable to store the answer
           let res = 0;
           for (let i = Math.floor((k + X) / (1 + X)); i <= k; i++) {
               if (1 * (i - 1) * (X + 1) + 1 <= N) {

                   // Update res with maximum one
                   res = Math.max(
                       res,
                       big[i]
                       + small[N - 1
                       * (i - 1)
                       * (X + 1) - 1]);
               }
           }

           // Return res
           return res;
       }

       // Driver Code
       let arr = [9, 13, 16, 21, 6];
       let X = 2;
       let K = 15;
       let N = arr.length;

       document.write(maxScore(arr, X, K, N));

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
50
```

***时间复杂度:** O(N*logN)*
***辅助空间:** O(N)*