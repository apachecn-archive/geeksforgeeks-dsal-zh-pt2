# 元素可被 k 整除的最长子阵列

> 原文:[https://www . geeksforgeeks . org/元素可被 k 整除的最长子数组/](https://www.geeksforgeeks.org/longest-subarray-with-elements-divisible-by-k/)

假设给定一个数组。你必须找到最长子阵列的长度，这样它的每一个元素都可以被 k 整除。
**示例:**

```
Input : arr[] = { 1, 7, 2, 6, 8, 100, 3, 6, 16}, k=2
Output : 4

Input : arr[] = { 3, 11, 22, 32, 55, 100, 1, 5}, k=5
Output : 2
```

**进场:**

*   用值 0 初始化两个变量 current_count 和 max _ count
*   从左到右迭代数组，用 k 检查每个元素的可除性。
*   如果元素是可分的，那么递增 current_count，否则使 current_count 等于 0
*   比较每个元素的当前计数和最大计数，如果当前计数大于最大计数，将当前计数的值赋给最大计数
*   最后，输出 max_count 的值

以下是上述方法的实现:

## C++

```
// C++ program of above approach
#include <bits/stdc++.h>
using namespace std;

// function to find longest subarray
int longestsubarray(int arr[], int n, int k)
{
    int current_count = 0;
    // this will contain length of longest subarray found
    int max_count = 0;

    for (int i = 0; i < n; i++) {
        if (arr[i] % k == 0)
            current_count++;
        else
            current_count = 0;
        max_count = max(current_count, max_count);
    }
    return max_count;
}

// Driver code
int main()
{
    int arr[] = { 2, 5, 11, 32, 64, 88 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 8;
    cout << longestsubarray(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program of above approach

import java.io.*;

class GFG {
    // function to find longest subarray
static int longestsubarray(int arr[],
                        int n, int k)
{
    int current_count = 0;

    // this will contain length of
    // longest subarray found
    int max_count = 0;

    for (int i = 0; i < n; i++)
    {
        if (arr[i] % k == 0)
            current_count++;
        else
            current_count = 0;
        max_count = Math.max(current_count,
                            max_count);
    }
    return max_count;
}

// Driver code
    public static void main (String[] args) {
int arr[] = { 2, 5, 11, 32, 64, 88 };
    int n = arr.length;
    int k = 8;
    System.out.println(longestsubarray(arr, n, k));
}
}

// This code is contributed
// by ajit
```

## 蟒蛇 3

```
# Python 3 program of above approach

# function to find longest subarray
def longestsubarray(arr, n, k):
    current_count = 0

    # this will contain length of
    # longest subarray found
    max_count = 0

    for i in range(0, n, 1):
        if (arr[i] % k == 0):
            current_count += 1
        else:
            current_count = 0
        max_count = max(current_count,
                            max_count)

    return max_count

# Driver code
if __name__ == '__main__':
    arr = [2, 5, 11, 32, 64, 88]    
    n = len(arr)
    k = 8
    print(longestsubarray(arr, n, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program of above approach
using System;

class GFG
{
// function to find longest subarray
static int longestsubarray(int[] arr,
                           int n, int k)
{
    int current_count = 0;

    // this will contain length of
    // longest subarray found
    int max_count = 0;

    for (int i = 0; i < n; i++)
    {
        if (arr[i] % k == 0)
            current_count++;
        else
            current_count = 0;
        max_count = Math.Max(current_count,
                             max_count);
    }
    return max_count;
}

// Driver code
public static void Main()
{
    int[] arr = { 2, 5, 11, 32, 64, 88 };
    int n = arr.Length;
    int k = 8;
    Console.Write(longestsubarray(arr, n, k));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program of above approach

// function to find longest subarray
function longestsubarray($arr, $n, $k)
{
    $current_count = 0;

    // This will contain length of
    // longest subarray found
    $max_count = 0;

    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] % $k == 0)
            $current_count++;
        else
            $current_count = 0;
        $max_count = max($current_count,
                         $max_count);
    }
    return $max_count;
}

// Driver code
$arr = array(2, 5, 11, 32, 64, 88 );
$n = sizeof($arr);
$k = 8;
echo longestsubarray($arr, $n, $k);

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>
    // Javascript program of above approach

    // function to find longest subarray
    function longestsubarray(arr, n, k)
    {
        let current_count = 0;
        // this will contain length of longest subarray found
        let max_count = 0;

        for (let i = 0; i < n; i++) {
            if (arr[i] % k == 0)
                current_count++;
            else
                current_count = 0;
            max_count = Math.max(current_count, max_count);
        }
        return max_count;
    }

    let arr = [ 2, 5, 11, 32, 64, 88 ];
    let n = arr.length;
    let k = 8;
    document.write(longestsubarray(arr, n, k));

</script>
```

**输出:**

```
3
```