# 最长交替子阵列的长度

> 原文:[https://www . geesforgeks . org/最长交替子阵列长度/](https://www.geeksforgeeks.org/length-of-the-longest-alternating-subarray/)

给定一个只有正数和负数的数组。任务是找出阵列中最长的交替(意味着负-正-负或正-负-正)子阵列的长度。
**例:**

```
Input: a[] = {-5, -1, -1, 2, -2, -3}
Output: 3 
The subarray {-1, 2, -2} 

Input: a[] = {1, -5, 1, -5}
Output: 4 
```

**方法:**按照以下步骤解决问题:

*   最初将 cnt 初始化为 1。
*   迭代数组元素，检查它是否有替代符号。
*   如果有替代符号，将 cnt 增加 1。
*   如果它没有替代符号，则用 1 重新初始化 cnt。

以下是上述方法的实现:

## C++

```
// C++ program to find the longest alternating
// subarray in an array of N number
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest subarray
int longestAlternatingSubarray(int a[], int n)
{
    // Length of longest alternating
    int longest = 1;
    int cnt = 1;

    // Iterate in the array
    for (int i = 1; i < n; i++) {

        // Check for alternate
        if (a[i] * a[i - 1] < 0) {
            cnt++;
            longest = max(longest, cnt);
        }
        else
            cnt = 1;
    }
    return longest;
}

/* Driver program to test above functions*/
int main()
{
    int a[] = { -5, -1, -1, 2, -2, -3 };
    int n = sizeof(a) / sizeof(a[0]);

    // Function to find the longest subarray
    cout << longestAlternatingSubarray(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest alternating
// subarray in an array of N number
class GFG
{

    // Function to find the longest subarray
    static int longestAlternatingSubarray(int a[], int n)
    {
        // Length of longest alternating
        int longest = 1;
        int cnt = 1;

        // Iterate in the array
        for (int i = 1; i < n; i++)
        {

            // Check for alternate
            if (a[i] * a[i - 1] < 0)
            {
                cnt++;
                longest = Math.max(longest, cnt);
            }
            else
                cnt = 1;
        }
        return longest;
    }

    /* Driver program to test above functions*/
    public static void main (String[] args)
    {
        int a[] = { -5, -1, -1, 2, -2, -3 };
        int n = a.length ;

        // Function to find the longest subarray
        System.out.println(longestAlternatingSubarray(a, n));
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python3 program to find the longest alternating
# subarray in an array of N number

# Function to find the longest subarray
def longestAlternatingSubarray(a, n):

    # Length of longest alternating
    longest = 1
    cnt = 1

    # Iterate in the array
    i = 1
    while i < n:

        # Check for alternate
        if (a[i] * a[i - 1] < 0):
            cnt = cnt + 1
            longest = max(longest, cnt)

        else:
            cnt = 1
        i = i + 1

    return longest

# Driver Code
a = [ -5, -1, -1, 2, -2, -3 ]
n = len(a)

# Function to find the longest subarray
print(longestAlternatingSubarray(a, n))

# This code is contributed
# by shashank_sharma
```

## C#

```
// C# program to find the longest alternating
// subarray in an array of N number
using System;
class GFG
{

// Function to find the longest subarray
static int longestAlternatingSubarray(int []a,
                                      int n)
{
    // Length of longest alternating
    int longest = 1;
    int cnt = 1;

    // Iterate in the array
    for (int i = 1; i < n; i++)
    {

        // Check for alternate
        if (a[i] * a[i - 1] < 0)
        {
            cnt++;
            longest = Math.Max(longest, cnt);
        }
        else
            cnt = 1;
    }
    return longest;
}

// Driver Code
public static void Main()
{
    int []a = { -5, -1, -1, 2, -2, -3 };
    int n = a.Length;

    // Function to find the longest subarray
    Console.Write(longestAlternatingSubarray(a, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the longest alternating
// subarray in an array of N number

// Function to find the longest subarray
function longestAlternatingSubarray($a, $n)
{

    // Length of longest alternating
    $longest = 1;
    $cnt = 1;

    // Iterate in the array
    for ($i = 1; $i < $n; $i++)
    {

        // Check for alternate
        if ($a[$i] * $a[$i - 1] < 0)
        {
            $cnt++;
            $longest = max($longest, $cnt);
        }
        else
            $cnt = 1;
    }
    return $longest;
}

// Driver Code
$a = array(-5, -1, -1, 2, -2, -3 );
$n = sizeof($a);

// Function to find the longest subarray
echo longestAlternatingSubarray($a, $n);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>
// JavaScript program to find the longest alternating
// subarray in an array of N number

// Function to find the longest subarray
function longestAlternatingSubarray(a, n)
{

    // Length of longest alternating
    let longest = 1;
    let cnt = 1;

    // Iterate in the array
    for (let i = 1; i < n; i++) {

        // Check for alternate
        if (a[i] * a[i - 1] < 0) {
            cnt++;
            longest = Math.max(longest, cnt);
        }
        else
            cnt = 1;
    }
    return longest;
}

/* Driver program to test above functions*/
    let a = [ -5, -1, -1, 2, -2, -3 ];
    let n = a.length;

    // Function to find the longest subarray
    document.write(longestAlternatingSubarray(a, n));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)