# 通过移除任意一个元素获得的最大连续递减序列

> 原文:[https://www . geeksforgeeks . org/最大连续递减序列-通过移除任意一个元素获得/](https://www.geeksforgeeks.org/maximum-contiguous-decreasing-sequence-obtained-by-removing-any-one-element/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是找到连续严格递减序列的长度，该序列在从数组中最多移除一个元素 **arr[]** 后可以导出。
**示例**

> **输入:** arr[] = {8，7，3，5，2，9}
> **输出:** 4
> **解释:**
> 如果去掉 3，递减序列的最大长度为 4，序列为{8，7，5，2 }
> 如果去掉 5，递减序列的最大长度为 4，序列为{ 8，7，3，2 }
> 在两次去掉中，我们得到 4 作为最大长度。
> **输入:** arr[] = {1，2，9，8，3，7，6，4}
> **输出:** 5

**进场:**

*   创建两个数组，**左[]** 存储从左到右递减序列的长度，**右[]** 存储从右到左递减序列的长度。
*   遍历给定数组 **arr[]** 。
*   如果前一个元素( **arr[i-1]** )大于下一个元素(**arr[I+1]【T3])，则检查移除该元素是否会给出递减子序列的最大长度。**
*   更新递减子序列的最大长度。

以下是上述方法的实现:

## C++

