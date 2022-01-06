# 产生相同和的最大对数

> 原文:[https://www . geeksforgeeks . org/产生相同总和的最大配对数/](https://www.geeksforgeeks.org/maximum-count-of-pairs-which-generate-the-same-sum/)

给定一个数组 **arr[]** ，任务是计算给出相同和的对的最大计数。
**例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 2
> (1，2) = 3
> (1，3) = 4
> (1，4)，(2 + 3) = 5
> (2，4) = 6
> (3，4) = 7
> **输入:** arr[] = {1，8，3，11，4，9，2，7}

**进场:**

1.  创建一个映射来存储每对总和的频率。
2.  遍历地图，找到最大频率。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// count of pairs with equal sum
int maxCountSameSUM(int arr[], int n)
{
    // Create a map to store frequency
    unordered_map<int, int> M;

    // Store counts of sum of all pairs
    // in the map
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            M[(arr[i] + arr[j])]++;

    int max_count = 0;

    // Find maximum count
    for (auto ele : M)
        if (max_count < ele.second)
            max_count = ele.second;

    return max_count;
}

// Driver code
int main()
{
    int arr[] = { 1, 8, 3, 11, 4, 9, 2, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxCountSameSUM(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

// return the max
static int Max(int arr[])
{
    int max = arr[0];
    for(int i = 1; i < arr.length; i++)
        if(arr[i] > max)max = arr[i];

    return max;
}

// Function to return the maximum
// count of pairs with equal sum
static int maxCountSameSUM(int arr[], int n)
{
    int maxi = Max(arr);

    // Create a map to store frequency
    int[] M = new int[2 * maxi + 1];

    for(int i = 0; i < M.length; i++)M[i] = 0;

    // Store counts of sum of all
    // pairs in the map
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            M[(arr[i] + arr[j])] += 1;

    int max_count = 0;

    // Find maximum count
    for (int i = 0; i < 2 * maxi; i++)
        if (max_count < M[i])
            max_count = M[i];

    return max_count;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 8, 3, 11, 4, 9, 2, 7 };
    int n = arr.length;
    System.out.print(maxCountSameSUM(arr, n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import defaultdict

# Function to return the maximum
# count of pairs with equal sum
def maxCountSameSUM(arr, n):

    # Create a map to store frequency
    M = defaultdict(lambda:0)

    # Store counts of sum of
    # all pairs in the map
    for i in range(0, n - 1):
        for j in range(i + 1, n):
            M[arr[i] + arr[j]] += 1

    max_count = 0

    # Find maximum count
    for ele in M:
        if max_count < M[ele]:
            max_count = M[ele]

    return max_count

# Driver code
if __name__ == "__main__":

    arr = [1, 8, 3, 11, 4, 9, 2, 7]
    n = len(arr)
    print(maxCountSameSUM(arr, n))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System.Linq;
using System;

class GFG
{

// Function to return the maximum
// count of pairs with equal sum
static int maxCountSameSUM(int []arr, int n)
{
    int maxi = arr.Max();

    // Create a map to store frequency
    int[] M = new int[2 * maxi + 1];

    // Store counts of sum of all
    // pairs in the map
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            M[(arr[i] + arr[j])] += 1;

    int max_count = 0;

    // Find maximum count
    for (int i = 0; i < 2 * maxi; i++)
        if (max_count < M[i])
            max_count = M[i];

    return max_count;
}

// Driver code
static void Main()
{
    int []arr = { 1, 8, 3, 11, 4, 9, 2, 7 };
    int n = arr.Length;
    Console.WriteLine(maxCountSameSUM(arr, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximum
// count of pairs with equal sum
function maxCountSameSUM($arr, $n)
{
    $maxi = max($arr);

    // Create a map to store frequency
    $M = array_fill(1, 2 * $maxi, 0);

    // Store counts of sum of all
    // pairs in the map
    for ($i = 0; $i < $n - 1; $i++)
        for ($j = $i + 1; $j < $n; $j++)
            $M[($arr[$i] + $arr[$j])] += 1;

    $max_count = 0;

    // Find maximum count
    for ($i = 0; $i < sizeof($M); $i++)
        if ($max_count < $M[$i])
            $max_count = $M[$i];

    return $max_count;
}

// Driver code
$arr = array( 1, 8, 3, 11, 4, 9, 2, 7 );
$n = sizeof($arr);
echo maxCountSameSUM($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum
// count of pairs with equal sum
function maxCountSameSUM(arr, n)
{
    // Create a map to store frequency
    var M = new Map();

    // Store counts of sum of all pairs
    // in the map
    for (var i = 0; i < n - 1; i++)
        for (var j = i + 1; j < n; j++)
        {
            if(M.has(arr[i] + arr[j]))
                M.set(arr[i] + arr[j], M.get(arr[i] + arr[j])+1)
            else   
                M.set(arr[i] + arr[j], 1);
        }

    var max_count = 0;

    // Find maximum count
    M.forEach((value, key) => {

        if (max_count < value)
            max_count = value;
    });

    return max_count;
}

// Driver code
var arr = [1, 8, 3, 11, 4, 9, 2, 7];
var n = arr.length;
document.write( maxCountSameSUM(arr, n));

</script>
```

**Output:** 

```
3
```