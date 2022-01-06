# 对给定数组中乘积位于给定范围内的对进行计数

> 原文:[https://www . geeksforgeeks . org/给定数组中产品位于给定范围内的计数对/](https://www.geeksforgeeks.org/count-pairs-from-a-given-array-whose-product-lies-in-a-given-range/)

给定一个大小为 **N、**和整数 **L** 和 **R** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**arr【】】**，任务是计算[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)**【arr】I，arr<sub>j</sub>**的数量，使得 **i < j** 和**arr【I】* arr【j】的乘积**

**示例:**

> **输入:** arr[ ] = {4，1，2，5}，L = 4，R = 9
> **输出:** 3
> **说明:**有效 p *空气为{4，1}、{1，5}和{4，2}。*
> 
> **输入:** arr[ ] = { *1，2，5，10，5* }，L = 2，R = 15
> T5】输出:6
> T8】说明:有效 p*air 为{1，2}、{1，5}、{1，10}、{1，5}、{2，5}、{2，5}。*

**天真方法:**解决问题最简单的方法是从数组中生成所有可能的[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)，对于每一对，检查其乘积是否在范围**【L，R】**内。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效途径:**这个问题可以通过[排序](https://www.geeksforgeeks.org/sorting-algorithms/)和[二分搜索法](https://www.geeksforgeeks.org/upper_bound-and-lower_bound-for-vector-in-cpp-stl/)技术解决。按照以下步骤解决此问题:

*   [排序数组](https://www.geeksforgeeks.org/sorting-algorithms/) **arr[]。**
*   初始化一个变量，将**和**设为 **0、**来存储产品在**【L，R】范围内的[对的数量。](https://www.geeksforgeeks.org/pair-in-cpp-stl/)**
*   [使用变量 **i** 迭代](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/) [范围](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)**【0，N-1】**，并执行以下步骤 **:**
    *   求一个元素的[上限](https://www.geeksforgeeks.org/upper_bound-in-cpp/)，使该元素小于等于 **R / arr[i]。**
    *   求一个元素的[下界](https://www.geeksforgeeks.org/lower_bound-in-cpp/)，使得该元素大于或等于 **L / arr[i]。**
    *   将**上限-下限**添加到**和**
*   完成以上步骤后，打印**和**。

下面是上述方法的实现。

## C++

```
// C++ program for above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count pairs from an array
// whose product lies in the range [l, r]
void countPairs(int arr[], int l,
                int r, int n)
{
    // Sort the array arr[]
    sort(arr, arr + n);

    // Stores the final answer
    int ans = 0;

    for (int i = 0; i < n; i++) {

        // Upper Bound for arr[j] such
        // that arr[j] <= r/arr[i]
        auto itr1 = upper_bound(
                        arr + i + 1,
                        arr + n, r / arr[i])
                    - arr;

        // Lower Bound for arr[j] such
        // that arr[j] >= l/arr[i]
        auto itr2 = lower_bound(
                        arr + i + 1, arr + n,
                        ceil(double(l) / double(arr[i])))
                    - arr;

        ans += itr1 - itr2;
    }

    // Print the answer
    cout << ans << endl;
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 2,2 };
    int l = 5, r = 9;

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countPairs(arr, l, r, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.Arrays;

class GFG{

// Function to count pairs from an array
// whose product lies in the range [l, r]
public static void countPairs(int[] arr, int l,
                              int r, int n)
{

    // Sort the array arr[]
    Arrays.sort(arr);

    // Stores the final answer
    int ans = 0;

    for(int i = 0; i < n; i++)
    {

        // Upper Bound for arr[j] such
        // that arr[j] <= r/arr[i]
        int itr1 = upper_bound(arr, 0, arr.length - 1,
                               l / arr[i]);

        // Lower Bound for arr[j] such
        // that arr[j] >= l/arr[i]
        int itr2 = lower_bound(arr, 0, arr.length - 1,
                               l / arr[i]);
        ans += itr1 - itr2;
    }

    // Print the answer
    System.out.println(ans);
}

public static int lower_bound(int[] arr, int low,
                              int high, int X)
{

    // Base Case
    if (low > high)
    {
        return low;
    }

    // Find the middle index
    int mid = low + (high - low) / 2;

    // If arr[mid] is greater than
    // or equal to X then search
    // in left subarray
    if (arr[mid] >= X)
    {
        return lower_bound(arr, low, mid - 1, X);
    }

    // If arr[mid] is less than X
    // then search in right subarray
    return lower_bound(arr, mid + 1, high, X);
}

public static int upper_bound(int[] arr, int low,
                              int high, int X)
{

    // Base Case
    if (low > high)
        return low;

    // Find the middle index
    int mid = low + (high - low) / 2;

    // If arr[mid] is less than
    // or equal to X search in
    // right subarray
    if (arr[mid] <= X)
    {
        return upper_bound(arr, mid + 1, high, X);
    }

    // If arr[mid] is greater than X
    // then search in left subarray
    return upper_bound(arr, low, mid - 1, X);
}

// Driver Code
public static void main(String args[])
{

    // Given Input
    int[] arr = { 4, 1, 2, 5 };
    int l = 4, r = 9;
    int n = arr.length;

    // Function Call
    countPairs(arr, l, r, n);
}
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python program for above approach

# Function to count pairs from an array
# whose product lies in the range [l, r]
def countPairs(arr, l, r, n):

    # Sort the array arr[]
    arr[::-1]

    # Stores the final answer
    ans = 0;

    for i in range(n):

        # Upper Bound for arr[j] such
        # that arr[j] <= r/arr[i]
        itr1 = upper_bound(arr, 0, len(arr) - 1, l // arr[i])

        # Lower Bound for arr[j] such
        # that arr[j] >= l/arr[i]
        itr2 = lower_bound(arr, 0, len(arr) - 1, l // arr[i]);

        ans += itr1 - itr2;

    # Print the answer
    print(ans);

def lower_bound(arr, low, high, X):

    # Base Case
    if (low > high):
        return low;

    # Find the middle index
    mid = low + (high - low) // 2;

    # If arr[mid] is greater than
    # or equal to X then search
    # in left subarray
    if (arr[mid] >= X):
        return lower_bound(arr, low, mid - 1, X);

    # If arr[mid] is less than X
    # then search in right subarray
    return lower_bound(arr, mid + 1, high, X);

def upper_bound(arr, low, high, X):

    # Base Case
    if (low > high):
        return low;

    # Find the middle index
    mid = low + (high - low) // 2;

    # If arr[mid] is less than
    # or equal to X search in
    # right subarray
    if (arr[mid] <= X):
        return upper_bound(arr, mid + 1, high, X);

    # If arr[mid] is greater than X
    # then search in left subarray
    return upper_bound(arr, low, mid - 1, X);

# Driver Code

# Given Input
arr = [4, 1, 2, 5];
l = 4;
r = 9;

n = len(arr)

# Function Call
countPairs(arr, l, r, n);

# This code is contributed by _Saurabh_Jaiswal.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count pairs from an array
// whose product lies in the range [l, r]
public static void countPairs(int[] arr, int l,
                              int r, int n)
{

    // Sort the array arr[]
    Array.Sort(arr);

    // Stores the final answer
    int ans = 0;

    for(int i = 0; i < n; i++)
    {

        // Upper Bound for arr[j] such
        // that arr[j] <= r/arr[i]
        int itr1 = upper_bound(arr, 0, arr.Length - 1,
                               l / arr[i]);

        // Lower Bound for arr[j] such
        // that arr[j] >= l/arr[i]
        int itr2 = lower_bound(arr, 0, arr.Length - 1,
                               l / arr[i]);
        ans += itr1 - itr2;
    }

    // Print the answer
    Console.WriteLine(ans);
}

public static int lower_bound(int[] arr, int low,
                              int high, int X)
{

    // Base Case
    if (low > high)
    {
        return low;
    }

    // Find the middle index
    int mid = low + (high - low) / 2;

    // If arr[mid] is greater than
    // or equal to X then search
    // in left subarray
    if (arr[mid] >= X)
    {
        return lower_bound(arr, low, mid - 1, X);
    }

    // If arr[mid] is less than X
    // then search in right subarray
    return lower_bound(arr, mid + 1, high, X);
}

public static int upper_bound(int[] arr, int low,
                              int high, int X)
{

    // Base Case
    if (low > high)
        return low;

    // Find the middle index
    int mid = low + (high - low) / 2;

    // If arr[mid] is less than
    // or equal to X search in
    // right subarray
    if (arr[mid] <= X)
    {
        return upper_bound(arr, mid + 1, high, X);
    }

    // If arr[mid] is greater than X
    // then search in left subarray
    return upper_bound(arr, low, mid - 1, X);
}

// Driver code
public static void Main(string[] args)
{

    // Given Input
    int[] arr = { 4, 1, 2, 5 };
    int l = 4, r = 9;
    int n = arr.Length;

    // Function Call
    countPairs(arr, l, r, n);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Function to count pairs from an array
// whose product lies in the range [l, r]
function countPairs(arr, l, r, n)
{

    // Sort the array arr[]
    arr.sort((a, b) => a - b);

    // Stores the final answer
    let ans = 0;

    for (let i = 0; i < n; i++)
    {

        // Upper Bound for arr[j] such
        // that arr[j] <= r/arr[i]
        let itr1 = upper_bound(arr, 0, arr.length - 1, Math.floor(l / arr[i]));

        // Lower Bound for arr[j] such
        // that arr[j] >= l/arr[i]
         let itr2 = lower_bound(arr, 0, arr.length - 1, Math.floor(l / arr[i]));
         ans += itr1 - itr2;
    }

    // Print the answer
    document.write(ans + "<br>");
}

function lower_bound(arr, low, high, X) {

    // Base Case
    if (low > high) {
        return low;
    }

    // Find the middle index
    let mid = Math.floor(low + (high - low) / 2);

    // If arr[mid] is greater than
    // or equal to X then search
    // in left subarray
    if (arr[mid] >= X) {
        return lower_bound(arr, low, mid - 1, X);
    }

    // If arr[mid] is less than X
    // then search in right subarray
    return lower_bound(arr, mid + 1, high, X);
}

function upper_bound(arr, low, high, X) {

    // Base Case
    if (low > high)
        return low;

    // Find the middle index
    let mid = Math.floor(low + (high - low) / 2);

    // If arr[mid] is less than
    // or equal to X search in
    // right subarray
    if (arr[mid] <= X) {
        return upper_bound(arr, mid + 1, high, X);
    }

    // If arr[mid] is greater than X
    // then search in left subarray
    return upper_bound(arr, low, mid - 1, X);
}

// Driver Code

// Given Input
let arr = [4, 1, 2, 5];
let l = 4, r = 9;

let n = arr.length

// Function Call
countPairs(arr, l, r, n);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*