# 负积最长子阵列长度

> 原文:[https://www . geeksforgeeks . org/带负积的最长子阵列长度/](https://www.geeksforgeeks.org/length-of-longest-subarray-with-negative-product/)

给定一个由 **N** 元素组成的数组 **arr[]** 。任务是找到最长子阵列的长度，使得子阵列的乘积为负。如果没有这样的子阵列，请打印-1。
**例:**

> **输入:** N = 6，arr[] = {-1，2，3，2，1，-4}
> **输出:** 5
> **解释:**
> 在示例中，范围【1，5】中的子阵列
> 具有负的积-12，
> 因此长度为 5。
> **输入:** N = 4，arr[] = {1，2，3，2}
> **输出:** -1

**进场:**

*   首先，检查数组的总积是否为负。如果数组的总积是负的，那么答案将是 n
*   如果数组的总积不是负数，则表示它是正数。所以，我们的想法是从数组中找到一个负元素，这样排除这个元素，比较数组两部分的长度，我们就可以得到负乘积的子数组的最大长度。
*   很明显-

> 负积的子阵列将存在于[1，x]或(x，N)范围内，其中 1 <= x <= N，arr[x]为负。

以下是上述方法的实施情况-

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find length of the
// longest subarray such that product
// of the subarray is negative
int maxLength(int a[], int n)
{
    int product = 1, len = -1;

    // Check if product of complete
    // array is negative
    for (int i = 0; i < n; i++)
        product *= a[i];

    // Total product is already
    // negative
    if (product < 0)
        return n;

    // Find an index i such the a[i]
    // is negative and compare length
    // of both halfs excluding a[i] to
    // find max length subarray
    for (int i = 0; i < n; i++) {
        if (a[i] < 0)
            len = max(len,
                      max(n - i - 1, i));
    }

    return len;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, -3, 2, 5, -6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxLength(arr, N)
         << "\n";

    int arr1[] = { 1, 2, 3, 4 };
    N = sizeof(arr1) / sizeof(arr1[0]);

    cout << maxLength(arr1, N)
         << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Arrays;

class GFG{

// Function to find length of the
// longest subarray such that product
// of the subarray is negative
static int maxLength(int a[], int n)
{
    int product = 1, len = -1;

    // Check if product of complete
    // array is negative
    for(int i = 0; i < n; i++)
        product *= a[i];

    // Total product is already
    // negative
    if (product < 0)
        return n;

    // Find an index i such the a[i]
    // is negative and compare length
    // of both halfs excluding a[i] to
    // find max length subarray
    for(int i = 0; i < n; i++)
    {
        if (a[i] < 0)
            len = Math.max(len,
                  Math.max(n - i - 1, i));
    }
    return len;
}

// Driver code
public static void main (String[] args)
{

    // Given array arr[]
    int arr[] = new int[]{ 1, 2, -3,
                           2, 5, -6 };
    int N = arr.length;

    System.out.println(maxLength(arr, N));

    // Given array arr[]
    int arr1[] = new int[]{ 1, 2, 3, 4 };
    N = arr1.length;

    System.out.println(maxLength(arr1, N));
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
# Function to find length of the
# longest subarray such that product
# of the subarray is negative
def maxLength(a, n):
    product = 1
    length = -1

    # Check if product of complete
    # array is negative
    for i in range (n):
        product *= a[i]

    # Total product is already
    # negative
    if (product < 0):
        return n

    # Find an index i such the a[i]
    # is negative and compare length
    # of both halfs excluding a[i] to
    # find max length subarray
    for i in range (n):
        if (a[i] < 0):
            length = max(length,
                         max(n - i - 1, i))

    return length

# Driver Code
if __name__ == "__main__": 
    arr = [1, 2, -3, 2, 5, -6]
    N = len(arr)
    print (maxLength(arr, N))
    arr1 = [1, 2, 3, 4]
    N = len(arr1)
    print (maxLength(arr1, N))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to find length of the
// longest subarray such that product
// of the subarray is negative
static int maxLength(int []a, int n)
{
    int product = 1, len = -1;

    // Check if product of complete
    // array is negative
    for(int i = 0; i < n; i++)
        product *= a[i];

    // Total product is already
    // negative
    if (product < 0)
        return n;

    // Find an index i such the a[i]
    // is negative and compare length
    // of both halfs excluding a[i] to
    // find max length subarray
    for(int i = 0; i < n; i++)
    {
        if (a[i] < 0)
            len = Math.Max(len,
                  Math.Max(n - i - 1, i));
    }
    return len;
}

// Driver code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = new int[]{ 1, 2, -3,
                           2, 5, -6 };
    int N = arr.Length;

    Console.WriteLine(maxLength(arr, N));

    // Given array []arr
    int []arr1 = new int[]{ 1, 2, 3, 4 };
    N = arr1.Length;

    Console.WriteLine(maxLength(arr1, N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find length of the
// longest subarray such that product
// of the subarray is negative
function maxLength(a, n)
{
    let product = 1, len = -1;

    // Check if product of complete
    // array is negative
    for(let i = 0; i < n; i++)
        product *= a[i];

    // Total product is already
    // negative
    if (product < 0)
        return n;

    // Find an index i such the a[i]
    // is negative and compare length
    // of both halfs excluding a[i] to
    // find max length subarray
    for(let i = 0; i < n; i++)
    {
        if (a[i] < 0)
            len = Math.max(len,
                  Math.max(n - i - 1, i));
    }
    return len;
}

// Driver code

    // Given array []arr
    let arr = [ 1, 2, -3,
                           2, 5, -6 ];
    let N = arr.length;

    document.write(maxLength(arr, N) + "<br/>");

    // Given array []arr
    let arr1 = [ 1, 2, 3, 4 ];
    N = arr1.Length;
    document.write(maxLength(arr1, N) + "<br/>");

 // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
5
-1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)