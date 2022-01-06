# 最小和最大元素之和小于 K 的子集计数

> 原文:[https://www . geesforgeks . org/具有小于 k 的最小和最大元素之和的子集计数/](https://www.geeksforgeeks.org/count-of-subsets-having-sum-of-min-and-max-element-less-than-k/)

给定整数数组 **arr[]** 和整数 **K** ，任务是找到非空子集 S 的数量，使得**最小(S) +最大(S) < K** 。
**举例:**

> **输入** : arr[] = {2，4，5，7} K = 8
> **输出** : 4
> **解释:**
> 可能的子集有{2}、{2，4}、{2，4，5}和{2，5}
> **输入:** : arr[] = {2，4，2，5，7} K = 10
> **输出:** 26

**接近**T2】

1.  首先对输入数组进行排序。
2.  现在使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)统计子集的数量。
3.  让我们左右取两个指针，设置左= 0，右= N-1。

> **if(arr[left]+arr[right]<K)**
> 将左指针增加 1，并将**2<sup>j–I</sup>**添加到答案中，因为左值和右值构成子集的潜在结束值。来自[i，j–1]的所有值也构成子集的末端，这些子集将具有总和< K。因此，我们需要计算左= i 和右∊ [i，j]的所有可能子集。因此，在苏明向上取值 GP 的 2<sup>j–I+1</sup>+2<sup>j–I–2</sup>+…+2<sup>0</sup>后，我们得到**2<sup>j–I</sup>**。
> **if(arr[左]+arr[右] > = K )**
> 将右指针减 1。

2.  重复以下过程，直到**左< =右**。

以下是上述方法的实现:

## C++

```
// C++ program to print count
// of subsets S such that
// min(S) + max(S) < K

#include <bits/stdc++.h>
using namespace std;

// Function that return the
// count of subset such that
// min(S) + max(S) < K
int get_subset_count(int arr[], int K,
                     int N)
{
    // Sorting the array
    sort(arr, arr + N);

    int left, right;
    left = 0;
    right = N - 1;

    // ans stores total number of subsets
    int ans = 0;

    while (left <= right) {
        if (arr[left] + arr[right] < K) {

            // add all possible subsets
            // between i and j
            ans += 1 << (right - left);
            left++;
        }
        else {
            // Decrease the sum
            right--;
        }
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 5, 7 };
    int K = 8;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << get_subset_count(arr, K, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print count
// of subsets S such that
// Math.min(S) + Math.max(S) < K
import java.util.*;

class GFG{

// Function that return the
// count of subset such that
// Math.min(S) + Math.max(S) < K
static int get_subset_count(int arr[], int K,
                                       int N)
{

    // Sorting the array
    Arrays.sort(arr);

    int left, right;
    left = 0;
    right = N - 1;

    // ans stores total number
    // of subsets
    int ans = 0;

    while (left <= right)
    {
        if (arr[left] + arr[right] < K)
        {

            // Add all possible subsets
            // between i and j
            ans += 1 << (right - left);
            left++;
        }
        else
        {

            // Decrease the sum
            right--;
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 4, 5, 7 };
    int K = 8;
    int N = arr.length;

    System.out.print(get_subset_count(arr, K, N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to print
# count of subsets S such
# that min(S) + max(S) < K

# Function that return the
# count of subset such that
# min(S) + max(S) < K
def get_subset_count(arr, K, N):

    # Sorting the array
    arr.sort()

    left = 0;
    right = N - 1;

    # ans stores total number of subsets
    ans = 0;

    while (left <= right):
        if (arr[left] + arr[right] < K):

            # Add all possible subsets
            # between i and j
            ans += 1 << (right - left);
            left += 1;
        else:

            # Decrease the sum
            right -= 1;

    return ans;

# Driver code
arr = [ 2, 4, 5, 7 ];
K = 8;

print(get_subset_count(arr, K, 4))

# This code is contributed by grand_master
```

## C#

```
// C# program to print count
// of subsets S such that
// Math.Min(S) + Math.Max(S) < K
using System;

class GFG{

// Function that return the
// count of subset such that
// Math.Min(S) + Math.Max(S) < K
static int get_subset_count(int []arr, int K,
                                       int N)
{

    // Sorting the array
    Array.Sort(arr);

    int left, right;
    left = 0;
    right = N - 1;

    // ans stores total number
    // of subsets
    int ans = 0;

    while (left <= right)
    {
        if (arr[left] + arr[right] < K)
        {

            // Add all possible subsets
            // between i and j
            ans += 1 << (right - left);
            left++;
        }
        else
        {

            // Decrease the sum
            right--;
        }
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 4, 5, 7 };
    int K = 8;
    int N = arr.Length;

    Console.Write(get_subset_count(arr, K, N));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program to print count
// of subsets S such that
// Math.min(S) + Math.max(S) < K

// Function that return the
// count of subset such that
// Math.min(S) + Math.max(S) < K
function get_subset_count(arr,K,N)
{
    // Sorting the array
    (arr).sort(function(a,b){return a-b;});

    let left, right;
    left = 0;
    right = N - 1;

    // ans stores total number
    // of subsets
    let ans = 0;

    while (left <= right)
    {
        if (arr[left] + arr[right] < K)
        {

            // Add all possible subsets
            // between i and j
            ans += 1 << (right - left);
            left++;
        }
        else
        {

            // Decrease the sum
            right--;
        }
    }
    return ans;
}

// Driver code
let arr=[ 2, 4, 5, 7];
let K = 8;
let N = arr.length;
document.write(get_subset_count(arr, K, N));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
4
```

**时间复杂度:***O(N * log N)*
T5】辅助空间: *O(1)*