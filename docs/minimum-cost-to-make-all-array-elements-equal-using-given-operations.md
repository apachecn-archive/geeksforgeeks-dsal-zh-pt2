# 使用给定操作使所有数组元素相等的最小成本

> 原文:[https://www . geeksforgeeks . org/最小成本制造所有数组元素-相等-使用给定操作/](https://www.geeksforgeeks.org/minimum-cost-to-make-all-array-elements-equal-using-given-operations/)

给定正整数的数组 **arr[]** 和三个整数 **A** 、 **R** 、 **M** ，其中

*   数组元素加 1 的代价是 **A** ，
*   从数组的一个元素中减去 1 的成本是 **R** 并且
*   一个元素加 1 同时另一个元素减 1 的成本是 **M** 。

任务是找到使数组的所有元素相等的最小总成本。

**示例:**

> **输入:** arr[] = {5，5，3，6，5}，A = 1，R = 2，M = 4
> **输出:** 4
> **解释:**
> **运算 1:** 对元素 3 加两次，数组–{ 5，5，6，5}，成本= 2
> **运算 2:** 对元素 6 减去一次，数组–{ 5，5，5，5}
> 
> **输入:** arr[] = {5，5，3，6，5}，A = 1，R = 2，M = 2
> **输出:** 3

**方法:**想法是:

1.  找到 **M** 和**A+R**T5【的*最小值，因为 M 可以同时进行两个操作。*
2.  然后将[前缀和存储在一个数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)中，求常数时间内的和。
3.  现在计算每个元素与当前元素相等的成本，并找出它们的最小值。
4.  当我们使所有元素等于数组的平均值时，最小的答案也可以存在。
5.  因此，最后还要计算使所有元素等于元素的近似平均总和的成本。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum cost to make all array
// elements equal

#include <bits/stdc++.h>
using namespace std;

// Function that returns the cost of
// making all elements equal to current element
int costCalculation(
    int current, int arr[],
    int n, int pref[],
    int a, int r,
    int minimum)
{

    // Compute the lower bound
    // of current element
    int index
        = lower_bound(
              arr, arr + n, current)
          - arr;

    // Calculate the requirement
    // of add operation
    int left
        = index * current - pref[index];

    // Calculate the requirement
    // of subtract operation
    int right
        = pref[n] - pref[index]
          - (n - index)
                * current;

    // Compute minimum of left and right
    int res = min(left, right);
    left -= res;
    right -= res;

    // Computing the total cost of add
    // and subtract operations
    int total = res * minimum;
    total += left * a;
    total += right * r;

    return total;
}

// Function that prints minimum cost
// of making all elements equal
void solve(int arr[], int n,
           int a, int r, int m)
{
    // Sort the given array
    sort(arr, arr + n);

    // Calculate minimum from a + r and m
    int minimum = min(a + r, m);

    int pref[n + 1] = { 0 };

    // Compute prefix sum
    // and store in pref
    // array
    for (int i = 0; i < n; i++)
        pref[i + 1] = pref[i] + arr[i];

    int ans = 10000;

    // Find the minimum cost
    // from the given elements
    for (int i = 0; i < n; i++)
        ans
            = min(
                ans,
                costCalculation(
                    arr[i], arr, n,
                    pref, a, r,
                    minimum));

    // Finding the minimum cost
    // from the other cases where
    // minimum cost can occur
    ans
        = min(
            ans,
            costCalculation(
                pref[n] / n, arr,
                n, pref, a,
                r, minimum));
    ans
        = min(
            ans,
            costCalculation(
                pref[n] / n + 1,
                arr, n, pref,
                a, r, minimum));

    // Printing the minimum cost of making
    // all elements equal
    cout << ans << "\n";
}

// Driver Code
int main()
{
    int arr[] = { 5, 5, 3, 6, 5 };

    int A = 1, R = 2, M = 4;

    int size = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    solve(arr, size, A, R, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum cost to make all array
// elements equal
import java.lang.*;
import java.util.*;

class GFG{

public static int lowerBound(int[] array, int length,
                                          int value)
{
    int low = 0;
    int high = length;

    while (low < high)
    {
        final int mid = (low + high) / 2;

        // Checks if the value is less
        // than middle element of the array
        if (value <= array[mid])
        {
            high = mid;
        }
        else
        {
            low = mid + 1;
        }
    }
    return low;
}

// Function that returns the cost of making
// all elements equal to current element
public static int costCalculation(int current, int arr[],
                                  int n, int pref[],
                                  int a, int r,
                                  int minimum)
{

    // Compute the lower bound
    // of current element
    int index = lowerBound(arr, arr.length, current);

    // Calculate the requirement
    // of add operation
    int left = index * current - pref[index];

    // Calculate the requirement
    // of subtract operation
    int right = pref[n] -
                pref[index]- (n - index)* current;

    // Compute minimum of left and right
    int res = Math.min(left, right);
    left -= res;
    right -= res;

    // Computing the total cost of add
    // and subtract operations
    int total = res * minimum;
    total += left * a;
    total += right * r;

    return total;
}

// Function that prints minimum cost
// of making all elements equal
public static void solve(int arr[], int n,
                         int a, int r, int m)
{

    // Sort the given array
    Arrays.sort(arr);

    // Calculate minimum from a + r and m
    int minimum = Math.min(a + r, m);

    int []pref = new int [n + 1];
    Arrays.fill(pref, 0);

    // Compute prefix sum and
    // store in pref array
    for(int i = 0; i < n; i++)
       pref[i + 1] = pref[i] + arr[i];

    int ans = 10000;

    // Find the minimum cost
    // from the given elements
    for(int i = 0; i < n; i++)
       ans = Math.min(ans, costCalculation(arr[i], arr,
                                           n, pref,
                                           a, r, minimum));

    // Finding the minimum cost
    // from the other cases where
    // minimum cost can occur
    ans = Math.min(ans, costCalculation(pref[n] / n, arr,
                                        n, pref, a, r,
                                        minimum));
    ans = Math.min(ans, costCalculation(pref[n] / n + 1,
                                        arr, n, pref,
                                        a, r, minimum));

    // Printing the minimum cost of making
    // all elements equal
    System.out.println(ans);
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 5, 5, 3, 6, 5 };
    int A = 1, R = 2, M = 4;
    int size = arr.length ;

    // Function Call
    solve(arr, size, A, R, M);
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum cost to make all array
# elements equal
def lowerBound(array, length, value):

    low = 0
    high = length

    while (low < high):
        mid = (low + high) // 2

        # Checks if the value is less
        # than middle element of the array
        if (value <= array[mid]):
            high = mid
        else:
            low = mid + 1

    return low

# Function that returns the cost of making
# all elements equal to current element
def costCalculation(current, arr,
                    n, pref, a, r, minimum):

    # Compute the lower bound
    # of current element
    index = lowerBound(arr, len(arr), current)

    # Calculate the requirement
    # of add operation
    left = index * current - pref[index]

    # Calculate the requirement
    # of subtract operation
    right = (pref[n] - pref[index] -
            (n - index) * current)

    # Compute minimum of left and right
    res = min(left, right)
    left -= res
    right -= res

    # Computing the total cost of add
    # and subtract operations
    total = res * minimum
    total += left * a
    total += right * r

    return total

# Function that prints minimum cost
# of making all elements equal
def solve(arr, n, a, r, m):

    # Sort the given array
    arr.sort()

    # Calculate minimum from a + r and m
    minimum = min(a + r, m)

    pref = [0] * (n + 1)

    # Compute prefix sum and
    # store in pref array
    for i in range(n):
        pref[i + 1] = pref[i] + arr[i]

    ans = 10000

    # Find the minimum cost
    # from the given elements
    for i in range(n):
        ans = min(ans, costCalculation(arr[i], arr,
                                       n, pref, a,
                                       r, minimum))

    # Finding the minimum cost
    # from the other cases where
    # minimum cost can occur
    ans = min(ans, costCalculation(pref[n] // n,
                                   arr, n, pref,
                                   a, r, minimum))
    ans = min(ans, costCalculation(pref[n] // n + 1,
                                   arr, n, pref, a,
                                   r, minimum))

    # Printing the minimum cost of making
    # all elements equal
    print(ans)

# Driver Code
if __name__ == "__main__":

    arr = [ 5, 5, 3, 6, 5 ]
    A = 1
    R = 2
    M = 4
    size = len(arr)

    # Function call
    solve(arr, size, A, R, M)

# This code is contributed by chitranayal
```

## C#

```
// C# implementation to find the
// minimum cost to make all array
// elements equal
using System;

class GFG{

public static int lowerBound(int[] array,
                             int length,
                             int value)
{
    int low = 0;
    int high = length;

    while (low < high)
    {
        int mid = (low + high) / 2;

        // Checks if the value is less
        // than middle element of the array
        if (value <= array[mid])
        {
            high = mid;
        }
        else
        {
            low = mid + 1;
        }
    }
    return low;
}

// Function that returns the cost of making
// all elements equal to current element
public static int costCalculation(int current,
                                  int []arr, int n,
                                  int []pref, int a,
                                  int r, int minimum)
{

    // Compute the lower bound
    // of current element
    int index = lowerBound(arr, arr.Length, current);

    // Calculate the requirement
    // of add operation
    int left = index * current - pref[index];

    // Calculate the requirement
    // of subtract operation
    int right = pref[n] - pref[index] -
                          (n - index) *
                           current;

    // Compute minimum of left and right
    int res = Math.Min(left, right);
    left -= res;
    right -= res;

    // Computing the total cost of add
    // and subtract operations
    int total = res * minimum;
    total += left * a;
    total += right * r;

    return total;
}

// Function that prints minimum cost
// of making all elements equal
public static void solve(int []arr, int n,
                         int a, int r, int m)
{

    // Sort the given array
    Array.Sort(arr);

    // Calculate minimum from a + r and m
    int minimum = Math.Min(a + r, m);

    int []pref = new int [n + 1];
    Array.Fill(pref, 0);

    // Compute prefix sum and
    // store in pref array
    for(int i = 0; i < n; i++)
        pref[i + 1] = pref[i] + arr[i];

    int ans = 10000;

    // Find the minimum cost
    // from the given elements
    for(int i = 0; i < n; i++)
        ans = Math.Min(ans, costCalculation(arr[i], arr,
                                            n, pref, a,
                                            r, minimum));

    // Finding the minimum cost
    // from the other cases where
    // minimum cost can occur
    ans = Math.Min(ans, costCalculation(pref[n] / n, arr,
                                        n, pref, a, r,
                                        minimum));
    ans = Math.Min(ans, costCalculation(pref[n] / n + 1,
                                        arr, n, pref,
                                        a, r, minimum));

    // Printing the minimum cost of making
    // all elements equal
    Console.WriteLine(ans);
}

// Driver Code
public static void Main(string []args)
{
    int []arr = { 5, 5, 3, 6, 5 };
    int A = 1, R = 2, M = 4;
    int size = arr.Length ;

    // Function Call
    solve(arr, size, A, R, M);
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

// javascript implementation to find the
// minimum cost to make all array
// elements equal   
function lowerBound(array, length, value)
{
        var low = 0;
        var high = length;

        while (low < high)
        {
             var mid = parseInt((low + high) / 2);

            // Checks if the value is less
            // than middle element of the array
            if (value <= array[mid])
            {
                high = mid;
            }
            else
            {
                low = mid + 1;
            }
        }
        return low;
    }

    // Function that returns the cost of making
    // all elements equal to current element
    function costCalculation(current , arr , n , pref , a , r , minimum)
    {

        // Compute the lower bound
        // of current element
        var index = lowerBound(arr, arr.length, current);

        // Calculate the requirement
        // of add operation
        var left = index * current - pref[index];

        // Calculate the requirement
        // of subtract operation
        var right = pref[n] - pref[index] - (n - index) * current;

        // Compute minimum of left and right
        var res = Math.min(left, right);
        left -= res;
        right -= res;

        // Computing the total cost of add
        // and subtract operations
        var total = res * minimum;
        total += left * a;
        total += right * r;

        return total;
    }

    // Function that prints minimum cost
    // of making all elements equal
    function solve(arr , n , a , r , m) {

        // Sort the given array
        arr.sort();

        // Calculate minimum from a + r and m
        var minimum = Math.min(a + r, m);

        var pref = Array(n+1).fill(0);

        // Compute prefix sum and
        // store in pref array
        for (i = 0; i < n; i++)
            pref[i + 1] = pref[i] + arr[i];

        var ans = 10000;

        // Find the minimum cost
        // from the given elements
        for (i = 0; i < n; i++)
            ans = Math.min(ans, costCalculation(arr[i], arr, n, pref, a, r, minimum));

        // Finding the minimum cost
        // from the other cases where
        // minimum cost can occur
        ans = Math.min(ans, costCalculation(pref[n] / n, arr, n, pref, a, r, minimum));
        ans = Math.min(ans, costCalculation(pref[n] / n + 1, arr, n, pref, a, r, minimum));

        // Printing the minimum cost of making
        // all elements equal
        document.write(ans);
    }

    // Driver Code
        var arr = [ 5, 5, 3, 6, 5 ];
        var A = 1, R = 2, M = 4;
        var size = arr.length;

        // Function Call
        solve(arr, size, A, R, M);

// This code is contributed by Rajput-Ji.
</script>
```

**Output:** 

```
4
```