# 精确去除 K 个元素后，最大化连续元素的差值之和

> 原文:[https://www . geeksforgeeks . org/最大化移除精确 k 元素后连续元素的差异总和/](https://www.geeksforgeeks.org/maximize-the-sum-of-differences-of-consecutive-elements-after-removing-exactly-k-elements/)

给定长度为 **N** 的排序数组**arr【】**和整数 **K** ，使得 **K < N** ，任务是从数组中精确地移除 **K** 元素，使得数组中连续元素的差之和最大化。
**示例:**

> **输入:** arr[] = {1，2，3，4}，K = 1
> **输出:** 3
> 我们来考虑所有可能的情况:
> a)移除 arr[0]: arr[] = {2，3，4}，ans = 2
> b)移除 arr[1]: arr[] = {1，3，4}，ans = 3
> c)移除 arr[2]: arr[] = {1，2，4}，ans = 3
> d)
> **输入:** arr[] = {1，2，10}，K = 2
> **输出:** 0

**进场:**有两种情况:

1.  如果**K<N–1**那么答案将是**arr【N–1】–arr【0】**。这是因为数组的 N–2 个内部元素中的任何 K 个元素都可以被删除，而不会影响最大的差值总和。例如，如果必须从 1、2、3 和 4 中移除任何单个元素，则无论移除 2 还是移除 3，最终的差值总和都将保持不变(即(3–1)+(4–3))= 3，等于((2–1)+(4–2))= 3。
2.  如果**K = N–1**，那么答案将是 **0** ，因为只剩下一个既最小又最大的元素。因此，答案是 **0** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximized sum
int findSum(int* arr, int n, int k)
{

    // Remove any k internal elements
    if (k <= n - 2)
        return (arr[n - 1] - arr[0]);

    return 0;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(int);
    int k = 1;

    cout << findSum(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the maximized sum
    static int findSum(int []arr, int n, int k)
    {

        // Remove any k internal elements
        if (k <= n - 2)
            return (arr[n - 1] - arr[0]);

        return 0;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 3, 4 };
        int n = arr.length;
        int k = 1;

        System.out.println(findSum(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximized sum
def findSum(arr, n, k) :

    # Remove any k internal elements
    if (k <= n - 2) :
        return (arr[n - 1] - arr[0]);

    return 0;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4 ];
    n = len(arr);
    k = 1;

    print(findSum(arr, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the maximized sum
    static int findSum(int []arr,
                       int n, int k)
    {

        // Remove any k internal elements
        if (k <= n - 2)
            return (arr[n - 1] - arr[0]);

        return 0;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { 1, 2, 3, 4 };
        int n = arr.Length;
        int k = 1;

        Console.WriteLine(findSum(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximized sum
function findSum(arr, n, k)
{

    // Remove any k internal elements
    if (k <= n - 2)
        return (arr[n - 1] - arr[0]);

    return 0;
}

// Driver code
var arr = [1, 2, 3, 4];
var n = arr.length;
var k = 1;
document.write( findSum(arr, n, k));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(1)

**辅助空间:** O(1)