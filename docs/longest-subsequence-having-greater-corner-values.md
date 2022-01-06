# 具有较大角值的最长子序列

> 原文:[https://www . geeksforgeeks . org/最长子序列具有较大的角值/](https://www.geeksforgeeks.org/longest-subsequence-having-greater-corner-values/)

给定包含第一个 **N** 自然数的随机排列的数组 **arr[]** ，任务是找到最长的子序列，该子序列具有第一个和最后一个元素大于所有其他子序列元素的属性。
**例:**

> **输入:** arr[] = {3，1，5，2，4}
> 输出: 4
> 子序列为{3，1，2，4}。这个子序列的角元素大于所有其他元素。
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 2
> 我们不能生成大小大于 2 的子序列。

**方法:**如果我们固定一个子序列最左边和最右边的元素，我们感兴趣的是计算它们之间有多少元素的值小于两者。这个想法的直接实现具有 O(N <sup>3</sup> 的复杂性。
为了降低复杂性，我们以不同的方式处理问题。我们不是固定子序列的末端，而是固定中间的元素。想法是，对于给定的 X (1 ≤ X ≤ N)，我们希望找到两个大于或等于 X 的元素，它们之间有尽可能多的小于 X 的元素。对于固定的 X，最好选择最左边和最右边的元素≤ X。现在我们有了一个更好的 O(N <sup>2</sup> )解。
随着 X 的增加，最左边的元素只能增加，最右边的元素只能减少。我们可以为它们中的每一个使用一个指针来得到一个摊销的复杂度 O(N)。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

#define MAXN 100005

// Function to return the length of the
// longest required sub-sequence
int longestSubSeq(int n, int arr [])
{
    int max_length = 0;

    // Create a position array to find
    // where an element is present
    int pos[MAXN];

    for (int i = 0; i < n; i++)
        pos[arr[i] - 1] = i;

    int left = n, right = 0;

    for (int i = n - 1, num = 1; i >= 0;
                       i -= 1, num += 1)
    {

        // Store the minimum position
        // to the left
        left = min(left, pos[i]);

        // Store the maximum position to
        // the right
        right = max(right, pos[i]);

        // Recompute current maximum
        max_length = max(max_length,
                         right - left - num + 3);
    }

    // Edge case when there is a single
    // element in the sequence
    if (n == 1)
        max_length = 1;

    return max_length;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << longestSubSeq(n, arr);
}

// This code is contributed by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    static int MAXN = (int)1e5 + 5;

    // Function to return the length of the
    // longest required sub-sequence
    static int longestSubSeq(int n, int[] arr)
    {
        int max_length = 0;

        // Create a position array to find
        // where an element is present
        int[] pos = new int[MAXN];

        for (int i = 0; i < n; i++)
            pos[arr[i] - 1] = i;

        int left = n, right = 0;

        for (int i = n - 1, num = 1; i >= 0;
                         i -= 1, num += 1) {

            // Store the minimum position
            // to the left
            left = Math.min(left, pos[i]);

            // Store the maximum position to
            // the right
            right = Math.max(right, pos[i]);

            // Recompute current maximum
            max_length = Math.max(max_length,
                      right - left - num + 3);
        }

        // Edge case when there is a single
        // element in the sequence
        if (n == 1)
            max_length = 1;

        return max_length;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5 };
        int n = arr.length;
        System.out.println(longestSubSeq(n, arr));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MAXN = 100005

# Function to return the length of the
# longest required sub-sequence
def longestSubSeq(n, arr):

    max_length = 0

    # Create a position array to find
    # where an element is present
    pos = [0] * MAXN

    for i in range (0, n):
        pos[arr[i] - 1] = i

    left = n
    right = 0
    num = 1

    for i in range (n - 1, -1, -1) :

        # Store the minimum position
        # to the left
        left = min(left, pos[i])

        # Store the maximum position to
        # the right
        right = max(right, pos[i])

        # Recompute current maximum
        max_length = max(max_length,
                right - left - num + 3)

        num = num + 1

    # Edge case when there is a single
    # element in the sequence
    if (n == 1) :
        max_length = 1

    return max_length

# Driver code
arr = [ 1, 2, 3, 4, 5 ]
n = len(arr)
print(longestSubSeq(n, arr))

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int MAXN = (int)1e5 + 5;

    // Function to return the length of the
    // longest required sub-sequence
    static int longestSubSeq(int n, int[] arr)
    {
        int max_length = 0;

        // Create a position array to find
        // where an element is present
        int[] pos = new int[MAXN];

        for (int i = 0; i < n; i++)
            pos[arr[i] - 1] = i;

        int left = n, right = 0;

        for (int i = n - 1, num = 1; i >= 0;
                        i -= 1, num += 1)
        {

            // Store the minimum position
            // to the left
            left = Math.Min(left, pos[i]);

            // Store the maximum position to
            // the right
            right = Math.Max(right, pos[i]);

            // Recompute current maximum
            max_length = Math.Max(max_length,
                    right - left - num + 3);
        }

        // Edge case when there is a single
        // element in the sequence
        if (n == 1)
            max_length = 1;

        return max_length;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 2, 3, 4, 5 };
        int n = arr.Length;
        Console.WriteLine(longestSubSeq(n, arr));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

$MAXN = 100005;

// Function to return the length of the
// longest required sub-sequence
function longestSubSeq($n, $arr)
{
    global $MAXN;
    $max_length = 0;

    // Create a position array to find
    // where an element is present
    $pos = array();

    for ($i = 0; $i < $n; $i++)
        $pos[$arr[$i] - 1] = $i;

    $left = $n;
    $right = 0;
    $num = 1;
    for ($i = $n - 1; $i >= 0 ; $i--, $num++)
    {

        // Store the minimum position
        // to the left
        $left = min($left, $pos[$i]);

        // Store the maximum position to
        // the right
        $right = max($right, $pos[$i]);

        // Recompute current maximum
        $max_length = max($max_length,
                          $right - $left - $num + 3);
    }

    // Edge case when there is a single
    // element in the sequence
    if ($n == 1)
        $max_length = 1;

    return $max_length;
}

// Driver code
$arr = array(1, 2, 3, 4, 5);
$n = sizeof($arr);
echo longestSubSeq($n, $arr);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    let MAXN = 1e5 + 5;

    // Function to return the length of the
    // longest required sub-sequence
    function longestSubSeq(n, arr)
    {
        let max_length = 0;

        // Create a position array to find
        // where an element is present
        let pos = new Array(MAXN);
        pos.fill(0);

        for (let i = 0; i < n; i++)
            pos[arr[i] - 1] = i;

        let left = n, right = 0;

        for (let i = n - 1, num = 1; i >= 0;
                        i -= 1, num += 1)
        {

            // Store the minimum position
            // to the left
            left = Math.min(left, pos[i]);

            // Store the maximum position to
            // the right
            right = Math.max(right, pos[i]);

            // Recompute current maximum
            max_length = Math.max(max_length,
                    right - left - num + 3);
        }

        // Edge case when there is a single
        // element in the sequence
        if (n == 1)
            max_length = 1;

        return max_length;
    }

    let arr = [ 1, 2, 3, 4, 5 ];
    let n = arr.length;
    document.write(longestSubSeq(n, arr));

</script>
```

**Output:** 

```
2
```