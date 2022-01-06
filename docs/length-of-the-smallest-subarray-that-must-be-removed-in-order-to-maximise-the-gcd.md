# 最小子阵列的长度，为了最大化 GCD

> 原文:[https://www . geeksforgeeks . org/最小子阵列长度必须移除，以便最大化 gcd/](https://www.geeksforgeeks.org/length-of-the-smallest-subarray-that-must-be-removed-in-order-to-maximise-the-gcd/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是找到最小子数组的长度，这样当这个子数组从数组中移除时，得到的数组的 GCD 最大。
**注意:**生成的数组应该是非空的。
**示例:**

> **输入:** N = 4，arr[] = {3，6，1，2}
> **输出:** 2
> **解释:**
> 如果我们去掉子阵列{1，2}，那么得到的子阵列将是{3，6}，这个的 GCD 是 3，这是最大可能值。
> **输入:** N = 3，arr[] = {4，8，4}
> **输出:** 0
> **说明:**
> 这里我们不需要移除任何子阵列，最大可能 GCD 为 4。

**方法:**已知 GCD 是一个非递增函数。也就是说，如果我们在数组中添加元素，那么 gcd 要么减少，要么保持不变。所以，想法就是用这个概念来解决这个问题:

*   现在我们必须注意，在移除子阵列后，最终的子阵列应该具有第一个或最后一个元素，或者两个元素都有。这是因为我们需要确保移除子阵列后得到的阵列应该是非空的。所以，我们不能去除所有的元素。
*   所以最大可能 GCD 将是 **max(A[0]，A[N–1])**。
*   现在我们必须最小化子阵列的长度，为了得到这个答案，我们需要去掉子阵列。
*   为此，我们将使用[两个指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)，分别指向第一个和最后一个元素。
*   现在，如果元素可被 gcd 整除，我们将增加第一个指针，如果元素可被 gcd 整除，我们将减少最后一个指针，因为它不会影响我们的答案。
*   因此，最后，两个指针之间的元素数量将是我们需要移除的子阵列的长度。

以下是上述方法的实现:

## C++

```
// C++ program to find the length of
// the smallest subarray that must be
// removed in order to maximise the GCD

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// the smallest subarray that must be
// removed in order to maximise the GCD
int GetMinSubarrayLength(int a[], int n)
{

    // Store the maximum possible
    // GCD of the resulting subarray
    int ans = max(a[0], a[n - 1]);

    // Two pointers initially pointing
    // to the first and last element
    // respectively
    int lo = 0, hi = n - 1;

    // Moving the left pointer to the
    // right if the elements are
    // divisible by the maximum GCD
    while (lo < n and a[lo] % ans == 0)
        lo++;

    // Moving the right pointer to the
    // left if the elements are
    // divisible by the maximum GCD
    while (hi > lo and a[hi] % ans == 0)
        hi--;

    // Return the length of
    // the subarray
    return (hi - lo + 1);
}

// Driver code
int main()
{

    int arr[] = { 4, 8, 2, 1, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    int length = GetMinSubarrayLength(arr, N);

    cout << length << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of
// the smallest subarray that must be
// removed in order to maximise the GCD
class GFG {

    // Function to find the length of
    // the smallest subarray that must be
    // removed in order to maximise the GCD
    static int GetMinSubarrayLength(int a[], int n)
    {

        // Store the maximum possible
        // GCD of the resulting subarray
        int ans = Math.max(a[0], a[n - 1]);

        // Two pointers initially pointing
        // to the first and last element
        // respectively
        int lo = 0, hi = n - 1;

        // Moving the left pointer to the
        // right if the elements are
        // divisible by the maximum GCD
        while (lo < n && a[lo] % ans == 0)
            lo++;

        // Moving the right pointer to the
        // left if the elements are
        // divisible by the maximum GCD
        while (hi > lo && a[hi] % ans == 0)
            hi--;

        // Return the length of
        // the subarray
        return (hi - lo + 1);
    }

    // Driver code
    public static void main (String[] args)
    {

        int arr[] = { 4, 8, 2, 1, 4 };
        int N = arr.length;

        int Length = GetMinSubarrayLength(arr, N);

        System.out.println(Length);

    }
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python3 program to find the length of
# the smallest subarray that must be
# removed in order to maximise the GCD

# Function to find the length of
# the smallest subarray that must be
# removed in order to maximise the GCD
def GetMinSubarrayLength(a, n):

    # Store the maximum possible
    # GCD of the resulting subarray
    ans = max(a[0], a[n - 1])

    # Two pointers initially pointing
    # to the first and last element
    # respectively
    lo = 0
    hi = n - 1

    # Moving the left pointer to the
    # right if the elements are
    # divisible by the maximum GCD
    while (lo < n and a[lo] % ans == 0):
        lo += 1

    # Moving the right pointer to the
    # left if the elements are
    # divisible by the maximum GCD
    while (hi > lo and a[hi] % ans == 0):
        hi -= 1

    # Return the length of
    # the subarray
    return (hi - lo + 1)

# Driver code
if __name__ == '__main__':

    arr = [4, 8, 2, 1, 4]
    N = len(arr)

    length = GetMinSubarrayLength(arr, N)

    print(length)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the length of
// the smallest subarray that must be
// removed in order to maximise the GCD
using System;

class GFG {

    // Function to find the length of
    // the smallest subarray that must be
    // removed in order to maximise the GCD
    static int GetMinSubarrayLength(int []a, int n)
    {

        // Store the maximum possible
        // GCD of the resulting subarray
        int ans = Math.Max(a[0], a[n - 1]);

        // Two pointers initially pointing
        // to the first and last element
        // respectively
        int lo = 0, hi = n - 1;

        // Moving the left pointer to the
        // right if the elements are
        // divisible by the maximum GCD
        while (lo < n && a[lo] % ans == 0)
            lo++;

        // Moving the right pointer to the
        // left if the elements are
        // divisible by the maximum GCD
        while (hi > lo && a[hi] % ans == 0)
            hi--;

        // Return the length of
        // the subarray
        return (hi - lo + 1);
    }

    // Driver code
    public static void Main (string[] args)
    {

        int []arr = { 4, 8, 2, 1, 4 };
        int N = arr.Length;

        int Length = GetMinSubarrayLength(arr, N);

        Console.WriteLine(Length);

    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// Javascript program to find the length of
// the smallest subarray that must be
// removed in order to maximise the GCD

// Function to find the length of
// the smallest subarray that must be
// removed in order to maximise the GCD
function GetMinSubarrayLength(a, n)
{

    // Store the maximum possible
    // GCD of the resulting subarray
    var ans = Math.max(a[0], a[n - 1]);

    // Two pointers initially pointing
    // to the first and last element
    // respectively
    var lo = 0, hi = n - 1;

    // Moving the left pointer to the
    // right if the elements are
    // divisible by the maximum GCD
    while (lo < n && a[lo] % ans == 0)
        lo++;

    // Moving the right pointer to the
    // left if the elements are
    // divisible by the maximum GCD
    while (hi > lo && a[hi] % ans == 0)
        hi--;

    // Return the length of
    // the subarray
    return (hi - lo + 1);
}

// Driver code
var arr = [4, 8, 2, 1, 4 ];
var N = arr.length;
var length = GetMinSubarrayLength(arr, N);
document.write( length );

// This code is contributed by itsok.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)