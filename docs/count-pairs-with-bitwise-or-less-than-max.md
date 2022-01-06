# 按位“或”小于“最大”的计数对

> 原文:[https://www . geesforgeks . org/count-pairs-with-bitwise-or-小于-max/](https://www.geeksforgeeks.org/count-pairs-with-bitwise-or-less-than-max/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是对索引对 **(i，j)** 进行计数，使得 **0 ≤ i < j ≤ N** 和 **arr[i] | arr[j] ≤ max(arr[i]，arr[j])** ，其中 **|** 是按位“或”。
**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 2
> (1，3)和(2，3)是唯一有效的对。
> **输入:** arr[] = {11，45，12，14，5}
> **输出:** 3

**方法:**运行两个嵌套循环，并检查每个可能的对。如果**arr[I]| arr[j]<= max(arr[I]，arr[j])** ，则递增计数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of valid pairs
int countPairs(int arr[], int n)
{
    int cnt = 0;

    // Check all possible pairs
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            if ((arr[i] | arr[j]) <= max(arr[i], arr[j]))
                cnt++;

    return cnt;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

// Function to return the count of valid pairs
static int countPairs(int arr[], int n)
{
    int cnt = 0;

    // Check all possible pairs
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            if ((arr[i] | arr[j]) <= Math.max(arr[i], arr[j]))
                cnt++;

    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3 };
    int n = arr.length;
    System.out.println(countPairs(arr, n));
}
}

// This code is Contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the count
# of valid pairs
def countPairs(arr, n):
    cnt = 0

    # Check all possible pairs
    for i in range(n - 1):
        for j in range(i + 1, n, 1):
            if ((arr[i] | arr[j]) <= max(arr[i],
                                         arr[j])):
                cnt += 1

    return cnt

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3]
    n = len(arr)
    print(countPairs(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of valid pairs
static int countPairs(int []arr, int n)
{
    int cnt = 0;

    // Check all possible pairs
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            if ((arr[i] | arr[j]) <= Math.Max(arr[i], arr[j]))
                cnt++;

    return cnt;
}

// Driver code
static void Main()
{
    int []arr = { 1, 2, 3 };
    int n = arr.Length;
    Console.WriteLine(countPairs(arr, n));
}
}

// This code is Contributed by mits.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of valid pairs
function countPairs($arr, $n)
{
    $cnt = 0;

    // Check all possible pairs
    for ($i = 0; $i < $n - 1; $i++)
        for ($j = $i + 1; $j < $n; $j++)
            if (($arr[$i] |
                 $arr[$j]) <= max($arr[$i],
                                  $arr[$j]))
                $cnt++;

    return $cnt;
}

// Driver code
$arr = array(1, 2, 3);
$n = sizeof($arr);
echo countPairs($arr, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count of valid pairs
function countPairs(arr, n) {
    let cnt = 0;

    // Check all possible pairs
    for (let i = 0; i < n - 1; i++)
        for (let j = i + 1; j < n; j++)
            if ((arr[i] | arr[j]) <= Math.max(arr[i], arr[j]))
                cnt++;

    return cnt;
}

// Driver code

let arr = [1, 2, 3];
let n = arr.length;
document.write(countPairs(arr, n));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
2
```