# 阵列中的最小反转因子

> 原文:[https://www . geesforgeks . org/最小反相阵列因子/](https://www.geeksforgeeks.org/minimum-inverting-factor-in-an-array/)

给定一个 n 个正整数的数组，任务是找到给定数组中的最小反转因子。
**反转因子**定义为任意两个数字的反转的绝对差 arr <sub>i</sub> 和 arr <sub>j</sub> 其中 I！= j.
**注**:反转数字时应忽略尾随零，即反转时 1200 变为 21。
**举例:**

> **输入** : arr[] = { 56，20，47，93，45 }
> **输出** : 9
> 这对(56，47)中最小反相因子为 9。
> **输入** : arr[] = { 26，15，45，150 }
> **输出** : 0
> 该对(15，150)的最小反相因子为 0。

[Recommended: Please solve it on “*<u>PRACTICE</u>*” first, before moving on to the solution.](https://practice.geeksforgeeks.org/problems/the-inverting-factor/0)

一种简单的方法是迭代两个循环来找到所有可能的对。分别反转这两个数字，找出它们的绝对差值。在每一步更新反相因子(最小绝对差)。时间复杂度为 0(T2 2)。
一种有效的方法是预先计算每个数组元素的逆序，并只以逆序的形式存储它(也考虑尾随零的情况)。现在，要找到最小反转因子，请按非递减顺序对数组进行排序。因为数组是排序的，所以最小绝对差总是出现在任何两个相邻的数字之间。
以下是上述方法的实施。

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum inverting factor
int findMinimumInvertingFactor(int arr[], int N)
{
    // ans stores the minimum inverting factor
    int ans = INT_MAX;

    // Iterate over the loop and convert each
    // array element into its reversed form
    for (int i = 0; i < N; i++) {
        string s;
        int num = arr[i];

        // Extract each digit of the number and
        // store it in reverse order
        while (num > 0) {
            s.push_back(num % 10 + '0');
            num /= 10;
        }

        // Find the position upto which trailing
        // zeroes occur
        int pos;
        for (pos = 0; pos < s.size(); pos++)
            if (s[pos] != 0)
                break;

        // Form the reversed number
        num = 0;
        for (int j = pos; j < s.size(); j++)
            num = num * 10 + (s[j] - '0');
        arr[i] = num;
    }
    sort(arr, arr + N);

    // Consider all adjacent pairs and update the
    // answer accordingly
    for (int i = 1; i < N; i++)
        ans = min(ans, abs(arr[i] - arr[i - 1]));

    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 56, 20, 47, 93, 45 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << findMinimumInvertingFactor(arr, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function to find the minimum inverting factor
static int findMinimumInvertingFactor(int arr[], int N)
{
    // ans stores the minimum inverting factor
    int ans = Integer.MAX_VALUE;

    // Iterate over the loop and convert each
    // array element into its reversed form
    for (int i = 0; i < N; i++)
    {
        String s = "";
        int num = arr[i];

        // Extract each digit of the number and
        // store it in reverse order
        while (num > 0)
        {
            s+=(char)((num % 10) + '0');
            num /= 10;
        }

        // Find the position upto which trailing
        // zeroes occur
        int pos;
        for (pos = 0; pos < s.length(); pos++)
            if (s.charAt(pos) != 0)
                break;

        // Form the reversed number
        num = 0;
        for (int j = pos; j < s.length(); j++)
            num = num * 10 + (s.charAt(j) - '0');
        arr[i] = num;
    }
    Arrays.sort(arr);

    // Consider all adjacent pairs and update the
    // answer accordingly
    for (int i = 1; i < N; i++)
        ans = Math.min(ans, Math.abs(arr[i] - arr[i - 1]));

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 56, 20, 47, 93, 45 };
    int N = arr.length;

    System.out.println(findMinimumInvertingFactor(arr, N));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

import sys

# Function to find the minimum inverting factor
def findMinimumInvertingFactor(arr, N) :

    # ans stores the minimum inverting factor
    ans = sys.maxsize

    # Iterate over the loop and convert each
    # array element into its reversed form
    for i in range(N) :
        num = arr[i]
        s = ""

        # Extract each digit of the number and
        # store it in reverse order
        while (num > 0) :
            s += str(num % 10)
            num //= 10

        # Find the position upto which trailing
        # zeroes occur
        for pos in range(len(s)) :
            if (s[pos] != "0") :
                break;

        # Form the reversed number
        num = 0
        for j in range(pos, len(s)) :
            num = num * 10 + (ord(s[j]) - ord("0"))
        arr[i] = num

    arr.sort()
    # Consider all adjacent pairs and update the
    # answer accordingly
    for i in range(N) :
        ans = min(ans, abs(arr[i] - arr[i - 1]))

    return ans

# Driver Code
if __name__ == "__main__" :

    arr= [ 56, 20, 47, 93, 45 ]
    N = len(arr)

    print(findMinimumInvertingFactor(arr, N))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the minimum inverting factor
static int findMinimumInvertingFactor(int []arr, int N)
{
    // ans stores the minimum inverting factor
    int ans = int.MaxValue;

    // Iterate over the loop and convert each
    // array element into its reversed form
    for (int i = 0; i < N; i++)
    {
        String s = "";
        int num = arr[i];

        // Extract each digit of the number and
        // store it in reverse order
        while (num > 0)
        {
            s+=(char)((num % 10) + '0');
            num /= 10;
        }

        // Find the position upto which trailing
        // zeroes occur
        int pos;
        for (pos = 0; pos < s.Length;pos++)
            if (s[pos] != 0)
                break;

        // Form the reversed number
        num = 0;
        for (int j = pos; j < s.Length; j++)
            num = num * 10 + (s[j] - '0');
        arr[i] = num;
    }
    Array.Sort(arr);

    // Consider all adjacent pairs and update the
    // answer accordingly
    for (int i = 1; i < N; i++)
        ans = Math.Min(ans, Math.Abs(arr[i] - arr[i - 1]));

    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 56, 20, 47, 93, 45 };
    int N = arr.Length;

    Console.WriteLine(findMinimumInvertingFactor(arr, N));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find the minimum inverting factor
function findMinimumInvertingFactor($arr, $N)
{
    // ans stores the minimum inverting factor
    $ans = PHP_INT_MAX;

    // Iterate over the loop and convert each
    // array element into its reversed form
    for ($i = 0; $i < $N; $i++)
    {
        $s="";
        $num = $arr[$i];

        // Extract each digit of the number and
        // store it in reverse order
        while ($num > 0)
        {
            $s.=chr($num % 10 + ord('0'));
            $num =(int)($num/10);
        }

        // Find the position upto which trailing
        // zeroes occur
        for ($pos = 0; $pos < strlen($s); $pos++)
            if ($s[$pos] != 0)
                break;

        // Form the reversed number
        $num = 0;
        for ($j = $pos; $j < strlen($s); $j++)
            $num = $num * 10 + (ord($s[$j]) - ord('0'));
        $arr[$i] = $num;
    }
    sort($arr);

    // Consider all adjacent pairs and update the
    // answer accordingly
    for ($i = 1; $i < $N; $i++)
        $ans = min($ans, abs($arr[$i] - $arr[$i - 1]));

    return $ans;
}

// Driver Code

$arr = array( 56, 20, 47, 93, 45 );
$N = count($arr);

echo findMinimumInvertingFactor($arr, $N)."\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to find the minimum inverting factor
    function findMinimumInvertingFactor(arr, N)
    {

        // ans stores the minimum inverting factor
        let ans = Number.MAX_VALUE;

        // Iterate over the loop and convert each
        // array element into its reversed form
        for (let i = 0; i < N; i++)
        {
            let s = "";
            let num = arr[i];

            // Extract each digit of the number and
            // store it in reverse order
            while (num > 0)
            {
                s+=String.fromCharCode((num % 10) + '0'.charCodeAt());
                num = parseInt(num / 10, 10);
            }

            // Find the position upto which trailing
            // zeroes occur
            let pos;
            for (pos = 0; pos < s.length;pos++)
                if (s[pos] != 0)
                    break;

            // Form the reversed number
            num = 0;
            for (let j = pos; j < s.length; j++)
                num = num * 10 + (s[j].charCodeAt() - '0'.charCodeAt());
            arr[i] = num;
        }
        arr.sort(function(a, b){return a - b});

        // Consider all adjacent pairs and update the
        // answer accordingly
        for (let i = 1; i < N; i++)
            ans = Math.min(ans, Math.abs(arr[i] - arr[i - 1]));

        return ans;
    }

    let arr = [ 56, 20, 47, 93, 45 ];
    let N = arr.length;

    document.write(findMinimumInvertingFactor(arr, N));

    // This code is contributed by decode2207.
</script>
```

**Output:** 

```
9
```

**时间复杂度** : O(N * logN)