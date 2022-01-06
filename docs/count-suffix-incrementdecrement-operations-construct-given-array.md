# 构造给定数组的后缀递增/递减操作的计数

> 原文:[https://www . geesforgeks . org/count-后缀-increment 减量-operations-construct-给定-array/](https://www.geeksforgeeks.org/count-suffix-incrementdecrement-operations-construct-given-array/)

给定一个非负整数数组。我们需要从全零的数组中构造给定的数组。我们被允许做以下操作。

*   选择任意一个索引，比如 I，给所有元素加 1，或者从索引 I 到最后一个索引的所有元素减 1。我们基本上是将后缀增加/减少 1。

**例:**

```
Input : brr[] = {1, 2, 3, 4, 5}
Output : 5
Here, we can successively choose indices 1, 2, 
3, 4, and 5, and add 1 to corresponding suffixes.

Input : brr[] = {1, 2, 2, 1}
Output : 3
Here, we choose indices 1 and 2 and adds 1 to 
corresponding suffixes, then we choose index 4 
and subtract 1.
```

设 **brr[]** 为给定数组， **arr[]** 为当前数组(初始为 0)。
方法很简单:

*   为了使第一个元素相等，我们必须进行|brr[1]|运算。一旦完成，arr[2]，arr[3]，arr[4]，… arr[n] = brr[1]。
*   为了使第二个元素相等，我们必须进行| brr[2]–brr[1]|运算。一旦完成，arr[3]，arr[4]，arr[5]，… arr[n] = brr[2]。

一般来说，要进行 arr[i] = brr[i]，我们需要进行| brr[I]–b[I–1]|操作。因此，总的来说，我们必须进行| b[1]|+| b[2]–b[1]|+| b[3]–b[2]|+…+| b[n]–b[n–1]|运算。
下面是上述方法的 CPP 和 Java 实现:

## C++

```
// CPP program to find minimum number of steps
// to make the array equal to the given array.
#include <bits/stdc++.h>
using namespace std;

// function to calculate min_Steps
int minSteps(int arr[], int n)
{
    int min_Steps = 0;
    for (int i = 0; i < n; i++) {
        if (i > 0)
            min_Steps += abs(arr[i] - arr[i - 1]);

        // first element of arr.
        else
            min_Steps += abs(arr[i]);
    }
    return min_Steps;
}

// driver function
int main()
{
    int arr[] = { 1, 2, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minSteps(arr, n) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number of steps
// to make the array equal to the given array.
import java.util.*;
import java.lang.*;

public class GfG {
    // function to calculate min_Steps
    public static int minSteps(int arr[], int n)
    {
        int min_Steps = 0;
        for (int i = 0; i < n; i++) {
            if (i > 0)
                min_Steps +=
                    Math.abs(arr[i] - arr[i - 1]);

            // first element of arr.
            else
                min_Steps += Math.abs(arr[i]);
        }
        return min_Steps;
    }

    // driver function
    public static void main(String argc[])
    {
        int[] arr = new int[] { 1, 2, 2, 1 };
        int n = 4;
        System.out.println(minSteps(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find minimum number
# of steps to make the array equal to the
# given array.

# function to calculate min_Steps
def minSteps(arr, n):
    min_Steps = 0
    for i in range(n):
        if (i > 0):
            min_Steps += abs(arr[i] -
                             arr[i - 1])

        # first element of arr.
        else:
            min_Steps += abs(arr[i])
    return min_Steps

# Driver Code
if __name__ == '__main__':
    arr = [ 1, 2, 2, 1 ]
    n = len(arr)
    print(minSteps(arr, n))

# This code is contributed
# by PrinciRaj19992
```

## C#

```
// C# program to find minimum number of steps
// to make the array equal to the given array.
using System;

public class GfG {

    // function to calculate min_Steps
    public static int minSteps(int[] arr, int n)
    {
        int min_Steps = 0;
        for (int i = 0; i < n; i++) {
            if (i > 0)
                min_Steps += Math.Abs(arr[i] - arr[i - 1]);

            // first element of arr.
            else
                min_Steps += Math.Abs(arr[i]);
        }
        return min_Steps;
    }

    // driver function
    public static void Main()
    {
        int[] arr = new int[] { 1, 2, 2, 1 };
        int n = 4;
        Console.WriteLine(minSteps(arr, n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// number of steps to make the
// array equal to the given array.

// function to calculate min_Steps
function minSteps($arr, $n)
{
    $min_Steps = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($i > 0)
            $min_Steps += abs($arr[$i] -
                              $arr[$i - 1]);

        // first element of arr.
        else
            $min_Steps += abs($arr[$i]);
    }
    return $min_Steps;
}

// Driver Code
$arr = array( 1, 2, 2, 1 );
$n = sizeof($arr) ;

echo minSteps($arr, $n),"\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to find minimum number of steps
    // to make the array equal to the given array.

    // function to calculate min_Steps
    function minSteps(arr, n)
    {
        let min_Steps = 0;
        for (let i = 0; i < n; i++) {
            if (i > 0)
                min_Steps += Math.abs(arr[i] - arr[i - 1]);

            // first element of arr.
            else
                min_Steps += Math.abs(arr[i]);
        }
        return min_Steps;
    }

    let arr = [ 1, 2, 2, 1 ];
    let n = arr.length;
    document.write(minSteps(arr, n));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
3
```

**时间复杂度** = O(n)。