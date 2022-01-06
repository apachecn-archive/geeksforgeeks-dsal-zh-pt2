# 计数满足给定条件的子集

> 原文:[https://www . geesforgeks . org/count-满足给定条件的子集/](https://www.geeksforgeeks.org/count-sub-sets-that-satisfy-the-given-condition/)

给定一个数组 **arr[]** 和一个整数 **x** ，任务是计算所有子集(单独)可被 **x** 整除的 **arr[]** 的子集数量。
**举例:**

> **输入:** arr[] = {2，4，3，7}，x = 2
> **输出:** 3
> 所有有效子集为{2}、{4}和{2，4}
> {2} = > 2 可被 2 整除
> {4} = > 4 可被 2 整除
> {2，4} = > 2，4 和 6 均可被 2 整除
> **输入:**

**方法:**要选择所有子集之和可被 **x** 整除的子集，该子集的所有元素必须可被 **x** 整除。所以，

*   计算数组中可被 **x** 整除的所有元素，并将它们存储在变量 **count** 中。
*   现在，满足条件的所有可能子集将是 **2 <sup>计数</sup>–1**

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to return the count of the required sub-sets
ll count(int arr[], int n, int x)
{

    // Every element is divisible by 1
    if (x == 1) {
        ll ans = pow(2, n) - 1;
        return ans;
    }

    // Count of elements which are divisible by x
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] % x == 0)
            count++;
    }

    ll ans = pow(2, count) - 1;
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 3, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 1;
    cout << count(arr, n, x) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class solution
{

// Function to return the count of the required sub-sets
static long count(int arr[], int n, int x)
{

    // Every element is divisible by 1
    if (x == 1) {
        long ans = (long)Math.pow(2, n) - 1;
        return ans;
    }

    // Count of elements which are divisible by x
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] % x == 0)
            count++;
    }

    long ans = (long)Math.pow(2, count) - 1;
    return ans;
}

// Driver code
public static void main(String args[])
{
    int []arr = { 2, 4, 3, 5 };
    int n = arr.length;
    int x = 1;
    System.out.println(count(arr, n, x));
}
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# the required sub-sets
def count(arr, n, x) :

    # Every element is divisible by 1
    if (x == 1) :
        ans = pow(2, n) - 1
        return ans;

    # Count of elements which are
    # divisible by x
    count = 0
    for i in range(n) :
        if (arr[i] % x == 0) :
            count += 1

    ans = pow(2, count) - 1
    return ans

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 4, 3, 5 ]
    n = len(arr)
    x = 1
    print(count(arr, n, x))

# This code is contributed by Ryuga
```

## C#

```
//C# implementation of the approach

using System;

public class GFG{

// Function to return the count of the required sub-sets
static double count(int []arr, int n, int x)
{
    double ans=0;
    // Every element is divisible by 1
    if (x == 1) {
        ans = (Math.Pow(2, n) - 1);
        return ans;
    }

    // Count of elements which are divisible by x
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] % x == 0)
            count++;
    }

    ans = (Math.Pow(2, count) - 1);
    return ans;
}

// Driver code

    static public void Main (){

    int []arr = { 2, 4, 3, 5 };
    int n = arr.Length;
    int x = 1;
    Console.WriteLine(count(arr, n, x));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP  implementation of the approach

// Function to return the count of the required sub-sets
function count_t($arr, $n, $x)
{
    // Every element is divisible by 1
    if ($x == 1) {
    $ans = pow(2, $n) - 1;
        return $ans;
    }

    // Count of elements which are divisible by x
    $count = 0;
    for ($i = 0; $i < $n; $i++) {
        if ($arr[$i] % $x == 0)
            $count++;
    }

    $ans = pow(2, $count) - 1;
    return $ans;
}

// Driver code

    $arr = array( 2, 4, 3, 5 );
    $n = sizeof($arr) / sizeof($arr[0]);
    $x = 1;
    echo  count_t($arr, $n, $x);

#This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the count of
    // the required sub-sets
    function count(arr, n, x)
    {
        let ans=0;
        // Every element is divisible by 1
        if (x == 1) {
            ans = (Math.pow(2, n) - 1);
            return ans;
        }

        // Count of elements which are divisible by x
        let count = 0;
        for (let i = 0; i < n; i++) {
            if (arr[i] % x == 0)
                count++;
        }

        ans = (Math.pow(2, count) - 1);
        return ans;
    }

    let arr = [ 2, 4, 3, 5 ];
    let n = arr.length;
    let x = 1;
    document.write(count(arr, n, x));

</script>
```

**Output:** 

```
15
```