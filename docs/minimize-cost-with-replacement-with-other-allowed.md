# 用其他允许的替代物来降低成本

> 原文:[https://www . geeksforgeeks . org/最小化-允许用其他替换成本/](https://www.geeksforgeeks.org/minimize-cost-with-replacement-with-other-allowed/)

给定一个 n 个整数的数组，我们可以通过以下操作移除数组中的一个元素。
**操作:**我们选择数组的任意两个数字，去掉较大的数字，这个操作中的 Cost including 等于较小的数字。
你必须通过以最小的成本执行上述操作，将数组缩减为单个元素。
**例:**

> 输入:arr[] = {3 4}
> 输出:3
> 我们通过选择两个元素并支付等于较小的成本来移除 4。
> 输入:4 2 5
> 输出:4
> 我们先选 4，2，支付费用 2 去掉 4。然后我们通过再次支付成本 2 来移除 5。

因为我们必须将数组简化为单个元素，并且假设如果我们选择任意两个数字，那么移除较大数字的成本等于移除较小数字的成本。所以为了最小化总成本，我们总是用最小的数和其他数相加，这样总成本就是(n-1)*最小的数。

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// this function returns the minimum
// cost of the array
int getMinCost(int arr[], int n)
{
    int min_ele = *min_element(arr, arr+n);
    return min_ele * (n - 1);
}

int main()
{
    int arr[] = { 4, 2, 5 };
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << getMinCost(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.util.Collections;
import java.util.Arrays;

public class GfG {

    // This function returns the minimum
    // cost of the array
    public static int getMinCost(Integer arr[], int n)
    {
        int min_ele = Collections.min(Arrays.asList(arr));
        return min_ele * (n - 1);
    }

    // Driver code
    public static void main(String []args){

        Integer[] arr = { 4, 2, 5 };
        int n = arr.length;

        System.out.println(getMinCost(arr, n));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 Program for the above approach

# Function returns the minimum
# cost of the array
def getMinCost(arr, n):
    min_ele = min(arr)
    return min_ele * (n - 1)

# Driver Code
arr = [4, 2, 5]
n = len(arr)
print(getMinCost(arr, n))

# This code is contributed
# by Shrikant13
```

## C#

```
// C# Program for the above approach
using System;
using System.Linq;

class GfG
{

    // This function returns the minimum
    // cost of the array
    public static int getMinCost(int []arr, int n)
    {
        int min_ele = arr.Min();
        return min_ele * (n - 1);
    }

    // Driver code
    public static void Main(String []args)
    {
        int[] arr = { 4, 2, 5 };
        int n = arr.Length;

        Console.WriteLine(getMinCost(arr, n));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program for the above approach

// this function returns the minimum
// cost of the array
function  getMinCost($arr, $n)
{
     $min_ele = min($arr);
    return $min_ele * ($n - 1);
}
// Code driven
    $arr =array (4, 2, 5 );
     $n = sizeof($arr)/sizeof($arr[0]);
    echo  getMinCost($arr, $n);

#This code contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript Program for the above approach

    // This function returns the minimum
    // cost of the array
    function getMinCost(arr, n)
    {
        let min_ele = Number.MAX_VALUE;
        for(let i = 0; i < n; i++)
        {
            min_ele = Math.min(min_ele, arr[i]);
        }

        return min_ele * (n - 1);
    }

    let arr = [ 4, 2, 5 ];
    let n = arr.length;

    document.write(getMinCost(arr, n));

</script>
```

**Output:** 

```
4
```