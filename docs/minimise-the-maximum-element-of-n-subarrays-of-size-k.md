# 最小化大小为 K 的 N 个子阵列的最大元素

> 原文:[https://www . geeksforgeeks . org/minimum-n 最大元素大小为 k 的子阵列/](https://www.geeksforgeeks.org/minimise-the-maximum-element-of-n-subarrays-of-size-k/)

给定一个数组 **arr[]** 和两个整数 **N** 和 **K** ，任务是选择大小为 K 的不重叠的 N 个子阵列，使得所有子阵列的最大元素最小。
**注意:**如果无法选择 N 个这样的子阵列，那么返回-1。
**示例:**

> **输入:** arr[] = {1，10，3，10，2}，N = 3，K = 1
> **输出:** 3
> **解释:**
> 这三个不重叠的子阵是–
> 子阵= > {{1}、{2}、{3}}
> 这些子阵中最大的是= > 3
> **输入:** arr[] = {7，7 K = 3
> **输出:** 12
> **说明:**
> 这两个不重叠的子阵是–
> 子阵= > {{7，7，7}，{7，12，7}}
> 这些子阵的最大元素是= > 12

**进场:**思路是用一个[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。下面是二分搜索法的插图:

*   **搜索空间:**因为我们必须从 N 个子阵列中找到最大元素，这是阵列中的元素之一。因此，搜索空间将是数组的最小元素到最大元素。
*   **二分搜索法的函数:**二分搜索法的函数是在所有元素都小于给定数量的情况下找到可能的 K 大小数组的计数，该数量将位于搜索空间的中间。
*   **左搜索空间:**当 K 大小的子阵的可能计数大于或等于 N 时的条件，那么可能的答案可以位于左搜索空间。
*   **右搜索空间:**K 大小子阵可能数小于 N 的条件，那么答案可能扫描在右搜索空间。

下面是上述方法的实现:

## C++

```
// C++ implementation to choose
// N subarrays of size K such that
// the maximum element of
// subarrays is minimum

#include <bits/stdc++.h>
using namespace std;

// Function to choose
// N subarrays of size K such that
// the maximum element of
// subarrays is minimum
int minDays(vector<int>& arr,
                int n, int k)
{
    int l = arr.size(),
left = 1, right = 1e9;

    // Condition to check if it
    // is not possible to choose k
    // sized N subarrays
    if (n * k > l)
        return -1;

    // Using binary search
    while (left < right) {

        // calculating mid
        int mid = (left + right) / 2,
                 cnt = 0, product = 0;

        // Loop to find the count of the
        // K sized subarrays possible with
        // elements less than  mid
        for (int j = 0; j < l; ++j) {
            if (arr[j] > mid) {
                cnt = 0;
            }
            else if (++cnt >= k) {
                product++;
                cnt = 0;
            }
        }

        // Condition to check if the
        // answer is in right subarray
        if (product < n) {
            left = mid + 1;
        }
        else {
            right = mid;
        }
    }
    return left;
}

// Driver Code
int main()
{
    vector<int> arr{ 1, 10, 3, 10, 2 };
    int n = 3, k = 1;

    // Function Call
    cout << minDays(arr, n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to choose
// N subarrays of size K such that
// the maximum element of
// subarrays is minimum
class GFG{

// Function to choose
// N subarrays of size K such that
// the maximum element of
// subarrays is minimum
static int minDays(int []arr,
                   int n, int k)
{
    int l = arr.length,
        left = 1, right = (int) 1e9;

    // Condition to check if it
    // is not possible to choose k
    // sized N subarrays
    if (n * k > l)
        return -1;

    // Using binary search
    while (left < right)
    {

        // calculating mid
        int mid = (left + right) / 2,
                   cnt = 0, product = 0;

        // Loop to find the count of the
        // K sized subarrays possible with
        // elements less than mid
        for (int j = 0; j < l; ++j)
        {
            if (arr[j] > mid)
            {
                cnt = 0;
            }
            else if (++cnt >= k)
            {
                product++;
                cnt = 0;
            }
        }

        // Condition to check if the
        // answer is in right subarray
        if (product < n)
        {
            left = mid + 1;
        }
        else
        {
            right = mid;
        }
    }
    return left;
}

// Driver Code
public static void main(String[] args)
{
    int []arr = {1, 10, 3, 10, 2};
    int n = 3, k = 1;

    // Function Call
    System.out.print(minDays(arr, n, k) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation to choose
# N subarrays of size K such that
# the maximum element of
# subarrays is minimum

# Function to choose
# N subarrays of size K such that
# the maximum element of
# subarrays is minimum
def minDays(arr, n, k):

    l = len(arr)
    left = 1
    right = 1e9

    # Condition to check if it
    # is not possible to choose k
    # sized N subarrays
    if (n * k > l):
        return -1

    # Using binary search
    while (left < right):

        # calculating mid
        mid = (left + right) // 2
        cnt = 0
        product = 0

        # Loop to find the count of the
        # K sized subarrays possible with
        # elements less than  mid
        for j in range (l):
            if (arr[j] > mid):
                cnt = 0
            else:
                cnt += 1
                if (cnt >= k):
                    product += 1
                    cnt = 0

        # Condition to check if the
        # answer is in right subarray
        if (product < n):
            left = mid + 1
        else:
            right = mid

    return left

# Driver Code
if __name__ == "__main__":
    arr = [1, 10, 3, 10, 2]
    n = 3
    k = 1

    # Function Call
    print (int(minDays(arr, n, k)))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation to choose N 
// subarrays of size K such that
// the maximum element of
// subarrays is minimum
using System;
class GFG{

// Function to choose N subarrays 
// of size K such that the maximum
// element of subarrays is minimum
static int minDays(int []arr,
                   int n, int k)
{
    int l = arr.Length;
    int left = 1, right = (int)1e9;

    // Condition to check if it
    // is not possible to choose k
    // sized N subarrays
    if (n * k > l)
        return -1;

    // Using binary search
    while (left < right)
    {

        // Calculating mid
        int mid = (left + right) / 2,
                   cnt = 0, product = 0;

        // Loop to find the count of the
        // K sized subarrays possible with
        // elements less than mid
        for(int j = 0; j < l; ++j)
        {
           if (arr[j] > mid)
           {
               cnt = 0;
           }
           else if (++cnt >= k)
           {
               product++;
               cnt = 0;
           }
        }

        // Condition to check if the
        // answer is in right subarray
        if (product < n)
        {
            left = mid + 1;
        }
        else
        {
            right = mid;
        }
    }
    return left;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 10, 3, 10, 2 };
    int n = 3, k = 1;

    // Function Call
    Console.Write(minDays(arr, n, k) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript implementation to choose
// N subarrays of size K such that
// the maximum element of
// subarrays is minimum

// Function to choose
// N subarrays of size K such that
// the maximum element of
// subarrays is minimum
function minDays(arr, n, k)
{
    let l = arr.length,
left = 1, right = 1000000000;

    // Condition to check if it
    // is not possible to choose k
    // sized N subarrays
    if (n * k > l)
        return -1;

    // Using binary search
    while (left < right) {

        // calculating mid
        let mid = parseInt((left + right) / 2),
                 cnt = 0, product = 0;

        // Loop to find the count of the
        // K sized subarrays possible with
        // elements less than  mid
        for (let j = 0; j < l; ++j) {
            if (arr[j] > mid) {
                cnt = 0;
            }
            else if (++cnt >= k) {
                product++;
                cnt = 0;
            }
        }

        // Condition to check if the
        // answer is in right subarray
        if (product < n) {
            left = mid + 1;
        }
        else {
            right = mid;
        }
    }
    return left;
}

// Driver Code
    let arr = [ 1, 10, 3, 10, 2 ];
    let n = 3, k = 1;

    // Function Call
    document.write(minDays(arr, n, k));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N*logN)