```
// C++ program to find maximum length
// of decreasing sequence by removing
// at most one element
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum length
int maxLength(int* a, int n)
{
    // Initialise maximum length to 1
    int maximum = 1;

    // Initialise left[] to find the
    // length of decreasing sequence
    // from left to right
    int left[n];

    // Initialise right[] to find the
    // length of decreasing sequence
    // from right to left
    int right[n];

    // Initially store 1 at each index of
    // left and right array
    for (int i = 0; i < n; i++) {
        left[i] = 1;
        right[i] = 1;
    }

    // Iterate over the array arr[] to
    // store length of decreasing
    // sequence that can be obtained
    // at every index in the right array
    for (int i = n - 2; i >= 0; i--) {

        if (a[i] > a[i + 1]) {
            right[i] = right[i + 1] + 1;
        }

        // Store the length of longest
        // continuous decreasing
        // sequence in maximum
        maximum = max(maximum, right[i]);
    }

    // Iterate over the array arr[] to
    // store length of decreasing
    // sequence that can be obtained
    // at every index in the left array
    for (int i = 1; i < n; i++) {
        if (a[i] < a[i - 1]) {
            left[i] = left[i - 1] + 1;
        }
    }

    if (n > 2) {
        // Check if we can obtain a
        // longer decreasing sequence
        // after removal of any element
        // from the array arr[] with
        // the help of left[] & right[]
        for (int i = 1; i < n - 1; i++) {
            if (a[i - 1] > a[i + 1]) {
                maximum = max(maximum,
                              left[i - 1] + right[i + 1]);
            }
        }
    }

    // Return maximum length of sequence
    return maximum;
}

// Driver code
int main()
{
    int arr[6] = { 8, 7, 3, 5, 2, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function calling
    cout << maxLength(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum length
// of decreasing sequence by removing
// at most one element
class GFG {

    // Function to find the maximum length
    static int maxLength(int []a, int n)
    {
        // Initialise maximum length to 1
        int maximum = 1;

        // Initialise left[] to find the
        // length of decreasing sequence
        // from left to right
        int left [] = new int[n];

        // Initialise right[] to find the
        // length of decreasing sequence
        // from right to left
        int right[] = new int[n];

        // Initially store 1 at each index of
        // left and right array
        for (int i = 0; i < n; i++) {
            left[i] = 1;
            right[i] = 1;
        }

        // Iterate over the array arr[] to
        // store length of decreasing
        // sequence that can be obtained
        // at every index in the right array
        for (int i = n - 2; i >= 0; i--) {

            if (a[i] > a[i + 1]) {
                right[i] = right[i + 1] + 1;
            }

            // Store the length of longest
            // continuous decreasing
            // sequence in maximum
            maximum = Math.max(maximum, right[i]);
        }

        // Iterate over the array arr[] to
        // store length of decreasing
        // sequence that can be obtained
        // at every index in the left array
        for (int i = 1; i < n; i++) {
            if (a[i] < a[i - 1]) {
                left[i] = left[i - 1] + 1;
            }
        }

        if (n > 2) {
            // Check if we can obtain a
            // longer decreasing sequence
            // after removal of any element
            // from the array arr[] with
            // the help of left[] & right[]
            for (int i = 1; i < n - 1; i++) {
                if (a[i - 1] > a[i + 1]) {
                    maximum = Math.max(maximum, left[i - 1] + right[i + 1]);
                }
            }
        }

        // Return maximum length of sequence
        return maximum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 8, 7, 3, 5, 2, 9 };
        int n = arr.length;

        // Function calling
        System.out.println(maxLength(arr, n));
    }  
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find maximum length
# of decreasing sequence by removing
# at most one element

# Function to find the maximum length
def maxLength(a, n) :

    # Initialise maximum length to 1
    maximum = 1;

    # Initialise left[] to find the
    # length of decreasing sequence
    # from left to right
    left = [0]*n;

    # Initialise right[] to find the
    # length of decreasing sequence
    # from right to left
    right = [0]*n;

    # Initially store 1 at each index of
    # left and right array
    for i in range(n) :
        left[i] = 1;
        right[i] = 1;

    # Iterate over the array arr[] to
    # store length of decreasing
    # sequence that can be obtained
    # at every index in the right array
    for i in range(n - 2, -1, -1) :

        if (a[i] > a[i + 1]) :
            right[i] = right[i + 1] + 1;

        # Store the length of longest
        # continuous decreasing
        # sequence in maximum
        maximum = max(maximum, right[i]);

    # Iterate over the array arr[] to
    # store length of decreasing
    # sequence that can be obtained
    # at every index in the left array
    for i in range(1, n) :
        if (a[i] < a[i - 1]) :
            left[i] = left[i - 1] + 1;

    if (n > 2) :
        # Check if we can obtain a
        # longer decreasing sequence
        # after removal of any element
        # from the array arr[] with
        # the help of left[] & right[]
        for i in range(1, n -1) :
            if (a[i - 1] > a[i + 1]) :
                maximum = max(maximum, left[i - 1] + right[i + 1]);

    # Return maximum length of sequence
    return maximum;

# Driver code
if __name__ == "__main__" :

    arr = [ 8, 7, 3, 5, 2, 9 ];
    n = len(arr);

    # Function calling
    print(maxLength(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find maximum length
// of decreasing sequence by removing
// at most one element
using System;

class GFG {

    // Function to find the maximum length
    static int maxLength(int []a, int n)
    {
        // Initialise maximum length to 1
        int maximum = 1;

        // Initialise left[] to find the
        // length of decreasing sequence
        // from left to right
        int []left = new int[n];

        // Initialise right[] to find the
        // length of decreasing sequence
        // from right to left
        int []right = new int[n];

        // Initially store 1 at each index of
        // left and right array
        for (int i = 0; i < n; i++) {
            left[i] = 1;
            right[i] = 1;
        }

        // Iterate over the array arr[] to
        // store length of decreasing
        // sequence that can be obtained
        // at every index in the right array
        for (int i = n - 2; i >= 0; i--) {

            if (a[i] > a[i + 1]) {
                right[i] = right[i + 1] + 1;
            }

            // Store the length of longest
            // continuous decreasing
            // sequence in maximum
            maximum = Math.Max(maximum, right[i]);
        }

        // Iterate over the array arr[] to
        // store length of decreasing
        // sequence that can be obtained
        // at every index in the left array
        for (int i = 1; i < n; i++) {
            if (a[i] < a[i - 1]) {
                left[i] = left[i - 1] + 1;
            }
        }

        if (n > 2) {
            // Check if we can obtain a
            // longer decreasing sequence
            // after removal of any element
            // from the array arr[] with
            // the help of left[] & right[]
            for (int i = 1; i < n - 1; i++) {
                if (a[i - 1] > a[i + 1]) {
                    maximum = Math.Max(maximum, left[i - 1] + right[i + 1]);
                }
            }
        }

        // Return maximum length of sequence
        return maximum;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 8, 7, 3, 5, 2, 9 };
        int n = arr.Length;

        // Function calling
        Console.WriteLine(maxLength(arr, n));
    }  
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript program to find maximum length
// of decreasing sequence by removing
// at most one element

// Function to find the maximum length
function maxLength(a, n)
{
    // Initialise maximum length to 1
    let maximum = 1;

    // Initialise left[] to find the
    // length of decreasing sequence
    // from left to right
    let left = new Array(n);

    // Initialise right[] to find the
    // length of decreasing sequence
    // from right to left
    let right = new Array(n);

    // Initially store 1 at each index of
    // left and right array
    for (let i = 0; i < n; i++) {
        left[i] = 1;
        right[i] = 1;
    }

    // Iterate over the array arr[] to
    // store length of decreasing
    // sequence that can be obtained
    // at every index in the right array
    for (let i = n - 2; i >= 0; i--) {

        if (a[i] > a[i + 1]) {
            right[i] = right[i + 1] + 1;
        }

        // Store the length of longest
        // continuous decreasing
        // sequence in maximum
        maximum = Math.max(maximum, right[i]);
    }

    // Iterate over the array arr[] to
    // store length of decreasing
    // sequence that can be obtained
    // at every index in the left array
    for (let i = 1; i < n; i++) {
        if (a[i] < a[i - 1]) {
            left[i] = left[i - 1] + 1;
        }
    }

    if (n > 2) {
        // Check if we can obtain a
        // longer decreasing sequence
        // after removal of any element
        // from the array arr[] with
        // the help of left[] & right[]
        for (let i = 1; i < n - 1; i++) {
            if (a[i - 1] > a[i + 1]) {
                maximum = Math.max(maximum,
                            left[i - 1] + right[i + 1]);
            }
        }
    }

    // Return maximum length of sequence
    return maximum;
}

// Driver code

let arr = [ 8, 7, 3, 5, 2, 9 ];
let n = arr.length;

// Function calling
document.write(maxLength(arr, n) + "<br>");

// This code is contributed by gfgking
</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)