# 总和不能被 K 整除的最长可能子阵列的计数

> 原文:[https://www . geeksforgeeks . org/具有不可被 k 整除的和的最长可能子阵列计数/](https://www.geeksforgeeks.org/count-of-longest-possible-subarrays-with-sum-not-divisible-by-k/)

给定一个整数数组 **arr[]** 和一个正整数 **K** ，任务是找到最长可能子阵的计数，其元素之和不能被 **K** 整除。

**示例:**

> **输入:** arr[] = {2，3，4，6}，K = 3
> **输出:** 1
> **解释:**大小为 3 的最长可能子阵列只有一个，即{3，4，6}的和为 13，不能被 K = 3 整除。
> 
> **输入:** arr[] = {2，4，3，5，1}，K = 3
> **输出:** 2
> **解释:**有 2 个最长的可能大小为 4 的子阵列，即{2，4，3，5}和{4，3，5，1}分别有 14 和 13 的和，不能被 K = 3 整除。

**进场:**

1.  检查数组中所有元素的和是否能被 K 整除
2.  如果总和不能被 K 整除，则返回 1，因为最长的子阵列大小为 n
3.  其他
    *   求第一个不能被 k 整除的数的索引，设其为 **L** 。
    *   找出最后一个不能被 k 整除的数的索引，设其为 **R** 。
    *   移除一直到索引 L 的元素，并找到子阵列的大小。去掉 R 以外的元素，也找出这个子阵列的大小。无论哪个长度更大，都是最长的不能被 k 整除的子阵列的大小
    *   使用该长度作为窗口大小，在 arr[]上应用滑动窗口技术，找出上面获得的大小不能被 k 整除的子阵列的计数

下面是上述方法的实现:

## C++

```
// C++ program for the above problem

#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// longest subarrays with sum not
// divisible by K
int CountLongestSubarrays(
    int arr[], int n, int k)
{

    // Sum of all elements in
    // an array
    int i, s = 0;
    for (i = 0; i < n; ++i) {
        s += arr[i];
    }

    // If overall sum is not
    // divisible then return
    // 1, as only one subarray
    // of size n is possible
    if (s % k) {
        return 1;
    }
    else {
        int ini = 0;

        // Index of the first number
        // not divisible by K
        while (ini < n
               && arr[ini] % k == 0) {
            ++ini;
        }

        int final = n - 1;

        // Index of the last number
        // not divisible by K
        while (final >= 0
               && arr[final] % k == 0) {
            --final;
        }

        int len, sum = 0, count = 0;
        // Subarray doesn't exist
        if (ini == n) {
            return -1;
        }
        else {
            len = max(n - 1 - ini,
                      final);
        }

        // Sum of the window
        for (i = 0; i < len; i++) {
            sum += arr[i];
        }

        if (sum % k != 0) {
            count++;
        }
        // Calculate the sum of rest of
        // the windows of size len
        for (i = len; i < n; i++) {
            sum = sum + arr[i];
            sum = sum - arr[i - len];
            if (sum % k != 0) {
                count++;
            }
        }
        return count;
    }
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 2, 2, 3 };
    int n = sizeof(arr)
            / sizeof(arr[0]);
    int k = 3;
    cout << CountLongestSubarrays(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above problem
import java.util.*;

class GFG{

// Function to find the count of
// longest subarrays with sum not
// divisible by K
static int CountLongestSubarrays(int arr[],
                                int n, int k)
{

    // Sum of all elements in
    // an array
    int i, s = 0;
    for(i = 0; i < n; ++i)
    {
    s += arr[i];
    }

    // If overall sum is not
    // divisible then return
    // 1, as only one subarray
    // of size n is possible
    if ((s % k) != 0)
    {
        return 1;
    }
    else
    {
        int ini = 0;

        // Index of the first number
        // not divisible by K
        while (ini < n && arr[ini] % k == 0)
        {
            ++ini;
        }

        int fin = n - 1;

        // Index of the last number
        // not divisible by K
        while (fin >= 0 && arr[fin] % k == 0)
        {
            --fin;
        }

        int len, sum = 0, count = 0;

        // Subarray doesn't exist
        if (ini == n)
        {
            return -1;
        }
        else
        {
            len = Math.max(n - 1 - ini, fin);
        }

        // Sum of the window
        for(i = 0; i < len; i++)
        {
        sum += arr[i];
        }

        if (sum % k != 0)
        {
            count++;
        }

        // Calculate the sum of rest of
        // the windows of size len
        for(i = len; i < n; i++)
        {
        sum = sum + arr[i];
        sum = sum - arr[i - len];
        if (sum % k != 0)
        {
            count++;
        }
        }
        return count;
    }
}

// Driver Code
public static void main (String []args)
{
    int arr[] = { 3, 2, 2, 2, 3 };
    int n = arr.length;
    int k = 3;

    System.out.print(CountLongestSubarrays(
                    arr, n, k));
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program for the above problem

# Function to find the count of
# longest subarrays with sum not
# divisible by K
def CountLongestSubarrays(arr, n, k):

    # Sum of all elements in
    # an array
    s = 0
    for i in range(n):
        s += arr[i]

    # If overall sum is not
    # divisible then return
    # 1, as only one subarray
    # of size n is possible
    if(s % k):
        return 1
    else:
        ini = 0

        # Index of the first number
        # not divisible by K
        while (ini < n and arr[ini] % k == 0):
            ini += 1
        final = n - 1

        # Index of the last number
        # not divisible by K
        while (final >= 0 and arr[final] % k == 0):
            final -= 1

        sum, count = 0, 0

        # Subarray doesn't exist
        if(ini == n):
            return -1
        else:
            length = max(n - 1 - ini, final)

        # Sum of the window
        for i in range(length):
            sum += arr[i]

        if(sum % k != 0):
            count += 1

        # Calculate the sum of rest of
        # the windows of size len
        for i in range(length, n):
            sum = sum + arr[i]
            sum = sum + arr[i - length]
            if (sum % k != 0):
                count += 1

        return count

# Driver Code
if __name__ == '__main__':

    arr = [ 3, 2, 2, 2, 3 ]
    n = len(arr)
    k = 3

    print(CountLongestSubarrays(arr, n, k))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above problem
using System;

class GFG{

// Function to find the count of
// longest subarrays with sum not
// divisible by K
static int CountLongestSubarrays(int[] arr,
                                 int n, int k)
{

    // Sum of all elements in
    // an array
    int i, s = 0;
    for(i = 0; i < n; ++i)
    {
       s += arr[i];
    }

    // If overall sum is not
    // divisible then return
    // 1, as only one subarray
    // of size n is possible
    if ((s % k) != 0)
    {
        return 1;
    }
    else
    {
        int ini = 0;

        // Index of the first number
        // not divisible by K
        while (ini < n && arr[ini] % k == 0)
        {
            ++ini;
        }

        int fin = n - 1;

        // Index of the last number
        // not divisible by K
        while (fin >= 0 && arr[fin] % k == 0)
        {
            --fin;
        }

        int len, sum = 0, count = 0;

        // Subarray doesn't exist
        if (ini == n)
        {
            return -1;
        }
        else
        {
            len = Math.Max(n - 1 - ini, fin);
        }

        // Sum of the window
        for(i = 0; i < len; i++)
        {
           sum += arr[i];
        }

        if (sum % k != 0)
        {
            count++;
        }

        // Calculate the sum of rest of
        // the windows of size len
        for(i = len; i < n; i++)
        {
           sum = sum + arr[i];
           sum = sum - arr[i - len];
           if (sum % k != 0)
           {
               count++;
           }
        }
        return count;
    }
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 3, 2, 2, 2, 3 };
    int n = arr.Length;
    int k = 3;

    Console.WriteLine(CountLongestSubarrays(
                      arr, n, k));
}
}

// This code is contributed by jrishabh99
```

## java 描述语言

```
<script>

// JavaScript program for the above problem 

// Function to find the count of
// longest subarrays with sum not
// divisible by K
function CountLongestSubarrays(arr, n, k)
{

    // Sum of all elements in
    // an array
    let i, s = 0;
    for(i = 0; i < n; ++i)
    {
        s += arr[i];
    }

    // If overall sum is not
    // divisible then return
    // 1, as only one subarray
    // of size n is possible
    if ((s % k) != 0)
    {
        return 1;
    }
    else
    {
        let ini = 0;

        // Index of the first number
        // not divisible by K
        while (ini < n && arr[ini] % k == 0)
        {
            ++ini;
        }

        let fin = n - 1;

        // Index of the last number
        // not divisible by K
        while (fin >= 0 && arr[fin] % k == 0)
        {
            --fin;
        }

        let len, sum = 0, count = 0;

        // Subarray doesn't exist
        if (ini == n)
        {
            return -1;
        }
        else
        {
            len = Math.max(n - 1 - ini, fin);
        }

        // Sum of the window
        for(i = 0; i < len; i++)
        {
            sum += arr[i];
        }

        if (sum % k != 0)
        {
            count++;
        }

        // Calculate the sum of rest of
        // the windows of size len
        for(i = len; i < n; i++)
        {
            sum = sum + arr[i];
            sum = sum - arr[i - len];

            if (sum % k != 0)
            {
                count++;
            }
        }
        return count;
    }
}

// Driver Code
let arr = [ 3, 2, 2, 2, 3 ];
let n = arr.length;
let k = 3;

document.write(CountLongestSubarrays(
                arr, n, k));

// This code is contributed by sanjoy_62     

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*
***辅助空间复杂度:** O(1)*