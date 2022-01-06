# 计算可以从数组中选择的元素的最大数量

> 原文:[https://www . geesforgeks . org/count-从数组中可以选择的最大元素数/](https://www.geeksforgeeks.org/count-the-maximum-number-of-elements-that-can-be-selected-from-the-array/)

给定一个数组 **arr[]** ，任务是按照以下选择过程计算可以从给定数组中选择的元素的最大数量:

*   在*第一次*选择时，选择大于或等于 1 的元素。
*   在*第二次*选择时，选择大于或等于 2 的元素。
*   在*第三次*选择时，选择大于或等于 3 的元素，以此类推。

一个元素只能选择一次。当无法选择任何元素时，操作停止。因此，任务是最大化从数组中选择的数量。

**示例:**

> **输入:** arr[] = { 4，1，3，1 }
> **输出:** 3
> 第一次选择:1 选择为 1 > = 1。
> 第二次选择:选择 3 作为 3 > = 2。
> 第三次选择:选择 4 作为 4 > = 3。
> 不能再选择了。因此，答案是 3。
> 
> **输入:** arr[] = { 2，1，1，2，1 }
> **输出:** 2

**方法:**为了最大化选择的计数，有必要首先选择最小的可能数，如果选择不可能，则选择较大的数。这可以通过对数组进行排序来轻松完成。现在，循环遍历数组，当元素大于或等于当前操作要选择的数字时，将结果增加 1。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum count of
// selection possible from the given array
// following the given process
int maxSelectionCount(int a[], int n)
{
    // Initialize result
    int res = 0;

    // Sorting the array
    sort(a, a + n);

    // Initialize the select variable
    int select = 1;

    // Loop through array
    for (int i = 0; i < n; i++) {
        // If selection is possible
        if (a[i] >= select) {
            res++; // Increment result
            select++; // Increment selection variable
        }
    }

    return res;
}

// Driver Code
int main()
{
    int arr[] = { 4, 2, 1, 3, 5, 1, 4 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxSelectionCount(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the maximum count of
    // selection possible from the given array
    // following the given process
    static int maxSelectionCount(int a[], int n)
    {
        // Initialize result
        int res = 0;

        // Sorting the array
        Arrays.sort(a);

        // Initialize the select variable
        int select = 1;

        // Loop through array
        for (int i = 0; i < n; i++)
        {
            // If selection is possible
            if (a[i] >= select)
            {
                res++; // Increment result
                select++; // Increment selection variable
            }
        }

        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = {4, 2, 1, 3, 5, 1, 4};

        int N = arr.length;

        System.out.println(maxSelectionCount(arr, N));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the maximum count of
# selection possible from the given array
# following the given process
def maxSelectionCount(a, n):
    # Initialize result
    res = 0;

    # Sorting the array
    a.sort();

    # Initialize the select variable
    select = 1;

    # Loop through array
    for i in range(n):
        # If selection is possible
        if (a[i] >= select):
            res += 1; # Increment result
            select += 1; # Increment selection variable

    return res;

# Driver Code
arr = [ 4, 2, 1, 3, 5, 1, 4 ];
N = len(arr);
print(maxSelectionCount(arr, N));

# This code contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return the maximum count of
    // selection possible from the given array
    // following the given process
    static int maxSelectionCount(int []a, int n)
    {
        // Initialize result
        int res = 0;

        // Sorting the array
        Array.Sort(a);

        // Initialize the select variable
        int select = 1;

        // Loop through array
        for (int i = 0; i < n; i++)
        {
            // If selection is possible
            if (a[i] >= select)
            {
                res++; // Increment result
                select++; // Increment selection variable
            }
        }

        return res;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {4, 2, 1, 3, 5, 1, 4};

        int N = arr.Length;

        Console.WriteLine(maxSelectionCount(arr, N));
    }
}

// This code contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum count of
// selection possible from the given array
// following the given process
function maxSelectionCount(a, n)
{

    // Initialize result
    var res = 0;

    // Sorting the array
    a.sort();

    // Initialize the select variable
    var select = 1;

    // Loop through array
    for(var i = 0; i < n; i++)
    {

        // If selection is possible
        if (a[i] >= select)
        {
            // Increment result
            res++;

            // Increment selection variable
            select++;
        }
    }
    return res;
}

// Driver Code
var arr = [ 4, 2, 1, 3, 5, 1, 4 ];
var N = arr.length;

document.write(maxSelectionCount(arr, N));

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N * log(N))
**辅助空间:** O(1)