# 最小数字 N，使得从 1 到 N 的所有数字的总设置位至少为-X

> 原文:[https://www . geeksforgeeks . org/最小数字-n-这样-从 1 到 n 的所有数字的总位数至少是-x/](https://www.geeksforgeeks.org/minimum-number-n-such-that-total-set-bits-of-all-numbers-from-1-to-n-is-at-least-x/)

给定一个数 X，任务是找到最小数 N，使得从 1 到 N 的所有数的总集合位至少为 X

**示例:**

```
Input: x = 5 
Output: 4 
Set bits in 1-> 1
Set bits in 2-> 1
Set bits in 3-> 2 
Set bits in 4-> 1 
Hence first four numbers add upto 5 

Input: x = 20 
Output: 11 
```

**方法:**使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)获得最小最大数，其[位之和直到 N](https://www.geeksforgeeks.org/count-total-set-bits-in-all-numbers-from-1-to-n/) 至少为 x。开始时，低为 0，高根据约束初始化。检查设置位的计数是否至少为 X，每次都将高电平变为中间 1，否则变为中间+1。每次我们做 high = mid-1，存储最小的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
#define INF 99999
#define size 10

// Function to count sum of set bits
// of all numbers till N
int getSetBitsFromOneToN(int N)
{
    int two = 2, ans = 0;
    int n = N;

    while (n) {
        ans += (N / two) * (two >> 1);

        if ((N & (two - 1)) > (two >> 1) - 1)
            ans += (N & (two - 1)) - (two >> 1) + 1;

        two <<= 1;
        n >>= 1;
    }
    return ans;
}

// Function to find the minimum number
int findMinimum(int x)
{
    int low = 0, high = 100000;

    int ans = high;

    // Binary search for the lowest number
    while (low <= high) {

        // Find mid number
        int mid = (low + high) >> 1;

        // Check if it is atleast x
        if (getSetBitsFromOneToN(mid) >= x) {
            ans = min(ans, mid);
            high = mid - 1;
        }
        else
            low = mid + 1;
    }

    return ans;
}

// Driver Code
int main()
{
    int x = 20;
    cout << findMinimum(x);

return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class solution
{
static int INF = 99999;
static int size = 10;

// Function to count sum of set bits
// of all numbers till N
static int getSetBitsFromOneToN(int N)
{
    int two = 2, ans = 0;
    int n = N;

    while (n!=0) {
        ans += (N / two) * (two >> 1);

        if ((N & (two - 1)) > (two >> 1) - 1)
            ans += (N & (two - 1)) - (two >> 1) + 1;

        two <<= 1;
        n >>= 1;
    }
    return ans;
}

// Function to find the minimum number
static int findMinimum(int x)
{
    int low = 0, high = 100000;

    int ans = high;

    // Binary search for the lowest number
    while (low <= high) {

        // Find mid number
        int mid = (low + high) >> 1;

        // Check if it is atleast x
        if (getSetBitsFromOneToN(mid) >= x) {
            ans = Math.min(ans, mid);
            high = mid - 1;
        }
        else
            low = mid + 1;
    }

    return ans;
}

// Driver Code
public static void main(String args[])
{
    int x = 20;
    System.out.println(findMinimum(x));

}

}

//This code is contributed by
// Shashank_Sharma
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach
INF = 99999
size = 10

# Function to count sum of set bits
# of all numbers till N
def getSetBitsFromOneToN(N):

    two, ans = 2, 0
    n = N

    while (n > 0):
        ans += (N // two) * (two >> 1)

        if ((N & (two - 1)) > (two >> 1) - 1):
            ans += (N & (two - 1)) - (two >> 1) + 1

        two <<= 1
        n >>= 1
    return ans

# Function to find the minimum number
def findMinimum(x):

    low = 0
    high = 100000

    ans = high

    # Binary search for the lowest number
    while (low <= high):

        # Find mid number
        mid = (low + high) >> 1

        # Check if it is atleast x
        if (getSetBitsFromOneToN(mid) >= x):

            ans = min(ans, mid)
            high = mid - 1
        else:
            low = mid + 1

    return ans

# Driver Code
x = 20
print(findMinimum(x))

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System ;

class solution
{
static int INF = 99999;
static int size = 10;

// Function to count sum of set bits
// of all numbers till N
static int getSetBitsFromOneToN(int N)
{
    int two = 2, ans = 0;
    int n = N;

    while (n!=0) {
        ans += (N / two) * (two >> 1);

        if ((N & (two - 1)) > (two >> 1) - 1)
            ans += (N & (two - 1)) - (two >> 1) + 1;

        two <<= 1;
        n >>= 1;
    }
    return ans;
}

// Function to find the minimum number
static int findMinimum(int x)
{
    int low = 0, high = 100000;

    int ans = high;

    // Binary search for the lowest number
    while (low <= high) {

        // Find mid number
        int mid = (low + high) >> 1;

        // Check if it is atleast x
        if (getSetBitsFromOneToN(mid) >= x) {
            ans = Math.Min(ans, mid);
            high = mid - 1;
        }
        else
            low = mid + 1;
    }

    return ans;
}

    // Driver Code
    public static void Main()
    {
        int x = 20;
        Console.WriteLine(findMinimum(x));

    }
    // This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to count sum of set bits
// of all numbers till N
function getSetBitsFromOneToN($N)
{
    $two = 2;
    $ans = 0;
    $n = $N;

    while ($n)
    {
        $ans += (int)($N / $two) * ($two >> 1);

        if (($N & ($two - 1)) > ($two >> 1) - 1)
            $ans += ($N & ($two - 1)) -
                          ($two >> 1) + 1;

        $two <<= 1;
        $n >>= 1;
    }
    return $ans;
}

// Function to find the minimum number
function findMinimum($x)
{
    $low = 0;
    $high = 100000;

    $ans = $high;

    // Binary search for the lowest number
    while ($low <= $high)
    {

        // Find mid number
        $mid = ($low + $high) >> 1;

        // Check if it is atleast x
        if (getSetBitsFromOneToN($mid) >= $x)
        {
            $ans = min($ans, $mid);
            $high = $mid - 1;
        }
        else
            $low = $mid + 1;
    }

    return $ans;
}

// Driver Code
$x = 20;
echo findMinimum($x);

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach
const INF = 99999;
const size = 10;

// Function to count sum of set bits
// of all numbers till N
function getSetBitsFromOneToN(N)
{
    let two = 2, ans = 0;
    let n = N;

    while (n)
    {
        ans += parseInt(N / two) * (two >> 1);

        if ((N & (two - 1)) > (two >> 1) - 1)
            ans += (N & (two - 1)) - (two >> 1) + 1;

        two <<= 1;
        n >>= 1;
    }
    return ans;
}

// Function to find the minimum number
function findMinimum(x)
{
    let low = 0, high = 100000;

    let ans = high;

    // Binary search for the lowest number
    while (low <= high)
    {

        // Find mid number
        let mid = (low + high) >> 1;

        // Check if it is atleast x
        if (getSetBitsFromOneToN(mid) >= x)
        {
            ans = Math.min(ans, mid);
            high = mid - 1;
        }
        else
            low = mid + 1;
    }
    return ans;
}

// Driver Code
let x = 20;

document.write(findMinimum(x));

// This code is contributed by subhammahato348

</script>
```

**Output:** 

```
11
```

**时间复杂度:** O(对数 N *对数 N)