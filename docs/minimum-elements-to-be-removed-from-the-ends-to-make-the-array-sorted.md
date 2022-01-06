# 从末端移除的最小元素，使数组排序

> 原文:[https://www . geeksforgeeks . org/要从末端移除的最小元素进行数组排序/](https://www.geeksforgeeks.org/minimum-elements-to-be-removed-from-the-ends-to-make-the-array-sorted/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是从数组末端移除最小数量的元素，使数组不递减。只能从左端或右端移除元素。

**示例:**

> **输入:** arr[] = {1，2，4，1，5}
> **输出:** 2
> 我们无法使数组在一次移除后排序。
> 但是如果我们从右端去掉 2 个元素，
> 数组就变成了排序后的{1，2，4}。
> **输入:** arr[] = {3，2，1}
> **输出:** 2

**方法:**这个问题的一个非常简单的解决方案是找到给定阵列的最长非递减子阵列的长度。假设长度为 **L** 。因此，需要移除的元素数量将是**N–L**。使用本文[中讨论的方法可以很容易地找到最长的非递减子阵列的长度。](https://www.geeksforgeeks.org/longest-increasing-subarray/)

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number
// of elements to be removed from the ends
// of the array to make it sorted
int findMin(int* arr, int n)
{

    // To store the final answer
    int ans = 1;

    // Two pointer loop
    for (int i = 0; i < n; i++) {
        int j = i + 1;

        // While the array is increasing increment j
        while (j < n and arr[j] >= arr[j - 1])
            j++;

        // Updating the ans
        ans = max(ans, j - i);

        // Updating the left pointer
        i = j - 1;
    }

    // Returning the final answer
    return n - ans;
}

// Driver code
int main()
{
    int arr[] = { 3, 2, 1 };
    int n = sizeof(arr) / sizeof(int);

    cout << findMin(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the minimum number
    // of elements to be removed from the ends
    // of the array to make it sorted
    static int findMin(int arr[], int n)
    {

        // To store the final answer
        int ans = 1;

        // Two pointer loop
        for (int i = 0; i < n; i++)
        {
            int j = i + 1;

            // While the array is increasing increment j
            while (j < n && arr[j] >= arr[j - 1])
                j++;

            // Updating the ans
            ans = Math.max(ans, j - i);

            // Updating the left pointer
            i = j - 1;
        }

        // Returning the final answer
        return n - ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 3, 2, 1 };
        int n = arr.length;
        System.out.println(findMin(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum number
# of elements to be removed from the ends
# of the array to make it sorted
def findMin(arr, n):

    # To store the final answer
    ans = 1

    # Two pointer loop
    for i in range(n):
        j = i + 1

        # While the array is increasing increment j
        while (j < n and arr[j] >= arr[j - 1]):
            j += 1

        # Updating the ans
        ans = max(ans, j - i)

        # Updating the left pointer
        i = j - 1

    # Returning the final answer
    return n - ans

# Driver code
arr = [3, 2, 1]
n = len(arr)

print(findMin(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum number
// of elements to be removed from the ends
// of the array to make it sorted
static int findMin(int []arr, int n)
{

    // To store the readonly answer
    int ans = 1;

    // Two pointer loop
    for (int i = 0; i < n; i++)
    {
        int j = i + 1;

        // While the array is increasing increment j
        while (j < n && arr[j] >= arr[j - 1])
            j++;

        // Updating the ans
        ans = Math.Max(ans, j - i);

        // Updating the left pointer
        i = j - 1;
    }

    // Returning the readonly answer
    return n - ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3, 2, 1 };
    int n = arr.Length;
    Console.WriteLine(findMin(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Java script implementation of the approach

    // Function to return the minimum number
    // of elements to be removed from the ends
    // of the array to make it sorted
    function findMin(arr,n)
    {

        // To store the final answer
        let ans = 1;

        // Two pointer loop
        for (let i = 0; i < n; i++)
        {
            let j = i + 1;

            // While the array is increasing increment j
            while (j < n && arr[j] >= arr[j - 1])
                j++;

            // Updating the ans
            ans = Math.max(ans, j - i);

            // Updating the left pointer
            i = j - 1;
        }

        // Returning the final answer
        return n - ans;
    }

    // Driver code
        let arr = [ 3, 2, 1 ];
        let n = arr.length;
        document.write(findMin(arr, n));

// This code is contributed by sravan kumar G
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)

**辅助空间:** O(1)