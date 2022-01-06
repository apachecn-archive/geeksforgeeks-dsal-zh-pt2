# 子阵列的最大长度，使得子阵列的总和为偶数

> 原文:[https://www . geeksforgeeks . org/子阵列最大长度-这样子阵列的总和就是偶数/](https://www.geeksforgeeks.org/maximum-length-of-subarray-such-that-sum-of-the-subarray-is-even/)

给定一个由 N 个元素组成的数组。任务是找到最长子阵列的长度，使得子阵列的和为偶数。
**例:**

```
Input : N = 6, arr[] = {1, 2, 3, 2, 1, 4}
Output : 5
Explanation: In the example the subarray 
in range [2, 6] has sum 12 which is even, 
so the length is 5.

Input : N = 4, arr[] = {1, 2, 3, 2}
Output : 4
```

**方法:**首先检查数组的总和是否为偶数。如果数组的总和是偶数，那么答案将是 N.
如果数组的总和不是偶数，则表示它是奇数。因此，我们的想法是从数组中找到一个奇数元素，这样排除该元素并比较数组两部分的长度，我们就可以得到具有偶数和的子数组的最大长度。
很明显，偶和的子阵会存在于[1，x]或[x，N]，
范围内，其中 1 < = x < = N，arr[x]为 ODD。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find length of the longest
// subarray such that sum of the
// subarray is even
int maxLength(int a[], int n)
{
    int sum = 0, len = 0;

    // Check if sum of complete array is even
    for (int i = 0; i < n; i++)
        sum += a[i];

    if (sum % 2 == 0) // total sum is already even
        return n;

    // Find an index i such the a[i] is odd
    // and compare length of both halfs excluding
    // a[i] to find max length subarray
    for (int i = 0; i < n; i++) {
        if (a[i] % 2 == 1)
            len = max(len, max(n - i - 1, i));
    }

    return len;
}

// Driver Code
int main()
{
    int a[] = { 1, 2, 3, 2 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << maxLength(a, n) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Function to find length of the longest
    // subarray such that sum of the
    // subarray is even
    static int maxLength(int a[], int n)
    {
        int sum = 0, len = 0;

        // Check if sum of complete array is even
        for (int i = 0; i < n; i++)
        {
            sum += a[i];
        }

        if (sum % 2 == 0) // total sum is already even
        {
            return n;
        }

        // Find an index i such the a[i] is odd
        // and compare length of both halfs excluding
        // a[i] to find max length subarray
        for (int i = 0; i < n; i++)
        {
            if (a[i] % 2 == 1)
            {
                len = Math.max(len, Math.max(n - i - 1, i));
            }
        }

        return len;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int a[] = {1, 2, 3, 2};
        int n = a.length;
        System.out.println(maxLength(a, n));

    }
}

// This code has been contributed by 29AjayKumar
```

## 计算机编程语言

```
# Python3 implementation of the above approach

# Function to find Length of the longest
# subarray such that Sum of the
# subarray is even
def maxLength(a, n):

    Sum = 0
    Len = 0

    # Check if Sum of complete array is even
    for i in range(n):
        Sum += a[i]

    if (Sum % 2 == 0): # total Sum is already even
        return n

    # Find an index i such the a[i] is odd
    # and compare Length of both halfs excluding
    # a[i] to find max Length subarray
    for i in range(n):
        if (a[i] % 2 == 1):
            Len = max(Len, max(n - i - 1, i))

    return Len

# Driver Code

a= [1, 2, 3, 2]
n = len(a)

print(maxLength(a, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to find length of the longest
    // subarray such that sum of the
    // subarray is even
    static int maxLength(int []a, int n)
    {
        int sum = 0, len = 0;

        // Check if sum of complete array is even
        for (int i = 0; i < n; i++)
        {
            sum += a[i];
        }

        if (sum % 2 == 0) // total sum is already even
        {
            return n;
        }

        // Find an index i such the a[i] is odd
        // and compare length of both halfs excluding
        // a[i] to find max length subarray
        for (int i = 0; i < n; i++)
        {
            if (a[i] % 2 == 1)
            {
                len = Math.Max(len, Math.Max(n - i - 1, i));
            }
        }

        return len;
    }

    // Driver Code
    static public void Main ()
    {
        int []a = {1, 2, 3, 2};
        int n = a.Length;
        Console.WriteLine(maxLength(a, n));

    }
}

// This code has been contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP implementation of the above approach

// Function to find length of the longest
// subarray such that sum of the
// subarray is even
function maxLength($a, $n)
{
    $sum = 0;
    $len = 0;

    // Check if sum of complete array is even
    for ($i = 0; $i < $n; $i++)
        $sum += $a[$i];

    if ($sum % 2 == 0) // total sum is already even
        return $n;

    // Find an index i such the a[i] is odd
    // and compare length of both halfs excluding
    // a[i] to find max length subarray
    for ($i = 0; $i < $n; $i++)
    {
        if ($a[$i] % 2 == 1)
            $len = max($len, $max($n - $i - 1, $i));
    }

    return $len;
}

// Driver Code
$a = array (1, 2, 3, 2 );
$n = count($a);

echo maxLength($a, $n) , "\n";

// This code is contributed by akt_mit.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find length of the longest
// subarray such that sum of the
// subarray is even
function maxLength(a, n)
{
    let sum = 0, len = 0;

    // Check if sum of complete array is even
    for (let i = 0; i < n; i++)
        sum += a[i];

    if (sum % 2 == 0) // total sum is already even
        return n;

    // Find an index i such the a[i] is odd
    // and compare length of both halfs excluding
    // a[i] to find max length subarray
    for (let i = 0; i < n; i++) {
        if (a[i] % 2 == 1)
            len = Math.max(len, Math.max(n - i - 1, i));
    }

    return len;
}

// Driver Code
    let a = [ 1, 2, 3, 2 ];
    let n = a.length;

    document.write(maxLength(a, n) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N)