# 乘积大于等于 0 的最长子阵列长度

> 原文:[https://www . geesforgeks . org/产品大于或等于 0 的最长子阵列长度/](https://www.geeksforgeeks.org/length-of-longest-subarray-with-product-greater-than-or-equal-to-0/)

给定一个由 **N 个**整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出乘积大于等于 0 的最长[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度。
**示例:**

> **输入:** arr[] = {-1，1，1，-2，3，2，-1 }
> **输出:** 6
> **解释:**
> 乘积≥ 0 的最长子阵= {1，1，-2，3，2，-1 }和{-1，1，1，-2，3，2}。
> 每根长度= 6。
> 
> **输入:** arr[] = {-1，-2，-3，-4}
> **输出:** 4
> **解释:**
> 乘积≥ 0 的最长子阵= {-1，-2，-3，-4}。
> 长度= 4。

**进场:**

1.  检查给定数组中所有元素的[乘积是否大于或等于零。](https://www.geeksforgeeks.org/program-for-product-of-array/)
2.  如果是，乘积大于或等于零的最长子阵列的长度为阵列的**长度**。
3.  如果上面的说法不成立，那么数组包含奇数个负元素。在这种情况下，要找到最长的子阵列，请执行以下操作:
    *   对于数组中出现的每个负元素，当前元素左右的子数组给出大于或等于 0 的乘积。因此，所需最长子阵列的长度为:

```
L = max(L, max(i, N - i - 1))
```

*   不断更新数组中每个负元素的子数组长度。
*   **L** 的值是乘积大于等于 0 的最长子阵的长度。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that count the length
// of longest subarray with product
// greater than or equals to zero
int maxLength(int arr[], int N)
{
    int product = 1, len = 0;

    for (int i = 0; i < N; i++) {
        product *= arr[i];
    }

    // If product is greater than
    // zero, return array size
    if (product >= 0) {
        return N;
    }

    // Traverse the array and if
    // any negative element found
    // then update the length of
    // longest subarray with the
    // length of left and right subarray
    for (int i = 0; i < N; i++) {
        if (arr[i] < 0) {
            len = max(len,
                      max(N - i - 1, i));
        }
    }

    return len;
}

// Driver Code
int main()
{
    int arr[] = { -1, 1, 1, -2, 3, 2, -1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxLength(arr, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

public class GFG{
// Function that count the length
// of longest subarray with product
// greater than or equals to zero
    static int maxLength(int arr[], int N)
    {
        int product = 1, len = 0;

        for (int i = 0; i < N; i++) {
            product *= arr[i];
        }

        // If product is greater than
        // zero, return array size
        if (product >= 0) {
            return N;
        }

        // Traverse the array and if
        // any negative element found
        // then update the length of
        // longest subarray with the
        // length of left and right subarray
        for (int i = 0; i < N; i++) {
            if (arr[i] < 0) {
                len = Math.max(len, Math.max(N - i - 1, i));
            }
        }

        return len;
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { -1, 1, 1, -2, 3, 2, -1 };
        int N = arr.length;
        System.out.println(maxLength(arr, N));

    }
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function that count the Length
# of longest subarray with product
# greater than or equals to zero
def maxLength(arr, N):
    product = 1
    Len = 0

    for i in arr:
        product *= i

    # If product is greater than
    # zero, return array size
    if (product >= 0):
        return N

    # Traverse the array and if
    # any negative element found
    # then update the Length of
    # longest subarray with the
    # Length of left and right subarray
    for i in range(N):
        if (arr[i] < 0):
            Len = max(Len,max(N - i - 1, i))

    return Len

# Driver Code
if __name__ == '__main__':
    arr = [-1, 1, 1, -2, 3, 2, -1]
    N = len(arr)

    print(maxLength(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{
// Function that count the length
// of longest subarray with product
// greater than or equals to zero
    static int maxLength(int []arr, int N)
    {
        int product = 1, len = 0;

        for (int i = 0; i < N; i++) {
            product *= arr[i];
        }

        // If product is greater than
        // zero, return array size
        if (product >= 0) {
            return N;
        }

        // Traverse the array and if
        // any negative element found
        // then update the length of
        // longest subarray with the
        // length of left and right subarray
        for (int i = 0; i < N; i++) {
            if (arr[i] < 0) {
                len = Math.Max(len, Math.Max(N - i - 1, i));
            }
        }

        return len;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = { -1, 1, 1, -2, 3, 2, -1 };
        int N = arr.Length;
        Console.WriteLine(maxLength(arr, N));

    }
}

// This code is contributed by abhaysingh290895
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function that count the length
// of longest subarray with product
// greater than or equals to zero
function maxLength(arr, N)
{
    var product = 1, len = 0;

    for (var i = 0; i < N; i++) {
        product *= arr[i];
    }

    // If product is greater than
    // zero, return array size
    if (product >= 0) {
        return N;
    }

    // Traverse the array and if
    // any negative element found
    // then update the length of
    // longest subarray with the
    // length of left and right subarray
    for (var i = 0; i < N; i++) {
        if (arr[i] < 0) {
            len = Math.max(len,
                      Math.max(N - i - 1, i));
        }
    }

    return len;
}

// Driver Code
var arr = [ -1, 1, 1, -2, 3, 2, -1 ];
var N = arr.length;
document.write(maxLength(arr, N));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N)* ，其中 N 为数组长度。
***辅助空间:** O(1)*